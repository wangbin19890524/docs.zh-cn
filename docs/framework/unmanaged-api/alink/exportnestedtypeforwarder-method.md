---
description: 了解详细信息： ExportNestedTypeForwarder 方法
title: ExportNestedTypeForwarder 方法
ms.date: 03/30/2017
api_name:
- IALink.ExportNestedTypeForwarder
api_location:
- alink.dll
api_type:
- COM
f1_keywords:
- ExportNestedTypeForwarder
helpviewer_keywords:
- ExportNestedTypeForwarder method
ms.assetid: 886ea6c5-6b26-4b88-8bf6-448d6d191950
topic_type:
- apiref
ms.openlocfilehash: fd791e3fea76338f191fcf924d56720d257d2e8b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/06/2021
ms.locfileid: "99638101"
---
# <a name="exportnestedtypeforwarder-method"></a>ExportNestedTypeForwarder 方法

将嵌套类型的类型转发器添加到给定程序集的类型表。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT ExportNestedTypeForwarder(  
    mdAssembly      AssemblyID,  
    mdToken         FileToken,  
    mdTypeDef       TypeToken,  
    mdExportedType  ParentType,  
    LPCWSTR         pszTypename,  
    DWORD           dwFlags,  
    mdExportedType* pType  
) PURE;  
```  
  
## <a name="parameters"></a>参数  

 `AssemblyID`  
 要从中导出的程序集的 ID。  
  
 `FileToken`  
 定义类型的文件的文件标记或程序集 ID。  
  
 `TypeToken`  
 类型的标记。  
  
 `ParentType`  
 父类型的标记。  
  
 `pszTypename`  
 要导出的完全限定的类型名称。  
  
 `dwFlags`  
 `ComType` 标志，如 `tdPublic` 或 `tdNested` 。  
  
 `pType`  
 接收导出类型的令牌。 这仅适用于发出嵌套类型。  
  
## <a name="return-value"></a>返回值  

 如果方法成功，则返回 S_OK。  
  
## <a name="requirements"></a>要求  

 需要 alink  
  
## <a name="see-also"></a>请参阅

- [IALink 接口](ialink-interface.md)
- [IALink2 接口](ialink2-interface.md)
- [ALink API](index.md)
