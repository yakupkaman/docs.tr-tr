---
title: Genel Bakış
ms.date: 12/13/2019
description: Microsoft.Data.Sqlite'e genel bakış
ms.openlocfilehash: e84c68f0615f187e8dea7ab87ac917c0ad796a1c
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/15/2020
ms.locfileid: "77543605"
---
# <a name="microsoftdatasqlite-overview"></a>Microsoft.Data.Sqlite genel bakış

Microsoft.Data.Sqlite, SQLite için hafif [ADO.NET](../../../framework/data/adonet/index.md) sağlayıcısıdır. SQLite için [Entity Framework Core](/ef/core/) sağlayıcısı bu kitaplığın üzerine inşa edilmiştir. Ancak, bağımsız olarak veya diğer veri erişim kitaplıkları ile de kullanılabilir.

## <a name="installation"></a>Yükleme

En son kararlı sürümü [NuGet](https://www.nuget.org/packages/Microsoft.Data.Sqlite)mevcuttur.

### <a name="net-core-cli"></a>[.NET Core CLI](#tab/netcore-cli)

```dotnetcli
dotnet add package Microsoft.Data.Sqlite
```

### <a name="visual-studio"></a>[Visual Studio](#tab/visual-studio)

``` PowerShell
Install-Package Microsoft.Data.Sqlite
```

---

## <a name="usage"></a>Kullanım

Bu kitaplık, bağlantılar, komutlar, veri okuyucuları ve benzeri için ortak ADO.NET soyutlamaları uygular.

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/HelloWorldSample/Program.cs?name=snippet_HelloWorld)]

## <a name="see-also"></a>Ayrıca bkz.

* [Bağlantı dizeleri](connection-strings.md)
* [API Başvurusu](/dotnet/api/?view=msdata-sqlite-3.0)
* [SQL Söz Dizimi](https://www.sqlite.org/lang.html)
