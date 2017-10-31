---
title: "&lt;permission&gt; (Visual Basic) | Microsoft Docs"
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
  - "<permission> XML 标记"
  - "permission XML 标记"
ms.assetid: 0edf0500-5cd7-49c0-9255-64c48f972b77
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# &lt;permission&gt; (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定成员所需权限。  
  
## 语法  
  
```  
<permission cref="member">description</permission>  
```  
  
#### 参数  
 `member`  
 对可以通过当前编译环境进行调用的成员或字段的引用。  编译器检查给定的代码元素是否存在，并将 `member` 转换为输出 XML 中的规范化元素名称。  将 `member` 放入引号 \(" "\) 中。  
  
 `description`  
 对成员的访问的说明。  
  
## 备注  
 使用 `<permission>` 标记记录成员的访问权限。  使用 <xref:System.Security.PermissionSet> 类指定对成员的访问权限。  
  
 使用 [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md) 进行编译可以将文档注释处理到文件中。  
  
## 示例  
 此示例使用 `<permission>` 标记描述 <xref:System.Security.Permissions.FileIOPermission> 是 `ReadFile` 方法所必需的。  
  
 [!code-vb[VbVbcnXmlDocComments#7](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/permission_1.vb)]  
  
## 请参阅  
 [XML 注释标记](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)