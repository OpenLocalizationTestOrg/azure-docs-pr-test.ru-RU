---
title: "Как регистрировать события в концентраторах событий Azure в службе управления Azure API | Документация Майкрософт"
description: "Узнайте, как регистрировать события в концентраторах событий Azure в службе управления Azure API."
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
ms.openlocfilehash: a310236179677046ec49930b07cfdffdadc37974
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-log-events-to-azure-event-hubs-in-azure-api-management"></a><span data-ttu-id="f8151-103">Как регистрировать события в концентраторах событий Azure в службе управления Azure API</span><span class="sxs-lookup"><span data-stu-id="f8151-103">How to log events to Azure Event Hubs in Azure API Management</span></span>
<span data-ttu-id="f8151-104">Концентраторы событий Azure — это высокомасштабируемая служба приема данных, которая может обрабатывать миллионы событий в секунду, позволяя вам обрабатывать и анализировать огромное количество данных, создаваемых подключенными устройствами и приложениями.</span><span class="sxs-lookup"><span data-stu-id="f8151-104">Azure Event Hubs is a highly scalable data ingress service that can ingest millions of events per second so that you can process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="f8151-105">Концентраторы событий выступают в качестве "входной двери"для событий конвейера. После того как данные поступили в концентратор событий, они могут быть преобразованы и сохранены с использованием любого поставщика аналитики в режиме реального времени или адаптера пакетной обработки или хранения.</span><span class="sxs-lookup"><span data-stu-id="f8151-105">Event Hubs acts as the "front door" for an event pipeline, and once data is collected into an event hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="f8151-106">Концентраторы событий отделяют создание потока событий от потребления этих событий, чтобы потребители событий могли обращаться к событиям по собственному расписанию.</span><span class="sxs-lookup"><span data-stu-id="f8151-106">Event Hubs decouples the production of a stream of events from the consumption of those events, so that event consumers can access the events on their own schedule.</span></span>

<span data-ttu-id="f8151-107">Эта статья сопровождает видеоролик [Интеграция службы управления API Azure с концентраторами событий](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/). В ней рассматривается регистрация событий управления API с помощью концентраторов событий Azure.</span><span class="sxs-lookup"><span data-stu-id="f8151-107">This article is a companion to the [Integrate Azure API Management with Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video and describes how to log API Management events using Azure Event Hubs.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="f8151-108">Создание концентратора событий Azure</span><span class="sxs-lookup"><span data-stu-id="f8151-108">Create an Azure Event Hub</span></span>
<span data-ttu-id="f8151-109">Чтобы создать новый концентратор событий, войдите на [классический портал Azure](https://manage.windowsazure.com) и последовательно щелкните **Создать**->**Службы приложений**->**Служебная шина**->**Концентратор событий**->**Быстрое создание**.</span><span class="sxs-lookup"><span data-stu-id="f8151-109">To create a new Event Hub, sign-in to the [Azure classic portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Service Bus**->**Event Hub**->**Quick Create**.</span></span> <span data-ttu-id="f8151-110">Введите имя концентратора событий, регион, выберите подписку и пространство имен.</span><span class="sxs-lookup"><span data-stu-id="f8151-110">Enter an Event Hub name, region, select a subscription, and select a namespace.</span></span> <span data-ttu-id="f8151-111">Если пространство имен не было создано ранее, его можно создать, введя имя в текстовом поле **Пространство имен** .</span><span class="sxs-lookup"><span data-stu-id="f8151-111">If you haven't previously created a namespace you can create one by typing a name in the **Namespace** textbox.</span></span> <span data-ttu-id="f8151-112">После настройки всех свойств щелкните **Создать новый концентратор событий** , чтобы создать концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="f8151-112">Once all properties are configured, click **Create a new Event Hub** to create the Event Hub.</span></span>

![Создание концентратора событий][create-event-hub]

<span data-ttu-id="f8151-114">Затем перейдите на вкладку **Настройка**, связанную с новым концентратором событий, и создайте две **политики общего доступа**.</span><span class="sxs-lookup"><span data-stu-id="f8151-114">Next, navigate to the **Configure** tab for your new Event Hub and create two **shared access policies**.</span></span> <span data-ttu-id="f8151-115">Назовите первую **Отправка** и назначьте ей разрешения **Отправка**.</span><span class="sxs-lookup"><span data-stu-id="f8151-115">Name the first one **Sending** and give it **Send** permissions.</span></span>

![Политика «Отправка»][sending-policy]

<span data-ttu-id="f8151-117">Назовите вторую **Получение**, назначьте ей разрешения **Прослушивание** и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f8151-117">Name the second one **Receiving**, give it **Listen** permissions, and click **Save**.</span></span>

![Политика «Получение»][receiving-policy]

<span data-ttu-id="f8151-119">Каждая политика общего доступа позволяет приложениям отправлять события концентратору событий и получать их.</span><span class="sxs-lookup"><span data-stu-id="f8151-119">Each shared access policy allows applications to send and receive events to and from the Event Hub.</span></span> <span data-ttu-id="f8151-120">Чтобы получить доступ к строкам подключения для этих политик, перейдите на вкладку **Панель мониторинга** концентратора событий и щелкните **Сведения о подключении**.</span><span class="sxs-lookup"><span data-stu-id="f8151-120">To access the connection strings for these policies, navigate to the **Dashboard** tab of the Event Hub and click **Connection information**.</span></span>

![Строка подключения][event-hub-dashboard]

<span data-ttu-id="f8151-122">Строка подключения **Отправка** используется при регистрации событий, а строка подключения **Получение** — при загрузке событий из концентратора событий.</span><span class="sxs-lookup"><span data-stu-id="f8151-122">The **Sending** connection string is used when logging events, and the **Receiving** connection string is used when downloading events from the Event Hub.</span></span>

![Строка подключения][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a><span data-ttu-id="f8151-124">Создание средства ведения журнала для управления API</span><span class="sxs-lookup"><span data-stu-id="f8151-124">Create an API Management logger</span></span>
<span data-ttu-id="f8151-125">Теперь, когда концентратор событий создан, нужно настроить [средство ведения журнала](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) в службе управления API, которое сможет регистрировать события в концентраторе событий.</span><span class="sxs-lookup"><span data-stu-id="f8151-125">Now that you have an Event Hub, the next step is to configure a [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) in your API Management service so that it can log events to the Event Hub.</span></span>

<span data-ttu-id="f8151-126">Средства ведения журнала службы управления API настраиваются с помощью [REST API службы управления API](http://aka.ms/smapi).</span><span class="sxs-lookup"><span data-stu-id="f8151-126">API Management loggers are configured using the [API Management REST API](http://aka.ms/smapi).</span></span> <span data-ttu-id="f8151-127">Прежде чем использовать REST API впервые, просмотрите информацию о [необходимых компонентах](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) и убедитесь, что [включен доступ к REST API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span><span class="sxs-lookup"><span data-stu-id="f8151-127">Before using the REST API for the first time, review the [prerequisites](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) and ensure that you have [enabled access to the REST API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span></span>

<span data-ttu-id="f8151-128">Чтобы создать средство ведения журнала, выполните HTTP-запрос PUT, используя следующий шаблон URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="f8151-128">To create a logger, make an HTTP PUT request using the following URL template.</span></span>

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* <span data-ttu-id="f8151-129">Замените `{your service}` именем экземпляра службы управления API.</span><span class="sxs-lookup"><span data-stu-id="f8151-129">Replace `{your service}` with the name of your API Management service instance.</span></span>
* <span data-ttu-id="f8151-130">Замените `{new logger name}` требуемым именем нового средства ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="f8151-130">Replace `{new logger name}` with the desired name for your new logger.</span></span> <span data-ttu-id="f8151-131">Вы укажете это имя при настройке политики [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) (регистрация в концентраторе событий).</span><span class="sxs-lookup"><span data-stu-id="f8151-131">You will reference this name when you configure the [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) policy</span></span>

<span data-ttu-id="f8151-132">Добавьте в запрос следующие заголовки:</span><span class="sxs-lookup"><span data-stu-id="f8151-132">Add the following headers to the request.</span></span>

* <span data-ttu-id="f8151-133">тип содержимого: «application/json»;</span><span class="sxs-lookup"><span data-stu-id="f8151-133">Content-Type : application/json</span></span>
* <span data-ttu-id="f8151-134">авторизация: SharedAccessSignature 58...</span><span class="sxs-lookup"><span data-stu-id="f8151-134">Authorization : SharedAccessSignature 58...</span></span>
  * <span data-ttu-id="f8151-135">указания по созданию `SharedAccessSignature` см. в [справочнике по REST API Azure](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span><span class="sxs-lookup"><span data-stu-id="f8151-135">For instructions on generating the `SharedAccessSignature` see [Azure API Management REST API Authentication](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span></span>

<span data-ttu-id="f8151-136">Укажите текст запроса, используя следующий шаблон.</span><span class="sxs-lookup"><span data-stu-id="f8151-136">Specify the request body using the following template.</span></span>

```json
{
  "type" : "AzureEventHub",
  "description" : "Sample logger description",
  "credentials" : {
    "name" : "Name of the Event Hub from the Azure Classic Portal",
    "connectionString" : "Endpoint=Event Hub Sender connection string"
    }
}
```

* <span data-ttu-id="f8151-137">Для параметра `type` нужно задать значение `AzureEventHub`.</span><span class="sxs-lookup"><span data-stu-id="f8151-137">`type` must be set to `AzureEventHub`.</span></span>
* <span data-ttu-id="f8151-138">`description` предоставляет дополнительное описание средства ведения журнала. При желании эту строку можно оставить пустой.</span><span class="sxs-lookup"><span data-stu-id="f8151-138">`description` provides an optional description of the logger and can be a zero length string if desired.</span></span>
* <span data-ttu-id="f8151-139">`credentials` содержит `name` и `connectionString` концентратора событий Azure.</span><span class="sxs-lookup"><span data-stu-id="f8151-139">`credentials` contains the `name` and `connectionString` of your Azure Event Hub.</span></span>

<span data-ttu-id="f8151-140">Если при выполнении запроса средство ведения журнала создано, возвращается код состояния `201 Created` .</span><span class="sxs-lookup"><span data-stu-id="f8151-140">When you make the request, if the logger is created a status code of `201 Created` is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="f8151-141">Другие возможные коды возврата и их причины см. в статье, посвященной [созданию средств ведения журнала](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span><span class="sxs-lookup"><span data-stu-id="f8151-141">For other possible return codes and their reasons, see [Create a Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span></span> <span data-ttu-id="f8151-142">Чтобы узнать, как выполнять другие операции, такие как перечисление, обновление и удаление, см. документацию [средствах ведения журнала](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity).</span><span class="sxs-lookup"><span data-stu-id="f8151-142">To see how perform other operations such as list, update, and delete, see the [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) entity documentation.</span></span>
>
>

## <a name="configure-log-to-eventhubs-policies"></a><span data-ttu-id="f8151-143">Настройка политик регистрации в концентраторах событий</span><span class="sxs-lookup"><span data-stu-id="f8151-143">Configure log-to-eventhubs policies</span></span>
<span data-ttu-id="f8151-144">Если средство ведения журналов в управлении API уже настроено, вы можете настроить политики регистрации в концентраторах событий для регистрации нужных событий.</span><span class="sxs-lookup"><span data-stu-id="f8151-144">Once your logger is configured in API Management, you can configure your log-to-eventhubs policies to log the desired events.</span></span> <span data-ttu-id="f8151-145">Политику регистрации в концентраторах событий можно использовать в разделе входящей или исходящей политики.</span><span class="sxs-lookup"><span data-stu-id="f8151-145">The log-to-eventhubs policy can be used in either the inbound policy section or the outbound policy section.</span></span>

<span data-ttu-id="f8151-146">Чтобы настроить политики, войдите на [портал Azure](https://portal.azure.com), перейдите к службе управления API и щелкните **Publisher portal** (Портал издателя), чтобы получить доступ к порталу издателя.</span><span class="sxs-lookup"><span data-stu-id="f8151-146">To configure policies, sign-in to the [Azure portal](https://portal.azure.com), navigate to your API Management service, and click **Publisher portal** to access the publisher portal.</span></span>

![Портал издателя][publisher-portal]

<span data-ttu-id="f8151-148">В меню управления API слева щелкните **Политики**, выберите желаемый продукт и интерфейс API и щелкните **Добавить политику**.</span><span class="sxs-lookup"><span data-stu-id="f8151-148">Click **Policies** in the API Management menu on the left, select the desired product and API, and click **Add policy**.</span></span> <span data-ttu-id="f8151-149">В этом примере мы добавляем политику **Echo API** (API вывода на экран) в продукт **Unlimited**.</span><span class="sxs-lookup"><span data-stu-id="f8151-149">In this example we're adding a policy to the **Echo API** in the **Unlimited** product.</span></span>

![добавление политики;][add-policy]

<span data-ttu-id="f8151-151">Наведите указатель мыши на раздел политики `inbound` и щелкните политику **Регистрация в концентраторе событий**, чтобы вставить шаблон инструкции политики `log-to-eventhub`.</span><span class="sxs-lookup"><span data-stu-id="f8151-151">Position your cursor in the `inbound` policy section and click the **Log to EventHub** policy to insert the `log-to-eventhub` policy statement template.</span></span>

![Редактор политики][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

<span data-ttu-id="f8151-153">Замените `logger-id` именем средства ведения журнала службы управления API, настроенного на предыдущем этапе.</span><span class="sxs-lookup"><span data-stu-id="f8151-153">Replace `logger-id` with the name of the API Management logger you configured in the previous step.</span></span>

<span data-ttu-id="f8151-154">Вы можете использовать любое выражение, которое возвращает строку в качестве значения для элемента `log-to-eventhub` .</span><span class="sxs-lookup"><span data-stu-id="f8151-154">You can use any expression that returns a string as the value for the `log-to-eventhub` element.</span></span> <span data-ttu-id="f8151-155">В этом примере регистрируется строка, содержащая дату и время, имя службы, идентификатор запроса, IP-адрес запроса и имя операции.</span><span class="sxs-lookup"><span data-stu-id="f8151-155">In this example a string containing the date and time, service name, request id, request ip address, and operation name is logged.</span></span>

<span data-ttu-id="f8151-156">Нажмите кнопку **Сохранить** , чтобы сохранить конфигурацию обновленной политики.</span><span class="sxs-lookup"><span data-stu-id="f8151-156">Click **Save** to save the updated policy configuration.</span></span> <span data-ttu-id="f8151-157">Сразу же после сохранения политика становится активной, а события регистрируются в указанном концентраторе событий.</span><span class="sxs-lookup"><span data-stu-id="f8151-157">As soon as it is saved the policy is active and events are logged to the designated Event Hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8151-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f8151-158">Next steps</span></span>
* <span data-ttu-id="f8151-159">Дополнительная информация о концентраторах событий Azure</span><span class="sxs-lookup"><span data-stu-id="f8151-159">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="f8151-160">Приступая к работе с концентраторами событий Azure</span><span class="sxs-lookup"><span data-stu-id="f8151-160">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="f8151-161">Прием сообщений через EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="f8151-161">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="f8151-162">Руководство по программированию концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="f8151-162">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="f8151-163">Дополнительные сведения об интеграции службы управления API и концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="f8151-163">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="f8151-164">Справочник по сущности "Средство ведения журнала"</span><span class="sxs-lookup"><span data-stu-id="f8151-164">Logger entity reference</span></span>](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [<span data-ttu-id="f8151-165">Справочник по политике регистрации в концентраторе событий</span><span class="sxs-lookup"><span data-stu-id="f8151-165">log-to-eventhub policy reference</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [<span data-ttu-id="f8151-166">Мониторинг API-интерфейсов с помощью службы управления API Azure, концентраторов событий и Runscope</span><span class="sxs-lookup"><span data-stu-id="f8151-166">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a><span data-ttu-id="f8151-167">Просмотрите видеоруководство</span><span class="sxs-lookup"><span data-stu-id="f8151-167">Watch a video walkthrough</span></span>
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
