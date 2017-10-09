---
title: "конечные точки с портала Azure hello потоковой передачи aaaManage | Документы Microsoft"
description: "В этом разделе показано, как toomanage конечных точек потоковой передачи с hello портал Azure."
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
ms.openlocfilehash: dfa9352894d37edb317a6334d7f109419deb362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-hello-azure-portal"></a><span data-ttu-id="f97f6-103">Управление конечных точек потоковой передачи с hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="f97f6-103">Manage streaming endpoints with hello Azure portal</span></span>

<span data-ttu-id="f97f6-104">В этом разделе показано, как toouse hello Azure портала toomanage конечных точек потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="f97f6-104">This topic shows  how toouse hello Azure portal toomanage streaming endpoints.</span></span> 

>[!NOTE]
><span data-ttu-id="f97f6-105">Убедитесь, что hello tooreview [Обзор](media-services-streaming-endpoints-overview.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="f97f6-105">Make sure tooreview hello [overview](media-services-streaming-endpoints-overview.md) topic.</span></span> 

<span data-ttu-id="f97f6-106">Сведения о том, как tooscale hello конечной точки потоковой передачи см. в разделе [это](media-services-portal-scale-streaming-endpoints.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="f97f6-106">For information about how tooscale hello streaming endpoint, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <a name="start-managing-streaming-endpoints"></a><span data-ttu-id="f97f6-107">Как приступить к управлению конечными точками потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="f97f6-107">Start managing streaming endpoints</span></span> 

<span data-ttu-id="f97f6-108">Управление конечных точек потоковой передачи для вашей учетной записи toostart hello следующие.</span><span class="sxs-lookup"><span data-stu-id="f97f6-108">toostart managing streaming endpoints for your account, do hello following.</span></span>

1. <span data-ttu-id="f97f6-109">В hello [портал Azure](https://portal.azure.com/), выберите учетную запись служб мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="f97f6-109">In hello [Azure portal](https://portal.azure.com/), select your Azure Media Services account.</span></span>
2. <span data-ttu-id="f97f6-110">В hello **параметры** колонке выберите **конечные точки потоковой передачи**.</span><span class="sxs-lookup"><span data-stu-id="f97f6-110">In hello **Settings** blade, select **Streaming endpoints**.</span></span>
   
    ![конечной точки потоковой передачи](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> <span data-ttu-id="f97f6-112">Плата взимается, только когда конечная точка потоковой передачи используется.</span><span class="sxs-lookup"><span data-stu-id="f97f6-112">You are only billed when your Streaming Endpoint is in running state.</span></span>

## <a name="adddelete-a-streaming-endpoint"></a><span data-ttu-id="f97f6-113">Добавление или удаление конечной точки потоковой передачи</span><span class="sxs-lookup"><span data-stu-id="f97f6-113">Add/delete a streaming endpoint</span></span>

>[!NOTE]
><span data-ttu-id="f97f6-114">не удается удалить конечную точку потоковой передачи по умолчанию Hello.</span><span class="sxs-lookup"><span data-stu-id="f97f6-114">hello default streaming endpoint cannot be deleted.</span></span>

<span data-ttu-id="f97f6-115">Потоковая передача с помощью конечной точки tooadd или удаления Здравствуйте портал Azure, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="f97f6-115">tooadd/delete streaming endpoint using hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="f97f6-116">tooadd конечную точку потоковой передачи, нажмите кнопку hello **+ конечной точки** вверху hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="f97f6-116">tooadd a streaming endpoint, click hello **+ Endpoint** at hello top of hello page.</span></span> 

    <span data-ttu-id="f97f6-117">Вы можете несколько конечных точек потоковой передачи, если планируется toohave различных CDN или CDN и прямой доступ.</span><span class="sxs-lookup"><span data-stu-id="f97f6-117">You might want multiple Streaming Endpoints if you plan toohave different CDNs or a CDN and direct access.</span></span>

2. <span data-ttu-id="f97f6-118">Нажмите клавишу toodelete конечной точки потоковой передачи **удалить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="f97f6-118">toodelete a streaming endpoint, press **Delete** button.</span></span>      
3. <span data-ttu-id="f97f6-119">Нажмите кнопку hello **запустить** hello toostart кнопку конечной точки потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="f97f6-119">Click hello **Start** button toostart hello streaming endpoint.</span></span>
   
    ![конечной точки потоковой передачи](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <span data-ttu-id="f97f6-121"><a id="configure_streaming_endpoints"></a>Настройка конечной точки потоковой передачи hello</span><span class="sxs-lookup"><span data-stu-id="f97f6-121"><a id="configure_streaming_endpoints"></a>Configuring hello Streaming Endpoint</span></span>
<span data-ttu-id="f97f6-122">Конечная точка потоковой передачи обеспечивает hello tooconfigure следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="f97f6-122">Streaming Endpoint enables you tooconfigure hello following properties:</span></span>

* <span data-ttu-id="f97f6-123">управление доступом;</span><span class="sxs-lookup"><span data-stu-id="f97f6-123">Access control</span></span>
* <span data-ttu-id="f97f6-124">управление кэшем;</span><span class="sxs-lookup"><span data-stu-id="f97f6-124">Cache control</span></span>
* <span data-ttu-id="f97f6-125">межсайтовые политики доступа.</span><span class="sxs-lookup"><span data-stu-id="f97f6-125">Cross site access policies</span></span>

<span data-ttu-id="f97f6-126">Дополнительные сведения об этих свойствах см. [здесь](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span><span class="sxs-lookup"><span data-stu-id="f97f6-126">For detailed information about these properties, see [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).</span></span>

<span data-ttu-id="f97f6-127">Можно настроить конечную точку потоковой передачи, выполнив hello ниже:</span><span class="sxs-lookup"><span data-stu-id="f97f6-127">You can configure streaming endpoint by doing hello following:</span></span>

1. <span data-ttu-id="f97f6-128">Выберите hello требуется tooconfigure конечной точки потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="f97f6-128">Select hello streaming endpoint you want tooconfigure.</span></span>
2. <span data-ttu-id="f97f6-129">Щелкните **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="f97f6-129">Click **Settings**.</span></span>

<span data-ttu-id="f97f6-130">Краткое описание hello поля ниже.</span><span class="sxs-lookup"><span data-stu-id="f97f6-130">A brief description of hello fields follows.</span></span>

![конечной точки потоковой передачи](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. <span data-ttu-id="f97f6-132">Политика кэширования: используется tooconfigure время существования кэша для активов, обслуживаемых с помощью этой конечной точки потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="f97f6-132">Maximum cache policy: used tooconfigure cache lifetime for assets served through this streaming endpoint.</span></span> <span data-ttu-id="f97f6-133">Если значение не задано, используется по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="f97f6-133">If no value is set, hello default is used.</span></span> <span data-ttu-id="f97f6-134">значения по умолчанию Hello также можно создавать непосредственно в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="f97f6-134">hello default values can also be defined directly in Azure storage.</span></span> <span data-ttu-id="f97f6-135">Для hello конечной точки потоковой передачи включена Azure CDN, не устанавливайте сборки hello кэша политики значение более 600 секунд.</span><span class="sxs-lookup"><span data-stu-id="f97f6-135">If Azure CDN is enabled for hello streaming endpoint, you should not set hello cache policy value tooless than 600 seconds.</span></span>  
2. <span data-ttu-id="f97f6-136">Разрешенные IP-адреса: использовать toospecify IP-адресов, которые допустимы tooconnect toohello публикации конечной точки потоковой передачи.</span><span class="sxs-lookup"><span data-stu-id="f97f6-136">Allowed IP addresses: used toospecify IP addresses that would be allowed tooconnect toohello published streaming endpoint.</span></span> <span data-ttu-id="f97f6-137">Если IP-адреса не указано, любой IP-адрес будет может tooconnect.</span><span class="sxs-lookup"><span data-stu-id="f97f6-137">If no IP addresses specified, any IP address would be able tooconnect.</span></span> <span data-ttu-id="f97f6-138">Можно указать отдельный IP-адрес (например, 10.0.0.1) или диапазон IP-адресов, используя IP-адрес и маску подсети CIDR (например, 10.0.0.1/22) или IP-адрес и маску подсети с точками (например, 10.0.0.1(255.255.255.0)).</span><span class="sxs-lookup"><span data-stu-id="f97f6-138">IP addresses can be specified as either a single IP address (for example, '10.0.0.1'), an IP range using an IP address and a CIDR subnet mask (for example, '10.0.0.1/22'), or an IP range using IP address and a dotted decimal subnet mask (for example, '10.0.0.1(255.255.255.0)').</span></span>
3. <span data-ttu-id="f97f6-139">Конфигурация для проверки подлинности заголовка подписи Akamai: использовать toospecify, как настроен запрос проверки подлинности заголовка подписи от серверов Akamai.</span><span class="sxs-lookup"><span data-stu-id="f97f6-139">Configuration for Akamai signature header authentication: used toospecify how signature header authentication request from Akamai servers is configured.</span></span> <span data-ttu-id="f97f6-140">Срок действия указывается в формате UTC.</span><span class="sxs-lookup"><span data-stu-id="f97f6-140">Expiration is in UTC.</span></span>

## <a name="scale-your-premium-streaming-endpoint"></a><span data-ttu-id="f97f6-141">Масштабирование конечной точки потоковой передачи уровня "Премиум"</span><span class="sxs-lookup"><span data-stu-id="f97f6-141">Scale your Premium streaming endpoint</span></span>

<span data-ttu-id="f97f6-142">Чтобы узнать больше, ознакомьтесь с [этим](media-services-portal-scale-streaming-endpoints.md) разделом.</span><span class="sxs-lookup"><span data-stu-id="f97f6-142">For more information, see [this](media-services-portal-scale-streaming-endpoints.md) topic.</span></span>

## <span data-ttu-id="f97f6-143"><a id="enable_cdn"></a>Включение интеграции Azure CDN</span><span class="sxs-lookup"><span data-stu-id="f97f6-143"><a id="enable_cdn"></a>Enable Azure CDN integration</span></span>

<span data-ttu-id="f97f6-144">При создании учетной записи интеграция Azure CDN с конечной точкой потоковой передачи включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f97f6-144">When you create a new account, default Streaming Endpoint Azure CDN integration is enabled by default.</span></span>

<span data-ttu-id="f97f6-145">Если требуется более поздней версии hello toodisable Включение CDN, потоковой передачи конечной точки должны находиться в hello **остановлена** состояния.</span><span class="sxs-lookup"><span data-stu-id="f97f6-145">If you later want toodisable/enable hello CDN, your streaming endpoint must be in hello **stopped** state.</span></span> <span data-ttu-id="f97f6-146">Через все hello извлекает CDN может занять несколько часов too2 для hello Azure CDN integration tooget включен и toobe изменения hello active.</span><span class="sxs-lookup"><span data-stu-id="f97f6-146">It could take up too2 hours for hello Azure CDN integration tooget enabled and for hello changes toobe active across all hello CDN POPs.</span></span> <span data-ttu-id="f97f6-147">Тем не менее вы можете запустить ваш потоковой передачи конечной точки и потока без прерываний из hello конечной точки потоковой передачи и после завершения интеграции hello поток hello доставляется в от hello CDN.</span><span class="sxs-lookup"><span data-stu-id="f97f6-147">However, your can start your streaming endpoint and stream without interruptions from hello streaming endpoint and once hello integration is complete, hello stream will be delivered from hello CDN.</span></span> <span data-ttu-id="f97f6-148">Во время подготовки период hello вашей конечной точки потоковой передачи будет находиться в **запуск** состояния и вы заметите degredad производительности.</span><span class="sxs-lookup"><span data-stu-id="f97f6-148">During hello provisioning period your streaming endpoint will be in **starting** state and you might observe degredad performance.</span></span>

<span data-ttu-id="f97f6-149">Во всех execpt центрах обработки данных Azure hello Китае и областей федеральным Goverment включена интеграция CDN.</span><span class="sxs-lookup"><span data-stu-id="f97f6-149">CDN integration is enabled in all hello Azure data centers execpt China and Federal Goverment regions.</span></span>

<span data-ttu-id="f97f6-150">После включения hello **управления доступом**, **пользовательского имени узла** и **проверки подлинности подписи Akamai** конфигурация получает отключена.</span><span class="sxs-lookup"><span data-stu-id="f97f6-150">Once it is enabled, hello **Access Control**, **Custom hostname** and **Akamai Signature authentication** configuration gets disabled.</span></span>
 
> [!IMPORTANT]
> <span data-ttu-id="f97f6-151">Для конечных точек потоковой передачи уровня "Стандартный" интеграция служб мультимедиа Azure с Azure CDN реализуется на базе **Azure CDN от Verizon**.</span><span class="sxs-lookup"><span data-stu-id="f97f6-151">Azure Media Services integration with Azure CDN is implemented on **Azure CDN from Verizon** for standard streaming endpoints.</span></span> <span data-ttu-id="f97f6-152">Конечные точки потоковой передачи уровня "Премиум" можно настроить, используя все **ценовые категории и поставщики Azure CDN**.</span><span class="sxs-lookup"><span data-stu-id="f97f6-152">Premium streaming endpoints can be configured using all **Azure CDN pricing tiers and providers**.</span></span> <span data-ttu-id="f97f6-153">Дополнительные сведения о функциях Azure CDN см. в разделе hello [Обзор CDN](../cdn/cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f97f6-153">For more information about Azure CDN features, see hello [CDN overview](../cdn/cdn-overview.md).</span></span>
 
### <a name="additional-considerations"></a><span data-ttu-id="f97f6-154">Дополнительные замечания</span><span class="sxs-lookup"><span data-stu-id="f97f6-154">Additional considerations</span></span>

* <span data-ttu-id="f97f6-155">При включении CDN для конечной точки потоковой передачи клиентам не удается запросить содержимое непосредственно из источника hello.</span><span class="sxs-lookup"><span data-stu-id="f97f6-155">When CDN is enabled for a streaming endpoint, clients cannot request content directly from hello origin.</span></span> <span data-ttu-id="f97f6-156">Если требуется возможность tootest hello контент с или без CDN, можно создать другой конечной точки потоковой передачи, не включена CDN.</span><span class="sxs-lookup"><span data-stu-id="f97f6-156">If you need hello ability tootest your content with or without CDN, you can create another streaming endpoint that isn't CDN enabled.</span></span>
* <span data-ttu-id="f97f6-157">Ваш потоковой передачи остается имя узла конечной точки hello же после включения CDN.</span><span class="sxs-lookup"><span data-stu-id="f97f6-157">Your streaming endpoint hostname remains hello same after enabling CDN.</span></span> <span data-ttu-id="f97f6-158">Не нужно toomake любой рабочий процесс изменения tooyour media services после включения CDN.</span><span class="sxs-lookup"><span data-stu-id="f97f6-158">You don’t need toomake any changes tooyour media services workflow after CDN is enabled.</span></span> <span data-ttu-id="f97f6-159">Например если ваш потоковой передачи узла конечной точки, strasbourg.streaming.mediaservices.windows.net, после включения CDN используется hello точно того же имени узла.</span><span class="sxs-lookup"><span data-stu-id="f97f6-159">For example, if your streaming endpoint hostname is strasbourg.streaming.mediaservices.windows.net, after enabling CDN, hello exact same hostname is used.</span></span>
* <span data-ttu-id="f97f6-160">Для новых конечных точек потоковой передачи можно включить CDN просто путем создания новой конечной точки; для существующих конечных точек потоковой передачи необходимо toofirst stop hello endpoint, а затем включить или отключить hello CDN.</span><span class="sxs-lookup"><span data-stu-id="f97f6-160">For new streaming endpoints, you can enable CDN simply by creating a new endpoint; for existing streaming endpoints, you need toofirst stop hello endpoint and then enable/disable hello CDN.</span></span>
* <span data-ttu-id="f97f6-161">Конечную точку потоковой передачи уровня "Стандартный" можно настроить только с помощью **поставщика CDN уровня "Стандартный" от Verizon** на портале управления Azure.</span><span class="sxs-lookup"><span data-stu-id="f97f6-161">Standard streaming endpoint can only be configured using **Verizon Standard CDN provider** using Azure management portal.</span></span> <span data-ttu-id="f97f6-162">Тем не менее вы можете включить другие поставщики Azure CDN с помощью REST API.</span><span class="sxs-lookup"><span data-stu-id="f97f6-162">However, you can enable other Azure CDN providers using REST APIs.</span></span>

## <a name="configure-cdn-profile"></a><span data-ttu-id="f97f6-163">Настройка профиля CDN</span><span class="sxs-lookup"><span data-stu-id="f97f6-163">Configure CDN profile</span></span>

<span data-ttu-id="f97f6-164">Можно настроить профиль CDN hello, выбрав hello **управление CDN** кнопку сверху hello.</span><span class="sxs-lookup"><span data-stu-id="f97f6-164">You can configure hello CDN profile by selecting hello **Manage CDN** button from hello top.</span></span>

![конечной точки потоковой передачи](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a><span data-ttu-id="f97f6-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f97f6-166">Next steps</span></span>
<span data-ttu-id="f97f6-167">Просмотрите схемы обучения работе со службами мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="f97f6-167">Review Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f97f6-168">Отзывы</span><span class="sxs-lookup"><span data-stu-id="f97f6-168">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

