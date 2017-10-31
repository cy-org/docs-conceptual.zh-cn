---
title: "面向多个平台的库的应用程序资源 | Microsoft Docs"
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
helpviewer_keywords: 
  - ".NET Framework, 面向多个平台时的资源"
  - "多个平台, 资源"
  - "资源 [.NET Framework]"
  - "资源, 对于多个平台"
  - "面向多个平台, 资源"
ms.assetid: 72c76f0b-7255-4576-9261-3587f949669c
caps.latest.revision: 20
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 20
---
# 面向多个平台的库的应用程序资源
可使用 .NET Framework [可移植类库](../../../docs/standard/cross-platform/cross-platform-development-with-the-portable-class-library.md)项目类型确保可从多个平台访问类库中的资源。  此项目类型适用于 [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)]，且面向 .NET Framework 类库的可移植子集。  使用[!INCLUDE[net_portable](../../../includes/net-portable-md.md)]确保可从桌面应用、Silverlight 应用、Windows Phone 应用和 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用访问你的库。  
  
 虽然[!INCLUDE[net_portable](../../../includes/net-portable-md.md)]项目仅使 <xref:System.Resources> 命名空间中的极少数类型对你的应用程序可用，但它允许你使用 <xref:System.Resources.ResourceManager> 类检索资源。  但是，如果你使用 Visual Studio 创建应用，则应使用 Visual Studio 创建的强类型包装器而不是直接使用 <xref:System.Resources.ResourceManager> 类。  
  
 若要在 Visual Studio 中创建强类型包装器，请在 Visual Studio 资源设计器中将主资源文件的**“访问修饰符”**设置为**“公共”**。  这将创建一个包含强类型 ResourceManager 包装器的 \[resourceFileName\].designer.cs 或 \[resourceFileName\].designer.vb 文件。  有关使用强类型资源包装器的详细信息，请参阅 [Resgen.exe（资源文件生成器）](../../../docs/framework/tools/resgen-exe-resource-file-generator.md)主题中的“生成强类型资源类”章节。  
  
## [!INCLUDE[net_portable](../../../includes/net-portable-md.md)]中的资源管理器  
 在[!INCLUDE[net_portable](../../../includes/net-portable-md.md)]项目中，所有对资源的访问均由 <xref:System.Resources.ResourceManager> 类处理。  由于 <xref:System.Resources> 命名空间中的类型（例如 <xref:System.Resources.ResourceReader> 和 <xref:System.Resources.ResourceSet>）不可从[!INCLUDE[net_portable](../../../includes/net-portable-md.md)]项目进行访问，因此它们不能用于访问资源。  
  
 [!INCLUDE[net_portable](../../../includes/net-portable-md.md)]项目包含下表中列出的四个 <xref:System.Resources.ResourceManager> 成员。  这些构造函数和方法使你能够实例化 <xref:System.Resources.ResourceManager> 对象和检索字符串资源。  
  
|`ResourceManager` 成员|描述|  
|--------------------------|--------|  
|<xref:System.Resources.ResourceManager.%23ctor%28System.String%2CSystem.Reflection.Assembly%29>|创建一个可访问在指定程序集中找到的已命名资源文件的 <xref:System.Resources.ResourceManager> 实例。|  
|<xref:System.Resources.ResourceManager.%23ctor%28System.Type%29>|创建一个与指定类型对应的 <xref:System.Resources.ResourceManager> 实例。|  
|<xref:System.Resources.ResourceManager.GetString%28System.String%29>|检索当前区域性的已命名资源。|  
|<xref:System.Resources.ResourceManager.GetString%28System.String%2CSystem.Globalization.CultureInfo%29>|检索属于指定区域性的已命名资源。|  
  
 从<xref:System.Resources.ResourceManager>中排除其他 [!INCLUDE[net_portable](../../../includes/net-portable-md.md)] 成员意味着，无法从资源文件中检索序列化的对象、非字符串数据和图像。  若要使用[!INCLUDE[net_portable](../../../includes/net-portable-md.md)]中的资源，你应使用字符串形式存储所有对象数据。  例如，你可以通过将数值转换为字符串来将其存储在资源文件中，并且你可以检索它们，然后使用数字数据类型的 `Parse` 或 `TryParse` 方法将其转换回数字。  你可通过调用 <xref:System.Convert.ToBase64String%2A?displayProperty=fullName> 方法将图像或其他二进制数据转换为字符串表示形式，并通过调用 <xref:System.Convert.FromBase64String%2A?displayProperty=fullName> 方法将其还原到字节数组。  
  
## [!INCLUDE[net_portable](../../../includes/net-portable-md.md)]和 Windows 应用商店应用  
 [!INCLUDE[net_portable](../../../includes/net-portable-md.md)]项目将资源存储在 .resx 文件中，这些文件随后将编译为 .resources 文件并在编译时嵌入到主程序集或附属程序集中。  另一方面，[!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用需在 .resw 文件中存储资源，这些文件随后将被编译为单个包资源索引 \(PRI\) 文件。  但是，尽管文件格式不兼容，你的[!INCLUDE[net_portable](../../../includes/net-portable-md.md)]仍将在 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用中工作。  
  
 若要从 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用使用你的类库，请在 Windows 应用商店应用项目中添加对类库的引用。  Visual Studio 将以透明方式从你的程序集中将资源提取到 .resw 文件中，并将其用于生成 [!INCLUDE[wrt](../../../includes/wrt-md.md)]可从中提取资源的 PRI 文件。  在运行时，[!INCLUDE[wrt](../../../includes/wrt-md.md)]会在你的[!INCLUDE[net_portable](../../../includes/net-portable-md.md)]中执行代码，但它从 PRI 文件中检索你的可移植类库的资源。  
  
 如果你的[!INCLUDE[net_portable](../../../includes/net-portable-md.md)]项目包含本地化资源，则根据需要对桌面应用中的库使用集散模型来部署这些资源。  若要在 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用中使用主资源文件和所有本地化的资源文件，可添加对主程序集的引用。  在编译时，Visual Studio 会将你的主资源文件以及所有本地化资源文件中的资源提取到单独的 .resw 文件中。  然后，它将 .resw 文件编译为 [!INCLUDE[wrt](../../../includes/wrt-md.md)]在运行时访问的单个 PRI 文件。  
  
<a name="NonLoc"></a>   
## 示例：非本地化的[!INCLUDE[net_portable](../../../includes/net-portable-md.md)]  
 以下是一个简单的非本地化的[!INCLUDE[net_portable](../../../includes/net-portable-md.md)]示例，它使用资源来存储列的名称并确定要为表格数据保留的字符数。  此示例使用名为 LibResources.resx 的文件存储下表中列出的字符串资源。  
  
|资源名称|资源值|  
|----------|---------|  
|Born|Birthdate|  
|BornLength|12|  
|Hired|雇佣日期|  
|HiredLength|12|  
|ID|ID|  
|ID.Length|12|  
|名称|名称|  
|NameLength|25|  
|标题|Employee Database|  
  
 以下代码定义 `UILibrary` 类，当文件的`resources`“访问修饰符”更改为**“公共”**时，该类使用 Visual Studio 所生成的名为  **的资源管理器包装器。** UILibrary 类根据需要分析字符串数据。  。  请注意，该类位于 `MyCompany.Employees` 命名空间中。  
  
 [!code-csharp[Conceptual.Resources.Portable#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.portable/cs/uilibrary.cs#1)]
 [!code-vb[Conceptual.Resources.Portable#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.portable/vb/uilibrary.vb#1)]  
  
 以下代码阐释如何从控制台模式应用访问 `UILibrary` 类及其资源。  它需要将对 UILIbrary.dll 的引用添加到控制台应用项目。  
  
 [!code-csharp[Conceptual.Resources.Portable#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.portable/cs/program.cs#2)]
 [!code-vb[Conceptual.Resources.Portable#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.portable/vb/module1.vb#2)]  
  
 下列代码阐释了如何从 `UILibrary`应用访问 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 类及其资源。  它需要将对 UILIbrary.dll 的引用添加到 Windows 应用商店应用项目。  
  
 [!code-csharp[Conceptual.Resources.PortableMetro#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.portablemetro/cs/blankpage.xaml.cs#1)]  
  
## 示例：本地化的[!INCLUDE[net_portable](../../../includes/net-portable-md.md)]  
 下面的本地化的[!INCLUDE[net_portable](../../../includes/net-portable-md.md)]示例包括法语（法国）和英语（美国）区域性的资源。  英语（美国）区域性是应用的默认区域性；其资源显示在[上一部分](../../../docs/standard/cross-platform/app-resources-for-libraries-that-target-multiple-platforms.md#NonLoc)的表中。  法语（法国）区域性的资源文件命名为 LibResources.fr\-FR.resx，该文件包含下表中列出的字符串资源。  `UILibrary` 类的源代码与上一部分中所示的相同。  
  
|资源名称|资源值|  
|----------|---------|  
|Born|Date de naissance|  
|BornLength|20|  
|Hired|Date embauché|  
|HiredLength|16|  
|ID|ID|  
|名称|Nom|  
|标题|Base de données des employés|  
  
 以下代码阐释如何从控制台模式应用访问 `UILibrary` 类及其资源。  它需要将对 UILIbrary.dll 的引用添加到控制台应用项目。  
  
 [!code-csharp[Conceptual.Resources.Portable#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.portable/cs/program2.cs#3)]
 [!code-vb[Conceptual.Resources.Portable#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.portable/vb/module2.vb#3)]  
  
 下列代码阐释了如何从 `UILibrary`应用访问 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 类及其资源。  它需要将对 UILIbrary.dll 的引用添加到 Windows 应用商店应用项目。  它使用静态 `ApplicationLanguages.PrimaryLanguageOverride` 属性将应用的首选语言设置为法语。  
  
 [!code-csharp[Conceptual.Resources.PortableMetroLoc#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.portablemetroloc/cs/blankpage.xaml.cs#1)]
 [!code-vb[Conceptual.Resources.PortableMetroLoc#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.portablemetroloc/vb/blankpage.xaml.vb#1)]  
  
## 请参阅  
 <xref:System.Resources.ResourceManager>   
 [桌面应用程序中的资源](../../../docs/framework/resources/index.md)   
 [打包和部署资源](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md)