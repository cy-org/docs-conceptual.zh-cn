---
title: "UI Automation TextPattern Overview | Microsoft Docs"
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
  - "UI Automation, TextPattern class"
  - "TextPattern class"
  - "classes, TextPattern"
ms.assetid: 41787927-df1f-4f4a-aba3-641662854fc4
caps.latest.revision: 38
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 37
---
# UI Automation TextPattern Overview
> [!NOTE]
>  本文档适用于想要使用 <xref:System.Windows.Automation> 命名空间中定义的托管 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 类的 .NET Framework 开发人员。 有关 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 的最新信息，请参阅 [Windows 自动化 API：UI 自动化](http://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本概述介绍如何使用 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 公开文本内容，其中包括在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 支持的平台中的文本控件的格式和样式特性。 这些控件包括但不限于：[!INCLUDE[TLA#tla_winfx](../../../includes/tlasharptla-winfx-md.md)] <xref:System.Windows.Controls.TextBox> 和 <xref:System.Windows.Controls.RichTextBox> 以及其 [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] 等效项。  
  
 控件文本内容的功能通过使用 <xref:System.Windows.Automation.TextPattern> 控件模式完成，该控件模式表示作为文本流的文本容器的内容。 与之相反，<xref:System.Windows.Automation.TextPattern> 需要 <xref:System.Windows.Automation.Text.TextPatternRange> 的支持，以公开格式和样式特性。<xref:System.Windows.Automation.Text.TextPatternRange> 通过采用一系列 <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint> 和 <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint> 终结点表示文本容器中连续或多个不连续的的文本段来支持 <xref:System.Windows.Automation.TextPattern>。<xref:System.Windows.Automation.Text.TextPatternRange> 支持功能包括选择、比较、检索和遍历。  
  
> [!NOTE]
>  <xref:System.Windows.Automation.TextPattern> 类不提供插入或修改文本的方法。 但是，具体取决于该控件，这可以通过 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] <xref:System.Windows.Automation.ValuePattern> 或直接键盘输入得到解决。 有关示例，请参见[TextPattern Insert Text Sample](http://msdn.microsoft.com/zh-cn/67353f93-7ee2-42f2-ab76-5c078cf6ca16)。  
  
 本概述中所述的功能对辅助技术供应商及其最终用户至关重要。 辅助技术可以使用 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 为用户收集完整的文本格式信息，并通过 <xref:System.Windows.Automation.Text.TextUnit>（字符、单词、行或段落）提供编程方式导航和文本选择。  
  
<a name="UI_Automation_TextPattern_vs__Cicero"></a>   
## UI 自动化 TextPattern 与文本服务框架  
 [!INCLUDE[TLA#tla_tsf](../../../includes/tlasharptla-tsf-md.md)] 是一个简单的可伸缩系统框架，允许自然语言服务和在桌面上和应用程序中进行高级的文本输入。 除了为应用程序提供接口以公开其文本存储，它还支持该文本存储的元数据。  
  
 但是，[!INCLUDE[TLA2#tla_tsf](../../../includes/tla2sharptla-tsf-md.md)] 适用于需要将输入注入到上下文感知的情境中，而 <xref:System.Windows.Automation.TextPattern> 是只读解决方案（如上所示，具有有限的解决方法），用于提供对屏幕阅读器和盲文设备的文本存储的优化访问。  
  
 简单来说，需要对文本存储的只读访问权限的可访问技术可以使用 <xref:System.Windows.Automation.TextPattern>，但对于上下文感知输入则需要更复杂的 [!INCLUDE[TLA2#tla_tsf](../../../includes/tla2sharptla-tsf-md.md)] 功能。  
  
<a name="Control_Types"></a>   
## 控件类型  
  
#### Text  
 Text 控件是表示屏幕上一段文本的基本元素。  
  
 独立的文本控件可用作标签或窗体上的静态文本。 文本控件也可包含在 <xref:System.Windows.Automation.ControlType.ListItem>、<xref:System.Windows.Automation.ControlType.TreeItem> 或 <xref:System.Windows.Automation.ControlType.DataItem> 的结构中。  
  
> [!NOTE]
>  文本控件可能不会显示在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 树的内容视图中（请参阅 [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)）。 这是因为文本控件通常通过另一个控件的 Name 属性显示。 例如，用于标记编辑控件的文本是通过编辑控件的 Name 属性公开的。 因为，此编辑控件位于 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 树的内容视图中，文本元素自身没有必要处于 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 树的视图中。 在内容视图中显示的唯一文本为不是冗余信息的文本。 这能让任何辅助技术仅对其用户需要的信息段进行快速筛选。  
  
#### 编辑  
 编辑控件使用户可以查看和编辑单个文本行。  
  
> [!NOTE]
>  在某些布局方案中，单个文本行可能会换行。  
  
#### Document  
 文档控件能让用户导航并从多个页面的文本上获取的信息。  
  
<a name="TextPattern_Client_API_s"></a>   
## TextPattern 客户端 API 的  
  
|||  
|-|-|  
|`System.Windows.Automation.TextPattern Class`|文本模型 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 的入口点。<br /><br /> 此类还包含两个 <xref:System.Windows.Automation.TextPattern> 事件侦听器：<xref:System.Windows.Automation.TextPattern.TextSelectionChangedEvent> 和 <xref:System.Windows.Automation.TextPattern.TextChangedEvent>。|  
|`System.Windows.Automation.Text.TextPatternRange Class`|支持 <xref:System.Windows.Automation.TextPattern> 的文本容器内的文本段的表示形式。<br /><br /> UI 自动化客户端应该小心使用 <xref:System.Windows.Automation.Text.TextPatternRange> 创建的文本范围的当前有效性。 如果新的文本完全替换文本控件中的原始文本，则当前的文本范围将变为无效。 但是，如果只更改了原始文本的一部分，并且基础的文本控件使用定位点（或终结点）而不是绝对字符定位来管理其文本“指示器”，则文本范围可能仍具有有效性。<br /><br /> 客户端可以侦听 <xref:System.Windows.Automation.TextPattern.TextChangedEvent>，获取任何他们正在处理的文本内容的更改通知。|  
|`System.Windows.Automation.AutomationTextAttribute Class`|用于标识文本范围的格式属性。|  
  
<a name="TextPattern_Provider_API_s"></a>   
## TextPattern 提供程序 API 的  
 在本机或通过 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 代理的方式执行 <xref:System.Windows.Automation.Provider.ITextProvider> 和 <xref:System.Windows.Automation.Provider.ITextRangeProvider> 接口来支持 <xref:System.Windows.Automation.TextPattern> 的 UI 元素或控件，除了提供强大的导航功能之外，还能够公开它们包含的任何文本的详细的属性信息。  
  
 如果控件缺少对任何特定特性的支持，则 <xref:System.Windows.Automation.TextPattern> 提供程序不需要支持所有的文本特性。  
  
 如果控件支持在文本区域（或系统插入标记）内的文本选择或位置，则 <xref:System.Windows.Automation.TextPattern> 提供程序必须支持 <xref:System.Windows.Automation.TextPattern.GetSelection%2A> 和 <xref:System.Windows.Automation.Text.TextPatternRange.Select%2A> 函数。 如果该控件不支持此功能，则它不必支持上述任一方法。 但是，该控件必须通过执行 <xref:System.Windows.Automation.Provider.ITextProvider.SupportedTextSelection%2A> 属性公开其支持的文本选择类型。  
  
 一个 <xref:System.Windows.Automation.TextPattern> 提供程序必须始终支持 <xref:System.Windows.Automation.Text.TextUnit> 常量 <xref:System.Windows.Automation.Text.TextUnit> 和 <xref:System.Windows.Automation.Text.TextUnit> 及其支持的任何其他 <xref:System.Windows.Automation.Text.TextUnit> 常量。  
  
> [!NOTE]
>  提供程序可以跳过某一特定 <xref:System.Windows.Automation.Text.TextUnit> 的支持，只需通过按如下顺序延迟到下一个受支持的最大 <xref:System.Windows.Automation.Text.TextUnit>：<xref:System.Windows.Automation.Text.TextUnit><xref:System.Windows.Automation.Text.TextUnit><xref:System.Windows.Automation.Text.TextUnit><xref:System.Windows.Automation.Text.TextUnit>、<xref:System.Windows.Automation.Text.TextUnit>、<xref:System.Windows.Automation.Text.TextUnit> 和 <xref:System.Windows.Automation.Text.TextUnit>。  
  
|||  
|-|-|  
|`ITextProvider Interface`|公开在客户端应用程序中支持 <xref:System.Windows.Automation.TextPattern> 的方法、属性和特性（请参阅 <xref:System.Windows.Automation.Provider.ITextProvider>）。|  
|`ITextRangeProvider Interface`|表示文本提供程序中的一段文本（请参阅 <xref:System.Windows.Automation.Provider.ITextRangeProvider>）。|  
|`System.Windows.Automation.TextPatternIdentifiers Class`|包含用作文本提供程序标识符的值（请参阅 <xref:System.Windows.Automation.TextPatternIdentifiers>）。|  
  
<a name="Security"></a>   
## 安全性  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 体系结构的设计考虑到了安全性（请参阅 [UI Automation Security Overview](../../../docs/framework/ui-automation/ui-automation-security-overview.md)）。 但是，此概述中所述的 TextPattern 类需要一些特定的安全注意事项。  
  
-   [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 文本提供程序提供只读接口，并且不提供能够更改控件中的现有文本的功能。  
  
-   如果 UI 自动化客户端是完全“信任”的，则 UI 自动化客户端只能使用 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)]。 此示例将为受保护的登录桌面，只有已知和受信任的应用程序可以运行。  
  
-   UI 自动化提供程序的开发人员应注意：所有他们选择通过 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 在控件中公开的信息实质上是公用的并且其他代码都可访问。[!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 不会尝试确定任何 UI 自动化客户端的可信度，因此 UI 自动化提供程序不应公开受保护内容或敏感文本信息（如密码字段）。  
  
-   [!INCLUDE[TLA#tla_winvista](../../../includes/tlasharptla-winvista-md.md)] 安全性最重要的更改之一是：广泛地称为“安全输入”，其包括如最低特权（或有限权限）、用户帐户 \(LUA\) 和用户界面特权级别隔离 \(UIPI\) 在内的技术。  
  
    -   UIPI 防止一个程序控制和\/或监控另一个具有更多“特权”的程序，防止欺骗用户输入的跨进程窗口消息攻击。  
  
    -   LUA 对 Administrators 组中的用户正在运行的应用程序的权限进行限制设置。 应用程序不一定具有管理员权限，但将以必需的最低权限运行。 因此，可能会在 LUA 方案中强制执行一些限制。 最值得注意的字符串截断（包括 TextPattern 字符串），可能有必要限制从管理员级别的应用程序检索的字符串的大小，因此它们不会被强制将内存分配给禁用该应用程序的点。  
  
<a name="Performance"></a>   
## 性能  
 由于 TextPattern 依赖于跨进程调用其大多数功能，处理内容时，它不提供缓存机制来提高性能。 这与其他可以使用 <xref:System.Windows.Automation.AutomationElement.GetCachedPattern%2A> 或 <xref:System.Windows.Automation.AutomationElement.TryGetCachedPattern%2A> 方法访问的 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 中的控件模式不同。  
  
 改善性能的一种策略是通过确保 UI 自动化客户端使用 <xref:System.Windows.Automation.Text.TextPatternRange.GetText%2A> 尝试检索中等规模的文本块。 例如，GetText\(1\) 调用将对每个字符产生跨进程命中，而一次 GetText\(\-1\) 调用将产生一次跨进程命中，但根据文本提供程序的大小，可以具有高延时。  
  
<a name="Glossary"></a>   
## TextPattern 术语  
 **特性**  
 文本范围的格式特性（例如，<xref:System.Windows.Automation.TextPattern.IsItalicAttribute> 或 <xref:System.Windows.Automation.TextPattern.FontNameAttribute>）。  
  
 **退化范围**  
 退化范围为空或零字符文本区域。 出于 TextPattern 控件模式的目的，文本插入点（或系统插入标记）被视为退化范围。 如果未选择文本，<xref:System.Windows.Automation.TextPattern.GetSelection%2A> 将返回文本插入点处的退化范围，<xref:System.Windows.Automation.TextPattern.RangeFromPoint%2A> 将返回退化范围作为其起始终结点。 文本提供程序找不到任何与给定条件相匹配的文本范围时，<xref:System.Windows.Automation.TextPattern.RangeFromChild%2A> 和 <xref:System.Windows.Automation.TextPattern.GetVisibleRanges%2A> 可能会返回退化范围。 此退化范围可用作文本提供程序内的起始终结点。<xref:System.Windows.Automation.Text.TextPatternRange.FindText%2A> 和 <xref:System.Windows.Automation.Text.TextPatternRange.FindAttribute%2A> 返回空引用（[!INCLUDE[TLA2#tla_visualbnet](../../../includes/tla2sharptla-visualbnet-md.md)] 中的 `Nothing`），以避免与发现范围和退化范围相混淆。  
  
 **嵌入式对象**  
 在 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 文本模型中，有两种类型的嵌入对象。 它们包含基于文本的内容元素，如超链接或表，以及控制元素（如图像和按钮）。 有关详细信息，请参见[Access Embedded Objects Using UI Automation](../../../docs/framework/ui-automation/access-embedded-objects-using-ui-automation.md)。  
  
 **终结点**  
 文本容器内的文本范围的绝对 <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint> 或 <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint> 点。  
  
 ![TextPatternRangeEndpoints（开始和结束）。](../../../docs/framework/ui-automation/media/uia-textpattern-endpoints.PNG "UIA\_TextPattern\_Endpoints")  
下面显示了一套起始点和终结点。  
  
 **TextRange**  
 表示包括所有的相关特性和功能的文本容器中带起始点和终结点的一段文本。  
  
 <xref:System.Windows.Automation.Text.TextUnit>  
 用于导航文本范围的逻辑分段的预定义文本单元（字符、单词、行或段落）。  
  
## 请参阅  
 [UI Automation Control Patterns for Clients](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)   
 [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)   
 [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)   
 [Use Caching in UI Automation](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)   
 [Support Control Patterns in a UI Automation Provider](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)   
 [Control Pattern Mapping for UI Automation Clients](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md)   
 [文本服务框架](http://msdn.microsoft.com/library/default.asp?url=/library/tsf/tsf/text_services_framework.asp)