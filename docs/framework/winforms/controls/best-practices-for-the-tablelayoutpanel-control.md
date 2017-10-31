---
title: "TableLayoutPanel 控件的最佳做法 | Microsoft Docs"
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
  - "最佳做法, TableLayoutPanel 控件"
  - "控件 [Windows 窗体], 调整大小"
  - "窗体, 最佳做法"
  - "布局 [Windows 窗体]"
  - "布局 [Windows 窗体], 最佳做法"
  - "布局 [Windows 窗体], AutoSize"
  - "调整大小, 自动"
  - "TableLayoutPanel 控件 [Windows 窗体], 最佳做法"
  - "TableLayoutPanel 控件 [Windows 窗体], AutoSize 行为"
ms.assetid: b6706efb-d7a4-45ec-8cf4-08fa993e3afb
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# TableLayoutPanel 控件的最佳做法
<xref:System.Windows.Forms.TableLayoutPanel> 控件提供了强大的布局功能，在 Windows 窗体上使用该控件之前应仔细考虑这些功能。  
  
## 建议  
 下面的建议将帮助您最有效地使用 <xref:System.Windows.Forms.TableLayoutPanel> 控件。  
  
### 目标用法  
 请有选择地使用 <xref:System.Windows.Forms.TableLayoutPanel> 控件。  不应在一切需要可调整大小的布局的情况下都使用该控件。  下面的列表描述了能从 <xref:System.Windows.Forms.TableLayoutPanel> 控件的使用中最大程度获益的布局：  
  
-   在其中窗体的多个部件成比例调整大小的布局。  
  
-   将在运行时动态修改或生成的布局，如根据首选项增减了用户自定义字段的数据输入窗体。  
  
-   应该保持在总体固定大小的布局。  例如，您可能有一个应保持小于 800 x 600 的对话框，但是您需要支持本地化的字符串。  
  
 下面的列表描述了不会从 <xref:System.Windows.Forms.TableLayoutPanel> 控件的使用中获得很大益处的布局：  
  
-   只有一个标签列和一个文本输入区域列的简单数据输入窗体。  
  
-   含有单个较大显示区域的窗体，该显示区域应在调整大小时填充所有可用的空间。  此类窗体的一个示例是显示单个 <xref:System.Windows.Forms.PropertyGrid> 控件的窗体。  在此情况下，请使用锚定，因为在调整窗体大小时不应展开任何其他项。  
  
 认真选择哪些控件需要位于 <xref:System.Windows.Forms.TableLayoutPanel> 控件中。  如果有空间让文本使用锚定增大 30%，请考虑仅使用 <xref:System.Windows.Forms.Control.Anchor%2A> 属性。  如果可以估计布局需要的空间，则使用 <xref:System.Windows.Forms.Control.Dock%2A> 和 <xref:System.Windows.Forms.Control.Anchor%2A> 要比估计剩余空间和 <xref:System.Windows.Forms.Control.AutoSize%2A> 行为的详细信息要容易。  
  
 通常，当使用 <xref:System.Windows.Forms.TableLayoutPanel> 控件设计布局时，请使设计尽可能保持简单。  
  
### 使用“文档大纲”窗口  
 “文档大纲”窗口提供布局的树视图，可以使用该树视图来控制控件的 Z 顺序和父子关系。  从**“视图”**菜单中选择**“其他窗口”**，然后选择**“文档大纲”**。  
  
### 避免嵌套  
 避免在一个 <xref:System.Windows.Forms.TableLayoutPanel> 控件中嵌套其他 <xref:System.Windows.Forms.TableLayoutPanel> 控件。  调试嵌套布局可能比较困难。  
  
### 避免可视化继承  
 在 Windows 窗体设计器中，<xref:System.Windows.Forms.TableLayoutPanel> 控件不支持可视继承。  派生类中的 <xref:System.Windows.Forms.TableLayoutPanel> 控件在设计时显示为“锁定”。  
  
## 请参阅  
 <xref:System.Windows.Forms.TableLayoutPanel>   
 <xref:System.Windows.Forms.FlowLayoutPanel>