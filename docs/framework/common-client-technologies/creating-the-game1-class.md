---
title: "建立 Game1 類別"
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
ms.contentlocale: zh-tw
ms.lasthandoff: 07/28/2017

---
# Creating the Game1 Class
針對所有 Microsoft XNA 專案，Game1 類別衍生自 [Microsoft.Xna.Framework.Game](http://msdn.microsoft.com/library/microsoft.xna.framework.game.aspx) 類別，其為 XNA 遊戲提供基本的圖形裝置初始化、遊戲邏輯和轉譯程式碼。  Game1 類別相當簡單，因為大部分工作都是在 GamePiece 和 GamePieceCollection 類別中完成。  
  
## 建立程式碼  
 此類別的私用成員包括用來保存遊戲片段的 **GamePieceCollection** 物件、[GraphicsDeviceManager](http://msdn.microsoft.com/library/microsoft.xna.framework.graphicsdevicemanager.aspx) 物件，以及用來轉譯遊戲片段的 [SpriteBatch](http://msdn.microsoft.com/library/microsoft.xna.framework.graphics.spritebatch.aspx) 物件。  
  
 [!code-csharp[ManipulationXNA#_Game1_PrivateMembers](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_privatemembers)]  
  
 在遊戲初始化期間，這些物件會具現化。  
  
 [!code-csharp[ManipulationXNA#_Game1_ConstructorInitialize](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_constructorinitialize)]  
  
 呼叫 [LoadContent](http://msdn.microsoft.com/library/microsoft.xna.framework.game.loadcontent.aspx) 方法時，會建立遊戲片段，並將其指派給 **GamePieceCollection** 物件。  遊戲片段分為兩種類型：  片段的縮放比例稍有變更，導致有些片段較小，有些片段較大。  
  
 [!code-csharp[ManipulationXNA#_Game1_LoadContent](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_loadcontent)]  
  
 遊戲執行時，XNA Framework 會重複呼叫 [Update](http://msdn.microsoft.com/library/microsoft.xna.framework.game.update.aspx) 方法。  [Update](http://msdn.microsoft.com/library/microsoft.xna.framework.game.update.aspx) 方法會在遊戲片段集合上呼叫 **ProcessInertia** 和 **UpdateFromMouse** 方法。  [Creating the GamePieceCollection Class](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md)中有這些方法的說明。  
  
 [!code-csharp[ManipulationXNA#_Game1_UpdateGame](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_updategame)]  
  
 遊戲執行時，XNA Framework 也會重複呼叫 [Draw](http://msdn.microsoft.com/library/microsoft.xna.framework.game.draw.aspx) 方法。  [Draw](http://msdn.microsoft.com/library/microsoft.xna.framework.game.draw.aspx) 方法會藉由呼叫 **GamePieceCollection** 物件的 **Draw** 方法來執行遊戲片段的轉譯。  [Creating the GamePieceCollection Class](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md)中有這個方法的說明。  
  
 [!code-csharp[ManipulationXNA#_Game1_DrawGame](../../../samples/snippets/csharp/VS_Snippets_Misc/manipulationxna/cs/game1.cs#_game1_drawgame)]  
  
## <a name="see-also"></a>另請參閱  
 [操作和慣性](../../../docs/framework/common-client-technologies/manipulations-and-inertia.md)   
 [在 XNA 應用程式中使用操作和慣性](../../../docs/framework/common-client-technologies/use-manipulations-and-inertia-in-an-xna-application.md)   
 [建立 GamePiece 類別](../../../docs/framework/common-client-technologies/creating-the-gamepiece-class.md)   
 [建立 GamePieceCollection 類別](../../../docs/framework/common-client-technologies/creating-the-gamepiececollection-class.md)   
 [完整程式碼清單](../../../docs/framework/common-client-technologies/full-code-listings.md)

