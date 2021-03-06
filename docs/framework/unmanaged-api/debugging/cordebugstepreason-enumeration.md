---
description: 了解详细信息： CorDebugStepReason 枚举
title: CorDebugStepReason 枚举
ms.date: 03/30/2017
api_name:
- CorDebugStepReason
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugStepReason
helpviewer_keywords:
- CorDebugStepReason enumeration [.NET Framework debugging]
ms.assetid: fe248069-b33c-48e1-a777-06ac9b239c54
topic_type:
- apiref
ms.openlocfilehash: 2a331b09709ffb6179f2e481baf4bf421d60ea99
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/06/2021
ms.locfileid: "99801535"
---
# <a name="cordebugstepreason-enumeration"></a>CorDebugStepReason 枚举

指示一个单步执行的结果。  
  
## <a name="syntax"></a>语法  
  
```cpp  
typedef enum CorDebugStepReason {  
    STEP_NORMAL,  
    STEP_RETURN,  
    STEP_CALL,  
    STEP_EXCEPTION_FILTER,  
    STEP_EXCEPTION_HANDLER,  
    STEP_INTERCEPT,  
    STEP_EXIT  
} CorDebugStepReason;  
```  
  
## <a name="members"></a>成员  
  
|成员|说明|  
|------------|-----------------|  
|`STEP_NORMAL`|单步执行在同一函数内正常完成。|  
|`STEP_RETURN`|在函数返回后，按正常方式继续执行。|  
|`STEP_CALL`|在新调用的函数开始时以正常方式继续执行。|  
|`STEP_EXCEPTION_FILTER`|已生成异常，并已将控制权传递给异常筛选器。|  
|`STEP_EXCEPTION_HANDLER`|已生成异常，并已将控制权传递给异常处理程序。|  
|`STEP_INTERCEPT`|控件已传递给侦听器。|  
|`STEP_EXIT`|线程在步骤完成之前退出。|  
  
## <a name="requirements"></a>要求  

 **平台：** 请参阅 [系统要求](../../get-started/system-requirements.md)。  
  
 **标头**：CorDebug.idl、CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>请参阅

- [StepComplete 方法](icordebugmanagedcallback-stepcomplete-method.md)
- [调试枚举](debugging-enumerations.md)
