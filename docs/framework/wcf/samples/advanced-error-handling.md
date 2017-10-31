---
title: "高级错误处理 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ed54b687-78af-4eda-8507-9fd081bdea1a
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# 高级错误处理
此示例演示 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 路由服务。  路由服务是一个 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 组件，使用该组件可方便地在应用程序中包含基于内容的路由器。  此示例使用事务和其他更加复杂的消息传递概念（如多播）演示如何智能地将路由服务从错误中恢复过来。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。  在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。  此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\RoutingServices\AdvancedErrorHandling`  
  
## 示例详细信息  
 在此示例中，路由服务配置为从 MSMQ 队列读取一个消息并将此消息多播到两个队列列表。  一个列表用于服务队列，另一个用于日志记录队列。  
  
 因为在默认情况下，为路由服务配置的 MSMQ 绑定支持使用事务，所以路由服务可确保在向入站队列 \(`InQ`\) 报告消息已成功路由之前，消息是事务性的且由每个列表中的至少一个队列接收。  因此，在两个服务队列或两个日志记录队列都不可用时，路由服务报告消息无法路由，入站队列应采取某种操作。  此操作包含将消息移动至系统死信队列。  
  
#### 使用此示例  
  
1.  > [!IMPORTANT]
    >  在运行此示例之前安装 MSMQ。  如果未安装 MSMQ，会在运行该示例时返回异常消息。  在[安装消息队列 \(MSMQ\)](http://go.microsoft.com/fwlink/?LinkId=166437)（可能为英文网页）上，可以找到有关安装 MSMQ 的说明。  
  
     使用 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 打开 AdvancedErrorHandling.sln。  
  
2.  在 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 中按**“F5”**或**“Ctrl\+Shift\+B”**。  
  
    1.  如果使用 Ctrl\+Shift\+B 生成应用程序，则必须用 .\/RoutingService\/bin\/debug\/RoutingService.exe 启动应用程序。  
  
3.  在控制台窗口中，按 Enter 启动客户端。  
  
4.  客户端针对每种情况返回不同的有关队列的统计信息。  
  
    1.  下面是针对情况 1（无故障）返回的输出。  
  
        ```Output  
  
                            入站队列有 0 个消息。  
  
        主服务队列有 1 个消息。  
  
        备份服务队列有 0 个消息。  
  
        主日志记录队列有 1 个消息。  
  
        备份日志记录队列有 0 个消息。  
  
        按 <Enter> 继续  
  
        ```  
  
    2.  下面是针对情况 3（主服务和日志记录队列故障）返回的输出。  
  
        ```Output  
  
        入站队列有 0 个消息。  
  
        主服务队列不存在。  
  
        备份服务队列有 1 个消息。  
  
        主日志记录队列不存在。  
  
        备份日志记录队列有 1 个消息。  
  
        按 <Enter> 继续。  
  
        ```  
  
    3.  下面是针对情况 4（主服务队列以及主和备份日志记录队列故障）返回的输出。  
  
        ```Output  
  
                            入站队列有 0 个消息。  
  
        主服务队列不存在。  
  
        备份服务队列有 0 个消息。  
  
        主日志记录队列不存在。  
  
        备份日志记录队列不存在。  
  
        系统死信队列有 1 个消息。  
  
        按 <Enter> 退出。  
  
        ```  
  
    4.  下面是针对情况 2（主服务队列故障）返回的输出。  
  
        ```Output  
  
                            入站队列有 0 个消息。  
  
        主服务队列不存在。  
  
        备份服务队列有 1 个消息。  
  
        主日志记录队列有 1 个消息。  
  
        备份日志记录队列有 0 个消息。  
  
        按 <Enter> 继续。  
  
        ```  
  
## 可通过代码或 App.config 配置  
 所提供的示例配置为使用 App.config 文件来定义路由器行为。  还可以将 RoutingService\\App.config 文件的名称更改为其他名称，使之无法识别，并在 RoutingService\\Program.cs 中将 `configDriven` 字段的值更改为 `false`，以便使用代码中定义的配置。  以上任一方法都可产生相同的路由器行为。  
  
### 方案  
 此示例演示路由服务可以处理高级消息传递功能（如事务和接收上下文），并且可以将这些功能用作正确处理错误方案的一部分。  
  
### 实际方案  
 Contoso 希望通过路由服务利用事务性接收，以确保即使在出现错误的情况下，所有必要服务也可接收信息。  此外，还希望在无法传递消息时，即使利用错误处理逻辑，也可自动地正确处理错误并报告失败。  为此，将路由服务配置为按预期方式故障转移到特定终结点，并且路由服务处理错误情况，具体包括根据需要创建、完成和回滚\/中止事务\/接收上下文。  
  
## 请参阅  
 [AppFabric 承载和持久性示例 （可能为英文网页）](http://go.microsoft.com/fwlink/?LinkId=193961)