---
title: "创建 GamePiece 类"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 37a27a86-ac1c-47be-b477-cb4b819459d3
caps.latest.revision: 9
author: wadepickett
ms.author: wpickett
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 7ac9884766812cd635b5a70c028cf15c19838511
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="creating-the-gamepiece-class"></a>创建 GamePiece 类
GamePiece 类封装加载 Microsoft XNA 游戏块图像、跟踪与游戏块相关的鼠标状态、捕获鼠标、提供操作和惯性处理以及在游戏块达到视区限制时提供弹跳功能所需的所有功能。  
  
## <a name="private-members"></a>私有成员  
 在 GamePiece 类的顶部，声明了多个私有成员。  
  
 [!code-csharp[ManipulationXNA#_GamePiece_PrivateMembers](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_privatemembers)]  
  
## <a name="public-properties"></a>公共属性  
 这些私有成员中的三个是通过公共属性公开的。 Scale 和 PieceColor 属性使应用程序能够分别指定块的比例和颜色。 公开 Bounds 属性从而使一个块可以使用另一个块的边界来呈现自身，例如当一个块应覆盖另一个块时。 下面的代码显示公共属性的声明。  
  
 [!code-csharp[ManipulationXNA#_GamePiece_PublicProperties](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_publicproperties)]  
  
## <a name="class-constructor"></a>类构造函数  
 GamePiece 类的构造函数接受以下参数：  
  
-   [SpriteBatch](http://msdn.microsoft.com/library/microsoft.xna.framework.graphics.spritebatch.aspx) 类型。 在此处传递的引用被分配给私有成员 `spriteBatch`，并在游戏块呈现自身时用于访问 [SpriteBatch.Draw](http://msdn.microsoft.com/library/microsoft.xna.framework.graphics.spritebatch.draw.aspx) 方法。 此外，[GraphicsDevice](http://msdn.microsoft.com/library/microsoft.xna.framework.graphics.spritebatch.graphicsdevice.aspx) 属性用于创建与游戏块关联的 [Texture](http://msdn.microsoft.com/library/microsoft.xna.framework.graphics.texture.aspx) 对象，及获取视区大小，从而检测出游戏块遇到窗口边界的时间，实现游戏块回弹。  
  
-   指定要用于游戏块的图像的文件名的字符串。  
  
 构造函数还创建 <xref:System.Windows.Input.Manipulations.ManipulationProcessor2D> 对象和 <xref:System.Windows.Input.Manipulations.InertiaProcessor2D> 对象，并为它们的事件建立事件处理程序。  
  
 下面的代码显示了 GamePiece 类的构造函数。  
  
 [!code-csharp[ManipulationXNA#_GamePiece_Constructor](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_constructor)]  
  
## <a name="capturing-mouse-input"></a>捕获鼠标输入  
 UpdateFromMouse 方法负责检测在鼠标位于游戏块边界内时按下鼠标按钮的时间，并且用于检测释放鼠标按钮的时间。  
  
 按下鼠标左键时（鼠标位于块边界内），此方法设置标志以指示此游戏块已捕获鼠标并开始操作处理。  
  
 通过创建 <xref:System.Windows.Input.Manipulations.Manipulator2D> 对象的数组并将它们传递给 <xref:System.Windows.Input.Manipulations.ManipulationProcessor2D> 对象来启动操作处理。 这将导致操作处理器评估操控器（在这种情况下为单操控器），并引发操作事件。  
  
 此外，将保存发生拖动的点。 随后会在 <xref:System.Windows.Input.Manipulations.ManipulationProcessor2D.Delta> 事件期间使用它来调整增量转换值，以便游戏块波动成拖动点之后的线。  
  
 最后，此方法返回鼠标捕获的状态。 这使 [GamePieceCollection](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md) 对象可在存在多个游戏块时管理捕获。  
  
 下面的代码显示了 UpdateFromMouse 方法。  
  
 [!code-csharp[ManipulationXNA#_GamePiece_UpdateFromMouse](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_updatefrommouse)]  
  
## <a name="processing-manipulations"></a>处理操作  
 操作开始时，引发 <xref:System.Windows.Input.Manipulations.ManipulationProcessor2D.Started> 事件。 此事件的处理程序将停止惯性处理（如果发生惯性处理），并将 processInertia 标记设置为 `false`。  
  
 [!code-csharp[ManipulationXNA#_GamePiece_OnManipulationStarted](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_onmanipulationstarted)]  
  
 由于与操作关联的值发生变化，将引发 <xref:System.Windows.Input.Manipulations.ManipulationProcessor2D.Delta> 事件。 此事件的处理程序使用事件自变量中传递的增量值来对游戏块的位置和旋转值进行更改。  
  
 [!code-csharp[ManipulationXNA#_GamePiece_OnManipulationDelta](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_onmanipulationdelta)]  
  
 删除所有与操作关联的操控器（这种情况下为单个操控器）后，操作处理器将引发 <xref:System.Windows.Input.Manipulations.ManipulationProcessor2D.Completed> 事件。 此事件的处理程序通过将惯性处理器的初速度设置为事件自变量报告的初速度来开始惯性处理，并将 processInertia 标志设置为 `true`。  
  
 [!code-csharp[ManipulationXNA#_GamePiece_OnManipulationCompleted](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_onmanipulationcompleted)]  
  
## <a name="processing-inertia"></a>处理惯性  
 当惯性处理为角速度和线速度、位置（转换）坐标和旋转外推新值时，引发 <xref:System.Windows.Input.Manipulations.InertiaProcessor2D.Delta> 事件。 此事件的处理程序使用事件参数中传递的增量值来修改游戏块的位置和旋转。  
  
 如果新坐标导致游戏块移到视区边界外，则惯性处理速度将被反转。 这将导致游戏块弹出已遇到的视区边界。  
  
 运行外推法时，不能更改 <xref:System.Windows.Input.Manipulations.InertiaProcessor2D> 对象的属性。 因此，反转 X 或 Y 速度时，事件处理程序首先通过调用 <xref:System.Windows.Input.Manipulations.InertiaProcessor2D.Complete%2A> 方法停止惯性。 然后，它将新的初速度值指派为当前速度值（为 sponge 行为进行调整），并将 processInertia 标记设置为 `true`。  
  
 下面的代码显示 <xref:System.Windows.Input.Manipulations.InertiaProcessor2D.Delta> 事件的事件处理程序。  
  
 [!code-csharp[ManipulationXNA#_GamePiece_OnInertiaDelta](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_oninertiadelta)]  
  
 惯性处理完成后，惯性处理器将引发 <xref:System.Windows.Input.Manipulations.InertiaProcessor2D.Completed> 事件。 此事件的处理程序将 processInertia 标记设置为 `false`。  
  
 [!code-csharp[ManipulationXNA#_GamePiece_OnInertiaCompleted](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_oninertiacompleted)]  
  
 没有任何迄今存在的逻辑实际导致惯性外推的发生。 这是在 ProcessInertia 方法中完成的。 从游戏更新循环中反复调用的这一方法（[Game.Update](http://msdn.microsoft.com/library/microsoft.xna.framework.game.update.aspx) 方法）检查是否已将 processInertia 标志设置为 `true`，如果是，则调用 <xref:System.Windows.Input.Manipulations.InertiaProcessor2D.Process%2A> 方法。 调用此方法会导致发生外推，并引发 <xref:System.Windows.Input.Manipulations.InertiaProcessor2D.Delta> 事件。  
  
 [!code-csharp[ManipulationXNA#_GamePiece_ProcessInertia](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_processinertia)]  
  
 直到调用了 Draw 方法重载之一，才会实际呈现游戏块。 程序会反复从游戏绘制循环中调用此方法的第一个重载（[Game.Draw](http://msdn.microsoft.com/library/microsoft.xna.framework.game.draw.aspx) 方法）。 这会使游戏块呈现当前的位置、旋转和比例因子。  
  
 [!code-csharp[ManipulationXNA#_GamePiece_Draw](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_draw)]  
  
## <a name="additional-properties"></a>其他属性  
 GamePiece 类使用三个专用属性。  
  
1.  Timestamp - 获取操作和惯性处理器将要使用的时间戳值。  
  
2.  X - 获取或设置游戏块的 X 坐标。 设置时，调整用于命中测试和操作处理器的枢轴位置的边界。  
  
3.  Y - 获取或设置游戏块的 Y 坐标。 设置时，调整用于命中测试和操作处理器的枢轴位置的边界。  
  
 [!code-csharp[ManipulationXNA#_GamePiece_PrivateProperties](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/gamepiece.cs#_gamepiece_privateproperties)]  
  
## <a name="see-also"></a>另请参阅  
 [操作和惯性](../../../docs/framework/common-client-technologies/manipulations-and-inertia.md)   
 [在 XNA 应用程序中使用操作和惯性](../../../docs/framework/common-client-technologies/use-manipulations-and-inertia-in-an-xna-application.md)   
 [创建 GamePieceCollection 类](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md)   
 [创建 Game1 类](../../../docs/framework/common-client-technologies/creating-the-game1-class.md)

