---
title: "从零开始的 vs。在 Visual Basic 中的基于&1; 的字符串访问 |Microsoft 文档"
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
- strings [Visual Basic], indexing
ms.assetid: 0ed39f35-d68e-421d-ae14-460a5c0373b8
caps.latest.revision: 11
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
ms.openlocfilehash: 6cd2cab888bf336151ed26968119431f4ffc75f4
ms.lasthandoff: 03/13/2017

---
# <a name="zero-based-vs-one-based-string-access-in-visual-basic"></a>从零开始的 vs。在 Visual Basic 中的基于&1; 的字符串访问
本主题将比较如何[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]和[!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)]提供对字符串中字符的访问。 [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)]始终提供了对字符串中字符的从零开始访问，而[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]提供从零开始的和基于&1; 的访问权限，具体取决于该函数。  
  
## <a name="one-based"></a>基于&1; 的  
 为举例说明如何从一开始[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]函数，请考虑`Mid`函数。 它采用了参数，该值指示子字符串开始，从位置 1 开始的字符位置。 [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] <xref:System.String.Substring%2A?displayProperty=fullName>方法采用字符的索引处的子字符串将启动的字符串中从位置 0 开始。</xref:System.String.Substring%2A?displayProperty=fullName> 因此，如果您有一个字符串"ABCDE"，单个字符进行编号用于 1,2,3,4,5`Mid`函数，但适用于 0,1,2,3,4<xref:System.String.Substring%2A?displayProperty=fullName>方法。</xref:System.String.Substring%2A?displayProperty=fullName>  
  
## <a name="zero-based"></a>从零开始  
 有关从零开始的示例[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]函数，请考虑`Split`函数。 它将字符串拆分，并返回一个数组，包含子字符串。 [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] <xref:System.String.Split%2A?displayProperty=fullName>方法还将字符串拆分，并返回一个数组，包含子字符串。</xref:System.String.Split%2A?displayProperty=fullName> 因为`Split`函数和<xref:System.String.Split%2A>方法将返回[!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)]的数组，它们必须是从零开始。</xref:System.String.Split%2A>  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualBasic.Strings.Mid%2A></xref:Microsoft.VisualBasic.Strings.Mid%2A>   
 <xref:Microsoft.VisualBasic.Strings.Split%2A></xref:Microsoft.VisualBasic.Strings.Split%2A>   
 <xref:System.String.Substring%2A></xref:System.String.Substring%2A>   
 <xref:System.String.Split%2A></xref:System.String.Split%2A>   
 [在 Visual Basic 中字符串的简介](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)
