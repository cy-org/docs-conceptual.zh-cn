---
title: "如何：使用 X.509 证书保证服务的安全 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2d06c2aa-d0d7-4e5e-ad7e-77416aa1c10b
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 8
---
# 如何：使用 X.509 证书保证服务的安全
使用 X.509 证书保证服务的安全是 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 中多数绑定使用的基本技术。本主题演练使用 X.509 证书配置自承载服务的步骤。  
  
 先决条件是具有可用于对服务器进行身份验证的有效证书。证书必须由受信任的证书颁发机构颁发给服务器。如果证书无效，则尝试使用该服务的任何客户端都不会信任该服务，因此不会建立连接。[!INCLUDE[crabout](../../../../includes/crabout-md.md)] 使用证书，请参见 [使用证书](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)。  
  
### 使用代码用证书配置服务  
  
1.  创建服务协定和实现的服务。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][设计和实现服务](../../../../docs/framework/wcf/designing-and-implementing-services.md).  
  
2.  创建 <xref:System.ServiceModel.WSHttpBinding> 类的一个实例，并将其安全模式设置为 <xref:System.ServiceModel.SecurityMode>，如下面的代码所示。  
  
     [!code-csharp[C_SecureWithCertificate#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#1)]
     [!code-vb[C_SecureWithCertificate#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#1)]  
  
3.  创建两个 <xref:System.Type> 变量，分别用于协定类型和实现的协定，如下面的代码所示。  
  
     [!code-csharp[C_SecureWithCertificate#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#2)]
     [!code-vb[C_SecureWithCertificate#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#2)]  
  
4.  为服务的基址创建 <xref:System.Uri> 类的一个实例。由于 `WSHttpBinding` 使用 HTTP 传输，因此，统一资源标识符 \(URI\) 必须以该架构开始，否则打开服务时，[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 将引发异常。  
  
     [!code-csharp[C_SecureWithCertificate#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#3)]
     [!code-vb[C_SecureWithCertificate#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#3)]  
  
5.  使用实现的协定类型变量和 URI 创建 <xref:System.ServiceModel.ServiceHost> 类的新实例。  
  
     [!code-csharp[C_SecureWithCertificate#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#4)]
     [!code-vb[C_SecureWithCertificate#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#4)]  
  
6.  使用 <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A> 方法向服务中添加一个 <xref:System.ServiceModel.Description.ServiceEndpoint>。将协定、绑定和终结点地址传递给构造函数，如下面的代码所示。  
  
     [!code-csharp[C_SecureWithCertificate#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#5)]
     [!code-vb[C_SecureWithCertificate#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#5)]  
  
7.  可选。若要从服务中检索元数据，请创建一个新的 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 对象并将 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpGetEnabled%2A> 属性设置为 `true`。  
  
     [!code-csharp[C_SecureWithCertificate#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#6)]
     [!code-vb[C_SecureWithCertificate#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#6)]  
  
8.  使用 <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential> 类的 <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential.SetCertificate%2A> 方法将有效证书添加到服务中。该方法可以使用多个方法之一查找证书。本示例使用 <xref:System.Security.Cryptography.X509Certificates.X509FindType> 枚举。该枚举指定提供的值是为其颁发证书的实体的名称。  
  
     [!code-csharp[C_SecureWithCertificate#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#7)]
     [!code-vb[C_SecureWithCertificate#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#7)]  
  
9. 调用 <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A> 方法以开始服务侦听。如果您要创建控制台应用程序，请调用 <xref:System.Console.ReadLine%2A> 方法以保持服务处于侦听状态。  
  
     [!code-csharp[C_SecureWithCertificate#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#8)]
     [!code-vb[C_SecureWithCertificate#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#8)]  
  
## 示例  
 下面的示例使用 <xref:System.ServiceModel.Security.X509CertificateRecipientServiceCredential.SetCertificate%2A> 方法用 X.509 证书配置服务。  
  
 [!code-csharp[C_SecureWithCertificate#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewithcertificate/cs/source.cs#9)]
 [!code-vb[C_SecureWithCertificate#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewithcertificate/vb/source.vb#9)]  
  
## 编译代码  
 编译该代码需要以下命名空间：  
  
-   <xref:System>  
  
-   <xref:System.ServiceModel>  
  
-   <xref:System.ServiceModel.Channels>  
  
-   <xref:System.Web.Services.Description>  
  
-   <xref:System.Security.Cryptography.X509Certificates>  
  
-   <xref:System.Runtime.Serialization>  
  
## 请参阅  
 [使用证书](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)