---
title: "编译该项目中的 XML 架构时发生错误 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc36810
- vbc36810
dev_langs:
- VB
helpviewer_keywords:
- BC36810
ms.assetid: 9323b5d2-ba14-4e49-91f1-9ad647162144
caps.latest.revision: 11
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
ms.openlocfilehash: cf04e85da98db53d1c78269169571936f708cd21
ms.lasthandoff: 03/13/2017

---
# <a name="errors-occurred-while-compiling-the-xml-schemas-in-the-project"></a>编译项目中的 XML 架构时发生错误
编译项目中的 XML 架构时发生错误。 因此，XML IntelliSense 不可用。  
  
 在项目中包含的 XML 架构定义 (XSD) 架构中没有错误。 当您添加为项目设置与现有的 XSD 架构冲突的 XSD 架构 (.xsd) 文件时，将发生此错误。  
  
 **错误 ID:** BC36810  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   双击中的警告**错误列表**窗口。 Visual Basic 将可访问的源的警告的 XSD 文件中的位置。 更正的 XSD 架构中的错误。  
  
-   确保所有必需的 XSD 架构 (.xsd) 文件都包括在项目中。 您可能需要单击**显示所有文件**上**项目**菜单以查看您.xsd 文件中**解决方案资源管理器**。 右键单击一个.xsd 文件，然后单击**包括在项目**若要将文件包括在你的项目。  
  
-   如果您使用的 XML 到架构向导，如果从同一源推断架构不止一次可以发生此错误。 在这种情况下，您可以从项目中，删除现有的 XSD 架构文件将添加新的 XML 到架构项模板，然后提供 XML 到架构向导使用所有适用的 XML 源为您的项目。  
  
-   如果在 XSD 架构中不标识任何错误，则 XML 编译器可能没有足够的信息来提供详细的错误消息。 您可能能够获得更详细的错误信息，如果您确保.xsd 文件的 XML 命名空间包括项目匹配项中标识为在 Visual Studio 中设置 XML 架构的 XML 命名空间。  
  
## <a name="see-also"></a>另请参阅  
 [错误列表窗口](https://docs.microsoft.com/visualstudio/ide/reference/error-list-window)   
 [在 Visual Basic 中的 XML IntelliSense](../../../visual-basic/programming-guide/language-features/xml/xml-intellisense.md)   
 [XML](../../../visual-basic/programming-guide/language-features/xml/index.md)
