---
title: "各种自定义控件 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "复合控件"
  - "控件 [Windows 窗体], 复合"
  - "控件 [Windows 窗体], 扩展的"
  - "控件 [Windows 窗体], 类型"
  - "控件 [Windows 窗体], 用户控件"
  - "自定义控件 [Windows 窗体]"
  - "扩展控件"
  - "用户控件 [Windows 窗体]"
ms.assetid: 3cea09e5-4344-4ccb-9858-b66ccac210ff
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# 各种自定义控件
使用 .NET Framework 可以开发和实现新的控件。  可以通过继承来扩展熟悉的用户控件和现有控件的功能。  还可以编写自定义控件，这些控件执行自己的绘制功能。  
  
 确定创建何种类型的控件可能会费一番功夫。  本主题重点介绍各种可继承控件之间的差异，并提供有关如何为项目选择某种特定控件的信息。  
  
> [!NOTE]
>  有关创作用于 Web 窗体的控件的信息，请参见 [Developing Custom ASP.NET Server Controls](../Topic/Developing%20Custom%20ASP.NET%20Server%20Controls.md)。  
  
## 基控件类  
 <xref:System.Windows.Forms.Control> 类是 Windows 窗体控件的基类。  它提供了在 Windows 窗体应用程序中进行可视显示所需的基础结构。  
  
 <xref:System.Windows.Forms.Control> 类执行下列任务，以便在 Windows 窗体应用程序中提供可视显示：  
  
-   公开窗口句柄。  
  
-   管理消息路由。  
  
-   提供鼠标和键盘事件，以及许多其他用户界面事件。  
  
-   提供高级布局功能。  
  
-   包含特定于可视显示的许多属性，如 <xref:System.Windows.Forms.Control.ForeColor%2A>、<xref:System.Windows.Forms.Control.BackColor%2A>、<xref:System.Windows.Forms.Control.Height%2A> 和 <xref:System.Windows.Forms.Control.Width%2A>。  
  
-   为 Windows 窗体控件充当 Microsoft® ActiveX® 控件提供必需的安全和线程支持。  
  
 由于基类提供了很多基础结构，使得开发自己的 Windows 窗体控件变得相对简单。  
  
## 控件的种类  
 Windows 窗体支持三种用户定义的控件：复合、扩展和自定义。  以下各节分别描述各种控件，并就如何选择项目中使用的控件种类提供建议。  
  
### 复合控件  
 复合控件是封装在公共容器内的 Windows 窗体控件的集合。  这种控件有时称为“用户控件”。  包含的控件称为“构成控件”。  
  
 复合控件包含与每个包含的 Windows 窗体控件相关联的所有固有功能，允许您有选择地公开和绑定它们的属性。  复合控件还提供了大量的默认键盘处理功能，您不需要任何额外的开发。  
  
 例如，可以生成复合控件以显示来自数据库的客户地址数据。  此控件可以包括一个用来显示数据库字段的 <xref:System.Windows.Forms.DataGridView> 控件、一个用来处理到数据源的绑定的 <xref:System.Windows.Forms.BindingSource> 和一个用来在记录之间移动的 <xref:System.Windows.Forms.BindingNavigator> 控件。  可以有选择地公开数据绑定属性，还可以将整个控件打包并在不同应用程序之间重复使用。  有关这种复合控件的示例，请参见[如何：应用 Windows 窗体控件中的特性](../../../../docs/framework/winforms/controls/how-to-apply-attributes-in-windows-forms-controls.md)。  
  
 若要创作复合控件，请从 <xref:System.Windows.Forms.UserControl> 类派生。  基类 <xref:System.Windows.Forms.UserControl> 为子控件提供了键盘路由并使子控件可以作为一个组进行工作。  有关更多信息，请参见 [开发复合 Windows 窗体控件](../../../../docs/framework/winforms/controls/developing-a-composite-windows-forms-control.md)。  
  
 **建议**  
  
 在下列情况下，从 <xref:System.Windows.Forms.UserControl> 类继承：  
  
-   要将若干个 Windows 窗体控件的功能合成一个可重新使用的单元。  
  
### 扩展控件  
 可以从任何现有的 Windows 窗体控件导出继承控件。  此方法使您得以保留 Windows 窗体控件的所有固有功能，然后通过添加自定义属性、方法或其他功能扩展此固有功能。  可以使用此选项重写基控件的绘制逻辑，然后更改该控件的外观以扩展其用户界面。  
  
 例如，可以创建一个由 <xref:System.Windows.Forms.Button> 控件派生的控件，用于跟踪用户的单击次数。  
  
 在某些控件中，也可以通过重写基类的 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法为图形用户界面添加自定义外观。  对于跟踪单击次数的扩展按钮，可以重写 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法来调用 <xref:System.Windows.Forms.Control.OnPaint%2A> 的基实现，然后在 <xref:System.Windows.Forms.Button> 控件的工作区的一角绘制单击计数。  
  
 **建议**  
  
 处于下列情况时继承 Windows 窗体控件：  
  
-   大多数所需的功能已经与现有的 Windows 窗体控件相同。  
  
-   不需要自定义图形用户界面，或者想为现有控件设计一个新的图形用户界面。  
  
### 自定义控件  
 创建控件的另一种方法是通过从 <xref:System.Windows.Forms.Control> 继承从头开始创建一个控件。  <xref:System.Windows.Forms.Control> 类提供控件所需的所有基本功能（包括鼠标和键盘处理事件），但不提供控件特定的功能或图形界面。  
  
 与通过从 <xref:System.Windows.Forms.UserControl> 或现有 Windows 窗体控件继承创建控件相比，通过从 <xref:System.Windows.Forms.Control> 类继承创建控件需要耗费更多的心思和精力。  由于大量的实现将留给您进行，因此，您的控件可以具有比复合控件或扩展控件更大的灵活性，而且您可以使控件完全满足自己的需要。  
  
 若要实现自定义控件，必须编写该控件的 <xref:System.Windows.Forms.Control.OnPaint%2A> 事件的代码，以及所需的任何功能特定的代码。  还可以重写 <xref:System.Windows.Forms.Control.WndProc%2A> 方法并直接处理窗口消息。  这是创建控件的最强大的方法，但是要有效地使用此技术，需要熟悉 Microsoft Win32® API。  
  
 时钟控件即是一个自定义控件，它复制模拟时钟的外观和行为。  自定义绘制将被调用来促使时钟指针走动，以响应内部 <xref:System.Windows.Forms.Timer> 组件的 <xref:System.Windows.Forms.Timer.Tick> 事件。  有关更多信息，请参见[如何：开发简单的 Windows 窗体控件](../../../../docs/framework/winforms/controls/how-to-develop-a-simple-windows-forms-control.md)。  
  
 **建议**  
  
 在下列情况下，从 <xref:System.Windows.Forms.Control> 类继承：  
  
-   想要提供控件的自定义图形化表示形式。  
  
-   需要实现无法从标准控件获得的自定义功能。  
  
### ActiveX 控件  
 尽管 Windows 窗体基础结构已经为承载 Windows 窗体控件进行了优化，您仍可以使用 ActiveX 控件。  Visual Studio 中对此任务提供了支持。  有关更多信息，请参见[如何：向 Windows 窗体添加 ActiveX 控件](../../../../docs/framework/winforms/controls/how-to-add-activex-controls-to-windows-forms.md)。  
  
### 无窗口控件  
 Microsoft Visual Basic® 6.0 和 ActiveX 技术支持无窗口控件。  在 Windows 窗体中不支持无窗口控件。  
  
## 自定义设计体验  
 如果您需要实现自定义设计时体验，可以创作自己的设计器。  对于复合控件，从 <xref:System.Windows.Forms.Design.ParentControlDesigner> 或 <xref:System.Windows.Forms.Design.DocumentDesigner> 类派生自定义的设计器类。  对于扩展控件和自定义控件，从 <xref:System.Windows.Forms.Design.ControlDesigner> 类派生自定义的设计器类。  
  
 使用 <xref:System.ComponentModel.DesignerAttribute> 将控件与设计器关联。  有关更多信息，请参见[Extending Design\-Time Support](../Topic/Extending%20Design-Time%20Support.md)和[How to: Create a Windows Forms Control That Takes Advantage of Design\-Time Features](../Topic/How%20to:%20Create%20a%20Windows%20Forms%20Control%20That%20Takes%20Advantage%20of%20Design-Time%20Features.md)。  
  
## 请参阅  
 [使用 .NET Framework 开发自定义 Windows 窗体控件](../../../../docs/framework/winforms/controls/developing-custom-windows-forms-controls.md)   
 [如何：开发简单的 Windows 窗体控件](../../../../docs/framework/winforms/controls/how-to-develop-a-simple-windows-forms-control.md)   
 [开发复合 Windows 窗体控件](../../../../docs/framework/winforms/controls/developing-a-composite-windows-forms-control.md)   
 [Extending Design\-Time Support](../Topic/Extending%20Design-Time%20Support.md)   
 [How to: Create a Windows Forms Control That Takes Advantage of Design\-Time Features](../Topic/How%20to:%20Create%20a%20Windows%20Forms%20Control%20That%20Takes%20Advantage%20of%20Design-Time%20Features.md)