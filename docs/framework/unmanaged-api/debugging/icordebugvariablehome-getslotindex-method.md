---
title: 'Icordebugvariablehome:: Getslotındex yöntemi'
ms.date: 03/30/2017
api_name:
- ICorDebugVariableHome.GetSlotIndex
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugVariableHome::GetSlotIndex
helpviewer_keywords:
- ICorDebugVariableHome::GetSlotIndex method [.NET Framework debugging]
- GetSlotIndex method, ICorDebugVariableHome interface [.NET Framework debugging]
ms.assetid: 966da50d-5665-4fff-bf7b-1c72bbadd9a4
topic_type:
- apiref
ms.openlocfilehash: 542bfa05c55ef224d1b9111f9af6c069e9e23542
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/28/2020
ms.locfileid: "76790966"
---
# <a name="icordebugvariablehomegetslotindex-method"></a>Icordebugvariablehome:: Getslotındex yöntemi
Yerel bir değişkenin yönetilen yuva dizinini alır.  
  
## <a name="syntax"></a>Sözdizimi  
  
```cpp  
HRESULT GetSlotIndex(  
    [out] ULONG32 *pSlotIndex  
);  
```  
  
## <a name="parameters"></a>Parametreler  
 `pSlotIndex`  
 dışı Yerel bir değişkenin yuva dizinine yönelik bir işaretçi.  
  
## <a name="return-value"></a>Dönüş Değeri  
 Yöntemi aşağıdaki değerleri döndürür.  
  
|Değer|Açıklama|  
|-----------|-----------------|  
|`S_OK`|Yöntem çağrısı `pSlotIndex`bir yuva dizini değeri döndürdü.|  
|`E_FAIL`|Geçerli [ıcordebugvariablehome](icordebugvariablehome-interface.md) örneği bir işlev bağımsız değişkenini temsil eder.|  
  
## <a name="remarks"></a>Açıklamalar  
 Bu yerel değişken için meta verileri almak için yuva dizini kullanılabilir.  
  
## <a name="requirements"></a>Gereksinimler  
 **Platformlar:** Bkz. [sistem gereksinimleri](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Üst bilgi:** CorDebug. IDL, CorDebug. h  
  
 **Kitaplık:** Corguid. lib  
  
 **.NET Framework sürümleri:** [!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]  
  
## <a name="see-also"></a>Ayrıca bkz.

- [ICorDebugVariableHome Arabirimi](icordebugvariablehome-interface.md)
