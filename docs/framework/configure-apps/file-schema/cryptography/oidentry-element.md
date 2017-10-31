---
title: "&lt;oidEntry&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/mscorlib/cryptographySettings/oidMap/oidEntry"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#oidEntry"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<oidEntry> 元素"
  - "oidEntry 元素"
ms.assetid: 22fb88b0-bf27-489c-9ca0-e65950ac136c
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 11
---
# &lt;oidEntry&gt; 元素
将 ASN.1 对象标识符 \(OID\) 映射到友好名称。  
  
## 语法  
  
```  
<oidEntry OID="object identifier number" name="friendly name" />  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|**OID**|必需的特性。<br /><br /> 指定与类实现的算法相对应的 ASN.1 OID。|  
|**name**|必需的特性。<br /><br /> 为[\<nameEntry\>](../../../../../docs/framework/configure-apps/file-schema/cryptography/nameentry-element.md)标签中**name** 属性指定值。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`cryptographySettings`|包含密码设置。|  
|`mscorlib`|包含 `cryptographySettings` 元素。|  
|`oidMap`|包含到类的 ASN.1 对象标识符 \(OID\) 映射。|  
  
## 备注  
 ASN.1 对象标识符以某些加密格式标识算法。  将对象标识符映射到要标识的算法的友好名称。  有关对象标识符的更多信息，请参见 MSDN Library。  
  
## 示例  
 下面的示例演示了如何使用**\<oidEntry\>**元素来为RIPEMD\-160哈希算法映射一个对象标识符映射到哈希算法的实现。  
  
```  
<configuration>  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
            <cryptoClasses>  
               <cryptoClass   MyCrypto="MyCryptoClass, MyAssembly  
                  Culture=neutral, PublicKeyToken=a5d015c7d5a0b012,  
                  Version=1.0.0.0"/>  
            </cryptoClasses>  
            <nameEntry name="RIPEMD-160" class="MyCrypto"/>  
         </cryptoNameMapping>  
         <oidMap>  
            <oidEntry OID="1.3.36.3.2.1"   name="MyCryptoClass"/>  
         </oidMap>  
      </cryptographySettings>  
   </mscorlib>  
</configuration>  
```  
  
## 请参阅  
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [密码设置架构](../../../../../docs/framework/configure-apps/file-schema/cryptography/index.md)   
 [加密服务](../../../../../docs/standard/security/cryptographic-services.md)   
 [配置加密类](../../../../../docs/framework/configure-apps/configure-cryptography-classes.md)   
 [将对象标识符映射到加密算法](../../../../../docs/framework/configure-apps/map-object-identifiers-to-cryptography-algorithms.md)