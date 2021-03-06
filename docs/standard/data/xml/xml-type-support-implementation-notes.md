---
title: XML Tür Desteği Uygulama Notları
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 26b071f3-1261-47ef-8690-0717f5cd93c1
ms.openlocfilehash: 40ab0f746ef82ccd195fc6b873f5c8edb255f868
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/07/2020
ms.locfileid: "75709874"
---
# <a name="xml-type-support-implementation-notes"></a>XML Tür Desteği Uygulama Notları
Bu konuda, farkında olmak istediğiniz bazı uygulama ayrıntıları açıklanmaktadır.  
  
## <a name="list-mappings"></a>Eşlemeleri Listele  
 <xref:System.Collections.IList>, <xref:System.Collections.ICollection>, <xref:System.Collections.IEnumerable>, **türü []** ve <xref:System.String> türleri XML şeması tanım DILI (xsd) liste türlerini temsil etmek için kullanılır.  
  
## <a name="union-mappings"></a>Birleşim eşlemeleri  
 Birleşim türleri <xref:System.Xml.Schema.XmlAtomicValue> veya <xref:System.String> türü kullanılarak temsil edilir. Bu nedenle, kaynak türü veya hedef türü her zaman <xref:System.String> ya da <xref:System.Xml.Schema.XmlAtomicValue>olmalıdır.  
  
 <xref:System.Xml.Schema.XmlSchemaDatatype> nesnesi bir liste türünü temsil ediyorsa, nesne giriş dize değerini bir veya daha fazla nesne listesine dönüştürür. <xref:System.Xml.Schema.XmlSchemaDatatype> bir birleşim türünü temsil ediyorsa, giriş değerini birleşimin üye türü olarak ayrıştırmaya yönelik bir girişimde bulunuldu. Ayrıştırma denemesi başarısız olursa, dönüştürme işleminin bir sonraki üyesi ile denenir ve dönüştürme başarılı olana kadar ya da denenecek başka hiçbir üye türü yoksa, bu durumda bir özel durum oluşturulur.  
  
## <a name="differences-between-clr-and-xml-data-types"></a>CLR ve XML veri türleri arasındaki farklar  
 Aşağıda, CLR türleri ve XML veri türleri arasında oluşabilecek bazı uyuşmazlıklar ve bunların nasıl işlendiği açıklanmaktadır.  
  
> [!NOTE]
> `xs` ön eki <https://www.w3.org/2001/XMLSchema> ve ad alanı URI 'sine eşlenir.
  
### <a name="systemtimespan-and-xsduration"></a>System. TimeSpan ve xs: Duration  
 `xs:duration` türü, farklı ancak eşdeğer olan belirli Duration değerleri olacak şekilde kısmen sıralanır. Bu, 1 ay (P1M) gibi `xs:duration` türü değeri için 32 günden (P32D), 27 günden (P27D) daha büyük ve 28, 29 veya 30 güne eşit olduğu anlamına gelir.  
  
 <xref:System.TimeSpan> sınıfı bu kısmi sıralamayı desteklemiyor. Bunun yerine, 1 yıl ve 1 ay için belirli sayıda gün seçer; 365 gün ve 30 gün sırasıyla.  
  
 `xs:duration` türü hakkında daha fazla bilgi için bkz. W3C [XML şeması Bölüm 2: veri türleri önerisi](https://www.w3.org/TR/xmlschema-2/).
  
### <a name="xstime-gregorian-date-types-and-systemdatetime"></a>xs: Time, Gregoryen tarih türleri ve System. DateTime  
 Bir `xs:time` değeri bir <xref:System.DateTime> nesnesiyle eşlendiğinde <xref:System.DateTime.MinValue> alanı, <xref:System.DateTime> nesnesinin Tarih özelliklerini (<xref:System.DateTime.Year%2A>, <xref:System.DateTime.Month%2A>ve <xref:System.DateTime.Day%2A>gibi) olası en küçük <xref:System.DateTime> değere başlatmak için kullanılır.  
  
 Benzer şekilde, `xs:gMonth`, `xs:gDay`, `xs:gYear`, `xs:gYearMonth` ve `xs:gMonthDay` örnekleri de bir <xref:System.DateTime> nesnesine eşlenir. <xref:System.DateTime> nesnesi üzerinde kullanılmayan Özellikler <xref:System.DateTime.MinValue>için başlatılır.  
  
> [!NOTE]
> İçerik `xs:gMonthDay`olarak yazıldığında <xref:System.DateTime.Year%2A?displayProperty=nameWithType> değerine güvenebilirsiniz. <xref:System.DateTime.Year%2A?displayProperty=nameWithType> değeri her zaman bu durumda 1904 olarak ayarlanır.  
  
### <a name="xsanyuri-and-systemuri"></a>xs: anyURI ve System. Uri  
 Göreli bir URI 'yi temsil eden bir `xs:anyURI` örneği bir <xref:System.Uri>eşleştirildiği zaman <xref:System.Uri> nesnenin temel URI 'SI yoktur.  
  
## <a name="see-also"></a>Ayrıca bkz.

- [System.Xml Sınıflarında Tür Desteği](../../../../docs/standard/data/xml/type-support-in-the-system-xml-classes.md)
