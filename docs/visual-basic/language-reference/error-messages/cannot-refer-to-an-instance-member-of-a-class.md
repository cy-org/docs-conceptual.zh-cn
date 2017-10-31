---
title: "没有类的显式实例，就无法从共享方法或共享成员初始值设定项中引用该类的实例成员 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30369"
  - "bc30369"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30369"
  - "Shared"
ms.assetid: 39d9466b-c1f3-4406-91a5-3d6c52d23a3d
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 没有类的显式实例，就无法从共享方法或共享成员初始值设定项中引用该类的实例成员
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

尝试从共享过程中引用类的非共享成员。  下面的示例演示了这样的情形。  
  
```  
Class sample  
    Public x as Integer  
    Public Shared Sub setX()  
        x = 10  
    End Sub  
End Class  
```  
  
 在前面的示例中，赋值语句 `x = 10` 生成此错误信息。  这是因为共享过程尝试访问实例变量。  
  
 变量 `x` 是一个实例成员，因为它没有被声明为 [Shared](../../../visual-basic/language-reference/modifiers/shared.md)。  类 `sample` 的每个实例都包含其自己单独的变量 `x`。  当一个实例设置或更改 `x` 的值时，它不会影响任何其他实例中的 `x` 的值。  
  
 但是，过程 `setX` 在类 `sample` 的所有实例中是 `Shared`。  这意味着，它与类的任一实例都不关联，而是独立于各个实例运行。  由于它与特定实例没有联系，因此 `setX` 无法访问实例变量。  它必须只对 `Shared` 变量进行运算。  当 `setX` 设置或更改共享变量的值时，那个新值可用于类的所有实例。  
  
 **错误 ID：**BC30369  
  
### 更正此错误  
  
1.  确定是要在类的所有实例中共享成员，还是使成员对于每个实例都保持独立。  
  
2.  如果要在所有实例中共享成员的一个副本，请将 `Shared` 关键字添加到成员声明中。  在过程声明中保留 `Shared` 关键字。  
  
3.  如果希望每个实例具有其自己单独的成员副本，请不要为成员声明指定 `Shared`。  将 `Shared` 关键字从该过程声明中移除。  
  
## 请参阅  
 [Shared](../../../visual-basic/language-reference/modifiers/shared.md)