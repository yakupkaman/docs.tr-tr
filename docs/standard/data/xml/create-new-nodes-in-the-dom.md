---
title: DOM’da Yeni Düğümler Oluşturma
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 6c2b9789-b61a-49f9-b33f-db01a945edf2
ms.openlocfilehash: f48990286405baee347becef87d0511cd42e9e77
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/07/2020
ms.locfileid: "75711005"
---
# <a name="create-new-nodes-in-the-dom"></a>DOM’da Yeni Düğümler Oluşturma
<xref:System.Xml.XmlDocument> tüm düğüm türleri için Create yöntemi vardır. Gerektiğinde bir ada sahip bir ad ve içerik veya diğer parametre (örneğin, bir metin düğümü) ve düğüm oluşturulur. Aşağıdaki yöntemler, uygun bir düğüm oluşturmak için bir ada ve diğer birkaç parametreye sahip olması gereken değerlerdir.  
  
- <xref:System.Xml.XmlDocument.CreateCDataSection%2A>  
  
- <xref:System.Xml.XmlDocument.CreateComment%2A>  
  
- <xref:System.Xml.XmlDocument.CreateDocumentFragment%2A>  
  
- <xref:System.Xml.XmlDocument.CreateDocumentType%2A>  
  
- <xref:System.Xml.XmlDocument.CreateElement%2A>  
  
- <xref:System.Xml.XmlDocument.CreateNode%2A>  
  
- <xref:System.Xml.XmlDocument.CreateProcessingInstruction%2A>  
  
- <xref:System.Xml.XmlDocument.CreateSignificantWhitespace%2A>  
  
- <xref:System.Xml.XmlDocument.CreateTextNode%2A>  
  
- <xref:System.Xml.XmlDocument.CreateWhitespace%2A>  
  
- <xref:System.Xml.XmlDocument.CreateXmlDeclaration%2A>  
  
 Diğer düğüm türleri yalnızca parametrelere veri sağlamaktan daha fazla gereksinimlere sahiptir.  
  
 Öznitelikler hakkında bilgi için bkz. [Dom 'Daki öğeler Için yeni öznitelikler oluşturma](../../../../docs/standard/data/xml/creating-new-attributes-for-elements-in-the-dom.md). Öğe ve öznitelik adı doğrulama hakkında bilgi için, bkz. [yeni düğümler oluştururken XML öğesi ve öznitelik adı doğrulama](../../../../docs/standard/data/xml/xml-element-and-attribute-name-verification-when-creating-new-nodes.md). Varlık başvuruları oluşturmak için, bkz. [yeni varlık başvuruları oluşturma](../../../../docs/standard/data/xml/creating-new-entity-references.md). Ad alanlarının varlık başvurularını genişletmesinin nasıl etkilediği hakkında daha fazla bilgi için, bkz. [öğeleri ve öznitelikleri Içeren yeni düğümler Için varlık başvurusu genişletmesi üzerinde ad alanı etkileri](../../../../docs/standard/data/xml/namespace-affect-on-entity-ref-expansion-for-new-nodes.md).  
  
 Yeni düğümler oluşturulduktan sonra ağaca eklemek için kullanabileceğiniz çeşitli yöntemler vardır. Tabloda, yeni düğümün XML Belge Nesne Modeli (DOM) içinde göründüğü bir açıklama ile Yöntemler listelenmektedir.  
  
|Yöntem|Düğüm yerleşimi|  
|------------|--------------------|  
|<xref:System.Xml.XmlNode.InsertBefore%2A>|Başvuru düğümünden önce eklenirler. Örneğin, konum 5 ' te yeni düğümü eklemek için:<br /><br /> `Dim refChild As XmlNode = node.ChildNodes(4) 'The reference is zero-based.node.InsertBefore(newChild, refChild);`<br /><br /> `XmlNode refChild = node.ChildNodes[4]; //The reference is zero-based. node.InsertBefore(newChild, refChild);`<br /><br /> Daha fazla bilgi için bkz. <xref:System.Xml.XmlNode.InsertBefore%2A> yöntemi.|  
|<xref:System.Xml.XmlNode.InsertAfter%2A>|Başvuru düğümünden sonra eklenirler. Örneğin:<br /><br /> `node.InsertAfter(newChild, refChild)`<br /><br /> `node.InsertAfter(newChild, refChild);`<br /><br /> Daha fazla bilgi için bkz. <xref:System.Xml.XmlNode.InsertAfter%2A> yöntemi.|  
|<xref:System.Xml.XmlNode.AppendChild%2A>|Düğümü, verilen düğüm için alt düğümler listesinin sonuna ekler. Eklenmekte olan düğüm bir <xref:System.Xml.XmlDocumentFragment>, belge parçasının tüm içeriği bu düğümün alt listesine taşınır. Daha fazla bilgi için bkz. <xref:System.Xml.XmlNode.AppendChild%2A> yöntemi.|  
|<xref:System.Xml.XmlNode.PrependChild%2A>|Düğümü, belirtilen düğümün alt düğümleri listesinin başına ekler. Eklenmekte olan düğüm bir <xref:System.Xml.XmlDocumentFragment>, belge parçasının tüm içeriği bu düğümün alt listesine taşınır. Daha fazla bilgi için bkz. <xref:System.Xml.XmlNode.PrependChild%2A> yöntemi.|  
|<xref:System.Xml.XmlAttributeCollection.Append%2A>|Bir öğe ile ilişkili öznitelik koleksiyonunun sonuna bir <xref:System.Xml.XmlAttribute> düğümü ekler. Daha fazla bilgi için bkz. <xref:System.Xml.XmlAttributeCollection.Append%2A> yöntemi.|  
  
## <a name="see-also"></a>Ayrıca bkz.

- [XML Belge Nesne Modeli (DOM)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
