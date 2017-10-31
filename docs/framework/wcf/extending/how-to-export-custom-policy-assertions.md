---
title: "如何：导出自定义策略断言 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 99030386-43b0-4f7b-866d-17ea307f5cbd
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# 如何：导出自定义策略断言
策略断言说明服务终结点的功能和要求。服务应用程序可以在服务元数据中使用自定义策略断言，来将终结点、绑定或协定自定义信息传递到客户端应用程序。您可以使用 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 根据通信的功能和要求导出终结点、操作或消息主题的 WSDL 绑定中附加的策略断言。  
  
 可以通过以下方式导出自定义策略断言：在 <xref:System.ServiceModel.Channels.BindingElement?displayProperty=fullName> 上实现 <xref:System.ServiceModel.Description.IPolicyExportExtension?displayProperty=fullName> 接口，然后或者将绑定元素直接插入到服务终结点的绑定，或者在应用程序配置文件中注册绑定元素。策略导出实现应将自定义策略断言作为 <xref:System.Xml.XmlElement?displayProperty=fullName> 实例添加到传入 <xref:System.ServiceModel.Description.IPolicyExportExtension.ExportPolicy%2A> 方法的 <xref:System.ServiceModel.Description.PolicyConversionContext?displayProperty=fullName> 上的相应 <xref:System.ServiceModel.Description.PolicyAssertionCollection?displayProperty=fullName>。  
  
 另外，您需要检查 <xref:System.ServiceModel.Description.WsdlExporter> 类的 <xref:System.ServiceModel.Description.MetadataExporter.PolicyVersion%2A> 属性，并根据指定的策略版本导出正确的命名空间中的嵌套策略表达式和策略框架属性。  
  
 若要导入自定义策略断言，请参见 <xref:System.ServiceModel.Description.IPolicyImportExtension?displayProperty=fullName> 和 [如何：导入自定义策略断言](../../../../docs/framework/wcf/extending/how-to-import-custom-policy-assertions.md)。  
  
### 导出自定义策略断言  
  
1.  在 <xref:System.ServiceModel.Channels.BindingElement?displayProperty=fullName> 上实现 <xref:System.ServiceModel.Description.IPolicyExportExtension?displayProperty=fullName> 接口。下面的代码示例演示了在绑定级别实现自定义策略断言。  
  
     [!code-csharp[CustomPolicySample#14](../../../../samples/snippets/csharp/VS_Snippets_CFX/custompolicysample/cs/policyexporter.cs#14)]
     [!code-vb[CustomPolicySample#14](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/custompolicysample/vb/policyexporter.vb#14)]  
  
2.  以编程方式或者使用应用程序配置文件将绑定元素插入到终结点绑定。请参见下面的过程。  
  
### 使用应用程序配置文件插入绑定元素  
  
1.  为自定义策略断言绑定元素实现 <xref:System.ServiceModel.Configuration.BindingElementExtensionElement?displayProperty=fullName>。  
  
2.  使用 [\<bindingElementExtensions\>](../../../../docs/framework/configure-apps/file-schema/wcf/bindingelementextensions.md) 元素将绑定元素扩展添加到配置文件。  
  
3.  使用 <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=fullName> 生成一个自定义绑定。  
  
### 以编程方式插入绑定元素  
  
1.  创建一个新的 <xref:System.ServiceModel.Channels.BindingElement?displayProperty=fullName> 并将其添加到 <xref:System.ServiceModel.Channels.CustomBinding?displayProperty=fullName>。  
  
2.  将步骤 1 中的自定义绑定添加到一个新的终结点，并通过调用 <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A> 方法将该新服务终结点添加到 <xref:System.ServiceModel.ServiceHost?displayProperty=fullName>。  
  
3.  打开 <xref:System.ServiceModel.ServiceHost>。下面的代码示例演示如何创建自定义绑定以及如何以编程方式插入绑定元素。  
  
     [!code-csharp[s_imperative#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_imperative/cs/service.cs#1)]
     [!code-vb[s_imperative#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_imperative/vb/service.vb#1)]  
  
## 请参阅  
 <xref:System.ServiceModel.Description.IPolicyImportExtension>   
 <xref:System.ServiceModel.Description.IPolicyExportExtension>   
 [如何：导入自定义策略断言](../../../../docs/framework/wcf/extending/how-to-import-custom-policy-assertions.md)