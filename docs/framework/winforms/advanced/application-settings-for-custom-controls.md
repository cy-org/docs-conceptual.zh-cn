---
title: "自定义控件的应用程序设置 | Microsoft Docs"
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
  - "应用程序设置 [Windows 窗体], 自定义控件"
  - "自定义控件 [Windows 窗体], 应用程序设置"
ms.assetid: f44afb74-76cc-44f2-890a-44b7cdc211a1
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 自定义控件的应用程序设置
您必须完成某些任务，以使自定义控件位于第三方应用程序上时，这些自定义控件能够保持应用程序设置。  
  
 在编写大多数关于应用程序设置功能的文档时，都假定您要创建的是独立应用程序。  然而，如果要创建的控件将由其他开发人员的应用程序承载时，则需要执行几个额外步骤，以使控件能够正确地保持其设置。  
  
## 应用程序设置和自定义控件  
 为了使控件能够正确地保持其设置，控件必须封装进程，方法是创建自己专用的应用程序设置包装类，该类派生自 <xref:System.Configuration.ApplicationSettingsBase>。  另外，主控件类必须实现 <xref:System.Configuration.IPersistComponentSettings>。  该接口包含几个属性和两个方法，这两个方法是 <xref:System.Configuration.IPersistComponentSettings.LoadComponentSettings%2A> 及 <xref:System.Configuration.IPersistComponentSettings.SaveComponentSettings%2A>。  如果在 Visual Studio 中使用**“Windows 窗体设计器”**将控件添加到窗体，则当初始化控件时，Windows 窗体将自动调用 <xref:System.Configuration.IPersistComponentSettings.LoadComponentSettings%2A>；但是您必须自己在控件的  `Dispose`  方法中调用 <xref:System.Configuration.IPersistComponentSettings.SaveComponentSettings%2A>。  
  
 此外，应实现以下内容，从而使自定义控件的应用程序设置在设计时环境（例如 Visual Studio）中正常工作：  
  
1.  自定义应用程序设置类，带有将 <xref:System.ComponentModel.IComponent> 作为单个参数的构造函数。  使用此类以保存并加载所有应用程序设置。  创建此类的新实例时，使用该构造函数传递自定义控件。  
  
2.  在控件已创建并放置在窗体上（例如窗体的 <xref:System.Windows.Forms.Form.Load> 事件处理程序中）之后，创建此自定义设置类。  
  
 有关创建自定义设置类的说明，请参见[如何：创建应用程序设置](../../../../docs/framework/winforms/advanced/how-to-create-application-settings.md)。  
  
## 设置键和共享设置  
 有些控件可以在同一窗体中使用多次。  大多数这种情况下，您都会希望这些控件能够保持它们自己的各个设置。  利用 <xref:System.Configuration.IPersistComponentSettings> 上的 <xref:System.Configuration.IPersistComponentSettings.SettingsKey%2A> 属性，可以提供一个唯一字符串，以区分窗体中同一控件的多个版本。  
  
 实现 <xref:System.Configuration.IPersistComponentSettings.SettingsKey%2A> 的最简单的方法是为 <xref:System.Configuration.IPersistComponentSettings.SettingsKey%2A> 使用控件的 <xref:System.Windows.Forms.Control.Name%2A> 属性。  当您加载或保存控件的设置时，可将 <xref:System.Configuration.IPersistComponentSettings.SettingsKey%2A> 的值传递到 <xref:System.Configuration.ApplicationSettingsBase> 类的 <xref:System.Configuration.ApplicationSettingsBase.SettingsKey%2A> 属性。  当应用程序设置在 XML 中保持用户的设置时，应用程序设置使用此唯一键。  下面的代码示例显示一个  `<userSettings>`  节可能如何查找名为  `CustomControl1`  的自定义控件的实例，该自定义控件保存其  `Text`  属性的设置。  
  
```  
<userSettings>  
    <CustomControl1>  
        <setting name="Text" serializedAs="string">  
            <value>Hello, World</value>  
        </setting>  
    </CustomControl1>  
</userSettings>  
```  
  
 所有没有为 <xref:System.Configuration.ApplicationSettingsBase.SettingsKey%2A> 提供值的控件的实例将共享相同的设置。  
  
## 请参阅  
 <xref:System.Configuration.ApplicationSettingsBase>   
 <xref:System.Configuration.IPersistComponentSettings>   
 [应用程序设置体系结构](../../../../docs/framework/winforms/advanced/application-settings-architecture.md)