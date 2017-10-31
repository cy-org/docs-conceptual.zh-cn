---
title: "对象变量或 With 块变量未设置 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbrID91
dev_langs:
- VB
ms.assetid: 2f03e611-f0ed-465c-99a2-a816e034faa3
caps.latest.revision: 9
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 820ef0115a6a27d77f10f4e41d95576bbd79bfa3
ms.lasthandoff: 03/13/2017

---
# <a name="object-variable-or-with-block-variable-not-set"></a>未设置对象变量或 With 块变量
正在引用无效的对象变量。   出现此错误的原因可能有多种：  
  
-   已声明变量，而无需指定一种类型。 如果不指定类型声明的变量，则默认键入`Object`。  
  
     例如，与声明的变量`Dim x`属于类型`Object;`与声明的变量`Dim x As String`属于类型`String`。  
  
    > [!TIP]
    >  `Option Strict`语句不允许隐式类型化会导致`Object`类型。 如果省略该类型时，将发生编译时错误。 请参阅[Option Strict 语句](../../../visual-basic/language-reference/statements/option-strict-statement.md)。  
  
-   您试图引用已被设置为的对象`Nothing`  
  
     。  
  
-   您试图访问未被正确声明一个数组变量中的元素。  
  
     例如，数组声明为`products() As String`将触发该错误，如果您尝试引用数组的元素`products(3) = "Widget"`。 该数组不包含任何元素，将被视为对象。  
  
-   您正尝试访问代码中的`With...End With`阻止在初始化块之前。   一个`With...End With`块必须通过执行初始化`With`语句入口点。  
  
> [!NOTE]
>  在早期版本的 Visual Basic 或 VBA 此错误也由分配给变量的一个值，而无需使用触发`Set`关键字 (`x = "name"`而不是`Set x = "name"`)。 `Set`关键字将不再在 Visual Basic.Net 中有效。  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
1.  设置`Option Strict`到`On`通过将以下代码添加到文件的开头︰  
  
```vb  
Option Strict On  
```  

     When you run the project, a compiler error will appear in the **Error List** for any variable that was specified without a type.  
  
2.  如果不想要启用`Option Strict`，搜索您的代码是否已指定但无类型的任何变量 (`Dim x`而不是`Dim x As String`) 并将预期的类型添加到声明。  
  
3.  请确保不指已被设置为一个对象变量`Nothing`。  搜索关键字代码`Nothing`，并修改您的代码，以便该对象未设置为`Nothing`直到后具有引用它。  
  
4.  请确保任何数组变量就会标注之前访问它们。 首次创建数组时，既可以分配一个维度 (`Dim x(5) As String`而不是`Dim x() As String`)，或使用`ReDim`关键字可以在第一次访问之前设置数组的维数。  
  
5.  请确保您`With`块初始化通过执行`With`语句入口点。  
  
## <a name="see-also"></a>另请参阅  
 [对象变量声明](../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)   
 [ReDim 语句](../../../visual-basic/language-reference/statements/redim-statement.md)   
 [With...End With 语句](../../../visual-basic/language-reference/statements/with-end-with-statement.md)
