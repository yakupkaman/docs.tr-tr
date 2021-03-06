---
title: 'Nasıl yapılır: bir XML ağacının şeklini dönüştürme'
ms.date: 07/20/2015
ms.assetid: 84b60854-48b2-452c-87f2-77d53e1d653a
ms.openlocfilehash: 67ffd5f50572c0deba75c664ffd0e12ecfabf730
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74332415"
---
# <a name="how-to-transform-the-shape-of-an-xml-tree-visual-basic"></a>Nasıl yapılır: bir XML ağacının şeklini dönüştürme (Visual Basic)
Bir XML belgesinin *şekli* öğe adlarına, öznitelik adlarına ve hiyerarşisinin özelliklerine başvurur.  
  
 Bazen bir XML belgesinin şeklini değiştirmeniz gerekir. Örneğin, var olan bir XML belgesini farklı öğe ve öznitelik adları gerektiren başka bir sisteme göndermeniz gerekebilir. Belgeyi, gereken şekilde silip yeniden adlandırarak, ancak işlevsel oluşturmayı kullanmak daha okunabilir ve sürdürülebilir kod ile sonuçlanır. İşlevsel oluşturma hakkında daha fazla bilgi için bkz. [Işlevsel oluşturma (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/functional-construction-linq-to-xml.md).  
  
 İlk örnek, XML belgesi organizasyonunu değiştirir. Karmaşık öğeleri ağaçtaki bir konumdan diğerine taşımıştır.  
  
 Bu konudaki ikinci örnek, kaynak belgeden farklı bir şekle sahip bir XML belgesi oluşturur. Öğe adlarının büyük küçük harflerini değiştirir, bazı öğeleri yeniden adlandırır ve dışarı dönüştürülen ağacın bazı öğelerini kaynak ağacından bırakır.  
  
## <a name="example"></a>Örnek  
 Aşağıdaki kod, ekli sorgu ifadeleri kullanarak bir XML dosyasının şeklini değiştirir.  
  
 Bu örnekteki kaynak XML belgesi, tüm müşterileri içeren `Root` öğesi altında bir `Customers` öğesi içerir. Ayrıca, tüm siparişleri içeren `Root` öğesi altında bir `Orders` öğesi içerir. Bu örnek, her müşteri için siparişlerin `Customer` öğesi içindeki bir `Orders` öğesinde bulunduğu yeni bir XML ağacı oluşturur. Özgün belge ayrıca `Order` öğesinde bir `CustomerID` öğesi içerir; Bu öğe, yeniden şekillendirilmiş belgeden kaldırılacak.  
  
 Bu örnek, şu XML belgesini kullanır: [örnek xml dosyası: müşteriler ve siparişler (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-customers-and-orders-linq-to-xml.md).  
  
```vb  
Dim co As XElement = XElement.Load("CustomersOrders.xml")  
Dim newCustOrd = _  
    <Root>  
        <%= From cust In co.<Customers>.<Customer> _  
            Select _  
            <Customer>  
                <%= cust.Attributes() %>  
                <%= cust.Elements() %>  
                <Orders>  
                    <%= From ord In co.<Orders>.<Order> _  
                        Where ord.<CustomerID>.Value = cust.@CustomerID _  
                        Select _  
                        <Order>  
                            <%= ord.Attributes() %>  
                            <%= ord.<EmployeeID> %>  
                            <%= ord.<OrderDate> %>  
                            <%= ord.<RequiredDate> %>  
                            <%= ord.<ShipInfo> %>  
                        </Order> _  
                    %>  
                </Orders>  
            </Customer> _  
        %>  
    </Root>  
Console.WriteLine(newCustOrd)  
```  
  
 Bu kod aşağıdaki çıktıyı üretir:  
  
```xml  
        <Root>  
<Customer CustomerID="GREAL">  
  <CompanyName>Great Lakes Food Market</CompanyName>  
  <ContactName>Howard Snyder</ContactName>  
  <ContactTitle>Marketing Manager</ContactTitle>  
  <Phone>(503) 555-7555</Phone>  
  <FullAddress>  
    <Address>2732 Baker Blvd.</Address>  
    <City>Eugene</City>  
    <Region>OR</Region>  
    <PostalCode>97403</PostalCode>  
    <Country>USA</Country>  
  </FullAddress>  
  <Orders />  
</Customer>  
<Customer CustomerID="HUNGC">  
  <CompanyName>Hungry Coyote Import Store</CompanyName>  
  <ContactName>Yoshi Latimer</ContactName>  
  <ContactTitle>Sales Representative</ContactTitle>  
  <Phone>(503) 555-6874</Phone>  
  <Fax>(503) 555-2376</Fax>  
  <FullAddress>  
    <Address>City Center Plaza 516 Main St.</Address>  
    <City>Elgin</City>  
    <Region>OR</Region>  
    <PostalCode>97827</PostalCode>  
    <Country>USA</Country>  
  </FullAddress>  
  <Orders />  
</Customer>  
. . .  
```  
  
## <a name="example"></a>Örnek  
 Bu örnek bazı öğeleri yeniden adlandırır ve bazı öznitelikleri öğelere dönüştürür.  
  
 Kod, <xref:System.Xml.Linq.XElement> nesnelerinin bir listesini döndüren `ConvertAddress`çağırır. Yöntemin bağımsız değişkeni, `Type` özniteliğinin `"Shipping"`değerine sahip olduğu `Address` karmaşık öğeyi belirleyen bir sorgudur.  
  
 Bu örnek, şu XML belgesini kullanır: [örnek xml dosyası: tipik satın alma siparişi (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-typical-purchase-order-linq-to-xml.md).  
  
```vb  
Function ConvertAddress(ByVal add As XElement) As IEnumerable(Of XElement)  
    Dim fragment = New List(Of XElement)  
    fragment.Add(<NAME><%= add.<Name>.Value %></NAME>)  
    fragment.Add(<STREET><%= add.<Street>.Value %></STREET>)  
    fragment.Add(<CITY><%= add.<City>.Value %></CITY>)  
    fragment.Add(<ST><%= add.<State>.Value %></ST>)  
    fragment.Add(<POSTALCODE><%= add.<Zip>.Value %></POSTALCODE>)  
    fragment.Add(<COUNTRY><%= add.<Country>.Value %></COUNTRY>)  
    Return fragment  
End Function  
  
Sub Main()  
    Dim po As XElement = XElement.Load("PurchaseOrder.xml")  
    Dim newPo As XElement = _  
        <PO>  
            <ID><%= po.@PurchaseOrderNumber %></ID>  
            <DATE><%= CDate(po.@OrderDate) %></DATE>  
            <%= _  
                ConvertAddress( _  
                (From el In po.<Address> _  
                Where el.@Type = "Shipping" _  
                Select el) _  
                .First() _  
                ) _  
            %>  
        </PO>  
    Console.WriteLine(newPo)  
End Sub  
```  
  
 Bu kod aşağıdaki çıktıyı üretir:  
  
```xml  
<PO>  
  <ID>99503</ID>  
  <DATE>1999-10-20T00:00:00</DATE>  
  <NAME>Ellen Adams</NAME>  
  <STREET>123 Maple Street</STREET>  
  <CITY>Mill Valley</CITY>  
  <ST>CA</ST>  
  <POSTALCODE>10999</POSTALCODE>  
  <COUNTRY>USA</COUNTRY>  
</PO>  
```  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Tahminler ve dönüşümler (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/projections-and-transformations-linq-to-xml.md)
