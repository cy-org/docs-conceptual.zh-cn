---
title: "如何：作为 Atom 和 RSS 公开源 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fe374932-67f5-487d-9325-f868812b92e4
caps.latest.revision: 23
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 23
---
# 如何：作为 Atom 和 RSS 公开源
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 允许您创建公开联合源的服务。  本主题讨论如何使用 Atom 1.0 和 RSS 2.0 创建公开联合源的联合服务。  此服务公开一个可以返回任一联合格式的终结点。  为了简单起见，本示例中使用的服务为自承载服务。  在生产环境中，此类型的服务将承载在 IIS 或 WAS 下。  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]不同 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 承载选项的更多信息，请参见 [承载](../../../../docs/framework/wcf/feature-details/hosting.md)。  
  
### 创建基本联合服务  
  
1.  使用通过 <xref:System.ServiceModel.Web.WebGetAttribute> 属性标记的接口定义服务协定。  作为联合源公开的每个操作都会返回一个 <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter> 对象。  请注意 <xref:System.ServiceModel.Web.WebGetAttribute> 的参数。  `UriTemplate` 指定用于调用此服务操作的 URL。  此参数的字符串包含文本和一个用大括号括住的变量 \({*format*}\)。  此变量与服务操作的 `format` 参数相对应。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.UriTemplate>.  `BodyStyle` 会影响此服务操作所发送和接收的消息的写入方式。  <xref:System.ServiceModel.Web.WebMessageBodyStyle> 指定不使用基础结构定义的 XML 元素包装发送到和接收自此服务操作的数据。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.Web.WebMessageBodyStyle>.  
  
     [!code-csharp[htAtomRss#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/htatomrss/cs/program.cs#0)]
     [!code-vb[htAtomRss#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htatomrss/vb/program.vb#0)]  
  
    > [!NOTE]
    >  在此接口中使用 <xref:System.ServiceModel.ServiceKnownTypeAttribute> 以指定服务操作返回的类型。  
  
2.  实现服务协定。  
  
     [!code-csharp[htAtomRss#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/htatomrss/cs/program.cs#1)]
     [!code-vb[htAtomRss#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htatomrss/vb/program.vb#1)]  
  
3.  创建 <xref:System.ServiceModel.Syndication.SyndicationFeed> 对象，并添加作者、类别和说明。  
  
     [!code-csharp[htAtomRss#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/htatomrss/cs/program.cs#2)]
     [!code-vb[htAtomRss#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htatomrss/vb/program.vb#2)]  
  
4.  创建若干 <xref:System.ServiceModel.Syndication.SyndicationItem> 对象。  
  
     [!code-csharp[htAtomRss#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/htatomrss/cs/program.cs#3)]
     [!code-vb[htAtomRss#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htatomrss/vb/program.vb#3)]  
  
5.  向源中添加 <xref:System.ServiceModel.Syndication.SyndicationItem> 对象。  
  
     [!code-csharp[htAtomRss#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/htatomrss/cs/program.cs#4)]
     [!code-vb[htAtomRss#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htatomrss/vb/program.vb#4)]  
  
6.  使用格式参数返回请求的格式。  
  
     [!code-csharp[htAtomRss#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/htatomrss/cs/program.cs#5)]
     [!code-vb[htAtomRss#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htatomrss/vb/program.vb#5)]  
  
### 承载服务  
  
1.  创建 <xref:System.ServiceModel.Web.WebServiceHost> 对象。  除非在代码或配置中指定了一个终结点，<xref:System.ServiceModel.Web.WebServiceHost> 类会自动在服务的基地址添加终结点。  在此示例中，不指定任何终结点，因此公开默认终结点。  
  
     [!code-csharp[htAtomRss#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/htatomrss/cs/program.cs#6)]
     [!code-vb[htAtomRss#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htatomrss/vb/program.vb#6)]  
  
2.  打开服务主机，从服务加载源，显示源，然后等待用户按 Enter。  
  
     [!code-csharp[htAtomRss#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/htatomrss/cs/program.cs#8)]
     [!code-vb[htAtomRss#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htatomrss/vb/program.vb#8)]  
  
### 使用 HTTP GET 调用 GetBlog  
  
1.  打开 Internet Explorer，键入下面的 URL，然后按 ENTER。  http:\/\/localhost:8000\/BlogService\/GetBlog  
  
     URL 包含服务的基址 \(http:\/\/localhost:8000\/BlogService\)、终结点的相对地址，以及要调用的服务操作。  
  
### 从代码中调用 GetBlog\(\)  
  
1.  使用基址和调用的方法创建 <xref:System.Xml.XmlReader>。  
  
     [!code-csharp[htAtomRss#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/htatomrss/cs/snippets.cs#9)]
     [!code-vb[htAtomRss#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htatomrss/vb/snippets.vb#9)]  
  
2.  调用静态 <xref:System.ServiceModel.Syndication.SyndicationFeed.Load%28System.Xml.XmlReader%29> 方法，同时传入刚刚创建的 <xref:System.Xml.XmlReader>。  
  
     [!code-csharp[htAtomRss#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/htatomrss/cs/snippets.cs#10)]
     [!code-vb[htAtomRss#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htatomrss/vb/snippets.vb#10)]  
  
     这将调用服务操作，并用从服务操作返回的格式化程序填充新的 <xref:System.ServiceModel.Syndication.SyndicationFeed>。  
  
3.  访问源对象。  
  
     [!code-csharp[htAtomRss#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/htatomrss/cs/snippets.cs#11)]
     [!code-vb[htAtomRss#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htatomrss/vb/snippets.vb#11)]  
  
## 示例  
 下面列出了此示例的完整代码。  
  
 [!code-csharp[htAtomRss#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/htatomrss/cs/program.cs#12)]  
  
## 编译代码  
 编译前面的代码时，请引用 System.ServiceModel.dll 和 System.ServiceModel.Web.dll。  
  
## 请参阅  
 <xref:System.ServiceModel.WebHttpBinding>   
 <xref:System.ServiceModel.Web.WebGetAttribute>