---
title: "&lt;Library&gt; 元素 (.NET Native)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f642276b-33fb-4a81-b882-8808c31ba69e
caps.latest.revision: 14
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 4006b18e91b79d5f31649a0a15a18b9f7f28c38e
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="ltlibrarygt-element-net-native"></a>&lt;Library&gt; 元素 (.NET Native)
定义包含元数据在运行时间可以用于反射的类型和类型成员的程序集。  
  
 \<Directives> 元素  
\<Library> 元素  
  
## <a name="syntax"></a>语法  
  
```xml  
<Library Name="assembly_name" />  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`Name`|必需的特性。 指定一个程序集的名称。 这个 `<Library>` 元素的子元素为在这个程序集中找到的类型和类型成员定义运行时反射策略。|  
  
## <a name="name-attribute"></a>Name 特性  
  
|值|描述|  
|-----------|-----------------|  
|assembly_name|程序集的简单名称，不要包含文件扩展名。 此特性对应 <xref:System.Reflection.AssemblyName.Name%2A?displayProperty=fullName> 属性。 例如，一个名为 Extensions.dll 的程序集的名称为“Extensions”。 参阅“备注”部分，了解支持对来自程序集的元数据有条件包含的 assembly_name 的一种特殊形式。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<Assembly>](../../../docs/framework/net-native/assembly-element-net-native.md)|将策略应用到特定程序集中的所有类型。|  
|[\<Namespace>](../../../docs/framework/net-native/namespace-element-net-native.md)|将策略应用到特定命名空间中的所有类型。|  
|[\<Type>](../../../docs/framework/net-native/type-element-net-native.md)|将策略应用到一个特定类型，例如一个类或结构。|  
|[\<TypeInstantiation>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md)|将策略应用到一个构造泛型类型。 例如，一个 [\<TypeInstantiation>](../../../docs/framework/net-native/typeinstantiation-element-net-native.md) 元素可用于为一个 `List<String>` 类型定义策略。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[\<Directives>](../../../docs/framework/net-native/directives-element-net-native.md)|运行时指令文件的根元素。|  
  
## <a name="remarks"></a>备注  
 [\<Directives>](../../../docs/framework/net-native/directives-element-net-native.md) 元素可包括零个、一个或多个 `<Library>` 元素。  
  
 `<Library>` 元素充当容器，用来定义其元数据在运行时间需要存在的程序元素；此元素不表示策略。 在编译时间，编译器工具仅搜索由 `<Library>` 元素指定的库，以查找其子元素识别出的程序元素。 相比而言，编译器工具搜索 .NET Framework 核心库等所有库，以查找由 [\<Application>](../../../docs/framework/net-native/application-element-net-native.md) 元素识别出的子元素。  
  
 `<Library>` 指令可以有条件地使用。 如果 `<Library>` 元素名称的前后都有一个星号 (*)，`<Library>` 指令仅在星号之间指定的程序库被该应用引用时才有效。 例如，以下运行时指令仅在 Utillities.dll 程序库被应用引用时才适用。  
  
```xml  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
  <Library Name="*Utilities*">  
   ...  
  </Library>  
</Directives>  
```  
  
## <a name="see-also"></a>另请参阅  
 [\<Application> 元素](../../../docs/framework/net-native/application-element-net-native.md)   
 [\<Directives> 元素](../../../docs/framework/net-native/directives-element-net-native.md)   
 [运行时指令 (rd.xml) 配置文件参考](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)   
 [运行时指令元素](../../../docs/framework/net-native/runtime-directive-elements.md)

