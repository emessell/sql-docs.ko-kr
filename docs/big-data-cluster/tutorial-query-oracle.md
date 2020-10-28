---
title: Oracle에서 외부 데이터 쿼리
titleSuffix: SQL Server big data clusters
description: 이 자습서에서는 SQL Server 2019 빅 데이터 클러스터에서 Oracle 데이터를 쿼리하는 방법을 보여줍니다. Oracle에서 데이터에 대해 외부 테이블을 만든 다음, 쿼리를 실행합니다.
author: MikeRayMSFT
ms.author: dacoelho
ms.reviewer: mikeray
ms.date: 10/01/2020
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 48d7fb0f41446fa54f1376a9a84f7dbff7017960
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196088"
---
# <a name="tutorial-query-oracle-from-sql-server-big-data-cluster"></a>자습서: SQL Server 빅 데이터 클러스터에서 Oracle 쿼리

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

이 자습서에서는 SQL Server 2019 빅 데이터 클러스터에서 Oracle 데이터를 쿼리하는 방법을 보여 줍니다. 이 자습서를 실행하려면 Oracle 서버에 대한 액세스 권한이 있어야 합니다. 외부 개체에 대한 읽기 권한이 있는 Oracle 사용자 계정이 필요합니다. Oracle 프록시 사용자 인증이 지원됩니다. 액세스 권한이 없는 경우 이 자습서를 통해 SQL Server 빅 데이터 클러스터에서 외부 데이터 원본에 대해 데이터 가상화가 작동하는 방식을 이해할 수 있습니다.

이 자습서에서는 다음 작업 방법을 알아봅니다.

> [!div class="checklist"]
> * 외부 Oracle 데이터베이스의 데이터에 대해 외부 테이블을 만듭니다.
> * 이 데이터를 마스터 인스턴스의 중요 데이터와 조인합니다.

> [!TIP]
> 원하는 경우 이 자습서의 명령을 위해 스크립트를 다운로드하여 실행할 수 있습니다. 자세한 내용은 GitHub의 [데이터 가상화 샘플](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-virtualization)을 참조하세요.

## <a name="prerequisites"></a><a id="prereqs"></a> 필수 조건

- [빅 데이터 도구](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 확장**
- [빅 데이터 클러스터에 샘플 데이터 로드](tutorial-load-sample-data.md)

## <a name="create-an-oracle-table"></a>Oracle 테이블 만들기

다음 단계는 Oracle에서 `INVENTORY`라는 예제 테이블을 만듭니다.

1. 이 자습서에서 사용하려는 Oracle 인스턴스 및 데이터베이스에 연결합니다.

1. 다음 문을 실행하여 `INVENTORY` 테이블을 만듭니다.

   ```sql
    CREATE TABLE "INVENTORY"
    (
        "INV_DATE" NUMBER(10,0) NOT NULL,
        "INV_ITEM" NUMBER(10,0) NOT NULL,
        "INV_WAREHOUSE" NUMBER(10,0) NOT NULL,
        "INV_QUANTITY_ON_HAND" NUMBER(10,0)
    );

    CREATE INDEX INV_ITEM ON HR.INVENTORY(INV_ITEM);
    ```

1. **inventory.csv** 파일의 내용을 이 테이블로 가져옵니다. 이 파일은 [필수 구성 요소](#prereqs) 섹션의 샘플 생성 스크립트에 의해 생성되었습니다.

## <a name="create-an-external-data-source"></a>외부 데이터 원본 만들기

첫 번째 단계는 Oracle 서버에 액세스할 수 있는 외부 데이터 원본을 만드는 것입니다.

1. Azure Data Studio에서 빅 데이터 클러스터의 SQL Server 마스터 인스턴스에 연결합니다. 자세한 내용은 [SQL Server 마스터 인스턴스에 연결](connect-to-big-data-cluster.md#master)을 참조하세요.

1. **서버** 창에서 연결을 두 번 클릭하여 SQL Server 마스터 인스턴스의 서버 대시보드를 표시합니다. **새 쿼리** 를 선택합니다.

   ![SQL Server 마스터 인스턴스 쿼리](./media/tutorial-query-oracle/sql-server-master-instance-query.png)

1. 다음 Transact-SQL 명령을 실행하여 마스터 인스턴스의 **Sales** 데이터베이스로 컨텍스트를 변경합니다.

   ```sql
   USE Sales
   GO
   ```

1. Oracle 서버에 연결하기 위한 데이터베이스 범위 자격 증명을 만듭니다. 다음 문에서 Oracle 서버에 적절한 자격 증명을 제공합니다.

   ```sql
   CREATE DATABASE SCOPED CREDENTIAL [OracleCredential]
   WITH IDENTITY = '<oracle_user,nvarchar(100),SYSTEM>', SECRET = '<oracle_user_password,nvarchar(100),manager>';
   ```

1. Oracle 서버를 가리키는 외부 데이터 원본을 만듭니다.

   ```sql
   CREATE EXTERNAL DATA SOURCE [OracleSalesSrvr]
   WITH (LOCATION = 'oracle://<oracle_server,nvarchar(100)>',CREDENTIAL = [OracleCredential]);
   ```

### <a name="optional-oracle-proxy-authentication"></a>선택 사항: Oracle 프록시 인증

Oracle은 프록시 인증을 지원하여 세부적인 액세스 제어를 제공합니다. 프록시 사용자는 해당 자격 증명을 사용하여 Oracle 데이터베이스에 연결하고 데이터베이스에서 다른 사용자를 가장합니다. 

가장된 사용자에 비해 제한된 액세스 권한을 갖도록 프록시 사용자를 구성할 수 있습니다. 예를 들어 프록시 사용자는 가장된 사용자의 특정 데이터베이스 역할을 사용하여 연결하도록 허용될 수 있습니다. 프록시 사용자를 통해 Oracle 데이터베이스에 연결하는 사용자의 ID는 여러 사용자가 프록시 인증을 사용하여 연결하는 경우에도 연결에서 유지됩니다. Oracle은 이를 통해 액세스 제어를 적용하고 실제 사용자를 대신하여 수행된 작업을 감사할 수 있습니다.

시나리오에서 Oracle 프록시 사용자를 사용해야 하는 경우 __위의 4단계 및 5 단계를 다음으로 바꿉니다__ .

4. Oracle 서버에 연결하기 위한 데이터베이스 범위 자격 증명을 만듭니다. 다음 문에서 Oracle 서버에 적절한 Oracle 프록시 사용자 자격 증명을 제공합니다.

   ```sql
   CREATE DATABASE SCOPED CREDENTIAL [OracleProxyCredential]
   WITH IDENTITY = '<oracle_proxy_user,nvarchar(100),SYSTEM>', SECRET = '<oracle_proxy_user_password,nvarchar(100),manager>';
   ```

5. Oracle 서버를 가리키는 외부 데이터 원본을 만듭니다.

   ```sql
   CREATE EXTERNAL DATA SOURCE [OracleSalesSrvr]
   WITH (LOCATION = 'oracle://<oracle_server,nvarchar(100)>',
   CONNECTION_OPTIONS = 'ImpersonateUser=% CURRENT_USER',
   CREDENTIAL = [OracleProxyCredential]);
   ```

## <a name="create-an-external-table"></a>외부 테이블 만들기

그런 다음, Oracle 서버의 `INVENTORY` 테이블에 **iventory_ora** 라는 외부 테이블을 만듭니다.

```sql
CREATE EXTERNAL TABLE [inventory_ora]
    ([inv_date] DECIMAL(10,0) NOT NULL, [inv_item] DECIMAL(10,0) NOT NULL,
    [inv_warehouse] DECIMAL(10,0) NOT NULL, [inv_quantity_on_hand] DECIMAL(10,0))
WITH (DATA_SOURCE=[OracleSalesSrvr],
        LOCATION='<oracle_service_name,nvarchar(30),xe>.<oracle_schema,nvarchar(128),HR>.<oracle_table,nvarchar(128),INVENTORY>');
```

> [!NOTE]
> Oracle에 대해 쿼리하는 동안 테이블 이름과 열 이름은 ANSI SQL의 따옴표 붙은 식별자를 사용합니다. 따라서 이름은 대/소문자를 구분합니다. Oracle 메타데이터에 있는 테이블 및 열 이름의 정확한 대/소문자와 일치하는 이름을 외부 테이블 정의에 지정하는 것이 중요합니다.

## <a name="query-the-data"></a>데이터 쿼리

다음 쿼리를 실행하여 `iventory_ora` 외부 테이블의 데이터를 로컬 `Sales` 데이터베이스의 테이블과 조인합니다.

```sql
SELECT TOP(100) w.w_warehouse_name, i.inv_item, SUM(i.inv_quantity_on_hand) as total_quantity
  FROM [inventory_ora] as i
  JOIN item as it
    ON it.i_item_sk = i.inv_item
  JOIN warehouse as w
    ON w.w_warehouse_sk = i.inv_warehouse
 WHERE it.i_category = 'Books' and i.inv_item BETWEEN 1 and 18000 --> get items within specific range
 GROUP BY w.w_warehouse_name, i.inv_item;
```

## <a name="clean-up"></a>정리

다음 명령을 사용하여 이 자습서에서 만든 데이터베이스 개체를 제거합니다.

```sql
DROP EXTERNAL TABLE [inventory_ora];
DROP EXTERNAL DATA SOURCE [OracleSalesSrvr] ;
DROP DATABASE SCOPED CREDENTIAL [OracleCredential];
```

## <a name="next-steps"></a>다음 단계

데이터 풀에 데이터를 수집하는 방법을 알아봅니다.
> [!div class="nextstepaction"]
> [데이터 풀에 데이터 로드](tutorial-data-pool-ingest-sql.md)
