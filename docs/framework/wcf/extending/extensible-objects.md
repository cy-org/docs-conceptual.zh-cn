---
title: "可扩展对象 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "可扩展对象 [WCF]"
ms.assetid: bc88cefc-31fb-428e-9447-6d20a7d452af
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# 可扩展对象
可扩展对象模式用于使用新功能扩展现有运行时类，或者向对象中添加新状态。  附加到可扩展对象之一的扩展名，在访问附加到公共可扩展对象的共享状态和功能过程的各个不同阶段启用行为，各可扩展对象可以访问该公共扩展对象。  
  
## IExtensibleObject\<T\> 模式  
 可扩展对象模式中有三个接口：<xref:System.ServiceModel.IExtensibleObject%601>、<xref:System.ServiceModel.IExtension%601> 和 <xref:System.ServiceModel.IExtensionCollection%601>。  
  
 <xref:System.ServiceModel.IExtensibleObject%601> 接口通过允许 <xref:System.ServiceModel.IExtension%601> 对象自定义类型的功能的这些类型实现。  
  
 可扩展的对象允许动态聚合 <xref:System.ServiceModel.IExtension%601> 对象。  以下接口确定 <xref:System.ServiceModel.IExtension%601> 对象的特点：  
  
```  
public interface IExtension<T>  
where T : IExtensibleObject<T>  
{  
    void Attach(T owner);  
    void Detach(T owner);  
}  
```  
  
 类型限制保证仅为是 <xref:System.ServiceModel.IExtensibleObject%601> 的类定义扩展名。  <xref:System.ServiceModel.IExtension%601.Attach%2A> 和 <xref:System.ServiceModel.IExtension%601.Detach%2A> 提供聚合或解聚的通知。  
  
 对于实现限制它们何时可能会添加到所有者中或从所有者中移除有效。  例如，可以完全禁止移除（这将禁止在所有者或扩展名处于某个特定状态时添加或移除扩展名）、禁止同时添加多个所有者，或者仅允许单个移除后进行单个添加。  
  
 <xref:System.ServiceModel.IExtension%601> 不表示与其他标准托管接口进行的任何交互。  具体地说，所有者对象上的 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 方法通常不与它的扩展名分离。  
  
 将扩展名添加到集合中时，在 <xref:System.ServiceModel.IExtension%601.Attach%2A> 进入该集合前调用它。从集合中移除扩展名时，在移除 <xref:System.ServiceModel.IExtension%601.Detach%2A> 后调用它。这意味着（假设适当同步）当扩展名介于 <xref:System.ServiceModel.IExtension%601.Attach%2A> 和 <xref:System.ServiceModel.IExtension%601.Detach%2A> 之间时，仅可以在集合中找到它。  
  
 传递给 <xref:System.ServiceModel.IExtensionCollection%601.FindAll%2A> 或 <xref:System.ServiceModel.IExtensionCollection%601.Find%2A> 的对象不需要是 <xref:System.ServiceModel.IExtension%601>（例如，可以传递任何对象），但返回的扩展名是 <xref:System.ServiceModel.IExtension%601>。  
  
 如果集合中的扩展名不为 <xref:System.ServiceModel.IExtension%601>，则 <xref:System.ServiceModel.IExtensionCollection%601.Find%2A> 返回 null，并且 <xref:System.ServiceModel.IExtensionCollection%601.FindAll%2A> 返回一个空集合。如果多个扩展名实现 <xref:System.ServiceModel.IExtension%601>，则 <xref:System.ServiceModel.IExtensionCollection%601.Find%2A> 返回其中一个扩展名。  从 <xref:System.ServiceModel.IExtensionCollection%601.FindAll%2A> 中返回的值是快照。  
  
 有两种主要方案。  第一个方案使用 <xref:System.ServiceModel.IExtensibleObject%601.Extensions%2A> 属性作为基于类型的字典插入对象状态，以使另一组件使用该类型进行查找。  
  
 第二个方案使用 <xref:System.ServiceModel.IExtension%601.Attach%2A> 和 <xref:System.ServiceModel.IExtension%601.Detach%2A> 属性使对象可以参与自定义行为，例如注册事件、监视状态转换等。  
  
 <xref:System.ServiceModel.IExtensionCollection%601> 接口是允许按照其类型检索 <xref:System.ServiceModel.IExtension%601> 的 <xref:System.ServiceModel.IExtension%601> 对象集合。  <xref:System.ServiceModel.IExtensionCollection%601.Find%2A?displayProperty=fullName> 返回最近添加的对象，此对象是属于该类型的 <xref:System.ServiceModel.IExtension%601>。  
  
### Windows Communication Foundation 中的可扩展对象  
 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 中包含四个可扩展对象：  
  
-   <xref:System.ServiceModel.ServiceHostBase> — 这是服务主机的基类。  此类的扩展名可用于扩展 <xref:System.ServiceModel.ServiceHostBase> 自身的行为，或者用于存储每个服务的状态。  
  
-   <xref:System.ServiceModel.InstanceContext> — 此类将服务类型的实例与服务运行时相连。  它包含有关该实例的信息以及对 <xref:System.ServiceModel.InstanceContext> 的包含 <xref:System.ServiceModel.ServiceHostBase> 的引用。  此类的扩展名可用于扩展 <xref:System.ServiceModel.InstanceContext> 的行为，或者用于存储每个服务的状态。  
  
-   <xref:System.ServiceModel.OperationContext> — 此类表示为每个操作收集的运行时的操作信息。  这包括的信息有：传入消息头、传入消息属性和传入安全标识，以及其他信息。  此类的扩展名可以扩展 <xref:System.ServiceModel.OperationContext> 的行为，也可以存储每个操作的状态。  
  
-   <xref:System.ServiceModel.IContextChannel> — 此接口允检查 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 运行时生成的通道和代理的每个状态。  此类的扩展名可以扩展 <xref:System.ServiceModel.IClientChannel> 的行为，也可以使用它存储每个通道的状态。  
  
 下面的代码示例演示使用简单的扩展名来跟踪 <xref:System.ServiceModel.InstanceContext> 对象。  
  
 [!code-csharp[IInstanceContextInitializer#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/iinstancecontextinitializer/cs/initializer.cs#1)]  
  
## 请参阅  
 <xref:System.ServiceModel.IExtensibleObject%601>   
 <xref:System.ServiceModel.IExtension%601>   
 <xref:System.ServiceModel.IExtensionCollection%601>