---
title: "AutoSize 属性概述 | Microsoft Docs"
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
  - "自动调整大小"
  - "AutoSize 属性"
  - "AutoSizeMode 属性"
  - "布局 [Windows 窗体], AutoSize"
  - "调整大小, 自动"
ms.assetid: 62fd82a2-9565-4f65-925b-9d1e66dc4e7d
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# AutoSize 属性概述
<xref:System.Windows.Forms.Control.AutoSize%2A> 属性使控件能够更改其大小（如有必要），以达到由 <xref:System.Windows.Forms.Control.PreferredSize%2A> 属性指定的值。  通过设置 `AutoSizeMode` 属性，可以调整特定控件的大小调整行为。  
  
## AutoSize 行为  
 只有一些控件支持 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性。  此外，一些支持 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性的控件也支持 `AutoSizeMode` 属性。  
  
 根据特定控件类型以及 `AutoSizeMode` 属性的值（如果该属性存在），<xref:System.Windows.Forms.Control.AutoSize%2A> 属性可产生某些不同的行为。  下表描述了始终正确的行为，并提供每种行为的简要说明：  
  
|始终正确的行为|说明|  
|-------------|--------|  
|自动大小调整是运行时功能。|这意味着不会在增大或缩小控件后不产生进一步的影响。|  
|控件更改大小时其 <xref:System.Windows.Forms.Control.Location%2A> 属性的值始终保持不变。|当控件的内容导致控件增大时，控件向右向下增大。  控件不会向左增大。|  
|<xref:System.Windows.Forms.Control.AutoSize%2A> 为 `true` 时，<xref:System.Windows.Forms.Control.Dock%2A> 和 <xref:System.Windows.Forms.Control.Anchor%2A> 属性将起作用。|控件的 <xref:System.Windows.Forms.Control.Location%2A> 属性的值会调整为正确值。<br /><br /> **注意** <xref:System.Windows.Forms.Label> 控件是此规则的例外。  将停靠的 <xref:System.Windows.Forms.Label> 控件的 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性值设置为 `true` 时，<xref:System.Windows.Forms.Label> 控件不会拉伸。|  
|无论控件的 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性的值是什么，控件的 <xref:System.Windows.Forms.Control.MaximumSize%2A> 和 <xref:System.Windows.Forms.Control.MinimumSize%2A> 属性都始终会起作用。|<xref:System.Windows.Forms.Control.MaximumSize%2A> 和 <xref:System.Windows.Forms.Control.MinimumSize%2A> 属性不受 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性影响。|  
|默认情况下不设置最小大小。|这意味着，如果将某个控件设置为依据 <xref:System.Windows.Forms.Control.AutoSize%2A> 缩小，且该控件中没有内容，则该控件的 <xref:System.Windows.Forms.Control.Size%2A> 属性的值为 0,0。  这种情况下，该控件将缩小为一个点，并不容易看到。|  
|如果控件没有实现 <xref:System.Windows.Forms.Control.GetPreferredSize%2A> 方法，则 <xref:System.Windows.Forms.Control.GetPreferredSize%2A> 方法返回分配给 <xref:System.Windows.Forms.Control.Size%2A> 属性的上一个值。|这意味着将 <xref:System.Windows.Forms.Control.AutoSize%2A> 设置为 `true` 不会产生任何效果。|  
|<xref:System.Windows.Forms.TableLayoutPanel> 单元格中的控件始终会缩小以适合单元格，直至达到控件的 <xref:System.Windows.Forms.Control.MinimumSize%2A>。|此大小将强制为最大大小。  单元格是 <xref:System.Windows.Forms.SizeType> 行或列的部分时并非如此。|  
  
## AutoSizeMode 属性  
 `AutoSizeMode` 属性提供了对默认 <xref:System.Windows.Forms.Control.AutoSize%2A> 行为的更多细节上的控制。  `AutoSizeMode` 属性指定控件如何根据其内容调整自身大小。  例如，内容可以是 <xref:System.Windows.Forms.Button> 控件的文本或容器的子控件。  
  
 下表显示了 <xref:System.Windows.Forms.AutoSizeMode> 设置以及每种设置引起的行为的说明。  
  
|AutoSizeMode 设置|行为|  
|---------------------|--------|  
|GrowAndShrink|控件增大或缩小以包含其内容。<br /><br /> <xref:System.Windows.Forms.Control.MinimumSize%2A> 和 <xref:System.Windows.Forms.Control.MaximumSize%2A> 的值将起作用，但将忽略 <xref:System.Windows.Forms.Control.Size%2A> 属性的当前值。<br /><br /> 具有 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性但没有 `AutoSizeMode` 属性的控件的行为与此相同。|  
|GrowOnly|控件会增大到足以包含其内容，但不会缩小到小于由其 <xref:System.Windows.Forms.Control.Size%2A> 属性指定的值。<br /><br /> 这是 `AutoSizeMode` 的默认值。|  
  
## 支持 AutoSize 属性的控件  
 下表列出了支持 <xref:System.Windows.Forms.Control.AutoSize%2A> 和 `AutoSizeMode` 属性的控件。  
  
|AutoSize 支持|控件类型|  
|-----------------|----------|  
|-   支持 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性。<br />-   没有 `AutoSizeMode` 属性。|<xref:System.Windows.Forms.CheckBox><br /><br /> <xref:System.Windows.Forms.DomainUpDown><br /><br /> <xref:System.Windows.Forms.Label><br /><br /> <xref:System.Windows.Forms.LinkLabel><br /><br /> <xref:System.Windows.Forms.MaskedTextBox>（<xref:System.Windows.Forms.TextBox> 基控件）<br /><br /> <xref:System.Windows.Forms.NumericUpDown><br /><br /> <xref:System.Windows.Forms.RadioButton><br /><br /> <xref:System.Windows.Forms.TextBox><br /><br /> <xref:System.Windows.Forms.TrackBar>|  
|-   支持 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性。<br />-   支持 `AutoSizeMode` 属性。|<xref:System.Windows.Forms.Button><br /><br /> <xref:System.Windows.Forms.CheckedListBox><br /><br /> <xref:System.Windows.Forms.FlowLayoutPanel><br /><br /> <xref:System.Windows.Forms.Form><br /><br /> <xref:System.Windows.Forms.GroupBox><br /><br /> <xref:System.Windows.Forms.Panel><br /><br /> <xref:System.Windows.Forms.TableLayoutPanel>|  
|-   没有 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性。|<xref:System.Windows.Forms.CheckedListBox><br /><br /> <xref:System.Windows.Forms.ComboBox><br /><br /> <xref:System.Windows.Forms.DataGridView><br /><br /> <xref:System.Windows.Forms.DateTimePicker><br /><br /> <xref:System.Windows.Forms.ListBox><br /><br /> <xref:System.Windows.Forms.ListView><br /><br /> <xref:System.Windows.Forms.MaskedTextBox><br /><br /> <xref:System.Windows.Forms.MonthCalendar><br /><br /> <xref:System.Windows.Forms.ProgressBar><br /><br /> <xref:System.Windows.Forms.PropertyGrid><br /><br /> <xref:System.Windows.Forms.RichTextBox><br /><br /> <xref:System.Windows.Forms.SplitContainer><br /><br /> <xref:System.Windows.Forms.TabControl><br /><br /> <xref:System.Windows.Forms.TabPage><br /><br /> <xref:System.Windows.Forms.TreeView><br /><br /> <xref:System.Windows.Forms.WebBrowser><br /><br /> <xref:System.Windows.Forms.ScrollBar>|  
  
## 设计环境中的 AutoSize  
 下表描述了控件在设计时基于其 <xref:System.Windows.Forms.Control.AutoSize%2A> 和 `AutoSizeMode` 属性的值的大小调整行为。  
  
 重写 <xref:System.Windows.Forms.Design.ControlDesigner.SelectionRules%2A> 属性可确定给定控件是否处于用户可调整大小的状态。  下表中，“不能”表示只有 <xref:System.Windows.Forms.Design.SelectionRules>，“能”表示 <xref:System.Windows.Forms.Design.SelectionRules> 和 <xref:System.Windows.Forms.Design.SelectionRules>。  
  
|AutoSize 设置|设计时调整大小操作|  
|-----------------|---------------|  
|-   <xref:System.Windows.Forms.Control.AutoSize%2A> \= `true`<br />-   没有 `AutoSizeMode` 属性。|除以下控件外，用户不能在设计时调整控件的大小：<br /><br /> -   <xref:System.Windows.Forms.TextBox><br />-   <xref:System.Windows.Forms.MaskedTextBox><br />-   <xref:System.Windows.Forms.RichTextBox><br />-   <xref:System.Windows.Forms.TrackBar>|  
|-   <xref:System.Windows.Forms.Control.AutoSize%2A> \= `true`<br />-   `AutoSizeMode` \= <xref:System.Windows.Forms.AutoSizeMode>|用户不能在设计时调整控件的大小。|  
|-   <xref:System.Windows.Forms.Control.AutoSize%2A> \= `true`<br />-   `AutoSizeMode` \= <xref:System.Windows.Forms.AutoSizeMode>|用户可以在设计时调整控件的大小。  当设置了 <xref:System.Windows.Forms.Control.Size%2A> 属性时，用户只能增加控件的大小。|  
|-   <xref:System.Windows.Forms.Control.AutoSize%2A> \= `false`，或者 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性被隐藏。|用户可以在设计时调整控件的大小。|  
  
> [!NOTE]
>  为使工作效率最大化，Windows 窗体设计器隐藏了 <xref:System.Windows.Forms.Form> 类的 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性。  设计时，无论窗体的实际设置如何，该窗体的行为都如同将 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性设置为 `false`。  运行时，不做任何特殊处理，并按属性设置的指定应用 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性。  
  
## 请参阅  
 <xref:System.Windows.Forms.Control.AutoSize%2A>   
 <xref:System.Windows.Forms.Control.PreferredSize%2A>   
 <xref:System.Windows.Forms.Control.GetPreferredSize%2A>