---
title: "WPF 体系结构 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "关联线程"
  - "体系结构"
  - "附加属性"
  - "类, System.Object"
  - "类, System.Threading.DispatcherObject"
  - "类, System.Windows.Controls.Control"
  - "类, System.Windows.DependencyObject"
  - "类, System.Windows.FrameworkElement"
  - "类, System.Windows.Media.Visual"
  - "类, System.Windows.UIElement"
  - "CommandBindings"
  - "组件, unmanaged"
  - "Control 类"
  - "数据模板"
  - "DependencyObject 类"
  - "DispatcherObject 类"
  - "FrameworkElement 类"
  - "INotifyPropertyChange 接口"
  - "接口, INotifyPropertyChange"
  - "milcore"
  - "绘画器的算法"
  - "属性, 附加的"
  - "情节提要"
  - "System.Object 类"
  - "System.Threading.DispatcherObject 类"
  - "System.Windows.Controls.Control 类"
  - "System.Windows.DependencyObject 类"
  - "System.Windows.FrameworkElement 类"
  - "System.Windows.Media.Visual 类"
  - "System.Windows.UIElement 类"
  - "thread, 关联"
  - "UIElement 类"
  - "非托管组件"
  - "Visual 类"
ms.assetid: 8579c10b-76ab-4c52-9691-195ce02333c8
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# WPF 体系结构
本主题提供 [!INCLUDE[TLA#tla_wpf](../../../../includes/tlasharptla-wpf-md.md)] 类层次结构的指导教程，  涵盖了 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的大部分主要子系统，并描述它们是如何交互的。  本主题还详细介绍了 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 架构师所做的一些选择。  
  
   
  
<a name="System_Object"></a>   
## System.Object  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 主要编程模型是通过托管代码公开的。  在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的早期设计阶段，曾有过大量关于如何界定系统的托管组件和非托管组件的争论。  [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 提供一系列的功能，可以令开发效率更高并且更加可靠（包括内存管理、错误处理和常规类型系统等），但这是需要付出代价的。  
  
 下图说明了 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的主要组件。  关系图的红色部分（PresentationFramework、PresentationCore 和 milcore）是 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的主要代码部分。  在这些组件中，只有一个是非托管组件 – milcore。  milcore 是以非托管代码编写的，目的是实现与 [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)] 的紧密集成。  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中的所有显示都是通过 [!INCLUDE[TLA2#tla_dx](../../../../includes/tla2sharptla-dx-md.md)] 引擎完成的，因此硬件和软件呈现都很高效。  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 还要求对内存和执行进行精细控制。  milcore 中的组合引擎受性能影响关系大，需要放弃 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 的许多优点来提高性能。  
  
 ![WPF 在 .NET Framework 中的位置。](../../../../docs/framework/wpf/advanced/media/wpf-architect1.png "wpf\_architect1")  
  
 本主题的后面部分将讨论 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的托管和非托管部分之间的通信。  下面介绍托管编程模型的其余部分。  
  
<a name="System_Threading_DispatcherObject"></a>   
## System.Threading.DispatcherObject  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中的大多数对象是从 <xref:System.Windows.Threading.DispatcherObject> 派生的，这提供了用于处理并发和线程的基本构造。  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 基于调度程序实现的消息系统。  其工作方式与常见的 [!INCLUDE[TLA#tla_win32](../../../../includes/tlasharptla-win32-md.md)] 消息泵非常类似；事实上，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 调度程序使用 User32 消息执行跨线程调用。  
  
 要讨论 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中的并发，首先必须真正理解两个核心概念 – 调度程序和线程关联。  
  
 在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的设计阶段，目标趋向于单一线程的执行，但这不是一种与线程“关联的”模型。  当一个组件使用执行线程的标识来存储某种类型的状态时，将发生线程关联。  最常见的形式是使用线程本地存储 \(TLS\) 来存储状态。  线程关联要求执行的每个逻辑线程仅由操作系统中的一个物理线程所拥有，这将占用大量内存。  最后，WPF 的线程处理模型保持与具有线程关联的单一线程执行的现有 User32 线程处理模型同步。  主要原因是互操作性 – 类似于 [!INCLUDE[TLA2#tla_ole2.0](../../../../includes/tla2sharptla-ole2-0-md.md)] 的系统、剪贴板和 Internet Explorer 均需要单一线程关联 \(STA\) 执行。  
  
 假设您具有带有 STA 线程的对象，则需要一种方式来在线程之间通信，并验证您是否位于正确的线程上。  调度程序的作用就在于此。  调度程序是一个基本的消息调度系统，具有多个按优先级排列的队列。  消息的示例包括原始输入通知（鼠标移动）、框架函数（布局）或用户命令（执行此方法）。  通过从 <xref:System.Windows.Threading.DispatcherObject> 派生，您可以创建一个具有 STA 行为的 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 对象，并在创建时获得一个指向调度程序的指针。  
  
<a name="System_Windows_DependencyObject"></a>   
## System.Windows.DependencyObject  
 生成 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 时使用的主要体系结构原理之一是首选属性而不是方法或事件。  属性是声明性的，使您更方便地指定意图而不是操作。  它还支持模型驱动或数据驱动的系统，以显示用户界面内容。  这种理念的预期效果是创建您可以绑定到的更多属性，从而更好地控制应用程序的行为。  
  
 为了更加充分地利用由属性驱动的系统，需要一个比 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 提供的内容更丰富的属性系统。  此丰富性的一个简单示例就是更改通知。  为了实现双向绑定，您需要绑定的双方支持更改通知。  为了使行为与属性值相关联，您需要在属性值更改时得到通知。  [!INCLUDE[TLA#tla_netframewk](../../../../includes/tlasharptla-netframewk-md.md)] 具有一个 **INotifyPropertyChange** 接口，对象通过该接口可以发布更改通知，但该接口是可选的。  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 提供一个丰富的属性系统，该属性系统是从 <xref:System.Windows.DependencyObject> 类型派生的。  该属性系统实际是一个“依赖”属性系统，因为它会跟踪属性表达式之间的依赖关系，并在依赖关系更改时自动重新验证属性值。  例如，如果您具有一个会继承的属性（如 <xref:System.Windows.Controls.Control.FontSize%2A>），当继承该值的元素的父级发生属性更改时，会自动更新系统。  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 属性系统的基础是属性表达式的概念。  在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的第一版中，属性表达式系统是关闭的，表达式都是作为框架的一部分提供的。  表达式致使属性系统不具有硬编码的数据绑定、样式调整或继承，而是由框架内后面的层来提供这些功能。  
  
 属性系统还提供属性值的稀疏存储。  因为对象可以有数十个（如果达不到上百个）属性，并且大部分值处于其默认状态（被继承、由样式设置等），所以并非对象的每个实例都需要具有在该对象上定义的每个属性的完全权重。  
  
 属性系统的最后一个新功能是[附加属性](GTMT)的概念。  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 元素是基于组合和组件重用的原则生成的。  某些包含元素（如 <xref:System.Windows.Controls.Grid> 布局元素）通常需要子元素上的其他数据才能控制其行为（如行\/列信息）。  任何对象都可以为任何其他对象提供属性定义，而不是要将所有这些属性与每个元素相关联。  这与 JavaScript 中的“expando”功能相似。  
  
<a name="System_Windows_Media_Visual"></a>   
## System.Windows.Media.Visual  
 定义一个系统后，下一步是将像素绘制到屏幕上。  <xref:System.Windows.Media.Visual> 类用于生成可视化对象的树，每个对象可以选择性地包含绘制指令以及有关如何呈现这些指令（剪辑、变换等）的元数据。  <xref:System.Windows.Media.Visual> 旨在极致轻量且灵活，因此大部分功能均未公开 [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)]，并且非常依赖受保护的回调函数。  
  
 <xref:System.Windows.Media.Visual> 实际上是 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 组合系统的入口点。  <xref:System.Windows.Media.Visual> 是托管 [!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)] 和非托管 milcore 这两个子系统之间的连接点。  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 通过遍历由 milcore 管理的非托管数据结构来显示数据。  这些结构（称为组合节点）代表层次结构显示树，其中每个节点都有呈现指令。  只能通过消息传递协议来访问此树（下图右侧所示）。  
  
 当对 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 编程时，您将创建 <xref:System.Windows.Media.Visual> 元素及派生的类型，它们通过此消息传递协议在内部与此组合树进行通信。  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中的每个 <xref:System.Windows.Media.Visual> 可以不创建组合节点，也可以创建一个或多个组合节点。  
  
 ![Windows Presentation Foundation 可视化树。](../../../../docs/framework/wpf/advanced/media/wpf-architecture2.png "wpf\_architecture2")  
  
 请注意一个非常重要的体系结构细节 – 可视对象和绘制指令的整个树都要进行缓存。  在图形方面，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 使用一个保留的呈现系统。  这可以使系统以一个高刷新率重绘系统，并且不会发生组合系统阻止对用户代码的回调。  这有助于防止出现应用程序无响应的情况。  
  
 关系图中不十分引人注意的另一个重要细节是系统实际上如何执行组合。  
  
 在 User32 和 [!INCLUDE[TLA2#tla_gdi](../../../../includes/tla2sharptla-gdi-md.md)] 中，系统是在一个即时模式剪辑系统上工作。  当需要呈现一个组件时，系统会建立一个剪辑边界，不允许组件接触该边界之外的像素，然后会要求此组件在该框中绘制像素。  此系统在内存受限的系统上工作良好，因为当某些内容更改时，只需要处理受影响的组件即可 – 不会有两个组件对一个像素的颜色更改起作用。  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 使用“绘画器的算法”绘制模型。  这意味着并不是剪辑每个组件，而是要求从显示内容的背面至正面来呈现每个组件。  这允许每个组件在先前的组件的显示内容上绘制。  此模型的优点是您可以生成部分透明的复杂形状。  配合当今的新式图形硬件，此模型相对较快（创建 User32\/[!INCLUDE[TLA2#tla_gdi](../../../../includes/tla2sharptla-gdi-md.md)] 时则不然）。  
  
 如上面所述，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的一个核心原理是转移到一个更具声明性且“以属性为中心”的编程模型。  在可视化系统中，这会表现为需要关注的两种情况。  
  
 首先，如果您考虑保留的模式图形系统，则实际上是从命令性 DrawLine\/DrawLine 类型模型移动到面向数据的模型 new Line\(\)\/new Line\(\)。  通过这一向数据驱动的呈现移动，可以在使用属性表达的绘制指令上进行复杂的操作。  从 <xref:System.Windows.Media.Drawing> 派生的类型实际上是用于呈现的对象模型。  
  
 第二，如果评估动画系统，您将看到它几乎是完全声明性的。  无需要求开发人员计算下一位置或下一颜色，您可以将动画表示为动画对象上的一组属性。  于是，这些动画可以表示开发人员或设计人员的意图（在 5 秒内将此按钮从一个位置移动到另一个位置），系统就可以确定完成此任务的最有效方式。  
  
<a name="System_Windows_UIElement"></a>   
## System.Windows.UIElement  
 <xref:System.Windows.UIElement> 定义核心子系统，包括 Layout、Input 和 Event。  
  
 Layout 是 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中的一个核心概念。  在许多系统中，可能有一组固定的布局模型（HTML 支持三种布局模型：流、绝对和表），也可能没有布局模型（User32 实际仅支持绝对定位）。  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 先假设开发人员和设计人员希望有一个灵活的可扩展布局模型，该模型可能是由属性值而不是命令性逻辑驱动的。  在 <xref:System.Windows.UIElement> 级别，会引入布局的基本协定 \- 具有 <xref:System.Windows.UIElement.Measure%2A> 和 <xref:System.Windows.UIElement.Arrange%2A> 处理过程的两阶段模型。  
  
 <xref:System.Windows.UIElement.Measure%2A> 允许组件确定它要采用的大小。  此阶段独立于 <xref:System.Windows.UIElement.Arrange%2A>，因为在许多情形下，父元素会要求子元素测量若干次以确定其最佳位置和大小。  父元素要求子元素测量这一事实体现了 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的另一关键原则 – 内容大小。  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中的所有控件支持调整到内容原始大小的功能。  这使本地化更加容易，并允许在调整大小时对元素进行动态布局。  <xref:System.Windows.UIElement.Arrange%2A> 阶段允许父元素定位并确定每个子元素的最终大小。  
  
 通常会花费大量的时间来讨论 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的输出端（<xref:System.Windows.Media.Visual> 及其相关对象）。  然而，在输入端也有许多创新。  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 输入模型的最基本更改也许是一致模型，输入事件通过系统借助此模型进行路由。  
  
 输入是作为内核模式设备驱动程序上的信号发出的，并通过涉及 Windows 内核和 User32 的复杂进程路由到正确的进程和线程。  与输入相对应的 User32 消息路由到 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 后，就会转换为 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 原始输入消息，并发送到调度程序。  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 允许将原始输入事件转换为多个实际事件，允许在保证传递到位的情况下在较低的系统级别实现类似“MouseEnter”的功能。  
  
 每个输入事件至少会转换为两个事件 – “预览”事件和实际事件。  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中的所有事件都具有通过元素树路由的概念。  如果事件从目标向上遍历树直到根，则被称为“冒泡”，如果从根开始向下遍历到目标，它们被称为“隧道”。  输入预览事件隧道，使树中的任何元素都有机会筛选事件或对事件采取操作。  然后，常规（非预览）事件将从目标向上冒泡到根。  
  
 分割隧道和冒泡阶段使快捷键等功能在复合世界中表现一致。  在 User32 中，您可以通过使用一个全局表来实现快捷键，该表中包含您希望支持的所有快捷键（Ctrl\+N 映射为“新建”）。  在应用程序的调度程序中，您可以调用 **TranslateAccelerator**，它会探查 User32 中的输入消息，并确定是否有任何消息与已注册的快捷键匹配。  在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中，上述内容不会起作用，因为系统是完全“可组合”的 – 任何元素都可以处理和使用任何快捷键。  将这个两阶段模型用于输入，将允许组件实现其自己的 "TranslateAccelerator"。  
  
 为了进一步深化此功能，<xref:System.Windows.UIElement> 还引入了 CommandBindings 的概念。  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 命令系统允许开发人员以命令终结点（一种用于实现 <xref:System.Windows.Input.ICommand> 的功能）的方式定义功能。  命令绑定使元素可以定义输入笔势 \(Ctrl\+N\) 和命令（“新建”）之间的映射。  输入笔势和命令定义都是可扩展的，并且可以在使用时联系到一起。  这使得一些操作（例如，允许最终用户自定义其要在应用程序内使用的键绑定）显得无关紧要。  
  
 至此，本主题已重点讨论了 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的“核心”功能 \- PresentationCore 程序集中实现的功能。  当生成 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 时，基础部分（例如带有 **Measure** 和 **Arrange** 的布局的协定）和框架部分（例如 <xref:System.Windows.Controls.Grid> 的特定布局的实现）之间的明确划分是希望的结果。  目标就是提供在堆栈中处于较低位置的可扩展性点，这将允许外部开发人员可以在需要时创建自己的框架。  
  
<a name="System_Windows_FrameworkElement"></a>   
## System.Windows.FrameworkElement  
 可以按两种不同的方式来看待 <xref:System.Windows.FrameworkElement>。  它对在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的较低层中的子系统引入一组策略和自定义项。  它还引入了一组新的子系统。  
  
 <xref:System.Windows.FrameworkElement> 引入的主要策略是关于应用程序布局。  <xref:System.Windows.FrameworkElement> 基于 <xref:System.Windows.UIElement> 引入的基本布局构建而成，并增加了布局“插槽”的概念，使布局创作者可以更方便地拥有一组一致、属性驱动的布局语义。  <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A>、<xref:System.Windows.FrameworkElement.VerticalAlignment%2A>、<xref:System.Windows.FrameworkElement.MinWidth%2A> 和 <xref:System.Windows.FrameworkElement.Margin%2A> 等属性使得从 <xref:System.Windows.FrameworkElement> 派生的所有组件在布局容器内具有一致的行为。  
  
 利用 <xref:System.Windows.FrameworkElement>，[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的核心层中具有的许多功能可以更方便地进行 [!INCLUDE[TLA2#tla_api](../../../../includes/tla2sharptla-api-md.md)] 公开。  例如，<xref:System.Windows.FrameworkElement> 通过 <xref:System.Windows.FrameworkElement.BeginStoryboard%2A> 方法提供对动画的直接访问。  <xref:System.Windows.Media.Animation.Storyboard> 提供一种针对一组属性为多个动画编写脚本的方式。  
  
 <xref:System.Windows.FrameworkElement> 引入的两个最关键的内容是数据绑定和样式。  
  
 曾经使用 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]或 [!INCLUDE[TLA#tla_aspnet](../../../../includes/tlasharptla-aspnet-md.md)] 创建应用程序[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 的用户应当对 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中的数据绑定子系统较为熟悉。  在上述每个系统中，可通过一种简单的方式来表达希望将给定元素中的一个或多个属性绑定到一个数据片段。  [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 全面支持属性绑定、转换和列表绑定。  
  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中数据绑定的最值得关注的功能之一是引入了数据模板。  利用数据模板，您可以声明性地指定某个数据片断的可视化方式。  您可以将问题换个方向，让数据来确定将要创建的显示内容，而无需创建可绑定到数据的自定义用户界面。  
  
 样式实际上是轻量级的数据绑定。  使用样式，您可以将共享定义的一组属性绑定到元素的一个或多个实例。  通过显式引用（通过设置 <xref:System.Windows.FrameworkElement.Style%2A> 属性）或通过将样式与元素的 [!INCLUDE[TLA2#tla_clr](../../../../includes/tla2sharptla-clr-md.md)] 类型隐式关联，便可以将样式应用到元素。  
  
<a name="System_Windows_Controls_Control"></a>   
## System.Windows.Controls.Control  
 控件的最重要的功能是模板化。  如果将 WPF 的组合系统视为一个保留模式呈现系统，则控件可通过模板化以一种参数化的声明性方式描述其呈现。  <xref:System.Windows.Controls.ControlTemplate> 实际上不过是一个用于创建一组子元素的脚本，同时绑定到由控件提供的属性。  
  
 <xref:System.Windows.Controls.Control> 提供一组常用属性，如 <xref:System.Windows.Controls.Control.Foreground%2A>、<xref:System.Windows.Controls.Control.Background%2A>、<xref:System.Windows.Controls.Control.Padding%2A> 等，模板创作者可以使用这些常用属性来自定义控件的显示。  控件的实现提供了数据模型和交互模型。  交互模型定义了一组命令（如窗口的“关闭”），以及到输入笔势的绑定（如单击窗口上角的红叉）。  数据模型提供了一组属性，用于自定义交互模型或自定义显示（由模板确定）。  
  
 数据模型（属性）、交互模型（命令和事件）及显示模型（模板）之间的划分，使用户可以对控件的外观和行为进行完全自定义。  
  
 最常见的控件数据模型是内容模型。  如果查看 <xref:System.Windows.Controls.Button> 之类的控件，您会看到它具有一个类型为 <xref:System.Object> 的名为“Content”的属性。  在 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]和 [!INCLUDE[TLA#tla_aspnet](../../../../includes/tlasharptla-aspnet-md.md)] 中，此属性通常为一个字符串 – 不过，这会限制您可以在按钮中输入的内容类型。  按钮的内容可以是简单的字符串、复杂的数据对象或整个元素树。  如果是数据对象，可以使用数据模板构造显示内容。  
  
<a name="Summary"></a>   
## 摘要  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 旨在帮助您创建动态的数据驱动的演示系统。  系统的每一部分均可通过驱动行为的属性集来创建对象。  数据绑定是系统的基础部分，在每一层中均进行了集成。  
  
 传统的应用程序创建一个显示内容，然后绑定到某些数据。  在 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 中，关于控件的所有内容、显示内容的所有方面都是由某种类型的数据绑定生成的。  通过在按钮内部创建复合控件并将其显示绑定到按钮的内容属性，就会显示按钮内的文本。  
  
 当开始开发基于 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 的应用程序时，您应对其感到非常熟悉。  在其中设置属性、使用对象和数据绑定的方式与您使用 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]或 [!INCLUDE[TLA#tla_aspnet](../../../../includes/tlasharptla-aspnet-md.md)] 是极其相似的。  如果对 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 体系结构有更深的了解，您就能够创建更丰富的应用程序，这些应用程序在根本上会将数据视为应用程序的核心驱动力。  
  
## 请参阅  
 <xref:System.Windows.Media.Visual>   
 <xref:System.Windows.UIElement>   
 <xref:System.Windows.Input.ICommand>   
 <xref:System.Windows.FrameworkElement>   
 <xref:System.Windows.Threading.DispatcherObject>   
 <xref:System.Windows.Input.CommandBinding>   
 <xref:System.Windows.Controls.Control>   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [布局](../../../../docs/framework/wpf/advanced/layout.md)   
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)