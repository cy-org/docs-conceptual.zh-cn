---
title: "文档审批过程 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9b240937-76a7-45cd-8823-7f82c34d03bd
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# 文档审批过程
此示例演示如何将很多 [!INCLUDE[wf](../../../../includes/wf-md.md)] 功能和 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 功能一起使用。这些功能一起使用实现一个文档审批过程方案。客户端应用程序既可提交等待审批的文档，也可批准文档。有一个审批管理器应用程序，可用于促进客户端之间的通信和强制执行审批过程的规则。审批过程是一个可执行多种类型的审批的工作流。存在多个活动来获取个人审批过程、团体审批过程（一定百分比的审批者）和复合审批过程（由团体审批和个人审批按顺序组成）。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Application\DocumentApprovalProcess`  
  
## 示例详细信息  
 下图演示文档审批过程工作流。  
  
 ![文档审批进程工作流](../../../../docs/framework/windows-workflow-foundation/samples/media/approvalprocess.jpg "ApprovalProcess")  
  
 从客户端的角度来看，审批过程的工作方式如下：  
  
1.  客户端申请成为审批过程系统中的用户。  
  
2.  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端发送到审批管理器应用程序承载的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务。  
  
3.  将唯一的用户 ID 返回到客户端。此时，客户端可参与审批过程。  
  
4.  客户端在加入后可发送文档以通过个人审批过程、团体审批过程或复合审批过程进行审批。  
  
5.  单击客户端界面中的按钮，在客户端工作流服务主机中启动工作流实例。  
  
6.  工作流将审批请求发送到审批管理器应用程序。  
  
7.  工作流管理器启动其自身的工作流以表示审批过程。  
  
8.  一旦执行管理器审批工作流，就会将结果发送回客户端。  
  
9. 客户端显示结果。  
  
10. 客户端可以随时接收审批请求并对其做出响应。  
  
11. 客户端上承载的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务可接收来自审批管理器应用程序的审批请求。  
  
12. 客户端上将呈现文档信息以供审阅。  
  
13. 用户可以批准或拒绝文档。  
  
14. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端用于将审批响应发送回审批管理器应用程序。  
  
 从审批管理器应用程序的角度来看，审批过程的工作方式如下：  
  
1.  客户端请求加入审批过程系统。  
  
2.  审批管理器上的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务接收针对成为审批过程系统的一部分而提出的请求。  
  
3.  为客户端生成唯一的 ID。将用户信息存储在数据库中。  
  
4.  将唯一的 ID 发送回用户。  
  
5.  接收审批请求。审批管理器执行审批过程。  
  
6.  审批管理器接收审批请求，启动新的工作流。  
  
7.  根据请求的类型（个人、团体或复合）来执行不同的活动。  
  
8.  发送和接收相关的活动，这些活动用于向客户端发送供审阅的审批请求和从客户端接收响应。  
  
9. 将审批过程工作流的结果发送到客户端。  
  
## 使用示例  
  
##### 安装数据库  
  
1.  从使用管理员特权打开的 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 命令提示中，导航到此 DocumentApprovalProcess 文件夹并运行 Setup.cmd。  
  
##### 设置应用程序  
  
1.  使用 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 打开 DocumentApprovalProcess.sln 解决方案文件。  
  
2.  要生成解决方案，按 Ctrl\+Shift\+B。  
  
3.  若要运行解决方案，请通过右击**“解决方案资源管理器”**中的 ApprovalManager 项目并从右击菜单中单击**“调试”**\-\>**“启动新实例”**，启动审批管理器应用程序。  
  
     等待管理器的输出指示已做好准备工作。  
  
##### 运行个人审批方案  
  
1.  使用管理员权限打开命令提示符。  
  
2.  导航到包含解决方案的目录。  
  
3.  导航到 ApprovalClient\\Bin\\Debug 文件夹并执行两个 ApprovalClient.exe 实例。  
  
4.  单击**“discover”（发现）**，然后等待**“subscribe”（订阅）**按钮启用。  
  
5.  键入任意用户名，然后单击**“subscribe”（订阅）**。对于一个客户端，使用 `UserType1` 和其他类型 `UserType2`。  
  
6.  在 `UserType1` 客户端中，从下拉菜单中选择个人审批类型，然后键入文档名称和内容。单击**“Request Approval”（请求审批）**。  
  
7.  在 `UserType2` 客户端中，将显示等待审批的文档。选择该文档，然后按**“approve”（批准）**或**“reject”（拒绝）**。结果将显示在 `UserType1` 客户端中。  
  
##### 运行团体审批方案  
  
1.  使用管理员权限打开命令提示符。  
  
2.  导航到包含解决方案的目录。  
  
3.  导航到 ApprovalClient\\Bin\\Debug 文件夹并执行三个 ApprovalClient.exe 实例。  
  
4.  单击**“discover”（发现）**，然后等待**“subscribe”（订阅）**按钮启用。  
  
5.  键入任意用户名，然后单击**“subscribe”（订阅）**。对于一个客户端，使用 `UserType1` 和其他两个类型 `UserType2`。  
  
6.  在 `UserType1` 客户端中，从下拉菜单中选择团体审批类型，然后键入文档名称和内容。单击**“Request Approval”（请求审批）**。这将请求两个 `UserType2` 客户端批准或拒绝该文档。虽然两个 `UserType2` 客户端都必须做出响应，但只需一个客户端批准文档即可使文档获得审批。  
  
7.  在 `UserType2` 客户端中，将显示等待审批的文档。选择该文档，然后按**“approve”（批准）**或**“reject”（拒绝）**。结果将显示在 `UserType1` 客户端中。  
  
##### 运行复合审批方案  
  
1.  使用管理员权限打开命令提示符。  
  
2.  导航到包含解决方案的目录。  
  
3.  导航到 ApprovalClient\\Bin\\Debug 文件夹并执行四个 ApprovalClient.exe 实例。  
  
4.  单击**“discover”（发现）**，然后等待**“subscribe”（订阅）**按钮启用。  
  
5.  键入任意用户名，然后单击**“subscribe”（订阅）**。为第一个客户端使用 `UserType1`，为第二个客户端使用 `UserType2`，为最后一个客户端使用 `UserType3`。  
  
6.  在 `UserType1` 客户端中，从下拉菜单中选择个人审批类型，然后键入文档名称和内容。单击**“Request Approval”（请求审批）**。  
  
7.  在 `UserType2` 客户端中，将显示等待审批的文档。选择该文档并按**“approve”（批准）**，该文档将会传递到 `UserType3` 客户端。  
  
     如果第一个 `UserType2` 团体批准该文档，则该文档将传递到 `UserType3` 客户端。  
  
8.  批准或拒绝来自 `UserType3` 客户端的文档。结果将显示在 `UserType1` 客户端中。  
  
##### 清理  
  
1.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 命令提示符下，导航到 DocumentApprovalProcess 文件夹并运行 Cleanup.cmd。  
  
## 请参阅