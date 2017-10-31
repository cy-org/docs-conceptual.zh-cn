---
title: "如何：创建简单绑定 | Microsoft Docs"
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
  - "绑定数据, 创建"
  - "Data Binding — 数据绑定, 创建简单绑定"
  - "简单绑定, 创建"
ms.assetid: 69b80f72-6259-44cb-8294-5bdcebca1e08
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：创建简单绑定
此示例演示如何创建简单的 <xref:System.Windows.Data.Binding>。  
  
## 示例  
 在此示例中，假设您具有一个字符串属性名为 `PersonName` 的 `Person` 对象。  `Person` 对象是在名为 `SDKSample` 的命名空间中定义的。  
  
 下面的示例用值为 `Joe` 的 `PersonName` 属性来实例化 `Person` 对象。  这是在 `Resources` 部分中完成的，系统会为该对象分配一个 `x:Key`。  
  
 [!code-xml[SimpleBinding#Instantiation](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Page1.xaml#instantiation)]  
[!code-xml[SimpleBinding#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Page1.xaml#2)]  
[!code-xml[SimpleBinding#EndWindow](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Page1.xaml#endwindow)]  
  
 若要绑定到 `PersonName` 属性，需要执行以下操作：  
  
 [!code-xml[SimpleBinding#BDO1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Page1.xaml#bdo1)]  
  
 其结果是，<xref:System.Windows.Controls.TextBlock> 将显示值“Joe”。  
  
## 请参阅  
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)