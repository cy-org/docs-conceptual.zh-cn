---
title: "如何：在 BlockingCollection 中逐个添加和取出项"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- thread-safe collections, blocking dictionary
ms.assetid: 38f2f3d8-15e5-4bf4-9c83-2b5b6f22bad1
caps.latest.revision: 7
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 66b4e921a4c7285976694f4633ce1eeaadcb7cf9
ms.contentlocale: zh-cn
ms.lasthandoff: 09/19/2017

---
# <a name="how-to-add-and-take-items-individually-from-a-blockingcollection"></a>如何：在 BlockingCollection 中逐个添加和取出项
此示例演示如何以阻止和非阻止方式在 <xref:System.Collections.Concurrent.BlockingCollection%601> 中添加项和删除其中的项。 有关 <xref:System.Collections.Concurrent.BlockingCollection%601> 的详细信息，请参阅 [BlockingCollection 概述](../../../../docs/standard/collections/thread-safe/blockingcollection-overview.md)。  
  
 有关如何枚举 <xref:System.Collections.Concurrent.BlockingCollection%601> 直至其为空且不再添加更多元素的示例，请参阅[如何：使用 ForEach 删除 BlockingCollection 中的项](../../../../docs/standard/collections/thread-safe/how-to-use-foreach-to-remove.md)  
  
## <a name="example"></a>示例  
 第一个示例演示如何添加和取出项以便在集合暂时为空（取出时）或达到最大容量（添加时）或超过指定的超时时间时，将阻止相应的操作。 注意，仅当已创建 BlockingCollection 且构造函数中指定了最大容量时，才会启用在达到最大容量时进行阻止的功能。  
  
 [!code-csharp[CDS_BlockingCollection#01](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds_blockingcollection/cs/example01.cs#01)]
 [!code-vb[CDS_BlockingCollection#01](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_blockingcollection/vb/simpleblocking.vb#01)]  
  
## <a name="example"></a>示例  
 第二个示例演示如何添加和取出项以便不会阻止操作。 如果不存在任何项，或已达到绑定集合的最大容量，或已超过超时时间，则 <xref:System.Collections.Concurrent.BlockingCollection%601.TryAdd%2A> 或 <xref:System.Collections.Concurrent.BlockingCollection%601.TryTake%2A> 操作将返回 false。 这将允许线程暂时执行一些其他有用的工作，并在稍后再次尝试检索新项，或尝试添加此前无法添加的相同项。 该程序还演示如何在访问 <xref:System.Collections.Concurrent.BlockingCollection%601> 时实现取消。  
  
 [!code-csharp[CDS_BlockingCollection#02](../../../../samples/snippets/csharp/VS_Snippets_Misc/cds_blockingcollection/cs/example02.cs#02)]
 [!code-vb[CDS_BlockingCollection#02](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_blockingcollection/vb/nonblockingbc.vb#02)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Collections.Concurrent?displayProperty=fullName>   
 [BlockingCollection 概述](../../../../docs/standard/collections/thread-safe/blockingcollection-overview.md)

