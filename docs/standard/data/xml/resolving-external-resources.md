---
title: "解析外部资源 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: ad3fa320-4b8f-4e5c-b549-01157591007a
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 4
---
# 解析外部资源
**XmlDocument** 的 **XmlResolver** 属性由 **XmlDocument** 类用来定位没有内联的 XML 数据中的资源，如外部文档类型定义 \(DTD\)、实体和架构。  这些项可以位于网络或本地驱动器上，并通过统一资源标识符 \(URI\) 进行标识。  这使得 **XmlDocument** 可以解析文档中存在的 **EntityReference** 节点并根据外部 DTD 或架构验证文档的有效性。  
  
## 完全受信任的 XmlDocument  
 **XmlResolver** 属性影响 **XmlDocument.Load** 方法的功能。  下表显示了当 **XmlDocument** 完全受信任时 **XmlDocument.XmlResolver** 属性的作用。  之后的表显示了当 Load 的输入是 **TextReader**、**String**、**Stream** 或 **URI** 时的 **XmlDocument.Load** 方法。  如果从 **XmlReader** 中加载 **XmlDocument**，则此表不适用于 **Load** 方法。  
  
|XmlResolver 属性|函数|备注|  
|--------------------|--------|--------|  
|该属性设置为一个以前创建的而且用户已设置属性的 **XmlResolver** 类。|**XmlDocument** 使用给定的 **XmlResolver** 来解析文件名、解析对外部资源（如 DTD、实体和架构）的引用。<br /><br /> **XmlResolver** 还用来解析在 **XmlDocument** 中添加或编辑节点时需要的外部资源。|指定给 **XmlDocument** 的 **XmlResolver** 是每当需要定位和解析外部资源时使用的解析器。|  
|此属性设置为 **null**（在 Microsoft Visual Basic .NET 中为 **Nothing**）。|不支持需要外部资源的功能，如定位外部架构或 DTD。  也不能解析外部实体，而且也不支持执行编辑功能（如插入需要解析的实体节点）。|**XmlDocument** 匿名加载文件，而且不尝试解析任何其他资源。|  
|不设置此属性，而是将其保留为默认状态。|**XmlDocument** 解析文件名称和定位外部 DTD、实体和架构时，将实例化并使用带有 NULL 凭据的 **XmlUrlResolver**，**null** 凭据在编辑节点时使用。||  
  
 下表显示当 **Load** 的输入是一个 **XmlReader** 而且 **XmlDocument** 完全受信任时的 **XmlDocument.Load** 方法。  
  
|XmlResolver 属性|函数|备注|  
|--------------------|--------|--------|  
|**XmlDocument** 使用的 **XmlResolver** 类与 **XmlReader** 使用的是同一个类。|**XmlDocument** 使用分配给 **XmlReader** 的 **XmlResolver**。<br /><br /> 无论 **XmlDocument** 的信任级别如何，都无法设置 **XmlDocument.Resolver** 属性，因为它是从 **XmlReader** 获取 **XmlResolver**。  不能试图通过设置 **XmlDocument** 的 **XmlResolver** 属性来重写 **XmlReader** 的 **XmlResolver** 设置。|**XmlReader** 可以是 **XmlTextReader**、**XmlValidatingReader** 或自己编写的读取器。  如果使用的读取器支持实体解析，则解析外部实体。  如果传递的读取器不支持实体引用，那么就不解析实体引用。|  
  
## 不完全受信任的 XmlDocument  
 下表显示了当对象不完全受信任时 **XmlDocument.XmlResolver** 属性的作用。  当 Load 的输入是 **TextReader**、**String**、**Stream** 或 **URI** 时，此表适用于 **XmlDocument.Load** 方法。  如果从 **XmlReader** 中加载 **XmlDocument**，则此表不适用于 **Load** 方法。  
  
|XmlResolver 属性|函数|备注|  
|--------------------|--------|--------|  
|在不完全受信任的方案中，**XmlResolver** 属性只能设置为 null。|**XmlDocument** 解析文件名称和定位外部 DTD、实体和架构时，将实例化并使用带有 **null** 凭据的 **XmlUrlResolver**，**null** 凭据在编辑节点时使用。|此行为与不设置 **XmlResolver** 而是保持为默认状态时的行为完全相同。<br /><br /> **XmlDocument** 对所有操作使用匿名权限。|  
|此属性设置为 **null**（在 Microsoft Visual Basic .NET 中为 **Nothing**）。|不支持需要外部资源的功能，如定位外部架构或 DTD。  也不能解析外部实体，而且也不支持执行编辑功能（如插入需要解析的实体节点）。|当属性为 **null** 时，行为是相同的，不管 **XmlDocument** 是完全受信任的还是不完全受信任的。|  
|不设置此属性，而是将其保留为默认状态。|**XmlDocument** 解析文件名称和定位外部 DTD、实体和架构时，将实例化并使用带有 **null** 凭据的 **XmlUrlResolver**，**null** 凭据在编辑节点时使用。|**XmlDocument** 对所有操作使用匿名权限。|  
  
 当 **Load** 的输入是 **TextReader** 而且 **XmlDocument** 不完全受信任时，此表适用于 **XmlDocument.Load** 方法。  
  
|XmlResolver 属性|函数|备注|  
|--------------------|--------|--------|  
|**XmlDocument** 使用的 **XmlResolver** 类与 **XmlReader** 使用的是同一个类。|**XmlDocument** 使用分配给 **XmlReader** 的 **XmlResolver**。<br /><br /> 无论 **XmlDocument** 的信任级别如何，都无法设置 **XmlDocument.Resolver** 属性，因为它是从 **XmlReader** 获取 **XmlResolver**。  不能试图通过设置 **XmlDocument** 的 **XmlResolver** 属性来重写 **XmlReader** 的 **XmlResolver** 设置。|**XmlReader** 可以是 **XmlTextReader**、验证 <xref:System.Xml.XmlReader> 或自己编写的读取器。  如果使用的读取器支持实体解析，则解析外部实体。  如果传递的读取器不支持实体引用，那么就不解析实体引用。|  
  
 将 XmlResolver 设置为包含正确的凭据后，将可以访问外部资源。  
  
> [!NOTE]
>  无法检索 **XmlResolver** 属性。  这有助于防止用户重用已设置了凭据的 **XmlResolver**。  此外，如果使用 **XmlTextReader** 或验证 <xref:System.Xml.XmlReader> 加载 **XmlDocument**，而 **XmlDocument** 具有已设置的解析器，则 **XmlDocument** 在 **Load** 阶段后不缓存这些读取器中的解析器，因为这也会带来安全风险。  
  
 有关详细信息，请参阅 <xref:System.Xml.XmlResolver> 引用页的“备注”部分。  
  
## 请参阅  
 [XML 文档对象模型 \(DOM\)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)