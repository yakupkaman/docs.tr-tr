---
title: -doc
ms.date: 03/10/2018
helpviewer_keywords:
- doc compiler option [Visual Basic]
- -doc compiler option [Visual Basic]
- /doc compiler option [Visual Basic]
ms.assetid: 5fc32ec9-a149-4648-994c-a8d0cccd0a65
ms.openlocfilehash: a818fd46bd93682f0bede1d22b8cbc2ca6467a40
ms.sourcegitcommit: 5f236cd78cf09593c8945a7d753e0850e96a0b80
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/07/2020
ms.locfileid: "75716735"
---
# <a name="-doc"></a>-doc
Belge açıklamalarını bir XML dosyasına işler.  
  
## <a name="syntax"></a>Sözdizimi  
  
```console  
-doc[+ | -]  
```

veya  

```console
-doc:file  
```  
  
## <a name="arguments"></a>Arguments  
  
|Terim|Tanım|  
|---|---|  
|`+` &#124; `-`|İsteğe bağlı. \+ Veya yalnızca `-doc`belirtme, derleyicinin belge bilgilerini oluşturmasını ve bir XML dosyasına yerleştirmesini sağlar. `-` belirtmek, `-doc`Belirtmemeye, hiçbir belge bilgisinin oluşturumamasına neden olan eşdeğerdir.|  
|`file`|`-doc:` kullanılıyorsa gereklidir. Derlemenin kaynak kodu dosyalarındaki yorumlarla doldurulan çıkış XML dosyasını belirtir. Dosya adı bir boşluk içeriyorsa, adı tırnak işaretleri ("") içine alın.|  
  
## <a name="remarks"></a>Açıklamalar  
 `-doc` seçeneği, derleyicinin belge açıklamalarını içeren bir XML dosyası oluşturup oluşturmayacağını denetler. `-doc:file` sözdizimini kullanırsanız `file` parametresi, XML dosyasının adını belirtir. `-doc` veya `-doc+`kullanırsanız, derleyici XML dosya adını derleyicinin oluşturmakta olduğu yürütülebilir dosya veya kitaplıktan alır. `-doc-` kullanırsanız veya `-doc` seçeneğini belirtmezseniz, derleyici bir XML dosyası oluşturmaz.  
  
 Kaynak kodu dosyalarında, belge açıklamaları aşağıdaki tanımlardan önce olabilir:  
  
- Bir [sınıf](../../../visual-basic/language-reference/statements/class-statement.md) veya [arabirim](../../../visual-basic/language-reference/statements/interface-statement.md) gibi Kullanıcı tanımlı türler  
  
- Alan, [olay](../../../visual-basic/language-reference/statements/event-statement.md), [özellik](../../../visual-basic/language-reference/statements/property-statement.md), [işlev](../../../visual-basic/language-reference/statements/function-statement.md)veya alt [yordam](../../../visual-basic/language-reference/statements/sub-statement.md)gibi Üyeler.  
  
 Oluşturulan XML dosyasını Visual Studio [IntelliSense](/visualstudio/ide/using-intellisense) özelliğiyle birlikte kullanmak IÇIN, XML dosyasının dosya adının desteklemek istediğiniz derlemeyle aynı olmasına izin verin. XML dosyasının derlemeyle aynı dizinde olduğundan emin olun; böylece derlemeye Visual Studio projesinde başvuruluyorsa,. xml dosyası da bulunur. IntelliSense 'in bir proje içinde veya bir proje tarafından başvurulan projelerde kod için çalışması için XML belge dosyaları gerekli değildir.  
  
 `-target:module`ile derlemediğiniz takdirde, XML dosyası `<assembly></assembly>`Etiketler içerir. Bu Etiketler, derlemenin çıkış dosyası için derleme bildirimini içeren dosyanın adını belirtir.  
  
 Kodunuzda açıklamalardan belge oluşturma yolları için bkz. [XML açıklama etiketleri](../../../visual-basic/language-reference/xmldoc/index.md) .  
  
|Visual Studio tümleşik geliştirme ortamında belge ayarlamak için|  
|---|  
|1. **Çözüm Gezgini**bir proje seçili olmalıdır. **Proje** menüsünde **Özellikler**' e tıklayın. <br />2. **Derle** sekmesine tıklayın.<br />3. **XML belgesi oluştur dosyası** kutusunda değeri ayarlayın.|  
  
## <a name="example"></a>Örnek  
 Bkz. bir örnek için [kodunuzu XML Ile belgeleme](../../../visual-basic/programming-guide/program-structure/documenting-your-code-with-xml.md) .  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Visual Basic komut satırı derleyicisi](../../../visual-basic/reference/command-line-compiler/index.md)
- [XML ile Kodunuzu Belgeleme](../../../visual-basic/programming-guide/program-structure/documenting-your-code-with-xml.md)
