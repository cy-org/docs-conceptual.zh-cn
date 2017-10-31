---
title: "如何：将更改提交到数据库 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c7cba174-9d40-491d-b32c-f2d73b7e9eab
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 如何：将更改提交到数据库
无论您对对象做了多少项更改，都只是在更改内存中的副本。  您并未对数据库中的实际数据做任何更改。  直到您对 <xref:System.Data.Linq.DataContext> 显式调用 <xref:System.Data.Linq.DataContext.SubmitChanges%2A>，您所做的更改才会传输到服务器。  
  
 当您进行此调用时，<xref:System.Data.Linq.DataContext> 会设法将您所做的更改转换为等效的 SQL 命令。  您可以使用自己的自定义逻辑来重写这些操作，但提交顺序是由 <xref:System.Data.Linq.DataContext> 的一项称作“更改处理器”的服务来协调的。  事件的顺序如下：  
  
1.  当您调用 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 时，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 会检查已知对象的集合以确定新实例是否已附加到它们。  如果已附加，这些新实例将添加到被跟踪对象的集合。  
  
2.  所有具有挂起更改的对象将按照它们之间的依赖关系排序成一个对象序列。  如果一个对象的更改依赖于其他对象，则这个对象将排在其依赖项之后。  
  
3.  在即将传输任何实际更改时，[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 会启动一个事务来包装由各条命令组成的系列。  
  
4.  对对象的更改会逐个转换为 SQL 命令，然后发送到服务器。  
  
 此时，如果数据库检测到任何错误，都会造成提交进程停止并引发异常。  将回滚对数据库的所有更改，就像未进行过提交一样。  <xref:System.Data.Linq.DataContext> 仍具有所有更改的完整记录。  因此您可以设法修正问题并重新调用 <xref:System.Data.Linq.DataContext.SubmitChanges%2A>，就像下面的代码示例中那样。  
  
## 示例  
 用于执行提交的事务成功完成后，<xref:System.Data.Linq.DataContext> 就会通过忽略更改跟踪信息接受对对象的更改。  
  
 [!code-csharp[DLinqSubmittingChanges#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#1)]
 [!code-vb[DLinqSubmittingChanges#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#1)]  
  
## 请参阅  
 [如何：检测和解决提交冲突](../../../../../../docs/framework/data/adonet/sql/linq/how-to-detect-and-resolve-conflicting-submissions.md)   
 [如何：管理更改冲突](../../../../../../docs/framework/data/adonet/sql/linq/how-to-manage-change-conflicts.md)   
 [下载示例数据库](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md)   
 [生成和提交数据更改](../../../../../../docs/framework/data/adonet/sql/linq/making-and-submitting-data-changes.md)