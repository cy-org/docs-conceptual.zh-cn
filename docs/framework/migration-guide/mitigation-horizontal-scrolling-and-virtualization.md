---
title: "缓解：水平滚动和虚拟化"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d5bafd9b-a3b3-4f92-8241-2aad254fb1a9
caps.latest.revision: 6
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 40eaf185e9c0c60493e9a2e5428c58b7463789fe
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="mitigation-horizontal-scrolling-and-virtualization"></a>缓解：水平滚动和虚拟化
此更改适用于按与主滚动方向正交的方向自行执行虚拟化的 <xref:System.Windows.Controls.ItemsControl>。 （主要示例是 <xref:System.Windows.Controls.DataGrid> 控件，其 <xref:System.Windows.Controls.DataGrid.EnableColumnVirtualization%2A> 设置为 `true`。）已将特定水平滚动操作更改为生成更直观且更类似于可类比垂直滚动操作的结果。  具体操作包括“滚动到此处”和“滚动到右边缘”（使用右键单击水平滚动条所获得的菜单中的名称）。  这两种方法都能计算候选偏移和调用 <xref:System.Windows.Controls.Primitives.IScrollInfo.SetHorizontalOffset%2A?displayProperty=fullName>。  滚动到新偏移后，“滚动到此处”或“滚动到右边缘”的定义可能会发生变化，因为反虚拟化的新内容已更改 <xref:System.Windows.Controls.Primitives.IScrollInfo.ExtentWidth%2A?displayProperty=fullName> 的值。  
  
## <a name="description-of-the-change"></a>更改说明  
 在低于 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] 的版本中，滚动操作仅使用候选偏移，即使不再位于“此处”或“右边缘”，也不例外。  这会导致滚动翻阅出现“退回”等效果，最好是用举例来说明。  假设 <xref:System.Windows.Controls.DataGrid> 控件具有设置为 1000 的 <xref:System.Windows.Controls.Primitives.IScrollInfo.ExtentWidth%2A> 和设置为 200 的 <xref:System.Windows.FrameworkElement.Width%2A>。  “滚动到右边缘”使用候选偏移 1000 - 200 = 800。  在滚动到此偏移时，新列会进行反虚拟化；假设这些列都非常宽，这样就可以将 <xref:System.Windows.Controls.Primitives.IScrollInfo.ExtentWidth%2A> 更改为 2000。  滚动偏移最终为 <xref:System.Windows.Controls.Primitives.IScrollInfo.HorizontalOffset%2A>=800，而翻阅“退回”到滚动条中间位置附近，精确位置是 800/2000 = 40%。  
  
 自 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] 起，如果发生这种情况，将重新计算新的候选偏移。 （垂直滚动已采用这样的做法。）  
  
## <a name="impact"></a>影响  
 此更改为最终用户提供了更易于预测的直观体验，但还可能会影响依赖水平滚动后的 <xref:System.Windows.Controls.Primitives.IScrollInfo.HorizontalOffset%2A?displayProperty=fullName> 确切值的所有应用，不论水平滚动是由最终用户触发，还是由显式调用 <xref:System.Windows.Controls.Primitives.IScrollInfo.SetHorizontalOffset%2A?displayProperty=fullName> 所触发。  
  
## <a name="mitigation"></a>缓解操作  
 应将使用 <xref:System.Windows.Controls.Primitives.IScrollInfo.HorizontalOffset%2A?displayProperty=fullName> 预测值的应用更改为：在由于反虚拟化而可能更改 <xref:System.Windows.Controls.Primitives.IScrollInfo.ExtentWidth%2A> 的任何水平滚动发生后检索实际值（和 <xref:System.Windows.Controls.Primitives.IScrollInfo.ExtentWidth%2A> 值）。  
  
## <a name="see-also"></a>另请参阅  
 [运行时更改](../../../docs/framework/migration-guide/runtime-changes-in-the-net-framework-4-6-2.md)

