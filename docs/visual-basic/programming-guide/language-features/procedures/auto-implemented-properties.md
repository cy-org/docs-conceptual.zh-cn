---
title: "自动实现的属性 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.AutoProperty"
  - "vb.AutoImplementedProperty"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "自动实现的属性 [Visual Basic]"
  - "属性 [Visual Basic], 自动实现"
  - "属性, 自动实现 [Visual Basic]"
ms.assetid: 5c669f0b-cf95-4b4e-ae84-9cc55212ca87
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# 自动实现的属性 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

*自动实现的属性*使你可以快速指定类的属性，而不必编写代码以对属性进行 `Get` 和 `Set` 操作。  为自动实现的属性编写代码时，Visual Basic 编译器会自动创建私有字段以存储属性变量，并且会创建关联的 `Get` 和 `Set` 过程。  
  
 使用自动实现的属性，可以在单行中声明一个属性（包括默认值）。  下面的示例演示三个属性声明。  
  
 [!code-vb[VbVbalrAutoImplementedProperties#1](./codesnippet/VisualBasic/auto-implemented-properties_1.vb)]  
  
 自动实现的属性等效于其属性值存储在私有字段中的属性。  下面的代码示例演示一个自动实现的属性。  
  
 [!code-vb[VbVbalrAutoImplementedProperties#5](./codesnippet/VisualBasic/auto-implemented-properties_2.vb)]  
  
 下面的代码示例演示上面自动实现的属性示例的等效代码。  
  
 [!code-vb[VbVbalrAutoImplementedProperties#2](./codesnippet/VisualBasic/auto-implemented-properties_3.vb)]  
  
 以下代码演示如何实现只读属性：  
  
```vb  
Class Customer  
   Public ReadOnly Property Tags As New List(Of String)  
   Public ReadOnly Property Name As String = ""  
   Public ReadOnly Property File As String  
  
   Sub New(file As String)  
      Me.File = file  
   End Sub  
End Class  
  
```  
  
 可以使用初始化表达式分配给属性（如示例中所示），也可以在包含类型的构造函数中分配给属性。  可以随时分配给只读属性的支持字段。  
  
## 支持字段  
 声明自动实现的属性时，Visual Basic 会自动创建隐藏的私有字段（称为支*持字段*）来包含属性值。  支持字段名是前面带下划线 \(\_\) 的自动实现的属性名。  例如，如果声明一个名为 `ID` 的自动实现的属性，则支持字段名为 `_ID`。  如果包含一个也名为 `_ID` 的类成员，则会形成命名冲突，Visual Basic 会报告编译器错误。  
  
 支持字段还具有下列特征：  
  
-   支持字段的访问修饰符始终是 `Private`，即使在属性本身具有不同访问级别（如 `Public`）时也是如此。  
  
-   如果属性标记为 `Shared`，则支持字段也进行共享。  
  
-   为属性指定的属性不适用于支持字段。  
  
-   可以从类中的代码以及从调试工具（如监视窗口）访问支持字段。  但是，支持字段不显示在 IntelliSense 文字自动完成列表中。  
  
## 初始化自动实现的属性  
 任何可以用于实例化字段的表达式对于初始化自动实现的属性都是有效的。  初始化自动实现的属性时，表达式会进行计算并传递给属性的 `Set` 过程。  下面的代码示例演示一些包含初始值的自动实现的属性。  
  
 [!code-vb[VbVbalrAutoImplementedProperties#3](./codesnippet/VisualBasic/auto-implemented-properties_4.vb)]  
  
 无法初始化作为 `Interface` 的成员或标记为 `MustOverride` 的自动实现的属性。  
  
 将自动实现的属性声明为 `Structure` 的成员时，如果自动实现的属性标记为 `Shared`，则只能初始化它。  
  
 将自动实现的属性声明为数组时，不能指定显式数组边界。  但是，可以使用数组初始值设定项提供值，如下面的示例所示。  
  
 [!code-vb[VbVbalrAutoImplementedProperties#4](./codesnippet/VisualBasic/auto-implemented-properties_5.vb)]  
  
## 需要标准语法的属性定义  
 自动实现的属性十分方便，支持很多编程方案。  但是，在有些情况下无法使用自动实现的属性，必须改用标准或*扩展*属性语法。  
  
 如果要执行以下任一操作，则必须使用扩展属性定义语法：  
  
-   向属性的 `Get` 或 `Set` 过程添加代码，如用于在 `Set` 过程中验证传入值的代码。  例如，你可能要在设置属性值之前验证表示电话号码的字符串是否包含所需数量的数字。  
  
-   为 `Get` 和 `Set` 过程指定不同的可访问性。  例如，你可能要使 `Set` 过程是 `Private`，要使 `Get` 过程是 `Public`。  
  
-   创建作为 `WriteOnly` 的属性。  
  
-   使用参数化的属性（包括 `Default` 属性）。  必须声明扩展属性才能为属性指定参数或是为 `Set` 过程指定附加参数。  
  
-   将属性置于支持字段上，或更改支持字段的访问级别。  
  
-   为支持字段提供 XML 注释。  
  
## 扩展自动实现的属性  
 如果需要将自动实现的属性转换为包含 `Get` 或 `Set` 过程的扩展属性，则 Visual Basic 代码编辑器可以为属性自动生成 `Get` 和 `Set` 过程以及 `End Property` 语句。  如果将光标置于 `Property` 语句后的空白行上，输入 `G`（对于 `Get`）或 `S`（对于 `Set`），然后按 ENTER，则会生成代码。  在 `Property` 语句末尾按 Enter 时，Visual Basic 代码编辑器会为只读和只写属性自动生成 `Get` 或 `Set` 过程。  
  
## 请参阅  
 [如何：在 Visual Basic 中声明和调用默认属性](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-and-call-a-default-property.md)   
 [如何：声明具有混合访问级别的属性](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-a-property-with-mixed-access-levels.md)   
 [Property 语句](../../../../visual-basic/language-reference/statements/property-statement.md)   
 [ReadOnly](../../../../visual-basic/language-reference/modifiers/readonly.md)   
 [WriteOnly](../../../../visual-basic/language-reference/modifiers/writeonly.md)   
 [对象和类](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)