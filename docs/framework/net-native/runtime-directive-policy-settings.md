---
title: "运行时指令策略设置"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cb52b1ef-47fd-4609-b69d-0586c818ac9e
caps.latest.revision: 10
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 11c93b296bf34b24037b51a216b536087fe6cc2e
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="runtime-directive-policy-settings"></a>运行时指令策略设置
> [!NOTE]
>  该主题是指 .NET Native 开发者预览版这款预发布软件。 可从 [Microsoft Connect 网站](http://go.microsoft.com/fwlink/?LinkId=394611)（需要注册）下载该预览版。  
  
 .NET Native 的运行时指令策略设置决定在运行时间类型和类型成员的元数据的可用性。 如果没有必要的元数据，依赖于反射、序列化和反序列化的操作或 .NET 框架类型到 COM 的封送或 Windows 运行时会失败并引发一个异常。 最常见的异常是 [MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md) 和（在互操作的情况下）[MissingInteropDataException](../../../docs/framework/net-native/missinginteropdataexception-class-net-native.md)。  
  
 运行时策略设置是由一个运行时指令 (.rd.xml) 文件控制的。 每个运行时指令为特定的程序元素定义策略，比如程序集（[\<Assembly>](../../../docs/framework/net-native/assembly-element-net-native.md) 元素）、类型（[\<Type>](../../../docs/framework/net-native/type-element-net-native.md) 元素）或方法（[\<Method>](../../../docs/framework/net-native/method-element-net-native.md) 元素）。 指令包括一个或多个用于定义反射策略类型、序列化策略类型和互操作策略类型的特性，这些将在下一部分讨论到。 该特性的值定义策略设置。  
  
## <a name="policy-types"></a>策略类型  
 运行时指令文件可识别三类策略类型：反射、序列化和互操作。  
  
-   反射策略类型确定哪些元数据需要在运行时间可以用于反射：  
  
    -   `Activate` 控制运行时对构造函数的访问，以启用实例激活。  
  
    -   `Browse` 控制对有关程序元素的信息的查询。  
  
    -   `Dynamic` 控制运行时对所有类型和成员的访问，以启用动态编程。  
  
     以下表格中列出了这些反射策略类型和可以同它们一起使用的程序元素。  
  
    |元素|激活|浏览|动态|  
    |-------------|--------------|------------|-------------|  
    |[\<Application>](../../../docs/framework/net-native/application-element-net-native.md)|✓|✓|✓|  
    |[\<Assembly>](../../../docs/framework/net-native/assembly-element-net-native.md)|✓|✓|✓|  
    |[\<AttributeImplies>](../../../docs/framework/net-native/attributeimplies-element-net-native.md)|✓|✓|✓|  
    |[\<Event>](../../../docs/framework/net-native/event-element-net-native.md)||✓|✓|  
    |[\<Field>](../../../docs/framework/net-native/field-element-net-native.md)||✓|✓|  
    |[\<GenericParameter>](../../../docs/framework/net-native/genericparameter-element-net-native.md)|✓|✓|✓|  
    |[\<ImpliesType>](../../../docs/framework/net-native/impliestype-element-net-native.md)|✓|✓|✓|  
    |[\<Method>](../../../docs/framework/net-native/method-element-net-native.md)||✓|✓|  
    |[\<MethodInstantiation>](../../../docs/framework/net-native/methodinstantiation-element-net-native.md)||✓|✓|  
    |[\<Namespace>](../../../docs/framework/net-native/namespace-element-net-native.md)|✓|✓|✓|  
    |[\<Parameter>](../../../docs/framework/net-native/parameter-element-net-native.md)|✓|✓|✓|  
    |[\<Property>](../../../docs/framework/net-native/property-element-net-native.md)||✓|✓|  
    |[\<Subtypes>](../../../docs/framework/net-native/subtypes-element-net-native.md)|✓|✓|✓|  
    |[\<Type>](../../../docs/framework/net-native/type-element-net-native.md)|✓|✓|✓|  
    |[\<TypeInstantiation>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md)|✓|✓|✓|  
    |[\<TypeParameter>](../../../docs/framework/net-native/typeparameter-element-net-native.md)|✓|✓|✓|  
  
-   序列化策略类型确定哪些元数据需要在运行时间可以用于序列化和反序列化：  
  
    -   `Serialize` 控制运行时对构造函数、字段和属性的访问，使类型实例得到序列化和反序列化处理，这是通过第三方库进行的，例如 Newtonsoft JSON 序列化程序。  
  
    -   `DataContractSerializer` 控制运行时对构造函数、字段和属性的访问，使类型实例得到 <xref:System.Runtime.Serialization.DataContractSerializer> 类的序列化。  
  
    -   `DataContractJsonSerializer` 控制运行时对构造函数、字段和属性的访问，使类型实例得到 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 类的序列化。  
  
    -   `XmlSerializer` 控制运行时对构造函数、字段和属性的访问，使类型实例得到 <xref:System.Xml.Serialization.XmlSerializer> 类的序列化。  
  
     以下表格中列出了这些序列化策略类型和可以同它们一起使用的程序元素。  
  
    |元素|序列化|DataContractSerializer|DataContractJsonSerializer|XmlSerializer|  
    |-------------|---------------|----------------------------|--------------------------------|-------------------|  
    |[\<Application>](../../../docs/framework/net-native/application-element-net-native.md)|✓|✓|✓|✓|  
    |[\<Assembly>](../../../docs/framework/net-native/assembly-element-net-native.md)|✓|✓|✓|✓|  
    |[\<AttributeImplies>](../../../docs/framework/net-native/attributeimplies-element-net-native.md)|✓|✓|✓|✓|  
    |[\<Event>](../../../docs/framework/net-native/event-element-net-native.md)|||||  
    |[\<Field>](../../../docs/framework/net-native/field-element-net-native.md)|✓||||  
    |[\<GenericParameter>](../../../docs/framework/net-native/genericparameter-element-net-native.md)|✓|✓|✓|✓|  
    |[\<ImpliesType>](../../../docs/framework/net-native/impliestype-element-net-native.md)|✓|✓|✓|✓|  
    |[\<Method>](../../../docs/framework/net-native/method-element-net-native.md)|||||  
    |[\<MethodInstantiation>](../../../docs/framework/net-native/methodinstantiation-element-net-native.md)|||||  
    |[\<Namespace>](../../../docs/framework/net-native/namespace-element-net-native.md)|✓|✓|✓|✓|  
    |[\<Parameter>](../../../docs/framework/net-native/parameter-element-net-native.md)|✓|✓|✓|✓|  
    |[\<Property>](../../../docs/framework/net-native/property-element-net-native.md)|✓||||  
    |[\<Subtypes>](../../../docs/framework/net-native/subtypes-element-net-native.md)|✓|✓|✓|✓|  
    |[\<Type>](../../../docs/framework/net-native/type-element-net-native.md)|✓|✓|✓|✓|  
    |[\<TypeInstantiation>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md)|✓|✓|✓|✓|  
    |[\<TypeParameter>](../../../docs/framework/net-native/typeparameter-element-net-native.md)|✓|✓|✓|✓|  
  
-   互操作策略类型确定哪些元数据在运行时间通过了连接到 COM 和 Windows 运行时的引用类型、值类型和函数指针。  
  
    -   `MarshalObject` 控制到引用类型的 COM 和 Windows 运行时的本机封送处理。  
  
    -   `MarshalDelegate` 控制作为函数指针的委托类型的本机封送处理。  
  
    -   `MarshalStructure` 控制到值类型的 COM 和 Windows 运行时的本机封送处理。  
  
     以下表格中列出了这些互操作策略类型和可以同它们一起使用的程序元素。  
  
    |元素|封送对象|封送委托|封送结构|  
    |-------------|-------------------|---------------------|----------------------|  
    |[\<Application>](../../../docs/framework/net-native/application-element-net-native.md)|✓|✓|✓|  
    |[\<Assembly>](../../../docs/framework/net-native/assembly-element-net-native.md)|✓|✓|✓|  
    |[\<AttributeImplies>](../../../docs/framework/net-native/attributeimplies-element-net-native.md)|✓|✓|✓|  
    |[\<Event>](../../../docs/framework/net-native/event-element-net-native.md)||||  
    |[\<Field>](../../../docs/framework/net-native/field-element-net-native.md)||||  
    |[\<GenericParameter>](../../../docs/framework/net-native/genericparameter-element-net-native.md)|✓|✓|✓|  
    |[\<ImpliesType>](../../../docs/framework/net-native/impliestype-element-net-native.md)|✓|✓|✓|  
    |[\<Method>](../../../docs/framework/net-native/method-element-net-native.md)||||  
    |[\<MethodInstantiation>](../../../docs/framework/net-native/methodinstantiation-element-net-native.md)||||  
    |[\<Namespace>](../../../docs/framework/net-native/namespace-element-net-native.md)|✓|✓|✓|  
    |[\<Parameter>](../../../docs/framework/net-native/parameter-element-net-native.md)|✓|✓|✓|  
    |[\<Property>](../../../docs/framework/net-native/property-element-net-native.md)||||  
    |[\<Subtypes>](../../../docs/framework/net-native/subtypes-element-net-native.md)|✓|✓|✓|  
    |[\<Type>](../../../docs/framework/net-native/type-element-net-native.md)|✓|✓|✓|  
    |[\<TypeInstantiation>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md)|✓|✓|✓|  
    |[\<TypeParameter>](../../../docs/framework/net-native/typeparameter-element-net-native.md)|✓|✓|✓|  
  
## <a name="policy-settings"></a>策略设置  
 每个策略类型都可设置为以下表格中列出的一个值。 注意，代表类型成员的元素支持一组不同的策略设置，而不支持其他元素。  
  
|策略设置|描述|`Assembly`、`Namespace`、`Type` 和 `TypeInstantiation` 元素|`Event`、`Field`、`Method`、`MethodInstantiation` 和 `Property` 元素|  
|--------------------|-----------------|-----------------------------------------------------------------------|--------------------------------------------------------------------------------|  
|`All`|为 .NET Native 工具链未删除的所有类型和成员启用策略。|✓||  
|`Auto`|指定将默认策略用于该程序元素的策略类型。 这同省略该策略类型的策略是相同的。 `Auto` 通常用于显示策略是从一个父元素继承的。|✓|✓|  
|`Excluded`|指定了该策略禁止一个特定的程序元素使用。 例如，运行时指令：<br /><br /> `<Type Name="BusinessClasses.Person" Browse="Excluded" Dynamic="Excluded" />`<br /><br /> 指定了 `BusinessClasses.Person` 类的元数据既不能用来浏览，也不能用来动态实例化或修改 `Person` 对象。|✓|✓|  
|`Included`|在父类型的元数据可用时启用一个策略。||✓|  
|`Public`|启用针对公共类型或成员的策略，除非工具链确定该类型或成员无必要存在并已将其删除。 该设置不同于 `Required Public`，后者确保公共类型和成员的元数据始终可用，即使是在工具链确定这一步骤无必要时仍是如此。|✓||  
|`PublicAndInternal`|启用针对公共类型或成员以及内部类型或成员的策略，除非工具链确定该类型或成员无必要存在并已将其删除。 该设置不同于 `Required PublicAndInternal`，后者确保公共类型和成员以及内部类型或成员的元数据始终可用，即使是在工具链确定这一步骤无必要时仍是如此。|✓||  
|`Required`|指定了一个成员的策略已启用并且元数据是可用的，即使在该成员受到占用时仍是如此。||✓|  
|`Required Public`|为公共类型或成员启用策略，并确保公共类型和成员的元数据始终可用。 该设置不同于 `Public`，后者确保公共类型和成员的元数据仅在工具链确定这一步骤有必要时才可用。|✓||  
|`Required PublicAndInternal`|为公共类型或成员以及内部类型或成员启用策略，并确保公共类型和成员以及内部类型或成员的元数据始终可用。 该设置不同于 `PublicAndInternal`，后者确保公共类型和成员以及内部类型和成员的元数据仅在工具链确定这一步骤有必要时才可用。|✓||  
|`Required All`|要求工具链在不管所有类型是否受到占用情况下都保留它们，并为它们启用策略。|✓||  
  
## <a name="see-also"></a>另请参阅  
 [运行时指令 (rd.xml) 配置文件参考](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)   
 [运行时指令元素](../../../docs/framework/net-native/runtime-directive-elements.md)

