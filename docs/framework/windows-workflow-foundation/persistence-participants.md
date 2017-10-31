---
title: "持久性参与者 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f84d2d5d-1c1b-4f19-be45-65b552d3e9e3
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# 持久性参与者
持久性参与者可以参与应用程序宿主触发的持久性操作（保存或加载）。[!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)]附带两个抽象类：**PersistenceParticipant** 和 **PersistenceIOParticipant**，您可以使用它们来创建持久性参与者。持久性参与者派生自这些类之一，它实现所需的方法，然后将该类的实例添加到 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 上的 <xref:System.ServiceModel.Activities.WorkflowServiceHost.WorkflowExtensions%2A> 集合。应用程序宿主可在持久保存工作流实例时查找此类工作流扩展，并在适当时对持久性参与者调用适当的方法。  
  
 下面的列表介绍持久性子系统在持久保存（保存）操作的不同阶段执行的任务。持久性参与者用在第三和第四个阶段。如果参与者是 IO 参与者（还参与 IO 操作的持久性参与者），则该参与者还将在第六个阶段中使用。  
  
1.  收集内置值，包括工作流状态、书签、映射变量和时间戳。  
  
2.  收集已添加到与工作流实例关联的扩展集合中的所有持久性参与者。  
  
3.  调用由所有持久性参与者实现的 <xref:System.Activities.Persistence.PersistenceParticipant.CollectValues%2A> 方法。  
  
4.  调用由所有持久性参与者实现的 <xref:System.Activities.Persistence.PersistenceParticipant.MapValues%2A> 方法。  
  
5.  将工作流持久保存或保存到持久性存储区。  
  
6.  对所有持久性 IO 参与者调用 <xref:System.Activities.Persistence.PersistenceIOParticipant.BeginOnSave%2A> 方法。如果参与者不是 IO 参与者，则跳过此任务。如果持久性段是事务性的，则在 Transaction.Current 属性中提供事务。  
  
7.  等待所有持久性参与者完成。如果所有参与者在持久保存实例数据时都成功，则提交事务。  
  
 持久性参与者派生自 **PersistenceParticipant** 类，可以实现 **CollectValues** 和 **MapValues** 方法。持久性 IO 参与者派生自 **PersistenceIOParticipant** 类，除了实现 **CollectValues** 和 **MapValues** 方法外，还可以实现 **BeginOnSave** 方法。  
  
 一个阶段完成之后才开始下一个阶段。例如，从第一个阶段中的**所有**持久性参与者收集值。然后，将在第一个阶段中收集的所有值提供给第二个阶段中的所有持久性参与者进行映射。接下来，将在第一个阶段中收集的和在第二个阶段中映射的所有值提供给第三个阶段中的持久性提供程序，依此类推。  
  
 下面的列表介绍持久性子系统在加载操作的不同阶段执行的任务。持久性参与者用在第四个阶段中。持久性 IO 参与者（还参与 IO 操作的持久性参与者）还在第三个阶段中使用。  
  
1.  收集已添加到与工作流实例关联的扩展集合中的所有持久性参与者。  
  
2.  从持久性存储区加载工作流。  
  
3.  对所有持久性 IO 参与者调用 <xref:System.Activities.Persistence.PersistenceIOParticipant.BeginOnLoad%2A>，并等待所有持久性参与者完成。如果持久性段是事务性的，则在 Transaction.Current 中提供事务。  
  
4.  基于从持久性存储区检索的数据将工作流实例加载到内存中。  
  
5.  对每个持久性参与者调用 <xref:System.Activities.Persistence.PersistenceParticipant.PublishValues%2A>。  
  
 持久性参与者派生自 **PersistenceParticipant** 类，可以实现 **PublishValues** 方法。持久性 IO 参与者派生自 **PersistenceIOParticipant** 类，除了实现 **PublishValues** 方法外，还可以实现 **BeginOnLoad** 方法。  
  
 加载工作流实例时持久性提供程序将在该实例上创建锁。这可防止加载方案的多节点中的多个主机的实例。如果您试图加载已锁定的工作流实例，您将看到像下面的异常：异常" System.ServiceModel.Persistence.InstanceLockException：所请求的操作无法完成，因为该锁的实例 '00000000 0000 0000 0000 000000000000' 无法获取"。该错误发生在下列情况之一引起：  
  
-   在方案的多节点实例是由另一台主机加载。有几个不同的方法来解决这些类型的冲突：转发到的节点拥有锁和重试，处理或强制的负载，这会导致与其他主机无法保存他们的工作。  
  
-   在一个单节点方案和主机出现故障。主机启动时再次 （进程回收或创建新的持久性提供程序工厂） 新主机尝试加载一个实例，因为锁没有过期旧宿主仍锁定。  
  
-   单节点方案和实例问题已中止在一些点，创建一个新的持久性提供程序实例，有一个不同的主机 ID。  
  
 锁超时值的默认值为 5 分钟，在调用时，可以指定一个不同的超时值 <xref:System.ServiceModel.Persistence.PersistenceProvider.Load%2A>。  
  
## 本节内容  
  
-   [如何：创建自定义持久性参与者](../../../docs/framework/windows-workflow-foundation//how-to-create-a-custom-persistence-participant.md)  
  
## 请参阅  
 [存储扩展性](../../../docs/framework/windows-workflow-foundation//store-extensibility.md)