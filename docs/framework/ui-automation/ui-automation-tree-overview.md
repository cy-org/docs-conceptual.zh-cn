---
title: "UI 自动化树概述 | Microsoft Docs"
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
  - "自动化树"
  - "UI 自动化、 树"
ms.assetid: 03b98058-bdb3-47a0-8ff7-45e6cdf67166
caps.latest.revision: 25
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 25
---
# UI 自动化树概述
> [!NOTE]
>  本文档适用于.NET Framework 开发人员想要使用托管[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]中定义的类<xref:System.Windows.Automation>命名空间。 有关最新信息[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]，请参阅[Windows 自动化 API: UI 自动化](http://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 辅助技术产品和测试脚本，用于定位[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]树，以收集下列相关信息[!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)]及其元素。  
  
 在[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]有树是根元素 (<xref:System.Windows.Automation.AutomationElement.RootElement%2A>)，它表示当前的桌面，并且其子元素表示应用程序窗口。 每个这些子元素可以包含元素表示条[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]菜单、 按钮、 工具栏和列表框等。 这些子元素又可以包含列表项之类的元素。  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]树固定的结构并不因为它可能包含数千个元素很少显示出来。 可以根据需要生成树的某些部分，添加、移动或删除元素时，树也会发生相应更改。  
  
 UI 自动化提供程序都支持[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]通过实现一个片段，其中包含一个根目录 （通常承载在窗口中） 和一个子树中各项之间的导航树。 但是，提供程序并不参与控件之间的导航。 这由[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]核心，使用默认窗口提供程序中的信息。  
  
<a name="uiautomation_tree_view"></a>   
## <a name="views-of-the-automation-tree"></a>自动化树的视图  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]树可以进行筛选，以创建视图仅包含那些<xref:System.Windows.Automation.AutomationElement>适用于特定客户端的对象。 此方法允许客户端自定义结构通过显示[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]于其特定需要。  
  
 客户端可以通过以下两种方法来自定义视图：设置范围和筛选。 设置范围是指从基元素开始定义视图的范围，例如，应用程序可能希望仅查找桌面的直接子级，或者查找某个应用程序窗口的所有后代。 筛选是指定义要包括在视图中的元素类型。  
  
 UI 自动化提供程序支持通过在元素，其中包括上定义属性进行筛选<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>和<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>属性。  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]提供了三个默认视图。 这些视图由所执行筛选的类型定义；任何视图的范围都是由应用程序定义的。 另外，应用程序可以向属性应用其他筛选器，例如，在控件视图中仅包含已启用的控件。  
  
<a name="uiautomation_raw_view"></a>   
### <a name="raw-view"></a>原始视图  
 原始视图[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]树是完整的<xref:System.Windows.Automation.AutomationElement>桌面的根的对象。 原始视图完全遵循应用程序的本机编程结构，因此是最详细的可用视图。 原始视图还是其他树视图的生成基础。 因为该视图依赖于基础[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]框架、 的原始视图[!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)]按钮都将具有不同的原始视图比[!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)]按钮。  
  
 原始视图获取通过搜索而无需指定属性的元素或使用<xref:System.Windows.Automation.TreeWalker.RawViewWalker>若要在树中导航。  
  
<a name="uiautomation_control_view"></a>   
### <a name="control-view"></a>控件视图  
 控件视图[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]树简化了辅助技术产品的任务描述[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]对最终用户和帮助最终用户的应用程序交互由于紧密映射到[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]最终用户感觉到的结构。  
  
 控件视图是原始视图的子集。 它包括所有[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]项从最终用户能够看懂为交互式或相关的控件中的逻辑结构的原始视图[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]。 示例[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]项构成的逻辑结构[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]，但不是交互式自己，是项的容器，如列表视图页眉、 工具栏、 菜单和状态栏。 仅针对布局或修饰目的而使用的非交互式项将不会显示在控件视图中。 仅为了将控件放置在对话框中而本身不包含任何信息的面板就是这样的项。 对话框中包含信息和静态文本的图形是在控件视图中显示的非交互式项。 控件视图中包括的非交互式项不能接收键盘焦点。  
  
 控件视图获取通过搜索具有的元素的<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.IsControlElement%2A>属性设置为`true`，或通过使用<xref:System.Windows.Automation.TreeWalker.ControlViewWalker>若要在树中导航。  
  
<a name="uiautomation_content_view"></a>   
### <a name="content-view"></a>内容视图  
 内容视图[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]树是控件视图的子集。 它包含[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]传达在用户界面，真正的信息的项包括[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]项可以接收键盘焦点和一些不在一个标签的文本[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]项。 例如，下拉组合框中的值将出现在内容视图中，因为它们表示正由最终用户使用的信息。 在内容视图中，组合框和列表框均表示为一套[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]其中可以选择其中一个，或可能是多个项的项。 由于内容视图旨在显示要呈现给用户的数据或内容，因此，内容视图中不存在如下情况：始终有一项处于打开状态，而另有一项是可以展开和折叠的。  
  
 通过搜索具有的元素获得的内容视图<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.IsContentElement%2A>属性设置为`true`，或通过使用<xref:System.Windows.Automation.TreeWalker.ContentViewWalker>若要在树中导航。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Windows.Automation.AutomationElement>   
 [UI 自动化概述](../../../docs/framework/ui-automation/ui-automation-overview.md)