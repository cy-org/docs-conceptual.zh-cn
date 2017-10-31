---
title: "需要引用程序集 &quot;&lt;assemblyname&gt;包含基类&lt;classname&gt;&quot; |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc30007
- vbc30007
dev_langs:
- VB
helpviewer_keywords:
- BC30007
ms.assetid: 5f34cf47-6c6e-4954-bd8e-d6b020b75fb7
caps.latest.revision: 9
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
ms.openlocfilehash: 2692478864007c787eb19367109e6ce01882ffb1
ms.lasthandoff: 03/13/2017

---
# <a name="reference-required-to-assembly-39ltassemblynamegt39-containing-the-base-class-39ltclassnamegt39"></a>需要引用程序集 '&lt;assemblyname&gt;包含基类&lt;classname&gt;
需要引用程序集 '\<程序集名称&1;> 包含基类\<classname&1;>。 请向项目中添加一个。  
  
 该类是在动态链接库 (DLL) 或未在项目中直接引用的程序集中定义的。 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]编译器需要一个引用，以避免多义性的类定义在多个 DLL 或程序集。  
  
 **错误 ID：** BC30007  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   将未引用的 DLL 或程序集名称包括在项目引用中。  
  
## <a name="see-also"></a>另请参阅  
 [NIB 如何：使用“添加引用”对话框添加或删除引用](http://msdn.microsoft.com/en-us/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)   
 [管理项目中引用](https://docs.microsoft.com/visualstudio/ide/managing-references-in-a-project)   
 [有关无效的引用的疑难解答](https://docs.microsoft.com/visualstudio/ide/troubleshooting-broken-references)
