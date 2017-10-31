---
title: "如何：确定所按下的修改键 | Microsoft Docs"
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
  - "Alt 键"
  - "Ctrl 键"
  - "事件 [Windows 窗体], 键盘"
  - "事件 [Windows 窗体], 鼠标"
  - "键盘输入"
  - "键盘, 键盘输入"
  - "键, Alt 键"
  - "键, Ctrl 键"
  - "键, 确定上次按下的键"
  - "键, 修改键"
  - "键, Shift 键"
  - "Keys.Alt 枚举成员"
  - "Keys.ControlKey 枚举成员"
  - "Keys.Shift 枚举成员"
  - "修改键"
  - "Shift 键"
  - "用户输入, 检查键盘"
ms.assetid: 1e184048-0ae3-4067-a200-d4ba31dbc2cb
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：确定所按下的修改键
在创建接受用户击键的应用程序时，您可能还希望监视修改键，如 Shift、Alt 和 Ctrl 键。  并希望在同时按下修改键和其他键，或者单击鼠标的同时按下修改键时，您的应用程序可以做出适当的响应。  例如，如果按下了字母 S，此操作可能只会在屏幕上显示“s”，但如果您同时按下了 Ctrl\+S 键，则可能会保存当前文档。  如果处理 <xref:System.Windows.Forms.Control.KeyDown> 事件，则事件处理程序所接收的 <xref:System.Windows.Forms.KeyEventArgs> 的 <xref:System.Windows.Forms.KeyEventArgs.Modifiers%2A> 属性指定按下的修改键。  或者 <xref:System.Windows.Forms.KeyEventArgs> 的 <xref:System.Windows.Forms.KeyEventArgs.KeyData%2A> 属性指定按下的字符以及任何通过位 OR 组合的修改键。  但是，如果处理 <xref:System.Windows.Forms.Control.KeyPress> 事件或鼠标事件，则事件处理程序不接收此信息。  在这种情况下，您必须使用 <xref:System.Windows.Forms.Control> 类的 <xref:System.Windows.Forms.Control.ModifierKeys%2A> 属性。  无论哪种情况，您都必须对相应的 <xref:System.Windows.Forms.Keys> 值和正在测试的值执行按位 AND 运算。  <xref:System.Windows.Forms.Keys> 枚举提供每个修改键所对应的不同变体，因此使用正确的修改键值执行按位 AND 运算十分重要。  例如，<xref:System.Windows.Forms.Keys>、<xref:System.Windows.Forms.Keys>、<xref:System.Windows.Forms.Keys> 和 <xref:System.Windows.Forms.Keys> 都表示 Shift 键，而测试修改键 Shift 的正确值是 <xref:System.Windows.Forms.Keys>。  同样，若要测试修改键 Ctrl 和 Alt，应分别使用 <xref:System.Windows.Forms.Keys> 和 <xref:System.Windows.Forms.Keys> 值。  
  
> [!NOTE]
>  Visual Basic 程序员还可以通过 <xref:Microsoft.VisualBasic.Devices.Computer.Keyboard%2A> 属性访问键信息  
  
### 确定所按下的修改键  
  
-   将位 `AND` 运算符与 <xref:System.Windows.Forms.Control.ModifierKeys%2A> 属性和 <xref:System.Windows.Forms.Keys> 枚举的值一起使用，以确定是否按下了某个特定修改键。  下面的代码示例显示在 <xref:System.Windows.Forms.Control.KeyPress> 事件处理程序中如何确定是否按下了 Shift 键。  
  
     [!code-cpp[System.Windows.Forms.DetermineModifierKey#5](../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.DetermineModifierKey/cpp/form1.cpp#5)]
     [!code-csharp[System.Windows.Forms.DetermineModifierKey#5](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DetermineModifierKey/CS/form1.cs#5)]
     [!code-vb[System.Windows.Forms.DetermineModifierKey#5](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DetermineModifierKey/VB/form1.vb#5)]  
  
## 请参阅  
 <xref:System.Windows.Forms.Keys>   
 <xref:System.Windows.Forms.Control.ModifierKeys%2A>   
 [Windows 窗体应用程序中的键盘输入](../../../docs/framework/winforms/keyboard-input-in-a-windows-forms-application.md)   
 [How to: Determine If CapsLock is On in Visual Basic](http://msdn.microsoft.com/zh-cn/91e60f5c-dd61-4222-ba5f-39af803afd8c)