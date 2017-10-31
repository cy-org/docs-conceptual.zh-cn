---
title: "使用 DependentTransaction 管理并发  | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b85a97d8-8e02-4555-95df-34c8af095148
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 使用 DependentTransaction 管理并发 
<xref:System.Transactions.Transaction> 对象是使用 <xref:System.Transactions.Transaction.DependentClone%2A> 方法创建的。该对象的唯一目的是保证当某他一些代码段（如辅助线程）还在事务上工作时，不能提交事务。当在克隆的事务中执行的工作最终完成并可以提交时，该对象可以使用 <xref:System.Transactions.DependentTransaction.Complete%2A> 方法通知事务的创建者。因而您就可以保持数据的一致性和正确性。  
  
 此外，<xref:System.Transactions.DependentTransaction> 类还可用于管理异步任务之间的并发性。在这种情况下，当依赖的克隆执行其自己的任务时，父事务可以继续执行任意代码。换句话说，直到依赖的克隆完成时，父事务的执行才会被阻止。  
  
## 创建依赖的克隆  
 若要创建依赖的事务，请调用 <xref:System.Transactions.Transaction.DependentClone%2A> 方法并将 <xref:System.Transactions.DependentCloneOption> 枚举作为参数传递。此参数定义在依赖的克隆指示可以提交事务（通过调用 <xref:System.Transactions.DependentTransaction.Complete%2A> 方法）之前，对父事务调用 `Commit` 时的事务行为。下面列出了此参数的有效值：  
  
-   <xref:System.Transactions.DependentCloneOption> 会创建一个依赖的事务，后者在父事务超时或对所有依赖事务调用 <xref:System.Transactions.DependentTransaction.Complete%2A> 以指示完成之前一直阻止父事务的提交进程。当客户端希望在依赖事务完成后再提交父事务时，这一点十分有用。如果父事务的工作比该依赖事务早完成，并在此时对该依赖事务调用了 <xref:System.Transactions.CommittableTransaction.Commit%2A>，则提交进程会被阻止（在该状态下可在依赖事务上执行其他工作并可创建新登记），直到所有依赖事务都调用 <xref:System.Transactions.DependentTransaction.Complete%2A> 为止。只要所有依赖事务完成了工作并调用了 <xref:System.Transactions.DependentTransaction.Complete%2A>，就会立即启动事务的提交进程。  
  
-   另一方面，在调用 <xref:System.Transactions.CommittableTransaction.Commit%2A> 之前对父事务调用 <xref:System.Transactions.DependentTransaction.Complete%2A> 时，<xref:System.Transactions.DependentCloneOption> 会创建一个自动中止的依赖事务。在这种情况下，在该依赖事务中执行的所有工作在一个事务生存期内都保持不变，并且根本无法只提交其中的一部分。  
  
 当应用程序完成在该依赖事务上的工作时，必须调用一次 <xref:System.Transactions.DependentTransaction.Complete%2A> 方法；否则，会引发 <xref:System.InvalidOperationException>。在执行此调用之后，不能在事务上尝试任何附加工作，否则就会引发异常。  
  
 下面的代码示例演示如何创建一个依赖事务来管理两个并发任务，具体为克隆一个依赖的事务并将其传递给辅助线程。  
  
```csharp  
public class WorkerThread  
{  
    public void DoWork(DependentTransaction dependentTransaction)  
    {  
        Thread thread = new Thread(ThreadMethod);  
        thread.Start(dependentTransaction);   
    }  
  
    public void ThreadMethod(object transaction)   
    {   
        DependentTransaction dependentTransaction = transaction as DependentTransaction;  
        Debug.Assert(dependentTransaction != null);   
        try  
        {  
            using(TransactionScope ts = new TransactionScope(dependentTransaction))  
            {  
                /* Perform transactional work here */   
                ts.Complete();  
            }  
        }  
        finally  
        {  
            dependentTransaction.Complete();   
             dependentTransaction.Dispose();   
        }  
    }  
  
//Client code   
using(TransactionScope scope = new TransactionScope())  
{  
    Transaction currentTransaction = Transaction.Current;  
    DependentTransaction dependentTransaction;      
    dependentTransaction = currentTransaction.DependentClone(DependentCloneOption.BlockCommitUntilComplete);  
    WorkerThread workerThread = new WorkerThread();  
    workerThread.DoWork(dependentTransaction);  
    /* Do some transactional work here, then: */  
    scope.Complete();  
}  
  
```  
  
 客户端代码创建了一个还能够设置环境事务的事务范围。不能直接将环境事务传递给辅助线程。相反，应通过对当前事务调用 <xref:System.Transactions.Transaction.DependentClone%2A> 方法来克隆当前（环境）事务，并将依赖事务传递给辅助线程。  
  
 `ThreadMethod` 方法将在新线程上执行。客户端会启动一个新线程，以将该依赖事务作为 `ThreadMethod` 参数传递。  
  
 由于依赖事务是用 <xref:System.Transactions.DependentCloneOption> 创建的，因此应保证第二个线程上的所有事务工作都完成并对该依赖事务调用 <xref:System.Transactions.DependentTransaction.Complete%2A> 后才能提交事务。这意味着如果客户端的范围在新线程对该依赖事务调用 <xref:System.Transactions.DependentTransaction.Complete%2A> 之前结束（客户端尝试在 **using** 语句结束处释放事务对象时），则客户端代码会一直被阻止，直到对该依赖事务调用 <xref:System.Transactions.DependentTransaction.Complete%2A> 为止。这样，事务就可完成提交或中止。  
  
## 并发问题  
 使用 <xref:System.Transactions.DependentTransaction> 类时，存在其他一些需要了解的并发问题。  
  
-   如果辅助线程回滚事务而父事务却尝试提交它，则会引发 <xref:System.Transactions.TransactionAbortedException>。  
  
-   您应为事务中的每个辅助线程分别创建一个依赖的克隆。不要将同一依赖克隆传递给多个线程，因为只有一个线程能够对依赖克隆调用 <xref:System.Transactions.DependentTransaction.Complete%2A>。  
  
-   如果辅助线程生成新的辅助线程，请确保利用现有的依赖克隆中再创建一个依赖的克隆，然后将后者传递给该新线程。  
  
## 请参阅  
 <xref:System.Transactions.DependentTransaction>