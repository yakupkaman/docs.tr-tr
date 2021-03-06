---
title: CheckBox Denetimleriyle Seçenekleri Ayarlama
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
f1_keywords:
- checked
helpviewer_keywords:
- CheckBox control [Windows Forms], checked state
- check boxes [Windows Forms], using to set options
- CheckBox control [Windows Forms], using to set options
ms.assetid: 2ac70498-7e3e-4e07-8901-ccabaeb5fd3e
ms.openlocfilehash: 00b467836d8e60aeee51a010a6384abf7dd73c56
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/12/2020
ms.locfileid: "79141854"
---
# <a name="how-to-set-options-with-windows-forms-checkbox-controls"></a>Nasıl yapılır: Windows Forms CheckBox Denetimleriyle Seçenekleri Ayarlama
Windows Forms <xref:System.Windows.Forms.CheckBox> denetimi, kullanıcılara True/False veya Yes/No seçeneklerini vermek için kullanılır. Denetim seçildiğinde bir onay işareti görüntüler.  
  
### <a name="to-set-options-with-checkbox-controls"></a>Onay Kutusu denetimleriyle seçenekleri ayarlamak için  
  
1. Durumunu belirlemek için <xref:System.Windows.Forms.CheckBox.Checked%2A> özelliğin değerini inceleyin ve bir seçenek ayarlamak için bu değeri kullanın.  
  
     Aşağıdaki kod örneğinde, <xref:System.Windows.Forms.CheckBox> denetimin <xref:System.Windows.Forms.CheckBox.CheckedChanged> olayı yükseltildiğinde, onay <xref:System.Windows.Forms.Control.AllowDrop%2A> kutusu `false` işaretlenirse formun özelliği ayarlanır. Bu, kullanıcı etkileşimini kısıtlamak istediğiniz durumlar için yararlıdır.  
  
    ```vb  
    Private Sub CheckBox1_CheckedChanged(ByVal sender As System.Object, _  
       ByVal e As System.EventArgs) Handles CheckBox1.CheckedChanged  
       ' Determine the CheckState of the check box.  
       If CheckBox1.CheckState = CheckState.Checked Then  
          ' If checked, do not allow items to be dragged onto the form.  
          Me.AllowDrop = False  
       End If  
    End Sub  
    ```  
  
    ```csharp  
    private void checkBox1_CheckedChanged(object sender, System.EventArgs e)  
    {  
       // Determine the CheckState of the check box.  
       if (checkBox1.CheckState == CheckState.Checked)
       {  
          // If checked, do not allow items to be dragged onto the form.  
          this.AllowDrop = false;  
       }  
    }  
    ```  
  
    ```cpp  
    private:  
       void checkBox1_CheckedChanged(System::Object ^ sender,  
          System::EventArgs ^ e)  
       {  
          // Determine the CheckState of the check box.  
          if (checkBox1->CheckState == CheckState::Checked)
          {  
             // If checked, do not allow items to be dragged onto the form.  
             this->AllowDrop = false;  
          }  
       }  
    ```  
  
## <a name="see-also"></a>Ayrıca bkz.

- <xref:System.Windows.Forms.CheckBox>
- [CheckBox Denetimine Genel Bakış](checkbox-control-overview-windows-forms.md)
- [Nasıl yapılır: Windows Forms CheckBox Tıklamalarına Yanıt Verme](how-to-respond-to-windows-forms-checkbox-clicks.md)
- [CheckBox Denetimi](checkbox-control-windows-forms.md)
