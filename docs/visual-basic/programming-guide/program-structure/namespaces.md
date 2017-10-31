---
title: "在 Visual Basic 中的命名空间 |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.global
dev_langs:
- VB
helpviewer_keywords:
- assemblies [Visual Basic], namespaces
- name collisions
- Global keyword [Visual Basic]
- namespace pollution
- names, avoiding conflicts
- naming conflicts, namespaces
- namespaces, assemblies
- Visual Basic code, namespaces
- fully qualified names
- naming conventions, naming conflicts
- namespaces
ms.assetid: cffac744-ab8c-4f1f-ba50-732c22ab4b88
caps.latest.revision: 27
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: fe94e65ddbb4ebd2f7d26e8750a0a7ef5d3153af
ms.lasthandoff: 03/13/2017

---
# <a name="namespaces-in-visual-basic"></a>Visual Basic 中的命名空间
命名空间组织程序集中定义的对象。 程序集可以包含多个命名空间，命名空间又可以包含其他命名空间。 使用大组对象（比如类库）时，命名空间可以避免多义性和简化引用。  
  
 例如，[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]定义<xref:System.Windows.Forms.ListBox>类<xref:System.Windows.Forms?displayProperty=fullName>命名空间。</xref:System.Windows.Forms?displayProperty=fullName> </xref:System.Windows.Forms.ListBox> 以下代码段演示如何使用此类的完全限定名称声明变量：  
  
 [!code-vb[VbVbalrApplication #&6;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_1.vb)]  
  
## <a name="avoiding-name-collisions"></a>避免名称冲突  
 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]命名空间解决问题有时称为*命名空间污染*，在其中一个类库，开发人员，会影响使用的另一个库中的类似名称。 这些冲突及其现有组件有时被称为 *名称冲突*。  
  
 例如，如果创建一个名为 `ListBox`的新类，你可以在项目中不加限定地使用它。 但是，如果您想要使用[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]<xref:System.Windows.Forms.ListBox>类在同一项目中，您必须使用完全限定的引用以使引用唯一。</xref:System.Windows.Forms.ListBox> 如果引用不唯一，[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 会产生一个错误，指出名称不明确。 下面的代码示例演示如何声明这些对象：  
  
 [!code-vb[VbVbalrApplication #&7;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_2.vb)]  
  
 下图显示两个命名空间层次结构，它们都包含一个名为 `ListBox`的对象。  
  
 ![Namespace 层次结构](../../../visual-basic/programming-guide/program-structure/media/vanamespacehierarchy.gif "vaNamespaceHierarchy")  
  
 默认情况下，使用 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 创建的所有可执行文件都包含与项目具有相同名称的命名空间。 例如，如果在一个名为 `ListBoxProject`的项目中定义对象，则可执行文件 ListBoxProject.exe 包含一个名为 `ListBoxProject`的命名空间。  
  
 多个程序集可以使用相同的命名空间。 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 会将它们视为多个名称的单个组。 例如，你可以为名为 `Assemb1` 的程序集中名为 `SomeNameSpace` 的命名空间定义多个类，并为名为 `Assemb2` 的程序集中相同的命名空间定义其他类。  
  
## <a name="fully-qualified-names"></a>完全限定名  
 完全限定名是以在其中定义对象的命名空间的名称为前缀的对象引用。 如果创建对类的引用（通过选择“项目” **** 菜单中的“添加引用” **** ），然后为代码中的对象使用完全限定名，则可以使用在其他项目中定义的对象。 以下代码段演示如何为来自另一个项目命名空间的对象使用完全限定名：  
  
 [!code-vb[VbVbalrApplication #&8;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_3.vb)]  
  
 完全限定名避免命名冲突，因为它们可以使编译器确定哪些对象正在被使用。 但是，名称本身可能会变得冗长繁杂。 为避免这一问题，可以使用 `Imports` 语句来定义 *别名*- 可用于代替完全限定名的缩略名。 例如，以下代码示例为两个完全限定名创建别名，并使用这些别名来定义两个对象。  
  
 [!code-vb[VbVbalrApplication #&9;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_4.vb)]  
  
 [!code-vb[VbVbalrApplication #&10;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_5.vb)]  
  
 如果不带别名使用 `Imports` 语句，可以使用命名空间中的所有名称而无需限定，只要这些名称唯一。 如果项目包含同名的项的命名空间使用的 `Imports` 语句，则使用时必须完全限定该名称。 例如，假设项目包含以下两个 `Imports` 语句：  
  
 [!code-vb[VbVbalrApplication #&11;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_6.vb)]  
  
 如果尝试使用 `Class1` 而不对其完全限定，则 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 会产生错误消息，指出名称 `Class1` 不明确。  
  
## <a name="namespace-level-statements"></a>命名空间级别语句  
 在命名空间中，可以定义项，如模块、接口、类、委托、枚举、结构和其他命名空间。 无法在命名空间级别定义属性、过程、变量和事件等项。 这些项必须在模块、结构或类等容器内部进行声明。  
  
## <a name="global-keyword-in-fully-qualified-names"></a>完全限定名中的全局关键字  
 如果已定义的命名空间的嵌套层次结构，该层次结构内的代码可能会被阻止访问<xref:System?displayProperty=fullName>.NET Framework 命名空间。</xref:System?displayProperty=fullName> 下面的示例阐释了在其中的层次结构`SpecialSpace.System`命名空间块访问到<xref:System?displayProperty=fullName>。</xref:System?displayProperty=fullName>  
  
```vb  
Namespace SpecialSpace  
    Namespace System  
        Class abc  
            Function getValue() As System.Int32  
                Dim n As System.Int32  
                Return n  
            End Function  
        End Class  
    End Namespace  
End Namespace  
```  
  
 结果是，Visual Basic 编译器不能成功地解析对引用<xref:System.Int32?displayProperty=fullName>，这是因为`SpecialSpace.System`未定义`Int32`。</xref:System.Int32?displayProperty=fullName> 可以使用 `Global` 关键字在.NET Framework 类库的最外层级别上启动限定链。 这允许您指定<xref:System?displayProperty=fullName>命名空间或类库中的任何其他命名空间。</xref:System?displayProperty=fullName> 下面的示例阐释了这一点。  
  
```vb  
Namespace SpecialSpace  
    Namespace System  
        Class abc  
            Function getValue() As Global.System.Int32  
                Dim n As Global.System.Int32  
                Return n  
            End Function  
        End Class  
    End Namespace  
End Namespace  
```  
  
 您可以使用`Global`访问其他根级别的命名空间，如<xref:Microsoft.VisualBasic?displayProperty=fullName>，并与您的项目相关联的任何命名空间。</xref:Microsoft.VisualBasic?displayProperty=fullName>  
  
## <a name="global-keyword-in-namespace-statements"></a>命名空间语句中的全局关键字  
 您还可以使用`Global`中的关键字[Namespace 语句](../../../visual-basic/language-reference/statements/namespace-statement.md)。 这将允许你定义项目根命名空间之外的命名空间。  
  
 项目中的所有命名空间均基于项目的根命名空间。  Visual Studio 针对项目中的所有代码，将项目名称指定为默认根命名空间。 例如，如果项目命名为 `ConsoleApplication1`，则其编程元素属于命名空间 `ConsoleApplication1`。 如果声明 `Namespace Magnetosphere`，项目中对 `Magnetosphere` 的引用将访问 `ConsoleApplication1.Magnetosphere`。  
  
 以下示例使用 `Global` 关键字来为项目声明根命名空间之外的命名空间。  
  
 [!code-vb[VbVbalrApplication #&22;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_7.vb)]  
  
 在命名空间声明中， `Global` 不能嵌套于另一个命名空间中。  
  
 您可以使用[应用程序页，项目设计器 (Visual Basic 中)](https://docs.microsoft.com/visualstudio/ide/reference/application-page-project-designer-visual-basic)查看和修改**根 Namespace**的项目。  对于新项目，“根命名空间” **** 默认为该项目的名称。 若要使 `Global` 成为顶级命名空间，可以清除“根命名空间” **** 条目，以便此框为空。 清除“根命名空间” **** 移除了命名空间声明中需要的 `Global` 关键字。  
  
 如果 `Namespace` 语句声明一个名称，而该名称也是.NET Framework 中的命名空间，则如果 `Global` 关键字未在完全限定名中使用，.NET Framework 命名空间会变得不可用。 在不使用 `Global` 关键字的情况下，若要启用对该 .NET Framework 命名空间的访问，可以将 `Global` 关键字包括到 `Namespace` 语句中。  
  
 以下示例在 `Global` 命名空间声明中具有 `System.Text` 关键字。  
  
 如果`Global`关键字时不存在，请在命名空间声明<xref:System.Text.StringBuilder>无法访问而无需指定`Global.System.Text.StringBuilder`。</xref:System.Text.StringBuilder> 对于名为 `ConsoleApplication1`的项目，如果未使用 `System.Text` 关键字，对 `ConsoleApplication1.System.Text` 的引用会访问 `Global` 。  
  
 [!code-vb[VbVbalrApplication #&21;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/namespaces_8.vb)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Windows.Forms.ListBox></xref:System.Windows.Forms.ListBox>   
 <xref:System.Windows.Forms?displayProperty=fullName></xref:System.Windows.Forms?displayProperty=fullName>   
 [程序集和全局程序集缓存](../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)   
 [如何︰ 创建和使用程序集使用命令行](http://msdn.microsoft.com/library/70f65026-3687-4e9c-ab79-c18b97dd8be4)   
 [引用和 Imports 语句](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)   
 [Imports 语句（.NET 命名空间和类型）](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)   
 [在 Office 解决方案中编写代码](https://msdn.microsoft.com/library/bb608596)
