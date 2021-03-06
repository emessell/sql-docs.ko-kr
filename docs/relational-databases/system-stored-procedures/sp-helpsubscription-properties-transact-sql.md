---
description: sp_helpsubscription_properties(Transact-SQL)
title: sp_helpsubscription_properties (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpsubscription_properties
- sp_helpsubscription_properties_TSQL
helpviewer_keywords:
- sp_helpsubscription_properties
ms.assetid: 7a76a645-97eb-47ac-b3ea-e2d75012cbed
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4bcbd2ec90018561870d6159edb41105119ebc69
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547963"
---
# <a name="sp_helpsubscription_properties-transact-sql"></a>sp_helpsubscription_properties(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  [MSsubscription_properties](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md) 테이블에서 보안 정보를 검색 합니다. 이 저장 프로시저는 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpsubscription_properties [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db =] 'publisher_db' ]   
    [ , [ @publication =] 'publication' ]  
    [ , [ @publication_type = ] publication_type ]   
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'` 게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 **%** 모든 게시자에 대 한 정보를 반환 하는입니다.  
  
`[ @publisher_db = ] 'publisher_db'` 게시자 데이터베이스의 이름입니다. *publisher_db* 는 **sysname**이며 기본값은 **%** 모든 게시자 데이터베이스에 대 한 정보를 반환 하는입니다.  
  
`[ @publication = ] 'publication'` 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 **%** 모든 게시에 대 한 정보를 반환 하는입니다.  
  
`[ @publication_type = ] publication_type` 게시의 유형입니다. *publication_type* 은 **int**이며 기본값은 NULL입니다. 제공 된 경우 *publication_type* 는 다음 값 중 하나 여야 합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|트랜잭션 게시|  
|**1**|스냅샷 게시|  
|**2**|병합 게시|  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**발행자**|**sysname**|게시자의 이름입니다.|  
|**publisher_db**|**sysname**|게시자 데이터베이스의 이름입니다.|  
|**게시물**|**sysname**|게시의 이름입니다.|  
|**publication_type**|**int**|게시 유형입니다.<br /><br /> **0** = 트랜잭션<br /><br /> **1** = 스냅숏<br /><br /> **2** = 병합|  
|**publisher_login**|**sysname**|게시자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증에 사용되는 로그인 ID입니다.|  
|**publisher_password**|**nvarchar (524)**|게시자에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증에 사용하는 암호입니다(암호화됨).|  
|**publisher_security_mode**|**int**|게시자에서 사용하는 보안 모드입니다.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증<br /><br /> **1** = Windows 인증|  
|**총판**|**sysname**|배포자의 이름입니다.|  
|**distributor_login**|**sysname**|배포자 로그인입니다.|  
|**distributor_password**|**nvarchar (524)**|배포자 암호입니다(암호화됨).|  
|**distributor_security_mode**|**int**|배포자에서 사용하는 보안 모드입니다.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증<br /><br /> **1** = Windows 인증|  
|**ftp_address**|**sysname**|이전 버전과의 호환성을 위해서만 지원됩니다. 배포자용 FTP(파일 전송 프로토콜) 서비스의 네트워크 주소입니다.|  
|**ftp_port**|**int**|이전 버전과의 호환성을 위해서만 지원됩니다. 배포자용 FTP 서비스의 포트 번호입니다.|  
|**ftp_login**|**sysname**|이전 버전과의 호환성을 위해서만 지원됩니다. FTP 서비스에 연결하는 데 필요한 사용자 이름입니다.|  
|**ftp_password**|**nvarchar (524)**|이전 버전과의 호환성을 위해서만 지원됩니다. FTP 서비스에 연결하는 데 필요한 사용자 암호입니다.|  
|**alt_snapshot_folder**|**nvarchar(255)**|스냅샷의 대체 폴더 위치를 지정합니다.|  
|**working_directory**|**nvarchar(255)**|데이터 및 스키마 파일을 저장하는 데 사용하는 작업 디렉터리의 이름입니다.|  
|**use_ftp**|**bit**|일반 프로토콜 대신 FTP를 사용하여 스냅샷을 검색하도록 지정합니다. **1**인 경우 FTP를 사용 합니다.|  
|**dts_package_name**|**sysame**|DTS(데이터 변환 서비스) 패키지의 이름을 지정합니다.|  
|**dts_package_password**|**nvarchar (524)**|패키지의 암호를 지정합니다.|  
|**dts_package_location**|**int**|DTS 패키지가 저장된 위치입니다.<br /><br /> **0** = 배포자에 패키지 위치가 있습니다.<br /><br /> **1** = 패키지 위치가 구독자에 있습니다.|  
|**offload_agent**|**bit**|에이전트를 원격으로 활성화할 수 있는지 지정합니다. **0**인 경우 에이전트를 원격으로 활성화할 수 없습니다.|  
|**offload_server**|**sysname**|원격 활성화에 사용하는 서버의 네트워크 이름을 지정합니다.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|스냅샷 파일을 저장한 폴더의 경로를 지정합니다.|  
|**use_web_sync**|**bit**|HTTPS를 통해 구독을 동기화 할 수 있는지 여부를 지정 합니다. 여기서 값 **1** 은이 기능을 사용할 수 있음을 의미 합니다.|  
|**internet_url**|**nvarchar(260)**|웹 동기화를 위한 복제 수신기의 위치를 나타내는 URL입니다.|  
|**internet_login**|**nvarchar(128)**|기본 인증을 사용하여 웹 동기화를 호스팅하는 웹 서버에 연결할 때 병합 에이전트가 사용하는 로그인입니다.|  
|**internet_password**|**nvarchar (524)**|기본 인증을 사용하여 웹 동기화를 호스팅하는 웹 서버에 연결할 때 병합 에이전트가 사용하는 로그인 암호입니다.|  
|**internet_security_mode**|**int**|웹 동기화를 호스팅하는 웹 서버에 연결할 때 사용 되는 인증 모드입니다. 여기서 값 **1** 은 Windows 인증을 의미 하 고 **0** 은 기본 인증을 의미 합니다.|  
|**internet_timeout**|**int**|웹 동기화 요청이 만료되기 전까지의 시간(초)입니다.|  
|**hostname**|**nvarchar(128)**|WHERE 절 매개 변수가 있는 행 필터에서 HOST_NAME() 함수를 사용할 때 이 함수에 필요한 값을 지정합니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_helpsubscription_properties** 는 스냅숏 복제, 트랜잭션 복제 및 병합 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_helpsubscription_properties**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
