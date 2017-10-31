---
title: "Dim 语句 (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Dim
- Dim
dev_langs:
- VB
helpviewer_keywords:
- Public keyword, in Dim statement
- Dim statement
- fixed-length strings, declaring
- variables [Visual Basic], declaring
- WithEvents keyword, Dim statement
- dynamic arrays, Dim statement
- variables [Visual Basic], initializing
- '{} braces'
- fields, as member variables
- declarations, dynamic arrays
- member variables
- default values
- data types [Visual Basic], assigning
- braces {}
- As keyword, in Dim statement
- arrays [Visual Basic], declaring
- New keyword, Dim statement
- To keyword, in Dim statement
- storage, allocating
- local variables
- declaration statements
- Dim statement, syntax
- variables [Visual Basic], member and local
ms.assetid: fae3eca1-f0b2-4400-994b-7aa58a848448
caps.latest.revision: 72
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
ms.openlocfilehash: 00d5d0e83a88a0c7ac3ade92d09c584fce64fcd8
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="dim-statement-visual-basic"></a>Dim 语句 (Visual Basic)
声明，并为一个或多个变量分配存储空间。  
  
## <a name="syntax"></a>语法  
  
```  
[ <attributelist> ] [ accessmodifier ] [[ Shared ] [ Shadows ] | [ Static ]] [ ReadOnly ]   
Dim [ WithEvents ] variablelist  
```  
  
## <a name="parts"></a>部件  
  
-   `attributelist`  
  
     可选。 请参阅[属性列表](../../../visual-basic/language-reference/statements/attribute-list.md)。  
  
-   `accessmodifier`  
  
     可选。 可以是以下各项之一：  
  
    -   [Public](../../../visual-basic/language-reference/modifiers/public.md)  
  
    -   [Protected](../../../visual-basic/language-reference/modifiers/protected.md)  
  
    -   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)  
  
    -   [Private](../../../visual-basic/language-reference/modifiers/private.md)  
  
    -   `Protected Friend`  
  
     请参阅[访问 Visual Basic 中的级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。  
  
-   `Shared`  
  
     可选。 请参阅[共享](../../../visual-basic/language-reference/modifiers/shared.md)。  
  
-   `Shadows`  
  
     可选。 请参阅[阴影](../../../visual-basic/language-reference/modifiers/shadows.md)。  
  
-   `Static`  
  
     可选。 请参阅[静态](../../../visual-basic/language-reference/modifiers/static.md)。  
  
-   `ReadOnly`  
  
     可选。 请参阅[ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)。  
  
-   `WithEvents`  
  
     可选。 指定它们的对象变量的引用可以引发事件的类的实例。 请参阅[WithEvents](../../../visual-basic/language-reference/modifiers/withevents.md)。  
  
-   `variablelist`  
  
     必需。 此语句中声明的变量的列表。  
  
     `variable [ , variable ... ]`  
  
     每个 `variable` 都具有以下语法和部件：  
  
     `variablename [ ( [ boundslist ] ) ] [ As [ New ] datatype [ With`{`[ .propertyname = propinitializer [ , ... ] ] } ] ] [ = initializer ]`  
  
    |部件|描述|  
    |---|---|  
    |`variablename`|必需。 变量的名称。 请参阅[声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。|  
    |`boundslist`|可选。 列出每个维度的一个数组变量的界限。|  
    |`New`|可选。 创建类的新实例时`Dim`语句在运行时。|  
    |`datatype`|可选。 变量的数据类型。|  
    |`With`|可选。 引入了对象初始值设定项列表。|  
    |`propertyname`|可选。 在类中属性的名称将会创建的实例。|  
    |`propinitializer`|需要在之后`propertyname`=。 表达式，计算并将其分配给属性名称。|  
    |`initializer`|可选如果`New`未指定。 计算并将其创建时分配给变量的表达式。|  
  
## <a name="remarks"></a>备注  
 Visual Basic 编译器使用`Dim`语句来确定变量的数据类型和其他信息，例如哪些代码可以访问变量。 下面的示例声明一个变量以保存`Integer`值。  
  
```vb  
Dim numberOfStudents As Integer  
```  
  
 您可以指定任何数据类型或枚举、 结构、 类或接口的名称。  
  
```vb  
Dim finished As Boolean  
Dim monitorBox As System.Windows.Forms.Form  
```  
  
 对于引用类型，您使用`New`关键字来创建类的新实例或结构的指定数据类型。 如果您使用`New`，不使用初始值设定项表达式。 相反，如果它们是必需的要从其创建该变量的类的构造函数提供参数。  
  
```vb  
Dim bottomLabel As New System.Windows.Forms.Label  
```  
  
 您可以声明过程、 块、 类、 结构或模块中的变量。 不能声明源文件、 命名空间或接口中的变量。 有关详细信息，请参阅[声明上下文和默认访问级别](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)。  
  
 在模块级别，在任何过程外部声明的变量是*成员变量*或*字段*。 成员变量是在其类、 结构或模块整个范围内。 在过程级别声明的变量是*局部变量*。 本地变量是仅在它们的过程或块的作用域中。  
  
 下面的访问修饰符用于声明变量的过程之外︰ `Public`， `Protected`， `Friend`， `Protected Friend`，和`Private`。 有关详细信息，请参阅[Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。  
  
 `Dim`关键字是可选的通常省略如果指定任何以下修饰符︰ `Public`， `Protected`， `Friend`， `Protected Friend`， `Private`， `Shared`， `Shadows`， `Static`， `ReadOnly`，或`WithEvents`。  
  
```vb  
Public maximumAllowed As Double  
Protected Friend currentUserName As String  
Private salary As Decimal  
Static runningTotal As Integer  
```  
  
 如果`Option Explicit`是 （默认设置），则编译器会为您使用每个变量要求声明。 有关详细信息，请参阅[Option Explicit 语句](../../../visual-basic/language-reference/statements/option-explicit-statement.md)。  
  
## <a name="specifying-an-initial-value"></a>指定一个初始值  
 创建时，可以将一个值分配给一个变量。 对于值类型，您使用*初始值设定项*来提供要分配给该变量的表达式。 该表达式的计算结果必须为一个常量，它可以在编译时计算。  
  
```vb  
Dim quantity As Integer = 10  
Dim message As String = "Just started"  
```  
  
 如果指定一个初始值设定项和数据类型中未指定`As`子句，*类型推理*用于推断通过初始值设定项的数据类型。 在下面的示例中，同时`num1`和`num2`强类型化为整数。 在第二个声明中，类型推断推断出类型 3 的值。  
  
```vb  
' Use explicit typing.  
Dim num1 As Integer = 3  
  
' Use local type inference.  
Dim num2 = 3  
```  
  
 类型推理适用于过程级。 它不适用于在类、 结构、 模块或接口中的过程之外。 类型推理的详细信息，请参阅[Option Infer 语句](../../../visual-basic/language-reference/statements/option-infer-statement.md)和[本地类型推理](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)。  
  
 如果未指定数据类型或初始值设定项，则会发生什么情况的信息，请参阅[默认数据类型和值](../../../visual-basic/language-reference/statements/dim-statement.md#default)本主题中更高版本。  
  
 您可以使用*对象初始值设定项*声明命名和匿名类型的实例。 下面的代码创建的实例`Student`类，并使用对象初始值设定项来初始化属性。  
  
```vb  
Dim student1 As New Student With {.First = "Michael",   
                                  .Last = "Tucker"}  
```  
  
 有关对象初始值设定项的详细信息，请参阅[如何︰ 使用对象初始值设定项声明对象](../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-declare-an-object-by-using-an-object-initializer.md)，[对象初始值设定项︰ 命名类型和匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)，和[匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)。  
  
## <a name="declaring-multiple-variables"></a>声明多个变量  
 您可以声明多个变量在一个声明语句中，使用括号指定变量的名称为每个，并在每个数组名。 以逗号分隔多个变量。  
  
```vb  
Dim lastTime, nextTime, allTimes() As Date  
```  
  
 如果要声明多个变量与一个`As`子句中，不能提供该组的变量的初始值设定项。  
  
 您可以指定不同的数据类型为不同的变量使用单独的`As`子句为每个声明的变量。 每个变量将在第一个指定的数据类型`As`子句后遇到其`variablename`部件。  
  
```vb  
Dim a, b, c As Single, x, y As Double, i As Integer  
' a, b, and c are all Single; x and y are both Double  
```  
  
## <a name="arrays"></a>数组  
 您可以声明一个变量以保存*数组*，后者可以容纳多个值。 若要指定的变量保留了一个数组，请按照其`variablename`后面紧跟一对括号。 有关数组的详细信息，请参阅[数组](../../../visual-basic/programming-guide/language-features/arrays/index.md)。  
  
 您可以指定的下限和上限，每个维度的数组。 若要执行此操作，包括`boundslist`在括号内。 为每个维度`boundslist`指定上限和下限 （可选）。 无论您指定下限值始终为零。 每个索引可能会不同于通过其上界值为零。  
  
 下面的两个语句是等效的。 每个语句声明数组 21`Integer`元素。 当您访问该数组时，该索引可能会不同于 0 到 20。  
  
```vb  
Dim totals(20) As Integer  
Dim totals(0 To 20) As Integer  
```  
  
 下面的语句声明类型的二维数组`Double`。 数组所具有 6 列 (5 + 1) 每个 4 的行 (3 + 1)。 请注意，上限表示索引中，不维的长度的最大可能值。 维度的长度为上界加一。  
  
```vb  
Dim matrix2(3, 5) As Double  
```  
  
 数组可以包含 1 到 32 个维。  
  
 您可以将所有的边界中的数组声明留空。 如果这样做，则数组包含您指定的维度数，但不会被初始化。 它具有值`Nothing`至少初始化之前的某些元素。 `Dim`语句都必须指定边界的所有维度或任何维度。  
  
```vb  
' Declare an array with blank array bounds.  
Dim messages() As String  
' Initialize the array.  
ReDim messages(4)  
```  
  
 如果数组具有多个维度，必须包含以逗号分隔括号来表示的维度数。  
  
```vb  
Dim oneDimension(), twoDimensions(,), threeDimensions(,,) As Byte  
```  
  
 您可以声明*长度为零的数组*通过声明一个数组的维数为-1。 保存一个零长度的数组的变量不具有值`Nothing`。 长度为零的数组所需的某些公共语言运行时函数。 如果您尝试访问此类数组时，会发生运行时异常。 有关详细信息，请参阅[数组](../../../visual-basic/programming-guide/language-features/arrays/index.md)。  
  
 可以通过使用数组文本初始化数组的值。 若要执行此操作，环绕具有大括号初始化值 (`{}`)。  
  
```vb  
Dim longArray() As Long = {0, 1, 2, 3}  
```  
  
 对于多维数组，初始化的每个单独的维度包含在外部维度中的括号中。 其元素被指定按行优先的顺序。  
  
```vb  
Dim twoDimensions(,) As Integer = {{0, 1, 2}, {10, 11, 12}}  
```  
  
 数组文本的详细信息，请参阅[数组](../../../visual-basic/programming-guide/language-features/arrays/index.md)。  
  
##  <a name="default"></a>默认数据类型和值  
 下表描述了指定 `Dim` 语句中数据类型和初始值设定项的各种组合的结果。  
  
|是否指定数据类型？|是否指定初始值设定项？|示例|结果|  
|---|---|---|---|  
|否|No|`Dim qty`|如果[Option Strict](../../../visual-basic/language-reference/statements/option-strict-statement.md)为 off （默认），则变量设置为`Nothing`。<br /><br /> 如果 `Option Strict` 处于打开状态，则发生编译时错误。|  
|否|是|`Dim qty = 5`|如果[Option Infer](../../../visual-basic/language-reference/statements/option-infer-statement.md)处于打开状态 （默认值），则变量采用数据类型的初始值设定项。 请参阅[局部类型推理](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)。<br /><br /> 如果 `Option Infer` 和 `Option Strict` 均处于关闭状态，则变量采用 `Object` 的数据类型。<br /><br /> 如果 `Option Infer` 处于关闭状态但 `Option Strict` 处于打开状态，则发生编译时错误。|  
|是|否|`Dim qty As Integer`|将变量初始化为数据类型的默认值。 请参阅本节后面的表。|  
|是|是|`Dim qty  As Integer = 5`|如果初始值设定项的数据类型不可转换为指定数据类型，则会发生编译时错误。|  
  
 如果你指定的数据类型，但不是指定初始值设定项，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]将变量初始化为其数据类型的默认值。 下表显示的默认初始化值。  
  
|数据类型|默认值|  
|---|---|  
|所有数值类型 (包括`Byte`和`SByte`)|0|  
|`Char`|二进制 0|  
|所有引用类型 (包括`Object`， `String`，和所有数组)|`Nothing`|  
|`Boolean`|`False`|  
|`Date`|1 年 1 月 1 日的上午 12:00 (01/01/0001 12:00:00 AM)|  
  
 像它是一个单独的变量初始化结构的每个元素。 如果您声明数组的长度，但不是初始化它的元素，每个元素将初始化像它是一个单独的变量。  
  
## <a name="static-local-variable-lifetime"></a>静态局部变量生存期  
 一个`Static`局部变量具有较长的生存期比在其中声明该过程。 变量的生存期边界取决于声明该过程，以及是否有`Shared`。  
  
|过程声明|初始化变量|变量停止存在|  
|---|---|---|  
|在模块中|第一次调用该过程|当您的程序停止执行|  
|在类或结构中，过程都是`Shared`|第一次调用该过程的特定实例或对类或结构本身|当您的程序停止执行|  
|在类或结构中，过程不是`Shared`|第一次特定实例调用该过程|当垃圾回收 (GC) 释放该实例|  
  
## <a name="attributes-and-modifiers"></a>特性和修饰符  
 可以将特性应用于成员变量，不适用于本地变量。 特性提供信息对程序集的元数据，这并没有意义的临时存储 （如本地变量）。  
  
 在模块级别，不能使用`Static`修饰符可以声明成员变量。 在过程级别，不能使用`Shared`， `Shadows`， `ReadOnly`， `WithEvents`，或任何访问修饰符来声明本地变量。  
  
 您可以指定哪些代码可以访问的变量通过提供`accessmodifier`。 类和模块成员变量 （任何过程之外） 默认为私有访问，而结构成员变量默认为公共访问权限。 您可以调整它们的访问级别使用的访问修饰符。 不能使用访问修饰符 （过程） 中的本地变量上。  
  
 您可以指定`WithEvents`仅对成员变量上，而不在过程内的局部变量。 如果指定`WithEvents`，该变量的数据类型必须是特定的类类型，不`Object`。 不能声明与数组`WithEvents`。 有关事件的详细信息，请参阅[事件](../../../visual-basic/programming-guide/language-features/events/index.md)。  
  
> [!NOTE]
>  代码类之外，结构或模块必须限定成员变量的名称替换该类、 结构或模块的名称。 过程或块不能引用该过程或块内的任何局部变量之外的代码。  
  
## <a name="releasing-managed-resources"></a>释放托管的资源  
 .NET Framework 垃圾回收器释放托管资源而无需您采取任何额外的编码。 但是，您可以强制将托管资源而不是等待垃圾回收器处置。  
  
 如果一个类占用特别是有价值和稀缺资源 （例如数据库连接或文件句柄），可能不希望等到下一步的垃圾回收，来清理不再使用的类实例。 类可以实现<xref:System.IDisposable>接口，以提供一种方法来释放垃圾回收之前的资源。</xref:System.IDisposable> 实现该接口的类公开`Dispose`可以调用来强制立即释放重要资源的方法。  
  
 `Using`语句可自动执行获取资源，执行一组语句，然后释放的资源的过程。 但是，该资源必须实现<xref:System.IDisposable>接口。</xref:System.IDisposable> 有关详细信息，请参阅[Using 语句](../../../visual-basic/language-reference/statements/using-statement.md)。  
  
## <a name="example"></a>示例  
 下面的示例通过声明变量`Dim`带有不同选项的语句。  
  
 [!code-vb[VbVbalrStatements #&141;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/dim-statement_1.vb)]  
  
## <a name="example"></a>示例  
 以下示例列出 1 到 30 之间的素数。 本地变量的作用域是在代码注释中所述。  
  
 [!code-vb[VbVbalrStatements #&142;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/dim-statement_2.vb)]  
  
## <a name="example"></a>示例  
 在下面的示例中，`speedValue`在类级别声明变量。 `Private`关键字用于声明变量。 中的任何过程可以访问此变量`Car`类。  
  
 [!code-vb[VbVbalrStatements #&144;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/dim-statement_3.vb)]  
  
 [!code-vb[VbVbalrStatements #&145;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/dim-statement_4.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [Const 语句](../../../visual-basic/language-reference/statements/const-statement.md)   
 [ReDim 语句](../../../visual-basic/language-reference/statements/redim-statement.md)   
 [Option Explicit 语句](../../../visual-basic/language-reference/statements/option-explicit-statement.md)   
 [Option Infer 语句](../../../visual-basic/language-reference/statements/option-infer-statement.md)   
 [Option Strict 语句](../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [“项目设计器”->“编译”页 (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/compile-page-project-designer-visual-basic)   
 [变量声明](../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [数组](../../../visual-basic/programming-guide/language-features/arrays/index.md)   
 [对象初始值设定项︰ 命名类型和匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)   
 [匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [对象初始值设定项︰ 命名类型和匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)   
 [如何︰ 使用对象初始值设定项声明对象](../../../visual-basic/programming-guide/language-features/objects-and-classes/how-to-declare-an-object-by-using-an-object-initializer.md)   
 [局部类型推理](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)

