---
title: "使用 .NET Framework 针对多个平台开发 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: b153baaa-130c-4169-860b-e580591de91e
caps.latest.revision: 13
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 13
---
# 使用 .NET Framework 针对多个平台开发
可以通过使用 .NET Framework 和 Visual Studio 开发 Microsoft 和非 Microsoft 平台上的应用。  
  
## 跨平台开发的选项  
 若要针对多个平台进行开发，你可以共享源代码或二进制文件，并可以在 .NET Framework 代码和 Windows 运行时 API 之间进行调用。  
  
|若希望...|使用...|  
|------------|-----------|  
|在 Windows Phone 8.1 和 Windows 8.1 应用之间共享源代码|**共享的项目**（Visual Studio 2013 Update 2 中的通用应用模板）。<br /><br /> -   当前不支持 Visual Basic。<br />-   通过使用 \#`if` 语句，你可以分隔平台特定的代码。<br /><br /> 有关详细信息，请参见：<br /><br /> -   [通过使用 Visual Studio 构建面向 Windows 和 Windows Phone 的应用](http://msdn.microsoft.com/library/windows/apps/dn609832.aspx)（MSDN 文章）<br />-   [使用 Visual Studio 来构建通用 XAML 应用](http://blogs.msdn.com/b/visualstudio/archive/2014/04/14/using-visual-studio-to-build-universal-xaml-apps.aspx)（博客文章）<br />-   [使用 Visual Studio 来构建 XAML 融合应用](http://channel9.msdn.com/Events/Build/2014/3-591)（视频）|  
|在面向不同平台的应用之间共享二进制文件|平台不可知的代码的**可移植类库项目**。<br /><br /> -   此方法通常用于实现业务逻辑的代码。<br />-   你可以使用 Visual Basic 或 C\#。<br />-   API 支持因平台而异。<br />-   针对 Windows 8.1 和 Windows Phone 8.1 的可移植类库项目支持 Windows 运行时 API 和 XAML。  这些功能在较旧版本的可移植类库中不可用。<br />-   如果需要，可以通过使用接口或抽象类抽象处理平台特定的代码。<br /><br /> 有关详细信息，请参见：<br /><br /> -   [可移植类库](../../../docs/standard/cross-platform/cross-platform-development-with-the-portable-class-library.md)（MSDN 文章）<br />-   [如何使可移植类库为你工作](http://blogs.msdn.com/b/dsplaisted/archive/2012/08/27/how-to-make-portable-class-libraries-work-for-you.aspx)（博客文章）<br />-   [将可移植类库与 MVVM 配合使用](../../../docs/standard/cross-platform/using-portable-class-library-with-model-view-view-model.md)（MSDN 文章）<br />-   [面向多个平台的库的应用程序资源](../../../docs/standard/cross-platform/app-resources-for-libraries-that-target-multiple-platforms.md)（MSDN 文章）<br />-   [.NET 可移植性分析器](http://visualstudiogallery.msdn.microsoft.com/1177943e-cfb7-4822-a8a6-e56c7905292b)（Visual Studio 扩展）|  
|在平台（Windows8.1 和 Windows Phone 8.1 除外）的应用之间共享源代码|**添加为链接**功能。<br /><br /> -   这种方法适用于应用逻辑，其对这两种应用均常见，但出于某些原因不可移植。  你可以将此功能用于 C＃ 或 Visual Basic 代码。<br />     例如，Windows Phone 8 和 Windows 8 共享 Windows 运行时 API，但可移植类库不支持这些平台的 Windows 运行时。  你可以使用 `Add as link` 在 Windows Phone 8 应用和面向 Windows 8 的 Windows 应用商店应用之间共享公共 Windows 运行时代码。<br /><br /> 有关详细信息，请参见：<br /><br /> -   [使用“添加为链接”共享代码](http://msdn.microsoft.com/library/windowsphone/develop/jj714082\(v=vs.105\).aspx)（MSDN 文章）<br />-   [如何：将现有项添加到项目中](http://msdn.microsoft.com/library/vstudio/9f4t9t92\(v=vs.100\).aspx)（MSDN 文章）|  
|使用 .NET Framework 代码或从 NET Framework 代码调用 Windows 运行时 API，编写 Windows 应用商店应用|从 .NET Framework C\# 或 Visual Basic 代码调用 **Windows 运行时 API**，并使用 .NET Framework 框架来创建 Windows 应用商店应用。  你应该注意这两个平台的 API 差异。  但是，存在帮助你处理这些差异的类。<br /><br /> 有关详细信息，请参见：<br /><br /> -   [.NET Framework 对 Windows 应用商店应用程序和 Windows 运行时的支持情况](../../../docs/standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md)（MSDN 文章）<br />-   [向 Windows 运行时传递 URI](../../../docs/standard/cross-platform/passing-a-uri-to-the-windows-runtime.md)（MSDN 文章）<br />-   <xref:System.IO.WindowsRuntimeStreamExtensions>（MSDN API 引用页）<br />-   <xref:System.WindowsRuntimeSystemExtensions>（MSDN API 引用页）|  
|构建面向非 Microsoft 平台的 .NET Framework 应用|.NET Framework 中的**可移植类库参考程序集**，以及 Visual Studio 扩展或第三方工具（如 Xamarin）。<br /><br /> 有关详细信息，请参见：<br /><br /> -   [可移植类库现在在所有平台上可用。](http://blogs.msdn.com/b/dotnet/archive/2013/10/14/portable-class-library-pcl-now-available-on-all-platforms.aspx)（博客文章）<br />-   [Xamarin](http://xamarin.com/visual-studio)（Xamarin 网站）|  
|将 JavaScript 和 HTML 用于跨平台开发|使用 Visual Studio 2013 Update 2 中的**通用应用模板**，针对面向 Windows 8.1 和 Windows Phone 8.1 的 Windows 运行时 API 进行开发。  当前，你不能将 .NET Framework API 与 JavaScript 和 HTML 结合使用来开发跨平台应用。<br /><br /> 有关详细信息，请参见：<br /><br /> -   [JavaScript 项目模板](http://msdn.microsoft.com/library/windows/apps/hh758331.aspx)<br />-   [使用 JavaScript 将 Windows 运行时应用移植到 Windows Phone](http://msdn.microsoft.com/library/windows/apps/dn636144.aspx)|