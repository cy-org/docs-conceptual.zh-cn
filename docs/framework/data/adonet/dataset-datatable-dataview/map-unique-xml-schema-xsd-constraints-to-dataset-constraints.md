---
title: "将唯一 XML 架构 (XSD) 约束映射为数据集约束 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 56da90bf-21d3-4d1a-8bb8-de908866b78d
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 将唯一 XML 架构 (XSD) 约束映射为数据集约束
在 XML 架构定义语言 \(XSD\) 架构中，**unique** 元素对元素或属性指定唯一约束。  在将 XML 架构转换为关系架构的过程中，对 XML 架构中的元素或属性指定的唯一约束将映射到所生成的相应 <xref:System.Data.DataSet> 中的 <xref:System.Data.DataTable> 中的唯一约束。  
  
 下表概括了可在 **unique** 元素中指定的 **msdata** 属性。  
  
|特性名|描述|  
|---------|--------|  
|**msdata:ConstraintName**|如果指定了该属性，它的值将用作约束名。  否则，**name** 属性会提供约束名的值。|  
|**msdata:PrimaryKey**|如果 `PrimaryKey="true"` 出现在 **unique** 元素中，则在将 **IsPrimaryKey** 属性设置为 **true** 的情况下创建唯一约束。|  
  
 以下示例显示一个 XML 架构，它使用 **unique** 元素来指定唯一约束。  
  
```  
<xs:schema id="SampleDataSet"   
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  <xs:element name="Customers">  
    <xs:complexType>  
      <xs:sequence>  
        <xs:element name="CustomerID" type="xs:integer"   
           minOccurs="0"/>  
        <xs:element name="CompanyName" type="xs:string"   
           minOccurs="0"/>  
       <xs:element name="Phone" type="xs:string" />  
     </xs:sequence>  
   </xs:complexType>  
 </xs:element>  
  
 <xs:element name="SampleDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
      <xs:element ref="Customers" />  
    </xs:choice>  
  </xs:complexType>  
   <xs:unique      
msdata:ConstraintName="UCustID"      
name="UniqueCustIDConstr" >        
<xs:selector xpath=".//Customers" />        
<xs:field xpath="CustomerID" />      
</xs:unique>  
</xs:element>  
</xs:schema>  
```  
  
 该架构中的 **unique** 元素指定对于文档实例中的所有 **Customers** 元素，**CustomerID** 子元素的值必须是唯一的。  当生成 **DataSet** 时，映射过程将读取此架构并生成下表：  
  
```  
Customers (CustomerID, CompanyName, Phone)  
```  
  
 映射过程还会在 **CustomerID** 列上创建一个唯一约束，如以下 **DataSet** 所示。  （为简便起见，只显示相关属性。）  
  
```  
  
      DataSetName: MyDataSet  
TableName: Customers  
  ColumnName: CustomerID  
      AllowDBNull: True  
      Unique: True  
  ConstraintName: UcustID  
      Type: UniqueConstraint  
      Table: Customers  
      Columns: CustomerID   
      IsPrimaryKey: False  
```  
  
 在所生成的 **DataSet** 中，对于唯一约束，**IsPrimaryKey** 属性设置为 **False**。  该列上的 **unique** 属性指示 **CustomerID** 列值必须是唯一的（但它们可以是空引用，这是该列的 **AllowDBNull** 属性所指定的）。  
  
 如果修改了该架构并将可选的 **msdata:PrimaryKey** 属性值设置为 **True**，将在表上创建唯一约束。  **AllowDBNull** 列属性设置为 **False**，而约束的 **IsPrimaryKey** 属性设置为 **True**，从而使 **CustomerID** 列成为主键列。  
  
 您可以对 XML 架构中元素或属性的组合指定唯一约束。  以下示例演示如何通过在架构中添加另一个 **xs:field** 元素，指定 **CustomerID** 和 **CompanyName** 值的组合必须对于任何实例中的所有 **Customers** 都是唯一的。  
  
```  
  
      <xs:unique     
         msdata:ConstraintName="SomeName"    
         name="UniqueCustIDConstr" >   
  <xs:selector xpath=".//Customers" />   
  <xs:field xpath="CustomerID" />   
  <xs:field xpath="CompanyName" />   
</xs:unique>  
```  
  
 以下是在所生成的 **DataSet** 中创建的约束。  
  
```  
ConstraintName: SomeName  
  Table: Customers  
  Columns: CustomerID CompanyName   
  IsPrimaryKey: False  
```  
  
## 请参阅  
 [将 XML 架构 \(XSD\) 约束映射到 DataSet 约束](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)   
 [从 XML 架构 \(XSD\) 生成 DataSet 关系](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/generating-dataset-relations-from-xml-schema-xsd.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)