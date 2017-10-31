---
title: "运算符重载 | Microsoft Docs"
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
  - "重载的运算符 [.NET Framework]"
  - "名称 [.NET Framework] 重载运算符"
  - "成员设计准则操作员"
  - "重载运算符"
ms.assetid: 37585bf2-4c27-4dee-849a-af70e3338cc1
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# 运算符重载
运算符重载允许起来就像内置语言基元的框架类型。  
  
 虽然允许并且在某些情况下很有用，但应谨慎使用运算符重载。 有很多情况下在哪种运算符重载具有已被滥用，如框架设计器启动时若要使用的操作，应该是简单的方法的运算符。 以下准则可帮助您决定何时以及如何使用运算符重载。  
  
 **X 避免** 除定义运算符重载，就好像基元 （内置） 类型的类型中。  
  
 **✓ 请考虑** 中一种类型，就好像基元类型定义运算符重载。  
  
 例如， <xref:System.String?displayProperty=fullName> 具有 `operator==` 和 `operator!=` 定义。  
  
 **✓ 执行** 中表示的数字的结构定义运算符重载 \(如 <xref:System.Decimal?displayProperty=fullName>\)。  
  
 **X 不** 过于刻意定义运算符重载时。  
  
 运算符重载是的可在其中非常直观操作的结果将是非常有用。 例如，最好能够中减去 1 <xref:System.DateTime> 从另一个 `DateTime` 并获取 <xref:System.TimeSpan>。 但是，不适合使用逻辑 union 运算符来联合两个数据库查询，或使用移位运算符要写入到流。  
  
 **X 不** 提供运算符重载除非至少其中一个操作数的类型定义重载。  
  
 **✓ 执行** 对称方式重载运算符。  
  
 例如，如果您重载 `operator==`, ，还应重载 `operator!=`。 同样，如果重载 `operator<`, ，还应重载 `operator>`, ，依次类推。  
  
 **✓ 请考虑** 与每个重载运算符的方法提供相对应的友好名称。  
  
 许多语言不支持运算符重载。 出于此原因，建议重载运算符的类型包括具有恰当的特定于域的名称，它提供等效功能的辅助方法。  
  
 下表列出的运算符和相应的友好的方法名称。  
  
|C\# 运算符符号|元数据名称|友好名称|  
|---------------|-----------|----------|  
|`N/A`|`op_Implicit`|`To<TypeName>/From<TypeName>`|  
|`N/A`|`op_Explicit`|`To<TypeName>/From<TypeName>`|  
|`+ (binary)`|`op_Addition`|`Add`|  
|`- (binary)`|`op_Subtraction`|`Subtract`|  
|`* (binary)`|`op_Multiply`|`Multiply`|  
|`/`|`op_Division`|`Divide`|  
|`%`|`op_Modulus`|`Mod or Remainder`|  
|`^`|`op_ExclusiveOr`|`Xor`|  
|`& (binary)`|`op_BitwiseAnd`|`BitwiseAnd`|  
|`&#124;`|`op_BitwiseOr`|`BitwiseOr`|  
|`&&`|`op_LogicalAnd`|`And`|  
|`&#124;&#124;`|`op_LogicalOr`|`Or`|  
|`=`|`op_Assign`|`Assign`|  
|`<<`|`op_LeftShift`|`LeftShift`|  
|`>>`|`op_RightShift`|`RightShift`|  
|`N/A`|`op_SignedRightShift`|`SignedRightShift`|  
|`N/A`|`op_UnsignedRightShift`|`UnsignedRightShift`|  
|`==`|`op_Equality`|`Equals`|  
|`!=`|`op_Inequality`|`Equals`|  
|`>`|`op_GreaterThan`|`CompareTo`|  
|`<`|`op_LessThan`|`CompareTo`|  
|`>=`|`op_GreaterThanOrEqual`|`CompareTo`|  
|`<=`|`op_LessThanOrEqual`|`CompareTo`|  
|`*=`|`op_MultiplicationAssignment`|`Multiply`|  
|`-=`|`op_SubtractionAssignment`|`Subtract`|  
|`^=`|`op_ExclusiveOrAssignment`|`Xor`|  
|`<<=`|`op_LeftShiftAssignment`|`LeftShift`|  
|`%=`|`op_ModulusAssignment`|`Mod`|  
|`+=`|`op_AdditionAssignment`|`Add`|  
|`&=`|`op_BitwiseAndAssignment`|`BitwiseAnd`|  
|`&#124;=`|`op_BitwiseOrAssignment`|`BitwiseOr`|  
|`,`|`op_Comma`|`Comma`|  
|`/=`|`op_DivisionAssignment`|`Divide`|  
|`--`|`op_Decrement`|`Decrement`|  
|`++`|`op_Increment`|`Increment`|  
|`- (unary)`|`op_UnaryNegation`|`Negate`|  
|`+ (unary)`|`op_UnaryPlus`|`Plus`|  
|`~`|`op_OnesComplement`|`OnesComplement`|  
  
### 重载运算符 \= \=  
 重载 `operator ==` 非常复杂。 运算符的语义需要符合几个其他成员，如 <xref:System.Object.Equals%2A?displayProperty=fullName>。  
  
### 转换运算符  
 转换运算符是一元运算符，从而允许从一种类型到另一个转换。 必须为静态成员的操作数或返回类型定义运算符。 有两种类型的转换运算符︰ 隐式和显式。  
  
 **X 不** 如果最终用户未明确要求这样的转换提供转换运算符。  
  
 **X 不** 定义类型的域之外的转换运算符。  
  
 例如， <xref:System.Int32>, ，<xref:System.Double>, ，和 <xref:System.Decimal> 是所有数值类型，而 <xref:System.DateTime> 不是。 因此，应该有没有转换运算符以转换 `Double(long)` 到 `DateTime`。 这种情况下被首选构造函数。  
  
 **X 不** 提供隐式转换运算符，如果转换，则可能丢失信息。  
  
 例如，应该不存在隐式转换 `Double` 到 `Int32` 因为 `Double` 比后者具有更宽范围 `Int32`。 可以提供显式转换运算符，即使转换，则可能丢失信息。  
  
 **X 不** 从隐式强制转换引发异常。  
  
 它是很难使最终用户可了解发生了什么情况，因为它们可能不知道正在进行转换。  
  
 **✓ 执行** 引发 <xref:System.InvalidCastException?displayProperty=fullName> 如果强制转换运算符的调用将导致有损转换和运算符的协定不允许丢失数据的转换。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [成员设计准则](../../../docs/standard/design-guidelines/member.md)   
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)