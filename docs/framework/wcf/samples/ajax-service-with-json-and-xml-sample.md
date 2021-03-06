---
title: "含 JSON 和 XML 的 AJAX 服務範例 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8ea5860d-0c42-4ae9-941a-e07efdd8e29c
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# 含 JSON 和 XML 的 AJAX 服務範例
這個範例會示範如何使用 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 建立會傳回 JavaScript 物件標記法 \(JSON\) 或 XML 資料的 Asynchronous JavaScript 與 XML \(AJAX\) 服務。您可以從 Web 瀏覽器用戶端使用 JavaScript 程式碼存取 AJAX 服務。這個範例是以[基本 AJAX 服務](../../../../docs/framework/wcf/samples/basic-ajax-service.md)範例為基礎所建立。  
  
 不像其他 AJAX 範例，這個範例不會使用 ASP.NET AJAX 以及 <xref:System.Web.UI.ScriptManager> 控制項。搭配一些額外組態時，便可透過 JavaScript 從任何 HTML 網頁存取 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] AJAX 服務，以下即顯示此案例。如需搭配 ASP.NET AJAX 使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的範例，請參閱 [AJAX Samples](http://msdn.microsoft.com/zh-tw/f3fa45b3-44d5-4926-8cc4-a13c30a3bf3e)。  
  
 這個範例會示範如何從 JSON 和 XML 之間切換作業的回應型別。不論是設定由 ASP.NET AJAX 或 HTML\/JavaScript 用戶端頁面存取此服務，這項功能都會提供使用。  
  
> [!NOTE]
>  此範例的安裝程序與建置指示位於本主題的結尾。  
  
 若要啟用非 ASP.NET AJAX 用戶端，請使用 .svc 檔案中的 <xref:System.ServiceModel.Activation.WebServiceHostFactory> \(而非 <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory>\)。<xref:System.ServiceModel.Activation.WebServiceHostFactory> 會將 <xref:System.ServiceModel.Description.WebHttpEndpoint> 標準端點加入至服務。此端點是在相對於 .svc 檔的空位址設定，這表示此服務的位址會是 http:\/\/localhost\/ServiceModelSamples\/service.svc，不含任何有別於作業名稱的其他後置字元。  
  
```html  
<%@ServiceHost language="c#" Debug="true" Service="Microsoft.Samples.XmlAjaxService.CalculatorService" Factory="System.ServiceModel.Activation.WebServiceHostFactory" %>  
  
```  
  
 Web.config 中的以下區段可用來針對端點進行其他組態變更。如果不需要額外的變更，也可以加以移除。  
  
```xml  
<system.serviceModel>  
  <standardEndpoints>  
    <webHttpEndpoint>  
      <!-- Use this element to configure the endpoint -->  
      <standardEndpoint name="" />  
    </webHttpEndpoint>  
  </standardEndpoints>  
</system.serviceModel>  
  
```  
  
 <xref:System.ServiceModel.Description.WebHttpEndpoint> 的預設資料格式為 XML，而 [for T:System.ServiceModel.Description.WebScriptEndpoint](assetId:///for T:System.ServiceModel.Description.WebScriptEndpoint?qualifyHint=False&autoUpgrade=True) 的預設資料格式為 JSON。如需詳細資訊，請參閱[建立不含 ASP.NET 的 WCF AJAX 服務](../../../../docs/framework/wcf/feature-details/creating-wcf-ajax-services-without-aspnet.md)。  
  
 下列範例中的服務是包含兩種作業的標準 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服務。這兩種作業的 <xref:System.ServiceModel.Web.WebGetAttribute> 或 <xref:System.ServiceModel.Web.WebInvokeAttribute> 屬性上都必須是 <xref:System.ServiceModel.Web.WebMessageBodyStyle> 本文樣式，這是 `webHttp` 行為的特定需求，而且不會影響 JSON\/XML 資料格式切換。  
  
```  
[OperationContract]  
[WebInvoke(ResponseFormat = WebMessageFormat.Xml, BodyStyle = WebMessageBodyStyle.Wrapped)]  
MathResult DoMathXml(double n1, double n2);  
```  
  
 作業的回應格式會指定為 XML，這是 [\<webHttp\>](../../../../docs/framework/configure-apps/file-schema/wcf/webhttp.md) 行為的預設值。然而，明確指定回應格式是較好的做法。  
  
 其他作業會使用 `WebInvokeAttribute` 屬性，並且明確地指定回應型別為 JSON 而不是 XML。  
  
```  
[OperationContract]  
[WebInvoke(ResponseFormat = WebMessageFormat.Json, BodyStyle = WebMessageBodyStyle.Wrapped)]  
MathResult DoMathJson(double n1, double n2);  
```  
  
 請注意，在這兩種情況中，作業都會傳回屬於標準 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 資料合約型別的複雜類型 `MathResult`。  
  
 用戶端網頁 XmlAjaxClientPage.htm 包含的 JavaScript 程式碼，會在使用者按一下該頁上的 \[**執行計算 \(傳回 JSON\)**\] 或 \[**執行計算 \(傳回 XML\)**\] 按鈕時叫用前述兩種作業的其中一種作業。叫用此服務的程式碼會建構 JSON 本文，然後使用 HTTP POST 加以傳送。此要求是使用 JavaScript 手動建立，這點不同於[基本 AJAX 服務](../../../../docs/framework/wcf/samples/basic-ajax-service.md)範例以及使用 ASP.NET AJAX 的其他範例。  
  
```  
// Create HTTP request  
var xmlHttp;  
// Request instantiation code omitted…  
// Result handler code omitted…  
  
// Build the operation URL  
var url = "service.svc/ajaxEndpoint/";  
url = url + operation;  
  
// Build the body of the JSON message  
var body = '{"n1":';  
body = body + document.getElementById("num1").value + ',"n2":';  
body = body + document.getElementById("num2").value + '}';  
  
// Send the HTTP request  
xmlHttp.open("POST", url, true);  
xmlHttp.setRequestHeader("Content-type", "application/json");  
xmlHttp.send(body);  
```  
  
 當服務回應時，回應會不經任何處理地顯示在頁面的文字方塊中。這麼做是為了示範，以便您可直接觀察所使用的 XML 和 JSON 資料格式。  
  
```  
// Create result handler   
xmlHttp.onreadystatechange=function(){  
     if(xmlHttp.readyState == 4){  
          document.getElementById("result").value = xmlHttp.responseText;  
     }  
}  
```  
  
> [!IMPORTANT]
>  這些範例可能已安裝在您的電腦上。請先檢查下列 \(預設\) 目錄，然後再繼續。  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  如果此目錄不存在，請移至[用於 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 與 Windows Workflow Foundation \(WF\) 範例](http://go.microsoft.com/fwlink/?LinkId=150780)，以下載所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 範例。此範例位於下列目錄。  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\AJAX\XmlAjaxService`  
  
#### 若要安裝、建立及執行範例  
  
1.  請確定您已執行 [Windows Communication Foundation 範例的單次安裝程序](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  使用[建置 Windows Communication Foundation 範例](../../../../docs/framework/wcf/samples/building-the-samples.md)中描述的方式建置方案 XmlAjaxService.sln。  
  
3.  瀏覽到 http:\/\/localhost\/ServiceModelSamples\/XmlAjaxClientPage.htm \(不要使用瀏覽器從專案目錄開啟 XmlAjaxClientPage.htm\)。  
  
## 請參閱  
 [使用 HTTP POST 的 AJAX 服務](../../../../docs/framework/wcf/samples/ajax-service-using-http-post.md)