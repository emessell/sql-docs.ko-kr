---
title: azdata bdc spark statement 참조
titleSuffix: SQL Server big data clusters
description: azdata bdc spark statement 명령에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5d39e9b28edf04848fd718459219691f9c020b67
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358423"
---
# <a name="azdata-bdc-spark-statement"></a>azdata bdc spark statement

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]에 적용됩니다.

다음 문서에서는 **azdata** 도구의 **sql** 명령에 대한 참조를 제공합니다. 다른 **azdata** 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요.

## <a name="commands"></a>명령

|명령|설명|
| --- | --- |
[azdata bdc spark statement list](#azdata-bdc-spark-statement-list) | 지정된 Spark 세션의 문을 모두 나열합니다.
[azdata bdc spark statement create](#azdata-bdc-spark-statement-create) | 지정된 세션에서 새 Spark 문을 만듭니다.
[azdata bdc spark statement info](#azdata-bdc-spark-statement-info) | 지정된 Spark 세션에서 요청된 문에 대한 정보를 가져옵니다.
[azdata bdc spark statement cancel](#azdata-bdc-spark-statement-cancel) | 지정된 Spark 세션 내에서 문을 취소합니다.
## <a name="azdata-bdc-spark-statement-list"></a>azdata bdc spark statement list
지정된 Spark 세션의 문을 모두 나열합니다.
```bash
azdata bdc spark statement list --session-id -i 
                                
```
### <a name="examples"></a>예제
세션 문을 모두 나열합니다.
```bash
azdata bdc spark statement list --session-id 0
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--session-id -i`
Spark 세션 ID 번호입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org)를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-bdc-spark-statement-create"></a>azdata bdc spark statement create
지정된 세션에서 새 문을 만들고 실행합니다.  실행이 빠르면 결과에 실행 출력이 포함됩니다.  빠르지 않으면, 문이 완료된 후에 ‘spark session info’를 사용하여 결과를 검색할 수 있습니다.
```bash
azdata bdc spark statement create --session-id -i 
                                  --code -c
```
### <a name="examples"></a>예제
문을 실행합니다.
```bash
azdata bdc spark statement create --session-id 0 --code "2+2"
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--session-id -i`
Spark 세션 ID 번호입니다.
#### `--code -c`
문의 일부로 실행할 코드가 포함된 문자열입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org)를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-bdc-spark-statement-info"></a>azdata bdc spark statement info
문이 완료된 경우 실행 상태와 실행 결과를 가져옵니다. 문 ID는 ‘spark statement create’에서 반환됩니다.
```bash
azdata bdc spark statement info --session-id -i 
                                --statement-id -s
```
### <a name="examples"></a>예제
ID가 0이고 문 ID가 0인 세션의 문 정보를 가져옵니다.
```bash
azdata bdc spark statement info --session-id 0 --statement-id 0
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--session-id -i`
Spark 세션 ID 번호입니다.
#### `--statement-id -s`
지정된 세션 ID 내의 Spark 문 ID 번호입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org)를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.
## <a name="azdata-bdc-spark-statement-cancel"></a>azdata bdc spark statement cancel
지정된 Spark 세션 내에서 문을 취소합니다. 문 ID는 ‘spark statement create’에서 반환됩니다.
```bash
azdata bdc spark statement cancel --session-id -i 
                                  --statement-id -s
```
### <a name="examples"></a>예제
문을 취소합니다.
```bash
azdata bdc spark statement cancel --session-id 0 --statement-id 0
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--session-id -i`
Spark 세션 ID 번호입니다.
#### `--statement-id -s`
지정된 세션 ID 내의 Spark 문 ID 번호입니다.
### <a name="global-arguments"></a>전역 인수
#### `--debug`
로깅의 자세한 정도를 늘려 모든 디버그 로그를 표시합니다.
#### `--help -h`
이 도움말 메시지를 표시하고 종료합니다.
#### `--output -o`
출력 형식입니다.  허용되는 값: json, jsonc, table, tsv  기본값: json
#### `--query -q`
JMESPath 쿼리 문자열입니다. 자세한 내용 및 예제는 [http://jmespath.org/](http://jmespath.org)를 참조하세요.
#### `--verbose`
로깅의 자세한 정도를 늘립니다. 전체 디버그 로그를 표시하려면 --debug를 사용합니다.

## <a name="next-steps"></a>다음 단계

다른 **azdata** 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요. 

**azdata** 도구를 설치하는 방법에 대한 자세한 내용은 [azdata 설치](..\install\deploy-install-azdata.md)를 참조하세요.

