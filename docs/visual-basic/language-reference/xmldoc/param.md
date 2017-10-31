---
title: "&lt;param&gt; (Visual Basic 中) |Microsoft 文档"
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
- param XML tag
- <param> XML tag
ms.assetid: 4e32e86f-f6f3-4301-b7fc-2f321fb54368
caps.latest.revision: 14
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
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 41852a7fc41595050940d87f9e741df5cb23361c
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="ltparamgt-visual-basic"></a>&lt;param&gt; (Visual Basic)
定义参数名称和说明。  
  
## <a name="syntax"></a>语法  
  
```xml  
<param name="name">description</param>  
```  
  
#### <a name="parameters"></a>参数  
 `name`  
 方法参数的名称。 将名称括在双引号 ("")。  
  
 `description`  
 有关参数的说明。  
  
## <a name="remarks"></a>备注  
 `<param>`标记应当用于方法声明的注释，以描述一个方法的参数。  
  
 文本`<param>`标记将出现在以下位置︰  
  
-   IntelliSense 的参数信息。 有关详细信息，请参阅[使用 IntelliSense](https://docs.microsoft.com/visualstudio/ide/using-intellisense)。  
  
-   对象浏览器。 有关详细信息，请参阅[查看代码的结构](https://docs.microsoft.com/visualstudio/ide/viewing-the-structure-of-code)。  
  
 使用编译[/doc](../../../visual-basic/reference/command-line-compiler/doc.md)将文档注释处理到一个文件。  
  
## <a name="example"></a>示例  
 此示例使用`<param>`标记描述`id`参数。  
  
 [!code-vb[VbVbcnXmlDocComments #&6;](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/param_1.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [XML 注释标记](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)
