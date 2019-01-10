---
title: SqlStreamChars.Seek (Int64, SeekOrigin) yöntemi (System.Data.SqlTypes)
author: douglaslMS
ms.author: douglasl
ms.date: 12/20/2018
ms.technology:
- dotnet-data
api_name:
- System.Data.SqlTypes.SqlStreamChars.Seek
api_location:
- System.Data.dll
api_type:
- Assembly
ms.openlocfilehash: aab3195ec0d300a7f001f98f2d646c85be939356
ms.sourcegitcommit: 4ac80713f6faa220e5a119d5165308a58f7ccdc8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54152187"
---
# <a name="sqlstreamcharsseekint64-seekorigin-method"></a>(Int64, SeekOrigin) SqlStreamChars.Seek yöntemi

Türetilen bir sınıfta geçersiz kılındığında, geçerli akış içinde konumunu ayarlar. Bu yöntemi içeren derlemenin SQLAccess.dll bir arkadaş ilişkisi vardır. Bu, SQL Server tarafından kullanıma yöneliktir. Diğer veritabanları için veritabanı tarafından sağlanan barındırma mekanizmasına kullanın.

```csharp
public abstract long Seek (long offset, System.IO.SeekOrigin origin);
```

## <a name="parameters"></a>Parametreler

`offset`\
Göreli bir bayt uzaklığı `origin`.

`origin`\
Yeni konumunu alınacağı başvuru noktası belirten numaralandırma değerlerinden biri.

## <a name="returns"></a>Döndürür

<xref:System.Int32>\
Geçerli akışındaki yeni konumu.

## <a name="remarks"></a>Açıklamalar

> [!WARNING]
> `SqlStreamChars.Seek` Yöntemi private olduğuna ve kodunuzda doğrudan kullanılmak üzere tasarlanmamıştır.
>
> Microsoft hiçbir koşulda, bir üretim uygulamasında bu alanı kullanımını desteklemez.

## <a name="requirements"></a>Gereksinimler

**Namespace:** <xref:System.Data.SqlTypes>

**Derleme:** System.Data (içinde System.Data.dll)

**.NET framework sürümleri:** 2.0 sürümünden itibaren kullanılabilir.