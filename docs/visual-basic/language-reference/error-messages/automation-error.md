---
title: "自动化错误 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbrID440
dev_langs:
- VB
ms.assetid: 2c4be5c5-2f0d-4a2b-96fe-d1b24f08fc4c
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
ms.openlocfilehash: 0e48d5bde8b0fd3d31265d3d287623e32c0ea4cf
ms.lasthandoff: 03/13/2017

---
# <a name="automation-error"></a>自动错误
执行方法或者获取或设置对象变量的属性时发生错误。 错误由创建该对象的应用程序报告。  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
1.  检查 `Err` 对象的属性，以确定错误来源和错误性质。  
  
2.  在紧邻访问语句之前使用 `On Error Resume Next` 语句，然后检查紧邻访问语句之后是否存在错误。  
  
## <a name="see-also"></a>另请参阅  
 [错误类型](../../../visual-basic/programming-guide/language-features/error-types.md)   
 [与我们交流](https://docs.microsoft.com/visualstudio/ide/talk-to-us)
