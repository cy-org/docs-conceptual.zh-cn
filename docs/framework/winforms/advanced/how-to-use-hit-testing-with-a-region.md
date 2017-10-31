---
title: "如何：对区域使用命中测试 | Microsoft Docs"
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
  - "命中测试, 使用区域"
  - "区域, 命中测试"
ms.assetid: 3a4c07cb-a40a-4d14-ad35-008f531910a8
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：对区域使用命中测试
命中检测的目的是确定光标是否位于给定对象（如图标或按钮）上。  
  
## 示例  
 下面的示例通过合并两个矩形区域创建形状为加号的区域。  假设变量  `point`  中保存最近单击过的位置。  该代码查看  `point`  是否位于形状为加号的区域。  如果该点位于该区域（命中），则该区域将用不透明的红色画笔填充。  否则，该区域将用半透明的红色画笔填充。  
  
 [!code-csharp[System.Drawing.MiscLegacyTopics#31](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/CS/Class1.cs#31)]
 [!code-vb[System.Drawing.MiscLegacyTopics#31](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.MiscLegacyTopics/VB/Class1.vb#31)]  
  
## 编译代码  
 前面的示例是为使用 Windows 窗体而设计的，它需要 <xref:System.Windows.Forms.PaintEventHandler> 的参数 <xref:System.Windows.Forms.PaintEventArgs> `e`。  
  
## 请参阅  
 <xref:System.Drawing.Region>   
 [GDI\+ 中的区域](../../../../docs/framework/winforms/advanced/regions-in-gdi.md)   
 [如何：对区域使用剪辑](../../../../docs/framework/winforms/advanced/how-to-use-clipping-with-a-region.md)