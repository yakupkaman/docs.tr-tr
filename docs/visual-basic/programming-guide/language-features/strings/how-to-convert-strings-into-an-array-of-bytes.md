---
title: 'Nasıl yapılır: dizeleri bir bayt dizisine dönüştürme'
ms.date: 07/20/2015
helpviewer_keywords:
- string conversion [Visual Basic], arrays
- arrays [Visual Basic], converting strings to
- byte arrays
- examples [Visual Basic], string conversion
- arrays [Visual Basic], byte arrays
ms.assetid: f477d35c-a3fc-4a30-b1d4-cd0d353aae1d
ms.openlocfilehash: 76fde3120ce629ce32f29ca28d90eba24fff726c
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74351967"
---
# <a name="how-to-convert-strings-into-an-array-of-bytes-in-visual-basic"></a>Nasıl yapılır: Visual Basic'de Dizeleri Bir Bayt Dizisine Dönüştürme
Bu konuda bir dizenin bayt dizisine nasıl dönüştürüleceği gösterilmektedir.  
  
## <a name="example"></a>Örnek  
 Bu örnek, bir dizeyi bir bayt dizisine dönüştürmek için <xref:System.Text.Encoding.Unicode%2A?displayProperty=nameWithType> Encoding sınıfının <xref:System.Text.Encoding.GetBytes%2A> yöntemini kullanır.  
  
 [!code-vb[VbVbalrStrings#74](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#74)]  
  
 Bir dizeyi bir bayt dizisine dönüştürmek için çeşitli kodlama seçenekleri arasından seçim yapabilirsiniz:  
  
- <xref:System.Text.Encoding.ASCII%2A?displayProperty=nameWithType>: ASCII (7 bit) karakter kümesi için bir kodlama alır.  
  
- <xref:System.Text.Encoding.BigEndianUnicode%2A?displayProperty=nameWithType>: büyük endian bayt sırasını kullanarak UTF-16 biçimi için bir kodlama alır.  
  
- <xref:System.Text.Encoding.Default%2A?displayProperty=nameWithType>: sistemin geçerli ANSI kod sayfası için bir kodlama alır.  
  
- <xref:System.Text.Encoding.Unicode%2A?displayProperty=nameWithType>: küçük endian bayt sırasını kullanarak UTF-16 biçimi için bir kodlama alır.  
  
- <xref:System.Text.Encoding.UTF32%2A?displayProperty=nameWithType>: küçük endian bayt sırasını kullanarak UTF-32 biçimi için bir kodlama alır.  
  
- <xref:System.Text.Encoding.UTF7%2A?displayProperty=nameWithType>: UTF-7 biçimi için bir kodlama alır.  
  
- <xref:System.Text.Encoding.UTF8%2A?displayProperty=nameWithType>: UTF-8 biçimi için bir kodlama alır.  
  
## <a name="see-also"></a>Ayrıca bkz.

- <xref:System.Text.Encoding?displayProperty=nameWithType>
- <xref:System.Text.Encoding.GetBytes%2A>
- [Nasıl yapılır: bayt dizisini Visual Basic bir dizeye dönüştürme](../../../../visual-basic/programming-guide/language-features/strings/how-to-convert-an-array-of-bytes-into-a-string.md)
