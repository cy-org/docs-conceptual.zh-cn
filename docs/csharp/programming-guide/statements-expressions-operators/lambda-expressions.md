---
title: "Lambda 表达式（C# 编程指南）"
ms.date: 2017-03-03
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- lambda expressions [C#]
- outer variables [C#]
- statement lambda [C#]
- expression lambda [C#]
- expressions [C#], lambda
ms.assetid: 57e3ba27-9a82-4067-aca7-5ca446b7bf93
caps.latest.revision: 64
author: BillWagner
ms.author: wiwagn
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
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: c952c72d9108775fbd0f824f82cacdab5ba91d09
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="lambda-expressions-c-programming-guide"></a>Lambda 表达式（C# 编程指南）
Lambda 表达式是一种可用于创建 [委托](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md) 或 [表达式目录树](../../../csharp/programming-guide/delegates/using-delegates.md) 类型的 [匿名函数](http://msdn.microsoft.com/library/fb1d3ed8-d5b0-4211-a71f-dd271529294b) 。 通过使用 lambda 表达式，可以写入可作为参数传递或作为函数调用值返回的本地函数。 Lambda 表达式对于编写 LINQ 查询表达式特别有用。  
  
 若要创建 Lambda 表达式，需要在 Lambda 运算符 [=>](../../../csharp/language-reference/operators/lambda-operator.md)左侧指定输入参数（如果有），然后在另一侧输入表达式或语句块。 例如，lambda 表达式 `x => x * x` 指定名为 `x` 的参数并返回 `x` 的平方值。 如下面的示例所示，你可以将此表达式分配给委托类型：  
  
```csharp  
delegate int del(int i);  
static void Main(string[] args)  
{  
    del myDelegate = x => x * x;  
    int j = myDelegate(5); //j = 25  
}  
```  
  
 若要创建表达式目录树类型：  
  
```csharp  
using System.Linq.Expressions;  
  
namespace ConsoleApplication1  
{  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            Expression<del> myET = x => x * x;  
        }  
    }  
}  
```  
  
 `=>` 运算符具有与赋值运算符 (`=`) 相同的优先级并且是[右结合运算](../../../csharp/programming-guide/statements-expressions-operators/operators.md)（参见“运算符”文章的“结合性”部分）。  
  
 Lambda 在基于方法的 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 查询中用作标准查询运算符方法（如 <xref:System.Linq.Enumerable.Where%2A>）的参数。  
  
 使用基于方法的语法在 <xref:System.Linq.Enumerable.Where%2A> 类中调用 <xref:System.Linq.Enumerable> 方法时（如在 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] to Objects 和 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]中一样），参数是委托类型 <xref:System.Func%602?displayProperty=fullName>。 使用 Lambda 表达式创建该委托最为方便。 例如，在 <xref:System.Linq.Queryable?displayProperty=fullName> 类中调用相同的方法时（如在 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] 中一样），参数类型为 <xref:System.Linq.Expressions.Expression?displayProperty=fullName><Func\>，其中 Func 是最多具有十六个输入参数的任何一个 Func 委托。 同样，Lambda 表达式只是一种非常简洁的构造该表达式目录树的方式。 尽管事实上通过 Lambda 创建的对象具有不同的类型，但 Lambda 使得 `Where` 调用看起来类似。  
  
 在上一个示例中，请注意委托签名具有一个 `int`类型的隐式类型输入参数，并返回 `int`。 可以将 Lambda 表达式转换为该类型的委托，因为该表达式也具有一个输入参数 (`x`)，以及一个编译器可隐式转换为 `int` 类型的返回值。 （以下几节中将对类型推理进行详细讨论。）使用输入参数 5 调用委托时，它将返回结果 25。  
  
 在 [is](../../../csharp/language-reference/keywords/is.md) 或 [as](../../../csharp/language-reference/keywords/as.md) 运算符的左侧不允许使用 Lambda。  
  
 适用于匿名方法的所有限制也适用于 Lambda 表达式。 有关详细信息，请参阅[匿名方法](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)。  
  
## <a name="expression-lambdas"></a>表达式 lambda  
 表达式位于 => 运算符右侧的 Lambda 表达式称为“表达式 lambda”。 表达式 lambda 广泛用于[表达式树](http://msdn.microsoft.com/library/fb1d3ed8-d5b0-4211-a71f-dd271529294b)的构造。 表达式 lambda 会返回表达式的结果，并采用以下基本形式：  
  
```csharp
(input-parameters) => expression
```

 仅当 lambda 只有一个输入参数时，括号才是可选的；否则括号是必需的。 括号内的两个或更多输入参数使用逗号加以分隔：  
  
```csharp
(x, y) => x == y
```

 有时，编译器难以或无法推断输入类型。 如果出现这种情况，你可以按以下示例中所示方式显式指定类型：  
  
```csharp
(int x, string s) => s.Length > x
```

 使用空括号指定零个输入参数：  
  
```csharp
() => SomeMethod()
```

 在上一个示例中，请注意表达式 Lambda 的主体可以包含一个方法调用。 但是，如果要创建在 .NET Framework 之外计算的表达式目录树（例如，在 SQL Server 中），则不应在 lambda 表达式中使用方法调用。 在 .NET 公共语言运行时上下文之外，方法将没有任何意义。  
  
## <a name="statement-lambdas"></a>语句 lambda  
 语句 lambda 与表达式 lambda 表达式类似，只是语句括在大括号中：  
  
(input-parameters) => { statement; }

 语句 lambda 的主体可以包含任意数量的语句；但是，实际上通常不会多于两个或三个。  
  
[!code-csharp[StatementLamba#1](../../../../samples\snippets\csharp\programming-guide\lambda-expressions/statements.cs#1)]

[!code-csharp[StatementLamba#2](../../../../samples\snippets\csharp\programming-guide\lambda-expressions/statements.cs#2)]

 像匿名方法一样，语句 lambda 也不能用于创建表达式目录树。  
  
## <a name="async-lambdas"></a>异步 lambda  
 通过使用 [async](../../../csharp/language-reference/keywords/async.md) 和 [await](../../../csharp/language-reference/keywords/await.md) 关键字，你可以轻松创建包含异步处理的 lambda 表达式和语句。 例如，下面的 Windows 窗体示例包含一个调用和等待异步方法 `ExampleMethodAsync`的事件处理程序。  
  
```csharp
public partial class Form1 : Form  
{  
    public Form1()  
    {  
        InitializeComponent();  
    }  
  
    private async void button1_Click(object sender, EventArgs e)  
    {  
        // ExampleMethodAsync returns a Task.  
        await ExampleMethodAsync();  
        textBox1.Text += "\r\nControl returned to Click event handler.\n";  
    }  
  
    async Task ExampleMethodAsync()  
    {  
        // The following line simulates a task-returning asynchronous process.  
        await Task.Delay(1000);  
    }  
}  
```

 你可以使用异步 lambda 添加同一事件处理程序。 若要添加此处理程序，请在 lambda 参数列表前添加一个 `async` 修饰符，如下例所示。  
  
```csharp  
public partial class Form1 : Form  
{  
    public Form1()  
    {  
        InitializeComponent();  
        button1.Click += async (sender, e) =>  
        {  
            // ExampleMethodAsync returns a Task.  
            await ExampleMethodAsync();  
            textBox1.Text += "\nControl returned to Click event handler.\n";  
        };  
    }  
  
    async Task ExampleMethodAsync()  
    {  
        // The following line simulates a task-returning asynchronous process.  
        await Task.Delay(1000);  
    }  
}  
```  

 有关如何创建和使用异步方法的详细信息，请参阅[使用 Async 和 Await 的异步编程](../../../csharp/programming-guide/concepts/async/index.md)。  
  
## <a name="lambdas-with-the-standard-query-operators"></a>带有标准查询运算符的 lambda  
 许多标准查询运算符都具有输入参数，其类型是泛型委托系列 <xref:System.Func%602> 中的一种。 这些委托使用类型参数来定义输入参数的数量和类型，以及委托的返回类型。 `Func` 委托对于封装用户定义的表达式非常有用，这些表达式将应用于一组源数据中的每个元素。 例如，请考虑以下委托类型：  
  
```csharp  
public delegate TResult Func<TArg0, TResult>(TArg0 arg0)  
```  
  
 可以将委托实例化为 `Func<int,bool> myFunc` ，其中 `int` 是输入参数， `bool` 是返回值。 返回值始终在最后一个类型参数中指定。 `Func<int, string, bool>` 定义包含两个输入参数（ `int` 和 `string`）且返回类型为 `bool`的委托。 当调用下面的 `Func` 委托时，该委托将返回 true 或 false 以指示输入参数是否等于 5：  
  
```csharp  
Func<int, bool> myFunc = x => x == 5;  
bool result = myFunc(4); // returns false of course  
```  
  
 当参数类型为 `Expression<Func>`时，你也可以提供 Lambda 表达式，例如在 System.Linq.Queryable 内定义的标准查询运算符中。 如果指定 `Expression<Func>` 参数，lambda 将编译为表达式目录树。  
  
 此处显示了一个标准查询运算符， <xref:System.Linq.Enumerable.Count%2A> 方法：  
  
```csharp  
int[] numbers = { 5, 4, 1, 3, 9, 8, 6, 7, 2, 0 };  
int oddNumbers = numbers.Count(n => n % 2 == 1);  
```  
  
 编译器可以推断输入参数的类型，或者你也可以显式指定该类型。 这个特殊 lambda 表达式将计算那些除以 2 时余数为 1 的整数的数量 (`n`)。  
  
 下面一行代码将生成一个序列，其中包含 `numbers` 数组中在 9 左侧的所有元素，因为它是序列中第一个不满足条件的数字：  
  
```csharp  
var firstNumbersLessThan6 = numbers.TakeWhile(n => n < 6);  
```  
  
 此示例展示了如何通过将输入参数括在括号中来指定多个输入参数。 该方法将返回数字数组中的所有元素，直至遇到一个值小于其位置的数字为止。 不要将 lambda 运算符 (`=>`) 与大于等于运算符 (`>=`) 混淆。  
  
```csharp  
var firstSmallNumbers = numbers.TakeWhile((n, index) => n >= index);  
```  
  
## <a name="type-inference-in-lambdas"></a>Lambda 中的类型推理  
 在编写 lambda 时，通常不必为输入参数指定类型，因为编译器可以根据 lambda 主体、参数的委托类型以及 C# 语言规范中描述的其他因素来推断类型。 对于大多数标准查询运算符，第一个输入是源序列中的元素类型。 因此，如果要查询 `IEnumerable<Customer>`，则输入变量将被推断为 `Customer` 对象，这意味着你可以访问其方法和属性：  
  
```csharp  
customers.Where(c => c.City == "London");  
```  
  
 Lambda 的一般规则如下：  
  
-   Lambda 包含的参数数量必须与委托类型包含的参数数量相同。  
  
-   Lambda 中的每个输入参数必须都能够隐式转换为其对应的委托参数。  
  
-   Lambda 的返回值（如果有）必须能够隐式转换为委托的返回类型。  
  
 请注意，lambda 表达式本身没有类型，因为常规类型系统没有“Lambda 表达式”这一内部概念。 但是，有时以一种非正式的方式谈论 lambda 表达式的“类型”会很方便。 在这些情况下，类型是指委托类型或 lambda 表达式所转换到的 <xref:System.Linq.Expressions.Expression> 类型。  
  
## <a name="variable-scope-in-lambda-expressions"></a>Lambda 表达式中的变量范围  
 在定义 lambda 函数的方法内或包含 Lambda 表达式的类型内，Lambda 可以引用范围内的外部变量（请参阅[匿名方法](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)）。 以这种方式捕获的变量将进行存储以备在 lambda 表达式中使用，即使在其他情况下，这些变量将超出范围并进行垃圾回收。 必须明确地分配外部变量，然后才能在 lambda 表达式中使用该变量。 下面的示例演示这些规则：  
  
```csharp  
delegate bool D();  
delegate bool D2(int i);  
  
class Test  
{  
    D del;  
    D2 del2;  
    public void TestMethod(int input)  
    {  
        int j = 0;  
        // Initialize the delegates with lambda expressions.  
        // Note access to 2 outer variables.  
        // del will be invoked within this method.  
        del = () => { j = 10;  return j > input; };  
  
        // del2 will be invoked after TestMethod goes out of scope.  
        del2 = (x) => {return x == j; };  
  
        // Demonstrate value of j:  
        // Output: j = 0   
        // The delegate has not been invoked yet.  
        Console.WriteLine("j = {0}", j);        // Invoke the delegate.  
        bool boolResult = del();  
  
        // Output: j = 10 b = True  
        Console.WriteLine("j = {0}. b = {1}", j, boolResult);  
    }  
  
    static void Main()  
    {  
        Test test = new Test();  
        test.TestMethod(5);  
  
        // Prove that del2 still has a copy of  
        // local variable j from TestMethod.  
        bool result = test.del2(10);  
  
        // Output: True  
        Console.WriteLine(result);  
  
        Console.ReadKey();  
    }  
}  
```  
  
 下列规则适用于 lambda 表达式中的变量范围：  
  
-   捕获的变量将不会被作为垃圾回收，直至引用变量的委托符合垃圾回收的条件。  
  
-   在外部方法中看不到 lambda 表达式内引入的变量。  
  
-   Lambda 表达式无法从封闭方法中直接捕获 `ref` 或 `out` 参数。  
  
-   Lambda 表达式中的返回语句不会导致封闭方法返回。  
  
-   如果跳转语句的目标在块外部，则 lambda 表达式不能包含位于 lambda 函数内部的 `goto` 语句、 `break` 语句或 `continue` 语句。 同样，如果目标在块内部，则在 lambda 函数块外部使用跳转语句也是错误的。  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="featured-book-chapter"></a>重要章节  
 [C# 3.0 手册，第三版：为 C# 3.0 程序员提供的 250 多个解决方案](http://go.microsoft.com/fwlink/?LinkId=195395) 中的 [委托、事件和 Lambda 表达式](http://go.microsoft.com/fwlink/?LinkId=195369)  
  
## <a name="see-also"></a>请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [LINQ（语言集成查询）](http://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d)   
 [匿名方法](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)   
 [is](../../../csharp/language-reference/keywords/is.md)   
 [Expression Trees](http://msdn.microsoft.com/library/fb1d3ed8-d5b0-4211-a71f-dd271529294b)   
 [Visual Studio 2008 C# 示例（请参阅 LINQ 示例查询文件和 XQuery 程序）](http://code.msdn.microsoft.com/Visual-Studio-2008-C-d295cdba)   
 [递归 lambda 表达式](http://go.microsoft.com/fwlink/?LinkId=112395)

