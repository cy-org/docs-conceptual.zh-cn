---
title: "在 Windows 窗体上承载 ActiveX 控件时的注意事项 | Microsoft Docs"
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
  - "ActiveX 控件 [Windows 窗体], 添加"
  - "ActiveX 控件 [Windows 窗体], 承载"
  - "Windows 窗体控件, ActiveX 控件"
  - "Windows 窗体, ActiveX 控件"
  - "Windows 窗体, 承载 ActiveX 控件"
ms.assetid: 2509302d-a74e-484f-9890-2acdbfa67a68
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 在 Windows 窗体上承载 ActiveX 控件时的注意事项
尽管 Windows 窗体已经为承载 Windows 窗体控件而进行了优化，您仍可以使用 ActiveX 控件。  规划使用 ActiveX 控件的应用程序时应注意下列事项：  
  
-   **安全性** 公共语言运行时已增强了代码访问安全性。  以 Windows 窗体为特色的应用程序在完全受信任的环境中运行不会有任何问题；在不完全受信任的环境中运行时，大部分功能是可访问的。  Windows 窗体控件不用编译就可以在浏览器中承载。  然而，Windows 窗体上的 ActiveX 控件无法利用这些安全性增强。  运行 ActiveX 控件需要非托管代码权限，这种权限是使用 <xref:System.Security.Permissions.SecurityPermissionAttribute.UnmanagedCode%2A?displayProperty=fullName> 属性设置的。  有关安全性和非托管代码权限的更多信息，请参见 [SecurityPermissionAttribute 类](frlrfSystemSecurityPermissionsSecurityPermissionAttributeClassTopic)。  
  
-   **总拥有成本** 添加到 Windows 窗体的 ActiveX 控件将作为一个整体部署到该 Windows 窗体中，这会显著增加所创建文件的大小。  另外，在 Windows 窗体上使用 ActiveX 控件要求写入注册表。  与不要求这样做的 Windows 窗体控件相比，ActiveX 控件对用户的计算机更具有侵略性。  
  
    > [!NOTE]
    >  使用 ActiveX 控件时需要使用 COM 互操作包装。  有关更多信息，请参见 [Visual Basic 和 Visual C\# 中的 COM 互操作性](../Topic/COM%20Interoperability%20in%20.NET%20Framework%20Applications%20\(Visual%20Basic\).md)。  
  
    > [!NOTE]
    >  如果 ActiveX 控件的某个成员名与 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 中定义的某一名称匹配，则 ActiveX 控件导入程序在创建 <xref:System.Windows.Forms.AxHost> 派生类时会在该成员名前加上 **Ctl** 前缀。  例如，如果 ActiveX 控件有一个名为 **Layout** 的成员，由于 **Layout** 事件已在 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 中定义，所以该成员将在 AxHost 派生类中重命名为 **CtlLayout**。  
  
## 请参阅  
 [如何：向 Windows 窗体添加 ActiveX 控件](../../../../docs/framework/winforms/controls/how-to-add-activex-controls-to-windows-forms.md)   
 [代码访问安全性](../../../../docs/framework/misc/code-access-security.md)   
 [Controls and Programmable Objects Compared in Various Languages and Libraries](http://msdn.microsoft.com/zh-cn/021f2a1b-8247-4348-a5ad-e1d9ab23004b)   
 [将控件放在 Windows 窗体上](../../../../docs/framework/winforms/controls/putting-controls-on-windows-forms.md)   
 [Windows 窗体控件](../../../../docs/framework/winforms/controls/index.md)