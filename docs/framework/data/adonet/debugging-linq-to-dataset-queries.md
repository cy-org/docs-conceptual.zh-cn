---
title: "调试 LINQ to DataSet 查询 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f4c54015-8ce2-4c5c-8d18-7038144cc66d
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 调试 LINQ to DataSet 查询
[!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 支持 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 代码的调试。  但是，在调试 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 代码和非 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 托管代码之间存在一些差异。大多数调试功能使用 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 语句，包括单步执行、设置断点以及查看调试程序窗口中显示的结果。  而且，延迟查询执行有些在调试 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 代码时应考虑的副作用，并且在使用“编辑并继续”方面有些限制。  本主题讨论调试方面的问题，该调试对于与非 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 托管代码对比的 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 来说是唯一的。  
  
## 查看结果  
 您可以使用数据提示、“监视”窗口和“快速监视”对话框来查看 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 语句的结果。  使用源窗口，可以将指针暂时停留在源窗口中的查询上，这样数据提示就会出现。  可以复制 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 变量，然后将其粘贴到“监视”窗口或“快速监视”对话框。在 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 中，创建或声明查询时并不计算查询，而只在执行查询时才计算。  这称为*延迟执行*。  因此，查询变量直到计算时才有值。  有关详细信息，请参阅[LINQ to DataSet 中的查询](../../../../docs/framework/data/adonet/queries-in-linq-to-dataset.md)。  
  
 调试程序必须计算查询才能显示查询结果。  当您在调试程序中查看 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 查询结果时，将进行此隐式计算，应考虑到这存在一些副作用。  查询的每次计算都需要时间。  展开结果节点需要时间。  对于某些查询，重复计算可能引起明显的性能损失。  计算查询也会有副作用，这些副作用会更改数据值或程序的状态。  不是所有查询都具有副作用。  要确定查询能否安全计算而没有副作用，必须了解实现查询的代码。  有关详细信息，请参阅[副作用与表达式](../Topic/Side%20Effects%20and%20Expressions.md)。  
  
## 编辑并继续  
 “编辑并继续”不支持 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 查询的更改。  如果在调试会话过程中，添加、移除或更改 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 语句，则会显示一个对话框，告诉您“编辑并继续”不支持该更改。  此时，可以撤消更改，或停止调试会话并对编辑的代码重新启动新会话。  
  
 此外，“编辑并继续”不支持更改 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 语句中使用的变量的类型或值。  同样，可以撤消更改，或停止并重新启动调试会话。  
  
 在 Visual Studio 的 Visual C\# 中，无法在包含 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 查询的方法中的任何代码上使用“编辑并继续”。  
  
 在 Visual Studio 的 Visual Basic 中，可以对非 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 代码使用“编辑并继续”（即使在包含 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 查询的方法中也同样可以）。  可以在 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 语句之前添加或移除代码，即使这些更改会影响 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 查询的行号。  非 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 代码的 Visual Basic 调试过程仍与引入 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 之前的过程相同。  但是，您无法更改、添加或移除 [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 查询，除非停止调试才能应用这些更改。  
  
## 请参阅  
 [调试托管代码](../Topic/Debugging%20Managed%20Code.md)   
 [编程指南](../../../../docs/framework/data/adonet/programming-guide-linq-to-dataset.md)