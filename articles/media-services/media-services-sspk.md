---
title: "Microsoft® Smooth Streaming Client Porting Kit aaaLicensing"
description: "Дополнительные сведения о том, как toolicensing hello Microsoft® Smooth Streaming Client Porting Kit."
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: e3b488e7-8428-4c10-a072-eb3af46c82ad
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: xpouyat
ms.openlocfilehash: 56c3dccda73dd02207bb4dbe8109ba6fda917a6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-microsoft-smooth-streaming-client-porting-kit"></a><span data-ttu-id="59e67-103">Лицензирование пакета для портирования клиента бесперебойной потоковой передачи Microsoft® Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="59e67-103">Licensing Microsoft® Smooth Streaming Client Porting Kit</span></span>
## <a name="overview"></a><span data-ttu-id="59e67-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="59e67-104">Overview</span></span>
<span data-ttu-id="59e67-105">Microsoft Smooth Streaming Client Porting Kit (**SSPK** сокращенно) является реализация клиента Smooth Streaming оптимизированного toohelp внедренных производителя устройства, кабелей и операторам мобильной связи, поставщикам служб контента, переносные Изготовители, независимые поставщики (ISV) и решение поставщики toocreate продуктов и служб для адаптивной потоковой передачи содержимого в формат Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="59e67-105">Microsoft Smooth Streaming Client Porting Kit (**SSPK** for short) is a Smooth Streaming client implementation that is optimized toohelp embedded device manufacturers, cable and mobile operators, content service providers, handset manufacturers, independent software vendors (ISVs), and solution providers toocreate products and services for streaming adaptive streaming content in Smooth Streaming format.</span></span> <span data-ttu-id="59e67-106">SSPK — устройств и платформ независимых реализация клиента Smooth Streaming, который может быть перенесена с hello Лицензиат tooany устройств и платформ.</span><span class="sxs-lookup"><span data-stu-id="59e67-106">SSPK is a device and platform independent implementation of Smooth Streaming client that can be ported by hello licensee tooany device and platform.</span></span> 

<span data-ttu-id="59e67-107">Ниже приведены высокоуровневая архитектура и поле IIS Smooth Streaming Porting Kit реализации Smooth Streaming Client hello, предоставляемых корпорацией Майкрософт и включает в себя все hello основную логику для воспроизведения содержимого Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="59e67-107">Included below is a high level architecture and IIS Smooth Streaming Porting Kit box is hello Smooth Streaming Client implementation provided by Microsoft and includes all hello core logic for playback of Smooth Streaming content.</span></span> <span data-ttu-id="59e67-108">Партнеры затем портируют его на конкретное устройство или платформу, создавая соответствующие интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="59e67-108">This is then ported by partners for a specific device or platform by implementing appropriate interfaces.</span></span> 

![SSPK](./media/media-services-sspk/sspk-arch.png)

## <a name="description"></a><span data-ttu-id="59e67-110">Описание</span><span class="sxs-lookup"><span data-stu-id="59e67-110">Description</span></span>
<span data-ttu-id="59e67-111">Условия лицензирования SSPK повышают коммерческую ценность этого предложения.</span><span class="sxs-lookup"><span data-stu-id="59e67-111">SSPK is licensed on terms that offer excellent business value.</span></span> <span data-ttu-id="59e67-112">SSPK лицензия обеспечивает hello отрасли с:</span><span class="sxs-lookup"><span data-stu-id="59e67-112">SSPK license provides hello industry with:</span></span>

* <span data-ttu-id="59e67-113">Исходный код пакета для портирования Smooth Streaming на языке C++, в котором:</span><span class="sxs-lookup"><span data-stu-id="59e67-113">Smooth Streaming Porting Kit source in C++</span></span> 
  * <span data-ttu-id="59e67-114">реализованы функции клиента Smooth Streaming;</span><span class="sxs-lookup"><span data-stu-id="59e67-114">implements Smooth Streaming Client functionality</span></span>
  * <span data-ttu-id="59e67-115">добавлены возможности синтаксического и эвристического анализа, логика буферизации и другие функции.</span><span class="sxs-lookup"><span data-stu-id="59e67-115">adds format parsing, heuristics, buffering logic, etc.</span></span>
* <span data-ttu-id="59e67-116">API-интерфейсы приложения проигрывателя.</span><span class="sxs-lookup"><span data-stu-id="59e67-116">Player application APIs</span></span> 
  * <span data-ttu-id="59e67-117">Программные интерфейсы для взаимодействия с приложением Проигрывателя мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="59e67-117">programming interfaces for interaction with a media player application</span></span>
* <span data-ttu-id="59e67-118">Интерфейс слоя платформенных абстракций (PAL).</span><span class="sxs-lookup"><span data-stu-id="59e67-118">Platform Abstraction Layer (PAL) Interface</span></span> 
  * <span data-ttu-id="59e67-119">интерфейсы программирования для взаимодействия с операционной системой hello (потоки, сокеты)</span><span class="sxs-lookup"><span data-stu-id="59e67-119">programming interfaces for interaction with hello operating system (threads, sockets)</span></span>
* <span data-ttu-id="59e67-120">Интерфейс слоя аппаратных абстракций (HAL).</span><span class="sxs-lookup"><span data-stu-id="59e67-120">Hardware Abstraction Layer (HAL) Interface</span></span> 
  * <span data-ttu-id="59e67-121">Программные интерфейсы для взаимодействия с аппаратным оборудованием аудио- и видеодекодеров (декодирование, отрисовка).</span><span class="sxs-lookup"><span data-stu-id="59e67-121">programming interfaces for interaction with hardware A/V decoders (decoding, rendering)</span></span>
* <span data-ttu-id="59e67-122">Интерфейс управления цифровыми правами (DRM).</span><span class="sxs-lookup"><span data-stu-id="59e67-122">Digital Rights Management (DRM) Interface</span></span> 
  * <span data-ttu-id="59e67-123">интерфейсы программирования для обработки DRM через hello DRM Abstraction Layer (DAL)</span><span class="sxs-lookup"><span data-stu-id="59e67-123">programming interfaces for handling DRM through hello DRM Abstraction Layer (DAL)</span></span>
  * <span data-ttu-id="59e67-124">Пакет для портирования Microsoft PlayReady поставляется отдельно, но интегрируется через этот интерфейс.</span><span class="sxs-lookup"><span data-stu-id="59e67-124">Microsoft PlayReady Porting Kit ships separately but integrates through this interface.</span></span> <span data-ttu-id="59e67-125">Дополнительные сведения о лицензировании устройств Microsoft PlayReady приводятся [здесь](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span><span class="sxs-lookup"><span data-stu-id="59e67-125">For more details on Microsoft PlayReady Device licensing, click [here](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span></span>
* <span data-ttu-id="59e67-126">Примеры реализации</span><span class="sxs-lookup"><span data-stu-id="59e67-126">Implementation samples</span></span> 
  * <span data-ttu-id="59e67-127">Пример реализации PAL для Linux</span><span class="sxs-lookup"><span data-stu-id="59e67-127">sample PAL implementation for Linux</span></span>
  * <span data-ttu-id="59e67-128">Пример реализации HAL для GStreamer</span><span class="sxs-lookup"><span data-stu-id="59e67-128">sample HAL implementation for GStreamer</span></span>

## <a name="licensing-options"></a><span data-ttu-id="59e67-129">Варианты лицензирования</span><span class="sxs-lookup"><span data-stu-id="59e67-129">Licensing Options</span></span>
<span data-ttu-id="59e67-130">Microsoft Smooth Streaming Client Porting Kit выполняется через два различных соглашения доступны toolicensees: один для разработки Smooth Streaming в промежуточный клиенты, а другой для распространения пользователи tooend Smooth Streaming клиента готовой продукции.</span><span class="sxs-lookup"><span data-stu-id="59e67-130">Microsoft Smooth Streaming Client Porting Kit is made available toolicensees under two distinct license agreements: one for developing Smooth Streaming Client Interim Products and another for distributing Smooth Streaming Client Final Products tooend users.</span></span>

* <span data-ttu-id="59e67-131">Для изготовителей микросхем, системных интеграторов или независимые поставщики (ISV), которым требуется перенос кода источника комплект toodevelop продуктов промежуточная Microsoft Smooth Streaming Client Porting Kit **лицензии продукта промежуточная** должны быть выполнены.</span><span class="sxs-lookup"><span data-stu-id="59e67-131">For chipset manufacturers, system integrators, or independent software vendors (ISVs) who require a source code porting kit toodevelop Interim Products, a Microsoft Smooth Streaming Client Porting Kit **Interim Product License** should be executed.</span></span>
* <span data-ttu-id="59e67-132">Для производителей и независимые поставщики программного обеспечения, которым требуются права распространения для пользователей tooend Smooth Streaming клиента готовой продукции, hello Microsoft Smooth Streaming Client Porting Kit **лицензии конечного продукта** должны быть выполнены.</span><span class="sxs-lookup"><span data-stu-id="59e67-132">For device manufacturers or ISVs who require distribution rights for Smooth Streaming Client Final Products tooend users, hello Microsoft Smooth Streaming Client Porting Kit **Final Product License** should be executed.</span></span>

### <a name="microsoft-smooth-streaming-client-porting-kit-interim-product-license"></a><span data-ttu-id="59e67-133">Лицензия на промежуточный продукт пакета портирования клиента Microsoft Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="59e67-133">Microsoft Smooth Streaming Client Porting Kit Interim Product License</span></span>
<span data-ttu-id="59e67-134">В рамках данной лицензии Microsoft предлагает Smooth Streaming Client Porting Kit и hello toodevelop необходимые авторских прав и распространять Лицензиаты устройства Smooth Streaming Client Porting Kit для Smooth Streaming в промежуточный клиенты tooother, Распространите Smooth Streaming клиента готовой продукции.</span><span class="sxs-lookup"><span data-stu-id="59e67-134">Under this license, Microsoft offers a Smooth Streaming Client Porting Kit and hello necessary intellectual property rights toodevelop and distribute Smooth Streaming Client Interim Products tooother Smooth Streaming Client Porting Kit device licensees that distribute Smooth Streaming Client Final Products.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="59e67-135">Структура выплат</span><span class="sxs-lookup"><span data-stu-id="59e67-135">Fee structure</span></span>
<span data-ttu-id="59e67-136">Сбор разовой лицензии 50 000 долларов предоставляет доступ toohello Smooth Streaming Client Porting Kit.</span><span class="sxs-lookup"><span data-stu-id="59e67-136">A U.S. $50,000 one-time license fee provides access toohello Smooth Streaming Client Porting Kit.</span></span> 

### <a name="microsoft-smooth-streaming-client-porting-kit-final-product-license"></a><span data-ttu-id="59e67-137">Лицензия на конечный продукт пакета портирования клиента Microsoft Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="59e67-137">Microsoft Smooth Streaming Client Porting Kit Final Product License</span></span>
<span data-ttu-id="59e67-138">В рамках данной лицензии Корпорация Майкрософт предлагает все необходимые tooreceive права интеллектуальной собственности Smooth Streaming в промежуточный клиенты из других Smooth Streaming Client Porting Kit Лицензиатов и toodistribute фирменной символикой Smooth Streaming клиента окончательный Пользователи tooend продуктов.</span><span class="sxs-lookup"><span data-stu-id="59e67-138">Under this license, Microsoft offers all necessary intellectual property rights tooreceive Smooth Streaming Client Interim Products from other Smooth Streaming Client Porting Kit licensees and toodistribute company-branded Smooth Streaming Client Final Products tooend users.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="59e67-139">Структура выплат</span><span class="sxs-lookup"><span data-stu-id="59e67-139">Fee structure</span></span>
<span data-ttu-id="59e67-140">в разделе авторских отчислений модель, что и в разделе предлагается Hello Smooth Streaming клиента окончательной версии продукта:</span><span class="sxs-lookup"><span data-stu-id="59e67-140">hello Smooth Streaming Client Final Product is offered under a royalty model as under:</span></span>

* <span data-ttu-id="59e67-141">По 0,10 доллара США за каждое отправленное устройство, в котором используется конечный продукт.</span><span class="sxs-lookup"><span data-stu-id="59e67-141">$0.10 per device implementation shipped</span></span>
* <span data-ttu-id="59e67-142">прямые Hello ограничен $ 50 000 каждый год</span><span class="sxs-lookup"><span data-stu-id="59e67-142">hello royalty is capped at $50,000 each year</span></span>
* <span data-ttu-id="59e67-143">Отсутствие отчислений за первые 10 000 устройств в течение каждого года.</span><span class="sxs-lookup"><span data-stu-id="59e67-143">No royalty for first 10,000 device implementations each year</span></span> 

## <a name="licensing-procedure-and-sspk-access"></a><span data-ttu-id="59e67-144">Процедура лицензирования и доступ к SSPK.</span><span class="sxs-lookup"><span data-stu-id="59e67-144">Licensing Procedure and SSPK access</span></span>
<span data-ttu-id="59e67-145">Все запросы на лицензирование отправляйте по электронной почте на адрес [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) .</span><span class="sxs-lookup"><span data-stu-id="59e67-145">Please email [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) for all licensing queries.</span></span>

<span data-ttu-id="59e67-146">Hello [SSPK распространения портала](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) — доступны tooregistered промежуточная Лицензиаты.</span><span class="sxs-lookup"><span data-stu-id="59e67-146">hello [SSPK Distribution portal](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) is accessible tooregistered Interim licensees.</span></span>

<span data-ttu-id="59e67-147">Промежуточные и окончательный SSPK Лицензиаты могут отправлять технические вопросы слишком[smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="59e67-147">Interim and Final SSPK licensees can submit technical questions too[smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span></span>

## <a name="microsoft-smooth-streaming-client-interim-product-agreement-licensees"></a><span data-ttu-id="59e67-148">Обладатели лицензий на промежуточный продукт пакета для портирования клиента Microsoft Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="59e67-148">Microsoft Smooth Streaming Client Interim Product Agreement Licensees</span></span>
* <span data-ttu-id="59e67-149">Adroit Business Solutions, Inc</span><span class="sxs-lookup"><span data-stu-id="59e67-149">Adroit Business Solutions, Inc</span></span>
* <span data-ttu-id="59e67-150">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="59e67-150">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="59e67-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="59e67-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="59e67-152">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="59e67-152">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="59e67-153">Alticast Corporation</span><span class="sxs-lookup"><span data-stu-id="59e67-153">Alticast Corporation</span></span>
* <span data-ttu-id="59e67-154">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="59e67-154">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="59e67-155">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="59e67-155">Arion Technology, Inc.</span></span>
* <span data-ttu-id="59e67-156">AVC Multimedia Software Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="59e67-156">AVC Multimedia Software Co., Ltd.</span></span>
* <span data-ttu-id="59e67-157">Cavium, Inc.</span><span class="sxs-lookup"><span data-stu-id="59e67-157">Cavium, Inc.</span></span>
* <span data-ttu-id="59e67-158">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="59e67-158">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="59e67-159">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="59e67-159">Enseo, Inc.</span></span>
* <span data-ttu-id="59e67-160">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="59e67-160">Fluendo S.A.</span></span>
* <span data-ttu-id="59e67-161">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="59e67-161">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="59e67-162">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="59e67-162">Infomir GMBH</span></span>
* <span data-ttu-id="59e67-163">Irdeto USA Inc.</span><span class="sxs-lookup"><span data-stu-id="59e67-163">Irdeto USA Inc.</span></span>
* <span data-ttu-id="59e67-164">iWEDIA S.A.</span><span class="sxs-lookup"><span data-stu-id="59e67-164">iWEDIA S.A.</span></span> 
* <span data-ttu-id="59e67-165">Liberty Global Services BV</span><span class="sxs-lookup"><span data-stu-id="59e67-165">Liberty Global Services BV</span></span>
* <span data-ttu-id="59e67-166">MediaTek Inc.</span><span class="sxs-lookup"><span data-stu-id="59e67-166">MediaTek Inc.</span></span>
* <span data-ttu-id="59e67-167">MStar Co, Ltd</span><span class="sxs-lookup"><span data-stu-id="59e67-167">MStar Co, Ltd</span></span>
* <span data-ttu-id="59e67-168">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="59e67-168">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="59e67-169">OpenTV, Inc.</span><span class="sxs-lookup"><span data-stu-id="59e67-169">OpenTV, Inc.</span></span>
* <span data-ttu-id="59e67-170">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="59e67-170">Saffron Digital Limited</span></span>
* <span data-ttu-id="59e67-171">Sichuan Changhong Electric Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="59e67-171">Sichuan Changhong Electric Co., Ltd</span></span>
* <span data-ttu-id="59e67-172">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="59e67-172">SoftAtHome</span></span>
* <span data-ttu-id="59e67-173">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="59e67-173">Sony Corporation</span></span>
* <span data-ttu-id="59e67-174">Tatung Technology Inc.</span><span class="sxs-lookup"><span data-stu-id="59e67-174">Tatung Technology Inc.</span></span>
* <span data-ttu-id="59e67-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="59e67-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span></span>
* <span data-ttu-id="59e67-176">Top Victory Investments, Ltd.</span><span class="sxs-lookup"><span data-stu-id="59e67-176">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="59e67-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="59e67-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span></span>
* <span data-ttu-id="59e67-178">VisualOn, Inc.</span><span class="sxs-lookup"><span data-stu-id="59e67-178">VisualOn, Inc.</span></span>
* <span data-ttu-id="59e67-179">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="59e67-179">ZTE Corporation</span></span>

## <a name="microsoft-smooth-streaming-client-final-product-agreement-licensees"></a><span data-ttu-id="59e67-180">Обладатели лицензий на конечный продукт пакета для портирования клиента Microsoft Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="59e67-180">Microsoft Smooth Streaming Client Final Product Agreement Licensees</span></span>
* <span data-ttu-id="59e67-181">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="59e67-181">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="59e67-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="59e67-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="59e67-183">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="59e67-183">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="59e67-184">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="59e67-184">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="59e67-185">AmTRAN Technology Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="59e67-185">AmTRAN Technology Co., Ltd.</span></span>
* <span data-ttu-id="59e67-186">Arcadyan Technology Corporation</span><span class="sxs-lookup"><span data-stu-id="59e67-186">Arcadyan Technology Corporation</span></span>
* <span data-ttu-id="59e67-187">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="59e67-187">Arion Technology, Inc.</span></span>
* <span data-ttu-id="59e67-188">ATMACA ELEKTRONİK SAN.</span><span class="sxs-lookup"><span data-stu-id="59e67-188">ATMACA ELEKTRONİK SAN.</span></span> <span data-ttu-id="59e67-189">VE TİC.</span><span class="sxs-lookup"><span data-stu-id="59e67-189">VE TİC.</span></span> <span data-ttu-id="59e67-190">A.Ş</span><span class="sxs-lookup"><span data-stu-id="59e67-190">A.Ş</span></span>
* <span data-ttu-id="59e67-191">British Sky Broadcasting Limited</span><span class="sxs-lookup"><span data-stu-id="59e67-191">British Sky Broadcasting Limited</span></span>
* <span data-ttu-id="59e67-192">CastPal Technology Inc., Shenzhen</span><span class="sxs-lookup"><span data-stu-id="59e67-192">CastPal Technology Inc., Shenzhen</span></span>
* <span data-ttu-id="59e67-193">Compal Electronics, Inc.</span><span class="sxs-lookup"><span data-stu-id="59e67-193">Compal Electronics, Inc.</span></span>
* <span data-ttu-id="59e67-194">Dongguan Digital AV Technology Corp., Ltd.</span><span class="sxs-lookup"><span data-stu-id="59e67-194">Dongguan Digital AV Technology Corp., Ltd.</span></span>
* <span data-ttu-id="59e67-195">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="59e67-195">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="59e67-196">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="59e67-196">Enseo, Inc.</span></span>
* <span data-ttu-id="59e67-197">Filmflex Movies Limited</span><span class="sxs-lookup"><span data-stu-id="59e67-197">Filmflex Movies Limited</span></span>
* <span data-ttu-id="59e67-198">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="59e67-198">Fluendo S.A.</span></span>
* <span data-ttu-id="59e67-199">Gibson Innovations Limited</span><span class="sxs-lookup"><span data-stu-id="59e67-199">Gibson Innovations Limited</span></span>
* <span data-ttu-id="59e67-200">Haier Information Applicantion S.R.L</span><span class="sxs-lookup"><span data-stu-id="59e67-200">Haier Information Applicantion S.R.L</span></span>
* <span data-ttu-id="59e67-201">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="59e67-201">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="59e67-202">Hisense International Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="59e67-202">Hisense International Co., Ltd.</span></span> 
* <span data-ttu-id="59e67-203">Homecast Co.,Ltd</span><span class="sxs-lookup"><span data-stu-id="59e67-203">Homecast Co.,Ltd</span></span>
* <span data-ttu-id="59e67-204">Hon Hai Precision Industry Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="59e67-204">Hon Hai Precision Industry Co., Ltd.</span></span>
* <span data-ttu-id="59e67-205">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="59e67-205">Infomir GMBH</span></span>
* <span data-ttu-id="59e67-206">Kaonmedia Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="59e67-206">Kaonmedia Co., Ltd.</span></span>
* <span data-ttu-id="59e67-207">KDDI Corporation</span><span class="sxs-lookup"><span data-stu-id="59e67-207">KDDI Corporation</span></span>
* <span data-ttu-id="59e67-208">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="59e67-208">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="59e67-209">Orange SA</span><span class="sxs-lookup"><span data-stu-id="59e67-209">Orange SA</span></span>
* <span data-ttu-id="59e67-210">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="59e67-210">Saffron Digital Limited</span></span>
* <span data-ttu-id="59e67-211">Sagemcom Broadband SAS</span><span class="sxs-lookup"><span data-stu-id="59e67-211">Sagemcom Broadband SAS</span></span>
* <span data-ttu-id="59e67-212">Shenzhen Coship Electronics CO., LTD</span><span class="sxs-lookup"><span data-stu-id="59e67-212">Shenzhen Coship Electronics CO., LTD</span></span>
* <span data-ttu-id="59e67-213">Shenzhen Jiuzhou Electric Co.,Ltd</span><span class="sxs-lookup"><span data-stu-id="59e67-213">Shenzhen Jiuzhou Electric Co.,Ltd</span></span>
* <span data-ttu-id="59e67-214">Shenzhen Skyworth Digital Technology Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="59e67-214">Shenzhen Skyworth Digital Technology Co., Ltd</span></span>
* <span data-ttu-id="59e67-215">Sichuan Changhong Electric Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="59e67-215">Sichuan Changhong Electric Co., Ltd.</span></span>
* <span data-ttu-id="59e67-216">Skardin Industrial Corp.</span><span class="sxs-lookup"><span data-stu-id="59e67-216">Skardin Industrial Corp.</span></span>
* <span data-ttu-id="59e67-217">Sky Deutschland Fernsehen GmbH & Co. KG</span><span class="sxs-lookup"><span data-stu-id="59e67-217">Sky Deutschland Fernsehen GmbH & Co. KG</span></span>
* <span data-ttu-id="59e67-218">SmarDTV S.A.</span><span class="sxs-lookup"><span data-stu-id="59e67-218">SmarDTV S.A.</span></span>
* <span data-ttu-id="59e67-219">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="59e67-219">SoftAtHome</span></span>
* <span data-ttu-id="59e67-220">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="59e67-220">Sony Corporation</span></span>
* <span data-ttu-id="59e67-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span><span class="sxs-lookup"><span data-stu-id="59e67-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span></span>
* <span data-ttu-id="59e67-222">Technicolor Delivery Technologies, SAS</span><span class="sxs-lookup"><span data-stu-id="59e67-222">Technicolor Delivery Technologies, SAS</span></span>
* <span data-ttu-id="59e67-223">Tongfang Global Ltd.</span><span class="sxs-lookup"><span data-stu-id="59e67-223">Tongfang Global Ltd.</span></span>
* <span data-ttu-id="59e67-224">Top Victory Investments, Ltd.</span><span class="sxs-lookup"><span data-stu-id="59e67-224">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="59e67-225">Toshiba Lifestyle Products & Services Corporation</span><span class="sxs-lookup"><span data-stu-id="59e67-225">Toshiba Lifestyle Products & Services Corporation</span></span>
* <span data-ttu-id="59e67-226">Universal Media Corporation /Slovakia/ s.r.o.</span><span class="sxs-lookup"><span data-stu-id="59e67-226">Universal Media Corporation /Slovakia/ s.r.o.</span></span>
* <span data-ttu-id="59e67-227">VIZIO, Inc.</span><span class="sxs-lookup"><span data-stu-id="59e67-227">VIZIO, Inc.</span></span>
* <span data-ttu-id="59e67-228">Wistron Corporation</span><span class="sxs-lookup"><span data-stu-id="59e67-228">Wistron Corporation</span></span>
* <span data-ttu-id="59e67-229">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="59e67-229">ZTE Corporation</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="59e67-230">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="59e67-230">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="59e67-231">Отзывы</span><span class="sxs-lookup"><span data-stu-id="59e67-231">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

