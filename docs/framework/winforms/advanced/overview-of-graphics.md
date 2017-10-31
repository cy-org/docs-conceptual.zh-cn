---
title: "图形概述 | Microsoft Docs"
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
  - "图形, 关于图形"
  - "图形, 使用托管接口"
ms.assetid: a602aef8-a8c8-4c36-9816-74e7bad96a68
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 图形概述
[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 是构成 Microsoft Windows 操作系统子系统的应用程序编程接口 \(API\)。[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 负责在屏幕和打印机上显示信息。  顾名思义，[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 是 [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] 的后续，后者是包含在 Windows 早期版本中的图形设备接口。  
  
## 托管类接口  
 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] API 通过一组部署为托管代码的类公开。  这组类被称为 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 的*托管类接口*。  以下命名空间构成托管类接口：  
  
-   <xref:System.Drawing>  
  
-   <xref:System.Drawing.Drawing2D>  
  
-   <xref:System.Drawing.Imaging>  
  
-   <xref:System.Drawing.Text>  
  
-   <xref:System.Drawing.Printing>  
  
 使用图形设备接口（如 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)]），可以在屏幕或打印机上显示信息，而无需顾虑特定显示设备的详细信息。  程序员调用由 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 类提供的方法。这些方法，反过来，对特定的设备驱动程序进行适当的调用。  [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 使应用程序与图形硬件隔离。正是这种隔离使程序员能够创建独立于设备的应用程序。  
  
## 请参阅  
 [图形概述](../../../../docs/framework/winforms/advanced/graphics-overview-windows-forms.md)