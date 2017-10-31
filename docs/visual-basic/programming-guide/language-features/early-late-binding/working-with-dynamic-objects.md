---
title: "使用动态对象 (Visual Basic 中) |Microsoft 文档"
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
- dynamic objects [Visual Basic]
ms.assetid: bdee2a00-07ff-46f9-86dd-fdac9b99cc97
caps.latest.revision: 12
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
ms.openlocfilehash: 366b563764baaa39849356a782ecee264b2ae94f
ms.lasthandoff: 03/13/2017

---
# <a name="working-with-dynamic-objects-visual-basic"></a>使用动态对象 (Visual Basic)
动态对象提供另一种方法，而不`Object`类型，在运行时的后期绑定到一个对象。 使用动态中定义的接口在运行时动态对象公开的成员，例如属性和方法<xref:System.Dynamic>命名空间。</xref:System.Dynamic> 可以使用中的类<xref:System.Dynamic>命名空间以产生与静态类型或格式不匹配的数据结构一起处理的对象。</xref:System.Dynamic> 此外可以使用 IronPython 和 IronRuby 等动态语言中定义的动态对象。 有关说明如何创建动态对象或使用动态对象在动态语言中定义的示例，请参阅[演练︰ 创建和使用动态对象](../../../../csharp/programming-guide/types/walkthrough-creating-and-using-dynamic-objects.md)， <xref:System.Dynamic.DynamicObject>，或<xref:System.Dynamic.ExpandoObject>.</xref:System.Dynamic.ExpandoObject> </xref:System.Dynamic.DynamicObject>  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]通过将绑定到对象从动态语言运行时和 IronPython 和 IronRuby 等动态语言使用<xref:System.Dynamic.IDynamicMetaObjectProvider>接口。</xref:System.Dynamic.IDynamicMetaObjectProvider> 类的实现示例`IDynamicMetaObjectProvider`接口都是<xref:System.Dynamic.DynamicObject>和<xref:System.Dynamic.ExpandoObject>类。</xref:System.Dynamic.ExpandoObject> </xref:System.Dynamic.DynamicObject>  
  
 如果实现的对象进行后期绑定调用`IDynamicMetaObjectProvider`接口，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]将绑定到动态对象通过该接口。 如果在对对象没有实现进行后期绑定调用`IDynamicMetaObjectProvider`接口，或者，如果调用`IDynamicMetaObjectProvider`接口失败，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]绑定到对象使用的后期绑定功能[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]运行时。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Dynamic.DynamicObject></xref:System.Dynamic.DynamicObject>   
 <xref:System.Dynamic.ExpandoObject></xref:System.Dynamic.ExpandoObject>   
 [演练︰ 创建和使用动态对象](../../../../csharp/programming-guide/types/walkthrough-creating-and-using-dynamic-objects.md)   
 [早期绑定和后期绑定](../../../../visual-basic/programming-guide/language-features/early-late-binding/index.md)
