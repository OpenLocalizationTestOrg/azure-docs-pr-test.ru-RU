---
title: "Устранение неполадок подключения типа \"точка — сеть\" Azure | Документация Майкрософт"
description: "Узнайте, как устранять неполадки подключения типа \"точка — сеть\"."
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
ms.openlocfilehash: de37c8ffd47a2b8e201d18e3a20b5325d528ad59
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a><span data-ttu-id="5cfdc-103">Устранение неполадок подключения типа "точка — сеть" Azure</span><span class="sxs-lookup"><span data-stu-id="5cfdc-103">Troubleshooting: Azure point-to-site connection problems</span></span>

<span data-ttu-id="5cfdc-104">В этой статье перечисляются распространенные проблемы подключения типа "точка — сеть", которые могут возникнуть.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-104">This article lists common point-to-site connection problems that you might experience.</span></span> <span data-ttu-id="5cfdc-105">Кроме того, здесь рассматриваются возможные причины этих проблем и способы их устранения.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-105">It also discusses possible causes and solutions for these problems.</span></span>

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a><span data-ttu-id="5cfdc-106">Ошибка VPN-клиента: не удалось найти сертификат</span><span class="sxs-lookup"><span data-stu-id="5cfdc-106">VPN client error: A certificate could not be found</span></span>

### <a name="symptom"></a><span data-ttu-id="5cfdc-107">Симптом</span><span class="sxs-lookup"><span data-stu-id="5cfdc-107">Symptom</span></span>

<span data-ttu-id="5cfdc-108">При попытке подключения к виртуальной сети Azure с помощью VPN-клиента появляется следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="5cfdc-108">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="5cfdc-109">**Не удалось найти сертификат, который был бы использован с протоколом расширенной проверки подлинности (EAP). (Ошибка 798.)**</span><span class="sxs-lookup"><span data-stu-id="5cfdc-109">**A certificate could not be found that can be used with this Extensible Authentication Protocol. (Error 798)**</span></span>

### <a name="cause"></a><span data-ttu-id="5cfdc-110">Причина:</span><span class="sxs-lookup"><span data-stu-id="5cfdc-110">Cause</span></span>

<span data-ttu-id="5cfdc-111">Эта проблема возникает, если сертификат клиента отсутствует в папке **Certificates - Current User\Personal\Certificates**.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-111">This problem occurs if the client certificate is missing from **Certificates - Current User\Personal\Certificates**.</span></span>

### <a name="solution"></a><span data-ttu-id="5cfdc-112">Решение</span><span class="sxs-lookup"><span data-stu-id="5cfdc-112">Solution</span></span>

<span data-ttu-id="5cfdc-113">Убедитесь, что сертификат клиента установлен в следующем расположении в хранилище сертификатов (Certmgr.msc):</span><span class="sxs-lookup"><span data-stu-id="5cfdc-113">Make sure that the client certificate is installed in the following location of the Certificates store (Certmgr.msc):</span></span>
 
<span data-ttu-id="5cfdc-114">**Certificates - Current User\Personal\Certificates**</span><span class="sxs-lookup"><span data-stu-id="5cfdc-114">**Certificates - Current User\Personal\Certificates**</span></span>

<span data-ttu-id="5cfdc-115">Дополнительные сведения о том, как установить сертификат клиента, см. в статье [Создание и экспорт сертификатов для подключений типа "точка — сеть" с помощью PowerShell в Windows 10](vpn-gateway-certificates-point-to-site.md).</span><span class="sxs-lookup"><span data-stu-id="5cfdc-115">For more information about how to install the client certificate, see [Generate and export certificates for point-to-site connections](vpn-gateway-certificates-point-to-site.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5cfdc-116">При импорте сертификата клиента не выбирайте параметр **Включить усиленную защиту закрытого ключа**.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-116">When you import the client certificate, do not select the **Enable strong private key protection** option.</span></span>

## <a name="vpn-client-error-the-message-received-was-unexpected-or-badly-formatted"></a><span data-ttu-id="5cfdc-117">Ошибка VPN-клиента: получено непредвиденное или неправильно отформатированное сообщение</span><span class="sxs-lookup"><span data-stu-id="5cfdc-117">VPN client error: The message received was unexpected or badly formatted</span></span>

### <a name="symptom"></a><span data-ttu-id="5cfdc-118">Симптом</span><span class="sxs-lookup"><span data-stu-id="5cfdc-118">Symptom</span></span>

<span data-ttu-id="5cfdc-119">При попытке подключения к виртуальной сети Azure с помощью VPN-клиента появляется следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="5cfdc-119">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="5cfdc-120">**Получено непредвиденное сообщение или оно имеет неправильный формат. (Ошибка 0x80090326.)**</span><span class="sxs-lookup"><span data-stu-id="5cfdc-120">**The message received was unexpected or badly formatted. (Error 0x80090326)**</span></span>

### <a name="cause"></a><span data-ttu-id="5cfdc-121">Причина:</span><span class="sxs-lookup"><span data-stu-id="5cfdc-121">Cause</span></span>

<span data-ttu-id="5cfdc-122">Эта проблема возникает, если открытый ключ корневого сертификата не был передан на VPN-шлюз Azure.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-122">This problem occurs if the root certificate public key is not uploaded into the Azure VPN gateway.</span></span> <span data-ttu-id="5cfdc-123">Она также может возникать, если ключ поврежден или истек срок его действия.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-123">It can also occur if the key is corrupted or expired.</span></span>

### <a name="solution"></a><span data-ttu-id="5cfdc-124">Решение</span><span class="sxs-lookup"><span data-stu-id="5cfdc-124">Solution</span></span>

<span data-ttu-id="5cfdc-125">Чтобы устранить эту проблему, проверьте состояние корневого сертификата на портале Azure, чтобы узнать, не отозван ли он.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-125">To resolve this problem, check the status of the root certificate in the Azure portal to see whether it was revoked.</span></span> <span data-ttu-id="5cfdc-126">Если он не был отозван, попробуйте удалить корневой сертификат и повторить его передачу.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-126">If it is not revoked, try to delete the root certificate and reupload.</span></span> <span data-ttu-id="5cfdc-127">Дополнительные сведения см. в разделе [Создание сертификатов](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span><span class="sxs-lookup"><span data-stu-id="5cfdc-127">For more information, see [Create certificates](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).</span></span>

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a><span data-ttu-id="5cfdc-128">Ошибка VPN-клиента: цепочка сертификатов обработана, но обработка прервана</span><span class="sxs-lookup"><span data-stu-id="5cfdc-128">VPN client error: A certificate chain processed but terminated</span></span> 

### <a name="symptom"></a><span data-ttu-id="5cfdc-129">Симптом</span><span class="sxs-lookup"><span data-stu-id="5cfdc-129">Symptom</span></span> 

<span data-ttu-id="5cfdc-130">При попытке подключения к виртуальной сети Azure с помощью VPN-клиента появляется следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="5cfdc-130">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="5cfdc-131">**Цепочка сертификатов обработана, но обработка прервана на корневом сертификате, у которого отсутствует отношение доверия с поставщиком доверия.**</span><span class="sxs-lookup"><span data-stu-id="5cfdc-131">**A certificate chain processed but terminated in a root certificate which is not trusted by the trust provider.**</span></span>

### <a name="solution"></a><span data-ttu-id="5cfdc-132">Решение</span><span class="sxs-lookup"><span data-stu-id="5cfdc-132">Solution</span></span>

1. <span data-ttu-id="5cfdc-133">Убедитесь, что перечисленные ниже сертификаты находятся в правильном расположении.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-133">Make sure that the following certificates are in the correct location:</span></span>

    | <span data-ttu-id="5cfdc-134">Сертификат</span><span class="sxs-lookup"><span data-stu-id="5cfdc-134">Certificate</span></span> | <span data-ttu-id="5cfdc-135">Расположение</span><span class="sxs-lookup"><span data-stu-id="5cfdc-135">Location</span></span> |
    | ------------- | ------------- |
    | <span data-ttu-id="5cfdc-136">AzureClient.pfx</span><span class="sxs-lookup"><span data-stu-id="5cfdc-136">AzureClient.pfx</span></span>  | <span data-ttu-id="5cfdc-137">Current User\Personal\Certificates</span><span class="sxs-lookup"><span data-stu-id="5cfdc-137">Current User\Personal\Certificates</span></span> |
    | <span data-ttu-id="5cfdc-138">Azuregateway-*GUID*.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="5cfdc-138">Azuregateway-*GUID*.cloudapp.net</span></span>  | <span data-ttu-id="5cfdc-139">Current User\Trusted Root Certification Authorities</span><span class="sxs-lookup"><span data-stu-id="5cfdc-139">Current User\Trusted Root Certification Authorities</span></span>|
    | <span data-ttu-id="5cfdc-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span><span class="sxs-lookup"><span data-stu-id="5cfdc-140">AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer</span></span>    | <span data-ttu-id="5cfdc-141">Local Computer\Trusted Root Certification Authorities</span><span class="sxs-lookup"><span data-stu-id="5cfdc-141">Local Computer\Trusted Root Certification Authorities</span></span>|

2. <span data-ttu-id="5cfdc-142">Если сертификаты уже находятся в соответствующих расположениях, попробуйте удалить эти сертификаты и установить их заново.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-142">If the certificates are already in the location, try to delete the certificates and reinstall them.</span></span> <span data-ttu-id="5cfdc-143">Сертификат **azuregateway-*GUID*.cloudapp.net** находится в пакете конфигурации VPN-клиента, скачанном с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-143">The **azuregateway-*GUID*.cloudapp.net** certificate is in the VPN client configuration package that you downloaded from the Azure portal.</span></span> <span data-ttu-id="5cfdc-144">Для извлечения файлов из пакета можно использовать архиваторы.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-144">You can use file archivers to extract the files from the package.</span></span>

## <a name="file-download-error-target-uri-is-not-specified"></a><span data-ttu-id="5cfdc-145">Произошла ошибка скачивания файла. Целевой URI не указан</span><span class="sxs-lookup"><span data-stu-id="5cfdc-145">File download error: Target URI is not specified</span></span>

### <a name="symptom"></a><span data-ttu-id="5cfdc-146">Симптом</span><span class="sxs-lookup"><span data-stu-id="5cfdc-146">Symptom</span></span>

<span data-ttu-id="5cfdc-147">Отображается следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="5cfdc-147">You receive the following error message:</span></span>

<span data-ttu-id="5cfdc-148">**Ошибка скачивания файла. Не указан целевой URI.**</span><span class="sxs-lookup"><span data-stu-id="5cfdc-148">**File download error. Target URI is not specified.**</span></span>

### <a name="cause"></a><span data-ttu-id="5cfdc-149">Причина:</span><span class="sxs-lookup"><span data-stu-id="5cfdc-149">Cause</span></span> 

<span data-ttu-id="5cfdc-150">Эта проблема возникает из-за неправильного типа шлюза.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-150">This problem occurs because of an incorrect gateway type.</span></span> 

### <a name="solution"></a><span data-ttu-id="5cfdc-151">Решение</span><span class="sxs-lookup"><span data-stu-id="5cfdc-151">Solution</span></span>

<span data-ttu-id="5cfdc-152">Типом VPN-шлюза должен быть **VPN**, а типом VPN — **routebased**.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-152">The VPN gateway type must be **VPN**, and the VPN type must be **RouteBased**.</span></span>

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a><span data-ttu-id="5cfdc-153">Ошибка VPN-клиента: сбой настраиваемого сценария VPN Azure</span><span class="sxs-lookup"><span data-stu-id="5cfdc-153">VPN client error: Azure VPN custom script failed</span></span> 

### <a name="symptom"></a><span data-ttu-id="5cfdc-154">Симптом</span><span class="sxs-lookup"><span data-stu-id="5cfdc-154">Symptom</span></span>

<span data-ttu-id="5cfdc-155">При попытке подключения к виртуальной сети Azure с помощью VPN-клиента появляется следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="5cfdc-155">When you try to connect to an Azure virtual network by using the VPN client, you receive the following error message:</span></span>

<span data-ttu-id="5cfdc-156">**Custom script (to update your routing table) failed. (Error 8007026f)** (Произошел сбой настраиваемого сценария (для обновления таблицы маршрутизации). (Ошибка 8007026f)).</span><span class="sxs-lookup"><span data-stu-id="5cfdc-156">**Custom script (to update your routing table) failed. (Error 8007026f)**</span></span>

### <a name="cause"></a><span data-ttu-id="5cfdc-157">Причина:</span><span class="sxs-lookup"><span data-stu-id="5cfdc-157">Cause</span></span>

<span data-ttu-id="5cfdc-158">Это может произойти, если вы пытаетесь открыть VPN-подключение типа "сеть — точка" с помощью ярлыка.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-158">This problem might occur if you are trying to open the site-to-point VPN connection by using a shortcut.</span></span>

### <a name="solution"></a><span data-ttu-id="5cfdc-159">Решение</span><span class="sxs-lookup"><span data-stu-id="5cfdc-159">Solution</span></span> 

<span data-ttu-id="5cfdc-160">Откройте пакет VPN напрямую, а не с помощью ярлыка.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-160">Open the VPN package directly instead of opening it from the shortcut.</span></span>

## <a name="cannot-install-the-vpn-client"></a><span data-ttu-id="5cfdc-161">Не удается установить VPN-клиент</span><span class="sxs-lookup"><span data-stu-id="5cfdc-161">Cannot install the VPN client</span></span>

### <a name="cause"></a><span data-ttu-id="5cfdc-162">Причина:</span><span class="sxs-lookup"><span data-stu-id="5cfdc-162">Cause</span></span> 

<span data-ttu-id="5cfdc-163">Для установления отношений доверия между VPN-шлюзом и виртуальной сетью требуется дополнительный сертификат.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-163">An additional certificate is required to trust the VPN gateway for your virtual network.</span></span> <span data-ttu-id="5cfdc-164">Этот сертификат включен в пакет конфигурации VPN-клиента, который создается на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-164">The certificate is included in the VPN client configuration package that is generated from the Azure portal.</span></span>

### <a name="solution"></a><span data-ttu-id="5cfdc-165">Решение</span><span class="sxs-lookup"><span data-stu-id="5cfdc-165">Solution</span></span>

<span data-ttu-id="5cfdc-166">Извлеките содержимое пакета конфигурации VPN-клиента и найдите CER-файл.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-166">Extract the VPN client configuration package, and find the .cer file.</span></span> <span data-ttu-id="5cfdc-167">Для установки сертификата выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="5cfdc-167">To install the certificate, follow these steps:</span></span>

1. <span data-ttu-id="5cfdc-168">Запустите mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-168">Open mmc.exe.</span></span>
2. <span data-ttu-id="5cfdc-169">Добавьте оснастку **Сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-169">Add the **Certificates** snap-in.</span></span>
3. <span data-ttu-id="5cfdc-170">Выберите учетную запись **Компьютер** для локального компьютера.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-170">Select the **Computer** account for the local computer.</span></span>
4. <span data-ttu-id="5cfdc-171">Щелкните правой кнопкой мыши узел **Доверенные корневые центры сертификации**.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-171">Right-click the **Trusted Root Certification Authorities** node.</span></span> <span data-ttu-id="5cfdc-172">Щелкните **Все задачи** > **Импорт** и найдите CER-файл, извлеченный из пакета конфигурации VPN-клиента.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-172">Click **All-Task** > **Import**, and browse to the .cer file you extracted from the VPN client configuration package.</span></span>
5. <span data-ttu-id="5cfdc-173">Перезагрузите компьютер.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-173">Restart the computer.</span></span> 
6. <span data-ttu-id="5cfdc-174">Попробуйте установить VPN-клиент.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-174">Try to install the VPN client.</span></span>

## <a name="azure-portal-error-failed-to-save-the-vpn-gateway-and-the-data-is-invalid"></a><span data-ttu-id="5cfdc-175">Ошибка портала Azure: не удалось сохранить VPN-шлюз, так как данные являются недопустимыми</span><span class="sxs-lookup"><span data-stu-id="5cfdc-175">Azure portal error: Failed to save the VPN gateway, and the data is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="5cfdc-176">Симптом</span><span class="sxs-lookup"><span data-stu-id="5cfdc-176">Symptom</span></span>

<span data-ttu-id="5cfdc-177">При попытке сохранить изменения для VPN-шлюза на портале Azure появляется следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="5cfdc-177">When you try to save the changes for the VPN gateway in the Azure portal, you receive the following error message:</span></span>

<span data-ttu-id="5cfdc-178">**Не удалось сохранить шлюз виртуальной сети &lt;*имя шлюза*&gt;.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-178">**Failed to save virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="5cfdc-179">Недействительные данные для сертификата &lt;*идентификатор сертификата*&gt;**.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-179">Data for certificate &lt;*certificate ID*&gt; is invalid.**</span></span>

### <a name="cause"></a><span data-ttu-id="5cfdc-180">Причина:</span><span class="sxs-lookup"><span data-stu-id="5cfdc-180">Cause</span></span> 

<span data-ttu-id="5cfdc-181">Эта проблема может возникнуть, если переданный вами открытый ключ корневого сертификата содержит недопустимые знаки, например пробел.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-181">This problem might occur if the root certificate public key that you uploaded contains an invalid character, such as a space.</span></span>

### <a name="solution"></a><span data-ttu-id="5cfdc-182">Решение</span><span class="sxs-lookup"><span data-stu-id="5cfdc-182">Solution</span></span>

<span data-ttu-id="5cfdc-183">Убедитесь, что данные в сертификате не содержат недопустимых знаков, таких как разрывы строки (возврат каретки).</span><span class="sxs-lookup"><span data-stu-id="5cfdc-183">Make sure that the data in the certificate does not contain invalid characters, such as line breaks (carriage returns).</span></span> <span data-ttu-id="5cfdc-184">Значение целиком должно находиться в одной длинной строке.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-184">The entire value should be one long line.</span></span> <span data-ttu-id="5cfdc-185">Ниже приведен пример содержимого сертификата.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-185">The following text is a sample of the certificate:</span></span>

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

## <a name="azure-portal-error-failed-to-save-the-vpn-gateway-and-the-resource-name-is-invalid"></a><span data-ttu-id="5cfdc-186">Ошибка портала Azure: не удалось сохранить VPN-шлюз, так как имя ресурса является недопустимым</span><span class="sxs-lookup"><span data-stu-id="5cfdc-186">Azure portal error: Failed to save the VPN gateway, and the resource name is invalid</span></span>

### <a name="symptom"></a><span data-ttu-id="5cfdc-187">Симптом</span><span class="sxs-lookup"><span data-stu-id="5cfdc-187">Symptom</span></span>

<span data-ttu-id="5cfdc-188">При попытке сохранить изменения для VPN-шлюза на портале Azure появляется следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="5cfdc-188">When you try to save the changes for the VPN gateway in the Azure portal, you receive the following error message:</span></span> 

<span data-ttu-id="5cfdc-189">**Не удалось сохранить шлюз виртуальной сети &lt;*имя шлюза*&gt;.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-189">**Failed to save virtual network gateway &lt;*gateway name*&gt;.</span></span> <span data-ttu-id="5cfdc-190">Недопустимое имя ресурса &lt;*имя сертификата, который вы пытаетесь передать*&gt;**.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-190">Resource name &lt;*certificate name you try to upload*&gt; is invalid**.</span></span>

### <a name="cause"></a><span data-ttu-id="5cfdc-191">Причина:</span><span class="sxs-lookup"><span data-stu-id="5cfdc-191">Cause</span></span>

<span data-ttu-id="5cfdc-192">Эта проблема возникает, когда имя сертификата содержит недопустимые знаки, например пробел.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-192">This problem occurs because the name of the certificate contains an invalid character, such as a space.</span></span> 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a><span data-ttu-id="5cfdc-193">Ошибка портала Azure: ошибка 503 при скачивании файла пакета VPN</span><span class="sxs-lookup"><span data-stu-id="5cfdc-193">Azure portal error: VPN package file download error 503</span></span>

### <a name="symptom"></a><span data-ttu-id="5cfdc-194">Симптом</span><span class="sxs-lookup"><span data-stu-id="5cfdc-194">Symptom</span></span>

<span data-ttu-id="5cfdc-195">При попытке скачать пакет конфигурации VPN-клиента появляется следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="5cfdc-195">When you try to download the VPN client configuration package, you receive the following error message:</span></span>

<span data-ttu-id="5cfdc-196">**Не удалось скачать файл. Сведения об ошибке: ошибка 503. Сервер занят.**</span><span class="sxs-lookup"><span data-stu-id="5cfdc-196">**Failed to download the file. Error details: error 503. The server is busy.**</span></span>
 
### <a name="solution"></a><span data-ttu-id="5cfdc-197">Решение</span><span class="sxs-lookup"><span data-stu-id="5cfdc-197">Solution</span></span>

<span data-ttu-id="5cfdc-198">Эта ошибка может быть вызвана временным сбоем сети.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-198">This error can be caused by a temporary network problem.</span></span> <span data-ttu-id="5cfdc-199">Попробуйте еще раз скачать пакет VPN через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-199">Try to download the VPN package again after a few minutes.</span></span>

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-to-connect"></a><span data-ttu-id="5cfdc-200">Обновление VPN-шлюза Azure, всем клиентам типа "точка — сеть" не удается подключиться</span><span class="sxs-lookup"><span data-stu-id="5cfdc-200">Azure VPN Gateway upgrade: All P2S clients are unable to connect</span></span>

### <a name="cause"></a><span data-ttu-id="5cfdc-201">Причина:</span><span class="sxs-lookup"><span data-stu-id="5cfdc-201">Cause</span></span>

<span data-ttu-id="5cfdc-202">Если время существования сертификата составляет более 50 процентов, то сертификат сменяется.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-202">If the certificate is more than 50 percent through its lifetime, the certificate is rolled over.</span></span>

### <a name="solution"></a><span data-ttu-id="5cfdc-203">Решение</span><span class="sxs-lookup"><span data-stu-id="5cfdc-203">Solution</span></span>

<span data-ttu-id="5cfdc-204">Чтобы устранить эту проблему, создайте и распространите новые сертификаты для VPN-клиентов.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-204">To resolve this problem, create and redistribute new certificates to the VPN clients.</span></span> 

## <a name="too-many-vpn-clients-connected-at-once"></a><span data-ttu-id="5cfdc-205">Слишком много одновременно подключенных VPN-клиентов</span><span class="sxs-lookup"><span data-stu-id="5cfdc-205">Too many VPN clients connected at once</span></span>

<span data-ttu-id="5cfdc-206">Для каждого VPN-шлюза максимальное число допустимых подключений равно 128.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-206">For each VPN gateway, the maximum number of allowable connections is 128.</span></span> <span data-ttu-id="5cfdc-207">Общее количество подключенных клиентов можно просмотреть на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-207">You can see the total number of connected clients in the Azure portal.</span></span>

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-to-the-route-table"></a><span data-ttu-id="5cfdc-208">VPN-подключение типа "точка — сеть" неправильно добавляет маршрут для 10.0.0.0/8 в таблицу маршрутов</span><span class="sxs-lookup"><span data-stu-id="5cfdc-208">Point-to-site VPN incorrectly adds a route for 10.0.0.0/8 to the route table</span></span>

### <a name="symptom"></a><span data-ttu-id="5cfdc-209">Симптом</span><span class="sxs-lookup"><span data-stu-id="5cfdc-209">Symptom</span></span>

<span data-ttu-id="5cfdc-210">При установлении VPN-подключения с клиентом типа "точка — сеть" VPN-клиент должен добавить маршрут к виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-210">When you dial the VPN connection on the point-to-site client, the VPN client should add a route toward the Azure virtual network.</span></span> <span data-ttu-id="5cfdc-211">Служба модуля поддержки IP добавит маршрут для подсети VPN-клиентов.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-211">The IP helper service should add a route for the subnet of the VPN clients.</span></span> 

<span data-ttu-id="5cfdc-212">Диапазон адресов VPN-клиента принадлежит подсети, меньшей 10.0.0.0/8, например 10.0.12.0/24.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-212">The VPN client range belongs to a smaller subnet of 10.0.0.0/8, such as 10.0.12.0/24.</span></span> <span data-ttu-id="5cfdc-213">Вместо маршрута для 10.0.12.0/24 добавляется маршрут для 10.0.0.0/8, который имеет более высокий приоритет.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-213">Instead of a route for 10.0.12.0/24, a route for 10.0.0.0/8 is added that has higher priority.</span></span> 

<span data-ttu-id="5cfdc-214">Этот ошибочный маршрут разрывает связь с другими локальными сетями, которые могут входить в другую подсеть в пределах диапазона 10.0.0.0/8, например 10.50.0.0/24, для которой не определен конкретный маршрут.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-214">This incorrect route breaks connectivity with other on-premises networks that might belong to another subnet within the 10.0.0.0/8 range, such as 10.50.0.0/24, that don't have a specific route defined.</span></span> 

### <a name="cause"></a><span data-ttu-id="5cfdc-215">Причина:</span><span class="sxs-lookup"><span data-stu-id="5cfdc-215">Cause</span></span>

<span data-ttu-id="5cfdc-216">Это сделано намеренно для клиентов Windows.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-216">This behavior is by design for Windows clients.</span></span> <span data-ttu-id="5cfdc-217">При использовании протокола PPP IPCP клиент получает IP-адрес для интерфейса туннеля от сервера (в данном случае — VPN-шлюза).</span><span class="sxs-lookup"><span data-stu-id="5cfdc-217">When the client uses the PPP IPCP protocol, it obtains the IP address for the tunnel interface from the server (the VPN gateway in this case).</span></span> <span data-ttu-id="5cfdc-218">Однако из-за ограничений в протоколе у клиента нет маски подсети.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-218">However, because of a limitation in the protocol, the client does not have the subnet mask.</span></span> <span data-ttu-id="5cfdc-219">Так как нет другого способа получить ее, клиент пытается угадать маску подсети на основе класса IP-адрес интерфейса туннеля.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-219">Because there is no other way to get it, the client tries to guess the subnet mask based on the class of the tunnel interface IP address.</span></span> 

<span data-ttu-id="5cfdc-220">Следовательно, маршрут добавляется в зависимости от следующего статического сопоставления:</span><span class="sxs-lookup"><span data-stu-id="5cfdc-220">Therefore, a route is added based on the following static mapping:</span></span> 

<span data-ttu-id="5cfdc-221">если адрес относится к классу A, применяется маска /8;</span><span class="sxs-lookup"><span data-stu-id="5cfdc-221">If address belongs to class A --> apply /8</span></span>

<span data-ttu-id="5cfdc-222">если адрес относится к классу B, применяется маска /16;</span><span class="sxs-lookup"><span data-stu-id="5cfdc-222">If address belongs to class B --> apply /16</span></span>

<span data-ttu-id="5cfdc-223">если адрес относится к классу C, применяется маска /24.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-223">If address belongs to class C --> apply /24</span></span>

## <a name="vpn-client-cannot-access-network-file-shares"></a><span data-ttu-id="5cfdc-224">VPN-клиент не может получить доступ к сетевым файловым ресурсам</span><span class="sxs-lookup"><span data-stu-id="5cfdc-224">VPN client cannot access network file shares</span></span>

### <a name="symptom"></a><span data-ttu-id="5cfdc-225">Симптом</span><span class="sxs-lookup"><span data-stu-id="5cfdc-225">Symptom</span></span>

<span data-ttu-id="5cfdc-226">VPN-клиент подключился к виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-226">The VPN client has connected to the Azure virtual network.</span></span> <span data-ttu-id="5cfdc-227">Однако он не может получить доступ к сетевым папкам.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-227">However, the client cannot access network shares.</span></span>

### <a name="cause"></a><span data-ttu-id="5cfdc-228">Причина:</span><span class="sxs-lookup"><span data-stu-id="5cfdc-228">Cause</span></span>

<span data-ttu-id="5cfdc-229">Для доступа к файловым ресурсам используется протокол SMB.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-229">The SMB protocol is used for file share access.</span></span> <span data-ttu-id="5cfdc-230">Когда VPN-клиент добавляет учетные данные сеанса при инициировании подключения, происходит сбой.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-230">When the connection is initiated, the VPN client adds the session credentials and the failure occurs.</span></span> <span data-ttu-id="5cfdc-231">После установления подключения клиент принудительно использует кэшированные учетные данные для аутентификации Kerberos.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-231">After the connection is established, the client is forced to use the cache credentials for Kerberos authentication.</span></span> <span data-ttu-id="5cfdc-232">Это инициирует отправку запросов к центру распространения ключей (контроллеру домена) для получения токена.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-232">This process initiates queries to the Key Distribution Center (a domain controller) to get a token.</span></span> <span data-ttu-id="5cfdc-233">Так как клиенты подключаются через Интернет, они могут не подключиться к контроллеру домена.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-233">Because the client connects from the Internet, it might not be able to reach the domain controller.</span></span> <span data-ttu-id="5cfdc-234">Следовательно, клиенты не могут выполнить отработку отказа с Kerberos на NTLM.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-234">Therefore, the client cannot fail over from Kerberos to NTLM.</span></span> 

<span data-ttu-id="5cfdc-235">Единственный случай, в котором клиенту будет предложено указать учетные данные — когда у клиента есть действительный сертификат (в котором для параметра SAN указано имя участника-пользователя), выданный доменом, к которому присоединен клиент.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-235">The only time that the client is prompted for a credential is when it has a valid certificate (with SAN=UPN) issued by the domain to which it is joined.</span></span> <span data-ttu-id="5cfdc-236">Клиент также должен быть физически подключен к доменной сети.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-236">The client also must be physically connected to the domain network.</span></span> <span data-ttu-id="5cfdc-237">В этом случае клиент пытается использовать сертификат и подключиться к контроллеру домена.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-237">In this case, the client tries to use the certificate and reaches out to the domain controller.</span></span> <span data-ttu-id="5cfdc-238">Затем центр распространения ключей возвращает ошибку "KDC_ERR_C_PRINCIPAL_UNKNOWN".</span><span class="sxs-lookup"><span data-stu-id="5cfdc-238">Then the Key Distribution Center returns a "KDC_ERR_C_PRINCIPAL_UNKNOWN" error.</span></span> <span data-ttu-id="5cfdc-239">Это вынуждает клиента выполнить отработку отказа на NTLM.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-239">The client is forced to fail over to NTLM.</span></span> 

### <a name="solution"></a><span data-ttu-id="5cfdc-240">Решение</span><span class="sxs-lookup"><span data-stu-id="5cfdc-240">Solution</span></span>

<span data-ttu-id="5cfdc-241">Чтобы обойти эту проблему, отключите кэширование учетных данных домена в следующем подразделе реестра:</span><span class="sxs-lookup"><span data-stu-id="5cfdc-241">To work around the problem, disable the caching of domain credentials from the following registry subkey:</span></span> 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set the value to 1 


## <a name="cannot-find-the-point-to-site-vpn-connection-in-windows-after-reinstalling-the-vpn-client"></a><span data-ttu-id="5cfdc-242">Не удается найти VPN-подключение типа "точка — сеть" в Windows после повторной установки VPN-клиента</span><span class="sxs-lookup"><span data-stu-id="5cfdc-242">Cannot find the point-to-site VPN connection in Windows after reinstalling the VPN client</span></span>

### <a name="symptom"></a><span data-ttu-id="5cfdc-243">Симптом</span><span class="sxs-lookup"><span data-stu-id="5cfdc-243">Symptom</span></span>

<span data-ttu-id="5cfdc-244">Вы удаляете VPN-подключение типа "точка — сеть", а затем переустанавливаете VPN-клиент.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-244">You remove the point-to-site VPN connection and then reinstall the VPN client.</span></span> <span data-ttu-id="5cfdc-245">В этом случае VPN-подключение не будет успешно настроено.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-245">In this situation, the VPN connection is not configured successfully.</span></span> <span data-ttu-id="5cfdc-246">Вы не видите VPN-подключение в параметрах **Сетевые подключения** в Windows.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-246">You do not see the VPN connection in the **Network connections** settings in Windows.</span></span>

### <a name="solution"></a><span data-ttu-id="5cfdc-247">Решение</span><span class="sxs-lookup"><span data-stu-id="5cfdc-247">Solution</span></span>

<span data-ttu-id="5cfdc-248">Чтобы устранить эту проблему, удалите старые файлы конфигурации VPN-клиента из папки **C:\Users\{имя_пользователя}\AppData\Roaming\Microsoft\Network\Connections**, а затем снова запустите установщик VPN-клиента.</span><span class="sxs-lookup"><span data-stu-id="5cfdc-248">To resolve the problem, delete the old VPN client configuration files from **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, and then run the VPN client installer again.</span></span>
