---
title: "TextFieldParser 不支持包含空格的注释标记 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrTextFieldParser_WhitespaceInToken"
ms.assetid: 55107656-270e-4bbb-841a-478904df8e07
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# TextFieldParser 不支持包含空格的注释标记
提供了包含空格的注释标记。`TextFieldParser` 不支持包含空格的注释标记，除非空格出现在标记的开头。 出现在标记开头的空格将被忽略。  
  
### 更正此错误  
  
-   提供正确的注释标记。  
  
## 请参阅  
 [TextFieldParser.CommentTokens 属性](http://msdn.microsoft.com/zh-cn/2e6b6435-4bee-4c14-a353-e8f2c82e2d61)   
 [使用 TextFieldParser 对象分析文本文件](../../visual-basic/developing-apps/programming/drives-directories-files/parsing-text-files-with-the-textfieldparser-object.md)   
 [TextFieldParser 对象](../../visual-basic/language-reference/objects/textfieldparser-object.md)