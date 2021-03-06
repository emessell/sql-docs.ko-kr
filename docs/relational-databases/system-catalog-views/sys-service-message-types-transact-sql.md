---
description: sys.service_message_types(Transact-SQL)
title: sys. service_message_types (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.service_message_types
- service_message_types
- sys.service_message_types_TSQL
- service_message_types_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_message_types catalog view
ms.assetid: 6a38709a-60fe-46f6-89da-718f74f15600
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3eaaa45f6f34e690b7b8abc3fc0366b54748b16c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550433"
---
# <a name="sysservice_message_types-transact-sql"></a>sys.service_message_types(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  이 카탈로그 뷰에는 Service Broker에 등록된 각 메시지 유형에 대한 행이 포함되어 있습니다.
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|데이터베이스 내에서 고유한 메시지 유형의 이름입니다. NULL을 허용하지 않습니다.|  
|**message_type_id**|**int**|데이터베이스 내에서 고유한 메시지 유형의 ID입니다. NULL을 허용하지 않습니다.|  
|**principal_id**|**int**|해당 메시지 유형을 소유하는 데이터베이스 보안 주체의 ID입니다. NULL을 허용합니다.|  
|**validation**|**char(2)**|해당 유형의 메시지를 보내기 전에 Service Broker가 수행하는 유효성 검사입니다. NULL을 허용하지 않습니다. 다음 중 하나:<br /><br /> N = 없음<br /><br /> X = XML<br /><br /> E = 비어 있음|  
|**validation_desc**|**nvarchar(60)**|해당 유형의 메시지를 보내기 전에 Service Broker가 수행하는 유효성 검사에 대한 설명입니다. NULL을 허용합니다. 다음 중 하나:<br /><br /> 없음<br /><br /> XML<br /><br /> EMPTY|  
|**xml_collection_id**|**int**|XML 스키마를 사용하는 유효성 검사의 경우 스키마 컬렉션의 ID를 사용합니다.<br /><br /> 그렇지 않으면 NULL입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
  
