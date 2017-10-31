---
title: "规范函数映射的 CLR 方法 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: e3363261-2cb8-4b54-9555-2870be99b929
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 规范函数映射的 CLR 方法
实体框架提供了一组规范函数（如字符串操作函数和数学函数），这些函数可以实现很多数据库系统通用的功能。  这使开发人员可以面向广泛的数据库系统。  通过查询技术（如 LINQ to Entities）调用时，这些规范函数将转换为要使用的提供程序的相应正确存储区函数。  这样，可以用一种数据源通用的形式表示函数调用，从而在数据源之间提供一致的查询体验。  如果操作数是数值类型，则按位 AND、OR、NOT 和 XOR 运算符也将映射到规范函数。对于布尔操作数，按位 AND、OR、NOT 和 XOR 运算符将计算其操作数的逻辑 AND、OR、NOT 和 XOR 运算。  有关详细信息，请参阅[规范函数](../../../../../../docs/framework/data/adonet/ef/language-reference/canonical-functions.md)。  
  
 对于 LINQ 方案，对实体框架执行的查询涉及通过规范函数将某些 CLR 方法映射到基础数据源的方法。  LINQ to Entities 查询中未显式映射到规范函数的任何方法调用都会导致引发运行时 <xref:System.NotSupportedException> 异常。  
  
## System.String 方法（静态）映射  
  
|System.String 方法（静态）|规范函数|  
|--------------------------|----------|  
|System.String Concat\(String `str0`, String `str1`\)|Concat\(`str0`, `str1`\)|  
|System.String Concat\(String `str0`, String `str1`, String `str2`\)|Concat\(Concat\(`str0`, `str1`\), `str2`\)|  
|System.String Concat\(String `str0`, String `str1`, String `str2`, String `str03`\)|Concat\(Concat\(Concat\(`str0`, `str1`\), `str2`\), `str3`\)|  
|Boolean Equals\(String `a`, String `b`\)|\= 运算符|  
|Boolean IsNullOrEmpty\(String `value`\)|\(IsNull\(`value`\)\) OR Length\(`value`\) \= 0|  
|Boolean op\_Equality\(String `a`, String `b`\)|\= 运算符|  
|Boolean op\_Inequality\(String `a` , String `b`\)|\!\= 运算符|  
|Microsoft.VisualBasic.Strings.Trim\(String `str`\)|Trim\(`str`\)|  
|Microsoft.VisualBasic.Strings.LTrim\(String `str`\)|Ltrim\(`str`\)|  
|Microsoft.VisualBasic.Strings.RTrim\(String `str`\)|Rtrim\(`str`\)|  
|Microsoft.VisualBasic.Strings.Len\(String `expression`\)|Length\(`expression`\)|  
|Microsoft.VisualBasic.Strings.Left\(String `str`, Int32 `Length`\)|Left\(`str`, `Length`\)|  
|Microsoft.VisualBasic.Strings.Mid\(String `str`, Int32 `Start`, Int32 `Length`\)|Substring\(`str`, `Start`, `Length`\)|  
|Microsoft.VisualBasic.Strings.Right\(String `str`, Int32 `Length`\)|Right\(`str`, `Length`\)|  
|Microsoft.VisualBasic.Strings.UCase\(String `Value`\)|ToUpper\(`Value`\)|  
|Microsoft.VisualBasic.Strings.LCase\(String Value\)|ToLower\(`Value`\)|  
  
## System.String 方法（实例）映射  
  
|System.String 方法（实例）|规范函数|备注|  
|--------------------------|----------|--------|  
|Boolean Contains\(String `value`\)|`this` LIKE '%`value`%'|如果 `value` 不是常量，则它映射到 IndexOf\(`this`, `value`\) \> 0|  
|Boolean EndsWith\(String `value`\)|`this` LIKE `'`%`value`'|如果 `value` 不是常量，则它映射到 Right\(`this`, length\(`value`\)\) \= `value`。|  
|Boolean StartsWith\(String `value`\)|`this` LIKE '`value`%'|如果 `value` 不是常量，则它映射到 IndexOf\(`this`, `value`\) \= 1。|  
|长度|Length\(`this`\)||  
|Int32 IndexOf\(String `value`\)|IndexOf\(`this`, `value`\) \- 1||  
|System.String Insert\(Int32 `startIndex`, String `value`\)|Concat\(Concat\(Substring\(`this`, 1, `startIndex`\), `value`\), Substring\(`this`, `startIndex`\+1, Length\(`this`\) \- `startIndex`\)\)||  
|System.String Remove\(Int32 `startIndex`\)|Substring\(`this`, 1, `startIndex`\)||  
|System.String Remove\(Int32 `startIndex`, Int32 `count`\)|Concat\(Substring\(`this`, 1, `startIndex`\) , Substring\(`this`, `startIndex` \+ `count` \+1, Length\(`this`\) \- \(`startIndex` \+ `count`\)\)\)|Remove\(`startIndex`, `count`\) 仅在 `count` 是大于或等于 0 的整数时才受支持。|  
|System.String Replace\(String `oldValue`, String `newValue`\)|Replace\(`this`, `oldValue`, `newValue`\)||  
|System.String Substring\(Int32 `startIndex`\)|Substring\(`this`, `startIndex` \+1, Length\(`this`\) \- `startIndex`\)||  
|System.String Substring\(Int32 `startIndex`, Int32 `length`\)|Substring\(`this`, `startIndex` \+1, `length`\)||  
|System.String ToLower\(\)|ToLower\(`this`\)||  
|System.String ToUpper\(\)|ToUpper\(`this`\)||  
|System.String Trim\(\)|Trim\(`this`\)||  
|System.String TrimEnd\(Char\[\] `trimChars`\)|RTrim\(`this`\)||  
|System.String TrimStart\(Char\[\]`trimChars`\)|LTrim\(`this`\)||  
|Boolean Equals\(String `value`\)|\= 运算符||  
  
## System.DateTime 方法（静态）映射  
  
|System.DateTime 方法（静态）|规范函数|备注|  
|----------------------------|----------|--------|  
|Boolean Equals\(DateTime `t1`, DateTime `t2`\)|\= 运算符||  
|System.DateTime.Now|CurrentDateTime\(\)||  
|System.DateTime.UtcNow|CurrentUtcDateTime\(\)||  
|Boolean op\_Equality\(DateTime `d1`, DateTime `d2`\)|\= 运算符||  
|Boolean op\_GreaterThan\(DateTime `t1`, DateTime `t2`\)|\> 运算符||  
|Boolean op\_GreaterThanOrEqual\(DateTime `t1`, DateTime `t2`\)|\>\= 运算符||  
|Boolean op\_Inequality\(DateTime `t1`, DateTime `t2`\)|\!\= 运算符||  
|Boolean op\_LessThan\(DateTime `t1`, DateTime `t2`\)|\< 运算符||  
|Boolean op\_LessThanOrEqual\(DateTime `t1`, DateTime `t2`\)|\<\= 运算符||  
|Microsoft.VisualBasic.DateAndTime.DatePart\( \_<br /><br /> ByVal `Interval` As DateInterval, \_<br /><br /> ByVal `DateValue` As DateTime, \_<br /><br /> Optional ByVal `FirstDayOfWeekValue` As FirstDayOfWeek \= VbSunday, \_<br /><br /> Optional ByVal `FirstWeekOfYearValue` As FirstWeekOfYear \= VbFirstJan1 \_<br /><br /> \) As Integer||有关详细信息，请参见“DatePart 函数”部分。|  
|Microsoft.VisualBasic.DateAndTime.Now|CurrentDateTime\(\)||  
|Microsoft.VisualBasic.DateAndTime.Year\(DateTime `TimeValue`\)|Year\(\)||  
|Microsoft.VisualBasic.DateAndTime.Month\(DateTime `TimeValue`\)|Month\(\)||  
|Microsoft.VisualBasic.DateAndTime.Day\(DateTime `TimeValue`\)|Day\(\)||  
|Microsoft.VisualBasic.DateAndTime.Hour\(DateTime `TimeValue`\)|Hour\(\)||  
|Microsoft.VisualBasic.DateAndTime.Minute\(DateTime `TimeValue`\)|Minute\(\)||  
|Microsoft.VisualBasic.DateAndTime.Second\(DateTime `TimeValue`\)|Second\(\)||  
  
## System.DateTime 方法（实例）映射  
  
|System.DateTime 方法（实例）|规范函数|  
|----------------------------|----------|  
|Boolean Equals\(DateTime `value`\)|\= 运算符|  
|天|Day\(`this`\)|  
|小时|Hour\(`this`\)|  
|毫秒|Millisecond\(`this`\)|  
|分钟|Minute\(`this`\)|  
|月份|Month\(`this`\)|  
|秒|Second\(`this`\)|  
|年|Year\(`this`\)|  
  
## System.DateTimeOffset 方法（实例）映射  
 针对列出的属性上 `get` 方法显示的映射。  
  
|System.DateTimeOffset 方法（实例）|规范函数|备注|  
|----------------------------------|----------|--------|  
|天|Day\(`this`\)|对 SQL Server 2005 不支持。|  
|小时|Hour\(`this`\)|对 SQL Server 2005 不支持。|  
|毫秒|Millisecond\(`this`\)|对 SQL Server 2005 不支持。|  
|分钟|Minute\(`this`\)|对 SQL Server 2005 不支持。|  
|月份|Month\(`this`\)|对 SQL Server 2005 不支持。|  
|秒|Second\(`this`\)|对 SQL Server 2005 不支持。|  
|年|Year\(`this`\)|对 SQL Server 2005 不支持。|  
  
> [!NOTE]
>  如果比较的 <xref:System.DateTimeOffset> 对象相等，则 <xref:System.DateTimeOffset.Equals%2A> 方法返回 `true`；否则返回 `false`。  <xref:System.DateTimeOffset.CompareTo%2A> 方法返回 0、1 或 \-1，分别取决于比较的 <xref:System.DateTimeOffset> 对象是相等、大于还是小于。  
  
## System.DateTimeOffset  
 针对列出的属性上 `get` 方法显示的映射。  
  
|System.DateTimeOffset|规范函数|备注|  
|---------------------------|----------|--------|  
|System.DateTimeOffset.Now\(\)|CurrentDateTimeOffset\(\)|对 SQL Server 2005 不支持。|  
  
## System.TimeSpan  
 针对列出的属性上 `get` 方法显示的映射。  
  
|System.TimeSpan 方法（实例）|规范函数|备注|  
|----------------------------|----------|--------|  
|小时|Hour\(`this`\)|对 SQL Server 2005 不支持。|  
|毫秒|Millisecond\(`this`\)|对 SQL Server 2005 不支持。|  
|分钟|Minute\(`this`\)|对 SQL Server 2005 不支持。|  
|秒|Second\(`this`\)|对 SQL Server 2005 不支持。|  
  
> [!NOTE]
>  如果比较的 <xref:System.TimeSpan> 对象相等，则 <xref:System.TimeSpan.Equals%2A> 方法返回 `true`；否则返回 `false`。  <xref:System.TimeSpan.CompareTo%2A> 方法返回 0、1 或 \-1，分别取决于比较的 <xref:System.TimeSpan> 对象是相等、大于还是小于。  
  
### DatePart  
 `DatePart` 函数根据 `Interval` 的值映射到几个不同规范函数中的一个。  下表列出了受支持的 `Interval` 值的规范函数映射。  
  
|Interval 值|规范函数|  
|----------------|----------|  
|DateInterval.Year|Year\(\)|  
|DateInterval.Month|Month\(\)|  
|DateInterval.Day|Day\(\)|  
|DateInterval.Hour|Hour\(\)|  
|DateInterval.Minute|Minute\(\)|  
|DateInterval.Second|Second\(\)|  
  
## 数学函数映射  
  
|CLR 方法|规范函数|  
|------------|----------|  
|System.Decimal.Ceiling\(Decimal `d`\)|Ceiling\(`d`\)|  
|System.Decimal.Floor\(Decimal `d`\)|Floor\(`d`\)|  
|System.Decimal.Round\(Decimal `d`\)|Round\(`d`\)|  
|System.Math.Ceiling\(Decimal `d`\)|Ceiling\(`d`\)|  
|System.Math.Floor\(Decimal `d`\)|Floor\(`d`\)|  
|System.Math.Round\(Decimal `d`\)|Round\(`d`\)|  
|System.Math.Ceiling\(Double `a`\)|Ceiling\(`a`\)|  
|System.Math.Floor\(Double `a`\)|Floor\(`a`\)|  
|System.Math.Round\(Double `a`\)|Round\(`a`\)|  
|System.Math.Round\(Double 值, Int16 位数\)|Round\(值, 位数\)|  
|System.Math.Round\(Double 值, Int32 位数\)|Round\(值, 位数\)|  
|System.Math.Round\(Decimal 值, Int16 位数\)|Round\(值, 位数\)|  
|System.Math.Round\(Decimal 值, Int32, 位数\)|Round\(值, 位数\)|  
|System.Math.Abs\(Int16 值\)|Abs\(value\)|  
|System.Math.Abs\(Int32 值\)|Abs\(value\)|  
|System.Math.Abs\(Int64 值\)|Abs\(value\)|  
|System.Math.Abs\(Byte 值\)|Abs\(value\)|  
|System.Math.Abs\(Single 值\)|Abs\(value\)|  
|System.Math.Abs\(Double 值\)|Abs\(value\)|  
|System.Math.Abs\(Decimal 值\)|Abs\(value\)|  
|System.Math.Truncate\(Double 值, Int16 位数\)|Truncate\(值, 位数\)|  
|System.Math.Truncate\(Double 值, Int32 位数\)|Truncate\(值, 位数\)|  
|System.Math.Truncate\(Decimal 值, Int16 位数\)|Truncate\(值, 位数\)|  
|System.Math.Truncate\(Decimal 值, Int32 位数\)|Truncate\(值, 位数\)|  
|System.Math.Power\(Int32 值, Int64 指数\)|Power\(值, 指数\)|  
|System.Math.Power\(Int32 值, Double 指数\)|Power\(值, 指数\)|  
|System.Math.Power\(Int32 值, Decimal 指数\)|Power\(值, 指数\)|  
|System.Math.Power\(Int64 值, Int64 指数\)|Power\(值, 指数\)|  
|System.Math.Power\(Int64 值, Double 指数\)|Power\(值, 指数\)|  
|System.Math.Power\(Int64 值, Decimal 指数\)|Power\(值, 指数\)|  
|System.Math.Power\(Double 值, Int64 指数\)|Power\(值, 指数\)|  
|System.Math.Power\(Double 值, Double 指数\)|Power\(值, 指数\)|  
|System.Math.Power\(Double 值, Decimal 指数\)|Power\(值, 指数\)|  
|System.Math.Power\(Decimal 值, Int64 指数\)|Power\(值, 指数\)|  
|System.Math.Power\(Decimal 值, Double 指数\)|Power\(值, 指数\)|  
|System.Math.Power\(Decimal 值, Decimal 指数\)|Power\(值, 指数\)|  
  
## 位运算符映射  
  
|位运算符|非布尔操作数的规范函数|布尔操作数的规范函数|  
|----------|-----------------|----------------|  
|位 AND 运算符|BitWiseAnd|op1 AND op2|  
|位 OR 运算符|BitWiseOr|op1 OR op2|  
|位 NOT 运算符|BitWiseNot|NOT\(op\)|  
|位 XOR 运算符|BitWiseXor|\(\(op1 AND NOT\(op2\)\) OR \(NOT\(op1\) AND op2\)\)|  
  
## 其他映射  
  
|方法|规范函数|  
|--------|----------|  
|Guid.NewGuid\(\)|NewGuid\(\)|  
  
## 请参阅  
 [LINQ to Entities](../../../../../../docs/framework/data/adonet/ef/language-reference/linq-to-entities.md)