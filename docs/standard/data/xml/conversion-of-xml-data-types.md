---
title: "XML 数据类型的转换 | Microsoft Docs"
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
ms.assetid: a2aa99ba-8239-4818-9281-f1d72ee40bde
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# XML 数据类型的转换
**XmlConvert** 类中的多数方法用于在字符串和强类型化格式之间转换数据。  这些方法与区域设置无关。  这意味着它们在执行转换时不考虑任何区域设置。  
  
## 将字符串作为类型读取  
 下面的示例读取一个字符串，并将其转换为 **DateTime** 类型。  
  
 给定以下 XML 输入：  
  
 **输入**  
  
```  
<Element>2001-02-27T11:13:23</Element>  
```  
  
 下面的代码将此字符串转换为 **DateTime** 格式：  
  
```vb  
reader.ReadStartElement()  
Dim vDateTime As DateTime = XmlConvert.ToDateTime(reader.ReadString())  
Console.WriteLine(vDateTime)  
  
```  
  
```csharp  
reader.ReadStartElement();  
DateTime vDateTime = XmlConvert.ToDateTime(reader.ReadString());  
Console.WriteLine(vDateTime);  
```  
  
## 将字符串作为类型写入  
 下面的示例读取一个 **Int32**，并将其转换为字符串。  
  
 给定以下 XML 输入：  
  
 **输入**  
  
```  
<TestInt32>-2147483648</TestInt32>  
```  
  
 下面的代码将此 **Int32** 转换为 **String**：  
  
```vb  
Dim vInt32 As Int32 = -2147483648  
writer.WriteElementString("TestInt32", XmlConvert.ToString(vInt32))  
  
```  
  
```csharp  
Int32 vInt32=-2147483648;  
writer.WriteElementString("TestInt32",XmlConvert.ToString(vInt32));  
```  
  
## 请参阅  
 [将字符串转换为 .NET Framework 数据类型](../../../../docs/standard/data/xml/converting-strings-to-dotnet-data-types.md)   
 [将 .NET Framework 类型转换为字符串](../../../../docs/standard/data/xml/converting-dotnet-types-to-strings.md)