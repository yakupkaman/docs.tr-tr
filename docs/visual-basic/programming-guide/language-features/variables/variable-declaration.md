---
title: Değişken Bildirimi
ms.date: 07/20/2015
helpviewer_keywords:
- variables [Visual Basic], declaring
- member variables [Visual Basic], declarations
- Dim statement [Visual Basic], variable declaration
- declaring variables [Visual Basic]
- variables [Visual Basic], scope
- variables [Visual Basic], data types
- data types [Visual Basic], variable declarations
- lifetime [Visual Basic], variables
- variables [Visual Basic], lifetime
- access levels [Visual Basic], variables
- scope [Visual Basic], declaration statements
- variables [Visual Basic], access level
- local variables [Visual Basic], declarations
- scope [Visual Basic], variables
ms.assetid: d8f10226-92b1-480f-9f53-df377b2d7e15
ms.openlocfilehash: b89773e9527af0d65cde53b61654f2511f5c8dde
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74351760"
---
# <a name="variable-declaration-in-visual-basic"></a>Visual Basic'de Değişken Bildirimi
Adını ve özelliklerini belirtmek için bir değişken bildirirsiniz. Değişkenler için bildirim bildirimi, [Dim deyimidir](../../../../visual-basic/language-reference/statements/dim-statement.md). Konumu ve içeriği, değişkenin özelliklerini tespit.  
  
 Değişken adlandırma kuralları ve konuları için bkz. [bildirilmemiş öğe adları](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).  
  
## <a name="declaration-levels"></a>Bildirim düzeyleri  
  
### <a name="local-and-member-variables"></a>Yerel ve üye değişkenleri  
 *Yerel değişken* , bir yordam içinde belirtilen biridir. *Üye değişkeni* , Visual Basic türünün bir üyesidir; modül düzeyinde, bir sınıf, yapı veya modül içinde, ancak bu sınıf, yapı veya modülle iç yordam içinde değil, modül düzeyinde bildirilmiştir.  
  
### <a name="shared-and-instance-variables"></a>Paylaşılan ve örnek değişkenleri  
 Bir sınıf veya yapıda, bir üye değişkeninin kategorisi paylaşılıp paylaşıldığına bağlıdır. [Paylaşılan](../../../../visual-basic/language-reference/modifiers/shared.md) anahtar sözcüğü ile bildirilirse, *paylaşılan bir değişkendir*ve sınıf veya yapının tüm örnekleri arasında paylaşılan tek bir kopyada bulunur.  
  
 Aksi takdirde, bir *örnek değişkenidir*ve sınıfın ya da yapının her örneği için ayrı bir kopyası oluşturulur. Örnek değişkeninin belirli bir kopyası yalnızca oluşturulduğu sınıf veya yapının örneği için kullanılabilir. Sınıf veya yapının diğer örneğindeki örnek değişkeninin bir kopyasından bağımsızdır.  
  
## <a name="declaring-data-type"></a>Veri türü bildirme  
 Bildirim deyimindeki [as](../../../../visual-basic/language-reference/statements/as-clause.md) yan tümcesi, bildirdiğiniz değişkenin veri türünü veya nesne türünü tanımlamanızı sağlar. Bir değişken için aşağıdaki türlerden herhangi birini belirtebilirsiniz:  
  
- `Boolean`, `Long`veya `Decimal` gibi bir Öğesel veri türü  
  
- Dizi veya yapı gibi bir bileşik veri türü  
  
- Uygulamanızda ya da başka bir uygulamada tanımlanan bir nesne türü veya sınıf  
  
- <xref:System.Windows.Forms.Label> veya <xref:System.Windows.Forms.TextBox> gibi bir .NET Framework sınıfı  
  
- <xref:System.IComparable> veya <xref:System.IDisposable> gibi bir arabirim türü  
  
 Veri türünü yinelemek zorunda kalmadan, tek bir bildirimde birkaç değişken bildirebilirsiniz. Aşağıdaki deyimlerde `i`, `j`ve `k` değişkenleri tür `Integer`, `l` ve `m` `Long`olarak, `x` ve `y` `Single`olarak bildirilmiştir:  
  
```vb  
Dim i, j, k As Integer  
' All three variables in the preceding statement are declared as Integer.  
Dim l, m As Long, x, y As Single  
' In the preceding statement, l and m are Long, x and y are Single.  
```  
  
 Veri türleri hakkında daha fazla bilgi için bkz. [veri türleri](../../../../visual-basic/programming-guide/language-features/data-types/index.md). Nesneler hakkında daha fazla bilgi için bkz. [nesneler ve sınıflar](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md) ve [bileşenlerle programlama](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/0ffkdtkf(v=vs.120)).  
  
## <a name="local-type-inference"></a>Yerel Tür Arabirimi  
 *Tür çıkarımı* , `As` yan tümcesi olmadan belirtilen yerel değişkenlerin veri türlerini belirlemekte kullanılır. Derleyici, değişkenin türünü başlatma ifadesinin türünden algılar. Bu, açıkça bir tür belirtmeden değişkenleri bildirmenize olanak sağlar. Aşağıdaki örnekte, hem `num1` hem de `num2` kesin olarak tam sayı olarak türdedir.  
  
 [!code-vb[VbVbalrTypeInference#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrTypeInference/VB/Class1.vb#1)]  
  
 Yerel tür çıkarımı kullanmak istiyorsanız, `Option Infer` `On`olarak ayarlanmalıdır. Daha fazla bilgi için bkz. [Yerel tür çıkarımı](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md) ve [Option Infer deyimleri](../../../../visual-basic/language-reference/statements/option-infer-statement.md).  
  
## <a name="characteristics-of-declared-variables"></a>Belirtilen değişkenlerin özellikleri  
 Bir değişkenin kullanım *ömrü* , kullanım için kullanılabilir olduğu süredir. Genel olarak, bir değişken, kendisini bildiren öğe (bir yordam veya sınıf gibi) var olmaya devam ettiği sürece vardır. Değişkenin, kapsayan öğesinin yaşam süresinden daha fazla devam etmesi gerekmiyorsa, bildirimde özel bir şey yapmanız gerekmez. Değişkenin, kapsayan öğesinden daha uzun bir süre içinde var olmaya devam etmesi gerekiyorsa, `Dim` ifadesine `Static` veya `Shared` anahtar sözcüğünü dahil edebilirsiniz. Daha fazla bilgi için [Visual Basic ömrü](../../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md)' ne bakın.  
  
 Bir değişkenin *kapsamı* , adını nitelemeden kendisine başvurabilen tüm kod kümesidir. Bir değişkenin kapsamı, bildirildiği yere göre belirlenir. Belirli bir bölgede bulunan kod, adlarını nitelemek zorunda kalmadan bu bölgede tanımlanan değişkenleri kullanabilir. Daha fazla bilgi için [Visual Basic kapsam](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)bölümüne bakın.  
  
 Bir değişkenin *erişim düzeyi* , erişim izni olan kodun kapsamı olur. Bu, `Dim` bildiriminde kullandığınız erişim değiştiricisine ( [genel](../../../../visual-basic/language-reference/modifiers/public.md) veya [özel](../../../../visual-basic/language-reference/modifiers/private.md)) göre belirlenir. Daha fazla bilgi için bkz. [Visual Basic erişim düzeyleri](../../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Nasıl yapılır: Yeni Değişken Oluşturma](../../../../visual-basic/programming-guide/language-features/variables/how-to-create-a-new-variable.md)
- [Nasıl yapılır: Bir Değişkende Veri Ekleme Çıkarma](../../../../visual-basic/programming-guide/language-features/variables/how-to-move-data-into-and-out-of-a-variable.md)
- [Veri Türleri](../../../../visual-basic/language-reference/data-types/index.md)
- [Protected](../../../../visual-basic/language-reference/modifiers/protected.md)
- [Friend](../../../../visual-basic/language-reference/modifiers/friend.md)
- [Static](../../../../visual-basic/language-reference/modifiers/static.md)
- [Bildirilen Öğe Özellikleri](../../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-characteristics.md)
- [Yerel Çıkarım](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)
- [Option Infer Deyimi](../../../../visual-basic/language-reference/statements/option-infer-statement.md)
