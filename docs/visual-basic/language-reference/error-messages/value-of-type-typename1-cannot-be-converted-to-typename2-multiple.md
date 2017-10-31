---
title: "类型的值 &quot;&lt;typename1，而&gt;无法转换为&lt;typename2&gt;（多个文件引用） |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc30961
- bc30961
dev_langs:
- VB
helpviewer_keywords:
- BC30961
ms.assetid: 8be5aa0d-d236-4ac3-aa9c-5044f9f6562b
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
ms.openlocfilehash: 732291ce9c4b83bb9fc7e83fbbc2a8da9748db59
ms.lasthandoff: 03/13/2017

---
# <a name="value-of-type-39lttypename1gt39-cannot-be-converted-to-39lttypename2gt39-multiple-file-references"></a>类型的值 '&lt;typename1，而&gt;无法转换为&lt;typename2&gt;（多个文件引用）
类型的值 '\<typename1，而&1;> 不能转换为\<typename2&1;>。 类型不匹配可能是由于混合使用引用的文件\<filepath1&1;> 在项目中\<projectname1&1;> 文件引用和对\<filepath2&1;> 在项目中\<projectname2&1;>。 如果两个程序集完全相同，请尝试更换这些引用，以确保两个引用都来自相同的位置。  
  
 在其中项目进行的程序集的多个文件引用的情况下，编译器不能保证可将一种类型转换为另一个。  
  
 每个文件引用指定文件路径和一个项目 （通常为 DLL 文件） 的输出文件的名称。 编译器无法保证输出文件来自同一源，或者它们是否表示同一个程序集的相同版本。 因此，它不能保证中不同的引用的类型是相同的类型，或甚至一个可以转换为其他。  
  
 如果您知道所引用的程序集具有相同的程序集标识，可以使用单个文件引用。 *程序集标识* 包括程序集的名称、版本、公钥（如果有）和区域性。 此信息唯一地标识该程序集。  
  
 **错误 ID:** BC30961  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   如果引用的程序集具有相同的程序集标识，然后删除或替换其中的一个文件引用，以便只有单个文件引用。  
  
-   如果引用的程序集不具有相同的程序集标识，然后更改您的代码，以便不会尝试转换为类型在另一个中的类型。  
  
## <a name="see-also"></a>另请参阅  
 [在 Visual Basic 中的类型转换](../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [管理项目中引用](https://docs.microsoft.com/visualstudio/ide/managing-references-in-a-project)   
 [NIB 如何：使用“添加引用”对话框添加或删除引用](http://msdn.microsoft.com/en-us/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)
