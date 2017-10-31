---
title: "字符串内插 - C#"
description: "了解 C# 6 中的字符串内插的工作方式"
keywords: ".NET, .NET Core, C#, 字符串"
author: mgroves
ms.author: wiwagn
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: f8806f6b-3ac7-4ee6-9b3e-c524d5301ae9
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: de8f77e44319731f87f00d227a5373a78bf40e32
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="string-interpolation-in-c"></a>C# 中的字符串内插 #

借助字符串内插，可以将字符串中的占位符替换成字符串变量的值。 在低于 C# 6 的版本中，使用 `System.String.Format` 实现字符串内插。 虽然这样做是可行的，但由于要用到编号占位符，因此加大了读取难度且过程更为冗长。

其他编程语言一直将字符串内插内置于语言之中。 例如：在 PHP 中：

```php
$name = "Jonas";
echo "My name is $name.";
// This will output "My name is Jonas."
```

在 C# 6 中，我们最终实现了这种样式的字符串内插。 可以在字符串前面使用 `$`，以指明应使用变量/表达式替换相应的值。

## <a name="prerequisites"></a>先决条件
必须将计算机设置为运行 .Net Core。 有关安装说明，请访问 [.NET Core](https://www.microsoft.com/net/core) 页。
可以在 Windows、Ubuntu Linux、macOS 或 Docker 容器中运行此应用程序。 必须安装常用的代码编辑器。 在以下说明中，我们使用的是开放源代码跨平台编辑器 [Visual Studio Code](https://code.visualstudio.com/)。 不过，你可以使用习惯使用的任意工具。

## <a name="create-the-application"></a>创建应用程序

至此，你已安装所有工具，是时候新建 .NET Core 应用程序了。 若要使用命令行生成器，请先创建项目目录（如 `interpolated`），然后在常用的命令行管理程序中执行以下命令：

```
dotnet new console
```

此命令将创建基本的 .NET Core 项目，其中包含项目文件 *interpolated.csproj* 和源代码文件 *Program.cs*。 需要执行 `dotnet restore` 来还原编译此项目所需的依赖项。

若要运行程序，请使用 `dotnet run`。 此时，应该可以在控制台中看到“Hello, World”输出。

## <a name="intro-to-string-interpolation"></a>字符串内插简介

使用 `System.String.Format` 在字符串中指定要被字符串后面的参数替换的“占位符”。 例如：

[!code-csharp[String.Format 示例](../../../samples/snippets/csharp/new-in-6/string-interpolation.cs#StringFormatExample)]  

上面的代码将输出“My name is Matt Groves”。

在 C# 6 中，定义内插字符串的方式为，在内插字符串前面添加 `$` 符号，然后直接在字符串中使用变量，而不使用 `String.Format`。 例如：

[!code-csharp[内插示例](../../../samples/snippets/csharp/new-in-6/string-interpolation.cs#InterpolationExample)]  

不必局限于变量。 可以在括号内使用任意表达式。 例如：

[!code-csharp[内插表达式示例](../../../samples/snippets/csharp/new-in-6/string-interpolation.cs#InterpolationExpressionExample)]  

上面的代码将输出：

```
This is line number 1
This is line number 2
This is line number 3
This is line number 4
This is line number 5
```

## <a name="how-string-interpolation-works"></a>字符串内插的工作方式

在后台，编译器将此类字符串内插语法转换成 String.Format。 因此，可以执行[之前使用 String.Format 执行的相同操作](https://msdn.microsoft.com/en-us/library/dwhawy9k(v=vs.110).aspx)。

例如，可以添加填充和数值格式：

[!code-csharp[内插格式设置示例](../../../samples/snippets/csharp/new-in-6/string-interpolation.cs#InterpolationFormattingExample)]  

上面的代码将输出如下内容：

```
998        5,177.67
999        6,719.30
1000       9,910.61
1001       529.34
1002       1,349.86
1003       2,660.82
1004       6,227.77
```

如果找不到变量名称，则会生成编译时错误。

例如：

```csharp
var animal = "fox";
var localizeMe = $"The {adj} brown {animal} jumped over the lazy {otheranimal}";
var adj = "quick";
Console.WriteLine(localizeMe);
```

如果这样编译，则会看到以下错误消息：
 
* `Cannot use local variable 'adj' before it is declared` - 直到内插字符串*之后*，`adj` 变量也未声明。
* `The name 'otheranimal' does not exist in the current context` - 从未声明名为“`otheranimal`”的变量

## <a name="localization-and-internationalization"></a>本地化和国际化

内插字符串支持 `IFormattable` 和 `FormattableString`，这对国际化非常有用。

默认情况下，内插字符串使用当前区域性。 若要使用其他区域性，可以将其显式转换成 `IFormattable`

例如：

[!code-csharp[内插国际化示例](../../../samples/snippets/csharp/new-in-6/string-interpolation.cs#InterpolationInternationalizationExample)]  

## <a name="conclusion"></a>结束语 

此教程介绍了如何使用 C# 6 的字符串内插功能。 它主要是简化了 `String.Format` 简单语句的编写，而它的高级用途则存在一些注意事项。

