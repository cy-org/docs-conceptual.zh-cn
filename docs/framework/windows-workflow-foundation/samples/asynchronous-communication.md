---
title: "异步通信 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 128dc092-9eb2-4e33-9470-9a7f62b60df6
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 异步通信
此示例演示默认情况下如何异步执行两个不同的 [!INCLUDE[wf](../../../../includes/wf-md.md)] 服务间的通信。  
  
## 演示  
 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 服务间的异步通信。  
  
## 讨论  
 此示例演示如何使用 .NET Framework 提供的消息传递活动来异步执行 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 应用程序间的通信。  
  
 此示例包含以下三个项目。  
  
 CreditCheckService  
 此服务接收特定人员的信用评分或要购买的商品的价值，然后决定是否为该人员提供贷款。  
  
 RentalApprovalService  
 此服务接收来自需要贷款的人员的申请。此服务与 `CreditCheckService` 进行异步通信以决定贷款申请是否有效。  
  
 Client  
 此客户端与 `RentalApprovalService` 进行同步通信以了解是否已批准贷款。  
  
#### 设置、生成和运行示例  
  
1.  右击**“AsynchronousCommunication”**解决方案并选择**“属性”**。  
  
2.  在**“通用属性”**中，选择**“启动项目”**，然后选择**“多启动项目”**。  
  
3.  将**“RentalApprovalService”**移动到列表中的第一个位置，后跟**“CreditCheckService”**，再后跟**“Client”**。对所有三个项目设置**“启动”**操作。  
  
4.  单击**“确定”**并按 F5 运行示例。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Scenario\Services\AsynchronousCommunication`