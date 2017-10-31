---
title: "依赖项属性 | Microsoft Docs"
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
ms.assetid: 212cfb1e-cec4-4047-94a6-47209b387f6f
caps.latest.revision: 4
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 4
---
# 依赖项属性
依赖项属性 \(DP\) 是一个常规属性，而不是将其存储在类型变量 （字段），例如以属性存储中存储其值。  
  
 附加依赖项属性是一种建模为静态的 Get 和 Set 方法表示描述对象和其容器之间的关系的"属性"的依赖项属性 \(例如，位置 `Button` 对象 `Panel` 容器\)。  
  
 **✓ 执行** 提供的依赖项属性，如果您需要支持 WPF 功能，如样式、 触发器、 数据绑定、 动画、 动态资源和继承的属性。  
  
## 依赖项属性设计  
 **✓ 执行** 继承 <xref:System.Windows.DependencyObject>, ，或某个子类型，在实现依赖项属性时。 类型提供了一个非常有效的属性存储区实现，并且自动支持 WPF 数据绑定。  
  
 **✓ 执行** 提供常规 CLR 属性和公共的静态只读字段，存储的一个实例 <xref:System.Windows.DependencyProperty?displayProperty=fullName> 为每个依赖项属性。  
  
 **✓ 执行** 通过调用实例方法实现依赖项属性 <xref:System.Windows.DependencyObject.GetValue%2A?displayProperty=fullName> 和 <xref:System.Windows.DependencyObject.SetValue%2A?displayProperty=fullName>。  
  
 **✓ 执行** 通过添加后缀时会使用"属性"。 属性的名称来命名依赖项属性的静态字段  
  
 **X 不** 在代码中显式设置依赖项属性的默认值; 而是将它们设置在元数据中。  
  
 如果显式设置属性默认值，可能会阻止通过某些隐式方式，如样式设置该属性。  
  
 **X 不** 将代码放在属性访问器的标准代码以外，若要访问静态字段。  
  
 代码不会执行如果通过隐式方式，如样式，设置该属性，因为样式直接使用的静态字段。  
  
 **X 不** 使用依赖项属性来存储安全数据。 即使是专用的依赖项属性可公开访问。  
  
## 附加依赖项属性设计  
 在前面部分所述的依赖项属性表示声明类型; 内部的属性例如， `Text` 属性是属性的 `TextButton`, ，该声明。 一种特殊的依赖项属性是附加依赖项属性。  
  
 附加属性的一个典型示例是 <xref:System.Windows.Controls.Grid.Column%2A?displayProperty=fullName> 属性。 该属性表示按钮 （不网格的） 的列位置，但它才相关按钮包含在一个网格，以及因此它被"附加"到按钮的网格。  
  
```  
<Grid>  
    <Grid.ColumnDefinitions>  
        <ColumnDefinition />  
        <ColumnDefinition />  
    </Grid.ColumnDefinitions>  
  
    <Button Grid.Column="0">Click</Button>  
    <Button Grid.Column="1">Clack</Button>  
</Grid>  
```  
  
 附加属性的定义类似于主要的正则依赖项属性，只不过访问器的属性都是静态的 Get 和 Set 方法︰  
  
```  
public class Grid {  
  
    public static int GetColumn(DependencyObject obj) {  
        return (int)obj.GetValue(ColumnProperty);  
    }  
  
    public static void SetColumn(DependencyObject obj, int value) {  
        obj.SetValue(ColumnProperty,value);  
    }  
  
    public static readonly DependencyProperty ColumnProperty =  
        DependencyProperty.RegisterAttached(  
            "Column",  
            typeof(int),  
            typeof(Grid)  
    );  
}  
```  
  
## 依赖项属性验证  
 属性通常实现了称为验证。 在尝试更改一个属性的值时，将执行验证逻辑。  
  
 遗憾的是依赖项属性访问器不能包含任意验证代码。 相反，需要在注册过程中指定依赖项属性验证逻辑。  
  
 **X 不** 将依赖项属性的验证逻辑放入属性的访问器。 相反，传递验证回调到 `DependencyProperty.Register` 方法。  
  
## 依赖项属性更改通知  
 **X 不** 在依赖项属性访问器中实现更改通知逻辑。 依赖项属性都具有一种内置的更改通知功能，必须通过提供更改通知回调到使用 <xref:System.Windows.PropertyMetadata>。  
  
## 依赖项属性的值强制转换  
 属性强制转换时赋予属性 setter 的值被修改的 setter 属性存储实际修改之前发生。  
  
 **X 不** 在依赖项属性访问器中实现强制转换逻辑。  
  
 依赖项属性具有一个内置的强制转换的功能，且不能通过提供对强制回调用 `PropertyMetadata`。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)   
 [常见设计模式](../../../docs/standard/design-guidelines/common-design-patterns.md)