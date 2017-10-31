---
title: "WPF XAML 浏览器应用程序概述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "浏览器承载的应用程序 [WPF]"
  - "WPF XAML 浏览器应用程序 (XBAP)"
  - "XAML 浏览器应用程序 (XBAP)"
  - "XBAP, XAML 浏览器应用程序"
ms.assetid: 3a7a86a8-75d5-4898-96b9-73da151e5e16
caps.latest.revision: 47
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 47
---
# WPF XAML 浏览器应用程序概述
<a name="introduction"></a> [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)] 结合了 Web 应用程序和胖客户端应用程序二者的功能。  与 Web 应用程序类似，XBAP 可以部署到 Web 服务器且从 Internet Explorer 或 Firefox 启动。  与胖客户端应用程序类似，XBAP 可以利用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的功能。  开发 XBAP 也与开发胖客户端类似。  本主题简单概述 XBAP 开发，并介绍 XBAP 开发与标准胖客户端开发的不同之处。  
  
 本主题包含以下各节：  
  
-   [创建新的 XAML 浏览器应用程序 \(XBAP\)](#creating_a_new_xaml_browser_application_xbap)  
  
-   [部署 XBAP](#deploying_a_xbap)  
  
-   [与宿主网页通信](#communicating_with_the_host_web_page)  
  
-   [XBAP 安全注意事项](#xbap_security_considerations)  
  
-   [XBAP 启动时间性能注意事项](#xbap_start_time_performance_considerations)  
  
<a name="creating_a_new_xaml_browser_application_xbap"></a>   
## 创建新的 XAML 浏览器应用程序 \(XBAP\)  
 创建新的 XBAP 项目的最简单方法是使用 [!INCLUDE[vs_dev10_ext](../../../../includes/vs-dev10-ext-md.md)]。  创建新项目时，请从模板列表中选择**“WPF 浏览器应用程序”**。  有关更多信息，请参见[如何：创建新的 WPF 浏览器应用程序项目](http://msdn.microsoft.com/zh-cn/72ef4d90-e163-42a1-8df0-ea7ccfd1901f)。  
  
 运行 XBAP 项目时，它会在浏览器窗口中打开，而不是在单独的窗口中打开。  在 [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] 中调试 XBAP 时，该应用程序会使用 Internet 区域权限运行，因此，如果超出这些权限的范围，则会引发安全异常。  有关更多信息，请参见 [安全性](../../../../docs/framework/wpf/security-wpf.md)和 [WPF 部分信任安全](../../../../docs/framework/wpf/wpf-partial-trust-security.md)。  
  
> [!NOTE]
>  如果不是使用 [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] 开发的，或者想要了解有关项目文件的更多信息，请参见[生成 WPF 应用程序](../../../../docs/framework/wpf/app-development/building-a-wpf-application-wpf.md)。  
  
<a name="deploying_a_xbap"></a>   
## 部署 XBAP  
 生成 XBAP 时，输出包括以下三个文件：  
  
|文件|说明|  
|--------|--------|  
|可执行文件 \(.exe\)|该文件包含经过编译的代码，并具有 .exe 扩展名。|  
|应用程序清单 \(.manifest\)|它包含与应用程序关联的元数据，并具有 .manifest 扩展名。|  
|部署清单 \(.xbap\)|该文件包含 [!INCLUDE[TLA#tla_clickonce](../../../../includes/tlasharptla-clickonce-md.md)] 用来部署应用程序的信息，并具有 .xbap 扩展名。|  
  
 您将 XBAP 部署到 Web 服务器，例如 [!INCLUDE[TLA#tla_iis50](../../../../includes/tlasharptla-iis50-md.md)] 或更高版本。  您不必在 Web 服务器上安装 [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)]，但需要注册 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] [!INCLUDE[TLA#tla_mime](../../../../includes/tlasharptla-mime-md.md)] 类型和文件扩展名。  有关更多信息，请参见[配置 IIS 5.0 和 IIS 6.0 以部署 WPF 应用程序](../../../../docs/framework/wpf/app-development/how-to-configure-iis-5-0-and-iis-6-0-to-deploy-wpf-applications.md)。  
  
 为了准备好 XBAP 以便进行部署，请将 .exe 和关联的清单复制到 Web 服务器上。  创建包含超链接的 HTML 页以打开部署清单，即扩展名为 .xbap 的文件。  用户单击指向 .xbap 文件的链接时，[!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] 会自动处理应用程序的下载和启动机制。  下面的代码示例演示包含指向 XBAP 的超链接的 HTML 页。  
  
```  
<html>   
  <head></head>  
  <body>   
    <a href="XbapEx.xbap">Click this link to launch the application</a>  
  </body>   
</html>  
  
```  
  
 您还可以在网页框架中承载 XBAP。  创建具有一个或多个框架的网页。  将框架的源属性设置为部署清单文件。  如果希望使用内置机制在宿主网页和 XBAP 之间通信，则必须将应用程序承载到框架中。  下面的代码示例演示一个具有两个框架的 HTML 页，第二个框架的源设置为 XBAP。  
  
```  
<html>   
  <head>A page with frames.</head>  
    <frameset cols="50%,50%">   
      <frame src="introduction.htm" >   
      <frame src="XbapEx.xbap" >   
  </frameset>   
</html>  
```  
  
### 清除缓存的 XBAP  
 在某些情况下，重新生成并启动 XBAP 之后，您可能会发现打开了早期版本的 XBAP。  例如，如果 XBAP 程序集版本号是静态的，而您从命令行启动 XBAP，就会发生此行为。  在这种情况下，由于缓存的版本（以前启动的版本）和新版本的版本号相同，因此不会下载 XBAP 的新版本，  而会加载缓存的版本。  
  
 在这些情况下，您可以在命令提示符处使用 **Mage** 命令（该命令随 Visual Studio 或 [!INCLUDE[TLA2#tla_lhsdk](../../../../includes/tla2sharptla-lhsdk-md.md)] 一起安装）移除缓存的版本。  下面的命令可清除应用程序缓存。  
  
 `Mage.exe -cc`  
  
 此命令可保证启动最新版本的 XBAP。  在 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] 中调试应用程序时，应启动最新版本的 XBAP。一般来说，您应在每次生成时更新部署版本号。  有关 Mage 的更多信息，请参见 [Mage.exe（清单生成和编辑工具）](../../../../docs/framework/tools/mage-exe-manifest-generation-and-editing-tool.md)。  
  
<a name="communicating_with_the_host_web_page"></a>   
## 与宿主网页通信  
 应用程序承载到 HTML 框架中后，您可以与包含 XBAP 的网页通信。  可以通过检索 <xref:System.Windows.Interop.BrowserInteropHelper> 的 <xref:System.Windows.Interop.BrowserInteropHelper.HostScript%2A> 属性来完成此操作。  此属性会返回一个代表该 HTML 窗口的脚本对象。  然后，您可以使用常规的点语法访问 [window object](http://go.microsoft.com/fwlink/?LinkId=160274)（window 对象）的属性、方法和事件。  您还可以访问脚本方法和全局变量。  下面的示例演示如何检索脚本对象和关闭浏览器。  
  
 [!code-csharp[XbapBrowserInterop#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/xbapbrowserinterop/cs/page1.xaml.cs#10)]
 [!code-vb[XbapBrowserInterop#10](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/xbapbrowserinterop/vb/page1.xaml.vb#10)]  
  
### 调试使用 HostScript 的 XBAP  
 如果 XBAP 使用 <xref:System.Windows.Interop.BrowserInteropHelper.HostScript%2A> 对象与 HTML 窗口进行通信，则您必须指定两个设置以在 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] 中运行和调试应用程序。  应用程序必须有权访问其源站点，您必须使用包含 XBAP 的 HTML 页启动应用程序。  以下步骤介绍如何检查这两个设置：  
  
1.  在 Visual Studio 中打开项目属性。  
  
2.  在**“安全性”**选项卡上单击**“高级”**。  
  
     此时会显示“高级安全设置”对话框。  
  
3.  确保选中**“授予应用程序对其源站点的访问权”**复选框，然后单击**“确定”**。  
  
4.  在**“调试”**选项卡上，选择**“使用 URL 启动浏览器”**选项，然后指定包含 XBAP 的 HTML 页的 URL。  
  
5.  在 Internet Explorer 中，单击**“工具”**按钮，然后选择**“Internet 选项”**。  
  
     将出现“Internet 选项”对话框。  
  
6.  单击**“高级”**选项卡。  
  
7.  在**“安全性”**下的**“设置”**列表中，选中**“允许活动内容在我的计算机上的文件中运行”**复选框。  
  
8.  单击**“确定”**。  
  
     重新启动 Internet Explorer 之后，更改才会生效。  
  
> [!CAUTION]
>  如果在 Internet Explorer 中启用活动内容，则您的计算机会面临风险。  有关更多信息，请参见 [Internet Explorer 中的隐私和安全功能](http://go.microsoft.com/fwlink/?LinkId=179286)。  如果不希望更改 Internet Explorer 安全设置，则可以从服务器启动 HTML 页，然后将 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] 调试器附加到进程中。  
  
<a name="xbap_security_considerations"></a>   
## XBAP 安全注意事项  
 XBAP 通常在被限制到 Internet 区域权限集的部分信任的安全沙盒中执行。  因此，您的实现必须支持 Internet 区域中所支持的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 元素的子集，或者您必须提升应用程序的权限。  有关更多信息，请参见 [安全性](../../../../docs/framework/wpf/security-wpf.md)。  
  
 在应用程序中使用 <xref:System.Windows.Controls.WebBrowser> 控件时，WPF 会在内部实例化本机 WebBrowser ActiveX 控件。  如果应用程序是 Internet Explorer 中运行的部分信任的 XBAP，则该 ActiveX 控件会在 Internet Explorer 进程的专用线程中运行。  因此，存在以下限制：  
  
-   <xref:System.Windows.Controls.WebBrowser> 控件应提供与宿主浏览器相似的行为，包括安全限制。  可以通过 Internet Explorer 安全设置控制这些安全限制中的某些限制。  有关更多信息，请参见 [安全性](../../../../docs/framework/wpf/security-wpf.md)。  
  
-   如果在 HTML 页中跨域加载 XBAP，则会引发异常。  
  
-   输入位于与 WPF <xref:System.Windows.Controls.WebBrowser> 不同的线程上，因此无法截获键盘输入，不共享 IME 状态。  
  
-   由于 ActiveX 控件在另一个线程上运行，导航的计时或顺序可能有所不同。  例如，到某页的导航并不总是通过启动另一个导航请求来取消。  
  
-   由于 WPF 应用程序在另一个线程上运行，自定义 ActiveX 控件在通信时会出现问题。  
  
-   不会引发 <xref:System.Windows.Interop.HwndHost.MessageHook>，这是因为 <xref:System.Windows.Interop.HwndHost> 无法对另一个线程或进程中运行的窗口设置子类。  
  
### 创建完全信任的 XBAP  
 如果 XBAP 需要完全信任，则可以更改项目以启用此权限。  以下步骤介绍如何启用完全信任：  
  
1.  在 Visual Studio 中打开项目属性。  
  
2.  在**“安全性”**选项卡中，选择**“这是完全可信的应用程序”**选项。  
  
 此设置会进行下列更改：  
  
-   在项目文件中，`<TargetZone>` 元素值更改为 `Custom`。  
  
-   在应用程序清单 \(app.manifest\) 中，`Unrestricted="true"` 特性添加到 `PermissionSet` 元素中。  
  
    ```  
    <PermissionSet class="System.Security.PermissionSet"   
        version="1"   
        ID="Custom"   
        SameSite="site"   
        Unrestricted="true"   
    />  
    ```  
  
### 部署完全信任的 XBAP  
 部署不遵循 ClickOnce 受信任部署模型的完全信任的 XBAP 时，用户运行应用程序时的行为取决于安全区域。  在某些情况下，用户将在尝试安装它时收到警告。  用户可以选择继续或取消安装。  下表描述每个安全区域的应用程序的行为，以及您为了使应用程序接收完全信任而必须执行的操作。  
  
|安全区域|行为|获取完全信任|  
|----------|--------|------------|  
|本地计算机|自动完全信任|无需执行任何操作。|  
|Intranet 和可信站点|提示完全信任|使用证书对 XBAP 进行签名，以便用户在提示中看到源。|  
|Internet|失败，并显示“未授予信任”|使用证书对 XBAP 进行签名。|  
  
> [!NOTE]
>  上表中描述的行为针对的是不遵循 ClickOnce 受信任部署模型的完全信任的 XBAP。  
  
 建议您使用 ClickOnce 受信任部署模型来部署完全信任的 XBAP。  此模型允许您自动向 XBAP 授予完全信任（与安全区域无关），这样用户便不会收到提示。  作为此模型的一部分，您必须使用受信任发行者提供的证书来对应用程序进行签名。  有关更多信息，请参见[受信任的应用程序部署概述](../Topic/Trusted%20Application%20Deployment%20Overview.md)和 [Introduction to Code Signing](http://go.microsoft.com/fwlink/?LinkId=166327)（代码签名简介）。  
  
<a name="xbap_start_time_performance_considerations"></a>   
## XBAP 启动时间性能注意事项  
 衡量 XBAP 性能的一个重要方面是其启动时间。  如果 XBAP 是要加载的第一个 WPF 应用程序，“冷启动”时间可能为十秒钟或更长时间。  这是因为进度页是由 WPF 呈现的，而且必须冷启动 CLR 和 WPF 才能显示应用程序。  
  
 在 [!INCLUDE[net_v35SP1_short](../../../../includes/net-v35sp1-short-md.md)] 中启动时，通过在部署周期早期显示非托管进度页可以缩短 XBAP 的冷启动时间。应用程序启动后几乎可以立即显示进度页，因为它是由本机宿主代码显示并在 HTML 中呈现的。  
  
 此外，改进的 [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)] 下载序列并发最多可将启动时间缩短 10%。  当 [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)] 下载并验证了清单后，即启动应用程序下载，并开始更新进度栏。  
  
## 请参阅  
 [配置 Visual Studio 以调试 XAML 浏览器应用程序来调用 Web 服务](../../../../docs/framework/wpf/app-development/configure-vs-to-debug-a-xaml-browser-to-call-a-web-service.md)   
 [部署 WPF 应用程序](../../../../docs/framework/wpf/app-development/deploying-a-wpf-application-wpf.md)