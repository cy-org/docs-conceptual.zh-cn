---
title: "Mid 语句 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.MidB
- vb.Mid
dev_langs:
- VB
helpviewer_keywords:
- substrings, Mid statement
- strings [Visual Basic], substrings
- Mid statement
- strings [Visual Basic], replacing
ms.assetid: 2b82d7a8-9646-4cb0-bec5-80abc98297bf
caps.latest.revision: 20
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e385d6838daa16d45903c6b270fc47ad88797845
ms.lasthandoff: 03/13/2017

---
# <a name="mid-statement"></a>Mid 语句
替换中的字符数目为指定的数目`String`变量与另一个字符串中的字符。  
  
## <a name="syntax"></a>语法  
  
```  
Mid( _  
   ByRef Target As String, _  
   ByVal Start As Integer, _  
   Optional ByVal Length As Integer _  
) = StringExpression  
```  
  
## <a name="parts"></a>部件  
 `Target`  
 必需。 名称`String`变量来修改。  
  
 `Start`  
 必需。 `Integer`表达式。 字符位置`Target`替换文本的开始位置。 `Start`使用从&1; 开始的索引。  
  
 `Length`  
 可选。 `Integer`表达式。 要替换的字符数。 如果省略，所有`String`使用。  
  
 `StringExpression`  
 必需。 `String`替换的一部分的表达式`Target`。  
  
## <a name="exceptions"></a>异常  
  
|异常类型|条件|  
|--------------------|---------------|  
|<xref:System.ArgumentException></xref:System.ArgumentException>|`Start`<= 0="" or=""></=>`Length`< 0.></ 0.>|  
  
## <a name="remarks"></a>备注  
 替换的字符数是始终小于或等于中的字符数`Target`。  
  
 Visual Basic 具有<xref:Microsoft.VisualBasic.Strings.Mid%2A>函数和一个`Mid`语句。</xref:Microsoft.VisualBasic.Strings.Mid%2A> 这些元素都指定数量的字符在字符串中，操作但`Mid`函数将返回字符，而`Mid`语句替换字符。 有关详细信息，请参阅<xref:Microsoft.VisualBasic.Strings.Mid%2A>。</xref:Microsoft.VisualBasic.Strings.Mid%2A>  
  
> [!NOTE]
>  `MidB`的早期版本的 Visual Basic 语句替换中字节，而不是字符的子字符串。 它主要用于在双字节字符集 (DBCS) 应用程序中转换字符串。 所有 Visual Basic 字符串都并以 unicode 格式，并`MidB`不再受支持。  
  
## <a name="example"></a>示例  
 此示例使用`Mid`语句，以将指定的数目的字符串变量中的字符替换为另一个字符串中的字符。  
  
 [!code-vb[VbVbalrStrings #&5;](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/mid-statement_1.vb)]  
  
## <a name="requirements"></a>要求  
 **Namespace:** [Microsoft.VisualBasic](../../../visual-basic/language-reference/runtime-library-members.md)  
  
 **模块︰**`Strings`  
  
 **程序集︰**[!INCLUDE[vbprvbruntime](../../../visual-basic/language-reference/objects/includes/vbprvbruntime_md.md)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.VisualBasic.Strings.Mid%2A></xref:Microsoft.VisualBasic.Strings.Mid%2A>   
 [字符串](../../../visual-basic/programming-guide/language-features/strings/index.md)   
 [在 Visual Basic 中字符串的简介](../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)
