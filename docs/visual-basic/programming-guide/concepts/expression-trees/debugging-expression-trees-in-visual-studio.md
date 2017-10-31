---
title: "调试 Visual Studio (Visual Basic 中) 中的表达式树 |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 492cc28f-b7a2-4c47-b582-b3c437b8a5d5
caps.latest.revision: 4
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: efbd8c19947c45b3ba15ce7b574000d56526ef45
ms.lasthandoff: 03/13/2017

---
# <a name="debugging-expression-trees-in-visual-studio-visual-basic"></a>调试 Visual Studio (Visual Basic 中) 中的表达式树
在调试您的应用程序时，可以分析结构和内容的表达式树。 若要获取的简单表达式树结构概述，可以使用`DebugView`属性，它是仅在调试模式中可用。 有关调试的详细信息，请参阅[Visual Studio 中调试](https://docs.microsoft.com/visualstudio/debugger/debugging-in-visual-studio)。  
  
 若要更好地表示表达式树的内容`DebugView`属性使用 Visual Studio 可视化工具。 有关详细信息，请参阅[创建自定义可视化工具](https://docs.microsoft.com/visualstudio/debugger/create-custom-visualizers-of-data)。  
  
### <a name="to-open-a-visualizer-for-an-expression-tree"></a>若要打开表达式目录树的可视化工具  
  
1.  单击放大镜图标旁边显示`DebugView`表达式树中的属性**数据提示**、**监视**窗口中，**自动**窗口中，或**局部变量**窗口。  
  
     将会显示可视化工具列表。  
  
2.  单击要使用的可视化工具。  
  
 以下各节中所述，可视化工具中显示每个表达式类型。  
  
## <a name="parameterexpressions"></a>ParameterExpressions  
 <xref:System.Linq.Expressions.ParameterExpression>变量的名称将显示使用"$"符号开头。</xref:System.Linq.Expressions.ParameterExpression>  
  
 如果参数不具有一个名称，向其分配一个自动生成的名称，如`$var1`或`$var2`。  
  
### <a name="examples"></a>示例  
  
-   `Expression`  
  
    ```vb  
    Dim numParam As ParameterExpression =   
    Expression.Parameter(GetType(Integer), "num")  
    ```  
  
     `DebugView` 属性  
  
     `$num`  
  
-   `Expression`  
  
    ```vb  
    Dim numParam As ParameterExpression =   
    Expression.Parameter(GetType(Integer))  
    ```  
  
     `DebugView` 属性  
  
     `$var1`  
  
## <a name="constantexpressions"></a>ConstantExpressions  
 有关<xref:System.Linq.Expressions.ConstantExpression>表示字符串的整数值的对象和`null`，显示常量的值。</xref:System.Linq.Expressions.ConstantExpression>  
  
### <a name="examples"></a>示例  
  
-   `Expression`  
  
    ```vb  
    Dim num as Integer= 10  
    Dim expr As ConstantExpression = Expression.Constant(num)  
    ```  
  
     `DebugView` 属性  
  
     10  
  
-   `Expression`  
  
    ```vb  
    Dim num As Double = 10  
    Dim expr As ConstantExpression = Expression.Constant(num)  
    ```  
  
     `DebugView` 属性  
  
     10 个 D  
  
## <a name="blockexpression"></a>BlockExpression  
 如果的一种<xref:System.Linq.Expressions.BlockExpression>对象不同于块中的最后一个表达式的类型，该类型将显示在`DebugInfo`尖括号中的属性 (\<和&1;>)。</xref:System.Linq.Expressions.BlockExpression> 否则为的一种<xref:System.Linq.Expressions.BlockExpression>不显示对象。</xref:System.Linq.Expressions.BlockExpression>  
  
### <a name="examples"></a>示例  
  
-   `Expression`  
  
    ```vb  
    Dim block As BlockExpression = Expression.Block(Expression.Constant("test"))  
    ```  
  
     `DebugView` 属性  
  
     `.Block() {`  
  
     `"test"`  
  
     `}`  
  
-   `Expression`  
  
    ```vb  
    Dim block As BlockExpression =   
    Expression.Block(GetType(Object), Expression.Constant("test"))  
    ```  
  
     `DebugView` 属性  
  
     `.Block<System.Object>() {`  
  
     `"test"`  
  
     `}`  
  
## <a name="lambdaexpression"></a>LambdaExpression  
 <xref:System.Linq.Expressions.LambdaExpression>对象会显示以及它们的委托类型。</xref:System.Linq.Expressions.LambdaExpression>  
  
 如果 lambda 表达式不具有一个名称，向其分配一个自动生成的名称，如`#Lambda1`或`#Lambda2`。  
  
### <a name="examples"></a>示例  
  
-   `Expression`  
  
    ```vb  
    Dim lambda As LambdaExpression =   
    Expression.Lambda(Of Func(Of Integer))(Expression.Constant(1))  
    ```  
  
     `DebugView` 属性  
  
     `.Lambda #Lambda1<System.Func'1[System.Int32]>() {`  
  
     `1`  
  
     `}`  
  
-   `Expression`  
  
    ```vb  
    Dim lambda As LambdaExpression =   
    Expression.Lambda(Of Func(Of Integer))(Expression.Constant(1), "SampleLamda", Nothing)  
    ```  
  
     `DebugView` 属性  
  
     `.Lambda SampleLambda<System.Func'1[System.Int32]>() {`  
  
     `1`  
  
     `}`  
  
## <a name="labelexpression"></a>LabelExpression  
 如果指定默认值为<xref:System.Linq.Expressions.LabelExpression>对象时，此值显示在之前<xref:System.Linq.Expressions.LabelTarget>对象。</xref:System.Linq.Expressions.LabelTarget> </xref:System.Linq.Expressions.LabelExpression>  
  
 `.Label`令牌指示标签的开头。 `.LabelTarget`令牌该值指示要跳转到的目标的目标。  
  
 如果标签不具有一个名称，向其分配一个自动生成的名称，如`#Label1`或`#Label2`。  
  
### <a name="examples"></a>示例  
  
-   `Expression`  
  
    ```vb  
    Dim target As LabelTarget = Expression.Label(GetType(Integer), "SampleLabel")  
    Dim label1 As BlockExpression = Expression.Block(  
    Expression.Goto(target, Expression.Constant(0)),  
    Expression.Label(target, Expression.Constant(-1)))  
    ```  
  
     `DebugView` 属性  
  
     `.Block() {`  
  
     `.Goto SampleLabel { 0 };`  
  
     `.Label`  
  
     `-1`  
  
     `.LabelTarget SampleLabel:`  
  
     `}`  
  
-   `Expression`  
  
    ```vb  
    Dim target As LabelTarget = Expression.Label()  
    Dim block As BlockExpression = Expression.Block(  
    Expression.Goto(target), Expression.Label(target))  
    ```  
  
     `DebugView` 属性  
  
     `.Block() {`  
  
     `.Goto #Label1 { };`  
  
     `.Label`  
  
     `.LabelTarget #Label1:`  
  
     `}`  
  
## <a name="checked-operators"></a>Checked 的运算符  
 Checked 的运算符将显示为"#"符号前面运算符。 例如，检查的加法运算符显示为`#+`。  
  
### <a name="examples"></a>示例  
  
-   `Expression`  
  
    ```vb  
    Dim expr As Expression = Expression.AddChecked(  
    Expression.Constant(1), Expression.Constant(2))  
    ```  
  
     `DebugView` 属性  
  
     `1 #+ 2`  
  
-   `Expression`  
  
    ```vb  
    Dim expr As Expression = Expression.ConvertChecked(  
    Expression.Constant(10.0), GetType(Integer))  
    ```  
  
     `DebugView` 属性  
  
     `#(System.Int32)10D`  
  
## <a name="see-also"></a>另请参阅  
 [表达式树 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/expression-trees/index.md)   
 [在 Visual Studio 中进行调试](https://docs.microsoft.com/visualstudio/debugger/debugging-in-visual-studio)   
 [创建自定义可视化工具](https://docs.microsoft.com/visualstudio/debugger/create-custom-visualizers-of-data)
