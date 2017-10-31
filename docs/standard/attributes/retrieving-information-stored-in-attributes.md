---
title: "检索存储在特性中的信息 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "特性 [.NET Framework], 检索"
  - "多个特性实例"
  - "检索特性"
ms.assetid: 37dfe4e3-7da0-48b6-a3d9-398981524e1c
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# 检索存储在特性中的信息
检索自定义特性的过程很简单。  首先，声明要检索的特性实例。  然后，使用 <xref:System.Attribute.GetCustomAttribute%2A?displayProperty=fullName> 方法将新特性初始化为要检索的特性值。  初始化新特性后，只需使用其属性获取值即可。  
  
> [!IMPORTANT]
>  本主题描述如何检索已加载到执行上下文中的代码的特性。  若要检索已加载到只反射上下文中的代码的特性，必须使用 <xref:System.Reflection.CustomAttributeData> 类，如[如何：将程序集加载到仅反射上下文中](../../../docs/framework/reflection-and-codedom/how-to-load-assemblies-into-the-reflection-only-context.md)所示。  
  
 本节描述下列检索特性的方法：  
  
-   [检索特性的一个实例](#cpconretrievingsingleinstanceofattribute)  
  
-   [检索应用到同一范围的特性的多个实例](#cpconretrievingmultipleinstancesofattributeappliedtosamescope)  
  
-   [检索应用到不同范围的特性的多个实例](#cpconretrievingmultipleinstancesofattributeappliedtodifferentscopes)  
  
<a name="cpconretrievingsingleinstanceofattribute"></a>   
## 检索特性的一个实例  
 在下面的示例中，`DeveloperAttribute`（详见前一节的介绍）应用到类级别上的 `MainApp` 类。  `GetAttribute` 方法使用 **GetCustomAttribute** 检索存储在类级别上 `DeveloperAttribute` 中的值，然后将这些值显示到控制台。  
  
 [!code-cpp[Conceptual.Attributes.Usage#18](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source3.cpp#18)]
 [!code-csharp[Conceptual.Attributes.Usage#18](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source3.cs#18)]
 [!code-vb[Conceptual.Attributes.Usage#18](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source3.vb#18)]  
  
 该程序在执行时显示下列文本。  
  
```  
The Name Attribute is: Joan Smith.  
The Level Attribute is: 42.  
The Reviewed Attribute is: True.  
```  
  
 如果未找到该特性，则 **GetCustomAttribute** 方法将 `MyAttribute` 初始化为一个 null 值。  该示例检查 `MyAttribute` 以查找这样的实例，如未找到任何特性，则通知用户。  如果在类范围中未找到 `DeveloperAttribute`，则下列消息将显示到控制台。  
  
```  
The attribute was not found.   
```  
  
 该示例假定特性定义位于当前命名空间中。  如果特性定义不在当前命名空间中，请务必导入该特性定义所驻留的命名空间。  
  
<a name="cpconretrievingmultipleinstancesofattributeappliedtosamescope"></a>   
## 检索应用到同一范围的特性的多个实例  
 在前一个示例中，要检查的类和要查找的特定特性被传递到 <xref:System.Attribute.GetCustomAttribute%2A>。  如果类级别上只应用特性的一个实例，则该代码将运行良好。  但是，如果在同一类级别上应用特性的多个实例，则 **GetCustomAttribute** 方法不检索所有信息。  如果同一个特性的多个实例应用到相同的范围，可使用 <xref:System.Attribute.GetCustomAttributes%2A?displayProperty=fullName> 将特性的所有实例放到一个数组中。  例如，如果在同一个类的类级别上应用 `DeveloperAttribute` 的两个实例，则可修改 `GetAttribute` 方法以显示同时存在于这两个特性中的信息。  请记住，若要在同一级别上应用多个特性，必须在定义该特性时在 <xref:System.AttributeUsageAttribute> 中将 **AllowMultiple** 属性设置为 **true**。  
  
 下面的代码示例说明如何使用 **GetCustomAttributes** 方法创建在任意给定类中引用 `DeveloperAttribute` 的所有实例的数组。  然后，所有特性的值将显示到控制台。  
  
 [!code-cpp[Conceptual.Attributes.Usage#19](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source3.cpp#19)]
 [!code-csharp[Conceptual.Attributes.Usage#19](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source3.cs#19)]
 [!code-vb[Conceptual.Attributes.Usage#19](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source3.vb#19)]  
  
 如果没有找到任何特性，该代码将提醒用户。  否则，将显示两个 `DeveloperAttribute` 实例中都包含的信息。  
  
<a name="cpconretrievingmultipleinstancesofattributeappliedtodifferentscopes"></a>   
## 检索应用到不同范围的特性的多个实例  
 <xref:System.Attribute.GetCustomAttributes%2A> 方法和 <xref:System.Attribute.GetCustomAttribute%2A> 方法不搜索整个类和返回该类中某个特性的所有实例。  相反，它们一次只搜索一个指定方法或成员。  如果将具有同一特性的某个类应用到每个成员，并要检索应用到这些成员的所有特性值，则必须向 **GetCustomAttributes** 和 **GetCustomAttribute** 分别提供每个方法或成员。  
  
 下面的代码示例将类用作参数，并在类级别上以及该类的每个方法上搜索 `DeveloperAttribute`（先前已定义）。  
  
 [!code-cpp[Conceptual.Attributes.Usage#20](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source3.cpp#20)]
 [!code-csharp[Conceptual.Attributes.Usage#20](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source3.cs#20)]
 [!code-vb[Conceptual.Attributes.Usage#20](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source3.vb#20)]  
  
 如果在方法级别或类级别上未找到 `DeveloperAttribute` 的任何实例，`GetAttribute` 方法将通知用户未找到任何特性，并显示不包含该特性的方法或类的名称。  如果找到了特性，则控制台将显示 `Name`、`Level` 和 `Reviewed` 字段。  
  
 可使用 <xref:System.Type> 类的成员获取已传递的类中的各个方法和成员。  该示例首先查询 **Type** 对象以获取类级别的特性信息。  然后使用 <xref:System.Type.GetMethods%2A?displayProperty=fullName> 将所有方法的实例放到 <xref:System.Reflection.MemberInfo?displayProperty=fullName> 对象的一个数组中以检索方法级别的特性信息。  您也可以使用 <xref:System.Type.GetProperties%2A?displayProperty=fullName> 方法检查属性级别上的特性，或使用 <xref:System.Type.GetConstructors%2A?displayProperty=fullName> 方法检查构造函数级别上的特性。  
  
## 请参阅  
 <xref:System.Type?displayProperty=fullName>   
 <xref:System.Attribute.GetCustomAttribute%2A?displayProperty=fullName>   
 <xref:System.Attribute.GetCustomAttributes%2A?displayProperty=fullName>   
 [特性](../../../docs/standard/attributes/index.md)