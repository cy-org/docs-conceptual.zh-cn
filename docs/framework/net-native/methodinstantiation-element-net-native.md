---
title: "&lt;方法实例化&gt;元素 (.NET Native)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a3355d78-2a88-4109-8521-830d7cae260a
caps.latest.revision: 17
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: d247b2ea8a1b6a908e3eee5082638813545f144d
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="ltmethodinstantiationgt-element-net-native"></a>&lt;方法实例化&gt;元素 (.NET Native)
将运行时反射策略应用到一个构造泛型方法。  
  
## <a name="syntax"></a>语法  
  
```xml  
<MethodInstantiation Name="method_name"  
                     Signature="method_signature"  
                     Arguments="method_arguments"  
                     Browse="policy_type"  
                     Dynamic="policy_type" />  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|特性类型|描述|  
|---------------|--------------------|-----------------|  
|`Name`|常规|必需的特性。 指定方法名称。|  
|`Signature`|常规|可选特性。 指定该类型的命名参数。 多个命名参数由逗号分隔。 `Signature` 特性用于区分重载方法。|  
|`Arguments`|常规|必需的特性。 指定泛型类型参数。 如果存在多个自变量，它们之间用逗号分割。|  
|`Browse`|映像|可选特性。 控制对该方法信息的查询或列举该方法，但并不在运行时间启用任何动态调用。|  
|`Dynamic`|映像|可选特性。 控制运行时对构造函数或方法的访问，以启用动态编程。 该策略确保一个成员可在运行时间内得到调用。|  
  
## <a name="name-attribute"></a>Name 特性  
  
|值|描述|  
|-----------|-----------------|  
|method_name|方法名。 该方法的类型是由 [\<Type>](../../../docs/framework/net-native/type-element-net-native.md) 或 [\<TypeInstantiation>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md) 父元素定义的。|  
  
## <a name="signature-attribute"></a>签名特性  
  
|值|描述|  
|-----------|-----------------|  
|method_signature|指定该类型的命名参数。 如果存在多个参数，它们之间用逗号分割。|  
  
## <a name="arguments-attribute"></a>参数特性  
  
|值|描述|  
|-----------|-----------------|  
|method_arguments|指定泛型类型参数。 如果存在多个参数，它们之间用逗号分割。 每个参数必须包含一个完全限定的类型名称。|  
  
## <a name="all-other-attributes"></a>所有其他特性  
  
|值|描述|  
|-----------|-----------------|  
|policy_setting|该设置将应用到这个方法的策略类型。 可能值为 `Auto`、`Excluded`、`Included` 和 `Required`。 有关详细信息，请参阅[运行时指令策略设置](../../../docs/framework/net-native/runtime-directive-policy-settings.md)。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<Type>](../../../docs/framework/net-native/type-element-net-native.md)|将反射策略应用到一种类型及其所有成员。|  
|[\<TypeInstantiation>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md)|将反射策略应用到一种构造泛型类型及其所有成员。|  
  
## <a name="remarks"></a>备注  
 `<MethodInstantiation>` 元素替代其相应的开发泛型方法的运行时反射策略。  
  
## <a name="see-also"></a>另请参阅  
 [运行时指令 (rd.xml) 配置文件参考](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)   
 [运行时指令元素](../../../docs/framework/net-native/runtime-directive-elements.md)   
 [运行时指令策略设置](../../../docs/framework/net-native/runtime-directive-policy-settings.md)   
 [\<Method> 元素](../../../docs/framework/net-native/method-element-net-native.md)

