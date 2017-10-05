---
title: "Устранение неполадок со сжатием файлов в Azure CDN | Документация Майкрософт"
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
ms.openlocfilehash: 5ef8a8262eb40aa827161764f03a63d031e43273
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-cdn-file-compression"></a><span data-ttu-id="5f5cc-103">Устранение неполадок со сжатием файлов CDN</span><span class="sxs-lookup"><span data-stu-id="5f5cc-103">Troubleshooting CDN file compression</span></span>
<span data-ttu-id="5f5cc-104">Эта статья поможет вам устранить неполадки со [сжатием файлов CDN](cdn-improve-performance.md).</span><span class="sxs-lookup"><span data-stu-id="5f5cc-104">This article helps you troubleshoot issues with [CDN file compression](cdn-improve-performance.md).</span></span>

<span data-ttu-id="5f5cc-105">Если вам потребуется дополнительная помощь по любому из вопросов, рассматриваемых в статье, вы можете обратиться к экспертам по Azure на [форумах MSDN Azure и Stack Overflow](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="5f5cc-105">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="5f5cc-106">Кроме того, можно зарегистрировать обращение в службу поддержки Azure.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-106">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="5f5cc-107">Перейдите на [веб-сайт поддержки Azure](https://azure.microsoft.com/support/options/) и щелкните **Получить поддержку**.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-107">Go to the [Azure Support site](https://azure.microsoft.com/support/options/) and click **Get Support**.</span></span>

## <a name="symptom"></a><span data-ttu-id="5f5cc-108">Симптом</span><span class="sxs-lookup"><span data-stu-id="5f5cc-108">Symptom</span></span>
<span data-ttu-id="5f5cc-109">Сжатие для конечной точки включено, но файлы возвращаются без сжатия.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-109">Compression for your endpoint is enabled, but files are being returned uncompressed.</span></span>

> [!TIP]
> <span data-ttu-id="5f5cc-110">Чтобы проверить, сжаты ли возвращаемые файлы, используйте такой инструмент, как [Fiddler](http://www.telerik.com/fiddler), или [инструменты разработчика](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) в браузере.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-110">To check whether your files are being returned compressed, you need to use a tool like [Fiddler](http://www.telerik.com/fiddler) or your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).</span></span>  <span data-ttu-id="5f5cc-111">Проверьте заголовки HTTP-ответа, возвращаемые с кэшированным содержимым CDN.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-111">Check the HTTP response headers returned with your cached CDN content.</span></span>  <span data-ttu-id="5f5cc-112">Если есть заголовок с именем `Content-Encoding` со значением **gzip**, **bzip2** или **deflate**, то содержимое сжато.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-112">If there is a header named `Content-Encoding` with a value of **gzip**, **bzip2**, or **deflate**, your content is compressed.</span></span>
> 
> ![Заголовок Content-Encoding](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a><span data-ttu-id="5f5cc-114">Причина:</span><span class="sxs-lookup"><span data-stu-id="5f5cc-114">Cause</span></span>
<span data-ttu-id="5f5cc-115">Возможно несколько причин, включая указанные ниже.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-115">There are several possible causes, including:</span></span>

* <span data-ttu-id="5f5cc-116">Запрошенное содержимое не подходит для сжатия.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-116">The requested content is not eligible for compression.</span></span>
* <span data-ttu-id="5f5cc-117">Сжатие не включено для запрошенного типа файла.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-117">Compression is not enabled for the requested file type.</span></span>
* <span data-ttu-id="5f5cc-118">В запросе HTTP не было заголовка, запрашивающего допустимый тип сжатия.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-118">The HTTP request did not include a header requesting a valid compression type.</span></span>

## <a name="troubleshooting-steps"></a><span data-ttu-id="5f5cc-119">Действия по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="5f5cc-119">Troubleshooting steps</span></span>
> [!TIP]
> <span data-ttu-id="5f5cc-120">Как и при развертывании новых конечных точек, требуется некоторое время для распространения изменений конфигурации CDN по сети.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-120">As with deploying new endpoints, CDN configuration changes take some time to propagate through the network.</span></span>  <span data-ttu-id="5f5cc-121">Как правило, изменения применяются в течение 90 минут.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-121">Usually, changes are applied within 90 minutes.</span></span>  <span data-ttu-id="5f5cc-122">Если сжатие для конечной точки CDN задается впервые, следует подождать один-два часа, чтобы настройки сжатия гарантированно распространились на серверы POP.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-122">If this is the first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours to be sure the compression settings have propagated to the POPs.</span></span> 
> 
> 

### <a name="verify-the-request"></a><span data-ttu-id="5f5cc-123">Проверка запроса</span><span class="sxs-lookup"><span data-stu-id="5f5cc-123">Verify the request</span></span>
<span data-ttu-id="5f5cc-124">Сначала следует быстро проверить запрос.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-124">First, we should do a quick sanity check on the request.</span></span>  <span data-ttu-id="5f5cc-125">Чтобы просмотреть поступивший запрос, можно использовать [средства разработчика](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) в браузере.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-125">You can use your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) to view the requests being made.</span></span>

* <span data-ttu-id="5f5cc-126">Запрос должен отправляться по URL-адресу конечной точки ( `<endpointname>.azureedge.net`), а не в источник.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-126">Verify the request is being sent to your endpoint URL, `<endpointname>.azureedge.net`, and not your origin.</span></span>
* <span data-ttu-id="5f5cc-127">Запрос должен содержать заголовок **Accept-Encoding** со значением **gzip**, **deflate** или **bzip2**.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-127">Verify the request contains an **Accept-Encoding** header, and the value for that header contains **gzip**, **deflate**, or **bzip2**.</span></span>

> [!NOTE]
> <span data-ttu-id="5f5cc-128">Профили **Azure CDN от Akamai** поддерживают только кодирование **GZIP**.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-128">**Azure CDN from Akamai** profiles only support **gzip** encoding.</span></span>
> 
> 

![Заголовки запроса CDN](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a><span data-ttu-id="5f5cc-130">Проверка параметров сжатия (стандартный профиль CDN)</span><span class="sxs-lookup"><span data-stu-id="5f5cc-130">Verify compression settings (Standard CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="5f5cc-131">Это действие применимо только для профилей **Azure CDN уровня "Стандартный" от Verizon** или **Azure CDN уровня "Стандартный" от Akamai**.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-131">This step only applies if your CDN profile is an **Azure CDN Standard from Verizon** or **Azure CDN Standard from Akamai** profile.</span></span> 
> 
> 

<span data-ttu-id="5f5cc-132">Перейдите к конечной точке на [портале Azure](https://portal.azure.com) и нажмите кнопку **Настроить** .</span><span class="sxs-lookup"><span data-stu-id="5f5cc-132">Navigate to your endpoint in the [Azure portal](https://portal.azure.com) and click the **Configure** button.</span></span>

* <span data-ttu-id="5f5cc-133">Проверьте, включено ли сжатие.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-133">Verify compression is enabled.</span></span>
* <span data-ttu-id="5f5cc-134">Убедитесь в том, что тип MIME для сжимаемого содержимого включен в список сжимаемых форматов.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-134">Verify the MIME type for the content to be compressed is included in the list of compressed formats.</span></span>

![Параметры сжатия CDN](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a><span data-ttu-id="5f5cc-136">Проверка параметров сжатия (профиль CDN уровня "Премиум")</span><span class="sxs-lookup"><span data-stu-id="5f5cc-136">Verify compression settings (Premium CDN profile)</span></span>
> [!NOTE]
> <span data-ttu-id="5f5cc-137">Это действие применимо только для профиля **Azure CDN уровня "Премиум" от Verizon** .</span><span class="sxs-lookup"><span data-stu-id="5f5cc-137">This step only applies if your CDN profile is an **Azure CDN Premium from Verizon** profile.</span></span>
> 
> 

<span data-ttu-id="5f5cc-138">Перейдите к конечной точке на [портале Azure](https://portal.azure.com) и нажмите кнопку **Управление** .</span><span class="sxs-lookup"><span data-stu-id="5f5cc-138">Navigate to your endpoint in the [Azure portal](https://portal.azure.com) and click the **Manage** button.</span></span>  <span data-ttu-id="5f5cc-139">Откроется дополнительный портал.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-139">The supplemental portal will open.</span></span>  <span data-ttu-id="5f5cc-140">Наведите указатель мыши на вкладку **HTTP Large** (Большая платформа HTTP), а затем наведите указатель мыши на всплывающий элемент **Параметры кэша**.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-140">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="5f5cc-141">Щелкните **Сжатие**.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-141">Click **Compression**.</span></span> 

* <span data-ttu-id="5f5cc-142">Проверьте, включено ли сжатие.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-142">Verify compression is enabled.</span></span>
* <span data-ttu-id="5f5cc-143">Список **Типы файлов** должен включать разделенный запятыми список типов MIME (без пробелов).</span><span class="sxs-lookup"><span data-stu-id="5f5cc-143">Verify the **File Types** list contains a comma-separated list (no spaces) of MIME types.</span></span>
* <span data-ttu-id="5f5cc-144">Убедитесь в том, что тип MIME для сжимаемого содержимого включен в список сжимаемых форматов.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-144">Verify the MIME type for the content to be compressed is included in the list of compressed formats.</span></span>

![Параметры сжатия CDN уровня "Премиум"](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-the-content-is-cached"></a><span data-ttu-id="5f5cc-146">Проверка кэширования содержимого</span><span class="sxs-lookup"><span data-stu-id="5f5cc-146">Verify the content is cached</span></span>
> [!NOTE]
> <span data-ttu-id="5f5cc-147">Это действие применимо только для профиля **Azure CDN от Verizon** (уровня "Премиум" или "Стандартный").</span><span class="sxs-lookup"><span data-stu-id="5f5cc-147">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="5f5cc-148">С помощью средств разработчика в браузере проверьте заголовки ответов, чтобы убедиться в том, что файл кэширован в регионе, где он запрашивается.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-148">Using your browser's developer tools, check the response headers to ensure the file is cached in the region where it is being requested.</span></span>

* <span data-ttu-id="5f5cc-149">Проверьте заголовок ответа **Server** в формате</span><span class="sxs-lookup"><span data-stu-id="5f5cc-149">Check the **Server** response header.</span></span>  <span data-ttu-id="5f5cc-150">**платформа (POP/идентификатор сервера)**, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-150">The header should have the format **Platform (POP/Server ID)**, as seen in the following example.</span></span>
* <span data-ttu-id="5f5cc-151">Проверьте заголовок ответа **X-Cache** .</span><span class="sxs-lookup"><span data-stu-id="5f5cc-151">Check the **X-Cache** response header.</span></span>  <span data-ttu-id="5f5cc-152">Он должен иметь значение **HIT**.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-152">The header should read **HIT**.</span></span>  

![Заголовки ответа CDN](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-the-file-meets-the-size-requirements"></a><span data-ttu-id="5f5cc-154">Проверка соответствия файла требованиям к размеру</span><span class="sxs-lookup"><span data-stu-id="5f5cc-154">Verify the file meets the size requirements</span></span>
> [!NOTE]
> <span data-ttu-id="5f5cc-155">Это действие применимо только для профиля **Azure CDN от Verizon** (уровня "Премиум" или "Стандартный").</span><span class="sxs-lookup"><span data-stu-id="5f5cc-155">This step only applies if your CDN profile is an **Azure CDN from Verizon** profile (Standard or Premium).</span></span>
> 
> 

<span data-ttu-id="5f5cc-156">Чтобы сжатие файла было возможным, его размер должен удовлетворять таким требованиям:</span><span class="sxs-lookup"><span data-stu-id="5f5cc-156">To be eligible for compression, a file must meet the following size requirements:</span></span>

* <span data-ttu-id="5f5cc-157">более 128 байт;</span><span class="sxs-lookup"><span data-stu-id="5f5cc-157">Larger than 128 bytes.</span></span>
* <span data-ttu-id="5f5cc-158">менее 1 МБ.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-158">Smaller than 1 MB.</span></span>

### <a name="check-the-request-at-the-origin-server-for-a-via-header"></a><span data-ttu-id="5f5cc-159">Проверьте, есть ли в запросе на сервере-источнике заголовок **Via** .</span><span class="sxs-lookup"><span data-stu-id="5f5cc-159">Check the request at the origin server for a **Via** header</span></span>
<span data-ttu-id="5f5cc-160">HTTP-заголовок **Via** указывает веб-серверу, что запрос передается через прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-160">The **Via** HTTP header indicates to the web server that the request is being passed by a proxy server.</span></span>  <span data-ttu-id="5f5cc-161">Если запрос содержит заголовок **Via** , веб-серверы Microsoft IIS по умолчанию не сжимают ответы.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-161">Microsoft IIS web servers by default do not compress responses when the request contains a **Via** header.</span></span>  <span data-ttu-id="5f5cc-162">Чтобы изменить это поведение, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="5f5cc-162">To override this behavior, perform the following:</span></span>

* <span data-ttu-id="5f5cc-163">**IIS 6**: [задайте HcNoCompressionForProxies="FALSE" в свойствах метабазы IIS](https://msdn.microsoft.com/library/ms525390.aspx)</span><span class="sxs-lookup"><span data-stu-id="5f5cc-163">**IIS 6**: [Set HcNoCompressionForProxies="FALSE" in the IIS Metabase properties](https://msdn.microsoft.com/library/ms525390.aspx)</span></span>
* <span data-ttu-id="5f5cc-164">**IIS 7 и выше**: [присвойте параметрам **noCompressionForHttp10** и **noCompressionForProxies** значение False в конфигурации сервера](http://www.iis.net/configreference/system.webserver/httpcompression).</span><span class="sxs-lookup"><span data-stu-id="5f5cc-164">**IIS 7 and up**: [Set both **noCompressionForHttp10** and **noCompressionForProxies** to False in the server configuration](http://www.iis.net/configreference/system.webserver/httpcompression)</span></span>

