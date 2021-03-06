---
title: "HOW TO：自訂系統提供的繫結 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f8b97862-e8bb-470d-8b96-07733c21fe26
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# HOW TO：自訂系統提供的繫結
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 所包含的數種系統提供繫結可讓您設定一些基礎繫結項目的屬性，但不包含所有屬性。  本主題示範如何設定繫結項目上的屬性來建立自訂繫結。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]如何直接建立與設定繫結項目，而不使用系統提供繫結的詳細資訊，請參閱[自訂繫結](../../../../docs/framework/wcf/extending/custom-bindings.md)。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]建立並延伸自訂繫結的詳細資訊，請參閱[擴充繫結](../../../../docs/framework/wcf/extending/extending-bindings.md)。  
  
 在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中，所有的繫結是由「*繫結項目*」\(Binding Element\) 所構成。  每個繫結項目均衍生自 <xref:System.ServiceModel.Channels.BindingElement> 類別。  諸如 <xref:System.ServiceModel.BasicHttpBinding> 的系統提供繫結，會建立並設定自有的繫結項目。  本主題說明如何存取與變更這些繫結項目的屬性，而這些屬性並未直接在繫結上公開 \(特別是 <xref:System.ServiceModel.BasicHttpBinding> 類別\)。  
  
 個別的繫結項目會包含在由 <xref:System.ServiceModel.Channels.BindingElementCollection> 類別表示的集合中，並依下列順序新增：交易流程、可靠工作階段、安全性、複合雙工、單向、資料流安全性、訊息編碼和傳輸。  請注意，並非每個繫結都需要所列的所有繫結項目。  使用者定義的繫結項目也可以出現在此繫結項目集合中，而且必須依照前述順序。  例如，使用者定義的傳輸必須是繫結項目集合中的最後一個項目。  
  
 <xref:System.ServiceModel.BasicHttpBinding> 類別包含三個繫結項目：  
  
1.  一種選擇性的安全性繫結項目，可以是搭配 HTTP 傳輸 \(訊息層級安全性\) 一起使用的 <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement> 類別，或是當傳輸層提供安全性時所使用的 <xref:System.ServiceModel.Channels.TransportSecurityBindingElement> 類別 \(這時會使用 HTTPS 傳輸\)。  
  
2.  必要的訊息編碼器繫結項目，可以是 <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> 或 <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement>。  
  
3.  必要的傳輸繫結項目，可以是 <xref:System.ServiceModel.Channels.HttpTransportBindingElement> 或 <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>。  
  
 在此範例中，我們會建立一個繫結執行個體、從中產生一個「*自訂繫結*」\(Custom Binding\)、檢查自訂繫結中的繫結項目，並在找到 HTTP 繫結項目時，將其 `KeepAliveEnabled` 屬性設為 `false`。  `KeepAliveEnabled` 屬性不會直接在 `BasicHttpBinding` 上公開，因此我們必須建立自訂繫結以向下巡覽至繫結項目並設定此屬性。  
  
### 若要修改系統提供的繫結  
  
1.  建立 <xref:System.ServiceModel.BasicHttpBinding> 類別的執行個體，並將其安全性模式設為訊息層級。  
  
     [!code-csharp[C_HowTo_ChangeStandardBinding#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_changestandardbinding/cs/program.cs#1)]
     [!code-vb[C_HowTo_ChangeStandardBinding#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_changestandardbinding/vb/program.vb#1)]  
  
2.  從繫結中建立自訂繫結，並從其中一個自訂繫結的屬性中建立 <xref:System.ServiceModel.Channels.BindingElementCollection> 類別。  
  
     [!code-csharp[C_HowTo_ChangeStandardBinding#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_changestandardbinding/cs/program.cs#2)]
     [!code-vb[C_HowTo_ChangeStandardBinding#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_changestandardbinding/vb/program.vb#2)]  
  
3.  對 <xref:System.ServiceModel.Channels.BindingElementCollection> 類別執行迴圈，並在找到 <xref:System.ServiceModel.Channels.HttpTransportBindingElement> 類別時，將其 <xref:System.ServiceModel.Channels.HttpTransportBindingElement.KeepAliveEnabled%2A> 屬性設為 `false`。  
  
     [!code-csharp[C_HowTo_ChangeStandardBinding#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_changestandardbinding/cs/program.cs#3)]
     [!code-vb[C_HowTo_ChangeStandardBinding#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_changestandardbinding/vb/program.vb#3)]  
  
## 請參閱  
 <xref:System.ServiceModel.Channels.HttpTransportBindingElement>   
 <xref:System.ServiceModel.BasicHttpBinding>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [自訂繫結](../../../../docs/framework/wcf/extending/custom-bindings.md)