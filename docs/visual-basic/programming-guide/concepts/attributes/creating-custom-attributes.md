---
title: Özel Öznitelikler Oluşturma
ms.date: 07/20/2015
ms.assetid: 5c9ef584-6c7c-496b-92a9-6e42f8d9ca28
ms.openlocfilehash: 773a3e8e974f37a1554892dd3441c115681c5bae
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74350153"
---
# <a name="creating-custom-attributes-visual-basic"></a>Özel öznitelikler oluşturma (Visual Basic)

Meta verilerde hızlı ve kolay bir şekilde öznitelik tanımları tanımlamayı sağlayan, <xref:System.Attribute>doğrudan veya dolaylı olarak türetilen bir sınıf olan bir öznitelik sınıfı tanımlayarak kendi özel öznitelerinizi oluşturabilirsiniz. Türleri, türünü yazan programcının adıyla etiketlemek istediğinizi varsayalım. Özel bir `Author` öznitelik sınıfı tanımlayabilirsiniz:

```vb
<System.AttributeUsage(System.AttributeTargets.Class Or
                       System.AttributeTargets.Struct)>
Public Class Author
    Inherits System.Attribute
    Private name As String
    Public version As Double
    Sub New(ByVal authorName As String)
        name = authorName
        version = 1.0
    End Sub
End Class
```

Sınıf adı özniteliğin adı, `Author`. `System.Attribute`türetilir, bu nedenle özel bir öznitelik sınıfıdır. Oluşturucunun parametreleri özel özniteliğin konumsal parametreleridir. Bu örnekte, `name` konumsal bir parametredir. Tüm genel okuma/yazma alanları veya özellikleri parametreler olarak adlandırılır. Bu durumda, `version` tek parametre olarak adlandırılır. `Author` özniteliğini yalnızca sınıf ve `Structure` bildirimlerinde geçerli hale getirmek için `AttributeUsage` özniteliğinin kullanımını unutmayın.

Bu yeni özniteliği şu şekilde kullanabilirsiniz:

```vb
<Author("P. Ackerman", Version:=1.1)>
Class SampleClass
    ' P. Ackerman's code goes here...
End Class
```

`AttributeUsage` adlandırılmış bir parametreye sahiptir ve bu, özel bir özniteliği tek veya çoklu kullanımı yapmak için `AllowMultiple`. Aşağıdaki kod örneğinde, Multiuse özniteliği oluşturulur.

```vb
' multiuse attribute
<System.AttributeUsage(System.AttributeTargets.Class Or
                       System.AttributeTargets.Struct,
                       AllowMultiple:=True)>
Public Class Author
    Inherits System.Attribute
```

Aşağıdaki kod örneğinde, aynı türde birden çok öznitelik bir sınıfa uygulanır.

```vb
<Author("P. Ackerman", Version:=1.1),
Author("R. Koch", Version:=1.2)>
Class SampleClass
    ' P. Ackerman's code goes here...
    ' R. Koch's code goes here...
End Class
```

> [!NOTE]
> Öznitelik sınıfınız bir özellik içeriyorsa, bu özellik oku-yaz olmalıdır.

## <a name="see-also"></a>Ayrıca bkz.

- <xref:System.Reflection>
- [Visual Basic programlama kılavuzu](../../../../visual-basic/programming-guide/index.md)
- [Özel Öznitelikler Yazma](../../../../standard/attributes/writing-custom-attributes.md)
- [Yansıma (Visual Basic)](../../../../visual-basic/programming-guide/concepts/reflection.md)
- [Öznitelikler (Visual Basic)](../../../../visual-basic/language-reference/attributes.md)
- [Yansıma kullanarak özniteliklere erişme (Visual Basic)](../../../../visual-basic/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md)
- [AttributeUsage (Visual Basic)](../../../../visual-basic/programming-guide/concepts/attributes/attributeusage.md)
