---
title: "受信任的外观服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c34d1a8f-e45e-440b-a201-d143abdbac38
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# 受信任的外观服务
本方案示例演示如何使用 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 安全基础结构使调用方标识信息从一个服务流到另一个服务。  
  
 使用外观服务向公共网络公开由服务提供的功能是一种常见设计模式。 外观服务通常驻留在周边网络（也称为 DMZ、外围安全区域和被筛选的子网）中，可与实现业务逻辑的后端服务通信和访问内部数据。 外观服务和后端服务之间的通信通道通过防火墙并通常仅限用于单一目的。  
  
 本示例包含以下组件：  
  
-   计算器客户端  
  
-   计算器外观服务  
  
-   计算器后端服务  
  
 外观服务负责验证请求和对调用方进行身份验证。 成功进行身份验证和验证后，服务将使用从周边网络到内部网络的受控通信通道将请求转发到后端服务。 作为所转发请求的一部分，外观服务包含有关调用方标识的信息，这样后端服务可以在其处理过程中使用此信息。 使用消息 `Username` 标头内部的 `Security` 安全令牌传输调用方标识。 示例使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 安全基础结构在 `Security` 标头中传输和提取此信息。  
  
> [!IMPORTANT]
>  后端服务委托外观服务对调用方进行身份验证。 因此，后端服务不再对调用方进行身份验证；它使用外观服务在转发的请求中提供的标识信息。 由于此信任关系，后端服务必须对外观服务进行身份验证，以确保转发的消息来自受信任的源（在本例中为外观服务）。  
  
## 实现  
 本示例中有两个通信路径： 第一个路径是在客户端和外观服务之间，第二个路径是在外观服务和后端服务之间。  
  
### 客户端和外观服务之间的通信路径  
 客户端到外观服务这一通信路径使用具有 `wsHttpBinding` 客户端凭据类型的 `UserName`。 这意味着客户端使用用户名和密码对外观服务进行身份验证，而外观服务使用 X.509 证书对客户端进行身份验证。 绑定配置如下例所示：  
  
```  
<bindings>  
  <wsHttpBinding>  
    <binding name="Binding1">  
      <security mode="Message">  
        <message clientCredentialType="UserName"/>  
      </security>  
    </binding>  
  </wsHttpBinding>  
</bindings>  
```  
  
 外观服务使用自定义 `UserNamePasswordValidator` 实现对调用方进行身份验证。 出于演示目的，该身份验证只确保调用方的用户名与所提供的密码相匹配。 在现实情况中，可能会使用 Active Directory 或自定义 ASP.NET 成员资格提供程序对用户进行身份验证。 验证程序实现位于 `FacadeService.cs` 文件中。  
  
```  
public class MyUserNamePasswordValidator : UserNamePasswordValidator  
{  
    public override void Validate(string userName, string password)  
    {  
        // check that username matches password  
        if (null == userName || userName != password)  
        {  
            Console.WriteLine("Invalid username or password");  
            throw new SecurityTokenValidationException(  
                       "Invalid username or password");  
        }  
    }  
}  
```  
  
 自定义验证程序配置为在外观服务配置文件的 `serviceCredentials` 行为内部使用。 此行为还可用于配置服务的 X.509 证书。  
  
```  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="FacadeServiceBehavior">  
      <!--The serviceCredentials behavior allows you to define -->  
      <!--a service certificate. -->  
      <!--A service certificate is used by the service to  -->  
      <!--authenticate itself to its clients and to provide  -->  
      <!--message protection. -->  
      <!--This configuration references the "localhost"  -->  
      <!--certificate installed during the setup instructions. -->  
      <serviceCredentials>  
        <serviceCertificate   
               findValue="localhost"   
               storeLocation="LocalMachine"   
               storeName="My"   
               x509FindType="FindBySubjectName" />  
        <userNameAuthentication userNamePasswordValidationMode="Custom"  
            customUserNamePasswordValidatorType=  
           "Microsoft.ServiceModel.Samples.MyUserNamePasswordValidator,  
            FacadeService"/>  
      </serviceCredentials>  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
### 外观服务和后端服务之间的通信路径  
 外观服务到后端服务这一通信路径使用包含多个绑定元素的 `customBinding`。 此绑定可实现两个目的。 它对外观服务和后端服务进行身份验证，以确保通信的安全并确保通信来自受信任的源。 另外，它还可在 `Username` 安全令牌中传输初始调用方的标识。 在这种情况下，只将初始调用方的用户名传输到后端服务，密码不包括在消息中。 这是因为在将请求转发给调用方之前，后端服务会委托外观服务对调用方进行身份验证。 由于外观服务会向后端服务对其自身进行身份验证，因此后端服务可以信任所转发请求中包含的信息。  
  
 下面是此通信路径的绑定配置。  
  
```  
<bindings>  
  <customBinding>  
    <binding name="ClientBinding">  
      <security authenticationMode="UserNameOverTransport"/>  
      <windowsStreamSecurity/>  
      <tcpTransport/>  
    </binding>  
  </customBinding>  
</bindings>  
```  
  
 [\<安全性\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md) 绑定元素负责传输和提取初始调用方的用户名。[\<windowsStreamSecurity\>](../../../../docs/framework/configure-apps/file-schema/wcf/windowsstreamsecurity.md) 和 [\<tcpTransport\>](../../../../docs/framework/configure-apps/file-schema/wcf/tcptransport.md) 负责对外观服务和后端服务进行身份验证并保护消息。  
  
 为了转发请求，外观服务实现必须提供初始调用方的用户名，以便 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 安全基础结构将该用户名放在转发的消息中。 初始调用方的用户名是在外观服务实现中提供的，具体方式为在外观服务用于与后端服务进行通信的客户端代理实例的 `ClientCredentials` 属性中设置该用户名。  
  
 下面的代码演示如何在外观服务上实现 `GetCallerIdentity` 方法。 其他方法使用相同的模式。  
  
```  
public string GetCallerIdentity()  
{  
    CalculatorClient client = new CalculatorClient();  
    client.ClientCredentials.UserName.UserName = ServiceSecurityContext.Current.PrimaryIdentity.Name;  
    string result = client.GetCallerIdentity();  
    client.Close();  
    return result;  
}  
```  
  
 如前面的代码中所示，未针对 `ClientCredentials` 属性设置密码，只设置用户名。 在此例子中，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 安全基础结构创建不含密码的用户名安全令牌，这正是在情况下所要求的。  
  
 在后端服务上，必须对用户名安全令牌中包含的信息进行身份验证。 默认情况下，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 安全机制会尝试使用所提供的密码将用户映射到 Windows 帐户。 在这种情况下，不提供密码且不需要后端服务对用户名进行身份验证，因为外观服务已经执行了身份验证。 为了在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中实现此功能，提供了一个自定义 `UserNamePasswordValidator`，它只强制在令牌中指定用户名，不执行任何其他身份验证。  
  
```  
public class MyUserNamePasswordValidator : UserNamePasswordValidator  
{  
    public override void Validate(string userName, string password)  
    {  
        // Ignore the password because it is empty,   
        // we trust the facade service to authenticate the client.  
        // Accept the username information here so that the   
        // application gets access to it.  
        if (null == userName)  
        {  
            Console.WriteLine("Invalid username");  
            throw new   
             SecurityTokenValidationException("Invalid username");  
        }  
    }  
}  
```  
  
 自定义验证程序配置为在外观服务配置文件的 `serviceCredentials` 行为内部使用。  
  
```  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="BackendServiceBehavior">  
      <serviceCredentials>  
        <userNameAuthentication userNamePasswordValidationMode="Custom"  
           customUserNamePasswordValidatorType=  
          "Microsoft.ServiceModel.Samples.MyUserNamePasswordValidator,   
           BackendService"/>  
      </serviceCredentials>  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
 为提取用户名信息和有关受信任外观服务帐户的信息，后端服务实现使用 `ServiceSecurityContext` 类。 下面的代码演示如何实现 `GetCallerIdentity` 方法。  
  
```  
public string GetCallerIdentity()  
{  
    // Facade service is authenticated using Windows authentication.  
    //Its identity is accessible.  
    // On ServiceSecurityContext.Current.WindowsIdentity.  
    string facadeServiceIdentityName =   
          ServiceSecurityContext.Current.WindowsIdentity.Name;  
  
    // The client name is transmitted using Username authentication on   
    //the message level without the password  
    // using a supporting encrypted UserNameToken.  
    // Claims extracted from this supporting token are available in   
    // ServiceSecurityContext.Current.AuthorizationContext.ClaimSets   
    // collection.  
    string clientName = null;  
    foreach (ClaimSet claimSet in   
        ServiceSecurityContext.Current.AuthorizationContext.ClaimSets)  
    {  
        foreach (Claim claim in claimSet)  
        {  
            if (claim.ClaimType == ClaimTypes.Name &&   
                                   claim.Right == Rights.Identity)  
            {  
                clientName = (string)claim.Resource;  
                break;  
            }  
        }  
    }  
    if (clientName == null)  
    {  
        // In case there was no UserNameToken attached to the request.  
        // In the real world implementation the service should reject   
        // this request.  
        return "Anonymous caller via " + facadeServiceIdentityName;  
    }  
  
    return clientName + " via " + facadeServiceIdentityName;  
}  
```  
  
 使用 `ServiceSecurityContext.Current.WindowsIdentity` 属性提取外观服务帐户信息。 为访问有关初始调用方的信息，后端服务使用 `ServiceSecurityContext.Current.AuthorizationContext.ClaimSets` 属性。 该属性查找类型为 `Identity` 的 `Name` 声明。 此声明是由 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 安全基础结构根据 `Username` 安全令牌中包含的信息自动生成的。  
  
## 运行示例  
 运行示例时，操作请求和响应将显示在客户端控制台窗口中。 在客户端窗口中按 Enter 可以关闭客户端。 在外观服务和后端服务控制台窗口中按 Enter 可以关闭服务。  
  
```  
Username authentication required.  
Provide a valid machine or domain ac  
   Enter username:  
user  
   Enter password:  
****  
user via MyMachine\testaccount  
Add(100,15.99) = 115.99  
Subtract(145,76.54) = 68.46  
Multiply(9,81.25) = 731.25  
Divide(22,7) = 3.14285714285714  
  
Press <ENTER> to terminate client.  
  
```  
  
 使用“受信任外观”方案示例中包括的 Setup.bat 批处理文件可以用相关证书配置服务器，以便运行需要基于证书的安全向客户端对其自身进行身份验证的外观服务。 有关详细信息，请参见本主题末尾的设置过程。  
  
 下面提供该批处理文件不同部分的简要概述。  
  
-   创建服务器证书。  
  
     Setup.bat 批处理文件中的以下行创建将要使用的服务器证书。  
  
    ```  
    echo ************  
    echo Server cert setup starting  
    echo %SERVER_NAME%  
    echo ************  
    echo making server cert  
    echo ************  
    makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe  
    ```  
  
     `%SERVER_NAME%` 变量指定服务器名，默认值为 localhost。 该证书存储在 LocalMachine 存储区中。  
  
-   将外观服务的证书安装到客户端的受信任证书存储区中。  
  
     下面的行将外观服务的证书复制到客户端的受信任人存储中。 因为客户端系统不隐式信任 Makecert.exe 生成的证书，所以需要执行此步骤。 如果已经拥有一个证书，该证书来源于客户端的受信任根证书（例如由 Microsoft 颁发的证书），则不需要执行使用服务器证书填充客户端证书存储区这一步骤。  
  
    ```  
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople  
    ```  
  
#### 设置、生成和运行示例  
  
1.  请确保已经执行了[Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  若要生成 C\# 或 Visual Basic .NET 版本的解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
#### 在同一计算机上运行示例  
  
1.  确保路径包含 Makecert.exe 所在的文件夹。  
  
2.  运行示例安装文件夹中的 Setup.bat。 这将安装运行示例所需的所有证书。  
  
3.  在单独的控制台窗口中启动 \\BackendService\\bin 目录中的 BackendService.exe  
  
4.  在单独的控制台窗口中启动 \\FacadeService\\bin 目录中的 FacadeService.exe  
  
5.  启动 \\client\\bin 中的 Client.exe。 客户端活动将显示在客户端控制台应用程序上。  
  
6.  如果客户端与服务无法进行通信，请参见[Troubleshooting Tips](http://msdn.microsoft.com/zh-cn/8787c877-5e96-42da-8214-fa737a38f10b)。  
  
#### 运行示例后进行清理  
  
1.  运行完示例后运行示例文件夹中的 Cleanup.bat。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。 在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)以下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。 此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Scenario\TrustedFacade`  
  
## 请参阅