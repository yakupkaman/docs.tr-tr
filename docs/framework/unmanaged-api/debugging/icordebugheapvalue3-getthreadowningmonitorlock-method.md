---
title: ICorDebugHeapValue3::GetThreadOwningMonitorLock Metodu
ms.date: 03/30/2017
api_name:
- ICorDebugHeapValue3.GetThreadOwningMonitorLock
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugHeapValue3::GetThreadOwningMonitorLock
helpviewer_keywords:
- GetThreadOwningMonitorLock method [.NET Framework debugging]
- ICorDebugHeapValue3::GetThreadOwningMonitorLock method [.NET Framework debugging]
ms.assetid: e06fc19d-2cf4-4cad-81a3-137a68af8969
topic_type:
- apiref
ms.openlocfilehash: 8be7c0e32f6183deb354d8b3936ef55c2520fe9f
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/28/2020
ms.locfileid: "76788618"
---
# <a name="icordebugheapvalue3getthreadowningmonitorlock-method"></a>ICorDebugHeapValue3::GetThreadOwningMonitorLock Metodu
Bu nesne üzerinde izleyici kilidine sahip yönetilen iş parçacığını döndürür.  
  
## <a name="syntax"></a>Sözdizimi  
  
```cpp  
HRESULT GetThreadOwningMonitorLock (  
    [out] ICorDebugThread   **ppThread,  
    [out] DWORD              *pAcquisitionCount  
);  
```  
  
## <a name="parameters"></a>Parametreler  
 `ppThread`  
 dışı Bu nesne üzerindeki izleyici kilidine sahip yönetilen iş parçacığı.  
  
 `pAcquisitionCount`  
 dışı Bu iş parçacığının, sahip olunmadan önce kilidi serbest bırakmak zorunda olduğu zaman sayısı.  
  
## <a name="return-value"></a>Dönüş Değeri  
 Bu yöntem, aşağıdaki belirli Hsonuçların yanı sıra Yöntem hatasını belirten HRESULT hataları döndürür.  
  
|HRESULT|Açıklama|  
|-------------|-----------------|  
|S_OK|Yöntem başarıyla tamamlandı.|  
|S_FALSE|Bu nesnede izleyici kilidine sahip yönetilen iş parçacığı yok.|  
  
## <a name="exceptions"></a>Özel Durumlar  
  
## <a name="remarks"></a>Açıklamalar  
 Yönetilen bir iş parçacığının bu nesne üzerindeki izleyici kilidine sahip olması durumunda:  
  
- Yöntemi S_OK döndürür.  
  
- İş parçacığı nesnesi, iş parçacığı çıkış yapılıncaya kadar geçerlidir.  
  
 Bu nesnede izleyici kilidine sahip yönetilen bir iş parçacığı yoksa, `ppThread` ve `pAcquisitionCount` değiştirilmez ve Yöntem S_FALSE döndürür.  
  
 `ppThread` veya `pAcquisitionCount` geçerli bir işaretçi değilse, sonuç tanımsızdır.  
  
 Bir hata oluşursa, eğer varsa, iş parçacığı bu nesnede izleyici kilidine sahipse, yöntem hata belirten bir HRESULT döndürür.  
  
## <a name="requirements"></a>Gereksinimler  
 **Platformlar:** Bkz. [sistem gereksinimleri](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Üst bilgi:** CorDebug. IDL, CorDebug. h  
  
 **Kitaplık:** Corguid. lib  
  
 **.NET Framework sürümleri:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Hata Ayıklama Arabirimleri](debugging-interfaces.md)
- [Hata Ayıklama](index.md)
