---
title: "XML 到架构向导 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vb.XmlToSchemaWizard
dev_langs:
- VB
helpviewer_keywords:
- XML IntelliSense [Visual Basic]
- XML [Visual Basic], IntelliSense
- IntelliSense [Visual Basic], XML
- XML schemas, creating
ms.assetid: 98c495ba-8f37-4517-a0db-aa738611ab76
caps.latest.revision: 16
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: d0c9c0247f3d9934ef973c7322cb098f9b445a5a
ms.lasthandoff: 03/13/2017

---
# <a name="xml-to-schema-wizard-visual-basic"></a>XML 到架构向导 (Visual Basic)
使用 XML 到架构向导创建推断 XML 架构集从一个或多个 XML 文档并将其包含您的项目。 可以使用文本文件、 XML 从 HTTP Internet 地址或键入或粘贴到 XML 到架构向导的 XML 形式的 XML 文档的任意组合。  
  
 XML 架构用于为在 Visual Basic 中的 XML 属性提供智能感知。 有关详细信息，请参阅[XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)和[Visual Basic 中的 XML IntelliSense](../../../../visual-basic/programming-guide/language-features/xml/xml-intellisense.md)。  
  
> [!NOTE]
>  在运行 XML 到架构向导之前，建议从先前由向导生成的项目中删除任何现有的 XSD 文件。 如果推断 XML 架构集相匹配现有架构集时，可能发生冲突并[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]不能为 XML 属性提供智能感知。  
  
 XML 到架构向导使用<xref:System.Xml.Schema.XmlSchemaInference>类来为所提供的 XML 创建架构。</xref:System.Xml.Schema.XmlSchemaInference> 结果是，为架构集可能会创建多个架构文件。 每个 XML 命名空间中所提供的 XML，会创建一个可扩展架构定义 (XSD) 文件。 有关详细信息，请参阅<xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A>方法。</xref:System.Xml.Schema.XmlSchemaInference.InferSchema%2A>  
  
 若要访问 XML 到架构向导，请单击**添加新项**上**项目**菜单上，并添加**XML 到架构**模板**数据**或**常用项**模板组。 包括了要推断从 XML 架构集的所有 XML 文档源之后，单击**确定**创建推断出的架构集。  
  
 **源类型**  
 此列显示的 XML 文档的源的类型︰**文件**， **URL**，或**XML**。  
  
 **XML 文档位置**  
 此列显示 XML 文档的路径。 键入或粘贴的 XML 文档，用于显示 XML 文档的内容。  
  
 **从文件添加**  
 单击此按钮可通过使用文件资源管理器添加 XML 文档文件。  
  
 **从 Web 添加**  
 单击此按钮可提供 XML 文档的 HTTP 地址。  
  
 **键入或粘贴 XML**  
 单击此按钮以键入或粘贴到对话框中的 XML 文档。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Xml.Schema.XmlSchemaInference></xref:System.Xml.Schema.XmlSchemaInference>   
 [在 Visual Basic 中的 XML IntelliSense](../../../../visual-basic/programming-guide/language-features/xml/xml-intellisense.md)
