---
title: "区域性对在 Visual Basic 中的字符串的影响 |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- locale, effect on strings
- strings [Visual Basic], locale dependence
ms.assetid: c4664444-ee0d-47bf-bef1-eaa3c54bdd7f
caps.latest.revision: 20
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
ms.openlocfilehash: 63228a40897b29d0324be73ca1a17bcb19af2a16
ms.lasthandoff: 03/13/2017

---
# <a name="how-culture-affects-strings-in-visual-basic"></a>区域性对字符串的影响 (Visual Basic)
此帮助页讨论如何[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]使用区域性信息来执行字符串转换和比较。  
  
## <a name="when-to-use-culture-specific-strings"></a>何时使用特定于区域性的字符串  
 通常情况下，应使用特定于区域性的字符串的所有数据呈现给和阅读来自用户，并对应用程序的内部数据使用固定区域性的字符串。  
  
 例如，如果您的应用程序要求用户输入日期作为字符串，它应指望用户能以根据其区域性的字符串设置格式和应用程序应适当地转换字符串。 如果您的应用程序然后显示该日期在其用户界面，它应该存在它在用户的区域性。  
  
 但是，如果应用程序上载到中心服务器的日期，它应格式根据某个特定的区域性，以防止混淆之间可能不同的日期格式字符串。  
  
## <a name="culture-sensitive-functions"></a>区分区域性的函数  
 所有[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]字符串转换函数 (除`Str`和`Val`函数) 使用应用程序的区域性信息以确保转换和比较适合于应用程序的用户的区域性。  
  
 在具有不同的区域性设置的计算机运行的应用程序中使用字符串转换函数成功的关键是了解哪个函数将使用特定的区域性设置，并使用当前区域性设置。 请注意，应用程序的区域性设置，默认情况下，继承的操作系统的区域性设置。 有关详细信息，请参阅<xref:Microsoft.VisualBasic.Strings.Asc%2A>， <xref:Microsoft.VisualBasic.Strings.AscW%2A>， <xref:Microsoft.VisualBasic.Strings.Chr%2A>， <xref:Microsoft.VisualBasic.Strings.ChrW%2A>， <xref:Microsoft.VisualBasic.Strings.Format%2A>， <xref:Microsoft.VisualBasic.Conversion.Hex%2A>， <xref:Microsoft.VisualBasic.Conversion.Oct%2A>，和[类型转换函数](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)。</xref:Microsoft.VisualBasic.Conversion.Oct%2A> </xref:Microsoft.VisualBasic.Conversion.Hex%2A> </xref:Microsoft.VisualBasic.Strings.Format%2A> </xref:Microsoft.VisualBasic.Strings.ChrW%2A> </xref:Microsoft.VisualBasic.Strings.Chr%2A> </xref:Microsoft.VisualBasic.Strings.AscW%2A> </xref:Microsoft.VisualBasic.Strings.Asc%2A>  
  
 `Str` （将数字转换为字符串） 和`Val`（将字符串转换为数字） 函数在字符串和数字之间进行转换时不使用应用程序的区域性信息。 相反，它们将句点 （.） 识别为有效的小数分隔符。 可识别区域性的这些函数是︰  
  
-   **使用当前区域性的转换。** `CStr`和`Format`函数将数字转换为一个字符串，并且`CDbl`和`CInt`函数将字符串转换为数字。  
  
-   **使用特定区域性的转换。** 每个数字的对象都有`ToString(IFormatProvider)`方法，将数字转换为一个字符串，和一个`Parse(String, IFormatProvider)`将字符串转换为数字的方法。 例如，`Double`类型提供了<xref:System.Double.ToString%28System.IFormatProvider%29>和<xref:System.Double.Parse%28System.String%2CSystem.IFormatProvider%29>方法。</xref:System.Double.Parse%28System.String%2CSystem.IFormatProvider%29> </xref:System.Double.ToString%28System.IFormatProvider%29>  
  
 有关详细信息，请参阅<xref:Microsoft.VisualBasic.Conversion.Str%2A>和<xref:Microsoft.VisualBasic.Conversion.Val%2A>。</xref:Microsoft.VisualBasic.Conversion.Val%2A> </xref:Microsoft.VisualBasic.Conversion.Str%2A>  
  
## <a name="using-a-specific-culture"></a>使用非特定区域性  
 假设您正在开发的应用程序向 Web 服务发送日期 （格式为字符串）。 在这种情况下，您的应用程序必须使用特定区域性的字符串转换。 为了说明原因，请考虑使用的日期的结果<xref:System.DateTime.ToString>方法︰ 如果您的应用程序使用该方法来格式化日期 2005 年 7 月 4 日，它将返回"2005 年 7 月 4 日 12:00:00 AM"与美国英语 (EN-US) 区域性中，运行时，但它将返回"04.07.2005 00:00:00"德语 (DE-DE) 区域性与运行时。</xref:System.DateTime.ToString>  
  
 如果您需要执行特定区域性的格式的字符串转换，您应使用`CultureInfo`类内置于[!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)]。 您可以创建一个新`CultureInfo`针对特定区域性的区域性将名称传递到由对象<xref:System.Globalization.CultureInfo.%23ctor%2A>构造函数。</xref:System.Globalization.CultureInfo.%23ctor%2A> 支持的区域性名称列在<xref:System.Globalization.CultureInfo>类帮助页。</xref:System.Globalization.CultureInfo>  
  
 或者，您可以获取其实例*固定区域性*从<xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>属性。</xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName> 固定区域性基于英语区域性中，但有一些差异。 例如，固定区域性指定而不是以 12 小时时钟制采用 24 小时制。  
  
 若要将日期转换为区域性的字符串，将传递<xref:System.Globalization.CultureInfo>对象传递给 date 对象<xref:System.DateTime.ToString%28System.IFormatProvider%29>方法。</xref:System.DateTime.ToString%28System.IFormatProvider%29> </xref:System.Globalization.CultureInfo> 例如，下面的代码显示"07/04/2005年 00:00:00"，而不考虑应用程序的区域性设置。  
  
 [!code-vb[VbVbalrConcepts #&1;](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/codesnippet/VisualBasic/how-culture-affects-strings_1.vb)]  
  
> [!NOTE]
>  Date 文本始终解释取决于英语区域性设置中。  
  
## <a name="comparing-strings"></a>比较字符串  
 有两种重要的情况下需要字符串比较的位置︰  
  
-   **向用户显示的数据进行排序。** 使用基于当前区域性，因此字符串正确排序操作。  
  
-   **确定是否两个应用程序内部字符串完全匹配 （通常出于安全目的）。** 使用忽略当前区域性的操作。  
  
 您还可以使用的比较这两种类型[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]<xref:Microsoft.VisualBasic.Strings.StrComp%2A>函数。</xref:Microsoft.VisualBasic.Strings.StrComp%2A> 指定可选`Compare`参数控制比较的类型︰`Text`对于大多数输入和输出`Binary`用于确定完全匹配项。  
  
 `StrComp`函数将返回一个整数，指示在排序顺序基于比较的两个字符串之间的关系。 结果为正值指示第一个字符串大于第二个字符串。 产生负数结果指示第一个字符串较小，而零表示的字符串之间的相等性。  
  
 [!code-vb[VbVbalrStrings #&22;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-culture-affects-strings_2.vb)]  
  
 您还可以使用[!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)]合作伙伴`StrComp`函数，<xref:System.String.Compare%2A?displayProperty=fullName>方法。</xref:System.String.Compare%2A?displayProperty=fullName> 这是 base 字符串类的静态，重载方法。 下面的示例演示如何使用此方法︰  
  
 [!code-vb[VbVbalrStrings #&48;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/how-culture-affects-strings_3.vb)]  
  
 对于更好地控制如何执行比较，你可以使用的其他重载<xref:System.String.Compare%2A>方法。</xref:System.String.Compare%2A> 与<xref:System.String.Compare%2A?displayProperty=fullName>方法，则可以使用`comparisonType`参数指定要使用的比较的类型。</xref:System.String.Compare%2A?displayProperty=fullName>  
  
|值`comparisonType`参数|比较类型|何时使用|  
|---|---|---|  
|`Ordinal`|基于字符串的组成部分字节数进行比较。|在比较时使用此值︰ 区分大小写的标识符、 与安全相关设置或字节必须完全匹配其他非语言标识符。|  
|`OrdinalIgnoreCase`|基于字符串的组成部分字节数进行比较。<br /><br /> `OrdinalIgnoreCase`使用固定区域性信息来确定何时仅在大小写不同的两个字符。|在比较时使用此值︰ 不区分大小写的标识符、 与安全相关的设置和存储在 Windows 中的数据。|  
|`CurrentCulture` 或 `CurrentCultureIgnoreCase`|基于字符串的解读在当前区域性的比较。|比较时使用这些值︰ 显示给用户，大多数用户输入，以及需要语言学解读的其他数据的数据。|  
|`InvariantCulture` 或 `InvariantCultureIgnoreCase`|基于字符串的解读中固定区域性的比较。<br /><br /> 这一点不同于`Ordinal`和`OrdinalIgnoreCase`，这是因为固定区域性将其接受范围外的字符视为等效的固定字符。|仅当比较持久数据或显示与语言相关的数据需要固定的排序顺序，请使用这些值。|  
  
### <a name="security-considerations"></a>安全注意事项  
 如果您的应用程序做出安全决策基于比较或大小写更改操作的结果，则该操作应该使用<xref:System.String.Compare%2A?displayProperty=fullName>方法，并传递`Ordinal`或`OrdinalIgnoreCase`为`comparisonType`参数。</xref:System.String.Compare%2A?displayProperty=fullName>  
  
## <a name="see-also"></a>请参见  
 <xref:System.Globalization.CultureInfo></xref:System.Globalization.CultureInfo>   
 [在 Visual Basic 中字符串的简介](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)   
 [类型转换函数](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)
