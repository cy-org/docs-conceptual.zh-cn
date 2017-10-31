---
title: "&lt;程序集&gt;元素 (.NET Native)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cfe629eb-1106-4113-86e1-052f402d8d8b
caps.latest.revision: 24
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: df74599b5f68324540703bce6c5ca8e8805df3e7
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="ltassemblygt-element-net-native"></a>&lt;程序集&gt;元素 (.NET Native)
将运行时反射策略应用到指定程序集中的所有类型。  
  
## <a name="syntax"></a>语法  
  
```xml  
<Assembly Name="assembly_name"   
          Activate="policy_setting"  
          Browse="policy_setting"  
          Dynamic="policy_setting"  
          Serialize="policy_setting" />  
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
|`Name`|常规|必需的特性。 指定一个程序集的简单名称。|  
|`Activate`|映像|可选特性。 控制运行时对构造函数的访问，以启用实例激活。|  
|`Browse`|映像|可选特性。 控制查询或列举程序集中的类型的信息，但并不在运行时间启用任何动态访问。|  
|`Dynamic`|映像|可选特性。 控制运行时对所有类型成员的访问，包括构造函数、方法、字段、属性和事件，以启用动态编程。|  
|`Serialize`|序列化|可选特性。 控制运行时对构造函数、字段和属性的访问，使类型实例得到序列化和反序列化处理，这是通过库进行的，例如 Newtonsoft JSON 序列化程序。|  
|`DataContractSerializer`|序列化|可选特性。 控制使用 <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=fullName> 类的序列化策略。|  
|`DataContractJsonSerializer`|序列化|可选特性。 控制使用 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer?displayProperty=fullName> 类的 JSON 序列化策略。|  
|`XmlSerializer`|序列化|可选特性。 控制使用 <xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName> 类的 XML 序列化策略。|  
|`MarshalObject`|Interop|可选特性。 控制封送引用类型到 Windows 运行时和 COM 的策略。|  
|`MarshalDelegate`|Interop|可选特性。 控制将委托类型作为函数指针封送到本机代码的策略。|  
|`MarshalStructure`|Interop|可选特性。 控制封送结构到本机代码的策略。|  
  
## <a name="name-attribute"></a>Name 特性  
  
|值|描述|  
|-----------|-----------------|  
|assembly_name|程序集的简单名称，不要包含文件扩展名。 此特性对应 <xref:System.Reflection.AssemblyName.Name%2A?displayProperty=fullName> 属性。 例如，一个名为 Extensions.dll 的程序集的名称为“Extensions”。<br /><br /> 你也可以指定文本字符串 `*Application*`，从而将策略应用到你的程序包中的所有程序集，而不管这些程序集是否已加载。 `*Application*` 从不会将策略应用到 .NET Framework 程序集。|  
  
## <a name="all-other-attributes"></a>所有其他特性  
  
|值|描述|  
|-----------|-----------------|  
|policy_setting|该设置将应用这个策略类型到该程序集中的所有类型。 可能值为 `All`、`Auto`、`Excluded`、`Public`、`PublicAndInternal`、`Required Public`、`Required PublicAndInternal` 以及 `Required All`。 有关详细信息，请参阅[运行时指令策略设置](../../../docs/framework/net-native/runtime-directive-policy-settings.md)。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<Namespace>](../../../docs/framework/net-native/namespace-element-net-native.md)|将反射策略应用到一个子命名空间中的所有类型。|  
|[\<Type>](../../../docs/framework/net-native/type-element-net-native.md)|将反射策略应用到一个类型。|  
|[\<TypeInstantiation>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md)|将反射策略应用到一个构造泛型类型。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<Application>](../../../docs/framework/net-native/application-element-net-native.md)|作为应用程序范围内的类型和元数据可以反应在运行时间的类型成员的容器而服务。 [\<Application>](../../../docs/framework/net-native/application-element-net-native.md) 元素可包含零个、一个或多个 `<Assembly>` 元素。|  
|[\<Library>](../../../docs/framework/net-native/library-element-net-native.md)|定义包含元数据在运行时间可以用于反射的类型和类型成员的程序集。 [\<Library>](../../../docs/framework/net-native/library-element-net-native.md) 元素可包含零个或一个 `<Assembly>` 元素。|  
  
## <a name="remarks"></a>备注  
 `<Assembly>` 元素为一个程序集中的所有类型定义运行时策略。 它不同于 [\<Library>](../../../docs/framework/net-native/library-element-net-native.md) 元素，后者指定一个库但依赖其子元素来定义运行时反射策略。 `<Assembly>` 元素将应用到一个程序集中的所有类型，除非这些类型遭到一个子元素的替代。  
  
 以下示例展示了该如何通过分配给 `Name` 特性一个“*Application\*”值，从而将运行时策略应用到应用包内的程序集中的所有类型。 `<Assembly>` 元素必须是 [\<Application>](../../../docs/framework/net-native/application-element-net-native.md) 元素的子元素。  
  
```xml  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">   
  <Application>   
     <Assembly Name="*Application*" Dynamic="Required All" />   
  </Application>   
</Directives>  
```  
  
 `Activate`、`Browse`、`Dynamic` 和 `Serialize` 特性都是可选项。 然而，`<Assembly>` 元素必须至少包含这些属性中的一个。  
  
## <a name="see-also"></a>另请参阅  
 [运行时指令策略设置](../../../docs/framework/net-native/runtime-directive-policy-settings.md)   
 [运行时指令 (rd.xml) 配置文件参考](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)   
 [运行时指令元素](../../../docs/framework/net-native/runtime-directive-elements.md)

