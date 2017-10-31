---
title: "多文档界面 (MDI) 应用程序 | Microsoft Docs"
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
  - "窗体, MDI"
  - "MDI"
  - "Windows 窗体, MDI 应用程序"
  - "窗口, MDI"
ms.assetid: 599faf75-13cf-49cc-ad3c-255545e5cb97
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 多文档界面 (MDI) 应用程序
多文档界面 \(MDI\) 应用程序使您能同时显示多个文档，每个文档显示在各自的窗口中。  MDI 应用程序中常有包含子菜单的“窗口”菜单项，用于在窗口或文档之间进行切换。  
  
> [!NOTE]
>  MDI 窗体和 Windows 窗体中的单文档界面 \(SDI\) 窗口之间存在一些行为差异。  `Opacity` 属性不影响 MDI 子窗体的外观。  另外，<xref:System.Windows.Forms.Form.CenterToParent%2A> 方法不影响 MDI 子窗体的行为。  
  
## 本节内容  
 [如何：创建 MDI 父窗体](../../../../docs/framework/winforms/advanced/how-to-create-mdi-parent-forms.md)  
 提供有关如何为 MDI 应用程序内的多个文档创建容器的说明。  
  
 [如何：创建 MDI 子窗体](../../../../docs/framework/winforms/advanced/how-to-create-mdi-child-forms.md)  
 给出创建在 MDI 父窗体内操作的一个或多个窗口的说明。  
  
 [如何：确定活动的 MDI 子窗体](../../../../docs/framework/winforms/advanced/how-to-determine-the-active-mdi-child.md)  
 提供有关如何验证具有焦点的子窗口（并将其内容发送到剪贴板）的说明。  
  
 [如何：将数据发送到活动的 MDI 子窗体](../../../../docs/framework/winforms/advanced/how-to-send-data-to-the-active-mdi-child.md)  
 提供有关如何将信息传输到活动子窗口的说明。  
  
 [如何：排列 MDI 子窗体](../../../../docs/framework/winforms/advanced/how-to-arrange-mdi-child-forms.md)  
 提供有关如何平铺、层叠或排列 MDI 应用程序的子窗口的说明。