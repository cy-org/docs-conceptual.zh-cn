---
title: "路径文件访问错误 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbrID75
dev_langs:
- VB
ms.assetid: 6ce3a161-7316-46bd-a785-0d50e5414020
caps.latest.revision: 8
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
ms.openlocfilehash: ac730bac76540331206daebe600445ca54cc15a9
ms.lasthandoff: 03/13/2017

---
# <a name="pathfile-access-error"></a>路径/文件访问错误
文件访问权限或磁盘访问操作期间，操作系统无法获得的路径和文件名之间的连接。  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
1.  请确保已正确地格式化文件的详细信息。 文件名可以包含是完全限定的 （绝对） 路径或相对路径。 完全限定的路径开头的驱动器名称 （如果此路径为另一个驱动器上），并列出从根到该文件的显式路径。 任何不是完全限定的路径是相对于当前驱动器和目录。  
  
2.  请确保未尝试保存文件将替换现有只读文件。 如果出现这种情况，更改了目标文件的只读属性，或用其他文件名保存文件。  
  
3.  请确保您未尝试打开只读文件中顺序`Output`或`Append`模式。 如果出现这种情况，打开的文件中`Input`模式或更改文件的只读属性。  
  
4.  请确保不尝试更改[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]数据库或文档中的项目。  
  
## <a name="see-also"></a>另请参阅  
 [错误类型](../../../visual-basic/programming-guide/language-features/error-types.md)
