---
description: 了解详细信息： <param> (Visual Basic)
title: <param>
ms.date: 07/20/2015
helpviewer_keywords:
- param XML tag
- <param> XML tag
ms.assetid: 4e32e86f-f6f3-4301-b7fc-2f321fb54368
ms.openlocfilehash: 94fe5e11d5846f7fa00eb73c1c4363990ae23b2f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/06/2021
ms.locfileid: "99700287"
---
# <a name="param-visual-basic"></a>\<param> (Visual Basic)

定义参数名称和说明。  
  
## <a name="syntax"></a>语法  
  
```xml  
<param name="name">description</param>  
```  
  
## <a name="parameters"></a>参数  

 `name`  
 方法参数的名称。 用双引号 (" ") 将名称引起来。  
  
 `description`  
 参数的说明。  
  
## <a name="remarks"></a>备注  

 在方法声明的注释中，应使用 `<param>` 标记来描述方法参数之一。  
  
 标记的文本 `<param>` 将出现在以下位置：  
  
- IntelliSense 的参数信息。 有关详细信息，请参阅[使用 IntelliSense](/visualstudio/ide/using-intellisense)。  
  
- 对象浏览器。 有关详细信息，请参阅 [查看代码的结构](/visualstudio/ide/viewing-the-structure-of-code)。  
  
 使用 [-doc](../../reference/command-line-compiler/doc.md) 进行编译以便将文档注释处理到文件中。  
  
## <a name="example"></a>示例  

 此示例使用 `<param>` 标记来描述 `id` 参数。  
  
 [!code-vb[VbVbcnXmlDocComments#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnXmlDocComments/VB/Class1.vb#6)]  
  
## <a name="see-also"></a>请参阅

- [XML 注释标记](index.md)
