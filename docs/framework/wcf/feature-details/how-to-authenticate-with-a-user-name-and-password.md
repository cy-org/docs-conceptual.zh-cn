---
title: "如何：使用用户名和密码进行身份验证 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "身份验证 [WCF], 用户名和密码"
ms.assetid: a5415be2-0ef3-464c-9f76-c255cb8165a4
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# 如何：使用用户名和密码进行身份验证
本主题演示如何让 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务使用 Windows 域用户名和密码来对客户端进行身份验证。它假定您有一个工作，自承载的 WCF 服务。例如，创建基本的自承载 WCF 服务，请参见[入门教程](../../../../docs/framework/wcf/getting-started-tutorial.md)。本主题假定在代码中配置服务。如果你想看到使用配置文件配置类似服务的示例，请参见[用户名消息安全](../../../../docs/framework/wcf/samples/message-security-user-name.md)  
  
 要配置服务以使用 Windows 域的用户名和密码对客户端进行身份验证，使用 <xref:System.ServiceModel.WSHttpBinding>，并将其 `Security.Mode` 属性设置为`Message`。此外，您必须指定 X509证书，该证书将用于加密从客户端发送到服务的用户名和密码。  
  
 在客户端上，必须提示用户用户名和密码，并指定用户在 WCF 客户端代理服务器上的凭据。  
  
### 配置 WCF 服务以便使用 Windows 域的用户名和密码进行身份验证。  
  
1.  创建 <xref:System.ServiceModel.WSHttpBinding> 的实例，将绑定的安全性模式设置为 `SecurityMode.Message`，将绑定的 `ClientCredentialType` 设置为 `MessageCredentialType.UserName`，并使用配置的绑定将服务终结点添加到服务主机，如下面的代码中所示：  
  
    ```  
    // ...  
    WSHttpBinding userNameBinding = new WSHttpBinding();  
    userNameBinding.Security.Mode = SecurityMode.Message;  
    userNameBinding.Security.Message.ClientCredentialType = MessageCredentialType.UserName;  
    svcHost.AddServiceEndpoint(typeof(IService1), userNameBinding, "");  
    // ...  
    ```  
  
2.  指定用于加密通过网络发送的用户名和密码信息的服务器证书。此代码应紧跟在上面的代码之后。以下示例使用通过[用户名消息安全](../../../../docs/framework/wcf/samples/message-security-user-name.md)示例中的 setup.bat 文件创建的证书。  
  
    ```  
    // ...  
    svcHost.Credentials.ServiceCertificate.SetCertificate(StoreLocation.LocalMachine, StoreName.My, X509FindType.FindBySubjectName, "localhost");  
    // ...  
    ```  
  
     您可以使用您自己的证书，只是修改代码以引用您的证书。关于创建和使用证书的更多信息，请参见 [使用证书](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)。确保证书在本地计算机的受信任人证书存储区中。您可以通过运行 mmc.exe 并选择**“文件”**、**“添加\/删除管理单元…”**菜单项完成此操作。在**“添加或删除管理单元”**对话框中，选择**“证书管理单元”**，然后单击**“添加”**。在“证书管理单元”中，选择**“计算机帐户”**。默认情况下，从消息安全用户名称示例生成的证书将位于个人\/证书文件夹中。它将在 MMC窗口中的“持有者”列下列为“localhost”。拖放证书到**“受信任人”**文件夹中。这将允许 WCF 在执行身份验证时，将证书视为受信任的证书。  
  
### 调用服务密码传递用户名和密码的步骤  
  
1.  客户端应用程序必须提示用户输入其用户名和密码。下面的代码要求用户输入用户名和密码。  
  
    > [!WARNING]
    >  密码不应在生产中使用，因为密码在输入时显示。  
  
    ```  
    public static void GetPassword(out string username, out string password)  
            {  
                Console.WriteLine("Provide a valid machine or domain account. [domain\\user]");  
                Console.WriteLine("   Enter username:");  
                username = Console.ReadLine();  
                Console.WriteLine("   Enter password:");  
                password = Console.ReadLine();             
                return;  
            }  
  
    ```  
  
2.  创建客户端代理的一个实例，指定客户端的证书，如下面的代码所示。  
  
    ```  
    string username;  
    string password;  
  
    // Instantiate the proxy  
    Service1Client proxy = new Service1Client();  
  
    // Prompt the user for username & password  
    GetPassword(out username, out password);  
  
    // Set the user’s credentials on the proxy  
    proxy.ClientCredentials.UserName.UserName = username;  
    proxy.ClientCredentials.UserName.Password = password;  
  
    // Treat the test certificate as trusted  
    proxy.ClientCredentials.ServiceCertificate.Authentication.CertificateValidationMode = System.ServiceModel.Security.X509CertificateValidationMode.PeerOrChainTrust;  
    // Call the service operation using the proxy  
    ```  
  
## 请参阅  
 <xref:System.ServiceModel.WsHttpBinding>   
 <xref:System.ServiceModel.WSHttpSecurity>   
 <xref:System.ServiceModel.SecurityMode>   
 <xref:System.ServiceModel.Security.UserNamePasswordClientCredential.UserName%2A>   
 <xref:System.ServiceModel.Security.UserNamePasswordClientCredential.Password%2A>   
 <xref:System.ServiceModel.Security.UserNamePasswordClientCredential>   
 <xref:System.ServiceModel.WSHttpSecurity.Mode%2A>   
 <xref:System.ServiceModel.HttpTransportSecurity.ClientCredentialType%2A>   
 [通过基本身份验证确保的传输安全](../../../../docs/framework/wcf/feature-details/transport-security-with-basic-authentication.md)   
 [分布式应用程序安全](../../../../docs/framework/wcf/feature-details/distributed-application-security.md)   
 [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)