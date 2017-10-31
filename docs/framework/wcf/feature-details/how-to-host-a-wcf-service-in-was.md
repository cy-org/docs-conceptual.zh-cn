---
title: "如何：在 WAS 中承载 WCF 服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9e3e213e-2dce-4f98-81a3-f62f44caeb54
caps.latest.revision: 25
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 25
---
# 如何：在 WAS 中承载 WCF 服务
本主题概述了创建由 Windows 进程激活服务（也称为 WAS）承载的 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务所需的基本步骤。 WAS 是新的进程激活服务，是对使用非 HTTP 传输协议的 Internet Information Services (IIS) 功能的泛化。 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用监听器适配器接口传递激活请求，这些请求是通过由 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 支持的非 HTTP 协议（如 TCP、命名管道和消息队列）收到的。  
  
 此宿主选项要求正确安装和配置 WAS 激活组件，但不要求编写任何宿主代码作为应用程序的一部分。 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]安装和配置 WAS，请参阅[如何︰ 安装和配置 WCF 激活组件](../../../../docs/framework/wcf/feature-details/how-to-install-and-configure-wcf-activation-components.md)。  
  
> [!WARNING]
>  如果将 Web 服务器的请求处理管道设置为经典模式，则将不支持 WAS 激活。 如果要使用 WAS 激活，则必须将 Web 服务器的请求处理管道设置为集成模式。  
  
 在 WAS 中承载 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务时，可按照通常的方式使用标准绑定。 但是，当使用<xref:System.ServiceModel.NetTcpBinding>和<xref:System.ServiceModel.NetNamedPipeBinding>若要配置一个 WAS 承载的服务，必须满足的约束。 当不同的终结点使用相同的传输时，绑定设置必须在以下的七个属性上相匹配：  
  
-   ConnectionBufferSize  
  
-   ChannelInitializationTimeout  
  
-   MaxPendingConnections  
  
-   MaxOutputDelay  
  
-   MaxPendingAccepts  
  
-   ConnectionPoolSettings.IdleTimeout  
  
-   ConnectionPoolSettings.MaxOutboundConnectionsPerEndpoint  
  
 否则为初始化的终结点首先总是确定这些属性的值和更高版本添加终结点引发<xref:System.ServiceModel.ServiceActivationException>如果它们不匹配这些设置。  
  
 此示例的源副本，请参阅[TCP 激活](../../../../docs/framework/wcf/samples/tcp-activation.md)。  
  
### <a name="to-create-a-basic-service-hosted-by-was"></a>创建 WAS 承载的基本服务  
  
1.  为该类型的服务定义服务协定。  
  
     [!code-csharp[C_HowTo_HostInWAS#1121](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinwas/cs/service.cs#1121)]  
  
2.  在服务类中实现该服务协定。 请注意，在服务的实现内部，未指定地址或绑定信息。 而且，不必编写代码也可从配置文件中检索该信息。  
  
     [!code-csharp[C_HowTo_HostInWAS#1122](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinwas/cs/service.cs#1122)]  
  
3.  创建一个 Web.config 文件以定义<xref:System.ServiceModel.NetTcpBinding>由使用绑定`CalculatorService`终结点。  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <system.serviceModel>  
        <bindings>  
          <netTcpBinding>  
            <binding portSharingEnabled="true">  
              <security mode="None" />  
            </binding>  
          </netTcpBinding>  
        </bindings>  
      </system.serviceModel>  
    </configuration>  
    ```  
  
4.  创建包含以下代码的 Service.svc 文件。  
  
    ```  
    <%@ServiceHost language=c# Service="CalculatorService" %>   
    ```  
  
5.  将 Service.svc 文件放到 IIS 虚拟目录中。  
  
### <a name="to-create-a-client-to-use-the-service"></a>创建要使用服务的客户端  
  
1.  使用[ServiceModel 元数据实用工具 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)从命令行以从服务元数据生成代码。  
  
    ```  
    Svcutil.exe <service's Metadata Exchange (MEX) address or HTTP GET address>   
    ```  
  
2.  生成的客户端包含 `ICalculator` 接口，该接口定义了客户端实现必须满足的服务协定。  
  
     [!code-csharp[C_HowTo_HostInWAS#1221](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinwas/cs/client.cs#1221)]  
  
3.  生成的客户端应用程序还包含 `ClientCalculator` 的实现。 请注意，在服务的实现内部，未指定地址和绑定信息。 而且，不必编写代码也可从配置文件中检索该信息。  
  
     [!code-csharp[C_HowTo_HostInWAS#1222](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinwas/cs/client.cs#1222)]  
  
4.  使用的客户端的配置<xref:System.ServiceModel.NetTcpBinding>也通过 Svcutil.exe 生成。 在使用 Visual Studio 时，应在 App.config 文件中命名此文件。  
  
     <!-- TODO: review snippet reference [!code[C_HowTo_HostInWAS#2211](../../../../samples/snippets/common/VS_Snippets_CFX/c_howto_hostinwas/common/app.config#2211)]  -->  
  
5.  在应用程序中创建 `ClientCalculator` 的实例，然后调用服务操作。  
  
     [!code-csharp[C_HowTo_HostInWAS#1223](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinwas/cs/client.cs#1223)]  
  
6.  编译并运行客户端。  
  
## <a name="see-also"></a>另请参阅  
 [TCP 激活](../../../../docs/framework/wcf/samples/tcp-activation.md)   
 [Windows Server App Fabric 承载功能](http://go.microsoft.com/fwlink/?LinkId=201276)