---
title: "命令概述 | Microsoft Docs"
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
  - "类, CommandBinding"
  - "命令库"
  - "CommandBindings"
  - "命令"
  - "CommandManager"
  - "命令, 定义"
  - "ICommandSource 接口"
  - "接口, ICommandSource"
ms.assetid: bc208dfe-367d-426a-99de-52b7e7511e81
caps.latest.revision: 35
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 34
---
# 命令概述
<a name="introduction"></a> 命令是 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中的输入机制，它提供的输入处理比设备输入具有更高的语义级别。  例如，在许多应用程序中都能找到的**“复制”**、**“剪切”**和**“粘贴”**操作就是命令。  
  
 本概述定义哪些命令在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中，哪些类是命令模型的一部分，以及如何在您的应用程序中使用和创建命令。  
  
 本主题包含以下各节：  
  
-   [什么是命令？](#commands_at_10000_feet)  
  
-   [WPF 中的简单命令示例](#simple_command)  
  
-   [WPF 命令中的四个主要概念](#Four_main_Concepts)  
  
-   [命令库](#Command_Library)  
  
-   [创建自定义命令](#creating_commands)  
  
<a name="commands_at_10000_feet"></a>   
## 什么是命令？  
 命令有若干用途。  第一个用途是将语义以及调用命令的对象与执行命令的逻辑分离开来。  这使得多个完全不同的源可以调用相同的命令逻辑，并使得可以针对不同的目标对命令逻辑进行自定义。  例如，在许多应用程序中都能找到的编辑操作**“复制”**、**“剪切”**和**“粘贴”**都可使用不同的用户操作进行调用（如果这些操作是使用命令实现的）。  应用程序可能允许用户通过单击按钮、选择菜单项或使用组合键（例如 Ctrl\+X）剪切所选的对象或文本。  通过使用命令，您可以将各种类型的用户操作绑定到同一逻辑。  
  
 命令的另一个用途是指示操作是否可用。  仍然以剪切对象或文本作为示例，该操作只有在选择了某些内容时才有意义。  如果用户尝试在没有选择任何内容的情况下剪切对象或文本，则不会发生任何操作。  为了向用户指明这一点，许多应用程序都会禁用按钮和菜单项，以使用户了解是否能够执行某项操作。  命令可通过实现 <xref:System.Windows.Input.ICommand.CanExecute%2A> 方法来指出操作是否可以执行。  按钮可以订阅 <xref:System.Windows.Input.ICommand.CanExecuteChanged> 事件，并且，如果 <xref:System.Windows.Input.ICommand.CanExecute%2A> 返回 `false`，则可以禁用按钮，或者，如果 <xref:System.Windows.Input.ICommand.CanExecute%2A> 返回 `true`，则可以启用按钮。  
  
 命令的语义在应用程序和类之间可能是一致的，但是操作的逻辑是所作用于的特定对象所特有的。  Ctrl\+X 组合键在文本类、图像类以及 Web 浏览器中调用**“剪切”**命令，但用于执行**“剪切”**操作的实际逻辑是由执行剪切的应用程序定义的。  <xref:System.Windows.Input.RoutedCommand> 使客户端能够实现逻辑。  文本对象可以将所选文本剪切到剪贴板中，而图像对象则可以剪切所选图像。  当应用程序处理 <xref:System.Windows.Input.CommandManager.Executed> 事件时，它将能访问命令的目标，并根据目标的类型采取相应的操作。  
  
<a name="simple_command"></a>   
## WPF 中的简单命令示例  
 在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中使用命令的最简单方法是从某个命令库类中使用预定义的 <xref:System.Windows.Input.RoutedCommand>；使用对处理此命令具有固有支持的控件；以及使用对调用命令具有固有支持的控件。  <xref:System.Windows.Input.ApplicationCommands.Paste%2A> 命令是 <xref:System.Windows.Input.ApplicationCommands> 类中的预定义命令之一。  <xref:System.Windows.Controls.TextBox> 控件具有处理 <xref:System.Windows.Input.ApplicationCommands.Paste%2A> 命令的内置逻辑。  <xref:System.Windows.Controls.MenuItem> 类具有对调用命令的固有支持。  
  
 下面的示例演示如何设置 <xref:System.Windows.Controls.MenuItem>，以便单击该菜单项时，将对 <xref:System.Windows.Controls.TextBox> 调用 <xref:System.Windows.Input.ApplicationCommands.Paste%2A> 命令（假定该 <xref:System.Windows.Controls.TextBox> 具有键盘焦点）。  
  
 [!code-xml[CommandingOverviewSnippets#CommandingOverviewSimpleCommand](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml#commandingoverviewsimplecommand)]  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewCommandTargetCodeBehind](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewcommandtargetcodebehind)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewCommandTargetCodeBehind](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewcommandtargetcodebehind)]  
  
<a name="Four_main_Concepts"></a>   
## WPF 命令中的四个主要概念  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的路由命令模型可以分为四个主要概念：命令、命令源、命令目标以及命令绑定：  
  
-   命令是要执行的操作。  
  
-   命令源是调用命令的对象。  
  
-   命令目标是在其上执行命令的对象。  
  
-   命令绑定是将命令逻辑映射到命令的对象。  
  
 在前面的示例中，<xref:System.Windows.Input.ApplicationCommands.Paste%2A> 命令是命令，<xref:System.Windows.Controls.MenuItem> 是命令源，<xref:System.Windows.Controls.TextBox> 是命令目标，命令绑定由 <xref:System.Windows.Controls.TextBox> 控件提供。  值得注意的是，<xref:System.Windows.Input.CommandBinding> 并不总是由充当命令目标类的控件提供。  非常常见的情况是，<xref:System.Windows.Input.CommandBinding> 必须由应用程序开发人员创建，或者 <xref:System.Windows.Input.CommandBinding> 可能附加到命令目标的上级。  
  
<a name="Commands"></a>   
### 命令  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的命令是通过实现 <xref:System.Windows.Input.ICommand> 接口创建的。  <xref:System.Windows.Input.ICommand> 公开两个方法（<xref:System.Windows.Input.ICommand.Execute%2A> 及 <xref:System.Windows.Input.ICommand.CanExecute%2A>）和一个事件（<xref:System.Windows.Input.ICommand.CanExecuteChanged>）。  <xref:System.Windows.Input.ICommand.Execute%2A> 执行与命令关联的操作。<xref:System.Windows.Input.ICommand.CanExecute%2A> 确定是否可以在当前命令目标上执行命令。  如果集中管理命令操作的命令管理器检测到命令源中发生了更改，此更改可能使得已引发但尚未由命令绑定执行的命令无效，则将引发 <xref:System.Windows.Input.ICommand.CanExecuteChanged>。  <xref:System.Windows.Input.ICommand> 的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 实现是 <xref:System.Windows.Input.RoutedCommand> 类，这是本概述的重点。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的主要输入源是鼠标、键盘、墨迹和路由命令。  更加面向设备的输入使用 <xref:System.Windows.RoutedEvent> 来通知应用程序页中的对象已发生了输入事件。  <xref:System.Windows.Input.RoutedCommand> 没有不同。  <xref:System.Windows.Input.RoutedCommand> 的 <xref:System.Windows.Input.RoutedCommand.Execute%2A> 和 <xref:System.Windows.Input.RoutedCommand.CanExecute%2A> 方法不包含命令的应用程序逻辑，而是引发这样的路由事件：沿元素树以隧道和冒泡形式传递，直到遇到具有 <xref:System.Windows.Input.CommandBinding> 的对象。  <xref:System.Windows.Input.CommandBinding> 包含这些事件的处理程序，执行此命令的就是这些处理程序。  有关 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的事件路由的更多信息，请参见[路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)。  
  
 <xref:System.Windows.Input.RoutedCommand> 上的 <xref:System.Windows.Input.RoutedCommand.Execute%2A> 方法在命令目标上引发 <xref:System.Windows.Input.CommandManager.PreviewExecuted> 和 <xref:System.Windows.Input.CommandManager.Executed> 事件。  <xref:System.Windows.Input.RoutedCommand> 上的 <xref:System.Windows.Input.RoutedCommand.CanExecute%2A> 方法在命令目标上引发 <xref:System.Windows.Input.CommandManager.CanExecute> 和 <xref:System.Windows.Input.CommandManager.PreviewCanExecute> 事件。  这些事件沿元素树以隧道和冒泡形式传递，直到遇到具有该特定命令的 <xref:System.Windows.Input.CommandBinding> 的对象。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供了一组常用的路由命令，这组命令分布在几个类中：<xref:System.Windows.Input.MediaCommands>、<xref:System.Windows.Input.ApplicationCommands>、<xref:System.Windows.Input.NavigationCommands>、<xref:System.Windows.Input.ComponentCommands> 和 <xref:System.Windows.Documents.EditingCommands>。  这些类仅包含 <xref:System.Windows.Input.RoutedCommand> 对象，而不包含命令的实现逻辑。  实现逻辑由在其上执行命令的对象负责。  
  
<a name="Command_Sources"></a>   
### 命令源  
 命令源是调用命令的对象。  例如，<xref:System.Windows.Controls.MenuItem>、<xref:System.Windows.Controls.Button> 和 <xref:System.Windows.Input.KeyGesture> 就是命令源。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中的命令源通常实现 <xref:System.Windows.Input.ICommandSource> 接口。  
  
 <xref:System.Windows.Input.ICommandSource> 公开三个属性：<xref:System.Windows.Input.ICommandSource.Command%2A>、<xref:System.Windows.Input.ICommandSource.CommandTarget%2A> 和 <xref:System.Windows.Input.ICommandSource.CommandParameter%2A>：  
  
-   <xref:System.Windows.Input.ICommandSource.Command%2A> 是在调用命令源时执行的命令。  
  
-   <xref:System.Windows.Input.ICommandSource.CommandTarget%2A> 是要在其上执行命令的对象。  值得注意的是，在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中，<xref:System.Windows.Input.ICommandSource> 上的 <xref:System.Windows.Input.ICommandSource.CommandTarget%2A> 属性只有在 <xref:System.Windows.Input.ICommand> 是 <xref:System.Windows.Input.RoutedCommand> 时才适用。  如果在 <xref:System.Windows.Input.ICommandSource> 上设置了 <xref:System.Windows.Input.ICommandSource.CommandTarget%2A>，而对应的命令不是 <xref:System.Windows.Input.RoutedCommand>，将会忽略命令目标。  如果未设置 <xref:System.Windows.Input.ICommandSource.CommandTarget%2A>，则具有键盘焦点的元素将是命令目标。  
  
-   <xref:System.Windows.Input.ICommandSource.CommandParameter%2A> 是用户定义的数据类型，用于将信息传递到实现命令的处理程序。  
  
 实现 <xref:System.Windows.Input.ICommandSource> 的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 类包括：<xref:System.Windows.Controls.Primitives.ButtonBase>、<xref:System.Windows.Controls.MenuItem>、<xref:System.Windows.Documents.Hyperlink> 以及 <xref:System.Windows.Input.InputBinding>。  <xref:System.Windows.Controls.Primitives.ButtonBase>、<xref:System.Windows.Controls.MenuItem> 和 <xref:System.Windows.Documents.Hyperlink> 在被单击时调用命令，<xref:System.Windows.Input.InputBinding> 在与之关联的 <xref:System.Windows.Input.InputGesture> 执行时调用命令。  
  
 下面的示例演示如何将 <xref:System.Windows.Controls.ContextMenu> 中的 <xref:System.Windows.Controls.MenuItem> 用作 <xref:System.Windows.Input.ApplicationCommands.Properties%2A> 命令的命令源。  
  
 [!code-xml[CommandingOverviewSnippets#CommandingOverviewCmdSourceXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml#commandingoverviewcmdsourcexaml)]  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewCmdSource](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewcmdsource)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewCmdSource](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewcmdsource)]  
  
 通常，命令源会侦听 <xref:System.Windows.Input.RoutedCommand.CanExecuteChanged> 事件。  此事件通知命令源，在当前命令目标上执行命令的能力可能已更改。  命令源可以通过使用 <xref:System.Windows.Input.RoutedCommand.CanExecute%2A> 方法来查询 <xref:System.Windows.Input.RoutedCommand> 的当前状态。  之后，如果命令无法执行，则命令源可以禁用其自身。  这种情况的一个示例是：当无法执行命令时，<xref:System.Windows.Controls.MenuItem> 会将自己显示为灰色。  
  
 可以将 <xref:System.Windows.Input.InputGesture> 用作命令源。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中两种类型的输入笔势是 <xref:System.Windows.Input.KeyGesture> 和 <xref:System.Windows.Input.MouseGesture>。  可以将 <xref:System.Windows.Input.KeyGesture> 视为键盘快捷方式，如 Ctrl\+C。  <xref:System.Windows.Input.KeyGesture> 由一个 <xref:System.Windows.Input.Key> 和一组 <xref:System.Windows.Input.ModifierKeys> 组成。  <xref:System.Windows.Input.MouseGesture> 由一个 <xref:System.Windows.Input.MouseAction> 和一组可选的 <xref:System.Windows.Input.ModifierKeys> 组成。  
  
 为了使 <xref:System.Windows.Input.InputGesture> 充当命令源，必须将它与一个命令关联。  有几种方法可实现此目的。  一种方法是使用 <xref:System.Windows.Input.InputBinding>。  
  
 下面的示例演示如何在 <xref:System.Windows.Input.KeyGesture> 与 <xref:System.Windows.Input.RoutedCommand> 之间创建一个 <xref:System.Windows.Input.KeyBinding>。  
  
 [!code-xml[CommandingOverviewSnippets#CommandingOverviewXAMLKeyBinding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml#commandingoverviewxamlkeybinding)]  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewKeyBinding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewkeybinding)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewKeyBinding](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewkeybinding)]  
  
 将 <xref:System.Windows.Input.InputGesture> 与 <xref:System.Windows.Input.RoutedCommand> 关联的另一种方法是将 <xref:System.Windows.Input.InputGesture> 添加到 <xref:System.Windows.Input.RoutedCommand> 的 <xref:System.Windows.Input.InputGestureCollection>。  
  
 下面的示例演示如何将一个 <xref:System.Windows.Input.KeyGesture> 添加到 <xref:System.Windows.Input.RoutedCommand> 的 <xref:System.Windows.Input.InputGestureCollection>。  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewKeyGestureOnCmd](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewkeygestureoncmd)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewKeyGestureOnCmd](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewkeygestureoncmd)]  
  
<a name="Command_Binding"></a>   
### CommandBinding  
 <xref:System.Windows.Input.CommandBinding> 将一个命令与实现该命令的事件处理程序关联。  
  
 <xref:System.Windows.Input.CommandBinding> 类包含一个 <xref:System.Windows.Input.CommandBinding.Command%2A> 属性以及 <xref:System.Windows.Input.CommandBinding.PreviewExecuted>、<xref:System.Windows.Input.CommandBinding.Executed>、<xref:System.Windows.Input.CommandBinding.PreviewCanExecute> 和 <xref:System.Windows.Input.CommandBinding.CanExecute> 事件。  
  
 <xref:System.Windows.Input.CommandBinding.Command%2A> 是 <xref:System.Windows.Input.CommandBinding> 要与之关联的命令。  附加到 <xref:System.Windows.Input.CommandBinding.PreviewExecuted> 和 <xref:System.Windows.Input.CommandBinding.Executed> 事件的事件处理程序实现命令逻辑。  附加到 <xref:System.Windows.Input.CommandBinding.PreviewCanExecute> 和 <xref:System.Windows.Input.CommandBinding.CanExecute> 事件的事件处理程序确定命令是否可以在当前命令目标上执行。  
  
 下面的示例演示如何在应用程序的根 <xref:System.Windows.Window> 上创建一个 <xref:System.Windows.Input.CommandBinding>。  <xref:System.Windows.Input.CommandBinding> 将 <xref:System.Windows.Input.ApplicationCommands.Open%2A> 命令与 <xref:System.Windows.Input.CommandManager.Executed> 和 <xref:System.Windows.Input.CommandBinding.CanExecute> 处理程序关联。  
  
 [!code-xml[commandwithhandler#CommandHandlerCommandBinding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/commandWithHandler/CSharp/Window1.xaml#commandhandlercommandbinding)]  
  
 [!code-csharp[CommandHandlerProcedural#CommandHandlerBindingInit](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandHandlerProcedural/CSharp/Window1.xaml.cs#commandhandlerbindinginit)]
 [!code-vb[CommandHandlerProcedural#CommandHandlerBindingInit](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandHandlerProcedural/visualbasic/window1.xaml.vb#commandhandlerbindinginit)]  
  
 接下来，创建 <xref:System.Windows.Input.ExecutedRoutedEventHandler> 和 <xref:System.Windows.Input.CanExecuteRoutedEventHandler>。  <xref:System.Windows.Input.ExecutedRoutedEventHandler> 打开一个 <xref:System.Windows.MessageBox>，此消息框显示一个字符串，指出命令已执行。  <xref:System.Windows.Input.CanExecuteRoutedEventHandler> 将 <xref:System.Windows.Input.CanExecuteRoutedEventArgs.CanExecute%2A> 属性设置为 `true`。  
  
 [!code-csharp[commandwithhandler#CommandHandlerExecutedHandler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/commandWithHandler/CSharp/Window1.xaml.cs#commandhandlerexecutedhandler)]
 [!code-vb[commandwithhandler#CommandHandlerExecutedHandler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/commandWithHandler/VisualBasic/Window1.xaml.vb#commandhandlerexecutedhandler)]  
  
 [!code-csharp[commandwithhandler#CommandHandlerCanExecuteHandler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/commandWithHandler/CSharp/Window1.xaml.cs#commandhandlercanexecutehandler)]
 [!code-vb[commandwithhandler#CommandHandlerCanExecuteHandler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/commandWithHandler/VisualBasic/Window1.xaml.vb#commandhandlercanexecutehandler)]  
  
 <xref:System.Windows.Input.CommandBinding> 附加到一个特定的对象，如应用程序的根 <xref:System.Windows.Window> 或控件。  <xref:System.Windows.Input.CommandBinding> 所附加到的对象定义绑定的范围。  例如，可以通过 <xref:System.Windows.Input.CommandBinding.Executed> 事件来到达附加到命令目标上级的 <xref:System.Windows.Input.CommandBinding>，但无法到达附加到命令目标后代的 <xref:System.Windows.Input.CommandBinding>。  这是从引发事件的对象以隧道和冒泡方式传递 <xref:System.Windows.RoutedEvent> 的直接后果。  
  
 在某些情形下，<xref:System.Windows.Input.CommandBinding> 附加到命令目标本身，例如，对于 <xref:System.Windows.Controls.TextBox> 类以及 <xref:System.Windows.Input.ApplicationCommands.Cut%2A>、<xref:System.Windows.Input.ApplicationCommands.Copy%2A> 和 <xref:System.Windows.Input.ApplicationCommands.Paste%2A> 命令就是如此。  但是，更常见的情况是，将 <xref:System.Windows.Input.CommandBinding> 附加到命令目标上级（例如，主 <xref:System.Windows.Window> 或 Application 对象）更方便，尤其当同一个 <xref:System.Windows.Input.CommandBinding> 可以用于多个命令目标时，这种优势更为明显。  这些是您在创建命令基础结构时要考虑的设计决策。  
  
<a name="Commane_Target"></a>   
### 命令目标  
 命令目标是在其上执行命令的元素。  对于 <xref:System.Windows.Input.RoutedCommand> 而言，命令目标是 <xref:System.Windows.Input.CommandManager.Executed> 和 <xref:System.Windows.Input.CommandManager.CanExecute> 的路由的起始元素。  前面已提到，在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中，<xref:System.Windows.Input.ICommandSource> 上的 <xref:System.Windows.Input.ICommandSource.CommandTarget%2A> 属性只有在 <xref:System.Windows.Input.ICommand> 是一个 <xref:System.Windows.Input.RoutedCommand> 时才适用。  如果在 <xref:System.Windows.Input.ICommandSource> 上设置了 <xref:System.Windows.Input.ICommandSource.CommandTarget%2A>，而对应的命令不是 <xref:System.Windows.Input.RoutedCommand>，将会忽略命令目标。  
  
 命令源可以显式设置命令目标。  如果未定义命令目标，则具有键盘焦点的元素将用作命令目标。  将具有键盘焦点的元素用作命令目标的一个好处是，应用程序开发人员可以使用同一个命令源在多个目标上调用命令，而不必跟踪命令目标。  例如，如果 <xref:System.Windows.Controls.MenuItem> 在具有一个 <xref:System.Windows.Controls.TextBox> 控件和一个 <xref:System.Windows.Controls.PasswordBox> 控件的应用程序中调用**“粘贴”**命令，则目标既可以是 <xref:System.Windows.Controls.TextBox>，也可以是 <xref:System.Windows.Controls.PasswordBox>，具体取决于哪个控件具有键盘焦点。  
  
 下面的示例演示如何显式地在标记和代码隐藏中设置命令目标。  
  
 [!code-xml[CommandingOverviewSnippets#CommandingOverviewXAMLCommandTarget](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml#commandingoverviewxamlcommandtarget)]  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewCommandTargetCodeBehind](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewcommandtargetcodebehind)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewCommandTargetCodeBehind](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewcommandtargetcodebehind)]  
  
<a name="Command_Manager"></a>   
### CommandManager  
 <xref:System.Windows.Input.CommandManager> 提供许多命令相关函数。  它提供一组用于向\/从特定元素中添加\/移除 <xref:System.Windows.Input.CommandManager.PreviewExecuted>、<xref:System.Windows.Input.CommandManager.Executed>、<xref:System.Windows.Input.CommandManager.PreviewCanExecute> 和 <xref:System.Windows.Input.CommandManager.CanExecute> 事件处理程序的静态方法。  它提供一种将 <xref:System.Windows.Input.CommandBinding> 和 <xref:System.Windows.Input.InputBinding> 对象注册到特定类的方式。  <xref:System.Windows.Input.CommandManager> 还通过 <xref:System.Windows.Input.CommandManager.RequerySuggested> 事件提供一种通知命令应在何时引发 <xref:System.Windows.Input.ICommand.CanExecuteChanged> 事件的方式。  
  
 <xref:System.Windows.Input.CommandManager.InvalidateRequerySuggested%2A> 方法强制 <xref:System.Windows.Input.CommandManager> 引发 <xref:System.Windows.Input.CommandManager.RequerySuggested> 事件。  这对于应禁用\/启用命令、但不被 <xref:System.Windows.Input.CommandManager> 识别的条件很有用。  
  
<a name="Command_Library"></a>   
## 命令库  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供一组预定义命令。  命令库包含以下类：<xref:System.Windows.Input.ApplicationCommands>、<xref:System.Windows.Input.NavigationCommands>、<xref:System.Windows.Input.MediaCommands>、<xref:System.Windows.Documents.EditingCommands> 以及 <xref:System.Windows.Input.ComponentCommands>。  这些类提供诸如 <xref:System.Windows.Input.ApplicationCommands.Cut%2A>、<xref:System.Windows.Input.NavigationCommands.BrowseBack%2A>、<xref:System.Windows.Input.NavigationCommands.BrowseForward%2A>、<xref:System.Windows.Input.MediaCommands.Play%2A>、<xref:System.Windows.Input.MediaCommands.Stop%2A> 和 <xref:System.Windows.Input.MediaCommands.Pause%2A> 等命令。  
  
 其中的许多命令都包括一组默认输入绑定。  例如，如果您指定应用程序处理复制命令，则会自动获得键盘绑定“Ctrl\+C”。您还会获得其他输入设备（如 [!INCLUDE[TLA2#tla_tpc](../../../../includes/tla2sharptla-tpc-md.md)] 钢笔笔势和语音信息）的绑定。  
  
 当您使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 引用不同的命令库中的命令时，通常可以忽略公开静态命令属性的库类的类名。  通常，命令名称作为字符串是明确的，并且存在用于提供命令的逻辑分组的所属类型，但是这些类型对于消除歧义并不是必需的。  例如，您可以指定 `Command="Cut"`，而不必指定更详细的 `Command="ApplicationCommands.Cut"`。  这是一种内置于命令的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器中的便利机制（更准确地说，它是 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 处理器在加载时引用的 <xref:System.Windows.Input.ICommand> 的类型转换器行为）。  
  
<a name="creating_commands"></a>   
## 创建自定义命令  
 如果命令库类中的命令不满足您的需要，则您可以创建自己的命令。  有两种方法可创建自定义命令。  第一种是从头开始，并实现 <xref:System.Windows.Input.ICommand> 接口。  另一种方法，也是更常用的方法，是创建 <xref:System.Windows.Input.RoutedCommand> 或 <xref:System.Windows.Input.RoutedUICommand>。  
  
 有关创建自定义 <xref:System.Windows.Input.RoutedCommand> 的示例，请参见 [Create a Custom RoutedCommand Sample](http://go.microsoft.com/fwlink/?LinkID=159980)（创建自定义 RoutedCommand 示例）。  
  
## 请参阅  
 <xref:System.Windows.Input.RoutedCommand>   
 <xref:System.Windows.Input.CommandBinding>   
 <xref:System.Windows.Input.InputBinding>   
 <xref:System.Windows.Input.CommandManager>   
 [输入概述](../../../../docs/framework/wpf/advanced/input-overview.md)   
 [路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)   
 [实现 ICommandSource](../../../../docs/framework/wpf/advanced/how-to-implement-icommandsource.md)   
 [How to: Add a Command to a MenuItem](http://msdn.microsoft.com/zh-cn/013d68a0-5373-4a68-bd91-5de574307370)   
 [Create a Custom RoutedCommand Sample](http://go.microsoft.com/fwlink/?LinkID=159980)