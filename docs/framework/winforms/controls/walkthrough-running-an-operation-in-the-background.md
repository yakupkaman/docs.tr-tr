---
title: 'İzlenecek yol: Arka Planda İşlem Çalıştırma'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- background tasks
- forms [Windows Forms], multithreading
- forms [Windows Forms], background operations
- background threads
- BackgroundWorker class [Windows Forms], examples
- threading [Windows Forms], background operations
- background operations
ms.assetid: 1b9a4e0a-f134-48ff-a1be-c461446a31ba
ms.openlocfilehash: 6c705c6d6ff9bbd233bbddc3a73acf8aca13a547
ms.sourcegitcommit: 0d0a6e96737dfe24d3257b7c94f25d9500f383ea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65211519"
---
# <a name="walkthrough-running-an-operation-in-the-background"></a>İzlenecek yol: Arka Planda İşlem Çalıştırma

Sahip olduğunuz işleminin tamamlanması uzun sürer ve kullanıcı arabiriminizde gecikmelere neden istiyor musunuz, kullanabileceğiniz <xref:System.ComponentModel.BackgroundWorker> sınıfı, başka bir iş parçacığı üzerinde işlemi çalıştıramadı.

Bu örnekte kullanılan kod tam listesi için bkz. [nasıl yapılır: Arka planda işlem çalıştırma](how-to-run-an-operation-in-the-background.md).

## <a name="run-an-operation-in-the-background"></a>Arka planda işlem çalıştırma

1. Formun etkin Windows Form Tasarımcısı'nda Visual Studio ile iki <xref:System.Windows.Forms.Button> denetimler **araç kutusu** form ve ardından `Name` ve <xref:System.Windows.Forms.Control.Text%2A> göre düğmelerinin özellikleri Aşağıdaki tablo.

    |Düğme|Ad|Metin|
    |------------|----------|----------|
    |`button1`|`startBtn`|**Start**|
    |`button2`|`cancelBtn`|**İptal Etme**|

2. Açık **araç kutusu**, tıklayın **bileşenleri** sekmesine ve ardından sürükleyin <xref:System.ComponentModel.BackgroundWorker> formunuza bileşen.

     `backgroundWorker1` Bileşeni görünür **bileşeni Tepsi**.

3. İçinde **özellikleri** penceresinde <xref:System.ComponentModel.BackgroundWorker.WorkerSupportsCancellation%2A> özelliğini `true`.

4. İçinde **özellikleri** penceresinde tıklayarak **olayları** düğmesini ve ardından çift <xref:System.ComponentModel.BackgroundWorker.DoWork> ve <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> olayları olay işleyicilerini oluşturma.

5. Zaman kodunuza ekleyin <xref:System.ComponentModel.BackgroundWorker.DoWork> olay işleyicisi.

6. Ayıklama işlemi tarafından gereken herhangi bir parametre <xref:System.ComponentModel.DoWorkEventArgs.Argument%2A> özelliği <xref:System.ComponentModel.DoWorkEventArgs> parametresi.

7. Bir hesaplama sonucu atama <xref:System.ComponentModel.DoWorkEventArgs.Result%2A> özelliği <xref:System.ComponentModel.DoWorkEventArgs>.

     Bu işlem, kullanılabilir <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> olay işleyicisi.

     [!code-csharp[System.ComponentModel.BackgroundWorker.Example#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/CS/Form1.cs#2)]
     [!code-vb[System.ComponentModel.BackgroundWorker.Example#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/VB/Form1.vb#2)]

8. İçinde işlemin sonucunu almak için kod ekleme <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> olay işleyicisi.

     [!code-csharp[System.ComponentModel.BackgroundWorker.Example#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/CS/Form1.cs#3)]
     [!code-vb[System.ComponentModel.BackgroundWorker.Example#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/VB/Form1.vb#3)]

9. Uygulama `TimeConsumingOperation` yöntemi.

     [!code-csharp[System.ComponentModel.BackgroundWorker.Example#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/CS/Form1.cs#4)]
     [!code-vb[System.ComponentModel.BackgroundWorker.Example#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/VB/Form1.vb#4)]

10. Windows Form Tasarımcısı'nda çift `startButton` oluşturmak için <xref:System.Windows.Forms.Control.Click> olay işleyicisi.

11. Çağrı <xref:System.ComponentModel.BackgroundWorker.RunWorkerAsync%2A> yönteminde <xref:System.Windows.Forms.Control.Click> için olay işleyicisi `startButton`.

     [!code-csharp[System.ComponentModel.BackgroundWorker.Example#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/CS/Form1.cs#5)]
     [!code-vb[System.ComponentModel.BackgroundWorker.Example#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/VB/Form1.vb#5)]

12. Windows Form Tasarımcısı'nda çift `cancelButton` oluşturmak için <xref:System.Windows.Forms.Control.Click> olay işleyicisi.

13. Çağrı <xref:System.ComponentModel.BackgroundWorker.CancelAsync%2A> yönteminde <xref:System.Windows.Forms.Control.Click> için olay işleyicisi `cancelButton`.

     [!code-csharp[System.ComponentModel.BackgroundWorker.Example#6](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/CS/Form1.cs#6)]
     [!code-vb[System.ComponentModel.BackgroundWorker.Example#6](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/VB/Form1.vb#6)]

14. Dosyasının en üstüne System.ComponentModel ve System.Threading ad alanlarını içeri aktarın.

     [!code-csharp[System.ComponentModel.BackgroundWorker.Example#7](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/CS/Form1.cs#7)]
     [!code-vb[System.ComponentModel.BackgroundWorker.Example#7](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.BackgroundWorker.Example/VB/Form1.vb#7)]

15. Basın **F6** Çözümü derleyin ve ENTER tuşuna basın **Ctrl**+**F5** hata ayıklayıcı dışında uygulamayı çalıştırın.

    > [!NOTE]
    > Basarsanız **F5** hata ayıklayıcısı altında uygulamayı çalıştırmak için özel durum ortaya `TimeConsumingOperation` yöntemi yakalandı ve hata ayıklayıcı tarafından görüntülenir. Uygulama, hata ayıklayıcı dışında çalıştırırken <xref:System.ComponentModel.BackgroundWorker> içinde önbelleğe alır ve özel durum işleme <xref:System.ComponentModel.AsyncCompletedEventArgs.Error%2A> özelliği <xref:System.ComponentModel.RunWorkerCompletedEventArgs>.

16. Tıklayın **Başlat** zaman uyumsuz bir işlemin çalıştırılması için düğmesine ve ardından **iptal** bir çalıştırma zaman uyumsuz işlemi durdurmak için düğmeye.

     Her bir işlemin sonucunu görüntülenen bir <xref:System.Windows.Forms.MessageBox>.

## <a name="next-steps"></a>Sonraki adımlar

- Zaman uyumsuz bir işlem devam ederken, ilerleme durumunu raporlayan bir form uygulama. Daha fazla bilgi için [nasıl yapılır: Arka plan işlemi kullanan bir Form uygulama](how-to-implement-a-form-that-uses-a-background-operation.md).

- Bileşenler için zaman uyumsuz deseni destekleyen bir sınıf uygulamak. Daha fazla bilgi için [olay tabanlı zaman uyumsuz deseni uygulama](../../../standard/asynchronous-programming-patterns/implementing-the-event-based-asynchronous-pattern.md).

## <a name="see-also"></a>Ayrıca bkz.

- <xref:System.ComponentModel.BackgroundWorker>
- <xref:System.ComponentModel.DoWorkEventArgs>
- [Nasıl yapılır: Arka plan işlemi kullanan bir Form uygulama](how-to-implement-a-form-that-uses-a-background-operation.md)
- [Nasıl yapılır: Arka planda işlem çalıştırma](how-to-run-an-operation-in-the-background.md)
- [BackgroundWorker Bileşeni](backgroundworker-component.md)
