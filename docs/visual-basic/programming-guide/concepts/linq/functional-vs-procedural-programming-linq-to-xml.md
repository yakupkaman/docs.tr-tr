---
title: İşlevsel ve yordamsal programlama (LINQ to XML)
ms.date: 07/20/2015
ms.assetid: ea1015a5-d4c8-4d79-8e1e-ba17a40a4f39
ms.openlocfilehash: 3d1e3cf01b30454d29836f176afcd39cb2b55b73
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74353410"
---
# <a name="functional-vs-procedural-programming-linq-to-xml-visual-basic"></a>İşlevsel ve yordamsal programlama (LINQ to XML) (Visual Basic)
Çeşitli türlerdeki XML uygulamaları vardır:  
  
- Bazı uygulamalar kaynak XML belgelerini alır ve kaynak belgelerden farklı bir şekilde yeni XML belgeleri oluşturur.  
  
- Bazı uygulamalar kaynak XML belgelerini alır ve sonuç belgelerini HTML veya CSV metin dosyaları gibi tamamen farklı bir biçimde oluşturur.  
  
- Bazı uygulamalar kaynak XML belgelerini alır ve bir veritabanına kayıt ekler.  
  
- Bazı uygulamalar, bir veritabanı gibi başka bir kaynaktan veri alır ve bundan XML belgesi oluşturur.  
  
 Bunlar, XML uygulaması türlerinin hepsi değildir, ancak bunlar bir XML Programlayıcısının uygulamak zorunda olduğu işlevsellik türlerinin temsili bir kümesidir.  
  
 Bu tür uygulamaların tümünde, bir geliştiricinin uygulayabileceğiniz iki yaklaşım vardır:  
  
- Bildirim temelli bir yaklaşım kullanılarak işlevsel oluşturma.  
  
- Yordamsal kodu kullanarak bellek içi XML ağacı değişikliği.  
  
 LINQ to XML her iki yaklaşımı destekler.  
  
 İşlevsel yaklaşımı kullanırken, kaynak belgeleri alan ve istenen şekle sahip tamamen yeni sonuç belgeleri oluşturan dönüşümler yazarsınız.  
  
 Bir XML ağacını yerinde değiştirirken, düğüm içi bir XML ağacındaki düğümlerde geçen ve gezinen, düğümleri ekleme, silme ve değiştirme gibi bir kod yazın.  
  
 LINQ to XML iki yaklaşımla de kullanabilirsiniz. Aynı sınıfları ve bazı durumlarda aynı yöntemleri kullanırsınız. Ancak, iki yaklaşımdan oluşan yapı ve hedefler çok farklıdır. Örneğin, farklı durumlarda, bir veya diğer yaklaşım genellikle daha iyi performansa sahip olur ve daha fazla veya daha az bellek kullanır. Buna ek olarak, bir veya başka bir yaklaşım daha fazla erişilebilir kod yazmak ve sağlamak daha kolay olacaktır.  
  
 Bu iki yaklaşımı görmek için bkz. [bellek ıçı XML ağacı değişikliği ve Işlevsel oluşturma (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/in-memory-xml-tree-modification-vs-functional-construction.md).  
  
 İşlev dönüştürmeleri yazma hakkında bir öğretici için bkz. [XML 'In saf Işlevsel dönüştürmeleri (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/pure-functional-transformations-of-xml.md).  
  
## <a name="see-also"></a>Ayrıca bkz.

- [LINQ to XML programlamaya genel bakış (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml-programming-overview.md)
