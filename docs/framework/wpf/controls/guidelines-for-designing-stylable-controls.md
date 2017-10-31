---
title: "可样式化控件的设计准则 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "控件, 样式设计"
  - "控件的样式设计"
ms.assetid: c52dde45-a311-4531-af4c-853371c4d5f4
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 可样式化控件的设计准则
本文档概述在设计可方便地样式化和模板化的控件时需要考虑的一组最佳做法。  在为内置的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件集处理主题控件样式时，我们通过大量试验和错误总结出了这组最佳做法。  我们已经认识到，成功的样式化不只是设计完善的对象模型的功能，也是样式本身的功能。  本文档面向控件作者，而不是样式作者。  
  
   
  
<a name="Terminology"></a>   
## 术语  
 “样式化和模板化”是一组技术，控件作者可以通过该组技术来将控件的可视化特性延迟到控件的样式和模板。  这组技术包括：  
  
-   样式（包括属性 setter、触发器和演示图板）。  
  
-   资源。  
  
-   控件模板。  
  
-   数据模板。  
  
 有关样式化和模板化的介绍，请参见[样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)。  
  
<a name="Before_You_Start__Understanding_Your_Control"></a>   
## 准备工作：了解您的控件  
 在开始阅读本文档中的准则之前，一定要了解并定义了控件的一般用法，这一点很重要。  样式化公开一组通常不受约束的可能性。  旨在由许多开发人员在许多应用程序中广泛使用的控件面临着如下挑战：可以使用样式化来对控件的可视化外观进行广泛的更改。  实际上，带有样式的控件甚至可能并非控件作者的本意。  由于样式化在本质上可以提供无限的灵活性，因此您可以使用“一般用法”这一概念来帮助您限制自己的决定。  
  
 为了了解控件的一般用法，最好考虑控件的价值主张。  您的控件能够提供哪些无法由其他控件提供的内容？  一般用法并不表示任何特定的可视化外观，而是表示控件的基本原理和一组有关其用法的合理预期。  了解到这一点，就可以对控件在一般情况下的撰写模型和样式定义行为进行一些假设。  例如，对于 <xref:System.Windows.Controls.ComboBox>，如果您了解其一般用法，并不意味着您非常清楚特定的 <xref:System.Windows.Controls.ComboBox> 是否有圆角，但是您将由此清楚 <xref:System.Windows.Controls.ComboBox> 可能需要一个弹出窗口和某种用来切换其开关状态的方法。  
  
<a name="General_Guidelines"></a>   
## 通用准则  
  
-   **不严格实施模板约定。**控件的模板约定可以包含元素、命令、绑定和触发器，甚至还可以包含必需的或为了使控件正常工作而应当使用的属性设置。  
  
    -   尽可能减少约定。  
  
    -   围绕如下预期来设计：在设计时（即，在使用设计工具时），控件模板通常处于不完整状态。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 不提供“正在撰写”状态的基础结构，因此，控件必须围绕这样的状态可能有效这一预期来生成。  
  
    -   在没有遵循模板约定的任何方面时，不引发异常。  按照这一原则，当面板的子级太多或太少时，面板不应当引发异常。  
  
-   **将外围功能分解成模板帮助器元素。**每个控件都应当将重点放在其核心功能和真正的价值主张上，而且每个控件都应当由控件的一般用法来定义。  为此，请使用模板中的撰写和帮助器元素来实现外围行为和可视化，即，那些不构成控件核心功能的行为和可视化。  帮助器元素可分为三类：  
  
    -   **独立**帮助器类型是以“匿名方式”用在模板中的可重用的公共控件或基元，这意味着帮助器元素和带有样式的控件无法互相识别。  在技术上，任何元素都可以是匿名类型，但是在这里，术语“独立”用于描述那些封装专用功能以实现目标方案的类型。  
  
    -   **基于类型的**帮助器元素是封装专用功能的新类型。  通常，这些元素在设计上比公用控件或基元的功能范围要窄。  与独立帮助器元素不同的是，基于类型的帮助器元素能够识别它们的使用上下文，而且通常必须与包含它们所属模板的控件共享数据。  
  
    -   **命名的**帮助器元素是控件应当能够在其模板中根据名称找到的公用控件或基元。这些元素在模板中具有一个已知的名称，这使得控件能够找到这些元素并以编程方式与之交互。  在任何模板中，都只能有一个具有给定名称的元素。  
  
     下表显示的是由目前的控件样式使用的部分帮助器元素列表：  
  
    |元素|类型|使用者|  
    |--------|--------|---------|  
    |<xref:System.Windows.Controls.ContentPresenter>|基于类型的|<xref:System.Windows.Controls.Button>、<xref:System.Windows.Controls.CheckBox>、<xref:System.Windows.Controls.RadioButton>、<xref:System.Windows.Controls.Frame> 等（所有的 <xref:System.Windows.Controls.ContentControl> 类型）|  
    |<xref:System.Windows.Controls.ItemsPresenter>|基于类型的|<xref:System.Windows.Controls.ListBox>、<xref:System.Windows.Controls.ComboBox>、<xref:System.Windows.Controls.Menu> 等（所有的 <xref:System.Windows.Controls.ItemsControl> 类型）|  
    |<xref:System.Windows.Controls.Primitives.ToolBarOverflowPanel>|命名的|<xref:System.Windows.Controls.ToolBar>|  
    |<xref:System.Windows.Controls.Primitives.Popup>|独立|<xref:System.Windows.Controls.ComboBox>、<xref:System.Windows.Controls.ToolBar>、<xref:System.Windows.Controls.Menu>、<xref:System.Windows.Controls.ToolTip> 等|  
    |<xref:System.Windows.Controls.Primitives.RepeatButton>|命名的|<xref:System.Windows.Controls.Slider>、<xref:System.Windows.Controls.Primitives.ScrollBar> 等|  
    |<xref:System.Windows.Controls.Primitives.ScrollBar>|命名的|<xref:System.Windows.Controls.ScrollViewer>|  
    |<xref:System.Windows.Controls.ScrollViewer>|独立|<xref:System.Windows.Controls.ListBox>、<xref:System.Windows.Controls.ComboBox>、<xref:System.Windows.Controls.Menu>、<xref:System.Windows.Controls.Frame> 等|  
    |<xref:System.Windows.Controls.Primitives.TabPanel>|独立|<xref:System.Windows.Controls.TabControl>|  
    |<xref:System.Windows.Controls.TextBox>|命名的|<xref:System.Windows.Controls.ComboBox>|  
    |<xref:System.Windows.Controls.Primitives.TickBar>|基于类型的|<xref:System.Windows.Controls.Slider>|  
  
-   **尽可能减少帮助器元素所必需的、特定于用户的绑定或属性设置**。  通常，帮助器元素需要某些绑定或属性设置才能在控件模板中正确工作。  帮助器元素和模板化控件应当尽可能多地生成这些设置。  在设置属性或者建立绑定时，注意不要重写由用户设置的值。  具体的最佳做法如下所示：  
  
    -   命名的帮助器元素应当由父级标识，而且父级应当针对帮助器元素建立任何必需的设置。  
  
    -   对于基于类型的帮助器元素，应当直接针对它们建立任何必需的设置。  这样做可能需要帮助器元素查找它在使用时的信息上下文，包括其 `TemplatedParent`（它在使用时的模板的控件类型）。  例如，在用于 <xref:System.Windows.Controls.ContentControl> 派生类型时，<xref:System.Windows.Controls.ContentPresenter> 会自动将它的 `TemplatedParent` 的 `Content` 属性绑定到它的 <xref:System.Windows.Controls.ContentPresenter.Content%2A> 属性。  
  
    -   独立帮助器元素不能按这种方式进行优化，这是因为按照定义，帮助器元素和父级不能相互识别。  
  
-   **使用 Name 属性来标记模板中的元素**。  如果控件需要在样式中查找某个元素才能以编程方式访问它，则该控件应当使用 `Name` 属性和 `FindName` 范例来进行查找。  控件不应在未找到所需元素时引发异常，而是应在不提示的情况下禁用需要该元素的功能。  
  
-   **使用最佳做法来表示样式中的控件状态和行为。**下面按顺序列出了用来表示样式中的控件状态更改和行为的最佳做法。  您应当使用列表上的第一项来实现您的方案。  
  
    1.  属性绑定。  示例：在 <xref:System.Windows.Controls.ComboBox.IsDropDownOpen%2A?displayProperty=fullName> 和 <xref:System.Windows.Controls.Primitives.ToggleButton.IsChecked%2A?displayProperty=fullName> 之间绑定。  
  
    2.  触发的属性更改或属性动画。  示例：<xref:System.Windows.Controls.Button> 的悬停状态。  
  
    3.  命令。  示例：<xref:System.Windows.Controls.Primitives.ScrollBar> 中的 <xref:System.Windows.Controls.Primitives.ScrollBar.LineUpCommand> \/ <xref:System.Windows.Controls.Primitives.ScrollBar.LineDownCommand>。  
  
    4.  独立帮助器元素。  示例：<xref:System.Windows.Controls.TabControl> 中的 <xref:System.Windows.Controls.Primitives.TabPanel>。  
  
    5.  基于类型的帮助器类型。  示例：<xref:System.Windows.Controls.Button> 中的 <xref:System.Windows.Controls.ContentPresenter> 和 <xref:System.Windows.Controls.Slider> 中的 <xref:System.Windows.Controls.Primitives.TickBar>。  
  
    6.  命名的帮助器元素。  示例：<xref:System.Windows.Controls.ComboBox> 中的 <xref:System.Windows.Controls.TextBox>。  
  
    7.  命名帮助器类型中的冒泡事件。  如果您侦听样式元素中的冒泡事件，则应当要求生成该事件的元素能够进行唯一标识。  示例：<xref:System.Windows.Controls.ToolBar> 中的 <xref:System.Windows.Controls.Primitives.Thumb>。  
  
    8.  自定义 `OnRender` 行为。  示例：<xref:System.Windows.Controls.Button> 中的 <xref:Microsoft.Windows.Themes.ButtonChrome>。  
  
-   **慎用样式触发器（与模板触发器相对）**。  会影响到模板中元素属性的触发器必须在模板中进行声明。  会影响到控件属性（没有 `TargetName`）的触发器可以在样式中声明，除非您知道更改模板还可能会损坏触发器。  
  
-   **与现有的样式模式一致。**一个问题常常有多种解决办法。  注意尽可能与现有的控件样式模式保持一致。  这对于派生自同一基类型（例如，<xref:System.Windows.Controls.ContentControl>、<xref:System.Windows.Controls.ItemsControl>、<xref:System.Windows.Controls.Primitives.RangeBase> 等）的控件尤其重要。  
  
-   **在不重新模板化的情况下公开属性来启用常见自定义项方案**。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 不支持可插入\/可自定义的部件，因此控件用户只能使用两种自定义方法：直接设置属性或者使用样式设置属性。  请记住，比较合适的做法是，设置数量有限的属性，使其面向极其常见的高优先级自定义项方案，否则的话，这些方案需要重新模板化。  下面是有关何时以及如何启用自定义项方案的最佳方法：  
  
    -   极其常见的自定义项应当作为属性在控件上公开并由模板使用。  
  
    -   不太常见（尽管并非极少见）的自定义项应当作为附加属性公开并由模板使用。  
  
    -   需要对已知但是极少见的自定义项重新模板化，这一点也是可以接受的。  
  
<a name="Theme_Considerations"></a>   
## 主题注意事项  
  
-   **主题样式应当尝试在所有的主题之间具有一致的属性语义，但不保证能够实现这一点**。  作为控件文档的一部分，控件应当具有一个描述其属性语义（即控件属性的“含义”）的文档。  例如，<xref:System.Windows.Controls.ComboBox> 控件应当定义 <xref:System.Windows.Controls.Control.Background%2A> 属性在 <xref:System.Windows.Controls.ComboBox> 中的含义。  控件的默认样式应当尝试遵循在其文档中的所有主题中定义的语义。  另一方面，控件用户应当注意属性语义可能因主题而异。  在某些情况下，给定的属性在由特定主题所需的可视化约束下可能无法表示  （例如，对于许多控件来说，传统主题没有可以向其应用 `Thickness` 的边框）。  
  
-   **主题样式不需要在所有的主题之间具有一致的触发器语义**。  由控件样式通过触发器或动画公开的行为可能因主题而异。  控件用户应当注意到，控件将不必使用同一个机制在所有的主题中实现一个特定的行为。  例如，一个主题可以使用动画来表示悬停行为，而另一个主题则可以使用触发器。  这可能会导致自定义控件上的行为保留出现不一致现象  （例如，如果控件的悬停状态是使用触发器来表示的，那么，更改背景属性可能不会影响该状态）。  但是，如果悬停状态是使用动画来实现的，那么，更改背景属性可能会不可挽回地中断动画，从而中断状态过渡）。  
  
-   **主题样式不需要在所有的主题之间具有一致的“布局”语义**。  例如，默认的样式不需要保证控件将在所有的主题中占用同样的大小，也不需要保证控件将在所有的主题中具有同样的内容边距\/空白。  
  
## 请参阅  
 [样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [控件创作概述](../../../../docs/framework/wpf/controls/control-authoring-overview.md)