---
title: "aaaImprove производительности с помощью сжатия файлов в сети доставки Содержимого Azure | Документы Microsoft"
description: "Узнайте, как передача файлов tooimprove скорость и повышает производительность загрузки страницы, сжатие файлов в сети доставки Содержимого Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: af1cddff-78d8-476b-a9d0-8c2164e4de5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9a1698b6c29233c2e2e6fb17cdd8e919ae8bfa1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a><span data-ttu-id="a8eb8-103">Повышение производительности за счет сжатия файлов в Azure CDN</span><span class="sxs-lookup"><span data-stu-id="a8eb8-103">Improve performance by compressing files in Azure CDN</span></span>
<span data-ttu-id="a8eb8-104">Сжатие — это простой и эффективный метод скорость передачи файла tooimprove и увеличение производительности загрузки страницы за счет уменьшения размера файла до его отправки с сервера hello.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-104">Compression is a simple and effective method tooimprove file transfer speed and increase page load performance by reducing file size before it is sent from hello server.</span></span> <span data-ttu-id="a8eb8-105">Этот позволяет снизить потребление пропускной способности и обеспечивает более высокую скорость работы для пользователей.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-105">It reduces bandwidth costs and provides a more responsive experience for your users.</span></span>

<span data-ttu-id="a8eb8-106">Существует два способа tooenable сжатия:</span><span class="sxs-lookup"><span data-stu-id="a8eb8-106">There are two ways tooenable compression:</span></span>

* <span data-ttu-id="a8eb8-107">Можно включить сжатие на исходный сервер, в этом случае hello CDN, проходит через hello сжатые файлы и доставки tooclients сжатых файлов, запрашивают их.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-107">You can enable compression on your origin server, in which case hello CDN passes through hello compressed files and deliver compressed files tooclients that request them.</span></span>
* <span data-ttu-id="a8eb8-108">Можно включить сжатие непосредственно на пограничных серверов CDN, в которых сжимает CDN вариантов hello hello файлы и обслуживать пользователей tooend, даже если они не сжимает hello исходного сервера.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-108">You can enable compression directly on CDN edge servers, in which case hello CDN compresses hello files and serve them tooend users, even if they are not compressed by hello origin server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8eb8-109">Изменения конфигурации CDN раньше некоторые toopropagate времени через сеть hello.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-109">CDN configuration changes take some time toopropagate through hello network.</span></span>  <span data-ttu-id="a8eb8-110">Для профилей <b>Azure CDN от Akamai</b> распространение обычно завершается в течение одной минуты.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-110">For <b>Azure CDN from Akamai</b> profiles, propagation usually completes in under one minute.</span></span>  <span data-ttu-id="a8eb8-111">Для профилей <b>Azure CDN от Verizon</b> изменения вступают в силу в течение 90 минут.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-111">For <b>Azure CDN from Verizon</b> profiles, you will usually see your changes apply within 90 minutes.</span></span>  <span data-ttu-id="a8eb8-112">Если это hello при первом запуске настройки сжатия для конечной точки CDN, следует рассмотреть возможность ожидания toobe 1 – 2 часов, убедиться, что распространения параметров сжатия hello извлекает toohello до устранения неполадок</span><span class="sxs-lookup"><span data-stu-id="a8eb8-112">If this is hello first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours toobe sure hello compression settings have propagated toohello POPs before troubleshooting</span></span>
> 
> 

## <a name="enabling-compression"></a><span data-ttu-id="a8eb8-113">Включение сжатия</span><span class="sxs-lookup"><span data-stu-id="a8eb8-113">Enabling compression</span></span>
> [!NOTE]
> <span data-ttu-id="a8eb8-114">Hello уровней Standard и Premium CDN предоставляют hello же функциональные возможности сжатия, но hello пользовательский интерфейс отличается.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-114">hello Standard and Premium CDN tiers provide hello same compression functionality, but hello user interface differs.</span></span>  <span data-ttu-id="a8eb8-115">Дополнительные сведения об отличиях hello уровней Standard и Premium CDN см. в разделе [Общие сведения о Azure CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a8eb8-115">For more information about hello differences between Standard and Premium CDN tiers, see [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

### <a name="standard-tier"></a><span data-ttu-id="a8eb8-116">Уровень Standard</span><span class="sxs-lookup"><span data-stu-id="a8eb8-116">Standard tier</span></span>
> [!NOTE]
> <span data-ttu-id="a8eb8-117">В этом разделе также применяется**Azure CDN Standard из Verizon** и **Azure CDN Standard из Akamai** профилей.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-117">This section applies too**Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles.</span></span>
> 
> 

1. <span data-ttu-id="a8eb8-118">На странице профиля CDN hello нажмите hello конечной точкой CDN необходимо toomanage.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-118">From hello CDN profile page, click hello CDN endpoint you wish toomanage.</span></span>
   
    ![Конечные точки на странице профиля CDN](./media/cdn-file-compression/cdn-endpoints.png)
   
    <span data-ttu-id="a8eb8-120">Откроется страница конечной точки CDN Hello.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-120">hello CDN endpoint page opens.</span></span>
2. <span data-ttu-id="a8eb8-121">Нажмите кнопку hello **Настройка** кнопки.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-121">Click hello **Configure** button.</span></span>
   
    ![Кнопка управления на странице профиля CDN](./media/cdn-file-compression/cdn-config-btn.png)
   
    <span data-ttu-id="a8eb8-123">Откроется страница конфигурации CDN Hello.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-123">hello CDN Configuration page opens.</span></span>
3. <span data-ttu-id="a8eb8-124">Включите параметр **Сжатие**.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-124">Turn on **Compression**.</span></span>
   
    ![Параметры сжатия CDN](./media/cdn-file-compression/cdn-compress-standard.png)
4. <span data-ttu-id="a8eb8-126">Используйте типы по умолчанию hello, или изменить список hello путем удаления или добавления типов файлов.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-126">Use hello default types, or modify hello list by removing or adding file types.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="a8eb8-127">Время, возможно, не рекомендуется tooapply сжатия toocompressed форматах, например ZIP, MP3, MP4, JPG и т. д.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-127">While possible, it is not recommended tooapply compression toocompressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span>
   > 
   > 
5. <span data-ttu-id="a8eb8-128">После внесения изменений, нажмите кнопку hello **Сохранить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-128">After making your changes, click hello **Save** button.</span></span>

### <a name="premium-tier"></a><span data-ttu-id="a8eb8-129">Уровень Premium</span><span class="sxs-lookup"><span data-stu-id="a8eb8-129">Premium tier</span></span>
> [!NOTE]
> <span data-ttu-id="a8eb8-130">В этом разделе также применяется**Azure CDN Premium из Verizon** профилей.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-130">This section applies too**Azure CDN Premium from Verizon** profiles.</span></span>
> 
> 

1. <span data-ttu-id="a8eb8-131">На странице профиля CDN hello нажмите hello **управление** кнопки.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-131">From hello CDN profile page, click hello **Manage** button.</span></span>
   
    ![Кнопка управления на странице профиля CDN](./media/cdn-file-compression/cdn-manage-btn.png)
   
    <span data-ttu-id="a8eb8-133">Открытие портала управления CDN Hello.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-133">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="a8eb8-134">Наведите указатель мыши hello **HTTP больших** , а затем наведите указатель мыши hello **параметры кэша** всплывающим меню.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-134">Hover over hello **HTTP Large** tab, then hover over hello **Cache Settings** flyout.</span></span>  <span data-ttu-id="a8eb8-135">Щелкните **Сжатие**.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-135">Click on **Compression**.</span></span>

    ![Выбор сжатия файлов](./media/cdn-file-compression/cdn-compress-select.png)
   
    <span data-ttu-id="a8eb8-137">Отобразятся параметры сжатия.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-137">Compression options are displayed.</span></span>
   
    ![Сжатие файлов](./media/cdn-file-compression/cdn-compress-files.png)
3. <span data-ttu-id="a8eb8-139">Включить сжатие, щелкнув hello **включить сжатие** переключатель.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-139">Enable compression by clicking hello **Compression Enabled** radio button.</span></span>  <span data-ttu-id="a8eb8-140">Введите типы MIME hello toocompress обратиться в виде списка с разделителями запятыми (без пробелов) в hello **типы файлов** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-140">Enter hello MIME types you wish toocompress as a comma-delimited list (no spaces) in hello **File Types** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="a8eb8-141">Время, возможно, не рекомендуется tooapply сжатия toocompressed форматах, например ZIP, MP3, MP4, JPG и т. д.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-141">While possible, it is not recommended tooapply compression toocompressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span> 
   > 
   > 
4. <span data-ttu-id="a8eb8-142">После внесения изменений, нажмите кнопку hello **обновление** кнопки.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-142">After making your changes, click hello **Update** button.</span></span>

## <a name="compression-rules"></a><span data-ttu-id="a8eb8-143">Правила сжатия</span><span class="sxs-lookup"><span data-stu-id="a8eb8-143">Compression rules</span></span>
<span data-ttu-id="a8eb8-144">В приведенных ниже таблицах описан принцип работы сжатия CDN Azure для всех сценариев.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-144">These tables describe Azure CDN compression behavior for every scenario.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8eb8-145">Для **Azure CDN от Verizon** (уровня "Стандартный" и "Премиум") будут сжаты только подходящие файлы.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-145">For **Azure CDN from Verizon** (Standard and Premium), only eligible files are compressed.</span></span>  <span data-ttu-id="a8eb8-146">toobe отсрочить сжатие файла необходимо:</span><span class="sxs-lookup"><span data-stu-id="a8eb8-146">toobe eligible for compression, a file must:</span></span>
> 
> * <span data-ttu-id="a8eb8-147">более 128 байт;</span><span class="sxs-lookup"><span data-stu-id="a8eb8-147">Be larger than 128 bytes.</span></span>
> * <span data-ttu-id="a8eb8-148">менее 1 МБ;</span><span class="sxs-lookup"><span data-stu-id="a8eb8-148">Be smaller than 1 MB.</span></span>
> 
> <span data-ttu-id="a8eb8-149">Для **Azure CDN от Akamai**сжатие допускается для всех файлов.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-149">For **Azure CDN from Akamai**, all files are eligible for compression.</span></span>
> 
> <span data-ttu-id="a8eb8-150">Во всех продуктах Azure CDN используется файл типа MIME, для которого [в настройках разрешено сжатие](#enabling-compression).</span><span class="sxs-lookup"><span data-stu-id="a8eb8-150">For all Azure CDN products, a file must be a MIME type that has been [configured for compression](#enabling-compression).</span></span>
> 
> <span data-ttu-id="a8eb8-151">Профили **Azure CDN от Verizon** (уровня "Стандартный" и "Премиум") поддерживают кодирование **GZIP** (GNU zip), **Deflate**, **BZIP2** или **BR** (Brotli).</span><span class="sxs-lookup"><span data-stu-id="a8eb8-151">**Azure CDN from Verizon** profiles (Standard and Premium) support **gzip** (GNU zip), **deflate**, **bzip2**, or  **br** (Brotli) encoding.</span></span> <span data-ttu-id="a8eb8-152">Для кодирования Brotli, hello сжатие выполняется только на границе hello.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-152">For Brotli encoding, hello compression is done only at hello edge.</span></span> <span data-ttu-id="a8eb8-153">Hello браузер должен отправить запрос hello для кодирования Brotli и сжатых активов hello должен сжаты на стороне источника hello сначала.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-153">hello client/browser must send hello request for Brotli encoding and hello compressed asset must have been compressed on hello origin side first.</span></span> 
>
><span data-ttu-id="a8eb8-154">Профили **Azure CDN от Akamai** поддерживают только кодирование **GZIP**.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-154">**Azure CDN from Akamai** profiles support only **gzip** encoding.</span></span>
> 
> <span data-ttu-id="a8eb8-155">**Azure CDN с Akamai** конечных точек всегда запрашивают **gzip** файлы из исходной hello, вне зависимости от запроса клиента hello кодировке.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-155">**Azure CDN from Akamai** endpoints always request **gzip** encoded files from hello origin, regardless of hello client request.</span></span> 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a><span data-ttu-id="a8eb8-156">Сжатие отключено или для файла сжатие недопустимо</span><span class="sxs-lookup"><span data-stu-id="a8eb8-156">Compression disabled or file is ineligible for compression</span></span>
| <span data-ttu-id="a8eb8-157">Запрошенный клиентом формат (через заголовок Accept-Encoding)</span><span class="sxs-lookup"><span data-stu-id="a8eb8-157">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="a8eb8-158">Кэшированный формат файла</span><span class="sxs-lookup"><span data-stu-id="a8eb8-158">Cached file format</span></span> | <span data-ttu-id="a8eb8-159">Клиент toohello CDN ответа</span><span class="sxs-lookup"><span data-stu-id="a8eb8-159">CDN response toohello client</span></span> | <span data-ttu-id="a8eb8-160">Примечания</span><span class="sxs-lookup"><span data-stu-id="a8eb8-160">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a8eb8-161">сжатые;</span><span class="sxs-lookup"><span data-stu-id="a8eb8-161">Compressed</span></span> |<span data-ttu-id="a8eb8-162">сжатые;</span><span class="sxs-lookup"><span data-stu-id="a8eb8-162">Compressed</span></span> |<span data-ttu-id="a8eb8-163">сжатые;</span><span class="sxs-lookup"><span data-stu-id="a8eb8-163">Compressed</span></span> | |
| <span data-ttu-id="a8eb8-164">сжатые;</span><span class="sxs-lookup"><span data-stu-id="a8eb8-164">Compressed</span></span> |<span data-ttu-id="a8eb8-165">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="a8eb8-165">Uncompressed</span></span> |<span data-ttu-id="a8eb8-166">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="a8eb8-166">Uncompressed</span></span> | |
| <span data-ttu-id="a8eb8-167">сжатые;</span><span class="sxs-lookup"><span data-stu-id="a8eb8-167">Compressed</span></span> |<span data-ttu-id="a8eb8-168">Не кэширован</span><span class="sxs-lookup"><span data-stu-id="a8eb8-168">Not cached</span></span> |<span data-ttu-id="a8eb8-169">Сжатый или несжатый</span><span class="sxs-lookup"><span data-stu-id="a8eb8-169">Compressed or Uncompressed</span></span> |<span data-ttu-id="a8eb8-170">Зависит от ответа источника</span><span class="sxs-lookup"><span data-stu-id="a8eb8-170">Depends on origin response</span></span> |
| <span data-ttu-id="a8eb8-171">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="a8eb8-171">Uncompressed</span></span> |<span data-ttu-id="a8eb8-172">сжатые;</span><span class="sxs-lookup"><span data-stu-id="a8eb8-172">Compressed</span></span> |<span data-ttu-id="a8eb8-173">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="a8eb8-173">Uncompressed</span></span> | |
| <span data-ttu-id="a8eb8-174">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="a8eb8-174">Uncompressed</span></span> |<span data-ttu-id="a8eb8-175">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="a8eb8-175">Uncompressed</span></span> |<span data-ttu-id="a8eb8-176">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="a8eb8-176">Uncompressed</span></span> | |
| <span data-ttu-id="a8eb8-177">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="a8eb8-177">Uncompressed</span></span> |<span data-ttu-id="a8eb8-178">Не кэширован</span><span class="sxs-lookup"><span data-stu-id="a8eb8-178">Not cached</span></span> |<span data-ttu-id="a8eb8-179">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="a8eb8-179">Uncompressed</span></span> | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a><span data-ttu-id="a8eb8-180">Сжатие включено и для файла допускается сжатие</span><span class="sxs-lookup"><span data-stu-id="a8eb8-180">Compression enabled and file is eligible for compression</span></span>
| <span data-ttu-id="a8eb8-181">Запрошенный клиентом формат (через заголовок Accept-Encoding)</span><span class="sxs-lookup"><span data-stu-id="a8eb8-181">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="a8eb8-182">Кэшированный формат файла</span><span class="sxs-lookup"><span data-stu-id="a8eb8-182">Cached file format</span></span> | <span data-ttu-id="a8eb8-183">Клиент toohello CDN ответа</span><span class="sxs-lookup"><span data-stu-id="a8eb8-183">CDN response toohello client</span></span> | <span data-ttu-id="a8eb8-184">Примечания</span><span class="sxs-lookup"><span data-stu-id="a8eb8-184">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a8eb8-185">сжатые;</span><span class="sxs-lookup"><span data-stu-id="a8eb8-185">Compressed</span></span> |<span data-ttu-id="a8eb8-186">сжатые;</span><span class="sxs-lookup"><span data-stu-id="a8eb8-186">Compressed</span></span> |<span data-ttu-id="a8eb8-187">сжатые;</span><span class="sxs-lookup"><span data-stu-id="a8eb8-187">Compressed</span></span> |<span data-ttu-id="a8eb8-188">CDN перекодирует из одного поддерживаемого формата в другой</span><span class="sxs-lookup"><span data-stu-id="a8eb8-188">CDN transcodes between supported formats</span></span> |
| <span data-ttu-id="a8eb8-189">сжатые;</span><span class="sxs-lookup"><span data-stu-id="a8eb8-189">Compressed</span></span> |<span data-ttu-id="a8eb8-190">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="a8eb8-190">Uncompressed</span></span> |<span data-ttu-id="a8eb8-191">сжатые;</span><span class="sxs-lookup"><span data-stu-id="a8eb8-191">Compressed</span></span> |<span data-ttu-id="a8eb8-192">CDN выполняет сжатие</span><span class="sxs-lookup"><span data-stu-id="a8eb8-192">CDN performs compression</span></span> |
| <span data-ttu-id="a8eb8-193">сжатые;</span><span class="sxs-lookup"><span data-stu-id="a8eb8-193">Compressed</span></span> |<span data-ttu-id="a8eb8-194">Не кэширован</span><span class="sxs-lookup"><span data-stu-id="a8eb8-194">Not cached</span></span> |<span data-ttu-id="a8eb8-195">сжатые;</span><span class="sxs-lookup"><span data-stu-id="a8eb8-195">Compressed</span></span> |<span data-ttu-id="a8eb8-196">CDN выполняет сжатие, если источник возвращает несжатый файл.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-196">CDN performs compression if origin returns uncompressed.</span></span>  <span data-ttu-id="a8eb8-197">**CDN Azure из Verizon** передает hello несжатого файла на первый запрос hello и затем сжимает и кэши hello файл для последующих запросов.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-197">**Azure CDN from Verizon** passes hello uncompressed file on hello first request and then compresses and caches hello file for subsequent requests.</span></span>  <span data-ttu-id="a8eb8-198">Файлы с заголовком `Cache-Control: no-cache` никогда не сжимаются.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-198">Files with `Cache-Control: no-cache` header will never be compressed.</span></span> |
| <span data-ttu-id="a8eb8-199">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="a8eb8-199">Uncompressed</span></span> |<span data-ttu-id="a8eb8-200">сжатые;</span><span class="sxs-lookup"><span data-stu-id="a8eb8-200">Compressed</span></span> |<span data-ttu-id="a8eb8-201">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="a8eb8-201">Uncompressed</span></span> |<span data-ttu-id="a8eb8-202">CDN проводит распаковку</span><span class="sxs-lookup"><span data-stu-id="a8eb8-202">CDN performs decompression</span></span> |
| <span data-ttu-id="a8eb8-203">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="a8eb8-203">Uncompressed</span></span> |<span data-ttu-id="a8eb8-204">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="a8eb8-204">Uncompressed</span></span> |<span data-ttu-id="a8eb8-205">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="a8eb8-205">Uncompressed</span></span> | |
| <span data-ttu-id="a8eb8-206">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="a8eb8-206">Uncompressed</span></span> |<span data-ttu-id="a8eb8-207">Не кэширован</span><span class="sxs-lookup"><span data-stu-id="a8eb8-207">Not cached</span></span> |<span data-ttu-id="a8eb8-208">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="a8eb8-208">Uncompressed</span></span> | |

## <a name="media-services-cdn-compression"></a><span data-ttu-id="a8eb8-209">Сжатие CDN для служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="a8eb8-209">Media Services CDN Compression</span></span>
<span data-ttu-id="a8eb8-210">Для конечных точек потоковой передачи с поддержкой CDN служб мультимедиа, сжатие включено по умолчанию для hello следующие типы содержимого: приложение/vnd.ms-sstr + xml, application/dash+xml,application/vnd.apple.mpegurl, приложения или f4m + xml.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-210">For Media Services CDN enabled streaming endpoints, compression is enabled by default for hello following content types: application/vnd.ms-sstr+xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m+xml.</span></span> <span data-ttu-id="a8eb8-211">Вы не удается включить/отключить сжатие для hello упомянутые типов с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a8eb8-211">You cannot enable/disable compression for hello mentioned types using hello Azure portal.</span></span>  

## <a name="see-also"></a><span data-ttu-id="a8eb8-212">См. также</span><span class="sxs-lookup"><span data-stu-id="a8eb8-212">See also</span></span>
* [<span data-ttu-id="a8eb8-213">Устранение неполадок со сжатием файлов CDN</span><span class="sxs-lookup"><span data-stu-id="a8eb8-213">Troubleshooting CDN file compression</span></span>](cdn-troubleshoot-compression.md)    

