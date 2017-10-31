---
title: "&lt;serviceMetadata&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: 2b4c3b4c-31d4-4908-a9b7-5bb411c221f2
caps.latest.revision: 28
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 28
---
# &lt;serviceMetadata&gt;
指定服务元数据的发布和相关信息。  
  
## 语法  
  
```  
  
<serviceMetadata   
    externalMetadataLocation="String"  
    httpGetBinding=”String”  
    httpGetBindingConfiguration=”String”  
    httpGetEnabled="Boolean"   
    httpGetUrl="String"  
    httpsGetBinding=”String”  
    httpsGetBindingConfiguration=”String”  
    httpsGetEnabled="Boolean"   
    httpsGetUrl="String"  
    policyVersion="Policy12/Policy15"/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|externalMetadataLocation|一个包含 WSDL 文件的位置的 URI，该文件将返回到用户以响应 WSDL 和 MEX 请求而非自动生成的 WSDL。  当未设置此属性时，将返回默认的 WSDL。  默认值为一个空字符串。|  
|httpGetBinding|一个字符串，指定将用于通过 HTTP GET 进行元数据检索的绑定类型。  此设置是可选的。  如果未指定此设置，则将使用默认绑定。<br /><br /> 仅支持具有支持 <xref:System.ServiceModel.Channels.IReplyChannel> 的内部绑定元素的绑定。  此外，绑定的 <xref:System.ServiceModel.Channels.MessageVersion%2A> 属性必须为 <xref:System.ServiceModel.Channels.MessageVersion.None%2A>。|  
|httpGetBindingConfiguration|一个字符串，用于设置在 `httpGetBinding` 特性中指定的绑定的名称，此名称引用此绑定的其他配置信息。  必须在 `<bindings>` 节中定义相同的名称。|  
|httpGetEnabled|一个布尔值，指定是否发布服务元数据以便使用 HTTP\/Get 请求进行检索。  默认值为 `false`。<br /><br /> 如果未指定 httpGetUrl 属性，则发布元数据的地址为服务地址加上“?wsdl”。  例如，如果服务地址为“http:\/\/localhost:8080\/CalculatorService”，则 HTTP\/Get 元数据地址为“http:\/\/localhost:8080\/CalculatorService?wsdl”。<br /><br /> 如果此属性为 `false`，或服务的地址不基于 HTTP 或 HTTPS，则忽略“?wsdl”。|  
|httpGetUrl|一个 URI，指定发布元数据的地址以便使用 HTTP\/Get 请求进行检索。  如果指定了相对 Uri，则它将被视为相对于服务的基址。|  
|httpsGetBinding|一个字符串，指定将用于通过 HTTPS GET 进行元数据检索的绑定类型。  此设置是可选的。  如果未指定此设置，则将使用默认绑定。<br /><br /> 仅支持具有支持 <xref:System.ServiceModel.Channels.IReplyChannel> 的内部绑定元素的绑定。  此外，绑定的 <xref:System.ServiceModel.Channels.MessageVersion%2A> 属性必须为 <xref:System.ServiceModel.Channels.MessageVersion.None%2A>。|  
|httpsGetBindingConfiguration|一个字符串，用于设置在 `httpsGetBinding` 特性中指定的绑定的名称，此名称引用此绑定的其他配置信息。  必须在 `<bindings>` 节中定义相同的名称。|  
|httpsGetEnabled|一个布尔值，指定是否发布服务元数据以便使用 HTTPS\/Get 请求进行检索。  默认值为 `false`。<br /><br /> 如果未指定 httpsGetUrl 属性，则发布元数据的地址为服务地址加上“?wsdl”。  例如，如果服务地址为“https:\/\/localhost:8080\/CalculatorService”，则 HTTP\/Get 元数据地址为“https:\/\/localhost:8080\/CalculatorService?wsdl”。<br /><br /> 如果此属性为 `false`，或服务的地址不基于 HTTP 或 HTTPS，则忽略“?wsdl”。|  
|httpsGetUrl|一个 URI，指定发布元数据的地址以便使用 HTTPS\/Get 请求进行检索。|  
|policyVersion|一个字符串，指定所使用的 WS\-Policy 规范的版本。  此属性的类型为 <xref:System.ServiceModel.Description.PolicyVersion>。|  
  
### 子元素  
 无  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<行为\>](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)|指定行为元素。|  
  
## 备注  
 此配置元素允许您控制服务的元数据发布功能。  为了防止无意中泄露潜在的敏感服务元数据，[!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 服务的默认配置将禁用元数据发布。  默认情况下此行为是安全的，但也意味着您无法使用元数据导入工具（例如 Svcutil.exe）生成调用服务所需的客户端代码，除非在配置中显式启用服务的元数据发布行为。  使用此配置元素，可以为服务启用此发布行为。  
  
 有关配置此行为的详细代码示例，请参见[元数据发布行为](../../../../../docs/framework/wcf/samples/metadata-publishing-behavior.md)。  
  
 利用可选的 `httpGetBinding` 和 `httpsGetBinding`属性，您可以配置用于通过 HTTP GET（或 HTTPS GET）检索元数据的绑定。  如果未指定这两个属性，则根据情况使用相应的默认绑定（采用 HTTP 时为 `HttpTransportBindingElement`，采用 HTTPS 时为 `HttpsTransportBindingElement`）进行元数据检索。  请注意：不能将这些属性用于内置 WCF 绑定。  仅支持具有支持 <xref:System.ServiceModel.Channels.IReplyChannel> 的内部绑定元素的绑定。  此外，绑定的 <xref:System.ServiceModel.Channels.MessageVersion%2A> 属性必须为 <xref:System.ServiceModel.Channels.MessageVersion.None%2A>。  
  
 为了降低服务被恶意使用者滥用的可能性，可以使用 SSL over HTTP \(HTTPS\) 机制来确保传输的安全。  为此，必须首先将一个适合的 X.509 证书绑定到承载该服务的计算机上的特定端口。  \([!INCLUDE[crdefault](../../../../../includes/crdefault-md.md)] [使用证书](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)。）然后，将此元素添加到服务配置，并将 `httpsGetEnabled` 属性设置为 `true`。  最后，将 `httpsGetUrl` 属性设置为服务元数据终结点的 URL，如下面的示例所示。  
  
```  
<behaviors>  
 <serviceBehaviors>  
  <behavior name="NewBehavior">  
    <serviceMetadata httpsGetEnabled="true"   
     httpsGetUrl="https://myComputerName/myEndpoint" />  
  </behavior>  
 </serviceBehaviors>  
</behaviors>  
```  
  
## 示例  
 下面的示例配置服务以便使用 \<serviceMetadata\> 元素公开元数据。  它还配置终结点以便将 `IMetadataExchange` 协定作为 WS\-MetadataExchange \(MEX\) 协议的实现公开。  此示例使用的是 `mexHttpBinding`，这是一种便于使用的标准绑定，与安全模式设置为 `None` 的 `wsHttpBinding` 等效。  在终结点中使用相对地址“mex”，当针对服务基址对其进行解析时将得到终结点地址 http:\/\/localhost\/servicemodelsamples\/service.svc\/mex。  
  
```  
<configuration>  
<system.serviceModel>  
  <services>  
    <service   
        name="Microsoft.ServiceModel.Samples.CalculatorService"  
        behaviorConfiguration="CalculatorServiceBehavior">  
      <!-- This endpoint is exposed at the base address provided by the host: http://localhost/servicemodelsamples/service.svc  -->  
      <endpoint address=""  
                binding="wsHttpBinding"  
                contract="Microsoft.ServiceModel.Samples.ICalculator" />  
      <!-- the mex endpoint is exposed at http://localhost/servicemodelsamples/service.svc/mex   
           To expose the IMetadataExchange contract, you   
           must enable the serviceMetadata behavior as demonstrated below -->  
      <endpoint address="mex"  
                binding="mexHttpBinding"  
                contract="IMetadataExchange" />  
    </service>  
  </services>  
  
  <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
  <behaviors>  
    <serviceBehaviors>  
      <behavior name="CalculatorServiceBehavior">  
        <!-- The serviceMetadata behavior publishes metadata through   
             the IMetadataExchange contract. When this behavior is   
             present, you can expose this contract through an endpoint   
             as shown above. Setting httpGetEnabled to true publishes   
             the service's WSDL at the <baseaddress>?wsdl  
             eg. http://localhost/servicemodelsamples/service.svc?wsdl -->  
        <serviceMetadata httpGetEnabled="True"/>  
        <serviceDebug includeExceptionDetailInFaults="False" />  
      </behavior>  
    </serviceBehaviors>  
  </behaviors>  
  
</system.serviceModel>  
  
</configuration>  
```  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.ServiceMetadataPublishingElement>   
 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>   
 [安全行为](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)   
 [元数据发布行为](../../../../../docs/framework/wcf/samples/metadata-publishing-behavior.md)