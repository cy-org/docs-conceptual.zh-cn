---
title: "TableLayoutPanel 控件中的自动调整大小行为 | Microsoft Docs"
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
  - "自动调整大小"
  - "AutoSize 属性, TableLayoutPanel 控件"
  - "AutoSizeMode 属性"
  - "控件 [Windows 窗体], 调整大小"
  - "布局 [Windows 窗体], AutoSize"
  - "本地化窗体"
  - "调整大小, 自动"
  - "TableLayoutPanel 控件 [Windows 窗体], AutoSize 行为"
ms.assetid: 9233e0c3-2fa6-405e-8701-959479b1250e
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# TableLayoutPanel 控件中的自动调整大小行为
## 各种自动调整大小行为  
 <xref:System.Windows.Forms.TableLayoutPanel> 控件以下面的方式支持自动调整大小行为：  
  
-   通过 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性；  
  
-   通过 <xref:System.Windows.Forms.TableLayoutPanel> 控件的列和行样式的 <xref:System.Windows.Forms.TableLayoutStyle.SizeType%2A> 属性。  
  
### 行和列样式的 AutoSize 属性  
 下表描述 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性和 <xref:System.Windows.Forms.TableLayoutPanel> 控件的列和行样式之间的交互。  
  
|AutoSize 设置|样式交互|  
|-----------------|----------|  
|`false`|<xref:System.Windows.Forms.TableLayoutPanel> 控件的方向为从左至右，按下面的顺序为列或行分配空间。<br /><br /> 1.  如果 <xref:System.Windows.Forms.TableLayoutStyle.SizeType%2A> 属性设置为 <xref:System.Windows.Forms.SizeType>，则分配由 <xref:System.Windows.Forms.ColumnStyle.Width%2A> 或 <xref:System.Windows.Forms.RowStyle.Height%2A> 指定的像素数。<br />2.  如果 <xref:System.Windows.Forms.TableLayoutStyle.SizeType%2A> 属性设置为 <xref:System.Windows.Forms.SizeType>，则分配由子控件的 <xref:System.Windows.Forms.Control.GetPreferredSize%2A> 方法返回的像素数。<br />3.  在为具有 <xref:System.Windows.Forms.SizeType> 或 <xref:System.Windows.Forms.SizeType> 值的所有列或行分配空间之后，将使用 <xref:System.Windows.Forms.TableLayoutStyle.SizeType%2A> 设置为 <xref:System.Windows.Forms.SizeType> 的任何列或行按比例分配剩余的可用空间|  
|`true`|与上一交互相似，不同的是具有 <xref:System.Windows.Forms.SizeType> 值的列或行将获取自动调整大小的方位。<br /><br /> <xref:System.Windows.Forms.TableLayoutPanel> 控件对列或行进行扩展以创建足够的可用空间，以便具有 <xref:System.Windows.Forms.SizeType> 样式的列或行都不会剪裁掉其内容。  <xref:System.Windows.Forms.TableLayoutPanel> 控件根据 <xref:System.Windows.Forms.ColumnStyle.Width%2A> 或 <xref:System.Windows.Forms.RowStyle.Height%2A> 属性按比例分配新的空间。|  
  
## 请参阅  
 <xref:System.Windows.Forms.TableLayoutPanel>   
 [TableLayoutPanel 控件概述](../../../../docs/framework/winforms/controls/tablelayoutpanel-control-overview.md)