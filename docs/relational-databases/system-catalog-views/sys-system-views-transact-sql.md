---
description: sys.system_views(Transact-SQL)
title: sys.system_views (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.system_views_TSQL
- system_views
- system_views_TSQL
- sys.system_views
dev_langs:
- TSQL
helpviewer_keywords:
- sys.system_views catalog view
ms.assetid: a526c410-e7b5-4075-8103-e1f3c6837c3c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 45f2b39e809ac5df7ff2bb84d60d60d2cfec30dd
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545007"
---
# <a name="syssystem_views-transact-sql"></a>sys.system_views(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에 포함된 각 시스템 뷰당 한 개의 행을 포함합니다. 모든 시스템 뷰는 **sys** 또는 **INFORMATION_SCHEMA**이라는 스키마에 포함 되어 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|\<inherited columns>||이 뷰가 상속 하는 열 목록은 [sys. 개체 &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)를 참조 하세요.|  
|**is_replicated**|**bit**|1 = 뷰가 복제됩니다.|  
|**has_replication_filter**|**bit**|1 = 뷰에 복제 필터가 있습니다.|  
|**has_opaque_metadata**|**bit**|1 = 뷰에 VIEW_METADATA 옵션이 지정되었습니다. 자세한 내용은 [CREATE VIEW&#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)를 참조하세요.|  
|**has_unchecked_assembly_data**|**bit**|1 = 테이블은 마지막 ALTER ASSEMBLY를 수행하는 동안 정의가 변경된 어셈블리에 종속되어 있는 데이터를 포함합니다. 다음 번 DBCC CHECKDB 또는 DBCC CHECKTABLE이 성공적으로 수행된 후에 다시 0으로 설정됩니다.|  
|**with_check_option**|**bit**|1 = 뷰 정의에 WITH CHECK OPTION이 지정되었습니다.|  
|**is_date_correlation_view**|**bit**|1 = **datetime** 열 간의 상관 관계 정보를 저장 하기 위해 시스템에서 뷰를 자동으로 만들었습니다. DATE_CORRELATION_OPTIMIZATION을 ON으로 설정하여 이 뷰를 생성하도록 설정했습니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [DBCC CHECKDB &#40;Transact-sql&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)   
 [DBCC CHECKTABLE &#40;Transact-sql&#41;](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)   
 [ALTER ASSEMBLY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
  
