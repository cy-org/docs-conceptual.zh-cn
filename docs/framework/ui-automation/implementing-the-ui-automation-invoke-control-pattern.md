---
title: "Implementing the UI Automation Invoke Control Pattern | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "UI Automation, Invoke control pattern"
  - "control patterns, Invoke"
  - "Invoke control pattern"
ms.assetid: e5b1e239-49f8-468e-bfec-1fba02ec9ac4
caps.latest.revision: 31
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 30
---
# Implementing the UI Automation Invoke Control Pattern
> [!NOTE]
>  本文档适用于想要使用 <xref:System.Windows.Automation> 命名空间中定义的托管 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 类的 .NET Framework 开发人员。 有关 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 的最新信息，请参阅 [Windows 自动化 API：UI 自动化](http://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本主题介绍了实现 <xref:System.Windows.Automation.Provider.IInvokeProvider> 的准则和约定，包括有关事件和属性的信息。 本主题的结尾列出了指向其他参考资料的链接。  
  
 <xref:System.Windows.Automation.InvokePattern> 控件模式用于支持激活时不维护状态而是启动或执行单个明确操作的控件。 维护状态的控件（如复选框和单选按钮）则是必须分别实现 <xref:System.Windows.Automation.Provider.IToggleProvider> 和 <xref:System.Windows.Automation.Provider.ISelectionItemProvider>。 有关实现此 Invoke 控件模式的控件的示例，请参阅 [Control Pattern Mapping for UI Automation Clients](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md)。  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## 实现准则和约定  
 在实现 Invoke 控件模式时，请注意以下准则和约定：  
  
-   如果不通过另一个控件模式提供程序公开同一行为，则控件实现 <xref:System.Windows.Automation.Provider.IInvokeProvider>。 例如，如果控件上的 <xref:System.Windows.Automation.InvokePattern.Invoke%2A> 方法与 <xref:System.Windows.Automation.ExpandCollapsePattern.Expand%2A> 方法或 <xref:System.Windows.Automation.ExpandCollapsePattern.Collapse%2A> 方法执行同一操作，则控件不应实现 <xref:System.Windows.Automation.Provider.IInvokeProvider>。  
  
-   通常通过单击或双击或按 ENTER、预定义的键盘快捷键或某种备用的击键组合来调用控件。  
  
-   在已被激活的控件上引发 <xref:System.Windows.Automation.InvokePatternIdentifiers.InvokedEvent>（作为对执行关联操作的控件的响应）。 如果可能，应在控件完成操作后引发事件且在不阻止的情况下返回事件。 在以下情况中，应在服务 Invoke 请求之前引发调用的事件：  
  
    -   不可能等至操作完成，或这一做法不实际。  
  
    -   该操作需要用户交互。  
  
    -   该操作很耗时并且会导致调用的客户端花费大量的时间进行阻止。  
  
-   如果调用该控件会产生巨大的负面影响，应通过 <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.HelpText%2A> 属性公开这些副作用。 例如，即使 <xref:System.Windows.Automation.Provider.IInvokeProvider.Invoke%2A> 不与所选内容相关联，<xref:System.Windows.Automation.Provider.IInvokeProvider.Invoke%2A> 也可能会导致另一个控件变为处于选定状态。  
  
-   悬停（或鼠标悬停）效果通常不会构成调用的事件。 但是，执行基于悬停状态的操作（而不是导致视觉效果）的控件应支持 <xref:System.Windows.Automation.InvokePattern> 控件模式。  
  
> [!NOTE]
>  如果该控件仅可作为与鼠标相关的副作用的结果被调用，则此实现被视为可访问性问题。  
  
-   调用一个控件不同于选择一个项。 但是，具体取决于控件，调用控件可能导致项被选为副作用。 例如，调用“我的文档”文件夹中的 [!INCLUDE[TLA#tla_word](../../../includes/tlasharptla-word-md.md)] 文档列表项将会同时选择该项和打开该文档。  
  
-   元素被调用时将立即从 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 树中消失。 从由事件回调提供的元素请求信息可能失败。 建议的解决方法是预取缓存的信息。  
  
-   控件可实现多个控件模式。 例如，[!INCLUDE[TLA#tla_xl](../../../includes/tlasharptla-xl-md.md)] 工具栏上的“填充颜色”控件同时实现 <xref:System.Windows.Automation.InvokePattern> 和 <xref:System.Windows.Automation.ExpandCollapsePattern> 控件模式。<xref:System.Windows.Automation.ExpandCollapsePattern> 公开菜单，而 <xref:System.Windows.Automation.InvokePattern> 用所选颜色填充活动选择项。  
  
<a name="Required_Members_for_the_IValueProvider_Interface"></a>   
## IInvokeProvider 必需的成员  
 实现 <xref:System.Windows.Automation.Provider.IInvokeProvider> 需要以下属性和方法。  
  
|必需的成员|成员类型|备注|  
|-----------|----------|--------|  
|<xref:System.Windows.Automation.Provider.IInvokeProvider.Invoke%2A>|方法|<xref:System.Windows.Automation.Provider.IInvokeProvider.Invoke%2A> 是一个异步调用且必须立即返回而不阻塞。<br /><br /> 此行为对于被调用时直接或间接启动模式对话框的控件而言尤其重要。 引发该事件的任何 UI 自动化客户端将保持被阻止的状态，直到模式对话框关闭为止。|  
  
<a name="Exceptions"></a>   
## 异常  
 提供程序必须引发以下异常。  
  
|异常类型|条件|  
|----------|--------|  
|<xref:System.Windows.Automation.ElementNotEnabledException>|如果未启用该控件。|  
  
## 请参阅  
 [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)   
 [Support Control Patterns in a UI Automation Provider](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)   
 [UI Automation Control Patterns for Clients](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)   
 [Invoke a Control Using UI Automation](../../../docs/framework/ui-automation/invoke-a-control-using-ui-automation.md)   
 [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)   
 [Use Caching in UI Automation](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)