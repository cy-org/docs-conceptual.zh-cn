---
title: "如何︰ 重载参数 (Visual Basic 中) 的数量不确定的过程 |Microsoft 文档"
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
- procedures, parameters
- procedure overloading, indefinite number of parameters
- procedures, defining
- Visual Basic code, procedures
- procedure parameters
- procedures, overloading
- procedures, multiple versions
ms.assetid: c7042de2-2422-4039-94e8-ac298896af69
caps.latest.revision: 18
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
ms.openlocfilehash: c7e09bd482e35c7ce7f28a6cc7de0379b7cc89f6
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters-visual-basic"></a>如何：重载参数数量不确定的过程 (Visual Basic)
如果过程具有[ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md)参数，不能定义带有参数数组的一维数组的重载的版本。 有关详细信息，请参阅"隐式重载为 ParamArray 参数"[中重载过程注意事项](./considerations-in-overloading-procedures.md)。  
  
### <a name="to-overload-a-procedure-that-takes-a-variable-number-of-parameters"></a>若要重载采用可变数目的参数的过程  
  
1.  确定该过程，并调用代码逻辑受益于重载版本多于`ParamArray`参数。 请参阅中的"重载和参数"[重载过程注意事项](./considerations-in-overloading-procedures.md)。  
  
2.  确定的第几个提供的值，则过程应接受的参数列表的可变部分中。 这可能包括没有值，这种情况，并且它可能包含一个一维数组的大小写。  
  
3.  对于每个可接受提供的值数目，编写`Sub`或`Function`定义相应的参数列表的声明语句。 请不要使用`Optional`或`ParamArray`关键字在此重载版本。  
  
4.  在每个声明，前面`Sub`或`Function`关键字与[重载](../../../../visual-basic/language-reference/modifiers/overloads.md)关键字。  
  
5.  每个声明之后编写调用代码提供对应于该声明的参数列表值时应执行该过程代码。  
  
6.  终止与每个过程`End Sub`或`End Function`根据语句。  
  
## <a name="example"></a>示例  
 下面的示例演示用定义的过程[ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md)参数，然后一组等效的重载过程。  
  
 [!code-vb[VbVbcnProcedures #&69;](./codesnippet/VisualBasic/how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters_1.vb)]  
  
 [!code-vb[VbVbcnProcedures #&70;](./codesnippet/VisualBasic/how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters_2.vb)]  
  
 无法重载这种过程，将一维数组的参数数组的参数列表。 但是，您可以使用其他隐式重载的签名。 下面的声明说明这一点。  
  
 [!code-vb[VbVbcnProcedures #&71;](./codesnippet/VisualBasic/how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters_3.vb)]  
  
 不需要测试是否调用代码提供一个或多个值中的重载版本的代码`ParamArray`参数，或如果是这样，多少。 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]将控制权传递给调用的参数列表匹配的版本。  
  
## <a name="compiling-the-code"></a>编译代码  
 因为与过程`ParamArray`参数相当于一组重载版本，不能重载带有对应于任何这些隐式重载的参数列表的此类的过程。 有关详细信息，请参阅[中重载过程注意事项](./considerations-in-overloading-procedures.md)。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 每当您处理的可能会无限期地大数组，都无限大某种内部容量的您的应用程序的风险。 如果接受一个参数数组时，应测试调用代码传递给它，该数组的长度，并采取相应的措施，如果对于您的应用程序来说太大。  
  
## <a name="see-also"></a>另请参阅  
 [过程](./index.md)   
 [过程参数和变量](./procedure-parameters-and-arguments.md)   
 [可选参数](./optional-parameters.md)   
 [参数数组](./parameter-arrays.md)   
 [过程重载](./procedure-overloading.md)   
 [故障排除过程](./troubleshooting-procedures.md)   
 [如何︰ 定义一个过程的多个版本](./how-to-define-multiple-versions-of-a-procedure.md)   
 [如何︰ 调用重载的过程](./how-to-call-an-overloaded-procedure.md)   
 [如何︰ 重载带有可选参数的过程](./how-to-overload-a-procedure-that-takes-optional-parameters.md)   
 [重载决策](./overload-resolution.md)
