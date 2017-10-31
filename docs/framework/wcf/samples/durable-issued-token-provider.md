---
title: "持久性已颁发令牌提供程序 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 76fb27f5-8787-4b6a-bf4c-99b4be1d2e8b
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# 持久性已颁发令牌提供程序
此示例演示如何实现一个自定义客户端颁发的令牌提供程序。  
  
## 讨论  
 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 中的令牌提供程序用于为安全基础结构提供凭据。令牌提供程序一般检查目标并颁发相应的凭据，以使安全基础结构能够确保消息的安全。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 附带了一个 [!INCLUDE[infocard](../../../../includes/infocard-md.md)] 令牌提供程序。自定义令牌提供程序在下列情况下有用：  
  
-   存在不能由内置令牌提供程序操作的凭据存储区。  
  
-   如果要提供自己的自定义机制，以便从用户提供详细信息这一刻起到 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端使用凭据时转换凭据。  
  
-   如果生成自定义令牌。  
  
 此示例演示如何生成一个自定义令牌提供程序，该提供程序可以缓存由安全令牌服务 \(STS\) 颁发的令牌。  
  
 总之，此示例将演示如下内容：  
  
-   如何使用自定义令牌提供程序对客户端进行配置。  
  
-   如何缓存已颁发的令牌并将它们提供给 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端。  
  
-   客户端如何使用服务器的 X.509 证书对服务器进行身份验证。  
  
 此示例由客户端控制台程序 \(Client.exe\)、安全令牌服务控制台程序 \(Securitytokenservice.exe\) 和服务控制台程序 \(Service.exe\) 组成。该服务实现定义“请求\-答复”通信模式的协定。该协定由 `ICalculator` 接口定义，此接口公开数学运算（加、减、乘和除）。客户端从安全令牌服务 \(STS\) 获取安全令牌，向给定数学运算的服务发出同步请求，服务使用结果进行答复。客户端活动显示在控制台窗口中。  
  
> [!NOTE]
>  本主题的最后提供了此示例的设置过程和生成说明。  
  
 此示例使用 [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)公开 ICalculator 协定。下面的代码演示此绑定在客户端上的配置。  
  
```  
<bindings>  <wsFederationHttpBinding>    <binding name="ServiceFed" >      <security mode ="Message">        <message issuedKeyType ="SymmetricKey" issuedTokenType ="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1" >          <issuer address ="http://localhost:8000/sts/windows" binding ="wsHttpBinding" />        </message>      </security>    </binding>  </wsFederationHttpBinding></bindings>  
```  
  
 在 `wsFederationHttpBinding` 的 `security` 上，`mode` 值配置应该使用的安全模式。在此示例中使用了消息安全性，这就是在 `wsFederationHttpBinding` 的 `security` 元素内指定 `wsFederationHttpBinding` 的 `message` 元素的原因。`wsFederationHttpBinding` 的 `issuer` 元素（位于 `wsFederationHttpBinding` 的 `message` 元素内）为向客户端颁发安全令牌的安全令牌服务指定地址和绑定，以便客户端能够向计算器服务进行身份验证。  
  
 下面的代码演示了此绑定在服务上的配置。  
  
```  
<bindings>  <wsFederationHttpBinding>    <binding name="ServiceFed" >      <security mode ="Message">        <message issuedKeyType ="SymmetricKey" issuedTokenType ="http://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1" >          <issuerMetadata address ="http://localhost:8000/sts/mex" >            <identity>              <certificateReference storeLocation ="CurrentUser"                                     storeName="TrustedPeople"                                     x509FindType ="FindBySubjectDistinguishedName"                                     findValue ="CN=STS" />            </identity>          </issuerMetadata>        </message>      </security>    </binding>  </wsFederationHttpBinding></bindings>  
```  
  
 在 `wsFederationHttpBinding` 的 `security` 上，`mode` 值配置应该使用的安全模式。在此示例中使用了消息安全性，这就是在 `wsFederationHttpBinding` 的 `security` 元素内指定 `wsFederationHttpBinding` 的 `message` 元素的原因。`wsFederationHttpBinding` 的 `issuerMetadata` 元素（位于 `wsFederationHttpBinding` 的 `message` 元素内）为终结点指定地址和标识，该终结点可用于检索安全令牌服务的元数据。  
  
 下面的代码演示了该服务的行为。  
  
```  
<behavior name ="ServiceBehavior" >  <serviceDebug includeExceptionDetailInFaults ="true"/>  <serviceMetadata httpGetEnabled ="true"/>  <serviceCredentials>    <issuedTokenAuthentication>      <knownCertificates>        <add storeLocation ="LocalMachine"             storeName="TrustedPeople"             x509FindType="FindBySubjectDistinguishedName"             findValue="CN=STS" />      </knownCertificates>    </issuedTokenAuthentication>    <serviceCertificate storeLocation ="LocalMachine"                        storeName ="My"                        x509FindType ="FindBySubjectDistinguishedName"                        findValue ="CN=localhost"/>  </serviceCredentials></behavior>  
```  
  
 `serviceCredentials` 元素内的 `issuedTokenAuthentication` 元素允许服务对它在身份验证过程中允许客户端提供的令牌指定约束。此配置指定该服务接受由主题名称为 CN\=STS 的证书签名的令牌。  
  
 安全令牌服务使用标准 wsHttpBinding 来公开一个终结点。安全令牌服务响应客户端对令牌的请求，使用 Windows 帐户提供客户端身份验证，并颁发包含客户端用户名（作为已颁发令牌中的声明）的令牌。作为创建令牌的一部分，安全令牌服务使用与 CN\=STS 证书关联的私钥对令牌进行签名。另外，它还创建对称密钥并使用与 CN\=localhost 证书关联的公钥对该密钥进行加密。在向客户端返回令牌的过程中，安全令牌服务还返回对称密钥。客户端向计算器服务出示颁发的令牌，并通过使用该对称密钥对消息进行签名来证明客户端知道该密钥。  
  
## 自定义客户端凭据和令牌提供程序  
 下列步骤演示如何开发自定义令牌提供程序（用于缓存已颁发的令牌）并将其与 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 安全集成在一起。  
  
#### 开发自定义安全令牌提供程序  
  
1.  编写自定义令牌提供程序。  
  
     此示例实现一个自定义令牌提供程序，该提供程序返回从缓存中检索的安全令牌。  
  
     为了执行此任务，自定义令牌提供程序派生了 <xref:System.IdentityModel.Selectors.SecurityTokenProvider> 类，并重写了 <xref:System.IdentityModel.Selectors.SecurityTokenProvider.GetTokenCore%2A> 方法。此方法尝试从缓存中获取令牌，如果在缓存中找不到令牌，则从基础提供程序中检索令牌并缓存该令牌。在这两种情况下，该方法都返回 `SecurityToken`。  
  
    ```  
    protected override SecurityToken GetTokenCore(TimeSpan timeout)  
    {  
      GenericXmlSecurityToken token;  
      if (!this.cache.TryGetToken(target, issuer, out token))  
      {  
        token = (GenericXmlSecurityToken) this.innerTokenProvider.GetToken(timeout);  
        this.cache.AddToken(token, target, issuer);  
      }  
      return token;  
    }  
    ```  
  
2.  编写自定义安全令牌管理器。  
  
     <xref:System.IdentityModel.Selectors.SecurityTokenManager> 用于为在 `CreateSecurityTokenProvider` 方法中传递给它的特定 <xref:System.IdentityModel.Selectors.SecurityTokenRequirement> 创建 <xref:System.IdentityModel.Selectors.SecurityTokenProvider>。安全令牌管理器还用于创建令牌身份验证器和令牌序列化程序，但本示例不涉及这些内容。在此示例中，自定义安全令牌管理器从 <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager> 类集成，并重写 `CreateSecurityTokenProvider` 方法，以便在所传递的令牌要求指示需要一个已颁发的令牌时返回自定义令牌提供程序。  
  
    ```  
    class DurableIssuedTokenClientCredentialsTokenManager :  
     ClientCredentialsSecurityTokenManager  
    {  
      IssuedTokenCache cache;  
  
      public DurableIssuedTokenClientCredentialsTokenManager ( DurableIssuedTokenClientCredentials creds ): base(creds)  
      {  
        this.cache = creds.IssuedTokenCache;  
      }  
  
      public override SecurityTokenProvider CreateSecurityTokenProvider ( SecurityTokenRequirement tokenRequirement )  
      {  
        if (IsIssuedSecurityTokenRequirement(tokenRequirement))  
        {  
          return new DurableIssuedSecurityTokenProvider ((IssuedSecurityTokenProvider)base.CreateSecurityTokenProvider( tokenRequirement), this.cache);  
        }  
        Else  
        {  
          return base.CreateSecurityTokenProvider(tokenRequirement);  
        }  
      }  
    }  
    ```  
  
3.  编写自定义客户端凭据。  
  
     客户端凭据类用于表示为客户端代理配置的凭据并创建一个安全令牌管理器，该管理器用于获取令牌身份验证器、令牌提供程序和令牌序列化程序。  
  
    ```  
    public class DurableIssuedTokenClientCredentials : ClientCredentials  
    {  
      IssuedTokenCache cache;  
  
      public DurableIssuedTokenClientCredentials() : base()  
      {  
      }  
  
      DurableIssuedTokenClientCredentials ( DurableIssuedTokenClientCredentials other) : base(other)  
      {  
        this.cache = other.cache;  
      }  
  
      public IssuedTokenCache IssuedTokenCache  
      {  
        Get  
        {  
          return this.cache;  
        }  
        Set  
        {  
          this.cache = value;  
        }  
      }  
  
      protected override ClientCredentials CloneCore()  
      {  
        return new DurableIssuedTokenClientCredentials(this);  
      }  
  
      public override SecurityTokenManager CreateSecurityTokenManager()  
      {  
        return new DurableIssuedTokenClientCredentialsTokenManager ((DurableIssuedTokenClientCredentials)this.Clone());  
      }  
    }  
    ```  
  
4.  实现令牌缓存。该示例实现使用一个抽象基类，给定令牌缓存的使用方通过该基类与缓存进行交互。  
  
    ```  
    public abstract class IssuedTokenCache  
    {  
      public abstract void AddToken ( GenericXmlSecurityToken token, EndpointAddress target, EndpointAddress issuer);  
      public abstract bool TryGetToken(EndpointAddress target, EndpointAddress issuer, out GenericXmlSecurityToken cachedToken);  
    }  
    Configure the client to use the custom client credential.  
    ```  
  
     为了使客户端使用自定义客户端凭据，该示例删除了默认的客户端凭据类，并提供了新的客户端凭据类。  
  
    ```  
    clientFactory.Endpoint.Behaviors.Remove<ClientCredentials>();  
    DurableIssuedTokenClientCredentials durableCreds = new DurableIssuedTokenClientCredentials();  
    durableCreds.IssuedTokenCache = cache;  
    durableCreds.ServiceCertificate.Authentication.CertificateValidationMode = X509CertificateValidationMode.PeerOrChainTrust;  
    clientFactory.Endpoint.Behaviors.Add(durableCreds);  
    ```  
  
## 运行示例  
 请参见下面的说明来运行该示例。运行示例时，对安全令牌的请求显示在安全令牌服务控制台窗口中。操作请求和响应显示在客户端和服务控制台窗口中。在任何一个控制台窗口中按 Enter 可以关闭应用程序。  
  
## Setup.cmd 批处理文件  
 通过运行此示例随附的 Setup.cmd 批处理文件，可以用相关的证书来配置服务器和安全令牌服务以运行自承载的应用程序。批处理文件在 CurrentUser\/TrustedPeople 证书存储区中创建两个证书。第一个证书的主题名称为 CN\=STS，并由安全令牌服务用来对颁发给客户端的安全令牌进行签名。第二个证书的主题名称为 CN\=localhost，并由安全令牌服务使用以对机密进行加密，以便服务能够解密该机密。  
  
#### 设置、生成和运行示例  
  
1.  运行 Setup.cmd 文件以创建所需证书。  
  
2.  若要生成解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。确保生成解决方案中的所有项目（Shared、RSTRSTR、Service、SecurityTokenService 和 Client）。  
  
3.  确保 Service.exe 和 SecurityTokenService.exe 都使用管理员权限运行。  
  
4.  运行 Client.exe。  
  
#### 运行示例后进行清理  
  
1.  运行完示例后运行示例文件夹中的 Cleanup.cmd。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Extensibility\Security\DurableIssuedTokenProvider`  
  
## 请参阅