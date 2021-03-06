---
title: Dwloader 데이터 형식 변환 규칙
description: 이 항목에서는 데이터를 PDW (병렬 데이터 웨어하우스)로 로드할 때 dwloader 명령줄 로더가 지 원하는 입력 데이터 형식 및 암시적 데이터 형식 변환에 대해 설명 합니다. "
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: c1ce48c3352ffbd0a1c112f7fd60db2f0d85c6e6
ms.sourcegitcommit: 197a6ffb643f93592edf9e90b04810a18be61133
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2020
ms.locfileid: "91379562"
---
# <a name="data-type-conversion-rules-for-dwloader---parallel-data-warehouse"></a>Dwloader-병렬 데이터 웨어하우스의 데이터 형식 변환 규칙
이 항목에서는 데이터를 PDW로 로드할 때 [dwloader 명령줄 로더가](dwloader.md) 지 원하는 입력 데이터 형식 및 암시적 데이터 형식 변환에 대해 설명 합니다. 암시적 데이터 변환은 입력 데이터가 SQL Server PDW 대상 테이블의 데이터 형식과 일치 하지 않는 경우에 발생 합니다. 로드 프로세스를 설계할 때이 정보를 사용 하 여 데이터가 성공적으로 SQL Server PDW 로드 되는지 확인 합니다.  
   
  
## <a name="inserting-literals-into-binary-types"></a><a name="InsertBinaryTypes"></a>이진 형식에 리터럴 삽입  
다음 표에서는 리터럴 값을 **binary** (*n*) 또는 **varbinary**(*n*) 형식의 SQL Server PDW 열로 로드 하기 위한 허용 되는 리터럴 형식, 형식 및 변환 규칙을 정의 합니다.  
  
|입력 데이터 형식|입력 데이터 예제|Binary 또는 varbinary 데이터 형식으로 변환|  
|-------------------|-----------------------|-----------------------------------------------|  
|이진 리터럴|0x *hexidecimal_string*<br /><br />예: 12Ef 또는 0x12Ef|0x 접두사는 선택 사항입니다.<br /><br />데이터 원본 길이가 데이터 형식에 대해 지정 된 바이트 수를 초과할 수 없습니다.<br /><br />데이터 원본 길이가 **이진** 데이터 형식의 크기 보다 작은 경우 데이터를 데이터 형식 크기에 도달 하는 0으로 오른쪽으로 채웁니다.|  
  
## <a name="inserting-literals-into-date-and-time-types"></a><a name="InsertDateTimeTypes"></a>날짜 및 시간 형식에 리터럴 삽입  
날짜 및 시간 리터럴은 작은따옴표로 묶인 특정 형식의 문자열 리터럴을 사용 하 여 표현 됩니다. 다음 표에서는 날짜 또는 시간 리터럴을 **datetime**, **smalldatetime**, **date**, **time**, **datetimeoffset**또는 **datetime2**형식의 열로 로드 하는 데 사용할 수 있는 리터럴 형식, 형식 및 변환 규칙을 정의 합니다. 테이블은 지정 된 데이터 형식에 대 한 기본 형식을 정의 합니다. 지정할 수 있는 다른 형식은 [날짜/시간 형식](#DateFormats)섹션에서 정의 됩니다. 날짜 및 시간 리터럴은 선행 또는 후행 공백을 포함할 수 없습니다. **date**, **smalldatetime**및 null 값은 고정 너비 모드로 로드할 수 없습니다.  
  
### <a name="datetime-data-type"></a>datetime 데이터 형식  
다음 표에서는 리터럴 값을 **datetime**형식의 열로 로드 하기 위한 기본 형식 및 규칙을 정의 합니다. 빈 문자열 (' ')은 기본값인 ' 1900-01-01 12:00:00.000 '로 변환 됩니다. 공백 (' ')만 포함 하는 문자열은 오류를 생성 합니다.  
  
|입력 데이터 형식|입력 데이터 예제|Datetime 데이터 형식으로 변환|  
|-------------------|-----------------------|------------------------------------|  
|**Datetime** 형식의 문자열 리터럴|' yyyy-MM-dd hh: MM: ss [.fff] '<br /><br />예: ' 2007-05-08 12:35:29.123 '|값이 삽입 될 때 누락 된 소수 자릿수는 0으로 설정 됩니다. 예를 들어 ' 2007-05-08 12:35 ' 리터럴은 ' 2007-05-08 12:35:00.000 '로 삽입 됩니다.|  
|**Smalldatetime** 형식의 문자열 리터럴|' yyyy-mm-dd hh: mm '<br /><br />예: ' 2007-05-08 12:35 '|값이 삽입 될 때 초와 남은 소수 자릿수는 0으로 설정 됩니다.|  
|**날짜** 형식의 문자열 리터럴|' yyyy-MM-dd '<br /><br />예: ' 2007-05-08 '|값이 삽입 될 때 시간 값 (시, 분, 초 및 소수 자릿수)은 12:00:00.000로 설정 됩니다.|  
|**Datetime2** 형식의 문자열 리터럴|' yyyy-MM-dd hh: MM: ss. fffffff '<br /><br />예: ' 2007-05-08 12:35:29.1234567 '|원본 데이터는 세 자리 수를 초과할 수 없습니다. 예를 들어 ' 2007-05-08 12:35:29.123 ' 리터럴은 삽입 되지만 값 ' 2007-05-8 12:35:29.1234567 '은 오류를 생성 합니다.|  
  
### <a name="smalldatetime-data-type"></a>smalldatetime 데이터 형식  
다음 표에서는 리터럴 값을 **smalldatetime**형식의 열로 로드 하기 위한 기본 형식 및 규칙을 정의 합니다. 빈 문자열 (' ')이 기본 값인 ' 1900-01-01 12:00 '로 변환 됩니다. 공백 (' ')만 포함 하는 문자열은 오류를 생성 합니다.  
  
|입력 데이터 형식|입력 데이터 예제|Smalldatetime 데이터 형식으로 변환|  
|-------------------|-----------------------|-----------------------------------------|  
|**Smalldatetime** 형식의 문자열 리터럴|' yyyy-MM-dd hh: mm ' 또는 ' yyyy-mm-dd hh: mm: ss '<br /><br />예: ' 2007-05-08 12:00 ' 또는 ' 2007-05-08 12:00:15 '|원본 데이터에는 연도, 월, 날짜, 시 및 분의 값이 있어야 합니다. 초는 선택 사항이 며, 있는 경우 값 00으로 설정 해야 합니다. 다른 값은 오류를 생성 합니다.<br /><br />초는 선택 사항입니다. Smalldatetime 열로 로드 하는 경우 dwloader는 초 및 소수 자릿수 초를 반올림 합니다. 예를 들어 1999-01-05 20:10:35.123는 01-05 20:11로 로드 됩니다.|  
|**날짜** 형식의 문자열 리터럴|' yyyy-MM-dd '<br /><br />예: ' 2007-05-08 '|값이 삽입 될 때 시간 값 (시, 분, 초 및 소수 자릿수)은 0으로 설정 됩니다.|  
  
### <a name="date-data-type"></a>date 데이터 형식  
다음 표에서는 **date**형식의 열에 리터럴 값을 로드 하기 위한 기본 형식 및 규칙을 정의 합니다. 빈 문자열 (' ')이 기본 값인 ' 1900-01-01 '로 변환 됩니다. 공백 (' ')만 포함 하는 문자열은 오류를 생성 합니다.  
  
|입력 데이터 형식|입력 데이터 예제|날짜 데이터 형식으로 변환|  
|-------------------|-----------------------|--------------------------------|  
|**날짜** 형식의 문자열 리터럴|' yyyy-MM-dd '<br /><br />예: ' 2007-05-08 '||  
  
### <a name="time-data-type"></a>time 데이터 형식  
다음 표에서는 리터럴 값을 **time**형식의 열로 로드 하기 위한 기본 형식 및 규칙을 정의 합니다. 빈 문자열 (' ')은 기본값인 ' 00:00:00.0000 '로 변환 됩니다. 공백 (' ')만 포함 하는 문자열은 오류를 생성 합니다.  
  
|입력 데이터 형식|입력 데이터 예제|Time 데이터 형식으로 변환|  
|-------------------|-----------------------|--------------------------------|  
|**시간** 형식의 문자열 리터럴|' hh: mm: ss. fffffff '<br /><br />예: ' 12:35:29.1234567 '|데이터 원본에 **시간** 데이터 형식의 전체 자릿수 보다 작거나 같은 정밀도 (소수 자릿수)가 있는 경우 데이터는 0으로 오른쪽으로 채워집니다. 예를 들어 리터럴 값 ' 12:35:29.123 '는 ' 12:35:29.1230000 '로 삽입 됩니다.|  
  
### <a name="datetimeoffset-data-type"></a>datetimeoffset 데이터 형식  
다음 표에서는 **datetimeoffset** (*n*) 형식의 열에 리터럴 값을 로드 하기 위한 기본 형식 및 규칙을 정의 합니다. 기본 형식은 ' yyyy-MM-dd hh: mm: ss. fffffff {+ |-} hh: mm '입니다. 빈 문자열 (' ')은 기본값인 ' 1900-01-01 12:00:00.0000000 + 00:00 '로 변환 됩니다. 공백 (' ')만 포함 하는 문자열은 오류를 생성 합니다. 소수 자릿수는 열 정의에 따라 달라 집니다. 예를 들어 **datetimeoffset** (2)으로 정의 된 열에는 두 개의 소수 자릿수가 있습니다.  
  
|입력 데이터 형식|입력 데이터 예제|Datetimeoffset 데이터 형식으로 변환|  
|-------------------|-----------------------|------------------------------------------|  
|**Datetime** 형식의 문자열 리터럴|' yyyy-MM-dd hh: MM: ss [.fff] '<br /><br />예: ' 2007-05-08 12:35:29.123 '|값이 삽입 될 때 누락 된 소수 자릿수와 오프셋 값은 0으로 설정 됩니다. 예를 들어 ' 2007-05-08 12:35:29.123 ' 리터럴은 ' 2007-05-08 12:35:29.1230000 + 00:00 '로 삽입 됩니다.|  
|**Smalldatetime** 형식의 문자열 리터럴|' yyyy-mm-dd hh: mm '<br /><br />예: ' 2007-05-08 12:35 '|값이 삽입 될 때 초, 남은 소수 자릿수 및 오프셋 값이 0으로 설정 됩니다.|  
|**날짜** 형식의 문자열 리터럴|' yyyy-MM-dd '<br /><br />예: ' 2007-05-08 '|값이 삽입 될 때 시간 값 (시, 분, 초 및 소수 자릿수)은 0으로 설정 됩니다. 예를 들어 ' 2007-05-08 ' 리터럴은 ' 2007-05-08 00:00:00.0000000 + 00:00 '로 삽입 됩니다.|  
|**Datetime2** 형식의 문자열 리터럴|' yyyy-MM-dd hh: MM: ss. fffffff '<br /><br />예: ' 2007-05-08 12:35:29.1234567 '|원본 데이터는 datetimeoffset 열에서 지정 된 소수 자릿수 초를 초과할 수 없습니다. 데이터 원본에 소수 자릿수 초의 소수 자릿수가 작거나 같은 경우 0을 사용 하 여 해당 데이터를 오른쪽으로 채웁니다. 예를 들어 데이터 형식이 datetimeoffset (5) 이면 리터럴 값 ' 2007-05-08 12:35:29.123 + 12:15 '이 ' 12:35:29.12300 + 12:15 '로 삽입 됩니다.|  
|**Datetimeoffset** 형식의 문자열 리터럴|' yyyy-MM-dd hh: mm: ss. fffffff {+&#124;-} hh: mm '<br /><br />예: ' 2007-05-08 12:35:29.1234567 + 12:15 '|원본 데이터는 datetimeoffset 열에서 지정 된 소수 자릿수 초를 초과할 수 없습니다. 데이터 원본에 소수 자릿수 초의 소수 자릿수가 작거나 같은 경우 0을 사용 하 여 해당 데이터를 오른쪽으로 채웁니다. 예를 들어 데이터 형식이 datetimeoffset (5) 이면 리터럴 값 ' 2007-05-08 12:35:29.123 + 12:15 '이 ' 12:35:29.12300 + 12:15 '로 삽입 됩니다.|  
  
### <a name="datetime2-data-type"></a>datetime2 데이터 형식  
다음 표에서는 리터럴 값을 **datetime2** (*n*) 형식의 열로 로드 하기 위한 기본 형식 및 규칙을 정의 합니다. 기본 형식은 ' yyyy-MM-dd hh: MM: ss. fffffff '입니다. 빈 문자열 (' ')이 기본 값인 ' 1900-01-01 12:00:00 '로 변환 됩니다. 공백 (' ')만 포함 하는 문자열은 오류를 생성 합니다. 소수 자릿수는 열 정의에 따라 달라 집니다. 예를 들어 **datetime2** (2)로 정의 된 열에는 두 개의 소수 자릿수가 있습니다.  
  
|입력 데이터 형식|입력 데이터 예제|Datetime2 데이터 형식으로 변환|  
|-------------------|-----------------------|-------------------------------------|  
|**Datetime** 형식의 문자열 리터럴|' yyyy-MM-dd hh: MM: ss [.fff] '<br /><br />예: ' 2007-05-08 12:35:29.123 '|소수 자릿수 초는 선택 사항이 며 값이 삽입 될 때 0으로 설정 됩니다.|  
|**Smalldatetime** 형식의 문자열 리터럴|' yyyy-mm-dd hh: mm '<br /><br />예: ' 2007-05-08 12 '|값이 삽입 될 때 선택적 초와 남은 소수 자릿수는 0으로 설정 됩니다.|  
|**날짜** 형식의 문자열 리터럴|' yyyy-MM-dd '<br /><br />예: ' 2007-05-08 '|값이 삽입 될 때 시간 값 (시, 분, 초 및 소수 자릿수)은 0으로 설정 됩니다. 예를 들어 ' 2007-05-08 ' 리터럴은 ' 2007-05-08 12:00:00.0000000 '로 삽입 됩니다.|  
|**Datetime2** 형식의 문자열 리터럴|' yyyy-MM-dd hh: MM: ss: fffffff '<br /><br />예: ' 2007-05-08 12:35:29.1234567 '|데이터 원본에 **datetime2**(*n*)에 지정 된 값 보다 작거나 같은 데이터 및 시간 구성 요소가 포함 된 경우 데이터가 삽입 됩니다. 그렇지 않으면 오류가 생성 됩니다.|  
  
### <a name="datetime-formats"></a><a name="DateFormats"></a>Datetime 형식  
Dwloader는 SQL Server PDW 로드 되는 입력 데이터에 대해 다음과 같은 데이터 형식을 지원 합니다. 자세한 내용은 표 다음에 나열 되어 있습니다.  
  
|Datetime|smalldatetime|date|datetime2|datetimeoffset|  
|------------|-----------------|--------|-------------|------------------|  
|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fff]|[M[M]]M-[d]d-[yy]yy HH:mm[:00]|[M[M]]M-[d]d-[yy]yy|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fffffff]|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[d]d-[yy]yy hh:mm:ss[.fff][tt]|[M[M]]M-[d]d-[yy]yy hh:mm[:00][tt]||[M[M]]M-[d]d-[yy]yy hh:mm:ss[.fffffff][tt]|[M[M]]M-[d]d-[yy]yy hh:mm:ss[.fffffff][tt] zzz|  
|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fff]|[M[M]]M-[yy]yy-[d]d HH:mm[:00]|[M[M]]M-[yy]yy-[d]d|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fffffff]|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fff][tt]|[M[M]]M-[yy]yy-[d]d hh:mm[:00][tt]||[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fffffff][tt]|[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fffffff][tt] zzz|  
|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fff]|[yy]yy-[M[M]]M-[d]d HH:mm[:00]|[yy]yy-[M[M]]M-[d]d|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fffffff]|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fffffff]  zzz|  
|[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fff][tt]|[yy]yy-[M[M]]M-[d]d hh:mm[:00][tt]||[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fffffff][tt]|[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fffffff][tt] zzz|  
|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fff]|[yy]yy-[d]d-[M[M]]M HH:mm[:00]|[yy]yy-[d]d-[M[M]]M|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fffffff]|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fffffff]  zzz|  
|[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fff][tt]|[yy]yy-[d]d-[M[M]]M hh:mm[:00][tt]||[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fffffff][tt]|[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fffffff][tt] zzz|  
|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fff]|[d]d-[M[M]]M-[yy]yy HH:mm[:00]|[d]d-[M[M]]M-[yy]yy|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fffffff]|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fffffff] zzz|  
|[d]d-[M[M]]M-[yy]yy hh:mm:ss[.fff][tt]|[d]d-[M[M]]M-[yy]yy hh:mm[:00][tt]||[d]d-[M[M]]M-[yy]yy hh:mm:ss[.fffffff][tt]|[d]d-[M[M]]M-[yy]yy hh:mm:ss[.fffffff][tt] zzz|  
|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fff]|[d]d-[yy]yy-[M[M]]M HH:mm[:00]|[d]d-[yy]yy-[M[M]]M|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fffffff]|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fffffff] zzz|  
|[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fff][tt]|[d]d-[yy]yy-[M[M]]M hh:mm[:00][tt]||[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fffffff][tt]|[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fffffff][tt] zzz|  
  
상세 정보:  
  
-   월, 일 및 연도 값을 구분 하려면 '-', '/' 또는 '를 사용할 수 있습니다. '. 간단히 하기 위해 테이블에서는 '-' 구분 기호만 사용합니다.  
  
-   월을 텍스트로 지정 하려면 3 자 이상의 문자를 사용 합니다. 1 또는 2 자의 월은 숫자로 해석 됩니다.  
  
-   시간 값을 구분 하려면 ': ' 기호를 사용 합니다.  
  
-   대괄호 안에 있는 문자는 선택 사항입니다.  
  
-   'tt' 문자는 [AM|PM|am|pm]을 지정합니다. 기본값은 AM입니다. 'tt'를 지정한 경우 시간 값(hh)은 0-12 범위여야 합니다.  
  
-   'zzz' 문자는 {+|-}HH:ss] 형식으로 시스템의 현재 시간대에 대한 시간대 오프셋을 지정합니다.  
  
## <a name="inserting-literals-into-numeric-types"></a><a name="InsertNumerictypes"></a>숫자 형식에 리터럴 삽입  
다음 표에서는 숫자 형식을 사용 하는 SQL Server PDW 열에 리터럴 값을 로드 하기 위한 기본 형식 및 변환 규칙을 정의 합니다.  
  
### <a name="bit-data-type"></a>bit 데이터 형식  
다음 표에서는 **bit**형식의 열에 리터럴 값을 로드 하기 위한 기본 형식 및 규칙을 정의 합니다. 빈 문자열 (' ') 또는 공백 (' ')만 포함 하는 문자열은 0으로 변환 됩니다.  
  
|입력 데이터 형식|입력 데이터 예제|Bit 데이터 형식으로 변환|  
|-------------------|-----------------------|-------------------------------|  
|**정수** 형식의 문자열 리터럴|' ffffffffff '<br /><br />예: ' 1 ' 또는 ' 321 '|문자열 리터럴로 형식이 지정 된 정수 값에는 음수 값을 사용할 수 없습니다. 예를 들어 '-123 ' 값은 오류를 생성 합니다.<br /><br />1 보다 큰 값은 1로 변환 됩니다. 예를 들어 ' 123 ' 값은 1로 변환 됩니다.|  
|문자열 리터럴|' TRUE ' 또는 ' f a l s e '<br /><br />예: ' true '|' TRUE ' 값은 1로 변환 됩니다. 값 ' f a l s e '는 0으로 변환 됩니다.|  
|정수 리터럴|fffffffn<br /><br />예: 1 또는 321|1 보다 크거나 0 보다 작은 값은 1로 변환 됩니다. 예를 들어 123 및-123 값은 1로 변환 됩니다.|  
|10 진 리터럴|fffnn .fff<br /><br />예: 1234.5678|1 보다 크거나 0 보다 작은 값은 1로 변환 됩니다. 예를 들어 123.45 및-123.45 값은 1로 변환 됩니다.|  
  
### <a name="decimal-data-type"></a>decimal 데이터 형식  
다음 표에서는 리터럴 값을 **decimal** (*p, s*) 형식의 열로 로드 하는 규칙을 정의 합니다. 데이터 변환 규칙은 SQL Server와 동일 합니다. 자세한 내용은 MSDN의 [데이터 형식 변환 (데이터베이스 엔진)](/previous-versions/sql/sql-server-2008-r2/ms191530(v=sql.105)) 을 참조 하십시오.  
  
|입력 데이터 형식|입력 데이터 예제|  
|-------------------|-----------------------|  
|정수 리터럴|321312313123|  
|10 진 리터럴|123344.34455|  
  
### <a name="float-and-real-data-types"></a>float 및 real 데이터 형식  
다음 표에서는 **float** 또는 **real**형식의 열에 리터럴 값을 로드 하는 규칙을 정의 합니다. 데이터 변환 규칙은 SQL Server와 동일 합니다. 자세한 내용은 MSDN의 [데이터 형식 변환 (데이터베이스 엔진)](../t-sql/data-types/data-type-conversion-database-engine.md) 을 참조 하십시오.  
  
|입력 데이터 형식|입력 데이터 예제|  
|-------------------|-----------------------|  
|정수 리터럴|321312313123|  
|10 진 리터럴|123344.34455|  
|부동 소수점 리터럴|3.12323 e + 14|  
  
### <a name="int-bigint-tinyint-smallint-data-types"></a>int, bigint, tinyint, smallint 데이터 형식  
다음 표에서는 리터럴 값을 **int**, **bigint**, **tinyint**또는 **smallint**형식의 열로 로드 하는 규칙을 정의 합니다. 데이터 원본이 지정 된 데이터 형식에 허용 된 범위를 초과할 수 없습니다. 예를 들어 **tinyint** 의 범위는 0에서 255 사이이 고 **int** 의 범위는-2147483648에서 2147483647 사이입니다.  
  
|입력 데이터 형식|입력 데이터 예제|정수 데이터 형식으로 변환|  
|-------------------|-----------------------|------------------------------------|  
|정수 리터럴|321312313123||  
|10 진 리터럴|123344.34455|소수점 오른쪽에 있는 값이 잘립니다.|  
  
### <a name="money-and-smallmoney-data-types"></a>money 및 smallmoney 데이터 형식  
Money 리터럴 값은 선택적 소수점이 있는 숫자의 문자열로 표시 되며 선택적인 통화 기호는 접두사로 표시 됩니다. 데이터 원본이 지정 된 데이터 형식에 허용 된 범위를 초과할 수 없습니다. 예를 들어 **smallmoney** 의 범위는-214748.3648 ~ 214748.3647 이며 **money** 의 범위는-922337203685477.5808 ~ 922337203685477.5807입니다. 다음 표에서는 **money** 또는 **smallmoney**형식의 열에 리터럴 값을 로드 하는 규칙을 정의 합니다.  
  
|입력 데이터 형식|입력 데이터 예제|Money 또는 smallmoney 데이터 형식으로 변환|  
|-------------------|-----------------------|-----------------------------------------------|  
|정수 리터럴|321312|소수점 뒤의 누락 된 숫자는 값이 삽입 될 때 0으로 설정 됩니다. 예를 들어 리터럴 12345는 12345.0000으로 삽입 됩니다.|  
|10 진 리터럴|123344.34455|소수점이 하 자릿수가 4를 초과 하는 경우 값은 가장 가까운 값으로 반올림 됩니다. 예를 들어 값 123344.34455는 123344.3446으로 삽입 됩니다.|  
|Money 리터럴|$123456.7890|통화 기호는 값으로 삽입 되지 않습니다.<br /><br />소수점이 하 자릿수가 4를 초과 하는 경우 값은 가장 가까운 값으로 반올림 됩니다.|  
  
## <a name="inserting-literals-into-string-types"></a><a name="InsertStringTypes"></a>문자열 형식에 리터럴 삽입  
다음 표에서는 문자열 형식을 사용 하는 SQL Server PDW 열에 리터럴 값을 로드 하기 위한 기본 형식 및 변환 규칙을 정의 합니다.  
  
### <a name="char-varchar-nchar-and-nvarchar-data-types"></a>char, varchar, nchar 및 nvarchar 데이터 형식  
다음 표에서는 **char**, **varchar**, **nchar** 및 **nvarchar**형식의 열에 리터럴 값을 로드 하기 위한 기본 형식 및 규칙을 정의 합니다. 데이터 원본 길이가 데이터 형식에 대해 지정 된 크기를 초과할 수 없습니다. 데이터 원본 길이가 **char** 또는 **nchar** 데이터 형식의 크기 보다 작은 경우 데이터는 데이터 형식 크기에 도달할 수 있도록 공백이 있는 오른쪽으로 채워집니다.  
  
|입력 데이터 형식|입력 데이터 예제|문자 데이터 형식으로 변환|  
|---------------|-------------------|----------------------------------|  
|문자열 리터럴|Format: ' character string '<br /><br />예: ' abc '| 해당 없음 |  
|유니코드 문자열 리터럴|형식: N'character string '<br /><br />예: N'abc '| 해당 없음 |  
|정수 리터럴|형식: ffffffffffn<br /><br />예: 321312313123| 해당 없음 |  
|10 진 리터럴|형식: ffffff. fffffff<br /><br />예: 12344.34455| 해당 없음 |  
|Money 리터럴|형식: $ffffff .fffnn<br /><br />예: $123456.99|선택적 통화 기호는 값으로 삽입 되지 않습니다. 통화 기호를 삽입 하려면 값을 문자열 리터럴로 삽입 합니다. 이는 모든 리터럴을 문자열 리터럴로 처리 하는 로더의 형식과 일치 합니다.<br /><br />쉼표는 허용 되지 않습니다.<br /><br />소수점 뒤의 자릿수가 2를 초과 하는 경우 값은 가장 가까운 값으로 반올림 됩니다. 예를 들어 값 123.946789는 123.95으로 삽입 됩니다.<br /><br />CONVERT 함수를 사용 하 여 money 리터럴을 삽입 하는 경우에는 기본 스타일 0 (소수점 뒤에 쉼표 및 2 자리)만 사용할 수 있습니다.|  
  
### <a name="general-remarks"></a>일반적인 주의 사항  
**dwloader** 는 smp SQL Server 수행 하는 것과 동일한 암시적 변환을 수행 하지만 smp SQL Server 지원 되는 모든 암시적 변환을 지원 하지는 않습니다.  
 
<!-- MISSING LINKS 
## See Also  
[Grant Permissions to Load Data &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-load-data-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  

-->
