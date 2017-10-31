---
title: "将 keyref XML 架构 (XSD) 约束映射为数据集约束 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5b634fea-cc1e-4f6b-9454-10858105b1c8
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 将 keyref XML 架构 (XSD) 约束映射为数据集约束
**keyref** 元素用于在文档中的元素之间建立链接。  它类似于关系数据库中的外键关系。  如果架构指定了 **keyref** 元素，则在架构映射过程中，该元素将转换为 <xref:System.Data.DataSet> 的表列上的相应外键约束。  默认情况下，**keyref** 元素还会生成关系，并对关系指定 **ParentTable**、**ChildTable**、**ParentColumn** 和 **ChildColumn** 属性。  
  
 下表概括了可在 **keyref** 元素中指定的 **msdata** 属性。  
  
|特性名|描述|  
|---------|--------|  
|**msdata:ConstraintOnly**|如果对架构中的 **keyref** 元素指定了 **ConstraintOnly\="true"**，则将创建约束但不创建任何关系。  如果此属性未指定（或设置为 **False**），则将在 **DataSet** 中创建约束和关系。|  
|**msdata:ConstraintName**|如果指定了 **ConstraintName** 属性，则将其值用作约束的名称。  否则，架构中 **keyref** 元素的 **name** 属性将提供 **DataSet** 中的约束名称。|  
|**msdata:UpdateRule**|如果在架构的 **keyref** 元素中指定了 **UpdateRule** 属性，则将其值赋给 **DataSet** 中的 **UpdateRule** 约束属性。  否则，**UpdateRule** 属性将设置为 **Cascade**。|  
|**msdata:DeleteRule**|如果在架构的 **keyref** 元素中指定了 **DeleteRule** 属性，则将其值赋给 **DataSet** 中的 **DeleteRule** 约束属性。  否则，**DeleteRule** 属性将设置为 **Cascade**。|  
|**msdata:AcceptRejectRule**|如果在架构的 **keyref** 元素中指定了 **AcceptRejectRule** 属性，则将其值赋给 **DataSet** 中的 **AcceptRejectRule** 约束属性。  否则，**AcceptRejectRule** 属性将设置为 **None**。|  
  
 以下示例包含一个架构，在 **Order** 元素的 **OrderNumber** 子元素和 **OrderDetail** 元素的 **OrderNo** 子元素之间指定 **key** 和 **keyref** 关系。  
  
 在该示例中，**OrderDetail** 元素的 **OrderNumber** 子元素引用 **Order** 元素的 **OrderNo** 键子元素。  
  
```  
<xs:schema id="MyDataSet" xmlns=""   
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  
 <xs:element name="MyDataSet" msdata:IsDataSet="true">  
  <xs:complexType>  
    <xs:choice maxOccurs="unbounded">  
      <xs:element name="OrderDetail">  
       <xs:complexType>  
         <xs:sequence>  
           <xs:element name="OrderNo" type="xs:integer" />  
           <xs:element name="ItemNo" type="xs:string" />  
         </xs:sequence>  
       </xs:complexType>  
      </xs:element>  
      <xs:element name="Order">  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="OrderNumber" type="xs:integer" />  
            <xs:element name="EmpNumber" type="xs:integer" />  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:choice>  
  </xs:complexType>  
  
  <xs:key name="OrderNumberKey"  >  
    <xs:selector xpath=".//Order" />  
    <xs:field xpath="OrderNumber" />  
  </xs:key>  
  
  <xs:keyref name="OrderNoRef" refer="OrderNumberKey">  
    <xs:selector xpath=".//OrderDetail" />  
    <xs:field xpath="OrderNo" />  
  </xs:keyref>  
 </xs:element>  
</xs:schema>  
```  
  
 XML 架构定义语言 \(XSD\) 架构映射过程生成以下包含两个表的 **DataSet**：  
  
```  
OrderDetail(OrderNo, ItemNo) and  
Order(OrderNumber, EmpNumber)  
```  
  
 此外，该 **DataSet** 还定义以下约束：  
  
-   **Order** 表的唯一约束。  
  
    ```  
  
              Table: Order  
    Columns: OrderNumber   
    ConstraintName: OrderNumberKey  
    Type: UniqueConstraint  
    IsPrimaryKey: False  
    ```  
  
-   **Order** 表和 **OrderDetail** 表之间的关系。  由于这两个元素都不嵌套在架构中，所以 **Nested** 属性设置为 **False**。  
  
    ```  
  
              ParentTable: Order  
    ParentColumns: OrderNumber   
    ChildTable: OrderDetail  
    ChildColumns: OrderNo   
    ParentKeyConstraint: OrderNumberKey  
    ChildKeyConstraint: OrderNoRef  
    RelationName: OrderNoRef  
    Nested: False  
    ```  
  
-   **OrderDetail** 表的外键约束。  
  
    ```  
  
              ConstraintName: OrderNoRef  
    Type: ForeignKeyConstraint  
    Table: OrderDetail  
    Columns: OrderNo   
    RelatedTable: Order  
    RelatedColumns: OrderNumber   
    ```  
  
## 请参阅  
 [将 XML 架构 \(XSD\) 约束映射到 DataSet 约束](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)   
 [从 XML 架构 \(XSD\) 生成 DataSet 关系](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/generating-dataset-relations-from-xml-schema-xsd.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)