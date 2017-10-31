---
title: "自定义的对象是在我 (Visual Basic) 中的可用 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- My namespace, customizing
- My namespace
ms.assetid: 4e8279c2-ed5b-4681-8903-8a6671874000
caps.latest.revision: 12
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
ms.openlocfilehash: 6791398270e4348adf356eb36a385bfbefde873c
ms.lasthandoff: 03/13/2017

---
# <a name="customizing-which-objects-are-available-in-my-visual-basic"></a>自定义 My 中可用的对象 (Visual Basic)
本主题介绍如何控制哪些`My`通过设置项目的情况下启用对象`_MYTYPE`条件编译常数。 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]集成开发环境 (IDE) 保留`_MYTYPE`项目的类型与同步的项目的条件编译常数。  
  
## <a name="predefined-mytype-values"></a>预定义的 _MYTYPE 值  
 必须使用`/define`编译器选项来设置`_MYTYPE`条件编译常数。 指定您自己的值时`_MYTYPE`常量，您必须括起来的字符串值反斜杠/英文引号连用 (\\") 序列。 例如，您可以使用︰  
  
```  
/define:_MYTYPE=\"WindowsForms\"  
```  
  
 下表显示哪些`_MYTYPE`条件编译常量设置为几种项目类型。  
  
|项目类型|_MYTYPE 值|  
|------------------|--------------------|  
|类库|"Windows"|  
|控制台应用程序|"控制台"|  
|Web|"Web"|  
|Web 控件库|"WebControl"|  
|Windows 应用程序|"WindowsForms"|  
|Windows 应用程序，开始着手解决自定义时`Sub Main`|"WindowsFormsWithCustomSubMain"|  
|Windows 控件库|"Windows"|  
|Windows 服务|"控制台"|  
|空|"空"|  
  
> [!NOTE]
>  所有条件编译字符串比较都都区分大小写，而不考虑如何`Option Compare`语句设置。  
  
## <a name="dependent-my-compilation-constants"></a>相关 _MY 编译常数  
 `_MYTYPE`条件编译常数，反过来，控制的其他几个值`_MY`编译常量︰  
  
|_MYTYPE|_MYAPPLICATIONTYPE|_MYCOMPUTERTYPE|_MYFORMS|_MYUSERTYPE|_MYWEBSERVICES|  
|--------------|-------------------------|----------------------|---------------|------------------|---------------------|  
|"控制台"|"控制台"|"Windows"|未定义|"Windows"|TRUE|  
|"自定义"|未定义|未定义|未定义|未定义|未定义|  
|"空"|未定义|未定义|未定义|未定义|未定义|  
|"Web"|未定义|"Web"|FALSE|"Web"|FALSE|  
|"WebControl"|未定义|"Web"|FALSE|"Web"|TRUE|  
|"Windows"或""|"Windows"|"Windows"|未定义|"Windows"|TRUE|  
|"WindowsForms"|"WindowsForms"|"Windows"|TRUE|"Windows"|TRUE|  
|"WindowsFormsWithCustomSubMain"|"控制台"|"Windows"|TRUE|"Windows"|TRUE|  
  
 默认情况下，未定义的条件编译常数解析为`FALSE`。 在编译您的项目以重写默认行为时，可以指定未定义的常数的值。  
  
> [!NOTE]
>  当`_MYTYPE`设置为"Custom"的项目包含`My`命名空间，但它不包含任何对象。 但是，将设置`_MYTYPE`到"空"，则将阻止编译器从添加`My`命名空间及其对象。  
  
 下表描述预定义值的效果`_MY`编译常量。  
  
|常量|含义|  
|--------------|-------------|  
|`_MYAPPLICATIONTYPE`|使`My.Application`，该常量是"控制台"窗口，如果"或"WindowsForms":<br /><br /> 的从<xref:Microsoft.VisualBasic.ApplicationServices.ConsoleApplicationBase>。</xref:Microsoft.VisualBasic.ApplicationServices.ConsoleApplicationBase>派生而来"控制台"版本 并且具有比"Windows"的版本较少的成员。<br />-"Windows"版本派生自<xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>以及具有比"WindowsForms"版本较少的成员。</xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase><br />-的版本"WindowsForms"`My.Application`从<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>。</xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase>派生而来 如果`TARGET`常量被定义为"winexe"，则此类包括`Sub Main`方法。|  
|`_MYCOMPUTERTYPE`|使`My.Computer`，如果该常量是"Web"或"Windows":<br /><br /> -"Web"版本派生自<xref:Microsoft.VisualBasic.Devices.ServerComputer>，并且具有比"Windows"的版本较少的成员。</xref:Microsoft.VisualBasic.Devices.ServerComputer><br />-的版本"Windows"`My.Computer`从<xref:Microsoft.VisualBasic.Devices.Computer>。</xref:Microsoft.VisualBasic.Devices.Computer>派生而来|  
|`_MYFORMS`|使`My.Forms`，如果该常量是`TRUE`。|  
|`_MYUSERTYPE`|使`My.User`，如果该常量是"Web"或"Windows":<br /><br /> -的版本"Web"`My.User`与当前 HTTP 请求的用户标识相关联。<br />-的版本"Windows"`My.User`与线程的当前主体相关联。|  
|`_MYWEBSERVICES`|使`My.WebServices`，如果该常量是`TRUE`。|  
|`_MYTYPE`|使`My.Log`， `My.Request`，和`My.Response`，如果该常量是"Web"。|  
  
## <a name="see-also"></a>请参见  
 <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase></xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>   
 <xref:Microsoft.VisualBasic.Devices.Computer></xref:Microsoft.VisualBasic.Devices.Computer>   
 <xref:Microsoft.VisualBasic.Logging.Log></xref:Microsoft.VisualBasic.Logging.Log>   
 <xref:Microsoft.VisualBasic.ApplicationServices.User></xref:Microsoft.VisualBasic.ApplicationServices.User>   
 [我如何取决于项目类型](../../../visual-basic/developing-apps/development-with-my/how-my-depends-on-project-type.md)   
 [条件编译](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)   
 [/define (Visual Basic)](../../../visual-basic/reference/command-line-compiler/define.md)   
 [My.Forms 对象](../../../visual-basic/language-reference/objects/my-forms-object.md)   
 [My.Request 对象](../../../visual-basic/language-reference/objects/my-request-object.md)   
 [My.Response 对象](../../../visual-basic/language-reference/objects/my-response-object.md)   
 [My.WebServices 对象](../../../visual-basic/language-reference/objects/my-webservices-object.md)
