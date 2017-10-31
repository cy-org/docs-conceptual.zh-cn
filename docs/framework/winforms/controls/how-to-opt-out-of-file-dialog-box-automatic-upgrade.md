---
title: "如何：取消文件对话框自动升级 | Microsoft Docs"
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
  - "选择取消自动升级 OpenFileDialog [Windows 窗体]"
  - "文件对话框 [Windows 窗体] 中，选择取消自动升级"
  - "Windows Vista 文件对话框框中，选择取消自动升级"
  - "选择取消自动升级 SaveFileDialog [Windows 窗体]"
  - "AutoUpgradeEnabled 属性"
ms.assetid: 522e482e-cc01-48b1-8d59-9617dc2c4ac1
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：取消文件对话框自动升级
当<xref:System.Windows.Forms.OpenFileDialog>和<xref:System.Windows.Forms.SaveFileDialog>应用程序中使用类，其外观和行为取决于 Windows 运行该应用程序的版本。 应用程序在创建时[!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)]或前面部分显示在[!INCLUDE[wiprlhext](../../../../includes/wiprlhext-md.md)]， <xref:System.Windows.Forms.OpenFileDialog>和<xref:System.Windows.Forms.SaveFileDialog>自动显示与[!INCLUDE[wiprlhext](../../../../includes/wiprlhext-md.md)]外观和行为。 在启动[!INCLUDE[net_v30_short](../../../../includes/net-v30-short-md.md)]，您可以选择不自动升级，以便显示<xref:System.Windows.Forms.OpenFileDialog>和<xref:System.Windows.Forms.SaveFileDialog>与[!INCLUDE[winxp](../../../../includes/winxp-md.md)]-风格的外观和行为。  
  
### <a name="to-opt-out-of-file-dialog-box-automatic-upgrade"></a>选择不使用文件对话框自动升级  
  
1.  设置<xref:System.Windows.Forms.FileDialog.AutoUpgradeEnabled%2A>属性<xref:System.Windows.Forms.OpenFileDialog>或<xref:System.Windows.Forms.SaveFileDialog>到`false`然后才能显示对话框。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Windows.Forms.FileDialog>