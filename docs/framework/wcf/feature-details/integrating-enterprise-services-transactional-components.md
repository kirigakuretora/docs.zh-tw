---
title: "整合 Enterprise Services 異動元件 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 05dab277-b8b2-48cf-b40c-826be128b175
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 整合 Enterprise Services 異動元件
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 提供能與 Enterprise Services 整合的自動機制 \(請參閱[整合 COM\+ 應用程式](../../../../docs/framework/wcf/feature-details/integrating-with-com-plus-applications.md)\)。不過，您可能希望能夠彈性地開發出可透過內部方式使用裝載於 Enterprise Services 之交易元件的服務。由於 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 交易功能是建置在 <xref:System.Transactions> 基礎結構上，所以將 Enterprise Services 與 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 整合的程序就跟指定 <xref:System.Transactions> 和 Enterprise Services 之間互通性的程序完全相同，如 [Enterprise Services 和 COM\+ 交易的互通性](http://go.microsoft.com/fwlink/?LinkId=94949) \(本頁面可能為英文\) 中所述。  
  
 為了在傳入的流動交易和 COM\+ 內容交易之間提供所需等級的互通性，此服務的實作必須建立 <xref:System.Transactions.TransactionScope> 執行個體並使用適當的 <xref:System.Transactions.EnterpriseServicesInteropOption> 列舉值。  
  
## 整合 Enterprise Services 和服務作業  
 下列程式碼範例會示範一項允許交易流程的作業，這項作業會建立具有 <xref:System.Transactions.EnterpriseServicesInteropOption> 選項的 <xref:System.Transactions.TransactionScope>。下列狀況適用於本案例：  
  
-   如果用戶端流動交易，則作業 \(包括 Enterprise Services 元件的呼叫\) 會在該交易的範圍內執行。使用 <xref:System.Transactions.EnterpriseServicesInteropOption> 會確保交易與 <xref:System.EnterpriseServices> 內容為同步處理，也就是說 <xref:System.Transactions> 的環境交易和 <xref:System.EnterpriseServices> 會是相同的。  
  
-   如果用戶端沒有流動交易，此時將 <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> 設定為 `true` 便會建立供作業使用的新交易範圍。同樣地，使用 <xref:System.Transactions.EnterpriseServicesInteropOption> 可確保作業的交易與 <xref:System.EnterpriseServices> 元件內容中所使用的交易是相同的。  
  
 任何其他的方法呼叫也會發生在相同作業的交易範圍內。  
  
```  
[ServiceContract()]  
public interface ICustomerServiceContract  
{  
   [OperationContract]  
   [TransactionFlow(TransactionFlowOption.Allowed)]  
   void UpdateCustomerNameOperation(int customerID, string newCustomerName);  
}  
  
[ServiceBehavior(TransactionIsolationLevel = System.Transactions.IsolationLevel.Serializable)]  
public class CustomerService : ICustomerServiceContract  
{  
   [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = true)]  
   public void UpdateCustomerNameOperation(int customerID, string newCustomerName)  
   {  
   // Create a transaction scope with full ES interop  
      using (TransactionScope ts = new TransactionScope(  
                     TransactionScopeOption.Required,  
                     new TransactionOptions(),  
                     EnterpriseServicesInteropOption.Full))  
      {  
         // Create an Enterprise Services component  
         // Call UpdateCustomer method on an Enterprise Services   
         // component   
  
         // Call UpdateOtherCustomerData method on an Enterprise   
         // Services component   
         ts.Complete();  
      }  
  
      // Do UpdateAdditionalData on an non-Enterprise Services  
      // component  
   }  
}  
```  
  
 如果作業的目前交易和 Enterprise Services 交易元件的呼叫之間不需要同步處理，那麼請在初始化 <xref:System.Transactions.TransactionScope> 執行個體時使用 <xref:System.Transactions.EnterpriseServicesInteropOption> 選項。  
  
## 整合 Enterprise Services 和用戶端  
 下列程式碼會示範以 <xref:System.Transactions.EnterpriseServicesInteropOption> 設定來使用 <xref:System.Transactions.TransactionScope> 執行個體的用戶端程式碼。在此案例中，支援交易流程的服務作業呼叫會發生於呼叫 Enterprise Services 元件的相同交易範圍內，  
  
```  
static void Main()  
{  
    // Create a client  
    CalculatorClient client = new CalculatorClient();  
  
    // Create a transaction scope with full ES interop  
    using (TransactionScope ts = new TransactionScope(  
          TransactionScopeOption.Required,  
          new TransactionOptions(),  
          EnterpriseServicesInteropOption.Full))  
    {  
        // Call Add calculator service operation  
  
        // Create an Enterprise Services component  
  
        // Call UpdateCustomer method on an Enterprise Services   
        // component   
  
        ts.Complete();  
    }  
  
    // Closing the client gracefully closes the connection and   
    // cleans up resources  
    client.Close();  
}  
```  
  
## 請參閱  
 [整合 COM\+ 應用程式](../../../../docs/framework/wcf/feature-details/integrating-with-com-plus-applications.md)   
 [整合 COM 應用程式](../../../../docs/framework/wcf/feature-details/integrating-with-com-applications.md)