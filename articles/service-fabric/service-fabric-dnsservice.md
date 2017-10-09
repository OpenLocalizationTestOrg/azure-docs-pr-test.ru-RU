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
# <a name="dns-service-in-azure-service-fabric"></a><span data-ttu-id="005f4-103">Служба DNS в Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="005f4-103">DNS Service in Azure Service Fabric</span></span>
<span data-ttu-id="005f4-104">Hello служба DNS является необязательным Системная служба, которую можно включить в вашей toodiscover кластера другие службы, использующие протокол DNS hello.</span><span class="sxs-lookup"><span data-stu-id="005f4-104">hello DNS Service is an optional system service that you can enable in your cluster toodiscover other services using hello DNS protocol.</span></span>

<span data-ttu-id="005f4-105">Многие службы, особенно контейнерного служб может иметь имени существующего URL-адрес и выполняется доступ tooresolve их с помощью стандартного протокола DNS hello (а не протокол службы имен hello) является предпочтительным, особенно в сценариях «точности прогнозов и shift».</span><span class="sxs-lookup"><span data-stu-id="005f4-105">Many services, especially containerized services, can have an existing URL name, and being able tooresolve them using hello standard DNS protocol (rather than hello Naming Service protocol) is desirable, particularly in "lift and shift" scenarios.</span></span> <span data-ttu-id="005f4-106">Hello служба DNS позволяет вам toomap DNS имена tooa имя службы и таким образом разрешить IP-адреса конечной точки.</span><span class="sxs-lookup"><span data-stu-id="005f4-106">hello DNS service enables you toomap DNS names tooa service name and hence resolve endpoint IP addresses.</span></span> 

<span data-ttu-id="005f4-107">Служба DNS Hello сопоставляет tooservice имена DNS-имен, в свою очередь, разрешаемые hello службы имен tooreturn hello конечной точкой службы.</span><span class="sxs-lookup"><span data-stu-id="005f4-107">hello DNS service maps DNS names tooservice names, which in turn are resolved by hello Naming Service tooreturn hello service endpoint.</span></span> <span data-ttu-id="005f4-108">Hello DNS-имя для службы hello предоставляется во время создания hello.</span><span class="sxs-lookup"><span data-stu-id="005f4-108">hello DNS name for hello service is provided at hello time of creation.</span></span> 

![Конечные точки службы][0]

## <a name="enabling-hello-dns-service"></a><span data-ttu-id="005f4-110">Включение службы DNS hello</span><span class="sxs-lookup"><span data-stu-id="005f4-110">Enabling hello DNS service</span></span>
<span data-ttu-id="005f4-111">Сначала необходима служба DNS tooenable hello в кластере.</span><span class="sxs-lookup"><span data-stu-id="005f4-111">First you need tooenable hello DNS service in your cluster.</span></span> <span data-ttu-id="005f4-112">Получите шаблон hello hello кластера, которые должны toodeploy.</span><span class="sxs-lookup"><span data-stu-id="005f4-112">Get hello template for hello cluster that you want toodeploy.</span></span> <span data-ttu-id="005f4-113">Можно либо использовать hello [образцы шаблонов](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) или создать шаблон диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="005f4-113">You can either use hello [sample templates](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)  or create a Resource Manager template.</span></span> <span data-ttu-id="005f4-114">Вы можете включить службу DNS hello hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="005f4-114">You can enable hello DNS service with hello following steps:</span></span>

1. <span data-ttu-id="005f4-115">Проверьте, hello `apiversion` задано слишком`2017-07-01-preview` для hello `Microsoft.ServiceFabric/clusters` ресурсов и если нет, обновить его, как показано в следующий фрагмент кода hello:</span><span class="sxs-lookup"><span data-stu-id="005f4-115">Check that hello `apiversion` is set too`2017-07-01-preview` for hello `Microsoft.ServiceFabric/clusters` resource, and if not, update it as shown in hello following snippet:</span></span>

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. <span data-ttu-id="005f4-116">Теперь включите службу DNS hello, добавив следующие hello `addonFeatures` разделе после hello `fabricSettings` как показано в hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="005f4-116">Now enable hello DNS service by adding hello following `addonFeatures` section after hello `fabricSettings` section as shown in hello following snippet:</span></span> 

    ```json
        "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "DnsService"
        ],
    ```

3. <span data-ttu-id="005f4-117">После обновления шаблон кластера с hello перед внесением изменений их применения и позволить hello Обновление завершено.</span><span class="sxs-lookup"><span data-stu-id="005f4-117">Once you have updated your cluster template with hello preceding changes, apply them and let hello upgrade complete.</span></span> <span data-ttu-id="005f4-118">После завершения hello DNS Системная служба запуска в кластере, который вызывается `fabric:/System/DnsService` разделе службы системы в обозреватель Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="005f4-118">Once complete, hello DNS system service starts running in your cluster that is called `fabric:/System/DnsService` under system service section in hello Service Fabric explorer.</span></span> 

<span data-ttu-id="005f4-119">Кроме того можно включить hello служба DNS через портал hello во время создания кластера hello.</span><span class="sxs-lookup"><span data-stu-id="005f4-119">Alternatively, you can enable hello DNS service through hello portal at hello time of cluster creation.</span></span> <span data-ttu-id="005f4-120">Служба DNS Hello можно включить, установив флажок hello для `Include DNS service` в hello `Cluster configuration` меню, как показано на следующий снимок экрана приветствия:</span><span class="sxs-lookup"><span data-stu-id="005f4-120">hello DNS service can be enabled by checking hello box for `Include DNS service` in hello `Cluster configuration` menu as shown in hello following screenshot:</span></span>

![Включение службы DNS через портал hello][2]


## <a name="setting-hello-dns-name-for-your-service"></a><span data-ttu-id="005f4-122">Установка hello DNS-имя для службы</span><span class="sxs-lookup"><span data-stu-id="005f4-122">Setting hello DNS name for your service</span></span>
<span data-ttu-id="005f4-123">После запуска службы DNS hello в кластере можно установить DNS-имя службы: декларативно для служб по умолчанию в hello `ApplicationManifest.xml` или с помощью команд Powershell.</span><span class="sxs-lookup"><span data-stu-id="005f4-123">Once hello DNS service is running in your cluster, you can set a DNS name for your services either declaratively for default services in hello `ApplicationManifest.xml` or through Powershell commands.</span></span>

### <a name="setting-hello-dns-name-for-a-default-service-in-hello-applicationmanifestxml"></a><span data-ttu-id="005f4-124">Настройка DNS-имя службы по умолчанию hello в hello ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="005f4-124">Setting hello DNS name for a default service in hello ApplicationManifest.xml</span></span>
<span data-ttu-id="005f4-125">Откройте проект в Visual Studio или в любом редакторе, а hello `ApplicationManifest.xml` файла.</span><span class="sxs-lookup"><span data-stu-id="005f4-125">Open your project in Visual Studio, or your favorite editor, and open hello `ApplicationManifest.xml` file.</span></span> <span data-ttu-id="005f4-126">Перейдите в раздел служб toohello по умолчанию и для каждой службы добавить hello `ServiceDnsName` атрибута.</span><span class="sxs-lookup"><span data-stu-id="005f4-126">Go toohello default services section, and for each service add hello `ServiceDnsName` attribute.</span></span> <span data-ttu-id="005f4-127">Hello в следующем примере показано, как tooset слишком hello DNS-имя службы hello`service1.application1`</span><span class="sxs-lookup"><span data-stu-id="005f4-127">hello following example shows how tooset hello DNS name of hello service too`service1.application1`</span></span>

```xml
    <Service Name="Stateless1" ServiceDnsName="service1.application1">
    <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
        <SingletonPartition />
    </StatelessService>
    </Service>
```
<span data-ttu-id="005f4-128">После развертывания приложения hello hello экземпляру службы в hello Service Fabric explorer отображается hello DNS-имя для данного экземпляра, как показано в следующий рисунок hello:</span><span class="sxs-lookup"><span data-stu-id="005f4-128">Once hello application is deployed, hello service instance in hello Service Fabric explorer shows hello DNS name for this instance, as shown in hello following figure:</span></span> 

![Конечные точки службы][1]

### <a name="setting-hello-dns-name-for-a-service-using-powershell"></a><span data-ttu-id="005f4-130">Установка hello DNS-имя для службы с помощью Powershell</span><span class="sxs-lookup"><span data-stu-id="005f4-130">Setting hello DNS name for a service using Powershell</span></span>
<span data-ttu-id="005f4-131">Hello DNS-имя для службы можно задать при создании с помощью hello `New-ServiceFabricService` Powershell.</span><span class="sxs-lookup"><span data-stu-id="005f4-131">You can set hello DNS name for a service when creating it using hello `New-ServiceFabricService` Powershell.</span></span> <span data-ttu-id="005f4-132">Hello следующем примере создается новая служба без сохранения состояния с именем DNS hello`service1.application1`</span><span class="sxs-lookup"><span data-stu-id="005f4-132">hello following example creates a new stateless service with hello DNS name `service1.application1`</span></span>

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

## <a name="using-dns-in-your-services"></a><span data-ttu-id="005f4-133">Использование DNS в службах</span><span class="sxs-lookup"><span data-stu-id="005f4-133">Using DNS in your services</span></span>
<span data-ttu-id="005f4-134">При развертывании нескольких служб toocommunicate других служб с конечными точками hello можно найти с помощью DNS-имя.</span><span class="sxs-lookup"><span data-stu-id="005f4-134">If you deploy more than one service, you can find hello endpoints of other services toocommunicate with  by using a DNS name.</span></span> <span data-ttu-id="005f4-135">Hello служба DNS является только служб применимо toostateless, поскольку hello протокол DNS не удается связаться с отслеживанием состояния службы.</span><span class="sxs-lookup"><span data-stu-id="005f4-135">hello DNS service is only applicable toostateless services, since hello DNS protocol cannot communicate with stateful services.</span></span> <span data-ttu-id="005f4-136">Для служб с отслеживанием состояния можно использовать hello встроенных обратного прокси-сервера для toocall вызовы http секции конкретной службы.</span><span class="sxs-lookup"><span data-stu-id="005f4-136">For stateful services, you can use hello built-in reverse proxy for http calls toocall a particular service partition.</span></span>

<span data-ttu-id="005f4-137">Hello следующий код показан toocall другой службы, которая является просто регулярного http вызов где ввести порт hello и любой дополнительный путь, как часть URL-адрес hello.</span><span class="sxs-lookup"><span data-stu-id="005f4-137">hello following code shows how toocall another service, which is simply a regular http call where you provide hello port and any optional path as part of hello URL.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="005f4-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="005f4-138">Next steps</span></span>
<span data-ttu-id="005f4-139">Дополнительные сведения о взаимодействии службы в кластере hello с [подключаться и обмениваться данными со службами](service-fabric-connect-and-communicate-with-services.md)</span><span class="sxs-lookup"><span data-stu-id="005f4-139">Learn more about service communication within hello cluster with  [connect and communicate with services](service-fabric-connect-and-communicate-with-services.md)</span></span>

[0]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[1]: ./media/service-fabric-dnsservice/servicefabric-explorer-dns.PNG
[2]: ./media/service-fabric-dnsservice/DNSService.PNG
