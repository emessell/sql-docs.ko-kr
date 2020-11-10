---
description: 의미 체계 검색을 사용하여 유사하거나 관련된 문서 찾기
title: 의미 체계 검색을 사용하여 유사하거나 관련된 문서 찾기
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], document similarity queries
ms.assetid: 9f527883-031b-442f-8e95-24bc0151ecbf
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.custom: seo-lt-2019
ms.openlocfilehash: b0df002c1d170061d6db8b6ee1ba53611e869603
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88498603"
---
# <a name="find-similar-and-related-documents-with-semantic-search"></a>의미 체계 검색을 사용하여 유사하거나 관련된 문서 찾기
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  통계적 의미 체계 인덱싱을 위해 구성된 열에서 유사하거나 관련된 문서 또는 텍스트 값을 찾고 유사하거나 연관된 정도에 관한 정보를 찾는 방법에 대해 설명합니다.  
   
##  <a name="find-similar-or-related-documents-with-semanticsimilaritytable"></a><a name="HowToQuerySimilar"></a> SEMANTICSIMILARITYTABLE을 사용하여 유사하거나 관련된 문서 찾기  
 특정 열에서 유사하거나 관련된 문서를 식별하려면 [semanticsimilaritytable&#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritytable-transact-sql.md) 함수를 쿼리합니다.  
  
 **SEMANTICSIMILARITYTABLE** 은 지정된 열의 내용이 지정된 문서와 의미상 유사한 0개 이상의 행으로 구성된 테이블을 반환합니다. SELECT 문의 FROM 절에서 이 행 집합 함수를 일반 테이블 이름처럼 참조할 수 있습니다.  
  
 유사한 문서의 열 간에는 쿼리할 수 없습니다. **SEMANTICSIMILARITYTABLE** 함수는 **source_key** 인수로 식별된 원본 열과 동일한 열에서만 결과를 검색합니다.  
  
 **SEMANTICSIMILARITYTABLE** 함수에 필요한 매개 변수와 반환되는 결과 테이블에 대한 자세한 내용은 [semanticsimilaritytable&#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritytable-transact-sql.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  대상 열에는 전체 텍스트 및 의미 체계 인덱싱이 사용하도록 설정되어 있어야 합니다.  
  
###  <a name="example-find-the-top-documents-that-are-similar-to-another-document"></a><a name="HowToIdentifySimilar"></a>예제: 다른 문서와 유사한 상위 문서 찾기  
 다음 예에서는 AdventureWorks2012 예제 데이터베이스의 HumanResources.JobCandidate 테이블에서 *\@CandidateID* 에 지정된 입사 지원자와 유사한 상위 10명의 입사 지원자를 검색합니다.  
  
```scr  
SELECT TOP(10) KEY_TBL.matched_document_key AS Candidate_ID  
FROM SEMANTICSIMILARITYTABLE  
    (  
    HumanResources.JobCandidate,  
    Resume,  
    @CandidateID  
    ) AS KEY_TBL  
ORDER BY KEY_TBL.score DESC;  
GO  
```  
  
##  <a name="find-info-about-how-documents-are-similar-or-related-with-semanticsimilaritydetailstable"></a><a name="HowToQuerySimilarity"></a>SEMANTICSIMILARITYDETAILSTABLE을 사용하여 문서가 유사하거나 연관된 정도에 대한 정보 찾기  
 문서 유사성 또는 연관성을 확인하는 키 구에 대한 정보를 가져오려면 [semanticsimilaritydetailstable&#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql.md) 함수를 쿼리합니다.  
  
 **SEMANTICSIMILARITYDETAILSTABLE** 은 의미상 유사한 내용의 두 문서(원본 문서 및 대응 문서) 간에 공통적인 키 구가 있는 0개 이상의 행으로 구성된 테이블을 반환합니다. SELECT 문의 FROM 절에서 이 행 집합 함수를 일반 테이블 이름처럼 참조할 수 있습니다.  
  
 **SEMANTICSIMILARITYDETAILSTABLE** 함수에 필요한 매개 변수와 반환되는 결과 테이블에 대한 자세한 내용은 [semanticsimilaritydetailstable&#40;Transact-SQL&#41;](../../relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  대상 열에는 전체 텍스트 및 의미 체계 인덱싱이 사용하도록 설정되어 있어야 합니다.  
  
###  <a name="example-find-the-top-key-phrases-that-are-similar-between-documents"></a><a name="HowToSimilarPhrases"></a> 예제: 문서 간에 유사한 상위 키 구 찾기  
 다음 예에서는 AdventureWorks2012 예제 데이터베이스의 **HumanResources.JobCandidate** 테이블에서 지정된 입사 지원자 간에 유사성 점수가 가장 높은 5개의 키 구를 검색합니다.  
  
```sql  
SELECT TOP(5) KEY_TBL.keyphrase, KEY_TBL.score  
FROM SEMANTICSIMILARITYDETAILSTABLE  
    (  
    HumanResources.JobCandidate,  
    Resume, @CandidateID,  
    Resume, @MatchedID  
    ) AS KEY_TBL  
ORDER BY KEY_TBL.score DESC;  
GO  
```  
  
  
