---
title: "订阅 UI 自动化事件 | Microsoft Docs"
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
  - "UI 自动化，订阅事件"
  - "订阅 UI 自动化事件"
  - "订阅的事件"
  - "侦听事件"
ms.assetid: b688effa-b3e8-4b05-944d-05ed89a245aa
caps.latest.revision: 16
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 16
---
# 订阅 UI 自动化事件
> [!NOTE]
>  本文档适用于.NET Framework 开发人员想要使用托管[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]中定义的类<xref:System.Windows.Automation>命名空间。 有关最新信息[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]，请参阅[Windows 自动化 API: UI 自动化](http://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 本主题演示如何订阅 UI 自动化提供程序引发的事件。  
  
## <a name="example"></a>示例  
 下面的代码示例为调用控件（如按钮）时引发的事件注册事件处理程序，并在应用程序窗体关闭时删除该事件处理程序。 通过标识事件<xref:System.Windows.Automation.AutomationEvent>作为参数传递给<xref:System.Windows.Automation.Automation.AddAutomationEventHandler%2A>。  
  
 [!code-csharp[UIAClient_snip#101](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#101)]
 [!code-vb[UIAClient_snip#101](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#101)]  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用[!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)]璹綷焦点更改时引发的事件。 事件处理程序将在可在应用程序关闭时调用的方法中注销，或在不再需要 UI 事件通知时注销。  
  
 [!code-csharp[UIAClient_snip#102](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#102)]
 [!code-vb[UIAClient_snip#102](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#102)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Windows.Automation.Automation.AddAutomationEventHandler%2A>   
 <xref:System.Windows.Automation.Automation.RemoveAllEventHandlers%2A>   
 <xref:System.Windows.Automation.Automation.RemoveAutomationEventHandler%2A>   
 [UI 自动化事件概述](../../../docs/framework/ui-automation/ui-automation-events-overview.md)