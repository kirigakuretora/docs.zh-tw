---
title: "SQL XML 資料行值 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d97ce4da-f09c-4d1e-85b7-a0ccedd7246a
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# SQL XML 資料行值
[!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 支援 `xml` 資料類型，開發人員可以使用 <xref:System.Data.SqlClient.SqlCommand> 類別的標準行為擷取包含此類型的結果集。  如同擷取任意資料行一樣，您可以擷取 `xml` 資料行 \(例如，擷取至 <xref:System.Data.SqlClient.SqlDataReader>\)，但是如果您要以 XML 的型式來使用資料行的內容，則必須使用 <xref:System.Xml.XmlReader>。  
  
## 範例  
 下列主控台應用程式會從 **AdventureWorks** 資料庫中的 **Sales.Store** 資料表，選取兩個資料列 \(每個資料列包含一個 `xml` 資料行\) 至 <xref:System.Data.SqlClient.SqlDataReader> 執行個體中。  針對每個資料列，可使用 <xref:System.Data.SqlClient.SqlDataReader> 的 <xref:System.Data.SqlClient.SqlDataReader.GetSqlXml%2A> 方法讀取 `xml` 資料行的值。  該值儲存在 <xref:System.Xml.XmlReader> 中。  請注意，如果您要將內容設為 <xref:System.Data.SqlTypes.SqlXml> 變數，則必須使用 <xref:System.Data.SqlClient.SqlDataReader.GetSqlXml%2A> 而不是 <xref:System.Data.IDataRecord.GetValue%2A> 方法；<xref:System.Data.IDataRecord.GetValue%2A> 會以字串的形式傳回 `xml` 的值。  
  
> [!NOTE]
>  當您安裝 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 時，預設不會安裝 **AdventureWorks** 範例資料庫。  您可以執行 [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] 安裝程式加以安裝。  
  
 [!code-csharp[DataWorks SqlClient.GetXmlDataReader#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.GetXmlDataReader/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.GetXmlDataReader#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.GetXmlDataReader/VB/source.vb#1)]  
  
## 請參閱  
 <xref:System.Data.SqlTypes.SqlXml>   
 [SQL Server 中的 XML 資料](../../../../../docs/framework/data/adonet/sql/xml-data-in-sql-server.md)   
 [ADO.NET Managed 提供者和資料集開發人員中心](http://go.microsoft.com/fwlink/?LinkId=217917)