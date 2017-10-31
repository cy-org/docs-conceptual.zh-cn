---
title: "Module 语句 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "Module"
  - "vb.Module"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "类 [Visual Basic], 与模块"
  - "声明, 模块"
  - "模块语句"
  - "模块"
  - "模块, 类"
  - "模块, 声明"
  - "标准模块"
ms.assetid: a1243afc-14a5-45df-95d5-51118aeac362
caps.latest.revision: 24
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 24
---
# Module 语句
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

声明模块的名称，并引入模块包含的变量、属性、事件和过程的定义。  
  
## 语法  
  
```  
[ <attributelist> ] [ accessmodifier ]  Module name  
    [ statements ]  
End Module  
```  
  
## 部件  
 `attributelist`  
 可选。  请参见 [特性列表](../../../visual-basic/language-reference/statements/attribute-list.md)。  
  
 `accessmodifier`  
 可选。  可以是如下内容之一：  
  
-   [Public](../../../visual-basic/language-reference/modifiers/public.md)  
  
-   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)  
  
 请参见 [Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。  
  
 `name`  
 必选。  此模块的名称。  请参见 [已声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)。  
  
 `statements`  
 可选。  定义此模块的变量、属性、事件、过程和嵌套类型的语句。  
  
 `End Module`  
 终止 `Module` 定义。  
  
## 备注  
 `Module` 语句定义了在其整个命名空间中都可用的引用类型。  “模块”（有时称为“标准模块”）类似于类，但有一些重要的差别。  每个模块均正好有一个实例，并且无需创建此实例或将其赋给变量。  模块不支持继承，也不实现接口。  请注意，从类或结构是类型这一意义上说，模块并非类型 \- 您无法将编程元素声明为具有模块的数据类型。  
  
 仅可以在命名空间级别使用 `Module`。  这意味着模块的声明上下文必须是源文件或命名空间，而不能是类、结构、模块、接口、过程或块。  无法在一个模块或任何类型中嵌套另一个模块。  有关更多信息，请参见[声明上下文和默认访问级别](../../../visual-basic/language-reference/statements/declaration-contexts-and-default-access-levels.md)。  
  
 模块具有与程序相同的生存期。  由于它的成员全都为 `Shared`，因此，它们也都具有与程序相同的生存期。  
  
 模块默认为 [Friend](../../../visual-basic/language-reference/modifiers/friend.md) 访问级别。  可以使用访问修饰符来调整它们的访问级别。  有关更多信息，请参见 [Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)。  
  
 模块的所有成员均隐式地为 `Shared`。  
  
## 类和模块  
 这些元素具有许多相似性，但是也存在一些重要的差异。  
  
-   **术语。**以前的 Visual Basic 版本识别两种类型的模块：类模块（.cls 文件）和标准模块（.bas 文件）。  当前版本会分别调用这些类和模块。  
  
-   **共享成员。**可以控制类的成员是共享成员还是实例成员。  
  
-   **面向对象。**类是面向对象的，但模块不是。  因此，只能将类实例化为对象。  有关更多信息，请参见 [对象和类](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)。  
  
## 规则  
  
-   **修饰符。**所有模块成员均隐式地为 [Shared](../../../visual-basic/language-reference/modifiers/shared.md)。  在声明成员时，无法使用 `Shared` 关键字，而且无法更改任何成员的共享状态。  
  
-   **继承。**模块无法从除 <xref:System.Object>（所有模块均从它继承）外的任何类型继承。  特别地，一个模块无法从另一个模块继承。  
  
     无法在模块定义中使用 [Inherits 语句](../../../visual-basic/language-reference/statements/inherits-statement.md)，即使是指定 <xref:System.Object> 亦为如此。  
  
-   **默认属性。**不能在模块中定义任何默认属性。  有关更多信息，请参见[Default](../../../visual-basic/language-reference/modifiers/default.md)。  
  
## 行为  
  
-   **访问级别。**在模块中，可以利用成员自己的访问级别来声明每个成员。  模块成员默认为 [Public](../../../visual-basic/language-reference/modifiers/public.md) 访问级别，但变量和常数除外，它们默认为 [Private](../../../visual-basic/language-reference/modifiers/private.md) 访问级别。  如果模块的访问级别在限制性上高于其一个成员的访问级别，则指定的模块访问级别将具有优先权。  
  
-   **范围。**模块的范围贯穿其命名空间。  
  
     每个模块成员的范围是整个模块。  请注意，所有成员都会经受类型提升，这将使它们的范围提升到包含模块的命名空间。  有关更多信息，请参见 [类型提升](../../../visual-basic/programming-guide/language-features/declared-elements/type-promotion.md)。  
  
-   **限定。**可以在一个项目中具有多个模块，而且可以在两个或更多个模块中声明名称相同的成员。  但是，如果从模块外引用此类成员，则必须用适当的模块名称来限定此类成员。  有关更多信息，请参见 [对已声明元素的引用](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)。  
  
## 示例  
 [!code-vb[VbVbalrStatements#69](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/module-statement_1.vb)]  
  
## 请参阅  
 [Class 语句](../../../visual-basic/language-reference/statements/class-statement.md)   
 [Namespace 语句](../../../visual-basic/language-reference/statements/namespace-statement.md)   
 [Structure 语句](../../../visual-basic/language-reference/statements/structure-statement.md)   
 [Interface 语句](../../../visual-basic/language-reference/statements/interface-statement.md)   
 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)   
 [类型提升](../../../visual-basic/programming-guide/language-features/declared-elements/type-promotion.md)