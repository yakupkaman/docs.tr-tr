---
title: dotnet aracı geri yükleme komutu
description: Dotnet aracı geri yükleme komutu makinenize geçerli dizinin kapsamı içinde olan .NET Core yerel araçlarını yükler.
ms.date: 02/14/2020
ms.openlocfilehash: cb46f70afb58e482b6aedfddfbf5f3a0c40674f4
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/14/2020
ms.locfileid: "79146443"
---
# <a name="dotnet-tool-restore"></a>dotnet tool restore

**Bu makale şu şekilde dir:** ✔️ .NET Core 3.0 SDK ve sonraki sürümler

## <a name="name"></a>Adı

`dotnet tool restore`- Makinenize geçerli dizinin kapsamı içinde olan .NET Core yerel araçlarını yükler.

## <a name="synopsis"></a>Özet

```dotnetcli
dotnet tool restore <PACKAGE_NAME>
    [--configfile] [--add-source] [tool-manifest]
    [--disable-parallel] [--ignore-failed-sources]
    [--no-cache] [-interactive] [-v|--verbosity]

dotnet tool restore <-h|--help>
```

## <a name="description"></a>Açıklama

Komut, `dotnet tool restore` geçerli dizinin kapsamı içinde olan araç bildirimi dosyasını bulur ve içinde listelenen araçları yükler. Bildirim dosyaları hakkında bilgi için [bkz.](global-tools.md#install-a-local-tool) [Invoke a local tool](global-tools.md#invoke-a-local-tool)

## <a name="arguments"></a>Bağımsız Değişkenler

- **`PACKAGE_NAME`**

Yüklemek için .NET Core aracını içeren NuGet paketinin adı/kimliği.

## <a name="options"></a>Seçenekler

- **`--configfile <FILE>`**

  NuGet yapılandırması (*nuget.config*) dosyasını kullanmak.

- **`--add-source <SOURCE>`**

  Yükleme sırasında kullanmak üzere ek bir NuGet paket kaynağı ekler.

- **`--tool-manifest <PATH>`**

  Bildirim dosyasına giden yol.

- **`--disable-parallel`**

  Birden çok projeyi paralel olarak geri getirmeyi önleyin.

- **`--ignore-failed-sources`**

  Paket kaynağı hatalarını uyarı olarak ele ala.

- **`--no-cache`**

  Paketleri ve http isteklerini önbelleğe almıyor.

- **`--interactive`**

  Komutun durmasına ve kullanıcı girişinin veya eylemini beklemesine izin verir (örneğin kimlik doğrulamasını tamamlamak için).

- **`-h|--help`**

  Komut için kısa bir yardım yazdırır.

- **`-v|--verbosity <LEVEL>`**

  Komutun ayrıntılı düzeyini ayarlar. İzin verilen `q[uiet]` `m[inimal]`değerler `n[ormal]` `d[etailed]`, `diag[nostic]`, , , ve .

## <a name="example"></a>Örnek

- **`dotnet tool restore`**

  Geçerli dizin için yerel araçları geri yükler.

## <a name="see-also"></a>Ayrıca bkz.

- [.NET Çekirdek araçları](global-tools.md)
- [Öğretici: .NET Core CLI'yi kullanarak bir .NET Core yerel aracı nı yükleyin ve kullanın](local-tools-how-to-use.md)
