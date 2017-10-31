---
title: "&lt;摘要&gt;(Visual Basic 中) |Microsoft 文档"
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
- <summary> XML tag
- summary XML tag
ms.assetid: 861c847d-dd94-478a-aa23-bf4899cdc848
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
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: ad2053e21e58c49205fe869a484cb2dffd2169ee
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="ltsummarygt-visual-basic"></a>&lt;摘要&gt;(Visual Basic)
指定该成员的摘要。  
  
## <a name="syntax"></a>语法  
  
```xml  
<summary>description</summary>  
```  
  
#### <a name="parameters"></a>参数  
 `description`  
 对象的摘要。  
  
## <a name="remarks"></a>备注  
 使用`<summary>`标记来描述一个类型或类型成员。 使用[\<备注&1;>](../../../visual-basic/language-reference/xmldoc/remarks.md)将补充信息添加到类型说明。  
  
 文本`<summary>`标签是在 IntelliSense 中，类型信息的唯一源，它还会显示在对象浏览器。 对象浏览器有关的信息，请参阅[查看代码结构](https://docs.microsoft.com/visualstudio/ide/viewing-the-structure-of-code)。  
  
 使用编译[/doc](../../../visual-basic/reference/command-line-compiler/doc.md)将文档注释处理到一个文件。  
  
## <a name="example"></a>示例  
 此示例使用`<summary>`标记描述`ResetCounter`方法和`Counter`属性。  
  
 [!code-vb[VbVbcnXmlDocComments #&1;](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/summary_1.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [XML 注释标记](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)
