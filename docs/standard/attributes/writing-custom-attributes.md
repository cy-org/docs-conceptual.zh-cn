---
title: "编写自定义特性 | Microsoft Docs"
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
  - "AllowMultiple 属性"
  - "特性类, 声明"
  - "特性 [.NET Framework], 自定义"
  - "AttributeTargets 枚举"
  - "AttributeUsageAttribute 类, 自定义特性"
  - "自定义特性"
  - "“继承”属性"
  - "多个特性实例"
ms.assetid: 97216f69-bde8-49fd-ac40-f18c500ef5dc
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# 编写自定义特性
要设计你自己的自定义特性，无需掌握许多新的概念。 如果你熟悉面向对象的编程，并且知道如何设计类，那么你已经具备大部分所需知识。 自定义特性本质上是直接或间接派生自 <xref:System.Attribute?displayProperty=fullName> 的传统类。 与传统类一样，自定义特性包含用于存储和检索数据的方法。  
  
 正确设计自定义特性的主要步骤如下：  
  
-   [应用 AttributeUsageAttribute](#cpconapplyingattributeusageattribute)  
  
-   [声明特性类](#cpcondeclaringattributeclass)  
  
-   [声明构造函数](#cpcondeclaringconstructors)  
  
-   [声明属性](#cpcondeclaringproperties)  
  
 本节描述上述各个步骤，并以[自定义特性的示例](#cpconcustomattributeexample)结束本节的描述。  
  
<a name="cpconapplyingattributeusageattribute"></a>   
## 应用 AttributeUsageAttribute  
 自定义特性声明以 **AttributeUsageAttribute** 开始，定义了特性类的一些主要特征。 例如，你可以指定其他类是否可以继承你的特性，或者指定此特性可以应用到哪些元素。 下面的代码段演示如何使用 **AttributeUsageAttribute**。  
  
 [!code-cpp[Conceptual.Attributes.Usage#5](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#5)]
 [!code-csharp[Conceptual.Attributes.Usage#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#5)]
 [!code-vb[Conceptual.Attributes.Usage#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#5)]  
  
 <xref:System.AttributeUsageAttribute?displayProperty=fullName> 具有三个对于创建自定义特性很重要的成员：[AttributeTargets](#cpconwritingcustomattributesanchor1)、[Inherited](#cpconwritingcustomattributesanchor2) 和 [AllowMultiple](#cpconwritingcustomattributesanchor3)。  
  
<a name="cpconwritingcustomattributesanchor1"></a>   
### AttributeTargets 成员  
 在前面的示例中指定了 **AttributeTargets.All**，这表示此特性可以应用于所有程序元素。 或者，你可以指定 **AttributeTargets.Class**，表示你的特性只能应用于一个类，或者指定 **AttributeTargets.Method**，表示你的特性只能应用于一种方法。 所有程序元素都可以通过这种方式使用自定义特性来标记，以对其进行描述。  
  
 你还可以传递 <xref:System.AttributeTargets> 的多个实例。 下面的代码段指定了自定义特性可应用于任何类或方法。  
  
 [!code-cpp[Conceptual.Attributes.Usage#6](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#6)]
 [!code-csharp[Conceptual.Attributes.Usage#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#6)]
 [!code-vb[Conceptual.Attributes.Usage#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#6)]  
  
<a name="cpconwritingcustomattributesanchor2"></a>   
### Inherited 属性  
 <xref:System.AttributeUsageAttribute.Inherited%2A?displayProperty=fullName> 属性用于表示要应用你的特性的类所派生的类是否可以继承此特性。 此属性使用 **true**（默认值）或 **false** 标志。 例如，在以下示例中， `MyAttribute` 的 <xref:System.AttributeUsageAttribute.Inherited%2A> 的默认值为 **true**，`YourAttribute` 的 <xref:System.AttributeUsageAttribute.Inherited%2A> 的值为 **false**。  
  
 [!code-cpp[Conceptual.Attributes.Usage#7](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#7)]
 [!code-csharp[Conceptual.Attributes.Usage#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#7)]
 [!code-vb[Conceptual.Attributes.Usage#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#7)]  
  
 然后，这两个特性应用于基类 `MyClass` 中的方法。  
  
 [!code-cpp[Conceptual.Attributes.Usage#9](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#9)]
 [!code-csharp[Conceptual.Attributes.Usage#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#9)]
 [!code-vb[Conceptual.Attributes.Usage#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#9)]  
  
 最后，从基类 `MyClass` 中继承类 `YourClass`。 方法 `MyMethod` 显示 `MyAttribute`，但不显示 `YourAttribute`。  
  
 [!code-cpp[Conceptual.Attributes.Usage#10](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#10)]
 [!code-csharp[Conceptual.Attributes.Usage#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#10)]
 [!code-vb[Conceptual.Attributes.Usage#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#10)]  
  
<a name="cpconwritingcustomattributesanchor3"></a>   
### AllowMultiple 属性  
 <xref:System.AttributeUsageAttribute.AllowMultiple%2A?displayProperty=fullName> 属性表示一个元素是否可以存在特性的多个实例。 如果设置为 **true**，则允许多个实例；如果设置为 **false**（默认值），则只允许一个实例。  
  
 在下面的示例中， `MyAttribute` 的 <xref:System.AttributeUsageAttribute.AllowMultiple%2A> 的默认值为 **false**，`YourAttribute` 的对应值为 **true**。  
  
 [!code-cpp[Conceptual.Attributes.Usage#11](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#11)]
 [!code-csharp[Conceptual.Attributes.Usage#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#11)]
 [!code-vb[Conceptual.Attributes.Usage#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#11)]  
  
 当应用这些特性的多个实例时， `MyAttribute` 会生成编译器错误。 下面的代码示例显示 `YourAttribute` 的有效用法和 `MyAttribute` 的无效用法。  
  
 [!code-cpp[Conceptual.Attributes.Usage#13](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#13)]
 [!code-csharp[Conceptual.Attributes.Usage#13](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#13)]
 [!code-vb[Conceptual.Attributes.Usage#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#13)]  
  
 如果 <xref:System.AttributeUsageAttribute.AllowMultiple%2A> 属性和 <xref:System.AttributeUsageAttribute.Inherited%2A> 属性都设置为 **true**，那么从另一个类继承的类可以继承一个特性，并且具有应用于同一子类的同一特性的另一个实例。 如果 <xref:System.AttributeUsageAttribute.AllowMultiple%2A> 设置为 **false**，那么父类中的任何特性的值将被子类中同一特性的新实例覆盖。  
  
<a name="cpcondeclaringattributeclass"></a>   
## 声明特性类  
 应用 <xref:System.AttributeUsageAttribute> 以后，可以开始定义特性的细节。 特性类的声明类似于传统类的声明，如以下代码所示。  
  
 [!code-cpp[Conceptual.Attributes.Usage#14](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#14)]
 [!code-csharp[Conceptual.Attributes.Usage#14](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#14)]
 [!code-vb[Conceptual.Attributes.Usage#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#14)]  
  
 此特性定义说明了以下几点：  
  
-   特性类必须声明为公共类。  
  
-   按照约定，特性类的名称以单词 **Attribute** 结束。 尽管没有要求，但仍建议执行此约定以保证可读性。 应用特性时，可以选择是否包含单词 Attribute。  
  
-   所有特性类必须直接或间接从 **System.Attribute** 继承。  
  
-   在 Microsoft Visual Basic 中，所有自定义特性类必须具有 **AttributeUsageAttribute** 特性。  
  
<a name="cpcondeclaringconstructors"></a>   
## 声明构造函数  
 与传统类的初始化方式相同，使用构造函数初始化特性。 下面的代码段阐明了典型的特性构造函数。 此公共构造函数采用一个参数，并将其值设置为与成员变量的值相等。  
  
 [!code-cpp[Conceptual.Attributes.Usage#15](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#15)]
 [!code-csharp[Conceptual.Attributes.Usage#15](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#15)]
 [!code-vb[Conceptual.Attributes.Usage#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#15)]  
  
 可以重载此构造函数以适应值的各种组合。 如果你还为自定义特性类定义了[属性](../Topic/Properties%20Overview.md)，则在初始化该特性时可以使用命名参数和定位参数的组合。 通常情况下，将所有必选的参数定义为定位参数，将所有可选的参数定义为命名参数。 在这种情况下，没有必选参数则无法初始化特性。 其他所有参数都是可选参数。 请注意，在 Visual Basic 中，特性类的构造函数不应使用 ParamArray 参数。  
  
 下面的代码示例显示如何使用可选和必选参数应用使用上例中的构造函数的特性。 该示例假定特性有一个必选的布尔值和一个可选的字符串属性。  
  
 [!code-cpp[Conceptual.Attributes.Usage#17](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#17)]
 [!code-csharp[Conceptual.Attributes.Usage#17](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#17)]
 [!code-vb[Conceptual.Attributes.Usage#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#17)]  
  
<a name="cpcondeclaringproperties"></a>   
## 声明属性  
 如果你想要定义一个命名参数，或者提供一种简单的方法来返回由特性存储的值，请声明[属性](../Topic/Properties%20Overview.md)。 应将特性的属性声明为公共实体，此公告实体包含将返回的数据类型的描述。 定义将保存属性值的变量，并将此变量与 **get** 和 **set** 方法相关联。 下面的代码示例说明如何在特性中实现一个简单属性。  
  
 [!code-cpp[Conceptual.Attributes.Usage#16](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#16)]
 [!code-csharp[Conceptual.Attributes.Usage#16](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#16)]
 [!code-vb[Conceptual.Attributes.Usage#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#16)]  
  
<a name="cpconcustomattributeexample"></a>   
## 自定义特性的示例  
 本节内容结合了前面的信息，显示如何设计一个简单特性来记录有关代码段的作者的信息。 本示例中的特性存储了编程人员的姓名和级别，以及是否已检查此代码的信息。 它使用三个私有变量来存储要保存的实际值。 每个变量用获取和设置这些值的公共属性表示。 最后，使用两个必选参数定义构造函数。  
  
 [!code-cpp[Conceptual.Attributes.Usage#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#4)]
 [!code-csharp[Conceptual.Attributes.Usage#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#4)]
 [!code-vb[Conceptual.Attributes.Usage#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#4)]  
  
 可以采用以下任一种方法，使用全称 `DeveloperAttribute` 或缩写名称 `Developer` 应用此特性。  
  
 [!code-cpp[Conceptual.Attributes.Usage#12](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#12)]
 [!code-csharp[Conceptual.Attributes.Usage#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#12)]
 [!code-vb[Conceptual.Attributes.Usage#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#12)]  
  
 第一个示例显示只应用了必选命名参数的特性，第二个示例显示同时应用了必选参数和可选参数的特性。  
  
## 请参阅  
 <xref:System.Attribute?displayProperty=fullName>   
 <xref:System.AttributeUsageAttribute>   
 [特性](../../../docs/standard/attributes/index.md)