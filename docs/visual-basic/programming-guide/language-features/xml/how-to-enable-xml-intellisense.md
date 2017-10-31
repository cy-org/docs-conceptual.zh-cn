---
title: "如何︰ 启用 XML IntelliSense 在 Visual Basic |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- XML IntelliSense [Visual Basic]
- XML [Visual Basic], IntelliSense
- IntelliSense [Visual Basic], XML
ms.assetid: af67d0ee-a4a6-4abf-9c07-5a8cfe80d111
caps.latest.revision: 25
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
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 84af19189fa3fc510c8d4f8e408cbb2a393d8b8f
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-enable-xml-intellisense-in-visual-basic"></a>如何：在 Visual Basic 中启用 XML IntelliSense
在 Visual Basic 中的 XML IntelliSense 提供了完整单词的 XML 架构中定义的元素。 若要启用 XML IntelliSense 在 Visual Basic 中，必须执行以下操作︰  
  
1.  获取您的应用程序将读取或写入的 XML 文件的 XML 架构 (XSD) 文件。  
  
2.  在项目中包含的 XML 架构文件。  
  
3.  导入您的代码文件或项目的目标命名空间或命名空间。 由标识目标命名空间`targetNamespace`或`tns`XSD 架构的属性。  
  
     若要导入目标命名空间，请使用`Imports`语句，或通过将所有代码文件的命名空间添加到项目中**引用**项目设计器的页面。  
  
 功能在 Visual Basic 中的 XML IntelliSense 的详细信息，请参阅[Visual Basic 中的 XML IntelliSense](../../../../visual-basic/programming-guide/language-features/xml/xml-intellisense.md)。 导入 XML 命名空间的详细信息，请参阅[Imports 语句 (XML Namespace)](../../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)或[，项目设计器 (Visual Basic 中) 引用页](https://docs.microsoft.com/visualstudio/ide/reference/references-page-project-designer-visual-basic)。  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
 ![视频链接](../../../../visual-basic/programming-guide/language-features/xml/media/playvideo.gif "PlayVideo")本主题的视频版本，请参阅[视频帮助︰ 在 Visual Basic 中启用 XML IntelliSense](http://go.microsoft.com/fwlink/?LinkId=102466)。 有关相关的视频演示，请参阅[启用 XML IntelliSense 和使用 XML 命名空间如何实现？](http://go.microsoft.com/fwlink/?LinkId=143035)。  
  
## <a name="enable-xml-intellisense-in-visual-basic"></a>启用在 Visual Basic 中的 XML IntelliSense  
 如果您有一个 XML 文件，但您却没有为其 XSD 架构文件，在 SP1 中您可以创建 XSD 架构文件使用 XML 到架构向导。 您还可以使用架构推断 Visual Studio XML 编辑器中。  
  
#### <a name="to-create-an-xsd-schema-file-for-an-xml-file-by-using-the-xml-to-schema-wizard-requires-sp1"></a>若要使用 XML 到架构向导创建一个 XML 文件的 XSD 架构文件 （需要 SP1）  
  
1.  在项目中，单击**添加新项**上**项目**菜单。  
  
2.  选择**Xml 到架构**从项模板**数据**或**常用项**模板类别。  
  
3.  为提供一个文件名称或多个 XSD 文件，推断的架构集将存储在中，然后单击**添加**。  
  
4.  在**从 XML 文档推断 XML 架构集**窗口中，添加一个或多个要从中推断 XML 架构集的 XML 文档。  
  
    -   若要添加包含 XML 文档使用文件资源管理器的文本文件，请单击**从文件添加**。  
  
    -   若要添加从一个 HTTP 地址的 XML 文档，请单击**从 Web 添加**。  
  
    -   若要复制或键入到向导的 XML 文档的内容，请单击**键入或粘贴 XML**。  
  
5.  指定你想要推断 XML 架构集，请单击的所有 XML 文档源时**确定**推断 XML 架构设置。 架构集将保存在项目文件夹下面的一个或多个 XSD 文件。 （每个 XML 命名空间的架构中，创建文件。）  
  
#### <a name="to-create-an-xsd-schema-file-for-an-xml-file-by-using-schema-inference-in-the-visual-studio-xml-editor"></a>若要通过使用 Visual Studio XML 编辑器中的架构推断创建 XSD 架构文件的 XML 文件  
  
1.  编辑 Visual Studio XML 设计器中的 XML 文件。  
  
2.  当光标位于某个位置在 XML 文件中， **XML**菜单显示。 单击**Create Schema**上**XML**菜单。 从从 XML 文件推断 XSD 架构创建 XSD 文件。  
  
3.  保存该 XSD 架构文件。  
  
    > [!NOTE]
    >  可以从多个用于具有相同的架构的 XML 文档推断出不同的 XSD 架构。 这可发生在一个 XML 文件中而不是在另一台，找到特定的元素和属性时也顺序不同，例如包含元素。 使用 XSD 架构推断时，应检查推断出的 XSD 架构的完整性和精确性。  
  
#### <a name="to-include-an-xsd-schema-file"></a>若要包括的 XSD 架构文件  
  
-   默认情况下，您无法看到在 Visual Basic 项目的 XSD 文件。 如果在您的项目的文件夹中已经包含 XSD 文件，请单击**显示所有文件**按钮**解决方案资源管理器**。 找到 XSD 文件在**解决方案资源管理器**，用鼠标右键单击该文件，然后单击**将文件包括在项目**。  
  
-   如果 XSD 文件正在不属于您的项目，**解决方案资源管理器**，右键单击您要在其中存储 XSD 文件，指向的文件夹**添加**，然后单击**现有项**。 找到 XSD 文件，然后单击**添加**。  
  
#### <a name="to-import-an-xml-namespace-in-a-code-file"></a>若要导入到代码文件中的 XML 命名空间  
  
1.  标识从 XSD 架构的目标命名空间。  
  
2.  在代码文件的开头，添加`Imports`目标 XML 命名空间，如下面的示例中所示的语句。  
  
     [!code-vb[VbXMLSamples #&1;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-enable-xml-intellisense_1.vb)]  
  
     若要导入 XML 命名空间为默认命名空间，即应用于 XML 元素和属性不具有命名空间前缀的命名空间添加`Imports`目标默认 XML 命名空间的语句。 不要指定命名空间前缀。 以下是一种`Imports`语句。  
  
     [!code-vb[VbXmlSamples #&50;](../../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/how-to-enable-xml-intellisense_2.vb)]  
  
#### <a name="to-import-an-xml-namespace-for-all-files-in-a-project"></a>若要导入项目中的所有文件的 XML 命名空间  
  
1.  在代码文件中导入的 XML 命名空间适用于该代码文件。 若要导入适用于在项目中的所有代码文件的 XML 命名空间，请打开项目设计器，通过双击**我的项目**中**解决方案资源管理器**。  
  
2.  在**引用**选项卡上，在**导入的命名空间**框中，键入完整的 XML 命名空间声明的形式目标 XML 命名空间 (例如， `<xmlns: ns="http://sampleNamespace">`)。 如果目标 XML 命名空间没有指定命名空间前缀，命名空间将为该项目的默认 XML 命名空间。  
  
3.  单击**添加用户导入**。  
  
## <a name="see-also"></a>另请参阅  
 [Imports 语句 (XML Namespace)](../../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)   
 [项目设计器 ->“引用”页 (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/references-page-project-designer-visual-basic)   
 [在 Visual Basic 中的 XML IntelliSense](../../../../visual-basic/programming-guide/language-features/xml/xml-intellisense.md)

