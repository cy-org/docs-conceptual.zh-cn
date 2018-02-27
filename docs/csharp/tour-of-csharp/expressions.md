---
title: "C# 表达式 - C# 语言介绍"
description: "表达式、操作数和运算符是 C# 语言的构建基块"
keywords: ".NET, C#, 表达式, 运算符, 操作数"
author: BillWagner
ms.author: wiwagn
ms.date: 11/06/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 20d5eb10-7381-47b9-ad90-f1cc895aa27e
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 155804dd212d8eda8d81ce7e296a9fe308e9c69b
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="expressions"></a>表达式

*表达式*是在*操作数*和*运算符*的基础之上构造而成。 表达式的运算符指明了向操作数应用的运算。 运算符的示例包括 `+`、`-`、`*`、`/` 和 `new`。 操作数的示例包括文本、字段、局部变量和表达式。

如果表达式包含多个运算符，那么运算符的*优先级*决定了各个运算符的计算顺序。 例如，表达式 `x + y * z` 相当于计算 `x + (y * z)`，因为 `*` 运算符的优先级高于 `+` 运算符。

如果操作数两边的两个运算符的优先级相同，那么运算符的*结合性*决定了运算的执行顺序：

*   除了赋值运算符之外，所有二元运算符均为*左结合*运算符，即从左向右执行运算。 例如，`x + y + z` 将计算为 `(x + y) + z`。
*   赋值运算符和条件运算符 (`?:`) 为*右结合*运算符，即从右向左执行运算。 例如，`x = y = z` 将计算为 `x = (y = z)`。

可以使用括号控制优先级和结合性。 例如，`x + y * z` 先计算 `y` 乘 `z`，并将结果与 `x` 相加，而 `(x + y) * z` 则先计算 `x` 加 `y`，然后将结果与 `z` 相乘。

大多数运算符都可以*重载*。 借助运算符重载，可以为一个或两个操作数为用户定义类或结构类型的运算指定用户定义运算符实现代码。

下面总结了 C# 运算符，按优先级从高到低的顺序列出了各类运算符。 同一类别的运算符的优先级也相同。 每个类别下均列出了相应类别的表达式，以及对每种表达式类型的说明。

* 基本
    - `x.m`：成员访问
    - `x(...)`：方法和委托调用
    - `x[...]`：数组和索引器访问
    - `x++`：后置递增
    - `x--`：后置递减
    - `new T(...)`：创建对象和委托
    - `new T(...){...}`：使用初始值设定项的对象创建
    - `new {...}`：匿名对象初始值设定项
    - `new T[...]`：数组创建
    - `typeof(T)`：获取 `T` 的 @System.Type 对象
    - `checked(x)`：在已检查的上下文中计算表达式
    - `unchecked(x)`：在未检查的上下文中计算表达式
    - `default(T)`：获取类型为 `T` 的默认值
    - `delegate {...}`：匿名函数（匿名方法）
* 一元
    - `+x`：标识
    - `-x`：取反
    - `!x`：逻辑取反
    - `~x`：按位取反
    - `++x`：前置递增
    - `--x`：前置递减
    - `(T)x`：将 `x` 显式转换成类型 `T`
    - `await x`：异步等待 `x` 完成
* 乘法
    - `x * y`：乘法
    - `x / y`：除法
    - `x % y`：求余
* 加法
    - `x + y`：加法、字符串串联、委托组合
    - `x – y`：减法、委托删除
* Shift
    - `x << y`：左移位
    - `x >> y`：右移位
* 关系和类型测试
    - `x < y`：小于
    - `x > y`：大于
    - `x <= y`：小于或等于
    - `x >= y`：大于或等于
    - `x is T`：如果 `x` 是 `T`，返回 `true`；否则，返回 `false`
    - `x as T`：返回类型为 `T` 的 `x`；如果 `x` 的类型不是 `T`，返回 `null`
* 相等
    - `x == y`：等于
    - `x != y`：不等于
* 逻辑“与”
    - `x & y`：整数型位AND，布尔型逻辑 AND
* 逻辑 XOR
    - `x ^ y`：整数型位 XOR，布尔型逻辑 XOR
* 逻辑“或”
    - `x | y`：整数型位 OR，布尔型逻辑 OR
* 条件“与”
    - `x && y`：仅当 `x` 不是 `false` 时，才计算 `y`
* 条件“或”
    - `x || y`：仅当 `x` 不是 `true` 时，才计算 `y`
* null 合并
    - `x ?? y`：如果 `x` 为 null，计算结果为 `y`；否则，计算结果为 `x`
* 条件运算
    - `x ? y : z`：如果 `x` 为 `true`，计算 `y`；如果 `x` 为 `false`，计算 `z`
* 赋值或匿名函数
    - `x = y`：赋值
    - `x op= y`：复合赋值；支持以下运算符
        - `*=`   `/=`   `%=`   `+=`   `-=`   `<<=`   `>>=`   `&=`  `^=`  `|=`
    - `(T x) => y`：匿名函数（lambda 表达式）

>[!div class="step-by-step"]
[上一页](types-and-variables.md)
[下一页](statements.md)
