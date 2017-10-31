---
title: "基于消息队列的消息安全性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 329aea9c-fa80-45c0-b2b9-e37fd7b85b38
caps.latest.revision: 22
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 22
---
# 基于消息队列的消息安全性
此示例演示如何实现一个应用程序，该应用程序对客户端使用 WS\-Security 和 X.509v3 证书身份验证，并要求使用服务器的 X.509v3 证书对 MSMQ 进行服务器身份验证。有时候消息安全性更重要，以确保 MSMQ 存储区中的消息始终是加密的，并且应用程序能够对消息执行其自己的身份验证。  
  
 本示例基于[已经过事务处理的 MSMQ 绑定](../../../../docs/framework/wcf/samples/transacted-msmq-binding.md)示例。消息已经过加密和签名。  
  
### 设置、生成和运行示例  
  
1.  请确保已经执行了 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  如果先运行服务，则它将检查以确保队列存在。如果队列不存在，则服务将创建一个队列。可以先运行服务以创建队列或通过 MSMQ 队列管理器创建一个队列。执行下面的步骤来在 Windows 2008 中创建队列。  
  
    1.  在 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 中打开服务器管理器。  
  
    2.  展开**“功能”**选项卡。  
  
    3.  右击**“私有消息队列”**，然后选择**“新建”**和**“专用队列”**。  
  
    4.  选中**“事务性”**框。  
  
    5.  输入 `ServiceModelSamplesTransacted` 作为新队列的名称。  
  
3.  若要生成 C\# 或 Visual Basic .NET 版本的解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
### 在同一计算机上运行示例  
  
1.  请确保路径包括 Makecert.exe 和 FindPrivateKey.exe 所在的文件夹。  
  
2.  运行示例安装文件夹中的 Setup.bat。这将安装运行示例所需的所有证书。  
  
    > [!NOTE]
    >  请确保在运行完该示例后通过运行 Cleanup.bat 来移除证书。其他安全示例使用相同的证书。  
  
3.  启动 \\service\\bin 中的 Service.exe。  
  
4.  启动 \\client\\bin 中的 Client.exe。客户端活动将显示在客户端控制台应用程序上。  
  
5.  如果客户端与服务无法进行通信，请参见[Troubleshooting Tips](http://msdn.microsoft.com/zh-cn/8787c877-5e96-42da-8214-fa737a38f10b)。  
  
### 跨计算机运行示例  
  
1.  将 Setup.bat、Cleanup.bat 和 ImportClientCert.bat 文件复制到服务计算机上。  
  
2.  在客户端计算机上为这些客户端二进制文件创建一个目录。  
  
3.  将客户端程序文件复制到客户端计算机上的客户端目录中。另外，将 Setup.bat、Cleanup.bat 和 ImportServiceCert.bat 文件复制到客户端上。  
  
4.  在服务器上运行 `setup.bat service`。如果采用 `service` 参数运行 `setup.bat` ，则使用计算机的完全限定域名创建一个服务证书，并将此服务证书导出到名为 Service.cer 的文件中。  
  
5.  编辑服务的 service.exe.config 以反映新的证书名称（在 [\<serviceCertificate\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)的 `findValue` 属性中），该名称与计算机的完全限定域名相同。  
  
6.  将服务目录中的 Service.cer 文件复制到客户端计算机上的客户端目录中。  
  
7.  在客户端上，运行 `setup.bat client`。如果使用 `client` 参数运行 `setup.bat` ，则会创建一个名为 client.com 的客户端证书，并将此客户端证书导出到名为 Client.cer 的文件中。  
  
8.  在客户端计算机上的 Client.exe.config 文件中，更改终结点的地址值，使其与服务的新地址相匹配。通过用服务器的完全限定域名替换 localhost 来执行此操作。还必须更改服务的证书名称，使其与服务计算机的完全限定域名相同（在 `clientCredentials` 下的 `serviceCertificate` 的 `defaultCertificate` 元素的 `findValue` 属性中）。  
  
9. 将客户端目录中的 Client.cer 文件复制到服务器上的服务目录中。  
  
10. 在客户端上，运行 `ImportServiceCert.bat`。这会将 Service.cer 文件中的服务证书导入 CurrentUser – TrustedPeople 存储区。  
  
11. 在服务器上，运行 `ImportClientCert.bat`，这会将 Client.cer 文件中的客户端证书导入 LocalMachine \- TrustedPeople 存储区。  
  
12. 在服务计算机上，在命令提示符下启动 Service.exe。  
  
13. 在客户端计算机上，在命令提示符下启动 Client.exe。如果客户端与服务无法进行通信，请参见[Troubleshooting Tips](http://msdn.microsoft.com/zh-cn/8787c877-5e96-42da-8214-fa737a38f10b)。  
  
### 运行示例后进行清理  
  
-   运行完示例后运行示例文件夹中的 Cleanup.bat。  
  
    > [!NOTE]
    >  此脚本不会在跨计算机运行此示例时移除客户端上的服务证书。如果已运行跨计算机使用证书的 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 示例，请确保清除已安装在 CurrentUser \- TrustedPeople 存储中的服务证书。为此，请使用以下命令：`certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>`，例如：`certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`。  
  
## 要求  
 此示例要求安装并运行 MSMQ。  
  
## 演示  
 客户端使用服务的公钥对消息进行加密，并使用其自己的证书对消息进行签名。从队列中读取消息的服务使用其受信任人的存储区中的证书对客户端证书进行身份验证。然后它对消息进行解密并将消息调度给服务操作。  
  
 因为 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 消息是作为负载通过 MSMQ 消息的正文携带的，所以正文在 MSMQ 存储区中依然保持加密状态。这样可以保护消息，以防意外泄漏。请注意，MSMQ 本身并不知道它携带的消息是否经过加密。  
  
 此示例演示如何在消息级别对 MSMQ 进行相互身份验证。证书是在带外交换的。对于排队的应用程序始终是这样，因为服务和客户端不是必须同时处于开启状态并正在运行。  
  
## 说明  
 示例客户端和服务代码与[已经过事务处理的 MSMQ 绑定](../../../../docs/framework/wcf/samples/transacted-msmq-binding.md)示例基本相同，只有一点不同。操作协定是通过保护级别表示的，这说明消息必须是经过签名和加密的。  
  
```  
// Define a service contract.   
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface IOrderProcessor  
{  
    [OperationContract(IsOneWay = true, ProtectionLevel=ProtectionLevel.EncryptAndSign)]  
    void SubmitPurchaseOrder(PurchaseOrder po);  
}  
```  
  
 为了确保使用所要求的令牌来标识服务和客户端以保证消息的安全性，App.config 中包含了凭据信息。  
  
 客户端配置指定要用来对服务进行身份验证的服务证书。它使用其本地计算机存储区作为受信任的存储区，以依赖服务的有效性。它还指定消息所附加的用来对客户端进行服务身份验证的客户端证书。  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  
  <system.serviceModel>  
  
    <client>  
      <!-- Define NetMsmqEndpoint -->  
      <endpoint address="net.msmq://localhost/private/ServiceModelSamplesMessageSecurity"   
                binding="netMsmqBinding"   
                bindingConfiguration="messageSecurityBinding"  
                contract="Microsoft.ServiceModel.Samples.IOrderProcessor"  
                behaviorConfiguration="ClientCertificateBehavior" />  
    </client>  
  
    <bindings>  
        <netMsmqBinding>  
            <binding name="messageSecurityBinding">  
                <security mode="Message">  
                    <message clientCredentialType="Certificate"/>  
                </security>  
            </binding>  
        </netMsmqBinding>  
    </bindings>  
  
    <behaviors>  
      <endpointBehaviors>  
        <behavior name="ClientCertificateBehavior">  
          <!--   
        The clientCredentials behavior allows one to define a certificate to present to a service.  
        A certificate is used by a client to authenticate itself to the service and provide message integrity.  
        This configuration references the "client.com" certificate installed during the setup instructions.  
        -->  
          <clientCredentials>  
            <clientCertificate findValue="client.com" storeLocation="CurrentUser" storeName="My" x509FindType="FindBySubjectName" />  
            <serviceCertificate>  
                <defaultCertificate findValue="localhost" storeLocation="CurrentUser" storeName="TrustedPeople" x509FindType="FindBySubjectName"/>  
              <!--   
            Setting the certificateValidationMode to PeerOrChainTrust means that if the certificate   
            is in the user's Trusted People store, then it is trusted without performing a  
            validation of the certificate's issuer chain. This setting is used here for convenience so that the   
            sample can be run without having to have certificates issued by a certification authority (CA).  
            This setting is less secure than the default, ChainTrust. The security implications of this   
            setting should be carefully considered before using PeerOrChainTrust in production code.   
            -->  
              <authentication certificateValidationMode="PeerOrChainTrust" />  
            </serviceCertificate>  
          </clientCredentials>  
        </behavior>  
      </endpointBehaviors>  
    </behaviors>  
  
  </system.serviceModel>  
</configuration>  
```  
  
 请注意，安全模式设置为“消息”，而 ClientCredentialType 设置为“证书”。  
  
 服务配置中包括一个服务行为，该行为指定客户端对服务进行身份验证时使用的服务的凭据。服务器证书主题名称是在 [\<serviceCredentials\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md)的 `findValue` 属性中指定的。  
  
```  
  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  
  <appSettings>  
    <!-- Use appSetting to configure MSMQ queue name. -->  
    <add key="queueName" value=".\private$\ServiceModelSamplesMessageSecurity" />  
  </appSettings>  
  
  <system.serviceModel>  
    <services>  
      <service   
          name="Microsoft.ServiceModel.Samples.OrderProcessorService"  
          behaviorConfiguration="PurchaseOrderServiceBehavior">  
        <host>  
          <baseAddresses>  
            <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>  
          </baseAddresses>  
        </host>  
        <!-- Define NetMsmqEndpoint -->  
        <endpoint address="net.msmq://localhost/private/ServiceModelSamplesMessageSecurity"  
                  binding="netMsmqBinding"  
                  bindingConfiguration="messageSecurityBinding"  
                  contract="Microsoft.ServiceModel.Samples.IOrderProcessor" />  
        <!-- The mex endpoint is exposed at http://localhost:8000/ServiceModelSamples/service/mex. -->  
        <endpoint address="mex"  
                  binding="mexHttpBinding"  
                  contract="IMetadataExchange" />  
      </service>  
    </services>  
  
    <bindings>  
        <netMsmqBinding>  
            <binding name="messageSecurityBinding">  
                <security mode="Message">  
                    <message clientCredentialType="Certificate" />  
                </security>  
            </binding>  
        </netMsmqBinding>  
    </bindings>  
  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="PurchaseOrderServiceBehavior">  
          <serviceMetadata httpGetEnabled="True"/>  
          <!--   
               The serviceCredentials behavior allows one to define a service certificate.  
               A service certificate is used by the service to authenticate itself to its clients and to provide message protection.  
               This configuration references the "localhost" certificate installed during the setup instructions.  
          -->  
          <serviceCredentials>  
            <serviceCertificate findValue="localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectName" />  
            <clientCertificate>  
                <certificate findValue="client.com" storeLocation="LocalMachine" storeName="TrustedPeople" x509FindType="FindBySubjectName"/>  
              <!--   
            Setting the certificateValidationMode to PeerOrChainTrust means that if the certificate   
            is in the user's Trusted People store, then it is trusted without performing a  
            validation of the certificate's issuer chain. This setting is used here for convenience so that the   
            sample can be run without having to have certificates issued by a certification authority (CA).  
            This setting is less secure than the default, ChainTrust. The security implications of this   
            setting should be carefully considered before using PeerOrChainTrust in production code.   
            -->  
              <authentication certificateValidationMode="PeerOrChainTrust" />  
            </clientCertificate>  
          </serviceCredentials>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  
  </system.serviceModel>  
  
</configuration>  
  
```  
  
 此示例演示如何使用配置控制身份验证，以及如何从安全上下文中获取调用方的标识，如下面的示例代码所述：  
  
```  
    // Service class which implements the service contract.  
    // Added code to write output to the console window.  
    public class OrderProcessorService : IOrderProcessor  
    {  
        private string GetCallerIdentity()  
        {  
            // The client certificate is not mapped to a Windows identity by default.  
            // ServiceSecurityContext.PrimaryIdentity is populated based on the information  
            // in the certificate that the client used to authenticate itself to the service.  
            return ServiceSecurityContext.Current.PrimaryIdentity.Name;  
        }  
  
        [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = true)]  
        public void SubmitPurchaseOrder(PurchaseOrder po)  
        {  
            Console.WriteLine("Client's Identity {0} ", GetCallerIdentity());  
            Orders.Add(po);  
            Console.WriteLine("Processing {0} ", po);  
        }  
  //…  
}  
```  
  
 运行时，服务代码将显示客户端标识。下面提供了服务代码的示例输出：  
  
```  
The service is ready.  
Press <ENTER> to terminate service.  
  
Client's Identity CN=client.com; ECA6629A3C695D01832D77EEE836E04891DE9D3C  
Processing Purchase Order: 6536e097-da96-4773-9da3-77bab4345b5d  
        Customer: somecustomer.com  
        OrderDetails  
                Order LineItem: 54 of Blue Widget @unit price: $29.99  
                Order LineItem: 890 of Red Widget @unit price: $45.89  
        Total cost of this order: $42461.56  
        Order status: Pending  
```  
  
## 注释  
  
-   创建客户端证书。  
  
     批处理文件中的以下行用于创建客户端证书。创建的证书的主题名称中会使用指定的客户端名称。证书存储在 `CurrentUser` 存储位置下的 `My` 存储区中。  
  
    ```  
    echo ************  
    echo making client cert  
    echo ************  
    makecert.exe -sr CurrentUser -ss MY -a sha1 -n CN=%CLIENT_NAME% -sky exchange -pe  
  
    ```  
  
-   将客户端证书安装到服务器的受信任证书存储区中。  
  
     批处理文件中的以下行将客户端证书复制到服务器的 TrustedPeople 存储中，以使服务器能够做出相关的信任或非信任决定。为了使 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务信任安装在 TrustedPeople 存储区中的证书，必须将客户端证书验证模式设置为 `PeerOrChainTrust` 或 `PeerTrust` 值。请参见前面的服务配置示例，了解如何使用配置文件完成此操作。  
  
    ```  
    echo ************  
    echo copying client cert to server's LocalMachine store  
    echo ************  
    certmgr.exe -add -r CurrentUser -s My -c -n %CLIENT_NAME% -r LocalMachine -s TrustedPeople  
  
    ```  
  
-   创建服务器证书。  
  
     Setup.bat 批处理文件中的以下行创建将要使用的服务器证书：  
  
    ```  
    echo ************  
    echo Server cert setup starting  
    echo %SERVER_NAME%  
    echo ************  
    echo making server cert  
    echo ************  
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe  
    ```  
  
     %SERVER\_NAME% 变量指定服务器名称。该证书存储在 LocalMachine 存储区中。如果用服务参数（如 `setup.bat service`）运行 setup 批处理文件，则 %SERVER\_NAME% 包含计算机的完全限定域名。否则，它默认为 localhost。  
  
-   将服务器证书安装到客户端的受信任证书存储区中。  
  
     以下行将服务器证书复制到客户端的受信任人存储中。因为客户端系统不隐式信任 Makecert.exe 生成的证书，所以需要执行此步骤。如果已经拥有一个证书，该证书来源于客户端的受信任根证书（例如由 Microsoft 颁发的证书），则不需要执行使用服务器证书填充客户端证书存储区这一步骤。  
  
    ```  
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople  
    ```  
  
    > [!NOTE]
    >  如果您使用的是非美国对于英文版本的 Microsoft Windows，必须编辑 Setup.bat 文件，并用与您所在的区域对应的帐户名替换“NT AUTHORITY\\NETWORK SERVICE”帐户名。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Binding\Net\MSMQ\MessageSecurity`  
  
## 请参阅