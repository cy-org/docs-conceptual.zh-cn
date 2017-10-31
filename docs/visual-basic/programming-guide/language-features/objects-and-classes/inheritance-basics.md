---
title: "继承的基础知识 (Visual Basic 中) |Microsoft 文档"
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
- derived classes, inheritance
- MyClass keyword, using
- MyBase keyword, using
- Inherits statement, inheritance
- overriding, Overridable keyword
- MustInherit keyword, using
- Overrides keyword, using
- inheritance
- MustInherit classes
- MustOverride keyword, using
- classes [Visual Basic], derived
- NotInheritable keyword, using
- base classes, extending properties and methods
- NotOverridable keyword, using
- base classes, inheritance
- abstract classes, inheritance
- overriding, Overrides keyword
ms.assetid: dfc8deba-f5b3-4d1d-a937-7cb826446fc5
caps.latest.revision: 23
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
ms.openlocfilehash: 58aee9f8c348eb06daec2b8c9e332f3f2775bcb6
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="inheritance-basics-visual-basic"></a>继承的基础知识 (Visual Basic)
`Inherits`语句用于声明新类，称为*派生类*，将根据现有的类，称为*基类*。 派生的类继承，并可以扩展属性、 方法、 事件、 字段和基类中定义的常量。 下一节介绍了一些继承规则，并可用于更改方式类修饰符继承或被继承︰  
  
-   默认情况下，所有类都是可继承的除非使用标记`NotInheritable`关键字。 从您的项目中的其他类或你的项目引用其他程序集中的类，类可以继承。  
  
-   与允许多重继承的语言不同[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]允许仅单一继承类中; 也就是说，派生的类可以有一个基类。 虽然类中不允许多重继承，类可以实现多个接口，可以有效地实现同一目的。  
  
-   若要防止公开基类中的受限的项，必须等于或限制性强于其基本类派生的类的访问类型。 例如，`Public`类不能继承`Friend`或`Private`类，和一个`Friend`类不能继承`Private`类。  
  
## <a name="inheritance-modifiers"></a>继承修饰符  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]引入了以下类级语句和修饰符以支持继承︰  
  
-   `Inherits`语句-指定的基类。  
  
-   `NotInheritable`修饰符 — 防止程序员使用类作为基类。  
  
-   `MustInherit`修饰符 — 指定类旨在用作基类的类仅。 实例`MustInherit`不能直接创建类; 它们可以仅创建的派生类作为基类的类实例。 (其他编程语言，如 c + + 和 C# 中，使用术语*抽象类*来描述此类的类。)  
  
## <a name="overriding-properties-and-methods-in-derived-classes"></a>重写属性和方法在派生类中  
 默认情况下，派生的类从其基类继承属性和方法。 如果继承的属性或方法具有不同的行为在派生类中它可以是*中被重写*。 也就是说，您可以在派生类中定义该方法的新实现。 下列修饰符用于控制如何重写属性和方法：  
  
-   `Overridable`-在派生类中重写的类中，允许的属性或方法。  
  
-   `Overrides`— 重写`Overridable`属性或在基类中定义的方法。  
  
-   `NotOverridable`— 防止属性或方法被重写在继承类。 默认情况下，`Public`方法都是`NotOverridable`。  
  
-   `MustOverride`— 要求派生的类重写的属性或方法。 当`MustOverride`关键字用于构成，方法定义由不仅仅是`Sub`， `Function`，或`Property`语句。 不允许任何其他语句，以及具体是有没有`End Sub`或`End Function`语句。 `MustOverride`方法必须声明在`MustInherit`类。  
  
 假设你想要定义类以处理工资单。 您可以定义一个泛型`Payroll`类，该类包含`RunPayroll`普通周计算工资的方法。 然后，可以使用`Payroll`作为基类的更专业`BonusPayroll`类，该类可以分发雇员奖金时使用。  
  
 `BonusPayroll`类可以继承，并重写，`PayEmployee`基类中定义的方法`Payroll`类。  
  
 下面的示例定义一个基类，`Payroll,`和派生的类中， `BonusPayroll`，这会重写继承的方法， `PayEmployee`。 一个过程中， `RunPayroll`、 创建，然后传递`Payroll`对象和一个`BonusPayroll`对象传递给函数， `Pay`，用于执行`PayEmployee`这两个对象的方法。  
  
 [!code-vb[VbVbalrOOP #&28;](../../../../visual-basic/misc/codesnippet/VisualBasic/inheritance-basics_1.vb)]  
  
## <a name="the-mybase-keyword"></a>MyBase 关键字  
 `MyBase`关键字的行为方式类似指的是一个类的当前实例的基类的对象变量。 `MyBase`通常用于访问基类成员被重写或派生类中被隐藏。 具体而言，`MyBase.New`用来从派生的类构造函数中显式调用基类构造函数。  
  
 例如，假设您要设计一个重写从基类继承的方法的派生的类。 重写的方法可以调用基类中的方法和修改返回的值，如下面的代码段中所示︰  
  
 [!code-vb[VbVbalrOOP #&109;](../../../../visual-basic/misc/codesnippet/VisualBasic/inheritance-basics_2.vb)]  
  
 以下列表描述对使用的限制`MyBase`:  
  
-   `MyBase`指直接基类和继承的成员。 不能使用访问`Private`类中的成员。  
  
-   `MyBase`是关键字，而不是真实对象。 `MyBase`不能赋给变量、 传递给过程，或用于`Is`比较。  
  
-   该方法的`MyBase`限定不需要在直接基类; 中定义而可能间接继承的基类中定义。 为了使限定的引用`MyBase`正确编译，一些基类必须包含匹配的名称和类型的调用中出现的参数的方法。  
  
-   不能使用`MyBase`调用`MustOverride`基类方法。  
  
-   `MyBase`不能用于限定本身。 因此，下面的代码不是有效的︰  
  
     `MyBase.MyBase.BtnOK_Click()`  
  
-   `MyBase`不能在模块中使用。  
  
-   `MyBase`不能用于访问基类成员标记为`Friend`类的基类是否在另一个程序集。  
  
 有关详细信息和另一个示例，请参阅[如何︰ 访问被派生类变量隐藏](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-access-a-variable-hidden-by-a-derived-class.md)。  
  
## <a name="the-myclass-keyword"></a>MyClass 关键字  
 `MyClass`关键字的行为方式类似于最初实现的类的当前实例是指的对象变量。 `MyClass`类似于`Me`，但每个方法和属性调用`MyClass`将被视为方法或属性是[NotOverridable](../../../../visual-basic/language-reference/modifiers/notoverridable.md)。 因此，该方法或属性不是受在派生类中重写。  
  
-   `MyClass`是关键字，而不是真实对象。 `MyClass`不能赋给变量、 传递给过程，或用于`Is`比较。  
  
-   `MyClass`指包含类和其继承的成员。  
  
-   `MyClass`可以用作的限定符`Shared`成员。  
  
-   `MyClass`内不能使用`Shared`方法，但是可以在实例方法中用来访问共享的成员的类。  
  
-   `MyClass`不能在标准模块中使用。  
  
-   `MyClass`可以用于限定基类中定义的并且在该类中提供的方法没有实现的方法。 这种引用具有相同的含义为`MyBase.`*方法*。  
  
 下面的示例比较`Me`和`MyClass`。  
  
```vb
Class baseClass  
    Public Overridable Sub testMethod()  
        MsgBox("Base class string")  
    End Sub  
    Public Sub useMe()  
        ' The following call uses the calling class's method, even if   
        ' that method is an override.  
        Me.testMethod()  
    End Sub  
    Public Sub useMyClass()  
        ' The following call uses this instance's method and not any  
        ' override.  
        MyClass.testMethod()  
    End Sub  
End Class  
Class derivedClass : Inherits baseClass  
    Public Overrides Sub testMethod()  
        MsgBox("Derived class string")  
    End Sub  
End Class  
Class testClasses  
    Sub startHere()  
        Dim testObj As derivedClass = New derivedClass()  
        ' The following call displays "Derived class string".  
        testObj.useMe()  
        ' The following call displays "Base class string".  
        testObj.useMyClass()  
    End Sub  
End Class  
```  
  
 即使`derivedClass`替代`testMethod`、`MyClass`中的关键字`useMyClass`使无效的重写和编译器解析效果调用基类版本的`testMethod`。  
  
## <a name="see-also"></a>另请参阅  
 [Inherits 语句](../../../../visual-basic/language-reference/statements/inherits-statement.md)   
 [Me、My、MyBase 和 MyClass](../../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)

