---
title: "函数&lt;过程名&gt;并非在所有代码路径上都返回值 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc42105
- vbc42105
dev_langs:
- VB
helpviewer_keywords:
- BC42105
ms.assetid: b6929bf4-a365-4a70-8dc9-6b0fc09e1468
caps.latest.revision: 12
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 288fdf7c4845b20283681d9eb3504ac314f1ddd2
ms.lasthandoff: 03/13/2017

---
# <a name="function-39ltprocedurenamegt39-doesn39t-return-a-value-on-all-code-paths"></a>函数&lt;过程名&gt;并非在所有代码路径上都返回值
函数\<过程名&1;> 并非在所有代码路径上都返回值。 是否缺少 Return 语句？  
  
 一个`Function`过程具有至少一个可能不返回值的代码路径。  
  
 您可以返回一个介于`Function`处于以下任一过程︰  
  
-   中包括值[Return 语句](../../../visual-basic/language-reference/statements/return-statement.md)。  
  
-   将值赋给`Function`过程名，然后执行`Exit Function`语句。  
  
-   将值赋给`Function`过程名，然后执行`End Function`语句。  
  
 控制权将传递给`Exit Function`或`End Function`和您没有任何值分配到过程名称，该过程返回的返回数据类型的默认值。 详细信息，请参阅"行为"中[Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)。  
  
 默认情况下，此消息是一个警告。 有关隐藏警告或将警告视为错误的详细信息，请参阅[在 Visual Basic 中配置警告](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID:** BC42105  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   控制流逻辑检查并确保导致返回每个语句之前赋值。  
  
     很容易地保证每一次返回从过程返回一个值，如果始终使用`Return`语句。 如果这样做时之前, 的最后一个语句`End Function`应`Return`语句。  
  
## <a name="see-also"></a>另请参阅  
 [Function 过程](../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)   
 [“项目设计器”->“编译”页 (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/compile-page-project-designer-visual-basic)
