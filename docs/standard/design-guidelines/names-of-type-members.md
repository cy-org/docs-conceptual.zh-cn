---
title: "类型成员的名称 | Microsoft Docs"
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
  - "名称的事件 [.NET Framework]"
  - "名称的方法 [.NET Framework]"
  - "类型成员"
  - "名称的属性 [.NET Framework]"
  - "字段名称"
  - "字段名称"
  - "类型成员的名称 [.NET Framework]"
  - "类型的成员 [.NET Framework]"
ms.assetid: af5a0903-36af-4c2a-b848-cf959affeaa5
caps.latest.revision: 10
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 10
---
# 类型成员的名称
成员进行类型︰ 方法、 属性、 事件、 构造函数和字段。 以下各节描述了命名类型成员的准则。  
  
## 方法的名称  
 由于方法都是执行操作的方法，但设计准则需要方法名称是动词或动词短语。 也遵循这一准则可用于将方法名称与属性和类型名，即名词、 形容词短语区分开来。  
  
 **✓ 执行** 属于谓词或谓词短语方法的名称。  
  
```  
public class String {  
    public int CompareTo(...);  
    public string[] Split(...);  
    public string Trim();  
}  
  
```  
  
## 属性的名称  
 与其他成员不同名词短语或形容词名称，则应提供属性。 这是因为属性是指数据，而且属性的名称将反映的。 PascalCasing 始终用于属性名称。  
  
 **✓ 执行** 用名词、 名词短语或形容词命名属性。  
  
 **X 不** 具有如下面的示例所示的"Get"方法的名称匹配的属性︰  
  
 `public string TextWriter { get {...} set {...} }`   
 `public string GetTextWriter(int value) { ... }`  
  
 此模式通常指示该属性实际上应为一种方法。  
  
 **✓ 执行** 名称采用复数形式的词描述而不是使用单数短语后跟"List"或"集合"。 集合中的项集合的属性  
  
 **✓ 执行** 命名具有赞成短语的布尔值属性 \(`CanSeek` 而不是 `CantSeek`\)。 （可选） 还前缀布尔型属性与"是"，"可以"或"有，"但这仅在它增添价值。  
  
 **✓ 请考虑** 指定相同的名称作为其类型的属性。  
  
 例如，下面的属性正确地获取和设置名为枚举值 `Color`, ，因此该属性名为 `Color`:  
  
```  
public enum Color {...}  
public class Control {  
    public Color Color { get {...} set {...} }  
}  
```  
  
## 事件的名称  
 始终引用某一操作，是指位于发生或发生了一个事件。 因此，与方法一样，事件名称中带有谓词，并且谓词时态用于指示当引发该事件的时间。  
  
 **✓ 执行** 命名为谓词或谓词短语与事件。  
  
 示例包括 `Clicked`, ，`Painting`, ，`DroppedDown`, ，依次类推。  
  
 **✓ 执行** 的列名事件的概念与之前和之后，使用当前和过去时态。  
  
 例如，将调用前关闭了窗口引发的关闭事件 `Closing`, ，并将调用该窗口关闭之后，将引发的其中一个 `Closed`。  
  
 **X 不** 使用"Before"或"After"前缀或 postfixes 以指示预和后期事件。 并使用已存在过去时态刚才介绍的那样。  
  
 **✓ 执行** 以"事件处理程序"后缀命名事件处理程序 （用作事件类型的委托），如下面的示例中所示︰  
  
 `public delegate void ClickedEventHandler(object sender, ClickedEventArgs e);`  
  
 **✓ 执行** 使用两个参数名为 `sender` 和 `e` 事件处理程序中。  
  
 发件人参数表示引发事件的对象。 发件人参数的类型通常是 `object`, ，即使它也可使用更具体的类型。  
  
 **✓ 执行** 命名事件参数类与"EventArgs"后缀。  
  
## 字段的名称  
 字段命名准则适用于公共和受保护的静态字段。 内部和私有字段均未覆盖的指南，以及公共或受保护实例字段都不允许的 [成员设计准则](../../../docs/standard/design-guidelines/member.md)。  
  
 **✓ 执行** 在字段名称中使用 PascalCasing。  
  
 **✓ 执行** 命名字段使用名词、 名词短语或形容词。  
  
 **X 不** 字段名称中使用前缀。  
  
 例如，不要使用"g\_"或"s\_"来指示的静态字段。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)   
 [命名准则](../../../docs/standard/design-guidelines/naming-guidelines.md)