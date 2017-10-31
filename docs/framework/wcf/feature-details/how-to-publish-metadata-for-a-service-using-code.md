---
title: "如何：使用代码发布服务的元数据 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 51407e6d-4d87-42d5-be7c-9887b8652006
caps.latest.revision: 19
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 19
---
# 如何：使用代码发布服务的元数据
这是讨论发布 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务的元数据的两个帮助主题之一。有两种方式可以指定服务应如何发布元数据：使用配置文件和使用代码。本主题演示如何使用代码发布服务的元数据。  
  
> [!CAUTION]
>  本主题演示如何以不安全的方式发布元数据。任何客户端都可以检索服务的元数据。如果您要求服务以安全方式发布元数据。请参见 [自定义安全元数据终结点](../../../../docs/framework/wcf/samples/custom-secure-metadata-endpoint.md)。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]在配置文件中发布元数据的更多信息，请参见[如何：使用配置文件发布服务的元数据](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)。通过发布元数据，客户端可以使用 WS\-Transfer GET 请求或使用 `?wsdl` 查询字符串的 HTTP\/GET 来检索元数据。若要确保代码能够工作，必须创建一个基本的 WCF 服务。在以下代码中提供了一个基本的自承载服务。  
  
 [!code-csharp[htPublishMetadataCode#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#0)]
 [!code-vb[htPublishMetadataCode#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#0)]  
  
### 在代码中发布元数据  
  
1.  在控制台应用程序的主方法中，通过传入服务类型和基址来实例化 <xref:System.ServiceModel.ServiceHost> 对象。  
  
     [!code-csharp[htPublishMetadataCode#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#1)]
     [!code-vb[htPublishMetadataCode#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#1)]  
  
2.  紧接在步骤 1 的代码下面创建一个 try 块，这将捕获在服务运行过程中引发的任何异常。  
  
     [!code-csharp[htPublishMetadataCode#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#2)]
     [!code-vb[htPublishMetadataCode#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#2)]  
  
     [!code-csharp[htPublishMetadataCode#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#3)]
     [!code-vb[htPublishMetadataCode#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#3)]  
  
3.  检查服务主机是否已经包含一个 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>，如果没有，则创建一个新的 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 实例。  
  
     [!code-csharp[htPublishMetadataCode#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#4)]
     [!code-vb[htPublishMetadataCode#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#4)]  
  
4.  将 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpGetEnabled%2A> 属性设置为 `true.`  
  
     [!code-csharp[htPublishMetadataCode#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#5)]
     [!code-vb[htPublishMetadataCode#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#5)]  
  
5.  <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 包含一个 <xref:System.ServiceModel.Description.MetadataExporter> 属性。<xref:System.ServiceModel.Description.MetadataExporter> 包含一个 <xref:System.ServiceModel.Description.MetadataExporter.PolicyVersion%2A> 属性。将 <xref:System.ServiceModel.Description.MetadataExporter.PolicyVersion%2A> 属性的值设置为 <xref:System.ServiceModel.Description.PolicyVersion.Policy15%2A>。还可以将 <xref:System.ServiceModel.Description.MetadataExporter.PolicyVersion%2A> 属性设置为 <xref:System.ServiceModel.Description.PolicyVersion.Policy12%2A>。当设置为 <xref:System.ServiceModel.Description.PolicyVersion.Policy15%2A> 时，元数据导出程序会使用符合 WS\-Policy 1.5 的元数据生成策略信息。当设置为 <xref:System.ServiceModel.Description.PolicyVersion.Policy12%2A> 时，元数据导出程序会生成符合 WS\-Policy 1.2 的策略信息。  
  
     [!code-csharp[htPublishMetadataCode#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#6)]
     [!code-vb[htPublishMetadataCode#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#6)]  
  
6.  将 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 实例添加到服务主机的行为集合。  
  
     [!code-csharp[htPublishMetadataCode#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#7)]
     [!code-vb[htPublishMetadataCode#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#7)]  
  
7.  将元数据交换终结点添加到服务主机。  
  
     [!code-csharp[htPublishMetadataCode#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#8)]
     [!code-vb[htPublishMetadataCode#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#8)]  
  
8.  将应用程序终结点添加到服务主机。  
  
     [!code-csharp[htPublishMetadataCode#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#9)]
     [!code-vb[htPublishMetadataCode#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#9)]  
  
    > [!NOTE]
    >  如果不希望向服务添加任何终结点，则运行时为您添加默认终结点。在此示例中，由于服务的 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 设置为 `true`，服务还启用了发布元数据。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]默认终结点的更多信息，请参见[简化配置](../../../../docs/framework/wcf/simplified-configuration.md)和 [WCF 服务的简化配置](../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md)。  
  
9. 打开服务主机并等待传入调用。当用户按 Enter 时，关闭服务主机。  
  
     [!code-csharp[htPublishMetadataCode#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#10)]
     [!code-vb[htPublishMetadataCode#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#10)]  
  
10. 生成并运行控制台应用程序。  
  
11. 使用 Internet Explorer 浏览服务的基址（本示例中的 http:\/\/localhost:8001\/MetadataSample）并验证是否已打开元数据发布。您应会看到一个网页，该网页顶部显示“Simple Service”（简单服务），其下面紧接着显示“You have created a service”（已经创建服务）。如果未显示上述内容，则结果页顶部会显示消息：“Metadata publishing for this service is currently disabled”（当前禁用服务的元数据发布）。  
  
## 示例  
 下面的代码示例演示如何在代码中实现发布服务的元数据的基本 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务。  
  
 [!code-csharp[htPublishMetadataCode#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/htpublishmetadatacode/cs/program.cs#11)]
 [!code-vb[htPublishMetadataCode#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htpublishmetadatacode/vb/program.vb#11)]  
  
## 请参阅  
 [如何：在托管应用程序中承载 WCF 服务](../../../../docs/framework/wcf/how-to-host-a-wcf-service-in-a-managed-application.md)   
 [自承载](../../../../docs/framework/wcf/samples/self-host.md)   
 [元数据体系结构概述](../../../../docs/framework/wcf/feature-details/metadata-architecture-overview.md)   
 [使用元数据](../../../../docs/framework/wcf/feature-details/using-metadata.md)   
 [如何：使用配置文件发布服务的元数据](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)