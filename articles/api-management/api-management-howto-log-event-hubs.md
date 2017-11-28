---
title: "aaaHow toolog события tooAzure концентраторов событий в службе управления API Azure | Документы Microsoft"
description: "Узнайте, как tooAzure toolog событий концентраторов событий в службе управления API Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 88f6507d-7460-4eb2-bffd-76025b73f8c4
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 09ca65fc48a874467c6662858f7594e9b19fcdb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toolog-events-tooazure-event-hubs-in-azure-api-management"></a><span data-ttu-id="01acf-103">Как tooAzure toolog событий концентраторов событий в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="01acf-103">How toolog events tooAzure Event Hubs in Azure API Management</span></span>
<span data-ttu-id="01acf-104">Концентраторы событий Azure — служба входящих данных на высокую степень масштабируемости, можно принять миллионов событий в секунду, можно обрабатывать и анализировать hello значительные объемы данных, создаваемых подключенных устройств и приложений.</span><span class="sxs-lookup"><span data-stu-id="01acf-104">Azure Event Hubs is a highly scalable data ingress service that can ingest millions of events per second so that you can process and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="01acf-105">Концентраторов событий действует как hello «дверью» для конвейера событий и сбора данных в концентратор событий, он может преобразовываться и сохраненных с помощью любого поставщика аналитика в реальном времени или адаптеры пакетной обработки хранилища.</span><span class="sxs-lookup"><span data-stu-id="01acf-105">Event Hubs acts as hello "front door" for an event pipeline, and once data is collected into an event hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="01acf-106">Концентраторы событий отделяет hello рабочего потока событий из hello использования этих событий, чтобы потребители событий можно получать доступ к событиям hello по собственному расписанию.</span><span class="sxs-lookup"><span data-stu-id="01acf-106">Event Hubs decouples hello production of a stream of events from hello consumption of those events, so that event consumers can access hello events on their own schedule.</span></span>

<span data-ttu-id="01acf-107">Эта статья является toohello дополнительное [интегрируются с концентраторами событий управления API Azure](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) видео и показывается, как события toolog управления API, с помощью концентраторов событий Azure.</span><span class="sxs-lookup"><span data-stu-id="01acf-107">This article is a companion toohello [Integrate Azure API Management with Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video and describes how toolog API Management events using Azure Event Hubs.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="01acf-108">Создание концентратора событий Azure</span><span class="sxs-lookup"><span data-stu-id="01acf-108">Create an Azure Event Hub</span></span>
<span data-ttu-id="01acf-109">новый концентратор событий входа в toohello toocreate [классический портал Azure](https://manage.windowsazure.com) и нажмите кнопку **New**->**службы приложений**->**Service Bus**  -> **Концентратора событий**->**быстрое создание**.</span><span class="sxs-lookup"><span data-stu-id="01acf-109">toocreate a new Event Hub, sign-in toohello [Azure classic portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Service Bus**->**Event Hub**->**Quick Create**.</span></span> <span data-ttu-id="01acf-110">Введите имя концентратора событий, регион, выберите подписку и пространство имен.</span><span class="sxs-lookup"><span data-stu-id="01acf-110">Enter an Event Hub name, region, select a subscription, and select a namespace.</span></span> <span data-ttu-id="01acf-111">Если вы еще не создали пространство имен можно создать, введя имя в hello **имен** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="01acf-111">If you haven't previously created a namespace you can create one by typing a name in hello **Namespace** textbox.</span></span> <span data-ttu-id="01acf-112">После настройки всех свойств, нажмите кнопку **создать новый концентратор событий** toocreate hello концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="01acf-112">Once all properties are configured, click **Create a new Event Hub** toocreate hello Event Hub.</span></span>

![Создание концентратора событий][create-event-hub]

<span data-ttu-id="01acf-114">Далее перейдите toohello **Настройка** вкладке нового концентратора событий и создания двух **политики общего доступа**.</span><span class="sxs-lookup"><span data-stu-id="01acf-114">Next, navigate toohello **Configure** tab for your new Event Hub and create two **shared access policies**.</span></span> <span data-ttu-id="01acf-115">Имя первого hello **Отправка** и присвойте ему **отправки** разрешения.</span><span class="sxs-lookup"><span data-stu-id="01acf-115">Name hello first one **Sending** and give it **Send** permissions.</span></span>

![Политика «Отправка»][sending-policy]

<span data-ttu-id="01acf-117">Имя второго hello **получения**, ей следует присвоить **прослушивания** разрешений и нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="01acf-117">Name hello second one **Receiving**, give it **Listen** permissions, and click **Save**.</span></span>

![Политика «Получение»][receiving-policy]

<span data-ttu-id="01acf-119">Каждая политика общего доступа позволяет toosend приложений и получают события tooand от hello концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="01acf-119">Each shared access policy allows applications toosend and receive events tooand from hello Event Hub.</span></span> <span data-ttu-id="01acf-120">строки подключения hello tooaccess для этих политик перейдите toohello **мониторинга** hello концентратора событий и нажмите кнопку **сведения о соединении**.</span><span class="sxs-lookup"><span data-stu-id="01acf-120">tooaccess hello connection strings for these policies, navigate toohello **Dashboard** tab of hello Event Hub and click **Connection information**.</span></span>

![Строка подключения][event-hub-dashboard]

<span data-ttu-id="01acf-122">Hello **Отправка** строка подключения используется в том случае, если ведение журнала событий и hello **получения** строка подключения используется при загрузке события с hello концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="01acf-122">hello **Sending** connection string is used when logging events, and hello **Receiving** connection string is used when downloading events from hello Event Hub.</span></span>

![Строка подключения][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a><span data-ttu-id="01acf-124">Создание средства ведения журнала для управления API</span><span class="sxs-lookup"><span data-stu-id="01acf-124">Create an API Management logger</span></span>
<span data-ttu-id="01acf-125">Теперь, когда концентратора событий hello следующим шагом является tooconfigure [средства ведения журнала](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) в вашей службе управления API службы, чтобы его можно записывать в журнал событий toohello концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="01acf-125">Now that you have an Event Hub, hello next step is tooconfigure a [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) in your API Management service so that it can log events toohello Event Hub.</span></span>

<span data-ttu-id="01acf-126">Управление API средств ведения журнала настроены с использованием hello [API REST управления](http://aka.ms/smapi).</span><span class="sxs-lookup"><span data-stu-id="01acf-126">API Management loggers are configured using hello [API Management REST API](http://aka.ms/smapi).</span></span> <span data-ttu-id="01acf-127">Перед использованием hello API-интерфейса REST для hello первый раз, просмотрите hello [необходимые компоненты](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) и убедитесь, что [включен доступ toohello API-интерфейса REST](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span><span class="sxs-lookup"><span data-stu-id="01acf-127">Before using hello REST API for hello first time, review hello [prerequisites](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) and ensure that you have [enabled access toohello REST API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span></span>

<span data-ttu-id="01acf-128">toocreate средство ведения журнала, сделать запрос HTTP PUT, используя следующий шаблон URL-адреса hello.</span><span class="sxs-lookup"><span data-stu-id="01acf-128">toocreate a logger, make an HTTP PUT request using hello following URL template.</span></span>

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* <span data-ttu-id="01acf-129">Замените `{your service}` hello именем вашего экземпляра службы управления API.</span><span class="sxs-lookup"><span data-stu-id="01acf-129">Replace `{your service}` with hello name of your API Management service instance.</span></span>
* <span data-ttu-id="01acf-130">Замените `{new logger name}` с нужным именем hello для вашего новое средство ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="01acf-130">Replace `{new logger name}` with hello desired name for your new logger.</span></span> <span data-ttu-id="01acf-131">Это имя будет ссылаться при настройке hello [журнала eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) политики</span><span class="sxs-lookup"><span data-stu-id="01acf-131">You will reference this name when you configure hello [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) policy</span></span>

<span data-ttu-id="01acf-132">Добавьте следующие заголовки запроса toohello hello.</span><span class="sxs-lookup"><span data-stu-id="01acf-132">Add hello following headers toohello request.</span></span>

* <span data-ttu-id="01acf-133">тип содержимого: «application/json»;</span><span class="sxs-lookup"><span data-stu-id="01acf-133">Content-Type : application/json</span></span>
* <span data-ttu-id="01acf-134">авторизация: SharedAccessSignature 58...</span><span class="sxs-lookup"><span data-stu-id="01acf-134">Authorization : SharedAccessSignature 58...</span></span>
  * <span data-ttu-id="01acf-135">Инструкции о создании hello `SharedAccessSignature` разделе [проверки подлинности API REST управления API Azure](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span><span class="sxs-lookup"><span data-stu-id="01acf-135">For instructions on generating hello `SharedAccessSignature` see [Azure API Management REST API Authentication](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span></span>

<span data-ttu-id="01acf-136">Укажите hello текст запроса, используя следующий шаблон hello.</span><span class="sxs-lookup"><span data-stu-id="01acf-136">Specify hello request body using hello following template.</span></span>

```json
{
  "type" : "AzureEventHub",
  "description" : "Sample logger description",
  "credentials" : {
    "name" : "Name of hello Event Hub from hello Azure Classic Portal",
    "connectionString" : "Endpoint=Event Hub Sender connection string"
    }
}
```

* <span data-ttu-id="01acf-137">`type`необходимо задать слишком`AzureEventHub`.</span><span class="sxs-lookup"><span data-stu-id="01acf-137">`type` must be set too`AzureEventHub`.</span></span>
* <span data-ttu-id="01acf-138">`description`предоставляет средства ведения журнала hello необязательное описание и может быть строка нулевой длины, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="01acf-138">`description` provides an optional description of hello logger and can be a zero length string if desired.</span></span>
* <span data-ttu-id="01acf-139">`credentials`содержит hello `name` и `connectionString` из концентратора событий Azure.</span><span class="sxs-lookup"><span data-stu-id="01acf-139">`credentials` contains hello `name` and `connectionString` of your Azure Event Hub.</span></span>

<span data-ttu-id="01acf-140">При выполнении запроса hello hello средства ведения журнала, созданный код состояния `201 Created` возвращается.</span><span class="sxs-lookup"><span data-stu-id="01acf-140">When you make hello request, if hello logger is created a status code of `201 Created` is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="01acf-141">Другие возможные коды возврата и их причины см. в статье, посвященной [созданию средств ведения журнала](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span><span class="sxs-lookup"><span data-stu-id="01acf-141">For other possible return codes and their reasons, see [Create a Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span></span> <span data-ttu-id="01acf-142">toosee, как выполнить другие операции, такие как список, update и delete, в разделе hello [средства ведения журнала](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) документации сущности.</span><span class="sxs-lookup"><span data-stu-id="01acf-142">toosee how perform other operations such as list, update, and delete, see hello [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) entity documentation.</span></span>
>
>

## <a name="configure-log-to-eventhubs-policies"></a><span data-ttu-id="01acf-143">Настройка политик регистрации в концентраторах событий</span><span class="sxs-lookup"><span data-stu-id="01acf-143">Configure log-to-eventhubs policies</span></span>
<span data-ttu-id="01acf-144">После настройки вашей средства ведения журнала в службе управления API можно настроить события журнала eventhubs политики toolog требуемого hello.</span><span class="sxs-lookup"><span data-stu-id="01acf-144">Once your logger is configured in API Management, you can configure your log-to-eventhubs policies toolog hello desired events.</span></span> <span data-ttu-id="01acf-145">Hello журнала eventhubs политика может использоваться в любом hello раздел входящей политики или раздел исходящих политики hello.</span><span class="sxs-lookup"><span data-stu-id="01acf-145">hello log-to-eventhubs policy can be used in either hello inbound policy section or hello outbound policy section.</span></span>

<span data-ttu-id="01acf-146">tooconfigure политик, вход toohello [портал Azure](https://portal.azure.com), перейдите в службе управления API tooyour и нажмите кнопку **портал издателя** tooaccess hello портала издателя.</span><span class="sxs-lookup"><span data-stu-id="01acf-146">tooconfigure policies, sign-in toohello [Azure portal](https://portal.azure.com), navigate tooyour API Management service, and click **Publisher portal** tooaccess hello publisher portal.</span></span>

![Портал издателя][publisher-portal]

<span data-ttu-id="01acf-148">Нажмите кнопку **политики** в hello API управления меню слева hello, выберите нужный продукт hello и API и щелкните **Добавление политики**.</span><span class="sxs-lookup"><span data-stu-id="01acf-148">Click **Policies** in hello API Management menu on hello left, select hello desired product and API, and click **Add policy**.</span></span> <span data-ttu-id="01acf-149">В этом примере мы добавляем toohello политики **Echo API** в hello **неограниченное количество** продукта.</span><span class="sxs-lookup"><span data-stu-id="01acf-149">In this example we're adding a policy toohello **Echo API** in hello **Unlimited** product.</span></span>

![добавление политики;][add-policy]

<span data-ttu-id="01acf-151">Поместите курсор в hello `inbound` политики и нажмите кнопку hello **tooEventHub журнала** tooinsert hello политики `log-to-eventhub` инструкции шаблона политики.</span><span class="sxs-lookup"><span data-stu-id="01acf-151">Position your cursor in hello `inbound` policy section and click hello **Log tooEventHub** policy tooinsert hello `log-to-eventhub` policy statement template.</span></span>

![Редактор политики][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

<span data-ttu-id="01acf-153">Замените `logger-id` с именем hello API управления hello средства ведения журнала, настроенные в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="01acf-153">Replace `logger-id` with hello name of hello API Management logger you configured in hello previous step.</span></span>

<span data-ttu-id="01acf-154">Можно использовать любое выражение, возвращающее строку как значение hello для hello `log-to-eventhub` элемента.</span><span class="sxs-lookup"><span data-stu-id="01acf-154">You can use any expression that returns a string as hello value for hello `log-to-eventhub` element.</span></span> <span data-ttu-id="01acf-155">В этом примере регистрируется строка, содержащая hello даты и времени, имя службы, идентификатор запроса, запрос IP-адрес и имя операции.</span><span class="sxs-lookup"><span data-stu-id="01acf-155">In this example a string containing hello date and time, service name, request id, request ip address, and operation name is logged.</span></span>

<span data-ttu-id="01acf-156">Нажмите кнопку **Сохранить** toosave hello обновлена конфигурация политики.</span><span class="sxs-lookup"><span data-stu-id="01acf-156">Click **Save** toosave hello updated policy configuration.</span></span> <span data-ttu-id="01acf-157">Как только он сохраняется hello политика не активна, и события, зарегистрированного toohello назначенному концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="01acf-157">As soon as it is saved hello policy is active and events are logged toohello designated Event Hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01acf-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="01acf-158">Next steps</span></span>
* <span data-ttu-id="01acf-159">Дополнительная информация о концентраторах событий Azure</span><span class="sxs-lookup"><span data-stu-id="01acf-159">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="01acf-160">Приступая к работе с концентраторами событий Azure</span><span class="sxs-lookup"><span data-stu-id="01acf-160">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="01acf-161">Прием сообщений через EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="01acf-161">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="01acf-162">Руководство по программированию концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="01acf-162">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="01acf-163">Дополнительные сведения об интеграции службы управления API и концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="01acf-163">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="01acf-164">Справочник по сущности "Средство ведения журнала"</span><span class="sxs-lookup"><span data-stu-id="01acf-164">Logger entity reference</span></span>](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [<span data-ttu-id="01acf-165">Справочник по политике регистрации в концентраторе событий</span><span class="sxs-lookup"><span data-stu-id="01acf-165">log-to-eventhub policy reference</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [<span data-ttu-id="01acf-166">Мониторинг API-интерфейсов с помощью службы управления API Azure, концентраторов событий и Runscope</span><span class="sxs-lookup"><span data-stu-id="01acf-166">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a><span data-ttu-id="01acf-167">Просмотрите видеоруководство</span><span class="sxs-lookup"><span data-stu-id="01acf-167">Watch a video walkthrough</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Integrate-Azure-API-Management-with-Event-Hubs/player]
>
>

[publisher-portal]: ./media/api-management-howto-log-event-hubs/publisher-portal.png
[create-event-hub]: ./media/api-management-howto-log-event-hubs/create-event-hub.png
[event-hub-connection-string]: ./media/api-management-howto-log-event-hubs/event-hub-connection-string.png
[event-hub-dashboard]: ./media/api-management-howto-log-event-hubs/event-hub-dashboard.png
[receiving-policy]: ./media/api-management-howto-log-event-hubs/receiving-policy.png
[sending-policy]: ./media/api-management-howto-log-event-hubs/sending-policy.png
[event-hub-policy]: ./media/api-management-howto-log-event-hubs/event-hub-policy.png
[add-policy]: ./media/api-management-howto-log-event-hubs/add-policy.png
