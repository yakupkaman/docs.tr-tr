---
ms.openlocfilehash: 335647f899c79eff22e313fa40b2e2a73e7cfff0
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "66379592"
---
### <a name="wf-serializes-expressionsliteralt-datetimes-differently-now-breaks-custom-xaml-parsers"></a>WF serileştiren Expressions.Literal\<T > tarih/saat farklı artık (özel XAML ayrıştırıcıları sonu)

|   |   |
|---|---|
|Ayrıntılar|İlişkili <xref:System.Windows.Markup.ValueSerializer> nesnesi bir <xref:System.DateTime?displayProperty=name> veya <xref:System.DateTimeOffset?displayProperty=name> ikinci nesnesi ve <xref:System.DateTime.Millisecond?displayProperty=name> bileşenleri sıfır olmayan ve (için bir <xref:System.DateTime?displayProperty=name> değer), <xref:System.DateTime.Kind> özelliği için özellik öğesi belirtilmeyen değil bir dize yerine söz dizimi. Bu değişiklik sağlayan <xref:System.DateTime?displayProperty=name> ve <xref:System.DateTimeOffset?displayProperty=name> değerlerinin gidiş dönüşlü olmasına olanak. Nitelik söz dizimindeki giriş XAML'inin doğru çalışmayacağını varsayan özel XAML ayrıştırıcıları.|
|Öneri|Bu değişiklik sağlayan <xref:System.DateTime?displayProperty=name> ve <xref:System.DateTimeOffset?displayProperty=name> değerlerinin gidiş dönüşlü olmasına olanak. Nitelik söz dizimindeki giriş XAML'inin doğru çalışmayacağını varsayan özel XAML ayrıştırıcıları.|
|Kapsam|Kenar|
|Sürüm|4,5|
|Tür|Çalışma zamanı|
