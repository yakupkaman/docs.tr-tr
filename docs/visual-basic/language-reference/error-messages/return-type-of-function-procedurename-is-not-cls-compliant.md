---
title: "'<procedurename>' işlevinin dönüş türü CLS uyumlu değil"
ms.date: 07/20/2015
f1_keywords:
- bc40027
- vbc40027
helpviewer_keywords:
- BC40027
ms.assetid: 33c088c7-48e7-400c-920e-6d8967e1f3fc
ms.openlocfilehash: 881726ea2cfb23493d85097635adb15608ed741d
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65642251"
---
# <a name="return-type-of-function-procedurename-is-not-cls-compliant"></a>İşlevinin dönüş türü '\<procedurename >' CLS uyumlu değil
A `Function` yordam olarak işaretlenmiş `<CLSCompliant(True)>` ancak olarak işaretlenmiş bir tür döndüren `<CLSCompliant(False)>`işaret konulmadıysa veya uyumlu olmayan bir tür olduğu için uygun değil.  
  
 İle uyumlu olması için bir yordam için [dil bağımsızlığı ve dilden bağımsız bileşenler](../../../standard/language-independence-and-language-independent-components.md) (CLS), yalnızca CLS uyumlu türler kullanmalıdır. Bu parametre türleri, dönüş türü ve tüm yerel değişkenlerin türleri için geçerlidir.  
  
 Aşağıdaki Visual Basic veri türleri CLS uyumlu değildir:  
  
- [SByte Veri Türü](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)  
  
- [UInteger Veri Türü](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)  
  
- [ULong Veri Türü](../../../visual-basic/language-reference/data-types/ulong-data-type.md)  
  
- [UShort Veri Türü](../../../visual-basic/language-reference/data-types/ushort-data-type.md)  
  
 Uyguladığınızda <xref:System.CLSCompliantAttribute> bir programlama öğesine özniteliğin ayarladığınız `isCompliant` ya da parametre `True` veya `False` uyumluluk veya uyumsuzluk belirtmek için. Bu parametre için varsayılan yok ve bir değer sağlamanız gerekir.  
  
 Geçerli <xref:System.CLSCompliantAttribute> bir öğe için uyumsuz olarak değerlendirilir.  
  
 Varsayılan olarak, bu iletiyi bir uyarıdır. Uyarıları gizleme veya uyarıları hata olarak değerlendirmesini hakkında daha fazla bilgi için bkz: [Visual Basic'teki uyarıları yapılandırma](/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **Hata Kimliği:** BC40027  
  
## <a name="to-correct-this-error"></a>Bu hatayı düzeltmek için  
  
- Varsa `Function` yordamı bu türdeki döndürür, Kaldır <xref:System.CLSCompliantAttribute>. Yordamı, CLS uyumlu olamaz.  
  
- Varsa `Function` yordamı CLS uyumlu olmalıdır, dönüş türünü değiştirmek için en yakın CLS uyumlu türü. Örneğin, içinde yerine, `UInteger` kullanmanız mümkün olabilir `Integer` 2.147.483.647 yukarıda değer aralığı gerekmiyorsa. Genişletilmiş aralık gerekiyorsa, değiştirebileceğiniz `UInteger` ile `Long`.  
  
- Otomasyon ve COM nesneleri ile arabirim, .NET Framework'teki bazı türleri değerinden farklı veri genişliği olduğunu aklınızda bulundurun. Örneğin, `int` 16 bit diğer ortamlarda genellikle olur. Böyle bir bileşene bir 16 bitlik tamsayı döndüren, olarak bildirin `Short` yerine `Integer` Yönetilen Visual Basic kodunuzda.
