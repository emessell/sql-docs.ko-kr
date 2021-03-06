---
title: IServerVirtualDevice::CloseDevice
titlesuffix: SQL Server VDI reference
description: 이 문서에서는 IServerVirtualDevice::CloseDevice 명령에 대한 참조를 제공합니다.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 3e9ff54c500b626d667622105a39e742c5e2a339
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896833"
---
# <a name="iservervirtualdeviceclosedevice-vdi"></a>IServerVirtualDevice::CloseDevice (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**CloseDevice** 함수는 IServerVirtualDeviceSet2::OpenDevice를 사용하여 열린 가상 디바이스를 닫습니다.

## <a name="syntax"></a>구문

```c
HRESULT IServerVirtualDevice::CloseDevice ();
```

## <a name="return-value"></a>Return Value

|Return Value | 설명 |
|---|---|
| VD_E_CLOSE | 디바이스가 이미 닫혀 있습니다. |
| VD_E_ABORT | 인터페이스가 중단 상태에 있습니다. |

## <a name="remarks"></a>설명

SignalAbort를 사용하여 비정상적인 종료를 적용한 후에는 CloseDevice가 필요하지 않습니다. SignalAbort를 사용한 후 CloseDevice가 호출되면 아무 동작도 수행되지 않습니다.

## <a name="next-steps"></a>다음 단계

자세한 내용은 [SQL Server 가상 디바이스 인터페이스 참조 개요](reference-virtual-device-interface.md)를 참조하세요.