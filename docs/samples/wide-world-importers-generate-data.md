---
title: SQL 샘플에서 데이터 생성 WideWorldImporters
description: 다음 SQL 문을 사용 하 여 WideWorldImporters 예제 데이터베이스에 대 한 현재 날짜로 샘플 데이터를 생성 하 고 가져옵니다.
ms.date: 10/23/2020
ms.reviewer: ''
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: f60ad250ea68f58a98fb93da9f3c5853ad68bd47
ms.sourcegitcommit: 67befbf7435f256e766bbce6c1de57799e1db9ad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/24/2020
ms.locfileid: "92523938"
---
# <a name="wideworldimporters-data-generation"></a>WideWorldImporters 데이터 생성
[!INCLUDE [SQL Server Azure SQL Database](../includes/applies-to-version/sql-asdb.md)]
WideWorldImporters 및 WideWorldImportersDW 데이터베이스의 릴리스 버전에는 데이터베이스가 생성 된 날부터 2013 년 1 월 1 일 까지의 데이터가 있습니다.

이러한 예제 데이터베이스를 사용 하는 경우 최신 샘플 데이터를 포함 하는 것이 좋습니다.

## <a name="data-generation-in-wideworldimporters"></a>WideWorldImporters의 데이터 생성

현재 날짜까지 샘플 데이터를 생성 하려면:

1. 아직 수행 하지 않은 경우 WideWorldImporters 데이터베이스의 정리 버전을 설치 합니다. 설치 지침은 [설치 및 구성](wide-world-importers-oltp-install-configure.md)을 참조 하세요.
2. 데이터베이스에서 다음 문을 실행 합니다.

    ```
        EXECUTE DataLoadSimulation.PopulateDataToCurrentDate
            @AverageNumberOfCustomerOrdersPerDay = 60,
            @SaturdayPercentageOfNormalWorkDay = 50,
            @SundayPercentageOfNormalWorkDay = 0,
            @IsSilentMode = 1,
            @AreDatesPrinted = 1;
    ```

    이 문은 예제 판매 및 구매 데이터를 데이터베이스에 현재 날짜로 추가 합니다. 일별 데이터 생성의 진행 상태를 표시 합니다. 데이터 생성의 임의 요소로 인해 실행 간에 생성 되는 데이터에는 약간의 차이가 있습니다.

    매일 주문에 대해 생성 되는 데이터의 양을 늘리거나 줄이려면 매개 변수의 값을 변경 `@AverageNumberOfCustomerOrdersPerDay` 합니다. 및 매개 변수를 사용 `@SaturdayPercentageOfNormalWorkDay` `@SundayPercentageOfNormalWorkDay` 하 여 주말의 주문 볼륨을 확인 합니다.

> [!TIP]
> 데이터베이스에서 [지연 된 내구성](../relational-databases/logs/control-transaction-durability.md) 을 강제 적용 하면 특히 데이터베이스 트랜잭션 로그가 대기 시간이 긴 저장소 하위 시스템에 있는 경우 데이터 생성 속도를 향상 시킬 수 있습니다. 지연 된 내구성을 사용 하는 경우 [데이터 손실](../relational-databases/logs/control-transaction-durability.md#bkmk_DataLoss) 가능성을 파악 하 고 데이터를 생성 하는 동안 지연 된 내 구성을 사용 하도록 설정 하는 것이 좋습니다.

## <a name="import-generated-data-in-wideworldimportersdw"></a>WideWorldImportersDW에서 생성 된 데이터 가져오기

WideWorldImportersDW OLAP 데이터베이스의 현재 날짜로 샘플 데이터를 가져오려면 다음을 수행 합니다.

1. 이전 섹션의 단계를 사용 하 여 WideWorldImporters OLTP 데이터베이스에서 데이터 생성 논리를 실행 합니다.
2. 아직 수행 하지 않은 경우 WideWorldImportersDW 데이터베이스의 정리 버전을 설치 합니다. 설치 지침은 [설치 및 구성](wide-world-importers-oltp-install-configure.md)을 참조 하세요.
3. 데이터베이스에서 다음 문을 실행 하 여 OLAP 데이터베이스의 초기값을 재설정 합니다.

    ```sql
    EXECUTE [Application].Configuration_ReseedETL
    ```

4. *.Ispac* SQL Server Integration Services 패키지를 실행 하 여 OLAP 데이터베이스로 데이터를 가져옵니다. ETL 작업을 실행 하는 방법을 알아보려면 [WIDEWORLDIMPORTERS etl 워크플로](wide-world-importers-perform-etl.md)를 참조 하세요.

## <a name="generate-data-in-wideworldimportersdw-for-performance-testing"></a>성능 테스트를 위해 WideWorldImportersDW에서 데이터 생성

WideWorldImportersDW는 성능 테스트를 위해 데이터 크기를 임의로 늘릴 수 있습니다. 예를 들어 클러스터형 columnstore 인덱싱에 사용할 데이터 크기를 늘릴 수 있습니다.

문제 중 하나는 다운로드 크기를 쉽게 다운로드할 수 있는 크기를 유지 하는 것입니다. 하지만 SQL Server 성능 기능을 보여 줄 수 있을 정도로 커야 합니다. 예를 들어 많은 수의 행으로 작업 하는 경우에만 columnstore 인덱스에 대 한 상당한 이점을 얻을 수 있습니다. 

프로시저를 사용 `Application.Configuration_PopulateLargeSaleTable` 하 여 테이블의 행 수를 늘릴 수 있습니다 `Fact.Sale` . 2012 년 1 월 2013 1 일에 시작 하는 기존 세계 넓은 가져오기 데이터와의 충돌을 방지 하기 위해 행이 달력 년에 삽입 됩니다.

### <a name="procedure-details"></a>프로시저 세부 정보

#### <a name="name"></a>이름

`Application.Configuration_PopulateLargeSaleTable`

#### <a name="parameters"></a>매개 변수

`@EstimatedRowsFor2012`**bigint** (기본값 1200만)

#### <a name="result"></a>결과

대략 필요한 행 수가 `Fact.Sale` 2012 년의 테이블에 삽입 됩니다. 프로시저는 매일 행 수를 5만로 제한 합니다. 이 제한을 변경할 수 있지만 이러한 제한을 통해 테이블의 실수로 인 한 overinflations 방지할 수 있습니다.

또한이 프로시저는 클러스터형 columnstore 인덱싱이 아직 적용 되지 않은 경우이를 적용 합니다.
