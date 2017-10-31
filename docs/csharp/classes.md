---
title: "类 - C# 指南"
description: "了解类类型及其创建方式"
keywords: .NET, .NET Core, C#
author: BillWagner
ms.author: wiwagn
ms.date: 10/10/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 95c686ba-ae4f-440e-8e94-0dbd6e04d11f
ms.translationtype: HT
ms.sourcegitcommit: b041fbec3ff22157d00af2447e76a7ce242007fc
ms.openlocfilehash: 13cbd3a5b53ea9b0f1acb22684b6a28639d00751
ms.contentlocale: zh-cn
ms.lasthandoff: 09/14/2017

---

# <a name="classes"></a>类
*类*属于构造，使用类，可以通过组合其他类型的变量、方法和事件创建自己的自定义类型。 类好比是蓝图。 它定义类型的数据和行为。 如果类未声明为静态，客户端代码就可以通过创建分配给变量的*对象*或*实例*来使用该类。 变量会一直保留在内存中，直至对变量的所有引用超出范围为止。 超出范围时，CLR 将对其进行标记，以便用于垃圾回收。 如果类声明为[静态](language-reference/keywords/static.md)，则内存中只有一个副本，且客户端代码只能通过类本身，而不是*实例变量*来访问它。 有关详细信息，请参阅[静态类和静态类成员](programming-guide/classes-and-structs/static-classes-and-static-class-members.md)。  

## <a name="reference-types"></a>引用类型  
定义为[类](language-reference/keywords/class.md)的一个类型是*引用类型*。 在运行时，当您声明引用类型的变量时，该变量会一直包含值 [null](language-reference/keywords/null.md)，直至您使用 [new](language-reference/keywords/new.md) 运算符显式创建对象的实例，或者为该变量分配已经在其他位置使用 [new](language-reference/keywords/new.md) 创建的对象，如下所示:  

[!code-csharp[Reference Types](../../samples/snippets/csharp/concepts/classes/reference-type.cs)]
  
创建对象后，内存位于托管堆上，并且变量只保留对对象位置的引用。 当分配托管堆上的类型和由 CLR 的自动内存管理功能对其进行回收（称为*垃圾回收*）时，需要开销。 但是，垃圾回收已是高度优化，并且在大多数情况下，不会产生性能问题。 有关垃圾回收的详细信息，请参阅[自动内存管理和垃圾回收](../standard/garbage-collection/gc.md)。  
  
引用类型完全支持*继承*，这是面向对象的编程的一个基本特点。 创建类时，可以从其他任何未定义为 [sealed](language-reference/keywords/sealed.md)（密封）的接口或类继承，而其他类可以从你的类继承并重写虚拟方法。 有关详细信息，请参阅[继承](programming-guide/classes-and-structs/inheritance.md)。

## <a name="declaring-classes"></a>声明类  
使用 [class](language-reference/keywords/class.md) 关键字可以声明类，如下例所示：  
  
[!code-csharp[Declaring Classes](../../samples/snippets/csharp/concepts/classes/declaring-classes.cs)]  
  
**class** 关键字前面是访问修饰符。 由于在此例中使用 [public](language-reference/keywords/public.md)，因此任何人都可以从此类创建对象。 类的名称遵循 **class** 关键字。 定义的其余部分是类的主体，其中定义了行为和数据。 类上的字段、属性、方法和事件统称为*类成员*。  
  
## <a name="creating-objects"></a>创建对象  
类定义对象类型，但不是对象本身。 对象是基于类的具体实体，有时称为类的实例。  
  
可通过使用 [new](language-reference/keywords/new.md) 关键字，后跟对象要基于的类的名称，来创建对象，如：  
  
[!code-csharp[Creating Objects](../../samples/snippets/csharp/concepts/classes/creating-objects.cs)]   
  
创建类的实例后，会将一个该对象的引用传递回程序员。 在上一示例中，`object1` 是对基于 `Customer` 的对象的引用。 该引用指向新对象，但不包含对象数据本身。 事实上，可以创建对象引用，而完全无需创建对象本身：  
  
[!code-csharp[Creating Objects](../../samples/snippets/csharp/concepts/classes/creating-objects2.cs)]  
  
不建议创建这样一个不引用对象的对象引用，因为尝试通过这类引用访问对象会在运行时失败。 但实际上可以使用这类引用来引用某个对象，方法是创建新对象，或者将其分配给现有对象，例如：  
  
[!code-csharp[Creating Objects](../../samples/snippets/csharp/concepts/classes/creating-objects3.cs)]  
  
此代码创建指向同一对象的两个对象引用。 因此，通过 `object3` 对对象所做的任何更改都将在以后使用 `object4` 时反映出来。 由于基于类的对象是通过引用来实现其引用的，因此类被称为引用类型。  
  
## <a name="class-inheritance"></a>类继承  
继承是通过使用*派生*来完成的，这意味着类是通过使用其数据和行为所派生自的*基类*来声明的。 基类通过在派生的类名称后面追加冒号和基类名称来指定，如：  
  
[!code-csharp[Inheritance](../../samples/snippets/csharp/concepts/classes/inheritance.cs)]  
  
类声明基类时，会继承基类除构造函数外的所有成员。  
  
与 C++ 不同，C# 中的类只能直接从基类继承。 但是，因为基类本身可能继承自其他类，因此类可能间接继承多个基类。 此外，类还可以直接实现多个接口。 有关详细信息，请参阅[接口](programming-guide/interfaces/index.md)。  
  
类可以声明为 [abstract](language-reference/keywords/abstract.md)（抽象）。 抽象类包含抽象方法，抽象方法包含签名定义但不包含实现。 抽象类不能实例化。 只能通过可实现抽象方法的派生类来使用该类。 与此相反，[sealed](language-reference/keywords/sealed.md)（密封）类不允许其他类继承。 有关详细信息，请参阅[抽象类、密封类及类成员](programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)。  
  
类定义可以在不同的源文件之间分割。 有关详细信息，请参阅[分部类定义](programming-guide/classes-and-structs/partial-classes-and-methods.md)。  
  
 
## <a name="example"></a>示例
下例定义了一个公共类，该类包含一个字段、一个方法和一个名为构造函数的特殊方法。 有关详细信息，请参阅[构造函数](programming-guide/classes-and-structs/constructors.md)。 然后使用 **new** 关键字实例化类。

[!code-csharp[Class Example](../../samples/snippets/csharp/concepts/classes/class-example.cs)]  
  
## <a name="c-language-specification"></a>C# 语言规范  
有关详细信息，请参阅 [C# 语言规范](language-reference/language-specification/index.md)。 该语言规范是 C# 语法和用法的权威资料。
  
## <a name="see-also"></a>请参阅  
[C# 编程指南](programming-guide/index.md)   
[多形性](programming-guide/classes-and-structs/polymorphism.md)   
[类和结构成员](programming-guide/classes-and-structs/members.md)   
[类和结构方法](programming-guide/classes-and-structs/methods.md)   
[构造函数](programming-guide/classes-and-structs/constructors.md)   
[终结器](programming-guide/classes-and-structs/destructors.md)   
[对象](programming-guide/classes-and-structs/objects.md)


