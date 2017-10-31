---
title: "RemoveHandler 语句 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.RemoveHandlerMethod
- vb.RemoveHandler
- RemoveHandler
dev_langs:
- VB
helpviewer_keywords:
- RemoveHandler keyword
- RemoveHandler statement
ms.assetid: 647cd825-e877-4910-b4f1-8d168beebe6a
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: d35de576bd9e267800acc2a9bfd5761dd977622f
ms.lasthandoff: 03/13/2017

---
# <a name="removehandler-statement"></a>RemoveHandler 语句
删除的事件和事件处理程序之间的关联。  
  
## <a name="syntax"></a>语法  
  
```  
RemoveHandler event, AddressOf eventhandler  
```  
  
## <a name="parts"></a>部件  
  
|术语|定义|  
|---|---|  
|`event`|正在处理的事件的名称。|  
|`eventhandler`|当前正在处理该事件的过程的名称。|  
  
## <a name="remarks"></a>备注  
 `AddHandler`和`RemoveHandler`语句可用于启动和停止程序执行期间随时特定事件的事件处理。  
  
> [!NOTE]
>  对于自定义事件`RemoveHandler`语句调用的事件`RemoveHandler`取值函数。 自定义事件的详细信息，请参阅[Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)。  
  
## <a name="example"></a>示例  
 [!code-vb[VbVbalrEvents #&17;](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/removehandler-statement_1.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [AddHandler 语句](../../../visual-basic/language-reference/statements/addhandler-statement.md)   
 [句柄](../../../visual-basic/language-reference/statements/handles-clause.md)   
 [Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)   
 [事件](../../../visual-basic/programming-guide/language-features/events/index.md)
