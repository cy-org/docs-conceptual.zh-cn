---
title: "将键 XML 架构 (XSD) 约束映射为数据集约束 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 22664196-f270-4ebc-a169-70e16a83dfa1
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 将键 XML 架构 (XSD) 约束映射为数据集约束
在架构中可以使用 **key** 元素对元素或属性指定键约束。  对其指定键约束的元素或属性必须在任何架构实例中都具有唯一值，并且不能具有空值。  
  
 除了对其定义键约束的列不能具有空值之外，键约束与唯一约束类似。  
  
 下表概括了可在 **key** 元素中指定的 **msdata** 属性。  
  
|特性名|描述|  
|---------|--------|  
|**msdata:ConstraintName**|如果指定了该属性，它的值将用作约束名。  否则，**name** 属性会提供约束名的值。|  
|**msdata:PrimaryKey**|如果存在 `PrimaryKey="true"`，**IsPrimaryKey** 约束属性将设置为 **true**，从而使其成为主键。  由于主键不能具有空值，所以 **AllowDBNull** 列属性将设置为 **false**。|  
  
 当转换指定了键约束的架构时，映射过程会在为约束中的每一列将 **AllowDBNull** 列属性设置为 **false** 的情况下在表上创建唯一约束。  除非对 **key** 元素指定 `msdata:PrimaryKey="true"`，否则唯一约束的 **IsPrimaryKey** 属性也将设置为 **false**。  它与 `PrimaryKey="true"` 的架构中的唯一约束相同。  
  
 在以下架构示例中，**key** 元素对 **CustomerID** 元素指定键约束。  
  
```  
<xs:schema id="cod"  
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  <xs:element name="Customers">  
    <xs:complexType>  
      <xs:sequence>  
        <xs:element name="CustomerID" type="xs:string" minOccurs="0" />  
        <xs:element name="CompanyName" type="xs:string" minOccurs="0" />  
       <xs:element name="Phone" type="xs:string" />  
     </xs:sequence>  
   </xs:complexType>  
 </xs:element>  
<xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
      <xs:element ref="Customers" />  
    </xs:choice>  
  </xs:complexType>  
   <xs:key  msdata:PrimaryKey="true"  
       msdata:ConstraintName="KeyCustID"  
          name="KeyConstCustomerID" >  
     <xs:selector xpath=".//Customers" />  
     <xs:field xpath="CustomerID" />  
    </xs:key>  
 </xs:element>  
</xs:schema>   
```  
  
 **key** 元素指定 **Customers** 元素的 **CustomerID** 子元素的值必须是唯一值，并且不能具有空值。  在转换 XML 架构定义语言 \(XSD\) 架构时，映射过程将创建下表：  
  
```  
Customers(CustomerID, CompanyName, Phone)  
```  
  
 XML 架构映射还会在 **CustomerID** 列上创建 **UniqueConstraint**，如以下 <xref:System.Data.DataSet> 所示。  （为简便起见，只显示相关属性。）  
  
```  
  
      DataSetName: MyDataSet  
TableName: customers  
  ColumnName: CustomerID  
      AllowDBNull: False  
      Unique: True  
  ConstraintName: KeyCustID  
      Table: customers  
      Columns: CustomerID   
      IsPrimaryKey: True  
```  
  
 在所生成的 **DataSet** 中，由于该架构在 **key** 元素中指定 `msdata:PrimaryKey="true"`，所以 **UniqueConstraint** 的 **IsPrimaryKey** 属性将设置为 **true**。  
  
 **DataSet** 中 **UniqueConstraint** 的 **ConstraintName** 属性值是在该架构的 **key** 元素中指定的 **msdata:ConstraintName** 属性值。  
  
## 请参阅  
 [将 XML 架构 \(XSD\) 约束映射到 DataSet 约束](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)   
 [从 XML 架构 \(XSD\) 生成 DataSet 关系](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/generating-dataset-relations-from-xml-schema-xsd.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)