---
ms.openlocfilehash: a5b3e325c13d2f56532ebc6ebb5c259d565a4952
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "66379559"
---
### <a name="xmlschemaexception-now-sets-line-positions-properly"></a>XmlSchemaException artık satır konumlarını düzgün ayarlar

|   |   |
|---|---|
|Ayrıntılar|Varsa <xref:System.Xml.Linq.LoadOptions.SetLineInfo> yük yönteme geçirilen değer ve bir doğrulama hatası oluşursa, <xref:System.Xml.Schema.XmlSchemaException.LineNumber> ve <xref:System.Xml.Schema.XmlSchemaException.LinePosition> özellikleri satır bilgileri içerir.|
|Öneri|Varsayar özel durum işleme kodları <xref:System.Xml.Schema.XmlSchemaException.LineNumber> ve <xref:System.Xml.Schema.XmlSchemaException.LinePosition> değişmeyecek SetLineInfo XML yüklenirken kullanıldığında bu özellikler artık düzgün şekilde ayarlanır bu yana kümesi güncelleştirilmelidir.|
|Kapsam|Kenar|
|Sürüm|4,5|
|Tür|Çalışma zamanı|
|Etkilenen API’ler|<ul><li><xref:System.Xml.Linq.LoadOptions.SetLineInfo?displayProperty=nameWithType></li></ul>|
