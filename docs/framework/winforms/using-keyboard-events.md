---
title: "使用键盘事件 | Microsoft Docs"
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
  - "事件 [Windows 窗体], 键盘"
  - "键盘事件"
  - "键盘, 键盘事件"
  - "KeyDown 事件"
  - "KeyPress 事件"
  - "KeyUp 事件"
ms.assetid: d3f3e14b-a459-4ee6-9875-8957e34f8ee9
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 使用键盘事件
大多数 Windows 窗体程序通过处理键盘事件处理键盘输入。  本主题提供对键盘事件的概述，包括有关何时使用每个事件和向每个事件提供的数据的详细信息。  另请参阅[事件处理程序概述（Windows 窗体）](http://msdn.microsoft.com/library/be6fx1bb\(v=vs.110\))、[事件概述（Windows 窗体）](http://msdn.microsoft.com/library/1h12f09z\(v=vs.110\))。  
  
## 键盘事件  
 Windows 窗体提供了两个在用户按下键盘键时发生的事件和一个在用户释放键盘键时发生的事件：  
  
-   <xref:System.Windows.Forms.Control.KeyDown> 事件发生一次  
  
-   用户按住相同的键时，<xref:System.Windows.Forms.Control.KeyPress> 事件可发生多次。  
  
-   用户释放某个键时，<xref:System.Windows.Forms.Control.KeyUp> 事件发生一次。  
  
 用户按某个键时，Windows 窗体会根据键盘消息指定的是字符键还是物理键来确定引发哪个事件。  有关字符键和物理键的详细信息，请参阅[键盘输入工作原理](../../../docs/framework/winforms/how-keyboard-input-works.md)。  
  
 下表介绍了这三种键盘事件：  
  
|键盘事件|描述|结果|  
|----------|--------|--------|  
|<xref:System.Windows.Forms.Control.KeyDown>|用户按下物理键时，引发此事件。|<xref:System.Windows.Forms.Control.KeyDown> 的处理程序接收：<br /><br /> <ul><li>一个 <xref:System.Windows.Forms.KeyEventArgs> 参数，它提供 <xref:System.Windows.Forms.KeyEventArgs.KeyCode%2A> 属性（该属性指定一个物理键盘按钮）。</li><li><xref:System.Windows.Forms.KeyEventArgs.Modifiers%2A> 属性（SHIFT、CTRL 或 ALT）。</li><li><xref:System.Windows.Forms.KeyEventArgs.KeyData%2A> 属性（它结合了键代码和修饰符）。  <xref:System.Windows.Forms.KeyEventArgs> 参数还提供：<br /><br /> <ul><li><xref:System.Windows.Forms.KeyEventArgs.Handled%2A> 属性，可以设置该属性以防止基础控件接收键。</li><li><xref:System.Windows.Forms.KeyEventArgs.SuppressKeyPress%2A> 属性，可用于取消该击键的 <xref:System.Windows.Forms.Control.KeyPress> 和 <xref:System.Windows.Forms.Control.KeyUp> 事件。</li></ul></li></ul>|  
|<xref:System.Windows.Forms.Control.KeyPress>|当所按的某个键或多个键生成一个字符时，则引发此事件。  例如，用户按 SHIFT 和小写的“a”键将会生成大写字母“A”字符。|<xref:System.Windows.Forms.Control.KeyPress> 在 <xref:System.Windows.Forms.Control.KeyDown> 后引发。<br /><br /> <ul><li><xref:System.Windows.Forms.Control.KeyPress> 的处理程序接收：</li><li>一个 <xref:System.Windows.Forms.KeyPressEventArgs> 参数，它包含所按的键的字符代码。  此字符代码对每个字符键和修改键组合都是唯一的。<br /><br />     例如，“A”键将生成：<br /><br /> <ul><li>字符代码 65（如果与 SHIFT 键一起按下）</li><li>或 CAPS LOCK 键 97（如果单独按下），</li><li>以及 1（如果与 CTRL 键一起按下）。</li></ul></li></ul>|  
|<xref:System.Windows.Forms.Control.KeyUp>|用户释放物理键时，将引发此事件。|<xref:System.Windows.Forms.Control.KeyUp> 的处理程序接收：<br /><br /> <ul><li>一个 <xref:System.Windows.Forms.KeyEventArgs> 参数：<br /><br /> <ul><li>它提供 <xref:System.Windows.Forms.KeyEventArgs.KeyCode%2A> 属性（该属性指定一个物理键盘按钮）。</li><li><xref:System.Windows.Forms.KeyEventArgs.Modifiers%2A> 属性（SHIFT、CTRL 或 ALT）。</li><li><xref:System.Globalization.SortKey.KeyData%2A> 属性（它结合了键代码和修饰符）。</li></ul></li></ul>|  
  
## 请参阅  
 [Windows 窗体应用程序中的键盘输入](../../../docs/framework/winforms/keyboard-input-in-a-windows-forms-application.md)   
 [键盘输入工作原理](../../../docs/framework/winforms/how-keyboard-input-works.md)   
 [Windows 窗体应用程序中的鼠标输入](../../../docs/framework/winforms/mouse-input-in-a-windows-forms-application.md)