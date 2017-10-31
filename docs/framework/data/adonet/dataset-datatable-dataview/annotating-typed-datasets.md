---
title: "批注类型化数据集 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f82aaa62-321e-4c8a-b51b-9d1114700170
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# 批注类型化数据集
批注使您能够在不修改基础架构的情况下修改类型化 <xref:System.Data.DataSet> 中元素的名称。  如果修改基础架构中元素的名称，则会使类型化 **DataSet** 引用不存在于数据源中的对象，并且会丢失对存在于数据源中的对象的引用。  
  
 利用批注，您可以使用更有意义的名称来自定义类型化 **DataSet** 中对象的名称，从而使代码更易于阅读，类型化 **DataSet** 更易于为客户端使用，同时保持基础架构不变。  例如，**Northwind** 数据库中 **Customers** 表的以下架构元素会生成 **CustomersRow** 这一 **DataRow** 对象名称和一个名为 **Customers** 的 <xref:System.Data.DataRowCollection>。  
  
```  
<xs:element name="Customers">  
  <xs:complexType>  
    <xs:sequence>  
      <xs:element name="CustomerID" type="xs:string" minOccurs="0" />  
    </xs:sequence>  
  </xs:complexType>  
</xs:element>  
```  
  
 **DataRowCollection** 名称 **Customers** 在客户端代码中是有意义的，但 **DataRow** 名称 **CustomersRow** 则会导致误解，因为它是单个对象。  此外，在通常情况下，将不使用 **Row** 标识符来引用该对象，而仅将该对象当作 **Customer** 对象来引用。  解决方案是为架构添加批注并标识 **DataRow** 和 **DataRowCollection** 对象的新名称。  下面是上一架构的批注版本。  
  
```  
<xs:element name="Customers" codegen:typedName="Customer" codegen:typedPlural="Customers">  
  <xs:complexType>  
    <xs:sequence>  
      <xs:element name="CustomerID" type="xs:string" minOccurs="0" />  
    </xs:sequence>  
  </xs:complexType>  
</xs:element>  
```  
  
 将 **typedName** 的值指定为 **Customer** 将生成 **DataRow** 对象名称 **Customer**。  将 **typedPlural** 的值指定为 **Customers** 则会保留 **DataRowCollection** 名称 **Customers**。  
  
 下表显示可用的批注。  
  
|批注|描述|  
|--------|--------|  
|**typedName**|对象的名称。|  
|**typedPlural**|对象集合的名称。|  
|**typedParent**|对象在父关系中被引用时的名称。|  
|**typedChildren**|用于从子关系中返回对象的方法的名称。|  
|**nullValue**|基础值为 **DBNull** 时的值。  有关 **nullValue** 批注的信息，请参见下表。  默认为 **\_throw**。|  
  
 下表显示可为 **nullValue** 批注指定的值。  
  
|nullValue 值|描述|  
|-----------------|--------|  
|*替换值*|指定要返回的值。  所返回的值必须匹配该元素的类型。  例如，使用 `nullValue="0"` 可为空整数字段返回 0。|  
|**\_throw**|引发异常。  这是默认设置。|  
|**\_null**|如果遇到基元类型，则返回空引用或引发异常。|  
|**\_empty**|对于字符串返回 **String.Empty**；否则，返回从空构造函数创建的对象。  如果遇到基元类型，则引发异常。|  
  
 下表显示类型化 **DataSet** 中对象的默认值以及可用的批注。  
  
|对象\/方法\/事件|默认|批注|  
|----------------|--------|--------|  
|**DataTable**|TableNameDataTable|typedPlural|  
|**DataTable** 方法|NewTableNameRow<br /><br /> AddTableNameRow<br /><br /> DeleteTableNameRow|typedName|  
|**DataRowCollection**|TableName|typedPlural|  
|**DataRow**|TableNameRow|typedName|  
|**DataColumn**|DataTable.ColumnNameColumn<br /><br /> DataRow.ColumnName|typedName|  
|**属性**|PropertyName|typedName|  
|**Child** 访问器|GetChildTableNameRows|typedChildren|  
|**Parent** 访问器|TableNameRow|typedParent|  
|**DataSet** 事件|TableNameRowChangeEvent<br /><br /> TableNameRowChangeEventHandler|typedName|  
  
 若要使用类型化 **DataSet** 批注，则必须在 XML 架构定义语言 \(XSD\) 架构中包含以下 **xmlns** 引用。  （若要从数据库表创建 xsd，请参见 <xref:System.Data.DataSet.WriteXmlSchema%2A> 或[在 Visual Studio 中使用数据集](http://msdn.microsoft.com/library/8bw9ksd6.aspx)（可能为英文网页））。  
  
```  
xmlns:codegen="urn:schemas-microsoft-com:xml-msprop"  
```  
  
 下面是一个批注架构示例，该架构公开 **Northwind** 数据库的 **Customers** 表，并包含与 **Orders** 表的关系。  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<xs:schema id="CustomerDataSet"   
      xmlns:codegen="urn:schemas-microsoft-com:xml-msprop"  
      xmlns=""   
      xmlns:xs="http://www.w3.org/2001/XMLSchema"   
      xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  <xs:element name="CustomerDataSet" msdata:IsDataSet="true">  
    <xs:complexType>  
      <xs:choice maxOccurs="unbounded">  
        <xs:element name="Customers" codegen:typedName="Customer"  
codegen:typedPlural="Customers">  
          <xs:complexType>  
            <xs:sequence>  
              <xs:element name="CustomerID"  
codegen:typedName="CustomerID" type="xs:string" minOccurs="0" />  
              <xs:element name="CompanyName"  
codegen:typedName="CompanyName" type="xs:string" minOccurs="0" />  
              <xs:element name="Phone" codegen:typedName="Phone"  
codegen:nullValue="" type="xs:string" minOccurs="0" />  
            </xs:sequence>  
          </xs:complexType>  
        </xs:element>  
        <xs:element name="Orders" codegen:typedName="Order"  
codegen:typedPlural="Orders">  
          <xs:complexType>  
            <xs:sequence>  
              <xs:element name="OrderID" codegen:typedName="OrderID"  
type="xs:int" minOccurs="0" />  
              <xs:element name="CustomerID"  
codegen:typedName="CustomerID"  
                 codegen:nullValue="" type="xs:string" minOccurs="0" />  
              <xs:element name="EmployeeID"  
codegen:typedName="EmployeeID" codegen:nullValue="0"   
type="xs:int" minOccurs="0" />  
              <xs:element name="OrderAdapter"  
codegen:typedName="OrderAdapter"  
codegen:nullValue="1980-01-01T00:00:00"   
type="xs:dateTime" minOccurs="0" />  
            </xs:sequence>  
          </xs:complexType>  
        </xs:element>  
      </xs:choice>  
    </xs:complexType>  
    <xs:unique name="Constraint1">  
      <xs:selector xpath=".//Customers" />  
      <xs:field xpath="CustomerID" />  
    </xs:unique>  
    <xs:keyref name="CustOrders" refer="Constraint1"  
codegen:typedParent="Customer" codegen:typedChildren="GetOrders">  
      <xs:selector xpath=".//Orders" />  
      <xs:field xpath="CustomerID" />  
    </xs:keyref>  
  </xs:element>  
</xs:schema>  
```  
  
 以下代码示例使用从示例架构创建的强类型 **DataSet**。  它使用一个 <xref:System.Data.SqlClient.SqlDataAdapter> 填充 **Customers** 表，并使用另一个 <xref:System.Data.SqlClient.SqlDataAdapter> 填充 **Orders** 表。  强类型 **DataSet** 定义 **DataRelations**。  
  
```vb  
' Assumes a valid SqlConnection object named connection.  
Dim customerAdapter As SqlDataAdapter = New SqlDataAdapter( _  
    "SELECT CustomerID, CompanyName, Phone FROM Customers", &  
    connection)  
Dim orderAdapter As SqlDataAdapter = New SqlDataAdapter( _  
    "SELECT OrderID, CustomerID, EmployeeID, OrderAdapter FROM Orders", &  
    connection)  
  
' Populate a strongly typed DataSet.  
connection.Open()  
Dim customers As CustomerDataSet = New CustomerDataSet()  
customerAdapter.Fill(customers, "Customers")  
orderAdapter.Fill(customers, "Orders")  
connection.Close()  
  
' Add a strongly typed event.  
AddHandler customers.Customers.CustomerChanged, &  
    New CustomerDataSet.CustomerChangeEventHandler( _  
    AddressOf OnCustomerChanged)  
  
' Add a strongly typed DataRow.  
Dim newCustomer As CustomerDataSet.Customer = _  
    customers.Customers.NewCustomeromer()  
newCustomer.CustomerID = "NEW01"  
newCustomer.CompanyName = "My New Company"  
customers.Customers.AddCustomer(newCustomer)  
  
' Navigate the child relation.  
Dim customer As CustomerDataSet.Customer  
Dim order As CustomerDataSet.Order  
  
For Each customer In customers.Customers  
  Console.WriteLine(customer.CustomerID)  
  For Each order In customer.GetOrders()  
    Console.WriteLine(vbTab & order.OrderID)  
  Next  
Next  
  
Private Shared Sub OnCustomerChanged( _  
    sender As Object, e As CustomerDataSet.CustomerChangeEvent)  
  
End Sub  
  
```  
  
```csharp  
// Assumes a valid SqlConnection object named connection.  
SqlDataAdapter customerAdapter = new SqlDataAdapter(  
    "SELECT CustomerID, CompanyName, Phone FROM Customers",  
    connection);  
SqlDataAdapter orderAdapter = new SqlDataAdapter(  
    "SELECT OrderID, CustomerID, EmployeeID, OrderAdapter FROM Orders",   
    connection);  
  
// Populate a strongly typed DataSet.  
connection.Open();  
CustomerDataSet customers = new CustomerDataSet();  
customerAdapter.Fill(customers, "Customers");  
orderAdapter.Fill(customers, "Orders");  
connection.Close();  
  
// Add a strongly typed event.  
customers.Customers.CustomerChanged += new   
  CustomerDataSet.CustomerChangeEventHandler(OnCustomerChanged);  
  
// Add a strongly typed DataRow.  
CustomerDataSet.Customer newCustomer =   
    customers.Customers.NewCustomeromer();  
newCustomer.CustomerID = "NEW01";  
newCustomer.CompanyName = "My New Company";  
customers.Customers.AddCustomer(newCustomer);  
  
// Navigate the child relation.  
foreach(CustomerDataSet.Customer customer in customers.Customers)  
{  
  Console.WriteLine(customer.CustomerID);  
  foreach(CustomerDataSet.Order order in customer.GetOrders())  
    Console.WriteLine("\t" + order.OrderID);  
}  
  
protected static void OnCustomerChanged(object sender, CustomerDataSet.CustomerChangeEvent e)  
    {  
  
    }  
```  
  
## 请参阅  
 <xref:System.Data.DataColumnCollection>   
 <xref:System.Data.DataSet>   
 [类型化数据集](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/typed-datasets.md)   
 [DataSet、DataTable 和 DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)