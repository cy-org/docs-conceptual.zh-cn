---
title: "授权策略 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1db325ec-85be-47d0-8b6e-3ba2fdf3dda0
caps.latest.revision: 38
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 38
---
# 授权策略
此示例演示如何实现一个自定义声明授权策略和一个关联的自定义服务授权管理器。这在服务对服务操作进行基于声明的访问检查，并在进行访问检查之前授予调用方某些权限时很有用。此示例演示添加声明的过程，以及对最终的声明集进行访问检查的过程。客户端与服务器之间的所有应用程序消息均已进行签名和加密。默认情况下，对于 `wsHttpBinding` 绑定，使用客户端提供的用户名和密码登录有效的 Windows NT 帐户。此示例演示如何利用自定义 <xref:System.IdentityModel.Selectors.UsernamePasswordValidator> 对客户端进行身份验证。此外，此示例还演示使用 X.509 证书对服务进行客户端身份验证。此示例演示了 <xref:System.IdentityModel.Policy.IAuthorizationPolicy> 和 <xref:System.ServiceModel.ServiceAuthorizationManager> 的实现，该实现在它们之间为特定用户授予对服务的特定方法的访问权限。此示例基于[用户名消息安全](../../../../docs/framework/wcf/samples/message-security-user-name.md)，但演示了如何在调用 <xref:System.ServiceModel.ServiceAuthorizationManager> 之前执行声明转换。  
  
> [!NOTE]
>  本主题的末尾介绍了此示例的设置过程和生成说明。  
  
 概括而言，此示例演示：  
  
-   如何使用用户名和密码对客户端进行身份验证。  
  
-   如何使用 X.509 证书对客户端进行身份验证。  
  
-   服务器如何根据自定义 `UsernamePassword` 验证程序验证客户端凭据。  
  
-   如何使用服务器的 X.509 证书对服务器进行身份验证。  
  
-   服务器可以使用 <xref:System.ServiceModel.ServiceAuthorizationManager> 控制对服务中的某些方法的访问。  
  
-   如何实现 <xref:System.IdentityModel.Policy.IAuthorizationPolicy>。  
  
 服务公开两个终结点，以便与使用配置文件 App.config 定义的服务进行通信。每个终结点由地址、绑定和协定组成。其中一个绑定是使用标准 `wsHttpBinding` 绑定配置的，该标准绑定使用 WS\-Security 和客户端用户名身份验证。另一个绑定是使用标准 `wsHttpBinding` 绑定配置的，该标准绑定使用 WS\-Security 和客户端证书身份验证。[\<行为\>](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)指定使用用户凭据对服务进行身份验证。服务器证书中包含的 `SubjectName` 属性 \(Property\) 值必须与 [\<serviceCertificate\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)中的 `findValue` 属性 \(Attribute\) 值相同。  
  
```  
<system.serviceModel>  
  <services>  
    <service name="Microsoft.ServiceModel.Samples.CalculatorService"  
             behaviorConfiguration="CalculatorServiceBehavior">  
      <host>  
        <baseAddresses>  
          <!-- configure base address provided by host -->  
          <add baseAddress ="http://localhost:8001/servicemodelsamples/service"/>  
        </baseAddresses>  
      </host>  
      <!-- use base address provided by host, provide two endpoints -->  
      <endpoint address="username"  
                binding="wsHttpBinding"  
                bindingConfiguration="Binding1"   
                contract="Microsoft.ServiceModel.Samples.ICalculator" />  
      <endpoint address="certificate"  
                binding="wsHttpBinding"  
                bindingConfiguration="Binding2"   
                contract="Microsoft.ServiceModel.Samples.ICalculator" />  
    </service>  
  </services>  
  
  <bindings>  
    <wsHttpBinding>  
      <!-- Username binding -->  
      <binding name="Binding1">  
        <security mode="Message">  
    <message clientCredentialType="UserName" />  
        </security>  
      </binding>  
      <!-- X509 certificate binding -->  
      <binding name="Binding2">  
        <security mode="Message">  
          <message clientCredentialType="Certificate" />  
        </security>  
      </binding>  
    </wsHttpBinding>  
  </bindings>  
  
  <behaviors>  
    <serviceBehaviors>  
      <behavior name="CalculatorServiceBehavior" >  
        <serviceDebug includeExceptionDetailInFaults ="true" />  
        <serviceCredentials>  
          <!--   
          The serviceCredentials behavior allows one to specify a custom validator for username/password combinations.    
          -->  
          <userNameAuthentication userNamePasswordValidationMode="Custom" customUserNamePasswordValidatorType="Microsoft.ServiceModel.Samples.MyCustomUserNameValidator, service" />  
          <!--   
          The serviceCredentials behavior allows one to specify authentication constraints on client certificates.  
          -->  
          <clientCertificate>  
            <!--   
            Setting the certificateValidationMode to PeerOrChainTrust means that if the certificate   
            is in the user's Trusted People store, then it will be trusted without performing a  
            validation of the certificate's issuer chain. This setting is used here for convenience so that the   
            sample can be run without having to have certificates issued by a certification authority (CA).  
            This setting is less secure than the default, ChainTrust. The security implications of this   
            setting should be carefully considered before using PeerOrChainTrust in production code.   
            -->  
            <authentication certificateValidationMode="PeerOrChainTrust" />  
          </clientCertificate>  
          <!--   
          The serviceCredentials behavior allows one to define a service certificate.  
          A service certificate is used by a client to authenticate the service and provide message protection.  
          This configuration references the "localhost" certificate installed during the setup instructions.  
          -->  
          <serviceCertificate findValue="localhost" storeLocation="LocalMachine" storeName="My" x509FindType="FindBySubjectName" />  
        </serviceCredentials>  
        <serviceAuthorization serviceAuthorizationManagerType="Microsoft.ServiceModel.Samples.MyServiceAuthorizationManager, service">  
          <!--   
          The serviceAuthorization behavior allows one to specify custom authorization policies.  
          -->  
          <authorizationPolicies>  
            <add policyType="Microsoft.ServiceModel.Samples.CustomAuthorizationPolicy.MyAuthorizationPolicy, PolicyLibrary" />  
          </authorizationPolicies>  
        </serviceAuthorization>  
      </behavior>  
    </serviceBehaviors>  
  </behaviors>  
  
</system.serviceModel>  
  
```  
  
 每个客户端终结点配置由配置名称、服务终结点的绝对地址、绑定和协定组成。客户端绑定是使用本例中在 [\<安全性\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-wshttpbinding.md)中指定的相应安全模式以及在 [\<消息\>](../../../../docs/framework/configure-apps/file-schema/wcf/message-of-wshttpbinding.md)中指定的 `clientCredentialType` 配置的。  
  
```  
<system.serviceModel>  
  
    <client>  
      <!-- Username based endpoint -->  
      <endpoint name="Username"  
            address="http://localhost:8001/servicemodelsamples/service/username"   
    binding="wsHttpBinding"   
    bindingConfiguration="Binding1"   
                behaviorConfiguration="ClientCertificateBehavior"  
                contract="Microsoft.ServiceModel.Samples.ICalculator" >  
      </endpoint>  
      <!-- X509 certificate based endpoint -->  
      <endpoint name="Certificate"  
                        address="http://localhost:8001/servicemodelsamples/service/certificate"   
                binding="wsHttpBinding"   
            bindingConfiguration="Binding2"   
                behaviorConfiguration="ClientCertificateBehavior"  
                contract="Microsoft.ServiceModel.Samples.ICalculator">  
      </endpoint>  
    </client>  
  
    <bindings>  
      <wsHttpBinding>  
        <!-- Username binding -->  
      <binding name="Binding1">  
        <security mode="Message">  
          <message clientCredentialType="UserName" />  
        </security>  
      </binding>  
        <!-- X509 certificate binding -->  
        <binding name="Binding2">  
          <security mode="Message">  
            <message clientCredentialType="Certificate" />  
          </security>  
        </binding>  
    </wsHttpBinding>  
    </bindings>  
  
    <behaviors>  
      <behavior name="ClientCertificateBehavior">  
        <clientCredentials>  
          <serviceCertificate>  
            <!--   
            Setting the certificateValidationMode to PeerOrChainTrust  
            means that if the certificate   
            is in the user's Trusted People store, then it will be   
            trusted without performing a  
            validation of the certificate's issuer chain. This setting   
            is used here for convenience so that the   
            sample can be run without having to have certificates   
            issued by a certification authority (CA).  
            This setting is less secure than the default, ChainTrust.   
            The security implications of this   
            setting should be carefully considered before using   
            PeerOrChainTrust in production code.   
            -->  
            <authentication certificateValidationMode = "PeerOrChainTrust" />  
          </serviceCertificate>  
        </clientCredentials>  
      </behavior>  
    </behaviors>  
  
  </system.serviceModel>  
  
```  
  
 对于基于用户名的终结点，客户端实现设置要使用的用户名和密码。  
  
```  
// Create a client with Username endpoint configuration  
CalculatorClient client1 = new CalculatorClient("Username");  
  
client1.ClientCredentials.UserName.UserName = "test1";  
client1.ClientCredentials.UserName.Password = "1tset";  
  
try  
{  
    // Call the Add service operation.  
    double value1 = 100.00D;  
    double value2 = 15.99D;  
    double result = client1.Add(value1, value2);  
    Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
    ...  
}  
catch (Exception e)  
{  
    Console.WriteLine("Call failed : {0}", e.Message);  
}  
  
client1.Close();  
  
```  
  
 对于基于证书的终结点，客户端实现设置要使用的客户端证书。  
  
```  
// Create a client with Certificate endpoint configuration  
CalculatorClient client2 = new CalculatorClient("Certificate");  
  
client2.ClientCredentials.ClientCertificate.SetCertificate(StoreLocation.CurrentUser, StoreName.My, X509FindType.FindBySubjectName, "test1");  
  
try  
{  
    // Call the Add service operation.  
    double value1 = 100.00D;  
    double value2 = 15.99D;  
    double result = client2.Add(value1, value2);  
    Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
    ...  
}  
catch (Exception e)  
{  
    Console.WriteLine("Call failed : {0}", e.Message);  
}  
  
client2.Close();  
  
```  
  
 此示例使用自定义 <xref:System.IdentityModel.Selectors.UsernamePasswordValidator> 验证用户名和密码。此示例实现从 <xref:System.IdentityModel.Selectors.UserNamePasswordValidator> 派生的 `MyCustomUserNamePasswordValidator`。有关更多信息，请参见有关 <xref:System.IdentityModel.Selectors.UsernamePasswordValidator> 的文档。为了演示与 <xref:System.IdentityModel.Selectors.UsernamePasswordValidator> 的集成，此自定义验证程序示例实现了 <xref:System.IdentityModel.Selectors.UsernamePasswordValidator.Validate%2A> 方法，以在用户名与密码匹配时接受用户名\/密码对，如下面的代码所示。  
  
```  
public class MyCustomUserNamePasswordValidator : UserNamePasswordValidator  
{  
  // This method validates users. It allows in two users,   
  // test1 and test2 with passwords 1tset and 2tset respectively.  
  // This code is for illustration purposes only and   
  // MUST NOT be used in a production environment because it   
  // is NOT secure.      
  public override void Validate(string userName, string password)  
  {  
    if (null == userName || null == password)  
    {  
      throw new ArgumentNullException();  
    }  
  
    if (!(userName == "test1" && password == "1tset") && !(userName == "test2" && password == "2tset"))  
    {  
      throw new SecurityTokenException("Unknown Username or Password");  
    }  
  }  
}  
  
```  
  
 在服务代码中实现验证程序后，必须通知服务主机关于要使用的验证程序实例的信息。这是使用以下代码完成的。  
  
```  
Servicehost.Credentials.UserNameAuthentication.UserNamePasswordValidationMode = UserNamePasswordValidationMode.Custom;  
serviceHost.Credentials.UserNameAuthentication.CustomUserNamePasswordValidator = new MyCustomUserNamePasswordValidatorProvider();  
```  
  
 或者，您可以在配置中执行相同的操作。  
  
```  
<behavior ...>  
    <serviceCredentials>  
      <!--   
      The serviceCredentials behavior allows one to specify a custom validator for username/password combinations.    
      -->  
      <userNameAuthentication userNamePasswordValidationMode="Custom" customUserNamePasswordValidatorType="Microsoft.ServiceModel.Samples.MyCustomUserNameValidator, service" />  
    ...  
    </serviceCredentials>  
</behavior>  
```  
  
 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 为执行访问检查提供了一个丰富的、基于声明的模型。<xref:System.ServiceModel.ServiceAuthorizationManager> 对象用于执行访问检查，并确定与客户端关联的声明是否满足访问服务方法的必需要求。  
  
 出于演示目的，此示例演示了 <xref:System.ServiceModel.ServiceAuthorizationManager> 的实现，它实现了 <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%2A> 方法，以允许用户基于声明类型 http:\/\/example.com\/claims\/allowedoperation（其值为允许调用的操作的操作 URI）来访问方法。  
  
```  
public class MyServiceAuthorizationManager : ServiceAuthorizationManager  
{  
  protected override bool CheckAccessCore(OperationContext operationContext)  
  {                  
    string action = operationContext.RequestContext.RequestMessage.Headers.Action;  
    Console.WriteLine("action: {0}", action);  
    foreach(ClaimSet cs in operationContext.ServiceSecurityContext.AuthorizationContext.ClaimSets)  
    {  
      if ( cs.Issuer == ClaimSet.System )  
      {  
        foreach (Claim c in cs.FindClaims("http://example.com/claims/allowedoperation", Rights.PossessProperty))  
        {  
          Console.WriteLine("resource: {0}", c.Resource.ToString());  
          if (action == c.Resource.ToString())  
            return true;  
        }  
      }  
    }  
    return false;                   
  }  
}  
  
```  
  
 实现自定义 <xref:System.ServiceModel.ServiceAuthorizationManager> 后，必须通知服务主机关于要使用的 <xref:System.ServiceModel.ServiceAuthorizationManager> 的信息。这是通过如下所示的代码完成的。  
  
```  
<behavior ...>  
    ...  
    <serviceAuthorization serviceAuthorizationManagerType="Microsoft.ServiceModel.Samples.MyServiceAuthorizationManager, service">  
        ...  
    </serviceAuthorization>  
</behavior>  
  
```  
  
 要实现的主要 <xref:System.IdentityModel.Policy.IAuthorizationPolicy> 方法是 <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%28System.IdentityModel.Policy.EvaluationContext%2CSystem.Object%40%29> 方法。  
  
```  
public class MyAuthorizationPolicy : IAuthorizationPolicy  
{  
    string id;  
  
    public MyAuthorizationPolicy()  
    {  
    id =  Guid.NewGuid().ToString();  
    }  
  
    public bool Evaluate(EvaluationContext evaluationContext,   
                                            ref object state)  
    {  
        bool bRet = false;  
        CustomAuthState customstate = null;  
  
        if (state == null)  
        {  
            customstate = new CustomAuthState();  
            state = customstate;  
        }  
        else  
            customstate = (CustomAuthState)state;  
        Console.WriteLine("In Evaluate");  
        if (!customstate.ClaimsAdded)  
        {  
           IList<Claim> claims = new List<Claim>();  
  
           foreach (ClaimSet cs in evaluationContext.ClaimSets)  
              foreach (Claim c in cs.FindClaims(ClaimTypes.Name,   
                                         Rights.PossessProperty))  
                  foreach (string s in   
                        GetAllowedOpList(c.Resource.ToString()))  
                  {  
                       claims.Add(new  
               Claim("http://example.com/claims/allowedoperation",   
                                    s, Rights.PossessProperty));  
                            Console.WriteLine("Claim added {0}", s);  
                      }  
                   evaluationContext.AddClaimSet(this,   
                           new DefaultClaimSet(this.Issuer,claims));  
                   customstate.ClaimsAdded = true;  
                   bRet = true;  
                }  
         else  
         {  
              bRet = true;  
         }  
         return bRet;  
     }  
...  
}  
```  
  
 上面的代码演示了 <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%28System.IdentityModel.Policy.EvaluationContext%2CSystem.Object%40%29> 方法如何检查尚未添加影响处理的新声明，并添加特定的声明。允许的声明是从 `GetAllowedOpList` 方法中获得的，实现该方法是为了返回允许用户执行的特定操作的列表。授权策略添加了访问特定操作的声明。<xref:System.ServiceModel.ServiceAuthorizationManager> 然后使用此授权策略执行访问检查决策。  
  
 实现自定义 <xref:System.IdentityModel.Policy.IAuthorizationPolicy> 后，必须通知服务主机关于要使用的授权策略的信息。  
  
```  
<serviceAuthorization ...>  
       <authorizationPolicies>   
            <add policyType='Microsoft.ServiceModel.Samples.CustomAuthorizationPolicy.MyAuthorizationPolicy, PolicyLibrary' />  
       </authorizationPolicies>   
</serviceAuthorization>  
  
```  
  
 运行示例时，操作请求和响应将显示在客户端控制台窗口中。客户端成功调用 Add、Subtract 和 Multiple 方法，在尝试调用 Divide 方法时获得“访问被拒绝”消息。在客户端窗口中按 Enter 可以关闭客户端。  
  
## 设置批处理文件  
 通过运行此示例随附的 Setup.bat 批处理文件，可以用相关的证书将服务器配置为运行需要基于服务器证书的安全性的自承载应用程序。  
  
 下面提供了批处理文件不同节的简要概述，以便可以修改批处理文件从而在相应的配置中运行：  
  
-   创建服务器证书。  
  
     Setup.bat 批处理文件中的以下行创建将要使用的服务器证书。%SERVER\_NAME% 变量指定服务器名称。更改此变量可以指定您自己的服务器名称。默认值为 localhost。  
  
    ```  
    echo ************  
    echo Server cert setup starting  
    echo %SERVER_NAME%  
    echo ************  
    echo making server cert  
    echo ************  
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe  
  
    ```  
  
-   将服务器证书安装到客户端的受信任证书存储区中。  
  
     Setup.bat 批处理文件中的以下行将服务器证书复制到客户端的受信任的人的存储区中。因为客户端系统不是隐式信任 Makecert.exe 生成的证书，所以需要执行此步骤。如果您已经拥有一个证书，该证书来源于客户端的受信任根证书（例如由 Microsoft 颁发的证书），则不需要执行使用服务器证书填充客户端证书存储区这一步骤。  
  
    ```  
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople  
    ```  
  
-   创建客户端证书。  
  
     Setup.bat 批处理文件中的以下行创建将要使用的客户端证书。%USER\_NAME% 变量指定服务器名称。此值设置为“test1”，因为这是 `IAuthorizationPolicy` 查找的名称。如果更改 %USER\_NAME% 的值，必须更改 `IAuthorizationPolicy.Evaluate` 方法中的对应值。  
  
     证书存储在 CurrentUser 存储位置下的 My（个人）存储区中。  
  
    ```  
    echo ************  
    echo making client cert  
    echo ************  
    makecert.exe -sr CurrentUser -ss MY -a sha1 -n CN=%CLIENT_NAME% -sky exchange -pe  
  
    ```  
  
-   将客户端证书安装到服务器的受信任证书存储区中。  
  
     Setup.bat 批处理文件中的以下行将客户端证书复制到受信任的人的存储区中。因为服务器系统不是隐式信任 Makecert.exe 生成的证书，所以需要执行此步骤。如果您已经拥有一个证书，该证书来源于受信任的根证书（例如由 Microsoft 颁发的证书），则不需要执行使用客户端证书填充服务器证书存储区这一步骤。  
  
    ```  
    certmgr.exe -add -r CurrentUser -s My -c -n %CLIENT_NAME% -r LocalMachine -s TrustedPeople  
    ```  
  
#### 设置和生成示例  
  
1.  若要生成解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
2.  若要用单一计算机配置或跨计算机配置来运行示例，请按照下列说明进行操作。  
  
> [!NOTE]
>  如果使用 Svcutil.exe 为此示例重新生成配置，请确保在客户端配置中修改终结点名称以与客户端代码匹配。  
  
#### 在同一计算机上运行示例  
  
1.  使用管理员特权打开 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 命令提示窗口并运行示例安装文件夹中的 Setup.bat。这将安装运行示例所需的所有证书。  
  
    > [!NOTE]
    >  Setup.bat 批处理文件设计为通过 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 命令提示运行。[!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 命令提示中设置的 PATH 环境变量指向包含 Setup.bat 脚本所需的可执行文件的目录。  
  
2.  在使用管理员特权打开的 Visual Studio 命令提示中运行示例安装文件夹中的 Setup.bat。这将安装运行示例所需的所有证书。  
  
3.  启动 service\\bin 中的 Service.exe。  
  
4.  启动 \\client\\bin 中的 Client.exe。客户端活动将显示在客户端控制台应用程序上。  
  
5.  如果客户端与服务无法进行通信，请参见[Troubleshooting Tips](http://msdn.microsoft.com/zh-cn/8787c877-5e96-42da-8214-fa737a38f10b)。  
  
#### 跨计算机运行示例  
  
1.  在服务计算机上创建目录。  
  
2.  将 \\service\\bin 中的服务程序文件复制到服务计算机上的目录中。另外，将 Setup.bat、Cleanup.bat、GetComputerName.vbs 和 ImportClientCert.bat 文件复制到服务计算机上。  
  
3.  在客户端计算机上为这些客户端二进制文件创建一个目录。  
  
4.  将客户端程序文件复制到客户端计算机上的客户端目录中。另外，将 Setup.bat、Cleanup.bat 和 ImportServiceCert.bat 文件复制到客户端上。  
  
5.  在服务器上，在使用管理员特权打开的 Visual Studio 命令提示中运行 `setup.bat service`。如果采用 `service` 参数运行 `setup.bat` ，则使用计算机的完全限定域名创建一个服务证书，并将此服务证书导出到名为 Service.cer 的文件中。  
  
6.  编辑 Service.exe.config 以反映新证书的名称（在 [\<serviceCertificate\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)的 `findValue` 属性中），该名称与计算机的完全限定域名相同。另外，将 \<service\>\/\<baseAddresses\> 元素中的计算机名称从 localhost 更改为服务计算机的完全限定名称。  
  
7.  将服务目录中的 Service.cer 文件复制到客户端计算机上的客户端目录中。  
  
8.  在客户端上，在使用管理员特权打开的 Visual Studio 命令提示中运行 `setup.bat client`。如果使用 `client` 参数运行 `setup.bat` ，将创建一个名为 test1 的客户端证书，并将该客户端证书导出到名为 Client.cer 的文件中。  
  
9. 在客户端计算机上的 Client.exe.config 文件中，更改终结点的地址值，使其与服务的新地址相匹配。通过用服务器的完全限定域名替换 localhost 来执行此操作。  
  
10. 将客户端目录中的 Client.cer 文件复制到服务器上的服务目录中。  
  
11. 在客户端上，在使用管理员特权打开的 Visual Studio 命令提示中运行 ImportServiceCert.bat。这会将 Service.cer 文件中的服务证书导入 CurrentUser – TrustedPeople 存储区。  
  
12. 在服务器上，在使用管理员特权打开的 Visual Studio 命令提示中运行 ImportClientCert。这会将 Client.cer 文件中的客户端证书导入 LocalMachine \- TrustedPeople 存储区。  
  
13. 在服务器计算机上，从命令提示窗口中启动 Service.exe。  
  
14. 在客户端计算机上，从命令提示窗口中启动 Client.exe。如果客户端与服务无法进行通信，请参见[Troubleshooting Tips](http://msdn.microsoft.com/zh-cn/8787c877-5e96-42da-8214-fa737a38f10b)。  
  
#### 运行示例后进行清理  
  
1.  运行完示例后运行示例文件夹中的 Cleanup.bat。这将从证书存储区中移除服务器和客户端证书。  
  
> [!NOTE]
>  此脚本不会在跨计算机运行此示例时移除客户端上的服务证书。如果已运行跨计算机使用证书的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 示例，请确保清除已安装在 CurrentUser \- TrustedPeople 存储中的服务证书。为此，请使用以下命令：`certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>`，例如：`certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`。  
  
## 请参阅