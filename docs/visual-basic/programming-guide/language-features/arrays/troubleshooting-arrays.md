---
title: "数组疑难解答 (Visual Basic) |Microsoft 文档"
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
- troubleshooting arrays
- arrays [Visual Basic], initialization errors
- troubleshooting Visual Basic, arrays
- arrays [Visual Basic], compilation errors
- arrays [Visual Basic], declaration errors
- arrays [Visual Basic], troubleshooting
ms.assetid: f4e971c7-c0a4-4ed7-a77a-8d71039f266f
caps.latest.revision: 17
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
ms.openlocfilehash: db38c0c2a4f8b74a6b862f86f426b4d8837f4424
ms.lasthandoff: 03/13/2017

---
# <a name="troubleshooting-arrays-visual-basic"></a>数组疑难解答 (Visual Basic)
此页列出与数组一起使用时可能会出现一些常见问题。  
  
## <a name="compilation-errors-declaring-and-initializing-an-array"></a>编译错误声明和初始化数组  
 因误解而声明、 创建和初始化数组的规则，将产生编译错误。 错误的最常见原因如下所示︰  
  
-   提供[New 运算符](../../../../visual-basic/language-reference/operators/new-operator.md)子句后在数组变量声明中指定维的长度。 下面的代码行显示了这种类型的无效声明。  
  
     `Dim INVALIDsingleDimByteArray(2) As Byte = New Byte()`  
  
     `Dim INVALIDtwoDimShortArray(1, 1) As Short = New Short(,)`  
  
     `Dim INVALIDjaggedByteArray(1)() As Byte = New Byte()()`  
  
-   为多个顶级数组交错数组的指定维的长度。 下面的代码行将演示这种类型的无效的声明。  
  
     `Dim INVALIDjaggedByteArray(1)(1) As Byte`  
  
-   省略`New`关键字时指定的元素值。 下面的代码行将演示这种类型的无效的声明。  
  
     `Dim INVALIDoneDimShortArray() As Short = Short() {0, 1, 2, 3}`  
  
-   提供`New`子句时没有使用大括号 (`{}`)。 下面的代码行显示了这种类型的无效声明。  
  
     `Dim INVALIDsingleDimByteArray() As Byte = New Byte()`  
  
     `Dim INVALIDsingleDimByteArray() As Byte = New Byte(2)`  
  
     `Dim INVALIDtwoDimShortArray(,) As Short = New Short(,)`  
  
     `Dim INVALIDtwoDimShortArray(,) As Short = New Short(1, 1)`  
  
## <a name="accessing-an-array-out-of-bounds"></a>访问超出界限的数组  
 初始化数组的过程将分配给每个维度的一个上限和下限。 每次访问该数组的元素必须指定有效的索引或下标，对于每个维度。 如果任何索引低于其下限或高于其上限<xref:System.IndexOutOfRangeException>异常结果。</xref:System.IndexOutOfRangeException> 编译器无法检测到这样的错误，因此在运行时就会出错。  
  
### <a name="determining-bounds"></a>确定边界  
 如果另一个组件将数组传递给您的代码，例如作为过程参数，您不知道该数组的大小或它的维的长度。 您应首先确定每个维度的数组上界，然后再尝试访问任何元素。 如果数组已创建通过某种方式以外[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]`New`子句，下限可能不是 0，并且是最安全的方式确定该下限。  
  
### <a name="specifying-the-dimension"></a>指定维度  
 在确定多维数组的边界时，请注意如何指定的维度。 `dimension`参数<xref:System.Array.GetLowerBound%2A>和<xref:System.Array.GetUpperBound%2A>方法都是从 0 开始时`Rank`参数[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]<xref:Microsoft.VisualBasic.Information.LBound%2A>和<xref:Microsoft.VisualBasic.Information.UBound%2A>函数是从 1 开始。</xref:Microsoft.VisualBasic.Information.UBound%2A> </xref:Microsoft.VisualBasic.Information.LBound%2A> </xref:System.Array.GetUpperBound%2A> </xref:System.Array.GetLowerBound%2A>  
  
## <a name="see-also"></a>另请参阅  
 [数组](../../../../visual-basic/programming-guide/language-features/arrays/index.md)   
 [如何︰ 初始化数组变量在 Visual Basic 中](../../../../visual-basic/programming-guide/language-features/arrays/how-to-initialize-an-array-variable.md)
