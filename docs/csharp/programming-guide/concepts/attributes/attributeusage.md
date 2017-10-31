---
title: AttributeUsage (C#)
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 22c45568-9a6a-4c2f-8480-f38c1caa0a99
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: c008c1a696e93bc3b756a926a046aa5a6942bc10
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="attributeusage-c"></a>AttributeUsage (C#)
确定如何使用自定义特性类。 `AttributeUsage` 是一个特性，可应用于自定义特性定义，以控制如何应用新特性。 在显式应用时的默认设置如下：  
  
```csharp  
[System.AttributeUsage(System.AttributeTargets.All,  
                   AllowMultiple = false,  
                   Inherited = true)]  
class NewAttribute : System.Attribute { }  
```  
  
 在此示例中，`NewAttribute` 类可应用于任何特性的代码实体，但只能对每个实体应用一次。 当应用于基类时，它由派生类继承。  
  
 `AllowMultiple` 和 `Inherited` 参数是可选的，因而此代码具有相同的效果：  
  
```csharp  
[System.AttributeUsage(System.AttributeTargets.All)]  
class NewAttribute : System.Attribute { }  
```  
  
 第一个 `AttributeUsage` 参数必须是 <xref:System.AttributeTargets> 枚举的一个或多个元素。 可将多个目标类型与 OR 运算符链接在一起，如下所示：  
  
```csharp  
using System;  

[AttributeUsage(AttributeTargets.Property | AttributeTargets.Field)]  
class NewPropertyOrFieldAttribute : Attribute { }  
```  
  
 如果 `AllowMultiple` 参数设置为 `true`，则结果特性可多次应用于单个实体，如下所示：  
  
```csharp  
using System;  

[AttributeUsage(AttributeTargets.Class, AllowMultiple = true)]  
class MultiUseAttr : Attribute { }  
  
[MultiUseAttr]  
[MultiUseAttr]  
class Class1 { }  
  
[MultiUseAttr, MultiUseAttr]  
class Class2 { }  
```  
  
 在本例中，`MultiUseAttr` 可重复应用，因为 `AllowMultiple` 设置为 `true`。 所显示的两种用于应用多个特性的格式均有效。  
  
 如果 `Inherited` 设置为 `false`，那么特性不会由派生自已特性化的类的类继承。 例如:   
  
```csharp  
using System;  

[AttributeUsage(AttributeTargets.Class, Inherited = false)]  
class Attr1 : Attribute { }  
  
[Attr1]  
class BClass { }  
  
class DClass : BClass { }  
```  
  
 在本例中，`Attr1` 不会通过继承应用于 `DClass`。  
  
## <a name="remarks"></a>备注  
 `AttributeUsage` 特性是单次使用的特性 -- 它无法应用于同一个类超过一次。 `AttributeUsage` 是 <xref:System.AttributeUsageAttribute> 的别名。  
  
 有关详细信息，请参阅[使用反射访问特性 (C#)](../../../../csharp/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md)。  
  
## <a name="example"></a>示例  
 以下示例演示 `Inherited` 和 `AllowMultiple` 参数对 `AttributeUsage` 特性的影响，以及如何枚举应用于类的自定义特性。  
  
```csharp  
using System;  

// Create some custom attributes:  
[AttributeUsage(System.AttributeTargets.Class, Inherited = false)]  
class A1 : System.Attribute { }  
  
[AttributeUsage(System.AttributeTargets.Class)]  
class A2 : System.Attribute { }  
  
[AttributeUsage(System.AttributeTargets.Class, AllowMultiple = true)]  
class A3 : System.Attribute { }  
  
// Apply custom attributes to classes:  
[A1, A2]  
class BaseClass { }  
  
[A3, A3]  
class DerivedClass : BaseClass { }  
  
public class TestAttributeUsage  
{  
    static void Main()  
    {  
        BaseClass b = new BaseClass();  
        DerivedClass d = new DerivedClass();  
  
        // Display custom attributes for each class.  
        Console.WriteLine("Attributes on Base Class:");  
        object[] attrs = b.GetType().GetCustomAttributes(true);  
        foreach (Attribute attr in attrs)  
        {  
            Console.WriteLine(attr);  
        }  
  
        Console.WriteLine("Attributes on Derived Class:");  
        attrs = d.GetType().GetCustomAttributes(true);  
        foreach (Attribute attr in attrs)  
        {  
            Console.WriteLine(attr);  
        }  
    }  
}  
```  
  
## <a name="sample-output"></a>示例输出  
  
```  
Attributes on Base Class:  
A1  
A2  
Attributes on Derived Class:  
A3  
A3  
A2  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Attribute>   
 <xref:System.Reflection>   
 [C# 编程指南](../../../../csharp/programming-guide/index.md)   
 [特性](https://msdn.microsoft.com/library/5x6cd29c)   
 [反射 (C#)](../../../../csharp/programming-guide/concepts/reflection.md)   
 [特性](../../../../csharp/programming-guide/concepts/attributes/index.md)   
 [创建自定义特性 (C#)](../../../../csharp/programming-guide/concepts/attributes/creating-custom-attributes.md)   
 [使用反射访问特性 (C#)](../../../../csharp/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md)

