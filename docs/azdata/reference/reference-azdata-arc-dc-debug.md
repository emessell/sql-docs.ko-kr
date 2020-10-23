---
title: azdata arc dc debug 참조
titleSuffix: SQL Server big data clusters
description: azdata arc dc debug 명령에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bfb4c13f262609328bf73dca282f9d3445a8bf8c
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358801"
---
# <a name="azdata-arc-dc-debug"></a>azdata arc dc debug

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]에 적용됩니다.

다음 문서에서는 **azdata** 도구의 **sql** 명령에 대한 참조를 제공합니다. 다른 **azdata** 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요.

## <a name="commands"></a>명령

|명령|설명|
| --- | --- |
[azdata arc dc debug copy-logs](#azdata-arc-dc-debug-copy-logs) | 로그를 복사합니다.
[azdata arc dc debug dump](#azdata-arc-dc-debug-dump) | 메모리 덤프를 트리거합니다.
## <a name="azdata-arc-dc-debug-copy-logs"></a>azdata arc dc debug copy-logs
데이터 컨트롤러에서 디버그 로그를 복사합니다. 시스템에 Kubernetes 구성이 있어야 합니다.
```bash
azdata arc dc debug copy-logs --namespace -ns 
                              [--container -c]  
                              
[--target-folder -d]  
                              
[--pod]  
                              
[--resource-kind -rk]  
                              
[--resource-name -rn]  
                              
[--timeout -t]  
                              
[--skip-compress -sc]  
                              
[--exclude-dumps -ed]
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--namespace -ns`
데이터 컨트롤러의 Kubernetes 네임스페이스입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--container -c`
유사한 이름을 가진 컨테이너의 로그를 복사합니다. 선택 사항이며, 기본적으로 모든 컨테이너의 로그를 복사합니다. 여러 번 지정할 수 없습니다. 여러 번 지정하면 마지막 항목이 사용됩니다.
#### `--target-folder -d`
로그를 복사할 대상 폴더 경로입니다. 선택 사항이며, 기본적으로 로컬 폴더에 결과를 만듭니다.  여러 번 지정할 수 없습니다. 여러 번 지정하면 마지막 항목이 사용됩니다.
#### `--pod`
유사한 이름을 가진 Pod의 로그를 복사합니다. 선택 사항이며, 기본적으로 모든 Pod의 로그를 복사합니다. 여러 번 지정할 수 없습니다. 여러 번 지정하면 마지막 항목이 사용됩니다.
#### `--resource-kind -rk`
특정 종류의 리소스에 대한 로그를 복사합니다. 여러 번 지정할 수 없습니다. 여러 번 지정하면 마지막 항목이 사용됩니다. 지정한 경우 --resource-name도 지정하여 리소스를 식별해야 합니다.
#### `--resource-name -rn`
지정한 이름의 리소스에 대한 로그를 복사합니다. 여러 번 지정할 수 없습니다. 여러 번 지정하면 마지막 항목이 사용됩니다. 지정한 경우 --resource-kind도 지정하여 리소스를 식별해야 합니다.
#### `--timeout -t`
명령이 완료될 때까지 대기할 시간(초)입니다. 기본값은 0으로, 무제한입니다.
#### `--skip-compress -sc`
결과 폴더 압축을 건너뛸지 여부를 지정합니다. 기본값은 False입니다. 이 값은 결과 폴더를 압축합니다.
#### `--exclude-dumps -ed`
결과 폴더에서 덤프를 제외할지 여부를 지정합니다. 기본값은 False입니다. 이 값은 덤프를 포함합니다.
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
## <a name="azdata-arc-dc-debug-dump"></a>azdata arc dc debug dump
메모리 덤프를 트리거하고 컨테이너에서 복사합니다. 시스템에 Kubernetes 구성이 있어야 합니다.
```bash
azdata arc dc debug dump --namespace -ns 
                         [--container -c]  
                         
[--target-folder -d]
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--namespace -ns`
데이터 컨트롤러의 Kubernetes 네임스페이스입니다.
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--container -c`
실행 중인 프로세스의 덤프를 위해 트리거할 대상 컨테이너입니다.
`controller`
#### `--target-folder -d`
덤프를 복사할 대상 폴더입니다. `./output/dump`
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

