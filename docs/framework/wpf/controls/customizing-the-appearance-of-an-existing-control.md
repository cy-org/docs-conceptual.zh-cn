---
title: "通过创建 ControlTemplate 自定义现有控件的外观 | Microsoft Docs"
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
  - "控件协定 [WPF]"
  - "控件 [WPF], 状态指定的外观"
  - "控件 [WPF], 可视结构更改"
  - "ControlTemplate [WPF], 自定义现有控件"
  - "外观控件 [WPF]"
  - "模板 [WPF], 自定义现有控件"
ms.assetid: 678dd116-43a2-4b8c-82b5-6b826f126e31
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 通过创建 ControlTemplate 自定义现有控件的外观
<a name="introduction"></a> <xref:System.Windows.Controls.ControlTemplate> 指定控件的可视结构和可视行为。  可以通过为新 <xref:System.Windows.Controls.ControlTemplate>自定义控件的外观。  当您创建 <xref:System.Windows.Controls.ControlTemplate>时，将替换现有控件的外观，而无需更改其功能。  例如，您可以将应用程序中的按钮设置而不是默认的方形，但是，按钮将引发 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件。  
  
 本主题说明 <xref:System.Windows.Controls.ControlTemplate>的各个部分，演示如何创建 <xref:System.Windows.Controls.Button>的简单 <xref:System.Windows.Controls.ControlTemplate> ，并说明如何了解控件的控件协定，使您可以自定义其外观。  由于您在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]创建 <xref:System.Windows.Controls.ControlTemplate> ，可以更改控件的外观无需编写任何代码。  您还可以使用设计器，如 Microsoft expression blend，创建自定义控件模板。  本主题介绍 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 显示自定义 <xref:System.Windows.Controls.Button> 外观的示例并列出了完整的示例在主题末尾的。  有关使用 expression blend 的更多信息，请 [样式支持模板的控件](http://go.microsoft.com/fwlink/?LinkId=161153)参见。  
  
 下图显示了使用 <xref:System.Windows.Controls.ControlTemplate> 本主题中创建的 <xref:System.Windows.Controls.Button> 。  
  
 ![一个具有自定义控件模板的按钮。](../../../../docs/framework/wpf/controls/media/ndp-buttonnormal.png "NDP\_ButtonNormal")  
使用自定义控件模板的按钮  
  
 ![一个具有红色边框的按钮。](../../../../docs/framework/wpf/controls/media/ndp-buttonmouseover.png "NDP\_ButtonMouseOver")  
使用自定义控件模板并将鼠标指针置于上的按钮  
  
   
  
<a name="prerequisites"></a>   
## 系统必备  
 本主题假设，您了解如何创建和使用控件和样式如中所述 [控件](../../../../docs/framework/wpf/controls/index.md)。  本主题中讨论的概念适用于从 <xref:System.Windows.Controls.Control> 类继承的元素，但 <xref:System.Windows.Controls.UserControl>。  不能将 <xref:System.Windows.Controls.ControlTemplate> 于 <xref:System.Windows.Controls.UserControl>。  
  
<a name="when_you_should_create_a_controltemplate"></a>   
## 何时应创建 ControlTemplate  
 控件有许多属性，如 <xref:System.Windows.Controls.Border.Background%2A>、 <xref:System.Windows.Controls.Control.Foreground%2A>和 <xref:System.Windows.Controls.Control.FontFamily%2A>，可以设置指定控件外观的不同方面，但是，您可以通过设置这些属性可进行的更改是有限的。  例如，可以设置 <xref:System.Windows.Controls.Control.Foreground%2A> 属性设置为蓝色和 <xref:System.Windows.Controls.Control.FontStyle%2A> 到 <xref:System.Windows.Controls.CheckBox>为斜体。  
  
 不能创建控件的新 <xref:System.Windows.Controls.ControlTemplate> ，所有控件在每 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]基于的应用程序将具有相同的一般外观，这限制能够创建具有自定义外观的应用程序。  默认情况下，每 <xref:System.Windows.Controls.CheckBox> 具有相似的特性。  例如， <xref:System.Windows.Controls.CheckBox> 的内容始终位于选择指示符的右侧，并且，复选标记总是用于表示 <xref:System.Windows.Controls.CheckBox> 中选择。  
  
 您创建 <xref:System.Windows.Controls.ControlTemplate> ，如果您要自定义后无法生成的外观设置控件的其他属性将执行。  在 <xref:System.Windows.Controls.CheckBox>的示例中，假设您希望复选框的内容位于选择指示符的上方，并希望 X 表示 <xref:System.Windows.Controls.CheckBox> 中选择。  指定将在 <xref:System.Windows.Controls.CheckBox>的 <xref:System.Windows.Controls.ControlTemplate> 并将这些更改。  
  
 使用默认 <xref:System.Windows.Controls.ControlTemplate>的下图显示 <xref:System.Windows.Controls.CheckBox> 。  
  
 ![一个具有默认控件模板的复选框。](../../../../docs/framework/wpf/controls/media/ndp-checkboxdefault.png "NDP\_CheckBoxDefault")  
使用默认控件模板的 checkbox  
  
 使用自定义 <xref:System.Windows.Controls.ControlTemplate> 放置 <xref:System.Windows.Controls.CheckBox> 内容位于选择指示符的上方的并显示 X 的下图显示 <xref:System.Windows.Controls.CheckBox> ，当 <xref:System.Windows.Controls.CheckBox> 时。  
  
 ![一个具有自定义控件模板的复选框。](../../../../docs/framework/wpf/controls/media/ndp-checkboxcustom.png "NDP\_CheckBoxCustom")  
使用自定义控件模板的 checkbox  
  
 <xref:System.Windows.Controls.CheckBox> 的 <xref:System.Windows.Controls.ControlTemplate> 此示例相对复杂，因此，本主题使用创建 <xref:System.Windows.Controls.Button>的 <xref:System.Windows.Controls.ControlTemplate> 的简单示例。  
  
<a name="changing_the_visual_structure_of_a_control"></a>   
## 更改控件的可视结构  
 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]，控件通常是复合 <xref:System.Windows.FrameworkElement> 对象。  当您创建 <xref:System.Windows.Controls.ControlTemplate>时，组合 <xref:System.Windows.FrameworkElement> 对象建立一个控件。  <xref:System.Windows.Controls.ControlTemplate> 必须只有一 <xref:System.Windows.FrameworkElement> 作为其根元素。  根元素通常包含其他 <xref:System.Windows.FrameworkElement> 对象。  对象组合构成了控件的可视结构。  
  
 下面的示例创建 <xref:System.Windows.Controls.Button>的自定义 <xref:System.Windows.Controls.ControlTemplate> 。  <xref:System.Windows.Controls.ControlTemplate> 创建 <xref:System.Windows.Controls.Button>的可视结构。  ，当您将鼠标指针或单击它时，此示例不更改按钮的外观。  更改按钮的外观，在处于不同状态时本主题后面讨论。  
  
 在此示例中，可视结构由以下部分组成:  
  
-   <xref:System.Windows.Controls.Border> 名为用作模板的根 <xref:System.Windows.FrameworkElement>的 `RootElement` 。  
  
-   是 `RootElement`的子 <xref:System.Windows.Controls.Grid> 。  
  
-   显示按钮的内容的 <xref:System.Windows.Controls.ContentPresenter> 。  <xref:System.Windows.Controls.ContentPresenter> 使任何类型的对象显示。  
  
 [!code-xml[VSMButtonTemplate#BasicTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/buttonstages.xaml#basictemplate)]  
  
### 保留控件属性的功能通过使用 TemplateBinding 的  
 在创建新的 <xref:System.Windows.Controls.ControlTemplate>时，您仍可能想要使用公共属性更改控件的外观。  [TemplateBinding](../../../../docs/framework/wpf/advanced/templatebinding-markup-extension.md) 标记扩展将 <xref:System.Windows.Controls.ControlTemplate> 到公共属性是由控件定义的元素的属性。  当您使用 [TemplateBinding](../../../../docs/framework/wpf/advanced/templatebinding-markup-extension.md)时，可让控件的属性作为参数传递给模板。  也就是说，在控件的属性设置为时，该值将传递到已的 [TemplateBinding](../../../../docs/framework/wpf/advanced/templatebinding-markup-extension.md) 的元素。  
  
 下面的示例重复使用 [TemplateBinding](../../../../docs/framework/wpf/advanced/templatebinding-markup-extension.md) 标记扩展将中元素的属性绑定在 <xref:System.Windows.Controls.ControlTemplate> 到由按钮定义的公共属性前面的示例部分。  
  
 [!code-xml[VSMButtonTemplate#TemplateBinding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/buttonstages.xaml#templatebinding)]  
  
 在此示例中， <xref:System.Windows.Controls.Grid> 其 <xref:System.Windows.Controls.Panel.Background%2A?displayProperty=fullName> 属性模板绑定到 <xref:System.Windows.Controls.Control.Background%2A?displayProperty=fullName>。  由于 <xref:System.Windows.Controls.Panel.Background%2A?displayProperty=fullName> 是通过模板绑定的，您可以创建使用同一 <xref:System.Windows.Controls.ControlTemplate> 并将 <xref:System.Windows.Controls.Control.Background%2A?displayProperty=fullName> 到在每个按钮的不同值的多个按钮。  如果 <xref:System.Windows.Controls.Control.Background%2A?displayProperty=fullName> 不是通过模板绑定到元素的属性。 <xref:System.Windows.Controls.ControlTemplate>的，将按钮的 <xref:System.Windows.Controls.Control.Background%2A?displayProperty=fullName> 到按钮的外观没有任何影响。  
  
 请注意两个属性的名称不必相同。  在前面的示例中， <xref:System.Windows.Controls.Button> 的 <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A?displayProperty=fullName> 属性通过模板绑定到 <xref:System.Windows.Controls.ContentPresenter>的 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A?displayProperty=fullName> 属性。  这使水平放置按钮的内容。  <xref:System.Windows.Controls.ContentPresenter> 没有名为 `HorizontalContentAlignment`的属性，但是， <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A?displayProperty=fullName> 可以绑定到 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A?displayProperty=fullName>。  通过模板绑定属性时，请确保目标属性和源属性是同一类型。  
  
 <xref:System.Windows.Controls.Control> 类定义必须由控件模板用于对控件的效果的属性，这些设置。  <xref:System.Windows.Controls.ControlTemplate> 如何使用属性取决于属性。  <xref:System.Windows.Controls.ControlTemplate> 必须以下列方式之一使用属性:  
  
-   在 <xref:System.Windows.Controls.ControlTemplate> 模板的元素绑定到属性。  
  
-   在 <xref:System.Windows.Controls.ControlTemplate> 的元素从父继承 <xref:System.Windows.FrameworkElement>的属性。  
  
 下表列出了 <xref:System.Windows.Controls.Control> 类的控件继承的可视属性。  它还指示控件的默认控件模板是使用继承的属性值，或者必须是通过模板绑定。  
  
|属性|使用方法|  
|--------|----------|  
|<xref:System.Windows.Controls.Control.Background%2A>|模板绑定|  
|<xref:System.Windows.Controls.Control.BorderThickness%2A>|模板绑定|  
|<xref:System.Windows.Controls.Control.BorderBrush%2A>|模板绑定|  
|<xref:System.Windows.Controls.Control.FontFamily%2A>|属性继承或模板绑定|  
|<xref:System.Windows.Controls.Control.FontSize%2A>|属性继承或模板绑定|  
|<xref:System.Windows.Controls.Control.FontStretch%2A>|属性继承或模板绑定|  
|<xref:System.Windows.Controls.Control.FontWeight%2A>|属性继承或模板绑定|  
|<xref:System.Windows.Controls.Control.Foreground%2A>|属性继承或模板绑定|  
|<xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A>|模板绑定|  
|<xref:System.Windows.Controls.Control.Padding%2A>|模板绑定|  
|<xref:System.Windows.Controls.Control.VerticalContentAlignment%2A>|模板绑定|  
  
 下表列出 <xref:System.Windows.Controls.Control> 从类继承的仅可视属性。  除了表中列出的属性之外，控件还可以继承 <xref:System.Windows.FrameworkElement.DataContext%2A>、 <xref:System.Windows.FrameworkElement.Language%2A>和 <xref:System.Windows.Controls.TextBlock.TextDecorations%2A> 属性从父 framework 组件。  
  
 此外，，如果 <xref:System.Windows.Controls.ContentPresenter> 在 <xref:System.Windows.Controls.ContentControl>的 <xref:System.Windows.Controls.ControlTemplate> ， <xref:System.Windows.Controls.ContentPresenter> 将自动绑定到 <xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> 和 <xref:System.Windows.Controls.ContentControl.Content%2A> 属性。  同样，在 <xref:System.Windows.Controls.ItemsControl> 的 <xref:System.Windows.Controls.ControlTemplate> 的 <xref:System.Windows.Controls.ItemsPresenter> 将自动绑定到 <xref:System.Windows.Controls.ItemsControl.Items%2A> 和 <xref:System.Windows.Controls.ItemsPresenter> 属性。  
  
 下面的示例创建使用上一示例中定义的 <xref:System.Windows.Controls.ControlTemplate> 的两个按钮。  此示例将 <xref:System.Windows.Controls.Control.Background%2A>、 <xref:System.Windows.Controls.Control.Foreground%2A>和 <xref:System.Windows.Controls.Control.FontSize%2A> 属性在每个按钮。  ，因为它是在 <xref:System.Windows.Controls.ControlTemplate>，通过模板绑定的设置 <xref:System.Windows.Controls.Control.Background%2A> 属性的效果。  即使 <xref:System.Windows.Controls.Control.Foreground%2A> 和 <xref:System.Windows.Controls.Control.FontSize%2A> 属性不是通过模板绑定的，设置它们也有作用，因为它们的值继承。  
  
 [!code-xml[VSMButtonTemplate#ButtonDeclaration](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/buttonstages.xaml#buttondeclaration)]  
  
 前面示例生成与下图类似的输出。  
  
 ![两个按钮，其中一个蓝色，一个紫色。](../../../../docs/framework/wpf/controls/media/ndp-buttontwo.png "NDP\_ButtonTwo")  
具有不同背景色的两个按钮  
  
<a name="changing_the_appearance_of_a_control_depending_on_its_state"></a>   
## 更改控件外观根据自身的状态  
 ，它不同状态时，在一个按钮具有默认外观的和按钮之间的区别在前面的示例中是默认按钮变化。  例如，默认按钮的外观更改，当按下时，或者，当鼠标指针移到按钮时。  虽然 <xref:System.Windows.Controls.ControlTemplate> 不更改控件的功能，但它更改控件的可视行为。  ，在处于特定状态时，可视行为描述控件的外观。  若要了解控件的功能和可视行为之间的区别，请考虑按钮示例。  按钮的功能是引发 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件，当单击该控件时，但是，按钮的可视行为是更改其外观，而指向它时或按。  
  
 ，在处于特定状态时，使用 <xref:System.Windows.VisualState> 对象指定控件的外观。  <xref:System.Windows.VisualState> 包含更改元素的外观。 <xref:System.Windows.Controls.ControlTemplate>的 <xref:System.Windows.Media.Animation.Storyboard> 。  通过使用， <xref:System.Windows.VisualStateManager>，，因为控件的逻辑更改状态您不必编写使此的任何代码发生。  当控件进入由 <xref:System.Windows.VisualState.Name%2A?displayProperty=fullName> 属性指定的状态时， <xref:System.Windows.Media.Animation.Storyboard> 启动。  当控件退出该状态时， <xref:System.Windows.Media.Animation.Storyboard> 停止。  
  
 更改 <xref:System.Windows.Controls.Button> 外观的下面的示例演示 <xref:System.Windows.VisualState> ，当鼠标指针悬停在其上时。  <xref:System.Windows.Media.Animation.Storyboard> 通过将 `BorderBrush`的颜色更改按钮的边框颜色。  如果本文开头的引用 <xref:System.Windows.Controls.ControlTemplate> 示例，您记住 `BorderBrush` 是分配给 <xref:System.Windows.Controls.Border>的 <xref:System.Windows.Controls.Border.Background%2A><xref:System.Windows.Media.SolidColorBrush> 的名称。  
  
 [!code-xml[VSMButtonTemplate#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/skinnedbutton.xaml#4)]  
  
 该控件负责定义状态作为其控件协定的一部分，在 [自定义其他控件通过了解控件协定](#customizing_other_controls_by_understanding_the_control_contract) 后详细讨论本主题。  下表列出了 <xref:System.Windows.Controls.Button>指定的状态。  
  
|VisualState 名称|VisualStateGroup 名称|说明|  
|--------------------|-------------------------|--------|  
|常规|CommonStates|默认状态。|  
|MouseOver|CommonStates|鼠标指针置于控件。|  
|按|CommonStates|该控件已按下。|  
|已禁用|CommonStates|控件被禁用。|  
|焦点|FocusStates|控件具有焦点。|  
|unfocused|FocusStates|控件不具有焦点。|  
  
 <xref:System.Windows.Controls.Button> 定义两个状态组: `CommonStates` 组包含 `Normal`、 `MouseOver`、 `Pressed`和 `Disabled` 状态。  `FocusStates` 组包含 `Focused` 和 `Unfocused` 状态。  基于同一状态组中互相排斥。  控件始终在正确每个组一个状态。  例如， <xref:System.Windows.Controls.Button> 可能具有焦点，即使当鼠标指针不在它，因此，在 `Focused` 状态的 <xref:System.Windows.Controls.Button> 可以在 `MouseOver`、 `Pressed`或 `Normal` 状态。  
  
 向该 <xref:System.Windows.VisualStateGroup> 对象的 <xref:System.Windows.VisualState> 对象。  请向该 <xref:System.Windows.VisualStateManager.VisualStateGroups%2A?displayProperty=fullName> 附加属性的 <xref:System.Windows.VisualStateGroup> 对象。  下面的示例定义 `Normal`、 `MouseOver`和 `Pressed` 状态的 <xref:System.Windows.VisualState> 对象，都在 `CommonStates` 组中。  每 <xref:System.Windows.VisualState><xref:System.Windows.VisualState.Name%2A> 上表中的匹配名称。  `Disabled` 状态和状态。 `FocusStates` 组中省略使该示例简短，但是，它们在整个示例包括本主题末尾的。  
  
> [!NOTE]
>  请确保将在 <xref:System.Windows.Controls.ControlTemplate>的根 <xref:System.Windows.FrameworkElement> 的 <xref:System.Windows.VisualStateManager.VisualStateGroups%2A?displayProperty=fullName> 附加属性。  
  
 [!code-xml[VSMButtonTemplate#VisualStates](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/buttonstages.xaml#visualstates)]  
  
 前面示例生成与下图类似的输出。  
  
 ![一个具有自定义控件模板的按钮。](../../../../docs/framework/wpf/controls/media/ndp-buttonnormal.png "NDP\_ButtonNormal")  
处于正常状态的使用自定义控件模板的按钮  
  
 ![一个具有红色边框的按钮。](../../../../docs/framework/wpf/controls/media/ndp-buttonmouseover.png "NDP\_ButtonMouseOver")  
在鼠标悬停状态的使用自定义控件模板的按钮  
  
 ![按下的按钮上的边框是透明的。](../../../../docs/framework/wpf/controls/media/ndp-buttonpressed.png "NDP\_ButtonPressed")  
在一个处于按下状态的使用自定义控件模板的按钮  
  
 若要查找附带 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]的控件的可视状态，请参见 [Control 样式和模板](../../../../docs/framework/wpf/controls/control-styles-and-templates.md)。  
  
<a name="specifying_the_behavior_of_a_control_when_it_transitions_between_states"></a>   
## 指定控件的行为，当在状态之间的转换  
 在前面的示例中，按钮的外观也会更改，当用户单击该按钮，，但，除非将按钮按下整整，则用户将看到该效果。  默认情况下，动画需要花费发生。  由于用户可以单击和释放对小于时的一个按钮，视觉上将看不到，如果您在其默认状态将 <xref:System.Windows.Controls.ControlTemplate> 保留。  
  
 可以指定它使动画出现到较为物价控件从一种状态到另一个通过向 <xref:System.Windows.Controls.ControlTemplate>的 <xref:System.Windows.VisualTransition> 对象的时间。  当您创建 <xref:System.Windows.VisualTransition>时，指定以下一种或多种:  
  
-   为转换采用在状态之间发生的时间。  
  
-   在转换时发生的控件外观的其他更改。  
  
-   的状态 <xref:System.Windows.VisualTransition> 适用。  
  
### 指定转换的持续时间  
 可以指定转换所需的时间通过设置 <xref:System.Windows.VisualTransition.GeneratedDuration%2A> 属性采用。  指定的前面的示例有 <xref:System.Windows.VisualState> 按钮边框变为透明，当按下时，但是，动画将来不及产生动作。，如果按钮快速按下并释放。  可以使用 <xref:System.Windows.VisualTransition> 指定所耗费转换为按下状态的时间。  下面的示例指定控件采用的一个进入按下状态。  
  
 [!code-xml[VSMButtonTemplate#PressedTransition](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/skinnedbutton.xaml#pressedtransition)]  
  
### 指定对控件外观的更改在传输时  
 <xref:System.Windows.VisualTransition> 包含开始，在控件转换状态时的 <xref:System.Windows.Media.Animation.Storyboard> 。  例如，可以指定某动画从 `MouseOver` 状态时，会发生控件转换为 `Normal` 状态。  指定下面的示例创建 <xref:System.Windows.VisualTransition> ，当用户将鼠标指针从按钮上移开时，按钮的边框变为蓝色，然后变为黄色，然后为黑色位于 1.5 秒。  
  
 [!code-xml[VSMButtonTemplate#8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/skinnedbutton.xaml#8)]  
  
### 指定，在何时应用的  
 <xref:System.Windows.VisualTransition> 可限制应用于某些状态，也可以随时将控件进行状态转换的。  在前面的示例中，那么，当控件从状态 `MouseOver` 转到 `Normal` 状态时， <xref:System.Windows.VisualTransition> 是应用程序的;在中， <xref:System.Windows.VisualTransition> 是应用前面的示例中，当控件进入 `Pressed` 状态。  您限制，当设置 <xref:System.Windows.VisualTransition.To%2A> 和 <xref:System.Windows.VisualTransition.From%2A> 特性时 <xref:System.Windows.VisualTransition> 。  下表描述的限制级别从最高的限制到最不受限制。  
  
|限制类型|值。|值|  
|----------|--------|-------|  
|从指定状态到另一个指定状态|<xref:System.Windows.VisualState>的名称|<xref:System.Windows.VisualState>的名称|  
|从任意状态到指定的状态|未设置|<xref:System.Windows.VisualState>的名称|  
|从指定状态到任意状态|<xref:System.Windows.VisualState>的名称|未设置|  
|从任意状态到其他状态|未设置|未设置|  
  
 可以引用同一状态。 <xref:System.Windows.VisualStateGroup> 的多个 <xref:System.Windows.VisualTransition> 对象，但是，将按上表指定的顺序。  在下面的示例中，有两 <xref:System.Windows.VisualTransition> 对象。  当具有的 `MouseOver` 状态， <xref:System.Windows.VisualTransition><xref:System.Windows.VisualTransition.From%2A> 和 <xref:System.Windows.VisualTransition.To%2A> 设置使用从 `Pressed` 状态的控件转换。  当，使用其他状态从不是 `Pressed` 到 `MouseOver` 的状态的控件转换。  
  
 [!code-xml[VSMButtonTemplate#7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/skinnedbutton.xaml#7)]  
  
 <xref:System.Windows.VisualStateGroup> 包含 <xref:System.Windows.VisualTransition> 对象应用于 <xref:System.Windows.VisualState> 在 <xref:System.Windows.VisualStateGroup>对象的一个 <xref:System.Windows.VisualStateGroup.Transitions%2A> 属性。  作为 <xref:System.Windows.Controls.ControlTemplate> 作者，您可以随意包括所有需要的 <xref:System.Windows.VisualTransition> 。  但是，因此，如果 <xref:System.Windows.VisualTransition.To%2A> 和 <xref:System.Windows.VisualTransition.From%2A> 属性设置为中不存在 <xref:System.Windows.VisualStateGroup>的名称， <xref:System.Windows.VisualTransition> 被忽略。  
  
 下面的示例演示 `CommonStates`的 <xref:System.Windows.VisualStateGroup> 。  在转换后，此示例定义按钮中的 <xref:System.Windows.VisualTransition> 。  
  
-   为 `Pressed` 状态。  
  
-   为 `MouseOver` 状态。  
  
-   从 `Pressed` 状态到 `MouseOver` 状态。  
  
-   从 `MouseOver` 状态到 `Normal` 状态。  
  
 [!code-xml[VSMButtonTemplate#VisualTransitions](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/buttonstages.xaml#visualtransitions)]  
  
<a name="customizing_other_controls_by_understanding_the_control_contract"></a>   
## 自定义其他控件通过了解控件协定  
 使用 <xref:System.Windows.Controls.ControlTemplate> 指定其可视结构的控件 \(通过使用 <xref:System.Windows.FrameworkElement> 对象\)，和可视行为 \(通过使用 <xref:System.Windows.VisualState> 对象\) 使用部件控件模型。  包含 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 4 的许多控件都使用此模型  <xref:System.Windows.Controls.ControlTemplate> 作者需要了解的部件通过控件协定传递。  当您了解控件协定的组成部分之后，您可以自定义使用部件控件模型的所有控件的外观。  
  
 控件协定有三个组件:  
  
-   控件的逻辑使用的可视元素。  
  
-   控件和组的状态每个状态所属。  
  
-   以可视方式影响控件的公共属性。  
  
### 在控件协定的可视元素  
 有时在 <xref:System.Windows.Controls.ControlTemplate>的控件的逻辑与 <xref:System.Windows.FrameworkElement> 交互。  例如，控件可以处理事件其元素之一。  在控件中找到在 <xref:System.Windows.Controls.ControlTemplate>时的特殊 <xref:System.Windows.FrameworkElement> ，它必须将该信息。 <xref:System.Windows.Controls.ControlTemplate> 作者。  控件使用 <xref:System.Windows.TemplatePartAttribute> 传递期望使用的元素的类型，，以及元素应具有的名称。  <xref:System.Windows.Controls.Button> 在其控件协定中没有 <xref:System.Windows.FrameworkElement> 部件，但是，其他控件，例如， <xref:System.Windows.Controls.ComboBox>。  
  
 下面的示例演示在 <xref:System.Windows.Controls.ComboBox> 类指定的 <xref:System.Windows.TemplatePartAttribute> 对象。  <xref:System.Windows.Controls.ComboBox> 逻辑找到 <xref:System.Windows.Controls.TextBox> 名为 `PART_EditableTextBox` 与其 <xref:System.Windows.Controls.ControlTemplate>名为的 `PART_Popup`<xref:System.Windows.Controls.Primitives.Popup> 。  
  
 [!code-csharp[VSMButtonTemplate#ComboBoxContract](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/controlcontracts.cs#comboboxcontract)]
 [!code-vb[VSMButtonTemplate#ComboBoxContract](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/vsmbuttontemplate/visualbasic/window1.xaml.vb#comboboxcontract)]  
  
 包含元素由 <xref:System.Windows.TemplatePartAttribute> 对象指定在 <xref:System.Windows.Controls.ComboBox> 类的示例显示 <xref:System.Windows.Controls.ComboBox> 的简化 <xref:System.Windows.Controls.ControlTemplate> 。  
  
 [!code-xml[VSMButtonTemplate#ComboBoxTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/window1.xaml#comboboxtemplate)]  
  
### 在控件协定的状态  
 控件状态也是控件协定的组成部分。  创建 <xref:System.Windows.Controls.Button> 的 <xref:System.Windows.Controls.ControlTemplate> 的示例演示如何根据其状态指定 <xref:System.Windows.Controls.Button> 的外观。  您创建的每一个指定状态的 <xref:System.Windows.VisualState> 并将共享。 <xref:System.Windows.VisualStateGroup>的 <xref:System.Windows.TemplateVisualStateAttribute.GroupName%2A> 的所有 <xref:System.Windows.VisualState> 对象，如 [更改控件外观根据自身的状态](#changing_the_appearance_of_a_control_depending_on_its_state) 本主题中前面所述  使用 <xref:System.Windows.TemplateVisualStateAttribute>，第三方控件应指定状态，使设计工具，例如 expression blend，显示创作的控件模板的状态。  
  
 若要查找附带 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]的控件的控件协定，请参见 [Control 样式和模板](../../../../docs/framework/wpf/controls/control-styles-and-templates.md)。  
  
### 在控件协定中的属性  
 以可视方式影响控件的公共属性在控件协定还包括。  可以设置这些属性更改控件的外观，而无需创建新的 <xref:System.Windows.Controls.ControlTemplate>。  还可以使用 [TemplateBinding](../../../../docs/framework/wpf/advanced/templatebinding-markup-extension.md) 标记扩展将中 <xref:System.Windows.Controls.ControlTemplate> 到公共属性由 <xref:System.Windows.Controls.Button>定义的元素的属性绑定。  
  
 下面的示例演示按钮的控件协定。  
  
 [!code-csharp[VSMButtonTemplate#ButtonContract](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/controlcontracts.cs#buttoncontract)]
 [!code-vb[VSMButtonTemplate#ButtonContract](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/vsmbuttontemplate/visualbasic/window1.xaml.vb#buttoncontract)]  
  
 在创建 <xref:System.Windows.Controls.ControlTemplate>时，从现有 <xref:System.Windows.Controls.ControlTemplate> 启动并对其进行更改通常最简便的。  可以执行下列操作之一来更改现有 <xref:System.Windows.Controls.ControlTemplate>:  
  
-   使用设计器，例如 expression blend，提供用于创建控件模板的图形用户界面。  有关更多信息，请参见 [样式支持模板的控件](http://go.microsoft.com/fwlink/?LinkId=161153)。  
  
-   获取默认 <xref:System.Windows.Controls.ControlTemplate> 并对其进行编辑。  若要查找该默认控件包含 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]的模板，请参见[默认 WPF 主题](http://go.microsoft.com/fwlink/?LinkID=158252)。  
  
<a name="complete_example"></a>   
## 完成示例  
 本主题讨论下面的示例演示完整 <xref:System.Windows.Controls.Button><xref:System.Windows.Controls.ControlTemplate> 。  
  
 [!code-xml[VSMButtonTemplate#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmbuttontemplate/csharp/skinnedbutton.xaml#3)]  
  
## 请参阅  
 [样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)