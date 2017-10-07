---
title: "сжатие файлов aaaTroubleshooting в Azure CDN | Документы Microsoft"
description: "Узнайте, как устранить неполадки со сжатием файлов Azure CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: a6624e65-1a77-4486-b473-8d720ce28f8b
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f00b98beaf6b3b3cd30108ece65a8191edc06ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-file-compression"></a><span data-ttu-id="10a82-103">Устранение неполадок со сжатием файлов CDN</span><span class="sxs-lookup"><span data-stu-id="10a82-103">Troubleshooting CDN file compression</span></span>
<span data-ttu-id="10a82-104">Эта статья поможет вам устранить неполадки со [сжатием файлов CDN](cdn-improve-performance.md).</span><span class="sxs-lookup"><span data-stu-id="10a82-104">This article helps you troubleshoot issues with [CDN file compression](cdn-improve-performance.md).</span></span>

<span data-ttu-id="10a82-105">Если вам нужна дополнительная помощь в любой момент в этой статье, можно обратиться в hello экспертов Azure на [hello MSDN Azure и hello переполнения стека форумы](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="10a82-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and hello Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="10a82-106">Кроме того, можно зарегистрировать обращение в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="10a82-106">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="10a82-107">Go toohello [сайте поддержки Azure](https://azure.microsoft.com/support/options/) и нажмите кнопку **Get Support**.</span><span class="sxs-lookup"><span data-stu-id="10a82-107">Go toohello [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="10a82-108">Симптом</span><span class="sxs-lookup"><span data-stu-id="10a82-108">Symptom</span></span>
<span data-ttu-id="10a82-109">Сжатие для конечной точки включено, но файлы возвращаются без сжатия.</span><span class="sxs-lookup"><span data-stu-id="10a82-109">Compression for your endpoint is enabled, but files are being returned uncompressed.</span></span>

> [!TIP]
> <span data-ttu-id="10a82-110">toocheck файлы возвращаются сжатые, необходимость toouse, такие как средство [Fiddler](http://www.telerik.com/fiddler) или обозревателя [средств разработчика](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span><span class="sxs-lookup"><span data-stu-id="10a82-110">toocheck whether your files are being returned compressed, you need toouse a tool like [Fiddler](http://www.telerik.com/fiddler) or your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span></span>  <span data-ttu-id="10a82-111">Заголовки ответа hello HTTP проверки возвращаемые CDN кэшированного содержимого.</span><span class="sxs-lookup"><span data-stu-id="10a82-111">Check hello HTTP response headers returned with your cached CDN content.</span></span>  <span data-ttu-id="10a82-112">Если есть заголовок с именем `Content-Encoding` со значением **gzip**, **bzip2** или **deflate**, то содержимое сжато.</span><span class="sxs-lookup"><span data-stu-id="10a82-112">If there is a header named `Content-Encoding` with a value of **gzip**, **bzip2**, or **deflate**, your content is compressed.</span></span>
> 
> ![Заголовок Content-Encoding](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a><span data-ttu-id="10a82-114">Причина:</span><span class="sxs-lookup"><span data-stu-id="10a82-114">Cause</span></span>
<span data-ttu-id="10a82-115">Возможно несколько причин, включая указанные ниже.</span><span class="sxs-lookup"><span data-stu-id="10a82-115">There are several possible causes, including:</span></span>

* <span data-ttu-id="10a82-116">Hello указанного содержимого не подходит для сжатия.</span><span class="sxs-lookup"><span data-stu-id="10a82-116">hello requested content is not eligible for compression.</span></span>
* <span data-ttu-id="10a82-117">Не включено сжатие для hello запрошенный тип файла.</span><span class="sxs-lookup"><span data-stu-id="10a82-117">Compression is not enabled for hello requested file type.</span></span>
* <span data-ttu-id="10a82-118">Hello HTTP-запроса не включать заголовок, запрашивает тип допустимым сжатия.</span><span class="sxs-lookup"><span data-stu-id="10a82-118">hello HTTP request did not include a header requesting a valid compression type.</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="10a82-119">Действия по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="10a82-119">Troubleshooting steps</span></span>
> [!TIP]
> <span data-ttu-id="10a82-120">Наряду с развертыванием новых конечных точек, CDN изменений конфигурации вступают некоторые toopropagate времени через сеть hello.</span><span class="sxs-lookup"><span data-stu-id="10a82-120">As with deploying new endpoints, CDN configuration changes take some time toopropagate through hello network.</span></span>  <span data-ttu-id="10a82-121">Как правило, изменения применяются в течение 90 минут.</span><span class="sxs-lookup"><span data-stu-id="10a82-121">Usually, changes are applied within 90 minutes.</span></span>  <span data-ttu-id="10a82-122">Если это hello при первом запуске настройки сжатия для конечной точки CDN, следует ожидания действительно распространения параметров сжатия hello извлекает toohello toobe 1 – 2 часов.</span><span class="sxs-lookup"><span data-stu-id="10a82-122">If this is hello first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours toobe sure hello compression settings have propagated toohello POPs.</span></span> 
> 
> 

### <a name="verify-hello-request"></a><span data-ttu-id="10a82-123">Проверьте запрос hello</span><span class="sxs-lookup"><span data-stu-id="10a82-123">Verify hello request</span></span>
<span data-ttu-id="10a82-124">Во-первых мы должны сделать быстрого проверочной меры по запросу hello.</span><span class="sxs-lookup"><span data-stu-id="10a82-124">First, we should do a quick sanity check on hello request.</span></span>  <span data-ttu-id="10a82-125">Можно использовать в браузере [средств разработчика](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview hello запросов.</span><span class="sxs-lookup"><span data-stu-id="10a82-125">You can use your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview hello requests being made.</span></span>

* <span data-ttu-id="10a82-126">Проверьте запрос hello отправляется URL-адрес конечной точки tooyour `<endpointname>.azureedge.net`, а не в источник.</span><span class="sxs-lookup"><span data-stu-id="10a82-126">Verify hello request is being sent tooyour endpoint URL, `<endpointname>.azureedge.net`, and not your origin.</span></span>
* <span data-ttu-id="10a82-127">Проверьте запрос hello содержит **Accept-Encoding** содержит заголовок, значение заголовка и hello **gzip**, **deflate**, или **bzip2** .</span><span class="sxs-lookup"><span data-stu-id="10a82-127">Verify hello request contains an **Accept-Encoding** header, and hello value for that header contains **gzip**, **deflate**, or **bzip2**.</span></span>

> [!NOTE]
> <span data-ttu-id="10a82-128">Профили **Azure CDN от Akamai** поддерживают только кодирование **GZIP**.</span><span class="sxs-lookup"><span data-stu-id="10a82-128">**Azure CDN from Akamai** profiles only support **gzip** encoding.</span></span>
> 
> 

![Заголовки запроса CDN](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a><span data-ttu-id="10a82-130">Проверка параметров сжатия (стандартный профиль CDN)</span><span class="sxs-lookup"><span data-stu-id="10a82-130">Verify compression settings (Standard CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="10a82-131">Это действие применимо только для профилей **Azure CDN уровня "Стандартный" от Verizon** или **Azure CDN уровня "Стандартный" от Akamai**.</span><span class="sxs-lookup"><span data-stu-id="10a82-131">This step only applies if your CDN profile is an **Azure CDN Standard from Verizon** or **Azure CDN Standard from Akamai** profile.</span></span> 
> 
> 

<span data-ttu-id="10a82-132">Перейдите tooyour конечной точки в hello [портал Azure](https://portal.azure.com) и нажмите кнопку hello **Настройка** кнопки.</span><span class="sxs-lookup"><span data-stu-id="10a82-132">Navigate tooyour endpoint in hello [Azure portal](https://portal.azure.com) and click hello **Configure** button.</span></span>

* <span data-ttu-id="10a82-133">Проверьте, включено ли сжатие.</span><span class="sxs-lookup"><span data-stu-id="10a82-133">Verify compression is enabled.</span></span>
* <span data-ttu-id="10a82-134">Проверьте hello тип MIME для содержимого, сжатые toobe входит в список hello сжатых форматов hello.</span><span class="sxs-lookup"><span data-stu-id="10a82-134">Verify hello MIME type for hello content toobe compressed is included in hello list of compressed formats.</span></span>

![Параметры сжатия CDN](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a><span data-ttu-id="10a82-136">Проверка параметров сжатия (профиль CDN уровня "Премиум")</span><span class="sxs-lookup"><span data-stu-id="10a82-136">Verify compression settings (Premium CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="10a82-137">Это действие применимо только для профиля **Azure CDN уровня "Премиум" от Verizon** .</span><span class="sxs-lookup"><span data-stu-id="10a82-137">This step only applies if your CDN profile is an **Azure CDN Premium from Verizon** profile.</span></span>
> 
> 

<span data-ttu-id="10a82-138">Перейдите tooyour конечной точки в hello [портал Azure](https://portal.azure.com) и нажмите кнопку hello **управление** кнопки.</span><span class="sxs-lookup"><span data-stu-id="10a82-138">Navigate tooyour endpoint in hello [Azure portal](https://portal.azure.com) and click hello **Manage** button.</span></span>  <span data-ttu-id="10a82-139">Hello дополнительный портал будет открыт.</span><span class="sxs-lookup"><span data-stu-id="10a82-139">hello supplemental portal will open.</span></span>  <span data-ttu-id="10a82-140">Наведите указатель мыши hello **HTTP больших** , а затем наведите указатель мыши hello **параметры кэша** всплывающим меню.</span><span class="sxs-lookup"><span data-stu-id="10a82-140">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="10a82-141">Щелкните **Сжатие**.</span><span class="sxs-lookup"><span data-stu-id="10a82-141">Click **Compression**.</span></span> 

* <span data-ttu-id="10a82-142">Проверьте, включено ли сжатие.</span><span class="sxs-lookup"><span data-stu-id="10a82-142">Verify compression is enabled.</span></span>
* <span data-ttu-id="10a82-143">Проверьте hello **типы файлов** список содержит список разделенных запятыми (без пробелов) типов MIME.</span><span class="sxs-lookup"><span data-stu-id="10a82-143">Verify hello **File Types** list contains a comma-separated list (no spaces) of MIME types.</span></span>
* <span data-ttu-id="10a82-144">Проверьте hello тип MIME для содержимого, сжатые toobe входит в список hello сжатых форматов hello.</span><span class="sxs-lookup"><span data-stu-id="10a82-144">Verify hello MIME type for hello content toobe compressed is included in hello list of compressed formats.</span></span>

![Параметры сжатия CDN уровня "Премиум"](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-hello-content-is-cached"></a><span data-ttu-id="10a82-146">Убедитесь, что кэш содержимого hello</span><span class="sxs-lookup"><span data-stu-id="10a82-146">Verify hello content is cached</span></span>
> [!NOTE]
> <span data-ttu-id="10a82-147">Это действие применимо только для профиля **Azure CDN от Verizon** (уровня "Премиум" или "Стандартный").</span><span class="sxs-lookup"><span data-stu-id="10a82-147">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="10a82-148">С помощью средств разработчика в браузере, убедитесь, что файл hello tooensure заголовки ответа hello кэшируются в области hello, где он был запрошен.</span><span class="sxs-lookup"><span data-stu-id="10a82-148">Using your browser's developer tools, check hello response headers tooensure hello file is cached in hello region where it is being requested.</span></span>

* <span data-ttu-id="10a82-149">Проверьте hello **сервера** заголовок ответа.</span><span class="sxs-lookup"><span data-stu-id="10a82-149">Check hello **Server** response header.</span></span>  <span data-ttu-id="10a82-150">Hello заголовок должен иметь формат hello **платформы (POP-сервер ID)**, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="10a82-150">hello header should have hello format **Platform (POP/Server ID)**, as seen in hello following example.</span></span>
* <span data-ttu-id="10a82-151">Проверьте hello **X кэша** заголовок ответа.</span><span class="sxs-lookup"><span data-stu-id="10a82-151">Check hello **X-Cache** response header.</span></span>  <span data-ttu-id="10a82-152">следует прочитать заголовок Hello **ПОПАДАНИЙ**.</span><span class="sxs-lookup"><span data-stu-id="10a82-152">hello header should read **HIT**.</span></span>  

![Заголовки ответа CDN](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-hello-file-meets-hello-size-requirements"></a><span data-ttu-id="10a82-154">Убедитесь, что файл hello отвечает требованиям к размеру hello</span><span class="sxs-lookup"><span data-stu-id="10a82-154">Verify hello file meets hello size requirements</span></span>
> [!NOTE]
> <span data-ttu-id="10a82-155">Это действие применимо только для профиля **Azure CDN от Verizon** (уровня "Премиум" или "Стандартный").</span><span class="sxs-lookup"><span data-stu-id="10a82-155">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="10a82-156">toobe отсрочить сжатие, файл должен соответствовать hello следующие требования к размеру:</span><span class="sxs-lookup"><span data-stu-id="10a82-156">toobe eligible for compression, a file must meet hello following size requirements:</span></span>

* <span data-ttu-id="10a82-157">более 128 байт;</span><span class="sxs-lookup"><span data-stu-id="10a82-157">Larger than 128 bytes.</span></span>
* <span data-ttu-id="10a82-158">менее 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="10a82-158">Smaller than 1 MB.</span></span>

### <a name="check-hello-request-at-hello-origin-server-for-a-via-header"></a><span data-ttu-id="10a82-159">Проверка запроса hello на исходном сервере hello для **через** заголовок</span><span class="sxs-lookup"><span data-stu-id="10a82-159">Check hello request at hello origin server for a **Via** header</span></span>
<span data-ttu-id="10a82-160">Hello **через** заголовок HTTP указывает toohello веб-сервера, hello запрос передается через прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="10a82-160">hello **Via** HTTP header indicates toohello web server that hello request is being passed by a proxy server.</span></span>  <span data-ttu-id="10a82-161">Веб-серверов Microsoft IIS по умолчанию не сжатия ответов, когда запрос hello содержит **через** заголовок.</span><span class="sxs-lookup"><span data-stu-id="10a82-161">Microsoft IIS web servers by default do not compress responses when hello request contains a **Via** header.</span></span>  <span data-ttu-id="10a82-162">toooverride такое поведение следующих hello:</span><span class="sxs-lookup"><span data-stu-id="10a82-162">toooverride this behavior, perform hello following:</span></span>

* <span data-ttu-id="10a82-163">**IIS 6**: [задать HcNoCompressionForProxies = «FALSE» в свойствах hello метабазы IIS](https://msdn.microsoft.com/library/ms525390.aspx)</span><span class="sxs-lookup"><span data-stu-id="10a82-163">**IIS 6**: [Set HcNoCompressionForProxies="FALSE" in hello IIS Metabase properties](https://msdn.microsoft.com/library/ms525390.aspx)</span></span>
* <span data-ttu-id="10a82-164">**Службы IIS 7 и выше**: [установите **noCompressionForHttp10** и **noCompressionForProxies** tooFalse в конфигурации сервера hello](http://www.iis.net/configreference/system.webserver/httpcompression)</span><span class="sxs-lookup"><span data-stu-id="10a82-164">**IIS 7 and up**: [Set both **noCompressionForHttp10** and **noCompressionForProxies** tooFalse in hello server configuration](http://www.iis.net/configreference/system.webserver/httpcompression)</span></span>

