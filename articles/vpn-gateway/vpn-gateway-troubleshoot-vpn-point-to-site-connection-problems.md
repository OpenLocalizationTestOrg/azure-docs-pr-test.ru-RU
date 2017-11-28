---
title: "проблем при подключении к Azure точки сайтами aaaTroubleshoot | Документы Microsoft"
description: "Узнайте, как tootroubleshoot проблем при подключении точки сайтами."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: genli
ms.openlocfilehash: 98d66074be62ad8c7153a903f69cb0d01f988cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a><span data-ttu-id="4cf5d-103">Устранение неполадок подключения типа "точка — сеть" Azure</span><span class="sxs-lookup"><span data-stu-id="4cf5d-103">Troubleshooting: Azure point-to-site connection problems</span></span>

<span data-ttu-id="4cf5d-104">В этой статье перечисляются распространенные проблемы подключения типа "точка — сеть", которые могут возникнуть.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-104">This article lists common point-to-site connection problems that you might experience.</span></span> <span data-ttu-id="4cf5d-105">Кроме того, здесь рассматриваются возможные причины этих проблем и способы их устранения.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-105">It also discusses possible causes and solutions for these problems.</span></span>

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a><span data-ttu-id="4cf5d-106">Ошибка VPN-клиента: не удалось найти сертификат</span><span class="sxs-lookup"><span data-stu-id="4cf5d-106">VPN client error: A certificate could not be found</span></span>

### <a name="symptom"></a><span data-ttu-id="4cf5d-107">Симптом</span><span class="sxs-lookup"><span data-stu-id="4cf5d-107">Symptom</span></span>

<span data-ttu-id="4cf5d-108">При попытке tooconnect tooan виртуальная сеть Azure с помощью VPN-клиента hello появляется hello следующие сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="4cf5d-108">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="4cf5d-109">**Не удалось найти сертификат, который был бы использован с протоколом расширенной проверки подлинности (EAP). (Ошибка 798.)**</span><span class="sxs-lookup"><span data-stu-id="4cf5d-109">**A certificate could not be found that can be used with this Extensible Authentication Protocol. (Error 798)**</span></span>

### <a name="cause"></a><span data-ttu-id="4cf5d-110">Причина:</span><span class="sxs-lookup"><span data-stu-id="4cf5d-110">Cause</span></span>

<span data-ttu-id="4cf5d-111">Эта проблема возникает, если отсутствует сертификат клиента hello **Сертификаты — текущий пользователь\личные\сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-111">This problem occurs if hello client certificate is missing from **Certificates - Current User\Personal\Certificates**.</span></span>

### <a name="solution"></a><span data-ttu-id="4cf5d-112">Решение</span><span class="sxs-lookup"><span data-stu-id="4cf5d-112">Solution</span></span>

<span data-ttu-id="4cf5d-113">Убедитесь, что этот сертификат клиента hello установлен в расположение хранилища сертификатов hello (Certmgr.msc) после hello:</span><span class="sxs-lookup"><span data-stu-id="4cf5d-113">Make sure that hello client certificate is installed in hello following location of hello Certificates store (Certmgr.msc):</span></span>
 
<span data-ttu-id="4cf5d-114">**Certificates - Current User\Personal\Certificates**</span><span class="sxs-lookup"><span data-stu-id="4cf5d-114">**Certificates - Current User\Personal\Certificates**</span></span>

<span data-ttu-id="4cf5d-115">Дополнительные сведения о как tooinstall hello сертификата клиента см. в разделе [Создание и экспорт сертификатов для соединений точка сеть](vpn-gateway-certificates-point-to-site.md).</span><span class="sxs-lookup"><span data-stu-id="4cf5d-115">For more information about how tooinstall hello client certificate, see [Generate and export certificates for point-to-site connections](vpn-gateway-certificates-point-to-site.md).</span></span>

> [!NOTE]
> <span data-ttu-id="4cf5d-116">При импорте hello сертификат клиента, не устанавливайте hello **Включить усиленную защиту закрытого ключа** параметр.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-116">When you import hello client certificate, do not select hello **Enable strong private key protection** option.</span></span>

## <a name="vpn-client-error-hello-message-received-was-unexpected-or-badly-formatted"></a><span data-ttu-id="4cf5d-117">Ошибка клиента VPN: получено сообщение hello был неверным или оно имеет неправильный формат</span><span class="sxs-lookup"><span data-stu-id="4cf5d-117">VPN client error: hello message received was unexpected or badly formatted</span></span>

### <a name="symptom"></a><span data-ttu-id="4cf5d-118">Симптом</span><span class="sxs-lookup"><span data-stu-id="4cf5d-118">Symptom</span></span>

<span data-ttu-id="4cf5d-119">При попытке tooconnect tooan виртуальная сеть Azure с помощью VPN-клиента hello появляется hello следующие сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="4cf5d-119">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="4cf5d-120">**Полученное сообщение Hello был неверным или оно имеет неправильный формат. (Ошибка 0x80090326.)**</span><span class="sxs-lookup"><span data-stu-id="4cf5d-120">**hello message received was unexpected or badly formatted. (Error 0x80090326)**</span></span>

### <a name="cause"></a><span data-ttu-id="4cf5d-121">Причина:</span><span class="sxs-lookup"><span data-stu-id="4cf5d-121">Cause</span></span>

<span data-ttu-id="4cf5d-122">Эта проблема возникает, если hello корневого сертификата открытый ключ не был загружен на шлюз Azure VPN hello.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-122">This problem occurs if hello root certificate public key is not uploaded into hello Azure VPN gateway.</span></span> <span data-ttu-id="4cf5d-123">Он также может возникать, если ключ hello повреждена или истек срок действия.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-123">It can also occur if hello key is corrupted or expired.</span></span>

### <a name="solution"></a><span data-ttu-id="4cf5d-124">Решение</span><span class="sxs-lookup"><span data-stu-id="4cf5d-124">Solution</span></span>

<span data-ttu-id="4cf5d-125">tooresolve эту проблему, проверьте состояние hello hello корневого сертификата в hello Azure портала toosee ли он отозван.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-125">tooresolve this problem, check hello status of hello root certificate in hello Azure portal toosee whether it was revoked.</span></span> <span data-ttu-id="4cf5d-126">Если он не был отозван, попробуйте toodelete hello корневой сертификат и reupload.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-126">If it is not revoked, try toodelete hello root certificate and reupload.</span></span> <span data-ttu-id="4cf5d-127">Дополнительные сведения см. в разделе [Создание сертификатов](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span><span class="sxs-lookup"><span data-stu-id="4cf5d-127">For more information, see [Create certificates](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span></span>

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a><span data-ttu-id="4cf5d-128">Ошибка VPN-клиента: цепочка сертификатов обработана, но обработка прервана</span><span class="sxs-lookup"><span data-stu-id="4cf5d-128">VPN client error: A certificate chain processed but terminated</span></span> 

### <a name="symptom"></a><span data-ttu-id="4cf5d-129">Симптом</span><span class="sxs-lookup"><span data-stu-id="4cf5d-129">Symptom</span></span> 

<span data-ttu-id="4cf5d-130">При попытке tooconnect tooan виртуальная сеть Azure с помощью VPN-клиента hello появляется hello следующие сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="4cf5d-130">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="4cf5d-131">**Цепочка сертификатов обработана, но обработка прервана на корневом сертификате, который не доверяет поставщик доверия hello.**</span><span class="sxs-lookup"><span data-stu-id="4cf5d-131">**A certificate chain processed but terminated in a root certificate which is not trusted by hello trust provider.**</span></span>

### <a name="solution"></a><span data-ttu-id="4cf5d-132">Решение</span><span class="sxs-lookup"><span data-stu-id="4cf5d-132">Solution</span></span>

1. <span data-ttu-id="4cf5d-133">Убедитесь что hello следующие сертификаты в правильном расположении hello.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-133">Make sure that hello following certificates are in hello correct location:</span></span>

    | <span data-ttu-id="4cf5d-134">Сертификат</span><span class="sxs-lookup"><span data-stu-id="4cf5d-134">Certificate</span></span> | <span data-ttu-id="4cf5d-135">Расположение</span><span class="sxs-lookup"><span data-stu-id="4cf5d-135">Location</span></span> |
    | ------------- | ------------- |
    | <span data-ttu-id="4cf5d-136">AzureClient.pfx</span><span class="sxs-lookup"><span data-stu-id="4cf5d-136">AzureClient.pfx</span></span>  | <span data-ttu-id="4cf5d-137">Current User\Personal\Certificates</span><span class="sxs-lookup"><span data-stu-id="4cf5d-137">Current User\Personal\Certificates</span></span> |
    | <span data-ttu-id="4cf5d-138">Azuregateway-*GUID*.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="4cf5d-138">Azuregateway-*GUID*.cloudapp.net</span></span>  | <span data-ttu-id="4cf5d-139">Current User\Trusted Root Certification Authorities</span><span class="sxs-lookup"><span data-stu-id="4cf5d-139">Current User\Trusted Root Certification Authorities</span></span>|
    | <span data-ttu-id="4cf5d-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span><span class="sxs-lookup"><span data-stu-id="4cf5d-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span></span>    | <span data-ttu-id="4cf5d-141">Local Computer\Trusted Root Certification Authorities</span><span class="sxs-lookup"><span data-stu-id="4cf5d-141">Local Computer\Trusted Root Certification Authorities</span></span>|

2. <span data-ttu-id="4cf5d-142">Hello сертификаты, в расположении hello, попробуйте toodelete hello сертификаты и установите их заново.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-142">If hello certificates are already in hello location, try toodelete hello certificates and reinstall them.</span></span> <span data-ttu-id="4cf5d-143">Hello  **azuregateway -*GUID*. cloudapp.net** сертификат находится в пакет конфигурации клиента VPN hello, загруженный с портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-143">hello **azuregateway-*GUID*.cloudapp.net** certificate is in hello VPN client configuration package that you downloaded from hello Azure portal.</span></span> <span data-ttu-id="4cf5d-144">Можно использовать файл archivers tooextract hello файлы из пакета hello.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-144">You can use file archivers tooextract hello files from hello package.</span></span>

## <a name="file-download-error-target-uri-is-not-specified"></a><span data-ttu-id="4cf5d-145">Произошла ошибка скачивания файла. Целевой URI не указан</span><span class="sxs-lookup"><span data-stu-id="4cf5d-145">File download error: Target URI is not specified</span></span>

### <a name="symptom"></a><span data-ttu-id="4cf5d-146">Симптом</span><span class="sxs-lookup"><span data-stu-id="4cf5d-146">Symptom</span></span>

<span data-ttu-id="4cf5d-147">Появляется сообщение об ошибке после hello:</span><span class="sxs-lookup"><span data-stu-id="4cf5d-147">You receive hello following error message:</span></span>

<span data-ttu-id="4cf5d-148">**Ошибка скачивания файла. Не указан целевой URI.**</span><span class="sxs-lookup"><span data-stu-id="4cf5d-148">**File download error. Target URI is not specified.**</span></span>

### <a name="cause"></a><span data-ttu-id="4cf5d-149">Причина:</span><span class="sxs-lookup"><span data-stu-id="4cf5d-149">Cause</span></span> 

<span data-ttu-id="4cf5d-150">Эта проблема возникает из-за неправильного типа шлюза.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-150">This problem occurs because of an incorrect gateway type.</span></span> 

### <a name="solution"></a><span data-ttu-id="4cf5d-151">Решение</span><span class="sxs-lookup"><span data-stu-id="4cf5d-151">Solution</span></span>

<span data-ttu-id="4cf5d-152">должен быть тип шлюза VPN Hello **VPN**, и должен быть тип VPN hello **routebased**.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-152">hello VPN gateway type must be **VPN**, and hello VPN type must be **RouteBased**.</span></span>

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a><span data-ttu-id="4cf5d-153">Ошибка VPN-клиента: сбой настраиваемого сценария VPN Azure</span><span class="sxs-lookup"><span data-stu-id="4cf5d-153">VPN client error: Azure VPN custom script failed</span></span> 

### <a name="symptom"></a><span data-ttu-id="4cf5d-154">Симптом</span><span class="sxs-lookup"><span data-stu-id="4cf5d-154">Symptom</span></span>

<span data-ttu-id="4cf5d-155">При попытке tooconnect tooan виртуальная сеть Azure с помощью VPN-клиента hello появляется hello следующие сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="4cf5d-155">When you try tooconnect tooan Azure virtual network by using hello VPN client, you receive hello following error message:</span></span>

<span data-ttu-id="4cf5d-156">**Пользовательский сценарий (tooupdate маршрут таблица) не удалось. (Error 8007026f)** (Произошел сбой настраиваемого сценария (для обновления таблицы маршрутизации). (Ошибка 8007026f)).</span><span class="sxs-lookup"><span data-stu-id="4cf5d-156">**Custom script (tooupdate your routing table) failed. (Error 8007026f)**</span></span>

### <a name="cause"></a><span data-ttu-id="4cf5d-157">Причина:</span><span class="sxs-lookup"><span data-stu-id="4cf5d-157">Cause</span></span>

<span data-ttu-id="4cf5d-158">Эта проблема может возникнуть, если вы пытаетесь tooopen hello сайта в точке VPN-подключение с помощью ярлыка.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-158">This problem might occur if you are trying tooopen hello site-to-point VPN connection by using a shortcut.</span></span>

### <a name="solution"></a><span data-ttu-id="4cf5d-159">Решение</span><span class="sxs-lookup"><span data-stu-id="4cf5d-159">Solution</span></span> 

<span data-ttu-id="4cf5d-160">Откройте пакет VPN hello напрямую, вместо открытия его с помощью ярлыка hello.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-160">Open hello VPN package directly instead of opening it from hello shortcut.</span></span>

## <a name="cannot-install-hello-vpn-client"></a><span data-ttu-id="4cf5d-161">Не удается установить VPN-клиента hello</span><span class="sxs-lookup"><span data-stu-id="4cf5d-161">Cannot install hello VPN client</span></span>

### <a name="cause"></a><span data-ttu-id="4cf5d-162">Причина:</span><span class="sxs-lookup"><span data-stu-id="4cf5d-162">Cause</span></span> 

<span data-ttu-id="4cf5d-163">Дополнительный сертификат является обязательным tootrust hello VPN-шлюз для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-163">An additional certificate is required tootrust hello VPN gateway for your virtual network.</span></span> <span data-ttu-id="4cf5d-164">Hello сертификат включается в пакет конфигурации клиента VPN hello, созданный из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-164">hello certificate is included in hello VPN client configuration package that is generated from hello Azure portal.</span></span>

### <a name="solution"></a><span data-ttu-id="4cf5d-165">Решение</span><span class="sxs-lookup"><span data-stu-id="4cf5d-165">Solution</span></span>

<span data-ttu-id="4cf5d-166">Извлеките пакет конфигурации VPN-клиента hello и найти hello CER-файл.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-166">Extract hello VPN client configuration package, and find hello .cer file.</span></span> <span data-ttu-id="4cf5d-167">tooinstall hello сертификатов, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="4cf5d-167">tooinstall hello certificate, follow these steps:</span></span>

1. <span data-ttu-id="4cf5d-168">Запустите mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-168">Open mmc.exe.</span></span>
2. <span data-ttu-id="4cf5d-169">Добавить hello **сертификаты** оснастки.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-169">Add hello **Certificates** snap-in.</span></span>
3. <span data-ttu-id="4cf5d-170">Выберите hello **компьютера** учетной записи для hello локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-170">Select hello **Computer** account for hello local computer.</span></span>
4. <span data-ttu-id="4cf5d-171">Щелкните правой кнопкой мыши hello **доверенные корневые центры сертификации** узла.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-171">Right-click hello **Trusted Root Certification Authorities** node.</span></span> <span data-ttu-id="4cf5d-172">Нажмите кнопку **все задачи** > **импорта**и обзор toohello CER-файл, извлеченный из пакета конфигурации клиента VPN hello.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-172">Click **All-Task** > **Import**, and browse toohello .cer file you extracted from hello VPN client configuration package.</span></span>
5. <span data-ttu-id="4cf5d-173">Перезагрузите компьютер hello.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-173">Restart hello computer.</span></span> 
6. <span data-ttu-id="4cf5d-174">Попробуйте tooinstall hello VPN-клиента.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-174">Try tooinstall hello VPN client.</span></span>

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-data-is-invalid"></a><span data-ttu-id="4cf5d-175">Azure портала ошибка: не удалось выполнить toosave hello VPN-шлюз и hello данные являются недопустимыми</span><span class="sxs-lookup"><span data-stu-id="4cf5d-175">Azure portal error: Failed toosave hello VPN gateway, and hello data is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="4cf5d-176">Симптом</span><span class="sxs-lookup"><span data-stu-id="4cf5d-176">Symptom</span></span>

<span data-ttu-id="4cf5d-177">При попытке изменения hello toosave для шлюза VPN hello в hello портал Azure, появляется сообщение об ошибке после hello:</span><span class="sxs-lookup"><span data-stu-id="4cf5d-177">When you try toosave hello changes for hello VPN gateway in hello Azure portal, you receive hello following error message:</span></span>

<span data-ttu-id="4cf5d-178">**Шлюз виртуальной сети не удалось toosave &lt;* имя шлюза*&gt;.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-178">**Failed toosave virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="4cf5d-179">Недействительные данные для сертификата &lt;*идентификатор сертификата*&gt;**.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-179">Data for certificate &lt;*certificate ID*&gt; is invalid.**</span></span>

### <a name="cause"></a><span data-ttu-id="4cf5d-180">Причина:</span><span class="sxs-lookup"><span data-stu-id="4cf5d-180">Cause</span></span> 

<span data-ttu-id="4cf5d-181">Эта проблема может возникнуть, если hello корневого сертификата открытый ключ, который вы отправили содержит недопустимый символ, например пробел.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-181">This problem might occur if hello root certificate public key that you uploaded contains an invalid character, such as a space.</span></span>

### <a name="solution"></a><span data-ttu-id="4cf5d-182">Решение</span><span class="sxs-lookup"><span data-stu-id="4cf5d-182">Solution</span></span>

<span data-ttu-id="4cf5d-183">Убедитесь, что данные hello в сертификате hello не содержит недопустимые символы, такие как разрывы строки (возврат каретки).</span><span class="sxs-lookup"><span data-stu-id="4cf5d-183">Make sure that hello data in hello certificate does not contain invalid characters, such as line breaks (carriage returns).</span></span> <span data-ttu-id="4cf5d-184">Hello всего должно содержать одну строку.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-184">hello entire value should be one long line.</span></span> <span data-ttu-id="4cf5d-185">После текста Hello приведен образец hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-185">hello following text is a sample of hello certificate:</span></span>

    -----BEGIN CERTIFICATE-----
    MIIC5zCCAc+gAwIBAgIQFSwsLuUrCIdHwI3hzJbdBjANBgkqhkiG9w0BAQsFADAW
    MRQwEgYDVQQDDAtQMlNSb290Q2VydDAeFw0xNzA2MTUwMjU4NDZaFw0xODA2MTUw
    MzE4NDZaMBYxFDASBgNVBAMMC1AyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEF
    AAOCAQ8AMIIBCgKCAQEAz8QUCWCxxxTrxF5yc5uUpL/bzwC5zZ804ltB1NpPa/PI
    sa5uwLw/YFb8XG/JCWxUJpUzS/kHUKFluqkY80U+fAmRmTEMq5wcaMhp3wRfeq+1
    G9OPBNTyqpnHe+i54QAnj1DjsHXXNL4AL1N8/TSzYTm7dkiq+EAIyRRMrZlYwije
    407ChxIp0stB84MtMShhyoSm2hgl+3zfwuaGXoJQwWiXh715kMHVTSj9zFechYd7
    5OLltoRRDyyxsf0qweTFKIgFj13Hn/bq/UJG3AcyQNvlCv1HwQnXO+hckVBB29wE
    sF8QSYk2MMGimPDYYt4ZM5tmYLxxxvGmrGhc+HWXzMeQIDAQABozEwLzAOBgNVHQ8B
    Af8EBAMCAgQwHQYDVR0OBBYEFBE9zZWhQftVLBQNATC/LHLvMb0OMA0GCSqGSIb3
    DQEBCwUAA4IBAQB7k0ySFUQu72sfj3BdNxrXSyOT4L2rADLhxxxiK0U6gHUF6eWz
    /0h6y4mNkg3NgLT3j/WclqzHXZruhWAXSF+VbAGkwcKA99xGWOcUJ+vKVYL/kDja
    gaZrxHlhTYVVmwn4F7DWhteFqhzZ89/W9Mv6p180AimF96qDU8Ez8t860HQaFkU6
    2Nw9ZMsGkvLePZZi78yVBDCWMogBMhrRVXG/xQkBajgvL5syLwFBo2kWGdC+wyWY
    U/Z+EK9UuHnn3Hkq/vXEzRVsYuaxchta0X2UNRzRq+o706l+iyLTpe6fnvW6ilOi
    e8Jcej7mzunzyjz4chN0/WVF94MtxbUkLkqP
    -----END CERTIFICATE-----

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-resource-name-is-invalid"></a><span data-ttu-id="4cf5d-186">Azure портала ошибка: не удалось выполнить toosave hello VPN-шлюз и недопустимое имя ресурса hello</span><span class="sxs-lookup"><span data-stu-id="4cf5d-186">Azure portal error: Failed toosave hello VPN gateway, and hello resource name is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="4cf5d-187">Симптом</span><span class="sxs-lookup"><span data-stu-id="4cf5d-187">Symptom</span></span>

<span data-ttu-id="4cf5d-188">При попытке изменения hello toosave для шлюза VPN hello в hello портал Azure, появляется сообщение об ошибке после hello:</span><span class="sxs-lookup"><span data-stu-id="4cf5d-188">When you try toosave hello changes for hello VPN gateway in hello Azure portal, you receive hello following error message:</span></span> 

<span data-ttu-id="4cf5d-189">**Шлюз виртуальной сети не удалось toosave &lt;* имя шлюза*&gt;.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-189">**Failed toosave virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="4cf5d-190">Имя ресурса &lt; *имя сертификата, попробуйте tooupload* &gt; является недопустимым **.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-190">Resource name &lt;*certificate name you try tooupload*&gt; is invalid**.</span></span>

### <a name="cause"></a><span data-ttu-id="4cf5d-191">Причина:</span><span class="sxs-lookup"><span data-stu-id="4cf5d-191">Cause</span></span>

<span data-ttu-id="4cf5d-192">Эта проблема возникает, поскольку имя hello hello сертификата содержит недопустимый символ, например пробел.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-192">This problem occurs because hello name of hello certificate contains an invalid character, such as a space.</span></span> 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a><span data-ttu-id="4cf5d-193">Ошибка портала Azure: ошибка 503 при скачивании файла пакета VPN</span><span class="sxs-lookup"><span data-stu-id="4cf5d-193">Azure portal error: VPN package file download error 503</span></span>

### <a name="symptom"></a><span data-ttu-id="4cf5d-194">Симптом</span><span class="sxs-lookup"><span data-stu-id="4cf5d-194">Symptom</span></span>

<span data-ttu-id="4cf5d-195">При запуске пакета конфигурации клиента VPN toodownload hello, появляется сообщение об ошибке после hello:</span><span class="sxs-lookup"><span data-stu-id="4cf5d-195">When you try toodownload hello VPN client configuration package, you receive hello following error message:</span></span>

<span data-ttu-id="4cf5d-196">**Не удалось выполнить файл toodownload hello. Сведения об ошибке: ошибки 503. Hello сервер занят.**</span><span class="sxs-lookup"><span data-stu-id="4cf5d-196">**Failed toodownload hello file. Error details: error 503. hello server is busy.**</span></span>
 
### <a name="solution"></a><span data-ttu-id="4cf5d-197">Решение</span><span class="sxs-lookup"><span data-stu-id="4cf5d-197">Solution</span></span>

<span data-ttu-id="4cf5d-198">Эта ошибка может быть вызвана временным сбоем сети.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-198">This error can be caused by a temporary network problem.</span></span> <span data-ttu-id="4cf5d-199">Пакет VPN toodownload hello, повторите попытку через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-199">Try toodownload hello VPN package again after a few minutes.</span></span>

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-tooconnect"></a><span data-ttu-id="4cf5d-200">Обновление VPN-шлюз Azure: P2S все клиенты, не удается tooconnect</span><span class="sxs-lookup"><span data-stu-id="4cf5d-200">Azure VPN Gateway upgrade: All P2S clients are unable tooconnect</span></span>

### <a name="cause"></a><span data-ttu-id="4cf5d-201">Причина:</span><span class="sxs-lookup"><span data-stu-id="4cf5d-201">Cause</span></span>

<span data-ttu-id="4cf5d-202">Если сертификат hello более 50 процентов через своего времени существования, будут перезаписаны hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-202">If hello certificate is more than 50 percent through its lifetime, hello certificate is rolled over.</span></span>

### <a name="solution"></a><span data-ttu-id="4cf5d-203">Решение</span><span class="sxs-lookup"><span data-stu-id="4cf5d-203">Solution</span></span>

<span data-ttu-id="4cf5d-204">tooresolve эту проблему, создавать и распространять новые сертификаты toohello VPN-клиентов.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-204">tooresolve this problem, create and redistribute new certificates toohello VPN clients.</span></span> 

## <a name="too-many-vpn-clients-connected-at-once"></a><span data-ttu-id="4cf5d-205">Слишком много одновременно подключенных VPN-клиентов</span><span class="sxs-lookup"><span data-stu-id="4cf5d-205">Too many VPN clients connected at once</span></span>

<span data-ttu-id="4cf5d-206">Для каждого шлюза VPN hello максимальное число разрешенных подключений — 128.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-206">For each VPN gateway, hello maximum number of allowable connections is 128.</span></span> <span data-ttu-id="4cf5d-207">Вы увидите hello общее количество подключенных клиентов в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-207">You can see hello total number of connected clients in hello Azure portal.</span></span>

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-toohello-route-table"></a><span data-ttu-id="4cf5d-208">Точка сеть VPN неправильно добавляет маршрут для таблицы маршрутов toohello 10.0.0.0/8</span><span class="sxs-lookup"><span data-stu-id="4cf5d-208">Point-to-site VPN incorrectly adds a route for 10.0.0.0/8 toohello route table</span></span>

### <a name="symptom"></a><span data-ttu-id="4cf5d-209">Симптом</span><span class="sxs-lookup"><span data-stu-id="4cf5d-209">Symptom</span></span>

<span data-ttu-id="4cf5d-210">При наборе hello VPN-подключения на клиенте точки сайтами hello hello VPN-клиента следует добавить маршрут к hello виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-210">When you dial hello VPN connection on hello point-to-site client, hello VPN client should add a route toward hello Azure virtual network.</span></span> <span data-ttu-id="4cf5d-211">Служба модуля поддержки IP Hello следует добавить маршрут для подсети hello hello VPN-клиентов.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-211">hello IP helper service should add a route for hello subnet of hello VPN clients.</span></span> 

<span data-ttu-id="4cf5d-212">Hello диапазон клиентов VPN принадлежит меньшее подсети 10.0.0.0/8, например 10.0.12.0/24 tooa.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-212">hello VPN client range belongs tooa smaller subnet of 10.0.0.0/8, such as 10.0.12.0/24.</span></span> <span data-ttu-id="4cf5d-213">Вместо маршрута для 10.0.12.0/24 добавляется маршрут для 10.0.0.0/8, который имеет более высокий приоритет.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-213">Instead of a route for 10.0.12.0/24, a route for 10.0.0.0/8 is added that has higher priority.</span></span> 

<span data-ttu-id="4cf5d-214">Этот маршрут неверные разрывает связь с других локальных сетях может принадлежать tooanother подсети в пределах диапазона 10.0.0.0/8 hello, такие как 10.50.0.0/24, у которых нет определенных конкретного маршрута.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-214">This incorrect route breaks connectivity with other on-premises networks that might belong tooanother subnet within hello 10.0.0.0/8 range, such as 10.50.0.0/24, that don't have a specific route defined.</span></span> 

### <a name="cause"></a><span data-ttu-id="4cf5d-215">Причина:</span><span class="sxs-lookup"><span data-stu-id="4cf5d-215">Cause</span></span>

<span data-ttu-id="4cf5d-216">Это сделано намеренно для клиентов Windows.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-216">This behavior is by design for Windows clients.</span></span> <span data-ttu-id="4cf5d-217">Когда клиент hello использует протокол PPP IPCP hello, он получает hello IP-адрес интерфейса туннеля hello сервере hello (шлюз VPN hello в данном случае).</span><span class="sxs-lookup"><span data-stu-id="4cf5d-217">When hello client uses hello PPP IPCP protocol, it obtains hello IP address for hello tunnel interface from hello server (hello VPN gateway in this case).</span></span> <span data-ttu-id="4cf5d-218">Однако из-за ограничений в протокол hello, hello клиента нет hello маску подсети.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-218">However, because of a limitation in hello protocol, hello client does not have hello subnet mask.</span></span> <span data-ttu-id="4cf5d-219">Так как нет других tooget способом, клиент hello предпринимается на основе класса hello hello туннельный интерфейс IP-адреса, маски подсети hello tooguess.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-219">Because there is no other way tooget it, hello client tries tooguess hello subnet mask based on hello class of hello tunnel interface IP address.</span></span> 

<span data-ttu-id="4cf5d-220">Таким образом маршрут добавляется основании hello после статического сопоставления:</span><span class="sxs-lookup"><span data-stu-id="4cf5d-220">Therefore, a route is added based on hello following static mapping:</span></span> 

<span data-ttu-id="4cf5d-221">Если адрес принадлежит tooclass A--> Применить/8 больше</span><span class="sxs-lookup"><span data-stu-id="4cf5d-221">If address belongs tooclass A --> apply /8</span></span>

<span data-ttu-id="4cf5d-222">Если адрес относится tooclass--> B применить /16</span><span class="sxs-lookup"><span data-stu-id="4cf5d-222">If address belongs tooclass B --> apply /16</span></span>

<span data-ttu-id="4cf5d-223">Если адрес относится C--> tooclass применить /24</span><span class="sxs-lookup"><span data-stu-id="4cf5d-223">If address belongs tooclass C --> apply /24</span></span>

## <a name="vpn-client-cannot-access-network-file-shares"></a><span data-ttu-id="4cf5d-224">VPN-клиент не может получить доступ к сетевым файловым ресурсам</span><span class="sxs-lookup"><span data-stu-id="4cf5d-224">VPN client cannot access network file shares</span></span>

### <a name="symptom"></a><span data-ttu-id="4cf5d-225">Симптом</span><span class="sxs-lookup"><span data-stu-id="4cf5d-225">Symptom</span></span>

<span data-ttu-id="4cf5d-226">Виртуальная сеть Azure toohello подключен клиент VPN Hello.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-226">hello VPN client has connected toohello Azure virtual network.</span></span> <span data-ttu-id="4cf5d-227">Однако hello клиента нет доступа к сетевым папкам.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-227">However, hello client cannot access network shares.</span></span>

### <a name="cause"></a><span data-ttu-id="4cf5d-228">Причина:</span><span class="sxs-lookup"><span data-stu-id="4cf5d-228">Cause</span></span>

<span data-ttu-id="4cf5d-229">Hello протокол SMB используется для общий доступ к файлам.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-229">hello SMB protocol is used for file share access.</span></span> <span data-ttu-id="4cf5d-230">При инициации подключения hello hello VPN-клиент добавляет учетные данные сеанса hello и происходит сбой hello.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-230">When hello connection is initiated, hello VPN client adds hello session credentials and hello failure occurs.</span></span> <span data-ttu-id="4cf5d-231">После установления соединения hello hello клиента принудительного toouse hello кэширование учетных данных для проверки подлинности Kerberos.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-231">After hello connection is established, hello client is forced toouse hello cache credentials for Kerberos authentication.</span></span> <span data-ttu-id="4cf5d-232">Этот процесс инициирует запросы toohello центр распространения ключей (контроллер домена) tooget маркер.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-232">This process initiates queries toohello Key Distribution Center (a domain controller) tooget a token.</span></span> <span data-ttu-id="4cf5d-233">Так как из Интернета hello подключается клиент hello, может оказаться контроллер домена может tooreach hello.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-233">Because hello client connects from hello Internet, it might not be able tooreach hello domain controller.</span></span> <span data-ttu-id="4cf5d-234">Таким образом клиент hello не может перенести нагрузку с Kerberos tooNTLM.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-234">Therefore, hello client cannot fail over from Kerberos tooNTLM.</span></span> 

<span data-ttu-id="4cf5d-235">Hello только время, этот клиент hello предлагается для учетных данных — когда в ней имеется действительный сертификат (с использованием SAN = имя участника-пользователя) выдан hello toowhich домена, он присоединен.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-235">hello only time that hello client is prompted for a credential is when it has a valid certificate (with SAN=UPN) issued by hello domain toowhich it is joined.</span></span> <span data-ttu-id="4cf5d-236">Hello клиент также должен быть физически подключен toohello доменной сети.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-236">hello client also must be physically connected toohello domain network.</span></span> <span data-ttu-id="4cf5d-237">В этом случае клиент hello пытается toouse hello сертификата и достигает toohello контроллера домена.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-237">In this case, hello client tries toouse hello certificate and reaches out toohello domain controller.</span></span> <span data-ttu-id="4cf5d-238">Затем hello центр распространения ключей возвращает ошибку «KDC_ERR_C_PRINCIPAL_UNKNOWN».</span><span class="sxs-lookup"><span data-stu-id="4cf5d-238">Then hello Key Distribution Center returns a "KDC_ERR_C_PRINCIPAL_UNKNOWN" error.</span></span> <span data-ttu-id="4cf5d-239">Клиент Hello — Принудительная toofail через tooNTLM.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-239">hello client is forced toofail over tooNTLM.</span></span> 

### <a name="solution"></a><span data-ttu-id="4cf5d-240">Решение</span><span class="sxs-lookup"><span data-stu-id="4cf5d-240">Solution</span></span>

<span data-ttu-id="4cf5d-241">toowork проблемы hello отключить hello кэширование учетных данных домена из hello следующий подраздел реестра:</span><span class="sxs-lookup"><span data-stu-id="4cf5d-241">toowork around hello problem, disable hello caching of domain credentials from hello following registry subkey:</span></span> 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set hello value too1 


## <a name="cannot-find-hello-point-to-site-vpn-connection-in-windows-after-reinstalling-hello-vpn-client"></a><span data-ttu-id="4cf5d-242">Не удается найти hello точка сеть VPN-подключения в Windows после переустановки hello VPN-клиента</span><span class="sxs-lookup"><span data-stu-id="4cf5d-242">Cannot find hello point-to-site VPN connection in Windows after reinstalling hello VPN client</span></span>

### <a name="symptom"></a><span data-ttu-id="4cf5d-243">Симптом</span><span class="sxs-lookup"><span data-stu-id="4cf5d-243">Symptom</span></span>

<span data-ttu-id="4cf5d-244">Удалить hello точка сеть VPN-подключения, а затем переустановить hello VPN-клиента.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-244">You remove hello point-to-site VPN connection and then reinstall hello VPN client.</span></span> <span data-ttu-id="4cf5d-245">В этом случае hello VPN-подключение не настроен успешно.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-245">In this situation, hello VPN connection is not configured successfully.</span></span> <span data-ttu-id="4cf5d-246">Вы не видите hello VPN-подключение в hello **сетевые подключения** параметров в Windows.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-246">You do not see hello VPN connection in hello **Network connections** settings in Windows.</span></span>

### <a name="solution"></a><span data-ttu-id="4cf5d-247">Решение</span><span class="sxs-lookup"><span data-stu-id="4cf5d-247">Solution</span></span>

<span data-ttu-id="4cf5d-248">проблема tooresolve hello, delete hello старого VPN файлах конфигурации клиента из **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, а затем снова запустите установщик клиента VPN hello.</span><span class="sxs-lookup"><span data-stu-id="4cf5d-248">tooresolve hello problem, delete hello old VPN client configuration files from **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, and then run hello VPN client installer again.</span></span>
