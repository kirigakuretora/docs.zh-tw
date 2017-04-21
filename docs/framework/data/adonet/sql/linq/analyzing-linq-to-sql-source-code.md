---
title: "分析 LINQ to SQL 原始程式碼 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cba3eef8-e108-4478-b588-ad59580e133e
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# 分析 LINQ to SQL 原始程式碼
使用下列步驟，您就可以從 Northwind 範例資料庫產生 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 原始程式碼。  您可以比較物件模型的項目與資料庫的項目，進一步了解不同項目的對應方式。  
  
> [!NOTE]
>  使用 [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] 的開發人員可以使用 [!INCLUDE[vs_ordesigner_short](../../../../../../includes/vs-ordesigner-short-md.md)] 來產生這個程式碼。  
  
1.  如果您的開發電腦上還沒有 Northwind 範例資料庫，則可以免費進行下載。  如需詳細資訊，請參閱[下載範例資料庫](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md)。  
  
2.  使用 SqlMetal 命令列工具產生 Visual Basic 或 C\# 原始程式檔。  如需詳細資訊，請參閱[SqlMetal.exe \(程式碼產生工具\)](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md)。  在命令提示字元中輸入下列命令，就可以產生內含預存程序 \(Stored Procedure\) 和函式的 Visual Basic 和 C\# 原始程式檔：  
  
    -   `sqlmetal /code:northwind.vb /language:vb "c:\northwnd.mdf" /sprocs /functions /pluralize`  
  
    -   `sqlmetal /code:northwind.cs /language:csharp "c:\northwnd.mdf" /sprocs /functions /pluralize`  
  
## 請參閱  
 [參考資料](../../../../../../docs/framework/data/adonet/sql/linq/reference.md)   
 [背景資訊](../../../../../../docs/framework/data/adonet/sql/linq/background-information.md)