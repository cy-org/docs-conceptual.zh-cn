---
title: "Declare 语句 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Declare"
  - "vb.Lib"
  - "vb.Any"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Alias 关键字"
  - "API, 声明 API 函数"
  - "As 关键字, 在 Declare 语句中"
  - "声明, 外部"
  - "声明, 过程"
  - "Declare 语句"
  - "声明过程, Declare 语句"
  - "DLL, 声明过程"
  - "外部引用, Visual Basic"
  - "Function 过程, 声明"
  - "函数 [Visual Basic], Function 过程"
  - "Lib 关键字"
  - "Platform Invoke — 平台调用, Visual Basic 外部引用"
  - "过程, declaration"
  - "过程, 外部"
  - "Public 关键字, Declare 语句"
  - "资源 [Visual Basic], 声明"
  - "Sub 过程, 声明"
  - "Visual Basic 代码, Function 过程"
  - "Visual Basic 代码, Sub 过程"
ms.assetid: d3f21fb0-b804-4c99-97ed-583b23894cf1
caps.latest.revision: 30
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 30
---
# Declare 语句
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

声明对在外部文件中实现的过程的引用。  
  
## 语法  
  
```  
[ <attributelist> ] [ accessmodifier ] [ Shadows ] [ Overloads ] _  
Declare [ charsetmodifier ] [ Sub ] name Lib "libname" _  
[ Alias "aliasname" ] [ ([ parameterlist ]) ]  
' -or-  
[ <attributelist> ] [ accessmodifier ] [ Shadows ] [ Overloads ] _  
Declare [ charsetmodifier ] [ Function ] name Lib "libname" _  
[ Alias "aliasname" ] [ ([ parameterlist ]) ] [ As returntype ]  
```  
  
## 部件  
  
|||  
|-|-|  
|术语|定义|  
|`attributelist`|可选。  请参见[特性列表](../../../visual-basic/language-reference/statements/attribute-list.md)。|  
|`accessmodifier`|可选。  可以是如下内容之一：<br /><br /> -   [Public](../../../visual-basic/language-reference/modifiers/public.md)<br />-   [Protected](../../../visual-basic/language-reference/modifiers/protected.md)<br />-   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)<br />-   [Private](../../../visual-basic/language-reference/modifiers/private.md)<br />-   `Protected Friend`<br /><br /> 请参见 [Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。|  
|`Shadows`|可选。  请参见 [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md)。|  
|`charsetmodifier`|可选。  指定字符集和文件搜索信息。  可以是如下内容之一：<br /><br /> -   [Ansi](../../../visual-basic/language-reference/modifiers/ansi.md)（默认值）<br />-   [Unicode](../../../visual-basic/language-reference/modifiers/unicode.md)<br />-   [Auto](../../../visual-basic/language-reference/modifiers/auto.md)|  
|`Sub`|可选项，但是 `Sub` 或 `Function` 必须出现。  指明外部过程并不返回值。|  
|`Function`|可选项，但是 `Sub` 或 `Function` 必须出现。  指明外部过程返回值。|  
|`name`|必选。  此外部引用的名称。  有关更多信息，请参见 [已声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。|  
|`Lib`|必选。  引入 `Lib` 子句，用于标识包含外部过程的外部文件（DLL 或代码资源）。|  
|`libname`|必选。  包含所声明过程的文件的名称。|  
|`Alias`|可选。  指明无法在所声明过程的文件内依据 `name` 中指定的名称标识该过程。  您在 `aliasname` 中指定其标识。|  
|`aliasname`|如果使用 `Alias` 关键字，则为必选项。  按以下两种方式之一标识过程的字符串：<br /><br /> 过程在其文件内的入口点名称，括在引号 \(`""`\) 内<br /><br /> \- 或 \-<br /><br /> 在数字符号 \(`#`\)后跟一个整数，指定过程入口点在其文件内的序号|  
|`parameterlist`|如果过程接受参数，则为必选项。  请参见 [参数列表](../../../visual-basic/language-reference/statements/parameter-list.md)。|  
|`returntype`|如果指定了 `Function`，并且 `Option Strict` 为 `On`，则为必选项。  过程所返回值的数据类型。|  
  
## 备注  
 有时，您需要调用在项目外部的某个文件（如 DLL 或代码资源）中定义的过程。  当您这样做时，Visual Basic 编译器没有权限访问其正确调用过程所需的信息，例如过程的位置、标识方式、调用顺序和返回类型，以及过程使用的字符串字符集。  `Declare` 语句创建一个对外部过程的引用，并提供这些必需的信息。  
  
 仅可以在模块级别使用 `Declare`。  这意味着，外部引用的声明上下文必须是类、结构或模块，不能是源文件、命名空间、接口、过程或块。  有关更多信息，请参见[声明上下文和默认访问级别](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)。  
  
 外部引用默认为 [Public](../../../visual-basic/language-reference/modifiers/public.md) 访问。  可以使用访问修饰符来调整它们的访问级别。  
  
## 规则  
  
-   **特性。**可以将特性应用于外部引用。  所应用的任何特性都只在项目中有效，在外部文件中无效。  
  
-   **修饰符。**外部过程隐式地为 [Shared](../../../visual-basic/language-reference/modifiers/shared.md)。  声明外部引用时不能使用 `Shared` 关键字，也不能改变它的共享状态。  
  
     外部过程不能参与重写过程、实现接口成员或处理事件。  因此，不能在 `Declare` 语句中使用 `Overrides`、`Overridable`、`NotOverridable`、`MustOverride`、`Implements` 或 `Handles` 关键字。  
  
-   **外部过程名称。**不必（在 `name` 中）为此外部引用指定与过程在其外部文件内的入口点名称 \(`aliasname`\) 相同的名称。  可以使用 `Alias` 子句来指定入口点名称。  如果外部过程具有与 Visual Basic 保留修饰符或变量、过程或同一范围中的任何其他编程元素相同的名称，这一点可能十分有用。  
  
    > [!NOTE]
    >  大多数 DLL 中的入口点名称都区分大小写。  
  
-   **外部过程编号。**或者，您可以使用 `Alias` 子句来指定外部文件的导出表内入口点的序号。  为此，您可使用数字符号 \(`#`\) 作为 `aliasname` 的开头。  如果不允许在 Visual Basic 中使用外部过程名称中的任何字符，或者，如果外部文件在导出过程时未使用名称，则这一点十分有用。  
  
## 数据类型规则  
  
-   **参数数据类型。**如果 `Option Strict` 为 `On`，您必须指定 `parameterlist` 中每个参数的数据类型。  这可以是任何数据类型或枚举、结构、类或接口的名称。  在 `parameterlist` 内，您使用 `As` 子句来指定要传递给每个参数的变量的数据类型。  
  
    > [!NOTE]
    >  如果外部过程不是针对 .NET Framework 编写的，您必须注意应使数据类型相符。  例如，如果用 `Integer` 参数（在 Visual Basic 6.0 中为 16 位）声明对 Visual Basic 6.0 过程的引用，则必须在 `Declare` 语句中将对应的变量标识为 `Short`，因为在 Visual Basic 中它是 16 位的整数类型。  同样，`Long` 在 Visual Basic 6.0 中具有不同的数据宽度，并且 `Date` 的实现方式也不同。  
  
-   **返回数据类型。**如果外部过程是 `Function`，并且 `Option Strict` 设置为 `On`，您必须指定返回到调用代码的值的数据类型。  这可以是任何数据类型或枚举、结构、类或接口的名称。  
  
    > [!NOTE]
    >  Visual Basic 编译器不会验证您的数据类型是否与外部过程的数据类型兼容。  如果存在不匹配现象，公共语言运行时将在运行时产生 <xref:System.Runtime.InteropServices.MarshalDirectiveException> 异常。  
  
-   **默认数据类型。**如果 `Option Strict` 设置为 `Off`，并且未在 `parameterlist` 中指定某个形参的数据类型，Visual Basic 编译器会将对应的实参转换为 [Object 数据类型](../../../visual-basic/language-reference/data-types/object-data-type.md)。  同样，如果未指定 `returntype`，编译器会将返回数据类型转换为 `Object`。  
  
    > [!NOTE]
    >  由于所处理的外部过程有可能是在不同平台上编写的，因此，对数据类型做出任何假定或允许它们采用默认设置会十分危险。  指定每个参数和返回值（如果有）的数据类型将会安全很多。  这还提高了代码的可读性。  
  
## 行为  
  
-   **范围。**外部引用的应用范围覆盖了其整个类、结构或模块。  
  
-   **生存期。**外部引用具有与声明它的类、结构或模块相同的生存期。  
  
-   **调用外部过程。**调用外部过程的方式与调用 `Function` 或 `Sub` 过程时相同，都是在表达式中使用它（如果它返回值）或在 [Call 语句](../../../visual-basic/language-reference/statements/call-statement.md) 中指定它（如果它不返回值）。  
  
     您将完全按照 `Declare` 语句中的 `parameterlist` 指定的方式将变量传递给外部过程。  不要考虑参数最初在外部文件中的声明方式。  同样，如果存在返回值，请完全按照 `Declare` 语句中 `returntype` 指定的方式使用它。  
  
-   **字符集。**可以在 `charsetmodifier` 中指定 Visual Basic 在调用外部过程时应如何封送字符串。  `Ansi` 修饰符指示 Visual Basic 将所有字符串封送为 ANSI 值，`Unicode` 修饰符则指示它将所有字符串封送为 Unicode 值。  `Auto` 修饰符指示 Visual Basic 依据 .NET Framework 规则，基于外部引用 `name` 或 `aliasname`（如果已指定）封送字符串。  默认值为 `Ansi`。  
  
     `charsetmodifier` 还指定 Visual Basic 应如何在外部文件中查找外部过程。  `Ansi` 和 `Unicode` 都指示 Visual Basic 在搜索过程中查找外部过程而不修改其名称。  `Auto` 指示 Visual Basic 确定运行时平台的基本字符集，并在可能时修改外部过程名称，如下所示：  
  
    -   在 ANSI 平台（如 Windows 95、Windows 98 或 Windows Millennium Edition）上，将首先查找外部过程，而不修改名称。  如果查找失败，则在外部过程名称结尾附加“A”，并再次查找。  
  
    -   在 Unicode 平台（如 Windows NT、Windows 2000 或 Windows XP）上，将首先查找外部过程，而不修改名称。  如果查找失败，则在外部过程名称结尾附加“W”，并再次查找。  
  
-   **机制。**Visual Basic 使用 .NET Framework 的平台调用 \(PInvoke\) 机制来解析和访问外部过程。  `Declare` 语句和 <xref:System.Runtime.InteropServices.DllImportAttribute> 类都会自动使用此机制，您无需对 PInvoke 有任何了解。  有关更多信息，请参见 [演练：调用 Windows API](../../../visual-basic/programming-guide/com-interop/walkthrough-calling-windows-apis.md)。  
  
> [!IMPORTANT]
>  如果外部过程在公共语言运行时 \(CLR\) 外部运行，则它为非托管代码。  当您调用此类过程（例如，Win32 API 函数或 COM 方法）时，可能会使应用程序面临安全风险。  有关更多信息，请参见 [托管代码的安全编码指南](../Topic/Secure%20Coding%20Guidelines%20for%20Unmanaged%20Code.md)。  
  
## 示例  
 下面的示例声明对 `Function` 过程的外部引用，该过程返回当前用户名。  它随后调用外部过程 `GetUserNameA` 作为 `getUser` 过程的一部分。  
  
 [!code-vb[VbVbalrStatements#15](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/declare-statement_1.vb)]  
  
## 示例  
 <xref:System.Runtime.InteropServices.DllImportAttribute> 提供了另一种在非托管代码中使用函数的方式。  下面的示例声明导入了一个函数，但不使用 `Declare` 语句。  
  
 [!code-vb[VbVbalrStatements#16](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/declare-statement_2.vb)]  
  
 [!code-vb[VbVbalrStatements#1](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/declare-statement_3.vb)]  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.ErrObject.LastDllError%2A>   
 [Imports 语句（.NET 命名空间和类型）](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)   
 [AddressOf 运算符](../../../visual-basic/language-reference/operators/addressof-operator.md)   
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [参数列表](../../../visual-basic/language-reference/statements/parameter-list.md)   
 [Call 语句](../../../visual-basic/language-reference/statements/call-statement.md)   
 [演练：调用 Windows API](../../../visual-basic/programming-guide/com-interop/walkthrough-calling-windows-apis.md)