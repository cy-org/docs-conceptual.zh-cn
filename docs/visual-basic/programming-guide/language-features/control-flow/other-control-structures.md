---
title: "其他控件结构 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- statements [Visual Basic], control flow
- control structures
ms.assetid: 24b811f7-98ba-40ec-8dd3-4d528cfa4574
caps.latest.revision: 19
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
ms.openlocfilehash: 639571b493037f26951bd8fbf140d7bce3244889
ms.lasthandoff: 03/13/2017

---
# <a name="other-control-structures-visual-basic"></a>其他控件结构 (Visual Basic)
[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]提供帮助您的控制结构释放资源或减少您必须重复的对象引用的次数。  
  
## <a name="usingend-using-construction"></a>使用...结束使用构造  
 `Using...End Using`构造建立要在其中一个语句块使用的资源，例如 SQL 连接。 （可选） 可以获取具有资源`Using`语句。 当您退出`Using`块中， [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] ，以便它不用于其他代码以使用自动释放资源。 资源必须是本地且可释放。 有关详细信息，请参阅[Using 语句](../../../../visual-basic/language-reference/statements/using-statement.md)。  
  
## <a name="withend-with-construction"></a>使用...以构造结尾  
 `With...End With`构造允许您指定的对象引用一次，然后运行一系列访问其成员的语句。 这可以简化代码，并提高性能，因为[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]无需重新建立访问它的每个语句的引用。 有关详细信息，请参阅[与...使用语句结束](../../../../visual-basic/language-reference/statements/with-end-with-statement.md)。  
  
## <a name="see-also"></a>另请参阅  
 [控制流](../../../../visual-basic/programming-guide/language-features/control-flow/index.md)   
 [决策结构](../../../../visual-basic/programming-guide/language-features/control-flow/decision-structures.md)   
 [循环结构](../../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [嵌套的控件结构](../../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)   
 [Using 语句](../../../../visual-basic/language-reference/statements/using-statement.md)   
 [With...End With 语句](../../../../visual-basic/language-reference/statements/with-end-with-statement.md)
