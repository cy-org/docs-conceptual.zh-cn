---
title: "AddHandler 语句 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.AddHandlerMethod
- addhandler
- vb.addhandler
dev_langs:
- VB
helpviewer_keywords:
- AddHandler statement
ms.assetid: cfe69799-2a0f-42c0-a99e-09fed954da01
caps.latest.revision: 15
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
ms.openlocfilehash: 728d8393c44d777f9cc016d9cf66030036582ae4
ms.lasthandoff: 03/13/2017

---
# <a name="addhandler-statement"></a>AddHandler 语句
在运行时将事件与事件处理程序。  
  
## <a name="syntax"></a>语法  
  
```  
AddHandler event, AddressOf eventhandler  
```  
  
## <a name="parts"></a>部件  
 `event`  
 要处理的事件的名称。  
  
 `eventhandler`  
 处理事件的过程的名称。  
  
## <a name="remarks"></a>备注  
 `AddHandler`和`RemoveHandler`语句可用于启动和停止事件处理程序执行期间随时。  
  
 签名`eventhandler`过程必须与该事件的签名匹配`event`。  
  
 `Handles` 关键字和 `AddHandler` 语句都允许你指定特定过程处理特定事件，但存在差异。 `AddHandler` 语句在运行时将过程连接到事件。 定义过程时使用 `Handles` 关键字，以指定它处理特定事件。 有关详细信息，请参阅[处理](../../../visual-basic/language-reference/statements/handles-clause.md)。  
  
> [!NOTE]
>  对于自定义事件`AddHandler`语句调用的事件`AddHandler`取值函数。 自定义事件的详细信息，请参阅[Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)。  
  
## <a name="example"></a>示例  
 [!code-vb[VbVbalrEvents #&17;](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/addhandler-statement_1.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [RemoveHandler 语句](../../../visual-basic/language-reference/statements/removehandler-statement.md)   
 [句柄](../../../visual-basic/language-reference/statements/handles-clause.md)   
 [Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)   
 [事件](../../../visual-basic/programming-guide/language-features/events/index.md)
