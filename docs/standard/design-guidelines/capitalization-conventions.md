---
title: "大小写约定 | Microsoft Docs"
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
  - "camel 大小写格式名称 [.NET Framework]"
  - "类库设计准则 [.NET Framework] 的大小写"
  - "Pascal 大小写名称 [.NET Framework]"
  - "区分大小写约定"
  - "大小写的名称 [.NET Framework]"
ms.assetid: 4c4ea526-9203-486f-b72d-29d61c5b3c6d
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 16
---
# 大小写约定
简单的方法来使用此章布局中的准则所大小写时一致地应用类型、 成员和参数易读的生成标识符。  
  
## 标识符的大小写规则  
 若要区分在标识符中的单词，改为在标识符中的每个单词的首字母大写。 不使用下划线来区分的单词，或就此而言，在标识符中的任意位置。 有两种适当的方法，以使其大写标识符，具体取决于标识符的使用︰  
  
-   PascalCasing  
  
-   camelcasing 大小写约定  
  
 用于除参数名称之外，所有标识符的 PascalCasing 约定转换成大写 （其中包括通过的长度的两个字母的首字母缩写词） 的每个单词的第一个字符，如下面的示例中所示︰  
  
 `PropertyDescriptor`   
 `HtmlTag`  
  
 一种特殊情况专为这两个字母都大写的两个字母缩写词，如以下标识符中所示︰  
  
 `IOStream`  
  
 CamelCasing 约定，参数名称仅用于转换成大写除第一个单词，每个单词的第一个字符，如下面的示例中所示。 如该示例还演示，开始驼峰式大小写的标识符的两个字母缩写词都小写。  
  
 `propertyDescriptor`   
 `ioStream`   
 `htmlTag`  
  
 **✓ 执行** PascalCasing 用于所有的公共成员、 类型和命名空间名称，由多个单词组成。  
  
 **✓ 执行** 参数名称中使用 camelcasing 大小写约定。  
  
 下表描述不同类型的标识符的大小写规则。  
  
|标识符|大小写|示例|  
|---------|---------|--------|  
|命名空间|Pascal|`namespace System.Security { ... }`|  
|类型|Pascal|`public class StreamReader { ... }`|  
|接口|Pascal|`public interface IEnumerable { ... }`|  
|方法|Pascal|`public class Object {` <br />  `public virtual string ToString();` <br /> `}`|  
|属性|Pascal|`public class String {` <br />  `public int Length { get; }` <br /> `}`|  
|Event|Pascal|`public class Process {` <br />  `public event EventHandler Exited;` <br /> `}`|  
|字段|Pascal|`public class MessageQueue {` <br />  `public static readonly TimeSpan` <br /> `InfiniteTimeout;` <br /> `}` <br /> `public struct UInt32 {` <br />  `public const Min = 0;` <br /> `}`|  
|枚举值|Pascal|`public enum FileMode {` <br />  `Append,` <br />  `...` <br /> `}`|  
|参数|Camel|`public class Convert {` <br />  `public static int ToInt32(string value);` <br /> `}`|  
  
## 利用复合词和常用术语  
 大多数复合字词被视为单个词出于的大小写。  
  
 **X 不** 每个单词的所谓关闭窗体复合词大写。  
  
 这些是写成单个字词，如终结点的组合词。 大小写规则，以便将关闭格式的复合词视为一个单词。 使用最新的词典来确定是否在关闭窗体中写入的组合词。  
  
|Pascal|Camel|不|  
|------------|-----------|-------|  
|`BitFlag`|`bitFlag`|`Bitflag`|  
|`Callback`|`callback`|`CallBack`|  
|`Canceled`|`canceled`|`Cancelled`|  
|`DoNot`|`doNot`|`Don't`|  
|`Email`|`email`|`EMail`|  
|`Endpoint`|`endpoint`|`EndPoint`|  
|`FileName`|`fileName`|`Filename`|  
|`Gridline`|`gridline`|`GridLine`|  
|`Hashtable`|`hashtable`|`HashTable`|  
|`Id`|`id`|`ID`|  
|`Indexes`|`indexes`|`Indices`|  
|`LogOff`|`logOff`|`LogOut`|  
|`LogOn`|`logOn`|`LogIn`|  
|`Metadata`|`metadata`|`MetaData, metaData`|  
|`Multipanel`|`multipanel`|`MultiPanel`|  
|`Multiview`|`multiview`|`MultiView`|  
|`Namespace`|`namespace`|`NameSpace`|  
|`Ok`|`ok`|`OK`|  
|`Pi`|`pi`|`PI`|  
|`Placeholder`|`placeholder`|`PlaceHolder`|  
|`SignIn`|`signIn`|`SignOn`|  
|`SignOut`|`signOut`|`SignOff`|  
|`UserName`|`userName`|`Username`|  
|`WhiteSpace`|`whiteSpace`|`Whitespace`|  
|`Writable`|`writable`|`Writeable`|  
  
## 区分大小写  
 可以在 CLR 运行的语言不支持所需区分大小写，尽管某些作用。 即使您的语言支持，不这样做可能会访问您的框架其他语言。 因此，任何 Api 时从外部访问，不能依赖于用例来区分同一上下文中的两个名称。  
  
 **X 不** 假定所有编程语言都是区分大小写。 它们不是。 名称不能通过大小写来区分。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)   
 [命名准则](../../../docs/standard/design-guidelines/naming-guidelines.md)