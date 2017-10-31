---
title: "创建 Game1 类"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 47932ce3-2ba5-476f-a26b-3ddfd5226f27
caps.latest.revision: 8
author: wadepickett
ms.author: wpickett
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 9c6d0bdfd21f431ae6da38e3868386f91d5b725b
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="creating-the-game1-class"></a>创建 Game1 类
在所有的 Microsoft XNA 项目中，Game1 类都派生自 [Microsoft.Xna.Framework.Game](http://msdn.microsoft.com/library/microsoft.xna.framework.game.aspx) 类，后者提供了 XNA 游戏的基本图形设备初始化、游戏逻辑和呈现代码。 Game1 类相对简单，因为大部分工作是在 GamePiece 和 GamePieceCollection 类中完成的。  
  
## <a name="creating-the-code"></a>创建代码  
 该类的私有成员包括用于保存游戏块的 GamePieceCollection 对象、[GraphicsDeviceManager](http://msdn.microsoft.com/library/microsoft.xna.framework.graphicsdevicemanager.aspx) 对象和用于呈现游戏块的 [SpriteBatch](http://msdn.microsoft.com/library/microsoft.xna.framework.graphics.spritebatch.aspx)。  
  
 [!code-csharp[ManipulationXNA#_Game1_PrivateMembers](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_privatemembers)]  
  
 在游戏初始化期间，这些对象被实例化。  
  
 [!code-csharp[ManipulationXNA#_Game1_ConstructorInitialize](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_constructorinitialize)]  
  
 调用 [LoadContent](http://msdn.microsoft.com/library/microsoft.xna.framework.game.loadcontent.aspx) 方法时，会创建游戏块并将其分配给 GamePieceCollection 对象。 有以下两种类型的游戏块。 略微更改这些游戏块的缩放比例，以便小块和大块同时存在。  
  
 [!code-csharp[ManipulationXNA#_Game1_LoadContent](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_loadcontent)]  
  
 游戏运行时，XNA Framework 会反复调用 [Update](http://msdn.microsoft.com/library/microsoft.xna.framework.game.update.aspx) 方法。 [Update](http://msdn.microsoft.com/library/microsoft.xna.framework.game.update.aspx) 方法会对游戏块集合调用 **ProcessInertia** 和 **UpdateFromMouse** 方法。 [创建 GamePieceCollection 类](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md)中介绍了这些方法。  
  
 [!code-csharp[ManipulationXNA#_Game1_UpdateGame](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_updategame)]  
  
 游戏运行时，XNA Framework 也会反复调用 [Draw](http://msdn.microsoft.com/library/microsoft.xna.framework.game.draw.aspx) 方法。 [Draw](http://msdn.microsoft.com/library/microsoft.xna.framework.game.draw.aspx) 方法通过调用 GamePieceCollection 对象的 Draw 方法来呈现游戏块。 [创建 GamePieceCollection 类](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md)中介绍了这些方法。  
  
 [!code-csharp[ManipulationXNA#_Game1_DrawGame](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_drawgame)]  
  
## <a name="see-also"></a>另请参阅  
 [操作和惯性](../../../docs/framework/common-client-technologies/manipulations-and-inertia.md)   
 [在 XNA 应用程序中使用操作和惯性](../../../docs/framework/common-client-technologies/use-manipulations-and-inertia-in-an-xna-application.md)   
 [创建 GamePiece 类](../../../docs/framework/common-client-technologies/creating-the-gamepiece-class.md)   
 [创建 GamePieceCollection 类](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md)   
 [完整代码清单](../../../docs/framework/common-client-technologies/full-code-listings.md)

