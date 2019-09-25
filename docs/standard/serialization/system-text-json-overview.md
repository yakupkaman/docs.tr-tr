---
title: .NET 'te JSON serileştirme
author: tdykstra
ms.author: tdykstra
ms.date: 09/16/2019
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.assetid: 4d1111c0-9447-4231-a997-96a2b74b3453
ms.openlocfilehash: 6cb45fded220b6123dbf4461f5f1cf1c3556ff69
ms.sourcegitcommit: a2d0e1f66367367065bc8dc0dde488ab536da73f
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/18/2019
ms.locfileid: "71083089"
---
# <a name="json-serialization-in-net"></a>.NET 'te JSON serileştirme

Ad `System.Text.Json` alanı, JavaScript nesne gösterimi (JSON) öğesine ve öğesinden serileştirmek için işlevsellik sağlar.

Kitaplık tasarımı, kapsamlı bir özellik kümesi üzerinden yüksek performans ve düşük bellek ayırmayı vurgular. Yerleşik UTF-8 desteği, UTF-8 olarak kodlanmış JSON metnini okuma ve yazma sürecini en iyi duruma getirir. Bu, Web ve disk üzerindeki dosyalardaki veriler için en yaygın kodlama olur.

Kitaplık Ayrıca, bellek içi belge nesne modeli (DOM) ile çalışmak için sınıflar sağlar. Bu özellik bir JSON dosyası veya dizesindeki öğelerin rastgele salt okunurdur erişimine izin vermez. 

## <a name="how-to-get-the-library"></a>Kitaplığı alma

* Kitaplığı, [.NET Core 3,0](https://aka.ms/netcore3download) paylaşılan çerçevesinin bir parçası olarak yerleşik olarak bulunur.
* Diğer hedef çerçeveler için [System. Text. JSON](https://www.nuget.org/packages/System.Text.Json) NuGet paketini yükler. Paket şunları destekler:
  * .NET Standard 2,0 ve sonraki sürümler
  * .NET Framework 4,61 ve sonraki sürümler
  * .NET Core 2,0 ve sonraki sürümleri

## <a name="additional-resources"></a>Ek kaynaklar

* [Kitaplığı kullanma](system-text-json-how-to.md)
* [Kaynak kodu](https://github.com/dotnet/corefx/tree/master/src/System.Text.Json)
* [API başvurusu](xref:System.Text.Json)
* [Yol Haritası](https://github.com/dotnet/corefx/blob/master/src/System.Text.Json/roadmap/README.md)
* DotNet/corefx deposundaki GitHub sorunları
  * [System. Text. JSON geliştirmesi hakkında tartışma](https://github.com/dotnet/corefx/issues/33115)
  * [Tüm System. Text. JSON sorunları](https://github.com/dotnet/corefx/issues?q=is%3Aopen+is%3Aissue+label%3Aarea-System.Text.Json)
  * [JSON işlevi etiketli System. Text. JSON sorunları-doc](https://github.com/dotnet/corefx/labels/json-functionality-doc)