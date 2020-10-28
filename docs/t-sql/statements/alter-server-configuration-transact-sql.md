---
description: ALTER SERVER CONFIGURATION(Transact-SQL)
title: ALTER SERVER CONFIGURATION(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER SERVER CONFIGURATION
- ALTER_SERVER_CONFIGURATION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SERVER CONFIGURATION, ALTER
- process affinity, setting
- ALTER SERVER CONFIGURATION statement
- setting process affinity
ms.assetid: f3059e42-5f6f-4a64-903c-86dca212a4b4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d3381300671d2303f8766351e19018d8122c861f
ms.sourcegitcommit: bd3a135f061e4a49183bbebc7add41ab11872bae
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92300919"
---
# <a name="alter-server-configuration-transact-sql"></a>ALTER SERVER CONFIGURATION(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 현재 서버에 대한 전역 구성 설정을 수정합니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  

```syntaxsql
ALTER SERVER CONFIGURATION  
SET <optionspec>   
[;]  
  
<optionspec> ::=  
{  
     <process_affinity>  
   | <diagnostic_log>  
   | <failover_cluster_property>  
   | <hadr_cluster_context>  
   | <buffer_pool_extension>  
   | <soft_numa>  
   | <memory_optimized>
}  
  
<process_affinity> ::=   
   PROCESS AFFINITY   
   {  
     CPU = { AUTO | <CPU_range_spec> }   
   | NUMANODE = <NUMA_node_range_spec>   
   }  
   <CPU_range_spec> ::=   
      { CPU_ID | CPU_ID  TO CPU_ID } [ ,...n ]   
  
   <NUMA_node_range_spec> ::=   
      { NUMA_node_ID | NUMA_node_ID TO NUMA_node_ID } [ ,...n ]  
  
<diagnostic_log> ::=   
   DIAGNOSTICS LOG   
   {   
     ON    
   | OFF    
   | PATH = { 'os_file_path' | DEFAULT }    
   | MAX_SIZE = { 'log_max_size' MB | DEFAULT }    
   | MAX_FILES = { 'max_file_count' | DEFAULT }    
   }  
  
<failover_cluster_property> ::=   
   FAILOVER CLUSTER PROPERTY <resource_property>  
   <resource_property> ::=  
      {  
        VerboseLogging = { 'logging_detail' | DEFAULT }    
      | SqlDumperDumpFlags = { 'dump_file_type' | DEFAULT }  
      | SqlDumperDumpPath = { 'os_file_path'| DEFAULT }  
      | SqlDumperDumpTimeOut = { 'dump_time-out' | DEFAULT }  
      | FailureConditionLevel = { 'failure_condition_level' | DEFAULT }  
      | HealthCheckTimeout = { 'health_check_time-out' | DEFAULT }  
      }  
  
<hadr_cluster_context> ::=  
   HADR CLUSTER CONTEXT = { 'remote_windows_cluster' | LOCAL }  
  
<buffer_pool_extension>::=  
    BUFFER POOL EXTENSION   
    { ON ( FILENAME = 'os_file_path_and_name' , SIZE = <size_spec> )   
    | OFF }  
  
    <size_spec> ::=  
        { size [ KB | MB | GB ] }  
  
<soft_numa> ::=  
    SOFTNUMA  
    { ON | OFF }  

<memory-optimized> ::=   
   MEMORY_OPTIMIZED   
   {   
     ON 
   | OFF
   | [ TEMPDB_METADATA = { ON [(RESOURCE_POOL='resource_pool_name')] | OFF }
   | [ HYBRID_BUFFER_POOL = { ON | OFF }
   }  
```  
  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
**\<process_affinity> ::=**  
  
PROCESS  AFFINITY  
CPU와 연결할 하드웨어 스레드를 사용하도록 설정합니다.  
  
CPU = { AUTO | \<CPU_range_spec> }  
지정된 범위의 각 CPU에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 작업자 스레드를 분산시킵니다. 지정된 범위 밖의 CPU에는 스레드가 할당되지 않습니다.  
  
AUTO  
CPU에 스레드가 할당되지 않도록 지정합니다. 운영 체제에서 서버 작업에 따라 CPU  간에 스레드를 자유롭게 이동할 수 있습니다. 이 설정은 기본값이며 권장됩니다.  
  
\<CPU_range_spec> ::=  
스레드를 할당할 CPU  또는 CPU  범위를 지정합니다.  
  
{ CPU_ID | CPU_ID  TO  CPU_ID } [ ,...n ]  
하나 이상의 CPU를 포함하는 목록입니다. CPU ID는 0부터 시작하는 **정수** 값입니다.  
  
NUMANODE = \<NUMA_node_range_spec>  
지정된 NUMA  노드 또는 노드 범위에 속하는 모든 CPU에 스레드를 할당합니다.  
  
\<NUMA_node_range_spec> ::=  
NUMA  노드 또는 NUMA  노드의 범위를 지정합니다.  
  
{ NUMA_node_ID | NUMA_node_ID  TO NUMA_node_ID } [ ,...n ]  
하나 이상의 NUMA  노드를 포함하는 목록입니다. NUMA 노드 ID는 0부터 시작하는 **정수** 값입니다.  
  
**\<diagnostic_log> ::=**  
  
**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터)  

  
DIAGNOSTICS  LOG  
sp_server_diagnostics 프로시저가 캡처하는 로깅 진단 데이터를 시작하거나 중지합니다. 또한 이 인수는 로그 파일 롤오버 수, 로그 파일 크기 및 파일 위치 등의 SQLDIAG 로그 구성 매개 변수를 설정합니다. 자세한 내용은 [장애 조치(failover) 클러스터 인스턴스 진단 로그 보기 및 읽기](../../sql-server/failover-clusters/windows/view-and-read-failover-cluster-instance-diagnostics-log.md)를 참조하세요.  
  
켜기  
PATH  파일 옵션에 지정된 위치에서 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 진단 데이터 로깅을 시작합니다. 이 인수는 기본값입니다.  
  
OFF  
진단 데이터 로깅을 중지합니다.  
  
PATH  =  {  'os_file_path'  |  DEFAULT  }  
진단 로그의 위치를 나타내는 경로입니다. 기본 위치는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스의 설치 폴더 내에 있는 \<\MSSQL\Log>입니다.  
  
MAX_SIZE  =  {  'log_max_size'  MB  |  DEFAULT  }  
각 진단 로그가 증가할 수 있는 최대 크기(MB)입니다. 기본값은 100  MB입니다.  
  
MAX_FILES  =  {  'max_file_count'  |  DEFAULT  }  
새 진단 로그에 재활용하기 전에 컴퓨터에 저장할 수 있는 최대 진단 로그 파일 수입니다.  
  
**\<failover_cluster_property> ::=**  
  
**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터)    
  
FAILOVER  CLUSTER  PROPERTY  
SQL  Server  리소스의 프라이빗 장애 조치(failover)  클러스터 속성을 수정합니다.  
  
VERBOSE  LOGGING  =  {  'logging_detail'  |  DEFAULT  }  
SQL  Server  장애 조치(failover)  클러스터링에 대한 로깅 수준을 설정합니다. 이 속성을 설정하여 오류 로그에 문제 해결을 위한 자세한 정보를 추가할 수 있습니다.  
  
-   0 - 로깅이 해제됩니다(기본값).  
  
-   1  -  오류만 로깅됩니다.  
  
-   2 - 오류 및 경고가 로깅됩니다.  
  
리소스 장애 조치 시나리오에서, SQL Server 리소스 DLL은 장애 조치가 이루어지기 전에 덤프 파일을 가져올 수 있습니다. 이는 FCI 기술과 가용성 그룹 기술에 모두 적용됩니다. SQL Server 리소스가 실패한 것을 확인한 SQL Server 리소스 DLL은 Sqldumper.exe 유틸리티를 사용하여 SQL Server 프로세스의 덤프 파일을 가져옵니다. Sqldumper.exe 유틸리티가 리소스 장애 조치 시점에 덤프 파일을 성공적으로 생성하도록 하려면 SqlDumperDumpTimeOut, SqlDumperDumpPath, SqlDumperDumpFlags와 같은 세 가지 속성을 필수 구성 요소로 설정해야 합니다.

SQLDUMPEREDUMPFLAGS  
SQL  Server  SQLDumper  유틸리티에서 생성되는 덤프 파일의 형식을 결정합니다. 기본 설정은 0입니다. 이 설정에는 16진수 값이 아닌 10진수 값이 사용됩니다. 미니 덤프에는 288을 사용하고, 간접 메모리를 사용하는 미니 덤프에는 296을 사용하고, 필터링된 덤프에는 33024를 사용합니다. 자세한 내용은 [SQL Server Dumper 유틸리티 기술 자료 문서](https://go.microsoft.com/fwlink/?LinkId=206173)를 참조하세요.  
  
SQLDUMPERDUMPPATH  =  {  'os_file_path'  |  DEFAULT  }  
SQLDumper  유틸리티에서 덤프 파일을 저장하는 위치입니다. 자세한 내용은 [SQL Server Dumper 유틸리티 기술 자료 문서](https://go.microsoft.com/fwlink/?LinkId=206173)를 참조하세요.  
  
SQLDUMPERDUMPTIMEOUT  =  {  'dump_time-out'  |  DEFAULT  }  
SQL Server 오류가 발생할 경우 SQLDumper 유틸리티에서 덤프를 생성하기 위한 제한 시간 값(밀리초)입니다. 기본값은 0이며 이는 덤프를 완료하는 데 시간 제한이 없음을 의미합니다. 자세한 내용은 [SQL Server Dumper 유틸리티 기술 자료 문서](https://go.microsoft.com/fwlink/?LinkId=206173)를 참조하세요.  
  
 FAILURECONDITIONLEVEL  =  {  'failure_condition_level'  |  DEFAULT  }  
 SQL Server 장애 조치(failover) 클러스터 인스턴스가 장애 조치(failover)되거나 다시 시작되는 조건입니다. 기본값은 3이며, 이는 치명적인 서버 오류 시 SQL Server 리소스가 장애 조치(failover)되거나 다시 시작됨을 의미합니다. 이 오류 상태 및 기타 오류 상태 수준에 대한 자세한 내용은 [FailureConditionLevel 속성 설정 구성](../../sql-server/failover-clusters/windows/configure-failureconditionlevel-property-settings.md)을 참조하세요.  
  
HEALTHCHECKTIMEOUT  =  {  'health_check_time-out'  |  DEFAULT  }  
SQL  Server  데이터베이스 엔진 리소스 DLL이 SQL  Server  인스턴스가 응답하지 않는 것으로 간주하기 전에 서버 상태 정보를 기다려야 하는 제한 시간 값입니다. 제한 시간 값은 밀리초로 표시됩니다. 기본값은 60,000밀리초(60초)입니다.  
  
**\<hadr_cluster_context> ::=**  
  
**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터)   
  
HADR CLUSTER CONTEXT **=** { **‘** _remote\_windows\_cluster_ **’** | LOCAL }  
서버 인스턴스의 HADR 클러스터 컨텍스트를 지정된 WSFC(Windows Server 장애 조치(Failover) 클러스터)로 전환합니다. *HADR 클러스터 컨텍스트* 는 서버 인스턴스에서 호스팅하는 가용성 복제본에 대한 메타데이터를 관리하는 WSFC를 결정합니다. 새 WSFC에서 [!INCLUDE[ssSQL11SP1](../../includes/sssql11sp1-md.md)] 또는 상위 버전 인스턴스로 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]의 클러스터 간 마이그레이션을 수행하는 동안에만 SET HADR CLUSTER CONTEXT 옵션을 사용합니다.  
  
HADR 클러스터 컨텍스트는 로컬 WSFC에서 원격 WSFC로 전환한 다음, 다시 원격 WSFC에서 로컬 WSFC로만 전환할 수 있습니다. HADR 클러스터 컨텍스트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 가용성 복제본을 호스트하지 않을 때만 원격 클러스터로 전환할 수 있습니다.  
  
원격 HADR 클러스터 컨텍스트는 언제든지 로컬 클러스터로 다시 전환할 수 있습니다. 그러나 서버 인스턴스에서 가용성 복제본을 호스트하는 동안에는 컨텍스트를 다시 전환할 수 없습니다. 
  
대상 클러스터를 식별하려면 다음 값 중 하나를 지정합니다.  
  
*windows_cluster*  
WSFC의 네트워크 이름입니다. 짧은 이름 또는 전체 도메인 이름을 지정할 수 있습니다. 짧은 이름의 대상 IP  주소를 찾기 위해 ALTER  SERVER  CONFIGURATION은 DNS  확인을 사용합니다. 경우에 따라 짧은 이름을 사용하면 혼동이 생길 수 있고 DNS에서 잘못된 IP 주소를 반환할 수 있습니다. 전체 도메인 이름을 지정하는 것이 좋습니다.  
  
> [!NOTE] 
> 이 설정을 사용하는 클러스터 간 마이그레이션을 더 이상 지원하지 않습니다. 클러스터 간 마이그레이션을 수행하려면 분산 가용성 그룹 또는 로그 전달 등 일부 다른 메서드를 사용합니다. 
  
LOCAL  
로컬 WSFC입니다.  
  
자세한 내용은 [서버 인스턴스의 HADR 클러스터 컨텍스트 변경&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/change-the-hadr-cluster-context-of-server-instance-sql-server.md)을 참조하세요.  
  
**\<buffer_pool_extension>::=**  
  
**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터)    
  
켜기  
버퍼 풀 확장 옵션을 설정합니다. 이 옵션은 비휘발성 스토리지를 사용해서 버퍼 풀 크기를 확장합니다. SSD(반도체 드라이브)와 같은 비휘발성 스토리지는 무결한 데이터 페이지를 풀에 저장합니다. 이 기능에 대한 자세한 내용은 [버퍼 풀 확장](../../database-engine/configure-windows/buffer-pool-extension.md)을 참조하세요. 모든 SQL Server 버전에서 버퍼 풀 확장을 사용할 수 있는 것은 아닙니다. 자세한 내용은 [SQL Server 2016의 버전과 지원하는 기능](../../sql-server/editions-and-components-of-sql-server-2016.md)을 참조하세요.  
  
FILENAME = 'os_file_path_and_name'  
버퍼 풀 확장 캐시 파일의 디렉터리 경로 및 이름을 정의합니다. 파일 확장명은 .BPE로 지정해야 합니다. FILENAME을 수정하기 전에 BUFFER POOL EXTENSION을 끕니다.  
  
SIZE = *size* [ **KB** | MB | GB ]  
캐시 크기를 정의합니다. 기본 크기 사양은 KB입니다. 최소 크기는 최대 서버 메모리 크기입니다. 최대 한도는 최대 서버 메모리 크기의 32배입니다. 최대 서버 메모리에 대한 자세한 내용은 [sp_configure&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)를 참조하세요.  
  
파일 크기를 수정하기 전에 BUFFER POOL EXTENSION을 끕니다. 현재 크기보다 크기를 작게 지정하려면 SQL Server의 인스턴스를 다시 시작하여 메모리를 재확보해야 합니다. 그렇지 않으면, 지정된 크기가 현재 크기보다 크거나 같아야 합니다.  
  
OFF  
버퍼 풀 확장 옵션을 해제합니다. 파일 크기 또는 이름과 같은 연관된 매개 변수를 수정하려면 먼저 버퍼 풀 확장 옵션을 사용하지 않도록 설정합니다. 이 옵션이 해제되었으면 모든 관련 구성 정보가 레지스트리에서 제거됩니다.  
  
> [!WARNING]  
>  버퍼 풀 확장을 해제하면 버퍼 풀 크기가 크게 줄어들어 서버 성능에 부정적인 영향을 줄 수 있습니다.  
  
**\<soft_numa>**  

**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터)  
  
켜기  
큰 NUMA 하드웨어 노드를 더 작은 NUMA 노드로 분할하도록 자동 분할을 사용합니다. 실행 중인 값을 변경하려면 데이터베이스 엔진을 다시 시작해야 합니다.  
  
OFF  
큰 NUMA 하드웨어 노드를 작은 NUMA 노드로 분할하는 자동 소프트웨어를 사용하지 않도록 설정합니다. 실행 중인 값을 변경하려면 데이터베이스 엔진을 다시 시작해야 합니다.  

> [!WARNING]
> SQL Server 에이전트 및 SOFT NUMA 옵션을 사용한 ALTER SERVER CONFIGURATION 문의 동작에는 알려진 문제가 있습니다.  다음은 권장되는 작업 순서입니다.  
> 1) SQL Server 에이전트 인스턴스를 중지합니다.  
> 2) ALTER SERVER CONFIGURATION SOFT NUMA 옵션을 실행합니다.  
> 3) SQL Server 인스턴스를 다시 시작합니다.  
> 4) SQL Server 에이전트 인스턴스를 시작합니다.  
  
**추가 정보:** SQL Server 서비스가 다시 시작되기 전에 SET SOFTNUMA 명령으로 ALTER SERVER CONFIGURATION을 실행하는 경우 SQL Server 에이전트 서비스가 중지되면, SOFTNUMA 설정을 ALTER SERVER CONFIGURATION 이전의 상태로 되돌리는 T-SQL RECONFIGURE 명령이 실행됩니다. 

**\<memory_optimized> ::=**

**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터)

켜기 <br>
[IMDB](../../relational-databases/in-memory-database.md) 기능군의 일부인 모든 인스턴스 수준 기능을 사용합니다. 이는 현재 [메모리 최적화 tempdb 메타데이터](../../relational-databases/databases/tempdb-database.md#memory-optimized-tempdb-metadata) 및 [하이브리드 버퍼 풀](../../database-engine/configure-windows/hybrid-buffer-pool.md)을 포함합니다. 적용하려면 다시 시작해야 합니다.

OFF <br>
IMDB 기능군의 일부인 모든 인스턴스 수준 기능을 사용하지 않습니다. 적용하려면 다시 시작해야 합니다.

TEMPDB_METADATA = ON | OFF <br>
메모리 최적화 tempdb 메타데이터만 사용하거나 사용하지 않습니다. 적용하려면 다시 시작해야 합니다. 

RESOURCE_POOL='resource_pool_name' <br>
TEMPDB_METADATA = ON과 결합할 경우 tempdb에 사용해야 하는 사용자 정의 리소스 풀을 지정합니다. 지정하지 않은 경우 tempdb는 기본 풀을 사용합니다. 풀이 이미 존재해야 합니다. 서비스가 다시 시작될 때 풀이 사용할 수 없는 경우 tempdb는 기본 풀을 사용합니다.


HYBRID_BUFFER_POOL = ON | OFF <br>
인스턴스 수준에서 하이브리드 버퍼 풀을 사용하거나 사용하지 않습니다. 적용하려면 다시 시작해야 합니다.


## <a name="general-remarks"></a>일반적인 주의 사항  
이 문은 별도로 명시하지 않는 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 다시 시작할 필요가 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover) 클러스터 인스턴스의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클러스터 리소스를 다시 시작할 필요가 없습니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
이 문은 DDL 트리거를 지원하지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
다음이 필요합니다.
- 프로세스 선호도 옵션에 대한 `ALTER SETTINGS` 권한.
- 장애 조치(Failover) 클러스터 속성 옵션에 대한 `ALTER SETTINGS` 및 `VIEW SERVER STATE` 권한.
- HADR 클러스터 컨텍스트 옵션에 대한 `CONTROL SERVER` 권한.  
- 버퍼 풀 확장 옵션에 대한 `ALTER SERVER STATE` 권한.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)] 리소스 DLL은 로컬 시스템 계정으로 실행됩니다. 따라서 로컬 시스템 계정에는 진단 로그 옵션의 지정된 경로에 대한 읽기 및 쓰기 권한이 있어야 합니다.  
  
## <a name="examples"></a>예제  
  
|범주|중요한 구문 요소|  
|--------------|------------------------------|  
|[프로세스 선호도 설정](#Affinity)|CPU  • NUMANODE  • AUTO|  
|[진단 로그 옵션 설정](#Diagnostic)|ON  • OFF  • PATH  • MAX_SIZE|  
|[장애 조치(failover) 클러스터 속성 설정](#Failover)|HealthCheckTimeout|  
|[가용성 복제본의 클러스터 컨텍스트 변경](#ChangeClusterContextExample)|**'** *windows_cluster* **'**|  
|[버퍼 풀 확장 설정](#BufferPoolExtension)|BUFFER POOL EXTENSION| 
|[IMDB 옵션 설정](#MemoryOptimized)|MEMORY_OPTIMIZED|

  
###  <a name="setting-process-affinity"></a><a name="Affinity"></a> 프로세스 선호도 설정  
이 섹션의 예에서는 CPU  및 NUMA  노드에 대한 프로세스 선호도를 설정하는 방법을 보여 줍니다. 이 예에서는 서버에 각각 16  NUMA  노드를 가진 4개 그룹으로 정렬된 256개의 CPU가 포함되어 있다고 가정합니다. 모든 NUMA 노드 또는 CPU에는 스레드가 할당되지 않습니다.  
  
-   그룹 0: 0~3개의 NUMA 노드, 0~63개의 CPU  
-   그룹 1: 4~7개의 NUMA 노드, 64~127개의 CPU  
-   그룹 2: 8~12개의 NUMA 노드, 128~191개의 CPU  
-   그룹 3: 13~16개의 NUMA 노드, 192~255개의 CPU  
  
#### <a name="a-setting-affinity-to-all-cpus-in-groups-0-and-2"></a>A. 그룹 0 및 2의 모든 CPU에 선호도 설정  
다음 예에서는 그룹 0  및 2의 모든 CPU에 선호도를 설정합니다.  
  
```sql  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY CPU=0 TO 63, 128 TO 191;  
```  
  
#### <a name="b-setting-affinity-to-all-cpus-in-numa-nodes-0-and-7"></a>B. NUMA 노드 0 및 7의 모든 CPU에 선호도 설정  
다음 예에서는 노드 `0` 및 `7`에만 CPU  선호도를 설정합니다.  
  
```sql  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY NUMANODE=0, 7;  
```  
  
#### <a name="c-setting-affinity-to-cpus-60-through-200"></a>C. CPU 60에서 200까지 선호도 설정  
다음 예에서는 CPU  60에서 200까지 선호도를 설정합니다.  
  
```sql  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY CPU=60 TO 200;  
```  
  
#### <a name="d-setting-affinity-to-cpu-0-on-a-system-that-has-two-cpus"></a>D. 두 개의 CPU가 있는 시스템에서 CPU 0에 선호도 설정  
다음 예에서는 두 개의 CPU가 있는 컴퓨터에서 `CPU=0`에 선호도를 설정합니다. 다음 문이 실행되기 전의 내부 선호도 비트 마스크는 00입니다.  
  
```sql  
ALTER SERVER CONFIGURATION SET PROCESS AFFINITY CPU=0;  
```  
  
#### <a name="e-setting-affinity-to-auto"></a>E. 선호도를 AUTO로 설정  
다음 예에서는 선호도를 `AUTO`로 설정합니다.  
  
```sql  
ALTER SERVER CONFIGURATION  
SET PROCESS AFFINITY CPU=AUTO;  
```  
  
###  <a name="setting-diagnostic-log-options"></a><a name="Diagnostic"></a> Setting diagnostic log options  
  
**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터)    
  
이 섹션의 예에서는 진단 로그 옵션 값을 설정하는 방법을 보여 줍니다.  
  
#### <a name="a-starting-diagnostic-logging"></a>A. 진단 로깅 시작  
다음 예에서는 진단 데이터의 로깅을 시작합니다.  
  
```sql  
ALTER SERVER CONFIGURATION SET DIAGNOSTICS LOG ON;  
```  
  
#### <a name="b-stopping-diagnostic-logging"></a>B. 진단 로깅 중지  
다음 예에서는 진단 데이터의 로깅을 중지합니다.  
  
```sql  
ALTER SERVER CONFIGURATION SET DIAGNOSTICS LOG OFF;  
```  
  
#### <a name="c-specifying-the-location-of-the-diagnostic-logs"></a>C. 진단 로그의 위치 지정  
다음 예에서는 진단 로그의 위치를 지정된 파일 경로로 설정합니다.  
  
```sql  
ALTER SERVER CONFIGURATION  
SET DIAGNOSTICS LOG PATH = 'C:\logs';  
```  
  
#### <a name="d-specifying-the-maximum-size-of-each-diagnostic-log"></a>D. 각 진단 로그의 최대 크기 지정  
다음 예에서는 각 진단 로그의 최대 크기를 10MB로 설정합니다.  
  
```sql  
ALTER SERVER CONFIGURATION   
SET DIAGNOSTICS LOG MAX_SIZE = 10 MB;  
```  
  
###  <a name="setting-failover-cluster-properties"></a><a name="Failover"></a> 장애 조치(failover) 클러스터 속성 설정  
  
**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터)   
  
다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 장애 조치(failover)  클러스터 리소스의 속성 값을 설정하는 방법을 보여 줍니다.  
  
#### <a name="a-specifying-the-value-for-the-healthchecktimeout-property"></a>A. HealthCheckTimeout 속성 값 지정  
다음 예에서는 `HealthCheckTimeout` 옵션을 15,000밀리초(15초)로 설정합니다.  
  
```sql  
ALTER SERVER CONFIGURATION   
SET FAILOVER CLUSTER PROPERTY HealthCheckTimeout = 15000;  
```  
  
###  <a name="b-changing-the-cluster-context-of-an-availability-replica"></a><a name="ChangeClusterContextExample"></a> 2. 가용성 복제본의 클러스터 컨텍스트 변경  
다음 예에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 HARD  클러스터 컨텍스트를 변경합니다. 이 예에서는 대상 WSFC  클러스터 `clus01`을 지정하기 위해 전체 클러스터 개체 이름 `clus01.xyz.com`을 지정합니다.  
  
```sql  
ALTER SERVER CONFIGURATION SET HADR CLUSTER CONTEXT = 'clus01.xyz.com';  
```  
  
### <a name="setting-buffer-pool-extension-options"></a>버퍼 풀 확장 옵션 설정  
  
####  <a name="a-setting-the-buffer-pool-extension-option"></a><a name="BufferPoolExtension"></a> 1. 버퍼 풀 확장 옵션 설정  
  
**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터)    
  
다음 예에서는 버퍼 풀 확장 옵션을 설정하고 파일 이름과 크기를 지정합니다.  
  
```sql  
ALTER SERVER CONFIGURATION   
SET BUFFER POOL EXTENSION ON  
    (FILENAME = 'F:\SSDCACHE\Example.BPE', SIZE = 50 GB);  
```  
  
#### <a name="b-modifying-buffer-pool-extension-parameters"></a>B. 버퍼 풀 확장 매개 변수 수정  
다음 예에서는 버퍼 풀 확장 파일의 크기를 수정합니다. 매개 변수를 수정하려면 먼저 버퍼 풀 확장 옵션을 해제해야 합니다.  
  
```sql  
ALTER SERVER CONFIGURATION   
SET BUFFER POOL EXTENSION OFF;  
GO  
EXEC sp_configure 'max server memory (MB)', 12000;  
GO  
RECONFIGURE;  
GO  
ALTER SERVER CONFIGURATION  
SET BUFFER POOL EXTENSION ON  
    (FILENAME = 'F:\SSDCACHE\Example.BPE', SIZE = 60 GB);  
GO   
```  

### <a name="setting-in-memory-database-options"></a><a name="MemoryOptimized"></a>IMDB 옵션 설정

**적용 대상** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]부터)

#### <a name="a-enable-all-in-memory-database-features-with-default-options"></a>A. 기본 옵션으로 모든 IMDB 기능 사용

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED ON;
GO
```

#### <a name="b-enable-memory-optimized-tempdb-metadata-using-the-default-resource-pool"></a>B. 기본 리소스 풀을 통해 메모리 최적화 tempdb 메타데이터 사용

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED TEMPDB_METADATA = ON;
GO
```

#### <a name="c-enable-memory-optimized-tempdb-metadata-with-a-user-defined-resource-pool"></a>C. 사용자 정의 리소스 풀을 통해 메모리 최적화 tempdb 메타데이터 사용

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED TEMPDB_METADATA = ON (RESOURCE_POOL = 'pool_name');
GO
```

#### <a name="d-enable-hybrid-buffer-pool"></a>D. 하이브리드 버퍼 풀 사용

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED HYBRID_BUFFER_POOL = ON;
GO
```

## <a name="see-also"></a>참고 항목  
[Soft-NUMA&#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)   
[서버 인스턴스의 HADR 클러스터 컨텍스트 변경&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/change-the-hadr-cluster-context-of-server-instance-sql-server.md)   
[sys.dm_os_schedulers&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md)   
[sys.dm_os_memory_nodes&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-nodes-transact-sql.md)   
[sys.dm_os_buffer_pool_extension_configuration&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-buffer-pool-extension-configuration-transact-sql.md)   
[버퍼 풀 확장](../../database-engine/configure-windows/buffer-pool-extension.md)  
  
