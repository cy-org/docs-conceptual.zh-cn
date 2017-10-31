---
title: "Windows Communication Foundation 使用展望：使未来迁移轻而易举 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f49664d9-e9e0-425c-a259-93f0a569d01b
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Windows Communication Foundation 使用展望：使未来迁移轻而易举
要确保将来将新的 ASP.NET 应用程序轻而易举地迁移到 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]，请遵循之前提出的建议以及下面的建议。  
  
## 协议  
 禁用 ASP.NET 2.0 对 SOAP 1.2 的支持：  
  
```  
<configuration>  
     <system.web>  
      <webServices >  
          <protocols>  
           <remove name="HttpSoap12"/>  
          </protocols>    
      </webServices>  
     </system.web>   
</configuration>  
  
```  
  
 建议进行此操作，因为 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 要求符合不同协议（如 SOAP 1.1 和 SOAP 1.2）的消息都可以通过使用不同的终结点进行传输。  如果将 ASP.NET 2.0 Web 服务配置为同时支持 SOAP 1.1 和 SOAP 1.2（该配置为默认配置），则不能将它向前迁移到原始地址处的单个 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 终结点，毫无疑问，该地址与所有 ASP.NET Web 服务的现有客户端相兼容。  另外，选择 SOAP 1.2 而非 SOAP 1.1 将更加严格地限制服务的客户。  
  
## 服务开发  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 允许您通过将 <xref:System.ServiceModel.ServiceContractAttribute> 应用到接口或类来定义服务协定。  建议将此属性应用于接口而不是类，因为这样可以为可由任意数量的类以不同方式实现的协定创建一个定义。  ASP.NET 2.0 支持将 <xref:System.Web.Services.WebService> 属性应用到接口和类的选项。  但是，如前所述，ASP.NET 2.0 中存在缺陷，如果将 <xref:System.Web.Services.WebService> 属性应用到接口而不是类，则此属性的 Namespace 参数将不起任何作用。  由于通常建议您使用 <xref:System.Web.Services.WebService> 属性的 Namespace 参数来修改服务的命名空间的默认值 \(http:\/\/tempuri.org\)，因此您应该通过将 <xref:System.ServiceModel.ServiceContractAttribute> 属性应用到接口或类来继续定义 ASP.NET Web 服务。  
  
-   在定义那些接口的方法中尽量少使用代码。  允许它们将其工作委托给其他类。  随后，新的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务类型也可以将其大量的工作委托给那些类。  
  
-   使用 <xref:System.Web.Services.WebMethodAttribute> 的 `MessageName` 参数为服务的操作提供显式名称。  
  
    ```  
    [WebMethod(MessageName="ExplicitName")]  
    string Echo(string input);  
    ```  
  
     此操作很重要，因为 ASP.NET 中的操作的默认名称与 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供的默认名称不同。  通过提供显式名称，可以避免依赖默认名称。  
  
-   不要使用多态方法来实现 ASP.NET Web 服务操作，因为 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 并不支持使用多态方法实现操作。  
  
-   使用 <xref:System.Web.Services.Protocols.SoapDocumentMethodAttribute> 为 SOAPAction HTTP 标头提供显式值，HTTP 请求将通过此标头路由到方法。  
  
    ```  
    [WebMethod]  
    [SoapDocumentMethod(RequestElementName="ExplicitAction")]  
    string Echo(string input);  
    ```  
  
     采用此方法可摆脱对 ASP.NET 所使用的 SOAPAction 默认值的依赖，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 也是如此。  
  
-   避免使用 SOAP 扩展。  如果需要使用 SOAP 扩展，则要确定使用扩展的目的是否为 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 已提供的功能。  如果情况确实如此，则重新考虑该选择以立即放弃采用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]。  
  
## 状态管理  
 避免必须在服务中保持状态。  不仅是因为保持状态会降低应用程序的可伸缩性，而且 ASP.NET 和 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的状态管理机制截然不同（虽然在 ASP.NET 兼容模式中 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 确实支持 ASP.NET 机制）。  
  
## 异常处理  
 在设计服务发送和接收的数据类型的结构时，请同时设计表示异常的不同类型的结构，这些异常可能发生在人们希望传送到客户端的服务中。  
  
```  
[Serializable]  
[XmlRoot(  
     Namespace="ExplicitNamespace", IsNullable=true)]  
    public partial class AnticipatedException {  
  
     private string anticipatedExceptionInformationField;  
  
     public string AnticipatedExceptionInformation {  
      get {  
          return this.anticipatedExceptionInformationField;  
          }  
      set {  
          this.anticipatedExceptionInformationField = value;  
          }  
     }  
}  
```  
  
 使这些类能够将其自身序列化为 XML：  
  
```  
public XmlNode ToXML()  
{  
     XmlSerializer serializer = new XmlSerializer(  
      typeof(AnticipatedException));  
     MemoryStream memoryStream = new MemoryStream();  
     XmlTextWriter writer = new XmlTextWriter(  
     memoryStream, UnicodeEncoding.UTF8);  
     serializer.Serialize(writer, this);  
     XmlDocument document = new XmlDocument();  
     document.LoadXml(new string(  
     UnicodeEncoding.UTF8.GetChars(  
     memoryStream.GetBuffer())).Trim());  
    return document.DocumentElement;  
}  
```  
  
 然后，可使用这些类为显式引发的 <xref:System.Web.Services.Protocols.SoapException> 实例提供详细信息：  
  
```  
AnctipatedException exception = new AnticipatedException();  
exception.AnticipatedExceptionInformation = "…";  
throw new SoapException(  
     "Fault occurred",  
     SoapException.ClientFaultCode,  
     Context.Request.Url.AbsoluteUri,  
     exception.ToXML());  
  
```  
  
 可随时重用这些异常类并结合 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] <xref:System.ServiceModel.FaultException%601> 类来引发新的 `FaultException<AnticipatedException>(anticipatedException);`  
  
## 安全性  
 下面是一些安全建议。  
  
-   避免使用 ASP.NET 2.0 配置文件，因为在将服务迁移到 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 时使用它们将限制对 ASP.NET 集成模式的使用。  
  
-   避免使用 ACL 来控制对服务的访问，因为 ASP.NET Web 服务支持使用 Internet 信息服务 \(IIS\) 的 ACL，而 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 却不支持（因为 ASP.NET Web 服务依赖 IIS 进行承载，而 WCF 则无需在 IIS 中进行承载）。  
  
-   请务必考虑使用 ASP.NET 2.0 角色提供程序来授权对服务资源的访问。  
  
## 请参阅  
 [预期采用 Windows Communication Foundation：便于以后集成](../../../../docs/framework/wcf/feature-details/anticipating-adopting-the-wcf-easing-future-integration.md)