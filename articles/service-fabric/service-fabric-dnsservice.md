---
title: "aaaAzure структуры службы DNS службы | Документы Microsoft"
description: "Использовать службу dns Service Fabric для обнаружения микрослужбами из внутри кластера hello."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/27/2017
ms.author: msfussell
ms.openlocfilehash: fa536f0e41f52c4942702d0a1bdcd3ed7d418d6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="dns-service-in-azure-service-fabric"></a>Служба DNS в Azure Service Fabric
Hello служба DNS является необязательным Системная служба, которую можно включить в вашей toodiscover кластера другие службы, использующие протокол DNS hello.

Многие службы, особенно контейнерного служб может иметь имени существующего URL-адрес и выполняется доступ tooresolve их с помощью стандартного протокола DNS hello (а не протокол службы имен hello) является предпочтительным, особенно в сценариях «точности прогнозов и shift». Hello служба DNS позволяет вам toomap DNS имена tooa имя службы и таким образом разрешить IP-адреса конечной точки. 

Служба DNS Hello сопоставляет tooservice имена DNS-имен, в свою очередь, разрешаемые hello службы имен tooreturn hello конечной точкой службы. Hello DNS-имя для службы hello предоставляется во время создания hello. 

![Конечные точки службы][0]

## <a name="enabling-hello-dns-service"></a>Включение службы DNS hello
Сначала необходима служба DNS tooenable hello в кластере. Получите шаблон hello hello кластера, которые должны toodeploy. Можно либо использовать hello [образцы шаблонов](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) или создать шаблон диспетчера ресурсов. Вы можете включить службу DNS hello hello следующие шаги:

1. Проверьте, hello `apiversion` задано слишком`2017-07-01-preview` для hello `Microsoft.ServiceFabric/clusters` ресурсов и если нет, обновить его, как показано в следующий фрагмент кода hello:

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. Теперь включите службу DNS hello, добавив следующие hello `addonFeatures` разделе после hello `fabricSettings` как показано в hello, следующий фрагмент кода: 

    ```json
        "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "DnsService"
        ],
    ```

3. После обновления шаблон кластера с hello перед внесением изменений их применения и позволить hello Обновление завершено. После завершения hello DNS Системная служба запуска в кластере, который вызывается `fabric:/System/DnsService` разделе службы системы в обозреватель Service Fabric hello. 

Кроме того можно включить hello служба DNS через портал hello во время создания кластера hello. Служба DNS Hello можно включить, установив флажок hello для `Include DNS service` в hello `Cluster configuration` меню, как показано на следующий снимок экрана приветствия:

![Включение службы DNS через портал hello][2]


## <a name="setting-hello-dns-name-for-your-service"></a>Установка hello DNS-имя для службы
После запуска службы DNS hello в кластере можно установить DNS-имя службы: декларативно для служб по умолчанию в hello `ApplicationManifest.xml` или с помощью команд Powershell.

### <a name="setting-hello-dns-name-for-a-default-service-in-hello-applicationmanifestxml"></a>Настройка DNS-имя службы по умолчанию hello в hello ApplicationManifest.xml
Откройте проект в Visual Studio или в любом редакторе, а hello `ApplicationManifest.xml` файла. Перейдите в раздел служб toohello по умолчанию и для каждой службы добавить hello `ServiceDnsName` атрибута. Hello в следующем примере показано, как tooset слишком hello DNS-имя службы hello`service1.application1`

```xml
    <Service Name="Stateless1" ServiceDnsName="service1.application1">
    <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
        <SingletonPartition />
    </StatelessService>
    </Service>
```
После развертывания приложения hello hello экземпляру службы в hello Service Fabric explorer отображается hello DNS-имя для данного экземпляра, как показано в следующий рисунок hello: 

![Конечные точки службы][1]

### <a name="setting-hello-dns-name-for-a-service-using-powershell"></a>Установка hello DNS-имя для службы с помощью Powershell
Hello DNS-имя для службы можно задать при создании с помощью hello `New-ServiceFabricService` Powershell. Hello следующем примере создается новая служба без сохранения состояния с именем DNS hello`service1.application1`

```powershell
    New-ServiceFabricService `
    -Stateless `
    -PartitionSchemeSingleton `
    -ApplicationName `fabric:/application1 `
    -ServiceName fabric:/application1/service1 `
    -ServiceTypeName Service1Type `
    -InstanceCount 1 `
    -ServiceDnsName service1.application1
```

## <a name="using-dns-in-your-services"></a>Использование DNS в службах
При развертывании нескольких служб toocommunicate других служб с конечными точками hello можно найти с помощью DNS-имя. Hello служба DNS является только служб применимо toostateless, поскольку hello протокол DNS не удается связаться с отслеживанием состояния службы. Для служб с отслеживанием состояния можно использовать hello встроенных обратного прокси-сервера для toocall вызовы http секции конкретной службы.

Hello следующий код показан toocall другой службы, которая является просто регулярного http вызов где ввести порт hello и любой дополнительный путь, как часть URL-адрес hello.

```csharp
public class ValuesController : Controller
{
    // GET api
    [HttpGet]
    public async Task<string> Get()
    {
        string result = "";
        try
        {
            Uri uri = new Uri("http://service1.application1:8080/api/values");
            HttpClient client = new HttpClient();
            var response = await client.GetAsync(uri);
            result = await response.Content.ReadAsStringAsync();
            
        }
        catch (Exception e)
        {
            Console.Write(e.Message);
        }

        return result;
    }
}
```

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о взаимодействии службы в кластере hello с [подключаться и обмениваться данными со службами](service-fabric-connect-and-communicate-with-services.md)

[0]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[1]: ./media/service-fabric-dnsservice/servicefabric-explorer-dns.PNG
[2]: ./media/service-fabric-dnsservice/DNSService.PNG
