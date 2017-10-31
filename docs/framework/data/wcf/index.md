---
title: "WCF 数据服务 4.5"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework-oob
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- HTML
- VB
- CSharp
- C++
helpviewer_keywords:
- Astoria
- WCF Data Services, getting started
ms.assetid: 73d2bec3-7c92-4110-b905-11bb0462357a
caps.latest.revision: 6
author: Erikre
ms.author: erikre
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 1b491d644112137cb24e847439aa133691e5261d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/05/2017

---
# <a name="wcf-data-services-45"></a>WCF 数据服务 4.5
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]（以前称为“ADO.NET Data Services”）是 .NET Framework 的一个组件。可以使用此组件创建一些服务，利用 [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 借助 [representational state transfer (REST)](http://go.microsoft.com/fwlink/?LinkId=113919)（表述性状态转移 (REST)）语义通过 Web 或 Intranet 公开和使用数据。 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 将数据公开为可通过 URI 进行寻址的资源。 通过使用标准 HTTP 谓词 GET、PUT、POST 和 DELETE 访问和更改数据。 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 使用[实体数据模型](../../../../docs/framework/data/adonet/entity-data-model.md)的实体关系约定将资源公开为通过关联相关的实体集。  
  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]使用 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 协议对资源进行寻址和更新。 通过这种方式，您可以从支持 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 的任何客户端访问这些服务。 通过 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 可以使用以下非常常见的传输格式请求数据以及将数据写入资源，即：Atom 与 JavaScript 对象表示法 (JSON)；前者是将数据作为 XML 进行交换和更新的一组标准，后者是在 AJAX 应用程序中广泛使用的基于文本的数据交换格式。  
  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]可以将源自各种源的数据作为 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源公开。 借助于 Visual Studio 工具，可以更轻松地使用 ADO.NET 实体框架数据模型来创建基于 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 的服务。 也可以基于公共语言运行时 (CLR) 类，甚至基于后期绑定的或未类型化的数据，创建 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源。  
  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 还包括一组客户端库，一个库用于常规 .NET Framework 客户端应用程序，另一个库专用于基于 Silverlight 的应用程序。 在从 .NET Framework 和 Silverlight 之类的环境访问 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源时，这些客户端库提供了基于对象的编程模型。  
  
## <a name="where-should-i-start"></a>从何处开始？  
 根据您的兴趣，可考虑从下列主题之一开始使用 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]。  
  
 我希望直接开始使用…  
 -   [快速入门](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)  
  
-   [入门](../../../../docs/framework/data/wcf/getting-started-with-wcf-data-services.md)  
  
-   [Silverlight 快速入门](http://go.microsoft.com/fwlink/?LinkID=192782)  
  
-   [Windows Phone 开发 Silverlight 快速入门](http://go.microsoft.com/fwlink/?LinkID=214535)  
  
 我只想查看一些代码……  
 -   [快速入门](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)  
  
-   [如何：执行数据服务查询](../../../../docs/framework/data/wcf/how-to-execute-data-service-queries-wcf-data-services.md)  
  
-   [如何：将数据绑定到 Windows Presentation Foundation 元素](../../../../docs/framework/data/wcf/bind-data-to-wpf-elements-wcf-data-services.md)  
  
 我希望更多地了解 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]…  
 -   [白皮书：OData 简介](http://go.microsoft.com/fwlink/?LinkId=220867)  
  
-   [Open Data Protocol 网站](http://go.microsoft.com/fwlink/?LinkID=184554)  
  
-   [OData：SDK](http://go.microsoft.com/fwlink/?LinkID=185248)  
  
-   [OData：常见问题](http://go.microsoft.com/fwlink/?LinkId=185867)  
  
 我想要观看一些视频…  
 -   [WCF Data Services 初学者指南](http://go.microsoft.com/fwlink/?LinkId=220864)  
  
-   [WCF Data Services 开发人员视频](http://go.microsoft.com/fwlink/?LinkId=220861)  
  
-   [OData：开发人员网站](http://go.microsoft.com/fwlink/?LinkId=185866)  
  
 我想要查看端到端示例  
 -   [MSDN 示例库上的 WCF Data Services 文档示例](http://go.microsoft.com/fwlink/?LinkID=220865)  
  
-   [MSDN 示例库上的其他 WCF Data Services 示例](http://go.microsoft.com/fwlink/?LinkId=220866)  
  
-   [OData：SDK](http://go.microsoft.com/fwlink/?LinkID=185248)  
  
 它如何与 Visual Studio 集成？  
 -   [生成数据服务客户端库](../../../../docs/framework/data/wcf/generating-the-data-service-client-library-wcf-data-services.md)  
  
-   [创建数据服务](../../../../docs/framework/data/wcf/creating-the-data-service.md)  
  
-   [实体框架提供程序](../../../../docs/framework/data/wcf/entity-framework-provider-wcf-data-services.md)  
  
 我可以对它执行何种操作？  
 -   [概述](../../../../docs/framework/data/wcf/wcf-data-services-overview.md)  
  
-   [白皮书：OData 简介](http://go.microsoft.com/fwlink/?LinkId=220867)  
  
-   [应用程序方案](../../../../docs/framework/data/wcf/application-scenarios-wcf-data-services.md)  
  
 我想要使用 Silverlight……  
 -   [Silverlight 快速入门](http://go.microsoft.com/fwlink/?LinkID=192782)  
  
-   [WCF Data Services (Silverlight)](http://go.microsoft.com/fwlink/?LinkID=143149)  
  
-   [Silverlight 入门](http://go.microsoft.com/fwlink/?LinkId=148366)  
  
 我要创建 Windows Phone 应用程序…  
 -   [Windows Phone 开发 Silverlight 快速入门](http://go.microsoft.com/fwlink/?LinkID=214535)  
  
-   [Windows Phone 的 Open Data Protocol (OData) 客户端](http://go.microsoft.com/fwlink/?LinkID=208749)  
  
 我想要使用 LINQ……  
 -   [查询数据服务](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md)  
  
-   [LINQ 注意事项](../../../../docs/framework/data/wcf/linq-considerations-wcf-data-services.md)  
  
-   [如何：执行数据服务查询](../../../../docs/framework/data/wcf/how-to-execute-data-service-queries-wcf-data-services.md)  
  
 我还需要了解更多信息…  
 -   [WCF Data Services Team Blog](http://go.microsoft.com/fwlink/?LinkID=150511)（WCF Data Services 团队博客）  
  
-   [资源](../../../../docs/framework/data/wcf/wcf-data-services-resources.md)  
  
-   [WCF Data Services 开发人员中心](http://go.microsoft.com/fwlink/?LinkId=220868)  
  
-   [Open Data Protocol 网站](http://go.microsoft.com/fwlink/?LinkID=184554)  
  
## <a name="in-this-section"></a>本节内容  
 [概述](../../../../docs/framework/data/wcf/wcf-data-services-overview.md)  
 概述 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 中提供的功能。  
  
 [WCF Data Services 新增功能](http://msdn.microsoft.com/en-us/cf22cad5-b8d9-472b-8d7c-b863b64eaae8)  
 说明 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 中的新功能以及对新 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 功能的支持。  
  
 [入门](../../../../docs/framework/data/wcf/getting-started-with-wcf-data-services.md)  
 说明如何使用 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 公开和使用 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源。  
  
 [定义 WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)  
 说明如何创建和配置公开 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源的数据服务。  
  
 [WCF Data Services 客户端库](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)  
 说明如何使用客户端库从 .NET Framework 客户端应用程序使用 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源。  
  
## <a name="see-also"></a>另请参阅  
 [Representational State Transfer (REST)](http://go.microsoft.com/fwlink/?LinkId=113919)（表述性状态转移 (REST)）

