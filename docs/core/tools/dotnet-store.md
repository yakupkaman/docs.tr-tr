---
title: dotnet mağaza komutu
description: "'dotnet mağazası' komutu belirtilen derlemeleri çalışma zamanı paket deposunda depolar."
ms.date: 02/14/2020
ms.openlocfilehash: da1d132b2b873ff55ec104b5bb092d0194889bdc
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/14/2020
ms.locfileid: "77503583"
---
# <a name="dotnet-store"></a>dotnet store

**Bu makale şu şekilde dir:** ✔️ .NET Core 2.x SDK ve sonraki sürümler

## <a name="name"></a>Adı

`dotnet store`- Belirtilen montajları [çalışma zamanı paket deposunda](../deploying/runtime-store.md)saklar.

## <a name="synopsis"></a>Özet

```dotnetcli
dotnet store -m|--manifest -f|--framework -r|--runtime  [--framework-version] [-h|--help] [--output] [--skip-optimization] [--skip-symbols] [-v|--verbosity] [--working-dir]
```

## <a name="description"></a>Açıklama

`dotnet store`belirtilen montajları çalışma [zamanı paket deposunda](../deploying/runtime-store.md)saklar. Varsayılan olarak, derlemeler hedef çalışma süresi ve çerçeve için en iyi duruma getirilir. Daha fazla bilgi için [çalışma zamanı paket deposu](../deploying/runtime-store.md) konusuna bakın.

## <a name="required-options"></a>Gerekli seçenekler

- **`-f|--framework <FRAMEWORK>`**

  [Hedef çerçeveyi](../../standard/frameworks.md)belirtir. Hedef çerçeve proje dosyasında belirtilmelidir.

- **`-m|--manifest <PATH_TO_MANIFEST_FILE>`**

  *Paket deposu bildirimi dosyası,* depoya çıkacak paketlerin listesini içeren bir XML dosyasıdır. Bildirim dosyasının biçimi SDK tarzı proje biçimiyle uyumludur. Bu nedenle, istenilen paketlere başvuran bir proje `-m|--manifest` dosyası, derlemeleri çalışma zamanı paket deposunda depolama seçeneğiyle birlikte kullanılabilir. Birden çok bildirim dosyası belirtmek için, her dosya için seçeneği ve yolu yineleyin. Örneğin: `--manifest packages1.csproj --manifest packages2.csproj`.

- **`-r|--runtime <RUNTIME_IDENTIFIER>`**

  Hedef için [çalışma zamanı tanımlayıcısı.](../rid-catalog.md)

## <a name="optional-options"></a>İsteğe bağlı seçenekler

- **`--framework-version <FRAMEWORK_VERSION>`**

  .NET Core SDK sürümünü belirtir. Bu seçenek, `-f|--framework` seçenek tarafından belirtilen çerçevenin ötesinde belirli bir çerçeve sürümü seçmenize olanak tanır.

- **`-h|--help`**

  Yardım bilgilerini gösterir.

- **`-o|--output <OUTPUT_DIRECTORY>`**

  Çalışma zamanı paket deposuna giden yolu belirtir. Belirtilmemişse, kullanıcı profili .NET Core yükleme dizininin *mağaza* alt dizini varsayılan olarak.

- **`--skip-optimization`**

  Optimizasyon aşamasını atlar.

- **`--skip-symbols`**

  Sembol neslini atlar. Şu anda yalnızca Windows ve Linux'ta semboller oluşturabilirsiniz.

- **`-v|--verbosity <LEVEL>`**

  Komutun ayrıntılı düzeyini ayarlar. İzin verilen `q[uiet]` `m[inimal]`değerler `n[ormal]` `d[etailed]`, `diag[nostic]`, , , ve .

- **`-w|--working-dir <WORKING_DIRECTORY>`**

  Komut tarafından kullanılan çalışma dizini. Belirtilmemişse, geçerli dizinin *obj* alt dizini kullanır.

## <a name="examples"></a>Örnekler

- .NET Core 2.0.0 için *packages.csproj* proje dosyasında belirtilen paketleri saklayın:

  ```dotnetcli
  dotnet store --manifest packages.csproj --framework-version 2.0.0
  ```

- *Paketlerde* belirtilen paketleri en iyi duruma kaynaklanmadan saklayın:

  ```dotnetcli
  dotnet store --manifest packages.csproj --skip-optimization
  ```

## <a name="see-also"></a>Ayrıca bkz.

- [Çalışma zamanı paket deposu](../deploying/runtime-store.md)
