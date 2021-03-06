---
title: "程式設計模型項目樹狀 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0229efde-19ac-4bdc-a187-c6227a7bd1a5
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# 程式設計模型項目樹狀
這個範例示範如何使用來自 [!INCLUDE[avalon1](../../../../includes/avalon1-md.md)] 樹狀檢視的宣告式資料繫結巡覽 <xref:System.Activities.Presentation.Model.ModelItem> 樹狀結構。  
  
## 範例詳細資料  
 <xref:System.Activities.Presentation.Model.ModelItem> 樹狀結構是一個抽象概念，由 [!INCLUDE[wfd1](../../../../includes/wfd1-md.md)] 基礎結構用來公開要編輯之基礎執行個體的相關資料。下圖描述 [!INCLUDE[wfd2](../../../../includes/wfd2-md.md)] 內基礎結構的各個不同層。  
  
 ![Workflow Designer 架構](../../../../docs/framework/windows-workflow-foundation/samples/media/workflowdesignerarch.JPG "WorkflowDesignerArch")  
  
 <xref:System.Activities.Presentation.Model.ModelItem> 包含基礎值的指標，以及 <xref:System.Activities.Presentation.Model.ModelProperty> 物件的集合。<xref:System.Activities.Presentation.Model.ModelProperty> 物件則是由名稱、屬性型別和值的指標這類資料所構成，而值的指標則會是另一個 <xref:System.Activities.Presentation.Model.ModelItem>。值轉換子可用來操作從 <xref:System.Activities.Presentation.Model.ModelProperty> 傳回的一些 <xref:System.Activities.Presentation.Model.ModelItem>，讓它們在樹狀檢視中正確顯示。接著這個範例會示範如何使用命令式語法，以命令方式對 <xref:System.Activities.Presentation.Model.ModelItem> 樹狀結構進行程式設計，如下面範例中所示。  
  
```csharp  
ModelItem mi = wd.Context.Services.GetService<ModelService>().Root;  
ModelProperty mp = mi.Properties["Activities"];  
mp.Collection.Add(new Persist());  
ModelItem justAdded = mp.Collection.Last();  
justAdded.Properties["DisplayName"].SetValue("new name");  
  
```  
  
#### 若要使用這個範例  
  
1.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 中開啟 \[ProgrammingModelItemTree.sln\] 方案。  
  
2.  從 \[**建置**\] 功能表選取 \[**建置方案**\]，藉此建置方案。  
  
3.  按 F5 執行應用程式。[!INCLUDE[avalon2](../../../../includes/avalon2-md.md)] 格式隨即顯示。  
  
4.  按一下 \[**載入 WF**\] 按鈕載入 <xref:System.Activities.Presentation.Model.ModelItem>，並將它繫結至樹狀檢視。  
  
5.  按一下 \[**變更模型項目樹狀檢視**\] 按鈕會執行上述的程式碼，將項目加入至樹狀結構中並且設定屬性。  
  
> [!IMPORTANT]
>  這些範例可能已安裝在您的電腦上。請先檢查下列 \(預設\) 目錄，然後再繼續。  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  如果此目錄不存在，請移至[用於 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 與 Windows Workflow Foundation \(WF\) 範例](http://go.microsoft.com/fwlink/?LinkId=150780)，以下載所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。此範例位於下列目錄。  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Designer\ProgrammingModelItemTree`  
  
## 請參閱  
 <xref:System.Windows.Data.IValueConverter>