---
title: "演练︰ 调用 Windows Api (Visual Basic 中) |Microsoft 文档"
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
- DLLs, calling
- Windows API, walkthroughs
- platform invoke, walkthroughs
- API calls, walkthroughs [Visual Basic]
- Windows API, calling
- walkthroughs [Visual Basic], API calls
- DllImport attribute, calling Windows API
- Declare statement, declaring DLL functions
ms.assetid: 9280ca96-7a93-47a3-8d01-6d01be0657cb
caps.latest.revision: 20
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
ms.openlocfilehash: 5001ccebb0a5b8cadd4e856342601506cf1d033f
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-calling-windows-apis-visual-basic"></a>演练：调用 Windows API (Visual Basic)
Windows Api 都是动态链接库 (Dll) 的 Windows 操作系统的一部分。 您可以使用它们来执行任务时都很难编写您自己的等效的过程。 例如，Windows 提供了一个名为函数`FlashWindowEx`，能让你将应用程序的标题栏显现深色和浅色之间交替。  
  
 在您的代码中使用 Windows Api 的优点是它们可以节省开发时间，因为它们包含大量有用的功能，已经编写并等待使用。 缺点是 Windows Api 可能很难处理和铁面无私出现故障时。  
  
 Windows Api 表示一类特殊的互操作性。 Windows Api 不使用托管的代码，并没有内置类型库，并使用有别于那些与 Visual Studio 一起使用的数据类型。 由于这些差异，并且因为 Windows Api 不是 COM 对象，与 Windows Api 互操作性和[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]执行使用平台调用，或 PInvoke。 平台调用是一种服务使托管代码能够调用非托管的 Dll 中实现的函数。 有关详细信息，请参阅[使用非托管 DLL 函数](http://msdn.microsoft.com/library/eca7606e-ebfb-4f47-b8d9-289903fdc045)。 您可以使用中的 PInvoke[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]使用`Declare`语句或应用`DllImport`属性设为一个空过程。  
  
 Windows API 调用了一个重要组成部分[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]编程在过去，但很少必要时使用[!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)]。 只要有可能，应使用托管的代码的[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]来执行任务，而不是 Windows API 调用。 本演练提供了用于在使用这些情况的信息是必需的 Windows Api。  
  
[!INCLUDE[note_settings_general](../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
## <a name="api-calls-using-declare"></a>使用 API 调用声明  
 调用 Windows Api 的最常见方法是通过使用`Declare`语句。  
  
#### <a name="to-declare-a-dll-procedure"></a>若要声明一个 DLL 过程  
  
1.  确定你想要调用，该函数及其参数、 参数类型的名称和返回值，以及名称和包含该 DLL 的位置。  
  
    > [!NOTE]
    >  有关 Windows Api 的完整信息，请参阅平台 SDK Windows API 中的 Win32 SDK 文档。 有关 Windows Api 使用的常量的详细信息，检查如 Windows.h Platform SDK 中包含的标头文件。  
  
2.  通过单击以打开新的 Windows 应用程序项目**新建**上**文件**菜单，并单击**项目**。 此时将出现 **“新建项目”** 对话框。  
  
3.  选择**Windows 应用程序**从列表中[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]项目模板。 将显示新项目。  
  
4.  将以下代码添加`Declare`函数到类或想要使用的 DLL 的模块︰  
  
     [!code-vb[VbVbalrInterop #&9;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_1.vb)]  
  
### <a name="parts-of-the-declare-statement"></a>部件的 Declare 语句  
 `Declare`语句包括以下元素。  
  
#### <a name="auto-modifier"></a>Auto 修饰符  
 `Auto`修饰符指示运行时转换基于根据公共语言运行时规则 （或已指定的别名） 的方法名称的字符串。  
  
#### <a name="lib-and-alias-keywords"></a>Lib 和别名关键字  
 名称以下`Function`关键字是您的程序用来访问导入的函数的名称。 它可以是您要调用的函数的实际名称相同，也可以使用任何有效的过程名称，然后采用`Alias`关键字来指定要调用的函数的真实名称。  
  
 指定`Lib`关键字后, 跟的名称和包含要调用的函数的 dll 的位置。 不需要指定位于 Windows 系统目录中的文件的路径。  
  
 使用`Alias`如果要调用的函数的名称不是有效的关键字[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]过程名称，或者与您的应用程序中的其他项的名称冲突。 `Alias`指示要调用的函数的真实名称。  
  
#### <a name="argument-and-data-type-declarations"></a>参数和数据类型声明  
 声明的参数和它们的数据类型。 此部分会很困难，因为 Windows 所使用的数据类型并不对应于 Visual Studio 的数据类型。 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]通过将参数转换为兼容的数据类型，名为的过程为您完成大量工作*封送处理*。 您可以显式控制参数封送的方式使用<xref:System.Runtime.InteropServices.MarshalAsAttribute>中定义特性<xref:System.Runtime.InteropServices>命名空间。</xref:System.Runtime.InteropServices> </xref:System.Runtime.InteropServices.MarshalAsAttribute>  
  
> [!NOTE]
>  以前版本的[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]允许您声明参数`As Any`，这意味着这些数据的任何数据就可以使用类型。 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]需要对所有使用特定的数据类型`Declare`语句。  
  
#### <a name="windows-api-constants"></a>Windows API 常量  
 某些参数是常量的组合。 例如，`MessageBox`在本演练中所示的 API 接受整数参数调用`Typ`，它控制如何显示消息框。 可以通过检查来确定这些常量的数值`#define`文件 WinUser.h 中的语句。 以十六进制形式，通常显示的数字值，因此您可能希望使用一个计算器来将它们添加并将转换为十进制。 例如，如果您想要合并的感叹号样式的常量`MB_ICONEXCLAMATION`0x00000030 和是 / 无样式`MB_YESNO`0x00000004，你可以将数字并获取结果 0x00000034 52 十进制。 尽管可以直接使用十进制的结果，则最好将这些值声明为您的应用程序中的常量并将其组合使用`Or`运算符。  
  
###### <a name="to-declare-constants-for-windows-api-calls"></a>可以声明为 Windows API 调用的常量  
  
1.  查阅文档以获取要调用的 Windows 函数。 确定使用的常数的名称以及包含这些常量的数值的.h 文件的名称。  
  
2.  使用文本编辑器，如记事本，若要查看的内容标头 (.h) 文件，并查找与您使用的常量相关联的值。 例如， `MessageBox` API 使用常数`MB_ICONQUESTION`以在消息框中显示一个问号。 有关定义`MB_ICONQUESTION`都在 WinUser.h 中，且出现，如下所示︰  
  
     `#define MB_ICONQUESTION             0x00000020L`  
  
3.  添加等效`Const`到类或模块，以使这些常量可供您的应用程序的语句。 例如：  
  
     [!code-vb[VbVbalrInterop #&11;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_2.vb)]  
  
###### <a name="to-call-the-dll-procedure"></a>若要调用 DLL 的过程  
  
1.  添加名为的按钮`Button1`的启动窗体让你的项目，然后双击它以查看其代码。 显示的事件处理程序按钮。  
  
2.  将代码添加到`Click`您添加的按钮，以调用过程并提供适当的参数的事件处理程序︰  
  
     [!code-vb[VbVbalrInterop #&12;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_3.vb)]  
  
3.  通过按 F5 运行项目。 这两种显示消息框**是**和**否**响应按钮。 单击其中一种方法。  
  
#### <a name="data-marshaling"></a>数据封送处理  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]自动转换为数据类型的参数和返回值为 Windows API 调用，但您可以使用`MarshalAs`特性显式指定 API 预期的非托管的数据类型。 关于互操作封送处理的详细信息，请参阅[互操作封送处理](http://msdn.microsoft.com/library/115f7a2f-d422-4605-ab36-13a8dd28142a)。  
  
###### <a name="to-use-declare-and-marshalas-in-an-api-call"></a>API 调用中使用 Declare 和 MarshalAs  
  
1.  确定所需的参数、 调用数据类型的函数的名称，并返回值。  
  
2.  若要简化对访问`MarshalAs`特性，请添加`Imports`到类或模块，如以下示例所示的代码的顶部的语句︰  
  
     [!code-vb[VbVbalrInterop #&13;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_4.vb)]  
  
3.  将导入的函数的函数原型添加到类或模块使用的，并应用`MarshalAs`属性设为参数或返回值。 在下面的示例中，要求类型的 API 调用`void*`作为封送`AsAny`:  
  
     [!code-vb[VbVbalrInterop #&14;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_5.vb)]  
  
## <a name="api-calls-using-dllimport"></a>使用 DllImport API 调用  
 `DllImport`属性提供了不带类型库的 Dll 中调用函数的第二个方法。 `DllImport`大致相当于使用`Declare`语句，但可以更好地控制函数的调用方式。  
  
 您可以使用`DllImport`与大多数 Windows API 调用，只要该调用是指共享 (有时称为*静态*) 方法。 不能使用需要的类实例的方法。 与不同`Declare`语句，`DllImport`调用不能使用`MarshalAs`属性。  
  
#### <a name="to-call-a-windows-api-using-the-dllimport-attribute"></a>若要调用 Windows API 使用 DllImport 特性  
  
1.  通过单击以打开新的 Windows 应用程序项目**新建**上**文件**菜单，并单击**项目**。 此时将出现 **“新建项目”** 对话框。  
  
2.  选择**Windows 应用程序**从列表中[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]项目模板。 将显示新项目。  
  
3.  添加名为的按钮`Button2`到启动窗体。  
  
4.  双击`Button2`打开窗体的代码视图。  
  
5.  若要简化对访问`DllImport`，添加`Imports`语句将启动窗体类的代码的顶部︰  
  
     [!code-vb[VbVbalrInterop #&13;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_4.vb)]  
  
6.  声明一个空函数前面`End Class`语句窗体中，并将函数命名`MoveFile`。  
  
7.  应用`Public`和`Shared`函数声明和设置的参数的修饰符`MoveFile`根据 Windows API 函数使用的参数︰  
  
     [!code-vb[VbVbalrInterop #&16;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_6.vb)]  
  
     您的函数名称可以是任意有效的过程;`DllImport`属性指定的名称与 DLL 中。 它还可以处理的参数的互操作封送处理和返回值，以便您可以选择 Visual Studio 的数据类型包含类似于的数据类型的 API 使用。  
  
8.  应用`DllImport`属性设为空的函数。 第一个参数是名称和包含要调用的函数的 dll 的位置。 不需要指定位于 Windows 系统目录中的文件的路径。 第二个参数是一个命名的参数，指定 Windows API 中的函数的名称。 在此示例中，`DllImport`属性强制对调用`MoveFile`转发到`MoveFileW`KERNEL32 中。DLL 中。 `MoveFileW`方法将文件复制从路径`src`到路径`dst`。  
  
     [!code-vb[VbVbalrInterop #&17;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_7.vb)]  
  
9. 将代码添加到`Button2_Click`事件处理程序调用的函数︰  
  
     [!code-vb[VbVbalrInterop #&18;](../../../visual-basic/programming-guide/com-interop/codesnippet/VisualBasic/walkthrough-calling-windows-apis_8.vb)]  
  
10. 创建一个名为 Test.txt 文件并将其放在硬盘上的 C:\Tmp 目录中。 如有必要，请创建临时目录。  
  
11. 按 F5 键启动该应用程序。 主窗体将显示。  
  
12. 单击**Button2**。 如果可以移动该文件，将显示"该文件已成功移动"消息。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Runtime.InteropServices.DllImportAttribute></xref:System.Runtime.InteropServices.DllImportAttribute>   
 <xref:System.Runtime.InteropServices.MarshalAsAttribute></xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md)   
 [自动](../../../visual-basic/language-reference/modifiers/auto.md)   
 [别名](../../../visual-basic/language-reference/statements/alias-clause.md)   
 [COM 互操作](../../../visual-basic/programming-guide/com-interop/index.md)   
 [在托管代码中创建原型](http://msdn.microsoft.com/library/ecdcf25d-cae3-4f07-a2b6-8397ac6dc42d)   
 [一个委托作为回调方法进行封送](http://msdn.microsoft.com/library/6ddd7866-9804-4571-84de-83f5cc017a5a)
