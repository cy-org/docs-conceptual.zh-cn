---
title: "成员资格和角色提供程序 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0d11a31c-e75f-4fcf-9cf4-b7f26e056bcd
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# 成员资格和角色提供程序
此“成员资格和角色提供程序”示例演示服务如何使用 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 成员资格和角色提供程序来对客户端进行身份验证和授权。  
  
 在此示例中，客户端是一个控制台应用程序 \(.exe\)，服务是由 Internet 信息服务 \(IIS\) 承载的。  
  
> [!NOTE]
>  本主题的末尾介绍了此示例的设置过程和生成说明。  
  
 此示例演示：  
  
-   客户端如何使用用户名和密码组合进行身份验证。  
  
-   服务器如何根据 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 成员资格提供程序来验证客户端凭据。  
  
-   如何使用服务器的 X.509 证书对该服务器进行身份验证。  
  
-   服务器如何使用 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 角色提供程序将经过身份验证的客户端映射到角色。  
  
-   服务器如何使用 `PrincipalPermissionAttribute` 控制对服务公开的某些方法的访问。  
  
 成员资格和角色提供程序配置为使用 SQL Server 支持的存储。连接字符串和各个选项在服务配置文件中指定。成员资格提供程序命名为 `SqlMembershipProvider`，而角色提供程序命名为 `SqlRoleProvider`。  
  
```  
<!-- Set the connection string for SQL Server -->  
<connectionStrings>  
  <add name="SqlConn"   
       connectionString="Data Source=localhost;Integrated Security=SSPI;Initial Catalog=aspnetdb;" />  
</connectionStrings>  
  
<system.web>  
  <!-- Configure the Sql Membership Provider -->  
  <membership defaultProvider="SqlMembershipProvider" userIsOnlineTimeWindow="15">  
    <providers>  
      <clear />  
      <add   
        name="SqlMembershipProvider"   
        type="System.Web.Security.SqlMembershipProvider"   
        connectionStringName="SqlConn"  
        applicationName="MembershipAndRoleProviderSample"  
        enablePasswordRetrieval="false"  
        enablePasswordReset="false"  
        requiresQuestionAndAnswer="false"  
        requiresUniqueEmail="true"  
        passwordFormat="Hashed" />  
    </providers>  
  </membership>  
  
  <!-- Configure the Sql Role Provider -->  
  <roleManager enabled ="true"   
               defaultProvider ="SqlRoleProvider" >  
    <providers>  
      <add name ="SqlRoleProvider"   
           type="System.Web.Security.SqlRoleProvider"   
           connectionStringName="SqlConn"   
           applicationName="MembershipAndRoleProviderSample"/>  
    </providers>  
  </roleManager>  
</system.web>  
```  
  
 服务会公开一个单一终结点以便与使用 Web.config 配置文件定义的服务进行通信。终结点由地址、绑定和协定组成。绑定使用默认使用 Windows 身份验证的标准 `wsHttpBinding` 进行配置。此示例将标准 `wsHttpBinding` 设置为使用用户名身份验证。该行为指定将使用服务器证书进行服务身份验证。服务器证书包含的 `SubjectName` 的值必须与 [\<serviceCertificate\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md) 配置元素中的 `findValue` 属性的值相同。此外，该行为指定用户名\-密码对的身份验证由 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 成员资格提供程序执行，角色映射由 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 角色提供程序执行，方法是指定为这两个提供程序定义的名称。  
  
```  
<system.serviceModel>  
  
  <protocolMapping>  
    <add scheme="http" binding="wsHttpBinding" />  
  </protocolMapping>  
  
  <bindings>  
    <wsHttpBinding>  
      <!-- Set up a binding that uses Username as the client credential type -->  
      <binding>  
        <security mode ="Message">  
          <message clientCredentialType ="UserName"/>  
        </security>  
      </binding>  
    </wsHttpBinding>  
  </bindings>  
  
  <behaviors>  
    <serviceBehaviors>  
      <behavior>  
        <!-- Configure role based authorization to use the Role Provider -->  
        <serviceAuthorization principalPermissionMode ="UseAspNetRoles"  
                              roleProviderName ="SqlRoleProvider" />  
        <serviceCredentials>  
          <!-- Configure user name authentication to use the Membership Provider -->  
          <userNameAuthentication userNamePasswordValidationMode ="MembershipProvider"   
                                  membershipProviderName ="SqlMembershipProvider"/>  
          <!-- Configure the service certificate -->  
          <serviceCertificate storeLocation ="LocalMachine"   
                              storeName ="My"   
                              x509FindType ="FindBySubjectName"  
                              findValue ="localhost" />  
        </serviceCredentials>  
        <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
        <serviceDebug includeExceptionDetailInFaults="false" />  
        <serviceMetadata httpGetEnabled="true"/>  
      </behavior>  
    </serviceBehaviors>  
  </behaviors>  
</system.serviceModel>  
```  
  
 运行此示例时，客户端使用三个不同的用户帐户来调用各个服务操作：Alice、Bob 和 Charlie。操作请求和响应显示在客户端控制台窗口中。以用户“Alice”身份执行的所有四个调用都应成功。用户“Bob”在尝试调用 Divide 方法时会收到拒绝访问错误。用户“Charlie”在尝试调用 Multiply 方法时会收到拒绝访问错误。在客户端窗口中按 Enter 可以关闭客户端。  
  
### 设置、生成和运行示例  
  
1.  若要生成 C\# 或 Visual Basic .NET 版本的解决方案，请按照[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)中的说明进行操作。  
  
2.  确保您已配置了 [ASP.NET 应用程序服务数据库](http://go.microsoft.com/fwlink/?LinkId=94997)（可能为英文网页）。  
  
    > [!NOTE]
    >  如果运行的是 SQL Server Express Edition，则服务器名称是。\\SQLEXPRESS。配置 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 应用程序服务数据库时应使用该服务器，Web.config 连接字符串中也应使用该服务器。  
  
    > [!NOTE]
    >  [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 工作进程帐户应对本步骤中创建的数据库具有权限。使用 sqlcmd 实用工具或 SQL Server Management Studio 来完成该工作。  
  
3.  若要用单一计算机配置或跨计算机配置来运行示例，请按照下列说明进行操作。  
  
### 在同一计算机上运行示例  
  
1.  请确保路径包含 Makecert.exe 所在的文件夹。  
  
2.  在使用管理员特权运行的 Visual Studio 命令提示中，运行示例安装文件夹中的 Setup.bat。这将安装运行此示例所需的服务证书。  
  
3.  启动 \\client\\bin 中的 Client.exe。客户端活动将显示在客户端控制台应用程序上。  
  
4.  如果客户端与服务无法进行通信，请参见[Troubleshooting Tips](http://msdn.microsoft.com/zh-cn/8787c877-5e96-42da-8214-fa737a38f10b)。  
  
### 跨计算机运行示例  
  
1.  在服务计算机上创建目录。使用 Internet Information Services \(IIS\) 管理工具为此目录创建名为 servicemodelsamples 的虚拟应用程序。  
  
2.  将服务程序文件从 \\inetpub\\wwwroot\\servicemodelsamples 复制到服务计算机上的虚拟目录中。确保复制 \\bin 子目录中的文件。另外，将 Setup.bat、GetComputerName.vbs 和 Cleanup.bat 文件复制到服务计算机上。  
  
3.  在客户端计算机上为这些客户端二进制文件创建一个目录。  
  
4.  将客户端程序文件复制到客户端计算机上的客户端目录中。另外，将 Setup.bat、Cleanup.bat 和 ImportServiceCert.bat 文件复制到客户端上。  
  
5.  在服务器上，使用管理特权打开 Visual Studio 命令提示并运行 `setup.bat service`。如果采用 `service` 参数运行 `setup.bat` ，则使用计算机的完全限定域名创建一个服务证书，并将此服务证书导出到名为 Service.cer 的文件中。  
  
6.  （在 [\<serviceCertificate\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-servicecredentials.md) 的 `findValue` 属性中）编辑 Web.config 以反映新的证书名称，该名称与计算机的完全限定域名相同。  
  
7.  将服务目录中的 Service.cer 文件复制到客户端计算机上的客户端目录中。  
  
8.  在客户端计算机上的 Client.exe.config 文件中，更改终结点的地址值，使其与服务的新地址相匹配。  
  
9. 在客户端上，使用管理特权打开 Visual Studio 命令提示并运行 ImportServiceCert.bat。这会将 Service.cer 文件中的服务证书导入 CurrentUser – TrustedPeople 存储区。  
  
10. 在客户端计算机上，在命令提示符下启动 Client.exe。如果客户端与服务无法进行通信，请参见[Troubleshooting Tips](http://msdn.microsoft.com/zh-cn/8787c877-5e96-42da-8214-fa737a38f10b)。  
  
### 运行示例后进行清理  
  
-   运行完示例后运行示例文件夹中的 Cleanup.bat。  
  
> [!NOTE]
>  此脚本不会在跨计算机运行此示例时移除客户端上的服务证书。如果已运行跨计算机使用证书的 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 示例，请确保清除已安装在 CurrentUser \- TrustedPeople 存储中的服务证书。为此，请使用以下命令：`certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>`，例如：`certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com`。  
  
## Setup 批处理文件  
 通过运行此示例随附的 Setup.bat 批处理文件，可以用相关的证书将服务器配置为运行需要基于服务器证书的安全性的自承载应用程序。必须修改此批处理文件，以便跨计算机或在非承载情况下工作。  
  
 下面提供了批处理文件不同节的简要概述，以便可以修改批处理文件从而在相应的配置中运行。  
  
-   创建服务器证书。  
  
     Setup.bat 批处理文件中的以下行创建将要使用的服务器证书。%SERVER\_NAME% 变量指定服务器名称。更改此变量可以指定您自己的服务器名称。在该批处理文件中，此名称默认为 localhost。  
  
     证书存储在 LocalMachine 存储位置下的 My（个人）存储区中。  
  
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
  
     Setup.bat 批处理文件中的以下行将服务器证书复制到客户端的受信任的人的存储区中。因为客户端系统不隐式信任 Makecert.exe 生成的证书，所以需要执行此步骤。如果已经拥有一个证书，该证书来源于客户端的受信任根证书（例如由 Microsoft 颁发的证书），则不需要执行使用服务器证书填充客户端证书存储区这一步骤。  
  
    ```  
    certmgr.exe -add -r LocalMachine -s My -c -n %SERVER_NAME% -r CurrentUser -s TrustedPeople  
    ```  
  
## 请参阅