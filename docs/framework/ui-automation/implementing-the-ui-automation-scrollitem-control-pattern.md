---
title: "实现 UI 自动化 ScrollItem 控件模式 | Microsoft Docs"
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
  - "控件模式，滚动项"
  - "UI 自动化 Scroll Item 控件模式"
  - "Scroll Item 控件模式"
ms.assetid: 903bab5c-80c1-44d7-bdc2-0a418893b987
caps.latest.revision: 16
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 16
---
# 实现 UI 自动化 ScrollItem 控件模式
> [!NOTE]
>  本文档适用于.NET Framework 开发人员想要使用托管[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]中定义的类<xref:System.Windows.Automation>命名空间。 有关最新信息[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]，请参阅[Windows 自动化 API: UI 自动化](http://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本主题介绍的实现准则和约定<xref:System.Windows.Automation.Provider.IScrollItemProvider>，包括属性、 方法和事件有关的信息。 本主题的结尾列出了指向其他参考资料的链接。  
  
 <xref:System.Windows.Automation.ScrollItemPattern>控件模式用于支持实现的容器的各个子控件<xref:System.Windows.Automation.Provider.IScrollProvider>。 此控件模式充当子控件与其容器之间的通信通道，以确保容器可以更改其视区内当前可见的内容（或区域）以显示子控件。 实现此控件模式的控件的示例，请参阅[UI 自动化客户端控件模式映射](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md)。  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## <a name="implementation-guidelines-and-conventions"></a>实现准则和约定  
 在实现“滚动项”控件模式时，请注意以下准则和约定：  
  
-   包含在 Window 或 Canvas 控件内的项不需要实现 IScrollItemProvider 接口。 作为替代方法，但是，它们必须公开的有效位置<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>。 这将允许 UI 自动化客户端应用程序，以使用<xref:System.Windows.Automation.ScrollPattern>控制容器以显示子项目上的模式方法。  
  
<a name="Required_Members_for_IScrollItemProvider"></a>   
## <a name="required-members-for-iscrollitemprovider"></a>IScrollItemProvider 必需的成员  
 需要以下方法来实现 IScrollProvider 接口。  
  
|必需的成员|成员类型|备注|  
|----------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.Provider.IScrollItemProvider.ScrollIntoView%2A>|方法|无|  
  
 没有与此控件模式关联的属性或事件。  
  
<a name="Exceptions"></a>   
## <a name="exceptions"></a>异常  
 提供程序必须引发以下异常。  
  
|异常类型|条件|  
|--------------------|---------------|  
|<xref:System.InvalidOperationException>|如果项无法滚动到视图：<br /><br /> -   <xref:System.Windows.Automation.ScrollItemPattern.ScrollIntoView%2A>|  
  
## <a name="see-also"></a>另请参阅  
 [UI 自动化控件模式概述](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)   
 [在 UI 自动化提供程序中支持控件模式](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)   
 [客户端 UI 自动化控件模式](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)   
 [UI 自动化树概述](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)   
 [在 UI 自动化中使用缓存](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)