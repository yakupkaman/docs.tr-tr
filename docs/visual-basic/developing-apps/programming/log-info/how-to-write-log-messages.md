---
title: 'Nasıl Yapılır: Günlük İletileri Yazma'
ms.date: 07/20/2015
helpviewer_keywords:
- My.Application.Log object, writing log messages
ms.assetid: 972a3e0c-2996-4623-a7a9-d7ebc4d207f8
ms.openlocfilehash: 38570047db48e009aea2af376304430db1ec29f4
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/15/2020
ms.locfileid: "74352062"
---
# <a name="how-to-write-log-messages-visual-basic"></a>Nasıl Yapılır: Günlük İletileri Yazma (Visual Basic)

Uygulamanızla ilgili `My.Application.Log` `My.Log` bilgileri günlüğe kaydetmek için nesneleri ve nesneleri kullanabilirsiniz. Bu örnek, izleme `My.Application.Log.WriteEntry` bilgilerini günlüğe kaydetmek için yöntemin nasıl kullanılacağını gösterir.

Özel durum bilgilerini günlüğe kaydetmek için `My.Application.Log.WriteException` yöntemi kullanın; bkz. [Nasıl yapılır: Özel Durumları Günlüğe](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-exceptions.md)Kaydedin.

## <a name="example"></a>Örnek

Bu örnek, `My.Application.Log.WriteEntry` izleme bilgilerini yazmak için yöntemi kullanır.

[!code-vb[VbVbalrMyApplicationLog#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyApplicationLog/VB/Form1.vb#11)]

## <a name="net-framework-security"></a>.NET Framework Güvenliği

Günlük lere yazdığınız verilerin kullanıcı parolaları gibi hassas bilgileri içermediğinden emin olun. Daha fazla bilgi için bkz: [Uygulama Günlükleriyle Çalışma.](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)

## <a name="see-also"></a>Ayrıca bkz.

- <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteEntry%2A>
- <xref:Microsoft.VisualBasic.Logging.Log.WriteException%2A>
- [Uygulama Günlükleriyle Çalışma](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)
- [Nasıl Yapılır: Günlük Özel Durumları](../../../../visual-basic/developing-apps/programming/log-info/how-to-log-exceptions.md)
- [İzlenecek Yol: My.Application.Log Günlüğünün Bilgileri Nereye Yazdığını Belirleme](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md)
- [İzlenecek Yol: My.Application.Log Günlüğünün Bilgileri Yazdığı Yeri Değiştirme](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-changing-where-my-application-log-writes-information.md)
- [İzlenecek Yol: My.Application.Log Çıktısını Filtreleme](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-filtering-my-application-log-output.md)
