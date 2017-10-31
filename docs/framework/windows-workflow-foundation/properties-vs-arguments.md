---
title: "属性与参数 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 14651389-4a49-4cbb-9ddf-c83fdc155df1
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 属性与参数
可使用多个选项将数据传入活动中。除使用 <xref:System.Activities.InArgument> 之外，还可以使用标准 CLR 属性或公共 <xref:System.Activities.ActivityAction> 属性开发接收数据的活动。本主题讨论如何选择适当的方法类型。  
  
## 使用 CLR 属性  
 在将数据传入活动中时，CLR 属性（即使用 Get 和 Set 例程来公开数据的公共方法）是受最多限制的选项。在编译解决方案时，必须知道传入 CLR 属性中的参数的值；此值对于每个工作流实例都是相同的。用这种方法，传递到 CLR 属性的值是类似于代码中定义的常量；此值无法更改活动的生命和无法更改活动的不同实例。<xref:System.Activities.Expressions.InvokeMethod%601.MethodName%2A> 是由活动公开的 CLR 属性的示例；无法根据运行时条件更改活动调用的方法名称，并且每个活动实例将相同。  
  
## 使用参数  
 活动的生存期内只对数据进行一次性计算时，也就是说，其值将不会在活动的生存期间更改，但该值因为不同的实例活动而不同，应使用参数。<xref:System.Activities.Statements.If.Condition%2A> 是一次性获取的值的示例；因此其将定义为参数。<xref:System.Activities.Statements.WriteLine.Text%2A> 是应该定义作为参数的方法的另一个示例，因为它在活动执行期间只进行一次计算，但它可以因不同的活动实例而不同。  
  
## 使用 ActivityAction  
 如果需要在活动的执行生存期内多次计算数据，则应使用 <xref:System.Activities.ActivityAction>。例如，为 <xref:System.Activities.Statements.While> 循环的每次迭代计算 <xref:System.Activities.Statements.While.Condition%2A> 属性。如果将 <xref:System.Activities.InArgument> 用于此目的，则循环将永不会退出，因为将不会为每个迭代重新计算该参数，并且将始终返回相同的结果。