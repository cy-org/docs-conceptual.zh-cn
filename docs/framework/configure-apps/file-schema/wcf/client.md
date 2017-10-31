---
title: "&lt;客户端&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.ServiceModel/client"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#client"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: bf0f7031-76c8-4e7e-a6c6-9ad9119134be
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# &lt;客户端&gt;
`client` 元素定义客户端可以连接的终结点的列表。  
  
## 语法  
  
```  
  
<system.serviceModel>  
    <client>  
        <endpoint>  
        </endpoint>  
                <metadata>  
        </metadata>  
    </client>  
</system.serviceModel>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
 无  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<endpoint（终结点）\>](../../../../../docs/framework/configure-apps/file-schema/wcf/endpoint-of-client.md)|包含终结点元素集合，这些元素指定此客户端可连接到的终结点。|  
|[\<元数据\>](../../../../../docs/framework/configure-apps/file-schema/wcf/metadata.md)|包含用于处理元数据的设置。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<system.serviceModel\>](../../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md)|所有 Windows Communication Foundation \(WCF\) 配置元素的根元素。|  
  
## 备注  
 `client` 节定义客户端可以连接的终结点的列表。  客户端节中列出的每个终结点都定义了它自己的绑定、行为和协定。  它由 `name` 和 `contract` 属性共同进行唯一标识。  客户端代码指定要连接到该客户端实现的服务终结点的 `name`。  如果省略 `name` 属性，则该终结点将作为其实现的协定的默认终结点。  
  
 此外，本节还指定了用于处理元数据的设置。  
  
## 示例  
  
```  
<client>  
    <endpoint address="/HelloWorld/"  
              bindingConfiguration="usingDefaults"  
              name="MyBinding"  
              binding="customBinding"  
              contract="HelloWorld">  
    <addressProperties actingAs="http://www.microsoft.com/TestActor"  
             identityData="BasicReadWrite" identityType="Spn" isAddressPrivate="false">  
    </endpoint>  
</client>  
```  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.ClientSection>   
 <xref:System.ServiceModel.Configuration.MetadataElement>   
 [WCF 客户端配置](../../../../../docs/framework/wcf/feature-details/client-configuration.md)   
 [客户端](../../../../../docs/framework/wcf/feature-details/clients.md)