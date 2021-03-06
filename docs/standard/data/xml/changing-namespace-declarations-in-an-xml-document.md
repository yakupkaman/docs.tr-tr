---
title: Bir XML Belgesindeki Ad Alanı Bildirimlerini Değiştirme
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: a2758f40-e497-4964-8d8d-1bb68af14dcd
ms.openlocfilehash: b8aa670764deb8e77cfb67fd16dbcf8b1cc9b4c0
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/07/2020
ms.locfileid: "75711135"
---
# <a name="changing-namespace-declarations-in-an-xml-document"></a>Bir XML Belgesindeki Ad Alanı Bildirimlerini Değiştirme
**XmlDocument** , belge nesne modelinin bir parçası olarak ad alanı bildirimlerini ve **xmlns** özniteliklerini gösterir. Bunlar **XmlDocument**içinde depolanır, böylece belgeyi kaydettiğinizde, bu özniteliklerin konumunu koruyabilir. Bu özniteliklerin değiştirilmesinin, ağaçta zaten bulunan diğer düğümlerin **adı**, **NamespaceURI**ve **önek** özellikleri üzerinde hiçbir etkisi yoktur. Örneğin, aşağıdaki belgeyi yüklerseniz `test` öğesi **namespaceUri 'sine** sahiptir `123.`  
  
```xml  
<test xmlns="123"/>  
```  
  
 `xmlns` özniteliğini aşağıdaki gibi kaldırırsanız, `test` öğesi hala `123`**NamespaceURI 'sine** sahiptir.  
  
```vb  
doc.documentElement.RemoveAttribute("xmlns")  
```  
  
```csharp  
doc.documentElement.RemoveAttribute("xmlns");  
```  
  
 Benzer şekilde, `doc` öğesine aşağıdaki şekilde farklı bir `xmlns` özniteliği eklerseniz, `test` öğesinde de **NamespaceURI** `123`vardır.  
  
```vb  
doc.documentElement.SetAttribute("xmlns","456")
```  
  
```csharp  
doc.documentElement.SetAttribute("xmlns","456");  
```  
  
 Bu nedenle, **XmlDocument** nesnesini kaydedip yeniden yükleyene kadar `xmlns` özniteliklerinin değiştirilmesinin hiçbir etkisi olmaz.  
  
## <a name="see-also"></a>Ayrıca bkz.

- [XML Belge Nesne Modeli (DOM)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
