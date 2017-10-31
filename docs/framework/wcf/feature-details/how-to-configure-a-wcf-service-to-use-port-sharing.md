---
title: "如何：配置 Windows Communication Foundation 服务以使用端口共享 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6400bc71-a858-4ac2-8d5a-caa72d3b5482
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# 如何：配置 Windows Communication Foundation 服务以使用端口共享
在 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 应用程序中使用 net.tcp:\/\/ 端口共享的最简单方式是使用 <xref:System.ServiceModel.NetTcpBinding> 公开一个服务。  
  
 此绑定提供了一个 <xref:System.ServiceModel.NetTcpBinding.PortSharingEnabled%2A> 属性，该属性控制是否为配置了此绑定的服务启用 net.tcp:\/\/ 端口共享。  
  
 下面的过程演示如何使用 <xref:System.ServiceModel.NetTcpBinding> 类打开一个位于统一资源标识符 \(URI\) net.tcp:\/\/localhost\/MyService 上的终结点（首先使用代码，然后使用配置元素）。  
  
### 使用代码在 NetTcpBinding 上启用 net.tcp:\/\/ 端口共享  
  
1.  创建一个服务以实现一个名为 `IMyService` 的协定，并将该服务命名为 `MyService`。  
  
     [!code-csharp[c_ConfigurePortSharing#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_configureportsharing/cs/source.cs#1)]
     [!code-vb[c_ConfigurePortSharing#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_configureportsharing/vb/source.vb#1)]  
  
2.  创建 <xref:System.ServiceModel.NetTcpBinding> 类的一个实例，并将 <xref:System.ServiceModel.NetTcpBinding.PortSharingEnabled%2A> 属性设置为 `true`。  
  
     [!code-csharp[c_ConfigurePortSharing#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_configureportsharing/cs/source.cs#2)]
     [!code-vb[c_ConfigurePortSharing#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_configureportsharing/vb/source.vb#2)]  
  
3.  创建一个 <xref:System.ServiceModel.ServiceHost>，并在其中为 `MyService` 添加一个服务终结点，该终结点使用启用了端口共享的 <xref:System.ServiceModel.NetTcpBinding> 并在终结点地址 URI“net.tcp:\/\/localhost\/MyService”上进行侦听。  
  
     [!code-csharp[c_ConfigurePortSharing#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_configureportsharing/cs/source.cs#3)]
     [!code-vb[c_ConfigurePortSharing#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_configureportsharing/vb/source.vb#3)]  
  
    > [!NOTE]
    >  此示例使用默认的 TCP 端口 808，因为终结点地址 URI 未指定其他端口号。由于在传输绑定上显式启用了端口共享，因此该服务可以与其他进程中的其他服务共享端口 808。如果不允许使用端口共享并且其他应用程序已在使用端口 808，则该服务在打开时会引发 <xref:System.ServiceModel.AddressAlreadyInUseException>。  
  
### 使用配置在 NetTcpBinding 上启用 net.tcp:\/\/ 端口共享  
  
1.  下面的示例演示如何使用配置元素来启用端口共享以及添加服务终结点。  
  
```  
<system.serviceModel>  
  <bindings>  
    <netTcpBinding name="portSharingBinding"   
                   portSharingEnabled="true" />  
  </bindings>  
  <services>  
    <service name="MyService">  
        <endpoint address="net.tcp://localhost/MyService"  
                  binding="netTcpBinding"  
                  contract="IMyService"  
                  bindingConfiguration="portSharingBinding" />  
    </service>  
  </services>  
</system.serviceModel>  
```  
  
## 请参阅  
 [Net.TCP Port Sharing](http://msdn.microsoft.com/zh-cn/f13692ee-a179-4439-ae72-50db9534eded)   
 [如何：启用 Net.TCP 端口共享服务](../../../../docs/framework/wcf/feature-details/how-to-enable-the-net-tcp-port-sharing-service.md)