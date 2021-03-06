---
title: SQL Server on Linux에 대한 보안 제한 사항
description: Azure Key Vault에 저장된 키 사용과 확장 가능한 키 관리가 어떻게 지원되지 않는지를 비롯하여 SQL Server on Linux의 제한 사항에 대해 알아봅니다.
author: VanMSFT
ms.author: vanto
ms.date: 09/12/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 64da74cc-14bf-4636-a55e-8cc1fce2aaff
ms.openlocfilehash: 611afe6c02e979c7c9672d7d94f84844b8932cf6
ms.sourcegitcommit: 3ea082c778f6771b17d90fb597680ed334d3e0ec
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/11/2020
ms.locfileid: "88088805"
---
# <a name="security-limitations-for-sql-server-on-linux"></a>SQL Server on Linux에 대한 보안 제한 사항

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

현재 SQL Server on Linux에는 다음과 같은 제한 사항이 있습니다.

* 표준 암호 정책이 제공됩니다. MUST_CHANGE는 구성할 수 있는 유일한 옵션입니다. CHECK_POLICY 옵션은 지원되지 않습니다.
* 확장 가능 키 관리는 지원되지 않습니다. 
* Azure Key Vault에 저장된 키를 사용하는 기능은 지원되지 않습니다.
* SQL Server는 연결을 암호화하기 위해 자체 서명된 인증서를 생성합니다. TLS에 사용자 제공 인증서를 사용하도록 SQL Server를 구성할 수 있습니다. 

SQL Server에서 사용할 수 있는 보안 기능에 대한 자세한 내용은 [SQL Server 데이터베이스 엔진 및 Azure SQL Database에 대한 보안 센터](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)를 참조하세요.

## <a name="next-steps"></a>다음 단계

일반적인 보안 작업은 [SQL Server on Linux의 보안 기능 시작](sql-server-linux-security-get-started.md)을 참조하세요. TCP 포트 번호, SQL Server 디렉터리를 변경하고 추적 플래그 또는 데이터 정렬을 구성하는 스크립트를 보려면 [mssql-conf를 사용하여 SQL Server on Linux 구성](sql-server-linux-configure-mssql-conf.md)을 참조하세요.
