---
title: "XSLT 參數 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: fe60aaa0-ae43-4b1c-9be1-426af66ba757
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# XSLT 參數
XSLT 參數可使用 <xref:System.Xml.Xsl.XsltArgumentList.AddParam%2A> 方法加入至 <xref:System.Xml.Xsl.XsltArgumentList>。  限定名稱與命名空間 URI 會在此時與參數物件產生關聯。  
  
### 使用 XSLT 參數  
  
1.  建立 <xref:System.Xml.Xsl.XsltArgumentList> 物件，並使用 <xref:System.Xml.Xsl.XsltArgumentList.AddParam%2A> 方法加入參數。  
  
2.  從樣式表呼叫參數。  
  
3.  將 <xref:System.Xml.Xsl.XsltArgumentList> 物件傳遞至 <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> 方法。  
  
## 參數型別  
 參數物件應對應至 W3C 型別。  下表顯示對應的 W3C 型別、對等的 Microsoft .NET 類別 \(型別\)，以及 W3C 型別是 XPath 型別還是 XSLT 型別。  
  
|W3C 類型|對等的 .NET 類別 \(型別\)|XPath 或 XSLT 型別|  
|------------|------------------------|---------------------|  
|`String`|<xref:System.String?displayProperty=fullName>|XPath|  
|`Boolean`|<xref:System.Boolean?displayProperty=fullName>|XPath|  
|`Number`|<xref:System.Double?displayProperty=fullName>|XPath|  
|`Result Tree Fragment`|<xref:System.Xml.XPath.XPathNavigator?displayProperty=fullName>|XSLT|  
|`Node*`|<xref:System.Xml.XPath.XPathNavigator?displayProperty=fullName>|XPath|  
|`Node Set`|<xref:System.Xml.XPath.XPathNodeIterator><br /><br /> **XPathNavigator\[\]**|XPath|  
  
 \*這相當於含有單一節點的節點集。  
  
 如果參數物件不是上述其中一個類別，則會根據下列規則進行轉換。  Common Language Runtime \(CLR\) 數字型別會轉換為 <xref:System.Double>。  <xref:System.DateTime> 類型會轉換為 <xref:System.String>。  <xref:System.Xml.XPath.IXPathNavigable> 類型會轉換為 <xref:System.Xml.XPath.XPathNavigator>。  **XPathNavigator\[\]** 會轉換為 <xref:System.Xml.XPath.XPathNodeIterator>。  
  
 所有其他類型都會擲回錯誤。  
  
## 範例  
 下列範例將使用 <xref:System.Xml.Xsl.XsltArgumentList.AddParam%2A> 方法，建立保留計算折扣日期的參數。  折扣日期計算為從訂購日期起的 20 天。  
  
 [!code-csharp[XSLT_Param#1](../../../../samples/snippets/csharp/VS_Snippets_Data/XSLT_Param/CS/xsltparam.cs#1)]
 [!code-vb[XSLT_Param#1](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XSLT_Param/VB/xsltparam.vb#1)]  
  
### 輸入  
  
##### order.xml  
 [!code-xml[XSLT_Param#2](../../../../samples/snippets/xml/VS_Snippets_Data/XSLT_Param/XML/order.xml#2)]  
  
##### discount.xsl  
 [!code-xml[XSLT_Param#3](../../../../samples/snippets/xml/VS_Snippets_Data/XSLT_Param/XML/discount.xsl#3)]  
  
### 輸出  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<order>  
  <total>36.9</total>  
     15% discount if paid by: 2/4/2004 12:00:00 AM  
</order>  
```  
  
## 請參閱  
 [XSLT 轉換](../../../../docs/standard/data/xml/xslt-transformations.md)