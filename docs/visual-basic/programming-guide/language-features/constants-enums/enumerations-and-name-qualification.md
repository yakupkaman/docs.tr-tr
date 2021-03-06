---
title: Numaralandırmalar ve Ad Niteliği
ms.date: 07/20/2015
helpviewer_keywords:
- declarations [Visual Basic], enumerations
- Imports statement [Visual Basic], namespace declarations
- declaring namespaces [Visual Basic], enumerations
- name collisions
- ambiguous names [Visual Basic], enumerations
- enumerations [Visual Basic], name qualification
- names [Visual Basic], avoiding conflicts
- namespaces [Visual Basic], declaring
- naming conflicts, enumerations
- naming conflicts, qualifying names
- declaring enumerations
- references [Visual Basic], enumeration members
- naming conventions [Visual Basic], naming conflicts
- declarations [Visual Basic], namespaces
ms.assetid: 08ba2738-df52-4140-bc55-f57c871c9b73
ms.openlocfilehash: 4121266447b771ba954ad52a46e0d8b88de3f9cc
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74347491"
---
# <a name="enumerations-and-name-qualification-visual-basic"></a>Numaralandırmalar ve Ad Niteliği (Visual Basic)
Normalde, bir numaralandırma üyesine başvuru yaparken, üye adını numaralandırma adıyla nitelemeniz gerekir. Örneğin, `Days` sabit listesinin `Sunday` üyesine başvurmak için aşağıdaki sözdizimini kullanın:  
  
 [!code-vb[VbEnumsTask#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#18)]  
  
## <a name="using-the-imports-statement"></a>Imports Ifadesini kullanma  
 Aşağıdaki örnekte olduğu gibi, kodunuzun ad alanı bildirimleri bölümüne `Imports` bir ifade ekleyerek tam nitelikli adları kullanmaktan kaçınabilirsiniz:  
  
 [!code-vb[VbEnumsTask#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class1.vb#22)]  
  
 `Imports` bir ifade, Başvurulmuş projelerden ve derlemelerden ad alanı adlarını ve deyimin göründüğü modülle aynı proje içinden içeri aktarır. Bu ifade eklendikten sonra, aşağıdaki örnekte olduğu gibi, nitelik olmadan sabit listesi üyelerinize başvurabilirsiniz:  
  
 [!code-vb[VbEnumsTask#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class1.vb#24)]  
  
 Numaralandırmalar içindeki ilgili sabitlerin kümelerini düzenleyerek, farklı bağlamlarda aynı sabit adları kullanabilirsiniz. Örneğin, `Days` hafta içi sabitler için aynı adları ve numaralandırmalar `WorkDays` kullanabilirsiniz. `Imports` deyimlerinizi Numaralandırmalarla birlikte kullanıyorsanız, belirsiz başvuruların oluşmaması için dikkatli olmanız gerekir. Aşağıdaki örnek göz önünde bulundurun:  
  
 [!code-vb[VbEnumsTask#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class1.vb#22)]  
  
 [!code-vb[VbEnumsTask#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class1.vb#25)]  
  
 `Monday` hem `Days` numaralandırması hem de `Workdays` numaralandırmasında bir üye olduğunu varsayarsak, bu kod bir derleyici hatası oluşturur. Tek bir Sabitte başvuru yaparken belirsiz başvuruların önüne geçmek için sabit adı kendi numaralandırmasına uygun hale getirebilirsiniz. Aşağıdaki kod, `Days` ve `WorkDays` numaralandırmalar `Saturday` sabitlerini ifade eder.  
  
 [!code-vb[VbEnumsTask#32](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbEnumsTask/VB/Class2.vb#32)]  
  
## <a name="see-also"></a>Ayrıca bkz.

- [Sabitler ve Sabit Listeleri](../../../../visual-basic/language-reference/constants-and-enumerations.md)
- [Nasıl yapılır: numaralandırma bildirme](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)
- [Nasıl yapılır: Bir Sabit Listesi Üyesine Başvurma](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-refer-to-an-enumeration-member.md)
- [Nasıl yapılır: Visual Basic bir numaralandırmada yineleme yapma](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-iterate-through-an-enumeration.md)
- [Nasıl yapılır: Bir Sabit Listesi Değeriyle İlişkili Dizeyi Belirleme](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-determine-the-string-associated-with-an-enumeration-value.md)
- [Sabit Listesi Ne Zaman Kullanılır?](../../../../visual-basic/programming-guide/language-features/constants-enums/when-to-use-an-enumeration.md)
- [Sabit ve Değişmez Değerli Veri Türleri](../../../../visual-basic/programming-guide/language-features/constants-enums/constant-and-literal-data-types.md)
- [Enum Deyimi](../../../../visual-basic/language-reference/statements/enum-statement.md)
- [Imports Deyimi (.NET Ad Alanı ve Türü)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)
- [Veri Türleri](../../../../visual-basic/language-reference/data-types/index.md)
