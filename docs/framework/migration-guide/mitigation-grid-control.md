---
title: "缓解：网格控件向 -列分配空间"
ms.custom: 
ms.date: 04/07/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- retargeting changes
- .NET Framework 4.7 retargeting changes
- WPF retargeting changes
- Grid control retargeting changes
ms.assetid: 707c064d-85e9-4ea1-aefb-e42b60b88679
caps.latest.revision: 4
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 54391538ac0b2daf307cba2f7ceff1984d26b0ce
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="mitigation-grid-control39s-space-allocation-to-star-columns"></a>缓解：网格控件向 -列分配空间

自定位 .NET Framework 4.7 的应用程序起，WPF 替换了 <xref:System.Windows.Controls.Grid> 控件用于向 \*-列分配空间的算法。 

## <a name="whats-changed"></a>具体更改

新算法修复了旧算法中的以下多处 bug：

1. 向列分配的总空间可能会超过网格宽度。 当向比例份额小于其大小下限的列分配空间时，可能会出现这种问题。 算法会分配大小下限对应的空间，这将减少其他列的可用空间。 如果没有可分配空间的 \*-列剩余，分配的总空间可能会过大。

1. 向列分配的总空间可能会占不满网格宽度。 这是第 1 个问题的对偶问题，当向比例份额大于其大小上限的列分配空间，没有剩余的 \*-列来收紧空间时，可能会出现这种问题。

1. 可能会向两个 \*-列分配与其 *-权重不成比例的空间。 这是第 1 个/第 2 个问题造成的较为温和的影响，当依序向 *-列 A、B 和 C 分配空间，但 B 列的比例份额与约束下限（或上限）冲突时，可能会出现这种问题。 同样，这会更改 C 列的可用空间，它将比 A 列获得更少（或更多）的按比例分配空间。

1. 权重极大 (> 10^298) 的列全都被视为具有权重 10^298。 这些列（以及权重略小的列）之间的比例差异将不会生效。

1. 无法正确处理权重无穷大的列。 [实际上，不能设置无穷大的权重，但这是一项人为限制。 空间分配代码是在努力处理这样的列，但处理得并不好。]

1. 在避免溢出、下溢、精度损失和类似浮点问题时，存在一些小问题。

1. 在 DPI 足够高的情况下，无法正确调整布局的圆化处理。

新算法生成符合以下条件的结果：

答： 分配给 *-列的实际宽度永远不会小于其最小宽度，也不会大于其最大宽度。

B. 对于没有分配最小或最大宽度的每个 *-列，向其分配与其 *-权重成比例的宽度。 确切地讲，如果分别使用宽度 x 和 y 声明两个列，且没有向这两个列分配最小或最大宽度，那么将按同一比例向这两个列分配实际宽度 v 和 w：v / w == x / y。

C. 分配给“成比例的”\*-列的总宽度等于分配给受约束列（向其分配了最小或最大宽度的固定、自动和 \*-列）后剩余的可用空间。 此空间可能为零（例如，当最小宽度的总和超过了网格的可用宽度时）。

D. 所有这些语句都是针对“理想”布局进行解释的。 当布局圆化处理有效时，实际宽度与理想宽度可能会相差一个像素。

旧算法只遵循了 (A)，并未遵循上面所述情况中的其他条件。

本主题中有关列和宽度的一切介绍同样也适用于行和高度。

## <a name="impact"></a>影响

新算法在以下许多情况下会更改分配给 \*-列的实际宽度：

- 当一个或多个 \*-列的最小或最大宽度替代相应列的按比例分配空间时。 （最小宽度可以派生自显式声明 <xref:System.Windows.FrameworkElement.MinWidth%2A>，也可以派生自从列内容中获取的隐式最小值。 只能通过 <xref:System.Windows.FrameworkElement.MaxWidth%2A> 声明显式定义最大宽度。）

- 当一个或多个 \*-列声明极大 \*-权重时（即大于 10^298）。

- 当 \*-权重明显不同，遇到了浮点不稳定问题（溢出、下溢、精度损失）时。

- 当布局圆化处理已启用且有效显示 DPI 足够高时。

在前两种情况下，新旧算法生成的宽度明显不同；在最后一种情况下，新旧算法生成的宽度最多相差一或两个像素。

## <a name="mitigation"></a>缓解操作

默认情况下，定位 .NET framework 4.7 及更高版本的应用程序将使用新算法，而定位 .NET Framework 4.6.2 或更低版本的应用程序将使用旧算法。

若要替代默认设置，请使用以下配置设置：

```xml
<runtime>
    <AppContextSwitchOverrides value="Switch.System.Windows.Controls.Grid.StarDefinitionsCanExceedAvailableSpace=true" /> 
</runtime>
```

值为“true”表示选择旧算法，值为“false”表示选择新算法。

## <a name="see-also"></a>请参阅
[.NET Framework 4.7 中的重定目标更改](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-7.md)

