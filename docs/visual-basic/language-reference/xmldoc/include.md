---
title: "&lt;include&gt; (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "<include> XML 标记"
  - "include XML 标记"
ms.assetid: ba8e9173-82cd-460b-8938-a075a2dfb36d
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# &lt;include&gt; (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

引用源代码中描述和成员的其他文件。  
  
## 语法  
  
```  
<include file="filename" path="tagpath[@name='id']" />  
```  
  
#### 参数  
 `filename`  
 必选。  包含文档的文件名。  该文件名可用路径加以限定。  将 `filename` 置于双引号 \(" "\) 内。  
  
 `tagpath`  
 必选。  `filename` 中指向标记 `name` 的标记路径。  将此路径置于双引号中 \(" "\) 内。  
  
 `name`  
 必选。  注释前边的标记中的名称说明符。  `Name` 具有一个 `id`。  
  
 `id`  
 必选。  位于注释之前的标记的 ID。  将此 ID 置于单引号中 \(' '\)。  
  
## 备注  
 使用 `<include>` 引用描述源代码中类型和成员的另一文件中的注释。  这是除了将文档注释直接置于源代码文件中之外的另一种可选方法。  
  
 `<include>` 标记使用 W3C XML Path Language \(XPath\) Version 1.0 Recommendation。  有关自定义 `<include>` 使用方法的更多信息，请访问 http:\/\/www.w3.org\/TR\/xpath。  
  
## 示例  
 此示例使用 `<include>` 标记从名称为 `commentFile.xml` 的文件中导入成员文档注释。  
  
 [!code-vb[VbVbcnXmlDocComments#4](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/include_1.vb)]  
  
 `commentFile.xml` 的格式如下。  
  
```  
<Docs>  
<Members name="Open">  
<summary>Opens a file.</summary>  
<param name="filename">File name to open.</param>  
</Members>  
<Members name="Close">  
<summary>Closes a file.</summary>  
<param name="filename">File name to close.</param>  
</Members>  
</Docs>  
```  
  
## 请参阅  
 [XML 注释标记](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)