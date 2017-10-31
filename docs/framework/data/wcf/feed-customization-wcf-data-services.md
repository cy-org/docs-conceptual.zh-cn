---
title: "源自定义（WCF 数据服务） | Microsoft Docs"
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
  - "WCF 数据服务，订阅源"
  - "WCF 数据服务，Atom 协议"
  - "Atom 发布协议 [WCF 数据服务]"
  - "WCF 数据服务，自定义源"
ms.assetid: 0d1a39bc-6462-4683-bd7d-e74e0fd28a85
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# 源自定义（WCF 数据服务）
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]使用[!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)]将数据作为源公开。 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]支持用于数据馈送的 Atom 和 JavaScript 对象表示法 (JSON) 格式。 当使用 Atom 馈送时，[!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]提供了一种标准方法来序列化数据，如实体和关系，可以包含在 HTTP 消息的正文以 XML 格式。 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]定义实体中包含的数据与 Atom 元素之间的默认实体-属性映射。 有关详细信息，请参阅[OData: Atom 格式](http://go.microsoft.com/fwlink/?LinkID=185794)。  
  
 您的应用程序方案可能要求以自定义方式而非标准源格式序列化数据服务返回的属性数据。 与[!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]，可以自定义数据源中的序列化，以便可以将实体属性映射到未使用的元素和属性的一项或数据源中某项的自定义元素。  
  
> [!NOTE]
>  只有 Atom 馈送才支持源自定义。 当为返回的源请求 JSON 格式时，不会返回自定义源。  
  
 利用 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]，您可以通过向数据模型中的实体类型手动应用特性，为 Atom 负载定义替代实体-属性映射。 数据服务的数据源提供程序确定应当如何应用这些特性。  
  
> [!IMPORTANT]
>  定义自定义源时，必须保证已定义自定义映射的所有实体属性都包含在投影中。 如果投影中不包含某个已映射的实体属性，则可能会丢失数据。 有关详细信息，请参阅[查询投影](../../../../docs/framework/data/wcf/query-projections-wcf-data-services.md)。  
  
## <a name="customizing-feeds-with-the-entity-framework-provider"></a>使用实体框架提供程序自定义源  
 在 .edmx 文件中，用于[!INCLUDE[adonet_ef](../../../../includes/adonet-ef-md.md)]提供程序的数据模型以 XML 格式表示。 在这种情况下，用于定义自定义源的特性将会添加到表示数据模型中的实体类型和属性的 `EntityType` 和 `Property` 元素中。 这些源自的定义特性中未定义[ \[MC CSDL\]︰ 概念架构定义文件格式](http://go.microsoft.com/fwlink/?LinkId=159072)，这是格式，[!INCLUDE[adonet_ef](../../../../includes/adonet-ef-md.md)]提供程序用于定义数据模型。 因此，必须在某个特定的架构命名空间中声明源自定义特性，此架构命名空间应按 `m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata"` 格式定义。 以下 XML 片段显示应用于 `Property` 实体类型的 `Products` 元素的源自定义特性，这些特性定义 `ProductName`、`ReorderLevel` 和 `UnitsInStock` 属性。  
  
  [Astoria 自定义源 #EdmFeedAttributes](../CodeSnippet/VS_Snippets_Misc/astoria custom feeds#edmfeedattributes)]  
  
 这些特性为 `Products` 实体集生成以下自定义数据源。 在自定义数据源中，`ProductName` 属性值同时显示在 `author` 元素以及 `ProductName` 属性元素中，`UnitsInStock` 属性显示在具有其自己的唯一命名空间并且其 `ReorderLevel` 属性作为特性的自定义元素中：  
  
  [Astoria 自定义源 #EdmFeedResultProduct](../CodeSnippet/VS_Snippets_Misc/astoria custom feeds#edmfeedresultproduct)]  
  
 有关详细信息，请参阅[如何︰ 使用实体框架提供程序自定义源](../../../../docs/framework/data/wcf/how-to-customize-feeds-with-ef-provider-wcf-data-services.md)。  
  
> [!NOTE]
>  由于实体设计器不支持数据模型扩展，因此必须手动修改包含数据模型的 XML 文件。 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]由生成的.edmx 文件[!INCLUDE[adonet_edm](../../../../includes/adonet-edm-md.md)]工具，请参阅[.edmx 文件概述](http://msdn.microsoft.com/zh-cn/f4c8e7ce-1db6-417e-9759-15f8b55155d4)。  
  
### <a name="custom-feed-attributes"></a>自定义源特性  
 下表列出了一些 XML 特性，这些特性自定义可添加到用于定义数据模型的概念架构定义语言 (CSDL) 的源。 这些特性是对属性的等效<xref:System.Data.Services.Common.EntityPropertyMappingAttribute>用于反射提供程序。  
  
|特性名|描述|  
|--------------------|-----------------|  
|`FC_ContentKind`|指示内容类型。 以下关键字定义联合内容类型。<br /><br /> `text:`属性值在源中显示为文本。<br /><br /> `html:`属性值在源中显示为 HTML。<br /><br /> `xhtml:`属性值在源中显示为 XML 格式的 HTML。<br /><br /> 这些关键字的值相等， <xref:System.Data.Services.Common.SyndicationTextContentKind>枚举用于反射提供程序。<br /><br /> 如果使用了 `FC_NsPrefix` 和 `FC_NsUri` 特性，则不支持此特性。<br /><br /> 为 `xhtml` 特性指定值 `FC_ContentKind` 时，必须确保该属性值包含格式正确的 XML。 数据服务返回值，但不执行任何转换。 还必须确保返回的 XML 中任何 XML 元素前缀在映射的源中定义了命名空间 URI 和前缀。|  
|`FC_KeepInContent`|指示是否应将引用的属性值包含到源的内容部分和映射的位置中。 有效值为 `true` 和 `false`。 若要使结果源与早期版本的向后兼容[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]，将值指定为`true`以确保将该值包含在该数据源的内容部分中。|  
|`FC_NsPrefix`|非联合映射中的 XML 元素的命名空间前缀。 此特性必须与 `FC_NsUri` 特性一起使用，但不能与 `FC_ContentKind` 特性一起使用。|  
|`FC_NsUri`|非联合映射中的 XML 元素的命名空间 URI。 此特性必须与 `FC_NsPrefix` 特性一起使用，但不能与 `FC_ContentKind` 特性一起使用。|  
|`FC_SourcePath`|应用此源映射规则的实体属性的路径。 仅当在 `EntityType` 元素中使用时，才支持此特性。<br /><br /> <xref:System.Data.Services.Common.EntityPropertyMappingAttribute.SourcePath%2A>属性无法直接引用复杂类型。 对于复杂类型，必须使用路径表达式，在此路径表达式中，使用反斜杠 (`/`) 字符分隔属性名称。 例如，针对某个实体类型可以为下列值`Person`具有整数属性`Age`和复杂属性<br /><br /> `Address`：<br /><br /> `Age`<br /><br /> `Address/Street`<br /><br /> <xref:System.Data.Services.Common.EntityPropertyMappingAttribute.SourcePath%2A>属性不能设置为一个值，包含空格或无效属性名称中的任何其他字符。|  
|`FC_TargetPath`|属性将映射到的结果源中的目标元素的名称。 此元素可以是按 Atom 规范定义的元素，也可以是自定义元素。<br /><br /> 以下关键字是指向 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源中特定位置的预定义联合目标路径值。<br /><br /> `SyndicationAuthorEmail:``atom:email`的子元素`atom:author`元素。<br /><br /> `SyndicationAuthorName:``atom:name`的子元素`atom:author`元素。<br /><br /> `SyndicationAuthorUri:``atom:uri`的子元素`atom:author`元素。<br /><br /> `SyndicationContributorEmail:``atom:email`的子元素`atom:contributor`元素。<br /><br /> `SyndicationContributorName:``atom:name`的子元素`atom:contributor`元素。<br /><br /> `SyndicationContributorUri:``atom:uri`的子元素`atom:contributor`元素。<br /><br /> `SyndicationCustomProperty:`一个自定义属性元素。 映射到自定义元素时，目标必须是路径表达式，在此路径表达式中，使用反斜杠 (`/`) 分隔嵌套元素，并使用 `@` 指定特性。 在以下示例中，字符串 `UnitsInStock/@ReorderLevel` 将属性值映射到根项元素的 `ReorderLevel` 子元素上的 `UnitsInStock` 特性。<br /><br /> `<Property Name="ReorderLevel" Type="Int16"               m:FC_TargetPath="UnitsInStock/@ReorderLevel"               m:FC_NsPrefix="Northwind"               m:FC_NsUri="http://schemas.examples.microsoft.com/dataservices"               m:FC_KeepInContent="false"               />`<br /><br /> 如果目标是自定义元素名称，还必须指定 `FC_NsPrefix` 和 `FC_NsUri` 特性。<br /><br /> `SyndicationPublished:``atom:published`元素。<br /><br /> `SyndicationRights:``atom:rights`元素。<br /><br /> `SyndicationSummary:``atom:summary`元素。<br /><br /> `SyndicationTitle:``atom:title`元素。<br /><br /> `SyndicationUpdated:``atom:updated`元素。<br /><br /> 这些关键字的值相等， <xref:System.Data.Services.Common.SyndicationItemProperty>枚举用于反射提供程序。|  
  
> [!NOTE]
>  特性名称和值是区分大小写的。 特性可以应用于 `EntityType` 元素，也可以应用于一个或多个 `Property` 元素，但不能同时应用于二者。  
  
## <a name="customizing-feeds-with-the-reflection-provider"></a>使用反射提供程序自定义源  
 若要自定义源通过使用反射提供程序实施的数据模型，将添加一个或多个实例<xref:System.Data.Services.Common.EntityPropertyMappingAttribute>属性设为表示数据模型中的实体类型的类。 属性的<xref:System.Data.Services.Common.EntityPropertyMappingAttribute>类对应于上一节中介绍的源自的定义特性。 以下是 `Order` 类型的声明示例，该示例为两个属性定义了自定义源映射。  
  
> [!NOTE]
>  在主题中定义此示例中的数据模型[如何︰ 创建数据服务使用反射提供程序](../../../../docs/framework/data/wcf/create-a-data-service-using-rp-wcf-data-services.md)。  
  
  [Astoria 自定义源 #CustomOrderFeed](../CodeSnippet/VS_Snippets_Misc/astoria custom feeds#customorderfeed)]  
  
 这些特性为 `Orders` 实体集生成以下自定义数据源。 在此自定义源，`OrderId`属性值仅显示在`title`元素`entry`和`Customer`属性值则同时显示在`author`元素并将它作为`Customer`属性元素︰  
  
  [Astoria 自定义源 #IQueryableFeedResult](../CodeSnippet/VS_Snippets_Misc/astoria custom feeds#iqueryablefeedresult)]  
  
 有关详细信息，请参阅[如何︰ 使用反射提供程序自定义源](../../../../docs/framework/data/wcf/how-to-customize-feeds-with-the-reflection-provider-wcf-data-services.md)。  
  
## <a name="customizing-feeds-with-a-custom-data-service-provider"></a>使用自定义数据服务提供程序自定义源  
 为资源类型通过调用定义中使用自定义数据服务提供商定义的数据模型的源自定义<xref:System.Data.Services.Providers.ResourceType.AddEntityPropertyMappingAttribute%2A>上<xref:System.Data.Services.Providers.ResourceType>表示数据模型中的实体类型。 有关详细信息，请参阅[自定义数据服务提供商](../../../../docs/framework/data/wcf/custom-data-service-providers-wcf-data-services.md)。  
  
## <a name="consuming-custom-feeds"></a>使用自定义源  
 如果您的应用程序直接使用[!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]源，它必须能够处理任何自定义的元素和属性返回的源中。 如果已在数据模型中实现自定义源，不管数据服务提供程序如何，`$metadata` 终结点都会返回自定义源信息，并作为数据服务返回的 CSDL 中的自定义源特性。 当您使用**添加服务引用**对话框或[datasvcutil.exe](../../../../docs/framework/data/wcf/wcf-data-service-client-utility-datasvcutil-exe.md)工具生成客户端数据服务类时，自定义源的特性可以保证以正确处理请求和响应发送给数据服务。  
  
## <a name="feed-customization-considerations"></a>源自定义注意事项  
 定义自定义源映射时，应考虑下列事项。  
  
-   当源中的映射元素只包含空白时，[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]客户端将这些元素视为空。 因此，在具有相同空白的客户端上不会具体化只包含空白的映射元素。 为了防止客户端上包含这种空白，在源映射特性中，必须将 `KeepInContext` 的值设置为 `true`。  
  
## <a name="versioning-requirements"></a>版本控制要求  
 源自定义具有以下 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 协议版本控制要求：  
  
-   源自定义要求客户端和数据服务都支持 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 协议的 2.0 版本以及更高版本。  
  
 有关详细信息，请参阅[数据服务版本管理](../../../../docs/framework/data/wcf/data-service-versioning-wcf-data-services.md)。  
  
## <a name="see-also"></a>另请参阅  
 [反射提供程序](../../../../docs/framework/data/wcf/reflection-provider-wcf-data-services.md)   
 [实体框架提供程序](../../../../docs/framework/data/wcf/entity-framework-provider-wcf-data-services.md)