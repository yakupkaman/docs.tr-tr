---
title: 'Nasıl yapılır: kök öğeyi bulma (XPath-LINQ to XML)'
ms.date: 07/20/2015
ms.assetid: 72c3aed5-9522-4454-a876-2070aad13f2e
ms.openlocfilehash: 0e381c074a935a0cda5bd74bc456b8d7d9a495a8
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74344609"
---
# <a name="how-to-find-the-root-element-xpath-linq-to-xml-visual-basic"></a>Nasıl yapılır: kök öğeyi bulma (XPath-LINQ to XML) (Visual Basic)
Bu konu, XPath ve [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]kök öğesinin nasıl alınacağını gösterir.  
  
 XPath ifadesi:  
  
 `/PurchaseOrders`  
  
## <a name="example"></a>Örnek  
 Bu örnek, kök öğesini bulur.  
  
 Bu örnek, şu XML belgesini kullanır: [örnek xml dosyası: birden fazla satın alma siparişi (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-multiple-purchase-orders-linq-to-xml.md).  
  
```vb  
Dim po As XDocument = XDocument.Load("PurchaseOrders.xml")  
  
' LINQ to XML query  
Dim el1 As XElement = po.Root  
  
' XPath expression  
Dim el2 As XElement = po.XPathSelectElement("/PurchaseOrders")  
  
If el1 Is el2 Then  
    Console.WriteLine("Results are identical")  
Else  
    Console.WriteLine("Results differ")  
End If  
Console.WriteLine(el1.Name)  
```  
  
 Bu örnek aşağıdaki çıktıyı üretir:  
  
```console  
Results are identical  
PurchaseOrders  
```  
  
## <a name="see-also"></a>Ayrıca bkz.

- [XPath kullanıcıları için LINQ to XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-for-xpath-users.md)
