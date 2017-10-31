---
title: "变量&lt;variablename&gt;在赋值前被使用 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc42104
- BC42104
dev_langs:
- VB
helpviewer_keywords:
- BC42104
ms.assetid: 6909aa0b-b4a1-46f5-a18c-ba3e565c1dd8
caps.latest.revision: 10
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
ms.openlocfilehash: 7ad1f392fae2f90e366277b7b531d96011648866
ms.lasthandoff: 03/13/2017

---
# <a name="variable-39ltvariablenamegt39-is-used-before-it-has-been-assigned-a-value"></a>变量&lt;variablename&gt;在赋值前被使用
变量\<variablename&1;> 在赋值前被使用。 可能在运行时导致 null 引用异常。  
  
 应用程序具有至少一个可能读取变量之前的任何值分配给它的代码路径。  
  
 如果从未为变量赋值，则它保持其数据类型的默认值。 对于引用数据类型，该默认值是[Nothing](../../../visual-basic/language-reference/nothing.md)。 读取的值为一个引用变量`Nothing`可能会导致<xref:System.NullReferenceException>在某些情况下。</xref:System.NullReferenceException>  
  
 默认情况下，此消息是一个警告。 有关隐藏警告或将警告视为错误的详细信息，请参阅[在 Visual Basic 中配置警告](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID:** BC42104  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   控制流逻辑检查并确保在控件传递给读取它的任何语句之前，该变量具有有效的值。  
  
-   若要确保该变量始终具有一个有效的值的一种方法是初始化为其声明的一部分。 请参阅中的"初始化" [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)   
 [变量声明](../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [变量疑难解答](../../../visual-basic/programming-guide/language-features/variables/troubleshooting-variables.md)
