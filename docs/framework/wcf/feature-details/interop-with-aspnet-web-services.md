---
title: "与 ASP.NET Web 服务的互操作性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 622422f8-6651-442f-b8be-e654a4aabcac
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 与 ASP.NET Web 服务的互操作性
确保使用 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] Web 服务技术和 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务技术实现的服务符合 WS\-I Basic Profile 1.1 规范，便可以实现这两种 Web 服务之间的互操作性。通过使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 系统提供的绑定 <xref:System.ServiceModel.BasicHttpBinding>，符合 WS\-I Basic Profile 1.1 的 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] Web 服务可与 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端进行互操作。  
  
 使用 [!INCLUDE[vstecasplong](../../../../includes/vstecasplong-md.md)] 选项，即将 <xref:System.Web.Services.WebService> 和 <xref:System.Web.Services.WebMethodAttribute> 属性添加到接口而不是添加到类，并编写实现该接口的类，如下面的示例代码所示。  
  
```  
[WebService]  
public interface IEcho  
{  
    [WebMethod]  
    string Echo(string input);  
}  
  
public class Service : IEcho  
{  
  
   public string Echo(string input)  
   {  
        return input;  
    }  
}  
```  
  
 使用此选项是首选方法，因为具有 <xref:System.Web.Services.WebService> 属性的接口为服务所执行的操作构成了一个协定，在以不同方式实现该协定的各个类中，都可重用该协定。  
  
 避免使用 <xref:System.Web.Services.Protocols.SoapDocumentServiceAttribute> 特性依据 SOAP 消息正文元素的完全限定名将消息路由到方法，而应使用 `SOAPAction` 标头。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用 `SOAPAction` 标头来路由消息。  
  
 只要为 XML 显式定义了命名空间，则在默认情况下，<xref:System.Xml.Serialization.XmlSerializer> 将类型序列化为的 XML 与 <xref:System.Runtime.Serialization.DataContractSerializer> 将类型序列化为的 XML 在语义上完全相同。如果要定义用于 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]Web 服务的数据类型，并且预期采用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]，请执行以下操作：  
  
-   使用 .NET Framework 类而不是 XML 架构来定义该类型。  
  
-   仅将 <xref:System.SerializableAttribute> 和 <xref:System.Xml.Serialization.XmlRootAttribute> 添加到该类，使用后者显式定义类型的命名空间。不要添加 <xref:System.Xml.Serialization> 命名空间中的其他属性来控制如何将 .NET Framework 类转换为 XML。  
  
-   通过采用此方法，以后可将 .NET 类转换为附加了 <xref:System.Runtime.Serialization.DataContractAttribute> 和 <xref:System.Runtime.Serialization.DataMemberAttribute> 的数据协定，而无需为了传输而对类序列化成的 XML 进行重大更改。消息中由 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] Web 服务使用的类型可作为数据协定由 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序处理，这样做的好处之一是，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序的性能会更好。  
  
 避免使用 Internet 信息服务 \(IIS\) 提供的身份验证选项。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端不支持这些选项。如果必须保护服务，请使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供的选项，因为这些选项是可靠的，它们基于标准协议。  
  
## 由加载 ServiceModel HttpModule 而导致的性能影响  
 在 .NET Framework 3.0 中，WCF `HttpModule` 安装在根 Web.config 文件中，因此，每个 ASP.NET 应用程序都启用了 WCF。这可能会影响性能，因此，可以移除 Web.config 文件的 `ServiceModel`，如下面的示例所示。  
  
```  
<httpModules>  
    <remove name=”ServiceModel” />  
<httpModules/>  
  
```  
  
## 请参阅  
 [如何：配置 WCF 服务以便与 ASP.NET Web 服务客户端进行互操作](../../../../docs/framework/wcf/feature-details/config-wcf-service-with-aspnet-web-service.md)