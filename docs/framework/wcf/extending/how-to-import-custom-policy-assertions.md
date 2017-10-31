---
title: "如何：导入自定义策略断言 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1f41d787-accb-4a10-bfc6-a807671d1581
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 如何：导入自定义策略断言
策略断言说明服务终结点的功能和需求。  客户端应用程序可以在服务元数据中使用策略断言来配置客户端绑定或自定义服务终结点的服务协定。  
  
 通过实现自定义策略断言导入<xref:System.ServiceModel.Description.IPolicyImportExtension?displayProperty=fullName>接口并将该对象传递给元数据系统或通过注册实现类型应用程序配置文件中。  实现<xref:System.ServiceModel.Description.IPolicyImportExtension>接口必须提供默认构造函数。  
  
### <a name="to-import-custom-policy-assertions"></a>导入自定义策略断言  
  
1.  实现<xref:System.ServiceModel.Description.IPolicyImportExtension?displayProperty=fullName>类上的接口。 请参见下面的过程。  
  
2.  通过以下方式之一插入自定义策略导入程序：  
  
3.  使用配置文件。 请参见下面的过程。  
  
4.  使用配置文件与[ServiceModel 元数据实用工具 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)。 请参见下面的过程。  
  
5.  以编程方式插入策略导入程序。 请参见下面的过程。  
  
### <a name="to-implement-the-systemservicemodeldescriptionipolicyimportextension-interface-on-any-class"></a>在任何类上实现 System.ServiceModel.Description.IPolicyImportExtension 接口  
  
1.  在<xref:System.ServiceModel.Description.IPolicyImportExtension.ImportPolicy%2A?displayProperty=fullName>方法中，对于您感兴趣，每个策略主题想要通过调用适当的方法 （取决于所需的断言范围） 导入的策略断言在找到<xref:System.ServiceModel.Description.PolicyConversionContext?displayProperty=fullName>对象传递给方法。 下面的代码示例演示如何使用<xref:System.ServiceModel.Description.PolicyAssertionCollection.Remove%2A?displayProperty=fullName>方法定位自定义策略断言并将其从一个步骤中的集合删除。 如果使用删除方法定位并删除断言，则不必执行步骤 4。  
  
     [!code-csharp[CustomPolicySample#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/custompolicysample/cs/policyimporter.cs#9)]
     [!code-vb[CustomPolicySample#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/custompolicysample/vb/policyimporter.vb#9)]  
  
2.  处理策略断言。 请注意，策略系统不会标准化嵌入的策略和 `wsp:optional`。 您必须在策略导入扩展实现中处理这些结构。  
  
3.  对支持策略断言指定的功能或要求的绑定或协定执行自定义。 断言通常指示绑定需要特定配置或特定绑定元素。 通过访问来进行这些修改<xref:System.ServiceModel.Description.PolicyConversionContext.BindingElements%2A?displayProperty=fullName>属性。 其他断言需要您修改协定。  您可以访问和修改协定使用<xref:System.ServiceModel.Description.PolicyConversionContext.Contract%2A?displayProperty=fullName>属性。  请注意，对于同一个绑定和协定，可能会多次调用策略导入程序，但导入的是不同的替代策略（如果一个替代策略导入失败）。 您的代码应该能够处理这一行为。  
  
4.  从断言集合中删除自定义策略断言。 如果不删除该断言，[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 将假定策略导入失败，并将不导入相关绑定。 如果您使用<xref:System.ServiceModel.Description.PolicyAssertionCollection.Remove%2A?displayProperty=fullName>方法定位自定义策略断言并将其删除集合中不需要执行此步骤中的一个步骤。  
  
### <a name="to-insert-the-custom-policy-importer-into-the-metadata-system-using-a-configuration-file"></a>使用配置文件将自定义策略导入程序插入到元数据系统  
  
1.  导入程序将类型添加到`<extensions>`元素内的[ <> \> ](../../../../docs/framework/configure-apps/file-schema/wcf/policyimporters.md)客户端配置文件中的元素。  
  
     <!-- TODO: review snippet reference [!code[CustomPolicySample#7](../../../../samples/snippets/common/VS_Snippets_CFX/custompolicysample/common/client.exe.config#7)]  -->
     <!-- TODO: review snippet reference [!code-csharp[CustomPolicySample#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/custompolicysample/cs/client.exe.config#7)]  -->
     <!-- TODO: review snippet reference [!code-vb[CustomPolicySample#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/custompolicysample/vb/client.exe.config#7)]  -->  
  
2.  在客户端应用程序，使用<xref:System.ServiceModel.Description.MetadataResolver?displayProperty=fullName>或<xref:System.ServiceModel.Description.WsdlImporter?displayProperty=fullName>解析会自动调用的元数据和导入程序。  
  
     [!code-csharp[CustomPolicySample#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/custompolicysample/cs/client.cs#10)]
     [!code-vb[CustomPolicySample#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/custompolicysample/vb/client.vb#10)]  
  
### <a name="to-insert-the-custom-policy-importer-into-the-metadata-system-using-svcutilexe"></a>使用 Svcutil.exe 将自定义策略导入程序插入到元数据系统  
  
1.  导入程序将类型添加到`<extensions>`元素内的[ <> \> ](../../../../docs/framework/configure-apps/file-schema/wcf/policyimporters.md) Svcutil.exe.config 配置文件中的元素。 也可以通过使用 `/svcutilConfig` 选项指示 Svcutil.exe 加载在其他配置文件中注册的策略导入程序类型。  
  
2.  使用[ServiceModel 元数据实用工具 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)要导入的元数据和导入程序会自动调用。  
  
### <a name="to-insert-the-custom-policy-importer-into-the-metadata-system-programmatically"></a>以编程方式将自定义策略导入程序插入到元数据系统  
  
1.  添加到导入程序<xref:System.ServiceModel.Description.MetadataImporter.PolicyImportExtensions%2A?displayProperty=fullName>属性 (例如，如果您使用<xref:System.ServiceModel.Description.WsdlImporter?displayProperty=fullName>) 之前导入元数据。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.ServiceModel.Description.MetadataResolver?displayProperty=fullName>   
 <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=fullName>   
 <xref:System.ServiceModel.Description.MetadataResolver?displayProperty=fullName>   
 [扩展元数据系统](../../../../docs/framework/wcf/extending/extending-the-metadata-system.md)