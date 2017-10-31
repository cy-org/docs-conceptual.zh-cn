---
title: "Event 语句 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Event
- vb.Custom
dev_langs:
- VB
helpviewer_keywords:
- Event statement
- declaring events, syntax
- Public keyword, Event statements
- Custom keyword
- declarations, events
- event keyword [Visual Basic]
- WithEvents keyword, Event statements
- events [Visual Basic], declaring
- ByVal keyword, Event statements
- events [Visual Basic], custom
- ByRef keyword, Event statements
- declaring user-defined events
ms.assetid: 306ff8ed-74dd-4b6a-bd2f-e91b17474042
caps.latest.revision: 33
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
ms.openlocfilehash: b0ea8074f996622df3cd88a7e87fc1156b63dcaf
ms.lasthandoff: 03/13/2017

---
# <a name="event-statement"></a>Event 语句
声明用户定义的事件。  
  
## <a name="syntax"></a>语法  
  
```  
[ <attrlist> ] [ accessmodifier ] _  
[ Shared ] [ Shadows ] Event eventname[(parameterlist)] _  
[ Implements implementslist ]  
' -or-  
[ <attrlist> ] [ accessmodifier ] _  
[ Shared ] [ Shadows ] Event eventname As delegatename _  
[ Implements implementslist ]  
' -or-  
 [ <attrlist> ] [ accessmodifier ] _  
[ Shared ] [ Shadows ] Custom Event eventname As delegatename _  
[ Implements implementslist ]  
   [ <attrlist> ] AddHandler(ByVal value As delegatename)  
      [ statements ]  
   End AddHandler  
   [ <attrlist> ] RemoveHandler(ByVal value As delegatename)  
      [ statements ]  
   End RemoveHandler  
   [ <attrlist> ] RaiseEvent(delegatesignature)  
      [ statements ]  
   End RaiseEvent  
End Event  
```  
  
## <a name="parts"></a>部件  
  
|部件|说明|  
|---|---|  
|`attrlist`|可选。 应用于此事件的特性列表。 用逗号分隔多个属性。 必须将括[属性列表](../../../visual-basic/language-reference/statements/attribute-list.md)在尖括号 ("`<`"和"`>`")。|  
|`accessmodifier`|可选。 指定哪些代码可以访问事件。 可以是以下各项之一：<br /><br /> -   [公共](../../../visual-basic/language-reference/modifiers/public.md)— 任何代码都可以访问声明它的元素可以访问它。<br />-   [受保护的](../../../visual-basic/language-reference/modifiers/protected.md)— 只有它的类或派生的类中的代码可以访问它。<br />-   [友元](../../../visual-basic/language-reference/modifiers/friend.md)— 只有同一个程序集中的代码可以访问它。<br />-   [专用](../../../visual-basic/language-reference/modifiers/private.md)— 仅在声明它的元素中的代码可以访问它。<br /><br /> 可以指定 `Protected Friend` 以便可以从事件的类、派生类或相同程序集中的代码进行访问。|  
|`Shared`|可选。 指定此事件不与类或结构的特定实例关联。|  
|`Shadows`|可选。 指示此事件重新声明并隐藏基类中具有相同名称的编程元素（或重载元素集）。 可以与任何其他类型一起隐藏任何类型的已声明元素。<br /><br /> 隐藏的元素不可在隐藏它的派生类中使用（除了从隐藏元素不可访问的位置）。 例如，如果 `Private` 元素隐藏一个基类元素，则无权访问 `Private` 元素的代码会改为访问该基类元素。|  
|`eventname`|必需。 事件的名称；遵循标准变量命名约定。|  
|`parameterlist`|可选。 表示此事件的参数的本地变量列表。 必须将括[参数列表](../../../visual-basic/language-reference/statements/parameter-list.md)在括号中。|  
|`Implements`|可选。 指示此事件实现接口的事件。|  
|`implementslist`|如果提供 `Implements`，则是必需的。 所实现的 `Sub` 过程的列表。 用逗号分隔多个过程：<br /><br /> *implementedprocedure* [， *implementedprocedure* ...]<br /><br /> 每个 `implementedprocedure` 都具有以下语法和部件：<br /><br /> `interface`.`definedname`<br /><br /> -   `interface`-必需。 此过程的包含类或结构所实现的接口的名称。<br />-   `Definedname`-必需。 在 `interface` 中用于定义过程的名称。 这不必与 `name`（此过程用于实现定义的过程的名称）相同。|  
|`Custom`|必需。 声明为 `Custom` 的事件必须定义自定义 `AddHandler`、`RemoveHandler` 和 `RaiseEvent` 访问器。|  
|`delegatename`|可选。 指定事件处理程序签名的委托的名称。|  
|`AddHandler`|必需。 声明 `AddHandler` 访问器，它指定要在添加事件处理程序（显式使用 `AddHandler` 语句或隐式使用 `Handles` 子句）时执行的语句。|  
|`End AddHandler`|必需。 终止 `AddHandler` 块。|  
|`value`|必需。 参数名。|  
|`RemoveHandler`|必需。 声明 `RemoveHandler` 访问器，它指定要在使用 `RemoveHandler` 语句移除事件处理程序时执行的语句。|  
|`End RemoveHandler`|必需。 终止 `RemoveHandler` 块。|  
|`RaiseEvent`|必需。 声明 `RaiseEvent` 访问器，它指定要在使用 `RaiseEvent` 语句引发事件时执行的语句。 通常这会调用由 `AddHandler` 和 `RemoveHandler` 访问器维护的委托的列表。|  
|`End RaiseEvent`|必需。 终止 `RaiseEvent` 块。|  
|`delegatesignature`|必需。 与 `delegatename` 委托需要的参数匹配的参数列表。 必须将括[参数列表](../../../visual-basic/language-reference/statements/parameter-list.md)在括号中。|  
|`statements`|可选。 包含 `AddHandler`、`RemoveHandler` 和 `RaiseEvent` 方法体的语句。|  
|`End Event`|必需。 终止 `Event` 块。|  
  
## <a name="remarks"></a>备注  
 一旦声明了事件，便可使用 `RaiseEvent` 语句引发事件。 可以按以下片段所示声明和引发典型事件：  
  
 [!code-vb[VbVbalrEvents #&13;](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/event-statement_1.vb)]  
  
> [!NOTE]
>  可以正如处理过程的参数一样来声明事件参数，不过有以下例外：事件不能具有命名参数、`ParamArray` 参数或 `Optional` 参数。 事件没有返回值。  
  
 若要处理事件，必须使用 `Handles` 或 `AddHandler` 语句将它与事件处理程序子例程关联。 子例程和事件的签名必须匹配。 若要处理共享事件，必须使用 `AddHandler` 语句。  
  
 只能在模块级别使用 `Event`。 这意味着*声明上下文*事件必须是类、 结构、 模块或接口，并且不能为源文件、 命名空间、 过程或块。 有关详细信息，请参阅[声明上下文和默认访问级别](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)。  
  
 在大多数情况下，可以使用本主题的“语法”部分中的第一个语法来声明事件。 但是，某些情况要求更好地控制事件的详细行为。 使用本主题“语法”部分中的最后一个语法（该语法使用 `Custom` 关键字）可通过使你可以定义自定义事件来提供这种控制。 在自定义事件中，可精确地指定在代码对事件添加或移除事件处理程序时，或是代码引发事件时发生的情况。 有关示例，请参阅[如何︰ 声明节省内存到自定义事件](../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-conserve-memory.md)和[如何︰ 声明自定义事件为避免阻塞](../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-avoid-blocking.md)。  
  
## <a name="example"></a>示例  
 下面的示例使用事件从 10 秒到 0 秒进行倒计时。 代码演示了几个与事件相关的方法、属性和语句。 这包括 `RaiseEvent` 语句。  
  
 引发事件的类是事件源，处理事件的方法是事件处理程序。 事件源对于它生成的事件可以具有多个处理程序。 类引发事件时，会在选择用于为对象的该实例处理事件的每个类上引发该事件。  
  
 该示例还使用一个窗体 (`Form1`)，其中包含一个按钮 (`Button1`) 和一个文本框 (`TextBox1`)。 单击该按钮时，第一个文本框显示从 10 秒到 0 秒的倒计时。 经过了全部时间（10 秒）之后，第一个文本框会显示“Done”。  
  
 `Form1` 的代码指定窗体的初始和最终状态。 它还包含引发事件时执行的代码。  
  
 若要使用此示例，请打开新的 Windows 窗体项目。 然后向名为 `Form1` 的主窗体添加一个名为 `Button1` 的按钮和一个名为 `TextBox1` 的文本框。 右键单击该表单，然后单击**查看代码**以打开代码编辑器。  
  
 向 `Form1` 类的声明部分添加一个 `WithEvents` 变量：  
  
 [!code-vb[VbVbalrEvents #&14;](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/event-statement_2.vb)]  
  
 将下面的代码添加到 `Form1` 的代码： 替换可能存在的任何重复过程，如 `Form_Load` 或 `Button_Click`。  
  
 [!code-vb[VbVbalrEvents #&15;](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/event-statement_3.vb)]  
  
 按 F5 以运行前面的示例中，并单击标记为按钮**启动**。 第一个文本框中开始倒计时秒数。 经过了全部时间（10 秒）之后，第一个文本框会显示“Done”。  
  
> [!NOTE]
>  `My.Application.DoEvents` 方法不会按照与窗体相同的方式来处理事件。 若要使窗体可以直接处理事件，可以使用多线程处理。 有关详细信息，请参阅[线程处理](http://msdn.microsoft.com/library/552f6c68-dbdb-4327-ae36-32cf9063d88c)。  
  
## <a name="see-also"></a>另请参阅  
 [RaiseEvent 语句](../../../visual-basic/language-reference/statements/raiseevent-statement.md)   
 [Implements 语句](../../../visual-basic/language-reference/statements/implements-statement.md)   
 [事件](../../../visual-basic/programming-guide/language-features/events/index.md)   
 [AddHandler 语句](../../../visual-basic/language-reference/statements/addhandler-statement.md)   
 [RemoveHandler 语句](../../../visual-basic/language-reference/statements/removehandler-statement.md)   
 [句柄](../../../visual-basic/language-reference/statements/handles-clause.md)   
 [Delegate 语句](../../../visual-basic/language-reference/statements/delegate-statement.md)   
 [如何︰ 声明自定义事件以节省内存](../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-conserve-memory.md)   
 [如何︰ 声明自定义事件以避免阻止](../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-avoid-blocking.md)   
 [共享](../../../visual-basic/language-reference/modifiers/shared.md)   
 [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md)
