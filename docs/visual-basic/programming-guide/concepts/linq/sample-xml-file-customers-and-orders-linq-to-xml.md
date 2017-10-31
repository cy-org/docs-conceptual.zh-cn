---
title: "示例 XML 文件︰ 客户和订单 (LINQ to XML) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: ed319807-c432-4f8e-9694-dad4c7648310
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: be682b421173c7c226f17145db383aae1ebad154
ms.lasthandoff: 03/13/2017

---
# <a name="sample-xml-file-customers-and-orders-linq-to-xml"></a>示例 XML 文件：客户和订单 (LINQ to XML)
下面的 XML 文件用在 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 文档的很多示例中。 此文件包含客户和订单。  
  
 主题[示例 XSD 文件︰ 客户和订单](../../../../visual-basic/programming-guide/concepts/linq/sample-xsd-file-customers-and-orders.md)包含可用来验证此文档的 XSD。 它使用 XSD 的 `xs:key` 和 `xs:keyref` 功能，将 `CustomerID` 元素的 `Customer` 属性设置为键，并在每个 `CustomerID` 元素的 `Order` 元素和每个 `CustomerID` 元素的 `Customer` 属性之间建立关系。  
  
 为举例说明如何编写 LINQ 查询，从而利用此关系使用`Join`子句中，请参阅[如何︰ 联接两个集合 (LINQ to XML) (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/linq/how-to-join-two-collections-linq-to-xml.md)。  
  
## <a name="customersordersxml"></a>CustomersOrders.xml  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<Root>  
  <Customers>  
    <Customer CustomerID="GREAL">  
      <CompanyName>Great Lakes Food Market</CompanyName>  
      <ContactName>Howard Snyder</ContactName>  
      <ContactTitle>Marketing Manager</ContactTitle>  
      <Phone>(503) 555-7555</Phone>  
      <FullAddress>  
        <Address>2732 Baker Blvd.</Address>  
        <City>Eugene</City>  
        <Region>OR</Region>  
        <PostalCode>97403</PostalCode>  
        <Country>USA</Country>  
      </FullAddress>  
    </Customer>  
    <Customer CustomerID="HUNGC">  
      <CompanyName>Hungry Coyote Import Store</CompanyName>  
      <ContactName>Yoshi Latimer</ContactName>  
      <ContactTitle>Sales Representative</ContactTitle>  
      <Phone>(503) 555-6874</Phone>  
      <Fax>(503) 555-2376</Fax>  
      <FullAddress>  
        <Address>City Center Plaza 516 Main St.</Address>  
        <City>Elgin</City>  
        <Region>OR</Region>  
        <PostalCode>97827</PostalCode>  
        <Country>USA</Country>  
      </FullAddress>  
    </Customer>  
    <Customer CustomerID="LAZYK">  
      <CompanyName>Lazy K Kountry Store</CompanyName>  
      <ContactName>John Steel</ContactName>  
      <ContactTitle>Marketing Manager</ContactTitle>  
      <Phone>(509) 555-7969</Phone>  
      <Fax>(509) 555-6221</Fax>  
      <FullAddress>  
        <Address>12 Orchestra Terrace</Address>  
        <City>Walla Walla</City>  
        <Region>WA</Region>  
        <PostalCode>99362</PostalCode>  
        <Country>USA</Country>  
      </FullAddress>  
    </Customer>  
    <Customer CustomerID="LETSS">  
      <CompanyName>Let's Stop N Shop</CompanyName>  
      <ContactName>Jaime Yorres</ContactName>  
      <ContactTitle>Owner</ContactTitle>  
      <Phone>(415) 555-5938</Phone>  
      <FullAddress>  
        <Address>87 Polk St. Suite 5</Address>  
        <City>San Francisco</City>  
        <Region>CA</Region>  
        <PostalCode>94117</PostalCode>  
        <Country>USA</Country>  
      </FullAddress>  
    </Customer>  
  </Customers>  
  <Orders>  
    <Order>  
      <CustomerID>GREAL</CustomerID>  
      <EmployeeID>6</EmployeeID>  
      <OrderDate>1997-05-06T00:00:00</OrderDate>  
      <RequiredDate>1997-05-20T00:00:00</RequiredDate>  
      <ShipInfo ShippedDate="1997-05-09T00:00:00">  
        <ShipVia>2</ShipVia>  
        <Freight>3.35</Freight>  
        <ShipName>Great Lakes Food Market</ShipName>  
        <ShipAddress>2732 Baker Blvd.</ShipAddress>  
        <ShipCity>Eugene</ShipCity>  
        <ShipRegion>OR</ShipRegion>  
        <ShipPostalCode>97403</ShipPostalCode>  
        <ShipCountry>USA</ShipCountry>  
      </ShipInfo>  
    </Order>  
    <Order>  
      <CustomerID>GREAL</CustomerID>  
      <EmployeeID>8</EmployeeID>  
      <OrderDate>1997-07-04T00:00:00</OrderDate>  
      <RequiredDate>1997-08-01T00:00:00</RequiredDate>  
      <ShipInfo ShippedDate="1997-07-14T00:00:00">  
        <ShipVia>2</ShipVia>  
        <Freight>4.42</Freight>  
        <ShipName>Great Lakes Food Market</ShipName>  
        <ShipAddress>2732 Baker Blvd.</ShipAddress>  
        <ShipCity>Eugene</ShipCity>  
        <ShipRegion>OR</ShipRegion>  
        <ShipPostalCode>97403</ShipPostalCode>  
        <ShipCountry>USA</ShipCountry>  
      </ShipInfo>  
    </Order>  
    <Order>  
      <CustomerID>GREAL</CustomerID>  
      <EmployeeID>1</EmployeeID>  
      <OrderDate>1997-07-31T00:00:00</OrderDate>  
      <RequiredDate>1997-08-28T00:00:00</RequiredDate>  
      <ShipInfo ShippedDate="1997-08-05T00:00:00">  
        <ShipVia>2</ShipVia>  
        <Freight>116.53</Freight>  
        <ShipName>Great Lakes Food Market</ShipName>  
        <ShipAddress>2732 Baker Blvd.</ShipAddress>  
        <ShipCity>Eugene</ShipCity>  
        <ShipRegion>OR</ShipRegion>  
        <ShipPostalCode>97403</ShipPostalCode>  
        <ShipCountry>USA</ShipCountry>  
      </ShipInfo>  
    </Order>  
    <Order>  
      <CustomerID>GREAL</CustomerID>  
      <EmployeeID>4</EmployeeID>  
      <OrderDate>1997-07-31T00:00:00</OrderDate>  
      <RequiredDate>1997-08-28T00:00:00</RequiredDate>  
      <ShipInfo ShippedDate="1997-08-04T00:00:00">  
        <ShipVia>2</ShipVia>  
        <Freight>18.53</Freight>  
        <ShipName>Great Lakes Food Market</ShipName>  
        <ShipAddress>2732 Baker Blvd.</ShipAddress>  
        <ShipCity>Eugene</ShipCity>  
        <ShipRegion>OR</ShipRegion>  
        <ShipPostalCode>97403</ShipPostalCode>  
        <ShipCountry>USA</ShipCountry>  
      </ShipInfo>  
    </Order>  
    <Order>  
      <CustomerID>GREAL</CustomerID>  
      <EmployeeID>6</EmployeeID>  
      <OrderDate>1997-09-04T00:00:00</OrderDate>  
      <RequiredDate>1997-10-02T00:00:00</RequiredDate>  
      <ShipInfo ShippedDate="1997-09-10T00:00:00">  
        <ShipVia>1</ShipVia>  
        <Freight>57.15</Freight>  
        <ShipName>Great Lakes Food Market</ShipName>  
        <ShipAddress>2732 Baker Blvd.</ShipAddress>  
        <ShipCity>Eugene</ShipCity>  
        <ShipRegion>OR</ShipRegion>  
        <ShipPostalCode>97403</ShipPostalCode>  
        <ShipCountry>USA</ShipCountry>  
      </ShipInfo>  
    </Order>  
    <Order>  
      <CustomerID>GREAL</CustomerID>  
      <EmployeeID>3</EmployeeID>  
      <OrderDate>1997-09-25T00:00:00</OrderDate>  
      <RequiredDate>1997-10-23T00:00:00</RequiredDate>  
      <ShipInfo ShippedDate="1997-09-30T00:00:00">  
        <ShipVia>3</ShipVia>  
        <Freight>76.13</Freight>  
        <ShipName>Great Lakes Food Market</ShipName>  
        <ShipAddress>2732 Baker Blvd.</ShipAddress>  
        <ShipCity>Eugene</ShipCity>  
        <ShipRegion>OR</ShipRegion>  
        <ShipPostalCode>97403</ShipPostalCode>  
        <ShipCountry>USA</ShipCountry>  
      </ShipInfo>  
    </Order>  
    <Order>  
      <CustomerID>GREAL</CustomerID>  
      <EmployeeID>4</EmployeeID>  
      <OrderDate>1998-01-06T00:00:00</OrderDate>  
      <RequiredDate>1998-02-03T00:00:00</RequiredDate>  
      <ShipInfo ShippedDate="1998-02-04T00:00:00">  
        <ShipVia>2</ShipVia>  
        <Freight>719.78</Freight>  
        <ShipName>Great Lakes Food Market</ShipName>  
        <ShipAddress>2732 Baker Blvd.</ShipAddress>  
        <ShipCity>Eugene</ShipCity>  
        <ShipRegion>OR</ShipRegion>  
        <ShipPostalCode>97403</ShipPostalCode>  
        <ShipCountry>USA</ShipCountry>  
      </ShipInfo>  
    </Order>  
    <Order>  
      <CustomerID>GREAL</CustomerID>  
      <EmployeeID>3</EmployeeID>  
      <OrderDate>1998-03-09T00:00:00</OrderDate>  
      <RequiredDate>1998-04-06T00:00:00</RequiredDate>  
      <ShipInfo ShippedDate="1998-03-18T00:00:00">  
        <ShipVia>2</ShipVia>  
        <Freight>33.68</Freight>  
        <ShipName>Great Lakes Food Market</ShipName>  
        <ShipAddress>2732 Baker Blvd.</ShipAddress>  
        <ShipCity>Eugene</ShipCity>  
        <ShipRegion>OR</ShipRegion>  
        <ShipPostalCode>97403</ShipPostalCode>  
        <ShipCountry>USA</ShipCountry>  
      </ShipInfo>  
    </Order>  
    <Order>  
      <CustomerID>GREAL</CustomerID>  
      <EmployeeID>3</EmployeeID>  
      <OrderDate>1998-04-07T00:00:00</OrderDate>  
      <RequiredDate>1998-05-05T00:00:00</RequiredDate>  
      <ShipInfo ShippedDate="1998-04-15T00:00:00">  
        <ShipVia>2</ShipVia>  
        <Freight>25.19</Freight>  
        <ShipName>Great Lakes Food Market</ShipName>  
        <ShipAddress>2732 Baker Blvd.</ShipAddress>  
        <ShipCity>Eugene</ShipCity>  
        <ShipRegion>OR</ShipRegion>  
        <ShipPostalCode>97403</ShipPostalCode>  
        <ShipCountry>USA</ShipCountry>  
      </ShipInfo>  
    </Order>  
    <Order>  
      <CustomerID>GREAL</CustomerID>  
      <EmployeeID>4</EmployeeID>  
      <OrderDate>1998-04-22T00:00:00</OrderDate>  
      <RequiredDate>1998-05-20T00:00:00</RequiredDate>  
      <ShipInfo>  
        <ShipVia>3</ShipVia>  
        <Freight>18.84</Freight>  
        <ShipName>Great Lakes Food Market</ShipName>  
        <ShipAddress>2732 Baker Blvd.</ShipAddress>  
        <ShipCity>Eugene</ShipCity>  
        <ShipRegion>OR</ShipRegion>  
        <ShipPostalCode>97403</ShipPostalCode>  
        <ShipCountry>USA</ShipCountry>  
      </ShipInfo>  
    </Order>  
    <Order>  
      <CustomerID>GREAL</CustomerID>  
      <EmployeeID>4</EmployeeID>  
      <OrderDate>1998-04-30T00:00:00</OrderDate>  
      <RequiredDate>1998-06-11T00:00:00</RequiredDate>  
      <ShipInfo>  
        <ShipVia>3</ShipVia>  
        <Freight>14.01</Freight>  
        <ShipName>Great Lakes Food Market</ShipName>  
        <ShipAddress>2732 Baker Blvd.</ShipAddress>  
        <ShipCity>Eugene</ShipCity>  
        <ShipRegion>OR</ShipRegion>  
        <ShipPostalCode>97403</ShipPostalCode>  
        <ShipCountry>USA</ShipCountry>  
      </ShipInfo>  
    </Order>  
    <Order>  
      <CustomerID>HUNGC</CustomerID>  
      <EmployeeID>3</EmployeeID>  
      <OrderDate>1996-12-06T00:00:00</OrderDate>  
      <RequiredDate>1997-01-03T00:00:00</RequiredDate>  
      <ShipInfo ShippedDate="1996-12-09T00:00:00">  
        <ShipVia>2</ShipVia>  
        <Freight>20.12</Freight>  
        <ShipName>Hungry Coyote Import Store</ShipName>  
        <ShipAddress>City Center Plaza 516 Main St.</ShipAddress>  
        <ShipCity>Elgin</ShipCity>  
        <ShipRegion>OR</ShipRegion>  
        <ShipPostalCode>97827</ShipPostalCode>  
        <ShipCountry>USA</ShipCountry>  
      </ShipInfo>  
    </Order>  
    <Order>  
      <CustomerID>HUNGC</CustomerID>  
      <EmployeeID>1</EmployeeID>  
      <OrderDate>1996-12-25T00:00:00</OrderDate>  
      <RequiredDate>1997-01-22T00:00:00</RequiredDate>  
      <ShipInfo ShippedDate="1997-01-03T00:00:00">  
        <ShipVia>3</ShipVia>  
        <Freight>30.34</Freight>  
        <ShipName>Hungry Coyote Import Store</ShipName>  
        <ShipAddress>City Center Plaza 516 Main St.</ShipAddress>  
        <ShipCity>Elgin</ShipCity>  
        <ShipRegion>OR</ShipRegion>  
        <ShipPostalCode>97827</ShipPostalCode>  
        <ShipCountry>USA</ShipCountry>  
      </ShipInfo>  
    </Order>  
    <Order>  
      <CustomerID>HUNGC</CustomerID>  
      <EmployeeID>3</EmployeeID>  
      <OrderDate>1997-01-15T00:00:00</OrderDate>  
      <RequiredDate>1997-02-12T00:00:00</RequiredDate>  
      <ShipInfo ShippedDate="1997-01-24T00:00:00">  
        <ShipVia>1</ShipVia>  
        <Freight>0.2</Freight>  
        <ShipName>Hungry Coyote Import Store</ShipName>  
        <ShipAddress>City Center Plaza 516 Main St.</ShipAddress>  
        <ShipCity>Elgin</ShipCity>  
        <ShipRegion>OR</ShipRegion>  
        <ShipPostalCode>97827</ShipPostalCode>  
        <ShipCountry>USA</ShipCountry>  
      </ShipInfo>  
    </Order>  
    <Order>  
      <CustomerID>HUNGC</CustomerID>  
      <EmployeeID>4</EmployeeID>  
      <OrderDate>1997-07-16T00:00:00</OrderDate>  
      <RequiredDate>1997-08-13T00:00:00</RequiredDate>  
      <ShipInfo ShippedDate="1997-07-21T00:00:00">  
        <ShipVia>1</ShipVia>  
        <Freight>45.13</Freight>  
        <ShipName>Hungry Coyote Import Store</ShipName>  
        <ShipAddress>City Center Plaza 516 Main St.</ShipAddress>  
        <ShipCity>Elgin</ShipCity>  
        <ShipRegion>OR</ShipRegion>  
        <ShipPostalCode>97827</ShipPostalCode>  
        <ShipCountry>USA</ShipCountry>  
      </ShipInfo>  
    </Order>  
    <Order>  
      <CustomerID>HUNGC</CustomerID>  
      <EmployeeID>8</EmployeeID>  
      <OrderDate>1997-09-08T00:00:00</OrderDate>  
      <RequiredDate>1997-10-06T00:00:00</RequiredDate>  
      <ShipInfo ShippedDate="1997-10-15T00:00:00">  
        <ShipVia>1</ShipVia>  
        <Freight>111.29</Freight>  
        <ShipName>Hungry Coyote Import Store</ShipName>  
        <ShipAddress>City Center Plaza 516 Main St.</ShipAddress>  
        <ShipCity>Elgin</ShipCity>  
        <ShipRegion>OR</ShipRegion>  
        <ShipPostalCode>97827</ShipPostalCode>  
        <ShipCountry>USA</ShipCountry>  
      </ShipInfo>  
    </Order>  
    <Order>  
      <CustomerID>LAZYK</CustomerID>  
      <EmployeeID>1</EmployeeID>  
      <OrderDate>1997-03-21T00:00:00</OrderDate>  
      <RequiredDate>1997-04-18T00:00:00</RequiredDate>  
      <ShipInfo ShippedDate="1997-04-10T00:00:00">  
        <ShipVia>3</ShipVia>  
        <Freight>7.48</Freight>  
        <ShipName>Lazy K Kountry Store</ShipName>  
        <ShipAddress>12 Orchestra Terrace</ShipAddress>  
        <ShipCity>Walla Walla</ShipCity>  
        <ShipRegion>WA</ShipRegion>  
        <ShipPostalCode>99362</ShipPostalCode>  
        <ShipCountry>USA</ShipCountry>  
      </ShipInfo>  
    </Order>  
    <Order>  
      <CustomerID>LAZYK</CustomerID>  
      <EmployeeID>8</EmployeeID>  
      <OrderDate>1997-05-22T00:00:00</OrderDate>  
      <RequiredDate>1997-06-19T00:00:00</RequiredDate>  
      <ShipInfo ShippedDate="1997-06-26T00:00:00">  
        <ShipVia>2</ShipVia>  
        <Freight>11.92</Freight>  
        <ShipName>Lazy K Kountry Store</ShipName>  
        <ShipAddress>12 Orchestra Terrace</ShipAddress>  
        <ShipCity>Walla Walla</ShipCity>  
        <ShipRegion>WA</ShipRegion>  
        <ShipPostalCode>99362</ShipPostalCode>  
        <ShipCountry>USA</ShipCountry>  
      </ShipInfo>  
    </Order>  
    <Order>  
      <CustomerID>LETSS</CustomerID>  
      <EmployeeID>1</EmployeeID>  
      <OrderDate>1997-06-25T00:00:00</OrderDate>  
      <RequiredDate>1997-07-23T00:00:00</RequiredDate>  
      <ShipInfo ShippedDate="1997-07-04T00:00:00">  
        <ShipVia>2</ShipVia>  
        <Freight>13.73</Freight>  
        <ShipName>Let's Stop N Shop</ShipName>  
        <ShipAddress>87 Polk St. Suite 5</ShipAddress>  
        <ShipCity>San Francisco</ShipCity>  
        <ShipRegion>CA</ShipRegion>  
        <ShipPostalCode>94117</ShipPostalCode>  
        <ShipCountry>USA</ShipCountry>  
      </ShipInfo>  
    </Order>  
    <Order>  
      <CustomerID>LETSS</CustomerID>  
      <EmployeeID>8</EmployeeID>  
      <OrderDate>1997-10-27T00:00:00</OrderDate>  
      <RequiredDate>1997-11-24T00:00:00</RequiredDate>  
      <ShipInfo ShippedDate="1997-11-05T00:00:00">  
        <ShipVia>2</ShipVia>  
        <Freight>51.44</Freight>  
        <ShipName>Let's Stop N Shop</ShipName>  
        <ShipAddress>87 Polk St. Suite 5</ShipAddress>  
        <ShipCity>San Francisco</ShipCity>  
        <ShipRegion>CA</ShipRegion>  
        <ShipPostalCode>94117</ShipPostalCode>  
        <ShipCountry>USA</ShipCountry>  
      </ShipInfo>  
    </Order>  
    <Order>  
      <CustomerID>LETSS</CustomerID>  
      <EmployeeID>6</EmployeeID>  
      <OrderDate>1997-11-10T00:00:00</OrderDate>  
      <RequiredDate>1997-12-08T00:00:00</RequiredDate>  
      <ShipInfo ShippedDate="1997-11-21T00:00:00">  
        <ShipVia>2</ShipVia>  
        <Freight>45.97</Freight>  
        <ShipName>Let's Stop N Shop</ShipName>  
        <ShipAddress>87 Polk St. Suite 5</ShipAddress>  
        <ShipCity>San Francisco</ShipCity>  
        <ShipRegion>CA</ShipRegion>  
        <ShipPostalCode>94117</ShipPostalCode>  
        <ShipCountry>USA</ShipCountry>  
      </ShipInfo>  
    </Order>  
    <Order>  
      <CustomerID>LETSS</CustomerID>  
      <EmployeeID>4</EmployeeID>  
      <OrderDate>1998-02-12T00:00:00</OrderDate>  
      <RequiredDate>1998-03-12T00:00:00</RequiredDate>  
      <ShipInfo ShippedDate="1998-02-13T00:00:00">  
        <ShipVia>2</ShipVia>  
        <Freight>90.97</Freight>  
        <ShipName>Let's Stop N Shop</ShipName>  
        <ShipAddress>87 Polk St. Suite 5</ShipAddress>  
        <ShipCity>San Francisco</ShipCity>  
        <ShipRegion>CA</ShipRegion>  
        <ShipPostalCode>94117</ShipPostalCode>  
        <ShipCountry>USA</ShipCountry>  
      </ShipInfo>  
    </Order>  
  </Orders>  
</Root>  
```  
  
## <a name="see-also"></a>另请参阅  
 [示例 XML 文档 (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-documents-linq-to-xml.md)
