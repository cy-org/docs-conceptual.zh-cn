---
title: "Me、 My、 MyBase 和 MyClass 在 Visual Basic |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- MyClass
- vb.Me
- MyBase
- vb.MyBase
- Me
- vb.MyClass
- vb.This
- vb.My
dev_langs:
- VB
helpviewer_keywords:
- My object
- self-reference, Me keyword
- MyClass keyword, relationship to similar programming elements
- Me keyword, relationship to similar programming elements
- Me keyword, referring to the current instance of an object
- Me keyword
- self-reference
- current instance, Me keyword
- MyBase keyword, relationship to similar programming elements
ms.assetid: f8e241ae-b1ed-4886-9aa0-08c632154029
caps.latest.revision: 15
author: dotnet-bot
ms.author: dotnetcontent
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 59dba8961712537367db9a60e8b8ba68bcb6a1ea
ms.lasthandoff: 03/13/2017

---
# <a name="me-my-mybase-and-myclass-in-visual-basic"></a>Visual Basic 中的 Me、My、MyBase 和 MyClass
`Me``My`， `MyBase`，和`MyClass`中[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]具有类似的名称，但不同的用途。 本主题将介绍其中每个实体以便将它们区分开来。  
  
## <a name="me"></a>Me  
 `Me`关键字提供了一种方法来指代类或当前正在其中执行代码的结构的特定实例。 `Me`行为类似的对象变量或结构变量引用当前实例。 使用`Me`很适合用于将有关当前执行实例的类或结构的信息传递给另一个类、 结构或模块中的过程。  
  
 例如，假设在模块中有下面的过程。  
  
```  
Sub ChangeFormColor(FormName As Form)  
   Randomize()  
   FormName.BackColor = Color.FromArgb(Rnd() * 256, Rnd() * 256, Rnd() * 256)  
End Sub  
```  
  
 您可以调用此过程，并将传递的当前实例<xref:System.Windows.Forms.Form>作为通过使用以下语句参数的类。</xref:System.Windows.Forms.Form>  
  
```  
ChangeFormColor(Me)  
```  
  
## <a name="my"></a>My  
 `My`功能提供对多种容易、 直观访问[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]类，从而[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]用户与计算机、 应用程序、 设置、 资源等进行交互。  
  
## <a name="mybase"></a>MyBase  
 `MyBase`关键字的行为类似于一个类的当前实例的基类引用的对象变量。 `MyBase`通常用于访问基类成员被重写或派生类中被隐藏。 `MyBase.New`用于从派生的类构造函数中显式调用基类构造函数。  
  
## <a name="myclass"></a>MyClass  
 `MyClass`关键字的行为类似于最初实现的类的当前实例引用的对象变量。 `MyClass`类似于`Me`，但在其上的所有方法调用将被都视为是`NotOverridable`。  
  
## <a name="see-also"></a>另请参阅  
 [继承的基础知识](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)
