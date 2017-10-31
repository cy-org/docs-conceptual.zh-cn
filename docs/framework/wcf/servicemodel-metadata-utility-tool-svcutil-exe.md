---
title: "ServiceModel 元数据实用工具 (Svcutil.exe) | Microsoft Docs"
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
  - "客户端 [WCF], 生成"
  - "终结点 [WCF]"
  - "Svcutil.exe"
  - "客户端 [WCF], 使用服务"
ms.assetid: 1abf3d9f-b420-46f1-b628-df238751f308
caps.latest.revision: 40
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 38
---
# ServiceModel 元数据实用工具 (Svcutil.exe)
ServiceModel 元数据实用工具用于依据元数据文档生成服务模型代码，以及依据服务模型代码生成元数据文档。  
  
## SvcUtil.exe  
 ServiceModel 元数据实用工具可在 Windows SDK 安装位置中找到，具体位置为 C:\\Program Files\\Microsoft SDKs\\Windows\\v6.0\\Bin  
  
### 功能  
 下表概括了此工具提供的各种功能，以及论述如何使用该工具的对应主题。  
  
|任务|主题|  
|--------|--------|  
|依据运行的服务或静态元数据文档生成代码。|[根据服务元数据生成 WCF 客户端](../../../docs/framework/wcf/feature-details/generating-a-wcf-client-from-service-metadata.md)|  
|从编译的代码中导出元数据文档。|[如何：使用 Svcutil.exe 将元数据从已编译的服务代码中导出](../../../docs/framework/wcf/feature-details/how-to-use-svcutil-exe-to-export-metadata-from-compiled-service-code.md)|  
|验证编译的服务代码。|[如何：使用 Svcutil.exe 验证已编译的服务代码](../../../docs/framework/wcf/feature-details/how-to-use-svcutil-exe-to-validate-compiled-service-code.md)|  
|从运行的服务中下载元数据文档。|[如何：使用 Svcutil.exe 下载元数据文档](../../../docs/framework/wcf/feature-details/how-to-use-svcutil-exe-to-download-metadata-documents.md)|  
|生成序列化代码。|[如何：使用 XmlSerializer 改善 WCF 客户端应用程序的启动时间](../../../docs/framework/wcf/feature-details/startup-time-of-wcf-client-applications-using-the-xmlserializer.md)|  
  
> [!CAUTION]
>  如果以参数形式提供的名称相同，Svcutil 将覆盖磁盘上的现有文件。 这可能包括代码文件、配置或元数据文件。 若要在生成代码和配置文件时避免这种情况，请使用 `/mergeConfig` 开关。  
>   
>  此外，用于引用类型的 `/r` 和 `/ct` 开关将用于生成数据协定。 使用 XmlSerializer 时，这些开关不起作用。  
  
### 超时  
 该工具在检索元数据时有 5 分钟的超时。  此超时仅适用于通过网络检索元数据的操作。 它不适用于该元数据的任何处理操作。  
  
### 多目标  
 该工具不支持多目标。 如果希望从 svcutil.exe 生成 .NET 4 项目，则必须使用 .NET 4 SDK 中的 svcutil.exe。 若要生成 .NET 3.5 项目，请使用 .NET 3.5 SDK 中的可执行文件。  
  
### 访问 WSDL 文档  
 使用 Svcutil 来访问具有对安全令牌服务 \(STS\) 的引用的 WSDL 文档时，Svcutil 将对 STS 执行 WS\-MetadataExchange 调用。 但是，服务可以使用 WS\-MetadataExchange 或 HTTP GET 来公开其 WSDL 文档。 因此，如果 STS 仅使用 HTTP GET 公开 WSDL 文档，则用 [!INCLUDE[vstecwinfx](../../../includes/vstecwinfx-md.md)] 编写的客户端将失败。 对于用 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] 编写的客户端，Svcutil 将尝试使用 WS\-MetadataExchange 和 HTTP GET 来获取 STS WSDL。  
  
## 使用 SvcUtil.exe  
  
### 常见用法  
 下表显示了此工具的一些常用选项。  
  
|选项|描述|  
|--------|--------|  
|\/directory:\<目录\>|要在其中创建文件的目录。<br /><br /> 默认设置：当前目录。<br /><br /> 缩写形式：`/d`|  
|\/help|显示此工具的命令语法和选项。<br /><br /> 缩写形式：`/?`|  
|\/noLogo|取消版权和标题消息。|  
|\/svcutilConfig:\<配置文件\>|指定要取代 App.config 文件使用的自定义配置文件。 可以使用该自定义配置文件来注册 system.serviceModel 扩展，而无需更改工具的配置文件。|  
|\/target:\<输出类型\>|指定要由工具生成的输出。<br /><br /> 有效的值为代码、元数据或 xmlSerializer。<br /><br /> 缩写形式：`/t`|  
  
### 代码生成  
 Svcutil.exe 可以依据元数据文档为服务协定、客户端和数据类型生成代码。 这些元数据文档可以位于持久存储区上，也可以联机检索。 联机检索采用 WS\-Metadata Exchange 协议或 DISCO 协议（有关详细信息，请参见“元数据下载”一节）。  
  
 可以使用 SvcUtil.exe 工具生成基于预定义 WSDL 文档的服务和数据协定。 使用 \/serviceContract 开关并指定可以从中下载或找到 WSDL 文档的 URL 或文件位置。 这将生成在 WSDL 文档中定义的服务和数据约定，然后它们可以用来实现投诉服务。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [如何：检索元数据并实现兼容服务。](../../../docs/framework/wcf/feature-details/how-to-retrieve-metadata-and-implement-a-compliant-service.md).  
  
 而对于使用 BasicHttpContextbinding 终结点的服务，Svcutil.exe 将生成 `allowCookies` 属性设置为 `true` 的 BasicHttpBinding。 Cookie 用于服务器上的上下文。 如果在服务使用 Cookie 时，您要管理客户端上的上下文，则可以手动修改配置以使用上下文绑定。  
  
> [!CAUTION]
>  Svcutil.exe 基于 WSDL 或从服务收到的策略文件生成客户端。 用户主要名称 \(UPN\) 是通过将用户名、“@”和完全限定域名 \(FQDN\) 串联在一起生成的。 但是，对于在 Active Directory 上注册的用户，此格式无效，并且工具生成的 UPN 将导致 Kerberos 身份验证失败，错误消息为“登录没有成功”。 若要解决此问题，您应手动修复此工具生成的客户端文件。  
  
 `svcutil.exe [/t:code]  <metadataDocumentPath>* | <url>* | <epr>`  
  
|参数|说明|  
|--------|--------|  
|`epr`|XML 文件的路径，该文件包含支持 WS\-Metadata Exchange 的服务终结点的 WS\-Addressing EndpointReference。 有关更多信息，请参见“元数据下载”一节。|  
|`metadataDocumentPath`|元数据文档（wsdl 或 xsd）的路径，该文档包含要导入代码（.wsdl、.xsd、.wspolicy 或 .wsmex）的协定。<br /><br /> 当您为元数据指定远程 URL 时，Svcutil 采用导入和包含的内容。 但是，如果要在本地文件系统上处理元数据文件，则必须在此参数中指定所有文件。 这样，您可以在不能有网络依赖项的生成环境中使用 Svcutil。 可以为此参数使用通配符（\*.xsd、\*.wsdl）。|  
|`url`|可提供元数据的服务终结点的 URL，或是联机承载的元数据文档的 URL。 有关如何检索这些文档的更多信息，请参见“元数据下载”一节。|  
  
|选项|描述|  
|--------|--------|  
|\/async|同时生成同步和异步方法签名。<br /><br /> 默认设置：只生成同步方法签名。<br /><br /> 缩写形式：`/a`|  
|\/collectionType:\<类型\>|同时生成同步和异步方法签名。<br /><br /> 默认设置：只生成同步方法签名。<br /><br /> 缩写形式：`/a`|  
|\/config:\<配置文件\>|为生成的配置文件指定文件名。<br /><br /> 默认设置：output.config|  
|\/dataContractOnly|只为数据协定类型生成代码。 不生成服务协定类型。<br /><br /> 只应为此选项指定本地元数据文件。<br /><br /> 缩写形式：`/dconly`|  
|\/enableDataBinding|在所有数据协定类型上实现 <xref:System.ComponentModel.INotifyPropertyChanged> 接口以启用数据绑定。<br /><br /> 缩写形式：`/edb`|  
|\/excludeType:\<类型\>|指定要从引用的协定类型中排除的完全限定或程序集限定类型名称。<br /><br /> 从单独的 DLL 中将此开关与 `/r` 一起使用时，将引用 XSD 类的全名。<br /><br /> 缩写形式：`/et`|  
|\/importXmlTypes|配置数据协定序列化程序，以便将非数据协定类型作为 IXmlSerializable 类型导入。|  
|\/internal|生成标记为内部的类。 默认设置：只生成公共类。<br /><br /> 缩写形式：`/i`|  
|\/language:\<语言\>|指定要用于代码生成的编程语言。 您应提供在 Machine.config 文件中注册的语言名称，或继承自 <xref:System.CodeDom.Compiler.CodeDomProvider> 的类的完全限定名称。<br /><br /> 值：c\#、cs、csharp、vb、visualbasic、c\+\+、cpp<br /><br /> 默认设置：csharp<br /><br /> 缩写形式：`/l` **Note:**  对于 Visual Studio 2005 SP1 附带的代码提供程序，此开关只支持 C\+\+。|  
|\/mergeConfig|将生成的配置合并到现有文件中，而不是覆盖现有文件。|  
|\/messageContract|生成消息协定类型。<br /><br /> 缩写形式：`/mc`|  
|\/namespace:\<字符串,字符串\>|指定从 WSDL 或 XML 架构 targetNamespace 到 CLR 命名空间的映射。 如果为 targetNamespace 使用“\*”，则会映射所有 targetNamespace，而不显式映射到该 CLR 命名空间。<br /><br /> 为了确保消息协定名称与操作名称不冲突，您应使用 `::` 限定类型引用，或确保名称是唯一的。<br /><br /> 默认设置：派生自数据协定架构文档的目标命名空间。 默认命名空间用于所有其他生成的类型。<br /><br /> 缩写形式：`/n`|  
|\/noConfig|不生成配置文件。|  
|\/noStdLib|不引用标准库。<br /><br /> 默认设置：引用 Mscorlib.dll 和 System.servicemodel.dll。|  
|\/out:\<文件\>|为生成的代码指定文件名。<br /><br /> 默认设置：派生自某个架构的 WSDL 定义名称、WSDL 服务名称或目标命名空间。<br /><br /> 缩写形式：`/o`|  
|\/reference:\<文件路径\>|引用指定程序集中的类型。 在生成客户端时，使用此选项来指定可能包含类型的程序集，这些类型表示所导入的元数据。<br /><br /> 无法使用此开关指定消息协定和 <xref:System.Xml.Serialization.XmlSerializer> 类型。<br /><br /> 如果引用了 <xref:System.DateTimeOffset>，则会使用此类型，而不是生成新类型。 如果应用程序是使用 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] 编写的，则 SvcUtil.exe 会自动引用 <xref:System.DateTimeOffset>。<br /><br /> 缩写形式：`/r`|  
|\/serializable|生成用 Serializable 属性标记的类。<br /><br /> 缩写形式：`/s`|  
|\/serviceContract|仅生成服务协定的代码。 不会生成客户端类和配置<br /><br /> 缩写形式：`/sc`|  
|\/serializer:Auto|生成用 Serializable 属性标记的类。<br /><br /> 缩写形式：`/s`|  
|\/serializer:DataContractSerializer|生成使用数据协定序列化程序进行序列化和反序列化的数据类型。<br /><br /> 缩写形式：`/ser:DataContractSerializer`|  
|\/serializer:XmlSerializer|生成使用 <xref:System.Xml.Serialization.XmlSerializer> 进行序列化和反序列化的数据类型。<br /><br /> 缩写形式：`/ser:XmlSerializer`|  
|\/targetClientVersion|指定应用程序针对 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 的哪个版本。 有效值为 `Version30` 和 `Version35`。 默认值为 `Version30`。<br /><br /> 缩写形式：`/tcv`<br /><br /> `Version30`：如果为使用 `/tcv:Version30` 的客户端生成代码，则使用 [!INCLUDE[vstecwinfx](../../../includes/vstecwinfx-md.md)]。<br /><br /> `Version35`：如果为使用 `/tcv:Version35` 的客户端生成代码，则使用 [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)]。 如果将 `/tcv:Version35` 与 `/async` 开关一起使用，则会同时生成基于事件的异步方法和基于回调\/委托的异步方法。 此外，还能够支持启用 LINQ 的数据集和 <xref:System.DateTimeOffset>。|  
|\/wrapped|控制是否对具有包装参数的 document\-literal 样式的文档使用特殊大小写。 请使用 **\/wrapped** 开关和 [Service Model Metadata Utility Tool \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 工具来指定正常大小写。|  
  
> [!NOTE]
>  如果服务绑定是系统提供的绑定（请参阅[系统提供的绑定](../../../docs/framework/wcf/system-provided-bindings.md)）之一，并且 <xref:System.ServiceModel.ServiceContractAttribute.ProtectionLevel%2A> 属性设置为 `None` 或 `Sign`，Svcutil 将使用 [\<customBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md) 元素（而不是预期的系统提供的元素）生成配置文件。 例如，如果服务使用 `<wsHttpBinding>` 设置为 `ProtectionLevel` 的 `Sign` 元素，则生成的配置在绑定部分中将有 `<customBinding>`，而不是 `<wsHttpBinding>`。 有关保护级别的详细信息，请参阅[了解保护级别](../../../docs/framework/wcf/understanding-protection-level.md)。  
  
### 元数据导出  
 Svcutil.exe 可以导出已编译程序集中服务、协定和数据类型的元数据。 若要导出服务的元数据，您必须使用 `/serviceName` 选项指定要导出的服务。 若要导出程序集内的所有数据协定类型，应使用 `/dataContractOnly` 选项。 默认情况下，将为输入程序集中的所有服务协定导出元数据。  
  
 `svcutil.exe [/t:metadata] [/serviceName:<serviceConfigName>] [/dataContractOnly] <assemblyPath>*`  
  
|参数|说明|  
|--------|--------|  
|`assemblyPath`|指定程序集的路径，该程序集包含要导出的服务、协定或数据协定类型。 可以使用标准命令行通配符提供多个文件作为输入。|  
  
|选项|描述|  
|--------|--------|  
|\/serviceName:\<服务配置名称\>|指定要导出的服务的配置名称。 如果使用此选项，则必须传递包含关联配置文件的可执行程序集作为输入。 Svcutil.exe 将为服务配置搜索所有关联的配置文件。 如果配置文件包含任何扩展类型，则包含这些类型的程序集必须位于 GAC 中，或者必须使用 `/reference` 选项显式提供。|  
|\/reference:\<文件路径\>|将指定程序集添加到用于解析类型引用的一组程序集中。 如果要导出或验证使用在配置中注册的第三方扩展（行为、绑定和绑定元素）的服务，请使用此选项找到不在 GAC 中的扩展程序集。<br /><br /> 缩写形式：`/r`|  
|\/dataContractOnly|只对数据协定类型进行操作。 不会处理服务协定。<br /><br /> 只应为此选项指定本地元数据文件。<br /><br /> 缩写形式：`/dconly`|  
|\/excludeType:\<类型\>|指定要从导出中排除的类型的完全限定或程序集限定名称。 在为服务或一组服务协定导出元数据时，可以使用此选项来防止导出某些类型。 此选项不能与 `/dconly` 选项一起使用。<br /><br /> 如果有包含多个服务的单一程序集，并且每个服务都使用具有相同 XSD 名称的单独的类，则您应为此开关指定服务名称，而不是 XSD 类名称。<br /><br /> 不支持 XSD 或数据协定类型。<br /><br /> 缩写形式：`/et`|  
  
### 服务验证  
 可以使用验证在不承载服务的情况下检测服务实现中的错误。 必须使用 `/serviceName` 选项指示要验证的服务。  
  
 `svcutil.exe /validate /serviceName:<serviceConfigName>  <assemblyPath>*`  
  
|参数|说明|  
|--------|--------|  
|`assemblyPath`|指定程序集的路径，该程序集包含要验证的服务类型。 程序集必须具有相关联的配置文件才能提供服务配置。 可以使用标准命令行通配符来提供多个程序集。|  
  
|选项|描述|  
|--------|--------|  
|\/validate|验证 `/serviceName` 选项指定的服务实现。 如果使用此选项，则必须传递包含关联配置文件的可执行程序集作为输入。<br /><br /> 缩写形式：`/v`|  
|\/serviceName:\<服务配置名称\>|指定要验证的服务的配置名称。 Svcutil.exe 将为服务配置搜索所有输入程序集的所有关联配置文件。 如果配置文件包含任何扩展类型，则包含这些类型的程序集必须位于 GAC 中，或者必须使用 `/reference` 选项显式提供。|  
|\/reference:\<文件路径\>|将指定程序集添加到用于解析类型引用的一组程序集中。 如果要导出或验证使用在配置中注册的第三方扩展（行为、绑定和绑定元素）的服务，请使用此选项找到不在 GAC 中的扩展程序集。<br /><br /> 缩写形式：`/r`|  
|\/dataContractOnly|只对数据协定类型进行操作。 不会处理服务协定。<br /><br /> 只应为此选项指定本地元数据文件。<br /><br /> 缩写形式：`/dconly`|  
|\/excludeType:\<类型\>|指定要从验证中排除的类型的完全限定或程序集限定名称。<br /><br /> 缩写形式：`/et`|  
  
### 元数据下载  
 可以使用 Svcutil.exe 从运行的服务中下载元数据，并将元数据保存到本地文件。 若要下载元数据，您必须指定 `/t:metadata` 选项。 否则，将生成客户端代码。 对于 HTTP 和 HTTPS URL 方案，Svcutil.exe 会尝试使用 WS\-Metadata Exchange 和 DISCO 检索元数据。 对于所有其他 URL 方案，Svcutil.exe 只使用 WS\-Metadata Exchange。  
  
 Svcutil 会同时发出以下元数据请求以检索元数据。  
  
-   针对所提供地址的 MEX \(WS\-Transfer\) 请求  
  
-   针对所提供地址的 MEX 请求（附加有 \/mex）  
  
-   针对所提供地址的 DISCO 请求（使用 ASMX 中的 DiscoveryClientProtocol）。  
  
 默认情况下，Svcutil.exe 使用 <xref:System.ServiceModel.Description.MetadataExchangeBindings> 类中定义的绑定进行 MEX 请求。 若要配置用于 WS\-Metadata Exchange 的绑定，您必须在使用 IMetadataExchange 协定的配置中定义一个客户端终结点。 可以在 Svcutil.exe 的配置文件中定义此终结点，也可以在使用 `/svcutilConfig` 选项指定的另一个配置文件中定义。  
  
 `svcutil.exe /t:metadata  <url>* | <epr>`  
  
|参数|说明|  
|--------|--------|  
|`url`|可提供元数据的服务终结点的 URL，或是联机承载的元数据文档的 URL。|  
|`epr`|XML 文件的路径，该文件包含支持 WS\-Metadata Exchange 的服务终结点的 WS\-Addressing EndpointReference。|  
  
### XmlSerializer 类型生成  
 如果服务和客户端应用程序使用可用 <xref:System.Xml.Serialization.XmlSerializer> 进行序列化的数据类型，则会在运行时生成并编译这些数据类型的序列化代码，从而导致启动性能降低。  
  
> [!NOTE]
>  预生成的序列化代码只能在客户端应用程序中使用，不能在服务中使用。  
  
 Svcutil.exe 可依据应用程序的已编译程序集生成必要的 C\# 序列化代码，因而可提高这些应用程序的启动性能。 有关详细信息，请参阅[如何：使用 XmlSerializer 改善 WCF 客户端应用程序的启动时间](../../../docs/framework/wcf/feature-details/startup-time-of-wcf-client-applications-using-the-xmlserializer.md)。  
  
> [!NOTE]
>  Svcutil.exe 只会为输入程序集中的服务协定使用的类型生成代码。  
  
 `svcutil.exe /t:xmlSerializer  <assemblyPath>*`  
  
|参数|描述|  
|--------|--------|  
|`assemblyPath`|指定包含服务协定类型的程序集的路径。 为每个协定中的所有 Xml 可序列化类型生成序列化类型。|  
  
|选项|描述|  
|--------|--------|  
|\/reference:\<文件路径\>|将指定程序集添加到用于解析类型引用的一组程序集中。<br /><br /> 缩写形式：`/r`|  
|\/excludeType:\<类型\>|指定要从导出或验证中排除的类型的完全限定或程序集限定名称。<br /><br /> 缩写形式：`/et`|  
|\/out:\<文件\>|为生成的代码指定文件名。 如果将多个程序集作为输入传递到工具，则会忽略此选项。<br /><br /> 默认设置：派生自程序集名称。<br /><br /> 缩写形式：`/o`|  
|\/UseSerializerForFaults|指定应该使用 <xref:System.Xml.XmlSerializer>（而不是默认的 <xref:System.Runtime.Serialization.DataContractSerializer>）来读取和写入错误。|  
  
## 示例  
 以下命令将依据运行的服务或联机元数据文档生成客户端代码。  
  
 `svcutil http://service/metadataEndpoint`  
  
 以下命令将依据本地元数据文档生成客户端代码。  
  
 `svcutil *.wsdl *.xsd /language:C#`  
  
 以下命令将依据本地架构文档用 Visual Basic 生成数据协定类型。  
  
 `svcutil /dconly *.xsd /language:VB`  
  
 以下命令从运行的服务中下载元数据文档。  
  
 `svcutil /t:metadata http://service/metadataEndpoint`  
  
 以下命令为程序集中的服务协定和关联的类型生成元数据文档。  
  
 `svcutil myAssembly.dll`  
  
 以下命令为程序集中的服务以及所有关联的服务协定和数据类型生成元数据文档。  
  
 `svcutil myServiceHost.exe /serviceName:myServiceName`  
  
 以下命令为程序集中的数据类型生成元数据文档。  
  
 `svcutil myServiceHost.exe /dconly`  
  
 以下命令验证服务主机。  
  
 `svcutil /validate /serviceName:myServiceName myServiceHost.exe`  
  
 以下命令为程序集中任何服务协定使用的 <xref:System.Xml.Serialization.XmlSerializer> 类型生成序列化类型。  
  
 `svcutil /t:xmlserializer myContractLibrary.exe`  
  
## 最大名称表字符计数配额  
 使用 svcutil 生成服务的元数据时，您会收到以下消息：  
  
 错误: 无法从 http:\/\/localhost:8000\/somesservice\/mex 获取元数据。读取 XML 数据时，超出最大名称表字符计数配额\(16384\)。 名称表是用于存储在处理 XML 时所遇到的字符串的数据结构 \- 具有非重复元素名称、特性名称和特性值的长 XML 文档可能会触发此配额。 通过更改在创建 XML 读取器时所使用的 XmlDictionaryReaderQuotas 对象的 MaxNameTableCharCount 属性，可增加此配额。  
  
 如果您请求某个服务的元数据时返回大 WSDL 文件，则该服务会导致此错误。 问题在于超过了 svcutil.exe 工具的字符配额。 设置此值是为了帮助防止遭受拒绝服务 \(dos\) 攻击。 您可以通过为 svcutil 指定下面的配置文件来增加此配额。  
  
 下面的配置文件演示如何设置 svcutil 的读取器配额  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
    <system.serviceModel>  
        <bindings>  
            <customBinding>  
                <binding name="MyBinding">  
                    <textMessageEncoding>  
                        <readerQuotas maxDepth="2147483647" maxStringContentLength="2147483647"  
                            maxArrayLength="2147483647" maxBytesPerRead="2147483647" maxNameTableCharCount="2147483647" />  
                    </textMessageEncoding>  
                    <httpTransport maxReceivedMessageSize="2147483647" maxBufferSize="2147483647" />  
                </binding>  
            </customBinding>  
        </bindings>  
        <client>  
            <endpoint binding="customBinding" bindingConfiguration="MyBinding"  
                contract="IMetadataExchange"  
                name="http" />  
        </client>  
    </system.serviceModel>  
</configuration>  
```  
  
 新建一个名为 svcutil.exe.config 的文件，再将 XML 示例代码复制到该文件中。 然后将该文件放到与 svcutil.exe 相同的目录中。 下次运行 svcutil.exe 时，它会选取新的设置。  
  
## 安全问题  
 您应使用适当的访问控制列表 \(ACL\) 来保护 Svcutil.exe 的安装文件夹、Svcutil.config 以及 `/svcutilConfig` 所指向的文件。 这样可以防止恶意扩展注册并运行。  
  
 此外，为了将安全性受到危害的可能性降到最低，您不应在系统中添加不受信任的扩展，或将不受信任的代码提供程序用于 Svcutil.exe。  
  
 最后，您不应在应用程序的中间层中使用该工具，因为它可能会导致当前进程拒绝服务。  
  
## 请参阅  
 <xref:System.Runtime.Serialization.DataContractAttribute>   
 <xref:System.Runtime.Serialization.DataMemberAttribute>   
 [如何：创建客户端](../../../docs/framework/wcf/how-to-create-a-wcf-client.md)