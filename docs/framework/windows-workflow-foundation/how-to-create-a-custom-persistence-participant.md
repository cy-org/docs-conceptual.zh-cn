---
title: "如何：创建自定义持久性参与者 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1d9cc47a-8966-4286-94d5-4221403d9c06
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 如何：创建自定义持久性参与者
下列过程包含持久性参与者的创建步骤。有关持久性参与者的示例实现，请参见 [Participating in Persistence](http://go.microsoft.com/fwlink/?LinkID=177735)（参与持久性）示例和[存储扩展性](../../../docs/framework/windows-workflow-foundation//store-extensibility.md)主题。  
  
1.  创建一个派生自 <xref:System.Activities.Persistence.PersistenceParticipant> 或 <xref:System.Activities.Persistence.PersistenceIOParticipant> 类的类。除能够参与 IO 操作以外，PersistenceIOParticipant 类还提供与 PersistenceParticipant 类相同的扩展点。请完成以下一个或多个步骤。  
  
2.  实现 <xref:System.Activities.Persistence.PersistenceParticipant.CollectValues%2A> 方法。**CollectValues** 方法具有两个字典参数，其中一个字典参数用于存储读\/写值，另一个字典参数用于存储只写值（稍后在查询中使用）。在此方法中，应使用特定于持久性参与者的数据填充这些字典。每个字典都包含值的名称和值自身，前者作为键，后者作为 <xref:System.Runtime.DurableInstancing.InstanceValue> 对象。  
  
     readWriteValues 字典中的值打包为 **InstanceValue** 对象。只写字典中的值打包为设置了 InstanceValueOptions.Optional 和 InstanceValueOption.WriteOnly 的 **InstanceValue** 对象。所有持久性参与者的 **CollectValues** 实现提供的各 **InstanceValue** 必须具有唯一的名称。  
  
    ```  
    protected virtual void CollectValues (out IDictionary<XName,Object> readWriteValues, out IDictionary<XName,Object> writeOnlyValues)  
  
    ```  
  
3.  实现 <xref:System.Activities.Persistence.PersistenceParticipant.MapValues%2A> 方法。**MapValues** 方法采用的两个参数类似于 **CollectValues** 方法接收到的参数。在 **CollectValues** 阶段收集的所有值都通过这些字典参数传递。**MapValues** 阶段添加的新值添加到只写值中。只写字典用于提供外部源不直接与实例值相关联的数据。所有持久性参与者的 **MapValues** 方法实现提供的各个值必须具有唯一的名称。  
  
    ```  
    protected virtual IDictionary<XName,Object> MapValues (IDictionary<XName,Object> readWriteValues,IDictionary<XName,Object> writeOnlyValues)  
    ```  
  
     <xref:System.Activities.Persistence.PersistenceParticipant.MapValues%2A> 方法提供 <xref:System.Activities.Persistence.PersistenceParticipant.CollectValues%2A> 不实现的功能，因为它允许由另一个持久性参与者提供另一个值的依赖项，该参与者尚未经过 <xref:System.Activities.Persistence.PersistenceParticipant.CollectValues%2A> 的处理。  
  
4.  实现 **PublishValues** 方法。**PublishValues** 方法接收一个包含从持久性存储加载的所有值的字典。  
  
    ```  
    protected virtual void PublishValues (IDictionary<XName,Object> readWriteValues)  
  
    ```  
  
5.  如果参与者是持久性 IO 参与者，请实现 **BeginOnSave** 方法。在执行保存操作期间，将调用此方法。在该方法中，应执行持久保存（保存）工作流实例的附加 IO。如果主机正将事务用于相应的持久性命令，则会在 Transaction.Current 中提供相同事务。此外，持久性 IO 参与者可公布事务一致性要求，在这种情况中，主机将为持久性段创建一个事务（如果不会在其他情况下使用该事务）。  
  
    ```  
  
    protected virtual IAsyncResult BeginOnSave (IDictionary<XName,Object> readWriteValues, IDictionary<XName,Object> writeOnlyValues, TimeSpan timeout, AsyncCallback callback, Object state)  
    ```  
  
6.  如果参与者是持久性 IO 参与者，请实现 **BeginOnLoad** 方法。在执行加载操作期间，将调用此方法。在该方法中，应执行加载工作流实例的附加 IO。如果主机正将事务用于相应的持久性命令，则会在 Transaction.Current 中提供相同事务。此外，持久性 IO 参与者可公布事务一致性要求，在这种情况中，主机将为持久性段创建一个事务（如果不会在其他情况下使用该事务）。  
  
    ```  
  
    protected virtual IAsyncResult BeginOnLoad (IDictionary<XName,Object> readWriteValues, TimeSpan timeout, AsyncCallback callback, Object state)  
  
    ```