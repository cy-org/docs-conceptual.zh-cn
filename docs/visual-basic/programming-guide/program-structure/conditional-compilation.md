---
title: "Visual Basic 中的条件编译 | Microsoft Docs"
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
  - "编译, 条件"
  - "条件编译, 关于条件编译"
ms.assetid: 9c35e55e-7eee-44fb-a586-dad1f1884848
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# Visual Basic 中的条件编译
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

在“*条件编译”*中，有选择地编译程序中的特定代码块而忽略其他代码块。  
  
 例如，可能需要编写调试语句来比较同一编程任务的不同方法的速度，或者可能需要本地化用于多种语言的应用程序。  条件编译语句被设计为在编译时（而不是在运行时）运行。  
  
 那些要满足一定条件才编译的代码块使用 `#If...Then...#Else` 指令来表示。  例如，若要从相同的源代码创建同一应用程序的法语和德语版本，使用预定义常数 `FrenchVersion` 和 `GermanVersion` 将特定于平台的代码段嵌入 `#If...Then` 语句。  下面的示例说明嵌入的方法：  
  
 [!code-vb[VbVbalrConditionalComp#5](../../../visual-basic/language-reference/directives/codesnippet/VisualBasic/conditional-compilation_1.vb)]  
  
 如果在编译时将 `FrenchVersion` 条件编译常量的值设置为 `True`，则将编译法语版本的条件代码。  如果将 `GermanVersion` 常数的值设置为 `True`，则编译器将使用德语版本。  如果二者均未设置为 `True`，则运行最后的 `Else` 块中的代码。  
  
> [!NOTE]
>  如果代码不是当前分支的一部分，编辑代码和使用条件编译指令时，自动完成功能将不起作用。  
  
## 声明条件编译常量  
 可用如下三种方式之一设置条件编译常数：  
  
-   在**“项目设计器”**中  
  
-   使用命令行编译器时在命令行上  
  
-   在代码中  
  
 条件编译常数具有特殊的范围并且不能从标准代码访问。  条件编译常数的范围取决于它的设置方式。  下表列出了分别使用上述三种方式声明的常数范围。  
  
|||  
|-|-|  
|常数的设置方式|常数范围|  
|**项目设计器**|对于项目中的所有文件是公共的|  
|命令行|对于传递到命令行编译器的所有文件是公共的|  
|代码中的 `#Const` 语句|对于声明它的文件是私有的|  
  
||  
|-|  
|在“项目设计器”中设置常数|  
|-   在创建可执行文件之前，请按照[如何：修改项目属性和配置设置](http://msdn.microsoft.com/zh-cn/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)中提供的步骤在**“项目设计器”**中设置常数。|  
  
||  
|-|  
|在命令行上设置常数|  
|-   使用 **\/d** 开关输入条件编译常数，如下例所示：<br />     `vbc MyProj.vb /d:conFrenchVersion=–1:conANSI=0`<br />     **\/d** 开关与第一个常数之间不需要空格。  有关更多信息，请参见 [\/define](../../../visual-basic/reference/command-line-compiler/define.md)。<br />     命令行声明重写在**“项目设计器”**中输入的声明，但不清除它们。  在**“项目设计器”**中设置的参数对后面的编译仍然有效。<br />     在代码本身中编写常数时，对其位置没有严格规定，这是由于它们的范围是声明它们的整个模块。|  
  
||  
|-|  
|在代码中设置常数|  
|-   将常数放在使用它们的模块的声明块中。  这有助于组织代码和使之易于读取。|  
  
## 相关主题  
  
|||  
|-|-|  
|标题|说明|  
|[程序结构和代码约定](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)|提供使代码易于阅读和维护的建议。|  
  
## 引用  
 [\#Const 指令](../../../visual-basic/language-reference/directives/const-directive.md)  
  
 [\#If...Then...\#Else 指令](../../../visual-basic/language-reference/directives/if-then-else-directives.md)  
  
 [\/define](../../../visual-basic/reference/command-line-compiler/define.md)