---
title: "Обзор шаблона лицензии Widevine | Документация Майкрософт"
description: "В этом разделе содержится обзор шаблона лицензии Widevine, который используется для настройки лицензий Widevine."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0e6f1f05-7ed6-4ed6-82a0-0cc2182b075a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 667ff16dc7608dab2a5b8b1fd7df715da4620ca1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="widevine-license-template-overview"></a><span data-ttu-id="29776-103">Обзор шаблона лицензии Widevine</span><span class="sxs-lookup"><span data-stu-id="29776-103">Widevine license template overview</span></span>
## <a name="overview"></a><span data-ttu-id="29776-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="29776-104">Overview</span></span>
<span data-ttu-id="29776-105">Теперь службы мультимедиа Azure позволяют настраивать и запрашивать лицензии Widevine.</span><span class="sxs-lookup"><span data-stu-id="29776-105">Azure Media Services now enables you to configure and request Widevine licenses.</span></span> <span data-ttu-id="29776-106">Когда проигрыватель конечного пользователя пытается воспроизвести содержимое, защищенное с помощью Widevine, в службу доставки лицензий отправляется запрос на получение лицензии.</span><span class="sxs-lookup"><span data-stu-id="29776-106">When the end user player tries to play your Widevine protected content, a request is sent to the license delivery service to obtain a license.</span></span> <span data-ttu-id="29776-107">Если служба лицензий утверждает запрос, она выдает лицензию, которая отправляется клиенту и может использоваться для расшифровки и воспроизведения указанного содержимого.</span><span class="sxs-lookup"><span data-stu-id="29776-107">If the license service approves the request, it issues the license which is sent to the client and can be used to decrypt and play the specified content.</span></span>

<span data-ttu-id="29776-108">Запрос на лицензию Widevine форматируется как сообщение JSON.</span><span class="sxs-lookup"><span data-stu-id="29776-108">Widevine license request is formatted as a JSON message.</span></span>  

>[!NOTE]
> <span data-ttu-id="29776-109">Вы можете создать пустое сообщение без значений (просто "{}"), и шаблон лицензии будет создан со всеми значениями по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="29776-109">You can choose to create an empty message with no values just "{}" and a license template will be created with all defaults.</span></span> <span data-ttu-id="29776-110">Значения по умолчанию подходят для большинства случаев.</span><span class="sxs-lookup"><span data-stu-id="29776-110">The default works for most cases.</span></span> <span data-ttu-id="29776-111">Например, для сценариев доставки лицензий на основе MS всегда используются значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="29776-111">For example, for MS based license delivery scenarios that should always be default.</span></span> <span data-ttu-id="29776-112">Если вам все-таки необходимо изменить значения параметров "provider" (поставщик) и "content_id" (идентификатор содержимого), то поставщик должен совпадать с учетными данными Google Widevine.</span><span class="sxs-lookup"><span data-stu-id="29776-112">If you do need to set the "provider" and "content_id" values, a provider must match Google's Widevine credentials.</span></span>

    {  
       “payload”:“<license challenge>”,
       “content_id”: “<content id>” 
       “provider”: ”<provider>”
       “allowed_track_types”:“<types>”,
       “content_key_specs”:[  
          {  
             “track_type”:“<track type 1>”
          },
          {  
             “track_type”:“<track type 2>”
          },
          …
       ],
       “policy_overrides”:{  
          “can_play”:<can play>,
          “can persist”:<can persist>,
          “can_renew”:<can renew>,
          “rental_duration_seconds”:<rental duration>,
          “playback_duration_seconds”:<playback duration>,
          “license_duration_seconds”:<license duration>,
          “renewal_recovery_duration_seconds”:<renewal recovery duration>,
          “renewal_server_url”:”<renewal server url>”,
          “renewal_delay_seconds”:<renewal delay>,
          “renewal_retry_interval_seconds”:<renewal retry interval>,
          “renew_with_usage”:<renew with usage>
       }
    }

## <a name="json-message"></a><span data-ttu-id="29776-113">Сообщение JSON</span><span class="sxs-lookup"><span data-stu-id="29776-113">JSON message</span></span>
| <span data-ttu-id="29776-114">Имя</span><span class="sxs-lookup"><span data-stu-id="29776-114">Name</span></span> | <span data-ttu-id="29776-115">Значение</span><span class="sxs-lookup"><span data-stu-id="29776-115">Value</span></span> | <span data-ttu-id="29776-116">Описание</span><span class="sxs-lookup"><span data-stu-id="29776-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="29776-117">payload</span><span class="sxs-lookup"><span data-stu-id="29776-117">payload</span></span> |<span data-ttu-id="29776-118">строка в кодировке Base64</span><span class="sxs-lookup"><span data-stu-id="29776-118">Base64 encoded string</span></span> |<span data-ttu-id="29776-119">Запрос на лицензию, отправленный клиентом.</span><span class="sxs-lookup"><span data-stu-id="29776-119">The license request sent by a client.</span></span> |
| <span data-ttu-id="29776-120">content_id</span><span class="sxs-lookup"><span data-stu-id="29776-120">content_id</span></span> |<span data-ttu-id="29776-121">строка в кодировке Base64</span><span class="sxs-lookup"><span data-stu-id="29776-121">Base64 encoded string</span></span> |<span data-ttu-id="29776-122">Идентификатор, используемый для получения ИД ключей и ключей содержимого для каждого content_key_specs.track_type.</span><span class="sxs-lookup"><span data-stu-id="29776-122">Identifier used to derive KeyId(s) and Content Key(s) for each content_key_specs.track_type.</span></span> |
| <span data-ttu-id="29776-123">provider</span><span class="sxs-lookup"><span data-stu-id="29776-123">provider</span></span> |<span data-ttu-id="29776-124">string</span><span class="sxs-lookup"><span data-stu-id="29776-124">string</span></span> |<span data-ttu-id="29776-125">Используется для поиска ключей и политик содержимого.</span><span class="sxs-lookup"><span data-stu-id="29776-125">Used to look up content keys and policies.</span></span> <span data-ttu-id="29776-126">Если для доставки лицензий Widevine используется доставка ключей MS, то этот параметр пропускается.</span><span class="sxs-lookup"><span data-stu-id="29776-126">If MS key delivery is used for Widevine license delivery, this parameter is ignored.</span></span> |
| <span data-ttu-id="29776-127">policy_name</span><span class="sxs-lookup"><span data-stu-id="29776-127">policy_name</span></span> |<span data-ttu-id="29776-128">string</span><span class="sxs-lookup"><span data-stu-id="29776-128">string</span></span> |<span data-ttu-id="29776-129">Имя ранее зарегистрированной политики.</span><span class="sxs-lookup"><span data-stu-id="29776-129">Name of a previously registered policy.</span></span> <span data-ttu-id="29776-130">Необязательно</span><span class="sxs-lookup"><span data-stu-id="29776-130">Optional</span></span> |
| <span data-ttu-id="29776-131">allowed_track_types</span><span class="sxs-lookup"><span data-stu-id="29776-131">allowed_track_types</span></span> |<span data-ttu-id="29776-132">enum</span><span class="sxs-lookup"><span data-stu-id="29776-132">enum</span></span> |<span data-ttu-id="29776-133">SD_ONLY или SD_HD.</span><span class="sxs-lookup"><span data-stu-id="29776-133">SD_ONLY or SD_HD.</span></span> <span data-ttu-id="29776-134">Контролирует, какие ключи содержимого должны быть включены в лицензию.</span><span class="sxs-lookup"><span data-stu-id="29776-134">Controls which content keys should be included in a license</span></span> |
| <span data-ttu-id="29776-135">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="29776-135">content_key_specs</span></span> |<span data-ttu-id="29776-136">массив структур JSON, см. раздел **Спецификации ключей содержимого** ниже</span><span class="sxs-lookup"><span data-stu-id="29776-136">array of JSON structures, see **Content Key Specs** below</span></span> |<span data-ttu-id="29776-137">Более точный контроль возвращаемых ключей содержимого.</span><span class="sxs-lookup"><span data-stu-id="29776-137">A finer grained control on what content keys to return.</span></span> <span data-ttu-id="29776-138">Более подробные сведения см. ниже в подразделе "Спецификации ключей содержимого".</span><span class="sxs-lookup"><span data-stu-id="29776-138">See Content Key Spec below for details.</span></span>  <span data-ttu-id="29776-139">Можно указать только один allowed_track_types и content_key_specs.</span><span class="sxs-lookup"><span data-stu-id="29776-139">Only one of allowed_track_types and content_key_specs can be specified.</span></span> |
| <span data-ttu-id="29776-140">use_policy_overrides_exclusively</span><span class="sxs-lookup"><span data-stu-id="29776-140">use_policy_overrides_exclusively</span></span> |<span data-ttu-id="29776-141">логическое</span><span class="sxs-lookup"><span data-stu-id="29776-141">boolean.</span></span> <span data-ttu-id="29776-142">Значение true или false</span><span class="sxs-lookup"><span data-stu-id="29776-142">true or false</span></span> |<span data-ttu-id="29776-143">Используйте атрибуты политики, указанные в параметре policy_overrides, и пропустите все сохраненные ранее политики.</span><span class="sxs-lookup"><span data-stu-id="29776-143">Use policy attributes specified by policy_overrides and omit all previously stored policy.</span></span> |
| <span data-ttu-id="29776-144">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="29776-144">policy_overrides</span></span> |<span data-ttu-id="29776-145">структура JSON, см. раздел **Переопределения политики** ниже</span><span class="sxs-lookup"><span data-stu-id="29776-145">JSON structure, see **Policy Overrides** below</span></span> |<span data-ttu-id="29776-146">Параметры политики для этой лицензии.</span><span class="sxs-lookup"><span data-stu-id="29776-146">Policy settings for this license.</span></span>  <span data-ttu-id="29776-147">В случае если этот ресурс имеет предопределенную политику, будут использоваться эти указанные значения.</span><span class="sxs-lookup"><span data-stu-id="29776-147">In the event this asset has a pre-defined policy, these specified values will be used.</span></span> |
| <span data-ttu-id="29776-148">session_init</span><span class="sxs-lookup"><span data-stu-id="29776-148">session_init</span></span> |<span data-ttu-id="29776-149">структура JSON, см. раздел **Инициализация сеанса** ниже</span><span class="sxs-lookup"><span data-stu-id="29776-149">JSON structure, see **Session Initialization** below</span></span> |<span data-ttu-id="29776-150">Необязательные данные, передаваемые в лицензию.</span><span class="sxs-lookup"><span data-stu-id="29776-150">Optional data passed to license.</span></span> |
| <span data-ttu-id="29776-151">parse_only</span><span class="sxs-lookup"><span data-stu-id="29776-151">parse_only</span></span> |<span data-ttu-id="29776-152">логическое</span><span class="sxs-lookup"><span data-stu-id="29776-152">boolean.</span></span> <span data-ttu-id="29776-153">Значение true или false</span><span class="sxs-lookup"><span data-stu-id="29776-153">true or false</span></span> |<span data-ttu-id="29776-154">Запрос на лицензию проанализирован, но лицензия не выдана.</span><span class="sxs-lookup"><span data-stu-id="29776-154">The license request is parsed but no license is issued.</span></span> <span data-ttu-id="29776-155">Однако в ответе возвращаются значения, формирующие запрос на лицензию.</span><span class="sxs-lookup"><span data-stu-id="29776-155">However, values form the license request are returned in the response.</span></span> |

## <a name="content-key-specs"></a><span data-ttu-id="29776-156">Спецификации ключей содержимого</span><span class="sxs-lookup"><span data-stu-id="29776-156">Content Key Specs</span></span>
<span data-ttu-id="29776-157">Если имеющаяся политика существует, указывать какие-либо значения в спецификации ключа содержимого не требуется.  Существующая политика, связанная с этим содержимым, будет использоваться для определения выходной защиты, например HDCP и CGMS.</span><span class="sxs-lookup"><span data-stu-id="29776-157">If a pre-existing policy exist, there is no need to specify any of the values in the Content Key Spec.  The pre-existing policy associated with this content will be used to determine the output protection such as HDCP and CGMS.</span></span>  <span data-ttu-id="29776-158">Если существующая политика не зарегистрирована на сервере лицензирования Widevine, поставщик содержимого может внедрить значения в запрос на лицензию.</span><span class="sxs-lookup"><span data-stu-id="29776-158">If a pre-existing policy is not registered with the Widevine License Server, the content provider can inject the values into the license request.</span></span>   

<span data-ttu-id="29776-159">Каждый параметр content_key_specs должен быть указан для всех записей независимо от параметра use_policy_overrides_exclusively.</span><span class="sxs-lookup"><span data-stu-id="29776-159">Each content_key_specs must be specified for all tracks, regardless of the option use_policy_overrides_exclusively.</span></span> 

| <span data-ttu-id="29776-160">Имя</span><span class="sxs-lookup"><span data-stu-id="29776-160">Name</span></span> | <span data-ttu-id="29776-161">Значение</span><span class="sxs-lookup"><span data-stu-id="29776-161">Value</span></span> | <span data-ttu-id="29776-162">Описание</span><span class="sxs-lookup"><span data-stu-id="29776-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="29776-163">content_key_specs.</span><span class="sxs-lookup"><span data-stu-id="29776-163">content_key_specs.</span></span> <span data-ttu-id="29776-164">track_type</span><span class="sxs-lookup"><span data-stu-id="29776-164">track_type</span></span> |<span data-ttu-id="29776-165">string</span><span class="sxs-lookup"><span data-stu-id="29776-165">string</span></span> |<span data-ttu-id="29776-166">Имя типа записи.</span><span class="sxs-lookup"><span data-stu-id="29776-166">A track type name.</span></span> <span data-ttu-id="29776-167">Если content_key_specs указан в запросе лицензии, убедитесь, что все типы записей указаны явным образом.</span><span class="sxs-lookup"><span data-stu-id="29776-167">If content_key_specs is specified in the license request, make sure to specify all track types explicitly.</span></span> <span data-ttu-id="29776-168">Невыполнение этого требования приведет к сбою воспроизведения последних 10 секунд.</span><span class="sxs-lookup"><span data-stu-id="29776-168">Failure to do so will result in failure to playback past 10 seconds.</span></span> |
| <span data-ttu-id="29776-169">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="29776-169">content_key_specs</span></span>  <br/> <span data-ttu-id="29776-170">security_level</span><span class="sxs-lookup"><span data-stu-id="29776-170">security_level</span></span> |<span data-ttu-id="29776-171">uint32</span><span class="sxs-lookup"><span data-stu-id="29776-171">uint32</span></span> |<span data-ttu-id="29776-172">Определяет требования к надежности клиента для воспроизведения.</span><span class="sxs-lookup"><span data-stu-id="29776-172">Defines client robustness requirements for playback.</span></span> <br/> <span data-ttu-id="29776-173">1. Требуется программное шифрование методом белого ящика.</span><span class="sxs-lookup"><span data-stu-id="29776-173">1 - Software-based whitebox crypto is required.</span></span> <br/> <span data-ttu-id="29776-174">2. Требуется шифрование ПО и скрытый декодер.</span><span class="sxs-lookup"><span data-stu-id="29776-174">2 - Software crypto and an obfuscated decoder is required.</span></span> <br/> <span data-ttu-id="29776-175">3. Материал ключа и операции шифрования должны быть выполнены в резервной доверенной среде выполнения оборудования.</span><span class="sxs-lookup"><span data-stu-id="29776-175">3 - The key material and crypto operations must be performed within a hardware backed trusted execution environment.</span></span> <br/> <span data-ttu-id="29776-176">4. Операции шифрования и расшифровки содержимого должны быть выполнены в резервной доверенной среде выполнения оборудования.</span><span class="sxs-lookup"><span data-stu-id="29776-176">4 - The crypto and decoding of content must be performed within a hardware backed trusted execution environment.</span></span>  <br/> <span data-ttu-id="29776-177">5. Шифрование, расшифровка и обработка всех носителей (сжатых и несжатых) должны быть выполнены в резервной доверенной среде выполнения оборудования.</span><span class="sxs-lookup"><span data-stu-id="29776-177">5 - The crypto, decoding and all handling of the media (compressed and uncompressed) must be handled within a hardware backed trusted execution environment.</span></span> |
| <span data-ttu-id="29776-178">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="29776-178">content_key_specs</span></span> <br/> <span data-ttu-id="29776-179">required_output_protection.hdc</span><span class="sxs-lookup"><span data-stu-id="29776-179">required_output_protection.hdc</span></span> |<span data-ttu-id="29776-180">строка — одна из: HDCP_NONE, HDCP_V1, HDCP_V2</span><span class="sxs-lookup"><span data-stu-id="29776-180">string - one of: HDCP_NONE, HDCP_V1, HDCP_V2</span></span> |<span data-ttu-id="29776-181">Указывает, требуется ли HDCP.</span><span class="sxs-lookup"><span data-stu-id="29776-181">Indicates whether HDCP is require</span></span> |
| <span data-ttu-id="29776-182">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="29776-182">content_key_specs</span></span> <br/><span data-ttu-id="29776-183">key</span><span class="sxs-lookup"><span data-stu-id="29776-183">key</span></span> |<span data-ttu-id="29776-184">строка в кодировке </span><span class="sxs-lookup"><span data-stu-id="29776-184">Base64</span></span> <br/><span data-ttu-id="29776-185">Base64</span><span class="sxs-lookup"><span data-stu-id="29776-185">encoded string</span></span> |<span data-ttu-id="29776-186">Ключ содержимого для этой записи. Если указано, требуется track_type или key_id.</span><span class="sxs-lookup"><span data-stu-id="29776-186">Content key to use for this track. If specified, the track_type or key_id is required.</span></span>  <span data-ttu-id="29776-187">Этот параметр позволяет поставщикам содержимого внедрить ключ содержимого для этой записи вместо того, чтобы сервер лицензирования Widevine создал или нашел ключ.</span><span class="sxs-lookup"><span data-stu-id="29776-187">This option allows the content provider to inject the content key for this track instead of letting Widevine license server generate or lookup a key.</span></span> |
| <span data-ttu-id="29776-188">content_key_specs.key_ID</span><span class="sxs-lookup"><span data-stu-id="29776-188">content_key_specs.key_id</span></span> |<span data-ttu-id="29776-189">Двоичные данные строки в кодировке Base64, 16 байт</span><span class="sxs-lookup"><span data-stu-id="29776-189">Base64 encoded string  binary, 16 bytes</span></span> |<span data-ttu-id="29776-190">Уникальный идентификатор ключа.</span><span class="sxs-lookup"><span data-stu-id="29776-190">Unique identifier for the key.</span></span> |

## <a name="policy-overrides"></a><span data-ttu-id="29776-191">Переопределения политики</span><span class="sxs-lookup"><span data-stu-id="29776-191">Policy Overrides</span></span>
| <span data-ttu-id="29776-192">Имя</span><span class="sxs-lookup"><span data-stu-id="29776-192">Name</span></span> | <span data-ttu-id="29776-193">Значение</span><span class="sxs-lookup"><span data-stu-id="29776-193">Value</span></span> | <span data-ttu-id="29776-194">Описание</span><span class="sxs-lookup"><span data-stu-id="29776-194">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="29776-195">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="29776-195">policy_overrides.</span></span> <span data-ttu-id="29776-196">can_play</span><span class="sxs-lookup"><span data-stu-id="29776-196">can_play</span></span> |<span data-ttu-id="29776-197">логическое</span><span class="sxs-lookup"><span data-stu-id="29776-197">boolean.</span></span> <span data-ttu-id="29776-198">Значение true или false</span><span class="sxs-lookup"><span data-stu-id="29776-198">true or false</span></span> |<span data-ttu-id="29776-199">Указывает, допускается ли воспроизведение содержимого.</span><span class="sxs-lookup"><span data-stu-id="29776-199">Indicates that playback of the content is allowed.</span></span> <span data-ttu-id="29776-200">Значение по умолчанию — false.</span><span class="sxs-lookup"><span data-stu-id="29776-200">Default is false.</span></span> |
| <span data-ttu-id="29776-201">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="29776-201">policy_overrides.</span></span> <span data-ttu-id="29776-202">can_persist</span><span class="sxs-lookup"><span data-stu-id="29776-202">can_persist</span></span> |<span data-ttu-id="29776-203">логическое</span><span class="sxs-lookup"><span data-stu-id="29776-203">boolean.</span></span> <span data-ttu-id="29776-204">Значение true или false</span><span class="sxs-lookup"><span data-stu-id="29776-204">true or false</span></span> |<span data-ttu-id="29776-205">Указывает, что лицензия может быть сохранена для долговременного хранения в целях автономного использования.</span><span class="sxs-lookup"><span data-stu-id="29776-205">Indicates that the license may be persisted to non-volatile storage for offline use.</span></span> <span data-ttu-id="29776-206">Значение по умолчанию — false.</span><span class="sxs-lookup"><span data-stu-id="29776-206">Default is false.</span></span> |
| <span data-ttu-id="29776-207">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="29776-207">policy_overrides.</span></span> <span data-ttu-id="29776-208">can_renew</span><span class="sxs-lookup"><span data-stu-id="29776-208">can_renew</span></span> |<span data-ttu-id="29776-209">логическое значение: true или false</span><span class="sxs-lookup"><span data-stu-id="29776-209">boolean true or false</span></span> |<span data-ttu-id="29776-210">Указывает, что разрешено продление лицензии.</span><span class="sxs-lookup"><span data-stu-id="29776-210">Indicates that renewal of this license is allowed.</span></span> <span data-ttu-id="29776-211">Если указано значение "true", лицензию можно расширить с помощью периодического сигнала.</span><span class="sxs-lookup"><span data-stu-id="29776-211">If true, the duration of the license can be extended by heartbeat.</span></span> <span data-ttu-id="29776-212">Значение по умолчанию — false.</span><span class="sxs-lookup"><span data-stu-id="29776-212">Default is false.</span></span> |
| <span data-ttu-id="29776-213">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="29776-213">policy_overrides.</span></span> <span data-ttu-id="29776-214">license_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="29776-214">license_duration_seconds</span></span> |<span data-ttu-id="29776-215">int64</span><span class="sxs-lookup"><span data-stu-id="29776-215">int64</span></span> |<span data-ttu-id="29776-216">Указывает интервал времени для данной конкретной лицензии.</span><span class="sxs-lookup"><span data-stu-id="29776-216">Indicates the time window for this specific license.</span></span> <span data-ttu-id="29776-217">Значение 0 указывает на неограниченное время.</span><span class="sxs-lookup"><span data-stu-id="29776-217">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="29776-218">Значение по умолчанию — 0.</span><span class="sxs-lookup"><span data-stu-id="29776-218">Default is 0.</span></span> |
| <span data-ttu-id="29776-219">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="29776-219">policy_overrides.</span></span> <span data-ttu-id="29776-220">rental_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="29776-220">rental_duration_seconds</span></span> |<span data-ttu-id="29776-221">int64</span><span class="sxs-lookup"><span data-stu-id="29776-221">int64</span></span> |<span data-ttu-id="29776-222">Указывает интервал времени, в течение которого разрешено воспроизведение.</span><span class="sxs-lookup"><span data-stu-id="29776-222">Indicates the time window while playback is permitted.</span></span> <span data-ttu-id="29776-223">Значение 0 указывает на неограниченное время.</span><span class="sxs-lookup"><span data-stu-id="29776-223">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="29776-224">Значение по умолчанию — 0.</span><span class="sxs-lookup"><span data-stu-id="29776-224">Default is 0.</span></span> |
| <span data-ttu-id="29776-225">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="29776-225">policy_overrides.</span></span> <span data-ttu-id="29776-226">playback_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="29776-226">playback_duration_seconds</span></span> |<span data-ttu-id="29776-227">int64</span><span class="sxs-lookup"><span data-stu-id="29776-227">int64</span></span> |<span data-ttu-id="29776-228">Окно просмотра времени после начала воспроизведения в течение срока действия лицензии.</span><span class="sxs-lookup"><span data-stu-id="29776-228">The viewing window of time once playback starts within the license duration.</span></span> <span data-ttu-id="29776-229">Значение 0 указывает на неограниченное время.</span><span class="sxs-lookup"><span data-stu-id="29776-229">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="29776-230">Значение по умолчанию — 0.</span><span class="sxs-lookup"><span data-stu-id="29776-230">Default is 0.</span></span> |
| <span data-ttu-id="29776-231">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="29776-231">policy_overrides.</span></span> <span data-ttu-id="29776-232">renewal_server_url</span><span class="sxs-lookup"><span data-stu-id="29776-232">renewal_server_url</span></span> |<span data-ttu-id="29776-233">string</span><span class="sxs-lookup"><span data-stu-id="29776-233">string</span></span> |<span data-ttu-id="29776-234">Все запросы на продление для этой лицензии должны направляться на указанный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="29776-234">All heartbeat (renewal) requests for this license shall be directed to the specified URL.</span></span> <span data-ttu-id="29776-235">Это поле используется только в том случае, если can_renew имеет значение "true".</span><span class="sxs-lookup"><span data-stu-id="29776-235">This field is only used if can_renew is true.</span></span> |
| <span data-ttu-id="29776-236">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="29776-236">policy_overrides.</span></span> <span data-ttu-id="29776-237">renewal_delay_seconds</span><span class="sxs-lookup"><span data-stu-id="29776-237">renewal_delay_seconds</span></span> |<span data-ttu-id="29776-238">int64</span><span class="sxs-lookup"><span data-stu-id="29776-238">int64</span></span> |<span data-ttu-id="29776-239">Количество секунд после license_start_time перед первой попыткой продления.</span><span class="sxs-lookup"><span data-stu-id="29776-239">How many seconds after license_start_time, before renewal is first attempted.</span></span> <span data-ttu-id="29776-240">Это поле используется только в том случае, если can_renew имеет значение "true".</span><span class="sxs-lookup"><span data-stu-id="29776-240">This field is only used if can_renew is true.</span></span> <span data-ttu-id="29776-241">Значение по умолчанию — 0.</span><span class="sxs-lookup"><span data-stu-id="29776-241">Default is 0</span></span> |
| <span data-ttu-id="29776-242">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="29776-242">policy_overrides.</span></span> <span data-ttu-id="29776-243">renewal_retry_interval_seconds</span><span class="sxs-lookup"><span data-stu-id="29776-243">renewal_retry_interval_seconds</span></span> |<span data-ttu-id="29776-244">int64</span><span class="sxs-lookup"><span data-stu-id="29776-244">int64</span></span> |<span data-ttu-id="29776-245">Определяет задержку в секундах между последующими запросами на продление лицензии (в случае сбоя).</span><span class="sxs-lookup"><span data-stu-id="29776-245">Specifies the delay in seconds between subsequent license renewal requests, in case of failure.</span></span> <span data-ttu-id="29776-246">Это поле используется только в том случае, если can_renew имеет значение "true".</span><span class="sxs-lookup"><span data-stu-id="29776-246">This field is only used if can_renew is true.</span></span> |
| <span data-ttu-id="29776-247">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="29776-247">policy_overrides.</span></span> <span data-ttu-id="29776-248">renewal_recovery_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="29776-248">renewal_recovery_duration_seconds</span></span> |<span data-ttu-id="29776-249">int64</span><span class="sxs-lookup"><span data-stu-id="29776-249">int64</span></span> |<span data-ttu-id="29776-250">Интервал времени, в течение которого разрешено продолжение воспроизведения во время попытки продления, если выполнение неудачно из-за внутренних проблем с сервером лицензирования.</span><span class="sxs-lookup"><span data-stu-id="29776-250">The window of time, in which playback is allowed to continue while renewal is attempted, yet unsuccessful due to backend problems with the license server.</span></span> <span data-ttu-id="29776-251">Значение 0 указывает на неограниченное время.</span><span class="sxs-lookup"><span data-stu-id="29776-251">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="29776-252">Это поле используется только в том случае, если can_renew имеет значение "true".</span><span class="sxs-lookup"><span data-stu-id="29776-252">This field is only used if can_renew is true.</span></span> |
| <span data-ttu-id="29776-253">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="29776-253">policy_overrides.</span></span> <span data-ttu-id="29776-254">renew_with_usage</span><span class="sxs-lookup"><span data-stu-id="29776-254">renew_with_usage</span></span> |<span data-ttu-id="29776-255">логическое значение: true или false</span><span class="sxs-lookup"><span data-stu-id="29776-255">boolean true or false</span></span> |<span data-ttu-id="29776-256">Указывает, что в начале использования лицензия должна быть отправлена для продления.</span><span class="sxs-lookup"><span data-stu-id="29776-256">Indicates that the license shall be sent for renewal when usage is started.</span></span> <span data-ttu-id="29776-257">Это поле используется только в том случае, если can_renew имеет значение "true".</span><span class="sxs-lookup"><span data-stu-id="29776-257">This field is only used if can_renew is true.</span></span> |

## <a name="session-initialization"></a><span data-ttu-id="29776-258">Инициализация сеанса</span><span class="sxs-lookup"><span data-stu-id="29776-258">Session Initialization</span></span>
| <span data-ttu-id="29776-259">Имя</span><span class="sxs-lookup"><span data-stu-id="29776-259">Name</span></span> | <span data-ttu-id="29776-260">Значение</span><span class="sxs-lookup"><span data-stu-id="29776-260">Value</span></span> | <span data-ttu-id="29776-261">Описание</span><span class="sxs-lookup"><span data-stu-id="29776-261">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="29776-262">provider_session_token</span><span class="sxs-lookup"><span data-stu-id="29776-262">provider_session_token</span></span> |<span data-ttu-id="29776-263">строка в кодировке Base64</span><span class="sxs-lookup"><span data-stu-id="29776-263">Base64 encoded string</span></span> |<span data-ttu-id="29776-264">Этот маркер сеанса передается обратно в лицензию и будет существовать в последующих продлениях.</span><span class="sxs-lookup"><span data-stu-id="29776-264">This session token is passed back in the license and will exist in subsequent renewals.</span></span>  <span data-ttu-id="29776-265">Маркер сеанса не сохраняется вне сеансов.</span><span class="sxs-lookup"><span data-stu-id="29776-265">The session token will not persist beyond sessions.</span></span> |
| <span data-ttu-id="29776-266">provider_client_token</span><span class="sxs-lookup"><span data-stu-id="29776-266">provider_client_token</span></span> |<span data-ttu-id="29776-267">строка в кодировке Base64</span><span class="sxs-lookup"><span data-stu-id="29776-267">Base64 encoded string</span></span> |<span data-ttu-id="29776-268">Маркер клиента для отправки обратно в ответе лицензии.</span><span class="sxs-lookup"><span data-stu-id="29776-268">Client token to send back in the license response.</span></span>  <span data-ttu-id="29776-269">Если запрос лицензии содержит маркер клиента, это значение игнорируется.</span><span class="sxs-lookup"><span data-stu-id="29776-269">If the license request contains a client token, this value is ignored.</span></span> <span data-ttu-id="29776-270">Маркер клиента будет сохраняться вне сеансов лицензии.</span><span class="sxs-lookup"><span data-stu-id="29776-270">The client token will persist beyond license sessions.</span></span> |
| <span data-ttu-id="29776-271">override_provider_client_token</span><span class="sxs-lookup"><span data-stu-id="29776-271">override_provider_client_token</span></span> |<span data-ttu-id="29776-272">логическое</span><span class="sxs-lookup"><span data-stu-id="29776-272">boolean.</span></span> <span data-ttu-id="29776-273">Значение true или false</span><span class="sxs-lookup"><span data-stu-id="29776-273">true or false</span></span> |<span data-ttu-id="29776-274">Если задано значение "false" и запрос лицензии содержит маркер клиента, используйте маркер из запроса, даже если в этой структуре был указан маркер клиента.</span><span class="sxs-lookup"><span data-stu-id="29776-274">If false and the license request contains a client token, use the token from the request even if a client token was specified in this structure.</span></span>  <span data-ttu-id="29776-275">Если задано значение "true", всегда используйте маркер, заданный в этой структуре.</span><span class="sxs-lookup"><span data-stu-id="29776-275">If true, always use the token specified in this structure.</span></span> |

## <a name="configure-your-widevine-licenses-using-net-types"></a><span data-ttu-id="29776-276">Настройка лицензий Widevine с помощью типов .NET</span><span class="sxs-lookup"><span data-stu-id="29776-276">Configure your Widevine licenses using .NET types</span></span>
<span data-ttu-id="29776-277">Службы мультимедиа предоставляют API-интерфейсы .NET, которые позволяют настраивать лицензии Widevine.</span><span class="sxs-lookup"><span data-stu-id="29776-277">Media Services provides .NET APIs that let you configure your Widevine licenses.</span></span> 

### <a name="classes-as-defined-in-the-media-services-net-sdk"></a><span data-ttu-id="29776-278">Классы, как определено в пакете SDK .NET для служб мультимедиа</span><span class="sxs-lookup"><span data-stu-id="29776-278">Classes as defined in the Media Services .NET SDK</span></span>
<span data-ttu-id="29776-279">Ниже приведены определения этих типов.</span><span class="sxs-lookup"><span data-stu-id="29776-279">The following are the definitions of these types.</span></span>

    public class WidevineMessage
    {
        public WidevineMessage();

        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public AllowedTrackTypes? allowed_track_types { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public ContentKeySpecs[] content_key_specs { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public object policy_overrides { get; set; }
    }

    [JsonConverter(typeof(StringEnumConverter))]
    public enum AllowedTrackTypes
    {
        SD_ONLY = 0,
        SD_HD = 1
    }
    public class ContentKeySpecs
    {
        public ContentKeySpecs();

        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public string key_id { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public RequiredOutputProtection required_output_protection { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public int? security_level { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public string track_type { get; set; }
    }

    public class RequiredOutputProtection
    {
        public RequiredOutputProtection();

        public Hdcp hdcp { get; set; }
    }

    [JsonConverter(typeof(StringEnumConverter))]
    public enum Hdcp
    {
        HDCP_NONE = 0,
        HDCP_V1 = 1,
        HDCP_V2 = 2
    }

### <a name="example"></a><span data-ttu-id="29776-280">Пример</span><span class="sxs-lookup"><span data-stu-id="29776-280">Example</span></span>
<span data-ttu-id="29776-281">В следующем примере показано, как использовать API-интерфейсы .NET для настройки простой лицензии Widevine.</span><span class="sxs-lookup"><span data-stu-id="29776-281">The following example shows how to use .NET APIs to configure  a simple Widevine license.</span></span>

    private static string ConfigureWidevineLicenseTemplate()
    {
        var template = new WidevineMessage
        {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                new ContentKeySpecs
                {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                    security_level = 1,
                    track_type = "SD"
                }
            },
            policy_overrides = new
            {
                can_play = true,
                can_persist = true,
                can_renew = false
            }
        };

        string configuration = JsonConvert.SerializeObject(template);
        return configuration;
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="29776-282">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="29776-282">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="29776-283">Отзывы</span><span class="sxs-lookup"><span data-stu-id="29776-283">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="29776-284">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="29776-284">See also</span></span>
[<span data-ttu-id="29776-285">Использование общего динамического шифрования PlayReady и (или) Widevine DRM</span><span class="sxs-lookup"><span data-stu-id="29776-285">Using PlayReady and/or Widevine Dynamic Common Encryption</span></span>](media-services-protect-with-drm.md)

