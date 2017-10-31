---
title: "无法读取分隔字段，因为当 EscapeQuotes 设置为 True 时，双引号不是合法的分隔符 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrTextFieldParser_IllegalDelimiter"
ms.assetid: ab8a0c3a-b89c-4617-9e31-7e81f5dca433
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# 无法读取分隔字段，因为当 EscapeQuotes 设置为 True 时，双引号不是合法的分隔符
`TextFieldParser` 无法从文件中读取，因为引号 \("\) 以分隔符形式提供，且 `EscapeQuotes` 设置为 `True`。  
  
### 更正此错误  
  
-   将 `EscapeQuotes` 设置为 `False`。  
  
## 请参阅  
 [TextFieldParser.SetDelimiters 方法](http://msdn.microsoft.com/zh-cn/21fa40ec-5866-4d0e-9fd9-c708a190dcc9)   
 [TextFieldParser.Delimiters 属性](http://msdn.microsoft.com/zh-cn/4eb18f4d-3011-40a9-b668-be93eed0444f)   
 [如何：读取逗号分隔的文本文件](../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-comma-delimited-text-files.md)   
 [TextFieldParser 对象](../../visual-basic/language-reference/objects/textfieldparser-object.md)