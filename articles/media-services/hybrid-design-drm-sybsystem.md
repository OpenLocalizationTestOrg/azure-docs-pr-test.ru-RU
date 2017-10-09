---
title: "Структура aaaHybrid subsystem(s) DRM, с помощью служб мультимедиа Azure | Документы Microsoft"
description: "Здесь рассматривается гибридная структура подсистем управления цифровыми правами (DRM) с использованием служб мультимедиа Azure."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: willzhan;juliako
ms.openlocfilehash: 4206248420ccd4dbfc9a87a86f4763534c6254a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-design-of-drm-subsystems"></a><span data-ttu-id="e0cbe-103">Гибридная структура подсистем DRM</span><span class="sxs-lookup"><span data-stu-id="e0cbe-103">Hybrid design of DRM subsystem(s)</span></span>

<span data-ttu-id="e0cbe-104">Здесь рассматривается гибридная структура подсистем управления цифровыми правами (DRM) с использованием служб мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="e0cbe-104">This topic discusses hybrid design of DRM subsystem(s) using Azure Media Services.</span></span>

## <a name="overview"></a><span data-ttu-id="e0cbe-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="e0cbe-105">Overview</span></span>

<span data-ttu-id="e0cbe-106">Службы мультимедиа Azure поддерживает следующие три системе DRM hello:</span><span class="sxs-lookup"><span data-stu-id="e0cbe-106">Azure Media Services provides support for hello following three DRM system:</span></span>

* <span data-ttu-id="e0cbe-107">PlayReady</span><span class="sxs-lookup"><span data-stu-id="e0cbe-107">PlayReady</span></span>
* <span data-ttu-id="e0cbe-108">Widevine (модульная);</span><span class="sxs-lookup"><span data-stu-id="e0cbe-108">Widevine (Modular)</span></span>
* <span data-ttu-id="e0cbe-109">FairPlay</span><span class="sxs-lookup"><span data-stu-id="e0cbe-109">FairPlay</span></span>

<span data-ttu-id="e0cbe-110">поддержка DRM Hello включает шифрование DRM (динамического шифрования) и доставки лицензий с помощью Azure Media Player, поддерживающие все 3 DRMs как пакет SDK проигрывателя браузера.</span><span class="sxs-lookup"><span data-stu-id="e0cbe-110">hello DRM support includes DRM encryption (dynamic encryption) and license delivery, with Azure Media Player supporting all 3 DRMs as a browser player SDK.</span></span>

<span data-ttu-id="e0cbe-111">Подробные работу, DRM или CENC подсистемы проектирования и реализации, см. в разделе hello документ с названием [CENC с несколькими DRM и управление доступом](media-services-cenc-with-multidrm-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="e0cbe-111">For a detailed treatment of DRM/CENC subsystem design and implementation, please see hello document titled [CENC with Multi-DRM and Access Control](media-services-cenc-with-multidrm-access-control.md).</span></span>

<span data-ttu-id="e0cbe-112">Несмотря на то, что мы обеспечивают полную поддержку трех систем управления цифровыми правами, иногда клиенты должны toouse различные части собственные инфраструктуры и подсистемами в toobuild Media Services tooAzure Добавление гибридного подсистемы управления цифровыми правами.</span><span class="sxs-lookup"><span data-stu-id="e0cbe-112">Although we offer complete support for three DRM systems, sometimes customers need toouse various parts of their own infrastructure/subsystems in addition tooAzure Media Services toobuild a hybrid DRM subsystem.</span></span>

<span data-ttu-id="e0cbe-113">Ниже представлены некоторые часто задаваемые вопросы пользователей:</span><span class="sxs-lookup"><span data-stu-id="e0cbe-113">Below are some common questions asked by customers:</span></span>

* <span data-ttu-id="e0cbe-114">Можно ли использовать собственные серверы лицензирования DRM?</span><span class="sxs-lookup"><span data-stu-id="e0cbe-114">"Can I use my own DRM license servers?"</span></span> <span data-ttu-id="e0cbe-115">(В этом случае пользователи вложили средства в кластер серверов лицензирования DRM со встроенной бизнес-логикой.)</span><span class="sxs-lookup"><span data-stu-id="e0cbe-115">(In this case, customers have invested in DRM license server farm with embedded business logic).</span></span>
* <span data-ttu-id="e0cbe-116">Можно ли использовать доставку лицензий DRM в службах мультимедиа Azure без размещения содержимого в AMS?</span><span class="sxs-lookup"><span data-stu-id="e0cbe-116">"Can I use only your DRM license delivery in Azure Media Services without hosting content in AMS?"</span></span>

## <a name="modularity-of-hello-ams-drm-platform"></a><span data-ttu-id="e0cbe-117">Модульность hello AMS DRM платформы</span><span class="sxs-lookup"><span data-stu-id="e0cbe-117">Modularity of hello AMS DRM platform</span></span>

<span data-ttu-id="e0cbe-118">Как часть комплексной облачной видеоплатформы, DRM служб мультимедиа Azure имеет гибкую и модульную структуру.</span><span class="sxs-lookup"><span data-stu-id="e0cbe-118">As part of a comprehensive cloud video platform, Azure Media Services DRM has a design with flexibility and modularity in mind.</span></span> <span data-ttu-id="e0cbe-119">Службы мультимедиа Azure можно использовать с любым hello следующие комбинации описано hello ниже в таблице (объяснение hello-Наура, используемой в таблице hello ниже).</span><span class="sxs-lookup"><span data-stu-id="e0cbe-119">You can use Azure Media Services with any of hello following different combinations described in hello table below (an explanation of hello notation used in hello table follows).</span></span> 

|<span data-ttu-id="e0cbe-120">**Размещение содержимого и источник**</span><span class="sxs-lookup"><span data-stu-id="e0cbe-120">**Content hosting & origin**</span></span>|<span data-ttu-id="e0cbe-121">**Шифрование содержимого**</span><span class="sxs-lookup"><span data-stu-id="e0cbe-121">**Content encryption**</span></span>|<span data-ttu-id="e0cbe-122">**Доставка лицензий DRM**</span><span class="sxs-lookup"><span data-stu-id="e0cbe-122">**DRM license delivery**</span></span>|
|---|---|---|
|<span data-ttu-id="e0cbe-123">AMS</span><span class="sxs-lookup"><span data-stu-id="e0cbe-123">AMS</span></span>|<span data-ttu-id="e0cbe-124">AMS</span><span class="sxs-lookup"><span data-stu-id="e0cbe-124">AMS</span></span>|<span data-ttu-id="e0cbe-125">AMS</span><span class="sxs-lookup"><span data-stu-id="e0cbe-125">AMS</span></span>|
|<span data-ttu-id="e0cbe-126">AMS</span><span class="sxs-lookup"><span data-stu-id="e0cbe-126">AMS</span></span>|<span data-ttu-id="e0cbe-127">AMS</span><span class="sxs-lookup"><span data-stu-id="e0cbe-127">AMS</span></span>|<span data-ttu-id="e0cbe-128">Сторонний производитель</span><span class="sxs-lookup"><span data-stu-id="e0cbe-128">Third-party</span></span>|
|<span data-ttu-id="e0cbe-129">AMS</span><span class="sxs-lookup"><span data-stu-id="e0cbe-129">AMS</span></span>|<span data-ttu-id="e0cbe-130">Сторонний производитель</span><span class="sxs-lookup"><span data-stu-id="e0cbe-130">Third-party</span></span>|<span data-ttu-id="e0cbe-131">AMS</span><span class="sxs-lookup"><span data-stu-id="e0cbe-131">AMS</span></span>|
|<span data-ttu-id="e0cbe-132">AMS</span><span class="sxs-lookup"><span data-stu-id="e0cbe-132">AMS</span></span>|<span data-ttu-id="e0cbe-133">Сторонний производитель</span><span class="sxs-lookup"><span data-stu-id="e0cbe-133">Third-party</span></span>|<span data-ttu-id="e0cbe-134">Сторонний производитель</span><span class="sxs-lookup"><span data-stu-id="e0cbe-134">Third-party</span></span>|
|<span data-ttu-id="e0cbe-135">Сторонний производитель</span><span class="sxs-lookup"><span data-stu-id="e0cbe-135">Third-party</span></span>|<span data-ttu-id="e0cbe-136">Сторонний производитель</span><span class="sxs-lookup"><span data-stu-id="e0cbe-136">Third-party</span></span>|<span data-ttu-id="e0cbe-137">AMS</span><span class="sxs-lookup"><span data-stu-id="e0cbe-137">AMS</span></span>|

### <a name="content-hosting--origin"></a><span data-ttu-id="e0cbe-138">Размещение содержимого и источник</span><span class="sxs-lookup"><span data-stu-id="e0cbe-138">Content hosting & origin</span></span>

* <span data-ttu-id="e0cbe-139">AMS: видеоресурсы размещаются в AMS, а потоковая передача ведется с помощью конечных точек потоковой передачи AMS (но не обязательно с динамической упаковкой).</span><span class="sxs-lookup"><span data-stu-id="e0cbe-139">AMS: video asset is hosted in AMS and streaming is through AMS streaming endpoints (but not necessarily dynamic packaging).</span></span>
* <span data-ttu-id="e0cbe-140">Сторонний производитель: видео размещается и доставляется с помощью платформы потоковой передачи стороннего производителя за пределами AMS.</span><span class="sxs-lookup"><span data-stu-id="e0cbe-140">Third-party: video is hosted and delivered on a third-party streaming platform outside of AMS.</span></span>

### <a name="content-encryption"></a><span data-ttu-id="e0cbe-141">Шифрование содержимого</span><span class="sxs-lookup"><span data-stu-id="e0cbe-141">Content encryption</span></span>

* <span data-ttu-id="e0cbe-142">AMS: шифрование содержимого происходит динамически или по требованию с помощью динамического шифрования AMS.</span><span class="sxs-lookup"><span data-stu-id="e0cbe-142">AMS: content encryption is performed dynamically/on-demand by AMS dynamic encryption.</span></span>
* <span data-ttu-id="e0cbe-143">Сторонний производитель: шифрование содержимого выполняется за пределами AMS с использованием рабочего процесса предварительной обработки.</span><span class="sxs-lookup"><span data-stu-id="e0cbe-143">Third-party: content encryption is performed outside of AMS using a pre-processing workflow.</span></span>

### <a name="drm-license-delivery"></a><span data-ttu-id="e0cbe-144">Доставка лицензий DRM</span><span class="sxs-lookup"><span data-stu-id="e0cbe-144">DRM license delivery</span></span>

* <span data-ttu-id="e0cbe-145">AMS: лицензию DRM доставляет служба доставки лицензий AMS.</span><span class="sxs-lookup"><span data-stu-id="e0cbe-145">AMS: DRM license is delivered by AMS license delivery service.</span></span>
* <span data-ttu-id="e0cbe-146">Сторонний производитель: лицензию DRM доставляет сервер лицензирования DRM стороннего производителя за пределами AMS.</span><span class="sxs-lookup"><span data-stu-id="e0cbe-146">Third-party: DRM license is delivered by a third-party DRM license server outside of AMS.</span></span>

## <a name="configure-based-on-your-hybrid-scenario"></a><span data-ttu-id="e0cbe-147">Настройка на основе своего гибридного сценария</span><span class="sxs-lookup"><span data-stu-id="e0cbe-147">Configure based on your hybrid scenario</span></span>

### <a name="content-key"></a><span data-ttu-id="e0cbe-148">Ключ содержимого</span><span class="sxs-lookup"><span data-stu-id="e0cbe-148">Content key</span></span>

<span data-ttu-id="e0cbe-149">Путем настройки ключа содержимого можно контролировать следующие атрибуты AMS динамического шифрования и службы доставки лицензий AMS hello:</span><span class="sxs-lookup"><span data-stu-id="e0cbe-149">Through configuration of a content key, you can control hello following attributes of both AMS dynamic encryption and AMS license delivery service:</span></span>

* <span data-ttu-id="e0cbe-150">Hello содержимого ключ, используемый для динамического шифрования управления цифровыми правами.</span><span class="sxs-lookup"><span data-stu-id="e0cbe-150">hello content key used for dynamic DRM encryption.</span></span>
* <span data-ttu-id="e0cbe-151">Toobe содержимого лицензии DRM, предоставляемых служб доставки лицензий: прав, ключ содержимого и ограничений.</span><span class="sxs-lookup"><span data-stu-id="e0cbe-151">DRM license content toobe delivered by license delivery services: rights, content key and restrictions.</span></span>
* <span data-ttu-id="e0cbe-152">Тип **ограничения политики авторизации ключа содержимого**: открытое, IP-адрес или ограничение по токену.</span><span class="sxs-lookup"><span data-stu-id="e0cbe-152">Type of **content key authorization policy restriction**: open, IP, or token restriction.</span></span>
* <span data-ttu-id="e0cbe-153">Если **маркера** тип **ограничение политики авторизации ключа контента используется**, hello **ограничений политики авторизации ключа содержимого** должны быть выполнены перед выдачей лицензию.</span><span class="sxs-lookup"><span data-stu-id="e0cbe-153">If **token** type of **content key authorization policy restriction is used**, hello **content key authorization policy restriction** must be met before a license is issued.</span></span>

### <a name="asset-delivery-policy"></a><span data-ttu-id="e0cbe-154">Политика доставки ресурсов</span><span class="sxs-lookup"><span data-stu-id="e0cbe-154">Asset delivery policy</span></span>

<span data-ttu-id="e0cbe-155">Через конфигурацию политики доставки активов можно управлять hello следующие атрибуты, используемые AMS работы динамического упаковщика и динамического шифрования AMS конечной точки потоковой передачи:</span><span class="sxs-lookup"><span data-stu-id="e0cbe-155">Through configuration of an asset delivery policy, you can control hello following attributes used by AMS dynamic packager and dynamic encryption of an AMS streaming endpoint:</span></span>

* <span data-ttu-id="e0cbe-156">Протокол потоковой передачи и комбинация шифрования DRM, например DASH в CENC (PlayReady и Widevine), Smooth Streaming в PlayReady, HLS в Widevine или PlayReady.</span><span class="sxs-lookup"><span data-stu-id="e0cbe-156">Streaming protocol and DRM encryption combination, such as DASH under CENC (PlayReady and Widevine), smooth streaming under PlayReady, HLS under Widevine or PlayReady.</span></span>
* <span data-ttu-id="e0cbe-157">Hello по умолчанию и внедренных лицензии доставки URL-адресов для каждого hello участвует DRMs.</span><span class="sxs-lookup"><span data-stu-id="e0cbe-157">hello default/embedded license delivery URLs for each of hello involved DRMs.</span></span>
* <span data-ttu-id="e0cbe-158">Содержат ли URL-адреса для приобретения лицензий (LA_URL) в DASH MPD или списке воспроизведения HLS строку запроса идентификатора ключа (KID) для Widevine и FairPlay соответственно.</span><span class="sxs-lookup"><span data-stu-id="e0cbe-158">Whether license acquisition URLs (LA_URLs) in DASH MPD or HLS playlist contain query string of key ID (KID) for Widevine and FairPlay, respectively.</span></span>

## <a name="scenarios-and-samples"></a><span data-ttu-id="e0cbe-159">Сценарии и примеры</span><span class="sxs-lookup"><span data-stu-id="e0cbe-159">Scenarios and samples</span></span>

<span data-ttu-id="e0cbe-160">В зависимости от описания hello в предыдущем разделе hello, hello следующие пять гибридные сценарии используйте соответствующие **ключ содержимого**-**политики доставки активов** сочетания конфигурации (hello образцы, упомянутые в последнем столбце hello выполните hello таблицы).</span><span class="sxs-lookup"><span data-stu-id="e0cbe-160">Based on hello explanations in hello previous section, hello following five hybrid scenarios use respective **Content key**-**Asset delivery policy** configuration combinations (hello samples mentioned in hello last column follow hello table):</span></span>

|<span data-ttu-id="e0cbe-161">**Размещение содержимого и источник**</span><span class="sxs-lookup"><span data-stu-id="e0cbe-161">**Content hosting & origin**</span></span>|<span data-ttu-id="e0cbe-162">**Шифрование DRM**</span><span class="sxs-lookup"><span data-stu-id="e0cbe-162">**DRM encryption**</span></span>|<span data-ttu-id="e0cbe-163">**Доставка лицензий DRM**</span><span class="sxs-lookup"><span data-stu-id="e0cbe-163">**DRM license delivery**</span></span>|<span data-ttu-id="e0cbe-164">**Настройка ключа содержимого**</span><span class="sxs-lookup"><span data-stu-id="e0cbe-164">**Configure content key**</span></span>|<span data-ttu-id="e0cbe-165">**Настройка политики доставки для ресурса-контейнера**</span><span class="sxs-lookup"><span data-stu-id="e0cbe-165">**Configure asset delivery policy**</span></span>|<span data-ttu-id="e0cbe-166">**Пример**</span><span class="sxs-lookup"><span data-stu-id="e0cbe-166">**Sample**</span></span>|
|---|---|---|---|---|---|
|<span data-ttu-id="e0cbe-167">AMS</span><span class="sxs-lookup"><span data-stu-id="e0cbe-167">AMS</span></span>|<span data-ttu-id="e0cbe-168">AMS</span><span class="sxs-lookup"><span data-stu-id="e0cbe-168">AMS</span></span>|<span data-ttu-id="e0cbe-169">AMS</span><span class="sxs-lookup"><span data-stu-id="e0cbe-169">AMS</span></span>|<span data-ttu-id="e0cbe-170">Да</span><span class="sxs-lookup"><span data-stu-id="e0cbe-170">Yes</span></span>|<span data-ttu-id="e0cbe-171">Да</span><span class="sxs-lookup"><span data-stu-id="e0cbe-171">Yes</span></span>|<span data-ttu-id="e0cbe-172">Пример 1</span><span class="sxs-lookup"><span data-stu-id="e0cbe-172">Sample 1</span></span>|
|<span data-ttu-id="e0cbe-173">AMS</span><span class="sxs-lookup"><span data-stu-id="e0cbe-173">AMS</span></span>|<span data-ttu-id="e0cbe-174">AMS</span><span class="sxs-lookup"><span data-stu-id="e0cbe-174">AMS</span></span>|<span data-ttu-id="e0cbe-175">Сторонний производитель</span><span class="sxs-lookup"><span data-stu-id="e0cbe-175">Third-party</span></span>|<span data-ttu-id="e0cbe-176">Да</span><span class="sxs-lookup"><span data-stu-id="e0cbe-176">Yes</span></span>|<span data-ttu-id="e0cbe-177">Да</span><span class="sxs-lookup"><span data-stu-id="e0cbe-177">Yes</span></span>|<span data-ttu-id="e0cbe-178">Пример 2</span><span class="sxs-lookup"><span data-stu-id="e0cbe-178">Sample 2</span></span>|
|<span data-ttu-id="e0cbe-179">AMS</span><span class="sxs-lookup"><span data-stu-id="e0cbe-179">AMS</span></span>|<span data-ttu-id="e0cbe-180">Сторонний производитель</span><span class="sxs-lookup"><span data-stu-id="e0cbe-180">Third-party</span></span>|<span data-ttu-id="e0cbe-181">AMS</span><span class="sxs-lookup"><span data-stu-id="e0cbe-181">AMS</span></span>|<span data-ttu-id="e0cbe-182">Да</span><span class="sxs-lookup"><span data-stu-id="e0cbe-182">Yes</span></span>|<span data-ttu-id="e0cbe-183">Нет</span><span class="sxs-lookup"><span data-stu-id="e0cbe-183">No</span></span>|<span data-ttu-id="e0cbe-184">Пример 3</span><span class="sxs-lookup"><span data-stu-id="e0cbe-184">Sample 3</span></span>|
|<span data-ttu-id="e0cbe-185">AMS</span><span class="sxs-lookup"><span data-stu-id="e0cbe-185">AMS</span></span>|<span data-ttu-id="e0cbe-186">Сторонний производитель</span><span class="sxs-lookup"><span data-stu-id="e0cbe-186">Third-party</span></span>|<span data-ttu-id="e0cbe-187">Внешняя</span><span class="sxs-lookup"><span data-stu-id="e0cbe-187">Outside</span></span>|<span data-ttu-id="e0cbe-188">Нет</span><span class="sxs-lookup"><span data-stu-id="e0cbe-188">No</span></span>|<span data-ttu-id="e0cbe-189">Нет</span><span class="sxs-lookup"><span data-stu-id="e0cbe-189">No</span></span>|<span data-ttu-id="e0cbe-190">Пример 4</span><span class="sxs-lookup"><span data-stu-id="e0cbe-190">Sample 4</span></span>|
|<span data-ttu-id="e0cbe-191">Сторонний производитель</span><span class="sxs-lookup"><span data-stu-id="e0cbe-191">Third-party</span></span>|<span data-ttu-id="e0cbe-192">Сторонний производитель</span><span class="sxs-lookup"><span data-stu-id="e0cbe-192">Third-party</span></span>|<span data-ttu-id="e0cbe-193">AMS</span><span class="sxs-lookup"><span data-stu-id="e0cbe-193">AMS</span></span>|<span data-ttu-id="e0cbe-194">Да</span><span class="sxs-lookup"><span data-stu-id="e0cbe-194">Yes</span></span>|<span data-ttu-id="e0cbe-195">Нет</span><span class="sxs-lookup"><span data-stu-id="e0cbe-195">No</span></span>|    

<span data-ttu-id="e0cbe-196">В образцы hello защиты PlayReady работе DASH и smooth streaming.</span><span class="sxs-lookup"><span data-stu-id="e0cbe-196">In hello samples, PlayReady protection works for both DASH and smooth streaming.</span></span> <span data-ttu-id="e0cbe-197">Hello видео URL-адреса smooth streaming URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="e0cbe-197">hello video URLs below are smooth streaming URLs.</span></span> <span data-ttu-id="e0cbe-198">tooget Здравствуйте соответствующего URL-адреса, ТИРЕ, просто добавлять» (формат = mpd время csf)».</span><span class="sxs-lookup"><span data-stu-id="e0cbe-198">tooget hello corresponding DASH URLs, just append "(format=mpd-time-csf)".</span></span> <span data-ttu-id="e0cbe-199">Можно использовать hello [мультимедиа azure тестирования проигрывателя](http://aka.ms/amtest) tootest в браузере.</span><span class="sxs-lookup"><span data-stu-id="e0cbe-199">You could use hello [azure media test player](http://aka.ms/amtest) tootest in a browser.</span></span> <span data-ttu-id="e0cbe-200">Позволяет tooconfigure которого потоковой передачи toouse протокола, в которой технический.</span><span class="sxs-lookup"><span data-stu-id="e0cbe-200">It allows you tooconfigure which streaming protocol toouse, under which tech.</span></span> <span data-ttu-id="e0cbe-201">IE11 и MS Edge в Windows 10 поддерживают PlayReady через EME.</span><span class="sxs-lookup"><span data-stu-id="e0cbe-201">IE11 and MS Edge on Windows 10 support PlayReady through EME.</span></span> <span data-ttu-id="e0cbe-202">Дополнительные сведения см. в разделе [средство тестирования, сведения о hello](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/).</span><span class="sxs-lookup"><span data-stu-id="e0cbe-202">For more information, see [details about hello test tool](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/).</span></span>

### <a name="sample-1"></a><span data-ttu-id="e0cbe-203">Пример 1</span><span class="sxs-lookup"><span data-stu-id="e0cbe-203">Sample 1</span></span>

* <span data-ttu-id="e0cbe-204">URL-адрес источника (основной): https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="e0cbe-204">Source (base) URL: https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest</span></span> 
* <span data-ttu-id="e0cbe-205">URL-адрес для приобретения лицензии PlayReady (DASH и Smooth Streaming): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span><span class="sxs-lookup"><span data-stu-id="e0cbe-205">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span></span> 
* <span data-ttu-id="e0cbe-206">URL-адрес для приобретения лицензии Widevine (DASH): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4</span><span class="sxs-lookup"><span data-stu-id="e0cbe-206">Widevine LA_URL (DASH): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4</span></span> 
* <span data-ttu-id="e0cbe-207">URL-адрес для приобретения лицензии FairPlay (HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8</span><span class="sxs-lookup"><span data-stu-id="e0cbe-207">FairPlay LA_URL (HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8</span></span> 

### <a name="sample-2"></a><span data-ttu-id="e0cbe-208">Пример 2</span><span class="sxs-lookup"><span data-stu-id="e0cbe-208">Sample 2</span></span>

* <span data-ttu-id="e0cbe-209">URL-адрес источника (основной): http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="e0cbe-209">Source (base) URL: http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest</span></span> 
* <span data-ttu-id="e0cbe-210">URL-адрес для приобретения лицензии PlayReady (DASH и Smooth Streaming): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx</span><span class="sxs-lookup"><span data-stu-id="e0cbe-210">PlayReady LA_URL (DASH & smooth): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx</span></span> 

### <a name="sample-3"></a><span data-ttu-id="e0cbe-211">Пример 3</span><span class="sxs-lookup"><span data-stu-id="e0cbe-211">Sample 3</span></span>

* <span data-ttu-id="e0cbe-212">URL-адрес источника: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="e0cbe-212">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest</span></span> 
* <span data-ttu-id="e0cbe-213">URL-адрес для приобретения лицензии PlayReady (DASH и Smooth Streaming): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span><span class="sxs-lookup"><span data-stu-id="e0cbe-213">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span></span> 

### <a name="sample-4"></a><span data-ttu-id="e0cbe-214">Пример 4</span><span class="sxs-lookup"><span data-stu-id="e0cbe-214">Sample 4</span></span>

* <span data-ttu-id="e0cbe-215">URL-адрес источника: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="e0cbe-215">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest</span></span> 
* <span data-ttu-id="e0cbe-216">URL-адрес для приобретения лицензии PlayReady (DASH и Smooth Streaming): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx</span><span class="sxs-lookup"><span data-stu-id="e0cbe-216">PlayReady LA_URL (DASH & smooth): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx</span></span> 

## <a name="summary"></a><span data-ttu-id="e0cbe-217">Сводка</span><span class="sxs-lookup"><span data-stu-id="e0cbe-217">Summary</span></span>

<span data-ttu-id="e0cbe-218">Таким образом, компоненты DRM служб мультимедиа Azure являются гибкими. Их можно использовать в гибридных сценариях при правильной настройке ключа содержимого и политики доставки ресурсов, как описано в этой статье.</span><span class="sxs-lookup"><span data-stu-id="e0cbe-218">In summary, Azure Media Services DRM components are flexible, you can use them in a hybrid scenario by properly configuring content key and asset delivery policy, as described in this topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0cbe-219">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e0cbe-219">Next steps</span></span>
<span data-ttu-id="e0cbe-220">Просмотрите схемы обучения работе со службами мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="e0cbe-220">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e0cbe-221">Отзывы</span><span class="sxs-lookup"><span data-stu-id="e0cbe-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

