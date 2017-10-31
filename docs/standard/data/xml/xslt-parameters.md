---
title: "XSLT 参数 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: fe60aaa0-ae43-4b1c-9be1-426af66ba757
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# XSLT 参数
使用 <xref:System.Xml.Xsl.XsltArgumentList.AddParam%2A> 方法将 XSLT 参数添加到 <xref:System.Xml.Xsl.XsltArgumentList>。  此时，限定名和命名空间 URI 与参数对象关联。  
  
### 使用 XSLT 参数  
  
1.  创建 <xref:System.Xml.Xsl.XsltArgumentList> 对象并使用 <xref:System.Xml.Xsl.XsltArgumentList.AddParam%2A> 方法添加参数。  
  
2.  从样式表调用参数。  
  
3.  将 <xref:System.Xml.Xsl.XsltArgumentList> 对象传递给 <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> 方法。  
  
## 参数类型  
 参数对象应对应于某种 W3C 类型。  下表显示了相应的 W3C 类型、等效的 Microsoft .NET 类（类型），以及 W3C 类型是 XPath 类型还是 XSLT 类型。  
  
|W3C 类型|等效的 .NET 类（类型）|XPath 还是 XSLT 类型|  
|------------|--------------------|----------------------|  
|`String`|<xref:System.String?displayProperty=fullName>|XPath|  
|`Boolean`|<xref:System.Boolean?displayProperty=fullName>|XPath|  
|`Number`|<xref:System.Double?displayProperty=fullName>|XPath|  
|`Result Tree Fragment`|<xref:System.Xml.XPath.XPathNavigator?displayProperty=fullName>|XSLT|  
|`Node*`|<xref:System.Xml.XPath.XPathNavigator?displayProperty=fullName>|XPath|  
|`Node Set`|<xref:System.Xml.XPath.XPathNodeIterator><br /><br /> **XPathNavigator\[\]**|XPath|  
  
 \*等效于包含单个节点的节点集。  
  
 如果参数对象不属于上述某个类，将根据下列规则进行转换。  公共语言运行库 \(CLR\) 数字类型转换为 <xref:System.Double>。  <xref:System.DateTime> 类型转换为 <xref:System.String>。  <xref:System.Xml.XPath.IXPathNavigable> 类型转换为 <xref:System.Xml.XPath.XPathNavigator>。  **XPathNavigator\[\]** 转换为 <xref:System.Xml.XPath.XPathNodeIterator>。  
  
 所有其他类型均将引发错误。  
  
## 示例  
 下面的示例使用 <xref:System.Xml.Xsl.XsltArgumentList.AddParam%2A> 方法创建一个参数来保存计算的折扣日期。  折扣日期计算为从订单日期算起的 20 天时间。  
  
 [!code-csharp[XSLT_Param#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XSLT_Param/CS/xsltparam.cs#1)]
 [!code-vb[XSLT_Param#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XSLT_Param/VB/xsltparam.vb#1)]  
  
### 输入  
  
##### order.xml  
 [!code-xml[XSLT_Param#2](../../../../samples/snippets/xml/VS_Snippets_Data/XSLT_Param/XML/order.xml#2)]  
  
##### discount.xsl  
 [!code-xml[XSLT_Param#3](../../../../samples/snippets/xml/VS_Snippets_Data/XSLT_Param/XML/discount.xsl#3)]  
  
### 输出  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<order>  
  <total>36.9</total>  
     15% discount if paid by: 2/4/2004 12:00:00 AM  
</order>  
```  
  
## 请参阅  
 [XSLT 转换](../../../../docs/standard/data/xml/xslt-transformations.md)