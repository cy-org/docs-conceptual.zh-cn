---
title: "在项目级 Imports&quot; 中指定 Namespace 或类型&lt;qualifiedelementname&gt;不包含任何公共成员，或者找不到 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc40057
- bc40057
dev_langs:
- VB
helpviewer_keywords:
- BC40057
ms.assetid: 4ae3506e-2ebe-4ff3-995d-14ac60db5e9f
caps.latest.revision: 10
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
ms.openlocfilehash: 5dae6f92f573a57d0974c860500bc7420f55a94f
ms.lasthandoff: 03/13/2017

---
# <a name="namespace-or-type-specified-in-the-project-level-imports-39ltqualifiedelementnamegt39-doesn39t-contain-any-public-member-or-cannot-be-found"></a>在项目级 Imports' 中指定 Namespace 或类型&lt;qualifiedelementname&gt;不包含任何公共成员，或者找不到
在项目级 Imports' 中指定 Namespace 或类型\<qualifiedelementname&1;> 不包含任何公共成员，或者找不到。 请确保该命名空间或类型定义，其中包含至少一个公共成员。 请确保别名名称不包含其他别名。  
  
 一个项目的导入属性指定的包含元素不能被发现，或未定义任何`Public`成员。  
  
 一个*包含元素*可以是命名空间、 类、 结构、 模块、 接口或枚举。 包含的元素可包含成员，如变量、 过程或其他包含的元素。  
  
 导入的目的是允许您的代码来访问命名空间或类型成员，而不必限定它们。 您的项目可能还需要添加对命名空间或类型的引用。 详细信息，请参阅"导入包含元素"中[对声明的元素的引用](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)。  
  
 如果编译器找不到指定的包含元素，它不能解决使用它的引用。 如果它找到的元素，但该元素不公开任何`Public`成员，则任何引用都不会成功。 在任一情况下是没有意义的导入元素。  
  
 您使用**项目设计器**可指定要导入元素。 使用**导入的命名空间**部分**引用**页。 您可以到达**项目设计器**通过双击**我的项目**图标**解决方案资源管理器**。  
  
 **错误 ID:** BC40057  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
1.  打开**项目设计器**并切换到**引用**页。  
  
2.  在**导入的命名空间**部分中，验证是否可以从您的项目访问包含元素。  
  
3.  验证包含元素公开至少一个`Public`成员。  
  
## <a name="see-also"></a>另请参阅  
 [项目设计器 ->“引用”页 (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/references-page-project-designer-visual-basic)   
 [NIB 如何︰ 修改项目属性和配置设置](http://msdn.microsoft.com/en-us/e7184bc5-2f2b-4b4f-aa9a-3ecfcbc48b67)   
 [公共](../../../visual-basic/language-reference/modifiers/public.md)   
 [在 Visual Basic 中的命名空间](../../../visual-basic/programming-guide/program-structure/namespaces.md)   
 [对已声明元素的引用](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
