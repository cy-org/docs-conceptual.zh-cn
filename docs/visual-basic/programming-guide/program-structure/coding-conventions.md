---
title: "Visual Basic 编码约定 |Microsoft 文档"
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
- coding conventions, Visual Basic
- examples [Visual Basic], coding conventions
- Visual Basic code, conventions
ms.assetid: c1df130b-fec6-49a5-becf-0a7e494a1d0f
caps.latest.revision: 48
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
ms.openlocfilehash: 5712f14d53b86552a0b82af38ecf579577ef3fa1
ms.lasthandoff: 03/13/2017

---
# <a name="visual-basic-coding-conventions"></a>Visual Basic 编码约定
Microsoft 开发示例和文档，请遵循本主题中的准则。 如果您遵循相同的编码约定，您可能会获得以下好处︰  
  
-   您的代码将具有一致的外观，以确保读取器可以更好地专注于内容而非布局。  
  
-   读者理解您的代码更加快速因为它们可能会使基于以前的经验的假设。  
  
-   您可以复制、 更改，并更轻松地维护代码。  
  
-   可帮助确保您的代码演示 Visual basic"的最佳做法"。  
  
## <a name="naming-conventions"></a>命名约定  
  
-   有关命名准则的信息，请参阅[命名准则](http://msdn.microsoft.com/library/fc076d66-9b5f-42d3-aa65-61d970c794a3)主题。  
  
-   不使用"我的"我的"作为变量名称的一部分。 这种做法会导致与混淆`My`对象。  
  
-   无需更改的自动生成的代码以使它们适合这些准则中的对象的名称。  
  
## <a name="layout-conventions"></a>布局约定  
  
-   插入选项卡中的根据空格，并使用具有四个空间缩进量智能缩进。  
  
-   使用**整齐排列 （重新格式化） 的代码**重新格式化您的代码在代码编辑器中。 有关详细信息，请参阅[选项，文本编辑器中，基本 (Visual Basic 中)](https://docs.microsoft.com/visualstudio/ide/reference/options-text-editor-basic-visual-basic)。  
  
-   使用每行只有一条语句。 不要使用 Visual Basic 行分隔符 （:）。  
  
-   避免使用该语言允许它支持隐式行继续符显式行延续字符"_"。  
  
-   使用每行只有一个声明。  
  
-   如果**整齐排列 （重新格式化） 的代码**不格式连续行自动、 手动缩进一个制表位的延续任务行。 但是，始终向左对齐列表中的项。  
  
    ```  
    a As Integer,  
    b As Integer  
    ```  
  
-   添加方法和属性定义之间的至少一个空白行。  
  
## <a name="commenting-conventions"></a>注释约定  
  
-   将注释放在单独的行而不是在代码行的末尾。  
  
-   开始注释文本以大写字母，并以句点结束注释文本。  
  
-   插入注释分隔符 （'） 与注释文本之间的一个空格。  
  
     [!code-vb[VbVbalrGuidelines #&2;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_1.vb)]  
  
-   请不要括起来格式化的星号块注释。  
  
## <a name="program-structure"></a>程序结构  
  
-   当您使用`Main`方法中，默认结构用于新的控制台应用程序，并使用`My`对命令行参数。  
  
     [!code-vb[VbVbalrGuidelines #&3;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_2.vb)]  
  
## <a name="language-guidelines"></a>语言准则  
  
### <a name="string-data-type"></a>String 数据类型  
  
-   若要连接字符串，使用 and 符 （&）。  
  
     [!code-vb[VbVbalrGuidelines #&4;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_3.vb)]  
  
-   若要追加在循环中的字符串，请使用<xref:System.Text.StringBuilder>对象。</xref:System.Text.StringBuilder>  
  
     [!code-vb[VbVbalrGuidelines #&5;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_4.vb)]  
  
### <a name="relaxed-delegates-in-event-handlers"></a>宽松的委托事件处理程序中  
 请勿显式限定 （对象和 EventArgs） 的参数与事件处理程序。 如果您未使用的事件参数传递给事件 （例如，发件人为对象，作为 EventArgs e），使用宽松的委托，并使出在代码中的事件参数︰  
  
 [!code-vb[VbVbalrGuidelines #&7;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_5.vb)]  
  
### <a name="unsigned-data-type"></a>无符号数据类型  
  
-   使用`Integer`而不是无符号类型，除非它们是所必需。  
  
### <a name="arrays"></a>数组  
  
-   在声明行上初始化数组时，请使用短语法。 例如，使用以下语法。  
  
     [!code-vb[VbVbalrGuidelines #&8;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_6.vb)]  
  
     不要使用下面的语法。  
  
     [!code-vb[VbVbalrGuidelines #&9;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_7.vb)]  
  
-   将数组指示符放在类型上，而不在该变量上。 例如，使用以下语法︰  
  
     [!code-vb[VbVbalrGuidelines #&11;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_8.vb)]  
  
     不要使用以下语法︰  
  
     [!code-vb[VbVbalrGuidelines #&10;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_9.vb)]  
  
-   在声明并初始化的基本数据类型的数组时，请使用 {} 语法。 例如，使用以下语法︰  
  
     [!code-vb[VbVbalrGuidelines #&12;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_10.vb)]  
  
     不要使用以下语法︰  
  
     [!code-vb[VbVbalrGuidelines #&13;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_11.vb)]  
  
### <a name="use-the-with-keyword"></a>使用 With 关键字  
 当你进行一系列调用到一个对象时，请考虑使用`With`关键字︰  
  
 [!code-vb[VbVbalrGuidelines #&15;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_12.vb)]  
  
### <a name="use-the-trycatch-and-using-statements-when-you-use-exception-handling"></a>可以使用 Try...Catch 和 Using 语句时使用异常处理  
 请不要使用`On Error Goto`。  
  
### <a name="use-the-isnot-keyword"></a>使用 IsNot 关键字  
 使用`IsNot`关键字而不是`Not...Is Nothing`。  
  
### <a name="new-keyword"></a>New 关键字  
  
-   使用短实例化。 例如，使用以下语法︰  
  
     [!code-vb[VbVbalrGuidelines #&21;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_13.vb)]  
  
     前面的行是等效于此︰  
  
     [!code-vb[VbVbalrGuidelines #&22;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_14.vb)]  
  
-   为新对象，而无参数构造函数不使用对象初始值设定项︰  
  
     [!code-vb[VbVbalrGuidelines 第&23;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_15.vb)]  
  
### <a name="event-handling"></a>事件处理  
  
-   使用`Handles`而不是`AddHandler`:  
  
     [!code-vb[VbVbalrGuidelines #&24;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_16.vb)]  
  
-   使用`AddressOf`，并不显式实例委托︰  
  
     [!code-vb[VbVbalrGuidelines #&25;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_17.vb)]  
  
-   在定义事件时，使用短语法，并让编译器定义委托︰  
  
     [!code-vb[VbVbalrGuidelines #&26;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_18.vb)]  
  
-   不验证事件是否是`Nothing`(null)，然后才能调用`RaiseEvent`方法。 `RaiseEvent`检查`Nothing`引发事件之前。  
  
### <a name="using-shared-members"></a>使用共享的成员  
 调用`Shared`通过类的名称，不能从实例变量的成员。  
  
### <a name="use-xml-literals"></a>使用 XML 文本  
 XML 文本简化您使用 XML （例如，加载、 查询和转换） 时遇到的最常见任务。 当使用 XML 进行开发时，请遵循以下准则︰  
  
-   使用 XML 文本来创建 XML 文档和片段而不是直接调用 XML Api。  
  
-   导入 XML 命名空间在文件或项目级别，以利用 XML 文本的性能优化。  
  
-   XML 轴属性用于访问 XML 文档中元素和属性。  
  
-   使用嵌入式的表达式包括值并根据现有值而不是使用 API 调用，如创建 XML`Add`方法︰  
  
     [!code-vb[VbVbalrGuidelines #&27;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_19.vb)]  
  
### <a name="linq-queries"></a>LINQ 查询  
  
-   对查询变量使用有意义的名称︰  
  
     [!code-vb[VbVbalrGuidelines #&28;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_20.vb)]  
  
-   若要确保匿名类型的属性名称正确大写使用 Pascal 查询中的元素为提供的名称的大小写︰  
  
     [!code-vb[VbVbalrGuidelines #&29;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_21.vb)]  
  
-   如果结果中的属性名称模棱两可，请对属性重命名。 例如，如果您的查询返回客户名称和一个订单 ID，将其重命名而不是将它们保留为`Name`和`ID`结果中︰  
  
     [!code-vb[VbVbalrGuidelines #&30;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_22.vb)]  
  
-   在查询变量和范围变量的声明中使用类型推断︰  
  
     [!code-vb[VbVbalrGuidelines #&31;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_23.vb)]  
  
-   对齐下的查询子句`From`语句︰  
  
     [!code-vb[VbVbalrGuidelines #&32;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_24.vb)]  
  
-   使用`Where`子句之前其他查询子句，以便更高版本的查询子句作用于筛选的数据集︰  
  
     [!code-vb[VbVbalrGuidelines 第&33;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_25.vb)]  
  
-   使用`Join`子句显式定义联接操作，而不是使用`Where`子句隐式定义联接操作︰  
  
     [!code-vb[VbVbalrGuidelines #&34;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/coding-conventions_26.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [安全编码准则](http://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177)
