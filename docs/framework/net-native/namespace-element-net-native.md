---
title: "&lt;命名空间&gt;元素 (.NET Native)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 57c614e5-18a9-4e87-bfd5-d0fe3396a192
caps.latest.revision: 20
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: f92797e9c06762602c30d7c3ed8e6b0d6e579bbf
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="ltnamespacegt-element-net-native"></a>&lt;命名空间&gt;元素 (.NET Native)
将运行时反射策略应用到一个指定的命名空间中的所有类型。  
  
## <a name="syntax"></a>语法  
  
```xml  
<Namespace Name="namespace_name"   
           Activate="policy_type"   
           Browse="policy_type" />  
           Dynamic="policy_setting"  
           Serialize="policy_setting"  
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
|`Name`|常规|必需的特性。 指定命名空间的名称。|  
|`Activate`|映像|可选特性。 控制运行时对构造函数的访问，以启用实例激活。|  
|`Browse`|映像|可选特性。 控制对有关程序元素信息的查询，但并不启用任何运行时访问。|  
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
|namespace_name|命名空间名称。 如果 \<Namespace> 元素是 [\<Application>](../../../docs/framework/net-native/application-element-net-native.md)、[\<Library>](../../../docs/framework/net-native/library-element-net-native.md) 或 [\<Assembly>](../../../docs/framework/net-native/assembly-element-net-native.md) 元素的子元素，namespace_name 必须是一个完全限定的命名空间名称。 如果 \<Namespace> 元素是另一个 \<Namespace> 元素的子元素，则 namespace_name 必须是一个相对的命名空间名称。|  
  
## <a name="all-other-attributes"></a>所有其他特性  
  
|值|描述|  
|-----------|-----------------|  
|policy_setting|该设置将应用这个策略类型到该命名空间的所有类型。 可能值为 `All`、`Auto`、`Excluded`、`Public`、`PublicAndInternal`、`Required Public`、`Required PublicAndInternal` 以及 `Required All`。 有关详细信息，请参阅[运行时指令策略设置](../../../docs/framework/net-native/runtime-directive-policy-settings.md)。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|说明|  
|-------------|-----------------|  
|`<Namespace>`|将运行时反射策略应用到一个父命名空间中的所有类型。|  
|[\<Type>](../../../docs/framework/net-native/type-element-net-native.md)|将反射策略应用到一个类型。|  
|[\<TypeInstantiation>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md)|将反射策略应用到一个构造泛型类型。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<Application>](../../../docs/framework/net-native/application-element-net-native.md)|作为应用程序范围内的类型和元数据可以反应在运行时间的类型成员的容器而服务。 [\<Application>](../../../docs/framework/net-native/application-element-net-native.md) 元素可包含零个、一个或多个 [\<Assembly>](../../../docs/framework/net-native/assembly-element-net-native.md) 元素。|  
|[\<Assembly>](../../../docs/framework/net-native/assembly-element-net-native.md)|将运行时反射策略应用到指定程序集中的所有类型。|  
|[\<Library>](../../../docs/framework/net-native/library-element-net-native.md)|定义包含元数据在运行时间可以用于反射的类型和类型成员的程序集。 [\<Library>](../../../docs/framework/net-native/library-element-net-native.md) 元素可包含零个或一个 [\<Assembly>](../../../docs/framework/net-native/assembly-element-net-native.md) 元素。|  
|`<Namespace>`|将反射策略应用到一个父命名空间中的所有类型。|  
  
## <a name="remarks"></a>备注  
 `Activate`、`Browse`、`Dynamic` 和 `Serialize` 特性都是可选项。 如果这些都不存在，`<Namespace>` 元素仅会充当子元素的容器。 如果它们存在，`<Namespace>` 元素会将运行时反射策略应用到一个指定的命名空间中的所有类型。  
  
 当它是 [\<Assembly>](../../../docs/framework/net-native/assembly-element-net-native.md) 元素的子元素时，`<Namespace>` 元素会替代 [\<Assembly>](../../../docs/framework/net-native/assembly-element-net-native.md) 元素定义的运行时反射策略。  
  
## <a name="see-also"></a>另请参阅  
 [运行时指令策略设置](../../../docs/framework/net-native/runtime-directive-policy-settings.md)   
 [运行时指令 (rd.xml) 配置文件参考](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)   
 [运行时指令元素](../../../docs/framework/net-native/runtime-directive-elements.md)

