---
description: 了解详细信息： IHostTaskManager：： BeginThreadAffinity 方法
title: IHostTaskManager::BeginThreadAffinity 方法
ms.date: 03/30/2017
api_name:
- IHostTaskManager.BeginThreadAffinity
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostTaskManager::BeginThreadAffinity
helpviewer_keywords:
- IHostTaskManager::BeginThreadAffinity method [.NET Framework hosting]
- BeginThreadAffinity method [.NET Framework hosting]
ms.assetid: fea3ab88-ce41-4c5a-847b-bb78cd748da6
topic_type:
- apiref
ms.openlocfilehash: 15ee917f5c81ee605c0cb4df3180041797c18daf
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/06/2021
ms.locfileid: "99784595"
---
# <a name="ihosttaskmanagerbeginthreadaffinity-method"></a>IHostTaskManager::BeginThreadAffinity 方法

通知宿主托管代码正在输入一个时间段，在此期间，不能将当前任务移动到另一个操作系统线程。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT BeginThreadAffinity ();  
```  
  
## <a name="return-value"></a>返回值  
  
|HRESULT|说明|  
|-------------|-----------------|  
|S_OK|`BeginThreadAffinity` 已成功返回。|  
|HOST_E_CLRNOTAVAILABLE| (CLR) 的公共语言运行时未加载到进程中，或 CLR 处于无法运行托管代码或成功处理调用的状态。|  
|HOST_E_TIMEOUT|调用超时。|  
|HOST_E_NOT_OWNER|调用方不拥有该锁。|  
|HOST_E_ABANDONED|已阻止的线程或纤程正在等待某个事件时，该事件被取消。|  
|E_FAIL|发生未知的灾难性故障。 当方法返回 E_FAIL 时，CLR 在该进程内将不再可用。 对宿主方法的后续调用会返回 HOST_E_CLRNOTAVAILABLE。|  
  
## <a name="remarks"></a>备注  

 CLR 通常在对的 `IHostTaskManager::BeginThreadAffinity` 调用的上下文中调用 <xref:System.Threading.Thread.BeginThreadAffinity%2A?displayProperty=nameWithType> 。 在对 [IHostTaskManager：： EndThreadAffinity](ihosttaskmanager-endthreadaffinity-method.md)进行相应的调用之前，不能重新计划当前任务。 可以切换出任务，但当它们切换回时，必须将它们分配到从中进行切换的相同操作系统线程。对的嵌套调用 `BeginThreadAffinity` 不起作用，因为调用指的是当前任务。  
  
## <a name="requirements"></a>要求  

 **平台：** 请参阅 [系统要求](../../get-started/system-requirements.md)。  
  
 **标头：** Mscoree.dll  
  
 **库：** 作为中的资源包含 MSCorEE.dll  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>请参阅

- [ICLRTask 接口](iclrtask-interface.md)
- [ICLRTaskManager 接口](iclrtaskmanager-interface.md)
- [IHostTask 接口](ihosttask-interface.md)
- [IHostTaskManager 接口](ihosttaskmanager-interface.md)
