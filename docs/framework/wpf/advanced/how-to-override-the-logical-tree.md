---
title: "如何：重写逻辑树 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Logical Tree — 逻辑树, 重写"
  - "重写逻辑树"
ms.assetid: 0ae4d074-8113-4b06-b4fa-e0f39d4967a6
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：重写逻辑树
资深的控件创作者可以选择重写[逻辑树](GTMT)，但这在大多数情况下都不是必需的。  
  
## 示例  
 本示例介绍如何创建 <xref:System.Windows.Controls.StackPanel> 子类以重写逻辑树，在本示例中重写逻辑树是为了强制该面板只能具有并且仅仅呈现一个子元素的行为。  这不一定是实际需要的行为，但在这里进行演示是为了举例说明重写元素的正常逻辑树的情况。  
  
 [!code-csharp[LogicalOverride#SingletonPanel](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LogicalOverride/CSharp/SDKSampleLibrary/class1.cs#singletonpanel)]  
  
 有关逻辑树的更多信息，请参见 [WPF 中的树](../../../../docs/framework/wpf/advanced/trees-in-wpf.md)。