---
title: "如何︰ 与其他应用程序 (Visual Basic 中) 共享程序集 |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 5388aedc-cb42-4622-8b70-8e701eee057a
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 8065a66c8f7c7b9ccb9125b060b0c03cde273482
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-share-an-assembly-with-other-applications-visual-basic"></a>如何︰ 与其他应用程序 (Visual Basic 中) 共享程序集
程序集可以为专用或共享︰ 默认情况下，大多数简单的程序都包含一个私有程序集，因为不应将它们用于其他应用程序。  
  
 为了与其他应用程序共享程序集，必须将它放置在[全局程序集缓存](http://msdn.microsoft.com/library/cf5eacd0-d3ec-4879-b6da-5fd5e4372202)(GAC 中)。  
  
### <a name="sharing-an-assembly"></a>共享程序集  
  
1.  创建您的程序集。 有关详细信息，请参阅[创建程序集](http://msdn.microsoft.com/library/54832ee9-dca8-4c8b-913c-c0b9d265e9a4)。  
  
2.  为您的程序集分配强名称。 有关详细信息，请参阅[如何︰ 使用强名称为程序集签名](http://msdn.microsoft.com/library/2c30799a-a826-46b4-a25d-c584027a6c67)。  
  
3.  将版本信息分配给您的程序集。 有关详细信息，请参阅[程序集版本控制](https://msdn.microsoft.com/library/51ket42z)。  
  
4.  将您的程序集添加到全局程序集缓存中。 有关详细信息，请参阅[如何︰ 将程序集安装到全局程序集缓存](http://msdn.microsoft.com/library/a7e6f091-d02c-49ba-b736-7295cb0eb743)。  
  
5.  访问包含从其他应用程序的程序集中的类型。 有关详细信息，请参阅[如何︰ 引用具有强名称程序集](http://msdn.microsoft.com/library/4c6a406a-b5eb-44fa-b4ed-4e95bb95a813)。  
  
## <a name="see-also"></a>另请参阅  
 [编程概念](../../../../visual-basic/programming-guide/concepts/index.md)
 [程序集和全局程序集缓存 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)   
 [使用程序集编程](http://msdn.microsoft.com/library/25918b15-701d-42c7-95fc-c290d08648d6)
