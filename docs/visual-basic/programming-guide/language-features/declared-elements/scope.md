---
title: "Visual Basic 中的范围 | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "块范围"
  - "已声明的元素, 范围"
  - "范围级别"
  - "模块级别"
  - "模块范围"
  - "命名空间, 范围"
  - "过程范围"
  - "过程, 范围"
  - "范围, 关于范围"
  - "范围, 已声明的元素"
  - "范围, 等级"
  - "范围, Visual Basic"
ms.assetid: 208106fe-79c9-4eec-93c6-55f08548895f
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# Visual Basic 中的范围
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

已声明的元素的范围为一个代码集合，其中包括所有不用限定元素的名称即可引用元素的代码，或所有不必通过 [Imports 语句（.NET 命名空间和类型）](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md) 使元素可用即可引用元素的代码。  元素可以具有下列范围级别之一：  
  
|级别|说明|  
|--------|--------|  
|块范围|只适用于在其中声明元素的代码块|  
|过程范围|适用于在其中声明元素的过程中的所有代码|  
|模块范围|适用于在其中声明元素的模块、类或结构中的所有代码|  
|命名空间范围|适用于在其中声明元素的命名空间中的所有代码|  
  
 这些范围级别从最窄（块）直到最宽（命名空间），其中“最窄的范围”是指不用限定即可引用元素的最小代码集。  有关更多信息，请参见本页中的“范围级别”。  
  
## 指定范围和定义变量  
 在声明元素时指定元素的范围。  范围取决于下列因素：  
  
-   声明元素的区域（块、过程、模块、类或结构）  
  
-   包含元素声明的命名空间  
  
-   为元素声明的访问级别  
  
 在不同的范围内用相同的名称定义变量时要小心，因为这样做可能导致意外的结果。  有关更多信息，请参见 [对已声明元素的引用](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)。  
  
## 范围级别  
 编程元素在声明它的整个区域内都可用。  同一区域内的所有代码不用限定元素的名称即可引用元素。  
  
### 块范围  
 块是初始声明语句与终止声明语句之间的一组语句，如下所示：  
  
-   `Do` 和 `Loop`  
  
-   `For` \[`Each`\] 和 `Next`  
  
-   `If` 和 `End If`  
  
-   `Select` 和 `End Select`  
  
-   `SyncLock` 和 `End SyncLock`  
  
-   `Try` 和 `End Try`  
  
-   `While` 和 `End While`  
  
-   `With` 和 `End With`  
  
 在某个块声明的变量只能在该块中使用。  在下面的示例中，整数变量 `cube` 的范围是 `If` 和 `End If` 之间的块，并且，在执行超出该块后便不能再引用 `cube`。  
  
```  
If n < 1291 Then  
    Dim cube As Integer  
    cube = n ^ 3  
End If  
```  
  
> [!NOTE]
>  即使变量的范围被限制在某个块内，其生存期仍为整个过程的生存期。  如果您在过程的生存期内多次进入该块，则每个块变量会保留它的前一个值。  若要避免在这种情况下出现意外结果，最好在块的开头对块变量进行初始化。  
  
### 过程范围  
 在某过程内声明的元素在该过程外不可用。  只有包含元素声明的过程才能使用该元素。  该级别的变量也称为“局部变量”。  使用 [Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md) 声明这些变量，使用或不使用 [Static](../../../../visual-basic/language-reference/modifiers/static.md) 关键字。  
  
 过程范围和块范围密切相关。  如果在过程内但在该过程内的任何块外声明变量，则可将该变量看作具有块范围，其中块就是整个过程。  
  
> [!NOTE]
>  所有的局部元素对它们出现在其中的过程来说都是私有的，即使它们是 `Static` 变量。  不能在过程中使用 [Public](../../../../visual-basic/language-reference/modifiers/public.md) 关键字声明任何元素。  
  
### 模块范围  
 为方便起见，单个术语*“模块级别”*同等地应用于模块、类和结构。  可以通过将声明语句放在模块、类或结构中的任一过程或块的外部来声明该级别的元素。  
  
 当在模块级声明时，由所选的访问级别确定范围。  包含模块、类或结构的命名空间也影响范围。  
  
 为其声明 [Private](../../../../visual-basic/language-reference/modifiers/private.md) 访问级别的元素可用于该模块内的每个过程，但不能用于其他模块中的任何代码。  如果不使用任何访问级别关键字，则模块级 `Dim` 语句默认为 `Private`。  但是，通过在 `Dim` 语句中使用 `Private` 关键字，可以使范围和访问级别更明显。  
  
 在下面的示例中，所有在模块中定义的过程均可以引用字符串变量 `strMsg`。  当调用第二个过程时，它在对话框中显示字符串变量 `strMsg` 的内容。  
  
```  
' Put the following declaration at module level (not in any procedure).  
Private strMsg As String  
' Put the following Sub procedure in the same module.  
Sub initializePrivateVariable()  
    strMsg = "This variable cannot be used outside this module."  
End Sub  
' Put the following Sub procedure in the same module.  
Sub usePrivateVariable()  
    MsgBox(strMsg)  
End Sub  
```  
  
### 命名空间范围  
 如果使用 [Friend](../../../../visual-basic/language-reference/modifiers/friend.md) 或 [Public](../../../../visual-basic/language-reference/modifiers/public.md) 关键字声明模块级元素，则该元素变为可用于在其中声明该元素的整个命名空间内的所有过程。  对上述示例进行如下更改后，字符串变量 `strMsg` 可由它的声明命名空间内任意位置的代码引用。  
  
```  
' Include this declaration at module level (not inside any procedure).  
Public strMsg As String  
```  
  
 命名空间范围包括嵌套命名空间。  可从命名空间内使用的元素同样可从该命名空间中的任何嵌套命名空间内使用。  
  
 如果项目中不包含任何 [Namespace 语句](../../../../visual-basic/language-reference/statements/namespace-statement.md)，则该项目中的所有内容全部在同一命名空间中。  在这种情况下，可以将命名空间作用域视为项目作用域。  模块、类或结构中的 `Public` 元素也可供引用其项目的任何项目使用。  
  
## 范围选择  
 声明变量时，应该在选择其范围时注意以下几点。  
  
### 局部变量的优点  
 对于任何类型的临时计算，局部变量都是很好的选择，原因如下：  
  
-   **可避免名称冲突。**局部变量名称不易发生冲突。  例如，可以创建若干个不同的过程，每个过程都包含称为 `intTemp` 的变量。  只要每个 `intTemp` 都被声明为局部变量，各过程就只识别自己版本的 `intTemp` 变量。  任何一个过程都可以修改其局部变量 `intTemp` 的值，而不会影响到其他过程中的 `intTemp` 变量。  
  
-   **内存消耗。**局部变量只在其过程运行时占用内存。  当过程返回到调用代码时，会释放其内存。  相形之下，[Shared](../../../../visual-basic/language-reference/modifiers/shared.md) 和 [Static](../../../../visual-basic/language-reference/modifiers/static.md) 变量在应用程序停止运行前将一直占用内存资源，因此，仅在必要时使用这些变量。  实例变量在其实例继续存在的同时占用内存，因此不如局部变量有效，但可能会比 `Shared` 或 `Static` 变量更为有效。  
  
### 将范围最小化  
 一般情况下，在声明任何变量或常数时，使其范围尽可能窄（块范围最窄）是好的编程习惯。  这有助于保留内存，并可最大限度地减少代码错误地引用错误变量的机会。  同样，仅当有必要在过程调用之间保留值时，才应将变量声明为 [Static](../../../../visual-basic/language-reference/modifiers/static.md)。  
  
## 请参阅  
 [已声明元素的特性](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)   
 [如何：控制变量的范围](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-control-the-scope-of-a-variable.md)   
 [Visual Basic 中的生存期](../../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md)   
 [Visual Basic 中的访问级别](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)   
 [对已声明元素的引用](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [变量声明](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)