---
title: "Повышение производительности за счет сжатия файлов в Azure CDN | Документация Майкрософт"
description: "В этом разделе описано, как ускорить передачу файла и повысить производительности загрузки страниц с помощью сжатия файлов в CDN Azure."
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
ms.openlocfilehash: 7546650e6096a880f4fb4d0c94dd4ecc00b70160
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a><span data-ttu-id="d2d0b-103">Повышение производительности за счет сжатия файлов в Azure CDN</span><span class="sxs-lookup"><span data-stu-id="d2d0b-103">Improve performance by compressing files in Azure CDN</span></span>
<span data-ttu-id="d2d0b-104">Сжатие файлов — это простой и эффективный способ, который позволяет повысить скорость передачи файлов и увеличить производительность загрузки страницы за счет уменьшения размера файлов перед их отправкой с сервера.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-104">Compression is a simple and effective method to improve file transfer speed and increase page load performance by reducing file size before it is sent from the server.</span></span> <span data-ttu-id="d2d0b-105">Этот позволяет снизить потребление пропускной способности и обеспечивает более высокую скорость работы для пользователей.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-105">It reduces bandwidth costs and provides a more responsive experience for your users.</span></span>

<span data-ttu-id="d2d0b-106">Сжатие файлов можно активировать двумя способами.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-106">There are two ways to enable compression:</span></span>

* <span data-ttu-id="d2d0b-107">Можно включить сжатие на сервер-источнике — в таком случае CDN обрабатывает сжатые файлы и доставляет их соответствующим клиентам.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-107">You can enable compression on your origin server, in which case the CDN passes through the compressed files and deliver compressed files to clients that request them.</span></span>
* <span data-ttu-id="d2d0b-108">Можно включить сжатие непосредственно на пограничных серверах CDN — в таком случае CDN сжимает файлы и доставляет их пользователям, даже если эти файлы не были сжаты на сервере-источнике.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-108">You can enable compression directly on CDN edge servers, in which case the CDN compresses the files and serve them to end users, even if they are not compressed by the origin server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d2d0b-109">Для распространения изменений конфигурации CDN по сети требуется некоторое время.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-109">CDN configuration changes take some time to propagate through the network.</span></span>  <span data-ttu-id="d2d0b-110">Для профилей <b>Azure CDN от Akamai</b> распространение обычно завершается в течение одной минуты.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-110">For <b>Azure CDN from Akamai</b> profiles, propagation usually completes in under one minute.</span></span>  <span data-ttu-id="d2d0b-111">Для профилей <b>Azure CDN от Verizon</b> изменения вступают в силу в течение 90 минут.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-111">For <b>Azure CDN from Verizon</b> profiles, you will usually see your changes apply within 90 minutes.</span></span>  <span data-ttu-id="d2d0b-112">Если сжатие для конечной точки CDN задается впервые, перед устранением неполадок следует подождать 1–2 часа, чтобы настройки сжатия гарантированно распространились на серверы POP.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-112">If this is the first time you've set up compression for your CDN endpoint, you should consider waiting 1-2 hours to be sure the compression settings have propagated to the POPs before troubleshooting</span></span>
> 
> 

## <a name="enabling-compression"></a><span data-ttu-id="d2d0b-113">Включение сжатия</span><span class="sxs-lookup"><span data-stu-id="d2d0b-113">Enabling compression</span></span>
> [!NOTE]
> <span data-ttu-id="d2d0b-114">Уровни CDN «Стандартный» и «Премиум» предоставляют одинаковые возможности сжатия, но разные пользовательские интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-114">The Standard and Premium CDN tiers provide the same compression functionality, but the user interface differs.</span></span>  <span data-ttu-id="d2d0b-115">Дополнительные сведения о различиях между уровнями CDN "Стандартный" и "Премиум" см. в разделе [Обзор Azure CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d2d0b-115">For more information about the differences between Standard and Premium CDN tiers, see [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

### <a name="standard-tier"></a><span data-ttu-id="d2d0b-116">Уровень Standard</span><span class="sxs-lookup"><span data-stu-id="d2d0b-116">Standard tier</span></span>
> [!NOTE]
> <span data-ttu-id="d2d0b-117">Сведения в этом разделе относятся к профилям **Azure CDN уровня "Стандартный" от Verizon** и **Azure CDN уровня "Стандартный" от Akamai**.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-117">This section applies to **Azure CDN Standard from Verizon** and **Azure CDN Standard from Akamai** profiles.</span></span>
> 
> 

1. <span data-ttu-id="d2d0b-118">На странице профиля CDN щелкните конечную точку CDN, которой хотите управлять.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-118">From the CDN profile page, click the CDN endpoint you wish to manage.</span></span>
   
    ![Конечные точки на странице профиля CDN](./media/cdn-file-compression/cdn-endpoints.png)
   
    <span data-ttu-id="d2d0b-120">Откроется страница конечной точки CDN.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-120">The CDN endpoint page opens.</span></span>
2. <span data-ttu-id="d2d0b-121">Нажмите кнопку **Настроить** .</span><span class="sxs-lookup"><span data-stu-id="d2d0b-121">Click the **Configure** button.</span></span>
   
    ![Кнопка управления на странице профиля CDN](./media/cdn-file-compression/cdn-config-btn.png)
   
    <span data-ttu-id="d2d0b-123">Откроется страница настройки CDN.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-123">The CDN Configuration page opens.</span></span>
3. <span data-ttu-id="d2d0b-124">Включите параметр **Сжатие**.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-124">Turn on **Compression**.</span></span>
   
    ![Параметры сжатия CDN](./media/cdn-file-compression/cdn-compress-standard.png)
4. <span data-ttu-id="d2d0b-126">Используйте типы по умолчанию либо измените список, удалив или добавив типы файлов.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-126">Use the default types, or modify the list by removing or adding file types.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="d2d0b-127">Хотя это и возможно, тем не менее не рекомендуется применять сжатие для сжатых форматов, таких как ZIP, MP3, MP4, JPG и т. д.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-127">While possible, it is not recommended to apply compression to compressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span>
   > 
   > 
5. <span data-ttu-id="d2d0b-128">Внеся необходимые изменения, нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="d2d0b-128">After making your changes, click the **Save** button.</span></span>

### <a name="premium-tier"></a><span data-ttu-id="d2d0b-129">Уровень Premium</span><span class="sxs-lookup"><span data-stu-id="d2d0b-129">Premium tier</span></span>
> [!NOTE]
> <span data-ttu-id="d2d0b-130">Сведения в этом разделе относятся к профилям **Azure CDN уровня "Премиум" от Verizon** .</span><span class="sxs-lookup"><span data-stu-id="d2d0b-130">This section applies to **Azure CDN Premium from Verizon** profiles.</span></span>
> 
> 

1. <span data-ttu-id="d2d0b-131">На странице профиля сети CDN нажмите кнопку **Управление**.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-131">From the CDN profile page, click the **Manage** button.</span></span>
   
    ![Кнопка управления на странице профиля CDN](./media/cdn-file-compression/cdn-manage-btn.png)
   
    <span data-ttu-id="d2d0b-133">Откроется портал управления CDN.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-133">The CDN management portal opens.</span></span>
2. <span data-ttu-id="d2d0b-134">Наведите указатель мыши на вкладку **HTTP Large** (Большая платформа HTTP), а затем наведите указатель мыши на всплывающий элемент **Параметры кэша**.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-134">Hover over the **HTTP Large** tab, then hover over the **Cache Settings** flyout.</span></span>  <span data-ttu-id="d2d0b-135">Щелкните **Сжатие**.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-135">Click on **Compression**.</span></span>

    ![Выбор сжатия файлов](./media/cdn-file-compression/cdn-compress-select.png)
   
    <span data-ttu-id="d2d0b-137">Отобразятся параметры сжатия.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-137">Compression options are displayed.</span></span>
   
    ![Сжатие файлов](./media/cdn-file-compression/cdn-compress-files.png)
3. <span data-ttu-id="d2d0b-139">Включите сжатие, установив переключатель **Использовать сжатие** .</span><span class="sxs-lookup"><span data-stu-id="d2d0b-139">Enable compression by clicking the **Compression Enabled** radio button.</span></span>  <span data-ttu-id="d2d0b-140">Введите типы MIME для сжатия в виде списка с разделителями-запятыми (без пробелов) в текстовом поле **Типы файлов** .</span><span class="sxs-lookup"><span data-stu-id="d2d0b-140">Enter the MIME types you wish to compress as a comma-delimited list (no spaces) in the **File Types** textbox.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="d2d0b-141">Хотя это и возможно, тем не менее не рекомендуется применять сжатие для сжатых форматов, таких как ZIP, MP3, MP4, JPG и т. д.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-141">While possible, it is not recommended to apply compression to compressed formats, such as ZIP, MP3, MP4, JPG, etc.</span></span> 
   > 
   > 
4. <span data-ttu-id="d2d0b-142">Внеся необходимые изменения, нажмите кнопку **Обновить** .</span><span class="sxs-lookup"><span data-stu-id="d2d0b-142">After making your changes, click the **Update** button.</span></span>

## <a name="compression-rules"></a><span data-ttu-id="d2d0b-143">Правила сжатия</span><span class="sxs-lookup"><span data-stu-id="d2d0b-143">Compression rules</span></span>
<span data-ttu-id="d2d0b-144">В приведенных ниже таблицах описан принцип работы сжатия CDN Azure для всех сценариев.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-144">These tables describe Azure CDN compression behavior for every scenario.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d2d0b-145">Для **Azure CDN от Verizon** (уровня "Стандартный" и "Премиум") будут сжаты только подходящие файлы.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-145">For **Azure CDN from Verizon** (Standard and Premium), only eligible files are compressed.</span></span>  <span data-ttu-id="d2d0b-146">Сжатие допускается для следующих файлов:</span><span class="sxs-lookup"><span data-stu-id="d2d0b-146">To be eligible for compression, a file must:</span></span>
> 
> * <span data-ttu-id="d2d0b-147">более 128 байт;</span><span class="sxs-lookup"><span data-stu-id="d2d0b-147">Be larger than 128 bytes.</span></span>
> * <span data-ttu-id="d2d0b-148">менее 1 МБ;</span><span class="sxs-lookup"><span data-stu-id="d2d0b-148">Be smaller than 1 MB.</span></span>
> 
> <span data-ttu-id="d2d0b-149">Для **Azure CDN от Akamai**сжатие допускается для всех файлов.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-149">For **Azure CDN from Akamai**, all files are eligible for compression.</span></span>
> 
> <span data-ttu-id="d2d0b-150">Во всех продуктах Azure CDN используется файл типа MIME, для которого [в настройках разрешено сжатие](#enabling-compression).</span><span class="sxs-lookup"><span data-stu-id="d2d0b-150">For all Azure CDN products, a file must be a MIME type that has been [configured for compression](#enabling-compression).</span></span>
> 
> <span data-ttu-id="d2d0b-151">Профили **Azure CDN от Verizon** (уровня "Стандартный" и "Премиум") поддерживают кодирование **GZIP** (GNU zip), **Deflate**, **BZIP2** или **BR** (Brotli).</span><span class="sxs-lookup"><span data-stu-id="d2d0b-151">**Azure CDN from Verizon** profiles (Standard and Premium) support **gzip** (GNU zip), **deflate**, **bzip2**, or  **br** (Brotli) encoding.</span></span> <span data-ttu-id="d2d0b-152">Для кодирования Brotli сжатие выполняется только на границе сред.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-152">For Brotli encoding, the compression is done only at the edge.</span></span> <span data-ttu-id="d2d0b-153">Клиент (или браузер) должен отправить запрос на кодирование Brotli, а сжатый ресурс необходимо сначала сжать на стороне источника.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-153">The client/browser must send the request for Brotli encoding and the compressed asset must have been compressed on the origin side first.</span></span> 
>
><span data-ttu-id="d2d0b-154">Профили **Azure CDN от Akamai** поддерживают только кодирование **GZIP**.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-154">**Azure CDN from Akamai** profiles support only **gzip** encoding.</span></span>
> 
> <span data-ttu-id="d2d0b-155">Конечные точки **Azure CDN от Akamai** всегда запрашивают из сервера-источника файлы в формате **GZIP** независимо от запроса клиента.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-155">**Azure CDN from Akamai** endpoints always request **gzip** encoded files from the origin, regardless of the client request.</span></span> 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a><span data-ttu-id="d2d0b-156">Сжатие отключено или для файла сжатие недопустимо</span><span class="sxs-lookup"><span data-stu-id="d2d0b-156">Compression disabled or file is ineligible for compression</span></span>
| <span data-ttu-id="d2d0b-157">Запрошенный клиентом формат (через заголовок Accept-Encoding)</span><span class="sxs-lookup"><span data-stu-id="d2d0b-157">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="d2d0b-158">Кэшированный формат файла</span><span class="sxs-lookup"><span data-stu-id="d2d0b-158">Cached file format</span></span> | <span data-ttu-id="d2d0b-159">Ответ CDN клиенту</span><span class="sxs-lookup"><span data-stu-id="d2d0b-159">CDN response to the client</span></span> | <span data-ttu-id="d2d0b-160">Примечания</span><span class="sxs-lookup"><span data-stu-id="d2d0b-160">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d2d0b-161">сжатые;</span><span class="sxs-lookup"><span data-stu-id="d2d0b-161">Compressed</span></span> |<span data-ttu-id="d2d0b-162">сжатые;</span><span class="sxs-lookup"><span data-stu-id="d2d0b-162">Compressed</span></span> |<span data-ttu-id="d2d0b-163">сжатые;</span><span class="sxs-lookup"><span data-stu-id="d2d0b-163">Compressed</span></span> | |
| <span data-ttu-id="d2d0b-164">сжатые;</span><span class="sxs-lookup"><span data-stu-id="d2d0b-164">Compressed</span></span> |<span data-ttu-id="d2d0b-165">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="d2d0b-165">Uncompressed</span></span> |<span data-ttu-id="d2d0b-166">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="d2d0b-166">Uncompressed</span></span> | |
| <span data-ttu-id="d2d0b-167">сжатые;</span><span class="sxs-lookup"><span data-stu-id="d2d0b-167">Compressed</span></span> |<span data-ttu-id="d2d0b-168">Не кэширован</span><span class="sxs-lookup"><span data-stu-id="d2d0b-168">Not cached</span></span> |<span data-ttu-id="d2d0b-169">Сжатый или несжатый</span><span class="sxs-lookup"><span data-stu-id="d2d0b-169">Compressed or Uncompressed</span></span> |<span data-ttu-id="d2d0b-170">Зависит от ответа источника</span><span class="sxs-lookup"><span data-stu-id="d2d0b-170">Depends on origin response</span></span> |
| <span data-ttu-id="d2d0b-171">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="d2d0b-171">Uncompressed</span></span> |<span data-ttu-id="d2d0b-172">сжатые;</span><span class="sxs-lookup"><span data-stu-id="d2d0b-172">Compressed</span></span> |<span data-ttu-id="d2d0b-173">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="d2d0b-173">Uncompressed</span></span> | |
| <span data-ttu-id="d2d0b-174">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="d2d0b-174">Uncompressed</span></span> |<span data-ttu-id="d2d0b-175">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="d2d0b-175">Uncompressed</span></span> |<span data-ttu-id="d2d0b-176">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="d2d0b-176">Uncompressed</span></span> | |
| <span data-ttu-id="d2d0b-177">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="d2d0b-177">Uncompressed</span></span> |<span data-ttu-id="d2d0b-178">Не кэширован</span><span class="sxs-lookup"><span data-stu-id="d2d0b-178">Not cached</span></span> |<span data-ttu-id="d2d0b-179">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="d2d0b-179">Uncompressed</span></span> | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a><span data-ttu-id="d2d0b-180">Сжатие включено и для файла допускается сжатие</span><span class="sxs-lookup"><span data-stu-id="d2d0b-180">Compression enabled and file is eligible for compression</span></span>
| <span data-ttu-id="d2d0b-181">Запрошенный клиентом формат (через заголовок Accept-Encoding)</span><span class="sxs-lookup"><span data-stu-id="d2d0b-181">Client requested format (via Accept-Encoding header)</span></span> | <span data-ttu-id="d2d0b-182">Кэшированный формат файла</span><span class="sxs-lookup"><span data-stu-id="d2d0b-182">Cached file format</span></span> | <span data-ttu-id="d2d0b-183">Ответ CDN клиенту</span><span class="sxs-lookup"><span data-stu-id="d2d0b-183">CDN response to the client</span></span> | <span data-ttu-id="d2d0b-184">Примечания</span><span class="sxs-lookup"><span data-stu-id="d2d0b-184">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d2d0b-185">сжатые;</span><span class="sxs-lookup"><span data-stu-id="d2d0b-185">Compressed</span></span> |<span data-ttu-id="d2d0b-186">сжатые;</span><span class="sxs-lookup"><span data-stu-id="d2d0b-186">Compressed</span></span> |<span data-ttu-id="d2d0b-187">сжатые;</span><span class="sxs-lookup"><span data-stu-id="d2d0b-187">Compressed</span></span> |<span data-ttu-id="d2d0b-188">CDN перекодирует из одного поддерживаемого формата в другой</span><span class="sxs-lookup"><span data-stu-id="d2d0b-188">CDN transcodes between supported formats</span></span> |
| <span data-ttu-id="d2d0b-189">сжатые;</span><span class="sxs-lookup"><span data-stu-id="d2d0b-189">Compressed</span></span> |<span data-ttu-id="d2d0b-190">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="d2d0b-190">Uncompressed</span></span> |<span data-ttu-id="d2d0b-191">сжатые;</span><span class="sxs-lookup"><span data-stu-id="d2d0b-191">Compressed</span></span> |<span data-ttu-id="d2d0b-192">CDN выполняет сжатие</span><span class="sxs-lookup"><span data-stu-id="d2d0b-192">CDN performs compression</span></span> |
| <span data-ttu-id="d2d0b-193">сжатые;</span><span class="sxs-lookup"><span data-stu-id="d2d0b-193">Compressed</span></span> |<span data-ttu-id="d2d0b-194">Не кэширован</span><span class="sxs-lookup"><span data-stu-id="d2d0b-194">Not cached</span></span> |<span data-ttu-id="d2d0b-195">сжатые;</span><span class="sxs-lookup"><span data-stu-id="d2d0b-195">Compressed</span></span> |<span data-ttu-id="d2d0b-196">CDN выполняет сжатие, если источник возвращает несжатый файл.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-196">CDN performs compression if origin returns uncompressed.</span></span>  <span data-ttu-id="d2d0b-197">**Azure CDN от Verizon** передает несжатый файл при первом запросе, а затем сжимает файл и помещает его в кэш для последующих запросов.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-197">**Azure CDN from Verizon** passes the uncompressed file on the first request and then compresses and caches the file for subsequent requests.</span></span>  <span data-ttu-id="d2d0b-198">Файлы с заголовком `Cache-Control: no-cache` никогда не сжимаются.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-198">Files with `Cache-Control: no-cache` header will never be compressed.</span></span> |
| <span data-ttu-id="d2d0b-199">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="d2d0b-199">Uncompressed</span></span> |<span data-ttu-id="d2d0b-200">сжатые;</span><span class="sxs-lookup"><span data-stu-id="d2d0b-200">Compressed</span></span> |<span data-ttu-id="d2d0b-201">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="d2d0b-201">Uncompressed</span></span> |<span data-ttu-id="d2d0b-202">CDN проводит распаковку</span><span class="sxs-lookup"><span data-stu-id="d2d0b-202">CDN performs decompression</span></span> |
| <span data-ttu-id="d2d0b-203">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="d2d0b-203">Uncompressed</span></span> |<span data-ttu-id="d2d0b-204">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="d2d0b-204">Uncompressed</span></span> |<span data-ttu-id="d2d0b-205">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="d2d0b-205">Uncompressed</span></span> | |
| <span data-ttu-id="d2d0b-206">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="d2d0b-206">Uncompressed</span></span> |<span data-ttu-id="d2d0b-207">Не кэширован</span><span class="sxs-lookup"><span data-stu-id="d2d0b-207">Not cached</span></span> |<span data-ttu-id="d2d0b-208">Без сжатия</span><span class="sxs-lookup"><span data-stu-id="d2d0b-208">Uncompressed</span></span> | |

## <a name="media-services-cdn-compression"></a><span data-ttu-id="d2d0b-209">Сжатие CDN для служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="d2d0b-209">Media Services CDN Compression</span></span>
<span data-ttu-id="d2d0b-210">Для конечных точек потоковой передачи служб мультимедиа с CDN сжатие включено по умолчанию для следующих типов содержимого: application/vnd.ms-sstr+xml, application/dash+xml, application/vnd.apple.mpegurl, application/f4m+xml.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-210">For Media Services CDN enabled streaming endpoints, compression is enabled by default for the following content types: application/vnd.ms-sstr+xml, application/dash+xml,application/vnd.apple.mpegurl, application/f4m+xml.</span></span> <span data-ttu-id="d2d0b-211">Вы не может включить или отключить сжатие для упомянутых выше типов с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="d2d0b-211">You cannot enable/disable compression for the mentioned types using the Azure portal.</span></span>  

## <a name="see-also"></a><span data-ttu-id="d2d0b-212">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="d2d0b-212">See also</span></span>
* [<span data-ttu-id="d2d0b-213">Устранение неполадок со сжатием файлов CDN</span><span class="sxs-lookup"><span data-stu-id="d2d0b-213">Troubleshooting CDN file compression</span></span>](cdn-troubleshoot-compression.md)    

