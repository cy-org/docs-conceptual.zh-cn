---
title: "如何：使用 Windows 凭据保护服务的安全 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF, 安全"
ms.assetid: d171b5ca-96ef-47ff-800c-c138023cf76e
caps.latest.revision: 26
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 26
---
# 如何：使用 Windows 凭据保护服务的安全
本主题演示如何在驻留于 Windows 域中并由同一域中的客户端调用的 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 服务上启用传输安全。 [!INCLUDE[crabout](../../../includes/crabout-md.md)]此方案中，请参阅[使用 Windows 身份验证的传输安全](../../../docs/framework/wcf/feature-details/transport-security-with-windows-authentication.md)。 有关示例应用程序，请参阅[WSHttpBinding](../../../docs/framework/wcf/samples/wshttpbinding.md)示例。  
  
 本主题假定您已定义一个现有的协定接口和实现及其加载项。 您还可以修改一个现有的服务和客户端。  
  
 您完全可以在代码中使用 Windows 凭据来保护服务。 或者，也可以通过使用配置文件省略某些代码。 本主题演示了这两种方法。 请务必仅使用其中一种方法，而不是同时使用两种方法。  
  
 前三个过程演示如何使用代码保护服务。 第四个和第五个过程演示如何使用配置文件保护服务。  
  
## <a name="using-code"></a>使用代码  
 服务和客户端的完整代码位于本主题末尾的“示例”一节中。  
  
 第一个过程演练创建和配置<xref:System.ServiceModel.WSHttpBinding>在代码中的类。 该绑定使用 HTTP 传输。 在客户端上使用了同一绑定。  
  
#### <a name="to-create-a-wshttpbinding-that-uses-windows-credentials-and-message-security"></a>创建使用 Windows 凭据和消息安全的 WSHttpBinding  
  
1.  在“示例”一节的服务代码中，将此过程的代码插入到 `Run` 类的 `Test` 方法开头。  
  
2.  创建的实例<xref:System.ServiceModel.WSHttpBinding>类。  
  
3.  设置<xref:System.ServiceModel.WsHttpSecurity.Mode%2A>属性<xref:System.ServiceModel.WsHttpSecurity>类<xref:System.ServiceModel.SecurityMode>。  
  
4.  设置<xref:System.ServiceModel.MessageSecurityOverHttp.ClientCredentialType%2A>属性<xref:System.ServiceModel.MessageSecurityOverHttp>类<xref:System.ServiceModel.MessageCredentialType>。  
  
5.  此过程的代码如下：  
  
     [!code-csharp[c_SecureWindowsService#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewindowsservice/cs/secureservice.cs#1)]
     [!code-vb[c_SecureWindowsService#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewindowsservice/vb/secureservice.vb#1)]  
  
### <a name="using-the-binding-in-a-service"></a>在服务中使用该绑定  
 这是第二个过程，演示如何在自承载服务中使用该绑定。 [!INCLUDE[crabout](../../../includes/crabout-md.md)]承载服务，请参见[托管服务](../../../docs/framework/wcf/hosting-services.md)。  
  
##### <a name="to-use-a-binding-in-a-service"></a>在服务中使用绑定  
  
1.  在上一过程的代码之后插入此过程的代码。  
  
2.  创建<xref:System.Type>变量名为`contractType`并将其分配接口类型 (`ICalculator`)。 在使用 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 时，请使用 `GetType` 运算符；在使用 C# 时，请使用 `typeof` 关键字。  
  
3.  创建另一个名为 `Type` 的 `serviceType` 变量，并为其分配所实现的协定的类型 (`Calculator`)。  
  
4.  创建的实例<xref:System.Uri>类名为`baseAddress`与该服务的基址。 基址必须具有与传输匹配的方案。 在本示例中，传输方案为 HTTP，且地址包含特殊的统一资源标识符 (URI)“localhost”和端口号 (8036)，以及一个终结点基址（“serviceModelSamples/”）：http://localhost:8036/serviceModelSamples/。  
  
5.  创建的实例<xref:System.ServiceModel.ServiceHost>类`serviceType`和`baseAddress`变量。  
  
6.  使用 `contractType`、绑定和终结点名称 (secureCalculator) 将一个终结点添加到服务中。 在启动对服务的调用时，客户端必须将基址和终结点名称连接起来。  
  
7.  调用<xref:System.ServiceModel.Channels.CommunicationObject.Open%2A>方法以启动服务。 此过程的代码如下所示：  
  
     [!code-csharp[c_SecureWindowsService#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewindowsservice/cs/secureservice.cs#2)]
     [!code-vb[c_SecureWindowsService#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewindowsservice/vb/secureservice.vb#2)]  
  
### <a name="using-the-binding-in-a-client"></a>在客户端中使用该绑定  
 此过程演示如何生成与服务进行通信的代理。 使用生成代理[ServiceModel 元数据实用工具 (Svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)它使用服务元数据创建代理。  
  
 此过程还创建的实例<xref:System.ServiceModel.WSHttpBinding>类与服务通信，然后再调用该服务。  
  
 本示例仅使用代码来创建客户端。 另一种方法是使用配置文件，如此过程之后的一节所示。  
  
##### <a name="to-use-a-binding-in-a-client-with-code"></a>通过代码在客户端中使用绑定  
  
1.  使用 SvcUtil.exe 工具根据服务的元数据生成代理代码。 [!INCLUDE[crdefault](../../../includes/crdefault-md.md)][如何︰ 创建客户端](../../../docs/framework/wcf/how-to-create-a-wcf-client.md)。 生成的代理代码继承自<xref:System.ServiceModel.ClientBase%601>类，这确保每个客户端具有必要的构造函数、 方法和属性，以与通信[!INCLUDE[indigo2](../../../includes/indigo2-md.md)]服务。 在本示例中，生成的代码包括 `CalculatorClient` 类，该类实现了 `ICalculator` 接口，以便与服务代码兼容。  
  
2.  在客户端程序的 `Main` 方法的开头插入此过程的代码。  
  
3.  创建的实例<xref:System.ServiceModel.WSHttpBinding>类并将其安全模式设置为`Message`和其客户端凭据类型设置为`Windows`。 本示例将变量命名为 `clientBinding`。  
  
4.  创建的实例<xref:System.ServiceModel.EndpointAddress>类名为`serviceAddress`。 将基址与终结点名称连接起来以初始化该实例。  
  
5.  使用 `serviceAddress` 和 `clientBinding` 变量创建所生成的客户端类的一个实例。  
  
6.  调用<xref:System.ServiceModel.ClientBase%601.Open%2A>方法，如下面的代码中所示。  
  
7.  调用服务并显示结果。  
  
     [!code-csharp[c_secureWindowsClient#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewindowsclient/cs/secureclient.cs#1)]
     [!code-vb[c_secureWindowsClient#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewindowsclient/vb/secureclient.vb#1)]  
  
## <a name="using-the-configuration-file"></a>使用配置文件  
 如果不用程序代码创建绑定，还可以使用下面所示的配置文件绑定节的代码。  
  
 如果没有定义的服务，请参阅[设计和实现服务](../../../docs/framework/wcf/designing-and-implementing-services.md)，和[配置服务](../../../docs/framework/wcf/configuring-services.md)。  
  
 **请注意**服务和客户端配置文件中使用此配置代码。  
  
#### <a name="to-enable-transfer-security-on-a-service-in-a-windows-domain-using-configuration"></a>使用配置在 Windows 域中的服务上启用传输安全  
  
1.  添加[ <> \> ](../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)元素[ <> \> ](../../../docs/framework/configure-apps/file-schema/wcf/bindings.md)元素节的配置的配置文件。  
  
2.  将一个 <`binding`> 元素添加到 <`WSHttpBinding`> 元素中，并将 `configurationName` 属性设置为适合于应用程序的值。  
  
3.  添加一个 <`security`> 元素，并将 `mode` 属性设置为 Message。  
  
4.  添加一个 <`message`> 元素，并将 `clientCredentialType` 属性设置为 Windows。  
  
5.  在服务的配置文件中，使用下面的代码替换 `<bindings>` 节。 如果没有服务配置文件，请参阅[使用绑定配置服务和客户端](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)。  
  
    ```  
    <bindings>  
      <wsHttpBinding>  
       <binding name = "wsHttpBinding_Calculator">  
         <security mode="Message">  
           <message clientCredentialType="Windows"/>  
         </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
    ```  
  
### <a name="using-the-binding-in-a-client"></a>在客户端中使用该绑定  
 此过程演示如何生成两个文件：一个与服务进行通信的代理和一个配置文件。 此过程还描述对客户端程序所做的更改，这是在客户端使用的第三个文件。  
  
##### <a name="to-use-a-binding-in-a-client-with-configuration"></a>通过配置在客户端中使用绑定  
  
1.  使用 SvcUtil.exe 工具根据服务的元数据生成代理代码和配置文件。 [!INCLUDE[crdefault](../../../includes/crdefault-md.md)][如何︰ 创建客户端](../../../docs/framework/wcf/how-to-create-a-wcf-client.md)。  
  
2.  替换[ <> \> ](../../../docs/framework/configure-apps/file-schema/wcf/bindings.md)与上一节中的配置代码生成的配置文件部分。  
  
3.  在客户端程序的 `Main` 方法的开头插入程序代码。  
  
4.  通过将配置文件中的绑定名称作为输入参数进行传递，创建所生成的客户端类的实例。  
  
5.  调用<xref:System.ServiceModel.ClientBase%601.Open%2A>方法，如下面的代码中所示。  
  
6.  调用服务并显示结果。  
  
     [!code-csharp[c_secureWindowsClient#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewindowsclient/cs/secureclient.cs#2)]  
  
## <a name="example"></a>示例  
 [!code-csharp[c_SecureWindowsService#0](../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewindowsservice/cs/secureservice.cs#0)]  
  
 [!code-csharp[c_SecureWindowsClient#0](../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewindowsclient/cs/secureclient.cs#0)]
 <!-- TODO: review snippet reference [!code-vb[c_SecureWindowsClient#0](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewindowsclient/vb/secureclient.vb#0)]  -->  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.ServiceModel.WSHttpBinding>   
 [ServiceModel 元数据实用工具 (Svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)   
 [如何︰ 创建客户端](../../../docs/framework/wcf/how-to-create-a-wcf-client.md)   
 [保证服务的安全](../../../docs/framework/wcf/securing-services.md)   
 [安全性概述](../../../docs/framework/wcf/feature-details/security-overview.md)