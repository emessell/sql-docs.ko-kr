---
title: azdata context 참조
titleSuffix: SQL Server big data clusters
description: azdata context 명령에 대한 참조 문서입니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 19f085016a0d2e4789dbdd7a5319f58332310e4f
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358147"
---
# <a name="azdata-context"></a>azdata context

[!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]에 적용됩니다.

다음 문서에서는 **azdata** 도구의 **sql** 명령에 대한 참조를 제공합니다. 다른 **azdata** 명령에 대한 자세한 내용은 [azdata 참조](reference-azdata.md)를 참조하세요.

## <a name="commands"></a>명령

|명령|설명|
| --- | --- |
[azdata context list](#azdata-context-list) | 사용자 프로필에서 사용할 수 있는 컨텍스트를 나열합니다.
[azdata context delete](#azdata-context-delete) | 사용자 프로필에서 특정 네임스페이스가 있는 컨텍스트를 삭제합니다.
[azdata context set](#azdata-context-set) | 특정 네임스페이스가 있는 컨텍스트를 사용자 프로필의 활성 컨텍스트로 설정합니다.
## <a name="azdata-context-list"></a>azdata context list
`azdata context set` 또는 `azdata context delete`를 사용하여 컨텍스트를 설정하거나 삭제할 수 있습니다. 새 컨텍스트에 로그인하려면 `azdata login`을 사용합니다.
```bash
azdata context list [--active -a] 
                    
```
### <a name="examples"></a>예제
사용자 프로필에서 사용할 수 있는 모든 컨텍스트를 나열합니다.
```bash
azdata context list
```
사용자 프로필의 활성 컨텍스트를 나열합니다.
```bash
azdata context list --active
```
### <a name="optional-parameters"></a>선택적 매개 변수
#### `--active -a`
현재 활성 컨텍스트만 나열합니다.
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
## <a name="azdata-context-delete"></a>azdata context delete
삭제된 컨텍스트가 활성 상태이면 사용자가 새 활성 컨텍스트를 설정해야 합니다. 설정하거나 삭제할 수 있는 컨텍스트를 확인하려면 `azdata context list`를 사용합니다.
```bash
azdata context delete --namespace -ns 
                      
```
### <a name="examples"></a>예제
사용자 프로필에서 contextNamespace를 삭제합니다.
```bash
azdata context delete -n contextNamespace
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--namespace -ns`
삭제하려는 컨텍스트의 네임스페이스입니다.
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
## <a name="azdata-context-set"></a>azdata context set
설정할 수 있는 컨텍스트를 확인하려면 `azdata context list`를 사용합니다. 나열된 컨텍스트가 없으면 로그인하여 사용자 프로필 `azdata login`에 컨텍스트를 만들어야 합니다. 로그인하는 컨텍스트는 활성 컨텍스트가 됩니다. 여러 엔터티에 로그인하는 경우 이 명령을 사용하여 활성 컨텍스트 간에 전환할 수 있습니다. 현재 활성 컨텍스트를 보려면 `azdata context list --active`를 사용합니다.
```bash
azdata context set --namespace -ns 
                   
```
### <a name="examples"></a>예제
contextNamespace를 사용자 프로필의 활성 컨텍스트로 설정합니다.
```bash
azdata context set -n contextNamespace
```
### <a name="required-parameters"></a>필수 매개 변수
#### `--namespace -ns`
설정하려는 컨텍스트의 네임스페이스입니다.
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

