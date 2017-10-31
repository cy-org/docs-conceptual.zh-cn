---
title: "Windows 窗体中的更加安全的打印 | Microsoft Docs"
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
  - "打印 [Windows 窗体], 安全性"
  - "PrintingPermission 类, Windows 窗体安全"
  - "安全性 [Windows 窗体], 打印"
  - "Windows 窗体, 打印"
ms.assetid: 48fd36ac-872f-4de0-902a-e52969cd4367
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Windows 窗体中的更加安全的打印
Windows 窗体应用程序中通常包括打印功能。  [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 使用 <xref:System.Drawing.Printing.PrintingPermission> 类控制对打印功能的访问，并使用相关联的 <xref:System.Drawing.Printing.PrintingPermissionLevel> 枚举值指示访问级别。  默认情况下，在“本地 Intranet”和“Internet”区域中将启用打印功能；但是，这两个区域中都限定了访问级别。  根据所授予的权限值，应用程序可能在打印时需要用户交互，或者根本无法打印。  默认情况下，“本地 Intranet”区域接收 <xref:System.Drawing.Printing.PrintingPermissionLevel> 访问，而“Intranet”区域接收 <xref:System.Drawing.Printing.PrintingPermissionLevel> 访问。  
  
 下表显示了在每个打印权限级别上可用的功能。  
  
|PrintingPermissionLevel|说明|  
|-----------------------------|--------|  
|<xref:System.Drawing.Printing.PrintingPermissionLevel>|提供对所有已安装打印机的完全访问权限。|  
|<xref:System.Drawing.Printing.PrintingPermissionLevel>|启用到默认打印机的编程打印并通过限制性打印对话框启用更安全的打印。  <xref:System.Drawing.Printing.PrintingPermissionLevel> 是 <xref:System.Drawing.Printing.PrintingPermissionLevel> 的子集。|  
|<xref:System.Drawing.Printing.PrintingPermissionLevel>|仅允许从受更多限制的对话框中提供打印。  <xref:System.Drawing.Printing.PrintingPermissionLevel> 是 <xref:System.Drawing.Printing.PrintingPermissionLevel> 的子集。|  
|<xref:System.Drawing.Printing.PrintingPermissionLevel>|禁止对打印机的访问。  <xref:System.Drawing.Printing.PrintingPermissionLevel> 是 <xref:System.Drawing.Printing.PrintingPermissionLevel> 的子集。|  
  
## 请参阅  
 [Windows 窗体中更加安全的文件和数据访问](../../../docs/framework/winforms/more-secure-file-and-data-access-in-windows-forms.md)   
 [Windows 窗体中额外的安全注意事项](../../../docs/framework/winforms/additional-security-considerations-in-windows-forms.md)   
 [Windows 窗体中的安全性概述](../../../docs/framework/winforms/security-in-windows-forms-overview.md)   
 [Windows 窗体安全](../../../docs/framework/winforms/windows-forms-security.md)