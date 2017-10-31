---
title: "创建自定义特性 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 5c9ef584-6c7c-496b-92a9-6e42f8d9ca28
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 1aa97a591fdbdfab931a8b5e4f70ec3c00762332
ms.lasthandoff: 03/13/2017

---
# <a name="creating-custom-attributes-visual-basic"></a>创建自定义特性 (Visual Basic)
可以通过定义属性类，派生的类直接或间接从创建您自己的自定义属性<xref:System.Attribute>，这样标识属性定义在元数据中快速而轻松地。</xref:System.Attribute> 假设您希望为同名的编写类型的程序员的标记类型。 您可能会定义一个自定义`Author`特性类︰  
  
```vb  
<System.AttributeUsage(System.AttributeTargets.Class Or   
                       System.AttributeTargets.Struct)>   
Public Class Author  
    Inherits System.Attribute  
    Private name As String  
    Public version As Double  
    Sub New(ByVal authorName As String)  
        name = authorName  
        version = 1.0  
    End Sub  
End Class  
```  
  
 类名是属性的名称， `Author`。 派生自`System.Attribute`，因此它是一个自定义特性类。 构造函数的参数是自定义特性的位置参数。 在此示例中，`name`是位置参数。 所有公共读 / 写字段或属性都被命名参数。 在这种情况下，`version`唯一的命名参数。 请注意，使用`AttributeUsage`特性，以使`Author`属性仅对类有效和`Structure`声明。  
  
 可以使用这一新属性，如下所示︰  
  
```vb  
<Author("P. Ackerman", Version:=1.1)>   
Class SampleClass  
    ' P. Ackerman's code goes here...  
End Class  
```  
  
 `AttributeUsage`有一个命名的参数， `AllowMultiple`，使用它可以使自定义特性单用途或使用多次。 在下面的代码示例创建多次使用的特性。  
  
```vb  
' multiuse attribute  
<System.AttributeUsage(System.AttributeTargets.Class Or   
                       System.AttributeTargets.Struct,   
                       AllowMultiple:=True)>   
Public Class Author  
    Inherits System.Attribute  
```  
  
 在下面的代码示例中，多个相同类型的属性应用于类中。  
  
```vb  
<Author("P. Ackerman", Version:=1.1),   
Author("R. Koch", Version:=1.2)>   
Class SampleClass  
    ' P. Ackerman's code goes here...  
    ' R. Koch's code goes here...  
End Class  
```  
  
> [!NOTE]
>  如果属性类包含一个属性，该属性必须为读写。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Reflection></xref:System.Reflection>   
 [Visual Basic 编程指南](../../../../visual-basic/programming-guide/index.md)   
 [编写自定义特性](http://msdn.microsoft.com/library/97216f69-bde8-49fd-ac40-f18c500ef5dc)   
 [反射 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/reflection.md)   
 [特性 (Visual Basic)](../../../../visual-basic/language-reference/attributes.md)   
 [使用反射 (Visual Basic 中) 访问特性](../../../../visual-basic/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md)   
 [AttributeUsage (Visual Basic)](../../../../visual-basic/programming-guide/concepts/attributes/attributeusage.md)
