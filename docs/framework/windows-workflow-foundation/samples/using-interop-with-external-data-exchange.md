---
title: "与外部数据交换结合使用互操作 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 96f6fe26-5305-494f-9119-7748e0c4b3fa
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 与外部数据交换结合使用互操作
可使用 <xref:System.Activities.Statements.Interop> 活动从 [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)] 和 [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] \(WF3\) 中的 [!INCLUDE[wf](../../../../includes/wf-md.md)] 执行活动以及在 [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] \(WF4\) 中的 [!INCLUDE[wf2](../../../../includes/wf2-md.md)] 内执行工作流。此示例演示如何通过使用 WF4 工作流服务中的 <xref:System.Activities.Statements.Interop> 活动配置和运行 WF3 工作流，该工作流使用 <xref:System.Workflow.Activities.ExternalDataExchangeService> 及对应的自定义活动进行方法调用和事件处理。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Migration\ExternalDataExchange`  
  
#### 使用此示例  
  
1.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中打开 ExternalDataExchange.sln 文件。  
  
2.  要生成此示例，按 Ctrl\+Shift\+B。  
  
3.  要运行此示例，按 F5。