---
title: XML Dosyasını İşleme
ms.date: 07/20/2015
helpviewer_keywords:
- XML comments [Visual Basic], parsing [Visual Basic]
ms.assetid: 78a15cd0-7708-4e79-85d1-c154b7a14a8c
ms.openlocfilehash: 4230fd88b4b60c631135f5b7fb15f4b6272b5351
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74347296"
---
# <a name="processing-the-xml-file-visual-basic"></a>XML Dosyasını İşleme (Visual Basic)
Derleyici, kodunuzda belge oluşturmak için etiketlenmiş her yapı için bir KIMLIK dizesi oluşturur. (Kodunuzu etiketleme hakkında daha fazla bilgi için bkz. [XML açıklama etiketleri](../../../visual-basic/language-reference/xmldoc/index.md).) KIMLIK dizesi yapıyı benzersiz bir şekilde tanımlar. XML dosyasını işleyen programlar, karşılık gelen .NET Framework meta veri/yansıma öğesini tanımlamak için KIMLIK dizesini kullanabilir.  
  
 XML dosyası, kodunuzun hiyerarşik bir temsili değildir; her öğe için oluşturulmuş KIMLIĞI olan düz bir liste.  
  
 Derleyici, KIMLIK dizelerini oluşturduğunda aşağıdaki kuralları sunar:  
  
- Dizeye boşluk yerleştirilmez.  
  
- KIMLIK dizesinin ilk bölümü, tanımlanmakta olan üyenin türünü tanımlar, tek bir karakter ve iki nokta üst üste gelir. Aşağıdaki üye türleri kullanılır.  
  
|Karakter|Açıklama|  
|---|---|  
|N|ad alanı<br /><br /> Bir ad alanına belge açıklamaları ekleyemezsiniz, ancak bu kişilere, desteklenmiş olduğu durumlarda bu başvuruları yapabilirsiniz.|  
|T|yazın: `Class`, `Module`, `Interface`, `Structure`, `Enum`, `Delegate`|  
|F|Alan: `Dim`|  
|P|Özellik: `Property` (varsayılan özellikler dahil)|  
|M|Yöntem: `Sub`, `Function`, `Declare`, `Operator`|  
|E|olay: `Event`|  
|!|hata dizesi<br /><br /> Dizenin geri kalanı hata hakkında bilgi sağlar. Visual Basic Derleyicisi çözümlenemeyen bağlantılar için hata bilgileri oluşturur.|  
  
- `String` ikinci bölümü, ad alanının kökünden başlayarak öğenin tam nitelikli adıdır. Öğenin adı, kapsayan tür (ler) ve ad alanı noktalarla ayrılır. Öğenin adının kendisi noktalar içeriyorsa, bunlar sayı işaretiyle (#) değiştirilmiştir. Hiçbir öğenin doğrudan adında numara işareti olmadığı varsayılır. Örneğin, `String` oluşturucusunun tam adı `System.String.#ctor`olur.  
  
- Özellikler ve yöntemler için, yöntem için bağımsız değişkenler varsa, parantez içine alınmış bağımsız değişken listesi aşağıda verilmiştir. Bağımsız değişken yoksa, parantezler yok. Bağımsız değişkenler virgülle ayrılır. Her bağımsız değişkenin kodlaması, .NET Framework imzasında nasıl kodlandığını doğrudan izler.  
  
## <a name="example"></a>Örnek  
 Aşağıdaki kod, bir sınıfa ve üyelerine ait KIMLIK dizelerinin nasıl oluşturulduğunu gösterir.  
  
 [!code-vb[VbVbcnXmlDocComments#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnXmlDocComments/VB/Class1.vb#10)]  
  
## <a name="see-also"></a>Ayrıca bkz.

- [-doc](../../../visual-basic/reference/command-line-compiler/doc.md)
- [Nasıl yapılır: XML Belgesi Oluşturma](../../../visual-basic/programming-guide/program-structure/how-to-create-xml-documentation.md)
