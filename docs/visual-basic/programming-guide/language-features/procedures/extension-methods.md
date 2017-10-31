---
title: "扩展方法 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.ExtensionMethods
dev_langs:
- VB
helpviewer_keywords:
- extending data types
- extension methods [Visual Basic]
ms.assetid: b8020aae-374d-46a9-bcb7-8cc2390b93b6
caps.latest.revision: 41
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
ms.openlocfilehash: 381fa0db2d92590d23ebd71a7823a8465e94a6e6
ms.lasthandoff: 03/13/2017

---
# <a name="extension-methods-visual-basic"></a>扩展方法 (Visual Basic)
扩展方法使开发人员能够将自定义功能添加到已定义而无需创建新的派生的类型的数据类型。 扩展方法使您可以用来编写，就好像从现有的类型的实例方法可以调用的方法。  
  
## <a name="remarks"></a>备注  
 只能是一个扩展方法`Sub`过程或`Function`过程。 不能定义扩展属性、 字段或事件。 所有扩展方法都必须都标记为扩展属性`<Extension()>`从<xref:System.Runtime.CompilerServices?displayProperty=fullName>命名空间。</xref:System.Runtime.CompilerServices?displayProperty=fullName>  
  
 扩展方法定义中的第一个参数指定该方法将扩展的数据类型。 该方法运行时，第一个参数是绑定到调用方法的数据类型的实例。  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>描述  
 下面的示例定义`Print`扩展<xref:System.String>数据类型。</xref:System.String> 该方法使用`Console.WriteLine`来显示的字符串。 参数`Print`方法， `aString`，建立方法扩展<xref:System.String>类。</xref:System.String>  
  
 [!code-vb[VbVbalrExtensionMethods #&1;](./codesnippet/VisualBasic/extension-methods_1.vb)]  
  
 请注意，与扩展特性标记扩展方法定义`<Extension()>`。 将标记在其中定义该方法的模块是可选的但必须标记每个扩展方法。 <xref:System.Runtime.CompilerServices>必须导入才能访问扩展属性。</xref:System.Runtime.CompilerServices>  
  
 可以仅在模块中声明的扩展方法。 通常情况下，在其中定义的扩展方法的模块不可调用它的一个相同的模块。 相反，包含扩展方法是导入的模块，如果需要以使其进入作用域。 在包含该模块后`Print`是在作用域，就好像不采用参数，如的普通实例方法可以调用该方法`ToUpper`:  
  
 [!code-vb[VbVbalrExtensionMethods #&2;](./codesnippet/VisualBasic/extension-methods_2.vb)]  
  
 下面的示例`PrintAndPunctuate`，也是一个扩展<xref:System.String>，这次使用两个参数定义。</xref:System.String> 第一个参数， `aString`，建立扩展方法扩展<xref:System.String>。</xref:System.String> 第二个参数， `punc`，旨在标点符号的字符串，它在作为参数传递时调用的方法。 该方法显示跟标点符号的字符串。  
  
 [!code-vb[VbVbalrExtensionMethods #&3;](./codesnippet/VisualBasic/extension-methods_3.vb)]  
  
 该方法由发送中的字符串参数调用`punc`:`example.PrintAndPunctuate(".")`  
  
 下面的示例演示`Print`和`PrintAndPunctuate`定义和调用。 <xref:System.Runtime.CompilerServices>将以导入定义模块以启用扩展属性的访问权限。</xref:System.Runtime.CompilerServices>  
  
### <a name="code"></a>代码  
  
```vb  
Imports System.Runtime.CompilerServices  
  
Module StringExtensions  
  
    <Extension()>   
    Public Sub Print(ByVal aString As String)  
        Console.WriteLine(aString)  
    End Sub  
  
    <Extension()>   
    Public Sub PrintAndPunctuate(ByVal aString As String,   
                                 ByVal punc As String)  
        Console.WriteLine(aString & punc)  
    End Sub  
  
End Module  
```  
  
 接下来，扩展方法置于范围中，调用。  
  
```vb  
Imports ConsoleApplication2.StringExtensions  
Module Module1  
  
    Sub Main()  
  
        Dim example As String = "Example string"  
        example.Print()  
  
        example = "Hello"  
        example.PrintAndPunctuate(".")  
        example.PrintAndPunctuate("!!!!")  
  
    End Sub  
End Module  
```  
  
### <a name="comments"></a>注释  
 来说，只需要能够运行这些或类似的扩展方法是，它们是在作用域中。 如果模块包含扩展方法的方法是在作用域中，它在 IntelliSense 中可见，并可以像调用的普通实例方法那样调用。  
  
 请注意，这些方法调用中时，未发送任何参数第一个参数。 参数`aString`在前一种方法中定义绑定到`example`，实例`String`调用的。 编译器将使用`example`作为参数发送到第一个参数。  
  
 如果对设置为对象调用扩展方法时`Nothing`，扩展方法执行。 这不适用于普通实例方法。 您可以显式地检查`Nothing`扩展方法中。  
  
## <a name="types-that-can-be-extended"></a>可以扩展的类型  
 您可以针对可能出现在 Visual Basic 参数列表，其中包括以下的大多数类型定义的扩展方法︰  
  
-   类 （引用类型）  
  
-   结构 （值类型）  
  
-   接口  
  
-   委托  
  
-   ByRef 和 ByVal 参数  
  
-   泛型方法的参数  
  
-   数组  
  
 第一个参数指定的数据类型的扩展方法扩展，因为它是必需的不能是可选的。 由于这个原因，`Optional`参数和`ParamArray`参数不能是参数列表中的第一个参数。  
  
 扩展方法不会考虑在后期绑定中。 在下面的示例中，该语句`anObject.PrintMe()`引发<xref:System.MissingMemberException>异常，而相同的异常时将看到第二个`PrintMe`扩展方法定义已删除。</xref:System.MissingMemberException>  
  
 [!code-vb[VbVbalrExtensionMethods #&9;](./codesnippet/VisualBasic/extension-methods_4.vb)]  
  
## <a name="best-practices"></a>最佳做法  
 扩展方法提供便利和功能强大的方式来扩展现有类型。 但是，若要成功使用，还是有一些需要考虑的要点。 这些注意事项主要适用于作者的类库，但它们可能会影响使用扩展方法的任何应用程序。  
  
 大多数情况下，您将添加到不属于您的类型的扩展方法是添加到您控制的类型的扩展方法比更易受到攻击。 多种情况可能不属于您的类中可能会影响您的扩展方法。  
  
-   如果存在任何可访问的实例成员都与从参数所需参数不收缩转换中调用的语句中，用参数兼容的签名，将优先于任何扩展方法使用实例方法。 因此，如果相应的实例方法添加到在某一时刻的类，您依赖于某个现有扩展成员变得不可访问。  
  
-   扩展方法的作者不能防止其他程序员编写冲突的扩展方法可能优先于原来的扩展名。  
  
-   可以通过扩展方法置于自己的命名空间来提高可靠性。 您的库的使用者可以包含命名空间或排除它，或在命名空间，独立于库的其余部分之间选择。  
  
-   它可能会比要扩展类，特别是如果您不拥有接口或类扩展接口更安全。 在接口中的更改会影响每个类来实现它。 因此，作者不大可能要添加或更改接口中的方法。 但是，如果类实现具有相同签名的扩展方法的两个接口，扩展方法都不是可见的。  
  
-   扩展可以最具体的类型。 在类型的层次结构，如果您选择从中派生的许多其他类型，类型有一些图层的实例方法或其他可能会影响您的扩展方法引入的可能性。  
  
## <a name="extension-methods-instance-methods-and-properties"></a>扩展方法、 实例方法和属性  
 当范围内实例方法具有与调用的语句的参数兼容的签名时，将任何扩展方法优先选择的实例方法。 实例方法具有优先级，即使扩展方法是更好的匹配。 在下面的示例中，`ExampleClass`包含名为实例方法`ExampleMethod`它具有一个参数类型的`Integer`。 扩展方法`ExampleMethod`扩展`ExampleClass`，并且具有一个类型的参数`Long`。  
  
 [!code-vb[VbVbalrExtensionMethods #&4;](./codesnippet/VisualBasic/extension-methods_5.vb)]  
  
 首次调用`ExampleMethod`下面的代码中调用扩展方法，因为`arg1`是`Long`和仅与兼容`Long`扩展方法中的参数。 第二次调用`ExampleMethod`具有`Integer`参数， `arg2`，它会调用实例方法。  
  
 [!code-vb[VbVbalrExtensionMethods #&5;](./codesnippet/VisualBasic/extension-methods_6.vb)]  
  
 现在反转中这两种方法的参数的数据类型︰  
  
 [!code-vb[VbVbalrExtensionMethods #&6;](./codesnippet/VisualBasic/extension-methods_7.vb)]  
  
 这次中的代码`Main`两次都调用实例方法。 这是因为两者`arg1`和`arg2`都可以扩大转换为`Long`，并与实例方法优先于这两种情况中的扩展方法。  
  
 [!code-vb[VbVbalrExtensionMethods #&7;](./codesnippet/VisualBasic/extension-methods_8.vb)]  
  
 因此，扩展方法不能替换现有的实例方法。 但是，如果扩展方法具有相同的名称作为实例方法，但这些签名不会发生冲突，则这两种方法可以访问。 例如，如果类`ExampleClass`包含一个名为方法`ExampleMethod`不采用任何参数、 扩展方法具有相同名称但不同的签名允许的如下面的代码中所示。  
  
 [!code-vb[VbVbalrExtensionMethods #&8;](./codesnippet/VisualBasic/extension-methods_9.vb)]  
  
 此代码的输出是，如下所示︰  
  
 `Extension method`  
  
 `Instance method`  
  
 这种情况是要简单的属性︰ 如果扩展方法具有相同的名称作为它所扩展的类的属性，扩展方法是不可见的并且不能访问。  
  
## <a name="extension-method-precedence"></a>扩展方法优先级  
 作用域中并且可以访问两个具有相同的签名的扩展方法时，将调用一个具有更高的优先级。 扩展方法的优先级取决于用来将该方法引入作用域的机制。 以下列表显示了优先级层次结构中的，从高到最低。  
  
1.  在当前模块中定义的扩展方法。  
  
2.  扩展方法数据类型内定义在当前命名空间或其任何一个的父与子命名空间具有优先权要高于父命名空间。  
  
3.  在任何类型的导入在当前文件中定义的扩展方法。  
  
4.  在任何命名空间导入当前文件中定义的扩展方法。  
  
5.  在任何项目级别类型 imports 语句中定义的扩展方法。  
  
6.  在任何项目级别命名空间导入定义的扩展方法。  
  
 如果优先级不能解决多义性问题，可以使用完全限定的名来指定要调用的方法。 如果`Print`在前面的示例中的方法定义一个名为模块中`StringExtensions`，完全限定的名是`StringExtensions.Print(example)`而不是`example.Print()`。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Runtime.CompilerServices></xref:System.Runtime.CompilerServices>   
 <xref:System.Runtime.CompilerServices.ExtensionAttribute></xref:System.Runtime.CompilerServices.ExtensionAttribute>   
 [扩展方法](../../../../csharp/programming-guide/classes-and-structs/extension-methods.md)   
 [Module 语句](../../../../visual-basic/language-reference/statements/module-statement.md)   
 [过程参数和变量](./procedure-parameters-and-arguments.md)   
 [可选参数](./optional-parameters.md)   
 [参数数组](./parameter-arrays.md)   
 [属性概述](../../../../visual-basic/programming-guide/concepts/attributes/index.md)   
 [在 Visual Basic 中的作用域](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)
