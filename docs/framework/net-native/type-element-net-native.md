---
title: "&lt;Type&gt; 元素 (.NET Native)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1e88d368-a886-4f1e-8eb6-6127979a9fce
caps.latest.revision: 33
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 0f483fba5ade9d33588a946984ca914b95cd1f18
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="lttypegt-element-net-native"></a>&lt;Type&gt; 元素 (.NET Native)
将运行时策略应用到一个特定类型，例如一个类或结构。  
  
## <a name="syntax"></a>语法  
  
```xml  
<Type Name="type_name"  
      Activate="policy_type"  
      Browse="policy_type"  
      Dynamic="policy_type"  
      Serialize="policy_type"   
      DataContractSerializer="policy_setting"  
      DataContractJsonSerializer="policy_setting"  
      XmlSerializer="policy_setting"  
      MarshalObject="policy_setting"  
      MarshalDelegate="policy_setting"  
      MarshalStructure="policy_setting" />  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|特性类型|描述|  
|---------------|--------------------|-----------------|  
|`Name`|常规|必需的特性。 指定类型名称。|  
|`Activate`|映像|可选特性。 控制运行时对构造函数的访问，以启用实例激活。|  
|`Browse`|映像|可选特性。 控制对有关程序元素信息的查询，但并不启用任何运行时访问。|  
|`Dynamic`|映像|可选特性。 控制运行时对所有类型成员的访问，包括构造函数、方法、字段、属性和事件，以启用动态编程。|  
|`Serialize`|序列化|可选特性。 控制运行时对构造函数、字段和属性的访问，使类型实例得到序列化和反序列化处理，这是通过库进行的，例如 Newtonsoft JSON 序列化程序。|  
|`DataContractSerializer`|序列化|可选特性。 控制使用 <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=fullName> 类的序列化策略。|  
|`DataContractJsonSerializer`|序列化|可选特性。 控制使用 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=fullName> 类的 JSON 序列化策略。|  
|`XmlSerializer`|序列化|可选特性。 控制使用 <xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName> 类的 XML 序列化策略。|  
|`MarshalObject`|Interop|可选特性。 控制封送引用类型到 Windows 运行时和 COM 的策略。|  
|`MarshalDelegate`|Interop|可选特性。 控制将委托类型作为函数指针封送到本机代码的策略。|  
|`MarshalStructure`|Interop|可选特性。 控制封送处理值类型到本机代码的策略。|  
  
## <a name="name-attribute"></a>Name 特性  
  
|值|描述|  
|-----------|-----------------|  
|type_name|类型名称。 如果此 `<Type>` 元素是 [\<Namespace>](../../../docs/framework/net-native/namespace-element-net-native.md) 元素或另一个 `<Type>` 元素的子元素，type_name 可能包括类型名称而不包括其命名空间。 否则，type_name 必须包含完全限定的类型名称。|  
  
## <a name="all-other-attributes"></a>所有其他特性  
  
|值|描述|  
|-----------|-----------------|  
|policy_setting|该设置将应用到这种策略类型。 可能值为 `All`、`Auto`、`Excluded`、`Public`、`PublicAndInternal`、`Required Public`、`Required PublicAndInternal` 以及 `Required All`。 有关详细信息，请参阅[运行时指令策略设置](../../../docs/framework/net-native/runtime-directive-policy-settings.md)。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<AttributeImplies>](../../../docs/framework/net-native/attributeimplies-element-net-native.md)|如果包含类型是一个特性，为该特性所应用到的代码元素定义一个运行时策略。|  
|[\<Event>](../../../docs/framework/net-native/event-element-net-native.md)|将反射策略应用到属于这种类型的一个事件。|  
|[\<Field>](../../../docs/framework/net-native/field-element-net-native.md)|将反射策略应用到属于这种类型的一个字段。|  
|[\<GenericParameter>](../../../docs/framework/net-native/genericparameter-element-net-native.md)|将策略应用到一个泛型类型的参数类型。|  
|[\<ImpliesType>](../../../docs/framework/net-native/impliestype-element-net-native.md)|如果该策略已应用到以包含 `<Type>` 元素为代表的类型，将该策略应用到一个类型。|  
|[\<Method>](../../../docs/framework/net-native/method-element-net-native.md)|将反射策略应用到属于这种类型的一个方法。|  
|[\<MethodInstantiation>](../../../docs/framework/net-native/methodinstantiation-element-net-native.md)|将反射策略应用到属于这种类型的一个构造泛型方法。|  
|[\<Property>](../../../docs/framework/net-native/property-element-net-native.md)|将反射策略应用到属于这种类型的一个属性。|  
|[\<Subtypes>](../../../docs/framework/net-native/subtypes-element-net-native.md)|将运行时策略应用到从包含类型继承的所有类。|  
|`<Type>`|将反射策略应用到一个嵌套类型。|  
|[\<TypeInstantiation>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md)|将反射策略应用到一个构造泛型类型。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<Application>](../../../docs/framework/net-native/application-element-net-native.md)|作为应用程序范围内的类型和元数据可以反应在运行时间的类型成员的容器而服务。|  
|[\<Assembly>](../../../docs/framework/net-native/assembly-element-net-native.md)|将反射策略应用到指定程序集中的所有类型。|  
|[\<Library>](../../../docs/framework/net-native/library-element-net-native.md)|定义包含元数据在运行时间可以用于反射的类型和类型成员的程序集。|  
|[\<Namespace>](../../../docs/framework/net-native/namespace-element-net-native.md)|将反射策略应用到命名空间中的所有类型。|  
|`<Type>`|将反射策略应用到一种类型及其所有成员。|  
|[\<TypeInstantiation>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md)|将反射策略应用到一种构造泛型类型及其所有成员。|  
  
## <a name="remarks"></a>备注  
 反射、序列化和互操作特性都是可选项。 如果这些都不存在，`<Type>` 元素会充当容器，其子类型为独立成员定义策略。  
  
 如果一个 `<Type>` 元素是 [\<Assembly>](../../../docs/framework/net-native/assembly-element-net-native.md)、[\<Namespace>](../../../docs/framework/net-native/namespace-element-net-native.md)、`<Type>` 或 [\<TypeInstantiation>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md) 元素的子元素，它会替代由父元素定义的策略设置。  
  
 一个泛型类型的 `<Type>` 元素会将其策略应用到所有不具有自身策略的实例化。 构造泛型类型的策略是由 [\<TypeInstantiation>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md) 元素定义的。  
  
 如果该类型是一个泛型类型，其名称包含一个重读音符 (\`)，后面还跟着其泛型参数的编号。 例如，<xref:System.Collections.Generic.List%601?displayProperty=fullName> 类的 `<Type>` 元素的 `Name` 属性显示为 `Name="System.Collections.Generic.List`1"`。  
  
## <a name="example"></a>示例  
 以下实例使用反射来展示 <xref:System.Collections.Generic.List%601?displayProperty=fullName> 类的字段、属性和方法。 示例中的变量 `b` 是 [TextBlock](http://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) 控件。 因为实例仅仅检索了类型信息，元数据的可用性是由 `Browse` 策略设置控制的。  
  
 [!code-csharp[ProjectN_Reflection#3](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_reflection/cs/browsegenerictype1.cs#3)]  
  
 因为 <xref:System.Collections.Generic.List%601> 类的元数据并不是自动包含在 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 工具链之中，该实例在运行时间内未能显示出请求的成员信息。 为提供所需的元数据，将以下 `<Type>` 元素添加到运行时指令文件。 注意，因为我们已经提供了父 [<Namespace\>](../../../docs/framework/net-native/namespace-element-net-native.md) 元素，因此不必在 `<Type>` 元素中提供完全限定的类型名称。  
  
```xml  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
   <Application>  
      <Assembly Name="*Application*" Dynamic="Required All" />  
      <Namespace Name ="System.Collections.Generic" >  
        <Type Name="List`1" Browse="Required All" />   
     </Namespace>  
   </Application>  
</Directives>  
```  
  
## <a name="example"></a>示例  
 以下实例使用了反射来检索一个代表 <xref:System.Reflection.PropertyInfo> 属性的 <xref:System.String.Chars%2A?displayProperty=fullName> 对象。 它使用 <xref:System.Reflection.PropertyInfo.GetValue%28System.Object%2CSystem.Object%5B%5D%29?displayProperty=fullName> 方法来检索一个字符串中的七个字符的值，并在该字符串中显示所有字符。 示例中的变量 `b` 是 [TextBlock](http://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) 控件。  
  
 [!code-csharp[ProjectN_Reflection#1](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_reflection/cs/propertyinfo1.cs#1)]  
  
 因为 <xref:System.String> 对象的元数据不可用，调用 <xref:System.Reflection.PropertyInfo.GetValue%28System.Object%2CSystem.Object%5B%5D%29?displayProperty=fullName> 的方法在同 <xref:System.NullReferenceException> 工具链汇编时，在运行时间引发一个 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 异常。 要消除异常并提供必需的元数据，请将以下 `<Type>` 元素添加到运行时指令文件：  
  
```xml  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
  <Application>  
    <Assembly Name="*Application*" Dynamic="Required All" />  
    <Type Name="System.String" Dynamic="Required Public"/> -->  
  </Application>  
</Directives>  
```  
  
## <a name="see-also"></a>另请参阅  
 [运行时指令 (rd.xml) 配置文件参考](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)   
 [运行时指令元素](../../../docs/framework/net-native/runtime-directive-elements.md)   
 [运行时指令策略设置](../../../docs/framework/net-native/runtime-directive-policy-settings.md)

