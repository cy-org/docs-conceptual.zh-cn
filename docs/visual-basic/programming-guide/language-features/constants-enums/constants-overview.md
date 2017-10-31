---
title: "常量概述 (Visual Basic 中) |Microsoft 文档"
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
- constants
ms.assetid: 29016fe8-78b3-4dc8-90b8-1cfec2fa8ac9
caps.latest.revision: 14
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
ms.openlocfilehash: 8004045d233da0db017b26b350743ad9f8d61845
ms.lasthandoff: 03/13/2017

---
# <a name="constants-overview-visual-basic"></a>常量概述 (Visual Basic)
常量是有意义的名称，取代了数字或字符串，它不会更改。 常数存储值，如名称所示，保持不变的在整个应用程序的执行过程。 可以极大地提高代码的可读性并更加轻松地使用常量的维护。 在包含重新出现的值的代码中使用它们，或这取决于一些难以记住或没有明显意义的数字。  
  
## <a name="how-to-create-and-use-constants"></a>如何创建和使用常量  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]包含大量的预定义的常量，主要用于打印和显示。 您还可以创建您自己常量与`Const`语句，但创建的变量名中使用相同的规则。 如果`Option Strict`是`On`，所以必须显式声明常量的类型。  
  
 常量的作用域，它是所有代码都可以引用它，而不用限定其名称的集，等同于在同一位置中声明的变量。 若要创建一个常量，它位于某个特定过程的作用域内，请在该过程内声明。 若要创建一个常量，它在整个应用程序都可用，将使用其声明`Public`类的声明部分中的关键字。  
  
> [!NOTE]
>  虽然常量某种程度上类似于变量，不能对其进行修改，或根据对变量可以将新值分配给它们。  
  
 可通过控件或您使用的组件的对象模型定义在代码中使用的常量或它们可以是用户定义 （即，您自己创建）。  
  
## <a name="compile-time-and-run-time-constants"></a>编译时和运行时常量  
 编译时常量是在编译代码，而可以只计算运行时常量，该应用程序运行时的时间计算的。 编译时常量将在每次应用程序运行，而每次时可能会更改运行时常量具有相同的值。 编译时常量是必需的情况下，如数组界限、 case 表达式或枚举器初始值设定项。  
  
## <a name="in-this-section"></a>本节内容  
  
|定义|术语|  
|---|---|  
|[如何：声明常量](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-a-constant.md)|说明如何使用`Const`语句声明一个常量，并将其值; 设置为值通过声明一个常数，分配有意义的名称。|  
|[用户定义的常量](../../../../visual-basic/programming-guide/language-features/constants-enums/user-defined-constants.md)|描述如何创建您自己的常数，包括有关范围的信息以及如何避免循环引用。|  
|[常量和文本数据类型](../../../../visual-basic/programming-guide/language-features/constants-enums/constant-and-literal-data-types.md)|提供了有关的信息[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]编译器初始化常量时`Option Explicit`处于禁用状态。|  
|[如何：将相关的常量值组合在一起](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-group-related-constant-values-together.md)|演示如何相关的常量值进行分组。|  
  
## <a name="reference"></a>参考  
  
|定义|术语|  
|---|---|  
|[常量和枚举](../../../../visual-basic/language-reference/constants-and-enumerations.md)|列出预定义的常量[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]。|  
|[Const 语句](../../../../visual-basic/language-reference/statements/const-statement.md)|描述`Const`语句和它的使用。|  
|[Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)|描述`Option Strict`语句和它的使用。|  
  
## <a name="see-also"></a>另请参阅  
 [枚举概述](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-overview.md)   
 [如何︰ 初始化数组变量在 Visual Basic 中](../../../../visual-basic/programming-guide/language-features/arrays/how-to-initialize-an-array-variable.md)
