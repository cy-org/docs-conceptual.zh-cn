---
title: "GUID_ManagedName 特性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "reference"
apiname: 
  - "GUID_ManagedName"
apilocation: 
  - "alink.dll"
apitype: "COM"
f1_keywords: 
  - "GUID_ManagedName"
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "GUID_ManagedName 特性"
ms.assetid: 11e18095-e444-47bc-aff6-b887ac5dc01e
caps.latest.revision: 6
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 6
---
# GUID_ManagedName 特性
定义指定的组件对象模型 \(COM\) 库的管理的命名空间名称的自定义接口属性。  
  
## 语法  
  
```  
[  
   custom(GUID_ManagedName, value)  
]  
```  
  
#### 参数  
 `value`  
 库管理的命名空间名称。  
  
## 定义  
 `GUID_ManagedName` 在定义 Cor.h，如下所示︰  
  
```  
// {0F21F359-AB84-41e8-9A78-36D110E6D2F9}  
EXTERN_GUID(GUID_ManagedName, 0xf21f359, 0xab84, 0x41e8, 0x9a, 0x78, 0x36, 0xd1, 0x10, 0xe6, 0xd2, 0xf9);  
```  
  
## 备注  
 自定义接口特性定义的类型库中的对象的元数据。  
  
 使用 <xref:System.Runtime.InteropServices.ComTypes.ITypeInfo2.GetCustData%2A?displayProperty=fullName> 或 <xref:System.Runtime.InteropServices.ComTypes.ITypeLib2.GetCustData%2A?displayProperty=fullName> 可从该属性检索托管的名称。  
  
 有关详细信息，请参阅 [Interface Attributes](../Topic/Interface%20Attributes.md) Visual c \+ \+ 参考文档。  
  
## 示例  
 下面的示例演示库定义使用 `GUID_ManagedName` 属性。  
  
```  
[  
   ...  
   custom(GUID_ManagedName, Microsoft.VisualStudio.CommandBars.dll")  
]  
library Microsoft_VisualStudio_CommandBars  
{  
   ...  
}  
```  
  
## 要求  
 **标头：**Cor.h