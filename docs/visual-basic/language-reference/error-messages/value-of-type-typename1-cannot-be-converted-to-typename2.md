---
title: "类型的值 &quot;&lt;typename1，而&gt;无法转换为&lt;typename2&gt;&quot; |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc30955
- bc30955
dev_langs:
- VB
helpviewer_keywords:
- BC30955
ms.assetid: 966b61eb-441e-48b0-bedf-ca95384ecb8b
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
ms.openlocfilehash: c973d5e2aa03d423e1dea8053946172655f08490
ms.lasthandoff: 03/13/2017

---
# <a name="value-of-type-39lttypename1gt39-cannot-be-converted-to-39lttypename2gt39"></a>类型的值 '&lt;typename1，而&gt;无法转换为&lt;typename2&gt;
类型的值 '\<typename1，而&1;> 不能转换为\<typename2&1;>。 类型不匹配可能是由于混合的文件引用与程序集的项目引用\<程序集名称&1;>。 请尝试替换为文件引用和对\<filepath&1;> 在项目中\<projectname1&1;> 到的项目引用\<projectname2&1;>。  
  
 在其中一个项目使项目引用和文件引用的情况下，编译器不能保证可将一种类型转换为另一个。  
  
 下面的伪代码说明了可能会产生此错误的情况。  
  
 `' ================ Visual Basic project P1 ================`  
  
 `'        P1 makes a PROJECT REFERENCE to project P2`  
  
 `'        and a FILE REFERENCE to project P3.`  
  
 `Public commonObject As P3.commonClass`  
  
 `commonObject = P2.getCommonClass()`  
  
 `' ================ Visual Basic project P2 ================`  
  
 `'        P2 makes a PROJECT REFERENCE to project P3`  
  
 `Public Function getCommonClass() As P3.commonClass`  
  
 `Return New P3.commonClass`  
  
 `End Function`  
  
 `' ================ Visual Basic project P3 ================`  
  
 `Public Class commonClass`  
  
 `End Class`  
  
 项目`P1`间接的项目引用了通过项目`P2`到项目`P3`，同时还对直接文件引用`P3`。 声明`commonObject`使用文件引用和对`P3`，而对调用`P2.getCommonClass`中使用项目引用`P3`。  
  
 这种情况下的问题是文件引用指定的文件路径和名称的输出文件`P3`(通常为 p3.dll)，而项目引用标识源项目 (`P3`) 按项目名称。 因此，编译器也不能保证该类型`P3.commonClass`来自通过两个不同的引用相同的源代码。  
  
 这种情况通常发生在项目引用和混合的文件引用。 在上图中，此问题不会发生如果`P1`进行直接的项目引用到`P3`而不是引用的文件。  
  
 **错误 ID:** BC30955  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   更改对项目引用的文件引用。  
  
## <a name="see-also"></a>另请参阅  
 [在 Visual Basic 中的类型转换](../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [管理项目中引用](https://docs.microsoft.com/visualstudio/ide/managing-references-in-a-project)   
 [NIB 如何：使用“添加引用”对话框添加或删除引用](http://msdn.microsoft.com/en-us/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)
