---
title: "WriteOnly (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "WriteOnly"
  - "vb.WriteOnly"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "属性 [Visual Basic], write-only"
  - "敏感数据"
  - "敏感数据, 保护"
  - "WriteOnly 关键字"
  - "只写属性"
ms.assetid: 488d2899-b09f-4cee-92f0-6f9f9fc4f944
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# WriteOnly (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定某个属性可写但不可读。  
  
## 备注  
  
## 规则  
 **声明上下文。**仅可以在模块级别使用 `WriteOnly`。  这表示，`WriteOnly` 属性的声明上下文必须是类、结构或模块，但不可以是源文件、命名空间或过程。  
  
 可以将属性声明为 `WriteOnly`，但不可以这样声明变量。  
  
## 何时使用 WriteOnly  
 有时，您可能希望使用属性的代码能够设置它的值，但无法读取其内容。  例如，身份证号或密码这样的敏感数据需要受到保护，以防止不设置它的其他组件访问它。  在这些情况下，可以使用 `WriteOnly` 属性来设置该值。  
  
> [!IMPORTANT]
>  在定义和使用 `WriteOnly` 属性时，请考虑下面的附加保护措施：  
  
-   **重写。**如果属性是类的成员，则将其默认为 [NotOverridable](../../../visual-basic/language-reference/modifiers/notoverridable.md)，不要将其声明为 `Overridable` 或 `MustOverride`。  这可以阻止派生类通过重写进行不需要的访问。  
  
-   **访问级别。**如果将属性的敏感数据存放在一个或多个变量中，请声明这些变量为 [Private](../../../visual-basic/language-reference/modifiers/private.md)，以便其他代码无法访问它们。  
  
-   **加密。**以加密的形式而不是纯文本的形式存储所有敏感数据。  如果恶意代码以某种方式获取了对该内存区域的访问权，经过加密的数据比纯文本相比更难于被利用。  如果必须序列化敏感数据，加密也很有用。  
  
-   **重置。**当定义属性的类、结构或模块终止时，将敏感数据重置为默认值或其他无意义的值。  在为一般访问释放该内存区域时，这会提供额外的保护。  
  
-   **持久性。**尽量避免持久性地存放任何敏感数据（例如存放在磁盘上）。  而且，不要将任何敏感数据写入剪贴板。  
  
 `WriteOnly` 修饰符可用于下面的上下文中：  
  
 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)  
  
## 请参阅  
 [ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)   
 [Private](../../../visual-basic/language-reference/modifiers/private.md)   
 [关键字](../../../visual-basic/language-reference/keywords/index.md)