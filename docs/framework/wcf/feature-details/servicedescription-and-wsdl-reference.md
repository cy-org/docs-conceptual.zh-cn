---
title: "ServiceDescription 和 WSDL 引用 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: eedc025d-abd9-46b1-bf3b-61d2d5c95fd6
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# ServiceDescription 和 WSDL 引用
本主题描述 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 如何在 Web 服务描述语言 \(WSDL\) 文档与 <xref:System.ServiceModel.Description.ServiceDescription> 实例之间进行映射。  
  
## ServiceDescription 如何映射到 WSDL 1.1  
 可以使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 为服务从 <xref:System.ServiceModel.Description.ServiceDescription> 实例导出 WSDL 文档。  发布元数据终结点时，将为服务自动生成 WSDL 文档。  
  
 还可以使用 `WsdlImporter` 类型从 WSDL 文档导入 <xref:System.ServiceModel.Description.ServiceEndpoint> 实例、<xref:System.ServiceModel.Description.ContractDescription> 实例和 <xref:System.ServiceModel.Channels.Binding> 实例。  
  
 由 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 导出的 WSDL 文档将从外部 XML 架构文档导入使用的所有 XML 架构定义。  为服务中数据类型使用的每个目标命名空间导出单独的 XML 架构文档。  同样，为服务协定使用的每个目标命名空间导出单独的 WSDL 文档。  
  
### ServiceDescription  
 <xref:System.ServiceModel.Description.ServiceDescription> 实例映射到 `wsdl:service` 元素。  <xref:System.ServiceModel.Description.ServiceDescription> 实例包含 <xref:System.ServiceModel.Description.ServiceEndpoint> 实例的集合，其中每个实例都映射到单独的 `wsdl:port` 元素。  
  
|属性|WSDL 映射|  
|--------|-------------|  
|`Name`|服务的 `wsdl:service`\/@name 值。|  
|`Namespace`|服务的 `wsdl:service` 定义的 targetNamespace。|  
|`Endpoints`|服务的 `wsdl:port` 定义。|  
  
### ServiceEndpoint  
 <xref:System.ServiceModel.Description.ServiceEndpoint> 实例映射到 `wsdl:port` 元素。  <xref:System.ServiceModel.Description.ServiceEndpoint> 实例包含一个地址、绑定和协定。  
  
 实现 <xref:System.ServiceModel.Description.IWsdlExportExtension> 接口的终结点行为可以修改它们所附加到的终结点的 `wsdl:port` 元素。  
  
|属性|WSDL 映射|  
|--------|-------------|  
|`Name`|终结点的 `wsdl:port`\/@name 值和终结点绑定的 `wsdl:binding`\/@name 值。|  
|`Address`|终结点的 `wsdl:port` 定义的地址。<br /><br /> 终结点的传输确定地址的格式。  例如，对于 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 支持的传输，则可能是 SOAP 地址或终结点引用。|  
|`Binding`|终结点的 `wsdl:binding` 定义。<br /><br /> 与 `wsdl:binding` 定义不同，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中的绑定不会与任何一个协定关联。|  
|`Contract`|终结点的 `wsdl:portType` 定义。|  
|`Behaviors`|实现 <xref:System.ServiceModel.Description.IWsdlExportExtension> 接口的终结点行为可以修改终结点的 `wsdl:port`。|  
  
### 绑定  
 `ServiceEndpoint` 实例的绑定实例映射到 `wsdl:binding` 定义。  `wsdl:binding` 定义与 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 绑定不同，前者必须与特定的 `wsdl:portType` 定义相关联，而后者独立于任何协定。  
  
 绑定由绑定元素的集合组成。  每个元素描述终结点与客户端的通信方式的某一方面。  另外，绑定还具有一个 <xref:System.ServiceModel.Channels.MessageVersion>，指示终结点的 <xref:System.ServiceModel.EnvelopeVersion> 和 <xref:System.ServiceModel.Channels.AddressingVersion>。  
  
|属性|WSDL 映射|  
|--------|-------------|  
|`Name`|在终结点的默认名称中使用，该名称是以下划线分隔追加的协定名称的绑定名称。|  
|`Namespace`|`wsdl:binding` 定义的 `targetNamespace`。<br /><br /> 导入时，如果将策略附加到 WSDL 端口，则导入的绑定命名空间将映射到 `wsdl:port` 定义的 `targetNamespace`。|  
|`BindingElementCollection`，由 `CreateBindingElements`\(\) 方法返回|`wsdl:binding` 定义的各种域特定的扩展，通常是策略断言。|  
|`MessageVersion`|终结点的 `EnvelopeVersion` 和 `AddressingVersion`。<br /><br /> 如果指定 `MessageVersion.None`，则 WSDL 绑定不包含 SOAP 绑定，并且 WSDL 端口不包含 WS\-Addressing 内容。  该设置通常用于 Plain Old XML \(POX\) 终结点。|  
  
#### BindingElements  
 终结点绑定的绑定元素映射到 `wsdl:binding` 中的各种 WSDL 扩展，如策略断言。  
  
 绑定的 <xref:System.ServiceModel.Channels.TransportBindingElement> 为 SOAP 绑定确定传输统一资源标识符 \(URI\)。  
  
#### AddressingVersion  
 绑定上的 `AddressingVersion` 映射到 `wsd:port` 中使用的寻址版本。  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 支持 SOAP 1.1 和 SOAP 1.2 地址以及 WS\-Addressing 08\/2004 和 WS\-Addressing 1.0 终结点引用。  
  
#### EnvelopeVersion  
 绑定上的 `EnvelopeVersion` 映射到 `wsdl:binding` 中使用的 SOAP 的版本。  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 支持 SOAP 1.1 和 SOAP 1.2 绑定。  
  
### 协定  
 `ServiceEndpoint` 实例的 <xref:System.ServiceModel.Description.ContractDescription> 实例映射到 `wsdl:portType`。  `ContractDescription` 实例描述给定协定的所有操作。  
  
|属性|WSDL 映射|  
|--------|-------------|  
|`Name`|协定的 `wsdl:portType`\/@name 值。|  
|`Namespace`|`wsdl:portType` 定义的 targetNamespace。|  
|`SessionMode`|协定的 `wsdl:portType`\/@msc:usingSession 值。  此属性是 WSDL 1.1 的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 扩展。|  
|`Operations`|协定的 `wsdl:operation` 定义。|  
  
### 操作  
 <xref:System.ServiceModel.Description.OperationDescription> 实例映射到 `wsdl:portType`\/`wsdl:operation`。  `OperationDescription` 包含用于描述操作消息的 `MessageDescription` 实例的集合。  
  
 如下两个操作行为广泛地参与 `OperationDescription` 到 WSDL 文档的映射方式：`DataContractSerializerOperationBehavior` 和 `XmlSerializerOperationBehavior`。  
  
|属性|WSDL 映射|  
|--------|-------------|  
|`Name`|操作的 `wsdl:portType`\/`wsdl:operation`\/@name 值。|  
|`ProtectionLevel`|附加到此操作的 `wsdl:binding/wsdl:operation` 消息的安全策略中的保护断言。|  
|`IsInitiating`|操作的 `wsdl:portType`\/`wsdl:operation`\/@msc:isInitiating 值。  此属性是 WSDL 1.1 的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 扩展。|  
|`IsTerminating`|操作的 `wsdl:portType`\/`wsdl:operation`\/@msc:isTerminating 值。  此属性是 WSDL 1.1 的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 扩展。|  
|`Messages`|操作的 `wsdl:portType`\/`wsdl:operation`\/`wsdl:input` 和 `wsdl:portType`\/`wsdl:operation`\/`wsdl:output` 消息。|  
|`Faults`|操作的 `wsdl:portType`\/`wsdl:operation`\/`wsdl:fault` 定义。|  
|`Behaviors`|`DataContractSerializerOperationBehavior` 和 `XmlSerializerOperationBehavior` 处理操作绑定和操作消息。|  
  
#### DataContractSerializerOperationBehavior  
 操作的 `DataContractSerializerOperationBehavior` 是用于为该操作导出 WSDL 消息和绑定的 `IWsdlExportExtension` 实现。  XML 架构类型是使用 `XsdDataContractExporter` 导出的。  `DataContractSerializerOperationBehavior` 还为该操作确定用途、样式和要使用的架构导出程序与导入程序。  
  
|属性|WSDL 映射|  
|--------|-------------|  
|`DataContractFormatAttribute`|此属性 \(attribute\) 的 `Style` 属性 \(property\) 映射到操作的 `wsdl:binding`\/`wsdl:operation`\/`soap:operation`\/@style 值。<br /><br /> `DataContractSerializerOperationBehavior` 仅支持 WSDL 中架构类型的文字用法。|  
  
#### XmlSerializerOperationBehavior  
 操作的 `XmlSerializerOperationBehavior` 是用于为该操作导出 WSDL 消息和绑定的 `IWsdlExportExtension` 实现。  XML 架构类型是使用 `XmlSchemaExporter` 导出的。  `XmlSerializerOperationBehavior` 还为该操作确定用途、样式和要使用的架构导出程序与导入程序。  
  
|属性|WSDL 映射|  
|--------|-------------|  
|`XmlSerializerFormatAttribute`|此属性 \(attribute\) 的 `Style` 属性 \(property\) 映射到操作的 `wsdl:binding`\/`wsdl:operation`\/`soap:operation`\/@style 值。<br /><br /> 此属性 \(attribute\) 的 `Use` 属性 \(property\) 映射到操作中所有消息的 `wsdl:binding`\/`wsdl:operation`\/`soap:operation`\/\*\/@use 值。|  
  
### 消息  
 `MessageDescription` 实例映射到由操作中的 `wsdl:portType`\/`wsdl:operation`\/`wsdl:input` 或 `wsdl:portType`\/`wsdl:operation`\/`wsdl:output` 消息引用的 `wsdl:message`。  `MessageDescription` 包含正文和标头。  
  
|属性|WSDL 映射|  
|--------|-------------|  
|`Action`|消息的 SOAP 或 WS\-Addressing 操作。<br /><br /> 请注意，使用操作字符串“\*”的操作不用 WSDL 表示。|  
|`Direction`|`MessageDirection.Input` 映射到 `wsdl:input`。<br /><br /> `MessageDirection.Output` 映射到 `wsdl:output`。|  
|`ProtectionLevel`|附加到此消息的 `wsdl:message` 定义的安全策略中的保护断言。|  
|`Body`|消息的消息正文。|  
|`Headers`|消息的标头。|  
|`ContractDescription.Name`, `OperationContract.Name`|导出时，用于派生 `wsdl:message`\/@name 值。|  
  
#### 消息正文  
 `MessageBodyDescription` 实例映射到消息正文的 `wsdl:message`\/`wsdl:part` 定义。  消息正文可以包装也可以裸露。  
  
|属性|WSDL 映射|  
|--------|-------------|  
|`WrapperName`|如果样式不是 RPC，则 `WrapperName` 将映射到由 `wsdl:message`\/`wsdl:part`（其 @name 设置为“parameters”）引用的元素名称。|  
|`WrapperNamespace`|如果样式不是 RPC，则 `WrapperNamespace` 将映射到 `wsdl:message`\/`wsdl:part`（其 @name 设置为“parameters”）的元素命名空间。|  
|`Parts`|此消息正文的消息部分。|  
|`ReturnValue`|如果存在包装元素（文档包装样式或 RPC 样式），则为包装元素的子元素，否则为消息中的第一个 `wsdl:message`\/`wsdl:part`。|  
  
#### 消息部分  
 `MessagePartDescription` 实例映射到 `wsdl:message`\/`wsdl:part` 和消息部分所指向的 XML 架构类型或元素。  
  
|属性|WSDL 映射|  
|--------|-------------|  
|`Name`|消息部分的 `wsd:message`\/`wsdl:part`\/@name 值和消息部分所指向的元素的名称。|  
|`Namespace`|消息部分所指向的元素的命名空间。|  
|`Index`|消息的 `wsdl:message`\/`wsdl:part` 的索引。|  
|`ProtectionLevel`|附加到此消息部分的 `wsdl:message` 定义的安全策略中的保护断言。  将策略参数化，使其指向特定的消息部分。|  
|`MessageType`|消息部分所指向的元素的 XML 架构类型。|  
  
#### 消息头  
 `MessageHeaderDescription` 实例是同时还映射到消息部分的 `soap:header` 绑定的消息部分。  
  
### 错误  
 `FaultDescription` 实例映射到 `wsdl:portType`\/`wsdl:operation`\/`wsdl:fault` 定义及其关联的 `wsdl:message` 定义。  将 `wsdl:message` 添加到与其关联的 WSDL 端口类型相同的目标命名空间。  `wsdl:message` 有一个名为“详细信息”的消息部分，该部分指向对应于 `FaultDescription` 实例的 `DefaultType` 属性值的 XML 架构元素。  
  
|属性|WSDL 映射|  
|--------|-------------|  
|`Name`|错误的 `wsdl:portType`\/`wsdl:operation`\/`wsdl:fault`\/@name 值。|  
|`Namespace`|错误详细消息部分所指向的 XML 架构元素的命名空间。|  
|`Action`|错误的 SOAP 或 WS\-Addressing 操作。|  
|`ProtectionLevel`|附加到此错误的 `wsdl:message` 定义的安全策略中的保护断言。|  
|`DetailType`|详细消息部分所指向的元素的 XML 架构类型。|  
|`Name, ContractDescription.Name, OperationDescription.Name,`|用于派生错误消息的 `wsdl:message`\/@name 值。|  
  
## 请参阅  
 <xref:System.ServiceModel.Description>