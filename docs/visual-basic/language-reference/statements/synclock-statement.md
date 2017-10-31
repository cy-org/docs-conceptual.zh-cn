---
title: "SyncLock 语句 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.SyncLock"
  - "SyncLock"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "锁定, 线程"
  - "SyncLock 语句"
  - "线程处理 [Visual Basic], 锁定"
ms.assetid: 14501703-298f-4d43-b139-c4b6366af176
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# SyncLock 语句
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

在执行一个语句块前获取此块的独占锁。  
  
## 语法  
  
```  
SyncLock lockobject  
    [ block ]  
End SyncLock  
```  
  
## 部件  
 `lockobject`  
 必需。  计算结果等于对象引用的表达式。  
  
 `block`  
 可选。  获取独占锁时要执行的语句块。  
  
 `End SyncLock`  
 终止 `SyncLock` 块。  
  
## 备注  
 `SyncLock` 语句可确保多个线程不在同一时间执行语句块。  `SyncLock` 防止各个线程进入该语句块，直到没有其他线程执行它为止。  
  
 `SyncLock` 的最常见作用是保护数据不被多个线程同时更新。  如果操作数据的语句必须在没有中断的情况下完成，请将它们放入 `SyncLock` 块。  
  
 有时将受独占锁保护的语句块称为“临界区”。  
  
## 规则  
  
-   分支。  您不能从此块的外部分支到 `SyncLock` 块。  
  
-   锁定对象值。  `lockobject` 的值不能为 `Nothing`。  必须先创建锁定对象，才能在 `SyncLock` 语句中使用此对象。  
  
     在执行 `SyncLock` 块时，不能更改 `lockobject` 的值。  机制要求锁定对象保持不变。  
  
-   在 `SyncLock` 不能使用 [等待](../../../visual-basic/language-reference/operators/await-operator.md) 运算符块。  
  
## 行为  
  
-   机制。  线程到达 `SyncLock` 语句时，它将计算 `lockobject` 表达式，并挂起执行，直到获取了由表达式返回的对象上的独占锁。  当另一线程到达 `SyncLock` 语句时，它将不能获取独占锁，直到第一个线程执行 `End SyncLock` 语句。  
  
-   受保护的数据。  如果 `lockobject` 为 `Shared` 变量，独占锁将防止类的任何实例中的线程在任何其他线程执行 `SyncLock` 块时执行该块。  这会保护所有实例所共享的数据。  
  
     如果 `lockobject` 为实例变量（非 `Shared`），此锁将防止当前实例中正在运行的线程与相同实例中的另一线程同时执行 `SyncLock` 块。  这会保护由单个实例维护的数据。  
  
-   捕获和释放。  `SyncLock` 块的操作就像 `Try...Finally` 结构，其中 `Try` 块获取 `lockobject` 上的独占锁，而 `Finally` 块则释放此锁。  因此，`SyncLock` 块确保锁的释放，不管您如何退出块。  即使发生未经处理的异常，也是如此。  
  
-   Framework 调用。  `SyncLock` 块通过调用 <xref:System.Threading> 命名空间中的 `Monitor` 类的 `Enter` 方法和 `Exit` 方法获取和释放独占锁。  
  
## 编程惯例  
 `lockobject` 表达式应始终计算仅属于您的类的对象。  您应该声明一个 `Private` 对象变量，以保护属于当前实例的数据，或声明一个 `Private Shared` 对象变量，以保护所有实例共有的数据。  
  
 不应使用 `Me` 关键字为实例数据提供锁定对象。  如果类之外的代码引用了您的类的实例，它可以使用该引用作为 `SyncLock` 块的锁定对象（与您的锁定对象完全不同），从而保护不同数据。  通过这种方式，您的类和其他类将相互阻止执行与它们无关的 `SyncLock` 块。  由于使用相同字符串的进程中的任何其他代码将共享相同的锁，所以对一个字符串进行相似锁定可能会有问题。  
  
 也不应使用 `Me.GetType` 方法为共享数据提供锁定对象。  这是因为 `GetType` 始终为给定类名称返回相同的 `Type` 对象。  外部代码可以调用您的类上的 `GetType`，并可以获取与您正在使用的锁定对象相同的锁定对象。  这将导致两个类相互阻止它们的 `SyncLock` 块。  
  
## 示例  
  
### 说明  
 下面的示例演示维护简单消息列表的类。  它将消息保存在数组中，并将最近使用的该数组的元素保存在变量中。  `addAnotherMessage` 过程增加最近使用的元素，并存储新消息。  这两个操作受到 `SyncLock` 和 `End SyncLock` 语句的保护，因为一旦增加了最近的元素，就必须先存储新消息，然后任何其他线程才可以再次增加最近的元素。  
  
 如果 `simpleMessageList` 类在其所有实例中共享一个消息列表，则变量 `messagesList` 和 `messagesLast` 将被声明为 `Shared`。  此时，变量 `messagesLock` 也应为 `Shared`，从而每个实例都将使用单个锁定对象。  
  
### 代码  
 [!code-vb[VbVbalrThreading#1](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/synclock-statement_1.vb)]  
  
### 说明  
 下面的示例使用线程和 `SyncLock`。  只要 `SyncLock` 语句存在，语句块就是临界区并且 `balance` 永远不会是负数。  可以注释掉 `SyncLock` 和 `End SyncLock` 语句，以查看省去 `SyncLock` 关键字的效果。  
  
### 代码  
 [!code-vb[VbVbalrThreading#21](../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/synclock-statement_2.vb)]  
  
### 注释  
  
## 请参阅  
 <xref:System.Threading>   
 <xref:System.Threading.Monitor>   
 [线程同步](../Topic/Thread%20Synchronization%20\(C%23%20and%20Visual%20Basic\).md)   
 [线程](../Topic/Threading%20\(C%23%20and%20Visual%20Basic\).md)