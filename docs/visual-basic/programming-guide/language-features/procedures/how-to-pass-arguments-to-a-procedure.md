---
title: 'Nasıl yapılır: Bir Yordama Bağımsız Değişkenler Geçirme'
ms.date: 07/20/2015
helpviewer_keywords:
- arguments [Visual Basic], passing to procedures
- procedures [Visual Basic], arguments
- procedures [Visual Basic], parameters
- procedure arguments
- Visual Basic code, procedures
- procedure parameters
- procedures [Visual Basic], calling
- argument passing [Visual Basic], procedures
ms.assetid: 08723588-3890-4ddc-8249-79e049e0f241
ms.openlocfilehash: 0267eed7c145988d61de715fd661bd4906d8d57d
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74344838"
---
# <a name="how-to-pass-arguments-to-a-procedure-visual-basic"></a>Nasıl yapılır: Bir Yordama Bağımsız Değişkenler Geçirme (Visual Basic)
Bir yordamı çağırdığınızda, yordam adını parantez içindeki bir bağımsız değişken listesiyle takip edersiniz. Yordamın tanımladığı her gerekli parametreye karşılık gelen bir bağımsız değişken sağlarsınız ve isteğe bağlı olarak `Optional` parametrelere bağımsız değişkenler sağlayabilirsiniz. Çağrıda bir `Optional` parametresi belirtmezseniz, sonraki bağımsız değişkenleri sağlarsanız, bağımsız değişken listesindeki yerini işaretlemek için bir virgül dahil etmeniz gerekir.  
  
 `String``Byte` gibi, karşılık gelen parametreden farklı bir veri türü bağımsız değişkenini geçirmek istiyorsanız, tür denetimi anahtarını ([Option Strict deyiminizi](../../../../visual-basic/language-reference/statements/option-strict-statement.md)) `Off`olarak ayarlayabilirsiniz. `Option Strict` `On`ise, genişleyen dönüşümler ya da açık dönüştürme anahtar sözcükleri kullanmanız gerekir. Daha fazla bilgi için bkz. [genişletme ve daraltma dönüştürmeleri](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md) ve [tür dönüştürme işlevleri](../../../../visual-basic/language-reference/functions/type-conversion-functions.md).  
  
 Daha fazla bilgi için bkz. [yordam parametreleri ve bağımsız değişkenleri](./procedure-parameters-and-arguments.md).  
  
### <a name="to-pass-one-or-more-arguments-to-a-procedure"></a>Bir yordama bir veya daha fazla bağımsız değişken geçirmek için  
  
1. Çağırma ifadesinde, parantez ile yordam adını izleyin.  
  
2. Parantez içinde bir bağımsız değişken listesi koyun. Yordamın tanımladığı her bir gerekli parametre için bir bağımsız değişken ekleyin ve bağımsız değişkenleri virgülle ayırın.  
  
3. Her bağımsız değişkenin, karşılık gelen parametre için, yordamın tanımladığı türe dönüştürülebilir bir veri türünü değerlendiren geçerli bir ifade olduğundan emin olun.  
  
4. Bir parametre [Isteğe bağlı](../../../../visual-basic/language-reference/modifiers/optional.md)olarak tanımlanmışsa bağımsız değişken listesine dahil edebilir veya atlayabilirsiniz. Bunu atlarsanız yordam, bu parametre için tanımlanan varsayılan değeri kullanır.  
  
5. Bir `Optional` parametresi için bir bağımsız değişkeni atlarsanız ve parametre listesinde bundan sonra başka bir parametre varsa, atlanan bağımsız değişkenin yerini bağımsız değişken listesinde fazladan bir virgül ile işaretleyebilirsiniz.  
  
     Aşağıdaki örnek Visual Basic <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A> işlevini çağırır.  
  
     [!code-vb[VbVbcnProcedures#34](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#34)]  
  
     Önceki örnek, görüntülenecek ileti dizesi olan gerekli ilk bağımsız değişkeni sağlar. İleti kutusunda görüntülenecek düğmeleri belirten isteğe bağlı ikinci parametre için bir bağımsız değişkeni atlar. Çağrı bir değer sağlamadığı için `MsgBox` varsayılan değer olan `MsgBoxStyle.OKOnly`kullanır ve yalnızca bir **Tamam** düğmesi görüntüler.  
  
     Bağımsız değişken listesindeki ikinci virgül, atlanan ikinci bağımsız değişkenin yerini işaret ediyor ve son dize, başlık çubuğunda görüntülenecek metin olan `MsgBox`isteğe bağlı üçüncü parametreye geçirilir.  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Alt Yordamlar](./sub-procedures.md)
- [İşlev Yordamları](./function-procedures.md)
- [Özellik Yordamları](./property-procedures.md)
- [İşleç Yordamları](./operator-procedures.md)
- [Nasıl yapılır: Bir Yordamın Parametresini Tanımlama](./how-to-define-a-parameter-for-a-procedure.md)
- [Bağımsız Değişkenleri Değere ve Başvuruya Göre Geçirme](./passing-arguments-by-value-and-by-reference.md)
- [Özyinelemeli Yordamlar](./recursive-procedures.md)
- [Yordam Aşırı Yüklemesi](./procedure-overloading.md)
- [Nesneler ve Sınıflar](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)
- [Nesne odaklı programlama (Visual Basic)](../../concepts/object-oriented-programming.md)
