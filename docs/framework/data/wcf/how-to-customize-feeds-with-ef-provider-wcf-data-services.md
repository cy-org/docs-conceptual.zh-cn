---
title: "如何：使用实体框架提供程序自定义源（WCF 数据服务） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF 数据服务, 自定义"
  - "WCF 数据服务, 自定义源"
ms.assetid: fd16272e-36f2-415e-850e-8a81f2b17525
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 如何：使用实体框架提供程序自定义源（WCF 数据服务）
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 使您可以在数据服务响应中自定义 Atom 序列化，以便可以将实体属性映射到在 AtomPub 协议中定义的未使用的元素。  本主题演示如何使用实体框架提供程序为 .edmx 文件中定义的数据模型中的实体类型定义映射特性。  有关详细信息，请参阅[源自定义](../../../../docs/framework/data/wcf/feed-customization-wcf-data-services.md)。  
  
 在本主题中，您将手动修改由工具生成且包含数据模型的 .edmx 文件。  由于实体设计器不支持数据模型扩展，因此必须手动修改此文件。  有关实体数据模型工具生成的 .edmx 文件的更多信息，请参见 [.edmx File Overview](http://msdn.microsoft.com/zh-cn/f4c8e7ce-1db6-417e-9759-15f8b55155d4)。  本主题中的示例使用罗斯文示例数据服务和自动生成的客户端数据服务类。  此服务和这些客户端数据类是在完成 [WCF 数据服务快速入门](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)时创建的。  
  
### 手动修改 Northwind.edmx 文件以添加源自定义特性  
  
1.  在**“解决方案资源管理器”**中右击 `Northwind.edmx` 文件，然后单击**“打开方式”**。  
  
2.  在**“打开方式 \- Northwind.edmx”**对话框中选择**“XML 编辑器”**，然后单击**“确定”**。  
  
3.  找到 `ConceptualModels` 元素，并用以下包含源自定义映射特性的元素替换现有的 `Customers` 实体类型：  
  
     [!code-xml[Astoria Custom Feeds#EdmFeedCustomers](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria custom feeds/xml/northwind.csdl#edmfeedcustomers)]  
  
4.  保存更改并关闭 Northwind.edmx 文件。  
  
5.  （可选）右击 Northwind.edmx 文件，并单击**“运行自定义工具”**。  
  
     此时将重新生成可能需要的对象层文件。  
  
6.  重新编译该项目。  
  
## 示例  
 以上示例为 URI `http://myservice/` `Northwind.svc/Customers('ALFKI')` 返回以下结果。  
  
 [!code-xml[Astoria Custom Feeds#EdmFeedResult](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria custom feeds/xml/edmfeedresult.xml#edmfeedresult)]  
  
## 请参阅  
 [实体框架提供程序](../../../../docs/framework/data/wcf/entity-framework-provider-wcf-data-services.md)