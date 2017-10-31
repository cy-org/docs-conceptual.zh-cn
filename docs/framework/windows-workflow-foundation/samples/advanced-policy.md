---
title: "高级策略 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 75a22c88-5e54-4ae8-84cb-fbb22a612f0a
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# 高级策略
此示例扩展了简单策略示例。除了简单策略示例中的住户折扣和企业折扣规则外，还添加了若干新规则。  
  
 添加了一条高价值规则，可为高价值订单提供更大的折扣。该规则被赋予了比前两条规则更小的优先级值，因此它将覆盖折扣字段，并优先于住户折扣或企业折扣规则。  
  
 另外还添加了一条计算总计规则，可基于折扣级别计算出总计。它显示了如何引用工作流活动上定义的方法，以及如何使用其他操作。此规则还演示了链接行为，因为任何时候当折扣字段发生更改时都会计算该规则。而且，还通过 CalculateTotal 方法上的 RuleWriteAttribute 显示了方法属性设置。这样，无论何时在执行方法时，都会重新计算受影响的规则 \(ErrorTotalRule\)。  
  
 添加的最后一条规则是用于检测错误（本例中为总计小于 0）的规则。如果出现这种错误，策略执行将停止。  
  
 `Console.Writeline` 还以操作的形式向每条规则中添加了 Console.Writeline 调用，以使规则执行的可见性更高，同时还显示它可能访问所引用类型上的静态方法。您还可以使用跟踪来查看所执行的规则。  
  
 此示例中使用的规则包括：  
  
 **ResidentialDiscountRule：**  
  
 IF OrderValue \> 500 AND CustomerType \= Residential  
  
 THEN Discount \= 5%  
  
 **BusinessDiscountRule：**  
  
 IF OrderValue \> 10000 AND CustomerType \= Business  
  
 THEN Discount \= 10%  
  
 **HighValueDiscountRule：**  
  
 IF OrderValue \> 20000  
  
 THEN Discount \= 15%  
  
 **TotalRule：**  
  
 IF Discount \> 0  
  
 THEN CalculateTotal\(OrderValue, Discount\)  
  
 ELSE Total \= OrderValue  
  
 **ErrorTotalRule：**  
  
 IF Total \< 0  
  
 THEN Error \= "Fired ErrorTotalRule"; Halt  
  
 也可以通过追踪和跟踪看到规则的计算和执行过程。  
  
### 生成示例  
  
1.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中打开解决方案。  
  
2.  按 Ctrl\+Shift\+B 生成解决方案。  
  
3.  按 Ctrl\+F5 不进行调试运行解决方案。  
  
### 运行示例  
  
-   在 SDK 命令提示窗口中，运行 AdvancedPolicy\\bin\\debug 文件夹（对于该示例的 Visual Basic 版本为 AdvancedPolicy \\bin 文件夹）中的 .exe 文件，该文件夹位于该示例的主文件夹下。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Rules\Policy\AdvancedPolicy`  
  
## 请参阅  
 <xref:System.Workflow.Activities.Rules.RuleSet>   
 <xref:System.Workflow.Activities.PolicyActivity>   
 [简单策略](../../../../docs/framework/windows-workflow-foundation/samples/simple-policy.md)