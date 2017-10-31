---
title: "对已声明的元素 (Visual Basic 中) 的引用 |Microsoft 文档"
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
- declared elements
- references, declared elements
- qualified names
ms.assetid: d6301709-f4cc-4b7a-b8ba-80898f14ab46
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
ms.openlocfilehash: 48a04f81075accc073b0d1f5b7a61006bef807ae
ms.lasthandoff: 03/13/2017

---
# <a name="references-to-declared-elements-visual-basic"></a>对已声明元素的引用 (Visual Basic)
如果代码引用已声明元素[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]编译器中引用与该名称的相应声明的名称匹配。 如果多个元素声明具有相同的名称，则可以控制哪些元素是由引用*限定*其名称。  
  
 编译器将尝试匹配对具有的名称声明的名称引用*最小范围*。 这意味着它以进行引用的代码开始并向外扩展到后续的包含元素的级别。  
  
 下面的示例演示对具有相同名称的两个变量的引用。 此示例声明两个变量中，每个命名为`totalCount`，模块中的作用域的不同级别`container`。 当该过程`showCount`显示`totalCount`无需限定即可，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]编译器将对具有最小范围，即内的局部声明的声明的引用解析`showCount`。 当它鉴定`totalCount`用包含模块`container`，则编译器将解析对具有范围更广的声明的引用。  
  
```vb  
' Assume these two modules are both in the same assembly.  
Module container  
    Public totalCount As Integer = 1  
    Public Sub showCount()  
        Dim totalCount As Integer = 6000  
        ' The following statement displays the local totalCount (6000).  
        MsgBox("Unqualified totalCount is " & CStr(totalCount))  
        ' The following statement displays the module's totalCount (1).  
        MsgBox("container.totalCount is " & CStr(container.totalCount))  
    End Sub  
End Module  
Module callingModule  
    Public Sub displayCount()  
        container.showCount()  
        ' The following statement displays the containing module's totalCount (1).  
        MsgBox("container.totalCount is " & CStr(container.totalCount))  
    End Sub  
End Module  
```  
  
## <a name="qualifying-an-element-name"></a>符合条件的元素名称  
 如果您想要覆盖此搜索过程，并指定一个名称声明在更广泛的范围内，您必须*限定*用范围更广的包含元素的名称。 在某些情况下，您可能还需要限定包含元素。  
  
 限定名称意味着前在源语句替换为标识定义目标元素的位置的信息。 此信息称为*限定字符串*。 它可以包含一个或多个命名空间和一个模块、 类或结构。  
  
 模块、 类或结构，它包含目标元素，应明确地指定限定字符串。 容器又可能位于另一个包含元素，通常是命名空间。 您可能需要在限定字符串中包含多个包含元素。  
  
#### <a name="to-access-a-declared-element-by-qualifying-its-name"></a>通过限定其名称来访问已声明的元素  
  
1.  确定在其中定义该元素的位置。 这可能包括命名空间中或甚至命名空间的层次结构。 在最低级别命名空间中，该元素必须包含在模块、 类或结构。  
  
    ```vb  
    ' Assume the following hierarchy exists outside your code.  
    Namespace outerSpace  
        Namespace innerSpace  
            Module holdsTotals  
                Public Structure totals  
                    Public thisTotal As Integer  
                    Public Shared grandTotal As Long  
                End Structure  
            End Module  
        End Namespace  
    End Namespace  
    ```  
  
2.  确定基于目标元素的位置的限定路径。 具有最高级别的命名空间、 进入最低级别的命名空间，以开头和结尾模块、 类或结构，它包含目标元素。 在路径中的每个元素必须包含它后面的元素。  
  
     `outerSpace` → `innerSpace` → `holdsTotals` → `totals`  
  
3.  准备目标元素的限定字符串。 放置一个句点 (`.`) 的路径中每个元素的后面。 限定字符串中，您的应用程序必须具有对每个元素的访问。  
  
    ```vb  
    outerSpace.innerSpace.holdsTotals.totals.  
    ```  
  
4.  编写的表达式或赋值语句以正常方式引用的目标元素。  
  
    ```vb  
    grandTotal = 9000  
    ```  
  
5.  目标元素的限定字符串名前面放置。 名称应紧跟在段 (`.`) 后面模块、 类或结构，它包含的元素。  
  
    ```vb  
    ' Assume the following module is part of your code.  
    Module accessGrandTotal  
        Public Sub setGrandTotal()  
            outerSpace.innerSpace.holdsTotals.totals.grandTotal = 9000  
        End Sub  
    End Module  
    ```  
  
6.  编译器使用限定字符串来查找可与目标元素引用匹配的清晰、 明确声明。  
  
 您可能需要限定名称引用，如果您的应用程序有权访问多个编程元素具有相同的名称。 例如，<xref:System.Windows.Forms>和<xref:System.Web.UI.WebControls>这两个命名空间包含具有`Label`类 (<xref:System.Windows.Forms.Label?displayProperty=fullName>和<xref:System.Web.UI.WebControls.Label?displayProperty=fullName>)。</xref:System.Web.UI.WebControls.Label?displayProperty=fullName> </xref:System.Windows.Forms.Label?displayProperty=fullName> </xref:System.Web.UI.WebControls> </xref:System.Windows.Forms> 如果您的应用程序使用这两种，或者如果定义了自己`Label`类中，您必须区分不同`Label`对象。 在变量声明中包括的命名空间或导入别名。 下面的示例使用导入别名。  
  
```vb  
' The following statement must precede all your declarations.  
Imports win = System.Windows.Forms, web = System.Web.UI.WebControls  
' The following statement references the Windows.Forms.Label class.  
Dim winLabel As New win.Label()  
```  
  
## <a name="members-of-other-containing-elements"></a>其他包含的元素的成员  
 当您使用的非共享另一个类或结构的成员时，必须首先限定成员名称的变量或表达式来指向类或结构的实例。 在下面的示例中，`demoClass`是一个名为类的实例`class1`。  
  
```vb  
Dim demoClass As class1 = New class1()  
demoClass.someSub[(argumentlist)]  
```  
  
 不能使用自身的类名来限定成员不可[共享](../../../../visual-basic/language-reference/modifiers/shared.md)。 您必须首先创建对象变量中的一个实例 (在这种情况下`demoClass`)，然后通过变量的名称引用它。  
  
 如果类或结构具有`Shared`成员，您可以限定该成员类或结构名称或者用变量或表达式来指向实例。  
  
 模块不具有任何单独的实例，并且所有成员都是`Shared`默认情况下。 因此，您有资格具有模块名称的模块成员。  
  
 下面的示例显示了对模块成员过程的限定的引用。 此示例声明两个`Sub`过程，其名称`perform`，在项目中的不同模块中。 每个可以指定无需限定即可在其自己的模块内，但必须是限定，如果从其他位置引用。 因为最后一个引用在`module3`没有资格`perform`，编译器无法解析该引用。  
  
```vb  
' Assume these three modules are all in the same assembly.  
Module module1  
    Public Sub perform()  
        MsgBox("module1.perform() now returning")  
    End Sub  
End Module  
Module module2  
    Public Sub perform()  
        MsgBox("module2.perform() now returning")  
    End Sub  
    Public Sub doSomething()  
        ' The following statement calls perform in module2, the active module.  
        perform()  
        ' The following statement calls perform in module1.  
        module1.perform()  
    End Sub  
End Module  
Module module3  
    Public Sub callPerform()  
        ' The following statement calls perform in module1.  
        module1.perform()  
        ' The following statement makes an unresolvable name reference  
        ' and therefore generates a COMPILER ERROR.  
        perform() ' INVALID statement  
    End Sub  
End Module  
```  
  
## <a name="references-to-projects"></a>对项目的引用  
 若要使用[公共](../../../../visual-basic/language-reference/modifiers/public.md)在另一个项目中定义的元素，则必须首先设置*引用*对该项目的程序集或类型库。 若要设置的引用，请单击**添加引用**上**项目**菜单上或使用[/reference (Visual Basic 中)](../../../../visual-basic/reference/command-line-compiler/reference.md)命令行编译器选项。  
  
 例如，可以使用的 XML 对象模型的[!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)]。 如果您将一个引用设置为<xref:System.Xml>命名空间中，您可以声明和使用的任何类，如<xref:System.Xml.XmlDocument>。</xref:System.Xml.XmlDocument> </xref:System.Xml> 下面的示例使用<xref:System.Xml.XmlDocument>。</xref:System.Xml.XmlDocument>  
  
```vb  
' Assume this project has a reference to System.Xml  
' The following statement creates xDoc as an XML document object.  
Dim xDoc As System.Xml.XmlDocument  
```  
  
## <a name="importing-containing-elements"></a>导入包含元素  
 您可以使用[Imports 语句 （.NET Namespace 和类型）](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)到*导入*包含模块或你想要使用的类的命名空间。 这使您可以引用在导入的命名空间中定义没有完全限定它们的名称元素。 下面的示例重写前面的示例，若要导入<xref:System.Xml>命名空间。</xref:System.Xml>  
  
```vb  
' Assume this project has a reference to System.Xml  
' The following statement must precede all your declarations.  
Imports System.Xml  
' The following statement creates xDoc as an XML document object.  
Dim xDoc As XmlDocument  
```  
  
 此外，`Imports`语句还可以定义*导入别名*每个导入的命名空间。 这会使源代码更短且更易于阅读。 下面的示例重写前面的示例使用`xD`的别名作为<xref:System.Xml>命名空间。</xref:System.Xml>  
  
```vb  
' Assume this project has a reference to System.Xml  
' The following statement must precede all your declarations.  
Imports xD = System.Xml  
' The following statement creates xDoc as an XML document object.  
Dim xDoc As xD.XmlDocument  
```  
  
 `Imports`语句不会将其他项目中的元素提供给您的应用程序。 也就是说，它不会对引用的设置的位置。 只需导入命名空间使得不再需要限定该命名空间中定义的名称。  
  
 您还可以使用`Imports`语句导入模块、 类、 结构和枚举。 然后可以使用此类导入的元素，而无需限定的成员。 但是，您必须始终限定类和结构的变量或表达式的计算结果为类或结构的实例与非共享的的成员。  
  
## <a name="naming-guidelines"></a>命名准则  
 如果定义了两个或多个具有相同名称的编程元素*名称多义性*可能会导致当编译器尝试解析该名称的引用。 如果有多个定义位于范围内，或者如果没有定义作用域中，引用是无法解析。 有关示例，请参阅此帮助页上的"限定引用示例"。  
  
 通过提供唯一的名称的所有元素，可以避免名称多义性。 然后您可以对任何元素的引用而无需限定其名称与命名空间、 模块或类。 您还可以减少意外引用错误的元素的可能性。  
  
## <a name="shadowing"></a>隐藏的比较  
 当两个编程元素共享相同的名称时，可以隐藏其中之一，或*阴影*，另一个。 隐藏的元素不能引用;相反，当您的代码使用隐藏的元素名称、[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]编译器将其解析为隐藏元素。 有关使用示例更详细说明，请参阅[Visual Basic 中的隐藏](../../../../visual-basic/programming-guide/language-features/declared-elements/shadowing.md)。  
  
## <a name="see-also"></a>另请参阅  
 [已声明的元素名称](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)   
 [已声明的元素的特性](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)   
 [NIB 如何︰ 修改项目属性和配置设置](http://msdn.microsoft.com/en-us/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)   
 [变量](../../../../visual-basic/programming-guide/language-features/variables/index.md)   
 [Imports 语句（.NET 命名空间和类型）](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)   
 [New 运算符](../../../../visual-basic/language-reference/operators/new-operator.md)   
 [Public](../../../../visual-basic/language-reference/modifiers/public.md)
