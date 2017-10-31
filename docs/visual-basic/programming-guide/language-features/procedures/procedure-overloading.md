---
title: "过程重载 (Visual Basic) | Microsoft Docs"
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
  - "按签名隐藏"
  - "Overloads 关键字"
  - "参数列表"
  - "参数, 列表"
  - "过程重载"
  - "过程, 多个版本"
  - "过程, 重载"
  - "过程, 参数列表"
  - "过程, 签名"
  - "Shadows 关键字"
  - "签名"
  - "签名, 过程"
  - "Visual Basic 代码, 参数列表"
  - "Visual Basic 代码, 过程"
ms.assetid: fbc7fb18-e3b2-48b6-b554-64c00ed09d2a
caps.latest.revision: 24
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 24
---
# 过程重载 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

重载过程是指使用相同的名称和不同的参数列表在多个版本中定义某个过程。  重载的目的是定义过程的若干个密切相关的版本，而不需要通过名称来区分它们，  可通过改变参数列表达到此目的。  
  
## 重载规则  
 重载过程时，适用以下规则：  
  
-   **相同名称**。  每一重载版本都必须使用同一个过程名。  
  
-   **不同签名**。  每个重载版本必须在以下至少一个方面不同于所有其他重载版本：  
  
    -   参数的数量  
  
    -   参数的顺序  
  
    -   参数的数据类型  
  
    -   类型参数的数量（适用于泛型过程）  
  
    -   返回类型（仅适用于转换运算符）  
  
     以上各项与过程名称一起称为过程的“签名”。  在调用重载的过程时，编译器使用签名来检查调用是否与定义正确匹配。  
  
-   **不属于签名部分的项**。  如果不改变签名，就不能重载过程。  尤其不能仅通过改变下列一项或多项来重载过程：  
  
    -   过程修饰符关键字，如 `Public`、`Shared` 和 `Static`  
  
    -   参数或类型参数的名称  
  
    -   类型参数约束（适用于泛型过程）  
  
    -   参数修饰符关键字，如 `ByRef` 和 `Optional`  
  
    -   是否返回值  
  
    -   返回值的数据类型（转换运算符除外）  
  
     以上列表中的项不属于签名。  虽然您无法用这些项区别重载版本，但可以在由其签名正确区分的重载版本中改变这些项。  
  
-   **后期绑定的参数**。  如果要将一个后期绑定对象变量传递给一个重载版本，必须将相应的参数声明为 <xref:System.Object>。  
  
## 过程的多个版本  
 假设要编写一个 `Sub` 过程来根据客户的余额公布交易，同时希望能够通过名称或者通过帐号引用客户。  为此，可以定义两个不同的 `Sub` 过程，如下例所示：  
  
 [!code-vb[VbVbcnProcedures#73](./codesnippet/VisualBasic/procedure-overloading_1.vb)]  
  
### 重载版本  
 另一种方法是重载一个单独的过程名。  可以使用 [Overloads](../../../../visual-basic/language-reference/modifiers/overloads.md) 关键字为每一个参数列表定义该过程的一个版本，如下所示：  
  
 [!code-vb[VbVbcnProcedures#72](./codesnippet/VisualBasic/procedure-overloading_2.vb)]  
  
#### 其他重载  
 如果还需要接受以 `Decimal` 或 `Single` 表示的交易金额，可进一步重载 `post` 以允许这种变化形式。  如果在上例中对每个重载都进行了这样的操作，就会有四个 `Sub` 过程，它们具有相同的名称但是具有四个不同的签名。  
  
## 重载的优点  
 重载过程的优点在于使调用更灵活。  若要使用前面示例中声明的 `post` 过程，调用代码可以获得 `String` 或 `Integer` 类型的客户标识，然后在两种情况下都调用同一过程。  下面的示例阐释了这一点：  
  
 [!code-vb[VbVbcnProcedures#56](./codesnippet/VisualBasic/procedure-overloading_3.vb)]  
  
 [!code-vb[VbVbcnProcedures#57](./codesnippet/VisualBasic/procedure-overloading_4.vb)]  
  
## 请参阅  
 [过程](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [如何：定义一个过程的多个版本](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-multiple-versions-of-a-procedure.md)   
 [如何：调用重载过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-an-overloaded-procedure.md)   
 [如何：重载带有可选参数的过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-overload-a-procedure-that-takes-optional-parameters.md)   
 [如何：重载参数数量不确定的过程](../../../../visual-basic/programming-guide/language-features/procedures/how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)   
 [重载过程注意事项](../../../../visual-basic/programming-guide/language-features/procedures/considerations-in-overloading-procedures.md)   
 [重载决策](../../../../visual-basic/programming-guide/language-features/procedures/overload-resolution.md)   
 [Overloads](../../../../visual-basic/language-reference/modifiers/overloads.md)   
 [Visual Basic 中的泛型类型](../../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)