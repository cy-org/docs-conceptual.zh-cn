---
title: "表达式具有类型&lt;typename&gt;这是受限的类型，不能用于访问从 Object 或 ValueType 继承的成员 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc31393
- vbc31393
dev_langs:
- VB
helpviewer_keywords:
- BC31393
ms.assetid: 2963cf3f-c527-4aa7-b67c-ee80b6d23186
caps.latest.revision: 6
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
ms.openlocfilehash: aaedfd825889498159f92cbd1d615cc0064973d3
ms.lasthandoff: 03/13/2017

---
# <a name="expression-has-the-type-39lttypenamegt39-which-is-a-restricted-type-and-cannot-be-used-to-access-members-inherited-from-39object39-or-39valuetype39"></a>表达式具有类型&lt;typename&gt;这是受限的类型，不能用于访问从 Object 或 ValueType 继承的成员
一个表达式的计算结果为不能由公共语言运行时 (CLR) 装箱的类型，但访问需要装箱的成员。  
  
 *装箱*将 type 转换为所需的处理是指`Object`或有时，到<xref:System.ValueType>。</xref:System.ValueType> 公共语言运行时不能某些结构类型装箱，例如<xref:System.ArgIterator>， <xref:System.RuntimeArgumentHandle>，和<xref:System.TypedReference>。</xref:System.TypedReference> </xref:System.RuntimeArgumentHandle> </xref:System.ArgIterator>  
  
 此表达式将尝试使用受限制的类型来调用的方法继承自<xref:System.Object>或<xref:System.ValueType>，如<xref:System.Object.GetHashCode%2A>或<xref:System.Object.ToString%2A>。</xref:System.Object.ToString%2A> </xref:System.Object.GetHashCode%2A> </xref:System.ValueType> </xref:System.Object> 若要访问此方法，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]已尝试隐式装箱的转换导致此错误。  
  
 **错误 ID:** BC31393  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
1.  查找计算结果为引用类型的表达式。  
  
2.  找到您尝试从<xref:System.Object><xref:System.ValueType>。</xref:System.ValueType>或</xref:System.Object>继承的方法调用的语句的一部分  
  
3.  重写语句以避免进行方法调用。  
  
## <a name="see-also"></a>另请参阅  
 [隐式转换和显式转换](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
