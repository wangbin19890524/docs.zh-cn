---
description: '详细了解： ^ = 运算符 (Visual Basic) '
title: ^= 运算符
ms.date: 07/20/2015
f1_keywords:
- vb.^=
helpviewer_keywords:
- assignment statements [Visual Basic], compound
- statements [Visual Basic], compound assignment
- ^= operator [Visual Basic]
- compound assignment statements [Visual Basic]
ms.assetid: 397da132-2d96-4a85-a7bc-f7c730a608c9
ms.openlocfilehash: 5894fdbedb411c6324a9355bd2d335bb6c6c5867
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/06/2021
ms.locfileid: "99773883"
---
# <a name="-operator-visual-basic"></a>^= 运算符 (Visual Basic)

将变量或属性的值提升为表达式的幂，并将结果赋回给变量或属性。  
  
## <a name="syntax"></a>语法  
  
```vb  
variableorproperty ^= expression  
```  
  
## <a name="parts"></a>组成部分  

 `variableorproperty`  
 必需。 任何数值变量或属性。  
  
 `expression`  
 必需。 任何数值表达式。  
  
## <a name="remarks"></a>备注  

 运算符左侧的元素 `^=` 可以是简单的标量变量、属性或数组的元素。 变量或属性不能是 [只读](../modifiers/readonly.md)的。  
  
 `^=`运算符首先在运算符的左侧引发变量或属性 (的值) ，以使运算符) 右侧 (表达式的值的的值的幂。 然后，运算符将该操作的结果赋给变量或属性。  
  
 Visual Basic 总是对 [Double 数据类型](../data-types/double-data-type.md)执行幂运算。 将任意不同类型的操作数转换为 `Double` ，并且结果始终为 `Double` 。  
  
 的值 `expression` 可以是小数、负数或同时为两者。  
  
## <a name="overloading"></a>重载  

 [^ 运算符](exponentiation-operator.md)可 *重载*，这意味着当操作数具有该类或结构的类型时，该类或结构可以重新定义其行为。 重载 `^` 运算符会影响运算符的行为 `^=` 。 如果你的代码 `^=` 在重载的类或结构上使用 `^` ，请确保你了解其重新定义的行为。 有关详细信息，请参阅 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)。  
  
## <a name="example"></a>示例  

 下面的示例使用 `^=` 运算符将一个变量的值提升 `Integer` 为第二个变量的幂，并将结果赋给第一个变量。  
  
 [!code-vb[VbVbalrOperators#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#21)]  
  
## <a name="see-also"></a>请参阅

- [^ 运算符](exponentiation-operator.md)
- [赋值运算符](assignment-operators.md)
- [算术运算符](arithmetic-operators.md)
- [Visual Basic 中的运算符优先级](operator-precedence.md)
- [按功能列出的运算符](operators-listed-by-functionality.md)
- [语句](../../programming-guide/language-features/statements.md)
