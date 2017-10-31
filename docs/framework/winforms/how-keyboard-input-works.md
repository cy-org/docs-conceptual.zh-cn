---
title: "键盘输入工作原理 | Microsoft Docs"
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
  - "键盘输入, 关于键盘输入"
  - "键盘, 键盘输入"
  - "Windows 窗体, 键盘输入"
ms.assetid: 9a29433c-a180-49bb-b74c-d187786584c8
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# 键盘输入工作原理
Windows 窗体通过引发键盘事件来处理键盘输入以响应 Windows 消息。  大多数 Windows 窗体应用程序都通过处理键盘事件来以独占方式处理键盘输入。  但是，必须了解键盘消息的工作方式，才能实现更高级的键盘输入方案（如在按键到达控件之前截获它们）。  本主题描述 Windows 窗体能够识别的按键数据的类型，并概述键盘消息的传送方式。  有关键盘事件的信息，请参见 [使用键盘事件](../../../docs/framework/winforms/using-keyboard-events.md)。  
  
## 按键的类型  
 Windows 窗体将键盘输入标识为由按位 <xref:System.Windows.Forms.Keys> 枚举表示的虚拟键代码。  使用 <xref:System.Windows.Forms.Keys> 枚举，可以综合一系列按键以生成单个值。  这些值与 WM\_KEYDOWN 和 WM\_SYSKEYDOWN Windows 消息所伴随的值相对应。  可通过处理 <xref:System.Windows.Forms.Control.KeyDown> 或 <xref:System.Windows.Forms.Control.KeyUp> 事件来检测大多数物理按键操作。  字符键是 <xref:System.Windows.Forms.Keys> 枚举的子集，它们与 WM\_CHAR 和 WM\_SYSCHAR Windows 消息所伴随的值相对应。  如果通过组合按键得到一个字符，则可以通过处理 <xref:System.Windows.Forms.Control.KeyPress> 事件来检测该字符。  或者，可以使用由 Visual Basic 编程接口公开的 <xref:Microsoft.VisualBasic.Devices.Keyboard> 来发现已按下的键并发送它们。  有关更多信息，请参见 [访问键盘](../Topic/Accessing%20the%20Keyboard%20\(Visual%20Basic\).md)。  
  
## 键盘事件的顺序  
 正如上面列出的那样，在一个控件上可能出现三个与键盘相关的事件。  以下顺序是发生这些事件的常规顺序：  
  
1.  用户按“a”键，该键将被预处理和调度，而且会发生 <xref:System.Windows.Forms.Control.KeyDown> 事件。  
  
2.  用户按住“a”键，该键将被预处理和调度，而且会发生 <xref:System.Windows.Forms.Control.KeyPress> 事件。  
  
     在用户按住某个键时，此事件会发生多次。  
  
3.  用户松开“a”键，该键将被预处理和调度，而且会发生 <xref:System.Windows.Forms.Control.KeyUp> 事件。  
  
## 键的预处理  
 像其他消息一样，键盘消息是在窗体或控件的 <xref:System.Windows.Forms.Control.WndProc%2A> 方法中处理的。  但是，在处理键盘消息之前，<xref:System.Windows.Forms.Control.PreProcessMessage%2A> 方法会调用一个或多个方法，这些方法可被重写以处理特殊的字符键和物理按键。  您可以重写这些方法，以便在控件处理消息之前检测并筛选某些按键。  下表按照方法出现的顺序列出了正在执行的操作以及所出现的相关方法。  
  
### KeyDown 事件的预处理  
  
|操作|相关方法|注释|  
|--------|----------|--------|  
|检查命令键（如快捷键或菜单快捷键）。|<xref:System.Windows.Forms.Control.ProcessCmdKey%2A>|此方法处理命令键，命令键的优先级高于常规键。  如果此方法返回 `true`，则将不调度键消息，而且将不发生键事件。  如果此方法返回 `false`，则将调用 <xref:System.Windows.Forms.Control.IsInputKey%2A>`.`|  
|检查该键是否为需要预处理的特殊键，或者它是否为应引发 <xref:System.Windows.Forms.Control.KeyDown> 事件并且被调度到某个控件的普通字符键。|<xref:System.Windows.Forms.Control.IsInputKey%2A>|如果此方法返回 `true`，则表示该控件为常规字符，而且将引发 <xref:System.Windows.Forms.Control.KeyDown> 事件。  如果此方法返回 `false`，则将调用 <xref:System.Windows.Forms.Control.ProcessDialogKey%2A>。 **Note:**  为了确保控件获取某个键或键的组合，您可以处理 <xref:System.Windows.Forms.Control.PreviewKeyDown> 事件，并针对所需的键，将 <xref:System.Windows.Forms.PreviewKeyDownEventArgs> 的 <xref:System.Windows.Forms.PreviewKeyDownEventArgs.IsInputKey%2A> 设置为 `true`。|  
|检查该键是否为导航键（Esc、Tab、回车键或箭头键）。|<xref:System.Windows.Forms.Control.ProcessDialogKey%2A>|此方法处理在控件内实现特殊功能（如在控件及其父级之间切换焦点）的物理按键。  如果中间控件不处理该键，则将调用父控件的 <xref:System.Windows.Forms.Control.ProcessDialogKey%2A>，直至层次结构中的最顶端控件。  如果此方法返回 `true`，则将完成预处理，而且将不生成按键事件。  如果此方法返回 `false`，则将发生 <xref:System.Windows.Forms.Control.KeyDown> 事件。|  
  
### KeyPress 事件的预处理  
  
|操作|相关方法|注释|  
|--------|----------|--------|  
|检查该键是否为控件应当处理的普通字符|<xref:System.Windows.Forms.Control.IsInputChar%2A>|如果该字符是普通字符，则此方法返回 `true`，并且将引发 <xref:System.Windows.Forms.Control.KeyPress> 事件，而且不再进行预处理。  否则，将调用 <xref:System.Windows.Forms.Control.ProcessDialogChar%2A>。|  
|检查该字符是否为助记符（如按钮上的“确定\(&O\)”）|<xref:System.Windows.Forms.Control.ProcessDialogChar%2A>|类似于 <xref:System.Windows.Forms.Control.ProcessDialogKey%2A>，将沿控件的层次结构向上调用此方法。  如果控件是容器控件，此方法将通过调用控件及其子控件的 <xref:System.Windows.Forms.Control.ProcessMnemonic%2A> 来检查助记键。  如果 <xref:System.Windows.Forms.Control.ProcessDialogChar%2A> 返回 `true`，则 <xref:System.Windows.Forms.Control.KeyPress> 事件不会发生。|  
  
## 处理键盘消息  
 键盘消息在到达窗体或控件的 <xref:System.Windows.Forms.Control.WndProc%2A> 方法之后，它们将由一组可被重写的方法来处理。  其中的每种方法都返回一个 <xref:System.Boolean> 值，该值指定控件是否已处理和使用了键盘消息。  如果其中的某种方法返回 `true`，则键盘消息将被视为已处理，而且它将不传递到控件的基控件或父控件进行进一步处理。  否则，消息将停留在消息队列中，而且可能会在控件的基控件或父控件的其他方法中进行处理。  下表显示用来处理键盘消息的方法。  
  
|方法|注释|  
|--------|--------|  
|<xref:System.Windows.Forms.Control.ProcessKeyMessage%2A>|此方法处理由控件的 <xref:System.Windows.Forms.Control.WndProc%2A> 方法接收的所有键盘消息。|  
|<xref:System.Windows.Forms.Control.ProcessKeyPreview%2A>|此方法将键盘消息发送到控件的父控件。  如果 <xref:System.Windows.Forms.Control.ProcessKeyPreview%2A> 返回 `true`，则将不生成键事件；否则将调用 <xref:System.Windows.Forms.Control.ProcessKeyEventArgs%2A>。|  
|<xref:System.Windows.Forms.Control.ProcessKeyEventArgs%2A>|此方法根据需要引发 <xref:System.Windows.Forms.Control.KeyDown>、<xref:System.Windows.Forms.Control.KeyPress> 和 <xref:System.Windows.Forms.Control.KeyUp> 事件。|  
  
## 重写键盘方法  
 在预处理和处理键盘消息时，可以使用许多方法进行重写；但是，这些方法有好有坏。  下表显示可能需要完成的任务以及重写键盘方法的最佳方式。  有关重写方法的更多信息，请参见[NOT IN BUILD: Overriding Properties and Methods](http://msdn.microsoft.com/zh-cn/2167e8f5-1225-4b13-9ebd-02591ba90213)。  
  
|任务|方法|  
|--------|--------|  
|截获导航键并引发 <xref:System.Windows.Forms.Control.KeyDown> 事件。  例如，您希望在文本框中处理 Tab 和回车键。|重写 <xref:System.Windows.Forms.Control.IsInputKey%2A>。 **Note:**  此外，也可以处理 <xref:System.Windows.Forms.Control.PreviewKeyDown> 事件，并针对所需的一个或多个键，将 <xref:System.Windows.Forms.PreviewKeyDownEventArgs> 的 <xref:System.Windows.Forms.PreviewKeyDownEventArgs.IsInputKey%2A> 设置为 `true`。|  
|在控件上执行特殊的输入或导航处理。  例如，您可能希望在列表控件中使用箭头键更改选定项。|重写 <xref:System.Windows.Forms.Control.ProcessDialogKey%2A>|  
|截获导航键并引发 <xref:System.Windows.Forms.Control.KeyPress> 事件。  例如，您可能希望在数字显示框控件中，多次按箭头键来加快数值的设定速度。|重写 <xref:System.Windows.Forms.Control.IsInputChar%2A>。|  
|在发生 <xref:System.Windows.Forms.Control.KeyPress> 事件期间执行特殊的输入或导航处理。  例如，在列表控件中，按住“r”键将跳到以字母 r 开头的项并在这些项间切换。|重写 <xref:System.Windows.Forms.Control.ProcessDialogChar%2A>|  
|执行自定义的助记键处理；例如，您希望处理所有者描述的、包含在工具栏中的按钮上的助记键。|重写 <xref:System.Windows.Forms.Control.ProcessMnemonic%2A>。|  
  
## 请参阅  
 <xref:System.Windows.Forms.Keys>   
 <xref:System.Windows.Forms.Control.WndProc%2A>   
 <xref:System.Windows.Forms.Control.PreProcessMessage%2A>   
 [My.Computer.Keyboard 对象](../../../ocs/visual-basic/language-reference/objects/my-computer-keyboard-object.md)   
 [访问键盘](../Topic/Accessing%20the%20Keyboard%20\(Visual%20Basic\).md)   
 [使用键盘事件](../../../docs/framework/winforms/using-keyboard-events.md)