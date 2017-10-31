---
title: "ErrorProvider 组件概述（Windows 窗体） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "ErrorProvider"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "错误信息, 显示"
  - "ErrorProvider 组件 [Windows 窗体], 关于 ErrorProvider 组件"
  - "错误 [Windows 窗体], 向用户显示"
ms.assetid: ced189f2-b5c8-46a7-a6f1-37f5af95dc99
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# ErrorProvider 组件概述（Windows 窗体）
使用 Windows 窗体 [ErrorProvider](../../../../docs/framework/winforms/controls/errorprovider-component-windows-forms.md) 组件，可以对窗体或控件上的用户输入进行验证。  当验证用户在窗体中的输入或显示数据集内的错误时，一般要用到该控件。  相对于在消息框中显示错误信息，错误提供程序是更好的选择，因为一旦关闭了消息框，就再也看不见错误信息。  <xref:System.Windows.Forms.ErrorProvider> 组件在相关控件（如文本框）旁显示一个错误图标 \(![“ErrorProvider”图标](../../../../docs/framework/winforms/controls/media/vberrorprovidericon.png "vbErrorProviderIcon")\)；当用户将鼠标指针放在该错误图标上时，将出现显示错误信息字符串的工具提示。  
  
## 主要属性  
 <xref:System.Windows.Forms.ErrorProvider> 组件的主要属性是 <xref:System.Windows.Forms.ErrorProvider.DataSource%2A>、<xref:System.Windows.Forms.ErrorProvider.ContainerControl%2A> 和 <xref:System.Windows.Forms.ErrorProvider.Icon%2A>。  将 <xref:System.Windows.Forms.ErrorProvider> 组件与数据绑定控件结合使用时，必须将 <xref:System.Windows.Forms.ErrorProvider.ContainerControl%2A> 属性设置为相应的容器（通常是 Windows 窗体），以便于该组件可以在窗体上显示错误图标。  在设计器中添加该组件时，将 <xref:System.Windows.Forms.ErrorProvider.ContainerControl%2A> 属性设置为包含窗体；如果在代码中添加该控件，必须自行设置该属性。  
  
 <xref:System.Windows.Forms.ErrorProvider.Icon%2A> 属性可以设置为自定义错误图标而不是默认图标。  设置 <xref:System.Windows.Forms.ErrorProvider.DataSource%2A> 属性后，<xref:System.Windows.Forms.ErrorProvider> 组件便可为数据集显示错误信息。  <xref:System.Windows.Forms.ErrorProvider> 组件的主要方法是 <xref:System.Windows.Forms.ErrorProvider.SetError%2A> 方法，该方法可以指定错误信息字符串和错误图标应出现的位置。  
  
> [!NOTE]
>  <xref:System.Windows.Forms.ErrorProvider> 组件不提供对具有辅助功能的客户端的内置支持。  若要在使用此组件时使应用程序可访问，必须提供一种附加的可访问反馈机制。  
  
## 请参阅  
 <xref:System.Windows.Forms.ErrorProvider>   
 [如何：使用 Windows 窗体 ErrorProvider 组件查看数据集中的错误](../../../../docs/framework/winforms/controls/view-errors-within-a-dataset-with-wf-errorprovider-component.md)   
 [如何：使用 Windows 窗体 ErrorProvider 组件显示窗体验证的错误图标](../../../../docs/framework/winforms/controls/display-error-icons-for-form-validation-with-wf-errorprovider.md)