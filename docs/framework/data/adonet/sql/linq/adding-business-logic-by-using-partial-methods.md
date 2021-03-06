---
title: "使用部分方法加入商務邏輯 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3a73991e-fd4e-4610-93fb-7ced4dc6b7f9
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 使用部分方法加入商務邏輯
您可以使用「*部分方法*.」\(Partial Method\)，在 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 專案中自訂 [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] 和 C\# 產生的程式碼。  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 產生的程式碼會將簽章定義成部分方法的一部分。  如果您想實作此方法，可以加入自己的部分方法。  如果您未加入自己的實作 \(Implementation\)，則編譯器 \(Compiler\) 會捨棄部分方法簽章並呼叫 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 中的預設方法。  
  
> [!NOTE]
>  如果您使用的是 [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)]，可以使用[!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)]將驗證和其他自訂加入至實體類別。  
  
 例如，Northwind 範例資料庫中 `Customer` 類別的預設對應包含下列部分方法：  
  
 [!code-csharp[DLinqOverrideDefault#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqOverrideDefault/cs/northwind.cs#2)]
 [!code-vb[DLinqOverrideDefault#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqOverrideDefault/vb/northwind.vb#2)]  
  
 您可以將下列程式碼加入至自己的部分 `Customer` 類別，進而實作自己的方法：  
  
 [!code-csharp[DLinqOverrideDefault#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqOverrideDefault/cs/Program.cs#3)]
 [!code-vb[DLinqOverrideDefault#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqOverrideDefault/vb/Module1.vb#3)]  
  
 這種方法通常用於 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 中，以覆寫 `Insert`、`Update`、`Delete` 的預設方法，以及驗證物件生命週期事件中的屬性。  
  
 如需詳細資訊，請參閱[Partial Methods](../Topic/Partial%20Methods%20\(Visual%20Basic\).md) \([!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)]\) 或[partial \(方法\) \(C\# 參考\)](../Topic/partial%20\(Method\)%20\(C%23%20Reference\).md) \(C\#\)。  
  
## 範例  
  
### 描述  
 下列範例會先顯示 `ExampleClass`，因為它可能是由程式碼產生工具 \(例如 SQLMetal\) 所定義，然後顯示您如何僅實作其中一種方法。  
  
### 程式碼  
 [!code-csharp[DLinqSubmittingChanges#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#4)]
 [!code-vb[DLinqSubmittingChanges#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#4)]  
  
## 範例  
  
### 描述  
 下列範例會使用 `Shipper` 和 `Order` 實體 \(Entity\) 之間的關聯性 \(Relationship\)。  請注意部分方法中的 `InsertShipper` 和 `DeleteShipper` 方法。  這些方法會覆寫 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 對應所提供的預設部分方法。  
  
### 程式碼  
 [!code-csharp[DLinqOverrideDefault#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqOverrideDefault/cs/northwind.cs#1)]
 [!code-vb[DLinqOverrideDefault#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqOverrideDefault/vb/northwind.vb#1)]  
  
## 請參閱  
 [進行和提交資料變更](../../../../../../docs/framework/data/adonet/sql/linq/making-and-submitting-data-changes.md)   
 [自訂插入、更新和刪除作業](../../../../../../docs/framework/data/adonet/sql/linq/customizing-insert-update-and-delete-operations.md)