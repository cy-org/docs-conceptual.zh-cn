---
title: "Sub 或 Function 未定义 (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbrID35
dev_langs:
- VB
ms.assetid: 661fdb90-ee7d-40ce-b30b-5e7267bd957a
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
ms.openlocfilehash: 7d32bc9c8f13b245e6333c4460cab541f6e9409e
ms.lasthandoff: 03/13/2017

---
# <a name="sub-or-function-not-defined-visual-basic"></a>未定义 Sub 或 Function (Visual Basic)
一个`Sub`或`Function`必须定义以便进行调用。 此错误的可能原因包括：  
  
-   过程名称拼写错误。  
  
-   尝试从另一个项目中调用的过程，而无需显式添加到该项目中引用**引用**对话框。  
  
-   指定对调用的过程是不可见的过程。  
  
-   声明的 Windows 动态链接库 (DLL) 例程或不在指定的库或代码资源的 Macintosh 代码资源例程。  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
1.  请确保过程名称拼写正确。  
  
2.  找到包含你想要调用的过程的项目名称**引用**对话框。 如果未出现，请单击**浏览**按钮对其进行搜索。 选择的项目名称，左边的复选框，然后单击**确定**。  
  
3.  请检查该例程的名称。  
  
## <a name="see-also"></a>另请参阅  
 [错误类型](../../../visual-basic/programming-guide/language-features/error-types.md)   
 [管理项目中引用](https://docs.microsoft.com/visualstudio/ide/managing-references-in-a-project)   
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)
