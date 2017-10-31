---
title: "文档标记的分隔符（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- XML [C#], delimiters
- /** */ delimiters for C# documentation tags
- /// delimiter for C# documentation
ms.assetid: 9b2bdd18-4f5c-4c0b-988e-fb992e0d233e
caps.latest.revision: 21
author: BillWagner
ms.author: wiwagn
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
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 3e31f0c3d815c0454a9be6813ff9a04e5fa4c7de
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="delimiters-for-documentation-tags-c-programming-guide"></a>文档标记的分隔符（C# 编程指南）
XML 文档注释需要使用分隔符，用来向编译器指示文档注释开始和结束的位置。 可以使用以下采用 XML 文档标记的分隔符：  
  
 `///`  
 单行分隔符。 这是在文档示例中显示的格式，由 Visual C# 项目模板使用。 如果在分隔符后面有一个空格字符，那么此字符不会包括在 XML 输出中。  
  
> [!NOTE]
>  Visual Studio IDE 具有一种称为智能注释编辑的功能，在代码编辑器中键入 `///` 分隔符后，此功能可自动插入 \<summary> 和 \</summary> 标记，并在此标记中移动游标。 可在项目属性页的[“选项”->“文本编辑器”->“C#”->“格式设置”](/visualstudio/ide/reference/options-text-editor-csharp-formatting)中访问此功能。  
  
 `/** */`  
 多行分隔符。  
  
 使用 `/** */` 分隔符时需遵守一些格式设置规则。  
  
-   在包含 `/**` 分隔符的行上，如果行的其余部分为空格，则不将此行作为注释处理。 如果 `/**` 分隔符后面的第一个字符为空格，则忽略此空格字符，并处理行的其余部分。 否则，将 `/**` 分隔符后面的行的所有文本作为注释的一部分进行处理。  
  
-   在包含 `*/` 分隔符的行中，如果 `*/` 分隔符前面只有空格，此行将被忽略。 否则，`*/` 分隔符前面的行的文本被处理为注释的一部分，并且需符合后面的项目符号所描述的模式匹配规则。  
  
-   对于以 `/**` 分隔符开头的行后面的行，编译器在各行的开头寻找共同模式。 此模式可以包含空格和星号 (`*`)，后面跟更多空格。 如果编译器在不以 `/**` 分隔符或 `*/` 分隔符开头的各行开头找到共同模式，则忽略此每个行的模式。  
  
 以下示例说明了这些规则。  
  
-   以下注释中将被处理的唯一部分是以 `<summary>` 开头的行。 三种标记格式产生的注释相同。  
  
    ```  
    /** <summary>text</summary> */   
  
    /**   
    <summary>text</summary>   
    */   
  
    /**   
     * <summary>text</summary>   
    */  
    ```  
  
-   编译器识别出第二和第三行开头的共同模式“*”。 此模式不包括在输出中。  
  
    ```  
    /**   
     * <summary>   
     * text </summary>*/   
    ```  
  
-   编译器在下面的注释中未找到共同模式，因为第三行的第二个字符不是一个星号。 因此，第二和第三行上的所有文本将处理为注释的一部分。  
  
    ```  
    /**   
     * <summary>   
       text </summary>  
    */   
    ```  
  
-   编译器在以下注释中未找到模式，原因有两个。 首先，星号前的空格数不一致。 其次，第 5 行以制表符开头，这与空格不匹配。 因此，第二到第五行的所有文本都作为注释的一部分进行处理。  
  
    ```  
    /**   
      * <summary>   
      * text   
     *  text2   
        *  </summary>   
    */   
    ```  
  
## <a name="see-also"></a>请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [XML 文档注释](../../../csharp/programming-guide/xmldoc/xml-documentation-comments.md)   
 [/doc（C# 编译器选项）](../../../csharp/language-reference/compiler-options/doc-compiler-option.md)   
 [XML 文档注释](../../../csharp/programming-guide/xmldoc/xml-documentation-comments.md)

