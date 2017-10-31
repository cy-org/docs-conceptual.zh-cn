---
title: "应用程序启动时间 | Microsoft Docs"
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
  - "应用程序启动 [WPF]"
  - "性能 [WPF], 启动时间"
  - "初始屏幕 [WPF], 启动时间"
  - "启动时间 [WPF]"
  - "WPF, 启动时间"
ms.assetid: f0ec58d8-626f-4d8a-9873-c20f95e08b96
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 应用程序启动时间
启动 WPF 应用程序所需的时间可能会有很大不同。  本主题介绍缩短 Windows Presentation Foundation \(WPF\) 应用程序的感觉启动时间和实际启动时间的各种技巧。  
  
## 了解冷启动和热启动  
 在以下情况下会发生冷启动：系统重新启动后首次启动应用程序；或者启动应用程序后将其关闭，然后经过一段较长时间之后再次启动它。  当应用程序启动时，如果所需的页面（代码、静态数据、注册表等）没有出现在 Windows 内存管理器的备用列表中，则会发生页面错误。  将页面调入内存需要访问磁盘。  
  
 在以下情况下会发生热启动：主公共语言运行时 \(CLR\) 组件的大多数页面已加载到内存中，从而节省了大量的磁盘访问时间。  这就是托管应用程序在第二次运行时，启动速度更快的原因。  
  
## 实现初始屏幕  
 当启动应用程序到显示第一个 UI 之间存在不可避免的明显延迟时，使用初始屏幕可优化感觉启动时间。  此方法在用户启动应用程序后会，立即显示一个图像。  当应用程序准备好显示它的第一个 UI 时，初始屏幕逐渐消失。  从 [!INCLUDE[net_v35SP1_short](../../../../includes/net-v35sp1-short-md.md)] 开始，可以使用 <xref:System.Windows.SplashScreen> 类来实现初始屏幕。  有关更多信息，请参见[将初始屏幕添加到 WPF 应用程序](../../../../docs/framework/wpf/app-development/how-to-add-a-splash-screen-to-a-wpf-application.md)。  
  
 您也可以使用本机 Win32 图形来实现自己的初始屏幕。  您的实现将在调用 <xref:System.Windows.Application.Run%2A> 方法之前显示。  
  
## 分析启动代码  
 确定冷启动慢的原因。  磁盘 I\/O 可能是一个原因，但并非总是它。  通常，应该将外部资源（例如网络、Web 服务或磁盘）的使用降到最低。  
  
 在测试之前，验证没有其他正在运行的应用程序或服务使用托管代码或 WPF 代码。  
  
 重新启动后立即启动 WPF 应用程序，并确定显示所需的时间。  如果应用程序的所有后续启动（热启动）速度更快，则冷启动问题很可能是由 I\/O 引起的。  
  
 如果应用程序的冷启动问题与 I\/O 无关，则可能是应用程序执行了某些冗长的初始化或计算，等待某些事件完成，或者在启动时需要大量的 JIT 编译。  后面几节更详细地介绍了其中一些情况。  
  
## 优化模块加载  
 使用进程资源管理器 \(Procexp.exe\) 和 Tlist.exe 等工具可确定应用程序需加载哪些模块。  `Tlist <pid>` 命令显示进程加载的所有模块。  
  
 例如，如果您没有连接到 Web 但看到加载了 System.Web.dll，则应用程序中存在引用此程序集的模块。  请检查以确保该引用是必需的。  
  
 如果应用程序有多个模块，请将它们合并为一个。  此方法需要的 CLR 程序集加载开销更少。  程序集越少，还意味着 CLR 保持的状态也越少。  
  
## 推迟初始化操作  
 考虑将初始化代码操作推迟到呈现主应用程序窗口之后进行。  
  
 请注意，初始化可能会在类构造函数内部执行，如果初始化代码引用其他类，则可能会导致需执行多个类构造函数的级联效果。  
  
## 避免应用程序配置  
 考虑避免应用程序配置。  例如，如果应用程序具有简单的配置要求，且具有严格的启动时间目标，则注册表项或简单的 INI 文件可能是更快的启动选择。  
  
## 使用 GAC  
 如果全局程序集缓存 \(GAC\) 中没有安装程序集，则强命名程序集的哈希验证和 Ngen 映像验证（如果该程序集的本机映像在计算机上可用）将导致延迟。  对于安装在 GAC 中的所有程序集，将跳过强名称验证。  有关更多信息，请参见[Gacutil.exe（全局程序集缓存工具）](../../../../docs/framework/tools/gacutil-exe-gac-tool.md)。  
  
## 使用 NGen.exe  
 考虑对应用程序使用本机映像生成器 \(Ngen.exe\)。  由于 Ngen.exe 生成的本机映像可能比 MSIL 映像大，因此使用 Ngen.exe 意味着：需要占用 CPU 使用时间来获得更多的磁盘访问。  
  
 为了缩短热启动时间，应始终对应用程序使用 Ngen.exe，因为这样可避免对应用程序代码进行 JIT 编译的 CPU 开销。  
  
 在某些冷启动方案中，使用 Ngen.exe 也很有用。  这是因为不必加载 JIT 编译器 \(mscorjit.dll\)。  
  
 同时具有 Ngen 和 JIT 模块的效果最差。  这是因为必须加载 mscorjit.dll，当 JIT 编译器处理代码时，如果 JIT 编译器读取程序集的元数据，则必须访问 Ngen 映像中的众多页面。  
  
### Ngen 和 ClickOnce  
 计划的应用程序部署方式也会造成加载时间上有一些不同。  [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)] 应用程序部署不支持 Ngen。  如果决定将 Ngen.exe 用于应用程序，则必须使用另一种部署机制，如 Windows Installer。  
  
 有关更多信息，请参见[Ngen.exe（本机映像生成器）](../../../../docs/framework/tools/ngen-exe-native-image-generator.md)。  
  
### 重定基址和 DLL 地址冲突  
 如果使用 Ngen.exe，请注意，在内存中加载本机映像时将重定基址。  如果 DLL 未在其首选基址加载（因为相应的地址范围已经分配），则 Windows 加载程序将在另一个地址加载它，这是一个耗时的操作。  
  
 可以使用虚拟地址转储 \(Vadump.exe\) 工具进行检查，看是否存在所有页面都是私有页面的模块。  如果存在这种情况，则可能已将模块的基址重定为其他地址。  因此，无法共享其页面。  
  
 有关如何设置基址的更多信息，请参见[Ngen.exe（本机映像生成器）](../../../../docs/framework/tools/ngen-exe-native-image-generator.md)。  
  
## 优化 Authenticode  
 Authenticode 验证会增加启动时间。  Authenticode 签名的程序集必须通过证书颁发机构 \(CA\) 验证。  此验证很耗时，因为它要求多次连接到网络来下载当前证书吊销列表。  它还确保连接到受信任的根的路径上存在完整的有效证书链。  这会导致在加载程序集时出现几秒的延迟。  
  
 考虑在客户端计算机上安装 CA 证书，或者在可能的情况下避免使用 Authenticode。  如果您知道应用程序不需要发行者证据，则不必支付签名验证开销。  
  
 从 [!INCLUDE[net_v35_short](../../../../includes/net-v35-short-md.md)] 开始，提供了一个允许绕过 Authenticode 验证的配置选项。  为此，请在 app.exe.config 文件中添加以下设置：  
  
```  
<configuration>  
    <runtime>  
        <generatePublisherEvidence enabled="false"/>   
    </runtime>  
</configuration>  
```  
  
 有关更多信息，请参见 [\<generatePublisherEvidence\> 元素](../../../../docs/framework/configure-apps/file-schema/runtime/generatepublisherevidence-element.md)。  
  
## 比较 Windows Vista 上的性能  
 Windows Vista 中的内存管理器包含一种称为 SuperFetch 的技术。  SuperFetch 分析内存在一段时间中的使用模式，以确定适合具体用户的最佳内存内容。  SuperFetch 会持续工作以便始终保持该内容。  
  
 此方法与 Windows XP 中使用的预提取技术不同，预提取技术是将数据预先加载到内存中而不分析使用模式。  随着时间的推移，如果用户经常在 Windows Vista 上使用 WPF 应用程序，则可能会缩短应用程序的冷启动时间。  
  
## 高效使用 AppDomain  
 如有可能，将程序集加载到非特定于域的代码区域中，以确保在应用程序内创建的所有 AppDomain 中都使用本机映像（如果存在）。  
  
 为了获得最佳性能，应通过减少跨域调用来强制高效的跨域通信。  如有可能，使用不含参数或含有基元类型参数的调用。  
  
## 使用 NeutralResourcesLanguage 特性  
 使用 <xref:System.Resources.NeutralResourcesLanguageAttribute> 为 <xref:System.Resources.ResourceManager> 指定非特定区域性。  此方法避免了不成功的程序集查找。  
  
## 将 BinaryFormatter 类用于序列化  
 如果必须使用序列化，请使用 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 类，而不要使用 <xref:System.Xml.Serialization.XmlSerializer> 类。  <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> 类是在 mscorlib.dll 程序集的基类库 \(BCL\) 中实现的。  <xref:System.Xml.Serialization.XmlSerializer> 是在 System.Xml.dll 程序集中实现的，该程序集可能是要加载的其他 DLL。  
  
 如果必须使用 <xref:System.Xml.Serialization.XmlSerializer> 类，则预生成序列化程序集可以获得更好的性能。  
  
## 配置 ClickOnce 以在启动后检查更新  
 如果应用程序使用 [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)]，请通过配置 [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)] 以在应用程序启动后检查部署站点是否有更新，从而避免启动时进行网络访问。  
  
 如果使用 XAML 浏览器应用程序 \(XBAP\) 模型，请记住，即使 XBAP 已在 [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)] 缓存中，[!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)] 也会检查部署站点是否有更新。  有关更多信息，请参见 [ClickOnce 安全和部署](../Topic/ClickOnce%20Security%20and%20Deployment.md)。  
  
## 将 PresentationFontCache 服务配置为自动启动  
 重新启动后运行的第一个 WPF 应用程序是 PresentationFontCache 服务。  该服务可以缓存系统字体，改进字体访问，以及改善整体性能。  启动该服务需要开销，在某些受控环境中，请考虑将该服务配置为在系统重新启动时自动启动。  
  
## 以编程方式设置数据绑定  
 不要使用 XAML 以声明方式设置主窗口的 <xref:System.Windows.FrameworkElement.DataContext%2A>，而应考虑以编程方式在 <xref:System.Windows.Application.OnActivated%2A> 方法中对其进行设置。  
  
## 请参阅  
 <xref:System.Windows.SplashScreen>   
 <xref:System.AppDomain>   
 <xref:System.Resources.NeutralResourcesLanguageAttribute>   
 <xref:System.Resources.ResourceManager>   
 [将初始屏幕添加到 WPF 应用程序](../../../../docs/framework/wpf/app-development/how-to-add-a-splash-screen-to-a-wpf-application.md)   
 [Ngen.exe（本机映像生成器）](../../../../docs/framework/tools/ngen-exe-native-image-generator.md)   
 [\<generatePublisherEvidence\> 元素](../../../../docs/framework/configure-apps/file-schema/runtime/generatepublisherevidence-element.md)