---
title: "支持令牌 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 65a8905d-92cc-4ab0-b6ed-1f710e40784e
caps.latest.revision: 29
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 29
---
# 支持令牌
支持令牌示例演示如何将其他令牌添加到使用 WS\-Security 的消息。  该示例除添加用户名安全令牌外，还添加 X.509 二进制安全令牌。  在 WS\-Security 消息头中将令牌从客户端传递到服务，部分消息使用与 X.509 安全令牌关联的私钥进行签名，以证明 X.509 证书相对于接收方的所有权。  这可用于当要求有多个与消息关联的声明时对发送方进行身份验证或授权。  该服务实现定义“请求\-答复”通信模式的协定。  
  
## 演示  
 本示例演示：  
  
-   客户端如何向服务传递其他安全令牌。  
  
-   服务器如何访问与其他安全令牌关联的声明。  
  
-   如何使用服务器的 X.509 证书保护用于消息加密和签名的对称密钥。  
  
> [!NOTE]
>  本主题的最后介绍了此示例的设置过程和生成说明。  
  
## 使用用户名令牌进行客户端身份验证并支持 X.509 安全令牌  
 服务公开一个用于通信的单一终结点，此终结点是使用 `BindingHelper` 和 `EchoServiceHost` 类以编程方式创建的。  终结点由地址、绑定和协定组成。  此绑定使用 `SymmetricSecurityBindingElement` 和 `HttpTransportBindingElement` 按照自定义绑定进行配置。  本示例设置了 `SymmetricSecurityBindingElement` 以便使用服务 X.509 证书在传输过程中保护对称密钥和在 WS\-Security 消息头中传递 `UserNameToken` 并支持 `X509SecurityToken`。  对称密钥用于对消息正文和用户名安全令牌进行加密。  支持令牌在 WS\-Security 消息头中作为附加二进制安全令牌进行传递。  支持令牌的真实性是使用与支持 X.509 安全令牌关联的私钥通过消息的签名部分证实的。  
  
```  
public static Binding CreateMultiFactorAuthenticationBinding()  
{  
    HttpTransportBindingElement httpTransport = new HttpTransportBindingElement();  
  
    // the message security binding element will be configured to require 2 tokens:  
    // 1) A username-password encrypted with the service token  
    // 2) A client certificate used to sign the message  
  
    // Instantiate a binding element that will require the username/password token in the message (encrypted with the server cert)  
    SymmetricSecurityBindingElement messageSecurity = SecurityBindingElement.CreateUserNameForCertificateBindingElement();  
  
    // Create supporting token parameters for the client X509 certificate.  
    X509SecurityTokenParameters clientX509SupportingTokenParameters = new X509SecurityTokenParameters();  
    // Specify that the supporting token is passed in message send by the client to the service  
    clientX509SupportingTokenParameters.InclusionMode = SecurityTokenInclusionMode.AlwaysToRecipient;  
    // Turn off derived keys  
    clientX509SupportingTokenParameters.RequireDerivedKeys = false;  
    // Augment the binding element to require the client's X509 certificate as an endorsing token in the message  
    messageSecurity.EndpointSupportingTokenParameters.Endorsing.Add(clientX509SupportingTokenParameters);  
  
    // Create a CustomBinding based on the constructed security binding element.  
    return new CustomBinding(messageSecurity, httpTransport);  
}  
  
```  
  
 此行为指定用于客户端身份验证的服务凭据和有关服务 X.509 证书的信息。  本示例在服务 X.509 证书中将 `CN=localhost` 用作主题名称。  
  
```  
override protected void InitializeRuntime()  
{  
    // Extract the ServiceCredentials behavior or create one.  
    ServiceCredentials serviceCredentials =   
        this.Description.Behaviors.Find<ServiceCredentials>();  
    if (serviceCredentials == null)  
    {  
        serviceCredentials = new ServiceCredentials();  
        this.Description.Behaviors.Add(serviceCredentials);  
    }  
  
    // Set the service certificate  
    serviceCredentials.ServiceCertificate.SetCertificate(  
                                       "CN=localhost");  
  
/*  
Setting the CertificateValidationMode to PeerOrChainTrust means that if the certificate is in the Trusted People store, then it will be trusted without performing a validation of the certificate's issuer chain. This setting is used here for convenience so that the sample can be run without having to have certificates issued by a certification authority (CA).  
This setting is less secure than the default, ChainTrust. The security implications of this setting should be carefully considered before using PeerOrChainTrust in production code.  
*/  
    serviceCredentials.ClientCertificate.Authentication.CertificateValidationMode = X509CertificateValidationMode.PeerOrChainTrust;  
  
    // Create the custom binding and add an endpoint to the service.  
    Binding multipleTokensBinding =  
         BindingHelper.CreateMultiFactorAuthenticationBinding();  
    this.AddServiceEndpoint(typeof(IEchoService),   
                          multipleTokensBinding, string.Empty);  
    base.InitializeRuntime();  
}  
```  
  
 服务代码：  
  
```  
[ServiceBehavior(IncludeExceptionDetailInFaults = true)]  
public class EchoService : IEchoService  
{  
    public string Echo()  
    {  
        string userName;  
        string certificateSubjectName;  
        GetCallerIdentities(  
            OperationContext.Current.ServiceSecurityContext,   
            out userName,   
            out certificateSubjectName);  
            return String.Format("Hello {0}, {1}",   
                    userName, certificateSubjectName);  
    }  
  
    public void Dispose()  
    {  
    }  
  
    bool TryGetClaimValue<TClaimResource>(ClaimSet claimSet,   
            string claimType, out TClaimResource resourceValue)  
            where TClaimResource : class  
    {  
        resourceValue = default(TClaimResource);  
        IEnumerable<Claim> matchingClaims =   
            claimSet.FindClaims(claimType, Rights.PossessProperty);  
        if(matchingClaims == null)  
            return false;  
        IEnumerator<Claim> enumerator = matchingClaims.GetEnumerator();  
        if (enumerator.MoveNext())  
        {  
            resourceValue =   
              (enumerator.Current.Resource == null) ? null :   
              (enumerator.Current.Resource as TClaimResource);  
            return true;  
        }  
        else  
        {  
            return false;  
        }  
    }  
  
    // Returns the username and certificate subject name provided by   
    //the client  
    void GetCallerIdentities(ServiceSecurityContext   
        callerSecurityContext,   
        out string userName, out string certificateSubjectName)  
    {  
        userName = null;  
        certificateSubjectName = null;  
  
       // Look in all the claimsets in the authorization context  
       foreach (ClaimSet claimSet in   
               callerSecurityContext.AuthorizationContext.ClaimSets)  
       {  
            if (claimSet is WindowsClaimSet)  
            {  
                // Try to find a Name claim. This will have been   
                // generated from the windows username.  
                string tmpName;  
                if (TryGetClaimValue<string>(claimSet, ClaimTypes.Name,   
                                                      out tmpName))  
                {  
                    userName = tmpName;  
                }  
            }  
            else if (claimSet is X509CertificateClaimSet)  
            {  
                // Try to find an X500DisinguishedName claim. This will   
                // have been generated from the client certificate.  
                X500DistinguishedName tmpDistinguishedName;  
                if (TryGetClaimValue<X500DistinguishedName>(claimSet,   
                               ClaimTypes.X500DistinguishedName,   
                               out tmpDistinguishedName))  
                {  
                    certificateSubjectName = tmpDistinguishedName.Name;  
                }  
            }  
        }  
    }  
}   
```  
  
 客户端终结点的配置方式与服务终结点类似。  客户端使用相同的 `BindingHelper` 类创建绑定。  设置的其余部分位于 `Client` 类中。  客户端设置有关用户名安全令牌、支持 X.509 安全令牌的信息，并在设置代码中将有关服务 X.509 证书的信息设置为客户端终结点行为集合。  
  
```  
 static void Main()  
 {  
     // Create the custom binding and an endpoint address for   
     // the service.  
     Binding multipleTokensBinding =   
         BindingHelper.CreateMultiFactorAuthenticationBinding();  
         EndpointAddress serviceAddress = new EndpointAddress(  
         "http://localhost/servicemodelsamples/service.svc");  
       ChannelFactory<IEchoService> channelFactory = null;  
       IEchoService client = null;  
  
       Console.WriteLine("Username authentication required.");  
       Console.WriteLine(  
         "Provide a valid machine or domain account. [domain\\user]");  
       Console.WriteLine("   Enter username:");  
       string username = Console.ReadLine();  
       Console.WriteLine("   Enter password:");  
       string password = "";  
       ConsoleKeyInfo info = Console.ReadKey(true);  
       while (info.Key != ConsoleKey.Enter)  
       {  
           if (info.Key != ConsoleKey.Backspace)  
           {  
               if (info.KeyChar != '\0')  
               {  
                   password += info.KeyChar;  
                }  
                info = Console.ReadKey(true);  
            }  
            else if (info.Key == ConsoleKey.Backspace)  
            {  
                if (password != "")  
                {  
                    password =   
                       password.Substring(0, password.Length - 1);  
                }  
                info = Console.ReadKey(true);  
            }  
         }  
         for (int i = 0; i < password.Length; i++)  
            Console.Write("*");  
         Console.WriteLine();  
         try  
         {  
           // Create a proxy with the previously create binding and   
           // endpoint address  
              channelFactory =   
                 new ChannelFactory<IEchoService>(  
                     multipleTokensBinding, serviceAddress);  
           // configure the username credentials, the client   
           // certificate and the server certificate on the channel   
           // factory   
           channelFactory.Credentials.UserName.UserName = username;  
           channelFactory.Credentials.UserName.Password = password;  
           channelFactory.Credentials.ClientCertificate.SetCertificate(  
           "CN=client.com", StoreLocation.CurrentUser, StoreName.My);  
              channelFactory.Credentials.ServiceCertificate.SetDefaultCertificate(  
           "CN=localhost", StoreLocation.LocalMachine, StoreName.My);  
           client = channelFactory.CreateChannel();  
           Console.WriteLine("Echo service returned: {0}",   
                                           client.Echo());  
  
           ((IChannel)client).Close();  
           channelFactory.Close();  
        }  
        catch (CommunicationException e)  
        {  
         Abort((IChannel)client, channelFactory);  
         // if there is a fault then print it out  
         FaultException fe = null;  
         Exception tmp = e;  
         while (tmp != null)  
         {  
            fe = tmp as FaultException;  
            if (fe != null)  
            {  
                break;  
            }  
            tmp = tmp.InnerException;  
        }  
        if (fe != null)  
        {  
           Console.WriteLine("The server sent back a fault: {0}",   
         fe.CreateMessageFault().Reason.GetMatchingTranslation().Text);  
        }  
        else  
        {  
         Console.WriteLine("The request failed with exception: {0}",e);  
        }  
    }  
    catch (TimeoutException)  
    {  
        Abort((IChannel)client, channelFactory);  
        Console.WriteLine("The request timed out");  
    }  
    catch (Exception e)  
    {  
         Abort((IChannel)client, channelFactory);  
          Console.WriteLine(  
          "The request failed with unexpected exception: {0}", e);  
    }  
    Console.WriteLine();  
    Console.WriteLine("Press <ENTER> to terminate client.");  
    Console.ReadLine();  
}  
```  
  
## 显示调用方信息  
 若要显示调用方信息，可以使用 `ServiceSecurityContext.Current.AuthorizationContext.ClaimSets`，如下面的代码中所示。  `ServiceSecurityContext.Current.AuthorizationContext.ClaimSets` 包含与当前调用方关联的授权声明。  [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 自动将这些声明提供给消息中接收的每个令牌。  
  
```  
bool TryGetClaimValue<TClaimResource>(ClaimSet claimSet, string   
                         claimType, out TClaimResource resourceValue)  
    where TClaimResource : class  
{  
    resourceValue = default(TClaimResource);  
    IEnumerable<Claim> matchingClaims =   
    claimSet.FindClaims(claimType, Rights.PossessProperty);  
    if (matchingClaims == null)  
          return false;  
    IEnumerator<Claim> enumerator = matchingClaims.GetEnumerator();  
    if (enumerator.MoveNext())  
    {  
        resourceValue = (enumerator.Current.Resource == null) ? null : (enumerator.Current.Resource as TClaimResource);  
        return true;  
    }  
    else  
    {  
         return false;  
    }  
}  
  
// Returns the username and certificate subject name provided by the client  
void GetCallerIdentities(ServiceSecurityContext callerSecurityContext, out string userName, out string certificateSubjectName)  
{  
    userName = null;  
    certificateSubjectName = null;  
  
    // Look in all the claimsets in the authorization context  
    foreach (ClaimSet claimSet in   
      callerSecurityContext.AuthorizationContext.ClaimSets)  
    {  
        if (claimSet is WindowsClaimSet)  
        {  
            // Try to find a Name claim. This will have been generated   
            //from the windows username.  
            string tmpName;  
            if (TryGetClaimValue<string>(claimSet, ClaimTypes.Name,   
                                                     out tmpName))  
            {  
                userName = tmpName;  
            }  
        }  
        else if (claimSet is X509CertificateClaimSet)  
         {  
            //Try to find an X500DisinguishedName claim.   
            //This will have been generated from the client   
            //certificate.  
            X500DistinguishedName tmpDistinguishedName;  
            if (TryGetClaimValue<X500DistinguishedName>(claimSet,   
               ClaimTypes.X500DistinguishedName,   
               out tmpDistinguishedName))  
            {  
                    certificateSubjectName = tmpDistinguishedName.Name;  
            }  
        }  
    }  
}  
```  
  
## 运行示例  
 运行此示例时，客户端首先提示您为用户名令牌提供用户名和密码。  请确保为系统帐户提供正确值，因为服务上的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将用户名令牌中提供的值映射为系统提供的标识。  此后，客户端会显示来自服务的响应。  在客户端窗口中按 Enter 可以关闭客户端。  
  
## 设置批处理文件  
 通过运行此示例随附的 Setup.bat 批处理文件，可以用相关的证书将服务器配置为运行以 Internet 信息服务 \(IIS\) 为宿主的应用程序，该应用程序要求基于服务器证书的安全性。  必须修改此批处理文件，以便跨计算机或在非承载情况下工作。  
  
 下面提供了批处理文件不同节的简要概述，以便可以修改批处理文件从而在相应的配置中运行。  
  
### 创建客户端证书  
 Setup.bat 批处理文件中的以下行创建将要使用的客户端证书。  `%CLIENT_NAME%` 变量指定客户端证书的主题。  本示例使用“client.com”作为主题名称。  
  
 证书存储在 `CurrentUser` 存储位置下的 My（个人）存储区中。  
  
```  
echo ************  
echo making client cert  
echo ************  
makecert.exe -sr CurrentUser -ss MY -a sha1 -n CN=%CLIENT_NAME% -sky exchange -pe  
```  
  
### 将客户端证书安装到服务器的受信任存储区中  
 Setup.bat 批处理文件中的以下行将客户端证书复制到服务器的受信任的人的存储区中。  因为服务器系统不隐式信任 Makecert.exe 生成的证书，所以需要执行此步骤。  如果您已经拥有一个证书，该证书来源于客户端的受信任根证书（例如由 Microsoft 颁发的证书），则不需要执行使用服务器证书填充客户端证书存储区这一步骤。  
  
```  
echo ************  
echo copying client cert to server's CurrentUserstore  
echo ************  
certmgr.exe -add -r CurrentUser -s My -c -n %CLIENT_NAME% -r LocalMachine -s TrustedPeople  
```  
  
### 创建服务器证书  
 Setup.bat 批处理文件中的以下行创建将要使用的服务器证书。  `%SERVER_NAME%` 变量指定服务器名称。  更改此变量可以指定您自己的服务器名称。  此批处理文件中的默认值为 localhost。  
  
 证书存储在 LocalMachine 存储位置下的 My（个人）存储区中。  对于 IIS 承载的服务，证书存储在 LocalMachine 存储区中。  对于自承载服务，应该通过用 CurrentUser 替换字符串 LocalMachine 来修改批处理文件，以便将服务器证书存储在 CurrentUser 存储位置中。  
  
```  
echo ************  
echo Server cert setup starting  
echo %SERVER_NAME%  
echo ************  
echo making server cert  
echo ************  
makecert.exe -sr LocalMachine -ss MY -a sha1 -n CN=%SERVER_NAME% -sky exchange -pe  
```  
  
### 将服务器证书安装到客户端的受信任证书存储区中  
 Setup.bat 批处理文件中的以下行将服务器证书复制到客户端的受信任的人的存储区中。  因为客户端系统不隐式信任 Makecert.exe 生成的证书，所以需要执行此步骤。  如果您已经拥有一个证书，该证书来源于客户端的受信任根证书（例如由 Microsoft 颁发的证书），则不需要执行使用服务器证书填充客户端证书存储区这一步骤。  
  
```  
echo ************  
echo copying server cert to client's TrustedPeople store  
echo ************certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople  
```  
  
### 启用对证书私钥的访问  
 若要从 IIS 承载的服务启用对证书私钥的访问，必须为 IIS 承载的进程运行时所使用的用户帐户授予对该私钥的适当权限。  这将由 Setup.bat 脚本中的最后步骤来完成。  
  
```  
echo ************  
echo setting privileges on server certificates  
echo ************  
for /F "delims=" %%i in ('"%ProgramFiles%\ServiceModelSampleTools\FindPrivateKey.exe" My LocalMachine -n CN^=%SERVER_NAME% -a') do set PRIVATE_KEY_FILE=%%i  
set WP_ACCOUNT=NT AUTHORITY\NETWORK SERVICE  
(ver | findstr /C:"5.1") && set WP_ACCOUNT=%COMPUTERNAME%\ASPNET  
echo Y|cacls.exe "%PRIVATE_KEY_FILE%" /E /G "%WP_ACCOUNT%":R  
iisreset  
```  
  
##### 设置、生成和运行示例  
  
1.  请确保已执行 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  若要生成解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
3.  若要用单一计算机配置或跨计算机配置来运行示例，请按照下列说明进行操作。  
  
##### 在同一计算机上运行示例  
  
1.  使用管理员特权在 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 命令提示中运行示例安装文件夹中的 Setup.bat。  这将安装运行示例所需的所有证书。  
  
    > [!NOTE]
    >  Setup.bat 批处理文件设计为通过 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 命令提示运行。  [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 命令提示中设置的 PATH 环境变量指向包含 Setup.bat 脚本所需的可执行文件的目录。  确保在运行完该示例后运行 Cleanup.bat 移除证书。  其他安全示例使用相同的证书。  
  
2.  启动 \\client\\bin 中的 Client.exe。  客户端活动将显示在客户端控制台应用程序上。  
  
3.  如果客户端与服务无法进行通信，请参见[疑难解答提示](http://msdn.microsoft.com/zh-cn/8787c877-5e96-42da-8214-fa737a38f10b)。  
  
##### 跨计算机运行示例  
  
1.  在服务计算机上创建目录。  使用 Internet 信息服务 \(IIS\) 管理工具为此目录创建名为 servicemodelsamples 的虚拟应用程序。  
  
2.  将服务程序文件从 \\inetpub\\wwwroot\\servicemodelsamples 复制到服务计算机上的虚拟目录中。  确保复制 \\bin 子目录中的文件。  另外，将 Setup.bat、Cleanup.bat 和 ImportClientCert.bat 文件复制到服务计算机上。  
  
3.  在客户端计算机上为这些客户端二进制文件创建一个目录。  
  
4.  将客户端程序文件复制到客户端计算机上的客户端目录中。  另外，将 Setup.bat、Cleanup.bat 和 ImportServiceCert.bat 文件复制到客户端上。  
  
5.  在服务器上，在使用管理员特权打开的 Visual Studio 命令提示中运行 `setup.bat service`。  如果采用 `service` 参数运行 `` `setup.bat`，则使用计算机的完全限定域名创建一个服务证书，并将此服务证书导出到名为 Service.cer 的文件中。  
  
6.  编辑 Web.config 以反映新的证书名（在 [\<serviceCertificate\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md)的 `findValue` 属性中），该名称与计算机的完全限定域名相同。  
  
7.  将服务目录中的 Service.cer 文件复制到客户端计算机上的客户端目录中。  
  
8.  在客户端上，在使用管理员特权打开的 Visual Studio 命令提示中运行 `setup.bat client`。  如果使用 `client` 参数运行 `setup.bat`，则会创建一个名为 client.com 的客户端证书，并将此客户端证书导出到名为 Client.cer 的文件中。  
  
9. 在客户端计算机上的 Client.exe.config 文件中，更改终结点的地址值，使其与服务的新地址相匹配。  通过用服务器的完全限定域名替换 localhost 来执行此操作。  
  
10. 将客户端目录中的 Client.cer 文件复制到服务器上的服务目录中。  
  
11. 在客户端上，运行 ImportServiceCert.bat。  这会将 Service.cer 文件中的服务证书导入 CurrentUser – TrustedPeople 存储区。  
  
12. 在服务器上，运行 ImportClientCert.bat，这会将 Client.cer 文件中的客户端证书导入 LocalMachine \- TrustedPeople 存储区。  
  
13. 在客户端计算机上，从命令提示符窗口中启动 Client.exe。  如果客户端与服务无法进行通信，请参见[疑难解答提示](http://msdn.microsoft.com/zh-cn/8787c877-5e96-42da-8214-fa737a38f10b)。  
  
##### 运行示例后进行清理  
  
-   运行完示例后运行示例文件夹中的 Cleanup.bat。  
  
> [!NOTE]
>  此脚本不会在跨计算机运行此示例时移除客户端上的服务证书。  如果已跨计算机运行使用证书的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 示例，请确保清除已安装在 CurrentUser \- TrustedPeople 存储区中的服务证书。  为此，请使用以下命令：`certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>`，例如：`certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`。  
  
## 请参阅