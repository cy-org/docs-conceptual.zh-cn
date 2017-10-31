---
title: "在 Visual Basic 中 MaskedTextBox 控件中使用正则表达式 |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- strings [Visual Basic], regular expressions
- strings [Visual Basic], masked edit
ms.assetid: 2a048fb0-7053-487d-b2c5-ffa5e22ed6f9
caps.latest.revision: 10
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 15d8f131aa834321fcf7e8ca633929385c666e6a
ms.lasthandoff: 03/13/2017

---
# <a name="using-regular-expressions-with-the-maskedtextbox-control-in-visual-basic"></a>在 MaskedTextBox 控件中使用正则表达式 (Visual Basic)
此示例演示如何转换简单的正则表达式，以使用<xref:System.Windows.Forms.MaskedTextBox>控件。</xref:System.Windows.Forms.MaskedTextBox>  
  
## <a name="description-of-the-masking-language"></a>掩码语言的说明  
 标准<xref:System.Windows.Forms.MaskedTextBox>掩码语言取决于使用的`Masked Edit`控制[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]6.0 应该熟悉该平台中迁移的用户。</xref:System.Windows.Forms.MaskedTextBox>  
  
 <xref:System.Windows.Forms.MaskedTextBox.Mask%2A>属性<xref:System.Windows.Forms.MaskedTextBox>控件指定要使用哪些输入的掩码。</xref:System.Windows.Forms.MaskedTextBox> </xref:System.Windows.Forms.MaskedTextBox.Mask%2A> 掩码必须是一个或多个从下表中的屏蔽元素构成的字符串。  
  
|屏蔽元素|描述|正则表达式元素|  
|---------------------|-----------------|--------------------------------|  
|0|0 到 9 之间的任何单个数字。 所需的项。|\d|  
|9|数字或空格。 可选的输入。|[ \d]?|  
|#|数字或空格。 可选的输入。 如果此位置为空掩码中，它将呈现为一个空格。 加号 （+） 和减号 （-） 允许符号。|[ \d+-]?|  
|L|ASCII 字母。 所需的项。|[-zA-A-z]|  
|?|ASCII 字母。 可选的输入。|[-zA-A-z]？|  
|&|字符。 所需的项。|[\p{Ll}\p{Lu}\p{Lt}\p{Lm}\p{Lo}]|  
|C|字符。 可选的输入。|[\p{Ll}\p{Lu}\p{Lt}\p{Lm}\p{Lo}]？|  
|包含当前请求的 URL 的|字母数字。 可选的输入。|\W|  
|。|相应于区域性的小数点占位符。|不可用。|  
|,|相应的区域性的千位占位符。|不可用。|  
|:|相应于区域性的时间分隔符。|不可用。|  
|/|相应于区域性的日期分隔符。|不可用。|  
|$|相应于区域性的货币符号。|不可用。|  
|\<|将转换为小写后面的所有字符。|不可用。|  
|>|将转换为大写后面的所有字符。|不可用。|  
|&#124;|撤消上一个班次向上或向下移动。|不可用。|  
|\|掩码字符，将其转变为文字进行转义。 "\\\\"是一个反斜杠的转义序列。|\|  
|所有其他字符。|原义字符。 所有非掩码元素将显示为自身内<xref:System.Windows.Forms.MaskedTextBox>。</xref:System.Windows.Forms.MaskedTextBox>|所有其他字符。|  
  
 小数点 （.），千分位 （，）、 时间 （:）、 （/）、 日期和货币 （$） 符号默认为显示这些符号由应用程序的区域性。 您可以强制其使用显示用于另一个区域性的符号<xref:System.Windows.Forms.MaskedTextBox.FormatProvider%2A>属性。</xref:System.Windows.Forms.MaskedTextBox.FormatProvider%2A>  
  
## <a name="regular-expressions-and-masks"></a>正则表达式和蒙板  
 尽管可以使用正则表达式和蒙板来验证用户输入，但它们并不完全相同。 正则表达式可以表示掩码，相比更复杂的模式，但更简洁地采用与区域相关的格式掩码可以表达相同的信息。  
  
 下表比较了每个四个正则表达式和等效的掩码。  
  
|正则表达式|掩码|备注|  
|------------------------|----------|-----------|  
|`\d{2}/\d{2}/\d{4}`|`00/00/0000`|`/`掩码中的字符是逻辑日期分隔符，并且它将向用户显示适合于应用程序的当前区域性的日期分隔符。|  
|`\d{2}-[A-Z][a-z]{2}-\d{4}`|`00->L<LL-0000`|在其中三个字母月份的缩写显示为首字母大写、 两个小写字母后跟与美国格式的日期 （日、 月缩写和年）。|  
|`(\(\d{3}\)-)?\d{3}-d{4}`|`(999)-000-0000`|美国电话号码，区号为可选项。 如果用户不希望输入的可选字符，她可以输入空格，或将鼠标指针放直接由第一个 0 表示掩码中的位置。|  
|`$\d{6}.00`|`$999,999.00`|0 到 999999 的范围中的货币值。 货币、 千分位和十进制字符将替换在运行时它们特定于区域性的等效项。|  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Windows.Forms.MaskedTextBox.Mask%2A></xref:System.Windows.Forms.MaskedTextBox.Mask%2A>   
 <xref:System.Windows.Forms.MaskedTextBox></xref:System.Windows.Forms.MaskedTextBox>   
 [验证在 Visual Basic 中的字符串](../../../../visual-basic/programming-guide/language-features/strings/validating-strings.md)   
 [MaskedTextBox 控件](http://msdn.microsoft.com/library/235d6121-027d-481d-8d59-4f6794d15d0c)
