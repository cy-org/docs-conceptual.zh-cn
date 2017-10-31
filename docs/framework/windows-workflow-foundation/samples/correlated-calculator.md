---
title: "相关计算器 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c365166e-6552-49a4-bf17-9f4e597d4d41
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 相关计算器
此示例演示如何基于消息中的参数，将设计器中的消息传递活动（<xref:System.ServiceModel.Activities.Receive> 和 <xref:System.ServiceModel.Activities.SendReply>）与基于内容的相关性一起使用。在此方案中，计算器的操作在一个并行的队列中。在将第一条消息发送到工作流时，将创建一个实例和一个相关性（基于 `CalculatorId`），后续的具有相同 `CalculatorId` 的消息将被调度到该实例，直到调用 Reset 操作。客户端作为一个 WPF 应用程序实现，它使用基于代码的客户端代理与服务通信。  
  
#### 使用此示例  
  
1.  使用提升的权限启动 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)]，打开 For.sln 解决方案文件。  
  
    1.  导航到包含 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 的文件夹。  
  
    2.  右击 Devenv.exe 并选择**“以管理员身份运行”**。  
  
2.  使用 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 打开 CorrelatedCalculator.sln 解决方案文件。  
  
3.  要生成解决方案，按 Ctrl\+Shift\+B。  
  
4.  若要运行服务项目，请按 Ctrl\+F5。  
  
5.  在服务准备就绪并开始侦听消息之后，在“解决方案资源管理器”中右击“Client”项目，并运行它。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>：\WF_WCF_Samples\WF\Scenario\Services\CorellatedCalculator`  
  
## 请参阅