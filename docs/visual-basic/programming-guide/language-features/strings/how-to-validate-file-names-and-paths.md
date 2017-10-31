---
title: "如何：在 Visual Basic 中验证文件名和路径 | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "布尔值"
  - "文件名, 验证"
  - "路径, 验证"
  - "字符串 [Visual Basic], 验证"
ms.assetid: f673462d-57b7-4120-b13a-6a7592f7ab2c
caps.latest.revision: 7
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# 如何：在 Visual Basic 中验证文件名和路径
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

此示例返回一个 `Boolean` 值，该值指示字符串表示文件名还是路径。  验证操作检查名称是否包含文件系统不允许的字符。  
  
## 示例  
 [!code-vb[VbVbcnRegEx#4](../../../../visual-basic/programming-guide/language-features/strings/codesnippet/VisualBasic/how-to-validate-file-names-and-paths_1.vb)]  
  
 此示例不会检查下列内容：名称中冒号的位置是否不正确、目录是否没有名称，或者名称的长度是否超过了系统定义的最大长度。  也不会检查应用程序是否有访问具有指定名称的文件系统资源的权限。  
  
## 请参阅  
 <xref:System.IO.Path.GetInvalidPathChars%2A>   
 [验证字符串 \(Visual Basic\)](../../../../visual-basic/programming-guide/language-features/strings/validating-strings.md)