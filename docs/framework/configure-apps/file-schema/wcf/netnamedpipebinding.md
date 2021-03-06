---
title: <netNamedPipeBinding>
ms.date: 03/30/2017
ms.assetid: 00a8580b-face-47a4-838d-b9fed48e72df
ms.openlocfilehash: f1aa68bcdda43fd77bee397c079695f7937faa52
ms.sourcegitcommit: fbb8a593a511ce667992502a3ce6d8f65c594edf
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/16/2019
ms.locfileid: "74139472"
---
# <a name="netnamedpipebinding"></a>netNamedPipeBinding > \<
Makine içi çapraz süreç iletişimi için güvenli, güvenilir ve iyileştirilmiş olan bir bağlama tanımlar. Varsayılan olarak, güvenlik için WS-ReliableMessaging ile bir çalışma zamanı iletişim yığını, aktarım güvenliği için taşıma güvenliği, ileti teslimi için adlandırılmış kanallar ve ikili ileti kodlaması.  
  
[ **\<configuration >** ](../configuration-element.md) \
&nbsp; &nbsp;[ **\<system. serviceModel >** ](system-servicemodel.md) \
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<bağlamaları >** ](bindings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; **\<netNamedPipeBinding >**  
  
## <a name="syntax"></a>Sözdizimi  
  
```xml  
<netNamedPipeBinding>
  <binding closeTimeout="TimeSpan"
           hostNameComparisonMode="StrongWildCard/Exact/WeakWildcard"
           maxBufferPoolSize="Integer"
           maxBufferSize="Integer"
           maxConnections="Integer"
           maxReceivedMessageSize="Integer"
           name="String"
           openTimeout="TimeSpan"
           receiveTimeout="TimeSpan"
           sendTimeout="TimeSpan"
           transactionFlow="Boolean"
           transactionProtocol="OleTransactions/WS-AtomicTransactionOctober2004"
           transferMode="Buffered/Streamed/StreamedRequest/StreamedResponse">
    <security mode="None/Transport">
      <transport protectionLevel="None/Sign/EncryptAndSign" />
    </security>
    <readerQuotas maxArrayLength="Integer"
                  maxBytesPerRead="Integer"
                  maxDepth="Integer"
                  maxNameTableCharCount="Integer"
                  maxStringContentLength="Integer" />
  </binding>
</netNamedPipeBinding>
```  
  
## <a name="attributes-and-elements"></a>Öznitelikler ve Öğeler  
 Aşağıdaki bölümlerde öznitelikler, alt öğeler ve üst öğeler açıklanır  
  
### <a name="attributes"></a>Öznitelikler  
  
|Öznitelik|Açıklama|  
|---------------|-----------------|  
|closeTimeout|Bir kapatma işleminin tamamlanabilmesi için belirtilen zaman aralığını belirten bir <xref:System.TimeSpan> değeri. Bu değer, <xref:System.TimeSpan.Zero>eşit veya ondan büyük olmalıdır. Varsayılan değer 00:01:00 ' dir.|  
|hostNameComparisonMode|URI 'Leri ayrıştırmak için kullanılan HTTP ana bilgisayar adını karşılaştırma modunu belirtir. Bu öznitelik, ana bilgisayar adının URI üzerinde eşleştirilirken hizmete erişmek için kullanılıp kullanılmadığını belirten <xref:System.ServiceModel.HostNameComparisonMode>türüdür. Varsayılan değer <xref:System.ServiceModel.HostNameComparisonMode.StrongWildcard>. Bu, eşleşbir ana bilgisayar adını yok saymaz.|  
|maxBufferPoolSize|Bu bağlama için en büyük arabellek havuzu boyutunu belirten bir tamsayı. Varsayılan değer 524.288 bayttır (512 * 1024). Windows Communication Foundation (WCF) birçok bölümü arabellekler kullanır. Her kullanıldıkları sırada arabellekleri oluşturma ve yok etme, her zaman pahalıdır ve arabellekler için çöp toplama de pahalıdır. Arabellek havuzları ile havuzdan bir arabellek alabilir, bunu kullanabilir ve işiniz bittiğinde havuza döndürebilirsiniz. Bu nedenle, arabelleklerin oluşturulmasıyla ve yok edilirken ek yük önlenmiş olur.|  
|maxBufferSize|İletileri bellekte depolamak için kullanılan arabelleğin bayt cinsinden en büyük boyutunu belirten pozitif bir tamsayı. Arabellek doluysa, arabelleğin tekrar boş olması bitinceye kadar aşırı veriler temeldeki yuvada kalır. Bu değer `maxReceivedMessageSize` öznitelikten küçük olamaz. Varsayılan değer 65536 ' dir. Daha fazla bilgi için bkz. <xref:System.ServiceModel.Configuration.NetNamedPipeBindingElement.MaxBufferSize%2A>.|  
|maxConnections|Hizmetin oluşturulacağı/kabul edeceği en fazla giden ve gelen bağlantı sayısını belirten bir tamsayı. Gelen ve giden bağlantılar, bu öznitelik tarafından belirtilen ayrı bir sınıra göre sayılır.<br /><br /> Sınırın üzerindeki gelen bağlantılar, sınırın altındaki bir boşluk kullanılabilir olana kadar sıraya alınır.<br /><br /> Sınırın üzerindeki giden bağlantılar, sınırın altındaki bir boşluk kullanılabilir olana kadar sıraya alınır.<br /><br /> Varsayılan değer 10 ' dur.|  
|Değerini|Bu bağlama ile yapılandırılmış bir kanalda alınabilecek üst bilgiler dahil olmak üzere bayt cinsinden en büyük ileti boyutunu belirten pozitif bir tamsayı. Bu sınırı aşan bir iletiyi gönderen bir SOAP hatası alır. Alıcı, iletiyi bırakır ve izleme günlüğünde olayın bir girişini oluşturur. Varsayılan değer 65536 ' dir.|  
|name|Bağlamanın yapılandırma adını içeren bir dize. Bağlama için bir kimlik olarak kullanıldığından, bu değer benzersiz olmalıdır. .NET Framework 4 ' den başlayarak bağlamalar ve davranışlar bir ada sahip olmak için gerekli değildir. Varsayılan yapılandırma ve ad Less bağlamaları ve davranışları hakkında daha fazla bilgi için bkz. [WCF Hizmetleri Için](../../../wcf/samples/simplified-configuration-for-wcf-services.md) [Basitleştirilmiş yapılandırma](../../../wcf/simplified-configuration.md) ve Basitleştirilmiş yapılandırma.|  
|openTimeout|Bir açık işlemin tamamlanabilmesi için belirtilen zaman aralığını belirten bir <xref:System.TimeSpan> değeri. Bu değer, <xref:System.TimeSpan.Zero>eşit veya ondan büyük olmalıdır. Varsayılan değer 00:01:00 ' dir.|  
|receiveTimeout|Alma işleminin tamamlanabilmesi için belirtilen zaman aralığını belirten bir <xref:System.TimeSpan> değeri. Bu değer, <xref:System.TimeSpan.Zero>eşit veya ondan büyük olmalıdır. Varsayılan değer 00:10:00 ' dir.|  
|Binding üstündeki SendTimeout|Bir gönderme işleminin tamamlanabilmesi için belirtilen zaman aralığını belirten bir <xref:System.TimeSpan> değeri. Bu değer, <xref:System.TimeSpan.Zero>eşit veya ondan büyük olmalıdır. Varsayılan değer 00:01:00 ' dir.|  
|transactionFlow|Bağlamanın, akan WS-Işlemleri destekleyip desteklemediğini belirten bir Boole değeri. Varsayılan, `false` değeridir.|  
|transactionProtocol|Bu bağlama ile kullanılacak işlem protokolünü belirtir. Geçerli değerler şunlardır<br /><br /> -OleTransactions<br />-WS-AtomicTransactionOctober2004<br /><br /> Varsayılan değer OleTransactions 'dir. Bu öznitelik <xref:System.ServiceModel.TransactionProtocol>türündedir.|  
|transferMode|İletilerin arabelleğe alınıp alınmayacağını veya bir istek ya da yanıt olduğunu belirten <xref:System.ServiceModel.TransferMode> bir değer.|  
  
### <a name="child-elements"></a>Alt Öğeler  
  
|Öğe|Açıklama|  
|-------------|-----------------|  
|[\<güvenlik >](security-of-netnamedpipebinding.md)|Bağlama için güvenlik ayarlarını tanımlar. Bu öğe <xref:System.ServiceModel.Configuration.NetNamedPipeBindingElement>türündedir.|  
|[\<readerQuotas >](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms731325(v=vs.100))|Bu bağlama ile yapılandırılan uç noktalar tarafından işlenebileceğini SOAP iletilerinin karmaşıklığı üzerindeki kısıtlamaları tanımlar. Bu öğe <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement>türündedir.|  
  
### <a name="parent-elements"></a>Üst Öğeler  
  
|Öğe|Açıklama|  
|-------------|-----------------|  
|[\<bağlamaları >](bindings.md)|Bu öğe, standart ve özel bağlamaların bir koleksiyonunu içerir.|  
  
## <a name="remarks"></a>Açıklamalar  
 `NetNamedPipeBinding`, aktarım güvenliği, ileti teslimi için adlandırılmış kanallar ve ikili ileti kodlaması kullanan, varsayılan olarak bir çalışma zamanı iletişim yığını oluşturur. Bu bağlama, makineye yönelik iletişim için uygun bir Windows Communication Foundation (WCF) sistem tarafından sağlanmış seçenektir. Ayrıca işlemleri destekler.  
  
 `NetNamedPipeBinding` varsayılan yapılandırması, `NetTcpBinding`tarafından sunulan yapılandırmaya benzerdir, ancak WCF uygulamasının yalnızca şirket içi kullanım için olduğu ve bu nedenle daha az sunulan özellik olduğu için daha basittir. En önemli fark, `securityMode` ayarının yalnızca `None` ve `Transport` seçeneklerini sunmaktadır. SOAP güvenlik desteği, eklenen bir seçenek değildir. Güvenlik davranışı, isteğe bağlı `securityMode` özniteliği kullanılarak yapılandırılabilir.  
  
## <a name="example"></a>Örnek  
 Aşağıdaki örnek, aynı makinede çapraz işlem iletişimi sağlayan netNamedPipeBinding bağlamasını gösterir. Adlandırılmış kanallar makineler arasında çalışmaz.  
  
 Bağlama, istemci ve hizmet için yapılandırma dosyalarında belirtilir. Bağlama türü, `<endpoint>` öğesinin `binding` özniteliğinde belirtilir. NetNamedPipeBinding bağlamasını yapılandırmak ve bazı ayarlarını değiştirmek istiyorsanız, bir bağlama yapılandırması tanımlamanız gerekir. Uç noktanın bağlama yapılandırmasına bir `bindingConfiguration` özniteliğiyle ad ile başvurması gerekir. Bu örnekte, bağlama yapılandırması Binding1 olarak adlandırılmıştır.  
  
```xml  
<configuration>
  <system.serviceModel>
    <services>
      <service name="Microsoft.ServiceModel.Samples.CalculatorService"
               behaviorConfiguration="CalculatorServiceBehavior">
        <host>
          <baseAddresses>
            <add baseAddress="http://localhost:8000/ServiceModelSamples/service" />
          </baseAddresses>
        </host>
        <!-- this endpoint is exposed at the base address provided by host: net.pipe://localhost/ServiceModelSamples/service  -->
        <endpoint address="net.pipe://localhost/ServiceModelSamples/service"
                  binding="netNamedPipeBinding"
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />
        <!-- the mex endpoint is exposed at http://localhost:8000/ServiceModelSamples/service/mex -->
        <endpoint address="mex"
                  binding="mexHttpBinding"
                  contract="IMetadataExchange" />
      </service>
    </services>
    <bindings>
      <netNamedPipeBinding>
        <binding closeTimeout="00:01:00"
                 openTimeout="00:01:00"
                 receiveTimeout="00:10:00"
                 sendTimeout="00:01:00"
                 transactionFlow="false"
                 transferMode="Buffered"
                 transactionProtocol="OleTransactions"
                 hostNameComparisonMode="StrongWildcard"
                 maxBufferPoolSize="524288"
                 maxBufferSize="65536"
                 maxConnections="10"
                 maxReceivedMessageSize="65536">
          <security mode="Transport">
            <transport protectionLevel="EncryptAndSign" />
          </security>
        </binding>
      </netNamedPipeBinding>
    </bindings>
    <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->
    <behaviors>
      <serviceBehaviors>
        <behavior name="CalculatorServiceBehavior">
          <serviceMetadata httpGetEnabled="True" />
          <serviceDebug includeExceptionDetailInFaults="False" />
        </behavior>
      </serviceBehaviors>
    </behaviors>
  </system.serviceModel>
</configuration>
```  
  
## <a name="see-also"></a>Ayrıca bkz.

- <xref:System.ServiceModel.Configuration.NetNamedPipeBindingElement>
- <xref:System.ServiceModel.NetNamedPipeBinding>
- [bağlama > \<](bindings.md)
- [Bağlamalar](../../../wcf/bindings.md)
- [Sistem Tarafından Sağlanan Bağlamaları Yapılandırma](../../../wcf/feature-details/configuring-system-provided-bindings.md)
- [Hizmetler ve İstemcileri Yapılandırmak için Bağlamaları Kullanma](../../../wcf/using-bindings-to-configure-services-and-clients.md)
