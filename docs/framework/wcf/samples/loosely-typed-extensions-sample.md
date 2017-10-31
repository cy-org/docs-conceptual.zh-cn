---
title: "松散类型化扩展示例 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 56ce265b-8163-4b85-98e7-7692a12c4357
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# 松散类型化扩展示例
联合对象模型为处理扩展数据（在联合源的 XML 表示形式中存在，但是未由 <xref:System.ServiceModel.Syndication.SyndicationFeed> 和 <xref:System.ServiceModel.Syndication.SyndicationItem> 等类显式公开的信息）提供了丰富的支持。此示例演示用于使用扩展数据的基本技术。  
  
 此示例使用 <xref:System.ServiceModel.Syndication.SyndicationFeed> 类作为示例。但是，此示例中演示的模式可用于支持扩展数据的所有 Syndication 类。  
  
 <xref:System.ServiceModel.Syndication.SyndicationFeed>  
  
 <xref:System.ServiceModel.Syndication.SyndicationItem>  
  
 <xref:System.ServiceModel.Syndication.SyndicationCategory>  
  
 <xref:System.ServiceModel.Syndication.SyndicationPerson>  
  
 <xref:System.ServiceModel.Syndication.SyndicationLink>  
  
## 示例 XML  
 下面的 XML 文档将在此实例中使用，可供您参考。  
  
```  
<?xml version="1.0" encoding="IBM437"?>  
<feed myAttribute="someValue" xmlns="http://www.w3.org/2005/Atom">  
  <title type="text"></title>  
  <id>uuid:8f60c7b3-a3c0-4de7-a642-2165d77ce3c1;id=1</id>  
  <updated>2007-09-07T22:15:34Z</updated>  
  <simpleString xmlns="">hello, world!</simpleString>  
  <simpleString xmlns="">another simple string</simpleString>  
  <DataContractExtension xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.d  
atacontract.org/2004/07/Microsoft.Syndication.Samples">  
    <Key>X</Key>  
    <Value>4</Value>  
  </DataContractExtension>  
  <XmlSerializerExtension xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://ww  
w.w3.org/2001/XMLSchema" xmlns="">  
    <Key>Y</Key>  
    <Value>8</Value>  
  </XmlSerializerExtension>  
  <xElementExtension xmlns="">  
    <Key attr1="someValue">Z</Key>  
    <Value attr1="someValue">15</Value>  
  </xElementExtension>  
</feed>  
  
```  
  
 此文档包含扩展数据的以下部分：  
  
-   `<feed>` 元素的 `myAttribute` 属性。  
  
-   `<simpleString>` 元素。  
  
-   `<DataContractExtension>` 元素。  
  
-   `<XmlSerializerExtension>` 元素。  
  
-   `<xElementExtension>` 元素。  
  
## 编写扩展数据  
 属性扩展是通过向 <xref:System.ServiceModel.Syndication.SyndicationFeed.AttributeExtensions%2A> 集合添加条目来创建的，如下面的示例代码所示。  
  
```  
//Attribute extensions are stored in a dictionary indexed by   
// XmlQualifiedName  
feed.AttributeExtensions.Add(new XmlQualifiedName("myAttribute", ""), "someValue");  
  
```  
  
 元素扩展是通过向 <xref:System.ServiceModel.Syndication.SyndicationFeed.ElementExtensions%2A> 集合添加条目来创建的。这些扩展可以是基本值（如字符串）、.NET Framework 对象的 XML 序列化或者是手动编码的 XML 节点。  
  
 下面的示例代码创建一个名为 `simpleString` 的扩展元素。  
  
```  
feed.ElementExtensions.Add("simpleString", "", "hello, world!");  
  
```  
  
 此元素的 XML 命名空间是空命名空间（“”），它的值是包含字符串“hello, world\!”的文本节点。  
  
 如果要创建包含许多嵌套元素的复杂元素扩展，一种方法是使用 .NET Framework API 进行序列化（均支持 <xref:System.Runtime.Serialization.DataContractSerializer> 和 <xref:System.Xml.Serialization.XmlSerializer>），如下面的示例所示。  
  
```  
feed.ElementExtensions.Add( new DataContractExtension() { Key = "X", Value = 4 } );  
feed.ElementExtensions.Add( new XmlSerializerExtension { Key = "Y", Value = 8 }, new XmlSerializer( typeof( XmlSerializerExtension ) ) );  
  
```  
  
 在本示例中，`DataContractExtension` 和 `XmlSerializerExtension` 属于自定义类型，它们是为与序列化程序协同使用而编写的。  
  
 <xref:System.ServiceModel.Syndication.SyndicationElementExtensionCollection> 类还可以用来从 <xref:System.Xml.XmlReader> 实例创建元素扩展。这允许与 XML 处理 API（如 <xref:System.Xml.Linq.XElement>）进行简单集成，如下面的示例代码所示。  
  
```  
feed.ElementExtensions.Add(new XElement("xElementExtension",  
        new XElement("Key", new XAttribute("attr1", "someValue"), "Z"),  
        new XElement("Value", new XAttribute("attr1", "someValue"),   
        "15")).CreateReader());  
  
```  
  
## 读取扩展数据  
 属性扩展的值可以通过在 <xref:System.ServiceModel.Syndication.SyndicationFeed.AttributeExtensions%2A> 集合中按 <xref:System.Xml.XmlQualifiedName> 查找属性来获取，如下面的示例代码所示。  
  
```  
Console.WriteLine( feed.AttributeExtensions[ new XmlQualifiedName( "myAttribute", "" )]);  
  
```  
  
 元素扩展是借助于 `ReadElementExtensions<T>` 方法来访问的。  
  
```  
foreach( string s in feed2.ElementExtensions.ReadElementExtensions<string>("simpleString", ""))  
{  
    Console.WriteLine(s);  
}  
  
foreach (DataContractExtension dce in feed2.ElementExtensions.ReadElementExtensions<DataContractExtension>("DataContractExtension",  
"http://schemas.datacontract.org/2004/07/SyndicationExtensions"))  
{  
    Console.WriteLine(dce.ToString());  
}  
  
foreach (XmlSerializerExtension xse in feed2.ElementExtensions.ReadElementExtensions<XmlSerializerExtension>("XmlSerializerExtension", "", new XmlSerializer(typeof(XmlSerializerExtension))))  
{  
    Console.WriteLine(xse.ToString());  
}  
  
```  
  
 还可以通过使用 <xref:System.ServiceModel.Syndication.SyndicationElementExtension.GetReader> 方法来在个别元素扩展上获取 `XmlReader`。  
  
```  
  
foreach (SyndicationElementExtension extension in feed2.ElementExtensions.Where<SyndicationElementExtension>(x => x.OuterName == "xElementExtension"))  
{  
    XNode xelement = XElement.ReadFrom(extension.GetReader());  
    Console.WriteLine(xelement.ToString());  
}  
  
```  
  
#### 设置、生成和运行示例  
  
1.  请确保已经执行了 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  若要生成 C\# 或 Visual Basic .NET 版本的解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
3.  若要用单机配置或跨计算机配置来运行示例，请按照[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)中的说明进行操作。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Syndication\LooselyTypedExtensions`  
  
## 请参阅  
 [强类型扩展](../../../../docs/framework/wcf/samples/strongly-typed-extensions-sample.md)   
 [WCF 联合](../../../../docs/framework/wcf/feature-details/wcf-syndication.md)