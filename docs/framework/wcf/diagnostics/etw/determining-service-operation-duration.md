---
title: "确定服务操作持续时间 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e8a93a2c-2c20-48b3-8986-57e90e9aa908
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 确定服务操作持续时间
如果在 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 应用程序中启用了分析跟踪，则通过检查事件日志可方便地确定服务操作的执行持续时间。  本主题演示如何确定完成服务操作所需的时间量。  
  
### 确定服务操作执行持续时间  
  
1.  通过单击**“开始”**、**“运行”**并输入 `eventvwr.exe` 来打开事件查看器。  
  
2.  如果尚未启用分析跟踪，请展开**“应用程序和服务日志”**、**“Microsoft”**、**“Windows”**、**“应用程序服务器”\-\>“应用程序”**。  选择**“视图”**、**“显示分析和调试日志”**。  右击**“分析”**，然后选择**“启用日志”**。  保持事件查看器打开，以便在服务操作运行后可以查看跟踪。  
  
3.  接下来，打开 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 应用程序，其中包含一个服务项目以及一个与该服务交互的客户端项目。  可以按照[入门教程](../../../../../docs/framework/wcf/getting-started-tutorial.md)中的说明创建这样一个应用程序。  如果安装了 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 示例，则可以打开[入门](../../../../../docs/framework/wcf/samples/getting-started-sample.md)，其中包含本教程中创建的完整项目。  
  
4.  按**“F5”**执行服务器应用程序。  通过右击**“客户端”**项目并选择**“调试”**、**“启动新实例”**，来执行客户端应用程序。  
  
5.  在事件查看器中，刷新分析日志，然后按事件 ID 对事件排序。  查找事件 ID 为 [214 \- OperationCompleted](../../../../../docs/framework/wcf/diagnostics/etw/214-operationcompleted.md) 的事件。  这些事件将显示已完成的操作以及操作的持续时间。  下面的事件显示 Add 操作的持续时间。  
  
    ```Output  
  
    OperationInvoker 已完成对“Add”方法的调用。  该方法调用持续了 3 毫秒。    
    ```