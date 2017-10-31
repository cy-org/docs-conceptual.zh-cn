---
title: "如何：修改标准控件中的键盘输入 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "键盘输入, 修改"
  - "键盘, 键盘输入"
  - "修改键盘输入"
  - "Windows 窗体, 修改键盘输入"
ms.assetid: 626d3712-d866-4988-bcda-a2d5b36ec0ba
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：修改标准控件中的键盘输入
Windows 窗体提供使用和修改键盘输入的功能。  使用键是指处理方法或事件处理程序内的键，以便消息队列更低处的其他方法和事件不会接收到键值。  修改键是指修改键的值，以便消息队列更低处的方法和事件处理程序接收不同的键值。  本主题演示如何完成这些任务。  
  
### 若要使用键  
  
-   在 <xref:System.Windows.Forms.Control.KeyPress> 事件处理程序中，将 <xref:System.Windows.Forms.KeyPressEventArgs> 类的 <xref:System.Windows.Forms.KeyPressEventArgs.Handled%2A> 属性设置为 `true`。  
  
     \- 或 \-  
  
     在 <xref:System.Windows.Forms.Control.KeyDown> 事件处理程序中，将 <xref:System.Windows.Forms.KeyEventArgs> 类的 <xref:System.Windows.Forms.KeyEventArgs.Handled%2A> 属性设置为 `true`。  
  
    > [!NOTE]
    >  设置 <xref:System.Windows.Forms.Control.KeyDown> 事件处理程序中的 <xref:System.Windows.Forms.KeyEventArgs.Handled%2A> 属性不会防止 <xref:System.Windows.Forms.Control.KeyPress> 和 <xref:System.Windows.Forms.Control.KeyUp> 事件因当前按键而引发。  要实现此目的，请使用 <xref:System.Windows.Forms.KeyEventArgs.SuppressKeyPress%2A> 属性。  
  
     以下示例是取自 `switch` 语句的摘要，可检查 <xref:System.Windows.Forms.Control.KeyPress> 事件处理程序接收的 <xref:System.Windows.Forms.KeyPressEventArgs> 的 <xref:System.Windows.Forms.KeyPressEventArgs.KeyChar%2A> 属性。  此代码使用“A”和“a”字符键。  
  
     [!code-csharp[System.Windows.Forms.KeyBoardInput#6](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/CS/form1.cs#6)]
     [!code-vb[System.Windows.Forms.KeyBoardInput#6](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/VB/form1.vb#6)]  
  
### 若要修改标准字符键  
  
-   在 <xref:System.Windows.Forms.Control.KeyPress> 事件处理程序中，将 <xref:System.Windows.Forms.KeyPressEventArgs> 类的 <xref:System.Windows.Forms.KeyPressEventArgs.KeyChar%2A> 属性设置为新字符键的值。  
  
     以下示例是取自 `switch` 语句的摘要，可将“A”修改为“B”，将“b”修改为“a”。  请注意，<xref:System.Windows.Forms.KeyPressEventArgs> 参数的 <xref:System.Windows.Forms.KeyPressEventArgs.Handled%2A> 属性设置为 `false`，以便将新的键值传播至消息队列中的其他方法和事件。  
  
     [!code-csharp[System.Windows.Forms.KeyBoardInput#7](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/CS/form1.cs#7)]
     [!code-vb[System.Windows.Forms.KeyBoardInput#7](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/VB/form1.vb#7)]  
  
### 若要修改非字符键  
  
-   重写 <xref:System.Windows.Forms.Control> 方法，此方法可处理 Windows 消息，检测 WM\_KEYDOWN 或 WM\_SYSKEYDOWN 消息，并将 <xref:System.Windows.Forms.Message> 参数的 <xref:System.Windows.Forms.Message.WParam%2A> 属性设置为 <xref:System.Windows.Forms.Keys> 值（表示新的非字符键）。  
  
     以下代码示例演示如何重写控件的 <xref:System.Windows.Forms.Control.PreProcessMessage%2A> 方法以检测 F1 至 F9 键并将任一 F3 按键修改为 F1。  有关可对其重写以截获键盘消息的 <xref:System.Windows.Forms.Control> 方法的详细信息，请参阅 [Windows 窗体应用程序中的用户输入](../../../docs/framework/winforms/user-input-in-a-windows-forms-application.md)和[键盘输入工作原理](../../../docs/framework/winforms/how-keyboard-input-works.md)。  
  
     [!code-csharp[System.Windows.Forms.KeyBoardInput#12](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/CS/form1.cs#12)]
     [!code-vb[System.Windows.Forms.KeyBoardInput#12](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/VB/form1.vb#12)]  
  
## 示例  
 以下代码示例显示前几节中的代码示例的完整应用程序。  应用程序使用派生自 <xref:System.Windows.Forms.TextBox> 类的自定义控件来使用和修改键盘输入。  
  
 [!code-csharp[System.Windows.Forms.KeyBoardInput#0](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/CS/form1.cs#0)]
 [!code-vb[System.Windows.Forms.KeyBoardInput#0](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.KeyboardInput/VB/form1.vb#0)]  
  
## 编译代码  
 此示例需要：  
  
-   对 System、System.Drawing 和 System.Windows.Forms 程序集的引用。  
  
 有关从 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 或 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] 命令行生成此示例的信息，请参阅[从命令行生成](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) 或[在命令行上使用 csc.exe 生成](../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)。  还可以通过将代码粘贴到新项目，在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中生成此示例。  另请参阅[如何：使用 Visual Studio 编译和运行完整的 Windows 窗体代码示例](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\))。  
  
## 请参阅  
 [Windows 窗体应用程序中的键盘输入](../../../docs/framework/winforms/keyboard-input-in-a-windows-forms-application.md)   
 [Windows 窗体应用程序中的用户输入](../../../docs/framework/winforms/user-input-in-a-windows-forms-application.md)   
 [键盘输入工作原理](../../../docs/framework/winforms/how-keyboard-input-works.md)