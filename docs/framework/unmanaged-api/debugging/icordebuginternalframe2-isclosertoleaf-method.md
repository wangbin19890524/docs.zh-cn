---
description: 了解详细信息： ICorDebugInternalFrame2：： IsCloserToLeaf 方法
title: ICorDebugInternalFrame2::IsCloserToLeaf 方法
ms.date: 03/30/2017
api_name:
- ICorDebugInternalFrame2.IsCloserToLeaf Method
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugInternalFrame2::IsCloserToLeaf
helpviewer_keywords:
- ICorDebugInternalFrame2::IsCloserToLeaf method [.NET Framework debugging]
- IsCloserToLeaf method [.NET Framework debugging]
ms.assetid: c1d3d1eb-8370-4f25-8297-3bd262b4740a
topic_type:
- apiref
ms.openlocfilehash: d773f8670f600a5bcd2a8dad7f23fe243195957c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/06/2021
ms.locfileid: "99801275"
---
# <a name="icordebuginternalframe2isclosertoleaf-method"></a>ICorDebugInternalFrame2::IsCloserToLeaf 方法

检查 `this` 内部帧是否接近于指定的 ICorDebugFrame 对象。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT IsCloserToLeaf([in] ICorDebugFrame * pFrameToCompare,  
                       [out] BOOL * pIsCloser);  
```  
  
## <a name="parameters"></a>参数  

 `pFrameToCompare`  
 中指向比较对象的指针 `ICorDebugFrame` 。  
  
 `pIsCloser`  
 [out] `true` 如果 `this` 内部帧比指定的帧更接近叶 `pFrameToCompare` ，则为; 否则为 `false` 。  
  
## <a name="return-value"></a>返回值  

 此方法返回以下特定 HRESULT 以及表示方法失败的 HRESULT 错误。  
  
|HRESULT|说明|  
|-------------|-----------------|  
|S_OK|已成功执行比较。|  
|E_FAIL|无法执行比较。|  
|E_INVALIDARG|`pFrameToCompare` 或 `pIsCloser` 为 null。|  
  
## <a name="remarks"></a>备注  

 `IsCloserToLeaf` 可用于实现将内部帧与堆栈上的其他帧交错的策略。  
  
## <a name="requirements"></a>要求  

 **平台：** 请参阅 [系统要求](../../get-started/system-requirements.md)。  
  
 **标头**：CorDebug.idl、CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>请参阅

- [ICorDebugInternalFrame2 接口](icordebuginternalframe2-interface.md)
- [调试接口](debugging-interfaces.md)
- [调试](index.md)
