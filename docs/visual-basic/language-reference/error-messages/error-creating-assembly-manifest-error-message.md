---
title: "创建程序集清单时出错︰&lt;错误信息&gt;|Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc30140
- vbc30140
dev_langs:
- VB
helpviewer_keywords:
- BC30140
ms.assetid: 1beb5aa0-7b79-4c85-946b-5c2d0a41d1d2
caps.latest.revision: 13
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
ms.openlocfilehash: 35a912bbcab78178ce636afa550c244823da512c
ms.lasthandoff: 03/13/2017

---
# <a name="error-creating-assembly-manifest-lterror-messagegt"></a>创建程序集清单时出错︰&lt;错误消息&gt;
[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 编译器调用程序集链接器（Al.exe，也称作 Alink）生成包含清单的程序集。 该链接器已报告在创建程序集的预发出阶段中出错。  
  
 如果指定的密钥文件或密钥容器有问题，就可能发生错误。 若要对程序集进行完全签名，必须提供包含公钥和私钥信息的有效密钥文件。 若要延迟对程序集签名，必须选择**仅延迟签名**复选框，并提供包含公钥信息有关的信息的有效密钥文件。 当程序集为延迟签名时，不需要使用私有密钥。 有关详细信息，请参阅[如何︰ 为程序集 (Visual Studio) 签名](http://msdn.microsoft.com/en-us/f468a7d3-234c-4353-924d-8e0ae5896564)。  
  
 **错误 ID:** BC30140  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
1.  检查引用的错误信息并参考主题[Al.exe 工具错误和警告](http://msdn.microsoft.com/en-us/7f125d49-0a03-47a6-9ba9-d61a679a7d4b)获得有关错误 AL1019 的进一步解释和建议  
  
2.  如果仍然出现错误，则收集有关该情况的信息并通知 Microsoft 产品支持服务。  
  
## <a name="see-also"></a>另请参阅  
 [如何：为程序集签名 (Visual Studio)](http://msdn.microsoft.com/en-us/f468a7d3-234c-4353-924d-8e0ae5896564)   
 [“项目设计器”->“签名”页](https://docs.microsoft.com/visualstudio/ide/reference/signing-page-project-designer)   
 [Al.exe （程序集链接器）](https://msdn.microsoft.com/library/c405shex)   
 [Al.exe 工具错误和警告](http://msdn.microsoft.com/en-us/7f125d49-0a03-47a6-9ba9-d61a679a7d4b)   
 [与我们交流](https://docs.microsoft.com/visualstudio/ide/talk-to-us)
