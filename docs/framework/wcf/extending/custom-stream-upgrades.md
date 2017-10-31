---
title: "自定义流升级 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e3da85c8-57f3-4e32-a4cb-50123f30fea6
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# 自定义流升级
面向流的传输（如 TCP 和命名管道）对客户端与服务器之间的连续字节流进行操作。  该流通过 <xref:System.IO.Stream> 对象实现。  在流升级中，客户端需要向通道堆栈中添加可选的协议层，并要求通信通道的另一端也执行该操作。  流升级包括使用升级后的对象替换原始 <xref:System.IO.Stream> 对象的过程。  
  
 例如，可以直接在传输流之上生成压缩流。  在这种情况下，原始传输 <xref:System.IO.Stream> 将替换为围绕原始传输流包装压缩 <xref:System.IO.Stream> 的传输流。  
  
 可以应用多次流升级，每次升级都包装前一次升级。  
  
## 流升级如何工作  
 流升级过程包括四个部分。  
  
1.  升级流发起程序开始该过程：在运行时，发起程序可以向其连接的另一端发起升级通道传输层的请求。  
  
2.  升级流接受程序执行该升级：在运行时，接受程序接收来自其他计算机的升级请求，如果可能，将接受该升级。  
  
3.  升级提供程序在客户端上创建发起程序，并在服务器上创建接受程序。  
  
4.  流升级绑定元素将添加到服务和客户端上的绑定，并在运行时创建提供程序。  
  
 请注意，如果要进行多个升级，则发起程序和接受程序将会封装状态计算机，以便强制实施哪些升级转变对于每次“发起”都是有效的。  
  
## 如何实现流升级  
 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 提供了四个可以实现的 `abstract` 类：  
  
-   <xref:System.ServiceModel.Channels.StreamUpgradeInitiator?displayProperty=fullName>  
  
-   <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor?displayProperty=fullName>  
  
-   <xref:System.ServiceModel.Channels.StreamUpgradeProvider?displayProperty=fullName>  
  
-   <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement?displayProperty=fullName>  
  
 若要实现自定义流升级，请执行下列操作。  此过程在客户端计算机和服务器计算机上均实现最低流升级过程。  
  
1.  创建用于实现 <xref:System.ServiceModel.Channels.StreamUpgradeInitiator> 的类。  
  
    1.  重写要在所升级的流中采用的 <xref:System.ServiceModel.Channels.StreamUpgradeInitiator.InitiateUpgrade%2A> 方法，并返回升级后的流。  此方法同步工作；异步启动升级存在类似方法。  
  
    2.  重写 <xref:System.ServiceModel.Channels.StreamUpgradeInitiator.GetNextUpgrade%2A> 方法以检查其他升级。  
  
2.  创建用于实现 <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor> 的类。  
  
    1.  重写要在所升级的流中采用的 <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor.AcceptUpgrade%2A> 方法，并返回升级后的流。  此方法同步工作；异步接受升级存在类似方法。  
  
    2.  重写 <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor.CanUpgrade%2A> 方法，以确定在升级过程中的此时该升级接受程序是否支持请求的升级。  
  
3.  创建用于实现 <xref:System.ServiceModel.Channels.StreamUpgradeProvider> 的类。  重写 <xref:System.ServiceModel.Channels.StreamUpgradeProvider.CreateUpgradeAcceptor%2A> 方法和 <xref:System.ServiceModel.Channels.StreamUpgradeProvider.CreateUpgradeInitiator%2A> 方法，以返回步骤 2 和步骤 1 中定义的接受程序和发起程序的实例。  
  
4.  创建用于实现 <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement> 的类。  
  
    1.  在客户端上重写 <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement.BuildClientStreamUpgradeProvider%2A> 方法，然后在服务上重写 <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement.BuildServerStreamUpgradeProvider%2A> 方法。  
  
    2.  在客户端上重写 <xref:System.ServiceModel.Channels.BindingElement.BuildChannelFactory%2A> 方法，然后在服务上重写 <xref:System.ServiceModel.Channels.BindingElement.BuildChannelListener%2A> 方法，以便将升级“绑定元素”添加到 <xref:System.ServiceModel.Channels.BindingContext.BindingParameters%2A>。  
  
5.  将新的流升级绑定元素添加到服务器计算机和客户端计算机上的绑定。  
  
## 安全升级  
 添加安全升级是常规流升级过程的专用版本。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 已为升级流安全提供了两个绑定元素。  传输级安全的配置由 <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement> 和 <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement> 封装，可以对该两个元素进行配置并将其添加到自定义绑定。  这些绑定元素扩展用于生成客户端和服务器流升级提供程序的 <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement> 类。  这些绑定元素包含的方法可用于创建专用的安全流升级提供程序类（不是 `public`），因此对于这两种情况，您需要做的只是将绑定元素添加到绑定。  
  
 对于上述两个绑定元素都不满足的安全方案，可从上述发起程序、接受程序和提供程序的基类派生三个与安全相关的 `abstract` 类：  
  
1.  <xref:System.ServiceModel.Channels.StreamSecurityUpgradeInitiator?displayProperty=fullName>  
  
2.  <xref:System.ServiceModel.Channels.StreamSecurityUpgradeAcceptor?displayProperty=fullName>  
  
3.  <xref:System.ServiceModel.Channels.StreamSecurityUpgradeProvider?displayProperty=fullName>  
  
 实现安全流升级的过程与以前的升级过程基本相同，不同的是将从这三个类进行派生。  重写这些类中的其他属性以便为运行时提供安全信息。  
  
## 多个升级  
 若要创建其他升级请求，请重复上述过程：创建 <xref:System.ServiceModel.Channels.StreamUpgradeProvider> 的附加扩展和绑定元素。  将绑定元素添加到绑定。  这些附加绑定元素将按顺序进行处理，首先处理添加到绑定的第一个绑定元素。  在 <xref:System.ServiceModel.Channels.BindingElement.BuildChannelFactory%2A> 和 <xref:System.ServiceModel.Channels.BindingElement.BuildChannelListener%2A> 中，每个升级提供程序均可确定如何在任何已预先存在的升级绑定参数上对自身进行分层。  然后，它应使用新的复合升级绑定参数替换现有的升级绑定参数。  
  
 或者，一个升级提供程序可以支持多个升级。  例如，您可能需要实现既支持安全又支持压缩的自定义流升级提供程序。  请执行下列步骤：  
  
1.  创建 <xref:System.ServiceModel.Channels.StreamSecurityUpgradeProvider> 的子类，以编写用于创建发起程序和接受程序的提供程序类。  
  
2.  创建 <xref:System.ServiceModel.Channels.StreamSecurityUpgradeInitiator> 的子类，确保重写 <xref:System.ServiceModel.Channels.StreamUpgradeInitiator.GetNextUpgrade%2A> 方法以按顺序返回压缩流和安全流的内容类型。  
  
3.  创建理解其 <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor.CanUpgrade%2A> 方法中的自定义内容类型的 <xref:System.ServiceModel.Channels.StreamSecurityUpgradeAcceptor> 的子类。  
  
4.  每次调用 <xref:System.ServiceModel.Channels.StreamUpgradeInitiator.GetNextUpgrade%2A> 和 <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor.CanUpgrade%2A> 之后，都会升级该流。  
  
## 请参阅  
 <xref:System.ServiceModel.Channels.StreamUpgradeInitiator>   
 <xref:System.ServiceModel.Channels.StreamSecurityUpgradeInitiator>   
 <xref:System.ServiceModel.Channels.StreamUpgradeAcceptor>   
 <xref:System.ServiceModel.Channels.StreamSecurityUpgradeAcceptor>   
 <xref:System.ServiceModel.Channels.StreamUpgradeProvider>   
 <xref:System.ServiceModel.Channels.StreamSecurityUpgradeProvider>   
 <xref:System.ServiceModel.Channels.StreamUpgradeBindingElement>   
 <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement>   
 <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement>