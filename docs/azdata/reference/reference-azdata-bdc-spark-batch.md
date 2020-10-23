---
title: azdata bdc spark batch 참조
titleSuffix: SQL Server big data clusters
description: azdata bdc spark batch 명령에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 74968c1efd64ecc382b7a0ab9669a983bb442ef7
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358510"
---
# <a name="azdata-bdc-spark-batch"></a>azdata bdc spark batch

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]에 적용됩니다.

다음 문서에서는 **azdata** 도구의 **sql** 명령에 대한 참조를 제공합니다. 다른 **azdata** 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요.

## <a name="commands"></a>명령

|명령|설명|
| --- | --- |
[azdata bdc spark batch create](#azdata-bdc-spark-batch-create) | 새 Spark 일괄 처리를 만듭니다.
[azdata bdc spark batch list](#azdata-bdc-spark-batch-list) | Spark의 일괄 처리를 모두 나열합니다.
[azdata bdc spark batch info](#azdata-bdc-spark-batch-info) | 활성 Spark 일괄 처리에 대한 정보를 가져옵니다.
[azdata bdc spark batch log](#azdata-bdc-spark-batch-log) | Spark 일괄 처리의 실행 로그를 가져옵니다.
[azdata bdc spark batch state](#azdata-bdc-spark-batch-state) | Spark 일괄 처리의 실행 상태를 가져옵니다.
[azdata bdc spark batch delete](#azdata-bdc-spark-batch-delete) | Spark 일괄 처리를 삭제합니다.
## <a name="azdata-bdc-spark-batch-create"></a>azdata bdc spark batch create
제공된 코드를 실행하는 새 Spark 일괄 작업을 만듭니다.
```bash
azdata bdc spark batch create --file -f 
                              [--class-name -c]  
                              
[--arguments -a]  
                              
[--jar-files -j]  
                              
[--py-files -p]  
                              
[--files]  
                              
[--driver-memory]  
                              
[--driver-cores]  
                              
[--executor-memory]  
                              
[--executor-cores]  
                              
[--executor-count]  
                              
[--archives]  
                              
[--queue -q]  
                              
[--name -n]  
                              
[--config]
```
### <a name="examples"></a>예제
새 Spark 일괄 처리를 만듭니다.
```bash
azdata bdc spark batch create --code "2+2"
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--file -f`
실행할 파일의 경로입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--class-name -c`
하나 이상의 jar 파일을 전달할 때 실행할 클래스의 이름입니다.
#### `--arguments -a`
인수 목록입니다.  목록을 전달하려면 값을 JSON으로 인코딩합니다.  예: ‘[“entry1”, “entry2”]‘
#### `--jar-files -j`
jar 파일 경로의 목록입니다.  목록을 전달하려면 값을 JSON으로 인코딩합니다.  예: ‘[“entry1”, “entry2”]‘
#### `--py-files -p`
python 파일 경로의 목록입니다.  목록을 전달하려면 값을 JSON으로 인코딩합니다.  예: ‘[“entry1”, “entry2”]‘
#### `--files`
파일 경로의 목록입니다.  목록을 전달하려면 값을 JSON으로 인코딩합니다.  예: ‘[“entry1”, “entry2”]‘
#### `--driver-memory`
드라이버에 할당할 메모리 크기입니다.  값의 일부로 단위를 지정합니다.  예: 512M 또는 2G
#### `--driver-cores`
드라이버에 할당할 CPU 코어 수량입니다.
#### `--executor-memory`
실행기에 할당할 메모리 크기입니다.  값의 일부로 단위를 지정합니다.  예: 512M 또는 2G
#### `--executor-cores`
실행기에 할당할 CPU 코어 수량입니다.
#### `--executor-count`
실행할 실행기 인스턴스 수입니다.
#### `--archives`
보관 경로의 목록입니다.  목록을 전달하려면 값을 JSON으로 인코딩합니다.  예: ‘[“entry1”, “entry2”]‘
#### `--queue -q`
세션을 실행할 Spark 큐의 이름입니다.
#### `--name -n`
Spark 세션의 이름입니다.
#### `--config`
Spark 구성 값을 포함하는 이름-값 쌍의 목록입니다.  JSON 사전으로 인코딩됩니다.  예: ‘{“name”:“value”, “name2”:“value2”}’
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
## <a name="azdata-bdc-spark-batch-list"></a>azdata bdc spark batch list
Spark의 일괄 처리를 모두 나열합니다.
```bash
azdata bdc spark batch list 
```
### <a name="examples"></a>예제
활성 일괄 처리를 모두 나열합니다.
```bash
azdata bdc spark batch list
```
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
## <a name="azdata-bdc-spark-batch-info"></a>azdata bdc spark batch info
지정된 ID를 가진 Spark 일괄 처리에 대한 정보를 가져옵니다.  일괄 처리 ID는 ‘spark batch create’에서 반환됩니다.
```bash
azdata bdc spark batch info --batch-id -i 
                            
```
### <a name="examples"></a>예제
ID가 0인 일괄 처리의 일괄 처리 정보를 가져옵니다.
```bash
azdata bdc spark batch info --batch-id 0
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--batch-id -i`
Spark 일괄 처리 ID 번호입니다.
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
## <a name="azdata-bdc-spark-batch-log"></a>azdata bdc spark batch log
지정된 ID를 가진 Spark 일괄 처리의 일괄 처리 로그 항목을 가져옵니다.  일괄 처리 ID는 ‘spark batch create’에서 반환됩니다.
```bash
azdata bdc spark batch log --batch-id -i 
                           
```
### <a name="examples"></a>예제
ID가 0인 일괄 처리의 일괄 처리 로그를 가져옵니다.
```bash
azdata bdc spark batch log --batch-id 0
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--batch-id -i`
Spark 일괄 처리 ID 번호입니다.
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
## <a name="azdata-bdc-spark-batch-state"></a>azdata bdc spark batch state
지정된 ID를 가진 Spark 일괄 처리의 일괄 처리 상태를 가져옵니다.  일괄 처리 ID는 ‘spark batch create’에서 반환됩니다.
```bash
azdata bdc spark batch state --batch-id -i 
                             
```
### <a name="examples"></a>예제
ID가 0인 일괄 처리의 일괄 처리 상태를 가져옵니다.
```bash
azdata bdc spark batch state --batch-id 0
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--batch-id -i`
Spark 일괄 처리 ID 번호입니다.
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
## <a name="azdata-bdc-spark-batch-delete"></a>azdata bdc spark batch delete
Spark 일괄 처리를 삭제합니다. 일괄 처리 ID는 ‘spark batch create’에서 반환됩니다.
```bash
azdata bdc spark batch delete --batch-id -i 
                              
```
### <a name="examples"></a>예제
일괄 처리를 삭제합니다.
```bash
azdata bdc spark batch delete --batch-id 0
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--batch-id -i`
Spark 일괄 처리 ID 번호입니다.
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

