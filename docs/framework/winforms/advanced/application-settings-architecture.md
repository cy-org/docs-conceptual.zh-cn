---
title: "应用程序设置体系结构 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "应用程序设置 [Windows 窗体], 体系结构"
ms.assetid: c8eb2ad0-fac6-4ea2-9140-675a4a44d562
caps.latest.revision: 25
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 25
---
# 应用程序设置体系结构
此主题描述应用程序设置结构是如何工作的，并探索该结构的高级功能，如分组设置和设置键。  
  
 应用程序设置结构支持定义应用程序或用户范围的强类型设置，并支持保留应用程序会话间的设置。  该结构提供一个默认的持久性引擎，用于将设置保存到本地文件系统以及从本地文件系统加载设置。  该结构还定义了用于提供自定义持久性引擎的接口。  
  
 利用所提供的接口，在应用程序中承载自定义组件时，能够使这些自定义组件保留它们自己的设置。  通过使用设置键，组件能够保持分隔组件的多个实例的设置。  
  
## 定义设置  
 应用程序设置结构用于 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 和 Windows 窗体，其中包含许多在这两种环境中共享的基类。  其中最重要的基类是 <xref:System.Configuration.SettingsBase>，它通过集合提供对设置的访问，并提供用于加载和保存设置的底层方法。  每个环境都实现从 <xref:System.Configuration.SettingsBase> 派生的其自己的类，以便为该环境提供附加的设置功能。  在基于 Windows 窗体的应用程序中，所有的应用程序设置都必须在从 <xref:System.Configuration.ApplicationSettingsBase> 类派生的类上定义，派生的类可将下列功能添加到基类：  
  
-   高层加载和保存操作  
  
-   对用户范围设置的支持  
  
-   将用户的设置还原为预定义的默认值  
  
-   从以前的应用程序版本升级设置  
  
-   在更改设置前或在保存设置前验证设置  
  
 这些设置能够用一些在 <xref:System.Configuration> 命名空间内定义的特性来描述；在 [应用程序设置特性](../../../../docs/framework/winforms/advanced/application-settings-attributes.md) 中介绍了这些特性。  定义设置时，必须将 <xref:System.Configuration.ApplicationScopedSettingAttribute> 或 <xref:System.Configuration.UserScopedSettingAttribute> 应用到设置，这两个属性描述该设置是应用于整个应用程序，还是仅应用于当前用户。  
  
 下面的代码示例定义一个具有单个设置  `BackgroundColor` 的自定义设置类。  
  
 [!code-csharp[ApplicationSettings.Create#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ApplicationSettings.Create/CS/MyAppSettings.cs#1)]
 [!code-vb[ApplicationSettings.Create#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ApplicationSettings.Create/VB/MyAppSettings.vb#1)]  
  
## 设置持久性  
 <xref:System.Configuration.ApplicationSettingsBase> 类自身不保留也不加载设置；此工作由设置提供程序完成，设置提供程序就是从 <xref:System.Configuration.SettingsProvider> 派生的一个类。  如果 <xref:System.Configuration.ApplicationSettingsBase> 的派生类没有通过 <xref:System.Configuration.SettingsProviderAttribute> 指定设置提供程序，则使用默认的设置提供程序，即 <xref:System.Configuration.LocalFileSettingsProvider>。  
  
 最初和 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 一起发布的配置系统，支持通过本地计算机的 machine.config 文件提供静态应用程序配置数据，或在与应用程序一起部署的 `app.`exe.config 文件内提供静态应用程序配置数据。  <xref:System.Configuration.LocalFileSettingsProvider> 类以下列方式扩展此本机支持：  
  
-   应用程序范围设置可以存储在 machine.config 或 `app.`exe.config 文件中。  Machine.config 始终是只读的，而出于安全考虑，`app`.exe.config 对于大多数应用程序也限制为只读。  
  
-   用户范围设置可以存储在 `app`.exe.config 文件中，在这种情况下，这些设置被视为静态默认设置。  
  
-   非默认的用户范围设置存储在新文件 *user*.config 中，其中 *user* 是当前执行应用程序的用户的用户名。  您可以使用 <xref:System.Configuration.DefaultSettingValueAttribute> 属性为用户范围设置指定默认值。  由于用户范围设置在应用程序执行期间经常更改，所以 `user`.config 始终是可读\/写的。  
  
 所有这三种配置文件都以 XML 格式存储设置。  应用程序范围设置的顶级 XML 元素为 `<appSettings>`，而 `<userSettings>` 用作用户范围设置。  既包含应用程序范围设置，又包含用户范围设置默认值的 `app`.exe.config 文件如下所示：  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
    <configSections>  
        <sectionGroup name="applicationSettings" type="System.Configuration.ApplicationSettingsGroup, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" >  
            <section name="WindowsApplication1.Properties.Settings" type="System.Configuration.ClientSettingsSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
        </sectionGroup>  
        <sectionGroup name="userSettings" type="System.Configuration.UserSettingsGroup, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" >  
            <section name="WindowsApplication1.Properties.Settings" type="System.Configuration.ClientSettingsSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" allowExeDefinition="MachineToLocalUser" />  
        </sectionGroup>  
    </configSections>  
    <applicationSettings>  
        <WindowsApplication1.Properties.Settings>  
            <setting name="Cursor" serializeAs="String">  
                <value>Default</value>  
            </setting>  
            <setting name="DoubleBuffering" serializeAs="String">  
                <value>False</value>  
            </setting>  
        </WindowsApplication1.Properties.Settings>  
    </applicationSettings>  
    <userSettings>  
        <WindowsApplication1.Properties.Settings>  
            <setting name="FormTitle" serializeAs="String">  
                <value>Form1</value>  
            </setting>  
            <setting name="FormSize" serializeAs="String">  
                <value>595, 536</value>  
            </setting>  
        </WindowsApplication1.Properties.Settings>  
    </userSettings>  
</configuration>  
```  
  
 有关配置文件的应用程序设置部分内的元素定义，请参见 [应用程序设置架构](../../../../docs/framework/configure-apps/file-schema/application-settings-schema.md)。  
  
### 设置绑定  
 应用程序设置使用 Windows 窗体数据绑定结构，提供设置对象和组件间设置更新的双向通信。  如果使用 Visual Studio 创建应用程序设置并将它们分配给组件属性，则将自动生成这些绑定。  
  
 只能将应用程序设置绑定到支持 <xref:System.Windows.Forms.IBindableComponent> 接口的组件。  此外，该组件必须实现特定绑定属性的更改事件，或通知应用程序设置已通过 <xref:System.ComponentModel.INotifyPropertyChanged> 接口更改属性。  如果组件没有实现 <xref:System.Windows.Forms.IBindableComponent>，且您要通过 Visual Studio 进行绑定，则将首次设置绑定属性，但不会更新。  如果组件实现了 <xref:System.Windows.Forms.IBindableComponent> 但不支持属性更改通知，则更改属性时不会在设置文件中更新绑定。  
  
 某些 Windows 窗体组件（如 <xref:System.Windows.Forms.ToolStripItem>）不支持设置绑定。  
  
### 设置序列化  
 当 <xref:System.Configuration.LocalFileSettingsProvider> 必须将设置保存到磁盘时，它执行下列操作：  
  
1.  使用反射来检查在 <xref:System.Configuration.ApplicationSettingsBase> 派生类上定义的所有属性，找出那些应用了 <xref:System.Configuration.ApplicationScopedSettingAttribute> 或 <xref:System.Configuration.UserScopedSettingAttribute> 的属性。  
  
2.  将属性序列化到磁盘。  设置提供程序首先尝试调用类型的关联 <xref:System.ComponentModel.TypeConverter> 上的 <xref:System.ComponentModel.TypeConverter.ConvertToString%2A> 或 <xref:System.ComponentModel.TypeConverter.ConvertFromString%2A>。  如果不成功，则设置提供程序改用 XML 序列化。  
  
3.  基于设置的特性，确定设置应保存到的文件。  
  
 如果您要实现自己的设置类，则可以使用 <xref:System.Configuration.SettingsSerializeAsAttribute> 标记二进制或自定义序列化（使用 <xref:System.Configuration.SettingsSerializeAs> 枚举）的设置。  有关在代码中创建您自己的设置类的更多信息，请参见 [如何：创建应用程序设置](../../../../docs/framework/winforms/advanced/how-to-create-application-settings.md)。  
  
### 设置文件的位置  
 根据应用程序安装方式的不同，`app`.exe.config 和 *user*.config 文件的位置有所不同。  对于复制到本地计算机上的基于 Windows 窗体的应用程序，`app`.exe.config 将驻留在与该应用程序的主可执行文件所在基目录相同的目录中，而 *user*.config 将驻留在由 <xref:System.Windows.Forms.Application.LocalUserAppDataPath%2A?displayProperty=fullName> 属性指定的位置中。  对于以 [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)] 方式安装的应用程序，这两个文件都驻留在 %InstallRoot%\\Documents and Settings\\*username*\\Local Settings 下的 [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)] 数据目录中。  
  
 如果用户启用了漫游配置文件，则这些文件的存储位置会稍有不同，漫游配置文件使用户在使用域内的其他计算机时能够定义不同的 Windows 和应用程序设置。  在这种情况下，[!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)] 应用程序和非 [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)] 应用程序两者的 `app`.exe.config 和 *user*.config 文件都将存储在 %InstallRoot%\\Documents and Settings\\*username*\\Application Data 下。  
  
 有关应用程序设置功能如何与新部署技术协同使用的更多信息，请参见 [ClickOnce 和应用程序设置](../Topic/ClickOnce%20and%20Application%20Settings.md)。  有关 [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)] 数据目录的更多信息，请参见 [在 ClickOnce 应用程序中访问本地数据和远程数据](../Topic/Accessing%20Local%20and%20Remote%20Data%20in%20ClickOnce%20Applications.md)。  
  
## 应用程序设置和安全  
 应用程序设置设计为在部分信任的环境中运行，这种环境是一种权限受限制的环境，对于 Internet 或 intranet 上承载的 Windows 窗体应用程序来说是默认环境。  通过默认设置提供程序使用应用程序设置时，不需要超出部分信任之外的特别权限。  
  
 在 [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)] 应用程序中使用应用程序设置时，`user`.config 文件存储在 [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)] 数据目录中。  应用程序的 `user`.config 文件大小不能超过由 [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)] 设置的数据目录配额。  有关更多信息，请参见 [ClickOnce 和应用程序设置](../Topic/ClickOnce%20and%20Application%20Settings.md)。  
  
## 自定义设置提供程序  
 在应用程序设置结构中，应用程序设置的包装类与关联的一个或多个设置提供程序间存在松散的耦合关系，其中包装类派生自 <xref:System.Configuration.ApplicationSettingsBase>，设置提供程序派生自 <xref:System.Configuration.SettingsProvider>。  这种关联关系仅由应用于包装类或其各个属性的 <xref:System.Configuration.SettingsProviderAttribute> 来定义。  如果未显式指定设置提供程序，则使用默认提供程序 <xref:System.Configuration.LocalFileSettingsProvider>。  因此，此结构支持创建和使用自定义的设置提供程序。  
  
 例如，假定您想开发和使用 `SqlSettingsProvider`，该提供程序将所有设置数据存储在 Microsoft SQL Server 数据库中。  在这种情况下，可以使用从 <xref:System.Configuration.SettingsProvider> 派生的类的  `Initialize`  方法来接收此信息，方法是将该信息作为 <xref:System.Collections.Specialized.NameValueCollection?displayProperty=fullName> 类型的参数传递。  然后实现 <xref:System.Configuration.SettingsProvider.GetPropertyValues%2A> 方法，从数据存储区检索设置，并实现 <xref:System.Configuration.SettingsProvider.SetPropertyValues%2A> 以保存设置。  提供程序可以使用提供给 <xref:System.Configuration.SettingsProvider.GetPropertyValues%2A> 的 <xref:System.Configuration.SettingsPropertyCollection> 来确定属性的名称、类型和范围，以及为该属性定义的所有其他设置特性。  
  
 您的提供程序需要实现一个属性和一个方法，这些实现可能不太明显。  <xref:System.Configuration.SettingsProvider.ApplicationName%2A> 属性是 <xref:System.Configuration.SettingsProvider> 的抽象属性；您应该对其进行编程，使其返回下列代码：  
  
 [!code-csharp[ApplicationSettings.Architecture#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ApplicationSettings.Architecture/CS/DummyClass.cs#2)]
 [!code-vb[ApplicationSettings.Architecture#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ApplicationSettings.Architecture/VB/DummyProviderClass.vb#2)]  
  
 您的派生类还必须实现一个 `Initialize` 方法，该方法既不采用参数也不返回值。  此方法不由 <xref:System.Configuration.SettingsProvider> 定义。  
  
 最后，在提供程序上实现 <xref:System.Configuration.IApplicationSettingsProvider>，以便为刷新设置、还原设置默认值，及将设置从一个应用程序版本升级到另一个应用程序版本提供支持。  
  
 实现并编译了该提供程序后，需要指示设置类使用此提供程序，而不是使用默认的提供程序。  这一点可以通过 <xref:System.Configuration.SettingsProviderAttribute> 来完成。  如果该提供程序应用于整个设置类，则此提供程序用于该类定义的每个设置；如果该提供程序应用于某些设置，则应用程序设置结构仅对这些设置使用此提供程序，而对其余设置使用 <xref:System.Configuration.LocalFileSettingsProvider>。  下面的代码示例说明如何指示设置类使用自定义提供程序。  
  
 [!code-csharp[ApplicationSettings.Architecture#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/ApplicationSettings.Architecture/CS/DummyClass.cs#1)]
 [!code-vb[ApplicationSettings.Architecture#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/ApplicationSettings.Architecture/VB/DummyProviderClass.vb#1)]  
  
 提供程序可能会同时被多个线程调用，但提供程序始终写入同一存储位置；因此，应用程序设置结构在任何时候都仅实例化提供程序类的一个实例。  
  
> [!IMPORTANT]
>  您应确保您的提供程序是线程安全的，并且一次只允许一个线程写配置文件。  
  
 您的提供程序不需要支持 <xref:System.Configuration?displayProperty=fullName> 命名空间中定义的所有设置特性，但至少必须支持 <xref:System.Configuration.ApplicationScopedSettingAttribute> 和 <xref:System.Configuration.UserScopedSettingAttribute>，此外还应支持 <xref:System.Configuration.DefaultSettingValueAttribute>。  对于提供程序不支持的那些特性，您的提供程序应直接失败，而不另行通知；提供程序不应引发异常。  然而，如果设置类使用无效的特性组合，如将 <xref:System.Configuration.ApplicationScopedSettingAttribute> 和 <xref:System.Configuration.UserScopedSettingAttribute> 应用于同一设置，则提供程序应引发异常并终止操作。  
  
## 请参阅  
 <xref:System.Configuration.ApplicationSettingsBase>   
 <xref:System.Configuration.SettingsProvider>   
 <xref:System.Configuration.LocalFileSettingsProvider>   
 [应用程序设置概述](../../../../docs/framework/winforms/advanced/application-settings-overview.md)   
 [自定义控件的应用程序设置](../../../../docs/framework/winforms/advanced/application-settings-for-custom-controls.md)   
 [ClickOnce 和应用程序设置](../Topic/ClickOnce%20and%20Application%20Settings.md)   
 [应用程序设置架构](../../../../docs/framework/configure-apps/file-schema/application-settings-schema.md)