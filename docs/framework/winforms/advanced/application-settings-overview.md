---
title: "应用程序设置概述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "ApplicationsSettingsOverview"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "应用程序设置 [Windows 窗体], 关于应用程序设置"
  - "动态属性"
  - "用户首选项, 跟踪"
ms.assetid: 0dd8bca5-a6bf-4ac4-8eec-5725d08b38dc
caps.latest.revision: 24
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 24
---
# 应用程序设置概述
本主题讨论如何代表你的应用程序和你的用户创建和存储设置数据。  
  
 Windows 窗体的应用程序设置功能使你可以在客户端计算机上轻松创建、存储和维护自定义应用程序和用户首选项。 利用 Windows 窗体应用程序设置，不仅可以存储应用程序数据（如数据库连接字符串），还可以存储特定于用户的数据（如用户应用程序首选项）。 使用 Visual Studio 或自定义托管代码，可以创建新设置、从磁盘读取设置和将设置写入磁盘、将设置绑定到窗体上的属性，以及在加载和保存设置数据前对设置数据进行验证。  
  
 应用程序设置使开发人员可以使用极少量的自定义代码在他们的应用程序中保存状态，这些设置替代了 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 的早期版本中的动态属性。 应用程序设置在很多方面优于动态属性，动态属性是只读的、后期绑定的，且需要较多的自定义编程。[!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)] 中保留了动态属性类，但它们只是 shell 类，用于对应用程序设置类进行简单包装。  
  
## 什么是应用程序设置？  
 Windows 窗体应用程序经常会需要某些特殊数据，这些数据对运行应用程序至关重要，但你又不想在应用程序代码中直接包含它们。 如果你的应用程序使用 Web 服务或数据库服务器，则你可能想将这种信息存储在一个单独的文件中，以便将来更改它而无需重新编译该应用程序。 同样，应用程序还可能需要存储特定于当前用户的数据。 例如，大多数应用程序都有用户首选项功能，该功能用于自定义应用程序的外观和行为。  
  
 应用程序设置通过提供一种简便方法，将应用程序范围设置和用户范围设置存储在客户端计算机上，从而满足了上述这两种需求。 使用 Visual Studio 或代码编辑器，可以通过指定设置的名称、数据类型和范围（应用程序或用户）来定义给定属性的设置。 还可以将相关设置放在命名组中以方便使用和读取。 定义设置后，这些设置将保持不变并在运行时被自动读回到内存中。 可插入体系结构允许更改保持机制，但默认情况下使用本地文件系统。  
  
 应用程序设置的工作方式是：根据设置是应用程序范围设置还是用户范围设置，将数据作为 XML 保持在不同的配置文件 \(.config\) 中。 在大多数情况下，应用程序范围设置是只读的；因为它们是编程信息，通常不需要覆盖它们。 相反，在运行时可以安全地读写用户范围设置，即使应用程序在部分信任环境下运行也是如此。 有关分部信任的详细信息，请参阅[Windows 窗体中的安全性概述](../../../../docs/framework/winforms/security-in-windows-forms-overview.md)。  
  
 设置在配置文件中存储为 XML 片段。 应用程序范围设置由 `<application.Settings>` 元素表示，这些设置通常位于 *app*.exe.config 中，其中 *app* 是主可执行文件的名称。 用户范围设置由 `<userSettings>` 元素表示，这些设置位于 *user*.config 中，其中 *user* 是当前运行应用程序的用户的用户名。*app*.exe.config 文件必须与应用程序一起部署；当应用程序首次保存用户设置时，设置体系结构将按要求创建 *user*.config 文件。 还可以在 *app*.exe.config 中定义 `<userSettings>` 块，以便为用户范围设置提供默认值。  
  
 自定义控件还可通过实现 <xref:System.Configuration.IPersistComponentSettings> 接口保存它们自己的设置，该接口公开 <xref:System.Configuration.IPersistComponentSettings.SaveSettings%2A> 方法。 Windows 窗体 <xref:System.Windows.Forms.ToolStrip> 控件实现此接口，以在应用程序会话之间保存工具栏和工具栏项的位置。 有关自定义控件和应用程序设置的详细信息，请参阅[自定义控件的应用程序设置](../../../../docs/framework/winforms/advanced/application-settings-for-custom-controls.md)。  
  
## 应用程序设置的限制  
 应用程序设置无法用于托管 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 的非托管应用程序。 这些设置在以下环境中将无效：Visual Studio 外接程序、用于 Microsoft Office 的 C\+\+、托管在 Internet Explorer 中的控件或 Microsoft Outlook 外接程序和项目。  
  
 当前无法绑定到 Windows 窗体中的某些属性。 最需要引起注意的是 <xref:System.Windows.Forms.Form.ClientSize%2A> 属性，因为绑定到该属性会导致在运行时发生不可预测的行为。 通常可以通过以编程方式保存和加载这些设置来解决这些问题。  
  
 应用程序设置不具备用于自动加密信息的内置功能。 切勿以明文形式存储与安全有关的信息，例如数据库密码。 如果要存储此类敏感信息，你作为应用程序开发人员有责任确保它是安全的。 如果要存储连接字符串，我们建议你使用 Windows 集成安全性，而不采用将密码硬编码到 URL 中的做法。 有关更多信息，请参见[代码访问安全性和 ADO.NET](../../../../docs/framework/data/adonet/code-access-security.md)。  
  
## 开始使用应用程序设置  
 如果使用 Visual Studio，则可以在 Windows 窗体设计器中使用“属性”窗口中的“\(ApplicationSettings\)”属性来定义设置。 当以这种方式定义设置时，Visual Studio 自动创建一个自定义托管包装器类，该包装器类将每个设置与一个类属性关联。 Visual Studio 还负责将设置绑定到窗体或控件上的属性，以便在显示控件窗体时自动还原控件设置，并在关闭窗体时自动保存控件设置。  
  
 如果要对设置进行更细致的控制，你可以定义自己的自定义应用程序设置包装器类。 此操作的实现步骤如下：从 <xref:System.Configuration.ApplicationSettingsBase> 派生一个类，然后添加与每个设置相对应的属性，最后将特殊的特性应用到这些属性。 有关创建包装类的详细信息，请参阅[应用程序设置体系结构](../../../../docs/framework/winforms/advanced/application-settings-architecture.md)。  
  
 还可以使用 <xref:System.Windows.Forms.Binding> 类以编程方式将设置绑定到窗体和控件上的属性。  
  
## 请参阅  
 <xref:System.Configuration.ApplicationSettingsBase>   
 <xref:System.Configuration.SettingsProvider>   
 <xref:System.Configuration.LocalFileSettingsProvider>   
 <xref:System.Configuration.IPersistComponentSettings>   
 [如何：验证应用程序设置](../../../../docs/framework/winforms/advanced/how-to-validate-application-settings.md)   
 [管理应用程序设置 \(.NET\)](../Topic/Managing%20Application%20Settings%20\(.NET\).md)   
 [如何：在运行时读取设置 \(C\#\)](../../../../docs/framework/winforms/advanced/how-to-read-settings-at-run-time-with-csharp.md)   
 [使用应用程序设置和用户设置](../../../../docs/framework/winforms/advanced/using-application-settings-and-user-settings.md)   
 [应用程序设置体系结构](../../../../docs/framework/winforms/advanced/application-settings-architecture.md)   
 [自定义控件的应用程序设置](../../../../docs/framework/winforms/advanced/application-settings-for-custom-controls.md)