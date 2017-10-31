---
title: "示例 XML 文件：命名空间 2 中的多个采购订单"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 595024f2-374a-4615-acb5-64fa1600f377
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 22e79b3b56bf9963518cfbd93dcf4e1f2d2842e0
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="sample-xml-file-multiple-purchase-orders-in-a-namespace"></a>示例 XML 文件：命名空间中的多个采购订单
下面的 XML 文件用在 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 文档的很多示例中。 此文件包含多个采购订单。 该 XML 在某个命名空间中。  
  
## <a name="purchaseordersinnamespacexml"></a>PurchaseOrdersInNamespace.xml  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<aw:PurchaseOrders xmlns:aw="http://www.adventure-works.com">  
  <aw:PurchaseOrder aw:PurchaseOrderNumber="99503" aw:OrderDate="1999-10-20">  
    <aw:Address aw:Type="Shipping">  
      <aw:Name>Ellen Adams</aw:Name>  
      <aw:Street>123 Maple Street</aw:Street>  
      <aw:City>Mill Valley</aw:City>  
      <aw:State>CA</aw:State>  
      <aw:Zip>10999</aw:Zip>  
      <aw:Country>USA</aw:Country>  
    </aw:Address>  
    <aw:Address aw:Type="Billing">  
      <aw:Name>Tai Yee</aw:Name>  
      <aw:Street>8 Oak Avenue</aw:Street>  
      <aw:City>Old Town</aw:City>  
      <aw:State>PA</aw:State>  
      <aw:Zip>95819</aw:Zip>  
      <aw:Country>USA</aw:Country>  
    </aw:Address>  
    <aw:DeliveryNotes>Please leave packages in shed by driveway.</aw:DeliveryNotes>  
    <aw:Items>  
      <aw:Item aw:PartNumber="872-AA">  
        <aw:ProductName>Lawnmower</aw:ProductName>  
        <aw:Quantity>1</aw:Quantity>  
        <aw:USPrice>148.95</aw:USPrice>  
        <aw:Comment>Confirm this is electric</aw:Comment>  
      </aw:Item>  
      <aw:Item aw:PartNumber="926-AA">  
        <aw:ProductName>Baby Monitor</aw:ProductName>  
        <aw:Quantity>2</aw:Quantity>  
        <aw:USPrice>39.98</aw:USPrice>  
        <aw:ShipDate>1999-05-21</aw:ShipDate>  
      </aw:Item>  
    </aw:Items>  
  </aw:PurchaseOrder>  
  <aw:PurchaseOrder aw:PurchaseOrderNumber="99505" aw:OrderDate="1999-10-22">  
    <aw:Address aw:Type="Shipping">  
      <aw:Name>Cristian Osorio</aw:Name>  
      <aw:Street>456 Main Street</aw:Street>  
      <aw:City>Buffalo</aw:City>  
      <aw:State>NY</aw:State>  
      <aw:Zip>98112</aw:Zip>  
      <aw:Country>USA</aw:Country>  
    </aw:Address>  
    <aw:Address aw:Type="Billing">  
      <aw:Name>Cristian Osorio</aw:Name>  
      <aw:Street>456 Main Street</aw:Street>  
      <aw:City>Buffalo</aw:City>  
      <aw:State>NY</aw:State>  
      <aw:Zip>98112</aw:Zip>  
      <aw:Country>USA</aw:Country>  
    </aw:Address>  
    <aw:DeliveryNotes>Please notify me before shipping.</aw:DeliveryNotes>  
    <aw:Items>  
      <aw:Item aw:PartNumber="456-NM">  
        <aw:ProductName>Power Supply</aw:ProductName>  
        <aw:Quantity>1</aw:Quantity>  
        <aw:USPrice>45.99</aw:USPrice>  
      </aw:Item>  
    </aw:Items>  
  </aw:PurchaseOrder>  
  <aw:PurchaseOrder aw:PurchaseOrderNumber="99504" aw:OrderDate="1999-10-22">  
    <aw:Address aw:Type="Shipping">  
      <aw:Name>Jessica Arnold</aw:Name>  
      <aw:Street>4055 Madison Ave</aw:Street>  
      <aw:City>Seattle</aw:City>  
      <aw:State>WA</aw:State>  
      <aw:Zip>98112</aw:Zip>  
      <aw:Country>USA</aw:Country>  
    </aw:Address>  
    <aw:Address aw:Type="Billing">  
      <aw:Name>Jessica Arnold</aw:Name>  
      <aw:Street>4055 Madison Ave</aw:Street>  
      <aw:City>Buffalo</aw:City>  
      <aw:State>NY</aw:State>  
      <aw:Zip>98112</aw:Zip>  
      <aw:Country>USA</aw:Country>  
    </aw:Address>  
    <aw:Items>  
      <aw:Item aw:PartNumber="898-AZ">  
        <aw:ProductName>Computer Keyboard</aw:ProductName>  
        <aw:Quantity>1</aw:Quantity>  
        <aw:USPrice>29.99</aw:USPrice>  
      </aw:Item>  
      <aw:Item aw:PartNumber="898-AM">  
        <aw:ProductName>Wireless Mouse</aw:ProductName>  
        <aw:Quantity>1</aw:Quantity>  
        <aw:USPrice>14.99</aw:USPrice>  
      </aw:Item>  
    </aw:Items>  
  </aw:PurchaseOrder>  
</aw:PurchaseOrders>  
```  
  
## <a name="see-also"></a>请参阅  
 [示例 XML 文档 (LINQ to XML)](../../../../csharp/programming-guide/concepts/linq/sample-xml-documents-linq-to-xml.md)

