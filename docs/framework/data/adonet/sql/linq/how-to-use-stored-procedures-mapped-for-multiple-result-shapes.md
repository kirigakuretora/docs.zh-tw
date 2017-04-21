---
title: "HOW TO：使用對應多個結果圖案的預存程序 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c2b84dfe-7fec-489a-92de-45215cec4518
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# HOW TO：使用對應多個結果圖案的預存程序
如果預存程序 \(Stored Procedure\) 可以傳回多個結果圖案，則傳回型別不可以強型別 \(Strongly Typed\) 為單一投影圖案。  雖然 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 可以產生所有可能的投影型別，但是無法得知它們傳回的順序。  
  
 請將這個案例與循序產生多個結果圖案的預存程序案例比較。  如需詳細資訊，請參閱[HOW TO：使用對應循序結果圖案的預存程序](../../../../../../docs/framework/data/adonet/sql/linq/how-to-use-stored-procedures-mapped-for-sequential-result-shapes.md)。  
  
 <xref:System.Data.Linq.Mapping.ResultTypeAttribute> 屬性 \(Attribute\) 會套用至傳回多個結果型別的預存程序，以指定程序可以傳回的型別集。  
  
## 範例  
 在下列 SQL 程式碼範例中，結果圖案會根據輸入 \(`shape =1` 或 `shape = 2`\) 而不同。  您無法得知會先傳回哪個投影。  
  
```  
CREATE PROCEDURE VariableResultShapes(@shape int)  
AS  
if(@shape = 1)  
    select CustomerID, ContactTitle, CompanyName from customers  
else if(@shape = 2)  
    select OrderID, ShipName from orders  
```  
  
 [!code-csharp[DLinqSprox#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSprox/cs/northwind-sprox.cs#4)]
 [!code-vb[DLinqSprox#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSprox/vb/northwind-sprox.vb#4)]  
  
## 範例  
 您可使用類似下列的程式碼來執行此預存程序。  
  
> [!NOTE]
>  您必須使用 <xref:System.Data.Linq.IMultipleResults.GetResult%2A> 模式，根據您對預存程序的了解以取得正確型別的列舉值。  
  
 [!code-csharp[DLinqSprox#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSprox/cs/Program.cs#5)]
 [!code-vb[DLinqSprox#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSprox/vb/Module1.vb#5)]  
  
## 請參閱  
 [預存程序](../../../../../../docs/framework/data/adonet/sql/linq/stored-procedures.md)