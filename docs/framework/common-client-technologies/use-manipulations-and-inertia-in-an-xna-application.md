---
title: "在 XNA 应用程序中使用操作和惯性"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b7c18905-850c-4da4-8977-a074406a4263
caps.latest.revision: 7
author: wadepickett
ms.author: wpickett
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 7d623a8c2276811ae443a4d745faffeeb79ffc6f
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="using-manipulations-and-inertia-in-an-xna-application"></a>在 XNA 应用程序中使用操作和惯性
本文介绍如何在 Microsoft XNA 应用程序中使用操作和惯性处理来控制游戏块的移动。 在阅读本文之前，应熟悉[操作和惯性概述](../../../docs/framework/common-client-technologies/manipulations-and-inertia-overview.md)主题以及基本的 XNA 编程概念。  
  
 若要执行本文所述的任务，你的 XNA 项目必须引用 <xref:System.Windows.Input.Manipulations> 程序集，且必须在计算机上安装 [XNA Game Studio](http://msdn.microsoft.com/library/bb200104.aspx)（[下载地址](http://www.microsoft.com/downloads/details.aspx?FamilyId=7D70D6ED-1EDD-4852-9883-9A33C0AD8FEE&displaylang=en)），这样你的项目才可以引用 XNA 程序集。  
  
## <a name="overview-of-functionality"></a>功能概述  
 本文介绍了如何创建表示游戏块（该游戏块使用操作和惯性处理）的自定义类。 此类使你能通过用鼠标拖动然后释放游戏块，在屏幕上操作游戏块。 一旦释放，惯性处理在游戏块逐渐减速的过程中使其保持移动。 移动是线性的和具有角度的。  
  
 ![一个简单的操作和惯性应用程序。](../../../docs/framework/common-client-technologies/media/ndp-gamexna.jpg "NDP_GameXna")  
  
 此外，创建了一个自定义集合，用于管理多个游戏块。 这简化了 XNA 游戏类所需的处理。  
  
 [创建 GamePiece 类](../../../docs/framework/common-client-technologies/creating-the-gamepiece-class.md)  
  
 [创建 GamePieceCollection 类](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md)  
  
 [创建 Game1 类](../../../docs/framework/common-client-technologies/creating-the-game1-class.md)  
  
 [完整代码清单](../../../docs/framework/common-client-technologies/full-code-listings.md)  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Windows.Input.Manipulations>   
 [控制和惯性概述](../../../docs/framework/common-client-technologies/manipulations-and-inertia-overview.md)

