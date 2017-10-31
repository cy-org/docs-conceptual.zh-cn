---
title: "本地化 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "应用程序开发 [.NET Framework], 本地化"
  - "代码块"
  - "区域性, 本地化"
  - "全局应用程序, 本地化"
  - "全球化 [.NET Framework], 本地化"
  - "国际应用程序 [.NET Framework], 本地化"
  - "本地化 [.NET Framework], 关于本地化"
  - "本地化资源"
  - "用户界面块"
  - "世界通用的应用程序, 本地化"
ms.assetid: 49d520d7-92d7-44ee-bb24-8b615db1d41b
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# 本地化
本地化是针对应用程序支持的每一个区域性将应用程序的资源翻译为本地化版本的过程。  只有在完成了 [本地化评审](../../../docs/standard/globalization-localization/localizability-review.md) 步骤，证实了全球化应用程序可以开始进行本地化之后，才应继续到本地化阶段。  
  
 可以开始进行本地化的应用程序分为两个概念块：一个是包含所有用户界面元素的块，另一个是包含可执行代码的块。  用户界面块仅包含非特定区域性的可本地化用户界面元素，如字符串、错误信息、对话框、菜单、嵌入的对象资源等。  代码块仅包含由所有支持的区域性使用的应用程序代码。  公共语言运行时支持一个附属程序集资源模型，该模型将应用程序的可执行代码同其资源分开。  有关实现此模型的更多信息，请参见 [桌面应用程序中的资源](../../../docs/framework/resources/index.md)。  
  
 要获取应用程序的每个本地化版本，请添加新的附属程序集（包含翻译成适当目标区域性语言的本地化用户界面块）。  所有区域性的代码块应保持相同。  用户界面块的本地化版本与代码块的组合产生应用程序的本地化版本。  
  
 [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)] 提供了 Windows 窗体资源编辑器 \(Winres.exe\)，可使您能够针对目标区域性快速本地化 Windows 窗体。  有关使用此工具的信息，请参见 [Winres.exe（Windows 窗体资源编辑器）](../../../docs/framework/tools/winres-exe-windows-forms-resource-editor.md)。  
  
## 请参阅  
 [全球化和本地化](../../../docs/standard/globalization-localization/index.md)   
 [本地化评审](../../../docs/standard/globalization-localization/localizability-review.md)   
 [全球化](../../../docs/standard/globalization-localization/globalization.md)   
 [桌面应用程序中的资源](../../../docs/framework/resources/index.md)