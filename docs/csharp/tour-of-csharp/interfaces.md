---
title: "C# 接口 - C# 语言介绍"
description: "接口定义 C# 类型实现的协定"
keywords: ".NET, C#, 接口, 多重继承, 多形性"
author: BillWagner
ms.author: wiwagn
ms.date: 08/10/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: a9bf82f4-efd1-4216-bd34-4ef0fa48c968
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 673ac56f3f5732fcda02d313b6f4273708ae365f
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="interfaces"></a>接口

***接口***定义了可由类和结构实现的协定。 接口可以包含方法、属性、事件和索引器。 接口不提供所定义的成员的实现代码，仅指定必须由实现接口的类或结构提供的成员。

接口可以采用***多重继承***。 在以下示例中，接口 `IComboBox` 同时继承自 `ITextBox` 和 `IListBox`。

[!code-csharp[InterfacesOne](../../../samples/snippets/csharp/tour/interfaces/Program.cs#L5-L17)]

类和结构可以实现多个接口。 在以下示例中，类 `EditBox` 同时实现 `IControl` 和 `IDataBound`。

[!code-csharp[InterfacesTwo](../../../samples/snippets/csharp/tour/interfaces/Program.cs#L19-L27)]

当类或结构实现特定接口时，此类或结构的实例可以隐式转换成相应的接口类型。 例如

[!code-csharp[InterfacesThree](../../../samples/snippets/csharp/tour/interfaces/Program.cs#L33-L35)]

如果已知实例不是静态地实现特定接口，可以使用动态类型显式转换功能。 例如，以下语句使用动态类型显式转换功能来获取对象的 `IControl` 和 `IDataBound` 接口实现代码。 因为对象的运行时实际类型是 `EditBox`，所以显式转换会成功。

[!code-csharp[InterfacesFour](../../../samples/snippets/csharp/tour/interfaces/Program.cs#L40-L42)]

在前面的 `EditBox` 类中，`IControl` 接口中的 `Paint` 方法和 `IDataBound` 接口中的 `Bind` 方法均使用公共成员进行实现。 C# 还支持显式***接口成员实现代码***，这样类或结构就不会将成员设为公共成员。 显式接口成员实现代码是使用完全限定的接口成员名称进行编写。 例如，`EditBox` 类可以使用显式接口成员实现代码来实现 `IControl.Paint` 和 `IDataBound.Bind` 方法，如下所示。

[!code-csharp[InterfacesFive](../../../samples/snippets/csharp/tour/interfaces/Program.cs#L60-L64)]

显式接口成员只能通过接口类型进行访问。 例如，只有先将 `EditBox` 引用转换成 `IControl` 接口类型，才能调用上面 EditBox 类提供的 `IControl.Paint` 实现代码。

[!code-csharp[InterfacesFive](../../../samples/snippets/csharp/tour/interfaces/Program.cs#L71-L74)]

>[!div class="step-by-step"]
[上一页](arrays.md)
[下一页](enums.md)

