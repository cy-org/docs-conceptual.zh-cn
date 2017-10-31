---
title: "对成员进行重载 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "默认自变量"
  - "重载成员 [.NET Framework]"
  - "重载成员设计准则 [.NET Framework]"
  - "重载的成员"
  - "成员的签名"
ms.assetid: 964ba19e-8b94-4b5b-b1e3-5a0b531a0bb1
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# 对成员进行重载
成员重载意味着对具有相同类型的区别只在于的数量或类型参数，但具有相同的名称创建两个或多个成员。 例如，在下列情况 `WriteLine` 方法重载方法︰  
  
```  
public static class Console {  
    public void WriteLine();  
    public void WriteLine(string value);  
    public void WriteLine(bool value);  
    ...  
}  
  
```  
  
 因为只有方法、 构造函数和索引的属性可以具有参数，可以重载只有那些成员。  
  
 重载是一种最重要的技术有关提高易用性、 生产力和可重用库的可读性。 重载的参数的数量，使可以提供更简单的构造函数和方法的版本。 对参数类型重载使可以使用相同的成员执行相同操作对所选不同类型的成员名称。  
  
 **✓ 执行** 尝试使用描述性的参数名称以指示使用较短的重载的默认值。  
  
 **X 避免** 随意更改中重载的参数名称。 如果某一重载中的一个参数表示相同的输入中另一个重载的参数，参数应具有相同的名称。  
  
 **X 避免** 在排序中的参数中不一致状态重载成员。 具有相同名称的参数应出现在同一位置中的所有重载。  
  
 **✓ 执行** 使只有最长的重载变为虚拟方法 （如果可扩展性时才需要）。 只需较短的重载应调用通过向较长的重载。  
  
 **X 不** 使用 `ref` 或 `out` 修饰符来重载成员。  
  
 某些语言中无法解析对此类的重载的调用。 此外，此类重载通常具有完全不同的语义和可能不应为重载，但两个单独的方法相反。  
  
 **X 不** 具有重载随着参数在相同的位置以及类似的类型而具有不同语义。  
  
 **✓ 执行**  允许 `null` 为可选参数传递。  
  
 **✓ 执行** 使用重载，而不是定义具有默认参数的成员的成员。  
  
 默认参数也不符合 CLS。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [成员设计准则](../../../docs/standard/design-guidelines/member.md)   
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)