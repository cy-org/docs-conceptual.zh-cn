---
title: "所有字段宽度（除了最后一个元素外）都必须大于零 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbrTextFieldParser_FieldWidthsMustPositive"
ms.assetid: 41d8c661-a749-4c89-be56-905c6e7c3c9d
caps.latest.revision: 7
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# 所有字段宽度（除了最后一个元素外）都必须大于零
所有字段宽度（除了最后一个元素外）都必须大于零。 最后一个元素的字段宽度小于或等于零表示最后一个字段的长度是可变的。  
  
 操作已失败，因为最后一个元素以外的某个字段宽度被设置为等于或小于零。 可将小于或等于零的字段宽度用作最后一个元素以指示最后一个字段的长度可变，但不能将它用作任何其他元素。  
  
### 更正此错误  
  
-   将字段宽度设置为正确的长度。  
  
## 请参阅  
 [TextFieldParser.SetFieldWidths 方法](http://msdn.microsoft.com/zh-cn/958fed9f-e0f3-4fc5-83b4-386156bdf036)   
 [TextFieldParser.FieldWidths 属性](http://msdn.microsoft.com/zh-cn/c6985360-60c6-494e-89e7-43b6b73f2597)   
 [如何：读取固定宽度的文本文件](../../visual-basic/developing-apps/programming/drives-directories-files/how-to-read-from-fixed-width-text-files.md)   
 [TextFieldParser 对象](../../visual-basic/language-reference/objects/textfieldparser-object.md)