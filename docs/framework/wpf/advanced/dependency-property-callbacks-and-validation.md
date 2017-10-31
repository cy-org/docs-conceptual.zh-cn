---
title: "依赖项属性回调和验证 | Microsoft Docs"
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
  - "回调, 验证"
  - "强制值回调"
  - "依赖项属性, 回调"
  - "依赖项属性, 验证"
  - "依赖项属性的验证"
ms.assetid: 48db5fb2-da7f-49a6-8e81-3540e7b25825
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 依赖项属性回调和验证
本主题介绍如何使用与属性相关的功能（如验证确定、更改属性的有效值时调用的回调）的替代自定义实现，并重写对值确定的外部可能影响来创建依赖项属性。  本主题还讨论了使用这些技术扩展默认属性系统行为所适用的方案。  
  
   
  
<a name="prerequisites"></a>   
## 必备组件  
 本主题假定您了解实现依赖项属性的基本方案以及如何将元数据应用到自定义依赖项属性。  有关上下文，请参见[自定义依赖项属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)和[依赖项属性元数据](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md)。  
  
<a name="Validation_Callbacks"></a>   
## 验证回调  
 在首次注册依赖项属性时，可以为其分配验证回调。  验证回调不属于属性元数据，而是 <xref:System.Windows.DependencyProperty.Register%2A> 方法的直接输入。  因此，在为某个依赖项属性创建验证回调后，新实现将无法重写该验证回调。  
  
 [!code-csharp[DPCallbackOverride#CurrentDefinitionWithWrapper](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DPCallbackOverride/CSharp/SDKSampleLibrary/class1.cs#currentdefinitionwithwrapper)]
 [!code-vb[DPCallbackOverride#CurrentDefinitionWithWrapper](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DPCallbackOverride/visualbasic/sdksamplelibrary/class1.vb#currentdefinitionwithwrapper)]  
  
 实现回调，以便为其提供对象值。  如果提供的值对属性有效，回调将返回 `true`；否则，回调返回 `false`。  假定按照向属性系统注册的类型，属性的类型是正确的，因此通常不会在回调内执行类型检查。  属性系统可在多种不同操作中使用回调。  其中包括按照默认值进行初始类型初始化、通过调用 <xref:System.Windows.DependencyObject.SetValue%2A> 进行编程更改或尝试使用提供的新默认值重写元数据。  如果验证回调是通过其中任何一种操作调用的，并且返回 `false`，则将会引发异常。  应用程序编写器必须准备处理这些异常。  验证回调常用于验证枚举值，或在属性设置的度量必须大于或等于零时约束整数值或双精度型值。  
  
 验证回调专用作类验证程序，而不用作实例验证程序。  回调参数不会与对其设置要验证的属性的特定 <xref:System.Windows.DependencyObject> 通信。  因此，验证回调不能用来强制执行可能会影响属性值的“依赖项”，其中，某个属性特定于实例的值依赖于其他属性特定于实例的值或运行时状态等因素。  
  
 下面是一个非常简单的验证回调方案的代码示例：验证类型化为 <xref:System.Double> 基元的属性是否为 <xref:System.Double.PositiveInfinity> 或 <xref:System.Double.NegativeInfinity>。  
  
 [!code-csharp[DPCallbackOverride#ValidateValueCallback](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DPCallbackOverride/CSharp/SDKSampleLibrary/class1.cs#validatevaluecallback)]
 [!code-vb[DPCallbackOverride#ValidateValueCallback](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DPCallbackOverride/visualbasic/sdksamplelibrary/class1.vb#validatevaluecallback)]  
  
<a name="Coerce_Value_Callbacks_and_Property_Changed_Events"></a>   
## 强制值回调和属性更改事件  
 强制值回调传递属性的特定 <xref:System.Windows.DependencyObject> 实例，在更改依赖项属性的值时属性系统调用的 <xref:System.Windows.PropertyChangedCallback> 实现也是如此。  通过将这两种回调组合使用，可以对元素创建一系列属性，其中，一个属性的更改将会对另一个属性实施强制或重新计算。  
  
 使用依赖项属性链接的典型方案是：您具有用户界面驱动属性，其中，元素为最小值和最大值分别保留了一个属性，为实际值或当前值保留了第三个属性。  此时，如果按照当前值超出新的最大值的方式调整最大值，则可能需要强制当前值不超过新的最大值，并对最小值与当前值强制类似的关系。  
  
 下面是一个非常简短的代码示例，仅针对阐释此关系的三个依赖项属性之一。  该示例演示如何注册相关的 \*Reading 属性的最小\/最大\/当前值集的 `CurrentReading` 属性。  它使用上一节中所示的验证。  
  
 [!code-csharp[DPCallbackOverride#CurrentDefinitionWithWrapper](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DPCallbackOverride/CSharp/SDKSampleLibrary/class1.cs#currentdefinitionwithwrapper)]
 [!code-vb[DPCallbackOverride#CurrentDefinitionWithWrapper](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DPCallbackOverride/visualbasic/sdksamplelibrary/class1.vb#currentdefinitionwithwrapper)]  
  
 当前值的属性更改回调用于将更改转发到其他依赖项属性，方法是显式调用为这些属性注册的强制值回调：  
  
 [!code-csharp[DPCallbackOverride#OnPCCurrent](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DPCallbackOverride/CSharp/SDKSampleLibrary/class1.cs#onpccurrent)]
 [!code-vb[DPCallbackOverride#OnPCCurrent](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DPCallbackOverride/visualbasic/sdksamplelibrary/class1.vb#onpccurrent)]  
  
 强制值回调将检查当前属性可能依赖的属性的值，并在必要时强制当前值：  
  
 [!code-csharp[DPCallbackOverride#CoerceCurrent](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DPCallbackOverride/CSharp/SDKSampleLibrary/class1.cs#coercecurrent)]
 [!code-vb[DPCallbackOverride#CoerceCurrent](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DPCallbackOverride/visualbasic/sdksamplelibrary/class1.vb#coercecurrent)]  
  
> [!NOTE]
>  不会强制属性的默认值。  如果属性值仍然采用其初始默认值，或通过使用 <xref:System.Windows.DependencyObject.ClearValue%2A> 清除其他值，则可能存在等于默认值的属性值。  
  
 强制值回调和属性更改回调属于属性元数据的一部分。  因此，您可以通过在自己的类型上重写特定依赖项属性的元数据来更改对该属性的回调，因为其类型派生自拥有该依赖项属性的类型。  
  
<a name="Advanced"></a>   
## 高级强制和回调方案  
  
### 约束和所需的值  
 属性系统将根据所声明的逻辑使用 <xref:System.Windows.PropertyMetadata.CoerceValueCallback%2A> 回调来强制值，但本地设置的属性的强制值仍然会在内部保留“所需的值”。  如果约束基于可能会在应用程序生存期间动态更改的其他属性值，则强制约束也会进行动态更改，并且在给定新约束的情况下约束属性可更改其值以尽可能接近所需的值。  如果解除所有约束，该值将成为所需的值。  如果您的多个属性以循环方式相互依赖，则可能会引入某些相当复杂的依赖项方案。  例如，在最小\/最大\/当前值方案中，可以选择将最小值和最大值作为用户可设置的资源。  在这种情况下，您可能需要强制最大值始终大于最小值，反之亦然。  但是，如果该强制处于活动状态，并且最大值强制为最小值，则会将当前值保留在不可设置的状态，因为它依赖于这二者，且被约束在这些值之间的范围内，即为零。  这样，如果调整最大值或最小值，当前值可能会“遵循”这些值之一，因为仍然存储了当前值所需的值，并且当前值会在放松约束时尝试接近所需的值。  
  
 复杂依赖项没有任何技术错误，但是，如果它们需要大量重新计算，则可能会略微降低性能，而且还可能导致用户混淆（如果直接影响 UI）。  请小心使用属性更改回调和强制值回调，确保可尽可能地明确处理所尝试的强制，并且不会“过度约束”。  
  
### 使用强制值取消值更改  
 属性系统将返回 <xref:System.Windows.DependencyProperty.UnsetValue> 值的任何 <xref:System.Windows.CoerceValueCallback> 都视为一种特殊情况。  此特殊情况意味着，属性系统应拒绝导致调用 <xref:System.Windows.CoerceValueCallback> 的属性更改，并且还应报告该属性以前的任何值。  该机制可用于检查异步启动的属性的更改对当前对象状态是否仍然有效，如果无效，则可取消这些更改。  另一个可能的方案是：您可以根据负责所报告的值的属性值确定组件来有选择地取消该值。  为此，可以将回调中传递的 <xref:System.Windows.DependencyProperty> 和属性标识符用作 <xref:System.Windows.DependencyPropertyHelper.GetValueSource%2A> 的输入，然后处理 <xref:System.Windows.ValueSource>。  
  
## 请参阅  
 [依赖项属性概述](../../../../docs/framework/wpf/advanced/dependency-properties-overview.md)   
 [依赖项属性元数据](../../../../docs/framework/wpf/advanced/dependency-property-metadata.md)   
 [自定义依赖项属性](../../../../docs/framework/wpf/advanced/custom-dependency-properties.md)