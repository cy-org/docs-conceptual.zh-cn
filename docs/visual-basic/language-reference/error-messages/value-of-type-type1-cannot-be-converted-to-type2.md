---
title: "类型“type1”的值无法转换为“type2” | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc31194"
  - "bc31194"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC31194"
ms.assetid: 03d50c31-addd-4c90-9c53-725b84f9782e
caps.latest.revision: 5
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 5
---
# 类型“type1”的值无法转换为“type2”
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

类型“type1”的值无法转换为“type2”。可以使用“Value”属性获取“\<parentElement\>”的第一个元素的字符串值。  
  
 已经尝试将 XML 文本隐式强制转换为特定类型。  无法将 XML 文本隐式强制转换为指定的类型。  
  
 **错误 ID：**BC31194  
  
### 更正此错误  
  
-   使用 XML 文本的 `Value` 属性以 `String` 形式引用其值。  使用 `CType` 函数、另一个类型转换函数或 <xref:System.Convert> 类将值强制转换为指定的类型。  
  
## 请参阅  
 <xref:System.Convert>   
 [类型转换函数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [XML 文本](../../../visual-basic/language-reference/xml-literals/index.md)   
 [XML](../../../visual-basic/programming-guide/language-features/xml/index.md)