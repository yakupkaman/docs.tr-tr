---
title: ComboBox Stilleri ve Şablonları
ms.date: 03/30/2017
helpviewer_keywords:
- ComboBox [WPF], styles and templates
- states [WPF], ComboBox
- ControlTemplate [WPF], ComboBox
- styles [WPF], ComboBox
- templates [WPF], ComboBox
- parts [WPF], ComboBox
ms.assetid: b0662fa1-16d7-4320-b26b-c1804e565a44
ms.openlocfilehash: 887698bdaebf7bc5ddac8997167589d9fbd3dd4d
ms.sourcegitcommit: 42ed59871db1f29a32b3d8e7abeb20e6eceeda7c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/10/2019
ms.locfileid: "74960368"
---
# <a name="combobox-styles-and-templates"></a>ComboBox Stilleri ve Şablonları
Bu konuda <xref:System.Windows.Controls.ComboBox> denetimine yönelik stiller ve şablonlar açıklanmaktadır. Denetime benzersiz bir görünüm sağlamak için varsayılan <xref:System.Windows.Controls.ControlTemplate> değiştirebilirsiniz. Daha fazla bilgi için bkz. [Denetim için şablon oluşturma](../../../desktop-wpf/themes/how-to-create-apply-template.md).  
  
## <a name="combobox-parts"></a>ComboBox bölümleri  
 Aşağıdaki tabloda <xref:System.Windows.Controls.ComboBox> denetimi için adlandırılmış bölümler listelenmektedir.  
  
|Bölüm|Tür|Açıklama|  
|-|-|-|  
|PART_EditableTextBox|<xref:System.Windows.Controls.TextBox>|<xref:System.Windows.Controls.ComboBox>metnini içerir.|  
|PART_Popup|<xref:System.Windows.Controls.Primitives.Popup>|Birleşik giriş kutusundaki öğeleri içeren açılır liste.|  
  
 Bir <xref:System.Windows.Controls.ComboBox>için <xref:System.Windows.Controls.ControlTemplate> oluşturduğunuzda, şablonunuz <xref:System.Windows.Controls.ScrollViewer>içinde bir <xref:System.Windows.Controls.ItemsPresenter> içerebilir. (<xref:System.Windows.Controls.ItemsPresenter>, <xref:System.Windows.Controls.ComboBox>her öğeyi görüntüler; <xref:System.Windows.Controls.ScrollViewer> denetimin içinde kaydırmaya izin vermez).  <xref:System.Windows.Controls.ItemsPresenter>, <xref:System.Windows.Controls.ScrollViewer>doğrudan alt öğesi değilse, `ItemsPresenter`adına <xref:System.Windows.Controls.ItemsPresenter> vermelisiniz.  
  
## <a name="combobox-states"></a>ComboBox durumları  
 Aşağıdaki tabloda <xref:System.Windows.Controls.ComboBox> denetimine yönelik durumlar listelenmektedir.  
  
|VisualState adı|VisualStateGroup adı|Açıklama|  
|-|-|-|  
|Normal|Ortak durumlar|Varsayılan durum.|  
|Devre dışı|Ortak durumlar|Denetim devre dışı bırakıldı.|  
|Gelme olayından|Ortak durumlar|Fare işaretçisi <xref:System.Windows.Controls.ComboBox> denetimin üzerinde.|  
|Odaklı|Odaklardaki durumlar|Denetim odağa sahiptir.|  
|Odaklanmadan gözetle|Odaklardaki durumlar|Denetimin odağı yok.|  
|FocusedDropDown|Odaklardaki durumlar|<xref:System.Windows.Controls.ComboBox> için açılan liste odağa sahiptir.|  
|Geçerli|Doğrulama durumları|Denetim, <xref:System.Windows.Controls.Validation> sınıfını ve <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> iliştirilmiş özelliği `false`kullanır.|  
|Invalidodaklanmış|Doğrulama durumları|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> ekli özelliği, denetimin odağa sahip `true`.|  
|Invalidunodaklanmış|Doğrulama durumları|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> ekli özelliği, denetimin odağa sahip `true`.|  
|Yapılamaz|EditStates|<xref:System.Windows.Controls.ComboBox.IsEditable%2A> özelliği `true`.|  
|Düzenlenemez|EditStates|<xref:System.Windows.Controls.ComboBox.IsEditable%2A> özelliği `false`.|  
  
## <a name="comboboxitem-parts"></a>ComboBoxItem parçaları  
 <xref:System.Windows.Controls.ComboBoxItem> denetiminde hiç adlandırılmış bölüm yok.  
  
## <a name="comboboxitem-states"></a>ComboBoxItem durumları  
 Aşağıdaki tabloda <xref:System.Windows.Controls.ComboBoxItem> denetimine yönelik durumlar listelenmektedir.  
  
|VisualState adı|VisualStateGroup adı|Açıklama|  
|-|-|-|  
|Normal|Ortak durumlar|Varsayılan durum.|  
|Devre dışı|Ortak durumlar|Denetim devre dışı bırakıldı.|  
|Gelme olayından|Ortak durumlar|Fare işaretçisi <xref:System.Windows.Controls.ComboBoxItem> denetimin üzerinde.|  
|Odaklı|Odaklardaki durumlar|Denetim odağa sahiptir.|  
|Odaklanmadan gözetle|Odaklardaki durumlar|Denetimin odağı yok.|  
|Seçildi|SelectionStates|Öğe şu anda seçili durumda.|  
|Değilken|SelectionStates|Öğe seçilmemiş.|  
|Selectedunodaklanmış|SelectionStates|Öğe seçilir, ancak odağa sahip değildir.|  
|Geçerli|Doğrulama durumları|Denetim, <xref:System.Windows.Controls.Validation> sınıfını ve <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> iliştirilmiş özelliği `false`kullanır.|  
|Invalidodaklanmış|Doğrulama durumları|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> ekli özelliği, denetimin odağa sahip `true`.|  
|Invalidunodaklanmış|Doğrulama durumları|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> ekli özelliği, denetimin odağa sahip `true`.|  
  
## <a name="combobox-controltemplate-example"></a>ComboBox ControlTemplate örneği  
 Aşağıdaki örnek, <xref:System.Windows.Controls.ComboBox> denetimi ve ilişkili türler için <xref:System.Windows.Controls.ControlTemplate> nasıl tanımlanacağını gösterir.  
  
 [!code-xaml[ControlTemplateExamples#ComboBox](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/combobox.xaml#combobox)]  
  
 Yukarıdaki örnekte aşağıdaki kaynaklardan biri veya daha fazlası kullanılmaktadır.  
  
 [!code-xaml[ControlTemplateExamples#Resources](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/shared.xaml#resources)]  
  
 Tüm örnek için bkz. [ControlTemplates Ile stillendirme örneği](https://github.com/Microsoft/WPF-Samples/tree/master/Styles%20&%20Templates/IntroToStylingAndTemplating).  
  
## <a name="see-also"></a>Ayrıca bkz.

- <xref:System.Windows.FrameworkElement.Style%2A>
- <xref:System.Windows.Controls.ControlTemplate>
- [Denetim Stilleri ve Şablonları](control-styles-and-templates.md)
- [Denetim Özelleştirme](control-customization.md)
- [Stil ve Şablon Oluşturma](../../../desktop-wpf/fundamentals/styles-templates-overview.md)
- [Denetim için şablon oluşturma](../../../desktop-wpf/themes/how-to-create-apply-template.md)
