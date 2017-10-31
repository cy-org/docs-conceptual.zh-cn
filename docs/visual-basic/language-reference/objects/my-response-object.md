---
title: "My.Response 对象 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- My.MyWebExtension.Response
- My.Response
dev_langs:
- VB
helpviewer_keywords:
- My.Response object
ms.assetid: 626359bc-3165-40b4-bfaf-2c610e26eb5b
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
ms.openlocfilehash: e2ae9a659bb7575023dfa1847c9d405d0f7d6ac3
ms.lasthandoff: 03/13/2017

---
# <a name="myresponse-object"></a>My.Response 对象
获取<xref:System.Web.HttpResponse>与<xref:System.Web.UI.Page>。</xref:System.Web.UI.Page>关联的对象</xref:System.Web.HttpResponse> 此对象可用于将 HTTP 响应数据发送到客户端，并包含有关该响应的信息。  
  
## <a name="remarks"></a>备注  
 `My.Response`对象包含当前<xref:System.Web.HttpResponse>与页关联的对象。</xref:System.Web.HttpResponse>  
  
 `My.Response`对象功能仅适用于[!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)]应用程序。  
  
## <a name="example"></a>示例  
 下面的示例获取该标头集合`My.Request`对象，并使用`My.Response`要写入到 ASP.NET 页面对象。  
  
 [!code-vb[VbVbalrMyWeb #&1;](../../../visual-basic/language-reference/objects/codesnippet/VisualBasic/my-response-object_1.aspx)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Web.HttpResponse></xref:System.Web.HttpResponse>   
 [My.Request 对象](../../../visual-basic/language-reference/objects/my-request-object.md)
