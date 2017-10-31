---
title: "AttributeUsage (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: 48757216-c21d-4051-86d5-8a3e03c39d2c
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
ms.openlocfilehash: bf56f40033f9d1547d63fccd25e3c0561bb62cb1
ms.lasthandoff: 03/13/2017

---
# <a name="attributeusage-visual-basic"></a>AttributeUsage (Visual Basic)
确定如何使用自定义特性类。 `AttributeUsage`是可以应用于自定义特性定义来控制如何将应用新的属性的属性。 当显式应用默认设置如下所示︰  
  
```vb  
<System.AttributeUsage(System.AttributeTargets.All,   
                   AllowMultiple:=False,   
                   Inherited:=True)>   
Class NewAttribute  
    Inherits System.Attribute  
End Class  
```  
  
 在此示例中，`NewAttribute`类可以是应用于任何特性的代码的实体，但可以一次只能应用于每个实体。 它由派生类时应用于基类继承。  
  
 `AllowMultiple`和`Inherited`参数是可选的所以此代码具有相同的效果︰  
  
```vb  
<System.AttributeUsage(System.AttributeTargets.All)>   
Class NewAttribute  
    Inherits System.Attribute  
End Class  
```  
  
 第一个`AttributeUsage`参数必须是一个或多个元素的<xref:System.AttributeTargets>枚举。</xref:System.AttributeTargets> 多个目标类型可以被链接在一起的或运算符如下︰  
  
```vb  
Imports System  
```  
  
```vb  
<AttributeUsage(AttributeTargets.Property Or AttributeTargets.Field)>   
Class NewPropertyOrFieldAttribute  
    Inherits Attribute  
End Class  
```  
  
 如果`AllowMultiple`参数设置为`true`，则生成的属性可以多次应用于单个实体，如下︰  
  
```vb  
Imports System  
```  
  
```vb  
<AttributeUsage(AttributeTargets.Class, AllowMultiple:=True)>   
Class MultiUseAttr  
    Inherits Attribute  
End Class  
  
<MultiUseAttr(), MultiUseAttr()>   
Class Class1  
End Class  
```  
  
 在这种情况下`MultiUseAttr`可以重复应用，因为`AllowMultiple`设置为`true`。 这两种格式所示的应用多个属性均有效。  
  
 如果`Inherited`设置为`false`，则该属性不会由从特性化的类派生的类继承。 例如:   
  
```vb  
Imports System  
```  
  
```vb  
<AttributeUsage(AttributeTargets.Class, Inherited:=False)>   
Class Attr1  
    Inherits Attribute  
End Class  
  
<Attr1()>   
Class BClass  
  
End Class    
  
Class DClass  
    Inherits BClass  
End Class  
```  
  
 在这种情况下`Attr1`不应用于`DClass`通过继承。  
  
## <a name="remarks"></a>备注  
 `AttributeUsage`属性是一个单用途属性 — 不能为同一个类不止一次应用。 `AttributeUsage`是<xref:System.AttributeUsageAttribute>。</xref:System.AttributeUsageAttribute>的别名  
  
 有关详细信息，请参阅[访问通过使用反射 (Visual Basic 中) 的属性](../../../../visual-basic/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md)。  
  
## <a name="example"></a>示例  
 下面的示例演示的效果`Inherited`和`AllowMultiple`参数`AttributeUsage`属性和要如何枚举应用于类的自定义特性。  
  
```vb  
Imports System  
```  
  
```vb  
' Create some custom attributes:  
<AttributeUsage(System.AttributeTargets.Class, Inherited:=False)>   
Class A1  
    Inherits System.Attribute  
End Class  
  
<AttributeUsage(System.AttributeTargets.Class)>   
Class A2  
    Inherits System.Attribute  
End Class      
  
<AttributeUsage(System.AttributeTargets.Class, AllowMultiple:=True)>   
Class A3  
    Inherits System.Attribute  
End Class  
  
' Apply custom attributes to classes:  
<A1(), A2()>   
Class BaseClass  
  
End Class  
  
<A3(), A3()>   
Class DerivedClass  
    Inherits BaseClass  
End Class  
  
Public Class TestAttributeUsage  
    Sub Main()  
        Dim b As New BaseClass  
        Dim d As New DerivedClass  
        ' Display custom attributes for each class.  
        Console.WriteLine("Attributes on Base Class:")  
        Dim attrs() As Object = b.GetType().GetCustomAttributes(True)  
  
        For Each attr In attrs  
            Console.WriteLine(attr)  
        Next  
  
        Console.WriteLine("Attributes on Derived Class:")  
        attrs = d.GetType().GetCustomAttributes(True)  
        For Each attr In attrs  
            Console.WriteLine(attr)  
        Next              
    End Sub  
End Class  
```  
  
## <a name="sample-output"></a>示例输出  
  
```  
Attributes on Base Class:  
A1  
A2  
Attributes on Derived Class:  
A3  
A3  
A2  
```  
  
## <a name="see-also"></a>请参见  
 <xref:System.Attribute></xref:System.Attribute>   
 <xref:System.Reflection></xref:System.Reflection>   
 [Visual Basic 编程指南](../../../../visual-basic/programming-guide/index.md)   
 [属性](https://msdn.microsoft.com/library/5x6cd29c)   
 [反射 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/reflection.md)   
 [特性 (Visual Basic)](../../../../visual-basic/language-reference/attributes.md)   
 [创建自定义特性 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/attributes/creating-custom-attributes.md)   
 [使用反射 (Visual Basic 中) 访问特性](../../../../visual-basic/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md)
