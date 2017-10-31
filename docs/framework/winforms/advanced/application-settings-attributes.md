---
title: "应用程序设置特性 | Microsoft Docs"
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
  - "应用程序设置 [Windows 窗体], 特性"
  - "特性 [Windows 窗体], 应用程序设置"
  - "包装类, 应用程序设置"
ms.assetid: 53caa66c-a9fb-43a5-953c-ad092590098d
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 应用程序设置特性
应用程序设置结构提供很多特性，这些特性可应用于应用程序设置包装类或应用程序设置包装类的各个属性。  这些特性在运行时由应用程序设置基础结构（通常具体指设置提供程序）进行检查，以便使这些特性的功能符合自定义包装的要求。  
  
 下表中列出了一些特性，这些特性有的可应用于应用程序设置包装类、有的可应用于应用程序设置包装类的各个属性，有的可应用于这两者。  根据定义，对于每个设置属性，必须而且只能应用一个范围特性（**UserScopedSettingAttribute** 或 **ApplicationScopedSettingAttribute**）。  
  
> [!NOTE]
>  只有在识别以下三个特性：**ApplicationScopedSettingAttribute**、**UserScopedSettingAttribute** 和 **DefaultSettingValueAttribute** 时，才需要从 <xref:System.Configuration.SettingsProvider> 类派生的自定义设置提供程序。  
  
|特性|Target|说明|  
|--------|------------|--------|  
|<xref:System.Configuration.SettingsProviderAttribute>|高度和宽度|指定要用于保持的设置提供程序的简称。<br /><br /> 如果未提供此特性，则假定为默认提供程序 <xref:System.Configuration.LocalFileSettingsProvider>。|  
|<xref:System.Configuration.UserScopedSettingAttribute>|高度和宽度|将属性定义为用户范围的应用程序设置。|  
|<xref:System.Configuration.ApplicationScopedSettingAttribute>|高度和宽度|将属性定义为应用程序范围的应用程序设置。|  
|<xref:System.Configuration.DefaultSettingValueAttribute>|属性|指定一个字符串，提供程序可以将该字符串反序列化为此属性的硬编码默认值。<br /><br /> <xref:System.Configuration.LocalFileSettingsProvider> 不需要此特性，如果已保留某个值，则设置提供程序将重写此特性所提供的任何相应值。|  
|<xref:System.Configuration.SettingsDescriptionAttribute>|属性|对单个设置进行描述性检查，该特性主要由运行时和设计时工具使用。|  
|<xref:System.Configuration.SettingsGroupNameAttribute>|类|提供设置组的显式名称。  如果没有此特性，则 <xref:System.Configuration.ApplicationSettingsBase> 使用包装类的名称。|  
|<xref:System.Configuration.SettingsGroupDescriptionAttribute>|类|对设置组进行描述性检查，该特性主要由运行时和设计时工具使用。|  
|<xref:System.Configuration.SettingsManageabilityAttribute>|高度和宽度|指定零个或多个应提供给设置组或属性的管理功能服务。  可用的服务在 <xref:System.Configuration.SettingsManageability> 枚举中给出。|  
|<xref:System.Configuration.SpecialSettingAttribute>|属性|指示设置属于专用的预定义类别（如连接字符串），该类别应由设置提供程序进行专门处理。  此特性的预定义类别由 <xref:System.Configuration.SpecialSetting> 枚举定义。|  
|<xref:System.Configuration.SettingsSerializeAsAttribute>|高度和宽度|指定设置组或属性的首选序列化机制。  可用序列化机制由 <xref:System.Configuration.SettingsSerializeAs> 枚举定义。|  
|<xref:System.Configuration.NoSettingsVersionUpgradeAttribute>|属性|指定设置提供程序应禁用已标记属性的所有应用程序升级功能。|  
  
 “类”指示特性只可以应用到应用程序设置包装类。  “属性”指示特性只可以应用到设置属性。  “属性和类”指示特性可应用到任何一级。  
  
## 请参阅  
 <xref:System.Configuration.ApplicationSettingsBase>   
 <xref:System.Configuration.SettingsProvider>   
 [应用程序设置体系结构](../../../../docs/framework/winforms/advanced/application-settings-architecture.md)   
 [How to: Create Application Settings](http://msdn.microsoft.com/zh-cn/53b3af80-1c02-4e35-99c6-787663148945)