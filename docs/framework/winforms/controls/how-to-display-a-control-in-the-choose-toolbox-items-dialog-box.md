---
title: "如何：在“选择工具箱项”对话框中显示控件 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "全局程序集缓存，“选择工具箱项”对话框"
  - "AssemblyFoldersEx，“选择工具箱项”对话框"
  - "控件，在“选择工具箱项”对话框中显示"
  - "程序集文件夹注册，“选择工具箱项”对话框"
  - "“选择工具箱项”对话框，显示控件"
ms.assetid: 01ef6eba-d044-40f0-951d-78eff7ebd9a9
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：在“选择工具箱项”对话框中显示控件
在开发和分发控件时，您可能希望这些控件显示在**“选择工具箱项”**对话框中，该对话框会在您右击**“工具箱”**并选择**“选择项”**时显示。  通过使用 AssemblyFoldersEx 注册过程，可以使控件显示在此对话框中。  
  
### 在“选择工具箱项”对话框中显示控件  
  
-   将控件程序集安装到全局程序集缓存中。  有关更多信息，请参见[如何：将程序集安装到全局程序集缓存](../../../../docs/framework/app-domains/how-to-install-an-assembly-into-the-gac.md)  
  
     \- 或 \-  
  
-   通过使用 AssemblyFoldersEx 注册过程来注册控件及其相关设计时程序集。  AssemblyFoldersEx 是注册表中的一个位置，供第三方供应商存储他们所支持的每个框架版本的路径。  设计时解决方案可以在该注册表位置中查找引用程序集。  注册表脚本可以指定要显示在工具箱中的控件。  有关更多信息，请参见[部署自定义控件和设计时程序集](http://msdn.microsoft.com/zh-cn/96158eb0-b691-4ae1-9e7b-3c65a1b798cb)。  
  
## 请参阅  
 [Choose Toolbox Items Dialog Box \(Visual Studio\)](http://msdn.microsoft.com/zh-cn/bd07835f-18a8-433e-bccc-7141f65263bb)   
 [部署自定义控件和设计时程序集](http://msdn.microsoft.com/zh-cn/96158eb0-b691-4ae1-9e7b-3c65a1b798cb)   
 [设计时开发 Windows 窗体控件](../../../../docs/framework/winforms/controls/developing-windows-forms-controls-at-design-time.md)   
 [如何：将程序集安装到全局程序集缓存](../../../../docs/framework/app-domains/how-to-install-an-assembly-into-the-gac.md)   
 [演练：使用自定义组件自动填充工具箱](../../../../docs/framework/winforms/controls/walkthrough-automatically-populating-the-toolbox-with-custom-components.md)