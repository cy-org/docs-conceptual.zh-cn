---
title: "如何：配置自定义 WS-Metadata Exchange 绑定 | Microsoft Docs"
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
  - "WS-Metadata Exchange [WCF]"
  - "WS-Metadata Exchange [WCF], 配置自定义绑定"
ms.assetid: cdba4d73-da64-4805-bc56-9822becfd1e4
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 如何：配置自定义 WS-Metadata Exchange 绑定
本主题将说明如何配置自定义 WS\-Metadata 交换绑定。  [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 提供四种系统定义的元数据绑定，不过，您可以使用所需的任何绑定来发布元数据。  本主题将演示如何使用 `wsHttpBinding` 发布元数据。  此绑定提供了以安全方式公开元数据的选择。  本文中的代码基于[入门](../../../../docs/framework/wcf/samples/getting-started-sample.md)。  
  
### 使用配置文件  
  
1.  在服务的配置文件中，添加一个包含 `serviceMetadata` 标记的服务行为：  
  
    ```  
    <behaviors>  
       <serviceBehaviors>  
         <behavior name="CalculatorServiceBehavior">  
           <serviceMetadata httpGetEnabled="True"/>  
         </behavior>  
       </serviceBehaviors>  
    </behaviors>  
    ```  
  
2.  将一个 `behaviorConfiguration` 属性添加到该服务标记，该属性引用这一新行为：  
  
    ```  
    <service        name="Microsoft.ServiceModel.Samples.CalculatorService"  
    behaviorConfiguration="CalculatorServiceBehavior">   
    ```  
  
3.  添加一个元数据终结点，该终结点将 mex 指定为地址，将 `wsHttpBinding` 指定为绑定，并将 <xref:System.ServiceModel.Description.IMetadataExchange> 指定为协定：  
  
    ```  
    <endpoint address="mex"  
              binding="wsHttpBinding"  
              contract="IMetadataExchange" />  
    ```  
  
4.  若要验证元数据交换终结点是否能够正常工作，请在客户端配置文件中添加一个终结点标记：  
  
    ```  
    <endpoint name="MyMexEndpoint"               address="http://localhost:8000/servicemodelsamples/service/mex"  
              binding="wsHttpBinding"  
              contract="IMetadataExchange"/>  
    ```  
  
5.  在客户端的 Main\(\) 方法中，创建一个新的 <xref:System.ServiceModel.Description.MetadataExchangeClient> 实例，将该实例的 <xref:System.ServiceModel.Description.MetadataExchangeClient.ResolveMetadataReferences%2A> 属性设置为 `true`，调用 <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A>，然后循环访问返回的元数据集合：  
  
    ```  
    string mexAddress = "http://localhost:8000/servicemodelsamples/service/mex";  
  
    MetadataExchangeClient mexClient = new MetadataExchangeClient("MyMexEndpoint");  
    mexClient.ResolveMetadataReferences = true;  
    MetadataSet mdSet = mexClient.GetMetadata(new EndpointAddress(mexAddress));  
    foreach (MetadataSection section in mdSet.MetadataSections)  
    Console.WriteLine("Metadata section: " + section.Dialect.ToString());  
    ```  
  
### 通过代码进行配置  
  
1.  创建一个 <xref:System.ServiceModel.WsHttpBinding> 绑定实例：  
  
    ```  
    WSHttpBinding binding = new WSHttpBinding();  
    ```  
  
2.  创建一个 <xref:System.ServiceModel.ServiceHost> 实例：  
  
    ```  
    ServiceHost serviceHost = new ServiceHost(typeof(CalculatorService), baseAddress);  
    ```  
  
3.  添加一个服务终结点，并添加一个 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 实例：  
  
    ```  
    serviceHost.AddServiceEndpoint(typeof(ICalculator), binding, baseAddress);  
    ServiceMetadataBehavior smb = new ServiceMetadataBehavior();  
    smb.HttpGetEnabled = true;  
    serviceHost.Description.Behaviors.Add(smb);  
    ```  
  
4.  添加一个元数据交换终结点，并且指定先前创建的 <xref:System.ServiceModel.WSHttpBinding>：  
  
    ```  
    serviceHost.AddServiceEndpoint(typeof(IMetadataExchange), binding, mexAddress);  
    ```  
  
5.  若要验证元数据交换终结点是否能够正常工作，请在客户端配置文件中添加一个终结点标记：  
  
    ```  
    <endpoint name="MyMexEndpoint"               address="http://localhost:8000/servicemodelsamples/service/mex"  
              binding="wsHttpBinding"  
              contract="IMetadataExchange"/>  
    ```  
  
6.  在客户端的 Main\(\) 方法中，创建一个新的 <xref:System.ServiceModel.Description.MetadataExchangeClient> 实例，将该实例的 <xref:System.ServiceModel.Description.MetadataExchangeClient.ResolveMetadataReferences%2A> 属性设置为 `true`，调用 <xref:System.ServiceModel.Description.MetadataExchangeClient.GetMetadata%2A>，然后循环访问返回的元数据集合：  
  
    ```  
    string mexAddress = "http://localhost:8000/servicemodelsamples/service/mex";  
  
    MetadataExchangeClient mexClient = new MetadataExchangeClient("MyMexEndpoint");  
    mexClient.ResolveMetadataReferences = true;  
    MetadataSet mdSet = mexClient.GetMetadata(new EndpointAddress(mexAddress));  
    foreach (MetadataSection section in mdSet.MetadataSections)  
    Console.WriteLine("Metadata section: " + section.Dialect.ToString());  
  
    ```  
  
## 请参阅  
 [元数据发布行为](../../../../docs/framework/wcf/samples/metadata-publishing-behavior.md)   
 [检索元数据](../../../../docs/framework/wcf/samples/retrieve-metadata.md)   
 [元数据](../../../../docs/framework/wcf/feature-details/metadata.md)   
 [发布元数据](../../../../docs/framework/wcf/feature-details/publishing-metadata.md)   
 [发布元数据终结点](../../../../docs/framework/wcf/publishing-metadata-endpoints.md)