---
title: "嵌入到文档中的样式表指令 | Microsoft Docs"
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
ms.assetid: d79fb295-ebc7-438d-ba1b-05be7d534834
caps.latest.revision: 4
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 4
---
# 嵌入到文档中的样式表指令
有时，现有 XML 会包含 `<?xml:stylesheet?>` 形式的样式表指令。  Microsoft Internet Explorer 接受此指令作为 `<?xml-stylesheet?>` 语法的替换形式。  当 XML 数据包含 `<?xml:stylesheet?>` 指令时（如下面的数据所示），试图将此数据加载到 XML 文档对象模型 \(DOM\) 中将引发异常。  
  
```  
<?xml version="1.0" ?>  
<?xml:stylesheet type="text/xsl" href="test2.xsl"?>  
<root>  
    <test>Node 1</test>  
    <test>Node 2</test>  
</root>  
```  
  
 发生这种情况是由于 `<?xml:stylesheet?>` 被视为 DOM 的无效 **ProcessingInstruction**。  根据 XML 中的命名空间规范，任何 **ProcessingInstruction** 都只能是无冒号名称 \(NCNames\)，与限定名 \(QNames\) 相反。  
  
 根据 XML 中的命名空间规范的第 6 节，使 **Load** 和 **LoadXml** 方法符合此规范所产生的影响是，在文档中：  
  
-   所有元素类型和属性名都包含零个或一个冒号。  
  
-   任何实体名称、ProcessingInstruction 目标或表示法名称都不包含冒号。  
  
 因为 `<?xml:stylesheet?>` 包含一个冒号，所以您违反了第二条规则。  
  
 根据万维网联合会 \(W3C\) 将样式表与 XML 文档关联的 1.0 版建议（位于 www.w3.org\/TR\/xml\-stylesheet），将 XSL 样式表与 XML 文档关联的处理指令是 `<?xml-stylesheet?>`（用短划线代替冒号）。  
  
## 请参阅  
 [XML 文档对象模型 \(DOM\)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)