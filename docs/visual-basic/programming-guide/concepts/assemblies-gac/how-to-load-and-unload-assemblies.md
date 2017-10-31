---
title: "如何︰ 加载和卸载程序集 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: bbc84236-04b6-4c1b-9672-52773f65a5dc
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
ms.openlocfilehash: 460d3a18fdee74c9b9c49ee465247b5b12d554d8
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-load-and-unload-assemblies-visual-basic"></a>如何︰ 加载和卸载程序集 (Visual Basic)
由你的程序引用的程序集将自动加载在生成时，但也可以将特定的程序集加载到当前的应用程序域在运行时。 有关详细信息，请参阅[如何︰ 将程序集加载到应用程序域](http://msdn.microsoft.com/library/1432aa2d-bd83-4346-bf3b-a1b7920e2aa9)。  
  
 没有办法无需卸载所有包含它的应用程序域卸载单个程序集。 即使该程序集都超出范围，实际的程序集文件将保持被加载，直到包含它的所有应用程序域都会被卸载。  
  
 如果您想要卸载某些程序集而不是其他卸载，请考虑创建一个新的应用程序域，该域中，在中执行代码然后卸载该应用程序域。 有关详细信息，请参阅[如何︰ 卸载应用程序域](http://msdn.microsoft.com/library/f356116d-e415-4f7c-a332-6e6a60227192)。  
  
### <a name="to-load-an-assembly-into-an-application-domain"></a>将程序集加载到应用程序域  
  
1.  使用多个类<xref:System.AppDomain>和<xref:System.Reflection>。</xref:System.Reflection></xref:System.AppDomain>中包含的 load 方法 有关详细信息，请参阅[如何︰ 将程序集加载到应用程序域](http://msdn.microsoft.com/library/1432aa2d-bd83-4346-bf3b-a1b7920e2aa9)。  
  
### <a name="to-unload-an-application-domain"></a>若要卸载的应用程序域  
  
1.  没有办法无需卸载所有包含它的应用程序域卸载单个程序集。 使用`Unload`方法从<xref:System.AppDomain>卸载应用程序域。</xref:System.AppDomain> 有关详细信息，请参阅[如何︰ 卸载应用程序域](http://msdn.microsoft.com/library/f356116d-e415-4f7c-a332-6e6a60227192)。  
  
## <a name="see-also"></a>另请参阅  
 [编程概念](../../../../visual-basic/programming-guide/concepts/index.md)   
 [程序集和全局程序集缓存 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)   
 [如何︰ 将程序集加载到应用程序域](http://msdn.microsoft.com/library/1432aa2d-bd83-4346-bf3b-a1b7920e2aa9)
