---
title: "反射 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
ms.assetid: d991bc0f-d16a-4ac5-9351-70e5c5b9891b
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 3ae042933575849e105d7b681634a61319c1d6ee
ms.lasthandoff: 03/13/2017

---
# <a name="reflection-visual-basic"></a>反射 (Visual Basic)
反射提供的对象 (类型的<xref:System.Type>)，用于描述程序集、 模块和类型。</xref:System.Type> 可以使用反射动态地创建一种类型的实例，将类型绑定到现有对象，或从现有对象中获得的类型和调用它的方法或访问其字段和属性。 如果使用的在代码中的属性，可以利用反射来访问它们。 有关详细信息，请参阅[属性](https://msdn.microsoft.com/library/5x6cd29c)。  
  
 下面是一个简单的示例使用静态方法的反射的`GetType`-继承中的所有类型`Object`基类派生来获取变量的类型︰  
  
```vb  
' Using GetType to obtain type information:  
Dim i As Integer = 42  
Dim type As System.Type = i.GetType()  
System.Console.WriteLine(type)  
```  
  
 输出为︰  
  
 `System.Int32`  
  
 下面的示例使用反射来获取已加载程序集的完整名称。  
  
```vb  
' Using Reflection to get information from an Assembly:  
Dim info As System.Reflection.Assembly = GetType(System.Int32).Assembly  
System.Console.WriteLine(info)  
```  
  
 输出为︰  
  
 `mscorlib, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089`  
  
## <a name="reflection-overview"></a>反射概述  
 反射是在以下情况下有用︰  
  
-   当您需要访问程序的元数据中的特性。 有关详细信息，请参阅[检索信息存储在特性中](http://msdn.microsoft.com/library/37dfe4e3-7da0-48b6-a3d9-398981524e1c)。  
  
-   检查和实例化程序集中的类型。  
  
-   构建在运行时的新类型。 使用中<xref:System.Reflection.Emit>。</xref:System.Reflection.Emit>类  
  
-   用于执行后期绑定，访问在运行时创建的类型上的方法。 请参阅主题[动态加载和使用类型](http://msdn.microsoft.com/library/db985bec-5942-40ec-b13a-771ae98623dc)。  
  
## <a name="related-sections"></a>相关章节  
 更多相关信息：  
  
-   [反射](http://msdn.microsoft.com/library/d1a58e7f-fb39-4d50-bf84-e3b8f9bf9775)  
  
-   [查看类型信息](http://msdn.microsoft.com/library/7e7303a9-4064-4738-b4e7-b75974ed70d2)  
  
-   [反射和泛型类型](http://msdn.microsoft.com/library/f7180fc5-dd41-42d4-8a8e-1b34288e06de)  
  
-   <xref:System.Reflection.Emit></xref:System.Reflection.Emit>  
  
-   [检索存储在特性中的信息](http://msdn.microsoft.com/library/37dfe4e3-7da0-48b6-a3d9-398981524e1c)  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 编程指南](../../../visual-basic/programming-guide/index.md)   
 [公共语言运行时中的程序集](https://msdn.microsoft.com/library/k3677y81)
