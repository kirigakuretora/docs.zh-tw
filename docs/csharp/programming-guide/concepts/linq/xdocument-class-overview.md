---
title: "XDocument 類別概觀 (C#) | Microsoft Docs"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 63305603-ab54-49fc-84e4-f76eecc59549
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f3233a634e358ee227b0adbe30cb05d1efbf8fe0
ms.lasthandoff: 03/13/2017

---
# <a name="xdocument-class-overview-c"></a>XDocument 類別概觀 (C#)
本主題介紹 <xref:System.Xml.Linq.XDocument> 類別。  
  
## <a name="overview-of-the-xdocument-class"></a>XDocument 類別的概觀  
 <xref:System.Xml.Linq.XDocument> 類別包含有效 XML 文件所需的資訊。 這包括 XML 宣告、處理指示與註解。  
  
 請注意，如果您需要 <xref:System.Xml.Linq.XDocument> 類別所提供的特定功能，則僅需要建立 <xref:System.Xml.Linq.XDocument> 物件。 在許多情況下，您可以直接使用 <xref:System.Xml.Linq.XElement>。 直接使用 <xref:System.Xml.Linq.XElement> 是較簡單的程式設計模型。  
  
 <xref:System.Xml.Linq.XDocument> 衍生自 <xref:System.Xml.Linq.XContainer>。 因此，它可以包含子節點。 不過，<xref:System.Xml.Linq.XDocument> 物件只能有一個子 <xref:System.Xml.Linq.XElement> 節點。 這會反映 XML 標準，也就是說 XML 文件中只能有一個根項目 (Root Element)。  
  
## <a name="components-of-xdocument"></a>XDocument 的元件  
 <xref:System.Xml.Linq.XDocument> 可以包含下列項目：  
  
-   一個 <xref:System.Xml.Linq.XDeclaration> 物件。 <xref:System.Xml.Linq.XDeclaration> 可讓您指定 XML 宣告的關聯部分：XML 版本、文件的編碼，以及 XML 文件是否為獨立的。  
  
-   一個 <xref:System.Xml.Linq.XElement> 物件。 這是 XML 文件的根節點。  
  
-   任意數目的 <xref:System.Xml.Linq.XProcessingInstruction> 物件。 處理指示會將資訊傳達到處理 XML 的應用程式。  
  
-   任意數目的 <xref:System.Xml.Linq.XComment> 物件。 這些註解將是根項目的同層級。 <xref:System.Xml.Linq.XComment> 物件不得為清單中的第一個引數，因為 XML 文件的開頭不能是註解。  
  
-   DTD 的一個 <xref:System.Xml.Linq.XDocumentType>。  
  
 當您序列化 <xref:System.Xml.Linq.XDocument> 時，即使 `XDocument.Declaration` 為 `null`，如果寫入器已將 `Writer.Settings.OmitXmlDeclaration` 設定為 `false` (預設值)，則輸出還是會有 XML 宣告。  
  
 根據預設，[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 會將版本設定為 "1.0"，並將編碼設定為 "utf-8"。  
  
## <a name="using-xelement-without-xdocument"></a>在沒有 XDocument 的情況下使用 XElement  
 如先前所述，<xref:System.Xml.Linq.XElement> 類別是 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] 程式設計介面中的主要類別。 在許多情況下，您的應用程式將不需要您建立文件。 您可以使用 <xref:System.Xml.Linq.XElement> 類別來建立 XML 樹狀結構、在其中新增其他 XML 樹狀結構、修改 XML 樹狀結構，然後加以儲存。  
  
## <a name="using-xdocument"></a>使用 XDocument  
 若要建構 <xref:System.Xml.Linq.XDocument>，請使用功能結構，就像您建構 <xref:System.Xml.Linq.XElement> 物件時所執行的作業一樣。  
  
 下列程式碼會建立 <xref:System.Xml.Linq.XDocument> 物件和其相關聯的包含物件。  
  
```csharp  
XDocument d = new XDocument(  
    new XComment("This is a comment."),  
    new XProcessingInstruction("xml-stylesheet",  
        "href='mystyle.css' title='Compact' type='text/css'"),  
    new XElement("Pubs",  
        new XElement("Book",  
            new XElement("Title", "Artifacts of Roman Civilization"),  
            new XElement("Author", "Moreno, Jordao")  
        ),  
        new XElement("Book",  
            new XElement("Title", "Midieval Tools and Implements"),  
            new XElement("Author", "Gazit, Inbar")  
        )  
    ),  
    new XComment("This is another comment.")  
);  
d.Declaration = new XDeclaration("1.0", "utf-8", "true");  
Console.WriteLine(d);  
  
d.Save("test.xml");  
```  
  
 當您檢查 test.xml 檔案時，您會得到下列輸出：  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<!--This is a comment.-->  
<?xml-stylesheet href='mystyle.css' title='Compact' type='text/css'?>  
<Pubs>  
  <Book>  
    <Title>Artifacts of Roman Civilization</Title>  
    <Author>Moreno, Jordao</Author>  
  </Book>  
  <Book>  
    <Title>Midieval Tools and Implements</Title>  
    <Author>Gazit, Inbar</Author>  
  </Book>  
</Pubs>  
<!--This is another comment.-->  
```  
  
## <a name="see-also"></a>另請參閱  
 [LINQ to XML 程式設計概觀 (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-programming-overview.md)