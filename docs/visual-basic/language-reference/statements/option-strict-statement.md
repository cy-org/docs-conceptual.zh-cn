---
title: "Option Strict 语句 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Strict
- vb.OptionStrict
dev_langs:
- VB
helpviewer_keywords:
- Strict keyword
- Option Strict statement
- conversions, implicit
- late binding
- implicit conversions
ms.assetid: 5883e0c1-a920-4274-8e46-b0ff047eaee5
caps.latest.revision: 49
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
ms.openlocfilehash: 3bf0d4939f24c38392d7ca4764c41d12366067b5
ms.lasthandoff: 03/13/2017

---
# <a name="option-strict-statement"></a>Option Strict Statement
隐式数据类型将转换限制为只能扩大转换，不允许后期绑定，并禁止隐式类型化会导致`Object`类型。  
  
## <a name="syntax"></a>语法  
  
```  
Option Strict { On | Off }  
```  
  
## <a name="parts"></a>部件  
  
|术语|定义|  
|---|---|  
|`On`|可选。 使`Option Strict`检查。|  
|`Off`|可选。 禁用`Option Strict`检查。|  
  
## <a name="remarks"></a>备注  
 当`Option Strict On`或`Option Strict`出现在文件中，以下情况会导致编译时错误︰  
  
-   隐式收缩转换  
  
-   后期绑定  
  
-   隐式类型化会导致`Object`类型  
  
> [!NOTE]
>  您可以对设置的警告配置[编译页，项目设计器 (Visual Basic 中)](https://docs.microsoft.com/visualstudio/ide/reference/compile-page-project-designer-visual-basic)，有三个设置对应的三个条件会导致编译时错误。 有关如何使用这些设置的信息，请参阅[在 IDE 中设置警告配置](../../../visual-basic/language-reference/statements/option-strict-statement.md#conditions)本主题中更高版本。  
  
 `Option Strict Off`语句关闭错误和警告检查对于所有三个条件，即使相关联的 IDE 设置指定要打开这些错误或警告。 `Option Strict On`语句启用错误和警告检查对于所有三个条件，即使相关联的 IDE 设置指定将关闭这些错误或警告。  
  
 如果使用，`Option Strict`语句必须出现在文件中的任何其他源代码语句之前。  
  
 当您将设置`Option Strict`到`On`，Visual Basic 检查，指定所有编程元素的数据类型。 可以显式指定，或通过使用局部类型推理指定数据类型。 建议为所有编程元素指定数据类型，原因如下︰  
  
-   它使您的变量和参数的 IntelliSense 支持。 这使您以您键入代码时查看其属性和其他成员。  
  
-   它使编译器能够执行类型检查。 类型检查可以帮助您找到在运行时由于类型转换错误而失败的语句。 它还标识对不支持这些方法的对象上的方法的调用。  
  
-   它可以提高代码的执行。 一个原因是，如果未指定的编程元素的数据类型，Visual Basic 编译器将其分配`Object`类型。 已编译的代码可能需要将之间来回转换`Object`和其他数据类型，这会降低性能。  
  
## <a name="implicit-narrowing-conversion-errors"></a>隐式收缩转换错误  
 是收缩转换的隐式数据类型转换时，将发生隐式收缩转换错误。  
  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]可以将许多数据类型转换为其他数据类型。 一种数据类型的值转换为精度较低或容量较小的数据类型时，会发生数据丢失。 如果这种收缩转换失败，则会发生运行时错误。 `Option Strict`这样可以避免它们，请确保这些收缩转换提供编译时通知。 有关详细信息，请参阅[隐式和显式转换](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)和[扩大和收缩转换](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)。  
  
 可能会导致错误的转换包括在表达式中发生的隐式转换。 有关详细信息，请参阅下列主题：  
  
-   [+ 运算符](../../../visual-basic/language-reference/operators/addition-operator.md)  
  
-   [+= 运算符](../../../visual-basic/language-reference/operators/addition-assignment-operator.md)  
  
-   [\ 运算符 (Visual Basic)](../../../visual-basic/language-reference/operators/integer-division-operator.md)  
  
-   [/ = 运算符 (Visual Basic)](../../../visual-basic/language-reference/operators/floating-point-division-assignment-operator.md)  
  
-   [Char 数据类型](../../../visual-basic/language-reference/data-types/char-data-type.md)  
  
 通过使用连接字符串时[& 运算符](../../../visual-basic/language-reference/operators/concatenation-operator.md)，为字符串的所有转换被都认为是会扩大。 因此这些转换不会生成隐式收缩转换错误，即使`Option Strict`上。  
  
 当调用一个方法包含具有不同于相应的参数的数据类型的实际参数时，收缩转换会导致编译时错误如果`Option Strict`上。 若要避免编译时错误，可使用扩大转换或显式转换。  
  
 在转换中的元素的编译时，将隐式收缩转换错误会抑制`For Each…Next`循环控制变量的集合。 发生这种情况即使`Option Strict`上。 有关详细信息，请参阅中的"收缩转换"一节[为每个...下一条语句](../../../visual-basic/language-reference/statements/for-each-next-statement.md)。  
  
## <a name="late-binding-errors"></a>后期绑定错误  
 一个对象后期绑定到属性或方法声明为类型的变量的分配`Object`。 有关详细信息，请参阅[早期绑定和后期绑定](../../../visual-basic/programming-guide/language-features/early-late-binding/index.md)。  
  
## <a name="implicit-object-type-errors"></a>隐式对象类型错误  
 隐式对象类型错误发生时相应类型不能是为推断出声明的变量，因此一种类型的`Object`这方面的推断。 这主要发生在您使用`Dim`语句声明一个变量，但不使用`As`子句中，和`Option Infer`处于关闭状态。 有关详细信息，请参阅[Option Infer 语句](../../../visual-basic/language-reference/statements/option-infer-statement.md)和[Visual Basic 语言规范](../../../visual-basic/reference/language-specification.md)。  
  
 方法参数`As`子句是可选的如果`Option Strict`处于关闭状态。 但是，如果任何一个参数使用`As`子句，它们都必须使用它。 如果`Option Strict`处于打开状态，`As`子句是必需的每个参数定义。  
  
 如果您声明一个变量而无需使用`As`子句并将其设置为`Nothing`，变量有一种类型的`Object`。 在这种情况下出现任何编译时错误时`Option Strict`位于和`Option Infer`上。 此示例是`Dim something = Nothing`。  
  
### <a name="default-data-types-and-values"></a>默认数据类型和值  
 下表描述了指定的数据类型和初始值设定项中的各种组合的结果[Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)。  
  
|是否指定数据类型？|是否指定初始值设定项？|示例|结果|  
|---|---|---|---|  
|否|否|`Dim qty`|如果 `Option Strict` 处于关闭状态（默认），则将变量设置为 `Nothing`。<br /><br /> 如果 `Option Strict` 处于打开状态，则发生编译时错误。|  
|否|是|`Dim qty = 5`|如果 `Option Infer` 处于打开状态（默认），则变量采用初始值设定项的数据类型。 请参阅[局部类型推理](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)。<br /><br /> 如果 `Option Infer` 和 `Option Strict` 均处于关闭状态，则变量采用 `Object` 的数据类型。<br /><br /> 如果 `Option Infer` 处于关闭状态但 `Option Strict` 处于打开状态，则发生编译时错误。|  
|是|否|`Dim qty As Integer`|将变量初始化为数据类型的默认值。 有关详细信息，请参阅[Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)。|  
|是|是|`Dim qty  As Integer = 5`|如果初始值设定项的数据类型不可转换为指定数据类型，则会发生编译时错误。|  
  
## <a name="when-an-option-strict-statement-is-not-present"></a>当 Option Strict 语句不存在时  
 如果源代码不包含`Option Strict`语句， **Option strict**上设置[编译页，项目设计器 (Visual Basic 中)](https://docs.microsoft.com/visualstudio/ide/reference/compile-page-project-designer-visual-basic)使用。 **编译页**具有提供更多控制权生成错误的条件的设置。  
  
 如果你正在使用命令行编译器，则可以使用[/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)编译器选项指定的设置`Option Strict`。  
  
### <a name="to-set-option-strict-in-the-ide"></a>若要在 IDE 中设置 Option Strict  
[!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
1.  在**解决方案资源管理器**，选择一个项目。 在**项目**菜单上，单击**属性**。 有关详细信息，请参阅[项目设计器简介](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7)。  
  
2.  在**编译**选项卡上，在设置的值**Option Strict**框。  
  
###  <a name="conditions"></a>若要在 IDE 中设置警告配置  
 当您使用[编译页，项目设计器 (Visual Basic 中)](https://docs.microsoft.com/visualstudio/ide/reference/compile-page-project-designer-visual-basic)而不是`Option Strict`语句中，您有更多控制权会生成错误的条件。 **警告配置**部分**编译页**具有对应的三个条件会导致编译时错误的设置时`Option Strict`上。 这些设置如下︰  
  
-   **隐式转换**  
  
-   **后期绑定;调用可能在运行时失败**  
  
-   **隐式类型;假定为对象**  
  
 当您将设置**Option Strict**到**上**，所有这三个警告配置设置设置为**错误**。 当您将设置**Option Strict**到**关闭**，所有三个设置设置为**无**。  
  
 你可以单独更改将设置为每个警告配置**无**，**警告**，或**错误**。 如果所有三个警告的配置设置都设置为**错误**，`On`将出现在`Option strict`框。 如果所有三个设置为**无**，`Off`出现在此框中。 有关这些设置的任何其他组合**（自定义）**出现。  
  
### <a name="to-set-the-option-strict-default-setting-for-new-projects"></a>若要设置 Option Strict 的默认设置为新项目  
 当您创建项目时， **Option Strict**上设置**编译**选项卡上设置为**Option Strict**中设置**选项**对话框。  
  
 若要设置`Option Strict`在此对话框中，在**工具**菜单上，单击**选项**。 在**选项**对话框框中，展开**项目和解决方案**，然后单击**VB 默认值**。 中的初始默认设置**VB 默认值**是`Off`。  
  
### <a name="to-set-option-strict-on-the-command-line"></a>若要在命令行上设置 Option Strict  
 包括[/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)中的编译器选项**vbc**命令。  
  
## <a name="example"></a>示例  
 下面的示例演示了编译时错误引起的缩窄转换的隐式类型转换。 这类错误对应于**隐式转换**条件**编译页**。  
  
 [!code-vb[VbVbalrStatements #&161;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/option-strict-statement_1.vb)]  
  
## <a name="example"></a>示例  
 下面的示例演示了编译时错误引起的后期绑定。 这类错误对应于**Late 绑定; 调用可能在运行时失败**条件**编译页**。  
  
 [!code-vb[VbVbalrStatements #&162;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/option-strict-statement_2.vb)]  
  
## <a name="example"></a>示例  
 下面的示例演示使用隐式类型的声明的变量引起的错误`Object`。 这类错误对应于**隐式类型; 假定为对象**条件**编译页**。  
  
 [!code-vb[VbVbalrStatements #&163;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/option-strict-statement_3.vb)]  
  
 [!code-vb[VbVbalrStatements #&164;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/option-strict-statement_4.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [扩大转换和收缩转换](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [隐式和显式转换](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [“项目设计器”->“编译”页 (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/compile-page-project-designer-visual-basic)   
 [Option Explicit 语句](../../../visual-basic/language-reference/statements/option-explicit-statement.md)   
 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [如何︰ 访问对象的成员](../../../visual-basic/programming-guide/language-features/variables/how-to-access-members-of-an-object.md)   
 [XML 中的嵌入式的表达式](../../../visual-basic/programming-guide/language-features/xml/embedded-expressions-in-xml.md)   
 [宽松的委托转换](../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)   
 [Office 解决方案中的后期绑定](https://msdn.microsoft.com/library/3xxe951d)   
 [/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)   
 [“选项”对话框 ->“项目”->“Visual Basic 默认值”](https://docs.microsoft.com/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)
