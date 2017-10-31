---
title: "可恢复的 XSLT 错误 | Microsoft Docs"
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
ms.assetid: 484929b0-fefb-4629-87ee-ebdde70ff1f8
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# 可恢复的 XSLT 错误
W3C XSL 转换 \(XSLT\) 1.0 版建议中涉及到实现提供者可以在哪些方面确定如何处理某种情况。  这些方面被认为是任意行为。  例如，在第 7.3 节“Creating Processing Instructions”中，XSLT 1.0 建议指出，如果实例化 `xsl:processing-instruction` 的内容会创建文本节点以外的节点，则会发生错误。  对于某些问题，XSLT 1.0 建议指示在处理器决定从错误中恢复时应做的决策。  对于 7.3 节中给出的问题，W3C 指出，实现可以通过忽略节点及其内容来从此错误中恢复。  
  
## 任意行为  
 下表列出 XSLT 1.0 建议允许的每项任意行为以及这些行为如何通过 <xref:System.Xml.Xsl.XslCompiledTransform> 类进行处理。  
  
-   恢复指示 <xref:System.Xml.Xsl.XslCompiledTransform> 类将从此错误中恢复。  <xref:System.Xml.Xsl.XsltArgumentList.XsltMessageEncountered?displayProperty=fullName> 事件可以用于从 XSLT 处理器报告任意事件。  
  
-   错误指示此条件将引发异常。  
  
-   引用的章节可以在 [W3C XSL 转换 \(XSLT\) 1.0 版建议](http://go.microsoft.com/fwlink/?LinkId=49919)（可能为英文网页）和 [W3C XSL 转换 \(XSLT\) 1.0 版规范勘误表](http://go.microsoft.com/fwlink/?LinkId=49917)（可能为英文网页）中找到。  
  
|XSLT 条件|节|XslCompiledTransform 行为|  
|-------------|-------|-----------------------------|  
|文本节点同时与 `xsl:strip-space` 和 `xsl:preserve-space` 匹配。|3.4|恢复|  
|源节点与多个模板规则匹配。|5.5|恢复|  
|某个命名空间 URI 声明为多个命名空间 URI 的别名，所有这些 URI 都具有相同的导入优先级。|7.1.1|恢复|  
|通过属性值生成的 `xsl:attribute` 和 `xsl:element` 中的 `name` 属性不是 QName。|7.1.2, 7.1.3|错误\*|  
|具有相同导入和扩展名称的两个属性集具有一个公共的属性，没有其他包含该公共属性的同名属性集具有更高的优先级。|7.1.4|恢复|  
|在添加子级之后将属性添加到元素中。|7.1.3|错误\*|  
|创建名为“xmlns”的属性|7.1.3|错误\*|  
|将属性添加到非元素节点中。|7.1.3|错误\*|  
|在实例化 `xsl:attribute` 属性的内容期间创建文本节点以外的节点。|7.1.3|错误\*|  
|`xsl:processing-instruction` 的 `name` 属性不生成 NCName 和处理指令目标。|7.3|错误\*|  
|实例化 `xsl:processing-instruction` 的内容创建了文本节点以外的节点。|7.3|错误\*|  
|`xsl:processing-instruction` 内容的实例化结果中包含字符串“?\>”|7.3|恢复|  
|`xsl:processing-instruction` 内容的实例化结果中包含字符串“\-\-”或以“\-”结尾。|7.4|恢复|  
|`xsl:comment` 内容的实例化结果创建了文本节点以外的节点。|7.4|错误\*|  
|变量绑定元素内部的模板返回属性节点或命名空间节点。|11.2|错误\*|  
|从传入文档函数的 URI 中检索资源时出错。|12.1|错误|  
|文档函数中的 URI 引用包含片断标识符，在处理片断标识符时出错。|12.1|恢复\*|  
|存在多个名称相同但是值不同的属性，这些属性不是具有相同导入优先级的 `xsl:output` 中的命名 cdata 节元素。|16|恢复|  
|处理器不支持 `xsl:output` 编码属性中的编码。|16.1|恢复|  
|对用于结果树中的非文本节点内容的文本节点禁用输出转义。|16.4|恢复\*|  
|如果结果树片段包含启用了输出转义的文本节点，则将该结果树片断转换为数字或字符串。|16.4|恢复\*|  
|对不能以 XSLT 处理器用于输出的编码表示的字符禁用输出转义。|16.4|恢复\*|  
|向元素添加子级或添加属性后，向元素添加命名空间节点。|errata 25|错误\*|  
|`xsl:number` 的 `value` 属性为 NAN、无限大或小于 0.5。|errata 24|恢复|  
|文档函数的第二个参数 node\-set 为空，且 URI 引用是相对的。|errata 14|恢复|  
  
 <sup>*</sup> 此行为与 <xref:System.Xml.Xsl.XslTransform> 类的行为不同。  有关详细信息，请参阅[XslTransform 类中任意行为的实现](../../../../docs/standard/data/xml/implementation-of-discretionary-behaviors-in-the-xsltransform-class.md)。  
  
## 请参阅  
 [XSLT 转换](../../../../docs/standard/data/xml/xslt-transformations.md)