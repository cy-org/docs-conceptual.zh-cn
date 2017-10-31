---
title: "COM 类示例（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- examples [C#], COM classes
- COM, exposing Visual C# objects to
ms.assetid: 6504dea9-ad1c-4993-a794-830fec5270af
caps.latest.revision: 17
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: a759a7dcd211207c8740dd99d592daa509ddec47
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="example-com-class-c-programming-guide"></a>COM 类示例（C# 编程指南）
下面是将公开为 COM 对象的类的示例。 在将此代码放置在 .cs 文件中并添加到项目后，将“注册 COM 互操作”属性设置为“True”。 有关详细信息，请参阅 [NIB：如何：为 COM 互操作注册组件](http://msdn.microsoft.com/en-us/4de7d474-56e8-4027-994d-d47ca4725c5e)。  
  
 对 COM 公开 Visual C# 对象需要声明类接口、事件接口（如有必要）和类本身。 类成员必须遵循这些规则才能显示在 COM 中：  
  
-   类必须是公开的。  
  
-   属性、方法和事件必须是公开的。  
  
-   必须在类接口上声明属性和方法。  
  
-   必须在事件接口中声明事件。  
  
 该类中未在这些接口中声明的其他公共成员将对 COM 不可见，但它们对其他 .NET Framework 对象可见。  
  
 若要对 COM 公开属性和方法，则必须在类接口上声明这些属性和方法，将它们标记为 `DispId` 属性，并在类中实现它们。 在接口中声明成员的顺序是用于 COM vtable 的顺序。  
  
 若要从类中公开事件，则必须在事件接口上声明这些事件并将其标记为 `DispId` 属性。 此类不应实现此接口。  
  
 此类实现此类接口；它可以实现多个接口，但第一个实现将为默认类接口。 在此处实现向 COM 公开的方法和属性。 它们必须标记为公共，并且必须匹配类接口中的声明。 此外，在此处声明此类引发的事件。 它们必须标记为公共，并且必须匹配事件接口中的声明。  
  
## <a name="example"></a>示例  
 [!code-cs[csProgGuideInterop#8](../../../csharp/programming-guide/interop/codesnippet/CSharp/example-com-class_1.cs)]  
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [互操作性](../../../csharp/programming-guide/interop/index.md)   
 [“项目设计器”->“生成”页 (C#)](/visualstudio/ide/reference/build-page-project-designer-csharp)

