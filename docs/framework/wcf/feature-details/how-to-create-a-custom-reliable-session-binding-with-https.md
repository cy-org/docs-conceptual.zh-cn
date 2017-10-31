---
title: "如何：创建使用 HTTPS 的自定义可靠会话绑定 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fa772232-da1f-4c66-8c94-e36c0584b549
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# 如何：创建使用 HTTPS 的自定义可靠会话绑定
本主题演示如何对可靠会话使用安全套接字层 \(SSL\) 传输安全。  若要通过 HTTPS 使用可靠会话，必须创建使用可靠会话和 HTTPS 传输协议的自定义绑定。  可使用代码以强制方式或在配置文件中以声明方式来启用可靠会话。  此过程使用客户端和服务配置文件来启用可靠会话和 [\<httpsTransport\>](../../../../docs/framework/configure-apps/file-schema/wcf/httpstransport.md) 元素。  
  
 此过程的关键部分是 `endpoint` 配置元素包含一个 `bindingConfiguration` 属性，此属性引用名为“reliableSessionOverHttps”的自定义绑定配置。  然后，[\<绑定\>](../../../../docs/framework/misc/binding.md) 配置元素可以引用此名称来指定，通过包括 `reliableSession` 和 `httpsTransport` 元素来使用可靠会话和 HTTPS 传输协议。  
  
 有关此示例的源副本，请参见[基于 HTTPS 的自定义绑定可靠会话](../../../../docs/framework/wcf/samples/custom-binding-reliable-session-over-https.md)。  
  
### 使用 CustomBinding 配置服务以将可靠会话与 HTTPS 一起使用  
  
1.  为该类型的服务定义服务协定。  
  
     [!code-csharp[c_HowTo_CreateReliableSessionHTTPS#1121](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createreliablesessionhttps/cs/service.cs#1121)]  
  
2.  在服务类中实现该服务协定。  请注意，在服务的实现内部，未指定地址或绑定信息。  而且，不必编写代码也可从配置文件中检索该信息。  
  
     [!code-csharp[c_HowTo_CreateReliableSessionHTTPS#1122](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createreliablesessionhttps/cs/service.cs#1122)]  
  
3.  创建 Web.config 文件，并使用名为“reliableSessionOverHttps”的自定义绑定（使用可靠会话和 HTTPS 传输协议）为 `CalculatorService` 配置一个终结点。  
  
     <!-- TODO: review snippet reference [!code[c_HowTo_CreateReliableSessionHTTPS#2111](../../../../samples/snippets/common/VS_Snippets_CFX/c_howto_createreliablesessionhttps/common/web.config#2111)]  -->  
  
4.  创建包含以下代码行的 Service.svc 文件：  
  
    ```  
    <%@ServiceHost language=c# Service="CalculatorService" %>   
    ```  
  
5.  将 Service.svc 文件放到 Internet 信息服务 \(IIS\) 虚拟目录中。  
  
### 使用 CustomBinding 配置客户端以将可靠会话与 HTTPS 一起使用  
  
1.  从命令行使用 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 以从服务元数据生成代码。  
  
    ```  
    Svcutil.exe <service's Metadata Exchange (MEX) address or HTTP GET address>   
    ```  
  
2.  生成的客户端包含 `ICalculator` 接口，该接口定义了客户端实现必须满足的服务协定。  
  
     [!code-csharp[C_HowTo_CreateReliableSessionHTTPS#1221](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createreliablesessionhttps/cs/client.cs#1221)]  
  
3.  生成的客户端应用程序还包含 `ClientCalculator` 的实现。  请注意，在服务的实现内部，未指定地址和绑定信息。  而且，不必编写代码也可从配置文件中检索该信息。  
  
     [!code-csharp[C_HowTo_CreateReliableSessionHTTPS#1222](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createreliablesessionhttps/cs/client.cs#1222)]  
  
4.  配置一个名为“reliableSessionOverHttps”的自定义绑定以使用 HTTPS 传输和可靠的会话。  
  
     <!-- TODO: review snippet reference [!code[C_HowTo_CreateReliableSessionHTTPS#2211](../../../../samples/snippets/common/VS_Snippets_CFX/c_howto_createreliablesessionhttps/common/app.config#2211)]  -->  
  
5.  在应用程序中创建 `ClientCalculator` 的实例，然后调用服务操作。  
  
     [!code-csharp[C_HowTo_CreateReliableSessionHTTPS#1223](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createreliablesessionhttps/cs/client.cs#1223)]  
  
6.  编译并运行客户端。  
  
## 示例  
<!-- TODO: review snippet reference  [!CODE [Microsoft.Win32.RegistryKey#4](Microsoft.Win32.RegistryKey#4)]  -->  
  
## .NET Framework 安全性  
 因为此示例中使用的证书是用 Makecert.exe 创建的测试证书，所以当您尝试从浏览器中访问 HTTPS 地址（例如 https:\/\/localhost\/servicemodelsamples\/service.svc）时，将出现安全警报。  
  
## 请参阅  
 [可靠会话](../../../../docs/framework/wcf/feature-details/reliable-sessions.md)