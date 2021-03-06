---
title: Birleştirme İşleçleri
ms.date: 07/20/2015
helpviewer_keywords:
- '& operator [Visual Basic], concatenation'
- concatenation operators [Visual Basic]
- operators [Visual Basic], concatenation
- Visual Basic code, operators
- + operator [Visual Basic], concatenation
- concatenation operators [Visual Basic]
ms.assetid: e59908c3-89e0-41ae-933d-3e8826c16a04
ms.openlocfilehash: f86245c649647be4e040a61083d8b93eee4d7422
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74353682"
---
# <a name="concatenation-operators-in-visual-basic"></a>Visual Basic'de Birleştirme İşleçleri

Birleştirme işleçleri birden çok dizeyi tek bir dizeye birleştirir. `+` ve `&`iki birleştirme işleci vardır. Her ikisi de aşağıdaki örnekte gösterildiği gibi temel birleştirme işlemini çalıştırır.

```vb
Dim x As String = "Mic" & "ro" & "soft"
Dim y As String = "Mic" + "ro" + "soft"
' The preceding statements set both x and y to "Microsoft".
```

Bu işleçler Ayrıca, aşağıdaki örnekte gösterildiği gibi `String` değişkenlerini de birleştirebilir.

[!code-vb[VbVbalrOperators#76](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#76)]

## <a name="differences-between-the-two-concatenation-operators"></a>Iki birleştirme Işleci arasındaki farklar

[+ İşlecinin](../../../../visual-basic/language-reference/operators/addition-operator.md) iki sayı eklemenin birincil amacı vardır. Ancak, sayısal işlenenleri dize işlenenleri ile de birleştirebilir. `+` işleci, bir derleyici hatasına ekleme, birleştirme, sinyal sinyali atma veya bir çalışma zamanı <xref:System.InvalidCastException> özel durumu oluşturma gibi karmaşık bir kurallar kümesine sahiptir.

[& işleci](../../../../visual-basic/language-reference/operators/concatenation-operator.md) yalnızca `String` işlenenleri için tanımlanır ve `Option Strict`ayarından bağımsız olarak her zaman işlenenlerini `String`olarak widens. `&` işleci, dizeler için özel olarak tanımlandığından ve istenmeden dönüştürme oluşturma olasılığınızı azalttığından dize birleştirme için önerilir.

## <a name="performance-string-and-stringbuilder"></a>Performans: dize ve StringBuilder

Birleştirmeleri, silmeler ve değişiklikler gibi bir dizede önemli sayıda değişiklik yaparsanız, performans, <xref:System.Text> ad alanındaki <xref:System.Text.StringBuilder> sınıftan elde edebilir. <xref:System.Text.StringBuilder> nesne oluşturup başlatmaya yönelik ek bir yönerge ve son değerini bir `String`dönüştürmek için başka bir yönerge kullanır, ancak <xref:System.Text.StringBuilder> daha hızlı gerçekleştirebildiğinden bu süreyi kurtarabilirsiniz.

## <a name="see-also"></a>Ayrıca bkz.

- [Option Strict Deyimi](../../../../visual-basic/language-reference/statements/option-strict-statement.md)
- [Visual Basic içindeki dize düzenleme yöntemlerinin türleri](../../../../visual-basic/programming-guide/language-features/strings/types-of-string-manipulation-methods.md)
- [Visual Basic aritmetik Işleçler](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
- [Visual Basic karşılaştırma Işleçleri](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)
- [Visual Basic mantıksal ve bit düzeyinde Işleçler](../../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)
