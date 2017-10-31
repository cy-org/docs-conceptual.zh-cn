---
title: "焦点概述 | Microsoft Docs"
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
  - "应用程序, 焦点"
  - "应用程序中的焦点"
ms.assetid: 0230c4eb-0c8a-462b-ac4b-ae3e511659f4
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# 焦点概述
在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中，有两个与焦点有关的主要概念：键盘焦点和逻辑焦点。  键盘焦点指接收键盘输入的元素，而逻辑焦点指焦点范围中具有焦点的元素。  本概述将详细介绍这些概念。  理解这些概念之间的区别对于创建具有可以获取焦点的多个区域的复杂应用程序是非常重要的。  
  
 参与焦点管理的主要类有 <xref:System.Windows.Input.Keyboard> 类、<xref:System.Windows.Input.FocusManager> 类以及基元素类（如 <xref:System.Windows.UIElement> 和 <xref:System.Windows.ContentElement>）。  有关基元素的更多信息，请参见[基元素概述](../../../../docs/framework/wpf/advanced/base-elements-overview.md)。  
  
 <xref:System.Windows.Input.Keyboard> 类主要与键盘焦点相关，而 <xref:System.Windows.Input.FocusManager> 则与逻辑焦点相关，但这种区别不是绝对的。  具有键盘焦点的元素也将具有逻辑焦点，但具有逻辑焦点的元素不一定具有键盘焦点。  当您使用 <xref:System.Windows.Input.Keyboard> 类来设置具有键盘焦点的元素时，这一点是很明显的，因为它还在元素上设置逻辑焦点。  
  
   
  
<a name="Keyboard_Focus"></a>   
## 键盘焦点  
 键盘焦点指当前正在接收键盘输入的元素。  在整个桌面上，只能有一个具有键盘焦点的元素。  在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中，具有键盘焦点的元素会将 <xref:System.Windows.IInputElement.IsKeyboardFocused%2A> 设置为 `true`。  <xref:System.Windows.Input.Keyboard> 类的静态属性 <xref:System.Windows.Input.Keyboard.FocusedElement%2A> 获取当前具有键盘焦点的元素。  
  
 为了使元素能够获取键盘焦点，基元素的 <xref:System.Windows.UIElement.Focusable%2A> 和 <xref:System.Windows.UIElement.IsVisible%2A> 属性必须设置为 `true`。  有些类（如 <xref:System.Windows.Controls.Panel> 基类）默认情况下将 <xref:System.Windows.UIElement.Focusable%2A> 设置为 `false`；因此，如果您希望此类元素能够获取键盘焦点，必须将 <xref:System.Windows.UIElement.Focusable%2A> 设置为 `true`。  
  
 可以通过用户与 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 交互（例如，按 Tab 键定位到某个元素或者在某些元素上单击鼠标）来获取键盘焦点。  还可以通过使用 <xref:System.Windows.Input.Keyboard> 类的 <xref:System.Windows.Input.Keyboard.Focus%2A> 方法，以编程方式获取键盘焦点。  <xref:System.Windows.Input.Keyboard.Focus%2A> 方法尝试将键盘焦点给予指定的元素。  返回的元素是具有键盘焦点的元素，如果有旧的或新的焦点对象阻止请求，则具有键盘焦点的元素可能不是所请求的元素。  
  
 下面的示例使用 <xref:System.Windows.Input.Keyboard.Focus%2A> 方法在 <xref:System.Windows.Controls.Button> 上设置键盘焦点。  
  
 [!code-csharp[focussample#FocusSampleSetFocus](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FocusSample/CSharp/Window1.xaml.cs#focussamplesetfocus)]
 [!code-vb[focussample#FocusSampleSetFocus](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FocusSample/visualbasic/window1.xaml.vb#focussamplesetfocus)]  
  
 基元素类的 <xref:System.Windows.UIElement.IsKeyboardFocused%2A> 属性获取一个指示元素是否具有键盘焦点的值。  基元素类的 <xref:System.Windows.UIElement.IsKeyboardFocusWithin%2A> 属性获取一个指示元素或者它的任何一个可视子元素是否具有键盘焦点的值。  
  
 在应用程序启动时设置初始焦点的过程中，接收焦点的元素必须在应用程序加载的初始窗口的可视化树中，并且该元素必须将 <xref:System.Windows.UIElement.Focusable%2A> 和 <xref:System.Windows.UIElement.IsVisible%2A> 设置为 `true`。  设置初始焦点的推荐位置是在 <xref:System.Windows.FrameworkElement.Loaded> 事件处理程序中。  还可以通过调用 <xref:System.Windows.Threading.Dispatcher.Invoke%2A> 或 <xref:System.Windows.Threading.Dispatcher.BeginInvoke%2A> 来使用 <xref:System.Windows.Threading.Dispatcher> 回调。  
  
<a name="Logical_Focus"></a>   
## 逻辑焦点  
 逻辑焦点指焦点范围中的 <xref:System.Windows.Input.FocusManager.FocusedElement%2A?displayProperty=fullName>。  焦点范围是一个跟踪其范围内的 <xref:System.Windows.Input.FocusManager.FocusedElement%2A> 的元素。  当键盘焦点离开焦点范围时，焦点元素会失去键盘焦点，但保留逻辑焦点。  当键盘焦点返回到焦点范围时，焦点元素会再次获得键盘焦点。  这使得键盘焦点可以在多个焦点范围之间切换，但确保了在焦点返回到焦点范围时，焦点范围中的焦点元素再次获得键盘焦点。  
  
 一个应用程序中可以有多个具有逻辑焦点的元素，但在一个特定的焦点范围中只能有一个具有逻辑焦点的元素。  
  
 具有键盘焦点的元素还具有它所属的焦点范围的逻辑焦点。  
  
 在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 中，可以通过将 <xref:System.Windows.Input.FocusManager> 附加属性 <xref:System.Windows.Input.FocusManager.IsFocusScope%2A> 设置为 `true`，将元素转变为焦点范围。  在代码中，可以通过调用 <xref:System.Windows.Input.FocusManager.SetIsFocusScope%2A> 将元素转变为焦点范围。  
  
 下面的示例通过设置 <xref:System.Windows.Input.FocusManager.IsFocusScope%2A> 附加属性将 <xref:System.Windows.Controls.StackPanel> 转变为焦点范围。  
  
 [!code-xml[MarkupSnippets#MarkupIsFocusScopeXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MarkupSnippets/CSharp/Window1.xaml#markupisfocusscopexaml)]  
  
 [!code-csharp[FocusSnippets#FocusSetIsFocusScope](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FocusSnippets/CSharp/Window1.xaml.cs#focussetisfocusscope)]
 [!code-vb[FocusSnippets#FocusSetIsFocusScope](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FocusSnippets/visualbasic/window1.xaml.vb#focussetisfocusscope)]  
  
 <xref:System.Windows.Input.FocusManager.GetFocusScope%2A> 返回指定元素的焦点范围。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 中默认情况下即为焦点范围的类有 <xref:System.Windows.Window>、<xref:System.Windows.Controls.MenuItem>、<xref:System.Windows.Controls.ToolBar> 和 <xref:System.Windows.Controls.ContextMenu>。  
  
 <xref:System.Windows.Input.FocusManager.GetFocusedElement%2A> 获取指定焦点范围内具有焦点的元素。  <xref:System.Windows.Input.FocusManager.SetFocusedElement%2A> 设置指定焦点范围内具有焦点的元素。  <xref:System.Windows.Input.FocusManager.SetFocusedElement%2A> 通常用于设置最初具有焦点的元素。  
  
 下面的示例设置焦点范围中的焦点元素并获取焦点范围的焦点元素。  
  
 [!code-csharp[FocusSnippets#FocusGetSetFocusedElement](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FocusSnippets/CSharp/Window1.xaml.cs#focusgetsetfocusedelement)]
 [!code-vb[FocusSnippets#FocusGetSetFocusedElement](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FocusSnippets/visualbasic/window1.xaml.vb#focusgetsetfocusedelement)]  
  
<a name="Keyboard_Navigation"></a>   
## 键盘导航  
 当按下导航键之一时，<xref:System.Windows.Input.KeyboardNavigation> 类将负责实现默认键盘焦点导航。  导航键有：Tab、Shift\+Tab、Ctrl\+Tab、Ctrl\+Shift\+Tab、向上键、向下键、向左键和向右键。  
  
 可以通过设置附加的 <xref:System.Windows.Input.KeyboardNavigation> 属性 <xref:System.Windows.Input.KeyboardNavigation.TabNavigation%2A>、<xref:System.Windows.Input.KeyboardNavigation.ControlTabNavigation%2A> 和 <xref:System.Windows.Input.KeyboardNavigation.DirectionalNavigation%2A> 来更改导航容器的导航行为。  这些属性是 <xref:System.Windows.Input.KeyboardNavigationMode> 类型，可能值有 <xref:System.Windows.Input.KeyboardNavigationMode>、<xref:System.Windows.Input.KeyboardNavigationMode>、<xref:System.Windows.Input.KeyboardNavigationMode>、<xref:System.Windows.Input.KeyboardNavigationMode>、<xref:System.Windows.Input.KeyboardNavigationMode> 以及 <xref:System.Windows.Input.KeyboardNavigationMode>。  默认值是 <xref:System.Windows.Input.KeyboardNavigationMode>，这意味着元素不是导航容器。  
  
 下面的示例创建包含许多 <xref:System.Windows.Controls.MenuItem> 对象的 <xref:System.Windows.Controls.Menu>。  <xref:System.Windows.Controls.Menu> 的 <xref:System.Windows.Input.KeyboardNavigation.TabNavigation%2A> 附加属性设置为 <xref:System.Windows.Input.KeyboardNavigationMode>。  当使用 Tab 键在 <xref:System.Windows.Controls.Menu> 中改变焦点时，焦点将从每个元素上移过，当到达最后一个元素后会返回第一个元素。  
  
 [!code-xml[MarkupSnippets#MarkupKeyboardNavigationTabNavigationXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MarkupSnippets/CSharp/Window1.xaml#markupkeyboardnavigationtabnavigationxaml)]  
  
 [!code-csharp[MarkupSnippets#MarkupKeyboardNavigationTabNavigationCODE](../../../../samples/snippets/csharp/VS_Snippets_Wpf/MarkupSnippets/CSharp/Window1.xaml.cs#markupkeyboardnavigationtabnavigationcode)]
 [!code-vb[MarkupSnippets#MarkupKeyboardNavigationTabNavigationCODE](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/MarkupSnippets/visualbasic/window1.xaml.vb#markupkeyboardnavigationtabnavigationcode)]  
  
<a name="Manipulating_Focus_Programmatically"></a>   
## 以编程方式定位焦点  
 处理焦点的其他 [!INCLUDE[TLA#tla_api](../../../../includes/tlasharptla-api-md.md)] 有 <xref:System.Windows.UIElement.MoveFocus%2A> 和 <xref:System.Windows.UIElement.PredictFocus%2A>。  
  
 <xref:System.Windows.FrameworkElement.MoveFocus%2A> 将焦点移到应用程序中的下一个元素。  <xref:System.Windows.Input.TraversalRequest> 用于指定方向。  传递给 <xref:System.Windows.UIElement.MoveFocus%2A> 的 <xref:System.Windows.Input.FocusNavigationDirection> 指定焦点可以移动的不同方向，如 <xref:System.Windows.Input.FocusNavigationDirection>、<xref:System.Windows.Input.FocusNavigationDirection>、<xref:System.Windows.Input.FocusNavigationDirection> 和 <xref:System.Windows.Input.FocusNavigationDirection>。  
  
 下面的示例使用 <xref:System.Windows.FrameworkElement.MoveFocus%2A> 来改变焦点元素。  
  
 [!code-csharp[focussample#FocusSampleMoveFocus](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FocusSample/CSharp/Window1.xaml.cs#focussamplemovefocus)]
 [!code-vb[focussample#FocusSampleMoveFocus](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/FocusSample/visualbasic/window1.xaml.vb#focussamplemovefocus)]  
  
 <xref:System.Windows.FrameworkElement.PredictFocus%2A> 返回当要改变焦点时将接收焦点的对象。  当前，<xref:System.Windows.FrameworkElement.PredictFocus%2A> 仅支持 <xref:System.Windows.Input.FocusNavigationDirection>、<xref:System.Windows.Input.FocusNavigationDirection>、<xref:System.Windows.Input.FocusNavigationDirection> 以及 <xref:System.Windows.Input.FocusNavigationDirection>。  
  
<a name="Focus_Events"></a>   
## 焦点事件  
 与键盘焦点相关的事件有 <xref:System.Windows.Input.Keyboard.PreviewGotKeyboardFocus>、<xref:System.Windows.Input.Keyboard.GotKeyboardFocus>、<xref:System.Windows.Input.Keyboard.PreviewLostKeyboardFocus> 以及 <xref:System.Windows.Input.Keyboard.LostKeyboardFocus>。  这些事件定义为 <xref:System.Windows.Input.Keyboard> 类的附加事件，但更便于作为基元素类上的等效路由事件来访问。  有关事件的更多信息，请参见[路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)。  
  
 当元素获取键盘焦点时，引发 <xref:System.Windows.Input.Keyboard.GotKeyboardFocus>。  当元素失去键盘焦点时，引发 <xref:System.Windows.Input.Keyboard.LostKeyboardFocus>。  如果处理了 <xref:System.Windows.Input.Keyboard.PreviewGotKeyboardFocus> 事件或 <xref:System.Windows.Input.Keyboard.PreviewLostKeyboardFocusEvent> 事件，并且 <xref:System.Windows.RoutedEventArgs.Handled%2A> 设置为 `true`，则焦点将不会改变。  
  
 下面的示例将 <xref:System.Windows.UIElement.GotKeyboardFocus> 和 <xref:System.Windows.UIElement.LostKeyboardFocus> 事件处理程序附加到 <xref:System.Windows.Controls.TextBox>。  
  
 [!code-xml[keyboardsample#KeyboardSampleXAMLHandlerHookup](../../../../samples/snippets/csharp/VS_Snippets_Wpf/KeyboardSample/CSharp/Window1.xaml#keyboardsamplexamlhandlerhookup)]  
  
 当 <xref:System.Windows.Controls.TextBox> 获取键盘焦点时，<xref:System.Windows.Controls.TextBox> 的 <xref:System.Windows.Controls.Control.Background%2A> 属性会改为 <xref:System.Windows.Media.Brushes.LightBlue%2A>。  
  
 [!code-csharp[keyboardsample#KeyboardSampleGotFocus](../../../../samples/snippets/csharp/VS_Snippets_Wpf/KeyboardSample/CSharp/Window1.xaml.cs#keyboardsamplegotfocus)]
 [!code-vb[keyboardsample#KeyboardSampleGotFocus](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/KeyboardSample/visualbasic/window1.xaml.vb#keyboardsamplegotfocus)]  
  
 当 <xref:System.Windows.Controls.TextBox> 失去键盘焦点时，<xref:System.Windows.Controls.TextBox> 的 <xref:System.Windows.Controls.Control.Background%2A> 属性会重新改为 white。  
  
 [!code-csharp[keyboardsample#KeyboardSampleLostFocus](../../../../samples/snippets/csharp/VS_Snippets_Wpf/KeyboardSample/CSharp/Window1.xaml.cs#keyboardsamplelostfocus)]
 [!code-vb[keyboardsample#KeyboardSampleLostFocus](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/KeyboardSample/visualbasic/window1.xaml.vb#keyboardsamplelostfocus)]  
  
 与逻辑焦点有关的事件有 <xref:System.Windows.UIElement.GotFocus> 和 <xref:System.Windows.UIElement.LostFocus>。  这些事件在 <xref:System.Windows.Input.FocusManager> 中定义为附加事件，但 <xref:System.Windows.Input.FocusManager> 不公开 CLR 事件包装。  <xref:System.Windows.UIElement> 和 <xref:System.Windows.ContentElement> 可以更方便地公开这些事件。  
  
## 请参阅  
 <xref:System.Windows.Input.FocusManager>   
 <xref:System.Windows.UIElement>   
 <xref:System.Windows.ContentElement>   
 [输入概述](../../../../docs/framework/wpf/advanced/input-overview.md)   
 [基元素概述](../../../../docs/framework/wpf/advanced/base-elements-overview.md)