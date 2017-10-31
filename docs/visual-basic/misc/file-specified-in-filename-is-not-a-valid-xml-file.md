---
title: "在 FileName 中指定的文件不是有效的 XML 文件 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-visual-basic
ms.topic: article
ms.assetid: c4c30bf3-e0ad-4bc8-89e0-2c3e49e9793b
caps.latest.revision: 12
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 2fa595ab411fdd300327db9e1fcca1e3156c7eed
ms.lasthandoff: 03/13/2017

---
# <a name="file-specified-in-filename-is-not-a-valid-xml-file"></a>在 FileName 中指定的文件不是有效的 XML 文件
所提供的文件名称不是有效的 XML 文件。 若要指定允许的 XML 文档的结构和内容，可使用文档类型定义 (DTD)、Microsoft XML 数据缩减 (XDR) 架构或 XML 架构定义语言 (XSD) 架构。 XSD 架构是用于指定 XML 语法中的首选的方式[!INCLUDE[dnprdnshort](../../csharp/getting-started/includes/dnprdnshort_md.md)]。  
  
> [!NOTE]
>  在某些较早版本的 Visual Studio 中，“XML 设计器” **** 是针对类型化数据集和 XML 架构的设计器。 “XML 设计器” **** 仍可用于创建和编辑 XML 架构文件。 但是，在[!INCLUDE[vs_current_long](../../csharp/misc/includes/vs_current_long_md.md)]，用于创建和编辑类型化数据集设计器是**数据集设计器**。 有关详细信息，请参阅[创建和编辑类型化数据集](https://docs.microsoft.com/visualstudio/data-tools/creating-and-editing-typed-datasets)。  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   检查你所提供的文件名是否正确。  
  
-   通过将你想要检查的 XML 文件加载到“XML 设计器” ****中，检查指定文件是否包含有效的 XML。 从“XML” **** 菜单上，单击“验证 XML” ****。 错误都显示在“输出列表” ****中。  
  
-   如果 XML 文件具有关联的 XML 架构，请检查显示在已定义结构中的元素，以及单个元素的内容是否符合架构中指定的已声明的数据类型。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Xml></xref:System.Xml>   
 [如何：分析文件路径](../../visual-basic/developing-apps/programming/drives-directories-files/how-to-parse-file-paths.md)
