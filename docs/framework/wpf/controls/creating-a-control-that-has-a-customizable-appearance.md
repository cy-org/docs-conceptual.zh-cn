---
title: "创建具有可自定义外观的控件 | Microsoft Docs"
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
  - "控件 [WPF], 自定义"
  - "控件 [WPF], 定义可视结构和行为"
  - "ControlTemplate [WPF], 自定义外观"
  - "自定义外观 [WPF], ControlTemplate"
  - "管理控件状态 [WPF], VisualStateManager"
  - "VisualStateManager [WPF], 最佳做法"
  - "VisualStateManager [WPF], 管理控件的状态"
ms.assetid: 9e356d3d-a3d0-4b01-a25f-2d43e4d53fe5
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 创建具有可自定义外观的控件
<a name="introduction"></a> [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 使您能够创建其外观可自定义的控件。  例如，您可以通过创建新的 <xref:System.Windows.Controls.ControlTemplate> 来更改 <xref:System.Windows.Controls.CheckBox> 的外观，使之超越设置属性所能达到的效果。  下图演示一个使用默认 <xref:System.Windows.Controls.ControlTemplate> 的 <xref:System.Windows.Controls.CheckBox> 和一个使用自定义 <xref:System.Windows.Controls.ControlTemplate> 的 <xref:System.Windows.Controls.CheckBox>。  
  
 ![一个具有默认控件模板的复选框。](../../../../docs/framework/wpf/controls/media/ndp-checkboxdefault.png "NDP\_CheckBoxDefault")  
一个使用默认控件模板的 CheckBox  
  
 ![一个具有自定义控件模板的复选框。](../../../../docs/framework/wpf/controls/media/ndp-checkboxcustom.png "NDP\_CheckBoxCustom")  
一个使用自定义控件模板的 CheckBox  
  
 如果您在创建控件时遵循部件和状态模型，则控件的外观将是可自定义的。  诸如 Microsoft Expression Blend 的设计器工具支持部件和状态模型，因此，当您遵循此模型时，在这些类型的应用程序中，您的控件将是可自定义的。  本主题讨论部件和状态模型，以及您在创建自己的控件时如何遵循该模型。  本主题使用一个自定义控件示例 `NumericUpDown` 来说明此模型的原理。  `NumericUpDown` 控件显示一个数值，用户可通过单击控件的按钮来增加或减少该数值。  下图演示了在本主题中讨论的 `NumericUpDown` 控件。  
  
 ![NumericUpDown 自定义控件。](../../../../docs/framework/wpf/controls/media/ndp-numericupdown.png "NDP\_NumericUPDown")  
自定义 NumericUpDown 控件  
  
 本主题包含以下各节：  
  
-   [必备组件](#prerequisites)  
  
-   [部件和状态模型](#parts_and_states_model)  
  
-   [在 ControlTemplate 中定义控件的可视结构和可视行为](#defining_the_visual_structure_and_visual_behavior_of_a_control_in_a_controltemplate)  
  
-   [在代码中使用 ControlTemplate 的部件](#using_parts_of_the_controltemplate_in_code)  
  
-   [提供控件协定](#providing_the_control_contract)  
  
-   [完整的示例](#complete_example)  
  
<a name="prerequisites"></a>   
## 必备组件  
 本主题假设您了解如何为现有控件创建新的 <xref:System.Windows.Controls.ControlTemplate>，熟悉控件协定中各元素的含义，并且了解在[通过创建 ControlTemplate 自定义现有控件的外观](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md)中讨论的概念。  
  
> [!NOTE]
>  若要创建可自定义其外观的控件，您必须创建一个控件，此控件从 <xref:System.Windows.Controls.Control> 类或其一个子类（<xref:System.Windows.Controls.UserControl> 除外）继承。  从 <xref:System.Windows.Controls.UserControl> 继承的控件是一个可以快速创建的控件，但它不使用 <xref:System.Windows.Controls.ControlTemplate>，因此您无法自定义其外观。  
  
<a name="parts_and_states_model"></a>   
## 部件和状态模型  
 部件和状态模型指定如何定义控件的可视结构和可视行为。  若要遵循部件和状态模型，应执行以下操作：  
  
-   在控件的 <xref:System.Windows.Controls.ControlTemplate> 中定义可视结构和可视行为。  
  
-   当控件的逻辑与控件模板的部件交互时，请遵循某些最佳做法。  
  
-   提供控件协定，以指定应在 <xref:System.Windows.Controls.ControlTemplate> 中包含哪些内容。  
  
 当您在控件的 <xref:System.Windows.Controls.ControlTemplate> 中定义可视结构和可视行为时，应用程序作者可以通过创建新的 <xref:System.Windows.Controls.ControlTemplate> 而不是编写代码来更改控件的可视结构和可视行为。  您必须提供控件协定，以告知应用程序作者应在 <xref:System.Windows.Controls.ControlTemplate> 中定义哪些 <xref:System.Windows.FrameworkElement> 对象和状态。  当您与 <xref:System.Windows.Controls.ControlTemplate> 中的部件进行交互时，应遵循某些最佳做法，以便控件正确地处理不完整的 <xref:System.Windows.Controls.ControlTemplate>。  如果您遵循这三个原则，则应用程序作者将能够像对随 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供的控件一样，轻松地为您的控件创建 <xref:System.Windows.Controls.ControlTemplate>。  下面一节详细地说明其中的每条建议。  
  
<a name="defining_the_visual_structure_and_visual_behavior_of_a_control_in_a_controltemplate"></a>   
## 在 ControlTemplate 中定义控件的可视结构和可视行为  
 当您使用部件和状态模型创建自定义控件时，可以在其 <xref:System.Windows.Controls.ControlTemplate> 中（而不是在其逻辑中）定义控件的可视结构和可视行为。  控件的可视结构是构成控件的 <xref:System.Windows.FrameworkElement> 对象的组合。  可视行为是当控件处于特定状态时所显示的方式。  有关创建用于指定控件的可视结构和可视行为的 <xref:System.Windows.Controls.ControlTemplate> 的更多信息，请参见[通过创建 ControlTemplate 自定义现有控件的外观](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md)。  
  
 在 `NumericUpDown` 控件的示例中，可视结构包括两个 <xref:System.Windows.Controls.Primitives.RepeatButton> 控件和一个 <xref:System.Windows.Controls.TextBlock>。  如果您在 `NumericUpDown` 控件的代码（例如，其构造函数）中添加这些控件，则这些控件的位置将不可改变。  请勿在控件的代码中定义其可视结构和可视行为，而应在 <xref:System.Windows.Controls.ControlTemplate> 中定义这些内容。  然后，应用程序开发人员可以自定义按钮和 <xref:System.Windows.Controls.TextBlock> 的位置，并指定当 `Value` 为负时所发生的行为（因为可以替换 <xref:System.Windows.Controls.ControlTemplate>）。  
  
 下面的示例演示 `NumericUpDown` 控件的可视结构，它包括一个可增加 `Value` 的 <xref:System.Windows.Controls.Primitives.RepeatButton>、一个可减小 `Value` 的 <xref:System.Windows.Controls.Primitives.RepeatButton> 和一个可显示 `Value` 的 <xref:System.Windows.Controls.TextBlock>。  
  
 [!code-xml[VSMCustomControl#VisualStructure](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/window1.xaml#visualstructure)]  
  
 `NumericUpDown` 控件的可视行为是：如果值为负，则值为红色字体。  如果您当 `Value` 为负时在代码中更改 <xref:System.Windows.Controls.TextBlock> 的 <xref:System.Windows.Controls.TextBlock.Foreground%2A>，则 `NumericUpDown` 将始终显示红色的负值。  您可以通过将 <xref:System.Windows.VisualState> 对象添加到 <xref:System.Windows.Controls.ControlTemplate> 中，在 <xref:System.Windows.Controls.ControlTemplate> 中指定控件的可视行为。  下面的示例演示 `Positive` 和 `Negative` 状态的 <xref:System.Windows.VisualState> 对象。  `Positive` 和 `Negative` 是互斥的（控件始终处于这两种状态之一），因此，该示例将 <xref:System.Windows.VisualState> 对象放到单个 <xref:System.Windows.VisualStateGroup> 中。  当控件进入 `Negative` 状态时，<xref:System.Windows.Controls.TextBlock> 的 <xref:System.Windows.Controls.TextBlock.Foreground%2A> 将变为红色。  当控件处于 `Positive` 状态时，<xref:System.Windows.Controls.TextBlock.Foreground%2A> 将返回到其原始值。  将在[通过创建 ControlTemplate 自定义现有控件的外观](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md)中进一步讨论如何在 <xref:System.Windows.Controls.ControlTemplate> 中定义 <xref:System.Windows.VisualState> 对象。  
  
> [!NOTE]
>  请务必设置 <xref:System.Windows.Controls.ControlTemplate> 的根 <xref:System.Windows.FrameworkElement> 上的 <xref:System.Windows.VisualStateManager.VisualStateGroups%2A?displayProperty=fullName> 附加属性。  
  
 [!code-xml[VSMCustomControl#ValueStates](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/window1.xaml#valuestates)]  
  
<a name="using_parts_of_the_controltemplate_in_code"></a>   
## 在代码中使用 ControlTemplate 的部件  
 <xref:System.Windows.Controls.ControlTemplate> 作者可能会故意或错误地遗漏 <xref:System.Windows.FrameworkElement> 或 <xref:System.Windows.VisualState> 对象，但控件的逻辑可能需要这些部件才能正常运行。  部件和状态模型指定您的控件应能够处理缺少 <xref:System.Windows.FrameworkElement> 或 <xref:System.Windows.VisualState> 对象的 <xref:System.Windows.Controls.ControlTemplate>。  如果 <xref:System.Windows.Controls.ControlTemplate> 中缺少 <xref:System.Windows.FrameworkElement>、<xref:System.Windows.VisualState> 或 <xref:System.Windows.VisualStateGroup>，则控件不应引发异常或报告错误。  本节描述了与 <xref:System.Windows.FrameworkElement> 对象交互以及管理状态的建议做法。  
  
### 预计缺少的 FrameworkElement 对象  
 当您在 <xref:System.Windows.Controls.ControlTemplate> 中定义 <xref:System.Windows.FrameworkElement> 对象时，控件的逻辑可能需要与其中某些对象进行交互。  例如，`NumericUpDown` 控件订阅按钮的 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件以增加或减少 `Value`，并将 <xref:System.Windows.Controls.TextBlock> 的 <xref:System.Windows.Controls.TextBlock.Text%2A> 属性设置为 `Value`。  如果自定义 <xref:System.Windows.Controls.ControlTemplate> 遗漏 <xref:System.Windows.Controls.TextBlock> 或按钮，则控件失去其某些功能是可接受的，但您应确保控件不会导致错误。  例如，如果 <xref:System.Windows.Controls.ControlTemplate> 不包含用于更改 `Value` 的按钮，则 `NumericUpDown` 将失去该功能，但使用 <xref:System.Windows.Controls.ControlTemplate> 的应用程序将继续运行。  
  
 下面的做法将确保您的控件正确地响应缺少 <xref:System.Windows.FrameworkElement> 对象的情况：  
  
1.  为您需要在代码中引用的每个 <xref:System.Windows.FrameworkElement> 设置 `x:Name` 特性。  
  
2.  为您需要交互的每个 <xref:System.Windows.FrameworkElement> 定义私有属性。  
  
3.  订阅和取消订阅控件在 <xref:System.Windows.FrameworkElement> 属性的 set 访问器中处理的任何事件。  
  
4.  设置您在 <xref:System.Windows.FrameworkElement.OnApplyTemplate%2A> 方法的步骤 2 中定义的 <xref:System.Windows.FrameworkElement> 属性。  这是 <xref:System.Windows.Controls.ControlTemplate> 中的 <xref:System.Windows.FrameworkElement> 可用于控件的最早方式。  使用 <xref:System.Windows.FrameworkElement> 的 `x:Name` 从 <xref:System.Windows.Controls.ControlTemplate> 中获取该元素。  
  
5.  在访问 <xref:System.Windows.FrameworkElement> 的各成员之前，检查它是否为 `null`。  如果它为 `null`，则不报告错误。  
  
 下面的示例演示 `NumericUpDown` 控件如何按照上面列表中的建议与 <xref:System.Windows.FrameworkElement> 对象交互。  
  
 在用于在 <xref:System.Windows.Controls.ControlTemplate> 中定义 `NumericUpDown` 控件的可视结构的示例中，增加 `Value` 的 <xref:System.Windows.Controls.Primitives.RepeatButton> 已将其 `x:Name` 特性设置为 `UpButton`。  下面的示例声明一个称为 `UpButtonElement` 的属性，它表示在 <xref:System.Windows.Controls.ControlTemplate> 中声明的 <xref:System.Windows.Controls.Primitives.RepeatButton>。  `set` 访问器首先取消订阅按钮的 <xref:System.Windows.Controls.Primitives.ButtonBase.Click>（即使 `UpDownElement` 不为 `null`），然后它设置该属性，接着它订阅 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件。  在此还为另一个称为 `DownButtonElement` 的 <xref:System.Windows.Controls.Primitives.RepeatButton> 定义了属性，但并未显示。  
  
 [!code-csharp[VSMCustomControl#UpButtonProperty](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#upbuttonproperty)]
 [!code-vb[VSMCustomControl#UpButtonProperty](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#upbuttonproperty)]  
  
 下面的示例演示 `NumericUpDown` 控件的 <xref:System.Windows.FrameworkElement.OnApplyTemplate%2A>。  该示例使用 <xref:System.Windows.FrameworkElement.GetTemplateChild%2A> 方法从 <xref:System.Windows.Controls.ControlTemplate> 获取 <xref:System.Windows.FrameworkElement> 对象。  请注意，此示例可防止出现 <xref:System.Windows.FrameworkElement.GetTemplateChild%2A> 使用非预期类型的指定名称查找 <xref:System.Windows.FrameworkElement> 的情况。  忽略具有指定的 `x:Name` 但类型不正确的元素也是一种最佳做法。  
  
 [!code-csharp[VSMCustomControl#ApplyTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#applytemplate)]
 [!code-vb[VSMCustomControl#ApplyTemplate](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#applytemplate)]  
  
 通过遵循在前面示例中演示的做法，您可以确保控件将在 <xref:System.Windows.Controls.ControlTemplate> 缺少 <xref:System.Windows.FrameworkElement> 时继续运行。  
  
### 使用 VisualStateManager 管理状态  
 <xref:System.Windows.VisualStateManager> 可跟踪控件的状态，并执行在状态之间转换所需的逻辑。  当您将 <xref:System.Windows.VisualState> 对象添加到 <xref:System.Windows.Controls.ControlTemplate> 时，您可以将它们添加到 <xref:System.Windows.VisualStateGroup>，并将 <xref:System.Windows.VisualStateGroup> 添加到 <xref:System.Windows.VisualStateManager.VisualStateGroups%2A?displayProperty=fullName> 附加属性，以便 <xref:System.Windows.VisualStateManager> 可以访问它们。  
  
 下面的示例重复前一个用于演示与控件的 `Positive` 和 `Negative` 状态对应的 <xref:System.Windows.VisualState> 对象的示例。  `Negative` <xref:System.Windows.VisualState> 中的 <xref:System.Windows.Media.Animation.Storyboard> 将 <xref:System.Windows.Controls.TextBlock> 的 <xref:System.Windows.Controls.TextBlock.Foreground%2A> 变为红色。  当 `NumericUpDown` 控件处于 `Negative` 状态时，处于 `Negative` 状态的演示图板将开始。  然后，当控件返回到 `Positive` 状态时，处于 `Negative` 状态的 <xref:System.Windows.Media.Animation.Storyboard> 将停止。  `Positive` <xref:System.Windows.VisualState> 不需要包含 <xref:System.Windows.Media.Animation.Storyboard>，因为当 `Negative` 的 <xref:System.Windows.Media.Animation.Storyboard> 停止时，<xref:System.Windows.Controls.TextBlock.Foreground%2A> 将返回到其原始颜色。  
  
 [!code-xml[VSMCustomControl#ValueStates](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/window1.xaml#valuestates)]  
  
 请注意，会为 <xref:System.Windows.Controls.TextBlock> 提供一个名称，但 <xref:System.Windows.Controls.TextBlock> 不位于 `NumericUpDown` 的控件协定中，因为控件的逻辑从不引用 <xref:System.Windows.Controls.TextBlock>。  在 <xref:System.Windows.Controls.ControlTemplate> 中引用的元素具有名称，但不需要属于控件协定，因为控件的新 <xref:System.Windows.Controls.ControlTemplate> 可能不需要引用该元素。  例如，为 `NumericUpDown` 创建新 <xref:System.Windows.Controls.ControlTemplate> 的人员可能决定不通过更改 <xref:System.Windows.Controls.Control.Foreground%2A> 指示 `Value` 为负。  在这种情况下，代码和 <xref:System.Windows.Controls.ControlTemplate> 都不会按名称引用 <xref:System.Windows.Controls.TextBlock>。  
  
 控件的逻辑负责更改控件的状态。  下面的示例演示 `NumericUpDown` 控件调用 <xref:System.Windows.VisualStateManager.GoToState%2A> 方法，以在 `Value` 大于或等于 0 时进入 `Positive` 状态；而当 `Value` 小于 0 时进入 `Negative` 状态。  
  
 [!code-csharp[VSMCustomControl#ValueStateChange](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#valuestatechange)]
 [!code-vb[VSMCustomControl#ValueStateChange](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#valuestatechange)]  
  
 <xref:System.Windows.VisualStateManager.GoToState%2A> 方法可执行相应地启动和停止演示图板所需的逻辑。  当控件调用 <xref:System.Windows.VisualStateManager.GoToState%2A> 以更改其状态时，<xref:System.Windows.VisualStateManager> 将执行以下操作：  
  
-   如果控件要进入的 <xref:System.Windows.VisualState> 具有 <xref:System.Windows.Media.Animation.Storyboard>，演示图板将开始运行。  然后，如果控件要来自的 <xref:System.Windows.VisualState> 具有 <xref:System.Windows.Media.Animation.Storyboard>，演示图板将结束运行。  
  
-   如果控件已处于指定的状态，则 <xref:System.Windows.VisualStateManager.GoToState%2A> 不执行任何操作并会返回 `true`。  
  
-   如果在 `control` 的 <xref:System.Windows.Controls.ControlTemplate> 中不存在指定的状态，则 <xref:System.Windows.VisualStateManager.GoToState%2A> 不执行任何操作并会返回 `false`。  
  
#### 使用 VisualStateManager 的最佳做法  
 建议您执行以下操作以保持控件的状态：  
  
-   使用属性来跟踪其状态。  
  
-   创建帮助器方法以在状态之间进行转换。  
  
 `NumericUpDown` 控件使用其 `Value` 属性跟踪它是处于 `Positive` 还是 `Negative` 状态。  The `NumericUpDown` 控件还定义 `Focused` 和 `UnFocused` 状态，这些状态可跟踪 <xref:System.Windows.UIElement.IsFocused%2A> 属性。  如果使用的状态无法自然对应于控件的属性，则可以定义一个私有属性来跟踪状态。  
  
 更新所有状态的单个方法会集中对 <xref:System.Windows.VisualStateManager> 的调用并使代码易于管理。  下面的示例演示 `NumericUpDown` 控件的帮助器方法 `UpdateStates`。  当 `Value` 大于或等于 0 时，<xref:System.Windows.Controls.Control> 处于 `Positive` 状态。  当 `Value` 小于 0 时，控件处于 `Negative` 状态。  当 <xref:System.Windows.UIElement.IsFocused%2A> 为 `true` 时，控件处于 `Focused` 状态；否则它处于 `Unfocused` 状态。  每当控件需要更改其状态时，都可以调用 `UpdateStates`，这与什么状态发生更改无关。  
  
 [!code-csharp[VSMCustomControl#UpdateStates](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#updatestates)]
 [!code-vb[VSMCustomControl#UpdateStates](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#updatestates)]  
  
 如果您在控件已处于 <xref:System.Windows.VisualStateManager.GoToState%2A> 状态时将状态名称传递到该状态，<xref:System.Windows.VisualStateManager.GoToState%2A> 将不执行任何操作，因此，您不需要检查控件的当前状态。  例如，如果 `Value` 从一个负数更改为另一个负数，则 `Negative` 状态的演示图板将不会中断，用户在控件中将看不到更改。  
  
 当您调用 <xref:System.Windows.VisualStateManager.GoToState%2A> 时，<xref:System.Windows.VisualStateManager> 使用 <xref:System.Windows.VisualStateGroup> 对象来确定要退出哪种状态。  对于在控件的 <xref:System.Windows.Controls.ControlTemplate> 中定义的每个 <xref:System.Windows.VisualStateGroup>，控件始终处于一种状态；仅当控件从同一个 <xref:System.Windows.VisualStateGroup> 进入另一个状态时，才离开前一状态。  例如，`NumericUpDown` 控件的 <xref:System.Windows.Controls.ControlTemplate> 在一个 <xref:System.Windows.VisualStateGroup> 中定义 `Positive` 和 `Negative` <xref:System.Windows.VisualState> 对象，而在另一个组中定义 `Focused` 和 `Unfocused` <xref:System.Windows.VisualState> 对象。  （您可以查看在本主题的[完整的示例](#complete_example)一节中定义的 `Focused` 和 `Unfocused` <xref:System.Windows.VisualState>）当控件从 `Positive` 状态进入 `Negative` 状态（或相反）时，控件将保持在 `Focused` 或 `Unfocused` 状态。  
  
 在以下三种典型的情况下，控件的状态可能更改：  
  
-   当将 <xref:System.Windows.Controls.ControlTemplate> 应用到 <xref:System.Windows.Controls.Control> 时。  
  
-   当属性更改时。  
  
-   当发生事件时。  
  
 下面的示例演示在这些情况下如何更新 `NumericUpDown` 控件的状态。  
  
 您应在 <xref:System.Windows.FrameworkElement.OnApplyTemplate%2A> 方法中更新控件的状态，以便当应用 <xref:System.Windows.Controls.ControlTemplate> 时，控件以正确的状态出现。  下面的示例在 <xref:System.Windows.FrameworkElement.OnApplyTemplate%2A> 中调用 `UpdateStates`，以确保控件处于适当的状态。  例如，假设您创建 `NumericUpDown` 控件，然后将其 <xref:System.Windows.Controls.Control.Foreground%2A> 设置为绿色并将 `Value` 设置为 \-5。  如果在将 <xref:System.Windows.Controls.ControlTemplate> 应用于 `NumericUpDown` 控件时未调用 `UpdateStates`，则控件将不处于 `Negative` 状态，并且值为绿色而非红色。  必须调用 `UpdateStates` 才能使控件处于 `Negative` 状态。  
  
 [!code-csharp[VSMCustomControl#ApplyTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#applytemplate)]
 [!code-vb[VSMCustomControl#ApplyTemplate](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#applytemplate)]  
  
 当属性更改时，您通常需要更新控件的状态。  下面的示例演示整个 `ValueChangedCallback` 方法。  因为当 `Value` 更改时将调用 `ValueChangedCallback`，所以，当 `Value` 从正更改为负（或相反）时，此方法将调用 `UpdateStates`。  当 `Value` 更改但仍保持为正或负时调用 `UpdateStates` 是可接受的，因为在该情况下，控件将不更改状态。  
  
 [!code-csharp[VSMCustomControl#EntireValueChangedCallback](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#entirevaluechangedcallback)]
 [!code-vb[VSMCustomControl#EntireValueChangedCallback](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#entirevaluechangedcallback)]  
  
 当发生事件时，可能也需要更新状态。  下面的示例演示 `NumericUpDown` 如何对 <xref:System.Windows.Controls.Control> 调用 `UpdateStates` 来处理 <xref:System.Windows.UIElement.GotFocus> 事件。  
  
 [!code-csharp[VSMCustomControl#OnGotFocus](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#ongotfocus)]
 [!code-vb[VSMCustomControl#OnGotFocus](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#ongotfocus)]  
  
 <xref:System.Windows.VisualStateManager> 可帮助您管理控件的状态。  通过使用 <xref:System.Windows.VisualStateManager>，您可以确保控件在各状态之间正确地进行转换。  如果您遵循本节介绍的建议来使用 <xref:System.Windows.VisualStateManager>，则控件的代码将保持可读性和可维护性。  
  
<a name="providing_the_control_contract"></a>   
## 提供控件协定  
 提供控件协定以便 <xref:System.Windows.Controls.ControlTemplate> 作者将了解在模板中放入哪些内容。  控件协定具有三个元素：  
  
-   控件的逻辑使用的可视元素。  
  
-   控件的状态以及每个状态所属的组。  
  
-   以可视方式影响控件的公共属性。  
  
 创建新的 <xref:System.Windows.Controls.ControlTemplate> 的人员需要了解控件的逻辑使用哪些 <xref:System.Windows.FrameworkElement> 对象、每个对象属于什么类型以及各个对象的名称。  <xref:System.Windows.Controls.ControlTemplate> 作者还需要了解控件可能所处的每种可能状态的名称，以及状态属于哪个 <xref:System.Windows.VisualStateGroup>。  
  
 返回到 `NumericUpDown` 示例，控件预期 <xref:System.Windows.Controls.ControlTemplate> 具有以下 <xref:System.Windows.FrameworkElement> 对象：  
  
-   称为 `UpButton` 的 <xref:System.Windows.Controls.Primitives.RepeatButton>。  
  
-   称为 `DownButton.` 的 <xref:System.Windows.Controls.Primitives.RepeatButton>。  
  
 控件可能处于以下状态：  
  
-   在 `ValueStates` <xref:System.Windows.VisualStateGroup> 中  
  
    -   `Positive`  
  
    -   `Negative`  
  
-   在 `FocusStates` <xref:System.Windows.VisualStateGroup> 中  
  
    -   `Focused`  
  
    -   `Unfocused`  
  
 若要指定控件预期的 <xref:System.Windows.FrameworkElement> 对象，可以使用 <xref:System.Windows.TemplatePartAttribute>，它指定预期元素的名称和类型。  若要指定控件的可能状态，可以使用 <xref:System.Windows.TemplateVisualStateAttribute>，它指定状态的名称以及状态所属的 <xref:System.Windows.VisualStateGroup>。  将 <xref:System.Windows.TemplatePartAttribute> 和 <xref:System.Windows.TemplateVisualStateAttribute> 放在控件的类定义中。  
  
 影响控件外观的任何公共属性也是控件协定的一部分。  
  
 下面的示例为 `NumericUpDown` 控件指定 <xref:System.Windows.FrameworkElement> 对象和状态。  
  
 [!code-csharp[VSMCustomControl#ControlContract](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#controlcontract)]
 [!code-vb[VSMCustomControl#ControlContract](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#controlcontract)]  
  
<a name="complete_example"></a>   
## 完整的示例  
 下面的示例为 `NumericUpDown` 控件的整个 <xref:System.Windows.Controls.ControlTemplate>。  
  
 [!code-xml[VSMCustomControl#NUDTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/themes/generic.xaml#nudtemplate)]  
  
 下面的示例演示 `NumericUpDown` 的逻辑。  
  
 [!code-csharp[VSMCustomControl#ControlLogic](../../../../samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#controllogic)]
 [!code-vb[VSMCustomControl#ControlLogic](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#controllogic)]  
  
## 请参阅  
 [通过创建 ControlTemplate 自定义现有控件的外观](../../../../docs/framework/wpf/controls/customizing-the-appearance-of-an-existing-control.md)   
 [控件自定义](../../../../docs/framework/wpf/controls/control-customization.md)