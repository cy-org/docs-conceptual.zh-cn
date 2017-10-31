---
title: "XAML 激活 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 486760e2-bb10-4ed5-8c02-fe7472498d2d
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# XAML 激活
此示例演示如何在 IIS 中承载声明性工作流。此示例是一个名为 `EchoService` 的基本工作流，它具有一个操作。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果该目录不存在，请转到（下载页）以下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Services\XAMLActivation`  
  
#### 设置、生成和运行示例  
  
1.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中打开 XAMLActivation.sln 解决方案。  
  
2.  按 F5 生成解决方案。  
  
3.  运行 WcfTestClient.exe。在命令提示符下键入：  
  
    1.  cd %SystemDrive%\\Program Files\\Microsoft Visual Studio 10.0\\Common7\\IDE  
  
    2.  运行 WcfTestClient.exe。  
  
4.  通过以下方式设置 WcfTestClient.exe 的服务地址：按 Ctrl\+Shift\+A 并将服务地址设置为 http:\/\/localhost:56133\/Service.xamlx。  
  
5.  执行 echo 操作以测试服务。  
  
6.  使用管理员特权在命令提示中的 DeployToIIS.Bat 在 IIS 中运行服务。  
  
7.  将客户端中的服务地址更新为 http:\/\/localhost\/XAMLActivation\/Service.xamlx，并使用 WcfTestClient.exe 重新测试服务。