---
title: "WCF 服务发布 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c806b253-cd47-4b96-b831-e73cbf08808f
caps.latest.revision: 22
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# WCF 服务发布
从基于 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务主机和 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 测试客户端提供的早期开发环境进行处理，到实际将应用程序部署到生产环境中以进行测试，[!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 服务发布都对您有所帮助。  在提交最终部署计划之前，可以使用 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 服务发布来验证您的 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务是否正常运行以及是否可以发布。  也可以选择将 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务库部署到多个不同的目标位置，以进行测试。  
  
## 支持的服务和目标位置  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务发布支持发布基于 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务库模板集及其对应的项模板创建的 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务。这些模板包括：  
  
-   带有项模板的 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务库模板。  
  
-   带有项模板的顺序工作流服务库模板。  
  
-   带有项模板的状态机工作流服务库模板。  
  
-   联合服务库。  
  
 可以通过以下方法找到这些服务模板：选择“文件”\-\>“新建项目”\-\>“Visual Basic”或“Visual C\#”\-\>“WCF”。  
  
 可以将服务发布到以下目标位置。  
  
-   本地 IIS。  
  
-   文件系统。  
  
-   FTP 站点。  
  
-   远程站点。  
  
## 使用 WCF 服务发布  
 若要部署服务实现，请执行以下步骤：  
  
1.  使用提升的特权打开 Visual Studio（即，右击可执行文件并使用“以管理员身份运行”来启动它）。  如果使用的是 IIS 7.0 或更高版本，请确保已使用“控制面板”中的“打开或关闭 Windows 功能”安装“IIS 元数据库和 IIS 6 配置兼容性”组件。  
  
2.  打开服务项目，从主菜单中选择“生成”\-\>“发布 \<项目名称\>”，或者在“解决方案资源管理器”中右击该项目，然后单击“发布”。  
  
3.  将出现**“发布”**窗口。  单击**“…”**。  按钮指定服务应部署到的目标位置。  可以选择将应用程序部署到本地 IIS、文件系统、FTP 站点或远程站点。  如果将应用程序部署到本地 IIS，则可选择您的网站，并通过单击右上角的**“创建新 Web 应用程序”**图标在该网站下创建 Web 应用程序。  
  
4.  单击主窗口中的**“发布”**后，Visual Studio 会将此应用程序部署到指定的目标位置，并将 Web.config、.svc 和程序集文件复制到目标目录。  .  .svc 的名称将为“ProjectName.ServiceName.svc”。  在成功发布服务后，可在“Visual Studio 输出”窗口中找到一个热链接，该链接的外观类似于“正在连接到 http:\/\/localhost\/WebApplicationFolderName ...”。  可在按住 Ctrl 键的同时单击该链接来打开 Visual Studio 中的浏览器页面，以便查看服务目录结构。  
  
     如果您无法浏览到网站，这可能是因为 IIS 中未启用目录浏览器。  请按照“可尝试的操作”一节中的提示执行操作来启用目录浏览器。  或者，您可以直接键入“http:\/\/localhost\/WebApplicationFolderName\/ProjectName.ServiceName.svc”来查看服务页面。  
  
 可以使用**“发布”**来指定是否要将项目中定义的所有服务的程序集、配置和 .svc 文件复制到目标位置，并覆盖位于目标位置的现有文件。  
  
 如果选择将应用程序部署到本地 IIS，则可能会遇到与 IIS 设置有关的错误。  请确保已正确安装 IIS。  可在浏览器中键入“http:\/\/localhost”并检查是否显示了 IIS 默认页面。  在某些情况下，此类问题也可能由于 IIS 中的 ASP.NET 或 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 注册不正确导致的。  可打开 Visual Studio 命令提示并运行命令“aspnet\_regiis.exe \-ir”来解决 ASP.NET 注册问题，或运行命令“ServiceModelReg.exe –ia”来解决 WCF 注册问题。  
  
## 生成的待发布文件  
 在 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务库可以由 Web 承载之前，该工具生成以下文件：程序集文件、Web.config 文件和 .svc 文件。  这些文件全部复制到目标位置。  然后发布该服务。  
  
### 程序集文件  
 使用此工具发布 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务时，首先自动生成该服务，生成完毕后将在服务项目中生成程序集文件。  
  
### .SVC 文件  
 发布操作为每个 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务生成一个 \*.svc 文件（无论该文件存在与否），以确保版本有效性。  有两种不同的 svc 文件：一种针对 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务库和联合服务库，另一种针对顺序和状态机工作流服务库。  生成的 \*.svc 文件复制到目标位置的根文件夹中。  
  
### Web.config 文件  
 每次将服务项目发布到特定目标位置时，都会创建一个 Web.config 文件。  
  
 生成的 Web.config 文件包括一些对 Web 承载有用的 Web 节，以及 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务库的 App.config 的内容，其中包含以下更改：  
  
-   排除了基址。  
  
-   排除了 `<diagnostics>` 元素中的设置以保留目标平台的跟踪设置。  
  
## 将具有非 HTTP 绑定的 WCF 服务发布到 IIS  
 如果使用的是 IIS 7.0 或更高版本，则可使用非 HTTP 绑定将 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务发布到 IIS。  需要进行一些预配置。  有关更多信息，请参见 [在 Windows 进程激活服务中承载](../../../docs/framework/wcf/feature-details/hosting-in-windows-process-activation-service.md)中的主题。  
  
## 安全性  
 发布到本地 IIS 需要具有管理员权限，原因是 IIS 要求以 Administrator 帐户身份运行。  如果打开 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务发布的用户不具有管理员权限，则 IIS 将不可用作目标位置。  发布到文件系统、FTP 站点或远程站点不需要具有管理员权限。  
  
## 请参阅  
 [WCF Visual Studio 模板](../../../docs/framework/wcf/wcf-vs-templates.md)   
 [WCF 服务主机 \(WcfSvcHost.exe\)](../../../docs/framework/wcf/wcf-service-host-wcfsvchost-exe.md)   
 [WCF 测试客户端 \(WcfTestClient.exe\)](../../../docs/framework/wcf/wcf-test-client-wcftestclient-exe.md)