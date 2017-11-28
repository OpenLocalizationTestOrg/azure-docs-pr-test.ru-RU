---
title: "Управление конечными точками потоковой передачи с помощью портала Azure | Документация Майкрософт"
description: "В этой статье рассказывается, как управлять конечными точками потоковой передачи с помощью портала Azure."
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: bb1aca25-d23a-4520-8c45-44ef3ecd5371
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 797dced6c3e2525730afa29987259cb9b435ba66
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="manage-streaming-endpoints-with-the-azure-portal"></a><span data-ttu-id="b7b0f-103">Управление конечными точками потоковой передачи с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="b7b0f-103">Manage streaming endpoints with the Azure portal</span></span>

<span data-ttu-id="b7b0f-104">Здесь показано, как использовать портал Azure для управления конечными точками потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-104">This topic shows  how to use the Azure portal to manage streaming endpoints.</span></span> 

>[!NOTE]
><span data-ttu-id="b7b0f-105">Обязательно просмотрите [обзорную статью](media-services-streaming-endpoints-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b7b0f-105">Make sure to review the [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> 

<span data-ttu-id="b7b0f-106">Сведения о том, как масштабировать конечную точку потоковой передачи, см. [здесь](media-services-portal-scale-streaming-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="b7b0f-106">For information about how to scale the streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="start-managing-streaming-endpoints"></a><span data-ttu-id="b7b0f-107">Как приступить к управлению конечными точками потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="b7b0f-107">Start managing streaming endpoints</span></span> 

<span data-ttu-id="b7b0f-108">Чтобы приступить к управлению конечными точками потоковой передачи для своей учетной записи, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-108">To start managing streaming endpoints for your account, do the following.</span></span>

1. <span data-ttu-id="b7b0f-109">Создание учетной записи служб мультимедиа Azure с помощью [портала Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b7b0f-109">In the [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="b7b0f-110">В колонке **Параметры** щелкните **Конечные точки потоковой передачи**.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-110">In the **Settings** blade, select **Streaming endpoints**.</span></span>
   
    ![конечной точки потоковой передачи](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> <span data-ttu-id="b7b0f-112">Плата взимается, только когда конечная точка потоковой передачи используется.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-112">You are only billed when your Streaming Endpoint is in running state.</span></span>

## <a name="adddelete-a-streaming-endpoint"></a><span data-ttu-id="b7b0f-113">Добавление или удаление конечной точки потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="b7b0f-113">Add/delete a streaming endpoint</span></span>

>[!NOTE]
><span data-ttu-id="b7b0f-114">Конечную точку потоковой передачи по умолчанию удалить нельзя.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-114">The default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="b7b0f-115">Чтобы добавить или удалить конечную точку потоковой передачи с помощью портала Azure, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-115">To add/delete streaming endpoint using the Azure portal, do the following:</span></span>

1. <span data-ttu-id="b7b0f-116">Чтобы добавить конечную точку потоковой передачи, щелкните **+ Endpoint** (+ Конечная точка) в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-116">To add a streaming endpoint, click the **+ Endpoint** at the top of the page.</span></span> 

    <span data-ttu-id="b7b0f-117">Может потребоваться несколько конечных точек потоковой передачи, если вы планируете использовать разные сети CDN (или сеть CDN) и прямой доступ.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-117">You might want multiple Streaming Endpoints if you plan to have different CDNs or a CDN and direct access.</span></span>

2. <span data-ttu-id="b7b0f-118">Чтобы удалить конечную точку потоковой передачи, нажмите кнопку **Удалить** .</span><span class="sxs-lookup"><span data-stu-id="b7b0f-118">To delete a streaming endpoint, press **Delete** button.</span></span>      
3. <span data-ttu-id="b7b0f-119">Нажмите кнопку **Запуск** для запуска конечной точки.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-119">Click the **Start** button to start the streaming endpoint.</span></span>
   
    ![конечной точки потоковой передачи](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <span data-ttu-id="b7b0f-121"><a id="configure_streaming_endpoints"></a>Настройка конечной точки потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="b7b0f-121"><a id="configure_streaming_endpoints"></a>Configuring the Streaming Endpoint</span></span>
<span data-ttu-id="b7b0f-122">Конечная точка потоковой передачи позволяет настроить следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="b7b0f-122">Streaming Endpoint enables you to configure the following properties:</span></span>

* <span data-ttu-id="b7b0f-123">управление доступом;</span><span class="sxs-lookup"><span data-stu-id="b7b0f-123">Access control</span></span>
* <span data-ttu-id="b7b0f-124">управление кэшем;</span><span class="sxs-lookup"><span data-stu-id="b7b0f-124">Cache control</span></span>
* <span data-ttu-id="b7b0f-125">межсайтовые политики доступа.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-125">Cross site access policies</span></span>

<span data-ttu-id="b7b0f-126">Дополнительные сведения об этих свойствах см. [здесь](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="b7b0f-126">For detailed information about these properties, see [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="b7b0f-127">Конечную точку потоковой передачи можно настроить следующим образом.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-127">You can configure streaming endpoint by doing the following:</span></span>

1. <span data-ttu-id="b7b0f-128">Выберите конечную точку потоковой передачи, которую хотите настроить.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-128">Select the streaming endpoint you want to configure.</span></span>
2. <span data-ttu-id="b7b0f-129">Щелкните **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-129">Click **Settings**.</span></span>

<span data-ttu-id="b7b0f-130">Далее представлено краткое описание полей.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-130">A brief description of the fields follows.</span></span>

![конечная точка потоковой передачи](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. <span data-ttu-id="b7b0f-132">Политика максимального размера кэша используется для настройки времени существования кэша для ресурсов-контейнеров, обслуживаемых данной конечной точкой потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-132">Maximum cache policy: used to configure cache lifetime for assets served through this streaming endpoint.</span></span> <span data-ttu-id="b7b0f-133">Если значение не задано, то используется значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-133">If no value is set, the default is used.</span></span> <span data-ttu-id="b7b0f-134">Значения по умолчанию можно также задать непосредственно в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-134">The default values can also be defined directly in Azure storage.</span></span> <span data-ttu-id="b7b0f-135">Если для конечной точки потоковой передачи включена сеть Azure CDN, то не следует задавать значение политики кэша менее 600 секунд.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-135">If Azure CDN is enabled for the streaming endpoint, you should not set the cache policy value to less than 600 seconds.</span></span>  
2. <span data-ttu-id="b7b0f-136">С помощью поля разрешенных IP-адресов можно указать IP-адреса, которым будет разрешено подключение к опубликованной конечной точке потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-136">Allowed IP addresses: used to specify IP addresses that would be allowed to connect to the published streaming endpoint.</span></span> <span data-ttu-id="b7b0f-137">Если IP-адреса не указаны, можно подключаться с любого IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-137">If no IP addresses specified, any IP address would be able to connect.</span></span> <span data-ttu-id="b7b0f-138">Можно указать отдельный IP-адрес (например, 10.0.0.1) или диапазон IP-адресов, используя IP-адрес и маску подсети CIDR (например, 10.0.0.1/22) или IP-адрес и маску подсети с точками (например, 10.0.0.1(255.255.255.0)).</span><span class="sxs-lookup"><span data-stu-id="b7b0f-138">IP addresses can be specified as either a single IP address (for example, '10.0.0.1'), an IP range using an IP address and a CIDR subnet mask (for example, '10.0.0.1/22'), or an IP range using IP address and a dotted decimal subnet mask (for example, '10.0.0.1(255.255.255.0)').</span></span>
3. <span data-ttu-id="b7b0f-139">Конфигурация для аутентификации заголовка подписи Akamai используется, чтобы указать, как настроен запрос аутентификации заголовка подписи от серверов Akamai.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-139">Configuration for Akamai signature header authentication: used to specify how signature header authentication request from Akamai servers is configured.</span></span> <span data-ttu-id="b7b0f-140">Срок действия указывается в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-140">Expiration is in UTC.</span></span>

## <a name="scale-your-premium-streaming-endpoint"></a><span data-ttu-id="b7b0f-141">Масштабирование конечной точки потоковой передачи уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="b7b0f-141">Scale your Premium streaming endpoint</span></span>

<span data-ttu-id="b7b0f-142">Чтобы узнать больше, ознакомьтесь с [этим](media-services-portal-scale-streaming-endpoints.md) разделом.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-142">For more information, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <span data-ttu-id="b7b0f-143"><a id="enable_cdn"></a>Включение интеграции Azure CDN</span><span class="sxs-lookup"><span data-stu-id="b7b0f-143"><a id="enable_cdn"></a>Enable Azure CDN integration</span></span>

<span data-ttu-id="b7b0f-144">При создании учетной записи интеграция Azure CDN с конечной точкой потоковой передачи включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-144">When you create a new account, default Streaming Endpoint Azure CDN integration is enabled by default.</span></span>

<span data-ttu-id="b7b0f-145">Если позже вы захотите отключить или включить CDN, конечную точку потоковой передачи нужно перевести в состояние **Остановлена**.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-145">If you later want to disable/enable the CDN, your streaming endpoint must be in the **stopped** state.</span></span> <span data-ttu-id="b7b0f-146">Включение интеграции Azure CDN и активация изменений по всем расположениям POP CDN может занять до двух часов.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-146">It could take up to 2 hours for the Azure CDN integration to get enabled and for the changes to be active across all the CDN POPs.</span></span> <span data-ttu-id="b7b0f-147">Тем не менее вы можете запустить конечную точку потоковой передачи и поток из нее без прерываний. После завершения интеграции поток будет доставлен из сети CDN.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-147">However, your can start your streaming endpoint and stream without interruptions from the streaming endpoint and once the integration is complete, the stream will be delivered from the CDN.</span></span> <span data-ttu-id="b7b0f-148">Во время подготовки конечная точка потоковой передачи перейдет в состояние **Запуск**, и вы можете заметить снижение производительности.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-148">During the provisioning period your streaming endpoint will be in **starting** state and you might observe degredad performance.</span></span>

<span data-ttu-id="b7b0f-149">Интеграция CDN включена во всех центрах обработки данных Azure, за исключением Китая и регионов федерального правительства США.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-149">CDN integration is enabled in all the Azure data centers execpt China and Federal Goverment regions.</span></span>

<span data-ttu-id="b7b0f-150">После ее включения отключается конфигурация **контроля доступа**, **пользовательского имени узла** и **аутентификации с помощью подписи Akamai**.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-150">Once it is enabled, the **Access Control**, **Custom hostname** and **Akamai Signature authentication** configuration gets disabled.</span></span>
 
> [!IMPORTANT]
> <span data-ttu-id="b7b0f-151">Для конечных точек потоковой передачи уровня "Стандартный" интеграция служб мультимедиа Azure с Azure CDN реализуется на базе **Azure CDN от Verizon**.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-151">Azure Media Services integration with Azure CDN is implemented on **Azure CDN from Verizon** for standard streaming endpoints.</span></span> <span data-ttu-id="b7b0f-152">Конечные точки потоковой передачи уровня "Премиум" можно настроить, используя все **ценовые категории и поставщики Azure CDN**.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-152">Premium streaming endpoints can be configured using all **Azure CDN pricing tiers and providers**.</span></span> <span data-ttu-id="b7b0f-153">Дополнительные сведения о возможностях Azure CDN см. в [этом обзоре](../cdn/cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b7b0f-153">For more information about Azure CDN features, see the [CDN overview](../cdn/cdn-overview.md).</span></span>
 
### <a name="additional-considerations"></a><span data-ttu-id="b7b0f-154">Дополнительные замечания</span><span class="sxs-lookup"><span data-stu-id="b7b0f-154">Additional considerations</span></span>

* <span data-ttu-id="b7b0f-155">При включении CDN для конечной точки потоковой передачи клиенты не могут запрашивать содержимое непосредственно из источника.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-155">When CDN is enabled for a streaming endpoint, clients cannot request content directly from the origin.</span></span> <span data-ttu-id="b7b0f-156">Если требуется возможность проверки содержимого с CDN или без нее, то можно создать другую конечную точку потоковой передачи, для которой не включена CDN.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-156">If you need the ability to test your content with or without CDN, you can create another streaming endpoint that isn't CDN enabled.</span></span>
* <span data-ttu-id="b7b0f-157">Имя узла конечной точки потоковой передачи после включения CDN остается таким же.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-157">Your streaming endpoint hostname remains the same after enabling CDN.</span></span> <span data-ttu-id="b7b0f-158">После включения CDN не требуется вносить никакие изменения в рабочий процесс служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-158">You don’t need to make any changes to your media services workflow after CDN is enabled.</span></span> <span data-ttu-id="b7b0f-159">Например, если имя узла конечной точки потоковой передачи — strasbourg.streaming.mediaservices.windows.net, после включения CDN будет использоваться точно такое же имя узла.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-159">For example, if your streaming endpoint hostname is strasbourg.streaming.mediaservices.windows.net, after enabling CDN, the exact same hostname is used.</span></span>
* <span data-ttu-id="b7b0f-160">Для новых конечных точек потоковой передачи можно включить CDN, просто создавая новые конечные точки. Для имеющихся конечных точек потоковой передачи необходимо сначала остановить конечную точку, а затем включить или отключить CDN.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-160">For new streaming endpoints, you can enable CDN simply by creating a new endpoint; for existing streaming endpoints, you need to first stop the endpoint and then enable/disable the CDN.</span></span>
* <span data-ttu-id="b7b0f-161">Конечную точку потоковой передачи уровня "Стандартный" можно настроить только с помощью **поставщика CDN уровня "Стандартный" от Verizon** на портале управления Azure.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-161">Standard streaming endpoint can only be configured using **Verizon Standard CDN provider** using Azure management portal.</span></span> <span data-ttu-id="b7b0f-162">Тем не менее вы можете включить другие поставщики Azure CDN с помощью REST API.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-162">However, you can enable other Azure CDN providers using REST APIs.</span></span>

## <a name="configure-cdn-profile"></a><span data-ttu-id="b7b0f-163">Настройка профиля CDN</span><span class="sxs-lookup"><span data-stu-id="b7b0f-163">Configure CDN profile</span></span>

<span data-ttu-id="b7b0f-164">Вы можете настроить профиль CDN, нажав кнопку **Управление CDN** в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-164">You can configure the CDN profile by selecting the **Manage CDN** button from the top.</span></span>

![конечной точки потоковой передачи](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a><span data-ttu-id="b7b0f-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b7b0f-166">Next steps</span></span>
<span data-ttu-id="b7b0f-167">Просмотрите схемы обучения работе со службами мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="b7b0f-167">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b7b0f-168">Отзывы</span><span class="sxs-lookup"><span data-stu-id="b7b0f-168">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

