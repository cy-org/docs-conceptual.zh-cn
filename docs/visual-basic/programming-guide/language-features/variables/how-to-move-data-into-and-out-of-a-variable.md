---
title: "如何：将数据移入和移出变量 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "变量 [Visual Basic], 检索值"
  - "变量 [Visual Basic], 存储数据"
ms.assetid: 93744f46-bf78-4fa0-9640-1de01bc38d9a
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# 如何：将数据移入和移出变量 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

通过将变量名称置于赋值语句的左侧，可以在变量中存储值。  
  
## 将数据放入变量中  
  
#### 在变量中存储值  
  
-   在赋值语句的左侧使用变量名称。  
  
     下面的示例设置变量 `alpha` 的值。  
  
    ```  
    alpha = (beta * 6.27) / (gamma + 2.1)  
    ```  
  
     将赋值语句右侧生成的值存储在变量中。  
  
## 从变量中获取数据  
 通过将变量名称包含在表达式中，可以检索变量值。  
  
#### 从变量中检索值  
  
-   在表达式中使用变量名称。  在任何可以使用常数或文本的情况下均可以使用变量，除非表达式中已经定义了常数值。  
  
     \- 或 \-  
  
-   在赋值语句中的等号 \(`=`\) 后面使用变量名称。  
  
     下面的示例读取变量 `startValue` 的值，并在表达式中使用变量 `counter` 的值。  
  
    ```  
    counter = startValue  
    cellValue = (counter + 5) ^ 2  
    ```  
  
     变量的值像常数那样参与到表达式运算中，然后存储在赋值语句左侧的变量或属性中。  
  
## 请参阅  
 [变量](../../../../visual-basic/programming-guide/language-features/variables/index.md)   
 [变量声明](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [对象变量](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)