---
title: "跟踪和消息日志记录 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "跟踪和日志记录"
ms.assetid: a4f39bfc-3c5e-4d51-a312-71c5c3ce0afd
caps.latest.revision: 53
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 53
---
# 跟踪和消息日志记录
本示例演示如何启用跟踪和消息日志记录。生成的跟踪和消息日志可以使用[服务跟踪查看器工具 \(SvcTraceViewer.exe\)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md) 查看。此示例基于[入门](../../../../docs/framework/wcf/samples/getting-started-sample.md)。  
  
> [!NOTE]
>  本主题的末尾介绍了此示例的设置过程和生成说明。  
  
## 跟踪  
 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 使用 <xref:System.Diagnostics> 命名空间中定义的跟踪机制。在此跟踪模型中，由应用程序实现的跟踪源生成跟踪数据。每个源均由名称进行标识。跟踪使用程序会创建针对要为其检索信息的跟踪源的侦听器。若要接收跟踪数据，您必须创建针对该跟踪源的侦听器。在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中，可通过设置服务模型跟踪源 `switchValue` 并将下面的代码添加到服务或客户端的配置文件中来实现此目的：  
  
```  
<system.diagnostics>  
    <sources>  
      <source name="System.ServiceModel" switchValue="Information,ActivityTracing"  
        propagateActivity="true">  
        <listeners>  
          <add name="xml" />  
        </listeners>  
      </source>  
      <source name="System.ServiceModel.MessageLogging">  
        <listeners>  
          <add name="xml" />  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add initializeData="C:\logs\TracingAndLogging-service.svclog" type="System.Diagnostics.XmlWriterTraceListener"  
        name="xml" />  
    </sharedListeners>  
    <trace autoflush="true" />  
</system.diagnostics>  
```  
  
 有关跟踪源的更多信息，请参见[配置跟踪](../../../../docs/framework/wcf/diagnostics/tracing/configuring-tracing.md)主题中的“跟踪源”一节。  
  
## 活动跟踪和传播  
 在客户端和服务的 `system.ServiceModel` 跟踪源中启用 `ActivityTracing` 并将 `propagateActivity` 设置为 `true` 可在逻辑处理单元（活动）内、在终结点内的多个活动（通过活动传输）之间和在跨多个终结点的多个活动（通过活动 ID 传播）之间关联跟踪。  
  
 这三种机制（活动、传输和传播）可帮助您使用服务跟踪查看器工具更快地找到错误的根源。有关更多信息，请参见[使用服务跟踪查看器查看相关跟踪和进行故障诊断](../../../../docs/framework/wcf/diagnostics/tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md)。  
  
 通过创建用户定义的活动跟踪可以扩展 ServiceModel 提供的跟踪。用户定义的活动跟踪允许用户创建跟踪活动，以便执行下列操作：  
  
-   将跟踪分组到逻辑工作单元。  
  
-   通过传输和传播关联活动。  
  
-   降低 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 跟踪的性能成本（例如，日志文件的磁盘空间成本）。  
  
 有关用户定义的活动跟踪的更多信息，请参见[扩展跟踪](../../../../docs/framework/wcf/samples/extending-tracing.md)示例。  
  
## 消息日志记录  
 可以在任何 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序的客户端和服务上启用消息日志记录。若要启动消息日志记录，必须将下面的代码添加到客户端或服务：  
  
```  
<configuration>  
  <system.serviceModel>  
    <diagnostics>  
      <!-- Enable Message Logging here. -->  
      <!-- log all messages received or sent at the transport or service model levels >  
      <messageLogging logEntireMessage="true"  
                      maxMessagesToLog="300"  
                      logMessagesAtServiceLevel="true"  
                      logMalformedMessages="true"  
                      logMessagesAtTransportLevel="true" />  
    </diagnostics>  
  </system.serviceModel>  
</configuration>  
```  
  
 记录消息时，跟踪类型取决于是在客户端还是在服务器上进行跟踪。例如，发送到客户端的“Add”消息将在客户端的“TransportWrite”类别下跟踪，而同一消息将在服务的“TransportRead”类别下跟踪。  
  
 通过将下面的代码添加到客户端的 App.config 文件或服务的 Web.config 文件的 <xref:System.Diagnostics> 节，可以配置跟踪侦听器：  
  
```  
<system.diagnostics>  
    <sources>  
      <source name="System.ServiceModel" switchValue="Information,ActivityTracing"  
        propagateActivity="true">  
        <listeners>  
          <add name="xml" />  
        </listeners>  
      </source>  
      <source name="System.ServiceModel.MessageLogging">  
        <listeners>  
          <add name="xml" />  
        </listeners>  
      </source>  
    </sources>  
    <sharedListeners>  
      <add initializeData="C:\logs\TracingAndLogging-client.svclog" type="System.Diagnostics.XmlWriterTraceListener"  
        name="xml" />  
    </sharedListeners>  
    <trace autoflush="true" />  
  </system.diagnostics>  
```  
  
 消息将以 XML 格式记录在配置文件中指定的目标目录中。  
  
> [!NOTE]
>  如果开始时未创建日志目录，则不会创建跟踪文件。请确保 C:\\logs\\ 目录存在，或在侦听器配置中指定一个替换日志记录目录。有关更多信息，请参见本文档最后的初始安装说明。  
  
 有关消息日志记录的更多信息，请参见[配置消息日志记录](../../../../docs/framework/wcf/diagnostics/configuring-message-logging.md)主题。  
  
#### 设置、生成和运行示例  
  
1.  请确保已经执行了 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  运行“跟踪和消息日志记录”示例之前，创建 C:\\logs\\ 目录以便服务向其中写入 .svclog 文件。此目录的名称在配置文件中定义为要记录的跟踪和消息的路径，并可以进行更改。向用户授予对日志目录的网络服务写权限。  
  
3.  若要生成 C\#、C\+\+ 或 Visual Basic .NET 版本的解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
4.  若要用单机配置或跨计算机配置来运行示例，请按照[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)中的说明进行操作。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Management\TracingAndLogging`  
  
## 请参阅  
 [跟踪](../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [AppFabric 监视示例](http://go.microsoft.com/fwlink/?LinkId=193959)