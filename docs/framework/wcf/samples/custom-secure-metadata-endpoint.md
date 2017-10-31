---
title: "自定义安全元数据终结点 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9e369e99-ea4a-49ff-aed2-9fdf61091a48
caps.latest.revision: 19
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 19
---
# 自定义安全元数据终结点
本示例演示如何实现一个具有安全元数据终结点（使用一个非元数据交换绑定）的服务，以及如何配置 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 或客户端以从此类元数据终结点中获取元数据。有两个系统提供的绑定可供公开元数据终结点：mexHttpBinding 和 mexHttpsBinding。mexHttpBinding 用于非安全的方式，通过 HTTP 公开元数据终结点。mexHttpsBinding 以安全的方式，通过 HTTP 公开元数据终结点。本示例演示如何使用 <xref:System.ServiceModel.WSHttpBinding> 公开安全元数据终结点。要更改绑定的安全设置但不想使用 HTTPS 时需要这样做。如果使用 mexHttpsBinding，则元数据终结点是安全的，但无法修改绑定设置。  
  
> [!NOTE]
>  本主题的末尾介绍了此示例的设置过程和生成说明。  
  
## 服务  
 本示例中的服务有两个终结点。应用程序终结点可用于 `WSHttpBinding` 上的 `ICalculator` 协定，其中启用了 `ReliableSession` 并且 `Message` 安全性为使用证书。元数据终结点还使用具有相同安全设置但没有 `ReliableSession` 的 `WSHttpBinding`。下面是相关的配置：  
  
```  
<services>  
    …  
    <service name="Microsoft.ServiceModel.Samples.CalculatorService"  
            behaviorConfiguration="CalculatorServiceBehavior">  
     <!-- use base address provided by host -->  
     <endpoint address=""  
       binding="wsHttpBinding"  
       bindingConfiguration="Binding2"  
       contract="Microsoft.ServiceModel.Samples.ICalculator" />  
     <endpoint address="mex"  
       binding="wsHttpBinding"  
       bindingConfiguration="Binding1"  
       contract="IMetadataExchange" />  
     </service>  
 </services>  
 <bindings>  
   <wsHttpBinding>  
     <binding name="Binding1">  
       <security mode="Message">  
         <message clientCredentialType="Certificate" />  
       </security>  
     </binding>  
     <binding name="Binding2">  
       <reliableSession inactivityTimeout="00:01:00" enabled="true" />  
       <security mode="Message">  
         <message clientCredentialType="Certificate" />  
       </security>  
     </binding>  
   </wsHttpBinding>  
 </bindings>  
```  
  
 在很多其他示例中，元数据终结点使用默认 `mexHttpBinding`，这样会不安全。下面是使用具有 `Message` 安全性的 `WSHttpBinding` 来保护的元数据。为了使元数据客户端能够检索此元数据，必须用匹配的绑定来配置这些客户端。本示例演示两个此类客户端。  
  
 第一个客户端使用 Svcutil.exe 获取元数据并在设计时生成客户端代码和配置。由于服务针对元数据使用非默认绑定，因此必须专门配置 Svcutil.exe 工具，以便此工具能够使用该绑定从服务中获取元数据。  
  
 第二个客户端使用 `MetadataResolver` 动态获取已知协定的元数据，然后在动态生成的客户端上调用操作。  
  
## Svcutil 客户端  
 当使用默认绑定承载您的 `IMetadataExchange` 终结点时，可以使用该终结点的地址运行 Svcutil.exe：  
  
```  
svcutil http://localhost/servicemodelsamples/service.svc/mex  
```  
  
 它正常工作。但在本示例中，服务器使用非默认终结点承载元数据。因此，必须指示 Svcutil.exe 使用正确的绑定。使用 Svcutil.exe.config 文件可以实现此目标。  
  
 Svcutil.exe.config 文件类似于普通的客户端配置文件。唯一不同之处是客户端终结点名称和协定：  
  
```  
<endpoint name="http"  
          binding="wsHttpBinding"  
          bindingConfiguration="Binding1"  
          behaviorConfiguration="ClientCertificateBehavior"  
          contract="IMetadataExchange" />  
```  
  
 终结点名称必须是承载该元数据的地址的方案名称，终结点协定必须为 `IMetadataExchange`。因此，当使用如下所示的命令行运行 Svcutil.exe 时：  
  
```  
svcutil http://localhost/servicemodelsamples/service.svc/mex  
```  
  
 它查找名为“http”的终结点和 `IMetadataExchange` 协定，以使用元数据终结点配置通信交换的绑定和行为。示例中的 Svcutil.exe.config 文件的其余部分指定绑定配置和行为凭据以与元数据终结点的服务器配置相匹配。  
  
 为了使 Svcutil.exe 能够在 Svcutil.exe.config 中选取配置，Svcutil.exe 必须与该配置文件位于同一目录中。因此，您必须将 Svcutil.exe 从其安装位置复制到包含 Svcutil.exe.config 文件的目录中。然后，从该目录中运行以下命令：  
  
```  
.\svcutil.exe http://localhost/servicemodelsamples/service.svc/mex  
```  
  
 领先"。\\" 确保运行此目录（具有相应的 Svcutil.exe.config 的目录）中的 Svcutil.exe 副本。  
  
## MetadataResolver 客户端  
 如果客户端在设计时知道协定和如何与元数据交谈，客户端就可以使用 `MetadataResolver` 动态找到应用程序终结点的绑定和地址。本示例客户端对此进行了演示，显示如何通过创建和配置 `MetadataExchangeClient` 来配置 `MetadataResolver` 使用的绑定和凭据。  
  
 可以在 `MetadataExchangeClient` 上强制指定 Svcutil.exe.config 中出现的相同绑定和证书信息：  
  
```  
// Specify the Metadata Exchange binding and its security mode  
WSHttpBinding mexBinding = new WSHttpBinding(SecurityMode.Message);  
mexBinding.Security.Message.ClientCredentialType = MessageCredentialType.Certificate;  
  
// Create a MetadataExchangeClient for retrieving metadata, and set the // certificate details  
MetadataExchangeClient mexClient = new MetadataExchangeClient(mexBinding);  
mexClient.SoapCredentials.ClientCertificate.SetCertificate(    StoreLocation.CurrentUser, StoreName.My,  
    X509FindType.FindBySubjectName, "client.com");  
mexClient.SoapCredentials.ServiceCertificate.Authentication.    CertificateValidationMode =    X509CertificateValidationMode.PeerOrChainTrust;  
mexClient.SoapCredentials.ServiceCertificate.SetDefaultCertificate(    StoreLocation.CurrentUser, StoreName.TrustedPeople,  
    X509FindType.FindBySubjectName, "localhost");  
```  
  
 配置完 `mexClient`，我们可以枚举感兴趣的协定并使用 `MetadataResolver` 获取使用这些协定的终结点的列表：  
  
```  
// The contract we want to fetch metadata for  
Collection<ContractDescription> contracts =    new Collection<ContractDescription>();  
ContractDescription contract =    ContractDescription.GetContract(typeof(ICalculator));  
contracts.Add(contract);  
// Find endpoints for that contract  
EndpointAddress mexAddress = new    EndpointAddress(ConfigurationManager.AppSettings["mexAddress"]);  
ServiceEndpointCollection endpoints =    MetadataResolver.Resolve(contracts, mexAddress, mexClient);  
```  
  
 最后，我们可以使用这些终结点中的信息初始化 `ChannelFactory`（用于创建与应用程序终结点通信的通道）的绑定和地址。  
  
```  
ChannelFactory<ICalculator> cf = new    ChannelFactory<ICalculator>(endpoint.Binding, endpoint.Address);  
```  
  
 本示例的关键之处在于演示：如果您要使用 `MetadataResolver`，则必须指定用于元数据交换通信的自定义绑定或行为，您可以使用 `MetadataExchangeClient` 指定这些自定义设置。  
  
#### 设置和生成示例  
  
1.  请确保已经执行了 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  若要生成解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
#### 在同一计算机上运行示例  
  
1.  运行示例安装文件夹中的 Setup.bat。这将安装运行示例所需的所有证书。请注意，Setup.bat 使用 FindPrivateKey.exe 工具，通过运行 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)中的 setupCertTool.bat 可安装此工具。  
  
2.  运行 \\MetadataResolverClient\\bin 或 \\SvcutilClient\\bin 中的客户端应用程序。客户端活动将显示在客户端控制台应用程序上。  
  
3.  如果客户端与服务无法进行通信，请参见[Troubleshooting Tips](http://msdn.microsoft.com/zh-cn/8787c877-5e96-42da-8214-fa737a38f10b)。  
  
4.  在运行完该示例后运行 Cleanup.bat 移除证书。其他安全示例使用相同的证书。  
  
#### 跨计算机运行示例  
  
1.  在服务器上运行 `setup.bat service`。如果采用 `service` 参数运行 `setup.bat` ，则使用计算机的完全限定域名创建一个服务证书，并将此服务证书导出到名为 Service.cer 的文件中。  
  
2.  在服务器上，编辑 Web.config 以反映新证书名称。也就是说，将 [\<serviceCertificate\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-clientcredentials-element.md) 元素中的 `findValue` 属性更改为计算机的完全限定域名。  
  
3.  将服务目录中的 Service.cer 文件复制到客户端计算机上的客户端目录中。  
  
4.  在客户端上，运行 `setup.bat client`。如果使用 `client` 参数运行 `setup.bat` ，则会创建一个名为 Client.com 的客户端证书，并将此客户端证书导出到名为 Client.cer 的文件中。  
  
5.  在客户端计算机上的 `MetadataResolverClient` 的 App.config 文件中，更改 Mex 终结点的地址值以与服务的新地址相匹配。通过使用服务器的完全限定域名替换 localhost 来执行此操作。还要将 metadataResolverClient.cs 文件中出现的“localhost”更改为新的服务证书名称（服务器的完全限定域名）。对 SvcutilClient 项目的 App.config 执行相同的操作。  
  
6.  将客户端目录中的 Client.cer 文件复制到服务器上的服务目录中。  
  
7.  在客户端上，运行 `ImportServiceCert.bat`。这会将 Service.cer 文件中的服务证书导入 CurrentUser – TrustedPeople 存储区。  
  
8.  在服务器上，运行 `ImportClientCert.bat`，这会将 Client.cer 文件中的客户端证书导入 LocalMachine \- TrustedPeople 存储区。  
  
9. 在服务计算机上，在 Visual Studio 中生成服务项目，在 Web 浏览器中选择帮助页可验证该项目是否在运行。  
  
10. 在客户端计算机上，运行 VS 中的 MetadataResolverClient 或 SvcutilClient。  
  
    1.  如果客户端与服务无法进行通信，请参见[Troubleshooting Tips](http://msdn.microsoft.com/zh-cn/8787c877-5e96-42da-8214-fa737a38f10b)。  
  
#### 运行示例后进行清理  
  
-   运行完示例后运行示例文件夹中的 Cleanup.bat。  
  
    > [!NOTE]
    >  此脚本不会在跨计算机运行此示例时移除客户端上的服务证书。如果已运行跨计算机使用证书的 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 示例，请确保清除已安装在 CurrentUser \- TrustedPeople 存储中的服务证书。为此，请使用以下命令：`certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>`。例如：`certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Extensibility\Metadata\CustomMexEndpoint`  
  
## 请参阅