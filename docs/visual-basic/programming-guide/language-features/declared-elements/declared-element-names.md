---
title: "声明的元素名称 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- declared elements, case sensitivity
- names, Visual Basic rules
- naming conventions
- element names
- declared elements, identifiers
- declarations, elements
- declared elements, valid names
- '[] escape characters [Visual Basic]'
- names, elements
- declaration statements, declared elements
- declaring elements
- identifiers, declared elements
- case sensitivity, declared element names
- escape characters
- names, declared elements
- declared elements, about declared elements
- escaped names
- declared elements, names
- names, naming conventions
- identifiers, elements
ms.assetid: 09d8843b-c0dc-4afe-9dab-87c439a69e66
caps.latest.revision: 27
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
ms.openlocfilehash: 56ac0684e5176f33aa6f9600f20d9fe3fcf09416
ms.lasthandoff: 03/13/2017

---
# <a name="declared-element-names-visual-basic"></a>已声明的元素名称 (Visual Basic)
每个已声明的元素有一个名称，也称为*标识符*，这是该代码使用来引用它。  
  
## <a name="rules"></a>规则  
 中的元素名称[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]必须遵守以下规则︰  
  
-   它必须以字母字符或下划线开头 (`_`)。  
  
-   它必须仅包含字母字符、 十进制数字和下划线。  
  
-   如果以下划线开头，它必须包含至少一个字母字符或十进制数字类别。  
  
-   它不得超过 1023年个字符长。  
  
 1023 个字符的长度限制也适用于整个字符串的完全限定的名称，如`outerNamespace.middleNamespace.innerNamespace.thisClass.thisElement`。  
  
 下面的示例演示一些有效的元素名称。  
  
 `aB123__45`  
  
 `_567`  
  
 下面的示例演示一些无效的元素名称。 第一个仅包含一个下划线、 十进制数字，以开始第二个和第三个包含无效字符 （$）。  
  
 `' Three INVALID element names`  
  
 `_`  
  
 `12ABC`  
  
 `xyz$wv`  
  
> [!CAUTION]
>  元素名称以下划线开头 (`_`) 不属于[语言独立性和与语言无关的组件](https://msdn.microsoft.com/library/12a7a7h3)(CLS)，因此符合 cls 的代码不能使用一个组件，它定义了此类名称。 但是，元素名称中的任何其他位置的下划线是符合 CLS。  
  
### <a name="name-length-guidelines"></a>名称长度原则  
 在实践中，您的名称应尽可能短时仍然能够清楚地标识该元素的特性。 这可以提高您的代码的可读性并降低行长度和源文件大小。  
  
 另一方面，您的名称不应为太短，它不会不充分描述的元素表示以及您的代码如何使用它。 这是代码的重要的可读性。 如果其他人正试图了解它，或者如果您自己正在寻求通过它您撰写后很长时间，适当元素名称可以节省相当长的时间。  
  
## <a name="escaped-names"></a>转义的名称  
 通常情况下，元素名称必须与任何不匹配的保留的关键字[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]，如`Case`或`Friend`。 但是，可以定义*转义名称*，这由方括号括起来 (`[ ]`)。 转义的名称可以匹配任何[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]关键字，因为括号消除了不明确性。 在更高版本在代码中引用的名称时，还可以使用方括号。  
  
 通常情况下，应使用转义的名称时，才︰  
  
-   您的代码已从早期版本迁移[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]，没有保留关键字用作名称; 或  
  
-   您正在使用中的给定的关键字不保留的另一种语言编写的代码。  
  
 否则，应考虑重命名该元素，如果其名称与关键字冲突。 集成的开发环境 (IDE) 提供了轻松执行此操作。 有关详细信息，请参阅[重构](https://docs.microsoft.com/visualstudio/vb-ide/refactoring-vb)。  
  
## <a name="case-sensitivity-in-names"></a>在名称中的区分大小写  
 中的元素名称[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]不区分大小写。 这意味着当编译器在比较两个不同的字母大小写的名称，将其解释为相同的名称。 例如，它认为 `ABC` 和 `abc` 指的是同一个声明的元素。  
  
 但是，公共语言运行时 (CLR) 使用区分大小写的绑定。 因此，当你生成程序集或 DLL 并使其可供其他程序集使用时，则名称将不再不区分大小写。 例如，如果你用名为 `ABC`的元素定义类，而其他程序集通过公共语言运行时使用你的类，则元素必须指的是 `ABC`。 如果以后要重新编译该类并将更改元素的名称传递给`abc`，则使用您的类的其他程序集将无法再访问该元素。 因此，发布程序集的更新版本时，不应该更改公共元素的字母大小写。  
  
## <a name="names-and-locales"></a>名称和区域设置  
 名称的比较是独立于区域设置。 如果在一个区域设置中匹配两个名称，可确保在所有区域设置匹配。  
  
## <a name="see-also"></a>另请参阅  
 [已声明的元素](../../../../visual-basic/programming-guide/language-features/declared-elements/index.md)   
 [已声明的元素的特性](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)   
 [对已声明的元素的引用](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [语句](../../../../visual-basic/language-reference/statements/index.md)
