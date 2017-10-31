---
title: "在 .NET Framework 4.5 工作流中使用 .NET Framework 3.0 或 .NET Framework 3.5 活动 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6c53fd4c-5dd0-4fb4-ab6b-111302629548
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 在 .NET Framework 4.5 工作流中使用 .NET Framework 3.0 或 .NET Framework 3.5 活动
<xref:System.Activities.Statements.Interop> 活动允许您在 [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)] 工作流中运行 .NET Framework 3.0 [!INCLUDE[wf](../../../../includes/wf-md.md)] 活动。此示例演示如何使用 <xref:System.Activities.Statements.Interop> 活动来将字符串作为参数传递到自定义 [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)] 活动。  
  
## 使用此示例  
  
1.  使用 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 打开 SimpleInterop.sln 解决方案文件。  
  
2.  要生成解决方案，按 Ctrl\+Shift\+B。  
  
3.  若要运行解决方案，请按 Ctrl\+F5。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Migration\SimpleInterop`  
  
## 请参阅