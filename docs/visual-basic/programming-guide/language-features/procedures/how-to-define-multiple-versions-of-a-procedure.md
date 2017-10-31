---
title: "如何︰ 定义多个版本的过程 (Visual Basic 中) |Microsoft 文档"
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
helpviewer_keywords:
- procedures, defining
- Visual Basic code, procedures
- procedures, overloading
- procedures, multiple versions
- procedure overloading, multiple versions
ms.assetid: 71ccdd66-1b00-4b66-bee4-6926c0d696f4
caps.latest.revision: 14
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
ms.openlocfilehash: 0228083ce00a0f552227fd7ae8f0f5a24f65148e
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-define-multiple-versions-of-a-procedure-visual-basic"></a>如何：定义一个过程的多个版本 (Visual Basic)
可以通过多个版本中定义的过程*重载*它在每个版本使用相同的名称但不同的参数列表。 重载的目的是定义一个过程的几个密切相关的版本而无需将它们按名称区分开来。  
  
 有关详细信息，请参阅[过程重载](./procedure-overloading.md)。  
  
### <a name="to-define-multiple-versions-of-a-procedure"></a>若要定义一个过程的多个版本  
  
1.  编写`Sub`或`Function`你想要定义该过程的每个版本的声明语句。 在每个声明中使用相同的过程名称。  
  
2.  在前面上`Sub`或`Function`关键字在与每个声明[重载](../../../../visual-basic/language-reference/modifiers/overloads.md)关键字。 （可选） 可以省略`Overloads`在声明中，但如果您将其包括在任何声明，您必须将其包括在每个声明。  
  
3.  后面每个声明语句中，编写过程代码以处理调用的代码提供了该版本的参数列表匹配的参数的特定情况。 无需测试提供的参数调用的代码具有控制权。 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]将控制权传递给您的过程中匹配的版本。  
  
4.  终止与该过程的每个版本`End Sub`或`End Function`根据语句。  
  
## <a name="example"></a>示例  
 下面的示例定义`Sub`过程来针对客户的帐户余额发送一个事务。 它使用`Overloads`关键字来定义两个版本的过程中，一个接受按帐户名称和其他客户。  
  
 [!code-vb[VbVbcnProcedures #&72;](./codesnippet/VisualBasic/how-to-define-multiple-versions-of-a-procedure_1.vb)]  
  
 调用代码可以获取客户标识为`String`或`Integer`，然后在任一情况下使用相同的调用语句。  
  
 有关如何以调用这些版本的信息`post`的过程中，请参阅[如何︰ 调用重载过程](./how-to-call-an-overloaded-procedure.md)。  
  
## <a name="compiling-the-code"></a>编译代码  
 请确保每个重载版本具有相同的过程名称但不同的参数列表。  
  
## <a name="see-also"></a>另请参阅  
 [过程](./index.md)   
 [过程参数和变量](./procedure-parameters-and-arguments.md)   
 [故障排除过程](./troubleshooting-procedures.md)   
 [如何︰ 重载带有可选参数的过程](./how-to-overload-a-procedure-that-takes-optional-parameters.md)   
 [如何︰ 重载参数数量不确定的过程](./how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)   
 [重载过程注意事项](./considerations-in-overloading-procedures.md)   
 [重载决策](./overload-resolution.md)
