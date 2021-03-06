---
title: Beyanlar ve Kaynaklara Erişimi Reddetme
ms.date: 03/30/2017
helpviewer_keywords:
- claims [WCF], denying access to resources
ms.assetid: 145ebb41-680e-4256-b14c-1efb4af1e982
ms.openlocfilehash: 4f48c59090579f4b451f615bb792a4dcb73f6df5
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/23/2019
ms.locfileid: "61857603"
---
# <a name="claims-and-denying-access-to-resources"></a>Beyanlar ve Kaynaklara Erişimi Reddetme
Windows Communication Foundation (WCF) bir beyana dayalı yetkilendirme mekanizması destekler. Talep varlığını temel alarak kaynaklara erişimine yanı sıra sistemleri genellikle talep varlığını temel alarak kaynaklara erişimi reddetme. Bu sistemlere incelemelisiniz <xref:System.IdentityModel.Policy.AuthorizationContext> aramadan önce erişimine izin verilmesinden neden talepler için erişimin reddedilmesi neden talepler için.  
  
 Örneğin, bir sistem bir kaynağa erişim izni olan herkes bir talep türü ile reddetmek, `Age`, sağ <xref:System.IdentityModel.Claims.Rights.PossessProperty%2A>, kaynak değerini `Under 21` yalnızca o kimlik da bir talep türü olduğunda `Name`, sağ <xref:System.IdentityModel.Claims.Rights.Identity%2A>, Kaynak değeri `Mallory`. Başka bir deyişle, sistem erişimi herkes tarafından altında 21 yaşında olduğunu ve adı Mallory olduğunda erişim verir engeller. Bu doğru uygulamak için anlamsal, aranacak önemlidir `Age` ilk talep ve yaş altında 21 yaşında olup olmadığını belirler. Mallory 21'altında varsa, aksi takdirde, daha sonra kaynak yalnızca temeline göre erişim verilebilir `Name` talep.  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Kimlik Modeliyle Talep ve Yetkilendirmeyi Yönetme](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md)
- [Talepler ve Belirteçler](../../../../docs/framework/wcf/feature-details/claims-and-tokens.md)
