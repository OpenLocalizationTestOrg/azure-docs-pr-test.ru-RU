---
title: "Лицензирование пакета для портирования клиента бесперебойной потоковой передачи Microsoft® Smooth Streaming"
description: "Информация о лицензировании пакета для портирования клиента бесперебойной потоковой передачи Microsoft® Smooth Streaming"
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
ms.openlocfilehash: b5a36ac6771bef220afe29446cd56c1b65a498d9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="licensing-microsoft-smooth-streaming-client-porting-kit"></a><span data-ttu-id="2458e-103">Лицензирование пакета для портирования клиента бесперебойной потоковой передачи Microsoft® Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="2458e-103">Licensing Microsoft® Smooth Streaming Client Porting Kit</span></span>
## <a name="overview"></a><span data-ttu-id="2458e-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="2458e-104">Overview</span></span>
<span data-ttu-id="2458e-105">Пакет для портирования клиента бесперебойной потоковой передачи Microsoft Smooth Streaming (далее для краткости называется **SSPK**) представляет собой реализацию клиента Smooth Streaming. Он оптимизирован так, чтобы помочь производителям встроенных устройств, операторам кабельной и мобильной связи, поставщикам служб содержимого, производителям мобильных устройств, независимым поставщикам программного обеспечения и поставщикам решений создавать продукты и услуги, включающие в себя адаптивную потоковую передачу содержимого в формате Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="2458e-105">Microsoft Smooth Streaming Client Porting Kit (**SSPK** for short) is a Smooth Streaming client implementation that is optimized to help embedded device manufacturers, cable and mobile operators, content service providers, handset manufacturers, independent software vendors (ISVs), and solution providers to create products and services for streaming adaptive streaming content in Smooth Streaming format.</span></span> <span data-ttu-id="2458e-106">Клиент SSPK не зависит от оборудования и платформы. Лицензиат может легко портировать его на любое устройство и любую платформу.</span><span class="sxs-lookup"><span data-stu-id="2458e-106">SSPK is a device and platform independent implementation of Smooth Streaming client that can be ported by the licensee to any device and platform.</span></span> 

<span data-ttu-id="2458e-107">Ниже вы видите схему архитектуры высокого уровня. Поле IIS Smooth Streaming Porting Kit здесь обозначает клиента Smooth Streaming, который предоставляет корпорация Майкрософт. Этот клиент содержит всю основную логику для воспроизведения контента Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="2458e-107">Included below is a high level architecture and IIS Smooth Streaming Porting Kit box is the Smooth Streaming Client implementation provided by Microsoft and includes all the core logic for playback of Smooth Streaming content.</span></span> <span data-ttu-id="2458e-108">Партнеры затем портируют его на конкретное устройство или платформу, создавая соответствующие интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="2458e-108">This is then ported by partners for a specific device or platform by implementing appropriate interfaces.</span></span> 

![SSPK](./media/media-services-sspk/sspk-arch.png)

## <a name="description"></a><span data-ttu-id="2458e-110">Описание</span><span class="sxs-lookup"><span data-stu-id="2458e-110">Description</span></span>
<span data-ttu-id="2458e-111">Условия лицензирования SSPK повышают коммерческую ценность этого предложения.</span><span class="sxs-lookup"><span data-stu-id="2458e-111">SSPK is licensed on terms that offer excellent business value.</span></span> <span data-ttu-id="2458e-112">Лицензия SSPK предоставляет предприятиям отрасли следующие возможности.</span><span class="sxs-lookup"><span data-stu-id="2458e-112">SSPK license provides the industry with:</span></span>

* <span data-ttu-id="2458e-113">Исходный код пакета для портирования Smooth Streaming на языке C++, в котором:</span><span class="sxs-lookup"><span data-stu-id="2458e-113">Smooth Streaming Porting Kit source in C++</span></span> 
  * <span data-ttu-id="2458e-114">реализованы функции клиента Smooth Streaming;</span><span class="sxs-lookup"><span data-stu-id="2458e-114">implements Smooth Streaming Client functionality</span></span>
  * <span data-ttu-id="2458e-115">добавлены возможности синтаксического и эвристического анализа, логика буферизации и другие функции.</span><span class="sxs-lookup"><span data-stu-id="2458e-115">adds format parsing, heuristics, buffering logic, etc.</span></span>
* <span data-ttu-id="2458e-116">API-интерфейсы приложения проигрывателя.</span><span class="sxs-lookup"><span data-stu-id="2458e-116">Player application APIs</span></span> 
  * <span data-ttu-id="2458e-117">Программные интерфейсы для взаимодействия с приложением Проигрывателя мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="2458e-117">programming interfaces for interaction with a media player application</span></span>
* <span data-ttu-id="2458e-118">Интерфейс слоя платформенных абстракций (PAL).</span><span class="sxs-lookup"><span data-stu-id="2458e-118">Platform Abstraction Layer (PAL) Interface</span></span> 
  * <span data-ttu-id="2458e-119">Программные интерфейсы для взаимодействия с операционной системой (потоки, сокеты).</span><span class="sxs-lookup"><span data-stu-id="2458e-119">programming interfaces for interaction with the operating system (threads, sockets)</span></span>
* <span data-ttu-id="2458e-120">Интерфейс слоя аппаратных абстракций (HAL).</span><span class="sxs-lookup"><span data-stu-id="2458e-120">Hardware Abstraction Layer (HAL) Interface</span></span> 
  * <span data-ttu-id="2458e-121">Программные интерфейсы для взаимодействия с аппаратным оборудованием аудио- и видеодекодеров (декодирование, отрисовка).</span><span class="sxs-lookup"><span data-stu-id="2458e-121">programming interfaces for interaction with hardware A/V decoders (decoding, rendering)</span></span>
* <span data-ttu-id="2458e-122">Интерфейс управления цифровыми правами (DRM).</span><span class="sxs-lookup"><span data-stu-id="2458e-122">Digital Rights Management (DRM) Interface</span></span> 
  * <span data-ttu-id="2458e-123">Программные интерфейсы для обработки ограничений DRM через уровень абстракции DRM (DAL).</span><span class="sxs-lookup"><span data-stu-id="2458e-123">programming interfaces for handling DRM through the DRM Abstraction Layer (DAL)</span></span>
  * <span data-ttu-id="2458e-124">Пакет для портирования Microsoft PlayReady поставляется отдельно, но интегрируется через этот интерфейс.</span><span class="sxs-lookup"><span data-stu-id="2458e-124">Microsoft PlayReady Porting Kit ships separately but integrates through this interface.</span></span> <span data-ttu-id="2458e-125">Дополнительные сведения о лицензировании устройств Microsoft PlayReady приводятся [здесь](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span><span class="sxs-lookup"><span data-stu-id="2458e-125">For more details on Microsoft PlayReady Device licensing, click [here](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).</span></span>
* <span data-ttu-id="2458e-126">Примеры реализации</span><span class="sxs-lookup"><span data-stu-id="2458e-126">Implementation samples</span></span> 
  * <span data-ttu-id="2458e-127">Пример реализации PAL для Linux</span><span class="sxs-lookup"><span data-stu-id="2458e-127">sample PAL implementation for Linux</span></span>
  * <span data-ttu-id="2458e-128">Пример реализации HAL для GStreamer</span><span class="sxs-lookup"><span data-stu-id="2458e-128">sample HAL implementation for GStreamer</span></span>

## <a name="licensing-options"></a><span data-ttu-id="2458e-129">Варианты лицензирования</span><span class="sxs-lookup"><span data-stu-id="2458e-129">Licensing Options</span></span>
<span data-ttu-id="2458e-130">Пакет для портирования клиента Microsoft Smooth Streaming предлагается лицензиатам на условиях одного из двух различных лицензионных соглашений. Одно соглашение предназначено для разработки промежуточных продуктов Smooth Streaming, а другое — для распространения конечных клиентских продуктов Smooth Streaming среди конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="2458e-130">Microsoft Smooth Streaming Client Porting Kit is made available to licensees under two distinct license agreements: one for developing Smooth Streaming Client Interim Products and another for distributing Smooth Streaming Client Final Products to end users.</span></span>

* <span data-ttu-id="2458e-131">Изготовители микросхем, системные интеграторы и независимые поставщики программного обеспечения, которые используют исходный код пакета для разработки промежуточных продуктов, должны выполнять условия **лицензии на промежуточный продукт** пакета для портирования клиента Microsoft Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="2458e-131">For chipset manufacturers, system integrators, or independent software vendors (ISVs) who require a source code porting kit to develop Interim Products, a Microsoft Smooth Streaming Client Porting Kit **Interim Product License** should be executed.</span></span>
* <span data-ttu-id="2458e-132">Производители устройств и независимые поставщики программного обеспечения, которым нужны права на передачу конечных продуктов конечным пользователям, должны выполнять условия **лицензии на конечный продукт** пакета портирования клиента Microsoft Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="2458e-132">For device manufacturers or ISVs who require distribution rights for Smooth Streaming Client Final Products to end users, the Microsoft Smooth Streaming Client Porting Kit **Final Product License** should be executed.</span></span>

### <a name="microsoft-smooth-streaming-client-porting-kit-interim-product-license"></a><span data-ttu-id="2458e-133">Лицензия на промежуточный продукт пакета портирования клиента Microsoft Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="2458e-133">Microsoft Smooth Streaming Client Porting Kit Interim Product License</span></span>
<span data-ttu-id="2458e-134">По этой лицензии корпорация Майкрософт предоставляет пакет портирования клиента Smooth Streaming и необходимые права на интеллектуальную собственность для разработки промежуточных клиентских продуктов Smooth Streaming и их распространения среди других лицензиатов пакета портирования клиента Smooth Streaming, которые распространяют конечные клиентские продукты Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="2458e-134">Under this license, Microsoft offers a Smooth Streaming Client Porting Kit and the necessary intellectual property rights to develop and distribute Smooth Streaming Client Interim Products to other Smooth Streaming Client Porting Kit device licensees that distribute Smooth Streaming Client Final Products.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="2458e-135">Структура выплат</span><span class="sxs-lookup"><span data-stu-id="2458e-135">Fee structure</span></span>
<span data-ttu-id="2458e-136">Лицензия на пакет портирования клиента Smooth Streaming предоставляется с выплатой единовременного лицензионного сбора в размере 50 000 долларов США.</span><span class="sxs-lookup"><span data-stu-id="2458e-136">A U.S. $50,000 one-time license fee provides access to the Smooth Streaming Client Porting Kit.</span></span> 

### <a name="microsoft-smooth-streaming-client-porting-kit-final-product-license"></a><span data-ttu-id="2458e-137">Лицензия на конечный продукт пакета портирования клиента Microsoft Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="2458e-137">Microsoft Smooth Streaming Client Porting Kit Final Product License</span></span>
<span data-ttu-id="2458e-138">По этой лицензии корпорация Майкрософт предоставляет все необходимые права на интеллектуальную собственность для получения промежуточных продуктов от других лицензиатов промежуточных продуктов пакета портирования клиента Smooth Streaming и для распространения продуктов Smooth Streaming под своей торговой маркой среди конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="2458e-138">Under this license, Microsoft offers all necessary intellectual property rights to receive Smooth Streaming Client Interim Products from other Smooth Streaming Client Porting Kit licensees and to distribute company-branded Smooth Streaming Client Final Products to end users.</span></span>

#### <a name="fee-structure"></a><span data-ttu-id="2458e-139">Структура выплат</span><span class="sxs-lookup"><span data-stu-id="2458e-139">Fee structure</span></span>
<span data-ttu-id="2458e-140">Лицензия на конечный продукт пакета портирования клиента Smooth Streaming предоставляется на следующих условиях лицензионных отчислений.</span><span class="sxs-lookup"><span data-stu-id="2458e-140">The Smooth Streaming Client Final Product is offered under a royalty model as under:</span></span>

* <span data-ttu-id="2458e-141">По 0,10 доллара США за каждое отправленное устройство, в котором используется конечный продукт.</span><span class="sxs-lookup"><span data-stu-id="2458e-141">$0.10 per device implementation shipped</span></span>
* <span data-ttu-id="2458e-142">Общая сумма составляет не более 50 000 долларов США ежегодно.</span><span class="sxs-lookup"><span data-stu-id="2458e-142">The royalty is capped at $50,000 each year</span></span>
* <span data-ttu-id="2458e-143">Отсутствие отчислений за первые 10 000 устройств в течение каждого года.</span><span class="sxs-lookup"><span data-stu-id="2458e-143">No royalty for first 10,000 device implementations each year</span></span> 

## <a name="licensing-procedure-and-sspk-access"></a><span data-ttu-id="2458e-144">Процедура лицензирования и доступ к SSPK.</span><span class="sxs-lookup"><span data-stu-id="2458e-144">Licensing Procedure and SSPK access</span></span>
<span data-ttu-id="2458e-145">Все запросы на лицензирование отправляйте по электронной почте на адрес [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) .</span><span class="sxs-lookup"><span data-stu-id="2458e-145">Please email [sspkinfo@microsoft.com](mailto:sspkinfo@microsoft.com) for all licensing queries.</span></span>

<span data-ttu-id="2458e-146">Зарегистрированные обладатели лицензии на промежуточный продукт получают доступ к [Порталу распространения SSPK](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) .</span><span class="sxs-lookup"><span data-stu-id="2458e-146">The [SSPK Distribution portal](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) is accessible to registered Interim licensees.</span></span>

<span data-ttu-id="2458e-147">Обладатели лицензий на промежуточные и конечные продукты SSPK могут отправлять технические вопросы на адрес электронной почты [smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="2458e-147">Interim and Final SSPK licensees can submit technical questions to [smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).</span></span>

## <a name="microsoft-smooth-streaming-client-interim-product-agreement-licensees"></a><span data-ttu-id="2458e-148">Обладатели лицензий на промежуточный продукт пакета для портирования клиента Microsoft Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="2458e-148">Microsoft Smooth Streaming Client Interim Product Agreement Licensees</span></span>
* <span data-ttu-id="2458e-149">Adroit Business Solutions, Inc</span><span class="sxs-lookup"><span data-stu-id="2458e-149">Adroit Business Solutions, Inc</span></span>
* <span data-ttu-id="2458e-150">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="2458e-150">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="2458e-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="2458e-151">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="2458e-152">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="2458e-152">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="2458e-153">Alticast Corporation</span><span class="sxs-lookup"><span data-stu-id="2458e-153">Alticast Corporation</span></span>
* <span data-ttu-id="2458e-154">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="2458e-154">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="2458e-155">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="2458e-155">Arion Technology, Inc.</span></span>
* <span data-ttu-id="2458e-156">AVC Multimedia Software Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="2458e-156">AVC Multimedia Software Co., Ltd.</span></span>
* <span data-ttu-id="2458e-157">Cavium, Inc.</span><span class="sxs-lookup"><span data-stu-id="2458e-157">Cavium, Inc.</span></span>
* <span data-ttu-id="2458e-158">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="2458e-158">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="2458e-159">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="2458e-159">Enseo, Inc.</span></span>
* <span data-ttu-id="2458e-160">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="2458e-160">Fluendo S.A.</span></span>
* <span data-ttu-id="2458e-161">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="2458e-161">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="2458e-162">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="2458e-162">Infomir GMBH</span></span>
* <span data-ttu-id="2458e-163">Irdeto USA Inc.</span><span class="sxs-lookup"><span data-stu-id="2458e-163">Irdeto USA Inc.</span></span>
* <span data-ttu-id="2458e-164">iWEDIA S.A.</span><span class="sxs-lookup"><span data-stu-id="2458e-164">iWEDIA S.A.</span></span> 
* <span data-ttu-id="2458e-165">Liberty Global Services BV</span><span class="sxs-lookup"><span data-stu-id="2458e-165">Liberty Global Services BV</span></span>
* <span data-ttu-id="2458e-166">MediaTek Inc.</span><span class="sxs-lookup"><span data-stu-id="2458e-166">MediaTek Inc.</span></span>
* <span data-ttu-id="2458e-167">MStar Co, Ltd</span><span class="sxs-lookup"><span data-stu-id="2458e-167">MStar Co, Ltd</span></span>
* <span data-ttu-id="2458e-168">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="2458e-168">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="2458e-169">OpenTV, Inc.</span><span class="sxs-lookup"><span data-stu-id="2458e-169">OpenTV, Inc.</span></span>
* <span data-ttu-id="2458e-170">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="2458e-170">Saffron Digital Limited</span></span>
* <span data-ttu-id="2458e-171">Sichuan Changhong Electric Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="2458e-171">Sichuan Changhong Electric Co., Ltd</span></span>
* <span data-ttu-id="2458e-172">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="2458e-172">SoftAtHome</span></span>
* <span data-ttu-id="2458e-173">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="2458e-173">Sony Corporation</span></span>
* <span data-ttu-id="2458e-174">Tatung Technology Inc.</span><span class="sxs-lookup"><span data-stu-id="2458e-174">Tatung Technology Inc.</span></span>
* <span data-ttu-id="2458e-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="2458e-175">TCL Technoly Electronics (Huizhou) Co., Ltd.</span></span>
* <span data-ttu-id="2458e-176">Top Victory Investments, Ltd.</span><span class="sxs-lookup"><span data-stu-id="2458e-176">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="2458e-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="2458e-177">Vestel Elektronik Sanayi ve Ticaret A.S.</span></span>
* <span data-ttu-id="2458e-178">VisualOn, Inc.</span><span class="sxs-lookup"><span data-stu-id="2458e-178">VisualOn, Inc.</span></span>
* <span data-ttu-id="2458e-179">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="2458e-179">ZTE Corporation</span></span>

## <a name="microsoft-smooth-streaming-client-final-product-agreement-licensees"></a><span data-ttu-id="2458e-180">Обладатели лицензий на конечный продукт пакета для портирования клиента Microsoft Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="2458e-180">Microsoft Smooth Streaming Client Final Product Agreement Licensees</span></span>
* <span data-ttu-id="2458e-181">Advanced Digital Broadcast SA</span><span class="sxs-lookup"><span data-stu-id="2458e-181">Advanced Digital Broadcast SA</span></span>
* <span data-ttu-id="2458e-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span><span class="sxs-lookup"><span data-stu-id="2458e-182">AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.</span></span>
* <span data-ttu-id="2458e-183">Albis Technologies Ltd.</span><span class="sxs-lookup"><span data-stu-id="2458e-183">Albis Technologies Ltd.</span></span>
* <span data-ttu-id="2458e-184">Amazon Digital Services, Inc.</span><span class="sxs-lookup"><span data-stu-id="2458e-184">Amazon Digital Services, Inc.</span></span>
* <span data-ttu-id="2458e-185">AmTRAN Technology Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="2458e-185">AmTRAN Technology Co., Ltd.</span></span>
* <span data-ttu-id="2458e-186">Arcadyan Technology Corporation</span><span class="sxs-lookup"><span data-stu-id="2458e-186">Arcadyan Technology Corporation</span></span>
* <span data-ttu-id="2458e-187">Arion Technology, Inc.</span><span class="sxs-lookup"><span data-stu-id="2458e-187">Arion Technology, Inc.</span></span>
* <span data-ttu-id="2458e-188">ATMACA ELEKTRONİK SAN.</span><span class="sxs-lookup"><span data-stu-id="2458e-188">ATMACA ELEKTRONİK SAN.</span></span> <span data-ttu-id="2458e-189">VE TİC.</span><span class="sxs-lookup"><span data-stu-id="2458e-189">VE TİC.</span></span> <span data-ttu-id="2458e-190">A.Ş</span><span class="sxs-lookup"><span data-stu-id="2458e-190">A.Ş</span></span>
* <span data-ttu-id="2458e-191">British Sky Broadcasting Limited</span><span class="sxs-lookup"><span data-stu-id="2458e-191">British Sky Broadcasting Limited</span></span>
* <span data-ttu-id="2458e-192">CastPal Technology Inc., Shenzhen</span><span class="sxs-lookup"><span data-stu-id="2458e-192">CastPal Technology Inc., Shenzhen</span></span>
* <span data-ttu-id="2458e-193">Compal Electronics, Inc.</span><span class="sxs-lookup"><span data-stu-id="2458e-193">Compal Electronics, Inc.</span></span>
* <span data-ttu-id="2458e-194">Dongguan Digital AV Technology Corp., Ltd.</span><span class="sxs-lookup"><span data-stu-id="2458e-194">Dongguan Digital AV Technology Corp., Ltd.</span></span>
* <span data-ttu-id="2458e-195">EchoStar Purchasing Corporation</span><span class="sxs-lookup"><span data-stu-id="2458e-195">EchoStar Purchasing Corporation</span></span>
* <span data-ttu-id="2458e-196">Enseo, Inc.</span><span class="sxs-lookup"><span data-stu-id="2458e-196">Enseo, Inc.</span></span>
* <span data-ttu-id="2458e-197">Filmflex Movies Limited</span><span class="sxs-lookup"><span data-stu-id="2458e-197">Filmflex Movies Limited</span></span>
* <span data-ttu-id="2458e-198">Fluendo S.A.</span><span class="sxs-lookup"><span data-stu-id="2458e-198">Fluendo S.A.</span></span>
* <span data-ttu-id="2458e-199">Gibson Innovations Limited</span><span class="sxs-lookup"><span data-stu-id="2458e-199">Gibson Innovations Limited</span></span>
* <span data-ttu-id="2458e-200">Haier Information Applicantion S.R.L</span><span class="sxs-lookup"><span data-stu-id="2458e-200">Haier Information Applicantion S.R.L</span></span>
* <span data-ttu-id="2458e-201">HANDAN BroadInfoCom Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="2458e-201">HANDAN BroadInfoCom Co., Ltd.</span></span>
* <span data-ttu-id="2458e-202">Hisense International Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="2458e-202">Hisense International Co., Ltd.</span></span> 
* <span data-ttu-id="2458e-203">Homecast Co.,Ltd</span><span class="sxs-lookup"><span data-stu-id="2458e-203">Homecast Co.,Ltd</span></span>
* <span data-ttu-id="2458e-204">Hon Hai Precision Industry Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="2458e-204">Hon Hai Precision Industry Co., Ltd.</span></span>
* <span data-ttu-id="2458e-205">Infomir GMBH</span><span class="sxs-lookup"><span data-stu-id="2458e-205">Infomir GMBH</span></span>
* <span data-ttu-id="2458e-206">Kaonmedia Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="2458e-206">Kaonmedia Co., Ltd.</span></span>
* <span data-ttu-id="2458e-207">KDDI Corporation</span><span class="sxs-lookup"><span data-stu-id="2458e-207">KDDI Corporation</span></span>
* <span data-ttu-id="2458e-208">Nintendo Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="2458e-208">Nintendo Co., Ltd.</span></span>
* <span data-ttu-id="2458e-209">Orange SA</span><span class="sxs-lookup"><span data-stu-id="2458e-209">Orange SA</span></span>
* <span data-ttu-id="2458e-210">Saffron Digital Limited</span><span class="sxs-lookup"><span data-stu-id="2458e-210">Saffron Digital Limited</span></span>
* <span data-ttu-id="2458e-211">Sagemcom Broadband SAS</span><span class="sxs-lookup"><span data-stu-id="2458e-211">Sagemcom Broadband SAS</span></span>
* <span data-ttu-id="2458e-212">Shenzhen Coship Electronics CO., LTD</span><span class="sxs-lookup"><span data-stu-id="2458e-212">Shenzhen Coship Electronics CO., LTD</span></span>
* <span data-ttu-id="2458e-213">Shenzhen Jiuzhou Electric Co.,Ltd</span><span class="sxs-lookup"><span data-stu-id="2458e-213">Shenzhen Jiuzhou Electric Co.,Ltd</span></span>
* <span data-ttu-id="2458e-214">Shenzhen Skyworth Digital Technology Co., Ltd</span><span class="sxs-lookup"><span data-stu-id="2458e-214">Shenzhen Skyworth Digital Technology Co., Ltd</span></span>
* <span data-ttu-id="2458e-215">Sichuan Changhong Electric Co., Ltd.</span><span class="sxs-lookup"><span data-stu-id="2458e-215">Sichuan Changhong Electric Co., Ltd.</span></span>
* <span data-ttu-id="2458e-216">Skardin Industrial Corp.</span><span class="sxs-lookup"><span data-stu-id="2458e-216">Skardin Industrial Corp.</span></span>
* <span data-ttu-id="2458e-217">Sky Deutschland Fernsehen GmbH & Co. KG</span><span class="sxs-lookup"><span data-stu-id="2458e-217">Sky Deutschland Fernsehen GmbH & Co. KG</span></span>
* <span data-ttu-id="2458e-218">SmarDTV S.A.</span><span class="sxs-lookup"><span data-stu-id="2458e-218">SmarDTV S.A.</span></span>
* <span data-ttu-id="2458e-219">SoftAtHome</span><span class="sxs-lookup"><span data-stu-id="2458e-219">SoftAtHome</span></span>
* <span data-ttu-id="2458e-220">Sony Corporation</span><span class="sxs-lookup"><span data-stu-id="2458e-220">Sony Corporation</span></span>
* <span data-ttu-id="2458e-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span><span class="sxs-lookup"><span data-stu-id="2458e-221">TCL Overseas Marketing (Macao Commercial Offshore) Limited</span></span>
* <span data-ttu-id="2458e-222">Technicolor Delivery Technologies, SAS</span><span class="sxs-lookup"><span data-stu-id="2458e-222">Technicolor Delivery Technologies, SAS</span></span>
* <span data-ttu-id="2458e-223">Tongfang Global Ltd.</span><span class="sxs-lookup"><span data-stu-id="2458e-223">Tongfang Global Ltd.</span></span>
* <span data-ttu-id="2458e-224">Top Victory Investments, Ltd.</span><span class="sxs-lookup"><span data-stu-id="2458e-224">Top Victory Investments, Ltd.</span></span>
* <span data-ttu-id="2458e-225">Toshiba Lifestyle Products & Services Corporation</span><span class="sxs-lookup"><span data-stu-id="2458e-225">Toshiba Lifestyle Products & Services Corporation</span></span>
* <span data-ttu-id="2458e-226">Universal Media Corporation /Slovakia/ s.r.o.</span><span class="sxs-lookup"><span data-stu-id="2458e-226">Universal Media Corporation /Slovakia/ s.r.o.</span></span>
* <span data-ttu-id="2458e-227">VIZIO, Inc.</span><span class="sxs-lookup"><span data-stu-id="2458e-227">VIZIO, Inc.</span></span>
* <span data-ttu-id="2458e-228">Wistron Corporation</span><span class="sxs-lookup"><span data-stu-id="2458e-228">Wistron Corporation</span></span>
* <span data-ttu-id="2458e-229">ZTE Corporation</span><span class="sxs-lookup"><span data-stu-id="2458e-229">ZTE Corporation</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="2458e-230">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="2458e-230">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2458e-231">Отзывы</span><span class="sxs-lookup"><span data-stu-id="2458e-231">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

