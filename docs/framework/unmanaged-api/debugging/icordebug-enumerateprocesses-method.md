---
description: 了解详细信息： ICorDebug：： EnumerateProcesses 方法
title: ICorDebug::EnumerateProcesses 方法
ms.date: 03/30/2017
api_name:
- ICorDebug.EnumerateProcesses
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- EnumerateProcesses
helpviewer_keywords:
- EnumerateProcesses method [.NET Framework debugging]
- ICorDebug::EnumerateProcesses method [.NET Framework debugging]
ms.assetid: ba25d166-1d28-4f1d-aca2-de298bbca669
topic_type:
- apiref
ms.openlocfilehash: 44ee21a820a1c9f94f1d66c93ff040b504bfcc93
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791577"
---
# <a name="icordebugenumerateprocesses-method"></a>ICorDebug::EnumerateProcesses 方法

获取正在调试的进程的枚举器。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT EnumerateProcesses (  
    [out] ICorDebugProcessEnum      **ppProcess  
);  
```  
  
## <a name="parameters"></a>参数  

 `ppProcess`  
 指向 ICorDebugProcessEnum 对象地址的指针，该对象是正在调试的进程的枚举器。  
  
## <a name="requirements"></a>要求  

 **平台：** 请参阅 [系统要求](../../get-started/system-requirements.md)。  
  
 **标头**：CorDebug.idl、CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅

- [ICorDebug 接口](icordebug-interface.md)
