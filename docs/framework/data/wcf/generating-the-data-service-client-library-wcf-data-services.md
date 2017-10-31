---
title: "生成数据服务客户端库（WCF 数据服务） | Microsoft Docs"
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
  - "“添加服务引用”对话框"
  - "客户端应用程序, WCF 数据服务"
  - "WCF 数据服务, 客户端库"
ms.assetid: 314077c1-ac10-47e1-bed4-940b5462359d
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 生成数据服务客户端库（WCF 数据服务）
实现[!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 的数据服务可返回描述 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源公开的数据模型的服务元数据文档。  有关更多信息，请参见 [OData：服务元数据文档](http://go.microsoft.com/fwlink/?LinkId=186070)（可能为英文网页）。可以使用 Visual Studio 中的“添加服务引用”对话框来添加对基于 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 的服务的引用。  使用此工具在客户端项目中添加对 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源返回的元数据的引用时，将执行以下操作：  
  
-   从数据服务请求服务元数据文档并截获返回的元数据。  
  
    > [!NOTE]
    >  返回的元数据作为 .edmx 文件存储在客户端项目中。  此 .edmx 文件无法通过实体数据模型设计器打开，因为此文件的格式与实体框架所使用的 .edmx 文件的格式不相同。  可以通过使用 XML 编辑器或任何文本编辑器查看此元数据文件。  有关更多信息，请参见 [\[MC\-EDMX\]：用于数据服务打包格式的实体数据模型](http://go.microsoft.com/fwlink/?LinkID=178833)（可能为英文网页）规范  
  
-   作为从 <xref:System.Data.Services.Client.DataServiceContext> 继承的实体容器类生成数据服务的表示形式。  此生成的实体容器类与实体数据模型工具生成的实体容器类似。  有关详细信息，请参阅[Object Services Overview \(Entity Framework\)](http://msdn.microsoft.com/zh-cn/43014cf9-c9cb-4538-bfbb-197820b60038)。  
  
-   为在服务元数据中发现的数据模型类型生成数据类。  
  
-   在项目中添加对 `System.Data.Services.Client` 程序集的引用。  
  
 有关详细信息，请参阅[如何：添加数据服务引用](../../../../docs/framework/data/wcf/how-to-add-a-data-service-reference-wcf-data-services.md)。  
  
 还可以在命令提示符处使用 [DataSvcUtil.exe](../../../../docs/framework/data/wcf/wcf-data-service-client-utility-datasvcutil-exe.md) 工具来生成客户端数据服务类。  有关详细信息，请参阅[如何：手动生成客户端数据服务类](../../../../docs/framework/data/wcf/how-to-manually-generate-client-data-service-classes-wcf-data-services.md)。  
  
## 客户端数据类型映射  
 当使用 Visual Studio 中的**“添加服务引用”**对话框或 `DataSvcUtil.exe` 工具生成基于 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源客户端数据类时，.NET Framework 数据类型会映射到数据模型中的基元类型，如下所示：  
  
|数据模型类型|.NET Framework 数据类型|  
|------------|-------------------------|  
|`Edm.Binary`|<xref:System.Byte> `[]`|  
|`Edm.Boolean`|<xref:System.Boolean>|  
|`Edm.Byte`|<xref:System.Byte>|  
|`Edm.DateTime`|<xref:System.DateTime>|  
|`Edm.Decimal`|<xref:System.Decimal>|  
|`Edm.Double`|<xref:System.Double>|  
|`Edm.Guid`|<xref:System.Guid>|  
|`Edm.Int16`|<xref:System.Int16>|  
|`Edm.Int32`|<xref:System.Int32>|  
|`Edm.Int64`|<xref:System.Int64>|  
|`Edm.SByte`|<xref:System.SByte>|  
|`Edm.Single`|<xref:System.Single>|  
|`Edm.String`|<xref:System.String>|  
  
 有关更多信息，请参见 [OData：基元数据类型](http://go.microsoft.com/fwlink/?LinkId=186072)（可能为英文网页）。  
  
## 请参阅  
 [WCF 数据服务客户端库](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)   
 [快速入门](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)