---
title: "在 Visual Basic 中访问 XML |Microsoft 文档"
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
- LINQ to XML [Visual Basic], accessing XML
- Visual Basic code, XML
- accessing XML [Visual Basic], axis properties
- XML [Visual Basic], axis properties
- XML [Visual Basic], accessing
ms.assetid: c47f88b2-3cbc-4bb1-b4b9-be60f71ffc6a
caps.latest.revision: 18
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
ms.openlocfilehash: 215f057f0b4d884369aad53cbbdbb98f240b56c4
ms.lasthandoff: 03/13/2017

---
# <a name="accessing-xml-in-visual-basic"></a>在 Visual Basic 中访问 XML
[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]提供用于访问和导航 XML 轴属性[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]结构。 这些属性使用特殊语法来使您能够通过指定的 XML 名称来访问元素和属性。  
  
 下表列出了可用于访问 XML 元素和属性中的语言功能[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]。  
  
### <a name="xml-axis-properties"></a>XML 轴属性  
  
|属性说明|示例|说明|  
|--------------------------|-------------|-----------------|  
|*子轴*|`contact.<phone>`|获取所有`phone`元素属于的子元素`contact`元素。|  
|*attribute 轴*|`phone.@type`|获取所有`type`属性`phone`元素。|  
|*子代轴*|`contacts...<name>`|获取所有`name`元素`contacts`元素，而不考虑深度顺序层次结构中。|  
|*扩展索引器*|`contacts...<name>(0)`|获取第一个`name`从序列的元素。|  
|*值*|`contacts...<name>.Value`|获取在序列中，第一个对象的字符串表示或`Nothing`如果序列为空。|  
  
## <a name="in-this-section"></a>本节内容  
 [如何：访问 XML 子代元素](../../../../visual-basic/programming-guide/language-features/xml/how-to-access-xml-descendant-elements.md)  
 演示如何使用子代轴属性来访问所有 XML 元素具有指定的名称并且包含在指定的 XML 元素之下。  
  
 [如何：访问 XML 子元素](../../../../visual-basic/programming-guide/language-features/xml/how-to-access-xml-child-elements.md)  
 演示如何使用子轴属性来访问在一个 XML 元素具有指定的名称的所有 XML 子元素。  
  
 [如何：访问 XML 特性](../../../../visual-basic/programming-guide/language-features/xml/how-to-access-xml-attributes.md)  
 演示如何使用特性轴属性来访问在一个 XML 元素具有指定的名称的所有 XML 特性。  
  
 [如何：声明和使用 XML 命名空间前缀](../../../../visual-basic/programming-guide/language-features/xml/how-to-declare-and-use-xml-namespace-prefixes.md)  
 演示如何声明 XML 命名空间前缀，并使用它来创建和访问 XML 元素。  
  
## <a name="related-sections"></a>相关章节  
 [XML 轴属性](../../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)  
 提供指向介绍各种 XML 访问属性的章节。  
  
 [LINQ to XML 在 Visual Basic 中的概述](../../../../visual-basic/programming-guide/language-features/xml/overview-of-linq-to-xml.md)  
 提供介绍如何使用[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]在 Visual Basic 中。  
  
 [在 Visual Basic 中创建 XML](../../../../visual-basic/programming-guide/language-features/xml/creating-xml.md)  
 提供介绍如何在 Visual Basic 中使用 XML 文本。  
  
 [在 Visual Basic 中操作 XML](../../../../visual-basic/programming-guide/language-features/xml/manipulating-xml.md)  
 提供有关加载和修改 Visual Basic 中的 XML 部分的链接。  
  
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)  
 提供指向介绍如何使用章节[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]在 Visual Basic 中。
