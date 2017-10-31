---
title: "类型 &quot;&lt;typename&gt;没有构造函数 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc30251
- vbc30251
dev_langs:
- VB
helpviewer_keywords:
- BC30251
ms.assetid: aff3e1df-abe6-4bc0-9abc-a1e70514c561
caps.latest.revision: 9
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
ms.openlocfilehash: 505e3bbdfa830394efcea7226897ec0d3e6d2b02
ms.lasthandoff: 03/13/2017

---
# <a name="type-39lttypenamegt39-has-no-constructors"></a>类型 '&lt;typename&gt;没有构造函数
某个类型不支持对 `Sub New()` 的调用。 一个可能的原因是编译器或二进制文件被损坏。  
  
 **错误 ID:** BC30251  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
1.  如果该类型位于其他项目或一个引用的文件中，则重新安装此项目或文件。  
  
2.  如果该类型位于同一个项目中，则重新编译包含该类型的程序集。  
  
3.  如果错误重复出现，请重新安装 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 编译器。  
  
4.  如果仍然出现错误，则收集有关该情况的信息并通知 Microsoft 产品支持服务。  
  
## <a name="see-also"></a>另请参阅  
 [对象和类](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [与我们交流](https://docs.microsoft.com/visualstudio/ide/talk-to-us)
