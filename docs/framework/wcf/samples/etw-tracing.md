---
title: "ETW 跟踪 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ac99a063-e2d2-40cc-b659-d23c2f783f92
caps.latest.revision: 42
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 42
---
# ETW 跟踪
本示例演示如何通过使用 Windows 事件跟踪 \(ETW\) 和本示例提供的 `ETWTraceListener` 来实现端对端 \(E2E\) 跟踪。本示例基于[入门](../../../../docs/framework/wcf/samples/getting-started-sample.md)并包括 ETW 跟踪。  
  
> [!NOTE]
>  本主题的最后介绍了此示例的设置过程和生成说明。  
  
 本示例假定您熟悉[跟踪和消息日志记录](../../../../docs/framework/wcf/samples/tracing-and-message-logging.md)。  
  
 <xref:System.Diagnostics> 跟踪模型中的每个跟踪源都可以具有多个跟踪侦听器，这些侦听器确定跟踪数据的位置和方式。侦听器的类型定义记录跟踪数据的格式。下面的代码示例演示如何向配置中添加侦听器。  
  
```  
  
<system.diagnostics>  
    <sources>  
        <source name="System.ServiceModel"   
             switchValue="Verbose,ActivityTracing"  
             propagateActivity="true">  
            <listeners>  
                <add type=  
                   "System.Diagnostics.DefaultTraceListener"  
                   name="Default">  
                   <filter type="" />  
                </add>  
                <add name="ETW">  
                    <filter type="" />  
                </add>  
            </listeners>  
        </source>  
    </sources>  
    <sharedListeners>  
        <add type=  
            "Microsoft.ServiceModel.Samples.EtwTraceListener, ETWTraceListener"  
            name="ETW" traceOutputOptions="Timestamp">  
            <filter type="" />  
       </add>  
    </sharedListeners>  
</system.diagnostics>  
  
```  
  
 在使用此侦听器之前，必须启动 ETW 跟踪会话。可以通过使用 Logman.exe 或 Tracelog.exe 来启动此会话。本示例随附一个 SetupETW.bat 文件，您可以和 CleanupETW.bat 文件一起使用此文件来设置 ETW 跟踪会话，以便关闭会话并完成日志文件。  
  
> [!NOTE]
>  本主题的末尾介绍了此示例的设置过程和生成说明。有关这些工具的更多信息，请参见 [http:\/\/go.microsoft.com\/fwlink\/?LinkId\=56580](http://go.microsoft.com/fwlink/?LinkId=56580)  
  
 使用 ETWTraceListener 时，将在二进制 .etl 文件中记录跟踪。在打开 ServiceModel 跟踪的情况下，所有生成的跟踪都显示在同一个文件中。可以使用[服务跟踪查看器工具 \(SvcTraceViewer.exe\)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)查看 .etl 和 .svclog 日志文件。该查看器可创建系统的端对端视图，可以从消息源到消息目标和使用点来跟踪消息。  
  
 ETW 跟踪侦听器支持循环记录。若要启用此功能，请转到**“开始”**、**“运行”**，然后键入 `cmd` 以启动命令控制台。在下面的命令中，用日志文件的名称替换 `<logfilename>` 参数。  
  
```  
logman create trace Wcf -o <logfilename> -p "{411a0819-c24b-428c-83e2-26b41091702e}" -f bincirc -max 1000  
```  
  
 `-f` 和 `-max` 开关是可选的。它们分别指定二进制循环格式和 1000 MB 的最大日志大小。`-p` 开关用于指定跟踪提供程序。在我们的示例中，`"{411a0819-c24b-428c-83e2-26b41091702e}"` 是“XML ETW 示例提供程序”的 GUID。  
  
 若要启动会话，请键入以下命令。  
  
```  
Logman start Wcf  
  
```  
  
 在完成日志记录后，可以用下面的命令停止会话。  
  
```  
Logman stop Wcf  
```  
  
 此进程可生成二进制循环日志，您可以使用所选的工具（包括[服务跟踪查看器工具 \(SvcTraceViewer.exe\)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)或 Tracerpt）来处理该日志。  
  
 您也可以查看[循环跟踪](../../../../docs/framework/wcf/samples/circular-tracing.md)示例，了解有关用于执行循环记录的替代侦听器的更多信息。  
  
### 设置、生成和运行示例  
  
1.  请确保已执行 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  若要生成解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
    > [!NOTE]
    >  若要使用 RegisterProvider.bat、SetupETW.bat 和 CleanupETW.bat 命令，必须在本地管理员帐户下运行。如果使用的是 [!INCLUDE[wv](../../../../includes/wv-md.md)] 或更高版本，则还必须用提升的特权运行命令提示。为此，请右击命令提示图标，然后单击**“以管理员身份运行”**。  
  
3.  运行示例之前，在客户端和服务器上运行 RegisterProvider.bat。这会设置生成的 ETWTracingSampleLog.etl 文件以生成可由服务跟踪查看器读取的跟踪。此文件可以在 C:\\logs 文件夹中找到。如果此文件夹不存在，则必须创建此文件夹；否则将不会生成跟踪。然后，在客户端和服务器计算机上运行 SetupETW.bat 以开始 ETW 跟踪会话。SetupETW.bat 文件可以在 CS\\Client 文件夹下找到。  
  
4.  若要用单机配置或跨计算机配置来运行示例，请按照[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)中的说明进行操作。  
  
5.  示例完成后，运行 CleanupETW.bat 以完成 ETWTracingSampleLog.etl 文件的创建。  
  
6.  在服务跟踪查看器中打开 ETWTracingSampleLog.etl 文件。系统会提示您将二进制格式的文件另存为 .svclog 文件。  
  
7.  从服务跟踪查看器中打开新创建的 .svclog 文件以查看 ETW 和 ServiceModel 跟踪。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Management\AnalyticTrace`  
  
## 请参阅  
 [AppFabric 监视示例](http://go.microsoft.com/fwlink/?LinkId=193959)