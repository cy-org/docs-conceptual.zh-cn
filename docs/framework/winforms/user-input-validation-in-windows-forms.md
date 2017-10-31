---
title: "Windows 窗体中的用户输入验证 | Microsoft Docs"
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
  - "用户输入, 在 Windows 窗体中验证"
  - "验证用户输入, Windows 窗体"
  - "验证, Windows 窗体用户输入"
  - "Windows 窗体, 验证用户输入"
ms.assetid: 4ec07681-1dee-4bf9-be5e-718f635a33a1
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# Windows 窗体中的用户输入验证
用户在应用程序中输入数据时，可能需要在应用程序使用该数据之前，验证该数据是否有效。  可能需要让某些文本字段的长度不为零，或者让字段的格式设置为符合电话号码或其他类型的格式良好的数据，或者让字符串不包含任何可用来降低数据库安全性的不安全字符。  Windows 窗体提供了几种验证应用程序中的输入的方法。  
  
## 使用 MaskedTextBox 控件的验证  
 如果需要要求用户按正确定义的格式（例如，电话号码或部件号码）输入数据，则使用 <xref:System.Windows.Forms.MaskedTextBox> 控件可以用少量代码快速实现此目的。  掩码是由掩码语言中的字符组成的字符串，用于指定在文本框中的任何给定位置可以输入哪些字符。  该控件将向用户显示一组提示。  如果用户键入不正确的项（例如，在需要数字时用户键入字母），则该控件将自动拒绝输入。  
  
 <xref:System.Windows.Forms.MaskedTextBox> 使用的掩码语言非常灵活。  您可以通过掩码语言指定必选字符、可选字符、文字字符（如连字符和圆括号）、货币字符和日期分隔符。  该控件在绑定到数据源时也可以正常工作。  可使用数据绑定上的 <xref:System.Windows.Forms.Binding.Format> 事件重新设置传入数据的格式以符合掩码要求，并且可使用 <xref:System.Windows.Forms.Binding.Parse> 事件重新设置传出数据的格式以符合数据字段的规范。  
  
 有关更多信息，请参见 [MaskedTextBox 控件](../../../docs/framework/winforms/controls/maskedtextbox-control-windows-forms.md)。  
  
## 事件驱动的验证  
 如果想完全通过编程来控制验证，或者需要执行复杂的验证检查，应当使用大多数 Windows 窗体控件中内置的验证事件。  每个接受任意形式的用户输入的控件都有 <xref:System.Windows.Forms.Control.Validating> 事件，一旦控件需要数据验证，该事件就会发生。  在 <xref:System.Windows.Forms.Control.Validating> 事件处理方法中，可以采用多种方式验证用户输入。  例如，如果有一个必须包含邮政编码的文本框，则可以用以下方法执行验证：  
  
-   如果邮政编码必须属于某个特定的邮政编码组，则可以对输入执行字符串比较以验证用户输入的数据。  例如，如果邮政编码必须处于 {10001, 10002, 10003} 集中，则可以使用字符串比较来验证数据。  
  
-   如果邮政编码必须采用特定的格式，则可以使用正则表达式来验证用户输入的数据。  例如，若要验证 `#####` 或 `#####-####` 格式，则可以使用正则表达式 `^(\d{5})(-\d{4})?$`。  若要验证 `A#A #A#` 格式，则可以使用正则表达式 `[A-Z]\d[A-Z] \d[A-Z]\d`。  有关正则表达式的更多信息，请参见 [.NET Framework 正则表达式](../../../docs/standard/base-types/regular-expressions.md)和[正则表达式示例](../../../docs/standard/base-types/regular-expression-examples.md)。  
  
-   如果邮政编码必须是有效的美国邮政编码，则可以调用一个邮政编码 Web 服务来验证用户输入的数据。  
  
 系统为 <xref:System.Windows.Forms.Control.Validating> 事件提供了类型为 <xref:System.ComponentModel.CancelEventArgs> 的对象。  如果确定控件的数据无效，则可以通过将此对象的 <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> 属性设置为 `true` 来取消 <xref:System.Windows.Forms.Control.Validating> 事件。  如果未设置 <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> 属性，则 Windows 窗体将假定该控件的验证已成功，并引发 <xref:System.Windows.Forms.Control.Validated> 事件。  
  
 有关验证 <xref:System.Windows.Controls.TextBox> 中的电子邮件地址的代码示例，请参见 <xref:System.Windows.Forms.Control.Validating>。  
  
### 数据绑定和事件驱动的验证  
 在已将控件绑定到数据源（例如，数据库表）时，验证非常有用。  通过使用验证，可以确保控件的数据满足数据源要求的格式，并且其中不包含任何特殊字符（例如，可能不安全的引号和反斜杠）。  
  
 使用数据绑定时，控件中的数据将在执行 <xref:System.Windows.Forms.Control.Validating> 事件期间与数据源同步。  如果取消 <xref:System.Windows.Forms.Control.Validating> 事件，数据将不与数据源同步。  
  
> [!IMPORTANT]
>  如果您的自定义验证在 <xref:System.Windows.Forms.Control.Validating> 事件之后发生，则该验证将不会影响数据绑定。  例如，如果 <xref:System.Windows.Forms.Control.Validated> 事件中的代码尝试取消数据绑定的代码，则仍将发生数据绑定。  在此情况下，若要在 <xref:System.Windows.Forms.Control.Validated> 事件中执行验证，请将控件的**“数据源更新模式”**属性（在**“\(数据绑定\)”**\\**“\(高级\)”**下）从**“OnValidation”**更改为**“从不”**，并且将*控件*`.DataBindings["`*\<您的字段\>*`"].WriteValue()` 添加到验证代码中。  
  
### 隐式和显式验证  
 何时验证控件的数据？  这要由您 \- 开发人员来回答。  可以根据应用程序的需要来使用隐式或显式验证。  
  
#### 隐式验证  
 隐式验证方法将在用户输入数据的过程中验证数据。  如果在键被按下时读取键，则可以在向控件中输入数据时验证数据，或者更常见的做法是，在用户将输入焦点从一个控件移向下一个控件时验证数据。  当需要为用户提供有关所使用的数据的即时反馈时，此方法很有用。  
  
 如果要使用控件的隐式验证，则必须将该控件的 <xref:System.Windows.Forms.ContainerControl.AutoValidate%2A> 属性设置为 `true`。  如果取消 <xref:System.Windows.Forms.Control.Validating> 事件，则该控件的行为将由分配给 <xref:System.Windows.Forms.ContainerControl.AutoValidate%2A> 的值来确定。  如果分配了 <xref:System.Windows.Forms.AutoValidate>，则取消事件不会导致 <xref:System.Windows.Forms.Control.Validated> 事件发生。  在用户将数据更改为有效输入之前，输入焦点将一直保留在当前控件上。  如果分配了 <xref:System.Windows.Forms.AutoValidate>，则取消事件时将不会发生 <xref:System.Windows.Forms.Control.Validated> 事件，但焦点仍将更改到下一个控件上。  
  
 如果将 <xref:System.Windows.Forms.AutoValidate> 分配给 <xref:System.Windows.Forms.ContainerControl.AutoValidate%2A> 属性，将同时防止隐式验证。  若要验证控件，则必须使用显式验证。  
  
#### 显式验证  
 显式验证方法将一次性验证数据。  可以验证数据以响应用户操作，例如单击“保存”按钮或“下一步”链接的操作。  当发生用户操作时，可以通过下列方法之一来触发显式验证：  
  
-   调用 <xref:System.Windows.Forms.ContainerControl.Validate%2A> 以验证上一个失去焦点的控件。  
  
-   调用 <xref:System.Windows.Forms.ContainerControl.ValidateChildren%2A> 以验证窗体或容器控件中的所有子控件。  
  
-   调用自定义方法以手动验证控件中的数据。  
  
#### Windows 窗体控件的默认隐式验证行为  
 不同的 Windows 窗体控件的 <xref:System.Windows.Forms.ContainerControl.AutoValidate%2A> 属性有不同的默认值。  下表显示了最常见的控件及其默认值。  
  
|控件|默认验证行为|  
|--------|------------|  
|<xref:System.Windows.Forms.ContainerControl>|<xref:System.Windows.Forms.AutoValidate>|  
|<xref:System.Windows.Forms.Form>|<xref:System.Windows.Forms.AutoValidate>|  
|<xref:System.Windows.Forms.PropertyGrid>|Visual Studio 中不公开的属性|  
|<xref:System.Windows.Forms.ToolStripContainer>|Visual Studio 中不公开的属性|  
|<xref:System.Windows.Forms.SplitContainer>|<xref:System.Windows.Forms.AutoValidate>|  
|<xref:System.Windows.Forms.UserControl>|<xref:System.Windows.Forms.AutoValidate>|  
  
## 关闭窗体和重写验证  
 当控件因包含的数据无效而保持焦点时，使用以下常规方法之一将无法关闭父窗体：  
  
-   通过单击**“关闭”**按钮。  
  
-   通过在**“系统”**菜单中选择**“关闭”**。  
  
-   以编程方式调用 <xref:System.Windows.Forms.Form.Close%2A> 方法。  
  
 但在某些情况下，无论控件中的值是否有效，您都可能要让用户关闭窗体。  通过创建窗体的 <xref:System.Windows.Forms.Form.Closing> 事件的处理程序，您可以重写验证并关闭仍包含无效数据的窗体。  在事件中，将 <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> 属性设置为 `false`。  这将强制关闭该窗体。  有关更多信息及示例，请参见<xref:System.Windows.Forms.Form.Closing?displayProperty=fullName>。  
  
> [!NOTE]
>  如果以这种方式强制关闭窗体，则窗体的控件中尚未保存的任何数据都将丢失。  此外，模式窗体在关闭时不会验证控件的内容。  仍可以使用控件验证将焦点锁定到某个控件，但不必考虑与关闭窗体关联的行为。  
  
## 请参阅  
 <xref:System.Windows.Forms.Control.Validating?displayProperty=fullName>   
 <xref:System.Windows.Forms.Form.Closing?displayProperty=fullName>   
 <xref:System.ComponentModel.CancelEventArgs?displayProperty=fullName>   
 [MaskedTextBox 控件](../../../docs/framework/winforms/controls/maskedtextbox-control-windows-forms.md)   
 [正则表达式示例](../../../docs/standard/base-types/regular-expression-examples.md)