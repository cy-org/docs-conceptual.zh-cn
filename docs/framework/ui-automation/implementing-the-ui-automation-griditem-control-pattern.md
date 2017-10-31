---
title: "实现 UI 自动化 GridItem 控件模式 | Microsoft Docs"
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
  - "GridItem 控件模式"
  - "UI 自动化 GridItem 控件模式"
  - "GridItem 控件模式"
ms.assetid: bffbae08-fe2a-42fd-ab84-f37187518916
caps.latest.revision: 15
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 15
---
# 实现 UI 自动化 GridItem 控件模式
> [!NOTE]
>  本文档适用于.NET Framework 开发人员想要使用托管[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]中定义的类<xref:System.Windows.Automation>命名空间。 有关最新信息[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]，请参阅[Windows 自动化 API: UI 自动化](http://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本主题介绍的实现准则和约定<xref:System.Windows.Automation.Provider.IGridItemProvider>，包括有关属性的信息。 本概述的结尾列出了指向其他参考资料的链接。  
  
 <xref:System.Windows.Automation.GridItemPattern>控件模式用于支持实现的容器的各个子控件<xref:System.Windows.Automation.Provider.IGridProvider>。 实现此控件模式的控件的示例，请参阅[UI 自动化客户端控件模式映射](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md)。  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## <a name="implementation-guidelines-and-conventions"></a>实现准则和约定  
 在实现时<xref:System.Windows.Automation.Provider.IGridProvider>，请注意以下准则和约定︰  
  
-   网格坐标从零开始，左上角单元格坐标为 (0, 0)。  
  
-   合并的单元格将报告其<xref:System.Windows.Automation.Provider.IGridItemProvider.Row%2A>和<xref:System.Windows.Automation.Provider.IGridItemProvider.Column%2A>属性基于其基础的定位单元格如由 UI 自动化提供程序定义。 通常，它将是最左上方的行或列。  
  
-   <xref:System.Windows.Automation.Provider.IGridItemProvider>不提供如合并或拆分单元格网格的活动操作。  
  
-   控制用于实现<xref:System.Windows.Automation.Provider.IGridItemProvider>通常可以遍历 （即，UI 自动化客户端可以移动到相邻的控件） 使用键盘。  
  
<a name="Required_Members_for_IGridItemProvider"></a>   
## <a name="required-members-for-igriditemprovider"></a>IGridItemProvider 必需的成员  
 以下属性和方法所需的实现<xref:System.Windows.Automation.Provider.IGridItemProvider>。  
  
|必需的成员|成员类型|备注|  
|----------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider.Row%2A>|属性|无|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider.Column%2A>|属性|无|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider.RowSpan%2A>|属性|无|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider.ColumnSpan%2A>|属性|无|  
|<xref:System.Windows.Automation.Provider.IGridItemProvider.ContainingGrid%2A>|属性|无|  
  
 没有与此控件模式关联的方法或事件。  
  
<a name="Exceptions"></a>   
## <a name="exceptions"></a>异常  
 没有与此控件模式关联的异常。  
  
## <a name="see-also"></a>另请参阅  
 [UI 自动化控件模式概述](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)   
 [在 UI 自动化提供程序中支持控件模式](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)   
 [客户端 UI 自动化控件模式](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)   
 [实现 UI 自动化 Grid 控件模式](../../../docs/framework/ui-automation/implementing-the-ui-automation-grid-control-pattern.md)   
 [UI 自动化树概述](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)   
 [在 UI 自动化中使用缓存](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)