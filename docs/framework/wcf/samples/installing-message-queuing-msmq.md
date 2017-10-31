---
title: "安装“消息队列 (MSMQ)” | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7ddcd497-3e04-427e-bc04-3610ad98b01e
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# 安装“消息队列 (MSMQ)”
以下过程介绍如何安装“消息队列 4.0”和“消息队列 3.0”。  
  
> [!NOTE]
>  消息队列 4.0 在 [!INCLUDE[wxp](../../../../includes/wxp-md.md)] 和 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 中不可用。  
  
#### 在 Windows Server 2008 or Windows Server 2008 R2 上安装消息队列 4.0  
  
1.  在服务器管理器中，单击**“功能”**。  
  
2.  在**“功能摘要”**下的右窗格中，单击**“添加功能”**。  
  
3.  在生成的窗口中，展开**“消息队列”**。  
  
4.  展开**“消息队列服务”**。  
  
5.  单击**“目录服务集成”**（用于加入域的计算机），然后单击**“HTTP 支持”**。  
  
6.  单击**“下一步”**，然后单击**“安装”**。  
  
#### 在 Windows 7 或 Windows Vista 上安装消息队列 4.0  
  
1.  打开**“控制面板”**。  
  
2.  单击**“程序”**，然后在**“程序和功能”**下单击**“打开或关闭 Windows 功能”**。  
  
3.  展开“Microsoft Message Queue \(MSMQ\) 服务器”，展开“Microsoft Message Queue \(MSMQ\) 服务器核心”，然后选中对应于以下要安装的“消息队列”功能的复选框：  
  
    -   MSMQ Active Directory 域服务集成（用于加入域的计算机）。  
  
    -   MSMQ HTTP 支持。  
  
4.  单击**“确定”**。  
  
5.  如果提示您重新启动计算机，请单击**“确定”**完成安装。  
  
#### 在 Windows XP 和 Windows Server 2003 上安装消息队列 3.0  
  
1.  打开**“控制面板”**。  
  
2.  单击**“添加\/删除程序”**，然后单击**“添加\/删除 Windows 组件”**。  
  
3.  选择“消息队列”并单击**“详细信息”**。  
  
    > [!NOTE]
    >  如果运行的是 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)]，请选择“应用程序服务器”来访问消息队列。  
  
4.  确保在详细信息页上已选中“MSMQ HTTP 支持”选项。  
  
5.  单击**“确定”**退出详细信息页，然后单击**“下一步”**。完成安装。  
  
6.  如果提示您重新启动计算机，请单击**“确定”**完成安装。  
  
## 请参阅  
 [设置说明](../../../../docs/framework/wcf/samples/set-up-instructions.md)