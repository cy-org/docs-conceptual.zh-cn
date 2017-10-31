---
title: "WCF 中的事件日志记录 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "事件日志记录 [WCF]"
ms.assetid: aac0530d-f44c-45a1-bada-e30e0677b41f
caps.latest.revision: 22
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 22
---
# WCF 中的事件日志记录
[!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 在 Windows 事件日志中跟踪内部事件。  
  
## 查看事件日志  
 默认情况下自动启用事件日志记录，并且没有禁用它的机制。[!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 记录的事件可以使用事件查看器来查看。若要启动此工具，请单击**“开始”**，再单击**“控制面板”**，双击**“管理工具”**，再双击**“事件查看器”**。  
  
### 应用程序事件日志  
 **“应用程序事件日志”**包含 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 生成的大部分事件。大多数项都指示未能为应用程序启用某个功能。示例包括：  
  
-   消息日志记录\/跟踪：当跟踪和消息日志记录失败时，[!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 会将事件写入事件日志。但是，并非每个跟踪故障都会触发事件。为防止事件日志被跟踪故障完全填满，[!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 为此类事件实现一个 10 分钟中断周期。这意味着，如果 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 向事件日志中写入跟踪故障，则至少在 10 分钟内它不会再次进行写入。  
  
-   共享侦听器：WCF TCP 端口共享服务在未能启动时将记录一个事件。  
  
-   [!INCLUDE[infocard](../../../../../includes/infocard-md.md)]：当服务未能启动时记录一个事件。  
  
-   严重和错误事件，如启动故障或崩溃  
  
-   消息日志记录打开：当消息日志记录打开时记录事件。这将通知管理员可能在消息头和正文中记录应用程序特定的敏感信息。  
  
-   当设置 `machine.config` 文件的 `machineSettings` 元素中的 `enableLoggingKnownPII` 属性时，将记录一个事件。此属性指定是否允许计算机上运行的任何应用程序来记录已知的个人身份信息 \(PII\)。  
  
-   如果为特定应用程序将 `app.config` 或 `web.config` 文件中的 `logKnownPii` 属性设置为 `true` 以开启 PII 日志记录，但 `machine.config` 文件的 `machineSettings` 元素中的 `enableLoggingKnownPII` 属性设置为 `false`，则会记录一个事件。此外，如果将 `logKnownPii` 和 `enableLoggingKnownPII` 都设置为 `true`，也会记录一个事件。有关这些配置设置的更多信息，请参见[配置消息日志记录](../../../../../docs/framework/wcf/diagnostics/configuring-message-logging.md)主题的“安全性”一节。  
  
### 安全事件日志  
 **“安全事件日志”**包含由 WCF 记录的安全审核事件。  
  
### 系统事件日志  
 WCF 不在**“系统事件日志”**中记录任何内容。  
  
### 事件日志项  
 事件的**“源”**是生成日志项的程序集的名称。  
  
 事件日志项的类型用于指示事件的严重性。每个事件必须属于一种类型，应用程序在报告事件时将指示该类型。事件查看器使用该类型来确定在日志的列表视图中显示哪一个图标。有关事件日志项的不同事件类型，请参见 <xref:System.Diagnostics.EventLogEntryType>。  
  
 在事件查看器中查看事件时，如果单击“更多信息”，则事件查看器可能会通过 Internet 发送信息。有关更多信息，请参见事件查看器帮助。  
  
## 请参阅  
 [管理和诊断](../../../../../docs/framework/wcf/diagnostics/index.md)   
 [事件常规参考](../../../../../docs/framework/wcf/diagnostics/event-logging/events-general-reference.md)