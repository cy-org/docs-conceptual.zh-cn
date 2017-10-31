---
title: "从 XML 架构 (XSD) 派生数据集关系结构 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8f6cd04d-6197-4bc4-9096-8c51c7e4acae
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 从 XML 架构 (XSD) 派生数据集关系结构
本节将概述如何从 XML 架构定义语言 \(XSD\) 架构文档生成 <xref:System.Data.DataSet> 的关系架构。  通常，对于一个架构元素的每个 **complexType** 子元素，都将在 **DataSet** 中生成一个表。  表结构取决于复杂类型的定义。  表是在 **DataSet** 中为架构中的顶级元素而创建的。  但是，当 **complexType** 元素嵌套在另一个 **complexType** 元素中时，只会为顶级 **complexType** 元素创建表，在这种情况下，嵌套的 **complexType** 元素将映射到 **DataSet** 中的 <xref:System.Data.DataTable>。  
  
 有关 XSD 的更多信息，请参见万维网联合会 \(W3C\) 的“XML Schema Part 0: Primer Recommendation”（XML 架构第 0 部分：入门建议）、“XML Schema Part 1: Structures Recommendation”（XML 架构第 1 部分：结构建议）和“XML Schema Part 2: Datatypes Recommendation”（XML 架构第 2 部分：数据类型建议），网址为 [http:\/\/www.w3.org\/](http://www.w3.org/TR/)。  
  
 以下示例演示一个 XML 架构，其中 `customers` 为 `MyDataSet` 元素（一个 **DataSet** 元素）的子元素。  
  
```  
<xs:schema id="SomeID"   
            xmlns=""   
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
   <xs:element name="MyDataSet" msdata:IsDataSet="true">  
     <xs:complexType>  
       <xs:choice maxOccurs="unbounded">  
         <xs:element name="customers" >   
           <xs:complexType >  
             <xs:sequence>  
               <xs:element name="CustomerID" type="xs:integer"   
                            minOccurs="0" />  
               <xs:element name="CompanyName" type="xs:string"   
                            minOccurs="0" />  
               <xs:element name="Phone" type="xs:string" />  
             </xs:sequence>  
           </xs:complexType>  
          </xs:element>  
       </xs:choice>  
     </xs:complexType>  
   </xs:element>  
 </xs:schema>  
```  
  
 在上例中，`customers` 元素为复杂类型元素。  因此，将对复杂类型定义进行分析，而映射过程会创建下表。  
  
```  
Customers (CustomerID , CompanyName, Phone)  
```  
  
 该表中各列的数据类型是从所指定的相应元素或属性的 XML 架构类型派生的。  
  
> [!NOTE]
>  如果 `customers` 元素属于简单 XML 架构数据类型（如 **integer**），则不生成任何表。  表仅为属于复杂类型的顶级元素而创建。  
  
 在以下 XML 架构中，**Schema** 元素具有两个子元素：`InStateCustomers` 和 `OutOfStateCustomers`。  
  
```  
<xs:schema id="SomeID"   
            xmlns=""   
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
   <xs:element name="InStateCustomers" type="customerType" />  
   <xs:element name="OutOfStateCustomers" type="customerType" />  
    <xs:complexType name="customerType" >  
  
     </xs:complexType>  
  
   <xs:element name="MyDataSet" msdata:IsDataSet="true">  
     <xs:complexType>  
       <xs:choice maxOccurs="unbounded">  
         <xs:element ref="customers" />  
       </xs:choice>  
     </xs:complexType>  
   </xs:element>  
 </xs:schema>  
```  
  
 `InStateCustomers` 和 `OutOfStateCustomers` 两个子元素都是复杂类型元素 \(`customerType`\)。  因此，映射过程会在 **DataSet** 中生成以下两个完全相同的表。  
  
```  
InStateCustomers (CustomerID , CompanyName, Phone)  
OutOfStateCustomers (CustomerID , CompanyName, Phone)  
```  
  
## 本节内容  
 [将 XML 架构 \(XSD\) 约束映射到 DataSet 约束](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)  
 描述用于在 **DataSet** 中创建唯一约束和外键约束的 XML 架构元素。  
  
 [从 XML 架构 \(XSD\) 生成 DataSet 关系](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/generating-dataset-relations-from-xml-schema-xsd.md)  
 描述用于在 **DataSet** 中各表列间创建关系的 XML 架构元素。  
  
 [XML 架构约束和关系](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/xml-schema-constraints-and-relationships.md)  
 描述当使用 XML 架构元素在 **DataSet** 中创建约束时如何隐式地创建关系。  
  
## 相关章节  
 [在 DataSet 中使用 XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)  
 描述如何以 XML 数据形式来加载和保持 **DataSet** 中的关系结构和数据。  
  
## 请参阅  
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)