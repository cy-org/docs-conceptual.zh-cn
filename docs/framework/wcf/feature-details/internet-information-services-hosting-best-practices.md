---
title: "Internet 信息服务承载最佳实践 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0834768e-9665-46bf-86eb-d4b09ab91af5
caps.latest.revision: 22
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 22
---
# Internet 信息服务承载最佳实践
本主题概述承载 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务的一些最佳实践。  
  
## 将 WCF 服务实现为 DLL  
 将 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务实现为部署到 Web 应用程序的 \\bin 目录的 DLL，允许您在 Web 应用程序模型之外重用该服务，例如，在可能尚未部署 Internet 信息服务 \(IIS\) 的测试环境中。  
  
## 承载于 IIS 中的应用程序中的服务主机  
 不要使用强制性自承载 API 创建用于侦听 IIS 承载环境本身不支持的网络传输的新服务主机（例如，承载 TCP 服务的 [!INCLUDE[iis601](../../../../includes/iis601-md.md)]，因为 [!INCLUDE[iis601](../../../../includes/iis601-md.md)] 本身不支持 TCP 通信）。建议不要使用此方法。强制创建的服务主机在 IIS 承载环境内是未知的。很重要的一点是，在 IIS 确定承载应用程序池是否空闲时，它未说明强制创建的服务所进行的处理。结果是具有这样强制创建的服务主机的应用程序具有主动处置 IIS 宿主进程的 IIS 承载环境。  
  
## URI 和承载于 IIS 中的终结点  
 承载于 IIS 中的服务的终结点应该使用相对统一资源标识符 \(URI\) 而不是绝对地址进行配置。这保证终结点地址在属于承载应用程序的 URI 地址集范围内，并确保像预期的那样发生基于消息的激活。  
  
## 状态管理和进程回收  
 为不在内存中维护本地状态的服务优化了 IIS 承载环境。IIS 回收宿主进程以响应各种外部和内部事件，导致仅存储在内存中的任何可变状态丢失。寄宿在 IIS 中的服务应该在进程外存储其状态（例如，在数据库中），或者在出现应用程序回收事件时可以轻松重新创建的内存中缓存中存储其状态。  
  
> [!NOTE]
>  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 用于消息层可靠性和安全性的协议利用可变的内存中状态。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 可靠会话和安全会话可能由于应用程序回收而意外终止。利用这些协议的承载于 IIS 中的应用程序应该依赖于除 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供的会话密钥之外的某个密钥，以关联应用程序层状态（例如，应用程序层结构或自定义关联标头）或禁用寄宿应用程序的 IIS 进程回收。  
  
## 在中间层方案中优化性能  
 为了在“中间层方案”（一种调用其他服务以响应传入消息的服务）中获得最佳性能，将 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务客户端实例化到远程服务一次，并跨多个传入请求重用它。实例化 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务客户端是一种与对预先存在的客户端实例进行服务调用相关的高开销操作，而且中间层方案通过跨请求缓存远程客户端来产生明显的性能提升。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务客户端是线程安全的，因此不必跨多个线程同步对某个客户端的访问。  
  
 中间层方案还通过使用由 `svcutil /a` 选项生成的异步 API 来产生性能提升。`/a` 选项导致 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 为每个服务操作生成 `BeginXXX/EndXXX` 方法，这样就允许在后台线程上对远程服务进行可能长时间运行的调用。  
  
## 多宿主或多名称方案中的 WCF  
 可以在 IIS 网络场内部署 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务，在 IIS 网络场中一组计算机共享公共外部名称（如 http:\/\/www.contoso.com）但按不同的主机名单独寻址（例如，http:\/\/www.contoso.com 可能将流量定向到名为 http:\/\/machine1.internal.contoso.com 和 http:\/\/machine2.internal.contoso.com 的两台不同计算机）。此部署方案完全受 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的支持，但是需要承载 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的 IIS 网站的特殊配置，才能在服务的元数据（Web Services 描述语言）中显示正确的（外部）主机名。  
  
 若要确保在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 生成的服务元数据中显示正确的主机名，请将承载 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的 IIS 网站的默认标识配置为使用显式主机名。例如，驻留在 www.contoso.com 场内的计算机应该使用 \*:80:www.contoso.com（对于 HTTP）和 \*:443:www.contoso.com（对于 HTTPS）的 IIS 站点绑定。  
  
 可以使用 IIS Microsoft 管理控制台 \(MMC\) 管理单元配置 IIS 网站绑定。  
  
## 在不同用户上下文中运行的应用程序池覆盖来自临时文件夹中其他帐户的程序集  
 若要确保在不同用户上下文中运行的应用程序池无法覆盖来自临时 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 文件夹中其他帐户的程序集，请对不同的应用程序使用不同的标识和临时文件夹。例如，如果具有两个虚拟应用程序 \/Application1 和 \/ Application2，则可以创建两个应用程序池 A 和 B，它们具有不同的标识。应用程序池 A 可以使用一个用户标识 \(user1\) 运行，而应用程序池 B 可以使用其他用户标识 \(user2\) 运行，并将 \/Application1 配置为使用 A，将 \/Application2 配置为使用 B。  
  
 在 Web.config 中，可以使用 \<system.web\/compilation\/@tempFolder\> 配置临时文件夹。对于 \/Application1，它可以是“c:\\tempForUser1”，对于 application2，它可以是“c:\\tempForUser2”。将相应的写入权限授予两个标识的这些文件夹。  
  
 之后，user2 无法更改 \/application2 的代码生成文件夹（在 c:\\tempForUser1 下）。  
  
## 启用异步处理  
 默认情况下，以同步方式处理发送到承载于 IIS 6.0 及更早版本下的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的消息。ASP.NET 在它自己的线程（ASP.NET 工作线程）上调入 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]，且 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用其他线程处理请求。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 在完成其处理之前会保持 ASP.NET 工作线程。这将导致同步处理请求。异步处理请求能够实现更大的可伸缩性，因为它可减少处理请求所需的线程数（在处理请求时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 不保持 ASP.NET 线程）。对于运行 IIS 6.0 的计算机，不建议使用异步行为，因为无法限制会使服务器面临“拒绝服务”\(DOS\) 攻击的传入请求。从 IIS 7.0 开始，引入了并发请求限制：`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ASP.NET\2.0.50727.0]“MaxConcurrentRequestsPerCpu`。借助这一新的限制，可安全地使用异步处理。默认情况下，在 IIS 7.0 中会注册异步处理程序和模块。如果关闭了此功能，可在应用程序的 Web.config 文件中手动启用对请求的异步处理。所使用的设置取决于 `aspNetCompatibilityEnabled` 设置。如果已将 `aspNetCompatibilityEnabled` 设置为 `false`，请按照下面的配置代码段所示配置 <xref:System.ServiceModel.Activation.ServiceHttpModule>。  
  
```  
<system.serviceModel>  
    <serviceHostingEnvironment aspNetCompatibilityEnabled="false" />      
  </system.serviceModel>  
  <system.webServer>  
    <modules>  
      <remove name="ServiceModel"/>  
      <add name="ServiceModel"   
           preCondition="integratedMode,runtimeVersionv2.0"   
           type="System.ServiceModel.Activation.ServiceHttpModule, System.ServiceModel,Version=3.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"/>  
    </modules>  
    </system.webServer>  
  
```  
  
 如果已将 `aspNetCompatibilityEnabled` 设置为 `true`，请按照下面的配置代码段所示配置 <xref:System.ServiceModel.Activation.ServiceHttpHandlerFactory>。  
  
```  
<system.serviceModel>  
    <serviceHostingEnvironment aspNetCompatibilityEnabled="true" />      
  </system.serviceModel>  
  <system.webServer>  
    <handlers>  
          <clear/>  
          <add name="TestAsyncHttpHandler"   
               path="*.svc"   
               verb="*"   
               type="System.ServiceModel.Activation.ServiceHttpHandlerFactory, System.ServiceModel, Version=3.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"           
               />  
    </handlers>      
  </system.webServer>  
  
```  
  
## 请参阅  
 [Service Hosting Samples](http://msdn.microsoft.com/zh-cn/f703a3f6-0fba-418a-a92f-7ce75ccfa47e)   
 [Windows Server App Fabric 承载功能](http://go.microsoft.com/fwlink/?LinkId=201276)