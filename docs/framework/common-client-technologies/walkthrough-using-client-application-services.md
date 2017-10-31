---
title: "演练：使用客户端应用程序服务"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- application services host [client application services]
- client application services, walkthroughs
ms.assetid: bb7c8950-4517-4dae-b705-b74a14059b26
caps.latest.revision: 47
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 64a27269ee6f3711f0c51f2c97cd8876c3ea6103
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="walkthrough-using-client-application-services"></a>演练：使用客户端应用程序服务
本主题介绍如何创建使用客户端应用程序服务对用户进行身份验证并检索用户角色和设置的 Windows 应用程序。  
  
 在本演练中，你将要执行以下任务：  
  
-   创建一个 Windows 窗体应用程序并使用 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 项目设计器启用和配置客户端应用程序服务。  
  
-   创建一个简单 ASP.NET Web 服务应用程序，以承载应用程序服务并测试客户端配置。  
  
-   向应用程序添加 Forms 身份验证。 首先使用硬编码的用户名和密码测试服务。 随后通过在应用程序配置中将一个登录窗体指定为凭据提供程序，来添加该窗体。  
  
-   添加基于角色的功能，从而仅对具有“manager”角色的用户启用并显示一个按钮。  
  
-   访问 Web 设置。 首先在项目设计器的 **“设置”** 页上加载经过身份验证（测试）的用户的 Web 设置。 随后使用 Windows 窗体设计器将文本框绑定到 Web 设置。 最后，将修改的值保存回服务器。  
  
-   实现注销。 向窗体中添加一个注销选项，并调用一个注销方法。  
  
-   启用脱机模式。 提供一个复选框，以便用户可以指定其连接状态。 随后使用此值指定客户端应用程序服务提供程序是否使用本地缓存的数据而不是访问其 Web 服务。 最后，在应用程序返回联机模式时对当前用户重新进行身份验证。  
  
## <a name="prerequisites"></a>先决条件  
 你需要以下组件来完成本演练：  
  
-   [!INCLUDE[vs_orcas_long](../../../includes/vs-orcas-long-md.md)]。  
  
## <a name="creating-the-client-application"></a>创建客户端应用程序  
 将执行的第一个操作是创建一个 Windows 窗体项目。 本演练使用 Windows 窗体，因为更多的人熟悉它，不过过程类似于 Windows Presentation Foundation (WPF) 项目。  
  
#### <a name="to-create-a-client-application-and-enable-client-application-services"></a>创建客户端应用程序和启用客户端应用程序服务  
  
1.  在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中，选择“文件”|“新建”|“项目”菜单选项。  
  
2.  在“新建项目”对话框的“项目类型”窗格中，展开“Visual Basic”或“Visual C#”节点，然后选择“Windows”项目类型。  
  
3.  确保选择 **“.NET Framework 3.5”** ，然后选择 **“Windows 窗体应用程序”** 模板。  
  
4.  将项目 **“名称”** 更改为 `ClientAppServicesDemo`，然后单击 **“确定”**。  
  
     一个新 Windows 窗体项目随即在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]中打开。  
  
5.  在 **“项目”** 菜单上，选择 **“ClientAppServicesDemo 属性”**。  
  
     项目设计器随即出现。  
  
6.  在 **“服务”** 选项卡上，选择 **“启用客户端应用程序服务”**。  
  
7.  确保选择 **“使用 Forms 身份验证”** ，然后将 **“身份验证服务位置”**、 **“角色服务位置”**和 **“Web 设置服务位置”** 设置为 `http://localhost:55555/AppServices`。  
  
8.  对于 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]，在 **“应用程序”** 选项卡上，将 **“身份验证模式”** 设置为 **“由应用程序定义”**。  
  
 设计器会将指定设置存储在应用程序的 app.config 文件中。  
  
 此时，应用程序配置为从同一个主机访问所有三个服务。 在下一部分中，你会以简单 Web 服务应用程序的形式创建主机，从而使你可以测试客户端配置。  
  
## <a name="creating-the-application-services-host"></a>创建应用程序服务主机  
 在本部分中，你会创建一个简单 Web 服务应用程序，该应用程序从本地 SQL Server Compact 数据库文件访问用户数据。 然后，你将使用 [ASP.NET Web Site Administration Tool](http://msdn.microsoft.com/library/100ddd8b-7d11-4df9-91ef-0bbbe92e5aec)填充数据库。 通过这种简单配置可以快速测试客户端应用程序。 作为替代方法，可以配置 Web 服务主机以从完整 SQL Server 数据库或通过自定义 <xref:System.Web.Security.MembershipProvider> 和 <xref:System.Web.Security.RoleProvider> 类访问用户数据。 有关详细信息，请参阅 [Creating and Configuring the Application Services Database for SQL Server](http://msdn.microsoft.com/library/ab894e83-7e2f-4af8-a116-b1bff8f815b2)。  
  
 在下面的过程中，会创建和配置 AppServices Web 服务。  
  
#### <a name="to-create-and-configure-the-application-services-host"></a>创建和配置应用程序服务主机  
  
1.  在“解决方案资源管理器”中，选择 ClientAppServicesDemo 解决方案，然后在“文件”菜单上，选择“添加”|“新建项目”。  
  
2.  在“添加新项目”对话框的“项目类型”窗格中，展开“Visual Basic”或“Visual C#”节点，然后选择“Web”项目类型。  
  
3.  确保选择 **“.NET Framework 3.5”** ，然后选择 **“ASP.NET Web 服务应用程序”** 模板。  
  
4.  将项目 **“名称”** 更改为 `AppServices` ，然后单击 **“确定”**。  
  
     一个新 ASP.NET Web 服务应用程序项目随即添加到解决方案中，并且 Service1.asmx.vb 或 Service1.asmx.cs 文件会出现在编辑器中。  
  
    > [!NOTE]
    >  此示例中不使用 Service1.asmx.vb 或 Service1.asmx.cs 文件。 如果要使工作环境整洁，可以关闭它，并从 **“解决方案资源管理器”**中删除。  
  
5.  在 **“解决方案资源管理器”**中，选择 AppServices 项目，然后在 **“项目”** 菜单上，选择 **“AppServices 属性”**。  
  
     项目设计器随即出现。  
  
6.  在 **“Web”** 选项卡上，确保选择 **“使用 Visual Studio 开发服务器”** 。  
  
7.  选择 **“特定端口”**，指定值 `55555`，然后将 **“虚拟路径”** 设置为 `/AppServices`。  
  
8.  保存所有文件。  
  
9. 在 **“解决方案资源管理器”**中，打开 Web.config 并找到 `<system.web>` 开始标记。  
  
10. 在 `<system.web>` 标记之前添加以下代码：  
  
     此标记中的 `authenticationService`、 `profileService`和 `roleService` 元素会启用并配置应用程序服务。 为进行测试， `requireSSL` 元素的 `authenticationService` 特性设置为“false”。 `readAccessProperties` 元素的 `writeAccessProperties` 和 `profileService` 特性指示 `WebSettingsTestText` 属性为读/写。  
  
    > [!NOTE]
    >  在生产代码中，应始终通过安全套接字层（SSL，使用 HTTPS 协议）访问身份验证服务。 有关如何设置 SSL 的信息，请参阅 [配置安全套接字层（IIS 6.0 操作指南）](http://go.microsoft.com/fwlink/?LinkId=91844)。  
  
    ```xml  
    <system.web.extensions>  
      <scripting>  
        <webServices>  
          <authenticationService enabled="true" requireSSL = "false"/>  
          <profileService enabled="true"  
            readAccessProperties="WebSettingsTestText"  
            writeAccessProperties="WebSettingsTestText" />  
          <roleService enabled="true"/>  
        </webServices>  
      </scripting>  
    </system.web.extensions>  
    ```  
  
11. 在 `<system.web>` 开始标记之后添加以下标记，以便它位于 `<system.web>` 元素中。  
  
     `profile` 元素会配置一个名为 `WebSettingsTestText`的 Web 设置。  
  
    ```xml  
    <profile enabled="true" >  
      <properties>  
        <add name="WebSettingsTestText" type="string"   
          readOnly="false" defaultValue="DefaultText"   
          serializeAs="String" allowAnonymous="false" />  
      </properties>  
    </profile>  
    ```  
  
 在下面的过程中，会使用 ASP.NET 网站管理工具完成服务配置并填充本地数据库文件。 将添加两个名为 `employee` 和 `manager` 的用户，它们属于两个具有相同名称的角色。 用户密码分别为 `employee!` 和 `manager!` 。  
  
#### <a name="to-configure-membership-and-roles"></a>配置成员资格和角色  
  
1.  在 **“解决方案资源管理器”**中，选择 AppServices 项目，然后在 **“项目”** 菜单上，选择 **“ASP.NET 配置”**。  
  
     **“ASP.NET 网站管理工具”** 随即出现。  
  
2.  在 **“安全”** 选项卡上，单击 **“使用安全设置向导按部就班地配置安全性”**。  
  
     **“安全设置向导”** 随即出现并显示 **“欢迎使用”** 步骤。  
  
3.  单击 **“下一步”**。  
  
     **“选择访问方法”** 步骤随即出现。  
  
4.  选择 **“通过 Internet”**。 这会将服务配置为使用 Forms 身份验证，而不是 Windows 身份验证。  
  
5.  单击两次 **“下一步”** 。  
  
     **“定义角色”** 步骤随即出现。  
  
6.  选择 **“为此网站启用角色”**。  
  
7.  单击 **“下一步”**。 **“创建新角色”** 窗体随即出现。  
  
8.  在 **“新角色名称”** 文本框中，输入 `manager` ，然后单击 **“添加角色”**。  
  
     **“现有角色”** 表随即出现，其中包含指定值。  
  
9. 在 **“新角色名称”** 文本框中，将 `manager` 替换为 `employee` ，然后单击 **“添加角色”**。  
  
     新值随即出现在 **“现有角色”** 表。  
  
10. 单击 **“下一步”**。  
  
     **“添加新用户”** 步骤随即出现。  
  
11. 在 **“创建用户”** 窗体中，指定以下值。  
  
  	|||  
  	|-|-|  
  	|**用户名**|`manager`|  
  	|**密码**|`manager!`|  
  	|**确认密码**|`manager!`|  
  	|**电子邮件**|`manager@contoso.com`|  
  	|**安全提示问题**|`manager`|  
  	|**安全提示问题的答案**|`manager`|  
  
12. 单击 **“创建用户”**。  
  
     一条成功消息随即出现。  
  
    > [!NOTE]
    >  **“电子邮件”**、 **“安全提示问题”**和 **“安全提示问题的答案”** 值是窗体必需的，但不在此示例中使用。  
  
13. 单击 **“继续”**。  
  
     **“创建用户”** 窗体随即再次显示。  
  
14. 在 **“创建用户”** 窗体中，指定以下值。  
  
  	|||  
  	|-|-|  
  	|**用户名**|`employee`|  
  	|**密码**|`employee!`|  
  	|**确认密码**|`employee!`|  
  	|**电子邮件**|`employee@contoso.com`|  
  	|**安全提示问题**|`Employee`|  
  	|**安全提示问题的答案**|`employee`|  
  
15. 单击 **“创建用户”**。  
  
     一条成功消息随即出现。  
  
16. 单击 **“完成”**。  
  
     **“网站管理工具”** 随即再次出现。  
  
17. 单击 **“管理用户”**。  
  
     用户列表随即出现。  
  
18. 对 **“employee”** 用户单击 **“编辑角色”** ，然后选择 **“employee”** 角色。  
  
19. 对 **“manager”** 用户单击 **“编辑角色”** ，然后选择 **“manager”** 角色。  
  
20. 关闭承载 **“网站管理工具”**的浏览器窗口。  
  
21. 如果一个消息框出现，询问是否要重载修改后的 Web.config 文件，请单击 **“是”**。  
  
 这会完成 Web 服务设置。 此时，可以按 F5 以运行客户端应用程序， **“ASP.NET Development Server”** 会随客户端应用程序自动启动。 该服务器会在你退出应用程序之后继续运行，但是会在你重新启动应用程序时重新启动。 这使它可以检测对 Web.config 进行的任何更改。  
  
 若要手动停止服务器，请在任务栏的通知区域中右键单击“ASP.NET Development Server”图标，然后单击 **“停止”**。 这有时可用于确保进行正常的重新启动。  
  
## <a name="adding-forms-authentication"></a>添加 Forms 身份验证  
 在下面的过程中，会将代码添加到主窗体，该代码会尝试验证用户，并在用户提供的凭据无效时拒绝访问。 使用硬编码的用户名和密码测试服务。  
  
#### <a name="to-validate-the-user-in-your-application-code"></a>在应用程序代码中验证用户  
  
1.  在“解决方案资源管理器”的 ClientAppServicesDemo 项目中，添加对 System.Web 程序集的引用。  
  
2.  选择 Form1 文件，然后从 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 主菜单中选择“视图”|“代码”。  
  
3.  在代码编辑器中，将以下语句添加到 Form1 文件顶部：  
  
     [!code-csharp[ClientApplicationServices#001](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Form1.cs#001)]  [!code-vb[ClientApplicationServices#001](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Form1.vb#001)]  
  
4.  在 **“解决方案资源管理器”**中，双击 Form1 以显示设计器。  
  
5.  在设计器中，双击窗体图面，以生成名为 <xref:System.Windows.Forms.Form.Load?displayProperty=fullName> 的 `Form1_Load`事件处理程序。  
  
     代码编辑器随即出现，光标位于 `Form1_Load` 方法中。  
  
6.  将以下代码添加到 `Form1_Load` 方法中。  
  
     此代码通过退出应用程序，对未通过身份验证的用户拒绝访问。 或者，可以允许未通过身份验证的用户访问窗体，但拒绝对特定功能的访问。 通常不会像这样对用户名和密码进行硬编码，但对于测试十分有用。 在下一部分中，你会将此代码替换为显示登录对话框并包含异常处理的更可靠代码。  
  
     请注意， `static` <xref:System.Web.Security.Membership.ValidateUser%2A?displayProperty=fullName> 方法处于 [!INCLUDE[dnprdnext](../../../includes/dnprdnext-md.md)]中。 此方法将其工作委托给配置的身份验证提供程序，并在身份验证成功时返回 `true` 。 应用程序不需要直接引用客户端身份验证提供程序。  
  
     [!code-csharp[ClientApplicationServices#300](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Class1.cs#300)]  [!code-vb[ClientApplicationServices#300](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Class1.vb#300)]  
  
 现在可以按 F5 以运行应用程序，因为提供了正确的用户名和密码，所以会看到窗体。  
  
> [!NOTE]
>  如果无法运行应用程序，请尝试停止 ASP.NET Development Server。 该服务器重新启动时，验证该端口是否设置为 55555。  
  
 若要改为查看错误消息，请更改 <xref:System.Web.Security.Membership.ValidateUser%2A> 参数。 例如，将第二个 `"manager!"` 参数替换为不正确的密码（如 `"MANAGER"`）。  
  
## <a name="adding-a-login-form-as-a-credentials-provider"></a>添加一个登录窗体作为凭据提供程序  
 可以在应用程序代码中获取用户凭据，并将它们传递给 <xref:System.Web.Security.Membership.ValidateUser%2A> 方法。 但是，使凭据获取代码独立于应用程序代码通常会十分有用，以免你以后要更改它。  
  
 在下面的过程中，会将应用程序配置为使用凭据提供程序，然后更改 <xref:System.Web.Security.Membership.ValidateUser%2A> 方法调用以便为两个参数传递 <xref:System.String.Empty> 。 空字符串指示 <xref:System.Web.Security.Membership.ValidateUser%2A> 方法调用配置的凭据提供程序的 <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider.GetCredentials%2A> 方法。  
  
#### <a name="to-configure-your-application-to-use-a-credentials-provider"></a>将应用程序配置为使用凭据提供程序  
  
1.  在 **“解决方案资源管理器”**中，选择 ClientAppServicesDemo 项目，然后在 **“项目”** 菜单上，选择 **“ClientAppServicesDemo 属性”**。  
  
     项目设计器随即出现。  
  
2.  在 **“服务”** 选项卡上，将 **“可选: 凭据提供程序”** 设置为以下值。 此值指示程序集限定的类型名。  
  
    ```  
    ClientAppServicesDemo.Login, ClientAppServicesDemo  
    ```  
  
3.  在 Form1 代码文件中，将 `Form1_Load` 方法中的代码替换为以下代码。  
  
     此代码会显示一条欢迎消息，然后调用会在下一步中添加的 `ValidateUsingCredentialsProvider` 方法。 如果用户未通过身份验证，则 `ValidateUsingCredentialsProvider` 方法会返回 `false` ，并且 `Form1_Load` 方法会返回。 这会在应用程序退出之前阻止任何其他代码运行。 欢迎消息可用于清楚地表明应用程序重新启动。 你会在本演练后面实现注销时添加用于重新启动应用程序的代码。  
  
     [!code-csharp[ClientApplicationServices#011](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Form1.cs#011)]  [!code-vb[ClientApplicationServices#011](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Form1.vb#011)]  
  
4.  在 `Form1_Load` 方法之后添加以下方法。  
  
     此方法将空字符串传递给 `static` <xref:System.Web.Security.Membership.ValidateUser%2A?displayProperty=fullName> 方法，这会使登录对话框出现。 如果身份验证服务不可用，则 <xref:System.Web.Security.Membership.ValidateUser%2A> 方法会引发 <xref:System.Net.WebException>。 在这种情况下， `ValidateUsingCredentialsProvider` 方法会显示一条警告消息，并询问用户是否要在脱机模式下重试。 此功能需要 **How to: Configure Client Application Services** 中介绍的 [“将密码哈希保存在本地以实现脱机登录”](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md)功能。 此功能会在默认情况下为新项目启用。  
  
     如果用户未通过验证，则 `ValidateUsingCredentialsProvider` 方法会显示一条错误消息并退出应用程序。 最后，此方法会返回身份验证尝试的结果。  
  
     [!code-csharp[ClientApplicationServices#020](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Form1.cs#020)]  [!code-vb[ClientApplicationServices#020](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Form1.vb#020)]  
  
### <a name="creating-a-login-form"></a>创建一个登录窗体  
 凭据提供程序是实现 <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider> 接口的类。 此接口具有名为 <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider.GetCredentials%2A> 的单一方法，它返回 <xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationCredentials> 对象。 以下过程介绍如何创建一个登录对话框，它实现 <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider.GetCredentials%2A> 以显示本身并返回用户指定的凭据。  
  
 为 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 和 C# 提供了单独的过程，因为 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 提供 **“登录窗体”** 模板。 这可节省一些时间并减少编码工作。  
  
##### <a name="to-create-a-login-dialog-box-as-a-credentials-provider-in-visual-basic"></a>在 Visual Basic 中创建一个登录对话框作为凭据提供程序  
  
1.  在 **“解决方案资源管理器”**中，选择 ClientAppServicesDemo 项目，然后在 **“项目”** 菜单上，选择 **“添加新项”**。  
  
2.  在 **“添加新项”** 对话框中，选择 **“登录窗体”** 模板，将项 **“名称”** 更改为 `Login.vb`，然后单击 **“添加”**。  
  
     登录对话框随即出现在 Windows 窗体设计器中。  
  
3.  在该设计器中，选择 **“确定”** 按钮，然后在 **“属性”** 窗口中，将 `DialogResult` 设置为 `OK`。  
  
4.  在设计器中，在 `CheckBox` “密码” **文本框下将一个** 控件添加到窗体。  
  
5.  在“属性”窗口中，将“(Name)”值指定为 `rememberMeCheckBox`，并将“Text”值指定为 `&Remember me`。  
  
6.  从 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 主菜单中选择“视图”|“代码”。  
  
7.  在代码编辑器中，将以下代码添加到文件顶部：  
  
     [!code-vb[ClientApplicationServices#101](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Login.vb#101)]  
  
8.  修改类签名，以便类实现 <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider> 接口。  
  
     [!code-vb[ClientApplicationServices#110](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Class1.vb#110)]  
  
9. 确保光标位于 `IClientformsAuthenticationCredentialsProvider`之后，然后按 Enter 以生成 `GetCredentials` 方法。  
  
10. 找到 <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider.GetCredentials%2A> 实现，然后将它替换为以下代码。  
  
     [!code-vb[ClientApplicationServices#120](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Login.vb#120)]  
  
 下面的 C# 过程为简单登录对话框提供了完整代码清单。 此对话框的布局有点粗糙，但重要的部分是 <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider.GetCredentials%2A> 实现。  
  
##### <a name="to-create-a-login-dialog-box-as-a-credentials-provider-in-c"></a>在 C# 中创建一个登录对话框作为凭据提供程序  
  
1.  在 **“解决方案资源管理器”**中，选择 ClientAppServicesDemo 项目，然后在 **“项目”** 菜单上，选择 **“添加类”**。  
  
2.  在 **“添加新项”** 对话框中，将 **“名称”** 更改为 `Login.cs`，然后单击 **“添加”**。  
  
     Login.cs 文件随即在代码编辑器中打开。  
  
3.  将默认代码替换为以下代码。  
  
     [!code-csharp[ClientApplicationServices#200](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Login.cs#200)]  
  
 现在可以运行应用程序，并看到登录对话框出现。 若要测试此代码，请尝试不同的凭据（有效和无效），并确认只能使用有效凭据访问窗体。 有效用户名分别为 `employee` 和 `manager` ，密码分别为 `employee!` 和 `manager!` 。  
  
> [!NOTE]
>  此时不要选择 **“记住我”** ，否则在本演练后面实现注销之前，无法以其他用户身份登录。  
  
## <a name="adding-role-based-functionality"></a>添加基于角色的功能  
 在下面的过程中，会向窗体添加一个按钮，仅对采用 manager 角色的用户显示它。  
  
#### <a name="to-change-the-user-interface-based-on-user-role"></a>基于用户角色更改用户界面  
  
1.  在“解决方案资源管理器”的 ClientAppServicesDemo 项目中，选择 Form1，然后从 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 主菜单中选择“视图”|“设计器”。  
  
2.  在设计器中，从“工具箱”向窗体添加一个 <xref:System.Windows.Forms.Button> 控件。  
  
3.  在 **“属性”** 窗口中，为该按钮设置以下属性。  
  
  	|属性|值|  
  	|--------------|-----------|  
  	|**“(名称)”**|managerOnlyButton|  
  	|**“文本”**|&Manager task|  
  	|**可见**|`False`|  
  
4.  在 Form1 的代码编辑器中，将以下代码添加到 `Form1_Load` 方法的末尾。  
  
     此代码会调用将在下一步中添加的 `DisplayButtonForManagerRole` 方法。  
  
     [!code-csharp[ClientApplicationServices#012](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Form1.cs#012)]  [!code-vb[ClientApplicationServices#012](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Form1.vb#012)]  
  
5.  将以下方法添加到 Form1 类的末尾。  
  
     此方法会调用 `static` <xref:System.Threading.Thread.CurrentPrincipal%2A?displayProperty=fullName> 属性返回的 <xref:System.Security.Principal.IPrincipal> 的 <xref:System.Security.Principal.IPrincipal.IsInRole%2A> 方法。 对于配置为使用客户端应用程序服务的应用程序，此属性会返回 <xref:System.Web.ClientServices.ClientRolePrincipal>。 因为此类实现 <xref:System.Security.Principal.IPrincipal> 接口，所以无需显式引用它。  
  
     如果用户采用“manager”角色，则 `DisplayButtonForManagerRole` 方法会将 <xref:System.Windows.Forms.Control.Visible%2A> 的 `managerOnlyButton` 属性设置为 `true`。 如果引发了 <xref:System.Net.WebException> （它表示角色服务不可用），则此方法还会显示一条错误消息。  
  
    > [!NOTE]
    >  如果用户登录名已过期，则 <xref:System.Web.ClientServices.ClientRolePrincipal.IsInRole%2A> 方法会始终返回 `false` 。 如果应用程序在身份验证之后很快调用 <xref:System.Security.Principal.IPrincipal.IsInRole%2A> 方法一次（在本演练的代码示例中所示），则不会发生这种情况。 如果应用程序必须在其他时间检索用户角色，则可能要添加代码以重新验证登录名已过期的用户。 如果所有有效用户都分配给角色，则可以通过调用 <xref:System.Web.ClientServices.Providers.ClientRoleProvider.GetRolesForUser%2A?displayProperty=fullName> 方法来确定登录名是否已过期。 如果不返回任何角色，则登录名已过期。 有关此功能的示例，请参阅 <xref:System.Web.ClientServices.Providers.ClientRoleProvider.GetRolesForUser%2A> 方法。 仅当在应用程序配置中选择了 **“每次服务器 Cookie 到期时要求用户重新登录”** 时，此功能才是必需的。 有关更多信息，请参见 [How to: Configure Client Application Services](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md)。  
  
     [!code-csharp[ClientApplicationServices#030](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Form1.cs#030)]  [!code-vb[ClientApplicationServices#030](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Form1.vb#030)]  
  
 如果身份验证成功，则客户端身份验证提供程序会将 <xref:System.Threading.Thread.CurrentPrincipal%2A?displayProperty=fullName> 属性设置为 <xref:System.Web.ClientServices.ClientRolePrincipal> 类的实例。 此类实现 <xref:System.Security.Principal.IPrincipal.IsInRole%2A> 方法，以便将工作委托给配置的角色提供程序。 如前面一样，应用程序无需直接引用服务提供程序。  
  
 现在可以运行应用程序，并以 employee 身份登录以看到按钮不会出现，然后以 manager 身份登录以看到按钮。  
  
## <a name="accessing-web-settings"></a>访问 Web 设置  
 在下面的过程中，会将一个文本框添加到窗体，然后将它绑定到 Web 设置。 与前面使用身份验证和角色的代码一样，设置代码不直接访问设置提供程序。 而是使用由 `Settings` 为项目生成的强类型 `Properties.Settings.Default` 类（在 C# 中作为 `My.Settings` 并在 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]中作为 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]来访问）。  
  
#### <a name="to-use-web-settings-in-your-user-interface"></a>在用户界面中使用 Web 设置  
  
1.  通过检查任务栏的通知区域来确保 **“ASP.NET Web Development Server”** 仍在运行。 如果已停止了该服务器，请重新启动应用程序（这会自动启动服务器），然后关闭登录对话框。  
  
2.  在 **“解决方案资源管理器”**中，选择 ClientAppServicesDemo 项目，然后在 **“项目”** 菜单上，选择 **“ClientAppServicesDemo 属性”**。  
  
     项目设计器随即出现。  
  
3.  在 **“设置”** 选项卡上，单击 **“加载 Web 设置”**。  
  
     **“登录”** 对话框随即出现。  
  
4.  输入 employee 或 manager 的凭据，然后单击 **“登录”**。 将使用的 Web 设置配置为仅供经过身份验证的用户访问，因此单击 **“跳过登录”** 不会加载任何设置。  
  
     `WebSettingsTestText` 设置随即出现在设计器中，具有默认值 `DefaultText`。 此外，会为项目生成包含 `WebSettingsTestText` 属性的 `Settings` 类。  
  
5.  在“解决方案资源管理器”的 ClientAppServicesDemo 项目中，选择 Form1，然后从 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 主菜单中选择“视图”|“设计器”。  
  
6.  在设计器中，向窗体添加一个 <xref:System.Windows.Forms.TextBox> 控件。  
  
7.  在 **“属性”** 窗口中，将 **“(名称)”** 值指定为 `webSettingsTestTextBox`。  
  
8.  在代码编辑器中，将以下代码添加到 `Form1_Load` 方法末尾：  
  
     此代码会调用将在下一步中添加的 `BindWebSettingsTestTextBox` 方法。  
  
     [!code-csharp[ClientApplicationServices#013](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Form1.cs#013)]  [!code-vb[ClientApplicationServices#013](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Form1.vb#013)]  
  
9. 将以下方法添加到 Form1 类的末尾。  
  
     此方法将 <xref:System.Windows.Forms.TextBox.Text%2A> 的 `webSettingsTestTextBox` 属性绑定到此过程前面生成的 `WebSettingsTestText` 类的 `Settings` 属性。 如果引发了 <xref:System.Net.WebException>（它表示 Web 设置服务不可用），则此方法还会显示一条错误消息。  
  
     [!code-csharp[ClientApplicationServices#040](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Form1.cs#040)]   [!code-vb[ClientApplicationServices#040](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Form1.vb#040)]  
  
    > [!NOTE]
    >  通常会使用数据绑定在控件与 Web 设置之间实现自动双向通信。 但是，还可以直接访问 Web 设置，如下面的示例所示：  
  
     [!code-csharp[ClientApplicationServices#322](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Class1.cs#322)]   [!code-vb[ClientApplicationServices#322](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Class1.vb#322)]  
  
10. 在设计器中，选择窗体，然后在 **“属性”** 窗口中，单击 **“事件”** 按钮。  
  
11. 选择 <xref:System.Windows.Forms.Form.FormClosing> 事件，然后按 Enter 以生成事件处理程序。  
  
12. 将生成的方法替换为以下代码。  
  
     <xref:System.Windows.Forms.Form.FormClosing> 事件处理程序会调用 `SaveSettings` 方法，将在下一部分中添加的注销功能也使用该方法。 `SaveSettings` 方法首先确认用户尚未注销。 可通过当前主体返回的 <xref:System.Security.Principal.IIdentity.AuthenticationType%2A> 的 <xref:System.Security.Principal.IIdentity> 属性来实现此目的。 可通过 `static` <xref:System.Threading.Thread.CurrentPrincipal%2A> 属性检索当前主体。 如果用户针对客户端应用程序服务进行了身份验证，则身份验证类型将是“ClientForms”。 `SaveSettings` 方法不能只检查 <xref:System.Security.Principal.IIdentity.IsAuthenticated%2A?displayProperty=fullName> 属性，因为用户在注销之后可能具有有效的 Windows 标识。  
  
     如果用户尚未注销，则 `SaveSettings` 方法调用在此过程前面生成的 <xref:System.Configuration.ApplicationSettingsBase.Save%2A> 类的 `Settings` 方法。 如果身份验证 Cookie 已过期，则此方法可能会引发 <xref:System.Net.WebException> 。 仅当在应用程序配置中选择了 **“每次服务器 Cookie 到期时要求用户重新登录”** 时，才会发生这种情况。 有关更多信息，请参见 [How to: Configure Client Application Services](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md)。 `SaveSettings` 方法通过调用 <xref:System.Web.Security.Membership.ValidateUser%2A> 以显示登录对话框，来处理 Cookie 过期。 如果用户成功登录，则 `SaveSettings` 方法尝试通过调用自身来再次保存设置。  
  
     与前面的代码一样，如果远程服务不可用，则 `SaveSettings` 方法会显示一条错误消息。 如果设置提供程序无法访问远程服务，则设置仍会保存到本地缓存，并在应用程序重新启动时重载。  
  
     [!code-csharp[ClientApplicationServices#050](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Form1.cs#050)]  [!code-vb[ClientApplicationServices#050](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Form1.vb#050)]  
  
13. 将以下方法添加到 Form1 类的末尾。  
  
     此代码处理 <xref:System.Web.ClientServices.Providers.ClientSettingsProvider.SettingsSaved?displayProperty=fullName> 事件，并在任何设置无法保存时显示警告。 如果设置服务不可用，或者如果身份验证 Cookie 已过期，则 <xref:System.Web.ClientServices.Providers.ClientSettingsProvider.SettingsSaved> 事件不会发生。 <xref:System.Web.ClientServices.Providers.ClientSettingsProvider.SettingsSaved> 事件会发生的一个示例是如果用户已注销。 可以通过直接在 `SaveSettings` 方法调用之前向 <xref:System.Configuration.ApplicationSettingsBase.Save%2A> 方法添加注销代码，来测试此事件处理程序。 可以使用的注销代码在下一部分中进行介绍。  
  
     [!code-csharp[ClientApplicationServices#090](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Form1.cs#090)]  [!code-vb[ClientApplicationServices#090](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Form1.vb#090)]  
  
14. 对于 C#，在 `Form1_Load` 方法的末尾添加以下代码。 此代码将上一步中添加的方法与 <xref:System.Web.ClientServices.Providers.ClientSettingsProvider.SettingsSaved> 事件相关联。  
  
     [!code-csharp[ClientApplicationServices#015](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Form1.cs#015)]  
  
 此时若要测试应用程序，请以 employee 和 manager 身份多次运行它，并在文本框中输入不同的值。 值会针对每个用户在会话之间保持。  
  
## <a name="implementing-logout"></a>实现注销  
 当用户在登录时选中 **“记住我”** 复选框时，应用程序会在后续运行中自动对用户进行身份验证。 应用程序处于脱机模式时，或在身份验证 Cookie 过期之前，自动身份验证随后会继续进行。 但是，有时多个用户需要访问应用程序，或单个用户偶尔可能会使用不同的凭据登录。 若要实现此方案，必须实现注销功能，如下面的过程中所述。  
  
#### <a name="to-implement-logout-functionality"></a>实现注销功能  
  
1.  在 Form1 设计器中，从“工具箱”向窗体添加一个 <xref:System.Windows.Forms.Button> 控件。  
  
2.  在“属性”窗口中，将“(Name)”值指定为 `logoutButton`，将“Text”值指定为“&Log Out”。  
  
3.  双击 `logoutButton` 以生成 <xref:System.Windows.Forms.Control.Click> 事件处理程序。  
  
     代码编辑器随即出现，光标位于 `logoutButton_Click` 方法中。  
  
4.  将生成的 `logoutButton_Click` 方法替换为以下代码。  
  
     此事件处理程序首先调用在上一部分中添加的 `SaveSettings` 方法。 随后，事件处理程序会调用 <xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationMembershipProvider.Logout%2A?displayProperty=fullName> 方法。 如果身份验证服务不可用，则 <xref:System.Web.ClientServices.Providers.ClientFormsAuthenticationMembershipProvider.Logout%2A> 方法会引发 <xref:System.Net.WebException>。 在这种情况下， `logoutButton_Click` 方法会显示一条警告消息，并暂时切换为脱机模式以使用户注销。 下一部分中介绍了脱机模式。  
  
     注销会删除本地身份验证 Cookie，以便在应用程序重新启动时要求提供登录名。 注销之后，事件处理程序会重新启动应用程序。 应用程序重新启动时，它会显示一条欢迎消息，后跟登录对话框。 欢迎消息可清楚地表明应用程序已重新启动。 如果用户必须登录才能保存设置，并且随后因为应用程序重新启用而必须再次登录序，这样可防止可能的混淆。  
  
     [!code-csharp[ClientApplicationServices#070](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Form1.cs#070)]  [!code-vb[ClientApplicationServices#070](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Form1.vb#070)]  
  
 若要测试注销功能，请运行应用程序，然后在登录对话框中选择 **“记住我”** 。 接下来，关闭并重新启动应用程序，以确认不必再登录。 最后，通过单击“注销”来重新启动应用程序。  
  
## <a name="enabling-offline-mode"></a>启用脱机模式  
 在下面的过程中，会向窗体添加一个复选框，以使用户可以进入脱机模式。 应用程序通过将 `static` <xref:System.Web.ClientServices.ConnectivityStatus.IsOffline%2A?displayProperty=fullName> 属性设置为 `true`来指示脱机模式。 脱机状态存储在本地硬盘上由 <xref:System.Windows.Forms.Application.UserAppDataPath%2A?displayProperty=fullName> 属性指示的位置处。 这意味着会针对每个用户、每个应用程序来存储脱机状态。  
  
 在脱机模式下，所有客户端应用程序服务请求都从本地缓存检索数据而不是尝试访问服务。 在默认配置中，本地数据包括用户密码的加密形式。 这使用户可以应用程序处于脱机模式时登录。 有关更多信息，请参见 [How to: Configure Client Application Services](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md)。  
  
#### <a name="to-enable-offline-mode-in-your-application"></a>在应用程序中启用脱机模式  
  
1.  在“解决方案资源管理器”的 ClientAppServicesDemo 项目中，选择 Form1，然后从 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 主菜单中选择“视图”|“设计器”。  
  
2.  在设计器中，向窗体添加一个 <xref:System.Windows.Forms.CheckBox> 控件。  
  
3.  在“属性”窗口中，将“(Name)”值指定为 `workOfflineCheckBox`，将“Text”值指定为“&Work offline”。  
  
4.  在 **“属性”** 窗口中，单击 **“事件”** 按钮。  
  
5.  选择 <xref:System.Windows.Forms.CheckBox.CheckedChanged> 事件，然后按 Enter 以生成事件处理程序。  
  
6.  将生成的方法替换为以下代码。  
  
     此代码会更新 <xref:System.Web.ClientServices.ConnectivityStatus.IsOffline%2A> 值，并在他们返回联机模式时以静默方式重新验证用户。 <xref:System.Web.ClientServices.ClientFormsIdentity.RevalidateUser%2A?displayProperty=fullName> 方法使用缓存的凭据，以便用户不必显式登录。 如果身份验证服务不可用，则会出现警告消息，应用程序会保持脱机状态。  
  
    > [!NOTE]
    >  <xref:System.Web.ClientServices.ClientFormsIdentity.RevalidateUser%2A> 方法只是为了方便。 因为它没有返回值，所以无法指示重新验证是否失败。 例如，如果在服务器上更改了用户凭据，则重新验证可能会失败。 在这种情况下，你可能要包含在服务调用失败之后显式验证用户的代码。 有关详细信息，请参阅本演练前面的“访问 Web 设置”部分。  
  
     重新验证之后，此代码会将任何更改都保存到本地 Web 设置，具体方法是调用以前添加的 `SaveSettings` 方法。 它随后通过调用项目的 `Settings` 类的 <xref:System.Configuration.ApplicationSettingsBase.Reload%2A> 方法（在 C# 中作为 `Properties.Settings.Default` 并且在 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 中作为 `My.Settings` 来访问），来检索服务器上的任何新值。  
  
     [!code-csharp[ClientApplicationServices#080](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Form1.cs#080)]  [!code-vb[ClientApplicationServices#080](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Form1.vb#080)]  
  
7.  将以下代码添加到 `Form1_Load` 方法的末尾，以确保复选框显示当前连接状态。  
  
     [!code-csharp[ClientApplicationServices#014](../../../samples/snippets/csharp/VS_Snippets_Winforms/ClientApplicationServices/CS/Form1.cs#014)]  [!code-vb[ClientApplicationServices#014](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ClientApplicationServices/VB/Form1.vb#014)]  
  
 这样便完成了示例应用程序。 若要测试脱机功能，请运行应用程序，以 employee 或 manager 身份登录，然后选择 **“脱机工作”**。 修改文本框中的值，然后关闭应用程序。 重新启动应用程序。 登录之前，请在任务栏的通知区域中右键单击“ASP.NET 开发服务器”图标，然后单击 **“停止”**。 随后照常登录。 即使服务器未运行时，仍可以登录。 修改文本框值，退出，然后重新启动以查看修改后的值。  
  
## <a name="summary"></a>摘要  
 在本演练中，学习了如何在 Windows 窗体应用程序中启用并使用客户端应用程序服务。 设置测试服务器之后，向应用程序添加了代码以对用户进行身份验证，并从服务器检索用户角色和应用程序设置。 还学习了如何启用脱机模式，以便应用程序在连接不可用时使用本地数据缓存而不是远程服务。  
  
## <a name="next-steps"></a>后续步骤  
 在实际应用程序中，你会从可能并不始终可用，或可能在不进行通知的情况下停机的远程服务器访问许多用户的数据。 若要使应用程序可靠，必须正确响应服务不可用的情况。 本演练包含 try/catch 块来捕获 <xref:System.Net.WebException> ，并在服务不可用时显示一条错误消息。 在生产代码中，可能要通过切换为脱机模式、退出应用程序或拒绝对特定功能的访问来处理这种情况。  
  
 若要提高应用程序的安全性，请确保在部署之前全面测试应用程序和服务器。  
  
## <a name="see-also"></a>另请参阅  
 [客户端应用程序服务](../../../docs/framework/common-client-technologies/client-application-services.md)   
 [客户端应用程序服务概述](../../../docs/framework/common-client-technologies/client-application-services-overview.md)   
 [如何：配置客户端应用程序服务](../../../docs/framework/common-client-technologies/how-to-configure-client-application-services.md)   
 [ASP.NET Web Site Administration Tool](http://msdn.microsoft.com/library/100ddd8b-7d11-4df9-91ef-0bbbe92e5aec)   
 [为 SQL Server 创建和配置应用程序服务数据库](http://msdn.microsoft.com/library/ab894e83-7e2f-4af8-a116-b1bff8f815b2)   
 [演练：使用 ASP.NET 应用程序服务](http://msdn.microsoft.com/library/f3f394f0-20d6-4361-aa8f-4b21bf4933eb)

