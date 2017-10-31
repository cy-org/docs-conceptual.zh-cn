---
title: "使用 LINQ"
description: "此教程将介绍如何使用 LINQ 生成序列、编写用于 LINQ 查询的方法，以及如何区分及早计算和惰性计算。"
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 03/28/2017
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 0db12548-82cb-4903-ac88-13103d70aa77
ms.translationtype: Human Translation
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: ec86c558b9aa9c6269fcf9890978f61a934c081f
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="working-with-linq"></a>使用 LINQ

## <a name="introduction"></a>介绍

此教程将介绍 .NET Core 和 C# 语言的许多功能。 你将了解：

*   如何使用 LINQ 生成序列
*   如何编写可轻松用于 LINQ 查询的方法。
*   如何区分及早计算和惰性计算。

你将通过生成应用程序来了解如何执行这些操作，应用程序体现了所有魔术师都具备的一项基本技能，即[完美洗牌](https://en.wikipedia.org/wiki/Faro_shuffle)。 简而言之，完美洗牌这项技能是指，将一副纸牌分成两半，然后两手各拿一半交错洗牌（一张隔一张），以便重新生成原来的一副纸牌。

魔术师之所以要掌握这项技能是因为，每次洗牌后每张纸牌的位置已知，且顺序为重复模式。 

考虑到我们的目的，数据序列控制起来就会非常轻松。 生成的应用程序会构造一副纸牌，然后执行一系列洗牌操作，每次都会输出序列。 还可以将更新后的顺序与原始顺序进行比较。

在此教程中，将执行多步操作。 执行每步操作后，都可以运行应用程序，并查看进度。 还可参阅 dotnet/docs GitHub 库中的[完整示例](https://github.com/dotnet/docs/blob/master/samples/csharp/getting-started/console-linq)。 有关下载说明，请参阅[示例和教程](../../samples-and-tutorials/index.md#viewing-and-downloading-samples)。

## <a name="prerequisites"></a>先决条件

必须将计算机设置为运行 .Net Core。 有关安装说明，请访问 [.NET Core](https://www.microsoft.com/net/core) 页。 可以在 Windows、Ubuntu Linux、OS X 或 Docker 容器中运行此应用程序。 必须安装常用的代码编辑器。 在以下说明中，我们使用的是开放源代码跨平台编辑器 [Visual Studio Code](https://code.visualstudio.com/)。 不过，你可以使用习惯使用的任意工具。

## <a name="create-the-application"></a>创建应用程序

第一步是新建应用程序。 打开命令提示符，然后新建应用程序的目录。 将新建的目录设为当前目录。 在命令提示符处，键入命令 `dotnet new console`。 这将为基本的“Hello World”应用程序创建起始文件。

如果之前从未用过 C#，请参阅[这篇教程](console-teleprompter.md)，其中介绍了 C# 程序的结构。 可以阅读相应的内容，然后回到此教程详细了解 LINQ。 

## <a name="creating-the-data-set"></a>创建数据集

首先，我们要创建一副纸牌。 为此，请使用包含两个源（一个用于四套花色，另一个用于十三个值）的 LINQ 查询。 将这些源合并成一副纸牌（52 张）。 `foreach` 循环内的 `Console.WriteLine` 语句会显示纸牌。

查询如下：

```csharp
var startingDeck = from s in Suits()
                   from r in Ranks()
                   select new { Suit = s, Rank = r };

foreach (var c in startingDeck)
{
    Console.WriteLine(c);
}
```

多个 `from` 子句生成 `SelectMany`，用于将第一个和第二个序列中的所有元素合并成一个序列。 考虑到我们的目的，顺序非常重要。 第一个源序列（花色）中的首个元素与第二个序列（值）中的每个元素合并。 这就生成了第一个花色的所有十三张纸牌。 对第一个序列（花色）中的每个元素重复此过程。 最后生成按花色排序（后跟值）的一副纸牌。

接下来，需要生成 Suits() 和 Ranks() 方法。 让我们从一组非常简单的*迭代器方法*入手，这些方法将一个序列生成为可枚举的各个字符串：

```csharp
static IEnumerable<string> Suits()
{
    yield return "clubs";
    yield return "diamonds";
    yield return "hearts";
    yield return "spades";
}

static IEnumerable<string> Ranks()
{
    yield return "two";
    yield return "three";
    yield return "four";
    yield return "five";
    yield return "six";
    yield return "seven";
    yield return "eight";
    yield return "nine";
    yield return "ten";
    yield return "jack";
    yield return "queen";
    yield return "king";
    yield return "ace";
}
```

这两种方法都利用 `yield return` 语法在运行时生成序列。 编译器会生成对象来实现 `IEnumerable<T>`，并在有请求时生成字符串序列。

此时，运行已生成的示例。 将显示一副纸牌中的所有 52 张纸牌。 在调试器模式下运行此示例来观察 `Suits()` 和 `Values()` 方法的执行情况，你可能会觉得非常有用。 可以清楚地看到，每个序列中的所有字符串仅在需要时生成。

![显示应用输出 52 张纸牌的控制台窗口](./media/working-with-linq/console.png)

## <a name="manipulating-the-order"></a>控制顺序

接下来，让我们来生成一个可执行洗牌操作的实用工具方法。 第一步是将一副纸牌分成两半。 LINQ API 包含的 `Take()` 和 `Skip()` 方法提供了这种功能：

```csharp
var top = startingDeck.Take(26);
var bottom = startingDeck.Skip(26);
```

由于标准库中没有洗牌方法，因此必须自行编写。 这个新方法体现了要对基于 LINQ 的程序执行的几种操作，我们将逐步介绍此方法的每个部分。

此方法的签名可创建*扩展方法*：

```csharp
public static IEnumerable<T> InterleaveSequenceWith<T>
    (this IEnumerable<T> first, IEnumerable<T> second)
```

扩展方法是一种具有特殊用途的*静态方法*。 可以发现，在扩展方法的第一个自变量中添加了 `this` 修饰符。 也就是说，调用扩展方法，就像是第一个自变量类型的成员方法一样。

扩展方法只能在 `static` 类中声明，那么让我们新建一个 `extensions` 静态类来实现此功能。 在此教程接下来的部分中，你将会添加更多扩展方法，这些方法都位于同一类中。

此方法声明还遵循标准惯用做法，其中输入和输出类型为 `IEnumerable<T>`。 遵循这种做法，可以将 LINQ 方法链在一起，从而执行更复杂的查询。

```csharp
using System.Collections.Generic;

namespace LinqFaroShuffle
{
    public static class Extensions
    {
        public static IEnumerable<T> InterleaveSequenceWith<T>
            (this IEnumerable<T> first, IEnumerable<T> second)
        {
            // implementation coming.
        }
    }
}
```

将同时枚举两个序列，交错各个元素，然后创建一个对象。  必须了解 `IEnumerable` 的工作原理，才能编写处理两个序列的 LINQ 方法。

`IEnumerable` 接口有一个方法 (`GetEnumerator()`)。 `GetEnumerator()` 返回的对象包含用于移动到下一个元素的方法，以及用于检索序列中当前元素的属性。 将使用这两个成员来枚举集合并返回元素。 由于此交错方法是迭代器方法，因此将使用上面的 `yield return` 语法，而不用生成并返回集合。 

下面是此方法的实现代码：

[!CODE-csharp[InterleaveSequenceWith](../../../samples/csharp/getting-started/console-linq/extensions.cs?name=snippet1)]

至此，你已编写好这个方法，请回到 `Main` 方法，并进行一次洗牌：

```csharp
public static void Main(string[] args)
{
    var startingDeck = from s in Suits()
                       from r in Ranks()
                       select new { Suit = s, Rank = r };

    foreach (var c in startingDeck)
    {
        Console.WriteLine(c);
    }
        
    var top = startingDeck.Take(26);
    var bottom = startingDeck.Skip(26);
    var shuffle = top.InterleaveSequenceWith(bottom);

    foreach (var c in shuffle)
    {
        Console.WriteLine(c);
    }
}
```

## <a name="comparisons"></a>比较

让我们来看看进行多少次洗牌才能恢复一副纸牌的原始顺序。 需要编写用于确定两个序列是否相等的方法。 编写好此方法后，需要循环执行用于洗牌的代码，看看一副纸牌何时才能恢复原始顺序。

编写用于确定两个序列是否相等的方法应该很简单。 此方法的结构与你编写的洗牌方法类似。 不同之处在于，这一次将比较每个序列的匹配元素，而不是生成每个返回元素。 枚举整个序列后，如果每个元素都一致，那么序列就是相同的：

[!CODE-csharp[SequenceEquals](../../../samples/csharp/getting-started/console-linq/extensions.cs?name=snippet2)]

这反映了另一种 LINQ 惯用做法，即终端方法。 此类方法需要将序列（或在此示例中，为两个序列）用作输入，并返回一个标量值。 若使用，此类方法始终是查询的最终方法 （由此而得名）。 

使用此类方法来确定一副纸牌何时恢复原始顺序时，就可以了解实际效果。 循环执行洗牌代码，通过应用 `SequenceEquals()` 方法确定序列已恢复原始顺序时停止执行。 你会发现，此类方法始终是任何查询中的最后一个方法，因为返回的是一个值，而不是一个序列：

```csharp
var times = 0;
var shuffle = startingDeck;

do
{
    shuffle = shuffle.Take(26).InterleaveSequenceWith(shuffle.Skip(26));

    foreach (var c in shuffle)
    {
        Console.WriteLine(c);
    }

    Console.WriteLine();
    times++;
} while (!startingDeck.SequenceEquals(shuffle));

Console.WriteLine(times);
```

运行此示例，看看一副纸牌在每次洗牌时是如何重新排列的（纸牌在进行 8 次迭代后恢复原始配置）。

## <a name="optimizations"></a>优化

你已生成的示例执行的是*向内洗牌*，即每次洗牌时第一张和最后一张纸牌保持不变。 让我们来做出一处改变，执行*向外洗牌*，改变所有 52 张纸牌的位置。 向外洗牌是指，交错一副纸牌时，将后一半中的第一张纸牌变成一副纸牌中的第一张纸牌。 也就是说，上半部分中的最后一张纸牌变成一副纸牌中的最后一张纸牌。 只需更改一行代码即可。 将对 shuffle 的调用更新为，更改一副纸牌的上半部分和下半部分的顺序：

```csharp
shuffle = shuffle.Skip(26).InterleaveSequenceWith(shuffle.Take(26));
```

再次运行程序，你会发现需要进行 52 次迭代才能恢复一副纸牌的原始顺序。 随着程序的继续运行，你还会开始注意到一些非常严重的性能下降问题发生。

导致这种情况出现的原因有很多。 让我们来看看其中一个主要原因：*惰性计算*的使用效率低下。

LINQ 查询执行的是惰性计算。 仅当有元素请求时才生成序列。 通常情况下，这是 LINQ 的主要优势所在。 不过，在诸如此程序之类的用例中，这就会导致执行时间指数式增长。

原来的一副纸牌是使用 LINQ 查询生成。 每次洗牌操作是通过对上一副纸牌执行三次 LINQ 查询进行。 所有这些操作均采用惰性执行方式。 也就是说，每当有序列请求时，才会再次执行这些操作。 执行到第 52 次迭代时，就已经重新生成很多很多次原来的一副纸牌。 让我们来编写一个日志方法来阐明此行为。 然后，你就可以解决此问题。

下面展示了日志方法，可以将其追加到任何查询中，以标记查询已执行。

[!CODE-csharp[LogQuery](../../../samples/csharp/getting-started/console-linq/extensions.cs?name=snippet3)]

接下来，使用日志消息来检测每个查询的定义：

```csharp
public static void Main(string[] args)
{
    var startingDeck = (from s in Suits().LogQuery("Suit Generation")
                        from r in Ranks().LogQuery("Rank Generation")
                        select new { Suit = s, Rank = r }).LogQuery("Starting Deck");

    foreach (var c in startingDeck)
    {
        Console.WriteLine(c);
    }
        
    Console.WriteLine();
    var times = 0;
    var shuffle = startingDeck;

    do
    {
        /*
        shuffle = shuffle.Take(26)
            .LogQuery("Top Half")
            .InterleaveSequenceWith(shuffle.Skip(26)
            .LogQuery("Bottom Half"))
            .LogQuery("Shuffle");
        */

        shuffle = shuffle.Skip(26)
            .LogQuery("Bottom Half")
            .InterleaveSequenceWith(shuffle.Take(26).LogQuery("Top Half"))
            .LogQuery("Shuffle");

        foreach (var c in shuffle)
        {
            Console.WriteLine(c);
        }

        times++;
        Console.WriteLine(times);
    } while (!startingDeck.SequenceEquals(shuffle));

    Console.WriteLine(times);
}
```

请注意，不是每次访问查询都会生成日志。 只有在创建原始查询时，才会生成日志。 程序的运行时间仍然很长，但现在知道原因了。 如果对在启用日志记录的情况下运行向外洗牌失去了耐心，请切换回向内洗牌。 但仍会看到惰性计算效果。 在一次运行中，共执行 2592 次查询，包括生成所有值和花色。

可使用一种简单的方法来更新此程序，以省去所有这些执行。 LINQ 方法 `ToArray()` 和 `ToList()` 用于运行查询，并将结果分别存储在数组或列表中。 可以使用这些方法来缓存查询的数据结果，而不用再次执行源查询。  追加查询以通过调用 `ToArray()` 生成一副纸牌，然后再次运行查询：

[!CODE-csharp[Main](../../../samples/csharp/getting-started/console-linq/Program.cs?name=snippet1)]

再次运行程序，向内洗牌下降到 30 次查询。 再次运行向外洗牌程序，改善情况类似。 （现在执行 162 次查询）。

不要将此示例误认为，所有查询都应及早运行。 此示例旨在突出显示惰性计算可能会导致性能下降的用例。 这是因为每次重新排列一副纸牌都要以先前的排列为依据。 使用惰性计算意味着一副纸牌的每个新配置都以原来的一副纸牌为依据，甚至在执行生成 `startingDeck` 的代码时，也不例外。 这会导致大量额外的工作。 

在实践中，一些算法的效果优于使用及早计算，另一些算法的效果优于使用惰性计算。 （通常情况下，如果数据源为单独进程（如数据库引擎），更好的选择是使用惰性计算。 在这种情况下，使用惰性计算，更复杂的查询可以只对数据库进程执行一次往返。）LINQ 支持同时使用惰性计算和及早计算。 请进行衡量，做出最佳选择。

## <a name="preparing-for-new-features"></a>为添加新功能做好准备

为此示例编写的代码展示了如何创建简单的有效原型。 这样可以很好地探索问题空间；对于许多功能来说，这可能是最佳永久性解决方案。 已将*匿名类型*用于纸牌，每张纸牌均由字符串表示。

*匿名类型*在高效工作方面具有许多优势。 无需自行定义表示存储的类。 编译器会为你生成类型。 编译器生成的类型遵循多种关于简单数据对象的最佳做法。 此类型*不可变*，也就是说，在构造之后所有属性都不能更改。 由于匿名类型位于程序集内部，因此不视为属于相应程序集的公共 API。 匿名类型还包含 `ToString()` 方法（用于随每个值一起返回格式化字符串）的重写方法。

匿名类型也有缺点。 由于没有可访问的名称，因此无法用作返回值或自变量。 你会注意到，使用这些匿名类型的上述所有方法都是泛型方法。 `ToString()` 的重写方法可能无法满足你的需求，因为应用程序的功能越来越多。 

此示例还将字符串用于每张纸牌的花色和级别。 这是相当开放的。 借助 C# 类型系统，我们可以将 `enum` 类型用于这些值，从而编写更优质的代码。

从花色开始。 这是使用 `enum` 的大好时机：

[!CODE-csharp[花色枚举](../../../samples/csharp/getting-started/console-linq/Program.cs?name=snippet2)]

`Suits()` 方法也更改了类型和实现代码：

[!CODE-csharp[花色 IEnumerable](../../../samples/csharp/getting-started/console-linq/Program.cs?name=snippet4)]

接下来，对纸牌的级别进行同样的更改：

[!CODE-csharp[级别枚举](../../../samples/csharp/getting-started/console-linq/Program.cs?name=snippet3)]

以及用于生成级别的方法：

[!CODE-csharp[级别 IEnumerable](../../../samples/csharp/getting-started/console-linq/Program.cs?name=snippet5)]

作为最后一项清理工作，让我们使用一个类型来表示纸牌，而不是依赖于匿名类型。 匿名类型非常适合轻量级的局部类型，但在此示例中，扑克牌是主要概念之一。 它应为具体类型。

[!CODE-csharp[PlayingCard](../../../samples/csharp/getting-started/console-linq/playingcard.cs?name=snippet1)]

此类型使用在构造函数中设置的*自动实现的只读属性*，而且无法修改。 它还使用新的*字符串内插*功能，简化了字符串输出格式设置。

将生成初始的一副纸牌的查询更新为使用新类型：

```csharp
var startingDeck = (from s in Suits().LogQuery("Suit Generation")
                    from r in Ranks().LogQuery("Value Generation")
                    select new PlayingCard(s, r))
                    .LogQuery("Starting Deck")
                    .ToArray();
```

编译并再次运行。 输出更加清晰，代码更加清楚，扩展起来也更加容易。

## <a name="conclusion"></a>结束语

此示例展示了在 LINQ 中使用的一些方法，以及如何创建你自己的方法与支持 LINQ 的代码轻松结合使用。 还展示了惰性计算和及早计算的区别，以及决定使用哪种计算对性能产生的影响。

而且，你也了解了一点魔术师掌握的一项技能。 魔术师之所以采用完美洗牌是因为，可以控制每张纸牌在一副纸牌中的移动。 在一些戏法中，魔术师会让一位观众将一张纸牌放在一副纸牌的最上面，然后进行几次洗牌，指出观众所放那张纸牌的具体位置。 在另一些戏法中，则需要按特定方式设置一副纸牌。 魔术师会在变戏法前设置一副纸牌。 然后，她会对一副纸牌进行 5 次向内洗牌。 在舞台上，她可以向观众展示看似杂乱无章的一副纸牌，然后再进行 3 次洗牌，这样刚好就可以得到她想要的一副纸牌了。

