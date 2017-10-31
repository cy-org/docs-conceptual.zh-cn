---
title: "配置 Windows 进程激活服务以用于 Windows Communication Foundation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1d50712e-53cd-4773-b8bc-a1e1aad66b78
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# 配置 Windows 进程激活服务以用于 Windows Communication Foundation
本主题介绍在 [!INCLUDE[wv](../../../../includes/wv-md.md)] 中设置 Windows 进程激活服务（也称为 WAS）使其承载不通过 HTTP 网络协议进行通信的 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务所需的步骤。下面的部分略述此配置的步骤：  
  
-   安装（或确认安装）所需的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 激活组件。  
  
-   创建一个具有要使用的网络协议绑定的 WAS 站点，或者向现有站点添加新协议绑定。  
  
-   创建一个应用程序以承载服务，并使该应用程序可以使用所需的网络协议。  
  
-   生成一个公开非 HTTP 终结点的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务。  
  
## 使用非 HTTP 绑定配置站点  
 若要将非 HTTP 绑定与 WAS 一起使用，必须将站点绑定添加到 WAS 配置。WAS 的配置存储是 applicationHost.config 文件，该文件位于 %windir%\\system32\\inetsrv\\config 目录中。此配置存储由 WAS 和 IIS 7.0 共享。  
  
 applicationHost.config 是一个 XML 文本文件，可以使用任何标准文本编辑器（如记事本）打开。不过，[!INCLUDE[iisver](../../../../includes/iisver-md.md)] 命令行配置工具 \(appcmd.exe\) 是添加非 HTTP 站点绑定的首选方法。  
  
 下面的命令使用 appcmd.exe 将 net.tcp 站点绑定添加到默认网站（将此命令作为单独的一行输入）。  
  
```  
appcmd.exe set site "Default Web Site" -+bindings.[protocol='net.tcp',bindingInformation='808:*']  
```  
  
 通过将下面指示的行添加到 applicationHost.config 文件，此命令将新 net.tcp 绑定添加到默认网站。  
  
```  
<sites>  
    <site name="Default Web Site" id="1">  
        <bindings>  
            <binding protocol="HTTP" bindingInformation="*:80:" />  
            //The following line is added by the command.  
            <binding protocol="net.tcp" bindingInformation="808:*" />  
        </bindings>  
    </site>  
</sites>  
```  
  
## 使应用程序可以使用非 HTTP 协议  
 可以在应用程序级别上启用或禁用单个网络协议。下面的命令说明如何为在 `Default Web Site` 中运行的应用程序同时启用 HTTP 和 net.tcp 协议。  
  
```  
appcmd.exe set app "Default Web Site/appOne" /enabledProtocols:net.tcp  
```  
  
 也可以在 ApplicationHost.config 中存储的站点 XML 配置的 \<applicationDefaults\> 元素中设置已启用协议列表。  
  
 摘自 applicationHost.config 的以下 XML 代码说明一个已同时绑定到 HTTP 协议和非 HTTP 协议的站点。支持非 HTTP 协议所需的其他配置通过注释进行了突出。  
  
```  
<sites>  
    <site name="Default Web Site" id="1">  
    <application path="/">  
        <virtualDirectory path="/" physicalPath="D:\inetpub\wwwroot" />  
    </application>  
       <bindings>  
            //The following two lines are added by the command.  
            <binding protocol="HTTP" bindingInformation="*:80:" />  
            <binding protocol="net.tcp" bindingInformation="808:*" />  
       </bindings>  
    </site>  
    <siteDefaults>  
        <logFile   
        customLogPluginClsid="{FF160663-DE82-11CF-BC0A-00AA006111E0}"  
          directory="D:\inetpub\logs\LogFiles" />  
        <traceFailedRequestsLogging   
          directory="D:\inetpub\logs\FailedReqLogFiles" />  
    </siteDefaults>  
    <applicationDefaults   
      applicationPool="DefaultAppPool"   
      //The following line is inserted by the command.  
      enabledProtocols="http, net.tcp" />  
    <virtualDirectoryDefaults allowSubDirConfig="true" />  
</sites>  
```  
  
 如果您尝试使用 WAS 激活非 HTTP 激活的服务，并且您不安装并配置 WAS 您可能会看到以下错误：  
  
```Output  
[InvalidOperationException：协议 'net.tcp' 不会未有 HostedTransportConfiguration 类型的实现注册。]System.ServiceModel.AsyncResult.End(IAsyncResult result) +15778592 System.ServiceModel.Activation.HostedHttpRequestAsyncResult.End(IAsyncResult result) +15698937 System.ServiceModel.Activation.HostedHttpRequestAsyncResult.ExecuteSynchronous 布尔 flowContext HttpApplication上下文） +265 System.ServiceModel.Activation.HttpModule.ProcessRequest EventArgs e 对象发件人） +227 系统。网站/网页。SyncEventExecutionStep.System。网站/网页。HttpApplication.IExecutionStep.Execute() + 80 系统。网站/网页。HttpApplication.ExecuteStep (IExecutionStep 步，布尔值 & completedSynchronously) +171  
```  
  
 如果您看到此错误确保 WAS 非 HTTP 激活已安装并正确配置。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][如何：安装和配置 WCF 激活组件](../../../../docs/framework/wcf/feature-details/how-to-install-and-configure-wcf-activation-components.md).  
  
## 生成一个将 WAS 用于非 HTTP 激活的 WCF 服务  
 执行安装和配置 WAS 的步骤后（请参见 [如何：安装和配置 WCF 激活组件](../../../../docs/framework/wcf/feature-details/how-to-install-and-configure-wcf-activation-components.md)），将服务配置为使用 WAS 进行激活与配置承载于 IIS 中的服务类似。  
  
 有关生成 WAS 激活的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的详细说明，请参见[如何：在 WAS 中承载 WCF 服务](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-was.md)。  
  
## 请参阅  
 [在 Windows 进程激活服务中承载](../../../../docs/framework/wcf/feature-details/hosting-in-windows-process-activation-service.md)   
 [Windows Server App Fabric 承载功能](http://go.microsoft.com/fwlink/?LinkId=201276)