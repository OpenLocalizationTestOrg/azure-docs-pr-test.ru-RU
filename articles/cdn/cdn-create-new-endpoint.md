---
title: "Начало работы с Azure CDN | Документация Майкрософт"
description: "В статье описывается, как включить сеть доставки содержимого (CDN) в Azure. В этом руководстве описано, как создать профиль CDN и конечную точку."
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
ms.openlocfilehash: d263e911d0d0b3cdc1e48e300a3c8a0994b38c39
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-cdn"></a><span data-ttu-id="99624-104">Начало работы с Azure CDN</span><span class="sxs-lookup"><span data-stu-id="99624-104">Getting started with Azure CDN</span></span>
<span data-ttu-id="99624-105">В этой статье объясняется, как включить Azure CDN, создав новый профиль и конечную точку CDN.</span><span class="sxs-lookup"><span data-stu-id="99624-105">This topic walks through enabling Azure CDN by creating a new CDN profile and endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="99624-106">Общие сведения о работе CDN, включая список функций, см. в [обзорной статье о сети CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="99624-106">For an introduction to how CDN works, as well as a list of features, see the [CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="create-a-new-cdn-profile"></a><span data-ttu-id="99624-107">Создание нового профиля сети CDN</span><span class="sxs-lookup"><span data-stu-id="99624-107">Create a new CDN profile</span></span>
<span data-ttu-id="99624-108">Профиль сети CDN представляет собой коллекцию конечных точек сети CDN.</span><span class="sxs-lookup"><span data-stu-id="99624-108">A CDN profile is a collection of CDN endpoints.</span></span>  <span data-ttu-id="99624-109">Каждый профиль содержит одну или несколько конечных точек сети CDN.</span><span class="sxs-lookup"><span data-stu-id="99624-109">Each profile contains one or more CDN endpoints.</span></span>  <span data-ttu-id="99624-110">Вы можете использовать несколько профилей для упорядочения конечных точек сети CDN по домену Интернета, веб-приложению или согласно другим условиям.</span><span class="sxs-lookup"><span data-stu-id="99624-110">You may wish to use multiple profiles to organize your CDN endpoints by internet domain, web application, or some other criteria.</span></span>

> [!NOTE]
> <span data-ttu-id="99624-111">По умолчанию в одной подписке Azure можно создать не более восьми профилей CDN.</span><span class="sxs-lookup"><span data-stu-id="99624-111">By default, a single Azure subscription is limited to eight CDN profiles.</span></span> <span data-ttu-id="99624-112">Каждый профиль CDN может содержать не более десяти конечных точек CDN.</span><span class="sxs-lookup"><span data-stu-id="99624-112">Each CDN profile is limited to ten CDN endpoints.</span></span>
> 
> <span data-ttu-id="99624-113">Стоимость использования CDN определяется уровнем профиля CDN.</span><span class="sxs-lookup"><span data-stu-id="99624-113">CDN pricing is applied at the CDN profile level.</span></span> <span data-ttu-id="99624-114">Если вы хотите использовать ценовые категории Azure CDN, вам потребуется несколько профилей CDN.</span><span class="sxs-lookup"><span data-stu-id="99624-114">If you wish to use a mix of Azure CDN pricing tiers, you will need multiple CDN profiles.</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a><span data-ttu-id="99624-115">Создание новой конечной точки сети CDN</span><span class="sxs-lookup"><span data-stu-id="99624-115">Create a new CDN endpoint</span></span>
<span data-ttu-id="99624-116">**Создание новой конечной точки сети CDN**</span><span class="sxs-lookup"><span data-stu-id="99624-116">**To create a new CDN endpoint**</span></span>

1. <span data-ttu-id="99624-117">На [портале Azure](https://portal.azure.com)перейдите к профилю CDN.</span><span class="sxs-lookup"><span data-stu-id="99624-117">In the [Azure Portal](https://portal.azure.com), navigate to your CDN profile.</span></span>  <span data-ttu-id="99624-118">На предыдущем шаге вы могли прикрепить его к панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="99624-118">You may have pinned it to the dashboard in the previous step.</span></span>  <span data-ttu-id="99624-119">Если профиль не прикреплен, найдите его, нажав кнопку **Обзор**, выбрав **Профили CDN** и щелкнув профиль, к которому нужно добавить конечную точку.</span><span class="sxs-lookup"><span data-stu-id="99624-119">If you not, you can find it by clicking **Browse**, then **CDN profiles**, and clicking on the profile you plan to add your endpoint to.</span></span>
   
    <span data-ttu-id="99624-120">Появится колонка профиля сети CDN.</span><span class="sxs-lookup"><span data-stu-id="99624-120">The CDN profile blade appears.</span></span>
   
    ![Профиль сети CDN][cdn-profile-settings]
2. <span data-ttu-id="99624-122">Нажмите кнопку **Добавить конечную точку** .</span><span class="sxs-lookup"><span data-stu-id="99624-122">Click the **Add Endpoint** button.</span></span>
   
    ![Кнопка "Добавить конечную точку"][cdn-new-endpoint-button]
   
    <span data-ttu-id="99624-124">Появится колонка **Добавление конечной точки** .</span><span class="sxs-lookup"><span data-stu-id="99624-124">The **Add an endpoint** blade appears.</span></span>
   
    ![Колонка "Добавление конечной точки"][cdn-add-endpoint]
3. <span data-ttu-id="99624-126">Введите **имя** конечной точки сети CDN.</span><span class="sxs-lookup"><span data-stu-id="99624-126">Enter a **Name** for this CDN endpoint.</span></span>  <span data-ttu-id="99624-127">Это имя будет использоваться для доступа к кэшированным ресурсам в домене `<endpointname>.azureedge.net`.</span><span class="sxs-lookup"><span data-stu-id="99624-127">This name will be used to access your cached resources at the domain `<endpointname>.azureedge.net`.</span></span>
4. <span data-ttu-id="99624-128">В раскрывающемся списке **Тип источника** выберите тип источника.</span><span class="sxs-lookup"><span data-stu-id="99624-128">In the **Origin type** dropdown, select your origin type.</span></span>  <span data-ttu-id="99624-129">Выберите **Служба хранилища** для учетной записи хранения Azure, **Облачная служба** для облачной службы Azure, **Веб-приложение** для веб-приложения Azure или **Настраиваемый источник** для любого другого общедоступного источника на веб-сервере (размещенного в Azure или в другом месте).</span><span class="sxs-lookup"><span data-stu-id="99624-129">Select **Storage** for an Azure Storage account, **Cloud service** for an Azure Cloud Service, **Web App** for an Azure Web App, or **Custom origin** for any other publicly accessible web server origin (hosted in Azure or elsewhere).</span></span>
   
    ![Тип источника CDN](./media/cdn-create-new-endpoint/cdn-origin-type.png)
5. <span data-ttu-id="99624-131">В раскрывающемся списке **Имя узла источника** выберите или введите исходный домен.</span><span class="sxs-lookup"><span data-stu-id="99624-131">In the **Origin hostname** dropdown, select or type your origin domain.</span></span>  <span data-ttu-id="99624-132">В раскрывающемся списке будут перечислены все доступные источники типа, указанного на шаге 4.</span><span class="sxs-lookup"><span data-stu-id="99624-132">The dropdown will list all available origins of the type you specified in step 4.</span></span>  <span data-ttu-id="99624-133">Если в качестве значения параметра *Тип источника* вы выбрали **Настраиваемый источник**, потребуется ввести домен вашего настраиваемого источника.</span><span class="sxs-lookup"><span data-stu-id="99624-133">If you selected *Custom origin* as your **Origin type**, you will type in the domain of your custom origin.</span></span>
6. <span data-ttu-id="99624-134">В поле **Путь к источнику** введите путь к ресурсам, которые нужно кэшировать, или оставьте поле пустым, чтобы разрешить кэшировать любые ресурсы в домене, указанном на шаге 5.</span><span class="sxs-lookup"><span data-stu-id="99624-134">In the **Origin path** text box, enter the path to the resources you want to cache, or leave blank to allow cache any resource at the domain you specified in step 5.</span></span>
7. <span data-ttu-id="99624-135">В поле **Заголовок узла источника**введите заголовок узла, который сеть CDN будет отправлять с каждым запросом, или оставьте значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="99624-135">In the **Origin host header**, enter the host header you want the CDN to send with each request, or leave the default.</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="99624-136">Для некоторых типов источников, таких как служба хранилища Azure и веб-приложения, нужно, чтобы заголовок узла соответствовал домену источника.</span><span class="sxs-lookup"><span data-stu-id="99624-136">Some types of origins, such as Azure Storage and Web Apps, require the host header to match the domain of the origin.</span></span> <span data-ttu-id="99624-137">Если для вашего источника не требуется, чтобы заголовок узла отличался от домена, оставьте значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="99624-137">Unless you have an origin that requires a host header different from its domain, you should leave the default value.</span></span>
   > 
   > 
8. <span data-ttu-id="99624-138">Для параметров **Протокол** и **Порт источника** укажите протоколы и порты, используемые для доступа к ресурсам в источнике.</span><span class="sxs-lookup"><span data-stu-id="99624-138">For **Protocol** and **Origin port**, specify the protocols and ports used to access your resources at the origin.</span></span>  <span data-ttu-id="99624-139">Необходимо указать хотя бы один протокол (HTTP или HTTPS).</span><span class="sxs-lookup"><span data-stu-id="99624-139">At least one protocol (HTTP or HTTPS) must be selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="99624-140">**Порт источника** влияет только на то, какой порт будет использовать конечная точка для получения данных из источника.</span><span class="sxs-lookup"><span data-stu-id="99624-140">The **Origin port** only affects what port the endpoint uses to retrieve information from the origin.</span></span>  <span data-ttu-id="99624-141">Сама конечная точка будет доступна конечным клиентам только на портах HTTP и HTTPS по умолчанию (80 и 443) вне зависимости от **порта источника**.</span><span class="sxs-lookup"><span data-stu-id="99624-141">The endpoint itself will only be available to end clients on the default HTTP and HTTPS ports (80 and 443), regardless of the **Origin port**.</span></span>  
   > 
   > <span data-ttu-id="99624-142">В конечных точках **Azure CDN от Akamai** запрещено использовать полный диапазон портов TCP для источников.</span><span class="sxs-lookup"><span data-stu-id="99624-142">**Azure CDN from Akamai** endpoints do not allow the full TCP port range for origins.</span></span>  <span data-ttu-id="99624-143">Список запрещенных портов источников см. в статье о [разрешенных портах источников Azure CDN от Akamai](https://msdn.microsoft.com/library/mt757337.aspx).</span><span class="sxs-lookup"><span data-stu-id="99624-143">For a list of origin ports that are not allowed, see [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx).</span></span>  
   > 
   > <span data-ttu-id="99624-144">Доступ к содержимому CDN с использованием HTTPS имеет следующие ограничения.</span><span class="sxs-lookup"><span data-stu-id="99624-144">Accessing CDN content using HTTPS has the following constraints:</span></span>
   > 
   > * <span data-ttu-id="99624-145">Необходимо использовать сертификат SSL, предоставленный сетью CDN.</span><span class="sxs-lookup"><span data-stu-id="99624-145">You must use the SSL certificate provided by the CDN.</span></span> <span data-ttu-id="99624-146">Сертификаты третьих сторон не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="99624-146">Third party certificates are not supported.</span></span>
   > * <span data-ttu-id="99624-147">Для доступа к HTTPS-содержимому необходимо использовать домен, предоставленный сетью CDN (`<endpointname>.azureedge.net`).</span><span class="sxs-lookup"><span data-stu-id="99624-147">You must use the CDN-provided domain (`<endpointname>.azureedge.net`) to access HTTPS content.</span></span> <span data-ttu-id="99624-148">Поддержка HTTPS для имен личных доменов (CNAME) недоступна, поскольку в данный момент CDN не поддерживает пользовательские сертификаты.</span><span class="sxs-lookup"><span data-stu-id="99624-148">HTTPS support is not available for custom domain names (CNAMEs) since the CDN does not support custom certificates at this time.</span></span>
   > 
   > 
9. <span data-ttu-id="99624-149">Нажмите кнопку **Добавить** , чтобы создать новую конечную точку.</span><span class="sxs-lookup"><span data-stu-id="99624-149">Click the **Add** button to create the new endpoint.</span></span>
10. <span data-ttu-id="99624-150">Созданная конечная точка отображается в списке конечных точек для профиля.</span><span class="sxs-lookup"><span data-stu-id="99624-150">Once the endpoint is created, it appears in a list of endpoints for the profile.</span></span> <span data-ttu-id="99624-151">В режиме списка отображается URL-адрес для доступа к кэшированному содержимому, а также исходному домену.</span><span class="sxs-lookup"><span data-stu-id="99624-151">The list view shows the URL to use to access cached content, as well as the origin domain.</span></span>
    
    ![Конечная точка сети CDN][cdn-endpoint-success]
    
    > [!IMPORTANT]
    > <span data-ttu-id="99624-153">Конечная точка не будет доступна сразу. Распространение регистрационных сведений по сети CDN может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="99624-153">The endpoint will not immediately be available for use, as it takes time for the registration to propagate through the CDN.</span></span>  <span data-ttu-id="99624-154">Для профилей <b>Azure CDN от Akamai</b> распространение обычно занимает не более минуты.</span><span class="sxs-lookup"><span data-stu-id="99624-154">For <b>Azure CDN from Akamai</b> profiles, propagation will usually complete within one minute.</span></span>  <span data-ttu-id="99624-155">Для профилей <b>Azure CDN от Verizon</b> распространение обычно завершается в течение 90 минут, но в некоторых случаях может занимать больше времени.</span><span class="sxs-lookup"><span data-stu-id="99624-155">For <b>Azure CDN from Verizon</b> profiles, propagation will usually complete within 90 minutes, but in some cases can take longer.</span></span>
    > 
    > <span data-ttu-id="99624-156">При попытке использовать имя домена CDN до того, как конфигурация конечной точки распространится на POP, будет возвращен код ответа HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="99624-156">Users who try to use the CDN domain name before the endpoint configuration has propagated to the POPs will receive HTTP 404 response codes.</span></span>  <span data-ttu-id="99624-157">Если прошло несколько часов с момента создания конечной точки и вы по-прежнему получаете ответы 404, см. статью [Устранение неполадок конечных точек CDN, возвращающих состояние 404](cdn-troubleshoot-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="99624-157">If it's been several hours since you created your endpoint and you're still receiving 404 responses, please see [Troubleshooting CDN endpoints returning 404 statuses](cdn-troubleshoot-endpoint.md).</span></span>
    > 
    > 

## <a name="see-also"></a><span data-ttu-id="99624-158">См. также</span><span class="sxs-lookup"><span data-stu-id="99624-158">See Also</span></span>
* [<span data-ttu-id="99624-159">Управление режимом кэширования запросов CDN с использованием строк запроса</span><span class="sxs-lookup"><span data-stu-id="99624-159">Controlling caching behavior of requests with query strings</span></span>](cdn-query-string.md)
* [<span data-ttu-id="99624-160">Сопоставление содержимого CDN с пользовательским доменом</span><span class="sxs-lookup"><span data-stu-id="99624-160">How to Map CDN Content to a Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="99624-161">Предварительная загрузка ресурсов на конечной точке CDN Azure</span><span class="sxs-lookup"><span data-stu-id="99624-161">Pre-load assets on an Azure CDN endpoint</span></span>](cdn-preload-endpoint.md)
* [<span data-ttu-id="99624-162">Очистка конечной точки сети CDN Azure</span><span class="sxs-lookup"><span data-stu-id="99624-162">Purge an Azure CDN Endpoint</span></span>](cdn-purge-endpoint.md)
* [<span data-ttu-id="99624-163">Troubleshooting CDN endpoints returning 404 statuses (Устранение неполадок конечных точек CDN, возвращающих состояние 404)</span><span class="sxs-lookup"><span data-stu-id="99624-163">Troubleshooting CDN endpoints returning 404 statuses</span></span>](cdn-troubleshoot-endpoint.md)

[cdn-profile-settings]: ./media/cdn-create-new-endpoint/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-create-new-endpoint/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-create-new-endpoint/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-create-new-endpoint/cdn-endpoint-success.png
