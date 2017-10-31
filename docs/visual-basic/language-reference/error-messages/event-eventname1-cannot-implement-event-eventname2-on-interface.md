---
title: "事件&lt;eventname1&gt;&quot;不能实现事件&lt;eventname2&gt;on 接口&lt;接口&gt;因为它们的委托类型&lt;delegate1&gt;&quot;和&quot;&lt;delegate2&gt;&quot; 不匹配 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc31423
- bc31423
dev_langs:
- VB
helpviewer_keywords:
- BC31423
ms.assetid: 2e754b66-5836-48ff-9697-b9c0d7085f18
caps.latest.revision: 6
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
ms.openlocfilehash: b6253b3e9ad07c3715c55a8cfd0891792b45a452
ms.lasthandoff: 03/13/2017

---
# <a name="event-39lteventname1gt39-cannot-implement-event-39lteventname2gt39-on-interface-39ltinterfacegt39-because-their-delegate-types-39ltdelegate1gt39-and-39ltdelegate2gt39-do-not-match"></a>事件&lt;eventname1&gt;'不能实现事件&lt;eventname2&gt;on 接口&lt;接口&gt;因为它们的委托类型&lt;delegate1&gt;'和'&lt;delegate2&gt;' 不匹配
[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]不能实现一个事件，因为该事件的委托类型与接口中事件的委托类型不匹配。 如果在接口中定义了多个事件，然后试图用一个事件同时实现这些事件，则可能发生此错误。 只有当所有要实现的事件都使用 `As` 语法进行声明并指定相同的委托类型时，事件才能实现两个或更多个事件。  
  
 **错误 ID:** BC31423  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   单独实现事件。  
  
     - 或 -  
  
-   在接口中使用定义的事件`As`语法，并指定相同的委托类型。  
  
## <a name="see-also"></a>另请参阅  
 [Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)   
 [Delegate 语句](../../../visual-basic/language-reference/statements/delegate-statement.md)   
 [事件](../../../visual-basic/programming-guide/language-features/events/index.md)
