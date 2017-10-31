---
title: "Extension 特性可以只能应用于 Module、 Sub 或 Function 声明。 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc36550
- vbc36550
dev_langs:
- VB
helpviewer_keywords:
- BC36550
ms.assetid: 4387a51f-733c-45d7-abdb-eb64d4f51078
caps.latest.revision: 18
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
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 3eee008f737bf625023b6e4d58e1df7d282148d3
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="39extension39-attribute-can-be-applied-only-to-39module39-39sub39-or-39function39-declarations"></a>Extension 特性可以只能应用于 Module、 Sub 或 Function 声明。
若要扩展在 Visual Basic 中的数据类型的唯一方法是定义标准模块内的扩展方法。 扩展方法可以是`Sub`过程或`Function`过程。 所有扩展方法都必须都标记为扩展属性`<Extension()>`，从<xref:System.Runtime.CompilerServices?displayProperty=fullName>命名空间。</xref:System.Runtime.CompilerServices?displayProperty=fullName> （可选） 包含扩展方法的模块可能标记为相同的方式。 其他扩展属性的使用方式均有效。  
  
 **错误 ID:** BC36550  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   删除扩展属性。  
  
-   与封闭模块中定义的方法重新设计您的扩展。  
  
## <a name="example"></a>示例  
 下面的示例定义`Print`方法`String`数据类型。  
  
```  
Imports StringUtility  
Imports System.Runtime.CompilerServices  
Namespace StringUtility  
    <Extension()>   
    Module StringExtensions  
        <Extension()>   
        Public Sub Print (ByVal str As String)  
            Console.WriteLine(str)  
        End Sub  
    End Module  
End Namespace  
```  
  
## <a name="see-also"></a>另请参阅  
 [属性概述](../../../visual-basic/programming-guide/concepts/attributes/index.md)   
 [扩展方法](../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)   
 [Module 语句](../../../visual-basic/language-reference/statements/module-statement.md)

