---
title: "Windows 服务主机 | Microsoft Docs"
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
  - "NT 服务"
  - "NT 服务主机示例 [Windows Communication Foundation]"
ms.assetid: 1b2f45c5-2bed-4979-b0ee-8f9efcfec028
caps.latest.revision: 40
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 40
---
# Windows 服务主机
此示例演示在托管 Windows 服务中承载的 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务。Windows 服务是使用**“控制面板”**上的“服务”小程序控制的，所以可以配置为在系统重新启动后自动启动。此示例包含一个客户端程序和一个 Windows 服务程序。服务作为一个 .exe 程序实现，并包含其自己的宿主代码。在其他承载环境（如 Windows 进程激活服务 \(WAS\) 或 Internet Information Services \(IIS\)）中，您没有必要编写承载代码。  
  
> [!NOTE]
>  本主题的最后介绍了此示例的设置过程和生成说明。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\WindowsService`  
  
 生成此服务之后，必须像任何其他 Windows 服务一样使用 Installutil.exe 实用工具安装此服务。如果要对此服务进行更改，必须首先使用 `installutil /u` 将其卸载。此示例中随附的 Setup.bat 和 Cleanup.bat 文件是用于安装和启动 Windows 服务的命令，还可用于关闭和卸载 Windows 服务。只有在 Windows 服务正在运行的情况下，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务才能响应客户端。如果您使用**“控制面板”**上的“服务”小程序停止了 Windows 服务，然后运行客户端，当客户端尝试访问该服务时，将发生 <xref:System.ServiceModel.EndpointNotFoundException> 异常。如果重新启动 Windows 服务并重新运行客户端，通信将成功。  
  
 服务代码中包括一个安装程序类、一个实现 ICalculator 协定的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务实现类和一个用作运行时主机的 Windows 服务类。安装程序类继承自 <xref:System.Configuration.Install.Installer>，允许通过 Installutil.exe 工具将程序安装为 NT 服务。服务实现类 `WcfCalculatorService` 是一个实现基本服务协定的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务。此 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务在称为 `WindowsCalculatorService` 的 Windows 服务类中承载。为了符合作为 Windows 服务的要求，该类从 <xref:System.ServiceProcess.ServiceBase> 继承并实现 [OnStart\(String\<xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29> 和 <xref:System.ServiceProcess.ServiceBase.OnStop> 方法。在 [OnStart\(String\<xref:System.ServiceProcess.ServiceBase.OnStart%28System.String%5B%5D%29> 中，为 `WcfCalculatorService` 类型创建并打开了 <xref:System.ServiceModel.ServiceHost> 对象。在 <xref:System.ServiceProcess.ServiceBase.OnStop> 中，通过调用 <xref:System.ServiceModel.ServiceHost> 对象的 <xref:System.ServiceModel.Channels.CommunicationObject.Close%28System.TimeSpan%29> 方法关闭了 ServiceHost。主机的基本地址是使用 [\<添加\>](../../../../docs/framework/configure-apps/file-schema/wcf/add-of-baseaddresses.md) 元素配置的，该元素是 [\<baseAddresses\>](../../../../docs/framework/configure-apps/file-schema/wcf/baseaddresses.md) 的一个子元素，它又是 [\<Host — 宿主\>](../../../../docs/framework/configure-apps/file-schema/wcf/host.md) 元素的一个子元素，而该元素又是 [\<service\>](../../../../docs/framework/configure-apps/file-schema/wcf/service.md) 元素的一个子元素。  
  
 定义的终结点使用基本地址和一个 [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)。下面的示例演示了基本地址的配置以及公开 CalculatorService 的终结点。  
  
```  
<services>  
  <service name="Microsoft.ServiceModel.Samples.WcfCalculatorService"  
           behaviorConfiguration="CalculatorServiceBehavior">  
    <host>  
      <baseAddresses>  
        <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>  
      </baseAddresses>  
    </host>  
    <!-- This endpoint is exposed at the base address provided by host: http://localhost:8000/ServiceModelSamples/service.  -->  
    <endpoint address=""  
              binding="wsHttpBinding"  
              contract="Microsoft.ServiceModel.Samples.ICalculator" />  
    ...  
  </service>  
</services>  
  
```  
  
 运行示例时，操作请求和响应将显示在服务和客户端控制台窗口中。在每个控制台窗口中按 Enter 可以关闭服务和客户端。  
  
### 设置、生成和运行示例  
  
1.  请确保已经执行了 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  若要生成 C\# 或 Visual Basic .NET 版本的解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
3.  生成解决方案后，在提升后的 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 命令提示中运行 Setup.bat 以使用 Installutil.exe 工具安装 Windows 服务。该服务应出现在“服务”中。  
  
4.  若要用单机配置或跨计算机配置来运行示例，请按照[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)中的说明进行操作。  
  
## 请参阅  
 [AppFabric 承载和持久性示例](http://go.microsoft.com/fwlink/?LinkId=193961)