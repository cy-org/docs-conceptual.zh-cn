---
title: "部署承载于 Internet 信息服务中的 WCF 服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 04ebd329-3fbd-44c3-b3ab-1de3517e27d7
caps.latest.revision: 30
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 30
---
# 部署承载于 Internet 信息服务中的 WCF 服务
开发和部署承载于 Internet 信息服务 \(IIS\) 中的 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务包括以下任务：  
  
-   请确保正确安装和注册 IIS、ASP.NET、[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 和 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 激活组件。  
  
-   创建新的 IIS 应用程序，或重新使用现有的 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 应用程序。  
  
-   为 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务创建 .svc 文件。  
  
-   将服务实现部署到 IIS 应用程序。  
  
-   配置 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务。  
  
 有关创建承载于 IIS 中的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的详细演练，请参见 [如何：在 IIS 中承载 WCF 服务](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-iis.md)。  
  
## 确保已正确安装和注册 IIS、ASP.NET 和 WCF  
 必须同时安装 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]、IIS 和 ASP.NET，承载于 IIS 中的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务才能正常工作。 安装 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]（作为 [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)] 的一部分）、ASP.NET 和 IIS 的过程因所使用的操作系统版本不同而不同。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]安装 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 和 [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)]，请参见 [Microsoft .NET Framework 4.0 Web 安装程序](http://go.microsoft.com/fwlink/?LinkId=201185)。 有关安装 IIS 的说明可以在[安装 IIS](http://go.microsoft.com/fwlink/?LinkId=201188)（可能为英文网页）上找到。  
  
 如果计算机上已存在 IIS，则在安装 [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)] 的过程中自动向 IIS 注册 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]。 如果在安装 [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)] 后安装 IIS，则需要执行其他步骤向 IIS 和 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 注册 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]。 根据您的操作系统，可以按如下所述执行此操作：  
  
-   [!INCLUDE[wxpsp2](../../../../includes/wxpsp2-md.md)]、Windows 7 和 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)]：使用 [ServiceModel 注册工具 \(ServiceModelReg.exe\)](../../../../docs/framework/wcf/servicemodelreg-exe.md) 工具向 IIS 注册 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]：若要使用此工具，请在 Visual Studio 命令提示符处输入 **ServiceModelReg.exe \/i \/x**。 打开此命令提示符，方法是单击“开始”按钮、选择**“所有程序”**、**“Microsoft Visual Studio 2012”**、**“Visual Studio 工具”**和**“Visual Studio 命令提示符”**。  
  
-   [!INCLUDE[wv](../../../../includes/wv-md.md)]：安装 [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)] 的 Windows Communication Foundation Activation Components 子组件。 为此，请在控制面板中，单击**“添加或删除程序”**，然后单击**“添加\/删除 Windows 组件”**。 这将激活**“Windows 组件向导”**。  
  
-   Windows 7：  
  
 最后，必须确认已将 ASP.NET 配置为使用 .NET Framework 版本 4。 通过运行带 –i 选项的 ASPNET\_Regiis 工具执行此操作。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [ASP.NET IIS 注册工具](http://go.microsoft.com/fwlink/?LinkId=201186)  
  
## 创建新的 IIS 应用程序或重新使用现有的 ASP.NET 应用程序  
 承载于 IIS 中的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务必须驻留在 IIS 应用程序内。 可以创建一个新的 IIS 应用程序专门承载 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务。 或者，也可以将 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务部署到现有应用程序，该应用程序已经承载 [!INCLUDE[vstecasplong](../../../../includes/vstecasplong-md.md)] 内容（如 .aspx 页和 ASP.NET Web 服务 \[ASMX\]）。[!INCLUDE[crabout](../../../../includes/crabout-md.md)] 这些选项，请参见 [WCF 服务和 ASP.NET](../../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md) 中的“通过 ASP.NET 并行承载 WCF”和“在 ASP.NET 兼容模式下承载 WCF 服务”部分。  
  
 请注意，[!INCLUDE[iis601](../../../../includes/iis601-md.md)] 和更高版本定期重新启动独立的面向对象编程应用程序。 默认值为 1740 分钟。 支持的最大值为 71,582 分钟。 可以禁用此重新启动。[!INCLUDE[crabout](../../../../includes/crabout-md.md)] 此属性，请参见 [PeriodicRestartTime](http://go.microsoft.com/fwlink/?LinkId=109968)。  
  
## 为 WCF 服务创建 .svc 文件  
 承载于 IIS 中的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务在 IIS 应用程序内表示为特殊内容文件（.svc 文件）。 此模型与在 IIS 应用程序内将 ASMX 页表示为 .asmx 文件的方式类似。 .svc 文件包含 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 特定的处理指令 \([@ServiceHost](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md)\)，该指令允许 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 承载基础结构激活所承载的服务以响应传入消息。 .svc 文件的最常见语法如以下语句所示。  
  
```  
<% @ServiceHost Service="MyNamespace.MyServiceImplementationTypeName" %>  
```  
  
 它由 [@ServiceHost](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md) 指令和单个属性 `Service` 组成。`Service` 属性的值是服务实现的公共语言运行库 \(CLR\) 类型名称。 使用此指令与使用以下代码创建服务主机基本等效。  
  
```  
new ServiceHost( typeof( MyNamespace.MyServiceImplementationTypeName ) );  
```  
  
 也可以执行其他承载配置，如创建服务的基址列表。 也可以使用自定义 <xref:System.ServiceModel.Activation.ServiceHostFactory> 扩展指令以用于自定义承载解决方案。 承载 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的 IIS 应用程序不负责管理 <xref:System.ServiceModel.ServiceHost> 实例的创建和生存期。 收到 .svc 文件的第一个请求时，托管 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 承载基础结构动态创建必需的 <xref:System.ServiceModel.ServiceHost> 实例。 在代码显式关闭该实例之前或回收应用程序时，不释放该实例。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] .svc 文件语法的更多信息，请参见 [@ServiceHost](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md)。  
  
## 将服务实现部署到 IIS 应用程序  
 承载于 IIS 中的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务与 [!INCLUDE[vstecasplong](../../../../includes/vstecasplong-md.md)] 使用相同的动态编译模型。 就像在 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 中那样，可以在各种位置通过几种方式部署承载于 IIS 中的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的实现代码，如下所示：  
  
-   作为全局程序集缓存 \(GAC\) 或应用程序的 \\bin 目录中的预编译 .dll 文件。 在部署类库的新版本后，才更新预编译的二进制文件。  
  
-   作为位于应用程序的 \\App\_Code 目录中的未编译源文件。 处理应用程序的第一个请求时，动态需要位于此目录中的源文件。 对 \\App\_Code 目录中文件进行的任何更改都导致在收到下一个请求时回收和重新编译整个应用程序。  
  
-   作为直接放置在 .svc 文件中的未编译代码。 实现代码也可以按内联方式位于服务的 .svc 文件中，且在 @ServiceHost 指令之后。 对内联代码进行的任何更改导致在收到下一个请求时回收和重新编译应用程序。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] [!INCLUDE[vstecasplong](../../../../includes/vstecasplong-md.md)] 编译模型的更多信息，请参见 [ASP.NET 编译概述](http://go.microsoft.com/fwlink/?LinkId=94773)（可能为英文网页）。  
  
## 配置 WCF 服务  
 承载于 IIS 中的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务将其配置存储在应用程序 Web.config 文件中。 承载于 IIS 中的服务使用与承载于 IIS 外部的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务相同的配置元素和语法。 但是，下面的约束对 IIS 承载环境是唯一的：  
  
-   承载于 IIS 中的服务的基址。  
  
-   通过将一组基址 URI 传递到 <xref:System.ServiceModel.ServiceHost> 构造函数或者通过在服务配置中提供 [\<Host — 宿主\>](../../../../docs/framework/configure-apps/file-schema/wcf/host.md) 元素，在 IIS 外部承载 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的应用程序可以控制这些服务的基址。 承载于 IIS 中的服务无法控制其基址；承载于 IIS 中的服务的基址是其 .svc 文件的地址。  
  
### 承载于 IIS 中的服务的终结点地址  
 承载于 IIS 中时，任何终结点地址始终被认为相对于表示服务的 .svc 文件的地址。 例如，如果 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的基址是包含以下终结点配置的 http:\/\/localhost\/Application1\/MyService.svc。  
  
```  
<endpoint address="anotherEndpoint" .../>  
```  
  
 这提供了一个可以在“http:\/\/localhost\/Application1\/MyService.svc\/anotherEndpoint”上访问的终结点。  
  
 同样，将空字符串用作相对地址的终结点配置元素提供了一个可以在 http:\/\/localhost\/Application1\/MyService.svc（它是基址）上访问的终结点。  
  
```  
<endpoint address="" ... />  
```  
  
 对于承载于 IIS 中的服务的终结点，必须始终使用相对终结点地址。 如果终结点地址未指向承载公开终结点的服务的 IIS 应用程序，则提供完全限定的终结点地址（例如，http:\/\/localhost\/MyService.svc）可能导致在部署服务时出错。 对所承载的服务使用相对终结点地址避免了这些潜在冲突。  
  
### 可用传输  
 承载于 IIS 5.1 和 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中的 [!INCLUDE[iis601](../../../../includes/iis601-md.md)] 服务被限制为使用基于 HTTP 的通信。 在这些 IIS 平台上，将所承载的服务配置为使用非 HTTP 绑定会导致服务激活期间出错。 对于 [!INCLUDE[iisver](../../../../includes/iisver-md.md)]，支持的传输包括 HTTP、Net.TCP、Net.Pipe、Net.MSMQ 以及用于与现有 MSMQ 应用程序向后兼容的 msmq.formatname。  
  
### HTTP 传输安全  
 承载于 IIS 中的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务可以使用 HTTP 传输安全（例如 HTTPS 和 HTTP 身份验证方案，如基本、摘要式和 Windows 集成身份验证），前提是包含该服务的 IIS 虚拟目录支持这些设置。 所承载终结点的绑定上的 HTTP 传输安全设置必须与包含它的 IIS 虚拟目录上的传输安全设置匹配。  
  
 例如，配置为使用 HTTP 摘要式身份验证的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 终结点必须驻留在也配置为允许 HTTP 摘要式身份验证的 IIS 虚拟目录中。 IIS 设置和 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 终结点设置的不匹配组合会导致服务激活期间出错。  
  
## 请参阅  
 [在 Internet 信息服务中承载](../../../../docs/framework/wcf/feature-details/hosting-in-internet-information-services.md)   
 [Internet 信息服务承载最佳实践](../../../../docs/framework/wcf/feature-details/internet-information-services-hosting-best-practices.md)   
 [Windows Server App Fabric 承载功能](http://go.microsoft.com/fwlink/?LinkId=201276)