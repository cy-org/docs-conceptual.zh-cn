---
title: "在 Visual Basic 中编写查询 |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: get-started-article
dev_langs:
- VB
helpviewer_keywords:
- queries [LINQ in Visual Basic], writing
- LINQ [Visual Basic], walkthroughs
- LINQ [Visual Basic], writing queries
- writing LINQ queries [Visual Basic]
ms.assetid: f0045808-b9fe-4d31-88d1-473d9957211e
caps.latest.revision: 70
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
ms.openlocfilehash: e870d5d0640c68fa57b07986f2bf8268fd5246c9
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-writing-queries-in-visual-basic"></a>演练：用 Visual Basic 编写查询
本演练演示如何使用 Visual Basic 语言功能来编写[!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext_md.md)]查询表达式。 本演练演示如何在列表中的学生对象创建查询、 如何运行查询，以及如何对其进行修改。 这些查询加入了多种功能，包括对象初始值设定项、 局部类型推理和匿名类型。  
  
 完成此演练后，您将准备好迎接的示例和文档的特定[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]您感兴趣的提供程序。 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]提供程序包括[!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq_md.md)]， [!INCLUDE[linq_dataset](../../../../csharp/programming-guide/concepts/linq/includes/linq_dataset_md.md)]，和[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]。  
  
## <a name="create-a-project"></a>创建项目  
  
#### <a name="to-create-a-console-application-project"></a>若要创建控制台应用程序项目  
  
1.  启动 Visual Studio。  
  
2.  在 **“文件”** 菜单上，指向 **“新建”**，然后单击 **“项目”**。  
  
3.  在**已安装的模板**列表中，单击**Visual Basic**。  
  
4.  在项目类型列表中，单击**控制台应用程序**。 在**名称**框中，为项目中，键入一个名称，然后单击**确定**。  
  
     创建一个项目。 默认情况下，它包含对 System.Core.dll 的引用。 此外，**导入的命名空间**列表[，项目设计器 (Visual Basic 中) 引用页](https://docs.microsoft.com/visualstudio/ide/reference/references-page-project-designer-visual-basic)包括<xref:System.Linq?displayProperty=fullName>命名空间。</xref:System.Linq?displayProperty=fullName>  
  
5.  在[编译页，项目设计器 (Visual Basic 中)](https://docs.microsoft.com/visualstudio/ide/reference/compile-page-project-designer-visual-basic)，确保**Option infer**设置为**上**。  
  
## <a name="add-an-in-memory-data-source"></a>添加一个内存中数据源  
 在本演练中的查询的数据源是一份`Student`对象。 每个`Student`对象包含名字、 姓氏、 一类和学术排名学生正文内的。  
  
#### <a name="to-add-the-data-source"></a>若要添加数据源  
  
-   定义`Student`类，并创建一个类的实例的列表。  
  
    > [!IMPORTANT]
    >  定义所需的代码`Student`类，并创建使用的列表在本演练中提供示例[如何︰ 创建列表项](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md)。 可以将其复制并将其粘贴到您的项目。 新的代码替换在创建项目时显示的代码。  
  
#### <a name="to-add-a-new-student-to-the-students-list"></a>若要向学生列表中添加新的学生  
  
-   请按照中的模式`getStudents`方法添加的另一个实例`Student`到列表的类。 添加学生将向您介绍对象初始值设定项。 有关详细信息，请参阅[对象初始值设定项︰ 命名类型和匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)。  
  
## <a name="create-a-query"></a>创建查询  
 在执行时，此部分中添加此查询将生成其学术排名将其放入前&10; 个学生列表。 因为该查询用于选择完整`Student`对象在每次，查询结果的类型是`IEnumerable(Of Student)`。 但是，查询的类型通常是未指定在查询定义中。 相反，编译器使用局部类型推理来确定的类型。 有关详细信息，请参阅[本地类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)。 查询的范围变量`currentStudent`，用作一个对所有引用`Student`源中的实例`students`，提供对中的每个对象的属性访问`students`。  
  
#### <a name="to-create-a-simple-query"></a>创建简单查询  
  
1.  查找中的位置`Main`标记，如下所示的项目的方法︰  
  
     [!code-vb[VbLINQWalkthrough #&1;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_1.vb)]  
  
     将以下代码复制并粘贴到此位置。  
  
     [!code-vb[VbLINQWalkthrough #&2;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_2.vb)]  
  
2.  将鼠标指针停留在`studentQuery`代码来验证编译器指定类型是否为`IEnumerable(Of Student)`。  
  
## <a name="run-the-query"></a>运行查询  
 该变量`studentQuery`包含定义的查询，而不是运行查询的结果。 运行查询的典型机制是`For Each`循环。 返回序列中的每个元素的访问的循环迭代变量。 查询执行有关的详细信息，请参阅[编写您的第一个 LINQ 查询](../../../../visual-basic/programming-guide/concepts/linq/writing-your-first-linq-query.md)。  
  
#### <a name="to-run-the-query"></a>若要运行查询  
  
1.  将以下代码添加`For Each`循环在项目中查询的下面。  
  
     [!code-vb[VbLINQWalkthrough #&3;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_3.vb)]  
  
2.  将鼠标指针停留在循环控制变量`studentRecord`以查看其数据类型。 一种`studentRecord`被推断为`Student`，这是因为`studentQuery`返回的集合`Student`实例。  
  
3.  生成并按 CTRL + F5 运行该应用程序。 请注意控制台窗口中的结果。  
  
## <a name="modify-the-query"></a>修改查询  
 很方便地扫描查询结果，它们是否按指定顺序。 可以对基于任何可用字段返回的序列进行排序。  
  
#### <a name="to-order-the-results"></a>对结果进行排序  
  
1.  将以下代码添加`Order By`之间子句`Where`语句和`Select`查询语句。 `Order By`子句将字母顺序对结果从 A 到 Z，到最后一个根据每个学生的名字。  
  
    ```  
    Order By currentStudent.Last Ascending   
    ```  
  
2.  若要按姓氏，然后按名字排序，请向查询添加这两个字段︰  
  
    ```  
    Order By currentStudent.Last Ascending, currentStudent.First Ascending   
    ```  
  
     您还可以指定`Descending`到订单从 Z 到 a。  
  
3.  生成并按 CTRL + F5 运行该应用程序。 请注意控制台窗口中的结果。  
  
#### <a name="to-introduce-a-local-identifier"></a>若要将本地标识符引入  
  
1.  在查询表达式将本地标识符引入此部分中添加代码。 本地标识符将用于保存中间结果。 在下面的示例中，`name`是保留的学生串联的标识符的姓和名。 可以为方便起见，使用的本地标识符，或者也可以通过将存储结果的表达式，否则将计算多次用于提高性能。  
  
     [!code-vb[VbLINQWalkthrough #&4;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_4.vb)]  
  
2.  生成并按 CTRL + F5 运行该应用程序。 请注意控制台窗口中的结果。  
  
#### <a name="to-project-one-field-in-the-select-clause"></a>投影在 Select 子句中的一个字段  
  
1.  将查询添加和`For Each`从该部分以创建一个查询，生成一个序列，其元素与不同的源中元素的循环。 在以下示例中，源是一套`Student`返回对象，但每个对象只有一个成员︰ 其姓氏为 Garcia 的学生的名字。 因为`currentStudent.First`是一个字符串，返回的序列的数据类型`studentQuery3`是`IEnumerable(Of String)`，一个字符串序列。 如前面的示例中所示分配数据类型为`studentQuery3`保留以供编译器使用局部类型推理来确定的。  
  
     [!code-vb[VbLINQWalkthrough #&5;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_5.vb)]  
  
2.  将鼠标指针停留在`studentQuery3`在您的代码以验证分配的类型是否为`IEnumerable(Of String)`。  
  
3.  生成并按 CTRL + F5 运行该应用程序。 请注意控制台窗口中的结果。  
  
#### <a name="to-create-an-anonymous-type-in-the-select-clause"></a>若要在 Select 子句中创建一个匿名类型  
  
1.  添加查询中使用的该部分以查看如何匿名类型中的代码。 如果您使用它们在查询中你想要从数据源而不是完整的记录返回多个字段 (`currentStudent`前面的示例中的记录) 或单个字段 (`First`前一节中)。 而不是定义新的命名的类型，其中包含你想要在结果中包括的字段，指定在字段`Select`子句和编译器创建一个匿名类型与这些字段作为其属性。 有关详细信息，请参阅[匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)。  
  
     下面的示例创建一个查询，返回的名称和其学术排名是介于 1 和 10，学术并按排列的上级的秩。 在此示例中的一种`studentQuery4`必须推断，因为`Select`子句将返回一个匿名类型的实例和一个匿名类型已没有可用的名称。  
  
     [!code-vb[VbLINQWalkthrough #&6;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_6.vb)]  
  
2.  生成并按 CTRL + F5 运行该应用程序。 请注意控制台窗口中的结果。  
  
## <a name="additional-examples"></a>其他示例  
 现在，您已了解基础知识，下面是其他示例来说明灵活的列表以及利用[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]查询。 每个示例的前面有其用途的简短说明。 将鼠标指针停留在每个查询，以查看推断出的类型的查询结果变量。 使用`For Each`循环，以产生的结果。  
  
 [!code-vb[VbLINQWalkthrough #&7;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_7.vb)]  
  
## <a name="additional-information"></a>其他信息  
 您熟悉使用查询的基本概念后，你就可以读取的特定类型的文档和示例[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]您感兴趣的提供程序︰  
  
 [LINQ to Objects](http://msdn.microsoft.com/library/73cafe73-37cf-46e7-bfa7-97c7eea7ced9)  
  
 [LINQ to SQL](https://msdn.microsoft.com/library/bb386976)  
  
 [LINQ to XML](http://msdn.microsoft.com/library/f0fe21e9-ee43-4a55-b91a-0800e5782c13)  
  
 [LINQ to DataSet](http://msdn.microsoft.com/library/743e3755-3ecb-45a2-8d9b-9ed41f0dcf17)  
  
## <a name="see-also"></a>另请参阅  
 [语言集成查询 (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/index.md)   
 [在 Visual Basic 中的 LINQ 入门](../../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [局部类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [对象初始值设定项︰ 命名类型和匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)   
 [匿名类型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [在 Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [查询](../../../../visual-basic/language-reference/queries/queries.md)
