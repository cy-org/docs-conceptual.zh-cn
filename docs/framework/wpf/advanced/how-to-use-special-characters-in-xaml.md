---
title: "如何：在 XAML 中使用特殊字符 | Microsoft Docs"
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
  - "字符, 特殊"
  - "特殊字符"
  - "版式, 特殊字符"
  - "Unicode UTF-8 文件格式"
  - "UTF-8 文件格式"
ms.assetid: a57776d1-f353-4794-afa0-bfa3c712ed1c
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 3
---
# 如何：在 XAML 中使用特殊字符
在 [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] 中创建的标记文件自动以 [!INCLUDE[TLA#tla_unicode](../../../../includes/tlasharptla-unicode-md.md)] UTF\-8 的文件格式保存，这意味着大多数特殊字符（如重音符号）都会正确编码。  不过，有一组常用特殊字符的处理方式有所不同。  这些特殊字符遵循[!INCLUDE[TLA#tla_w3c](../../../../includes/tlasharptla-w3c-md.md)] [!INCLUDE[TLA#tla_xml](../../../../includes/tlasharptla-xml-md.md)] 编码标准。  
  
 下表显示了对这组特殊字符进行编码所用的语法：  
  
|字符|语法|说明|  
|--------|--------|--------|  
|\<|`<`|小于号。|  
|\>|`>`|大于号。|  
|&|`&`|“and”符。|  
|"|`"`|双引号。|  
  
> [!NOTE]
>  如果使用文本编辑器（如 [!INCLUDE[TLA#tla_mswin](../../../../includes/tlasharptla-mswin-md.md)] 记事本）创建标记文件，则必须以 [!INCLUDE[TLA#tla_unicode](../../../../includes/tlasharptla-unicode-md.md)] UTF\-8 文件格式保存文件以保留任何编码的特殊字符。  
  
 下面的示例演示在创建标记时如何在文本中使用特殊字符。  
  
## 示例  
 [!code-xml[SpecialCharsSnippets#SpecialCharsSnippet1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SpecialCharsSnippets/CS/Window1.xaml#specialcharssnippet1)]