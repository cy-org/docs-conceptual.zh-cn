---
title: "从 XML 架构 (XSD) 生成 DataSet 关系 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1c9a1413-c0d2-4447-88ba-9a2b0cbc0aa8
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 从 XML 架构 (XSD) 生成 DataSet 关系
在 <xref:System.Data.DataSet> 中，可通过创建父子关系来形成两个或更多个列之间的关联。  在 XML 架构定义语言 \(XSD\) 架构中，表示 **DataSet** 关系的方法有三种：  
  
-   指定嵌套复杂类型。  
  
-   使用 **msdata:Relationship** 批注。  
  
-   指定不带 **msdata:ConstraintOnly** 批注的 **xs:keyref**。  
  
## 嵌套的复杂类型  
 架构中的嵌套复杂类型定义指示元素的父子关系。  以下 XML 架构片断显示 **OrderDetail** 是 **Order** 元素的子元素。  
  
```  
<xs:element name="Order">  
  <xs:complexType>  
     <xs:sequence>          
       <xs:element name="OrderDetail" />  
           <xs:complexType>               
           </xs:complexType>  
     </xs:sequence>  
  </xs:complexType>  
</xs:element>  
```  
  
 XML 架构映射进程在 **DataSet** 中创建对应于架构中嵌套复杂类型的表。  它还会另外创建一些列，以用作所生成的表的父子列。  请注意，这些父子列指定关系，这与指定主键\/外键约束不同。  
  
## msdata:Relationship 批注  
 **msdata:Relationship** 批注用于在不嵌套的架构中的元素之间显式指定父子关系。  以下示例显示 **Relationship** 元素的结构。  
  
```  
  
  <msdata:Relationship name="CustOrderRelationship"    
msdata:parent=""    
msdata:child=""    
msdata:parentkey=""    
msdata:childkey="" />  
```  
  
 **msdata:Relationship** 批注的属性标识父子关系中所涉及的元素，以及该关系中所涉及的 **parentkey** 和 **childkey** 元素和属性。  映射进程使用该信息在 **DataSet** 中生成表并在这些表之间创建主键\/外键关系。  
  
 例如，以下架构片断指定位于同一级别（不嵌套）的 **Order** 和 **OrderDetail** 元素。  该架构指定了一个 **msdata:Relationship** 批注，此批注指定这两个元素之间的父子关系。  在这种情况下，必须使用 **msdata:Relationship** 批注来指定显式关系。  
  
```  
 <xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
        <xs:element name="OrderDetail">  
          <xs:complexType>  
  
          </xs:complexType>  
       </xs:element>  
       <xs:element name="Order">  
          <xs:complexType>  
  
          </xs:complexType>  
       </xs:element>  
    </xs:choice>  
  </xs:complexType>  
</xs:element>  
   <xs:annotation>  
     <xs:appinfo>  
       <msdata:Relationship name="OrdOrdDetailRelation"  
          msdata:parent="Order"  
          msdata:child="OrderDetail"   
          msdata:parentkey="OrderNumber"  
          msdata:childkey="OrderNo"/>  
     </xs:appinfo>  
  </xs:annotation>  
  
```  
  
 映射进程使用 **Relationship** 元素在 **Order** 表中的 **OrderNumber** 列和 **DataSet** 的 **OrderDetail** 表中的 **OrderNo** 列之间创建父子关系。  映射进程仅指定关系；与关系数据库中的主键\/外键约束不同，它并不会自动为这些列中的值指定任何约束。  
  
### 本节内容  
 [映射嵌套架构元素之间的隐式关系](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/map-implicit-relations-between-nested-schema-elements.md)  
 描述当在 XML 架构中遇到嵌套元素时在 **DataSet** 中隐式创建的约束和关系。  
  
 [映射对嵌套元素指定的关系](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/map-relations-specified-for-nested-elements.md)  
 描述如何在 **DataSet** 中为 XML 架构中的嵌套元素显式地设置关系。  
  
 [指定非嵌套元素之间的关系](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/specify-relations-between-elements-with-no-nesting.md)  
 描述如何在 **DataSet** 中创建不嵌套的 XML 架构元素之间的关系。  
  
### 相关章节  
 [从 XML 架构 \(XSD\) 派生数据集关系结构](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/deriving-dataset-relational-structure-from-xml-schema-xsd.md)  
 描述从 XML 架构定义语言 \(XSD\) 架构创建的 **DataSet** 的关系结构（即架构）。  
  
 [将 XML 架构 \(XSD\) 约束映射到 DataSet 约束](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)  
 描述用于在 **DataSet** 中创建唯一约束和外键约束的 XML 架构元素。  
  
## 请参阅  
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)