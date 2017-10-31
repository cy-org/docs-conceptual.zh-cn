---
title: "扩展跟踪 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2b971a99-16ec-4949-ad2e-b0c8731a873f
caps.latest.revision: 28
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 28
---
# 扩展跟踪
此示例演示如何通过在客户端和服务代码中编写用户定义的活动跟踪来扩展 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 跟踪功能。这样使用户可以创建跟踪活动，并将跟踪分组为逻辑工作单元。还可以通过传输（在同一个终结点内）和传播（在终结点之间）来关联活动。在此示例中，同时为客户端和服务启用了跟踪。有关如何在客户端和服务配置文件中启用跟踪的更多信息，请参见[跟踪和消息日志记录](../../../../docs/framework/wcf/samples/tracing-and-message-logging.md)。  
  
 此示例基于[入门](../../../../docs/framework/wcf/samples/getting-started-sample.md)。  
  
> [!NOTE]
>  本主题的最后介绍了此示例的设置过程和生成说明。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Management\ExtendingTracing`  
  
## 跟踪和活动传播  
 通过用户定义的活动跟踪，用户可以创建自己的跟踪活动，以便将跟踪分组为逻辑工作单元，通过传输和传播来关联活动，并降低 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 跟踪的性能成本（例如，日志文件的磁盘空间成本）。  
  
### 添加自定义源  
 用户定义的跟踪既可以添加到客户端代码中，又可以添加到服务代码中。在客户端或服务配置文件中添加跟踪源使得可以在[服务跟踪查看器工具 \(SvcTraceViewer.exe\)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)中记录和显示这些自定义跟踪。下面的代码演示如何在配置文件中添加一个名为 `ServerCalculatorTraceSource` 的用户定义的跟踪源。  
  
```  
<system.diagnostics>  
    <sources>  
        <source name="System.ServiceModel" switchValue="Warning" propagateActivity="true">  
            <listeners>  
                <add type="System.Diagnostics.DefaultTraceListener" name="Default">  
                    <filter type="" />  
                </add>  
                <add name="xml">  
                    <filter type="" />  
                </add>  
            </listeners>  
        </source>  
        <source name="ServerCalculatorTraceSource" switchValue="Information,ActivityTracing">  
            <listeners>  
                <add type="System.Diagnostics.DefaultTraceListener" name="Default">  
                    <filter type="" />  
                </add>  
                <add name="xml">  
                    <filter type="" />  
                </add>  
            </listeners>  
        </source>  
    </sources>  
    <sharedListeners>  
       <add initializeData="C:\logs\ServerTraces.svclog" type="System.Diagnostics.XmlWriterTraceListener"  
        name="xml" traceOutputOptions="Callstack">  
            <filter type="" />  
        </add>  
    </sharedListeners>  
    <trace autoflush="true" />  
</system.diagnostics>....  
....  
```  
  
### 关联活动  
 若要跨终结点直接关联活动，必须将 `System.ServiceModel` 跟踪源中的 `propagateActivity` 属性设置为 `true`。而且，若要不通过 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 活动而传播跟踪，必须关闭 ServiceModel 活动跟踪。这可以在以下代码示例中看到。  
  
> [!NOTE]
>  关闭 ServiceModel 活动跟踪与将 `switchValue` 属性表示的跟踪级别设置为 off 并不一样。  
  
```  
<system.diagnostics>  
    <sources>  
      <source name="System.ServiceModel" switchValue="Warning" propagateActivity="true">  
  
    ...  
  
       </source>  
    </sources>  
</system.diagnostics>  
```  
  
### 降低性能成本  
 将 `System.ServiceModel` 跟踪源中的 `ActivityTracing` 设置为 off 将生成一个只包含用户定义的活动跟踪的跟踪文件，而不包含任何 ServiceModel 活动跟踪。这样将产生非常小的日志文件。但会丢失关联 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 处理跟踪的机会。  
  
##### 设置、生成和运行示例  
  
1.  请确保已经执行了 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  若要生成 C\# 或 Visual Basic .NET 版本的解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
3.  若要用单机配置或跨计算机配置来运行示例，请按照[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)中的说明进行操作。  
  
## 请参阅  
 [AppFabric 监视示例](http://go.microsoft.com/fwlink/?LinkId=193959)