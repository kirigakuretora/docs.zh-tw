---
title: "在 Visual Basic 中撰寫查詢 |Microsoft 文件"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: get-started-article
dev_langs:
- VB
helpviewer_keywords:
- queries [LINQ in Visual Basic], writing
- LINQ [Visual Basic], walkthroughs
- LINQ [Visual Basic], writing queries
- writing LINQ queries [Visual Basic]
ms.assetid: f0045808-b9fe-4d31-88d1-473d9957211e
caps.latest.revision: 70
author: stevehoag
ms.author: shoag
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e870d5d0640c68fa57b07986f2bf8268fd5246c9
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-writing-queries-in-visual-basic"></a>逐步解說：在 Visual Basic 中撰寫查詢
本逐步解說會示範如何使用 Visual Basic 語言功能，撰寫[!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext_md.md)]查詢運算式。 逐步解說將示範如何建立查詢清單中的學生物件、 如何執行查詢，以及如何修改它們。 查詢會將數個功能，包括物件初始設定式、 區域型別推斷和匿名型別。  
  
 完成本逐步解說之後, 您就可以移到特定的文件與範例[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]您感興趣的提供者。 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]提供者包括[!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq_md.md)]， [!INCLUDE[linq_dataset](../../../../csharp/programming-guide/concepts/linq/includes/linq_dataset_md.md)]，和[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]。  
  
## <a name="create-a-project"></a>建立專案  
  
#### <a name="to-create-a-console-application-project"></a>若要建立主控台應用程式專案  
  
1.  啟動 Visual Studio。  
  
2.  在 [檔案] **** 功能表中，指向 [新增] ****，然後按一下 [專案] ****。  
  
3.  在**已安裝的範本**清單中，按一下**Visual Basic**。  
  
4.  在專案類型清單中，按一下 **主控台應用程式**。 在**名稱**方塊內輸入專案的名稱，然後按一下 **確定**。  
  
     建立專案。 根據預設，它包含 system.core.dll 的參考。 此外，**匯入命名空間**清單[專案設計工具 (Visual Basic)、 參考頁](https://docs.microsoft.com/visualstudio/ide/reference/references-page-project-designer-visual-basic)包含<xref:System.Linq?displayProperty=fullName>命名空間。</xref:System.Linq?displayProperty=fullName>  
  
5.  在[編譯的頁面上，專案設計工具 (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/compile-page-project-designer-visual-basic)，請確認**Option infer**設為**上**。  
  
## <a name="add-an-in-memory-data-source"></a>將記憶體中的資料來源  
 在此逐步解說中查詢的資料來源是一份`Student`物件。 每個`Student`物件包含名字、 姓氏、 類別年和學術學生主體中的陣序規範。  
  
#### <a name="to-add-the-data-source"></a>若要新增資料來源  
  
-   定義`Student`類別，並建立一份類別的執行個體。  
  
    > [!IMPORTANT]
    >  定義所需的程式碼`Student`類別使用的清單，並在這個逐步解說中提供範例[How to︰ 建立項目的清單](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md)。 您可以從該處複製它，並將它貼到您的專案。 新的程式碼會取代您在建立專案時出現的程式碼。  
  
#### <a name="to-add-a-new-student-to-the-students-list"></a>若要新增新的學生學生清單  
  
-   請依照下列中的模式`getStudents`方法，加入另一個執行個體`Student`類別清單。 加入學生將為您介紹物件初始設定式。 如需詳細資訊，請參閱[物件初始設定式︰ 具名和匿名型別](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)。  
  
## <a name="create-a-query"></a>建立查詢  
 執行時，加入本節中的查詢會產生一份學術排名將它們放入前十名的學生。 因為此查詢會選取完整`Student`物件每次都查詢結果的型別是`IEnumerable(Of Student)`。 不過，查詢的型別通常未指定在查詢定義中。 相反地，編譯器會使用區域型別推斷來判斷型別。 如需詳細資訊，請參閱[本機的型別推斷](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)。 查詢的範圍變數， `currentStudent`，做為每個參考`Student`來源中的執行個體`students`，在每個物件的屬性來存取`students`。  
  
#### <a name="to-create-a-simple-query"></a>建立簡單查詢  
  
1.  尋找中`Main`方法之專案的標記，如下所示︰  
  
     [!code-vb[VbLINQWalkthrough #&1;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_1.vb)]  
  
     下列程式碼複製並貼上。  
  
     [!code-vb[VbLINQWalkthrough #&2;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_2.vb)]  
  
2.  將滑鼠指標停留`studentQuery`在您的程式碼，以驗證的編譯器指派型`IEnumerable(Of Student)`。  
  
## <a name="run-the-query"></a>執行查詢  
 變數`studentQuery`包含定義的查詢，而不執行查詢的結果。 執行查詢的一般機制是`For Each`迴圈。 傳回序列中的每個項目被經由迴圈反覆運算變數。 如需查詢執行的詳細資訊，請參閱[撰寫您的第一個 LINQ 查詢](../../../../visual-basic/programming-guide/concepts/linq/writing-your-first-linq-query.md)。  
  
#### <a name="to-run-the-query"></a>若要執行查詢  
  
1.  新增下列`For Each`迴圈低於您的專案中的查詢。  
  
     [!code-vb[VbLINQWalkthrough #&3;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_3.vb)]  
  
2.  將滑鼠指標停留在迴圈控制變數`studentRecord`以查看其資料型別。 型別`studentRecord`就會推斷`Student`，因為`studentQuery`傳回的集合`Student`執行個體。  
  
3.  建置並按下 CTRL + F5 執行應用程式。 請注意主控台視窗中的結果。  
  
## <a name="modify-the-query"></a>修改查詢  
 就很容易掃描查詢結果，如果它們是在指定的順序。 您可以排序傳回的序列，根據任何可用的欄位。  
  
#### <a name="to-order-the-results"></a>若要排序結果  
  
1.  新增下列`Order By`子句之間`Where`陳述式和`Select`查詢陳述式。 `Order By`子句會排序結果依字母順序從 A 到 Z，到最後一個根據每個學生的名稱。  
  
    ```  
    Order By currentStudent.Last Ascending   
    ```  
  
2.  若要排序姓氏和名字，這兩個欄位加入查詢︰  
  
    ```  
    Order By currentStudent.Last Ascending, currentStudent.First Ascending   
    ```  
  
     您也可以指定`Descending`順序從 Z 到 a。  
  
3.  建置並按下 CTRL + F5 執行應用程式。 請注意主控台視窗中的結果。  
  
#### <a name="to-introduce-a-local-identifier"></a>導入區域識別項  
  
1.  本節介紹區域識別項在查詢運算式中的加入程式碼。 區域識別項會保留中繼結果。 在下列範例中，`name`是識別項會保留串連名學生的名字和姓氏。 為了方便起見，可用的本機識別碼或它可以儲存結果的運算式，否則會計算多次，以提高效能。  
  
     [!code-vb[VbLINQWalkthrough #&4;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_4.vb)]  
  
2.  建置並按下 CTRL + F5 執行應用程式。 請注意主控台視窗中的結果。  
  
#### <a name="to-project-one-field-in-the-select-clause"></a>專案 Select 子句中的一個欄位  
  
1.  將查詢加入和`For Each`迴圈，從這個區段來建立查詢，以產生的序列，其項目會與不同來源中的項目。 在下列範例中，來源是一系列`Student`傳回物件，而每個物件只能有一個成員︰ 姓氏是 Garcia 學生的名字。 因為`currentStudent.First`為字串時，所傳回的序列的資料型別`studentQuery3`是`IEnumerable(Of String)`，字串序列。 如先前的範例所示輸入的資料指派`studentQuery3`使用區域型別推斷來判斷編譯器會保留。  
  
     [!code-vb[VbLINQWalkthrough #&5;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_5.vb)]  
  
2.  將滑鼠指標停留`studentQuery3`在您的程式碼，以確認是否已指派的型別`IEnumerable(Of String)`。  
  
3.  建置並按下 CTRL + F5 執行應用程式。 請注意主控台視窗中的結果。  
  
#### <a name="to-create-an-anonymous-type-in-the-select-clause"></a>在 Select 子句中建立匿名型別  
  
1.  加入此區段可查看如何匿名型別中的程式碼會在查詢中使用。 您它們在查詢中使用當您想要從資料來源，而不是完整記錄傳回多個欄位 (`currentStudent`先前範例中的記錄) 或單一欄位 (`First`前一節)。 而不是定義新的具名型別，其中包含您想要包含在結果中的欄位，您指定的欄位`Select`子句和編譯器會使用這些欄位做為其屬性建立匿名型別。 如需詳細資訊，請參閱[匿名型別](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)。  
  
     下列範例會建立查詢，傳回的名稱和前輩學術排名是介於 1 到 10 的學術排名順序的陣序規範。 在此範例中的型別`studentQuery4`必須推斷，因為`Select`子句會傳回匿名型別執行個體和匿名型別已經沒有可用的名稱。  
  
     [!code-vb[VbLINQWalkthrough #&6;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_6.vb)]  
  
2.  建置並按下 CTRL + F5 執行應用程式。 請注意主控台視窗中的結果。  
  
## <a name="additional-examples"></a>其他範例  
 現在您已了解基本概念，以下是列出其他範例來說明彈性和能力[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]查詢。 每個範例被前面有何用途的簡短描述。 將滑鼠指標停留在查詢結果變數的每個查詢來查看推斷的型別。 使用`For Each`迴圈，產生的結果。  
  
 [!code-vb[VbLINQWalkthrough #&7;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_7.vb)]  
  
## <a name="additional-information"></a>其他資訊  
 您已熟悉使用查詢的基本概念之後，您就準備好要讀取的特定類型的文件和範例[!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]您感興趣的提供者︰  
  
 [LINQ to Objects](http://msdn.microsoft.com/library/73cafe73-37cf-46e7-bfa7-97c7eea7ced9)  
  
 [LINQ to SQL](https://msdn.microsoft.com/library/bb386976)  
  
 [LINQ to XML](http://msdn.microsoft.com/library/f0fe21e9-ee43-4a55-b91a-0800e5782c13)  
  
 [LINQ to DataSet](http://msdn.microsoft.com/library/743e3755-3ecb-45a2-8d9b-9ed41f0dcf17)  
  
## <a name="see-also"></a>另請參閱  
 [語言整合查詢 (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/index.md)   
 [在 Visual Basic 中撰寫 LINQ 入門](../../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [區域型別推斷](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [物件初始設定式︰ 具名和匿名類型](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)   
 [匿名型別](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [在 Visual Basic 中的 LINQ 簡介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [查詢](../../../../visual-basic/language-reference/queries/queries.md)