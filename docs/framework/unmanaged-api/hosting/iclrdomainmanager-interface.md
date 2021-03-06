---
description: 了解详细信息： ICLRDomainManager 接口
title: ICLRDomainManager 接口
ms.date: 03/30/2017
api_name:
- ICLRDomainManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRDomainManager
helpviewer_keywords:
- ICLRDomainManager interface [.NET Framework hosting]
ms.assetid: f08b2390-d872-4521-a815-e9c237c4c45d
ms.openlocfilehash: d719e89d81e8c7abb1f238ce50b4e236de17ac72
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790004"
---
# <a name="iclrdomainmanager-interface"></a>ICLRDomainManager 接口

使宿主能够指定将用于初始化默认应用程序域的应用程序域管理器，并指定初始化属性。  
  
## <a name="methods"></a>方法  
  
|方法|说明|  
|------------|-----------------|  
|[SetAppDomainManagerType 方法](iclrdomainmanager-setappdomainmanagertype-method.md)|指定从类派生的、 <xref:System.AppDomainManager?displayProperty=nameWithType> 将用于初始化默认应用程序域的应用程序域管理器的类型。|  
|[SetPropertiesForDefaultAppDomain 方法](iclrdomainmanager-setpropertiesfordefaultappdomain-method.md)|设置将用于初始化默认应用程序域的属性。|  
  
## <a name="remarks"></a>备注  

 若要获取此接口的实例，请使用管理器类型 IID 调用 [ICLRControl：： GetCLRManager](iclrcontrol-getclrmanager-method.md) 方法 `IID_ICLRDomainManager` 。  
  
## <a name="requirements"></a>要求  

 **平台：** 请参阅 [系统要求](../../get-started/system-requirements.md)。  
  
 **标头：** MetaHost  
  
 **库：** 作为中的资源包含 MSCorEE.dll  
  
 **.NET Framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>请参阅

- [承载接口](hosting-interfaces.md)
- [承载](index.md)
