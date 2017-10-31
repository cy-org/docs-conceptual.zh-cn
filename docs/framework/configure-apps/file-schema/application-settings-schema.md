---
title: "应用程序设置架构 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "应用程序设置, 架构 [Windows 窗体]"
  - "配置架构 [.NET Framework], 应用程序设置"
  - "架构应用程序设置"
  - "Windows 窗体, 应用程序设置架构"
ms.assetid: 5797fcff-6081-4e8c-bebf-63d9c70cf14b
caps.latest.revision: 3
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 3
---
# 应用程序设置架构
应用程序设置允许 Windows 窗体或 ASP.NET 应用程序存储和检索应用程序范围和用户范围的设置。  本上下文中的“设置”是可能特定于应用程序或特定于当前用户的任何信息 \-\- 从数据库连接字符串到用户的首选默认窗口大小的任何内容。  
  
 默认情况下，Windows 窗体应用程序中的应用程序设置使用 <xref:System.Configuration.LocalFileSettingsProvider>，后者使用 .NET 配置系统将设置存储在一个 XML 配置文件中。  有关应用程序设置所使用的文件的更多信息，请参见 [应用程序设置体系结构](../../../../docs/framework/winforms/advanced/application-settings-architecture.md)。  
  
 应用程序设置将下列元素定义为它使用的配置文件的一部分。  
  
|元素|说明|  
|--------|--------|  
|`<applicationSettings>` 元素|包含特定于应用程序的所有 `<setting>` 标记。|  
|`<userSettings>` 元素|包含特定于当前用户的所有 `<setting>` 标记。|  
|`<setting>` 元素|定义设置。  `<applicationSettings>` 或 `<userSettings>` 的子项。|  
|`<value>` 元素|定义设置的值。  `<setting>` 的子项。|  
  
## \<applicationSettings\> 元素  
 这个元素包含所有的被指定为客户端计算机上的应用程序的实例的\<setting\>标签。  它不定义任何特性。  
  
## \<userSettings\>元素  
 这个元素包含所有的被指定到当前应用程序的使用者的\<setting\>标签。  它不定义任何特性。  
  
## \<setting\> 元素  
 此元素定义设置。  它具有以下特性：  
  
|元素|说明|  
|--------|--------|  
|`name`|必选。  设置的唯一 ID。  通过 Visual Studio 创建的设置使用名称 `ProjectName``.Properties.Settings` 进行保存。|  
|`serializedAs`|必选。  用于将值序列化为文本的格式。  有效值为：<br /><br /> -   `string`。  值使用 <xref:System.ComponentModel.TypeConverter> 被序列化为字符串。<br />-   `xml`。  值使用 XML 序列化进行序列化。<br />-   `binary`。  值使用二进制序列化被序列化为文本编码的二进制。<br />-   `custom`。  设置提供程序本身知道存在此设置，并将对其进行序列化和反序列化。<br />-   若要使用二进制或自定义序列化，您必须定义自己的设置类并使用 <xref:System.Configuration.SettingsSerializeAsAttribute> 指定二进制或自定义序列化。|  
  
## \<value\> 元素  
 此元素包含设置的值。  
  
## 示例  
 下面的代码示例演示一个应用程序设置文件，该文件定义两个应用程序范围的设置和两个用户范围的设置。  
  
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
  
## 请参阅  
 [应用程序设置概述](../../../../docs/framework/winforms/advanced/application-settings-overview.md)   
 [应用程序设置体系结构](../../../../docs/framework/winforms/advanced/application-settings-architecture.md)