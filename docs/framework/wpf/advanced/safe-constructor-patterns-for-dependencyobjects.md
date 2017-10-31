---
title: "DependencyObject 的安全构造函数模式 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "依赖性对象的构造函数模式"
  - "依赖性对象, 构造函数模式"
  - "FXCop 工具"
ms.assetid: f704b81c-449a-47a4-ace1-9332e3cc6d60
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# DependencyObject 的安全构造函数模式
通常，类构造函数不应调用诸如虚方法或委托等的回调，其原因是构造函数可作为派生类构造函数的基本初始化进行调用。  输入该虚拟的操作可能会在任何给定对象的不完全初始化状态下进行。  但是，属性系统本身在内部调用并公开回调，作为依赖项属性系统的一部分。  类似使用 <xref:System.Windows.DependencyObject.SetValue%2A> 调用设置依赖项属性值等的简单操作就可能包含某处确认中的回调。  因此，当在构造函数体内设置依赖项属性值（如果将您的类型用作基类，这可能会有问题）时应保持谨慎。  存在一种特定的模式，用以实现可避免依赖项属性状态和内在回调特定问题的 <xref:System.Windows.DependencyObject> 构造函数，此处对其进行了说明。  
  
   
  
<a name="Property_System_Virtual_Methods"></a>   
## 属性系统虚方法  
 可能会在对设置依赖项属性值的 <xref:System.Windows.DependencyObject.SetValue%2A> 调用进行计算的期间调用以下虚方法或回调：<xref:System.Windows.ValidateValueCallback>、<xref:System.Windows.PropertyChangedCallback>、<xref:System.Windows.CoerceValueCallback>、<xref:System.Windows.DependencyObject.OnPropertyChanged%2A>。  这些虚方法或回调中的每一个在扩展 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 属性系统和依赖项属性的多样性方面都具有特定的用途。  有关如何使用这些虚方法以自定义属性值确定的更多信息，请参见[依赖项属性回调和验证](../../../../docs/framework/wpf/advanced/dependency-property-callbacks-and-validation.md)。  
  
### FXCop 规则强制与属性系统虚方法  
 如果使用 Microsoft 工具 FXCop 作为生成过程的一部分，并从某些调用基构造函数的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 框架类派生或在派生的类上实现自己的依赖项属性，则可能会遇到特定的 FXCop 规则冲突。  此冲突的名称字符串为：  
  
 `DoNotCallOverridableMethodsInConstructors`  
  
 这一规则是为 FXCop 设置的默认公共规则的一部分。  此规则报告的内容可能是对最终调用依赖项属性系统虚方法的依赖项属性系统的跟踪。  即使遵循了本主题中介绍的建议构造函数模式之后，此规则冲突也可能会继续出现，因此可能需要在 FXCop 规则设置配置中禁用或禁止该规则。  
  
### 大多数问题的原因在于派生类，而不是使用现有的类  
 当使用虚方法在其构造序列中实现的类随后被派生时发生此规则报告的问题。  如果您密封了类，或者了解或强制您的类不会被派生，则此处介绍的注意事项和激发 FXCop 规则的问题将不适用于您。  但是，如果按照打算将类用作基类的方式创作类，例如，如果正创建模板或可扩展的控件库集，则您应遵循此处建议的构造函数的模式。  
  
### 默认构造函数必须初始化回调请求的所有值  
 您的类重写或回调（从“属性系统虚拟”部分中的列表中的回调）使用的任何实例成员必须在您的类的默认构造函数中进行初始化，即使其中的某些值已由“实际”值通过非默认构造函数的参数填充时也是如此。  
  
 以下代码示例（和后面的示例）是一个与此规则冲突的伪 C\# 示例并对该问题进行了说明：  
  
```  
public class MyClass : DependencyObject  
{  
    public MyClass() {}  
    public MyClass(object toSetWobble)  
        : this()  
    {  
        Wobble = toSetWobble; //this is backed by a DependencyProperty  
        _myList = new ArrayList();    // this line should be in the default ctor  
    }  
    public static readonly DependencyProperty WobbleProperty =   
        DependencyProperty.Register("Wobble", typeof(object), typeof(MyClass));  
    public object Wobble  
    {  
        get { return GetValue(WobbleProperty); }  
        set { SetValue(WobbleProperty, value); }  
    }  
    protected override void OnPropertyChanged(DependencyPropertyChangedEventArgs e)  
    {  
        int count = _myList.Count;    // null-reference exception  
    }  
    private ArrayList _myList;  
}  
```  
  
 当应用程序代码调用 `new MyClass(objectvalue)` 时，这将调用默认构造函数和基类构造函数。  然后它设置 `Property1 = object1`，这将对所属 `MyClass` <xref:System.Windows.DependencyObject> 调用虚方法 `OnPropertyChanged`。  重写指向尚未初始化的 `_myList`。  
  
 避免这些问题的一个方法是：确保回调仅使用其他依赖项属性，并且每个这样的依赖项属性都有一个确立的默认值作为其注册元数据的一部分。  
  
<a name="Safe_Constructor_Patterns"></a>   
## 安全构造函数模式  
 若要在类用作基类的情况下避免未完全初始化的危险，请遵循以下模式：  
  
#### 调用基本初始化的默认构造函数  
 实现以下调用基默认值的构造函数：  
  
```  
public MyClass : SomeBaseClass {  
    public MyClass() : base() {  
        // ALL class initialization, including initial defaults for   
        // possible values that other ctors specify or that callbacks need.  
    }  
}  
```  
  
#### 非默认（方便）构造函数，不与任何基签名匹配  
 如果这些构造函数使用参数来设置初始化中的依赖项属性，首先应为初始化调用自己的类默认构造函数，然后使用参数设置依赖项属性。  这些可能是您的类定义的依赖项属性，也可能是从基类继承的依赖项属性，但是两者中的任何一种情况都使用以下模式：  
  
```  
public MyClass : SomeBaseClass {  
    public MyClass(object toSetProperty1) : this() {  
        // Class initialization NOT done by default.  
        // Then, set properties to values as passed in ctor parameters.  
        Property1 = toSetProperty1;  
    }  
}  
```  
  
#### 非默认（方便）构造函数，确实与基签名匹配  
 不是使用同样的参数化功能调用基构造函数，而是再次调用自己类的默认构造函数。  请勿调用基初始值设定项，而应调用 `this()`。  然后使用传递的参数作为设置关联属性的值来重现原始构造函数行为。  使用原始基构造函数文档作为准则，用以确定特定的参数需要设置的属性：  
  
```  
public MyClass : SomeBaseClass {  
    public MyClass(object toSetProperty1) : this() {  
        // Class initialization NOT done by default.  
        // Then, set properties to values as passed in ctor parameters.  
        Property1 = toSetProperty1;  
    }  
}  
```  
  
#### 必须匹配所有的签名  
 对于基类型有多个签名的情况，必须在设置进一步的属性前特意将所有可能的签名与自己的构造函数的实现匹配，该实现使用调用类默认构造函数的建议模式。  
  
#### 使用 SetValue 设置依赖项属性  
 如果设置的属性不具有便于属性设置的包装，并使用 <xref:System.Windows.DependencyObject.SetValue%2A> 设置值，则这些相同的模式都适用。  通过构造函数参数传递的对 <xref:System.Windows.DependencyObject.SetValue%2A> 的调用还应调用类的默认初始化构造函数。  
  
## 请参阅  
 [自定义依赖项属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)   
 [依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [依赖项属性的安全性](../../../../docs/framework/wpf/advanced/dependency-property-security.md)