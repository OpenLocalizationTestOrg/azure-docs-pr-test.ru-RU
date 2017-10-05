---
title: "Гибридная структура подсистем DRM с использованием служб мультимедиа Azure | Документация Майкрософт"
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
ms.openlocfilehash: 841b1164db6fd1a2c029b98392509c15f23158e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="hybrid-design-of-drm-subsystems"></a><span data-ttu-id="2fb36-103">Гибридная структура подсистем DRM</span><span class="sxs-lookup"><span data-stu-id="2fb36-103">Hybrid design of DRM subsystem(s)</span></span>

<span data-ttu-id="2fb36-104">Здесь рассматривается гибридная структура подсистем управления цифровыми правами (DRM) с использованием служб мультимедиа Azure.</span><span class="sxs-lookup"><span data-stu-id="2fb36-104">This topic discusses hybrid design of DRM subsystem(s) using Azure Media Services.</span></span>

## <a name="overview"></a><span data-ttu-id="2fb36-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="2fb36-105">Overview</span></span>

<span data-ttu-id="2fb36-106">Службы мультимедиа Azure поддерживают три следующие системы DRM:</span><span class="sxs-lookup"><span data-stu-id="2fb36-106">Azure Media Services provides support for the following three DRM system:</span></span>

* <span data-ttu-id="2fb36-107">PlayReady</span><span class="sxs-lookup"><span data-stu-id="2fb36-107">PlayReady</span></span>
* <span data-ttu-id="2fb36-108">Widevine (модульная);</span><span class="sxs-lookup"><span data-stu-id="2fb36-108">Widevine (Modular)</span></span>
* <span data-ttu-id="2fb36-109">FairPlay</span><span class="sxs-lookup"><span data-stu-id="2fb36-109">FairPlay</span></span>

<span data-ttu-id="2fb36-110">Поддержка DRM включает в себя шифрование DRM (динамическое шифрование) и доставку лицензий, а Проигрыватель мультимедиа Azure поддерживает все 3 системы DRM как пакет SDK проигрывателя браузера.</span><span class="sxs-lookup"><span data-stu-id="2fb36-110">The DRM support includes DRM encryption (dynamic encryption) and license delivery, with Azure Media Player supporting all 3 DRMs as a browser player SDK.</span></span>

<span data-ttu-id="2fb36-111">Подробные сведения о проектировании и реализации подсистемы DRM с CENC см. в статье [CENC с несколькими DRM и управление доступом: справочное проектирование и реализация в Azure и службах мультимедиа Azure](media-services-cenc-with-multidrm-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="2fb36-111">For a detailed treatment of DRM/CENC subsystem design and implementation, please see the document titled [CENC with Multi-DRM and Access Control](media-services-cenc-with-multidrm-access-control.md).</span></span>

<span data-ttu-id="2fb36-112">Несмотря на то что мы обеспечиваем полную поддержку трех систем DRM, иногда следует использовать различные части собственной инфраструктуры или подсистемы вместе со службами мультимедиа Azure, чтобы создать гибридную подсистему DRM.</span><span class="sxs-lookup"><span data-stu-id="2fb36-112">Although we offer complete support for three DRM systems, sometimes customers need to use various parts of their own infrastructure/subsystems in addition to Azure Media Services to build a hybrid DRM subsystem.</span></span>

<span data-ttu-id="2fb36-113">Ниже представлены некоторые часто задаваемые вопросы пользователей:</span><span class="sxs-lookup"><span data-stu-id="2fb36-113">Below are some common questions asked by customers:</span></span>

* <span data-ttu-id="2fb36-114">Можно ли использовать собственные серверы лицензирования DRM?</span><span class="sxs-lookup"><span data-stu-id="2fb36-114">"Can I use my own DRM license servers?"</span></span> <span data-ttu-id="2fb36-115">(В этом случае пользователи вложили средства в кластер серверов лицензирования DRM со встроенной бизнес-логикой.)</span><span class="sxs-lookup"><span data-stu-id="2fb36-115">(In this case, customers have invested in DRM license server farm with embedded business logic).</span></span>
* <span data-ttu-id="2fb36-116">Можно ли использовать доставку лицензий DRM в службах мультимедиа Azure без размещения содержимого в AMS?</span><span class="sxs-lookup"><span data-stu-id="2fb36-116">"Can I use only your DRM license delivery in Azure Media Services without hosting content in AMS?"</span></span>

## <a name="modularity-of-the-ams-drm-platform"></a><span data-ttu-id="2fb36-117">Модульность платформы AMS DRM</span><span class="sxs-lookup"><span data-stu-id="2fb36-117">Modularity of the AMS DRM platform</span></span>

<span data-ttu-id="2fb36-118">Как часть комплексной облачной видеоплатформы, DRM служб мультимедиа Azure имеет гибкую и модульную структуру.</span><span class="sxs-lookup"><span data-stu-id="2fb36-118">As part of a comprehensive cloud video platform, Azure Media Services DRM has a design with flexibility and modularity in mind.</span></span> <span data-ttu-id="2fb36-119">Службы мультимедиа Azure можно использовать вместе с любым сочетанием, представленным в следующей таблице (после таблицы идет объяснение).</span><span class="sxs-lookup"><span data-stu-id="2fb36-119">You can use Azure Media Services with any of the following different combinations described in the table below (an explanation of the notation used in the table follows).</span></span> 

|<span data-ttu-id="2fb36-120">**Размещение содержимого и источник**</span><span class="sxs-lookup"><span data-stu-id="2fb36-120">**Content hosting & origin**</span></span>|<span data-ttu-id="2fb36-121">**Шифрование содержимого**</span><span class="sxs-lookup"><span data-stu-id="2fb36-121">**Content encryption**</span></span>|<span data-ttu-id="2fb36-122">**Доставка лицензий DRM**</span><span class="sxs-lookup"><span data-stu-id="2fb36-122">**DRM license delivery**</span></span>|
|---|---|---|
|<span data-ttu-id="2fb36-123">AMS</span><span class="sxs-lookup"><span data-stu-id="2fb36-123">AMS</span></span>|<span data-ttu-id="2fb36-124">AMS</span><span class="sxs-lookup"><span data-stu-id="2fb36-124">AMS</span></span>|<span data-ttu-id="2fb36-125">AMS</span><span class="sxs-lookup"><span data-stu-id="2fb36-125">AMS</span></span>|
|<span data-ttu-id="2fb36-126">AMS</span><span class="sxs-lookup"><span data-stu-id="2fb36-126">AMS</span></span>|<span data-ttu-id="2fb36-127">AMS</span><span class="sxs-lookup"><span data-stu-id="2fb36-127">AMS</span></span>|<span data-ttu-id="2fb36-128">Сторонний производитель</span><span class="sxs-lookup"><span data-stu-id="2fb36-128">Third-party</span></span>|
|<span data-ttu-id="2fb36-129">AMS</span><span class="sxs-lookup"><span data-stu-id="2fb36-129">AMS</span></span>|<span data-ttu-id="2fb36-130">Сторонний производитель</span><span class="sxs-lookup"><span data-stu-id="2fb36-130">Third-party</span></span>|<span data-ttu-id="2fb36-131">AMS</span><span class="sxs-lookup"><span data-stu-id="2fb36-131">AMS</span></span>|
|<span data-ttu-id="2fb36-132">AMS</span><span class="sxs-lookup"><span data-stu-id="2fb36-132">AMS</span></span>|<span data-ttu-id="2fb36-133">Сторонний производитель</span><span class="sxs-lookup"><span data-stu-id="2fb36-133">Third-party</span></span>|<span data-ttu-id="2fb36-134">Сторонний производитель</span><span class="sxs-lookup"><span data-stu-id="2fb36-134">Third-party</span></span>|
|<span data-ttu-id="2fb36-135">Сторонний производитель</span><span class="sxs-lookup"><span data-stu-id="2fb36-135">Third-party</span></span>|<span data-ttu-id="2fb36-136">Сторонний производитель</span><span class="sxs-lookup"><span data-stu-id="2fb36-136">Third-party</span></span>|<span data-ttu-id="2fb36-137">AMS</span><span class="sxs-lookup"><span data-stu-id="2fb36-137">AMS</span></span>|

### <a name="content-hosting--origin"></a><span data-ttu-id="2fb36-138">Размещение содержимого и источник</span><span class="sxs-lookup"><span data-stu-id="2fb36-138">Content hosting & origin</span></span>

* <span data-ttu-id="2fb36-139">AMS: видеоресурсы размещаются в AMS, а потоковая передача ведется с помощью конечных точек потоковой передачи AMS (но не обязательно с динамической упаковкой).</span><span class="sxs-lookup"><span data-stu-id="2fb36-139">AMS: video asset is hosted in AMS and streaming is through AMS streaming endpoints (but not necessarily dynamic packaging).</span></span>
* <span data-ttu-id="2fb36-140">Сторонний производитель: видео размещается и доставляется с помощью платформы потоковой передачи стороннего производителя за пределами AMS.</span><span class="sxs-lookup"><span data-stu-id="2fb36-140">Third-party: video is hosted and delivered on a third-party streaming platform outside of AMS.</span></span>

### <a name="content-encryption"></a><span data-ttu-id="2fb36-141">Шифрование содержимого</span><span class="sxs-lookup"><span data-stu-id="2fb36-141">Content encryption</span></span>

* <span data-ttu-id="2fb36-142">AMS: шифрование содержимого происходит динамически или по требованию с помощью динамического шифрования AMS.</span><span class="sxs-lookup"><span data-stu-id="2fb36-142">AMS: content encryption is performed dynamically/on-demand by AMS dynamic encryption.</span></span>
* <span data-ttu-id="2fb36-143">Сторонний производитель: шифрование содержимого выполняется за пределами AMS с использованием рабочего процесса предварительной обработки.</span><span class="sxs-lookup"><span data-stu-id="2fb36-143">Third-party: content encryption is performed outside of AMS using a pre-processing workflow.</span></span>

### <a name="drm-license-delivery"></a><span data-ttu-id="2fb36-144">Доставка лицензий DRM</span><span class="sxs-lookup"><span data-stu-id="2fb36-144">DRM license delivery</span></span>

* <span data-ttu-id="2fb36-145">AMS: лицензию DRM доставляет служба доставки лицензий AMS.</span><span class="sxs-lookup"><span data-stu-id="2fb36-145">AMS: DRM license is delivered by AMS license delivery service.</span></span>
* <span data-ttu-id="2fb36-146">Сторонний производитель: лицензию DRM доставляет сервер лицензирования DRM стороннего производителя за пределами AMS.</span><span class="sxs-lookup"><span data-stu-id="2fb36-146">Third-party: DRM license is delivered by a third-party DRM license server outside of AMS.</span></span>

## <a name="configure-based-on-your-hybrid-scenario"></a><span data-ttu-id="2fb36-147">Настройка на основе своего гибридного сценария</span><span class="sxs-lookup"><span data-stu-id="2fb36-147">Configure based on your hybrid scenario</span></span>

### <a name="content-key"></a><span data-ttu-id="2fb36-148">Ключ содержимого</span><span class="sxs-lookup"><span data-stu-id="2fb36-148">Content key</span></span>

<span data-ttu-id="2fb36-149">Настроив ключ содержимого, можно управлять следующими атрибутами динамического шифрования AMS и службы доставки лицензий AMS:</span><span class="sxs-lookup"><span data-stu-id="2fb36-149">Through configuration of a content key, you can control the following attributes of both AMS dynamic encryption and AMS license delivery service:</span></span>

* <span data-ttu-id="2fb36-150">Ключ содержимого, используемый для динамического шифрования DRM.</span><span class="sxs-lookup"><span data-stu-id="2fb36-150">The content key used for dynamic DRM encryption.</span></span>
* <span data-ttu-id="2fb36-151">Содержимое лицензии DRM, которое будет доставляться с помощью службы доставки лицензий: права, ключ содержимого и ограничения.</span><span class="sxs-lookup"><span data-stu-id="2fb36-151">DRM license content to be delivered by license delivery services: rights, content key and restrictions.</span></span>
* <span data-ttu-id="2fb36-152">Тип **ограничения политики авторизации ключа содержимого**: открытое, IP-адрес или ограничение по токену.</span><span class="sxs-lookup"><span data-stu-id="2fb36-152">Type of **content key authorization policy restriction**: open, IP, or token restriction.</span></span>
* <span data-ttu-id="2fb36-153">Если для **ограничения политики авторизации ключа содержимого** используется **токен**, перед выдачей лицензии необходимо выполнить условия **ограничения политики авторизации ключа содержимого**.</span><span class="sxs-lookup"><span data-stu-id="2fb36-153">If **token** type of **content key authorization policy restriction is used**, the **content key authorization policy restriction** must be met before a license is issued.</span></span>

### <a name="asset-delivery-policy"></a><span data-ttu-id="2fb36-154">Политика доставки ресурсов</span><span class="sxs-lookup"><span data-stu-id="2fb36-154">Asset delivery policy</span></span>

<span data-ttu-id="2fb36-155">Настроив политику доставки ресурсов, можно контролировать следующие атрибуты, которые используются динамическим упаковщиком AMS и динамическим шифрованием конечной точки потоковой передачи AMS:</span><span class="sxs-lookup"><span data-stu-id="2fb36-155">Through configuration of an asset delivery policy, you can control the following attributes used by AMS dynamic packager and dynamic encryption of an AMS streaming endpoint:</span></span>

* <span data-ttu-id="2fb36-156">Протокол потоковой передачи и комбинация шифрования DRM, например DASH в CENC (PlayReady и Widevine), Smooth Streaming в PlayReady, HLS в Widevine или PlayReady.</span><span class="sxs-lookup"><span data-stu-id="2fb36-156">Streaming protocol and DRM encryption combination, such as DASH under CENC (PlayReady and Widevine), smooth streaming under PlayReady, HLS under Widevine or PlayReady.</span></span>
* <span data-ttu-id="2fb36-157">URL-адреса лицензий доставки (встроенных и по умолчанию) для каждой используемой системы DRM.</span><span class="sxs-lookup"><span data-stu-id="2fb36-157">The default/embedded license delivery URLs for each of the involved DRMs.</span></span>
* <span data-ttu-id="2fb36-158">Содержат ли URL-адреса для приобретения лицензий (LA_URL) в DASH MPD или списке воспроизведения HLS строку запроса идентификатора ключа (KID) для Widevine и FairPlay соответственно.</span><span class="sxs-lookup"><span data-stu-id="2fb36-158">Whether license acquisition URLs (LA_URLs) in DASH MPD or HLS playlist contain query string of key ID (KID) for Widevine and FairPlay, respectively.</span></span>

## <a name="scenarios-and-samples"></a><span data-ttu-id="2fb36-159">Сценарии и примеры</span><span class="sxs-lookup"><span data-stu-id="2fb36-159">Scenarios and samples</span></span>

<span data-ttu-id="2fb36-160">Как описано в предыдущем разделе, в следующих пяти гибридных сценариях используются соответствующие сочетания конфигураций **ключа содержимого** -**политики доставки ресурсов** (примеры указаны в последнем столбце таблицы):</span><span class="sxs-lookup"><span data-stu-id="2fb36-160">Based on the explanations in the previous section, the following five hybrid scenarios use respective **Content key**-**Asset delivery policy** configuration combinations (the samples mentioned in the last column follow the table):</span></span>

|<span data-ttu-id="2fb36-161">**Размещение содержимого и источник**</span><span class="sxs-lookup"><span data-stu-id="2fb36-161">**Content hosting & origin**</span></span>|<span data-ttu-id="2fb36-162">**Шифрование DRM**</span><span class="sxs-lookup"><span data-stu-id="2fb36-162">**DRM encryption**</span></span>|<span data-ttu-id="2fb36-163">**Доставка лицензий DRM**</span><span class="sxs-lookup"><span data-stu-id="2fb36-163">**DRM license delivery**</span></span>|<span data-ttu-id="2fb36-164">**Настройка ключа содержимого**</span><span class="sxs-lookup"><span data-stu-id="2fb36-164">**Configure content key**</span></span>|<span data-ttu-id="2fb36-165">**Настройка политики доставки для ресурса-контейнера**</span><span class="sxs-lookup"><span data-stu-id="2fb36-165">**Configure asset delivery policy**</span></span>|<span data-ttu-id="2fb36-166">**Пример**</span><span class="sxs-lookup"><span data-stu-id="2fb36-166">**Sample**</span></span>|
|---|---|---|---|---|---|
|<span data-ttu-id="2fb36-167">AMS</span><span class="sxs-lookup"><span data-stu-id="2fb36-167">AMS</span></span>|<span data-ttu-id="2fb36-168">AMS</span><span class="sxs-lookup"><span data-stu-id="2fb36-168">AMS</span></span>|<span data-ttu-id="2fb36-169">AMS</span><span class="sxs-lookup"><span data-stu-id="2fb36-169">AMS</span></span>|<span data-ttu-id="2fb36-170">Да</span><span class="sxs-lookup"><span data-stu-id="2fb36-170">Yes</span></span>|<span data-ttu-id="2fb36-171">Да</span><span class="sxs-lookup"><span data-stu-id="2fb36-171">Yes</span></span>|<span data-ttu-id="2fb36-172">Пример 1</span><span class="sxs-lookup"><span data-stu-id="2fb36-172">Sample 1</span></span>|
|<span data-ttu-id="2fb36-173">AMS</span><span class="sxs-lookup"><span data-stu-id="2fb36-173">AMS</span></span>|<span data-ttu-id="2fb36-174">AMS</span><span class="sxs-lookup"><span data-stu-id="2fb36-174">AMS</span></span>|<span data-ttu-id="2fb36-175">Сторонний производитель</span><span class="sxs-lookup"><span data-stu-id="2fb36-175">Third-party</span></span>|<span data-ttu-id="2fb36-176">Да</span><span class="sxs-lookup"><span data-stu-id="2fb36-176">Yes</span></span>|<span data-ttu-id="2fb36-177">Да</span><span class="sxs-lookup"><span data-stu-id="2fb36-177">Yes</span></span>|<span data-ttu-id="2fb36-178">Пример 2</span><span class="sxs-lookup"><span data-stu-id="2fb36-178">Sample 2</span></span>|
|<span data-ttu-id="2fb36-179">AMS</span><span class="sxs-lookup"><span data-stu-id="2fb36-179">AMS</span></span>|<span data-ttu-id="2fb36-180">Сторонний производитель</span><span class="sxs-lookup"><span data-stu-id="2fb36-180">Third-party</span></span>|<span data-ttu-id="2fb36-181">AMS</span><span class="sxs-lookup"><span data-stu-id="2fb36-181">AMS</span></span>|<span data-ttu-id="2fb36-182">Да</span><span class="sxs-lookup"><span data-stu-id="2fb36-182">Yes</span></span>|<span data-ttu-id="2fb36-183">Нет</span><span class="sxs-lookup"><span data-stu-id="2fb36-183">No</span></span>|<span data-ttu-id="2fb36-184">Пример 3</span><span class="sxs-lookup"><span data-stu-id="2fb36-184">Sample 3</span></span>|
|<span data-ttu-id="2fb36-185">AMS</span><span class="sxs-lookup"><span data-stu-id="2fb36-185">AMS</span></span>|<span data-ttu-id="2fb36-186">Сторонний производитель</span><span class="sxs-lookup"><span data-stu-id="2fb36-186">Third-party</span></span>|<span data-ttu-id="2fb36-187">Внешняя</span><span class="sxs-lookup"><span data-stu-id="2fb36-187">Outside</span></span>|<span data-ttu-id="2fb36-188">Нет</span><span class="sxs-lookup"><span data-stu-id="2fb36-188">No</span></span>|<span data-ttu-id="2fb36-189">Нет</span><span class="sxs-lookup"><span data-stu-id="2fb36-189">No</span></span>|<span data-ttu-id="2fb36-190">Пример 4</span><span class="sxs-lookup"><span data-stu-id="2fb36-190">Sample 4</span></span>|
|<span data-ttu-id="2fb36-191">Сторонний производитель</span><span class="sxs-lookup"><span data-stu-id="2fb36-191">Third-party</span></span>|<span data-ttu-id="2fb36-192">Сторонний производитель</span><span class="sxs-lookup"><span data-stu-id="2fb36-192">Third-party</span></span>|<span data-ttu-id="2fb36-193">AMS</span><span class="sxs-lookup"><span data-stu-id="2fb36-193">AMS</span></span>|<span data-ttu-id="2fb36-194">Да</span><span class="sxs-lookup"><span data-stu-id="2fb36-194">Yes</span></span>|<span data-ttu-id="2fb36-195">Нет</span><span class="sxs-lookup"><span data-stu-id="2fb36-195">No</span></span>|    

<span data-ttu-id="2fb36-196">В примерах защита PlayReady работает как для DASH, так и для Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="2fb36-196">In the samples, PlayReady protection works for both DASH and smooth streaming.</span></span> <span data-ttu-id="2fb36-197">Ниже приведены URL-адреса видео, которые являются URL-адресами Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="2fb36-197">The video URLs below are smooth streaming URLs.</span></span> <span data-ttu-id="2fb36-198">Чтобы получить соответствующие URL-адреса DASH, просто добавьте "(format=mpd-time-csf)".</span><span class="sxs-lookup"><span data-stu-id="2fb36-198">To get the corresponding DASH URLs, just append "(format=mpd-time-csf)".</span></span> <span data-ttu-id="2fb36-199">Для проверки в браузере можно использовать [проигрыватель для тестирования мультимедиа Azure](http://aka.ms/amtest).</span><span class="sxs-lookup"><span data-stu-id="2fb36-199">You could use the [azure media test player](http://aka.ms/amtest) to test in a browser.</span></span> <span data-ttu-id="2fb36-200">Он позволяет настроить протокол потоковой передачи для использования с каждой технологией.</span><span class="sxs-lookup"><span data-stu-id="2fb36-200">It allows you to configure which streaming protocol to use, under which tech.</span></span> <span data-ttu-id="2fb36-201">IE11 и MS Edge в Windows 10 поддерживают PlayReady через EME.</span><span class="sxs-lookup"><span data-stu-id="2fb36-201">IE11 and MS Edge on Windows 10 support PlayReady through EME.</span></span> <span data-ttu-id="2fb36-202">Дополнительные сведения см. в записи блога [Azure Media Test Tool](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/) (Средство для тестирования мультимедиа Azure).</span><span class="sxs-lookup"><span data-stu-id="2fb36-202">For more information, see [details about the test tool](https://blogs.msdn.microsoft.com/playready4/2016/02/28/azure-media-test-tool/).</span></span>

### <a name="sample-1"></a><span data-ttu-id="2fb36-203">Пример 1</span><span class="sxs-lookup"><span data-stu-id="2fb36-203">Sample 1</span></span>

* <span data-ttu-id="2fb36-204">URL-адрес источника (основной): https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="2fb36-204">Source (base) URL: https://willzhanmswest.streaming.mediaservices.windows.net/1efbd6bb-1e66-4e53-88c3-f7e5657a9bbd/RussianWaltz.ism/manifest</span></span> 
* <span data-ttu-id="2fb36-205">URL-адрес для приобретения лицензии PlayReady (DASH и Smooth Streaming): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span><span class="sxs-lookup"><span data-stu-id="2fb36-205">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span></span> 
* <span data-ttu-id="2fb36-206">URL-адрес для приобретения лицензии Widevine (DASH): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4</span><span class="sxs-lookup"><span data-stu-id="2fb36-206">Widevine LA_URL (DASH): https://willzhanmswest.keydelivery.mediaservices.windows.net/Widevine/?kid=78de73ae-6d0f-470a-8f13-5c91f7c4</span></span> 
* <span data-ttu-id="2fb36-207">URL-адрес для приобретения лицензии FairPlay (HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8</span><span class="sxs-lookup"><span data-stu-id="2fb36-207">FairPlay LA_URL (HLS): https://willzhanmswest.keydelivery.mediaservices.windows.net/FairPlay/?kid=ba7e8fb0-ee22-4291-9654-6222ac611bd8</span></span> 

### <a name="sample-2"></a><span data-ttu-id="2fb36-208">Пример 2</span><span class="sxs-lookup"><span data-stu-id="2fb36-208">Sample 2</span></span>

* <span data-ttu-id="2fb36-209">URL-адрес источника (основной): http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest</span><span class="sxs-lookup"><span data-stu-id="2fb36-209">Source (base) URL: http://willzhanmswest.streaming.mediaservices.windows.net/1a670626-4515-49ee-9e7f-cd50853e41d8/Microsoft_HoloLens_TransformYourWorld_816p23.ism/Manifest</span></span> 
* <span data-ttu-id="2fb36-210">URL-адрес для приобретения лицензии PlayReady (DASH и Smooth Streaming): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx</span><span class="sxs-lookup"><span data-stu-id="2fb36-210">PlayReady LA_URL (DASH & smooth): http://willzhan12.cloudapp.net/PlayReady/RightsManager.asmx</span></span> 

### <a name="sample-3"></a><span data-ttu-id="2fb36-211">Пример 3</span><span class="sxs-lookup"><span data-stu-id="2fb36-211">Sample 3</span></span>

* <span data-ttu-id="2fb36-212">URL-адрес источника: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="2fb36-212">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/8d078cf8-d621-406c-84ca-88e6b9454acc/20150807-bridges-2500.ism/manifest</span></span> 
* <span data-ttu-id="2fb36-213">URL-адрес для приобретения лицензии PlayReady (DASH и Smooth Streaming): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span><span class="sxs-lookup"><span data-stu-id="2fb36-213">PlayReady LA_URL (DASH & smooth): https://willzhanmswest.keydelivery.mediaservices.windows.net/PlayReady/</span></span> 

### <a name="sample-4"></a><span data-ttu-id="2fb36-214">Пример 4</span><span class="sxs-lookup"><span data-stu-id="2fb36-214">Sample 4</span></span>

* <span data-ttu-id="2fb36-215">URL-адрес источника: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest</span><span class="sxs-lookup"><span data-stu-id="2fb36-215">Source URL: https://willzhanmswest.streaming.mediaservices.windows.net/7c085a59-ae9a-411e-842c-ef10f96c3f89/20150807-bridges-2500.ism/manifest</span></span> 
* <span data-ttu-id="2fb36-216">URL-адрес для приобретения лицензии PlayReady (DASH и Smooth Streaming): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx</span><span class="sxs-lookup"><span data-stu-id="2fb36-216">PlayReady LA_URL (DASH & smooth): https://willzhan12.cloudapp.net/playready/rightsmanager.asmx</span></span> 

## <a name="summary"></a><span data-ttu-id="2fb36-217">Сводка</span><span class="sxs-lookup"><span data-stu-id="2fb36-217">Summary</span></span>

<span data-ttu-id="2fb36-218">Таким образом, компоненты DRM служб мультимедиа Azure являются гибкими. Их можно использовать в гибридных сценариях при правильной настройке ключа содержимого и политики доставки ресурсов, как описано в этой статье.</span><span class="sxs-lookup"><span data-stu-id="2fb36-218">In summary, Azure Media Services DRM components are flexible, you can use them in a hybrid scenario by properly configuring content key and asset delivery policy, as described in this topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2fb36-219">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2fb36-219">Next steps</span></span>
<span data-ttu-id="2fb36-220">Просмотрите схемы обучения работе со службами мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="2fb36-220">View Media Services learning paths.</span></span>

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="2fb36-221">Отзывы</span><span class="sxs-lookup"><span data-stu-id="2fb36-221">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

