---
description: 了解详细信息： RemoveHandler 语句
title: RemoveHandler 语句
ms.date: 07/20/2015
f1_keywords:
- vb.RemoveHandlerMethod
- vb.RemoveHandler
- RemoveHandler
helpviewer_keywords:
- RemoveHandler keyword [Visual Basic]
- RemoveHandler statement [Visual Basic]
ms.assetid: 647cd825-e877-4910-b4f1-8d168beebe6a
ms.openlocfilehash: 699db9edfc029b4149246e8b654645040ae6d89e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/06/2021
ms.locfileid: "99741297"
---
# <a name="removehandler-statement"></a>RemoveHandler 语句

删除事件和事件处理程序之间的关联。  
  
## <a name="syntax"></a>语法  
  
```vb  
RemoveHandler event, AddressOf eventhandler  
```  
  
## <a name="parts"></a>组成部分  
  
|术语|定义|  
|---|---|  
|`event`|正在处理的事件的名称。|  
|`eventhandler`|当前处理事件的过程的名称。|  
  
## <a name="remarks"></a>备注  

 使用 `AddHandler` 和 `RemoveHandler` 语句，可以在程序执行过程中随时启动和停止特定事件的事件处理。  
  
> [!NOTE]
> 对于自定义事件，该 `RemoveHandler` 语句将调用事件的 `RemoveHandler` 访问器。 有关自定义事件的详细信息，请参阅 [Event 语句](event-statement.md)。  
  
## <a name="example"></a>示例  

 [!code-vb[VbVbalrEvents#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEvents/VB/Class1.vb#17)]  
  
## <a name="see-also"></a>请参阅

- [AddHandler 语句](addhandler-statement.md)
- [句柄数](handles-clause.md)
- [Event 语句](event-statement.md)
- [事件](../../programming-guide/language-features/events/index.md)
