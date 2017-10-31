---
title: "预期采用 Windows Communication Foundation：便于以后集成 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3028bba8-6355-4ee0-9ecd-c56e614cb474
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 预期采用 Windows Communication Foundation：便于以后集成
如果您现在使用 ASP.NET，并预期在以后使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]，则本主题所提供的指导可确保新的 ASP.NET Web 服务可与 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序一起正常工作。  
  
## 一般性建议  
 对任何新服务采用 ASP.NET 2.0。这样做将允许新服务访问新版本中的改进和增强。不过，这也允许在同一个应用程序中与 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 组件一起使用 ASP.NET 2.0 组件。  
  
## 协议  
 使用 ASP.NET 2.0 的新工具验证与 WS\-I 基本配置文件 1.1 的一致性：  
  
```  
[WebService(Namespace = "http://tempuri.org/")]  
[WebServiceBinding(  
     ConformsTo = WsiProfiles.BasicProfile1_1,  
     EmitConformanceClaims=true)]  
public interface IEcho  
  
```  
  
 通过使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 预定义的绑定 <xref:System.ServiceModel.BasicHttpBinding>，符合 WS\-I 基础配置文件 1.1 的 ASP.NET Web 服务将可与 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端互操作。  
  
## 服务开发  
 避免使用 <xref:System.Web.Services.Protocols.SoapDocumentServiceAttribute> 特性依据 SOAP 消息正文元素的完全限定名将消息路由到方法，而应使用 SOAPAction HTTP 标头。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用 SOAPAction HTTP 标头来路由消息。  
  
## 数据表示形式  
 只要为 XML 显式定义了命名空间，则在默认情况下，<xref:System.Xml.Serialization.XmlSerializer> 将类型序列化为的 XML 与 <xref:System.Runtime.Serialization.DataContractSerializer> 将类型序列化为的 XML 在语义上完全相同。如果预期在以后采用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]，则在定义用于 ASP.NET Web 服务的数据类型时，请执行以下操作：  
  
1.  使用 .NET Framework 类而不是 XML 架构来定义该类型。  
  
2.  仅将 <xref:System.SerializableAttribute> 和 <xref:System.Xml.Serialization.XmlRootAttribute> 添加到该类，使用后者显式定义类型的命名空间。不要添加 <xref:System.Xml.Serialization> 命名空间中的其他属性来控制如何将 .NET Framework 类转换为 XML。  
  
 通过采用此方法，以后可将 .NET 类转换为附加了 <xref:System.Runtime.Serialization.DataContractAttribute> 和 <xref:System.Runtime.Serialization.DataMemberAttribute> 的数据协定，而无需为了传输而对类序列化成的 XML 进行重大更改。消息中由 ASP.NET Web 服务使用的类型将能够作为数据协定由 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序处理，从而使 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序具有更高的性能，同时还会有其他方面的益处。  
  
## 安全性  
 避免使用 Internet 信息服务 \(IIS\) 提供的身份验证选项。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端不支持这些选项。如果必须保护某一服务，请使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供的选项，因为这些选项更丰富，并且基于标准协议。  
  
## 请参阅  
 [Windows Communication Foundation 使用展望：使未来迁移轻而易举](../../../../docs/framework/wcf/feature-details/anticipating-adopting-wcf-migration.md)