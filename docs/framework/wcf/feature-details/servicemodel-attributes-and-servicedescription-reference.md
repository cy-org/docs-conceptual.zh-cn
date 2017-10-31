---
title: "ServiceModel 属性和 ServiceDescription 引用 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4ab86b17-eab9-4846-a881-0099f9a7cc64
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# ServiceModel 属性和 ServiceDescription 引用
*说明树* 是类型的层次结构 （从开始 <xref:System.ServiceModel.Description.ServiceDescription?displayProperty=fullName>类），一起描述服务的各个方面。 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]使用说明树形版本有效的服务运行时，发布网站\/网页服务描述语言 \(WSDL\)，XML架构定义语言 \(XSD\) 和客户端可以使用连接到和使用服务，并生成树形值描述的各种代码和配置文件表示服务的政策断言 （元数据）。  
  
 本主题介绍如何从服务协定获取与协定相关的属性，如何实现这些属性，以及如何将这些属性添加到说明树。在某些情况下，属性值会转换为行为属性，然后行为会插入到说明树中。如何将说明树值转换为元数据的更多信息，请参见 。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]如何将说明树值转换为元数据的更多信息，请参见 [ServiceDescription 和 WSDL 引用](../../../../docs/framework/wcf/feature-details/servicedescription-and-wsdl-reference.md)。  
  
## 将操作映射到说明树  
 在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序中，服务协定是由接口（或类）建模的，这些接口（或类）使用属性将接口（或类）及其方法标记为一组操作。<xref:System.ServiceModel.ServiceHost> 类打开后，所有服务协定和实现都会反映出来，并和配置信息一起合并到说明树中。  
  
 操作模型有两种类型：参数模型和消息协定模型。参数模型使用的托管方法不具有由 <xref:System.ServiceModel.MessageContractAttribute?displayProperty=fullName> 类标记的参数或返回值类型。在这种模型中，开发人员控制参数和返回值的序列化，但 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 会生成一些值，用于填充服务及其协定的说明树。  
  
 配置文件中指定的绑定直接加载到 <xref:System.ServiceModel.Description.ServiceEndpoint.Binding%2A?displayProperty=fullName> 属性中。  
  
|ServiceBehaviorAttribute 属性|受影响的说明树值|  
|---------------------------------|--------------|  
|Name|<xref:System.ServiceModel.Description.ServiceDescription.Name%2A>|  
|Namespace|<xref:System.ServiceModel.Description.ServiceDescription.Namespace%2A>|  
|ConfigurationName|<xref:System.ServiceModel.Description.ServiceDescription.ConfigurationName%2A>|  
|IgnoreExtensionDataObject|设置所有操作的 <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior.IgnoreExtensionDataObject%2A> 属性。|  
|MaxItemsInObjectGraph|设置所有操作的 <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior.MaxItemsInObjectGraph%2A> 属性。|  
  
|ServiceContractAttribute 属性|受影响的说明树值|  
|---------------------------------|--------------|  
|CallbackContract|添加到所有操作 <xref:System.ServiceModel.Description.OperationDescription.Messages%2A> 的 <xref:System.ServiceModel.Description.ContractDescription.CallbackContractType%2A>, <xref:System.ServiceModel.Description.MessageDescription>。|  
|ConfigurationName|<xref:System.ServiceModel.Description.ContractDescription.ConfigurationName%2A>|  
|ProtectionLevel|<xref:System.ServiceModel.Description.ContractDescription.ProtectionLevel%2A>和可能的子保护级别。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]保护级别层次结构的更多信息，请参见[了解保护级别](../../../../docs/framework/wcf/understanding-protection-level.md).|  
|SessionMode|<xref:System.ServiceModel.Description.ContractDescription.SessionMode%2A>|  
  
|ServiceKnownTypesAttribute 值|受影响的说明树值|  
|----------------------------------|--------------|  
|MethodName|<xref:System.ServiceModel.Description.OperationDescription.KnownTypes%2A>|  
  
|OperationContractAttribute 值|受影响的说明树值|  
|----------------------------------|--------------|  
|Action|用于输出消息或输入消息的 <xref:System.ServiceModel.Description.MessageDescription.Action%2A>，具体取决于协定\/回调协定。|  
|AsyncPattern|如果为 True，则执行 <xref:System.ServiceModel.Description.OperationDescription.BeginMethod%2A> 和 <xref:System.ServiceModel.Description.OperationDescription.EndMethod%2A>|  
|IsOneWay|映射到 <xref:System.ServiceModel.Description.OperationDescription.Messages%2A> 中的单个 <xref:System.ServiceModel.Description.MessageDescription>|  
|IsInitiating|<xref:System.ServiceModel.Description.OperationDescription.IsInitiating%2A>|  
|IsTerminating|<xref:System.ServiceModel.Description.OperationDescription.IsTerminating%2A>|  
|名称|<xref:System.ServiceModel.Description.OperationDescription.Name%2A>|  
|ProtectionLevel|<xref:System.ServiceModel.Description.OperationDescription.ProtectionLevel%2A>和可能的子保护级别。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]保护级别层次结构的更多信息，请参见[了解保护级别](../../../../docs/framework/wcf/understanding-protection-level.md).|  
|ReplyAction|用于输出消息或输入消息的 <xref:System.ServiceModel.Description.MessageDescription.Action%2A>，具体取决于协定\/回调协定。|  
  
|FaultContractAttribute 值|受影响的说明树值|  
|------------------------------|--------------|  
|操作|<xref:System.ServiceModel.Description.FaultDescription.Action%2A>，它取决于协定\/回调协定。|  
|DetailType|<xref:System.ServiceModel.Description.FaultDescription.DetailType%2A>|  
|Name|<xref:System.ServiceModel.Description.FaultDescription.Name%2A>|  
|Namespace|<xref:System.ServiceModel.Description.FaultDescription.Namespace%2A>|  
|ProtectionLevel|<xref:System.ServiceModel.Description.FaultDescription.ProtectionLevel%2A>|  
  
|DataContractFormatAttribute 值|受影响的说明树值|  
|-----------------------------------|--------------|  
|Use|<xref:System.ServiceModel.DataContractFormatAttribute.Style%2A> 值是在操作的 <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior> 上设置的。|  
  
|XmlSerializerFormatAttribute 值|受影响的说明树值|  
|------------------------------------|--------------|  
|Style|此 <xref:System.ServiceModel.XmlSerializerFormatAttribute> 属性是在操作的 <xref:System.ServiceModel.Description.XmlSerializerOperationBehavior> 上设置的。|  
|Use|<xref:System.ServiceModel.XmlSerializerFormatAttribute> 是在操作的 <xref:System.ServiceModel.Description.XmlSerializerOperationBehavior> 上设置的。|  
  
|TransactionFlowAttribute 值|受影响的说明树值|  
|--------------------------------|--------------|  
|TransactionFlowOption|<xref:System.ServiceModel.TransactionFlowAttribute> 作为操作行为添加到 <xref:System.ServiceModel.Description.OperationDescription.Behaviors%2A> 属性。|  
  
|MessageContractAttribute 值|受影响的说明树值|  
|--------------------------------|--------------|  
|ProtectionLevel|<xref:System.ServiceModel.Description.MessageDescription.ProtectionLevel%2A>|  
|WrapperName|<xref:System.ServiceModel.Description.MessageBodyDescription.WrapperName%2A>|  
|WrapperNamespace|<xref:System.ServiceModel.Description.MessageBodyDescription.WrapperNamespace%2A>|  
  
|MessageHeaderAttribute 值|受影响的说明树值|  
|------------------------------|--------------|  
|Actor|<xref:System.ServiceModel.Description.MessageHeaderDescription.Actor%2A> 中相应标头的<xref:System.ServiceModel.Description.MessageDescription.Headers%2A>|  
|MustUnderstand|<xref:System.ServiceModel.Description.MessageHeaderDescription.MustUnderstand%2A> 中相应标头的<xref:System.ServiceModel.Description.MessageDescription.Headers%2A>|  
|Name|<xref:System.ServiceModel.Description.MessagePartDescription.Name%2A> 中相应标头的<xref:System.ServiceModel.Description.MessageDescription.Headers%2A>|  
|Namespace|<xref:System.ServiceModel.Description.MessagePartDescription.Namespace%2A> 中相应标头的<xref:System.ServiceModel.Description.MessageDescription.Headers%2A>|  
|ProtectionLevel|<xref:System.ServiceModel.Description.MessagePartDescription.ProtectionLevel%2A> 中相应标头的<xref:System.ServiceModel.Description.MessageDescription.Headers%2A>|  
|Relay|<xref:System.ServiceModel.Description.MessageHeaderDescription.Relay%2A> 中相应标头的<xref:System.ServiceModel.Description.MessageDescription.Headers%2A>|  
  
|MessageBodyMemberAttribute 值|受影响的说明树值|  
|----------------------------------|--------------|  
|Name|<xref:System.ServiceModel.Description.MessagePartDescription.Name%2A> 中相应部分的<xref:System.ServiceModel.Description.MessageBodyDescription.Parts%2A>|  
|Namespace|<xref:System.ServiceModel.Description.MessagePartDescription.Namespace%2A> 中相应部分的<xref:System.ServiceModel.Description.MessageBodyDescription.Parts%2A>|  
|Order|<xref:System.ServiceModel.Description.MessagePartDescription.Index%2A> 中相应部分的<xref:System.ServiceModel.Description.MessageBodyDescription.Parts%2A>|  
|ProtectionLevel|<xref:System.ServiceModel.Description.MessagePartDescription.ProtectionLevel%2A> 中相应部分的<xref:System.ServiceModel.Description.MessageBodyDescription.Parts%2A>|  
  
|MessageHeaderArrayAttribute 值|受影响的说明树值|  
|-----------------------------------|--------------|  
|Actor|<xref:System.ServiceModel.Description.MessageHeaderDescription.Actor%2A>|  
|MustUnderstand|<xref:System.ServiceModel.Description.MessageHeaderDescription.MustUnderstand%2A>|  
|Name|<xref:System.ServiceModel.Description.MessagePartDescription.Name%2A>|  
|命名空间|<xref:System.ServiceModel.Description.MessagePartDescription.Namespace%2A>|  
|ProtectionLevel|<xref:System.ServiceModel.Description.MessagePartDescription.ProtectionLevel%2A>|  
|Relay|<xref:System.ServiceModel.Description.MessageHeaderDescription.Relay%2A>|  
  
|MessagePropertyAttribute 值|受影响的说明树值|  
|--------------------------------|--------------|  
|Name|<xref:System.ServiceModel.Description.MessagePartDescription.Name%2A>|  
  
|MessageParameterAttribute 值|受影响的说明树值|  
|---------------------------------|--------------|  
|Name|<xref:System.ServiceModel.Description.MessagePartDescription.name%2A> 中相应部分的<xref:System.ServiceModel.Description.MessageBodyDescription.Parts%2A>|  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]如何将说明树值转换为元数据的更多信息，请参见 [ServiceDescription 和 WSDL 引用](../../../../docs/framework/wcf/feature-details/servicedescription-and-wsdl-reference.md)。  
  
## 请参阅  
 [ServiceDescription 和 WSDL 引用](../../../../docs/framework/wcf/feature-details/servicedescription-and-wsdl-reference.md)