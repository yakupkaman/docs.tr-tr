---
ms.openlocfilehash: 923105114c9e8da02c61c842cc02bed1ead3eddc
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/15/2020
ms.locfileid: "67858935"
---
### <a name="tabcontrol-selectionchanged-event-and-selectedcontent-property"></a>SekmeSeçimiDeğiştirilen olay ve SelectedContent özelliği

|   |   |
|---|---|
|Ayrıntılar|.NET Framework 4.7.1 ile <xref:System.Windows.Controls.TabControl> başlayarak, seçimi <xref:System.Windows.Controls.TabControl.SelectedContent> değiştiğinde <xref:System.Windows.Controls.Primitives.Selector.SelectionChanged> olayı yükseltmeden önce özelliğinin değerini güncelleştirir. .NET Framework 4.7 ve önceki sürümlerinde, SelectedContent güncelleştirmesi olaydan sonra gerçekleşti.|
|Öneri|.NET Framework 4.7.1 veya sonraki leri hedefleyen uygulamalar bu değişikliği devre dışı bırakıp <code>&lt;runtime&gt;</code> uygulama yapılandırma dosyasının bölümüne aşağıdakileri ekleyerek eski davranışı kullanabilir:<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Controls.TabControl.SelectionPropertiesCanLagBehindSelectionChangedEvent=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>.NET Framework 4.7 veya daha öncesini hedefleyen ancak .NET Framework 4.7.1 veya sonraki bölümlerinde çalışan <code>&lt;runtime&gt;</code> uygulamalar, uygulama .configuration dosyasının bölümüne aşağıdaki satırı ekleyerek yeni davranışı etkinleştirebilir:<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Controls.TabControl.SelectionPropertiesCanLagBehindSelectionChangedEvent=false&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>|
|Kapsam|İkincil|
|Sürüm|4.7.1|
|Tür|Yeniden Hedefleme|
|Etkilenen API’ler|<ul><li><xref:System.Windows.Controls.TabControl.SelectedContent?displayProperty=nameWithType></li><li><xref:System.Windows.Controls.Primitives.Selector.SelectionChanged?displayProperty=nameWithType></li></ul>|
