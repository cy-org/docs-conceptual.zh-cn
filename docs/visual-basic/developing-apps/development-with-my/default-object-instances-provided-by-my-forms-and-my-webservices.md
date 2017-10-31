---
title: "My.Forms 和 My.WebServices 提供的默认对象实例 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "My.Forms 对象, 开发应用程序"
  - "My.WebServices 对象, 开发应用程序"
  - "快速应用程序开发 (RAD), My.Forms"
  - "快速应用程序开发 (RAD), My.WebServices"
ms.assetid: de930027-9108-4f0c-b97c-5e7db4d6ef79
caps.latest.revision: 5
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 5
---
# My.Forms 和 My.WebServices 提供的默认对象实例 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

[My.Forms](../../../visual-basic/language-reference/objects/my-forms-object.md) 和 [My.WebServices](../../../visual-basic/language-reference/objects/my-webservices-object.md) 对象提供对应用程序所使用的窗体、数据源以及 XML Web services 的访问。  它们通过提供每个对象的*“默认实例”*集合实现此功能。  
  
## 默认实例  
 默认实例是由运行时提供的类的实例，它不需要使用 `Dim` 和 `New` 语句进行声明和实例化。  下面的示例演示如何声明和实例化称为 `Form1` 的 <xref:System.Windows.Forms.Form> 类的实例，以及如何通过 `My.Forms` 获得此 <xref:System.Windows.Forms.Form> 类的默认实例。  
  
 [!code-vb[VbVbcnMy#5](../../../visual-basic/developing-apps/development-with-my/codesnippet/VisualBasic/default-object-instances-provided-by-my-forms-and-my-webservices_1.vb)]  
  
 [!code-vb[VbVbcnMy#6](../../../visual-basic/developing-apps/development-with-my/codesnippet/VisualBasic/default-object-instances-provided-by-my-forms-and-my-webservices_2.vb)]  
  
 `My.Forms` 对象会返回项目中每个 `Form` 类的默认实例的集合。  同样，对于您已在应用程序中创建引用的每一项 Web 服务，`My.WebServices` 都会为其代理类提供一个默认实例。  
  
## 请参阅  
 [My.Forms 对象](../../../visual-basic/language-reference/objects/my-forms-object.md)   
 [My.WebServices 对象](../../../visual-basic/language-reference/objects/my-webservices-object.md)   
 [My 对项目类型的依赖方式](../../../visual-basic/developing-apps/development-with-my/how-my-depends-on-project-type.md)