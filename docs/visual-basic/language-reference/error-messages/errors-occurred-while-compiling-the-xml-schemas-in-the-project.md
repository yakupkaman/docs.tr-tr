---
title: Projedeki XML şemaları derlenirken hataları oluştu
ms.date: 07/20/2015
f1_keywords:
- bc36810
- vbc36810
helpviewer_keywords:
- BC36810
ms.assetid: 9323b5d2-ba14-4e49-91f1-9ad647162144
ms.openlocfilehash: 7c05c712bcbb0a61bb3121bb71a7823a1c29afb5
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64625580"
---
# <a name="errors-occurred-while-compiling-the-xml-schemas-in-the-project"></a>Projedeki XML şemaları derlenirken hataları oluştu
Projedeki XML şemaları derlenirken hataları oluştu. Bu nedenle, XML IntelliSense kullanılamıyor.  
  
 Projeye dahil bir XML şema tanımı (XSD) şemasında bir hata var. Proje için mevcut bir XSD şeması ile çakışıyor ayarlanan XSD şema (.xsd) dosyası eklediğinizde, bu hata oluşur.  
  
 **Hata Kimliği:** BC36810  
  
## <a name="to-correct-this-error"></a>Bu hatayı düzeltmek için  
  
- Uyarıyı çift tıklatın **hata listesine** penceresi. Visual Basic uyarısı kaynağı XSD dosyası konumu yönlendirilirsiniz. XSD şema hatasını düzeltin.  
  
- Gerekli tüm XSD şema (.xsd) dosyaları projeye dahil olduğundan emin olun. Tıklaymanız gerekebilir **tüm dosyaları göster** üzerinde **proje** , .xsd görmek için menü dosyaları **Çözüm Gezgini**. .Xsd dosyasını sağ tıklatın ve ardından **projeye dahil et** dosyası projenize eklenecek.  
  
- XML ve şema Sihirbazı kullanıyorsanız, aynı kaynaktan birden fazla kez şemaları Infer, bu hata oluşabilir. Bu durumda, projeden varolan XSD şema dosyalarını kaldırabilirsiniz ekleme yeni bir XML şema öğesi şablonuna ve projeniz için sonra XML şema Sihirbazı ile tüm geçerli XML kaynakları sağlayın.  
  
- XSD Şemanızda herhangi bir hata belirlenirse, ayrıntılı hata iletisi sağlamak için yeterli bilgi XML derleyici olmayabilir. .Xsd dosyaları için XML ad alanları, proje eşlemesinde Visual Studio'da ayarlamak için XML şeması için belirtilen XML ad alanlarını dahil olun, ayrıntılı hata bilgisini almak mümkün olabilir.  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Hata Listesi Penceresi](/visualstudio/ide/reference/error-list-window)
- [XML](../../../visual-basic/programming-guide/language-features/xml/index.md)
