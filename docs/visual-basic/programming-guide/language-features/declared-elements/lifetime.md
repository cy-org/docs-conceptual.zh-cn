---
title: "在 Visual Basic 中的生存期 |Microsoft 文档"
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
- static variables, lifetime
- static variables, Visual Basic
- declared elements, lifetime
- Shared variable lifetime
- lifetime, declared elements
- lifetime, Visual Basic
- lifetime
ms.assetid: bd91e390-690a-469a-9946-8dca70bc14e7
caps.latest.revision: 14
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
ms.openlocfilehash: fa0cbdf4a8fe5e8fc41e4e4f373c79451fb7b75f
ms.lasthandoff: 03/13/2017

---
# <a name="lifetime-in-visual-basic"></a>Visual Basic 中的生存期
*生存期*已声明元素的是一段时间期间它是可供使用。 变量是唯一具有生存期的元素。 出于此目的，则编译器会将过程参数和函数返回值视为变量的特殊情况。 变量的生存期表示的时间在此期间，它可以保存一个值。 其值可以更改的生存期内，但它始终包含一些值。  
  
## <a name="different-lifetimes"></a>不同的生存期  
 一个*成员变量*（在模块级别，任何过程之外声明） 通常都有相同的生存期声明它的元素。 声明的类或结构中的非共享的变量作为单独的类或结构声明它的每个实例的副本存在。 每个此类变量具有相同的生存期与它的实例。 但是，`Shared`变量仅有一个生存期，即持续运行您的应用程序的整个时间。  
  
 一个*局部变量*（在过程内声明） 仅在声明它的过程的运行时才存在。 这同样适用于过程的参数和返回任何函数。 但是，如果该过程调用其他过程，本地变量保留其值在被调用的过程运行时。  
  
## <a name="beginning-of-lifetime"></a>生存期的开始  
 当控制权交给声明它的过程时，本地变量的生存期开始。 每个本地变量初始化为其数据类型的默认值，该过程开始时运行。 当该过程中遇到`Dim`语句中指定初始值，它将设置这些变量为这些值，即使您的代码必须对其分配了其他值。  
  
 像它是一个单独的变量，会初始化结构变量的每个成员。 同样，分别初始化数组变量的每个元素。  
  
 过程内部块中声明变量 (如`For`循环) 在进入过程上进行初始化。 曾经执行过代码块，这些初始化生效。  
  
## <a name="end-of-lifetime"></a>生存期结束  
 当一个过程终止时，不保留其本地变量的值，并[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]回收它们的内存。 下次调用该过程，所有本地变量重新创建和重新初始化订阅。  
  
 类或结构的实例终止时，将其非共享的变量会丢失其内存和它们的值。 类或结构的每个新实例创建，并重新初始化其非共享的变量。 但是，`Shared`变量被保留，直到您的应用程序将停止运行。  
  
## <a name="extension-of-lifetime"></a>生存期的扩展  
 如果您声明的局部变量`Static`关键字，它的生存期即比其过程的执行时间更长。 下表显示了过程声明确定多长时间`Static`变量确实存在。  
  
|过程位置与共享|静态变量生存期开始|静态变量的生存期结束|  
|------------------------------------|-------------------------------------|-----------------------------------|  
|（默认情况下共享） 的模块中|第一次调用该过程|在您的应用程序停止运行时|  
|在类中， `Shared` （过程不是实例成员）|第一次调用该过程是对特定实例或者对自身的类或结构名称|在您的应用程序停止运行时|  
|一个类的实例中不`Shared`（过程是一个实例成员）|第一次特定实例调用该过程|当垃圾回收 (GC) 释放该实例|  
  
## <a name="static-variables-of-the-same-name"></a>具有相同名称的静态变量  
 您可以声明具有多个过程中具有相同名称的静态变量。 如果执行此操作，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]编译器会考虑每个此类变量视为一个单独的元素。 其中一个变量的初始化并不影响其他值。 这同样适用于定义一个具有一组重载过程并声明中每个重载具有相同名称的静态变量。  
  
## <a name="containing-elements-for-static-variables"></a>静态变量的包含元素  
 可以在该类中的过程，即声明一个类中的静态局部变量。 但是，不能声明为静态局部变量在结构中，结构成员或该结构内的一个过程的本地变量。  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>说明  
 下面的示例声明的变量[静态](../../../../visual-basic/language-reference/modifiers/static.md)关键字。 (请注意，不需要`Dim`关键字时[Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md)使用修饰符，如`Static`。)  
  
### <a name="code"></a>代码  
 [!code-vb[VbVbalrKeywords #&13;](../../../../visual-basic/language-reference/codesnippet/VisualBasic/lifetime_1.vb)]  
  
### <a name="comments"></a>注释  
 在前面的示例中，该变量`applesSold`会继续保留在过程后面从而`runningTotal`返回到调用代码。 下一次`runningTotal`调用时，`applesSold`保留其以前计算的值。  
  
 如果`applesSold`内容而无需使用已声明`Static`，跨调用的将不会保留以前的累积的值`runningTotal`。 下一次`runningTotal`调用了，`applesSold`本来会被重新创建和初始化为 0，和`runningTotal`将只返回与调用了相同的值。  
  
### <a name="compiling-the-code"></a>编译代码  
 您可以初始化为其声明的一部分的静态局部变量的值。 如果您声明为一系列`Static`，则可以初始化其秩 （维数）、 每个维度的长度和各个元素的值。  
  
### <a name="security"></a>安全性  
 在前面的示例中，您可以通过声明生成相同的生存期`applesSold`在模块级别。 如果发生这种方式更改变量的作用域，但是，该过程将不再具有独占访问。 由于其他过程可以访问`applesSold`和将其值更改、 运行总计可能是不可靠和代码可能会更难维护。  
  
## <a name="see-also"></a>另请参阅  
 [共享](../../../../visual-basic/language-reference/modifiers/shared.md)   
 [执行任何操作](../../../../visual-basic/language-reference/nothing.md)   
 [已声明的元素名称](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)   
 [对已声明的元素的引用](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [在 Visual Basic 中的作用域](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)   
 [在 Visual Basic 中的访问级别](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)   
 [变量](../../../../visual-basic/programming-guide/language-features/variables/index.md)   
 [变量声明](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [数据类型疑难解答](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [Static](../../../../visual-basic/language-reference/modifiers/static.md)
