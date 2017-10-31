---
title: "与企业服务和 COM+ 事务的互操作性  | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d0fd0d26-fe86-443b-b208-4d57d39fa4aa
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 与企业服务和 COM+ 事务的互操作性 
<xref:System.Transactions> 命名空间支持使用此命名空间创建的事务对象与通过 COM\+ 创建的事务之间的互操作性。  
  
 在创建新的 <xref:System.Transactions.TransactionScope> 实例时，可以使用 <xref:System.Transactions.EnterpriseServicesInteropOption> 枚举来指定与 COM\+ 的互操作性的级别。  
  
 默认情况下，当应用程序代码检查静态 <xref:System.Transactions.Transaction.Current%2A> 属性时，<xref:System.Transactions> 会尝试查找当前事务或指示 <xref:System.Transactions.Transaction.Current%2A> 为 **null** 的 <xref:System.Transactions.TransactionScope> 对象。如果找不到上述任何一项，则 <xref:System.Transactions> 会查询事务的 COM\+ 上下文。请注意，即使 <xref:System.Transactions> 可从 COM\+ 上下文中找到事务，它仍会首选 <xref:System.Transactions> 的本机事务。  
  
## 互操作性级别  
 <xref:System.Transactions.EnterpriseServicesInteropOption> 枚举定义了下列互操作性级别：<xref:System.Transactions.EnterpriseServicesInteropOption>、<xref:System.Transactions.EnterpriseServicesInteropOption> 和 <xref:System.Transactions.EnterpriseServicesInteropOption>。  
  
 <xref:System.Transactions.TransactionScope> 类提供的构造函数接受 <xref:System.Transactions.EnterpriseServicesInteropOption> 作为参数。  
  
 顾名思义，<xref:System.Transactions.EnterpriseServicesInteropOption> 表示 <xref:System.EnterpriseServices> 上下文与事务范围之间不存在互操作性。在用 <xref:System.Transactions.EnterpriseServicesInteropOption> 创建 <xref:System.Transactions.TransactionScope> 对象后，对 <xref:System.Transactions.Transaction.Current%2A> 的任何更改都不会在 COM\+ 上下文中反映出来。同样，对 COM\+ 上下文中事务的更改也不会在 <xref:System.Transactions.Transaction.Current%2A> 中反映出来。对于 <xref:System.Transactions>，这是最快的操作模式，因为没有所需的额外同步。<xref:System.Transactions.EnterpriseServicesInteropOption> 是由具有所有构造函数的 <xref:System.Transactions.TransactionScope> 使用的默认值，这些构造函数不能接受作为参数的 <xref:System.Transactions.EnterpriseServicesInteropOption>。  
  
 如果需要将 <xref:System.EnterpriseServices> 事务与环境事务组合在一起，则需要使用 <xref:System.Transactions.EnterpriseServicesInteropOption> 或 <xref:System.Transactions.EnterpriseServicesInteropOption>。由于这两个值都依赖于一项无需组件即可调用服务的功能，因此在使用它们时，应在 Windows XP Service Pack 2 或 Windows Server 2003 上运行。  
  
 <xref:System.Transactions.EnterpriseServicesInteropOption> 指定 <xref:System.Transactions> 和 <xref:System.EnterpriseServices> 的环境事务始终是相同的。这会创建一个新的 <xref:System.EnterpriseServices> 事务性上下文，并使 <xref:System.Transactions.TransactionScope> 的当前事务成为该上下文的当前事务。因此，<xref:System.Transactions.Transaction.Current%2A> 中的事务与 <xref:System.EnterpriseServices.ContextUtil.Transaction%2A> 中的事务完全保持同步。该值会导致性能损失，因为可能会创建新的 COM\+ 上下文。  
  
 <xref:System.Transactions.EnterpriseServicesInteropOption> 指定下列要求：  
  
-   选中 <xref:System.Transactions.Transaction.Current%2A> 时，如果 <xref:System.Transactions> 检测到它没有运行在默认上下文中，则应支持 COM\+ 上下文中的事务。请注意，默认上下文不能包含事务。因此，在默认上下文中，即使使用 <xref:System.Transactions.EnterpriseServicesInteropOption>，也会对 <xref:System.Transactions.Transaction.Current%2A> 返回 <xref:System.Transactions> 所使用的、存储在线程本地存储区中的事务。  
  
-   如果创建一个新的 <xref:System.Transactions.TransactionScope> 对象，并在默认上下文之外的上下文中执行此操作，则 <xref:System.Transactions.TransactionScope> 对象的当前事务应在 COM\+ 中反映出来。在这种情况下，<xref:System.Transactions.EnterpriseServicesInteropOption> 的行为与 <xref:System.Transactions.EnterpriseServicesInteropOption> 类似，因为前者会创建新的 COM\+ 上下文。  
  
 此外，当在 <xref:System.Transactions.EnterpriseServicesInteropOption> 和 <xref:System.Transactions.EnterpriseServicesInteropOption> 中设置了 <xref:System.Transactions.Transaction.Current%2A> 时，这两种模式都表示不能直接设置 <xref:System.Transactions.Transaction.Current%2A>。任何直接设置 <xref:System.Transactions.Transaction.Current%2A> 而不是创建 <xref:System.Transactions.TransactionScope> 的尝试都会导致 <xref:System.InvalidOperationException>。<xref:System.Transactions.EnterpriseServicesInteropOption> 枚举值由未显式指定要使用哪个值的新事务范围继承。例如，如果用 <xref:System.Transactions.EnterpriseServicesInteropOption> 创建新的 <xref:System.Transactions.TransactionScope> 对象，然后创建另一个 <xref:System.Transactions.TransactionScope> 对象，但不指定 <xref:System.Transactions.EnterpriseServicesInteropOption> 值，则第二个 <xref:System.Transactions.TransactionScope> 对象也具有 <xref:System.Transactions.EnterpriseServicesInteropOption> 值。  
  
 总之，在创建新的事务范围时，应遵守下列规则：  
  
1.  检查 <xref:System.Transactions.Transaction.Current%2A> 以确定是否存在事务。此检查会执行下列操作：  
  
    -   检查是否存在范围。  
  
    -   如果存在范围，则选中最初创建该范围时传入的 <xref:System.Transactions.EnterpriseServicesInteropOption> 枚举值。  
  
    -   如果将 <xref:System.Transactions.EnterpriseServicesInteropOption> 枚举设置为 <xref:System.Transactions.EnterpriseServicesInteropOption>，则 COM\+ 事务（<xref:System.EnterpriseServices> 事务）将优先于托管线程本地存储区中的 <xref:System.Transactions> 事务。  
  
         如果将该枚举值设置为 <xref:System.Transactions.EnterpriseServicesInteropOption>，则托管线程本地存储区中的 <xref:System.Transactions> 事务将优先。  
  
         如果该枚举值为 <xref:System.Transactions.EnterpriseServicesInteropOption>，则仅存在一个事务，并且该事务是 COM\+ 事务。  
  
2.  检查由 <xref:System.Transactions.TransactionScope> 构造函数传入的 <xref:System.Transactions.TransactionScopeOption> 枚举值。这样可确定是否必须创建新事务。  
  
3.  如果需要创建新事务，则会生成 <xref:System.Transactions.EnterpriseServicesInteropOption> 的下列值：  
  
    -   <xref:System.Transactions.EnterpriseServicesInteropOption>：创建与 COM\+ 上下文关联的事务。  
  
    -   <xref:System.Transactions.EnterpriseServicesInteropOption>：创建 <xref:System.Transactions> 事务。  
  
    -   <xref:System.Transactions.EnterpriseServicesInteropOption>：如果存在 COM\+ 上下文，则会创建一个事务，并将其附加到该上下文。  
  
 下表使用 <xref:System.Transactions.EnterpriseServicesInteropOption> 枚举阐释了企业服务 \(ES\) 上下文和需要事务的事务范围。  
  
|ES 上下文|None|Automatic|Full|  
|------------|----------|---------------|----------|  
|默认上下文|默认上下文|默认上下文|创建新的<br />事务上下文|  
|非默认上下文|保持客户端的上下文|创建新的事务上下文|创建新的事务上下文|  
  
 下表使用 <xref:System.Transactions.EnterpriseServicesInteropOption> 枚举阐释了环境事务（给定特定的 <xref:System.EnterpriseServices> 上下文）和需要事务的事务范围。  
  
|ES 上下文|无|Automatic|Full|  
|------------|-------|---------------|----------|  
|默认上下文|ST|ST|ES|  
|非默认上下文|ST|ES|ES|  
  
 在上表中：  
  
-   ST 表示范围的环境事务由 <xref:System.Transactions> 管理，这一点不同于可能存在的任何 <xref:System.EnterpriseServices> 上下文的事务。  
  
-   ES 表示范围的环境事务与 <xref:System.EnterpriseServices> 上下文的事务相同。