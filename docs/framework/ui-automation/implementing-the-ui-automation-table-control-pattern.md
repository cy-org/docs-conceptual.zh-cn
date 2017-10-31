---
title: "实现 UI 自动化 Table 控件模式 | Microsoft Docs"
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
  - "UI 自动化 Table 控件模式"
  - "控件模式表"
  - "TableControl 模式"
ms.assetid: 880cd85c-aa8c-4fb5-9369-45491d34bb78
caps.latest.revision: 19
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 18
---
# 实现 UI 自动化 Table 控件模式
> [!NOTE]
>  本文档适用于.NET Framework 开发人员想要使用托管[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]中定义的类<xref:System.Windows.Automation>命名空间。 有关最新信息[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]，请参阅[Windows 自动化 API: UI 自动化](http://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本主题介绍的实现准则和约定<xref:System.Windows.Automation.Provider.ITableProvider>，包括属性、 方法和事件有关的信息。 本概述的结尾列出了指向其他参考资料的链接。  
  
 <xref:System.Windows.Automation.TablePattern>控件模式用于支持作为容器的子元素的集合的控件。 此元素的子级必须实现<xref:System.Windows.Automation.Provider.ITableItemProvider>和组织可以按行和列进行遍历二维逻辑坐标系统中。 此控件模式相当于<xref:System.Windows.Automation.Provider.IgridProvider>，与任何控件实现的区别<xref:System.Windows.Automation.Provider.ITableProvider>还必须公开的每个子元素的列和/或行标题关系。 实现此控件模式的控件的示例，请参阅[UI 自动化客户端控件模式映射](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md)。  
  
<a name="Implementation_Guidelines_and_Conventions"></a>   
## <a name="implementation-guidelines-and-conventions"></a>实现准则和约定  
 在实现 Table 控件模式时，请注意以下准则和约定：  
  
-   对各个单元格的内容的访问是通过二维逻辑坐标系统或提供的必需的并发实现数组<xref:System.Windows.Automation.Provider.IGridProvider>。  
  
-   列或行标头可包含在表对象中或可以为与表对象相关联的单独标头对象。  
  
-   列和行标头可能包含主标头以及任何支持的标头。  
  
> [!NOTE]
>  这一概念将变得显而易见中[!INCLUDE[TLA#tla_xl](../../../includes/tlasharptla-xl-md.md)]电子表格用户已在其中定义的"名字"列。 此列现在有两个标头 — 用户定义的“名字”标头和应用程序分配的该列的字母数字名称。  
  
-   请参阅[实现 UI 自动化 Grid 控件模式](../../../docs/framework/ui-automation/implementing-the-ui-automation-grid-control-pattern.md)了解相关的网格功能。  
  
 ![具有复杂标题项的表。](../../../docs/framework/ui-automation/media/uia-tablepattern-complex-column-headers.PNG "UIA_TablePattern_Complex_Column_Headers")  
具有复杂列标头的表示例  
  
 ![具有不明确的 RowOrColumnMajor 属性的表。](../../../docs/framework/ui-automation/media/uia-tablepattern-roworcolumnmajorproperty.PNG "UIA_TablePattern_RowOrColumnMajorProperty")  
具有不明确的 RowOrColumnMajor 属性的表示例。  
  
<a name="Required_Members_for_ITableProvider"></a>   
## <a name="required-members-for-itableprovider"></a>ITableProvider 必需的成员  
 ITableProvider 接口需要以下属性和方法。  
  
|必需的成员|成员类型|备注|  
|----------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.Provider.ITableProvider.RowOrColumnMajor%2A>|属性|无|  
|<xref:System.Windows.Automation.Provider.ITableProvider.GetColumnHeaders%2A>|方法|无|  
|<xref:System.Windows.Automation.Provider.ITableProvider.GetRowHeaders%2A>|方法|无|  
  
 没有与此控件模式关联的事件。  
  
<a name="Exceptions"></a>   
## <a name="exceptions"></a>异常  
 没有与此控件模式关联的异常。  
  
## <a name="see-also"></a>另请参阅  
 [UI 自动化控件模式概述](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)   
 [在 UI 自动化提供程序中支持控件模式](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)   
 [客户端 UI 自动化控件模式](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)   
 [实现 UI 自动化 TableItem 控件模式](../../../docs/framework/ui-automation/implementing-the-ui-automation-tableitem-control-pattern.md)   
 [实现 UI 自动化 Grid 控件模式](../../../docs/framework/ui-automation/implementing-the-ui-automation-grid-control-pattern.md)   
 [UI 自动化树概述](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)   
 [在 UI 自动化中使用缓存](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)