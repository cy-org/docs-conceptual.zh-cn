---
title: "在工作流服务中设置消息格式 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6d15d44b-20f8-4cb7-bd4f-598c32781ebc
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 在工作流服务中设置消息格式
此示例演示如何在消息传递活动（WF 服务）中使用不同的用户类型。此示例服务是一个简单的费用审批服务，并公开三个操作。`ApproveExpense` 采用数据合同类型，并演示如何使用已知的类型。操作基于消费金额返回 `true` 或 `false`。该操作根据费用金额返回 `ApprovePO`、`true` 或 `false`。如果供应商在已批准的供应商列表中，或者请求来自财务部门（财务部门可以使用任何供应商），`ApprovedVendor` 采用合同类型并返回 `true` 或 `false`。  
  
#### 使用此示例  
  
1.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中加载项目解决方案，然后生成项目。  
  
2.  首先运行 \[解决方案基目录\]\\FormatterService\\bin\\debug\\ 中生成的服务  
  
3.  然后运行 \[解决方案基目录\]\\FormatterClient\\bin\\debug 中生成的客户端应用程序。  
  
4.  客户端对服务调用三个操作，并输出结果。完成后，请按 Enter 退出客户端，然后退出服务。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Services\Formatter`  
  
## 请参阅