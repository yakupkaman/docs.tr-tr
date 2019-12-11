---
ms.openlocfilehash: 3d0a90a57c2b1c2759b8420e74c284668d54e9cb
ms.sourcegitcommit: 79a2d6a07ba4ed08979819666a0ee6927bbf1b01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74644042"
---
### <a name="duplicated-apis-removed-from-windows-forms"></a>Yinelenen API 'Ler Windows Forms kaldırıldı

.NET Core 3,0 Preview 4 ' te başlayan <xref:System.Windows.Forms?displayProperty=fullName> ad alanında yanlışlıkla çoğaltılan bir dizi API 'Ler .NET Core 3,0 RC1 sürümünde kaldırılmıştır.

#### <a name="change-description"></a>Açıklamayı Değiştir

.NET Core 3,0 Preview 4 istenmeden yinelenen <xref:System.Windows.Forms?displayProperty=fullName> ad alanındaki <xref:System.ComponentModel.Design?displayProperty=fullName> ad alanında zaten bulunan bir dizi tür. .NET Core 3,0 RC1 ile başlayarak, bu yinelenen türler artık kullanılamaz. Aşağıdaki tabloda, özgün tür ve onun yinelenen türü listelenmektedir:

|Özgün tür|Yinelenen tür|
|---|---|
|<xref:System.ComponentModel.Design.DesignerActionListsChangedEventArgs?displayProperty=fullName>|`System.Windows.Forms.DesignerActionListsChangedEventArgs`|
|<xref:System.ComponentModel.Design.DesignerActionListsChangedEventHandler?displayProperty=fullName>|`System.Windows.Forms.DesignerActionListsChangedEventHandler`|
|<xref:System.ComponentModel.Design.DesignerActionListsChangedType?displayProperty=fullName>|`System.Windows.Forms.DesignerActionListsChangedType`|
|<xref:System.ComponentModel.Design.DesignerActionUIService?displayProperty=fullName>|`System.Windows.Forms.DesignerActionUIService`|
|<xref:System.ComponentModel.Design.DesignerCommandSet?displayProperty=fullName>|`System.Windows.Forms.DesignerCommandSet`|

#### <a name="version-introduced"></a>Sunulan sürüm

3,0 RC1

#### <a name="recommended-action"></a>Önerilen eylem

Kodu, tablonun **özgün tür** sütununda gösterildiği gibi özgün türe başvuracak şekilde güncelleştirin.

#### <a name="category"></a>Kategori

Windows Forms

#### <a name="affected-apis"></a>Etkilenen API’ler

- API analizi aracılığıyla algılanamaz.

<!--

### Affected APIs

- Not detectable via API analysis.

-->