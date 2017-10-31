---
title: "流提供程序（WCF 数据服务） | Microsoft Docs"
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
  - "流数据提供程序 [WCF 数据服务]"
  - "WCF 数据服务, 二进制数据"
  - "WCF 数据服务, 提供程序"
  - "WCF 数据服务, 流"
ms.assetid: f0978fe4-5f9f-42aa-a5c2-df395d7c9495
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 流提供程序（WCF 数据服务）
数据服务可公开二进制大型对象数据。  此二进制数据可以表示视频和音频流、图像、文档文件或其他类型的二进制媒体。  当数据模型中的某个实体包括一个或多个二进制属性时，数据服务会在响应源的入口内以 base\-64 编码形式返回此二进制数据。  由于以这种方式加载和序列化大型二进制数据会影响到性能，因此[!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 定义了一种机制，该机制独立于二进制数据所属的实体来检索二进制数据。  这一点是通过将实体和二进制数据分隔到一个或多个数据流来实现的。  
  
-   媒体资源 \- 属于某个实体的二进制数据，例如视频、音频、图像或其他类型的媒体资源流。  
  
-   媒体链接入口 \- 引用相关媒体资源流的实体。  
  
 利用 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]，可通过实现流数据提供程序定义二进制资源流。  流提供程序实现以 <xref:System.IO.Stream> 对象的形式向数据服务提供与特定实体关联的媒体资源流。  有了此实现，数据服务能够以指定 MIME 类型的二进制数据流的形式通过 HTTP 接受和返回媒体资源。  
  
 将数据服务配置为支持二进制数据流需要以下步骤：  
  
1.  将数据模型中的一个或多个实体特性化为媒体链接入口。  这些实体不应包括要进行流处理的二进制数据。  始终在实体中以 base\-64 编码的二进制形式返回实体的所有二进制属性。  
  
2.  实现 T:System.Data.Services.Providers.IDataServiceStreamProvider 接口。  
  
3.  定义一个实现 <xref:System.IServiceProvider> 接口的数据服务。  数据服务使用 <xref:System.IServiceProvider.GetService%2A> 实现访问流数据提供程序实现。  此方法返回适当的流提供程序实现。  
  
4.  在 Web 应用程序配置中启用大型消息流。  
  
5.  启用对服务器上或数据源中的二进制资源的访问。  
  
 本主题中的示例基于示例流照片服务，该服务会在[数据服务流提供程序系列：实现流提供程序（第一部分）](http://go.microsoft.com/fwlink/?LinkID=198989)（可能为英文网页）一文中进行深入讨论。  MSDN 代码库的[流照片数据服务示例](http://go.microsoft.com/fwlink/?LinkID=198988)（可能为英文网页）页上提供了此示例服务的源代码。  
  
## 在数据模型中定义媒体链接入口  
 数据源提供程序确定在数据模型中将某个实体定义为媒体链接入口的方式。  
  
 **实体框架提供程序**  
 若要指示某个实体为媒体链接入口，需将 `HasStream` 特性添加到概念模型中的相应实体类型定义，如以下示例所示：  
  
 [!code-xml[Astoria Photo Streaming Service#HasStream](../../../../samples/snippets/xml/VS_Snippets_Misc/astoria photo streaming service/xml/photodata.edmx#hasstream)]  
  
 还必须将命名空间 `xmlns:m=http://schemas.microsoft.com/ado/2007/08/dataservices/metadata` 添加到实体，或添加到定义数据模型的 .edmx 或 .csdl 文件的根目录中。  
  
 [!INCLUDE[crexample](../../../../includes/crexample-md.md)]使用 [!INCLUDE[adonet_ef](../../../../includes/adonet-ef-md.md)] 提供程序并公开媒体资源的数据服务，请参见[数据服务流提供程序系列：实现流提供程序（第一部分）](http://go.microsoft.com/fwlink/?LinkID=198989)（可能为英文网页）一文。  
  
 **反射提供程序**  
 若要指示某个实体为媒体链接入口，需将 <xref:System.Data.Services.Common.HasStreamAttribute> 添加到在反射提供程序中定义相应实体类型的类中。  
  
 **自定义数据服务提供程序**  
 使用自定义服务提供程序时，可实现 <xref:System.Data.Services.Providers.IDataServiceMetadataProvider> 接口来定义数据服务的元数据。  有关详细信息，请参阅[自定义数据服务提供程序](../../../../docs/framework/data/wcf/custom-data-service-providers-wcf-data-services.md)。  通过将表示实体类型（媒体链接入口）的 <xref:System.Data.Services.Providers.ResourceType> 的 <xref:System.Data.Services.Providers.ResourceType.IsMediaLinkEntry%2A> 属性设置为 `true`，可以指示一个二进制资源流属于 <xref:System.Data.Services.Providers.ResourceType>。  
  
## 实现 IDataServiceStreamProvider 接口  
 若要创建支持二进制数据流的数据服务，必须实现 <xref:System.Data.Services.Providers.IDataServiceStreamProvider> 接口。  有了此实现，数据服务能够以流的形式将二进制数据返回给客户端，并使用从客户端发送的流形式的二进制数据。  每当数据服务需要访问流形式的二进制数据时，都会创建一个此接口实例。  <xref:System.Data.Services.Providers.IDataServiceStreamProvider> 接口指定以下成员：  
  
|成员名称|描述|  
|----------|--------|  
|<xref:System.Data.Services.Providers.IDataServiceStreamProvider.DeleteStream%2A>|当删除媒体资源的媒体链接入口时，数据服务将调用此方法来删除相应媒体资源。  当实现 <xref:System.Data.Services.Providers.IDataServiceStreamProvider> 时，此方法将包含会删除与所提供媒体链接入口关联的媒体资源的代码。|  
|<xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetReadStream%2A>|数据服务调用此方法来以流的形式返回媒体资源。  当实现 <xref:System.Data.Services.Providers.IDataServiceStreamProvider> 时，此方法将包含提供流的代码，数据服务使用提供的流返回与所提供媒体链接入口关联的媒体资源。|  
|<xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetReadStreamUri%2A>|数据服务调用此方法，来返回用于请求媒体链接入口的媒体资源的 URI。  使用此值可以在媒体链接入口的内容元素中创建 `src` 特性，也可以请求数据流。  当此方法返回 `null` 时，数据服务自动确定 URI。  需要向客户端提供不使用流提供程序直接访问二进制数据的权限时，使用此方法。|  
|<xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetStreamContentType%2A>|数据服务调用此方法，来返回与指定媒体链接入口关联的媒体资源的 Content\-Type 值。|  
|<xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetStreamETag%2A>|数据服务调用此方法，来返回与指定实体关联的数据流的 eTag。  管理二进制数据的并发性时使用此方法。  如果此方法返回 null，则数据服务不会跟踪并发。|  
|<xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetWriteStream%2A>|数据服务调用此方法，来获取在接收从客户端发送的流时所使用的流。  当实现 <xref:System.Data.Services.Providers.IDataServiceStreamProvider> 时，您必须返回一个可写入流，以便数据服务将接收到的流数据写入到其中。|  
|<xref:System.Data.Services.Providers.IDataServiceStreamProvider.ResolveType%2A>|返回一个命名空间限定的类型名称，该名称表示数据服务运行时必须为媒体链接入口创建的类型，该媒体链接入口与正在插入的媒体资源的数据流相关联。|  
  
## 创建流数据服务  
 若要向 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 运行时提供访问 <xref:System.Data.Services.Providers.IDataServiceStreamProvider> 实现的权限，所创建的数据服务还必须实现 <xref:System.IServiceProvider> 接口。  下面的示例演示如何实现 <xref:System.IServiceProvider.GetService%2A> 方法，以返回实现 <xref:System.Data.Services.Providers.IDataServiceStreamProvider> 的 `PhotoServiceStreamProvider` 类的实例。  
  
 [!code-csharp[Astoria Photo Streaming Service#PhotoServiceStreamingProvider](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria photo streaming service/cs/photodata.svc.cs#photoservicestreamingprovider)]
 [!code-vb[Astoria Photo Streaming Service#PhotoServiceStreamingProvider](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria photo streaming service/vb/photodata.svc.vb#photoservicestreamingprovider)]  
  
 有关如何创建数据服务的一般信息，请参见[配置数据服务](../../../../docs/framework/data/wcf/configuring-the-data-service-wcf-data-services.md)。  
  
## 在宿主环境中启用大型二进制数据流  
 在 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] Web 应用程序中创建数据服务时，使用 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 可提供 HTTP 协议实现。默认情况下，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将 HTTP 消息的大小限制为仅 65K 字节。  为了使大型二进制数据能够流入或流出数据服务，还必须将 Web 应用程序配置为启用大型二进制文件并使用流进行转换。  为此，请将以下内容添加到应用程序的 Web.config 文件的 `<configuration />` 元素中：  
  
  
  
> [!NOTE]
>  您必须使用 <xref:System.ServiceModel.TransferMode?displayProperty=fullName> 传输模式，以确保由 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 对请求和响应消息中的二进制数据进行流式处理且不进行缓冲。  
  
 有关详细信息，请参阅[流消息传输](../../../../docs/framework/wcf/feature-details/streaming-message-transfer.md)和[传输配额](../../../../docs/framework/wcf/feature-details/transport-quotas.md)。  
  
 默认情况下，Internet 信息服务 \(IIS\) 还将请求的大小限制为 4MB。  在 IIS 上运行时，若要允许您的数据服务接收超过 4MB 的流，则还必须在 `<system.web />` 配置部分设置 [httpRuntime 元素（ASP.NET 设置架构）](http://msdn.microsoft.com/zh-cn/e9b81350-8aaf-47cc-9843-5f7d0c59f369) 的 `maxRequestLength` 属性，如以下示例所示：  
  
  
  
## 在客户端应用程序中使用数据流  
 通过 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 客户端库，您可以在客户端上以二进制数据流的形式检索和更新这些公开的资源。  有关详细信息，请参阅[使用二进制数据](../../../../docs/framework/data/wcf/working-with-binary-data-wcf-data-services.md)。  
  
## 使用流提供程序时的注意事项  
 以下是在实现流提供程序时以及从数据服务访问媒体资源时要考虑的一些事项。  
  
-   对于媒体资源不支持 MERGE 请求。  使用 PUT 请求可更改现有实体的媒体资源。  
  
-   POST 请求不能用于创建新的媒体链接入口。  相反，您必须发出一个 POST 请求来创建新的媒体资源，而数据服务器则会使用默认值创建新的媒体链接入口。  这个新实体可由后续的 MERGE 或 PUT 请求进行更新。  您可能还应考虑缓存该实体并在处置器中进行更新，例如将属性值设置为 POST 请求中的 Slug 标头的值。  
  
-   收到 POST 请求时，数据服务将先调用 <xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetWriteStream%2A> 来创建媒体资源，然后再调用 <xref:System.Data.Services.IUpdatable.SaveChanges%2A> 来创建媒体链接入口。  
  
-   <xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetWriteStream%2A> 的实现不应返回 <xref:System.IO.MemoryStream> 对象。  如果使用这种类型的流，则在服务接收到非常大的数据流时将会释放内存资源。  
  
-   以下是在数据库中存储媒体资源时应考虑的事项：  
  
    -   数据模型中不应包括作为媒体资源的二进制属性。  数据模型中公开的所有属性都会在响应源的入口中返回。  
  
    -   为了提高使用大型二进制数据流时的性能，建议您创建一个自定义流类来存储数据库中的二进制数据。  此类由 <xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetWriteStream%2A> 实现返回并将二进制数据分块区发送到数据库。  对于 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] 数据库，当二进制数据大于 1MB 时，建议您使用 FILESTREAM 以流形式将数据传入数据库中。  
  
    -   确保您的数据库设计为存储将由数据服务接收的大型二进制数据流。  
  
    -   当客户端发送 POST 请求以便将媒体链接入口与媒体资源一起插入到单个请求时，将先调用 <xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetWriteStream%2A> 以获取流，然后数据服务才将新实体插入到数据库。  流提供程序实现必须能够处理此数据服务行为。  请考虑使用单独的数据表来存储二进制数据或者在文件中存储数据流，直至已在数据库中插入实体。  
  
-   当实现 <xref:System.Data.Services.Providers.IDataServiceStreamProvider.DeleteStream%2A>、<xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetReadStream%2A> 或 <xref:System.Data.Services.Providers.IDataServiceStreamProvider.GetWriteStream%2A> 方法时，您必须使用以方法参数的形式提供的 eTag 和 Content\-Type 值。  不要在 <xref:System.Data.Services.Providers.IDataServiceStreamProvider> 提供程序实现中设置 eTag 或 Content\-Type 标头。  
  
-   默认情况下，客户端通过使用分块的 HTTP 传输编码发送大型二进制数据流。  由于 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] Development Server 不支持此类编码方式，因此您无法使用此 Web 服务器来承载必须接受大型二进制数据流的流数据服务。有关 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] Development Server 的更多信息，请参见 [Visual Studio 中用于 ASP.NET Web 项目的 Web 服务器](http://msdn.microsoft.com/zh-cn/31d4f588-df59-4b7e-b9ea-e1f2dd204328)。  
  
<a name="versioning"></a>   
## 版本控制要求  
 流提供程序具有以下 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 协议版本控制要求：  
  
-   流提供程序要求数据服务支持 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 协议的 2.0 版本以及更高版本。  
  
 有关详细信息，请参阅[数据服务版本管理](../../../../docs/framework/data/wcf/data-service-versioning-wcf-data-services.md)。  
  
## 请参阅  
 [数据服务提供程序](../../../../docs/framework/data/wcf/data-services-providers-wcf-data-services.md)   
 [自定义数据服务提供程序](../../../../docs/framework/data/wcf/custom-data-service-providers-wcf-data-services.md)   
 [使用二进制数据](../../../../docs/framework/data/wcf/working-with-binary-data-wcf-data-services.md)