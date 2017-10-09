---
title: "aaaGetting к работе с Azure CDN | Документы Microsoft"
description: "В этом разделе показано, как tooenable hello Azure доставки содержимого сети (CDN). Hello учебника вы научитесь hello Создание нового профиля CDN и конечной точки."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 4ca51224-5423-419b-98cf-89860ef516d2
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0ce9802bfd7b60e70a9a62330f5593fc17ea07d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-cdn"></a><span data-ttu-id="4e120-104">Начало работы с Azure CDN</span><span class="sxs-lookup"><span data-stu-id="4e120-104">Getting started with Azure CDN</span></span>
<span data-ttu-id="4e120-105">В этой статье объясняется, как включить Azure CDN, создав новый профиль и конечную точку CDN.</span><span class="sxs-lookup"><span data-stu-id="4e120-105">This topic walks through enabling Azure CDN by creating a new CDN profile and endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4e120-106">Введение toohow CDN работает, а также список функций, в разделе hello [Обзор CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4e120-106">For an introduction toohow CDN works, as well as a list of features, see hello [CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="4e120-107">Создание нового профиля сети CDN</span><span class="sxs-lookup"><span data-stu-id="4e120-107">Create a new CDN profile</span></span>
<span data-ttu-id="4e120-108">Профиль сети CDN представляет собой коллекцию конечных точек сети CDN.</span><span class="sxs-lookup"><span data-stu-id="4e120-108">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="4e120-109">Каждый профиль содержит одну или несколько конечных точек сети CDN.</span><span class="sxs-lookup"><span data-stu-id="4e120-109">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="4e120-110">Вы можете toouse несколько профилей tooorganize конечными точками CDN с Интернет-домен, веб-приложения или некоторых других критериев.</span><span class="sxs-lookup"><span data-stu-id="4e120-110">You may wish toouse multiple profiles tooorganize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!NOTE]
> <span data-ttu-id="4e120-111">По умолчанию одной подписки Azure является ограниченной tooeight CDN профилей.</span><span class="sxs-lookup"><span data-stu-id="4e120-111">By default, a single Azure subscription is limited tooeight CDN profiles.</span></span> <span data-ttu-id="4e120-112">Каждый профиль CDN является ограниченной tooten конечных точек CDN.</span><span class="sxs-lookup"><span data-stu-id="4e120-112">Each CDN profile is limited tooten CDN endpoints.</span></span>
> 
> <span data-ttu-id="4e120-113">Цены CDN применяется на уровне профиля CDN hello.</span><span class="sxs-lookup"><span data-stu-id="4e120-113">CDN pricing is applied at hello CDN profile level.</span></span> <span data-ttu-id="4e120-114">Если вы хотите toouse сочетание Azure CDN ценовым категориям, потребуется несколько профилей CDN.</span><span class="sxs-lookup"><span data-stu-id="4e120-114">If you wish toouse a mix of Azure CDN pricing tiers, you will need multiple CDN profiles.</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="4e120-115">Создание новой конечной точки сети CDN</span><span class="sxs-lookup"><span data-stu-id="4e120-115">Create a new CDN endpoint</span></span>
<span data-ttu-id="4e120-116">**toocreate новой конечной точки CDN**</span><span class="sxs-lookup"><span data-stu-id="4e120-116">**toocreate a new CDN endpoint**</span></span>

1. <span data-ttu-id="4e120-117">В hello [портала Azure](https://portal.azure.com), перейдите tooyour профиля CDN.</span><span class="sxs-lookup"><span data-stu-id="4e120-117">In hello [Azure Portal](https://portal.azure.com), navigate tooyour CDN profile.</span></span>  <span data-ttu-id="4e120-118">Может закрепленной его toohello панели мониторинга в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="4e120-118">You may have pinned it toohello dashboard in hello previous step.</span></span>  <span data-ttu-id="4e120-119">Если вы не, можно найти его, нажав кнопку **Обзор**, затем **CDN профилей**, и щелкнув профиля hello планируется tooadd для конечной точки.</span><span class="sxs-lookup"><span data-stu-id="4e120-119">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on hello profile you plan tooadd your endpoint to.</span></span>
   
    <span data-ttu-id="4e120-120">Откроется колонка профиля CDN Hello.</span><span class="sxs-lookup"><span data-stu-id="4e120-120">hello CDN profile blade appears.</span></span>
   
    ![Профиль сети CDN][cdn-profile-settings]
2. <span data-ttu-id="4e120-122">Нажмите кнопку hello **добавить конечную точку** кнопки.</span><span class="sxs-lookup"><span data-stu-id="4e120-122">Click hello **Add Endpoint** button.</span></span>
   
    ![Кнопка "Добавить конечную точку"][cdn-new-endpoint-button]
   
    <span data-ttu-id="4e120-124">Hello **добавить конечную точку** колонке отображается.</span><span class="sxs-lookup"><span data-stu-id="4e120-124">hello **Add an endpoint** blade appears.</span></span>
   
    ![Колонка "Добавление конечной точки"][cdn-add-endpoint]
3. <span data-ttu-id="4e120-126">Введите **имя** конечной точки сети CDN.</span><span class="sxs-lookup"><span data-stu-id="4e120-126">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="4e120-127">Это имя будет использоваться tooaccess кэшированные ресурсы в домене hello `<endpointname>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="4e120-127">This name will be used tooaccess your cached resources at hello domain `<endpointname>.azureedge.net`.</span></span>
4. <span data-ttu-id="4e120-128">В hello **тип источника** раскрывающийся список, выберите тип источника.</span><span class="sxs-lookup"><span data-stu-id="4e120-128">In hello **Origin type** dropdown, select your origin type.</span></span>  <span data-ttu-id="4e120-129">Выберите **Служба хранилища** для учетной записи хранения Azure, **Облачная служба** для облачной службы Azure, **Веб-приложение** для веб-приложения Azure или **Настраиваемый источник** для любого другого общедоступного источника на веб-сервере (размещенного в Azure или в другом месте).</span><span class="sxs-lookup"><span data-stu-id="4e120-129">Select **Storage** for an Azure Storage account, **Cloud service** for an Azure Cloud Service, **Web App** for an Azure Web App, or **Custom origin** for any other publicly accessible web server origin (hosted in Azure or elsewhere).</span></span>
   
    ![Тип источника CDN](./media/cdn-create-new-endpoint/cdn-origin-type.png)
5. <span data-ttu-id="4e120-131">В hello **имя узла источника** раскрывающийся список, выберите или введите ваш исходный домен.</span><span class="sxs-lookup"><span data-stu-id="4e120-131">In hello **Origin hostname** dropdown, select or type your origin domain.</span></span>  <span data-ttu-id="4e120-132">Hello раскрывающемся списке будут перечислены все доступные источники hello типа, указанного на шаге 4.</span><span class="sxs-lookup"><span data-stu-id="4e120-132">hello dropdown will list all available origins of hello type you specified in step 4.</span></span>  <span data-ttu-id="4e120-133">Если вы выбрали *пользовательский источник* как ваш **тип источника**, вводе hello домен вашей настраиваемого источника.</span><span class="sxs-lookup"><span data-stu-id="4e120-133">If you selected *Custom origin* as your **Origin type**, you will type in hello domain of your custom origin.</span></span>
6. <span data-ttu-id="4e120-134">В hello **исходный путь** текста введите hello путь toohello ресурсов, toocache или оставьте пустым tooallow кэша любые ресурсы на hello домена, указанный на шаге 5.</span><span class="sxs-lookup"><span data-stu-id="4e120-134">In hello **Origin path** text box, enter hello path toohello resources you want toocache, or leave blank tooallow cache any resource at hello domain you specified in step 5.</span></span>
7. <span data-ttu-id="4e120-135">В hello **заголовок исходного узла**введите заголовок узла hello требуется hello toosend CDN с каждым запросом, или оставьте по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="4e120-135">In hello **Origin host header**, enter hello host header you want hello CDN toosend with each request, or leave hello default.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="4e120-136">Некоторые типы источников, таких как хранилище Azure и веб-приложениям, потребует домена hello узла заголовок toomatch hello происхождения hello.</span><span class="sxs-lookup"><span data-stu-id="4e120-136">Some types of origins, such as Azure Storage and Web Apps, require hello host header toomatch hello domain of hello origin.</span></span> <span data-ttu-id="4e120-137">При отсутствии источника, требующий заголовок узла, отличается от домена, следует оставить значение по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="4e120-137">Unless you have an origin that requires a host header different from its domain, you should leave hello default value.</span></span>
   > 
   > 
8. <span data-ttu-id="4e120-138">Для **протокола** и **порта источника**укажите hello протоколы и порты tooaccess используемые ресурсы в hello начала координат.</span><span class="sxs-lookup"><span data-stu-id="4e120-138">For **Protocol** and **Origin port**, specify hello protocols and ports used tooaccess your resources at hello origin.</span></span>  <span data-ttu-id="4e120-139">Необходимо указать хотя бы один протокол (HTTP или HTTPS).</span><span class="sxs-lookup"><span data-stu-id="4e120-139">At least one protocol (HTTP or HTTPS) must be selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4e120-140">Hello **порта источника** влияет только на какие hello порта конечной точки использует tooretrieve информацию из источника hello.</span><span class="sxs-lookup"><span data-stu-id="4e120-140">hello **Origin port** only affects what port hello endpoint uses tooretrieve information from hello origin.</span></span>  <span data-ttu-id="4e120-141">Hello конечной точки, сам только будет доступен tooend клиентов на hello по умолчанию порты HTTP и HTTPS (80 и 443), независимо от того, hello **порта источника**.</span><span class="sxs-lookup"><span data-stu-id="4e120-141">hello endpoint itself will only be available tooend clients on hello default HTTP and HTTPS ports (80 and 443), regardless of hello **Origin port**.</span></span>  
   > 
   > <span data-ttu-id="4e120-142">**Azure CDN с Akamai** конечные точки не допускают hello полного диапазона TCP-портов для источников.</span><span class="sxs-lookup"><span data-stu-id="4e120-142">**Azure CDN from Akamai** endpoints do not allow hello full TCP port range for origins.</span></span>  <span data-ttu-id="4e120-143">Список запрещенных портов источников см. в статье о [разрешенных портах источников Azure CDN от Akamai](https://msdn.microsoft.com/library/mt757337.aspx).</span><span class="sxs-lookup"><span data-stu-id="4e120-143">For a list of origin ports that are not allowed, see [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx).</span></span>  
   > 
   > <span data-ttu-id="4e120-144">Доступ к CDN содержимое с использованием HTTPS имеет hello следующие ограничения:</span><span class="sxs-lookup"><span data-stu-id="4e120-144">Accessing CDN content using HTTPS has hello following constraints:</span></span>
   > 
   > * <span data-ttu-id="4e120-145">Необходимо использовать SSL-сертификат hello, предоставляемые hello CDN.</span><span class="sxs-lookup"><span data-stu-id="4e120-145">You must use hello SSL certificate provided by hello CDN.</span></span> <span data-ttu-id="4e120-146">Сертификаты третьих сторон не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="4e120-146">Third party certificates are not supported.</span></span>
   > * <span data-ttu-id="4e120-147">Необходимо использовать домен CDN техники hello (`<endpointname>.azureedge.net`) содержимое tooaccess HTTPS.</span><span class="sxs-lookup"><span data-stu-id="4e120-147">You must use hello CDN-provided domain (`<endpointname>.azureedge.net`) tooaccess HTTPS content.</span></span> <span data-ttu-id="4e120-148">Поддержка HTTPS недоступна для пользовательских имен домена (CNAME), поскольку hello CDN не поддерживает пользовательские сертификаты в данный момент.</span><span class="sxs-lookup"><span data-stu-id="4e120-148">HTTPS support is not available for custom domain names (CNAMEs) since hello CDN does not support custom certificates at this time.</span></span>
   > 
   > 
9. <span data-ttu-id="4e120-149">Нажмите кнопку hello **добавить** toocreate кнопку hello новой конечной точки.</span><span class="sxs-lookup"><span data-stu-id="4e120-149">Click hello **Add** button toocreate hello new endpoint.</span></span>
10. <span data-ttu-id="4e120-150">После создания конечной точки hello, он отображается в списке конечных точек для профиля hello.</span><span class="sxs-lookup"><span data-stu-id="4e120-150">Once hello endpoint is created, it appears in a list of endpoints for hello profile.</span></span> <span data-ttu-id="4e120-151">представления списка Hello показывает, что tooaccess toouse hello URL-адрес в кэше содержимого, а также hello исходный домен.</span><span class="sxs-lookup"><span data-stu-id="4e120-151">hello list view shows hello URL toouse tooaccess cached content, as well as hello origin domain.</span></span>
    
    ![Конечная точка сети CDN][cdn-endpoint-success]
    
    > [!IMPORTANT]
    > <span data-ttu-id="4e120-153">Конечная точка Hello будет недоступен немедленно для использования, сколько потребуется времени для hello toopropagate регистрации через hello CDN.</span><span class="sxs-lookup"><span data-stu-id="4e120-153">hello endpoint will not immediately be available for use, as it takes time for hello registration toopropagate through hello CDN.</span></span>  <span data-ttu-id="4e120-154">Для профилей <b>Azure CDN от Akamai</b> распространение обычно занимает не более минуты.</span><span class="sxs-lookup"><span data-stu-id="4e120-154">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="4e120-155">Для профилей <b>Azure CDN от Verizon</b> распространение обычно завершается в течение 90 минут, но в некоторых случаях может занимать больше времени.</span><span class="sxs-lookup"><span data-stu-id="4e120-155">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
    > 
    > <span data-ttu-id="4e120-156">Пользователям, пытающимся имени домена CDN hello toouse перед hello конфигурацию конечной точки распространения toohello извлекает получит коды ответа HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="4e120-156">Users who try toouse hello CDN domain name before hello endpoint configuration has propagated toohello POPs will receive HTTP 404 response codes.</span></span>  <span data-ttu-id="4e120-157">Если прошло несколько часов с момента создания конечной точки и вы по-прежнему получаете ответы 404, см. статью [Устранение неполадок конечных точек CDN, возвращающих состояние 404](cdn-troubleshoot-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="4e120-157">If it's been several hours since you created your endpoint and you're still receiving 404 responses, please see [Troubleshooting CDN endpoints returning 404 statuses](cdn-troubleshoot-endpoint.md).</span></span>
    > 
    > 

## <a name="see-also"></a><span data-ttu-id="4e120-158">См. также</span><span class="sxs-lookup"><span data-stu-id="4e120-158">See Also</span></span>
* [<span data-ttu-id="4e120-159">Управление режимом кэширования запросов CDN с использованием строк запроса</span><span class="sxs-lookup"><span data-stu-id="4e120-159">Controlling caching behavior of requests with query strings</span></span>](cdn-query-string.md)
* [<span data-ttu-id="4e120-160">Как tooMap содержимого CDN tooa пользовательского домена</span><span class="sxs-lookup"><span data-stu-id="4e120-160">How tooMap CDN Content tooa Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="4e120-161">Предварительная загрузка ресурсов на конечной точке CDN Azure</span><span class="sxs-lookup"><span data-stu-id="4e120-161">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="4e120-162">Очистка конечной точки сети CDN Azure</span><span class="sxs-lookup"><span data-stu-id="4e120-162">Purge an Azure CDN Endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="4e120-163">Troubleshooting CDN endpoints returning 404 statuses (Устранение неполадок конечных точек CDN, возвращающих состояние 404)</span><span class="sxs-lookup"><span data-stu-id="4e120-163">Troubleshooting CDN endpoints returning 404 statuses</span></span>](cdn-troubleshoot-endpoint.md)

[cdn-profile-settings]: ./media/cdn-create-new-endpoint/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-create-new-endpoint/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-create-new-endpoint/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-create-new-endpoint/cdn-endpoint-success.png
