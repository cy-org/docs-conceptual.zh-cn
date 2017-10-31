---
title: "如何：检索元数据并实现兼容服务。 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f6f3a2b9-c8aa-4b0b-832c-ec2927bf1163
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# 如何：检索元数据并实现兼容服务。
通常，设计和实现服务并不是由同一个人完成的。 在交互操作应用程序很重要的环境中，可以用 Web 服务描述语言 (WSDL) 设计或描述协定，而且开发人员必须实现一个与所提供的协定相兼容的服务。 您可能还需要将现有服务迁移到 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]，但保留连网格式。 此外，双工协定还需要调用方实现一个回调协定。  
  
 在这些情况下，你必须使用[ServiceModel 元数据实用工具 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) （或等效工具） 可实现来满足该协定所要求的托管语言生成服务协定接口。 通常[ServiceModel 元数据实用工具 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)用于获取与通道工厂一起使用的服务协定或[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]客户端类型以及与设置正确的绑定和地址的客户端配置文件。 若要使用生成的配置文件，则必须将其更改到服务配置文件中。 您可能还需要修改服务协定。  
  
### <a name="to-retrieve-data-and-implement-a-compliant-service"></a>检索数据并实现兼容服务  
  
1.  使用[ServiceModel 元数据实用工具 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)针对元数据文件或元数据终结点生成的代码文件。  
  
2.  搜索输出代码文件包含感兴趣的 （以防存在多个） 界面中使用标记的部分<xref:System.ServiceModel.ServiceContractAttribute?displayProperty=fullName>属性。 下面的代码示例显示了生成这两个界面[ServiceModel 元数据实用工具 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)。 第一个 (`ISampleService`) 是服务协定接口，实现它可创建兼容服务。 第二个 (`ISampleServiceChannel`) 是用于扩展服务协定接口的客户端使用的帮助器接口和<xref:System.ServiceModel.IClientChannel?displayProperty=fullName>并可用于在客户端应用程序中。  
  
     [!code-csharp[ClientProxyCodeSample#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/clientproxycodesample/cs/proxycode.cs#2)]  
  
3.  如果 WSDL 未指定的所有操作的答复操作，生成的操作协定可能具有<xref:System.ServiceModel.OperationContractAttribute.ReplyAction%2A>属性设置为通配符 （*）。 移除该属性设置。 否则，当您实现服务协定元数据时，将不能为这些操作导出元数据。  
  
4.  实现类上的接口并承载服务。 有关示例，请参阅[如何︰ 实现服务协定](../../../../docs/framework/wcf/how-to-implement-a-wcf-contract.md)，或请参阅下面示例部分中的简单实现。  
  
5.  在客户端的配置文件[ServiceModel 元数据实用工具 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)生成时，更改[ <> \> ](../../../../docs/framework/configure-apps/file-schema/wcf/client.md)的配置节[ <> \> ](../../../../docs/framework/configure-apps/file-schema/wcf/services.md)配置节。 （有关生成的客户端应用程序配置文件的示例，请参见下面的“示例”部分。）  
  
6.  在[ <> \> ](../../../../docs/framework/configure-apps/file-schema/wcf/services.md)配置部分中，创建`name`属性中[ <> \> ](../../../../docs/framework/configure-apps/file-schema/wcf/services.md)配置节，用于您的服务实现。  
  
7.  将服务的 `name` 属性设置为服务实现的配置名称。  
  
8.  将使用实现的服务协定的终结点配置元素添加到服务配置部分。  
  
## <a name="example"></a>示例  
 下面的代码示例显示了通过运行生成的代码文件的大部分[ServiceModel 元数据实用工具 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)对元数据文件。  
  
 下面的代码演示：  
  
-   实现时符合协定要求的服务协定接口 (`ISampleService`)。  
  
-   扩展服务协定接口的客户端使用的帮助器接口和<xref:System.ServiceModel.IClientChannel?displayProperty=fullName>并可用于在客户端应用程序中 (`ISampleServiceChannel`)。  
  
-   扩展的帮助器类<xref:System.ServiceModel.ClientBase%601?displayProperty=fullName>并可用于在客户端应用程序中 (`SampleServiceClient`)。  
  
-   从服务生成的配置文件。  
  
-   简单的 `ISampleService` 服务实现。  
  
-   客户端配置文件到服务器端版本的转换。  
  
 [!code-csharp[ClientProxyCodeSample#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/clientproxycodesample/cs/proxycode.cs#1)]  
  
 <!-- TODO: review snippet reference [!code[ClientProxyCodeSample#10](../../../../samples/snippets/common/VS_Snippets_CFX/clientproxycodesample/common/client.exe.config#10)]  -->
 <!-- TODO: review snippet reference [!code-csharp[ClientProxyCodeSample#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/clientproxycodesample/cs/client.exe.config#10)]  -->  
  
 [!code-csharp[ClientProxyCodeSample#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/clientproxycodesample/cs/hostapplication.cs#5)]  
  
 <!-- TODO: review snippet reference [!code[ClientProxyCodeSample#20](../../../../samples/snippets/common/VS_Snippets_CFX/clientproxycodesample/common/hostapplication.exe.config#20)]  -->
 <!-- TODO: review snippet reference [!code-csharp[ClientProxyCodeSample#20](../../../../samples/snippets/csharp/VS_Snippets_CFX/clientproxycodesample/cs/hostapplication.exe.config#20)]  -->  
  
## <a name="see-also"></a>另请参阅  
 [ServiceModel 元数据实用工具 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)