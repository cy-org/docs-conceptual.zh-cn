---
title: "后期绑定的解决方案;可能会发生运行时错误 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc42017
- BC42017
dev_langs:
- VB
helpviewer_keywords:
- BC42017
ms.assetid: 45f552c8-57c6-44c0-97d3-e510119b257a
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
ms.openlocfilehash: 3ac885b0de2c4f44d4323487fc55cde9b23defa4
ms.lasthandoff: 03/13/2017

---
# <a name="late-bound-resolution-runtime-errors-could-occur"></a>后期绑定解决方案；可能会发生运行时错误
一个对象分配给变量声明为[Object 数据类型](../../../visual-basic/language-reference/data-types/object-data-type.md)。  
  
 当您声明一个变量，作为`Object`，编译器必须执行*后期绑定*，这在运行时将导致额外的操作。 它还使应用程序易于发生潜在的运行时错误。 例如，如果您分配<xref:System.Windows.Forms.Form>到`Object`变量，然后尝试访问<xref:System.Xml.XmlDocument.NameTable%2A?displayProperty=fullName>属性，则运行时会引发<xref:System.MemberAccessException>因为<xref:System.Windows.Forms.Form>类不公开`NameTable`属性。</xref:System.Windows.Forms.Form> </xref:System.MemberAccessException> </xref:System.Xml.XmlDocument.NameTable%2A?displayProperty=fullName> </xref:System.Windows.Forms.Form>  
  
 如果您声明要对特定类型的变量，因此编译器可以执行*早期绑定*在编译时。 这会导致提高性能的受控访问权限的特定类型的成员和更好地提高代码的可读性。  
  
 默认情况下，此消息是一个警告。 有关隐藏警告或将警告视为错误的信息，请参见 [Configuring Warnings in Visual Basic](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID:** BC42017  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   如果可能，请将变量声明为特定类型。  
  
## <a name="see-also"></a>另请参阅  
 [早期绑定和后期绑定](../../../visual-basic/programming-guide/language-features/early-late-binding/index.md)   
 [对象变量声明](../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)
