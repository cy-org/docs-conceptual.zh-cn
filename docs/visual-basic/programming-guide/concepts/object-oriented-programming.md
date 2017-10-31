---
title: "面向对象编程 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: 49794de4-64c3-473c-b8ed-fe98835df69c
caps.latest.revision: 4
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: d5491b3bd5a25908194d02063f688a319509bb77
ms.lasthandoff: 03/13/2017

---
# <a name="object-oriented-programming-visual-basic"></a>面向对象编程 (Visual Basic)
Visual Basic 提供完全支持面向对象的编程，包括封装、 继承和多态性。  
  
 *封装*意味着将一组相关的属性、 方法和其他成员视为一个单元或对象。  
  
 *继承*描述创建基于现有类的新类的能力。  
  
 *多态性*意味着您可以有多个可互换使用，使用的类，即使每个类以不同方式实现相同属性或方法。  
  
 本节介绍下列概念：  
  
-   [类和对象](#Classes)  
  
    -   [类成员](#Members)  
  
         [属性和字段](#Properties)  
  
         [方法](#Methods)  
  
         [构造函数](#Constructors)  
  
         [析构函数](#Destructors)  
  
         [事件](#Events)  
  
         [嵌套的类](#NestedClasses)  
  
    -   [访问修饰符和访问级别](#AccessModifiers)  
  
    -   [实例化类](#InstantiatingClasses)  
  
    -   [共享的类和成员](#Static)  
  
    -   [匿名类型](#AnonymousTypes)  
  
-   [继承](#Inheritance)  
  
    -   [重写成员](#Overriding)  
  
-   [接口](#Interfaces)  
  
-   [泛型](#Generics)  
  
-   [委托](#Delegates)  
  
##  <a name="Classes"></a>类和对象  
 这些条款*类*和*对象*有时会用到互换使用，但实际上，类描述*类型*对象，而对象是可用的*实例*的类。 因此，创建一个对象的操作称为*实例化*。 如果使用蓝图类比，类是蓝图，对象就是基于该蓝图的建筑。  
  
 定义类：  
  
```vb  
Class SampleClass  
End Class  
```  
  
 Visual Basic 还提供了类，名为的轻量版本*结构*时您需要创建大量对象并执行一些有用不想为此，消耗过多内存。  
  
 定义结构：  
  
```vb  
Structure SampleStructure  
End Structure  
```  
  
 有关详细信息，请参见:  
  
-   [Class 语句](../../../visual-basic/language-reference/statements/class-statement.md)  
  
-   [Structure 语句](../../../visual-basic/language-reference/statements/structure-statement.md)  
  
###  <a name="Members"></a>类成员  
 每个类都可以具有不同*类成员*包括描述了类数据、 定义类行为的方法和事件提供不同的类和对象之间的通信的属性。  
  
####  <a name="Properties"></a>属性和字段  
 字段和属性表示对象包含的信息。 字段类似于变量，因为可以直接读取或设置它们。  
  
 定义字段：  
  
```vb  
Class SampleClass  
    Public SampleField As String  
End Class  
```  
  
 属性具有 get 和 set 过程，它们对如何设置或返回值提供更多的控制。  
  
 Visual Basic 允许您创建私有字段来存储属性值，或者使用所谓自动实现的属性创建此字段自动在后台，并为属性过程提供基本逻辑。  
  
 定义自动实现的属性：  
  
```vb  
Class SampleClass  
    Public Property SampleProperty as String  
End Class  
```  
  
 如果你需要执行一些其他操作来读取和写入属性值，请定义一个用于存储属性值的字段，并提供用于存储和检索该字段的基本逻辑：  
  
```vb  
Class SampleClass  
    Private m_Sample As String  
    Public Property Sample() As String  
        Get  
            ' Return the value stored in the field.  
            Return m_Sample  
        End Get  
        Set(ByVal Value As String)  
            ' Store the value in the field.  
            m_Sample = Value  
        End Set  
    End Property  
End Class  
```  
  
 大多数属性的方法或过程都是既可以设置也可以获取属性值。 但你可以创建只读或只写属性来限制对它们的修改或读取。 在 Visual Basic 中，可以使用 `ReadOnly` 和 `WriteOnly` 关键字。 但是，自动实现的属性不能为只读或只写。  
  
 有关详细信息，请参见:  
  
-   [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)  
  
-   [Get 语句](../../../visual-basic/language-reference/statements/get-statement.md)  
  
-   [Set 语句](../../../visual-basic/language-reference/statements/set-statement.md)  
  
-   [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)  
  
-   [WriteOnly](../../../visual-basic/language-reference/modifiers/writeonly.md)  
  
####  <a name="Methods"></a>方法  
 一个*方法*是对象可以执行的操作。  
  
> [!NOTE]
>  在 Visual Basic 中，方法的创建途径有两种：如果方法不返回值，可使用 `Sub` 语句；如果方法返回值，可使用 `Function` 语句。  
  
 定义类的方法：  
  
```vb  
Class SampleClass  
    Public Function SampleFunc(ByVal SampleParam As String)  
        ' Add code here  
    End Function  
End Class  
```  
  
 一个类可以有多个实现，或*重载*，不同数量的参数或参数类型的相同方法。  
  
 重载方法：  
  
```vb  
Overloads Sub Display(ByVal theChar As Char)  
    ' Add code that displays Char data.  
End Sub  
Overloads Sub Display(ByVal theInteger As Integer)  
    ' Add code that displays Integer data.  
End Sub  
```  
  
 大多数情况下，方法是在类定义中声明的。 但是，Visual Basic 还支持*扩展方法*可用于将方法添加到现有类之外的类的实际定义。  
  
 有关详细信息，请参见:  
  
-   [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)  
  
-   [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
-   [重载](../../../visual-basic/language-reference/modifiers/overloads.md)  
  
-   [扩展方法](../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)  
  
####  <a name="Constructors"></a>构造函数  
 构造函数一种类方法，它们在创建给定类型的对象时自动执行。 构造函数通常用于初始化新对象的数据成员。 构造函数只能在创建类时运行一次。 此外，构造函数中的代码始终在类中所有其他代码之前运行。 但是，你可以按照为任何其他方法创建重载的方式，创建多个构造函数重载。  
  
 定义类的构造函数：  
  
```vb  
Class SampleClass  
    Sub New(ByVal s As String)  
        // Add code here.  
    End Sub  
End Class  
```  
  
 有关详细信息，请参阅︰[对象生存期︰ 对象的方式创建和破坏](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)。  
  
####  <a name="Destructors"></a>析构函数  
 析构函数用于析构类的实例。 在 .NET Framework 中，垃圾回收器自动管理应用程序中托管对象的内存分配和释放。 但是，你可能仍会需要析构函数来清理应用程序创建的所有非托管资源。 一个类只能有一个析构函数。  
  
 有关析构函数和.NET Framework 中的垃圾回收的详细信息，请参阅[垃圾回收](../../../standard/garbagecollection/index.md)。  
  
####  <a name="Events"></a>事件  
 类或对象可以通过事件向其他类或对象通知发生的相关事情。 发送 （或引发） 事件的类称为*publisher*和接收 （或处理） 事件的类称为*订户*。 有关事件的详细信息，如何引发和处理，请参阅[事件](http://msdn.microsoft.com/library/b6f65241-e0ad-4590-a99f-200ce741bb1f)。  
  
-   若要声明事件，请使用[Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)。  
  
-   若要引发事件，请使用[RaiseEvent 语句](../../../visual-basic/language-reference/statements/raiseevent-statement.md)。  
  
-   若要指定事件处理程序声明的方式，使用[WithEvents](../../../visual-basic/language-reference/modifiers/withevents.md)语句和[处理](../../../visual-basic/language-reference/statements/handles-clause.md)子句。  
  
-   若要能够动态地添加、 删除和更改与事件关联的事件处理程序，使用[AddHandler 语句](../../../visual-basic/language-reference/statements/addhandler-statement.md)和[RemoveHandler 语句](../../../visual-basic/language-reference/statements/removehandler-statement.md)连同[AddressOf 运算符](../../../visual-basic/language-reference/operators/addressof-operator.md)。  
  
####  <a name="NestedClasses"></a>嵌套的类  
 另一个类中定义的类被称为*嵌套*。 默认情况下，嵌套类是私有类。  
  
```vb  
Class Container  
    Class Nested  
    ' Add code here.  
    End Class  
End Class  
```  
  
 若要创建嵌套类的实例，请使用容器类的名称，后接一个点，再接嵌套类的名称：  
  
```vb  
Dim nestedInstance As Container.Nested = New Container.Nested()  
```  
  
###  <a name="AccessModifiers"></a>访问修饰符和访问级别  
 所有类和类成员可以都指定自己为其他类提供通过使用何种访问级别*访问修饰符*。  
  
 可用的访问修饰符有以下这些：  
  
|Visual Basic 修饰符|定义|  
|---------------------------|----------------|  
|[Public](../../../visual-basic/language-reference/modifiers/public.md)|同一程序集中的任何其他代码或引用该程序集的其他程序集都可以访问该类型或成员。|  
|[Private](../../../visual-basic/language-reference/modifiers/private.md)|只有同一类中的代码可以访问该类型或成员。|  
|[Protected](../../../visual-basic/language-reference/modifiers/protected.md)|只有同一类或派生类中的代码可以访问该类型或成员。|  
|[Friend](../../../visual-basic/language-reference/modifiers/friend.md)|同一程序集中的任何代码都可以访问该类型或成员，但其他程序集中的代码不可以。|  
|`Protected Friend`|同一程序集中的任何代码或其他程序集中的任何派生类都可以访问该类型或成员。|  
  
 有关详细信息，请参阅[Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。  
  
###  <a name="InstantiatingClasses"></a>实例化类  
 若要创建对象，你需要实例化类，即创建类实例。  
  
```vb  
Dim sampleObject as New SampleClass()  
```  
  
 实例化类之后，可以为该实例的属性和字段赋值，还可以调用类方法。  
  
```vb  
' Set a property value.  
sampleObject.SampleProperty = "Sample String"  
' Call a method.  
sampleObject.SampleMethod()  
```  
  
 若要在类的实例化过程中为属性赋值，请使用对象初始值设定项：  
  
```vb  
Dim sampleObject = New SampleClass With   
    {.FirstProperty = "A", .SecondProperty = "B"}  
```  
  
 有关详细信息，请参见:  
  
-   [New 运算符](../../../visual-basic/language-reference/operators/new-operator.md)  
  
-   [对象初始值设定项：命名类型和匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)  
  
###  <a name="Static"></a>共享的类和成员  
 共享的类的成员是属性、 过程或字段，它由类的所有实例共享。  
  
 若要定义一个共享的成员︰  
  
```vb  
Class SampleClass  
    Public Shared SampleString As String = "Sample String"  
End Class  
```  
  
 若要访问共享的成员，而无需创建此类的对象使用的类名称︰  
  
```vb  
MsgBox(SampleClass.SampleString)  
```  
  
 在 Visual Basic 中的共享的模块具有共享仅限成员，并且不能实例化。 共享的成员也不能访问非共享属性、 字段或方法  
  
 有关详细信息，请参见:  
  
-   [Shared](../../../visual-basic/language-reference/modifiers/shared.md)  
  
-   [Module 语句](../../../visual-basic/language-reference/statements/module-statement.md)  
  
###  <a name="AnonymousTypes"></a>匿名类型  
 匿名类型使你无需为数据类型编写类定义即可创建对象。 此时，编译器将为你生成类。 该类没有可使用的名称，且包含在声明对象时指定的属性。  
  
 创建匿名类型的实例：  
  
```vb  
' sampleObject is an instance of a simple anonymous type.  
Dim sampleObject =   
    New With {Key .FirstProperty = "A", .SecondProperty = "B"}  
```  
  
 有关详细信息，请参阅︰[匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)。  
  
##  <a name="Inheritance"></a>继承  
 通过继承，可以创建一个新类，它重用、扩展和修改另一个类中定义的行为。 其成员被继承的类称为*基类*，继承这些成员的类称为*派生类*。 但是，在 Visual Basic 中的所有类隐式都继承自<xref:System.Object>类，该类支持.NET 类层次结构并向所有类提供低级服务。</xref:System.Object>  
  
> [!NOTE]
>  Visual Basic 不支持多重继承。 也就是说，可以指定为派生类只有一个基类。  
  
 从基类继承：  
  
```vb  
Class DerivedClass  
    Inherits BaseClass  
End Class  
```  
  
 默认情况下，可以继承所有类。 但你可以指定不得将某个类用作基类，也可以创建只能用作基类的类。  
  
 指定不得将某个类用作基类：  
  
```vb  
NotInheritable Class SampleClass  
End Class  
```  
  
 指定只能用作基类且无法实例化的类：  
  
```vb  
MustInherit Class BaseClass  
End Class  
```  
  
 有关详细信息，请参见:  
  
-   [Inherits 语句](../../../visual-basic/language-reference/statements/inherits-statement.md)  
  
-   [NotInheritable](../../../visual-basic/language-reference/modifiers/notinheritable.md)  
  
-   [MustInherit](../../../visual-basic/language-reference/modifiers/mustinherit.md)  
  
###  <a name="Overriding"></a>重写成员  
 默认情况下，派生类继承其基类的所有成员。 若希望更改继承成员的行为，则需要重写该成员。 即，可以在派生类中定义方法、属性或事件的新实现。  
  
 下列修饰符用于控制如何重写属性和方法：  
  
|Visual Basic 修饰符|定义|  
|---------------------------|----------------|  
|[Overridable](../../../visual-basic/language-reference/modifiers/overridable.md)|允许在派生类中重写类成员。|  
|[Overrides](../../../visual-basic/language-reference/modifiers/overrides.md)|重写基类中定义的虚拟（可重写）成员。|  
|[NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md)|禁止在继承类中重写成员。|  
|[MustOverride](../../../visual-basic/language-reference/modifiers/mustoverride.md)|要求在派生类中重写类成员。|  
|[Shadows](../../../visual-basic/language-reference/modifiers/shadows.md)|隐藏继承自基类的成员|  
  
##  <a name="Interfaces"></a>接口  
 和类一样，接口也定义了一系列属性、方法和事件。 但与类不同的是，接口并不提供实现。 它们由类来实现，并从类中被定义为单独的实体。 接口表示一种约定，实现接口的类必须严格按其定义来实现接口的每个方面。  
  
 定义接口：  
  
```vb  
Public Interface ISampleInterface  
    Sub DoSomething()  
End Interface  
```  
  
 在类中实现接口：  
  
```vb  
Class SampleClass  
    Implements ISampleInterface  
    Sub DoSomething  
        ' Method implementation.  
    End Sub  
End Class  
```  
  
 有关详细信息，请参见:  
  
-   [接口](../../../visual-basic/programming-guide/language-features/interfaces/index.md)  
  
-   [Interface 语句](../../../visual-basic/language-reference/statements/interface-statement.md)  
  
-   [Implements 语句](../../../visual-basic/language-reference/statements/implements-statement.md)  
  
##  <a name="Generics"></a>泛型  
 类、 结构、 接口和.NET Framework 中的方法可以包括*类型参数*，用于定义类型的对象，它们可以存储或使用。 最常见的泛型示例是集合，从中可以指定要存储在集合中的对象的类型。  
  
 定义泛型类：  
  
```vb  
Class SampleGeneric(Of T)  
    Public Field As T  
End Class  
```  
  
 创建泛型类的实例：  
  
```vb  
Dim sampleObject As New SampleGeneric(Of String)  
sampleObject.Field = "Sample string"  
```  
  
 有关详细信息，请参见:  
  
-   [泛型](https://msdn.microsoft.com/library/ms172192)  
  
-   [在 Visual Basic 中的泛型类型](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)  
  
##  <a name="Delegates"></a>委托  
 一个*委托*是一种定义方法签名，并可提供具有兼容签名的任何方法的引用。 你可以通过委托调用方法。 委托用于将方法作为参数传递给其他方法。  
  
> [!NOTE]
>  事件处理程序就是通过委托调用的方法。 有关事件处理中使用委托的详细信息，请参阅[事件](http://msdn.microsoft.com/library/b6f65241-e0ad-4590-a99f-200ce741bb1f)。  
  
 创建委托：  
  
```vb  
Delegate Sub SampleDelegate(ByVal str As String)  
```  
  
 创建对与委托指定的签名相匹配的方法的引用：  
  
```vb  
Class SampleClass  
    ' Method that matches the SampleDelegate signature.  
    Sub SampleSub(ByVal str As String)  
        ' Add code here.  
    End Sub  
    ' Method that instantiates the delegate.  
    Sub SampleDelegateSub()  
        Dim sd As SampleDelegate = AddressOf SampleSub  
        sd("Sample string")  
    End Sub  
End Class  
```  
  
 有关详细信息，请参见:  
  
-   [委托](../../../visual-basic/programming-guide/language-features/delegates/index.md)  
  
-   [Delegate 语句](../../../visual-basic/language-reference/statements/delegate-statement.md)  
  
-   [AddressOf 运算符](../../../visual-basic/language-reference/operators/addressof-operator.md)  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 编程指南](../../../visual-basic/programming-guide/index.md)
