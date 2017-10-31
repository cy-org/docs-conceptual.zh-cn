---
title: "WPF 自定义控件的 UI 自动化 | Microsoft Docs"
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
  - "应用 UI 自动化的自定义控件 [WPF]"
  - "将应用于自定义控件的辅助功能 [WPF]"
  - "提高辅助功能的自定义控件 [WPF]"
  - "自定义控件中使用的 UI 自动化 [WPF]"
ms.assetid: 47b310fc-fbd5-4ce2-a606-22d04c6d4911
caps.latest.revision: 34
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 34
---
# WPF 自定义控件的 UI 自动化
[!INCLUDE[TLA#tla_uiautomation](../../../../includes/tlasharptla-uiautomation-md.md)]提供一个通用的接口，自动化客户端可用来检查或操作的各种平台和框架的用户界面。 [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)]使质量保证 （测试） 代码和可访问性应用程序，如屏幕阅读器可以检查用户界面元素，并模拟从其他代码与其用户交互。 璝惠[!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)]跨所有平台，请参阅辅助功能。  
  
 本主题介绍如何实现自定义控件在 WPF 应用程序中运行的服务器端 UI 自动化提供程序。 WPF 支持[!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)]通过对等方自动化对象，等同于用户界面元素的树的树。 测试代码和应用程序提供辅助功能可用于自动化的对等对象直接 （进程内的代码） 或通过提供的通用界面[!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)]。  
  
 
  
<a name="AutomationPeerClasses"></a>   
## <a name="automation-peer-classes"></a>自动化的对等类  
 WPF 控件支持[!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)]通过对等类派生自的树<xref:System.Windows.Automation.Peers.AutomationPeer>。 按照约定，对等类名称的控件类名开头和结尾"AutomationPeer"。 例如， <xref:System.Windows.Automation.Peers.ButtonAutomationPeer>是适用于的对等方<xref:System.Windows.Controls.Button>控件类。 对等类是大致相当于[!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)]控件类型，但特定于[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]元素。 访问通过 WPF 应用程序的自动化代码[!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)]接口不使用自动化对等类直接，但同一进程空间中的自动化代码可以直接使用自动化对等类。  
  
<a name="BuiltInAutomationPeerClasses"></a>   
## <a name="built-in-automation-peer-classes"></a>内置的自动化对等类  
 元素实现自动化对等类，如果用户接受接口活动，从该用户，或者当它们包含所需的屏幕阅读器应用程序的用户信息。 并非所有的 WPF 视觉元素具有自动化对等方。 实现自动化对等的类的示例包括<xref:System.Windows.Controls.Button>， <xref:System.Windows.Controls.TextBox>，和<xref:System.Windows.Controls.Label>。 不实现自动化对等的类的示例包括从派生类<xref:System.Windows.Controls.Decorator>，如<xref:System.Windows.Controls.Border>，基于和类<xref:System.Windows.Controls.Panel>，如<xref:System.Windows.Controls.Grid>和<xref:System.Windows.Controls.Canvas>。  
  
 基<xref:System.Windows.Controls.Control>类没有相应的对等类。 如果您需要一个对等类对应于派生自的自定义控件<xref:System.Windows.Controls.Control>，应派生自定义对等类从<xref:System.Windows.Automation.Peers.FrameworkElementAutomationPeer>。  
  
<a name="SecurityConsiderations"></a>   
## <a name="security-considerations-for-derived-peers"></a>有关派生的对等方的安全注意事项  
 自动化的对等方必须在部分信任环境中运行。 UIAutomationClient 程序集中的代码未配置为在部分信任环境中，运行和自动化的对等代码不应引用该程序集。 相反，您应使用 UIAutomationTypes 程序集中的类。 例如，您应使用<xref:System.Windows.Automation.AutomationElementIdentifiers>类从 UIAutomationTypes 程序集，它对应于<xref:System.Windows.Automation.AutomationElement> UIAutomationClient 程序集中的类。 它可以安全地引用在自动化代码中对等方 UIAutomationTypes 程序集。  
  
<a name="PeerNavigation"></a>   
## <a name="peer-navigation"></a>对等方导航  
 找到后的自动化对等方，进程内代码可以在树中导航对等方通过调用对象的<xref:System.Windows.Automation.Peers.AutomationPeer.GetChildren%2A>和<xref:System.Windows.Automation.Peers.AutomationPeer.GetParent%2A>方法。 间导航[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]由对等方的实现支持在控件内的元素<xref:System.Windows.Automation.Peers.AutomationPeer.GetChildrenCore%2A>方法。 UI 自动化系统调用此方法来构建一个树控件; 中包含的子元素例如，列表框中列表项。 默认值<xref:System.Windows.Automation.Peers.UIElementAutomationPeer.GetChildrenCore%2A?displayProperty=fullName>方法遍历元素来构建自动化对等方的树的可视化树。 自定义控件重写此方法以公开向自动化客户端，返回传达的信息或允许用户交互的元素自动化对等方的子元素。  
  
<a name="Customizations"></a>   
## <a name="customizations-in-a-derived-peer"></a>中派生的对等自定义项  
 派生自的所有类<xref:System.Windows.UIElement>和<xref:System.Windows.ContentElement>包含受保护的虚方法<xref:System.Windows.UIElement.OnCreateAutomationPeer%2A>。 WPF 调用<xref:System.Windows.UIElement.OnCreateAutomationPeer%2A>以获取每个控件的自动化的对等对象。 若要获取有关控件的特征和功能的信息并模拟交互使用，自动化代码可以使用对等方。 支持自动化的自定义控件必须重写<xref:System.Windows.UIElement.OnCreateAutomationPeer%2A>并返回派生自的类的实例<xref:System.Windows.Automation.Peers.AutomationPeer>。 例如，如果自定义控件派生<xref:System.Windows.Controls.Primitives.ButtonBase>类，则返回的对象<xref:System.Windows.UIElement.OnCreateAutomationPeer%2A>应派生自<xref:System.Windows.Automation.Peers.ButtonBaseAutomationPeer>。  
  
 在实现自定义控件时，必须重写中基本自动化对等类的描述行为唯一且特定于自定义控件的"核心"方法。  
  
### <a name="override-oncreateautomationpeer"></a>重写 OnCreateAutomationPeer  
 重写<xref:System.Windows.UIElement.OnCreateAutomationPeer%2A>方法为您的自定义控件，以便它返回您的提供程序对象，必须直接或间接派生自<xref:System.Windows.Automation.Peers.AutomationPeer>。  
  
### <a name="override-getpattern"></a>重写 GetPattern  
 自动化的对等方简化服务器端的一些实现方面[!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)]提供商，但自定义控件自动化对等方仍必须处理模式接口。 非 WPF 提供程序，如对等方支持控件模式通过提供的接口的实现<xref:System.Windows.Automation.Provider?displayProperty=fullName>命名空间，如<xref:System.Windows.Automation.Provider.IInvokeProvider>。 通过对等类自身或另一个对象，可以实现控件模式接口。 对等方的实现<xref:System.Windows.Automation.Peers.AutomationPeer.GetPattern%2A>返回支持指定的模式的对象。 [!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)]代码调用<xref:System.Windows.Automation.Peers.UIElementAutomationPeer.GetPattern%2A>方法，并指定<xref:System.Windows.Automation.Peers.PatternInterface>枚举值。 重写<xref:System.Windows.Automation.Peers.UIElementAutomationPeer.GetPattern%2A>应返回实现指定的模式的对象。 如果您的控件没有一种模式的自定义实现，则可以调用基类型实现<xref:System.Windows.Automation.Peers.AutomationPeer.GetPattern%2A>要检索其实现或者为 null，如果模式不支持此控件类型。 例如，可以为某个范围内的值设置自定义的 NumericUpDown 控件使其[!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)]对等方将会实现<xref:System.Windows.Automation.Provider.IRangeValueProvider>接口。 下面的示例演示如何对等方的<xref:System.Windows.Automation.Peers.UIElementAutomationPeer.GetPattern%2A>重写方法以响应<xref:System.Windows.Automation.Peers.PatternInterface?displayProperty=fullName>值。  
  
 [!code-csharp[CustomControlNumericUpDown#GetPattern](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDown/CSharp/CustomControlLibrary/NumericUpDown.cs#getpattern)]
 [!code-vb[CustomControlNumericUpDown#GetPattern](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDown/visualbasic/customcontrollibrary/numericupdown.vb#getpattern)]  
  
 一个<xref:System.Windows.Automation.Peers.UIElementAutomationPeer.GetPattern%2A>方法还可以指定一个子元素作为模式提供程序。 下面的代码演示如何<xref:System.Windows.Controls.ItemsControl>传输向下滚动到其内部的对等方的模式处理<xref:System.Windows.Controls.ScrollViewer>控件。  
  
```csharp  
public override object GetPattern(PatternInterface patternInterface)  
{  
    if (patternInterface == PatternInterface.Scroll)  
    {  
        ItemsControl owner = (ItemsControl) base.Owner;  
  
        // ScrollHost is internal to the ItemsControl class  
        if (owner.ScrollHost != null)  
        {  
            AutomationPeer peer = UIElementAutomationPeer.CreatePeerForElement(owner.ScrollHost);  
            if ((peer != null) && (peer is IScrollProvider))  
            {  
                peer.EventsSource = this;  
                return (IScrollProvider) peer;  
            }  
        }  
    }  
    return base.GetPattern(patternInterface);  
}  
```  
  
```vb  
Public Class Class1  
    Public Overrides Function GetPattern(ByVal patternInterface__1 As PatternInterface) As Object  
        If patternInterface1 = PatternInterface.Scroll Then  
            Dim owner As ItemsControl = DirectCast(MyBase.Owner, ItemsControl)  
  
            ' ScrollHost is internal to the ItemsControl class  
            If owner.ScrollHost IsNot Nothing Then  
                Dim peer As AutomationPeer = UIElementAutomationPeer.CreatePeerForElement(owner.ScrollHost)  
                If (peer IsNot Nothing) AndAlso (TypeOf peer Is IScrollProvider) Then  
                    peer.EventsSource = Me  
                    Return DirectCast(peer, IScrollProvider)  
                End If  
            End If  
        End If  
        Return MyBase.GetPattern(patternInterface1)  
    End Function  
End Class  
```  
  
 若要指定模式处理一个子元素，此代码将获取子元素的对象，通过创建一个对等方<xref:System.Windows.Automation.Peers.UIElementAutomationPeer.CreatePeerForElement%2A>方法，设置<xref:System.Windows.Automation.Peers.AutomationPeer.EventsSource%2A>到当前对等方，新的对等方的属性，并返回新的对等方。 设置<xref:System.Windows.Automation.Peers.AutomationPeer.EventsSource%2A>子元素可防止子元素出现在自动化对等方树并将引发的子元素的所有事件都指定为源自中指定的控件<xref:System.Windows.Automation.Peers.AutomationPeer.EventsSource%2A>。 <xref:System.Windows.Controls.ScrollViewer>控件未出现在自动化树中，和它所生成的滚动事件显示为来自<xref:System.Windows.Controls.ItemsControl>对象。  
  
### <a name="override-core-methods"></a>重写"核心"方法  
 自动化代码通过调用公共方法的对等类获取有关控件的信息。 若要提供有关控件的信息，请重写时控件的实现不同于基本自动化对等类所提供的名称以"核心"结尾的每个方法。 最低限度上，控件必须实现<xref:System.Windows.Automation.Peers.AutomationPeer.GetClassNameCore%2A>和<xref:System.Windows.Automation.Peers.AutomationPeer.GetAutomationControlTypeCore%2A>方法，如下面的示例中所示。  
  
 [!code-csharp[CustomControlNumericUpDown#CoreOverrides](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDown/CSharp/CustomControlLibrary/NumericUpDown.cs#coreoverrides)]
 [!code-vb[CustomControlNumericUpDown#CoreOverrides](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDown/visualbasic/customcontrollibrary/numericupdown.vb#coreoverrides)]  
  
 实现<xref:System.Windows.Automation.Peers.AutomationPeer.GetAutomationControlTypeCore%2A>通过返回描述您的控件<xref:System.Windows.Automation.ControlType>值。 尽管您可以返回<xref:System.Windows.Automation.ControlType.Custom?displayProperty=fullName>，如果该准确地描述您的控件，则应返回更具体的控件类型之一。 返回值为<xref:System.Windows.Automation.ControlType.Custom?displayProperty=fullName>需要额外的工作，从而实现提供程序[!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)]，和[!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)]客户端产品不能以应对预期的控件结构、 键盘交互和可能的控件模式。  
  
 实现<xref:System.Windows.Automation.Peers.AutomationPeer.IsContentElementCore%2A>和<xref:System.Windows.Automation.Peers.AutomationPeer.IsControlElementCore%2A>方法，以指示您的控件是否包含数据内容或执行的交互式角色中的用户界面 （或两者）。 默认情况下，这两种方法都返回`true`。 这些设置提高易用性自动化工具，如屏幕读取器，可以使用这些方法来筛选自动化树。 如果您<xref:System.Windows.Automation.Peers.AutomationPeer.GetPattern%2A>子元素对等方，子元素的对等方的处理方法传输模式<xref:System.Windows.Automation.Peers.AutomationPeer.IsControlElementCore%2A>方法可以返回 false，以便隐藏在自动化树中的子元素对等方。 例如，在滚动<xref:System.Windows.Controls.ListBox>由处理<xref:System.Windows.Controls.ScrollViewer>，和自动化对等方<xref:System.Windows.Automation.Peers.PatternInterface?displayProperty=fullName>返回<xref:System.Windows.Automation.Peers.AutomationPeer.GetPattern%2A>方法<xref:System.Windows.Automation.Peers.ScrollViewerAutomationPeer>关联<xref:System.Windows.Automation.Peers.ListBoxAutomationPeer>。因此， <xref:System.Windows.Automation.Peers.AutomationPeer.IsControlElementCore%2A>方法<xref:System.Windows.Automation.Peers.ScrollViewerAutomationPeer>返回`false`，以便<xref:System.Windows.Automation.Peers.ScrollViewerAutomationPeer>未出现在自动化树。  
  
 自动化同级应提供适当的默认值为您的控件。 请注意，引用您的控件的 XAML 可以通过重写您的核心方法的对等方实现包括<xref:System.Windows.Automation.AutomationProperties>属性。 例如，下面的 XAML 创建具有两个自定义的按钮[!INCLUDE[TLA2#tla_uiautomation](../../../../includes/tla2sharptla-uiautomation-md.md)]属性。  
  
```xaml  
<Button AutomationProperties.Name="Special"   
    AutomationProperties.HelpText="This is a special button."/>  
```  
  
### <a name="implement-pattern-providers"></a>实现模式提供程序  
 如果直接从所属的元素派生自定义提供程序实现的接口显式声明<xref:System.Windows.Controls.Control>。 例如，下面的代码声明的对等方<xref:System.Windows.Controls.Control>实现范围值。  
  
```csharp  
public class RangePeer1 : FrameworkElementAutomationPeer, IRangeValueProvider { }  
```  
  
```vb  
Public Class RangePeer1  
    Inherits FrameworkElementAutomationPeer  
    Implements IRangeValueProvider  
End Class  
```  
  
 如果所属的控件派生自指定类型的控件如<xref:System.Windows.Controls.Primitives.RangeBase>，对等方可以派生自非等效派生的对等类。 在这种情况下，对等方将派生自<xref:System.Windows.Automation.Peers.RangeBaseAutomationPeer>，其中提供的基实现<xref:System.Windows.Automation.Provider.IRangeValueProvider>。 下面的代码演示一个对等方的声明。  
  
```csharp  
public class RangePeer2 : RangeBaseAutomationPeer { }  
```  
  
```vb  
Public Class RangePeer2  
    Inherits RangeBaseAutomationPeer  
End Class  
```  
  
 有关示例实现，请参阅[带有主题和 UI 自动化支持示例的 NumericUpDown 自定义控件](http://go.microsoft.com/fwlink/?LinkID=160025)。  
  
### <a name="raise-events"></a>引发事件  
 自动化客户端可以订阅自动化事件。 自定义控件必须报告更改来控制通过调用状态<xref:System.Windows.Automation.Peers.AutomationPeer.RaiseAutomationEvent%2A>方法。 同样，当属性值更改，则调用<xref:System.Windows.Automation.Peers.AutomationPeer.RaisePropertyChangedEvent%2A>方法。 下面的代码演示如何获取从中的控制代码的对等对象并调用一个方法来引发事件。 作为一种优化，该代码确定是否有任何侦听器侦听此事件类型。 引发事件时，才侦听器可以避免不必要的开销，并有助于保持响应状态的控件。  
  
 [!code-csharp[CustomControlNumericUpDown#RaiseEventFromControl](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDown/CSharp/CustomControlLibrary/NumericUpDown.cs#raiseeventfromcontrol)]
 [!code-vb[CustomControlNumericUpDown#RaiseEventFromControl](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDown/visualbasic/customcontrollibrary/numericupdown.vb#raiseeventfromcontrol)]  
  
## <a name="see-also"></a>另请参阅  
 [UI 自动化概述](../../../../docs/framework/ui-automation/ui-automation-overview.md)   
 [带有主题和 UI 自动化支持示例的 NumericUpDown 自定义控件](http://go.microsoft.com/fwlink/?LinkID=160025)   
 [服务器端 UI 自动化提供程序实现](../../../../docs/framework/ui-automation/server-side-ui-automation-provider-implementation.md)