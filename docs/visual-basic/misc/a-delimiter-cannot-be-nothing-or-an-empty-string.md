---
title: "分隔符不能为 Nothing 或空字符串 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrTextFieldParser_DelimiterNothing"
ms.assetid: 8885fcd1-c201-409d-9a32-6ff2b13c0c13
caps.latest.revision: 7
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# 分隔符不能为 Nothing 或空字符串
`TextFieldParser` 无法读取文件，因为 `Delimiters` 属性被设置为 `Nothing` 或为空 `String` \(""\)。  
  
### 更正此错误  
  
-   提供 `Delimiters` 的有效值。  
  
## 请参阅  
 [TextFieldParser.SetDelimiters 方法](http://msdn.microsoft.com/zh-cn/21fa40ec-5866-4d0e-9fd9-c708a190dcc9)   
 [TextFieldParser.Delimiters 属性](http://msdn.microsoft.com/zh-cn/4eb18f4d-3011-40a9-b668-be93eed0444f)   
 [如何：读取逗号分隔的文本文件](../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-comma-delimited-text-files.md)   
 [TextFieldParser 对象](../../visual-basic/language-reference/objects/textfieldparser-object.md)   
 [使用 TextFieldParser 对象分析文本文件](../../visual-basic/developing-apps/programming/drives-directories-files/parsing-text-files-with-the-textfieldparser-object.md)