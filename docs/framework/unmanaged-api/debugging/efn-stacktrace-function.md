---
title: _EFN_StackTrace İşlevi
ms.date: 03/30/2017
api_name:
- _EFN_StackTrace
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- _EFN_StackTrace
helpviewer_keywords:
- _EFN_StackTrace function [.NET Framework debugging]
ms.assetid: caea7754-867c-4360-a65c-5ced4408fd9d
topic_type:
- apiref
ms.openlocfilehash: cc5093a5ba0afcccaf960e9b8776f93a061cc2f5
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/28/2020
ms.locfileid: "76785674"
---
# <a name="_efn_stacktrace-function"></a>\_EFN\_StackTrace Işlevi
Yönetilmeyen ve yönetilen kod arasındaki her geçiş için bir yönetilen yığın izlemenin ve bir dizi `CONTEXT` kaydın metin gösterimini sağlar.  
  
## <a name="syntax"></a>Sözdizimi  
  
```cpp  
HRESULT CALLBACK _EFN_StackTrace(  
    [in]  PDEBUG_CLIENT  Client,  
    [out] WCHAR          wszTextOut[],  
    [out] size_t         *puiTextLength,  
    [out] LPVOID         pTransitionContexts,  
    [out] size_t         *puiTransitionContextCount,  
    [in]  size_t         uiSizeOfContext,  
    [in]  DWORD          Flags  
);  
```  
  
## <a name="parameters"></a>Parametreler  
 `Client`  
 'ndaki Hata ayıklamakta olan istemci.  
  
 `wszTextOut`  
 dışı Yığın izlemenin metin temsili.  
  
 `puiTextLength`  
 dışı `wszTextOut`karakter sayısına yönelik bir işaretçi.  
  
 `pTransitionContexts`  
 dışı Geçiş bağlamlarının dizisi.  
  
 `puiTransitionContextCount`  
 dışı Dizideki geçiş bağlamlarının sayısına yönelik bir işaretçi.  
  
 `uiSizeOfContext`  
 'ndaki Bağlam yapısının boyutu.  
  
 `Flags`  
 'ndaki EBP kaydını ve her bir `module!functionname` satırının önünde yığın işaretçisini (ESP) göstermek için 0 veya SOS_STACKTRACE_SHOWADDRESSES (0x01) olarak ayarlayın.  
  
## <a name="remarks"></a>Açıklamalar  
 `_EFN_StackTrace` yapısı bir WinDbg programlı arabiriminden çağrılabilir. Parametreleri aşağıdaki gibi kullanılır:  
  
- `wszTextOut` null ise ve `puiTextLength` null değilse, işlev `puiTextLength`dize uzunluğunu döndürür.  
  
- `wszTextOut` null değilse, işlev, `puiTextLength`tarafından belirtilen konuma kadar `wszTextOut` metni depolar. Arabellekte yeterli yer varsa başarıyla geri döner veya arabellek yeterince uzunsa E_OUTOFMEMORY döndürür.  
  
- `pTransitionContexts` ve `puiTransitionContextCount` her ikisi de null ise işlevin geçiş bölümü yok sayılır. Bu durumda, işlev çağıranları yalnızca işlev adlarının metin çıktısı ile birlikte sunar.  
  
- `pTransitionContexts` null ise ve `puiTransitionContextCount` null değilse, işlev `puiTransitionContextCount`gereken bağlam girişi sayısını döndürür.  
  
- `pTransitionContexts` null değilse, işlevi onu `puiTransitionContextCount`uzunluklu bir yapı dizisi olarak değerlendirir. Yapı boyutu `uiSizeOfContext`tarafından verilir ve bu mimari için [SimpleContext](stacktrace-simplecontext-structure.md) veya `CONTEXT` boyutu olmalıdır.  
  
- `wszTextOut` aşağıdaki biçimde yazılır:  
  
    ```output  
    "<ModuleName>!<Function Name>[+<offset in hex>]  
    ...  
    (TRANSITION)  
    ..."  
    ```  
  
- Onaltılı konum 0x0 ise, hiçbir fark yazılmaz.  
  
- Şu anda bağlamda olan iş parçacığında yönetilen kod yoksa, işlev SOS_E_NOMANAGEDCODE döndürür.  
  
- `Flags` parametresi, her bir `module!functionname` satırının önünde EBP ve ESP 'yi görmek için 0 ya da SOS_STACKTRACE_SHOWADDRESSES. Varsayılan olarak, 0 ' dır.  
  
    ```cpp  
    #define SOS_STACKTRACE_SHOWADDRESSES   0x00000001  
    ```  
  
## <a name="requirements"></a>Gereksinimler  
 **Platformlar:** Bkz. [sistem gereksinimleri](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Üst bilgi:** SOS_Stacktrace. h  
  
 **.NET Framework sürümleri:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Hata Ayıklama Genel Statik İşlevleri](debugging-global-static-functions.md)
