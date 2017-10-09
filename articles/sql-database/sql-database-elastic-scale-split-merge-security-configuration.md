---
title: "Конфигурация безопасности слияния aaaSplit | Документы Microsoft"
description: "Настройка сертификатов x409 для шифрования"
metakeywords: Elastic Database certificates security
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: f9e89c57-61a0-484f-b787-82dae2349cb6
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 511c04be0598d8a0889aa3e3fcf02be0bf0e96cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="split-merge-security-configuration"></a><span data-ttu-id="724c4-103">Настройка параметров безопасности для службы разделения и объединения</span><span class="sxs-lookup"><span data-stu-id="724c4-103">Split-merge security configuration</span></span>
<span data-ttu-id="724c4-104">Служба разделения или слияния toouse hello, необходимо правильно настроить безопасность.</span><span class="sxs-lookup"><span data-stu-id="724c4-104">toouse hello Split/Merge service, you must correctly configure security.</span></span> <span data-ttu-id="724c4-105">Hello служба является частью hello возможность гибкого масштабирования базы данных SQL Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="724c4-105">hello service is part of hello Elastic Scale feature of Microsoft Azure SQL Database.</span></span> <span data-ttu-id="724c4-106">Дополнительные сведения см. в [руководстве по эластичному масштабированию службы разбиения и объединения](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="724c4-106">For more information, see [Elastic Scale Split and Merge Service Tutorial](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span></span>

## <a name="configuring-certificates"></a><span data-ttu-id="724c4-107">Настройка сертификатов</span><span class="sxs-lookup"><span data-stu-id="724c4-107">Configuring certificates</span></span>
<span data-ttu-id="724c4-108">Сертификаты настраиваются двумя способами.</span><span class="sxs-lookup"><span data-stu-id="724c4-108">Certificates are configured in two ways.</span></span> 

1. [<span data-ttu-id="724c4-109">hello tooConfigure SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="724c4-109">tooConfigure hello SSL Certificate</span></span>](#to-configure-the-ssl-certificate)
2. [<span data-ttu-id="724c4-110">tooConfigure сертификаты клиента</span><span class="sxs-lookup"><span data-stu-id="724c4-110">tooConfigure Client Certificates</span></span>](#to-configure-client-certificates) 

## <a name="tooobtain-certificates"></a><span data-ttu-id="724c4-111">сертификаты tooobtain</span><span class="sxs-lookup"><span data-stu-id="724c4-111">tooobtain certificates</span></span>
<span data-ttu-id="724c4-112">Сертификаты можно получить из открытых центров сертификации (ЦС) или hello [службы сертификатов Windows](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span><span class="sxs-lookup"><span data-stu-id="724c4-112">Certificates can be obtained from public Certificate Authorities (CAs) or from hello [Windows Certificate Service](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span></span> <span data-ttu-id="724c4-113">Это предпочтительный hello методы tooobtain сертификаты.</span><span class="sxs-lookup"><span data-stu-id="724c4-113">These are hello preferred methods tooobtain certificates.</span></span>

<span data-ttu-id="724c4-114">Если эти варианты недоступны, можно создавать **самозаверяющие сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="724c4-114">If those options are not available, you can generate **self-signed certificates**.</span></span>

## <a name="tools-toogenerate-certificates"></a><span data-ttu-id="724c4-115">Средства toogenerate сертификатов</span><span class="sxs-lookup"><span data-stu-id="724c4-115">Tools toogenerate certificates</span></span>
* [<span data-ttu-id="724c4-116">makecert.exe</span><span class="sxs-lookup"><span data-stu-id="724c4-116">makecert.exe</span></span>](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [<span data-ttu-id="724c4-117">pvk2pfx.exe</span><span class="sxs-lookup"><span data-stu-id="724c4-117">pvk2pfx.exe</span></span>](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="toorun-hello-tools"></a><span data-ttu-id="724c4-118">средства toorun hello</span><span class="sxs-lookup"><span data-stu-id="724c4-118">toorun hello tools</span></span>
* <span data-ttu-id="724c4-119">Сведения о запуске инструментов из командной строки разработчика для Visual Studio см. в статье [Командная строка разработчика для Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx).</span><span class="sxs-lookup"><span data-stu-id="724c4-119">From a Developer Command Prompt for Visual Studios, see [Visual Studio Command Prompt](http://msdn.microsoft.com/library/ms229859.aspx)</span></span> 
  
    <span data-ttu-id="724c4-120">Если ПО установлено, перейдите к:</span><span class="sxs-lookup"><span data-stu-id="724c4-120">If installed, go to:</span></span>
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* <span data-ttu-id="724c4-121">Получить hello WDK из [Windows 8.1: скачивание комплектов и средств](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span><span class="sxs-lookup"><span data-stu-id="724c4-121">Get hello WDK from [Windows 8.1: Download kits and tools](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span></span>

## <a name="tooconfigure-hello-ssl-certificate"></a><span data-ttu-id="724c4-122">tooconfigure hello SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="724c4-122">tooconfigure hello SSL certificate</span></span>
<span data-ttu-id="724c4-123">SSL-сертификат является обязательным tooencrypt hello связи и проверить подлинность сервера hello.</span><span class="sxs-lookup"><span data-stu-id="724c4-123">A SSL certificate is required tooencrypt hello communication and authenticate hello server.</span></span> <span data-ttu-id="724c4-124">Выберите наиболее применимым из трех сценариев hello ниже hello и выполните все шаги:</span><span class="sxs-lookup"><span data-stu-id="724c4-124">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="create-a-new-self-signed-certificate"></a><span data-ttu-id="724c4-125">Создание самозаверяющего сертификата</span><span class="sxs-lookup"><span data-stu-id="724c4-125">Create a new self-signed certificate</span></span>
1. [<span data-ttu-id="724c4-126">Создание самозаверяющего сертификата</span><span class="sxs-lookup"><span data-stu-id="724c4-126">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="724c4-127">Создание PFX-файла для самозаверяющего SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="724c4-127">Create PFX file for Self-Signed SSL Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="724c4-128">Отправка tooCloud SSL-сертификата службы</span><span class="sxs-lookup"><span data-stu-id="724c4-128">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
4. [<span data-ttu-id="724c4-129">Обновление SSL-сертификата в файле конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="724c4-129">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)
5. [<span data-ttu-id="724c4-130">Импорт центра сертификации SSL</span><span class="sxs-lookup"><span data-stu-id="724c4-130">Import SSL Certification Authority</span></span>](#import-ssl-certification-authority)

### <a name="toouse-an-existing-certificate-from-hello-certificate-store"></a><span data-ttu-id="724c4-131">сохранить существующий сертификат из сертификата hello toouse</span><span class="sxs-lookup"><span data-stu-id="724c4-131">toouse an existing certificate from hello certificate store</span></span>
1. [<span data-ttu-id="724c4-132">Экспорт SSL-сертификата из хранилища сертификатов</span><span class="sxs-lookup"><span data-stu-id="724c4-132">Export SSL Certificate From Certificate Store</span></span>](#export-ssl-certificate-from-certificate-store)
2. [<span data-ttu-id="724c4-133">Отправка tooCloud SSL-сертификата службы</span><span class="sxs-lookup"><span data-stu-id="724c4-133">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
3. [<span data-ttu-id="724c4-134">Обновление SSL-сертификата в файле конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="724c4-134">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

### <a name="toouse-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="724c4-135">toouse существующего сертификата в PFX-файла</span><span class="sxs-lookup"><span data-stu-id="724c4-135">toouse an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="724c4-136">Отправка tooCloud SSL-сертификата службы</span><span class="sxs-lookup"><span data-stu-id="724c4-136">Upload SSL Certificate tooCloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
2. [<span data-ttu-id="724c4-137">Обновление SSL-сертификата в файле конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="724c4-137">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

## <a name="tooconfigure-client-certificates"></a><span data-ttu-id="724c4-138">сертификаты клиентов tooconfigure</span><span class="sxs-lookup"><span data-stu-id="724c4-138">tooconfigure client certificates</span></span>
<span data-ttu-id="724c4-139">В порядке tooauthenticate запросов toohello службы требуются клиентские сертификаты.</span><span class="sxs-lookup"><span data-stu-id="724c4-139">Client certificates are required in order tooauthenticate requests toohello service.</span></span> <span data-ttu-id="724c4-140">Выберите наиболее применимым из трех сценариев hello ниже hello и выполните все шаги:</span><span class="sxs-lookup"><span data-stu-id="724c4-140">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="turn-off-client-certificates"></a><span data-ttu-id="724c4-141">Отключение сертификатов клиента</span><span class="sxs-lookup"><span data-stu-id="724c4-141">Turn off client certificates</span></span>
1. [<span data-ttu-id="724c4-142">Отключение аутентификации на основе сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="724c4-142">Turn Off Client Certificate-Based Authentication</span></span>](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a><span data-ttu-id="724c4-143">Выдача новых самозаверяющих сертификатов клиента</span><span class="sxs-lookup"><span data-stu-id="724c4-143">Issue new self-signed client certificates</span></span>
1. [<span data-ttu-id="724c4-144">Создание центра самозаверяющей сертификации</span><span class="sxs-lookup"><span data-stu-id="724c4-144">Create a Self-Signed Certification Authority</span></span>](#create-a-self-signed-certification-authority)
2. [<span data-ttu-id="724c4-145">Загрузить сертификат ЦС tooCloud службы</span><span class="sxs-lookup"><span data-stu-id="724c4-145">Upload CA Certificate tooCloud Service</span></span>](#upload-ca-certificate-to-cloud-service)
3. [<span data-ttu-id="724c4-146">Обновление сертификата ЦС в файле конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="724c4-146">Update CA Certificate in Service Configuration File</span></span>](#update-ca-certificate-in-service-configuration-file)
4. [<span data-ttu-id="724c4-147">Выдача сертификатов клиентов</span><span class="sxs-lookup"><span data-stu-id="724c4-147">Issue Client Certificates</span></span>](#issue-client-certificates)
5. [<span data-ttu-id="724c4-148">Создание PFX-файлов для сертификатов клиента</span><span class="sxs-lookup"><span data-stu-id="724c4-148">Create PFX files for Client Certificates</span></span>](#create-pfx-files-for-client-certificates)
6. [<span data-ttu-id="724c4-149">Импорт сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="724c4-149">Import Client Certificate</span></span>](#Import-Client-Certificate)
7. [<span data-ttu-id="724c4-150">Копирование отпечатков сертификатов клиента</span><span class="sxs-lookup"><span data-stu-id="724c4-150">Copy Client Certificate Thumbprints</span></span>](#copy-client-certificate-thumbprints)
8. [<span data-ttu-id="724c4-151">Настройка клиентов допускается в hello файл конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="724c4-151">Configure Allowed Clients in hello Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a><span data-ttu-id="724c4-152">Использование существующих сертификатов клиентов</span><span class="sxs-lookup"><span data-stu-id="724c4-152">Use existing client certificates</span></span>
1. [<span data-ttu-id="724c4-153">Find CA Public Key</span><span class="sxs-lookup"><span data-stu-id="724c4-153">Find CA Public Key</span></span>](#find-ca-public-key)
2. [<span data-ttu-id="724c4-154">Загрузить сертификат ЦС tooCloud службы</span><span class="sxs-lookup"><span data-stu-id="724c4-154">Upload CA Certificate tooCloud Service</span></span>](#Upload-CA-certificate-to-cloud-service)
3. [<span data-ttu-id="724c4-155">Обновление сертификата ЦС в файле конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="724c4-155">Update CA Certificate in Service Configuration File</span></span>](#Update-CA-Certificate-in-Service-Configuration-File)
4. [<span data-ttu-id="724c4-156">Копирование отпечатков сертификатов клиента</span><span class="sxs-lookup"><span data-stu-id="724c4-156">Copy Client Certificate Thumbprints</span></span>](#Copy-Client-Certificate-Thumbprints)
5. [<span data-ttu-id="724c4-157">Настройка клиентов допускается в hello файл конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="724c4-157">Configure Allowed Clients in hello Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)
6. [<span data-ttu-id="724c4-158">Настройка проверки отзыва сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="724c4-158">Configure Client Certificate Revocation Check</span></span>](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a><span data-ttu-id="724c4-159">Разрешенные IP-адреса</span><span class="sxs-lookup"><span data-stu-id="724c4-159">Allowed IP addresses</span></span>
<span data-ttu-id="724c4-160">Конечные точки службы toohello доступа может быть ограниченным toospecific диапазоны IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="724c4-160">Access toohello service endpoints can be restricted toospecific ranges of IP addresses.</span></span>

## <a name="tooconfigure-encryption-for-hello-store"></a><span data-ttu-id="724c4-161">шифрование tooconfigure hello хранилища</span><span class="sxs-lookup"><span data-stu-id="724c4-161">tooconfigure encryption for hello store</span></span>
<span data-ttu-id="724c4-162">Сертификат — hello tooencrypt необходимые учетные данные, которые хранятся в хранилище метаданных hello.</span><span class="sxs-lookup"><span data-stu-id="724c4-162">A certificate is required tooencrypt hello credentials that are stored in hello metadata store.</span></span> <span data-ttu-id="724c4-163">Выберите наиболее применимым из трех сценариев hello ниже hello и выполните все шаги:</span><span class="sxs-lookup"><span data-stu-id="724c4-163">Choose hello most applicable of hello three scenarios below, and execute all its steps:</span></span>

### <a name="use-a-new-self-signed-certificate"></a><span data-ttu-id="724c4-164">Использование нового самозаверяющего сертификата</span><span class="sxs-lookup"><span data-stu-id="724c4-164">Use a new self-signed certificate</span></span>
1. [<span data-ttu-id="724c4-165">Создание самозаверяющего сертификата</span><span class="sxs-lookup"><span data-stu-id="724c4-165">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="724c4-166">Создание PFX-файла для самозаверяющего сертификата шифрования</span><span class="sxs-lookup"><span data-stu-id="724c4-166">Create PFX file for Self-Signed Encryption Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="724c4-167">Отправить сертификат шифрования tooCloud службы</span><span class="sxs-lookup"><span data-stu-id="724c4-167">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
4. [<span data-ttu-id="724c4-168">Обновление сертификата шифрования в файле конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="724c4-168">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-hello-certificate-store"></a><span data-ttu-id="724c4-169">Использовать существующий сертификат из хранилища сертификатов hello</span><span class="sxs-lookup"><span data-stu-id="724c4-169">Use an existing certificate from hello certificate store</span></span>
1. [<span data-ttu-id="724c4-170">Экспорт сертификата шифрования из хранилища сертификатов</span><span class="sxs-lookup"><span data-stu-id="724c4-170">Export Encryption Certificate From Certificate Store</span></span>](#export-encryption-certificate-from-certificate-store)
2. [<span data-ttu-id="724c4-171">Отправить сертификат шифрования tooCloud службы</span><span class="sxs-lookup"><span data-stu-id="724c4-171">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
3. [<span data-ttu-id="724c4-172">Обновление сертификата шифрования в файле конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="724c4-172">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="724c4-173">Использование существующего сертификата в PFX-файле</span><span class="sxs-lookup"><span data-stu-id="724c4-173">Use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="724c4-174">Отправить сертификат шифрования tooCloud службы</span><span class="sxs-lookup"><span data-stu-id="724c4-174">Upload Encryption Certificate tooCloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
2. [<span data-ttu-id="724c4-175">Обновление сертификата шифрования в файле конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="724c4-175">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

## <a name="hello-default-configuration"></a><span data-ttu-id="724c4-176">Конфигурация по умолчанию Hello</span><span class="sxs-lookup"><span data-stu-id="724c4-176">hello default configuration</span></span>
<span data-ttu-id="724c4-177">Конфигурация по умолчанию Hello запрещает все конечной точки HTTP toohello доступа.</span><span class="sxs-lookup"><span data-stu-id="724c4-177">hello default configuration denies all access toohello HTTP endpoint.</span></span> <span data-ttu-id="724c4-178">Это hello, рекомендуется, поскольку конечные точки toothese запросы hello может содержать конфиденциальные сведения, такие как учетные данные базы данных.</span><span class="sxs-lookup"><span data-stu-id="724c4-178">This is hello recommended setting, since hello requests toothese endpoints may carry sensitive information like database credentials.</span></span>
<span data-ttu-id="724c4-179">Конфигурация по умолчанию Hello позволяет конечной точки HTTPS все toohello доступа.</span><span class="sxs-lookup"><span data-stu-id="724c4-179">hello default configuration allows all access toohello HTTPS endpoint.</span></span> <span data-ttu-id="724c4-180">Этот параметр в дальнейшем может быть ограничен.</span><span class="sxs-lookup"><span data-stu-id="724c4-180">This setting may be restricted further.</span></span>

### <a name="changing-hello-configuration"></a><span data-ttu-id="724c4-181">Изменение конфигурации hello</span><span class="sxs-lookup"><span data-stu-id="724c4-181">Changing hello Configuration</span></span>
<span data-ttu-id="724c4-182">Hello группы правил управления доступом, применяемые tooand конечной точки настраиваются в hello  **<EndpointAcls>**  раздела hello **файла конфигурации службы**.</span><span class="sxs-lookup"><span data-stu-id="724c4-182">hello group of access control rules that apply tooand endpoint are configured in hello **<EndpointAcls>** section in hello **service configuration file**.</span></span>

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

<span data-ttu-id="724c4-183">Hello правила в группе управления доступом настраиваются в <AccessControl name=""> раздел файла конфигурации службы hello.</span><span class="sxs-lookup"><span data-stu-id="724c4-183">hello rules in an access control group are configured in a <AccessControl name=""> section of hello service configuration file.</span></span> 

<span data-ttu-id="724c4-184">Формат Hello описан в документации списки управления сетевым доступом.</span><span class="sxs-lookup"><span data-stu-id="724c4-184">hello format is explained in Network Access Control Lists documentation.</span></span>
<span data-ttu-id="724c4-185">Например, tooallow только IP-адреса в hello 100.100.0.0 too100.100.255.255 tooaccess hello HTTPS конечная точка диапазона, hello правила может выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="724c4-185">For example, tooallow only IPs in hello range 100.100.0.0 too100.100.255.255 tooaccess hello HTTPS endpoint, hello rules would look like this:</span></span>

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a><span data-ttu-id="724c4-186">Предотвращение отказа в обслуживании</span><span class="sxs-lookup"><span data-stu-id="724c4-186">Denial of service prevention</span></span>
<span data-ttu-id="724c4-187">Существует два разных механизма поддерживается toodetect и предотвратить атаки отказа в обслуживании:</span><span class="sxs-lookup"><span data-stu-id="724c4-187">There are two different mechanisms supported toodetect and prevent Denial of Service attacks:</span></span>

* <span data-ttu-id="724c4-188">Ограничение количества одновременных запросов на удаленный узел (по умолчанию отключено)</span><span class="sxs-lookup"><span data-stu-id="724c4-188">Restrict number of concurrent requests per remote host (off by default)</span></span>
* <span data-ttu-id="724c4-189">Ограничение частоты доступа в расчете на удаленный узел (включено по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="724c4-189">Restrict rate of access per remote host (on by default)</span></span>

<span data-ttu-id="724c4-190">Они основаны на функции hello в динамических IP-безопасности в службах IIS.</span><span class="sxs-lookup"><span data-stu-id="724c4-190">These are based on hello features further documented in Dynamic IP Security in IIS.</span></span> <span data-ttu-id="724c4-191">При изменении этой конфигурации Учтите, что hello следующие факторы:</span><span class="sxs-lookup"><span data-stu-id="724c4-191">When changing this configuration beware of hello following factors:</span></span>

* <span data-ttu-id="724c4-192">поведение Hello прокси-серверы и устройства преобразования сетевых адресов над сведениями о hello удаленного узла</span><span class="sxs-lookup"><span data-stu-id="724c4-192">hello behavior of proxies and Network Address Translation devices over hello remote host information</span></span>
* <span data-ttu-id="724c4-193">Ресурс tooany каждого запроса в веб-роли hello считается (например загрузки скриптов, изображения, и т.д.)</span><span class="sxs-lookup"><span data-stu-id="724c4-193">Each request tooany resource in hello web role is considered (e.g. loading scripts, images, etc)</span></span>

## <a name="restricting-number-of-concurrent-accesses"></a><span data-ttu-id="724c4-194">Ограничение числа одновременных обращений</span><span class="sxs-lookup"><span data-stu-id="724c4-194">Restricting number of concurrent accesses</span></span>
<span data-ttu-id="724c4-195">Привет, настройки этого поведения следующие значения.</span><span class="sxs-lookup"><span data-stu-id="724c4-195">hello settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

<span data-ttu-id="724c4-196">Измените DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable защиту.</span><span class="sxs-lookup"><span data-stu-id="724c4-196">Change DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable this protection.</span></span>

## <a name="restricting-rate-of-access"></a><span data-ttu-id="724c4-197">Ограничение частоты доступа</span><span class="sxs-lookup"><span data-stu-id="724c4-197">Restricting rate of access</span></span>
<span data-ttu-id="724c4-198">Привет, настройки этого поведения следующие значения.</span><span class="sxs-lookup"><span data-stu-id="724c4-198">hello settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-hello-response-tooa-denied-request"></a><span data-ttu-id="724c4-199">Настройка tooa ответа hello отклонил запрос</span><span class="sxs-lookup"><span data-stu-id="724c4-199">Configuring hello response tooa denied request</span></span>
<span data-ttu-id="724c4-200">Hello следующий параметр настраивает hello ответа tooa отклонил запрос:</span><span class="sxs-lookup"><span data-stu-id="724c4-200">hello following setting configures hello response tooa denied request:</span></span>

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
<span data-ttu-id="724c4-201">См. документацию toohello динамических IP-безопасности в службах IIS для других поддерживаемых значений.</span><span class="sxs-lookup"><span data-stu-id="724c4-201">Refer toohello documentation for Dynamic IP Security in IIS for other supported values.</span></span>

## <a name="operations-for-configuring-service-certificates"></a><span data-ttu-id="724c4-202">Операции настройки службы сертификатов</span><span class="sxs-lookup"><span data-stu-id="724c4-202">Operations for configuring service certificates</span></span>
<span data-ttu-id="724c4-203">Этот раздел предназначен только для справки.</span><span class="sxs-lookup"><span data-stu-id="724c4-203">This topic is for reference only.</span></span> <span data-ttu-id="724c4-204">Выполните этапы настройки hello, описанные в.</span><span class="sxs-lookup"><span data-stu-id="724c4-204">Please follow hello configuration steps outlined in:</span></span>

* <span data-ttu-id="724c4-205">Настройка SSL-сертификата hello</span><span class="sxs-lookup"><span data-stu-id="724c4-205">Configure hello SSL certificate</span></span>
* <span data-ttu-id="724c4-206">Настройка сертификатов клиентов</span><span class="sxs-lookup"><span data-stu-id="724c4-206">Configure client certificates</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="724c4-207">Создание самозаверяющего сертификата</span><span class="sxs-lookup"><span data-stu-id="724c4-207">Create a self-signed certificate</span></span>
<span data-ttu-id="724c4-208">Выполните:</span><span class="sxs-lookup"><span data-stu-id="724c4-208">Execute:</span></span>

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

<span data-ttu-id="724c4-209">toocustomize:</span><span class="sxs-lookup"><span data-stu-id="724c4-209">toocustomize:</span></span>

* <span data-ttu-id="724c4-210">URL-адрес службы - n с hello.</span><span class="sxs-lookup"><span data-stu-id="724c4-210">-n with hello service URL.</span></span> <span data-ttu-id="724c4-211">Поддерживаются подстановочные знаки ("CN=*.cloudapp.net") и альтернативные имена ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net").</span><span class="sxs-lookup"><span data-stu-id="724c4-211">Wildcards ("CN=*.cloudapp.net") and alternative names ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") are supported.</span></span>
* <span data-ttu-id="724c4-212">-e с датой окончания срока действия сертификата hello создать надежный пароль и укажите его при появлении запроса.</span><span class="sxs-lookup"><span data-stu-id="724c4-212">-e with hello certificate expiration date Create a strong password and specify it when prompted.</span></span>

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a><span data-ttu-id="724c4-213">Создание PFX-файла для самозаверяющего SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="724c4-213">Create PFX file for self-signed SSL certificate</span></span>
<span data-ttu-id="724c4-214">Выполните:</span><span class="sxs-lookup"><span data-stu-id="724c4-214">Execute:</span></span>

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

<span data-ttu-id="724c4-215">Введите пароль, а затем экспортируйте сертификат с этими параметрами.</span><span class="sxs-lookup"><span data-stu-id="724c4-215">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="724c4-216">Да, экспортировать закрытый ключ hello</span><span class="sxs-lookup"><span data-stu-id="724c4-216">Yes, export hello private key</span></span>
* <span data-ttu-id="724c4-217">Экспортировать все расширенные свойства.</span><span class="sxs-lookup"><span data-stu-id="724c4-217">Export all extended properties</span></span>

## <a name="export-ssl-certificate-from-certificate-store"></a><span data-ttu-id="724c4-218">Экспорт SSL-сертификата из хранилища сертификатов</span><span class="sxs-lookup"><span data-stu-id="724c4-218">Export SSL certificate from certificate store</span></span>
* <span data-ttu-id="724c4-219">Поиск сертификата</span><span class="sxs-lookup"><span data-stu-id="724c4-219">Find certificate</span></span>
* <span data-ttu-id="724c4-220">Выберите «Действия > Все задачи > Экспортировать…»</span><span class="sxs-lookup"><span data-stu-id="724c4-220">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="724c4-221">Экспортируйте сертификат в PFX-файл со следующими параметрами.</span><span class="sxs-lookup"><span data-stu-id="724c4-221">Export certificate into a .PFX file with these options:</span></span>
  * <span data-ttu-id="724c4-222">Да, экспортировать закрытый ключ hello</span><span class="sxs-lookup"><span data-stu-id="724c4-222">Yes, export hello private key</span></span>
  * <span data-ttu-id="724c4-223">Включить по возможности все сертификаты в путь сертификации hello * экспортировать все расширенные свойства</span><span class="sxs-lookup"><span data-stu-id="724c4-223">Include all certificates in hello certification path if possible *Export all extended properties</span></span>

## <a name="upload-ssl-certificate-toocloud-service"></a><span data-ttu-id="724c4-224">Отправить службе toocloud сертификат SSL</span><span class="sxs-lookup"><span data-stu-id="724c4-224">Upload SSL certificate toocloud service</span></span>
<span data-ttu-id="724c4-225">Отправьте сертификат с hello существующий или создан. PFX-файл с hello пары ключей SSL:</span><span class="sxs-lookup"><span data-stu-id="724c4-225">Upload certificate with hello existing or generated .PFX file with hello SSL key pair:</span></span>

* <span data-ttu-id="724c4-226">Введите пароль hello для защиты информации о закрытом ключе hello</span><span class="sxs-lookup"><span data-stu-id="724c4-226">Enter hello password protecting hello private key information</span></span>

## <a name="update-ssl-certificate-in-service-configuration-file"></a><span data-ttu-id="724c4-227">Обновление SSL-сертификата в файле конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="724c4-227">Update SSL certificate in service configuration file</span></span>
<span data-ttu-id="724c4-228">Обновите значения отпечатка hello hello следующий параметр в файле конфигурации службы hello с отпечатком hello hello сертификат, переданный toohello облачной службы:</span><span class="sxs-lookup"><span data-stu-id="724c4-228">Update hello thumbprint value of hello following setting in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a><span data-ttu-id="724c4-229">Импорт центра сертификации SSL</span><span class="sxs-lookup"><span data-stu-id="724c4-229">Import SSL certification authority</span></span>
<span data-ttu-id="724c4-230">Выполните следующие действия в все учетной записи или компьютера, которым будет связываться со службой hello.</span><span class="sxs-lookup"><span data-stu-id="724c4-230">Follow these steps in all account/machine that will communicate with hello service:</span></span>

* <span data-ttu-id="724c4-231">Дважды щелкните значок "hello". CER-файл в проводнике Windows</span><span class="sxs-lookup"><span data-stu-id="724c4-231">Double-click hello .CER file in Windows Explorer</span></span>
* <span data-ttu-id="724c4-232">В диалоговом окне приветствия сертификат нажмите кнопку "установить сертификат"...</span><span class="sxs-lookup"><span data-stu-id="724c4-232">In hello Certificate dialog, click Install Certificate…</span></span>
* <span data-ttu-id="724c4-233">Импортируйте сертификат в хранилище доверенных корневых центров сертификации приветствия</span><span class="sxs-lookup"><span data-stu-id="724c4-233">Import certificate into hello Trusted Root Certification Authorities store</span></span>

## <a name="turn-off-client-certificate-based-authentication"></a><span data-ttu-id="724c4-234">Отключение аутентификации на основе сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="724c4-234">Turn off client certificate-based authentication</span></span>
<span data-ttu-id="724c4-235">Поддерживается только на основе сертификатов проверки подлинности клиента и его отключение позволит для конечных точек службы toohello общего доступа, если не предусмотрены другие механизмы на месте (например виртуальная сеть Microsoft Azure).</span><span class="sxs-lookup"><span data-stu-id="724c4-235">Only client certificate-based authentication is supported and disabling it will allow for public access toohello service endpoints, unless other mechanisms are in place (e.g. Microsoft Azure Virtual Network).</span></span>

<span data-ttu-id="724c4-236">Измените toofalse этих параметров в функции hello tooturn файла конфигурации hello службы из системы:</span><span class="sxs-lookup"><span data-stu-id="724c4-236">Change these settings toofalse in hello service configuration file tooturn hello feature off:</span></span>

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

<span data-ttu-id="724c4-237">Затем скопируйте hello же отпечатком, что hello SSL-сертификата в приветствия ЦС сертификата:</span><span class="sxs-lookup"><span data-stu-id="724c4-237">Then, copy hello same thumbprint as hello SSL certificate in hello CA certificate setting:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a><span data-ttu-id="724c4-238">Создание центра самозаверяющей сертификации</span><span class="sxs-lookup"><span data-stu-id="724c4-238">Create a self-signed certification authority</span></span>
<span data-ttu-id="724c4-239">Выполните следующие шаги toocreate tooact самозаверяющий сертификат, как центр сертификации hello:</span><span class="sxs-lookup"><span data-stu-id="724c4-239">Execute hello following steps toocreate a self-signed certificate tooact as a Certification Authority:</span></span>

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

<span data-ttu-id="724c4-240">toocustomize его</span><span class="sxs-lookup"><span data-stu-id="724c4-240">toocustomize it</span></span>

* <span data-ttu-id="724c4-241">-e с датой окончания срока действия сертификации hello</span><span class="sxs-lookup"><span data-stu-id="724c4-241">-e with hello certification expiration date</span></span>

## <a name="find-ca-public-key"></a><span data-ttu-id="724c4-242">Поиск открытого ключа ЦС</span><span class="sxs-lookup"><span data-stu-id="724c4-242">Find CA public key</span></span>
<span data-ttu-id="724c4-243">Все сертификаты клиента должен быть выдан центром сертификации, доверенным для службы hello.</span><span class="sxs-lookup"><span data-stu-id="724c4-243">All client certificates must have been issued by a Certification Authority trusted by hello service.</span></span> <span data-ttu-id="724c4-244">Найти открытого ключа toohello hello центра сертификации, выдавшего hello клиентских сертификатов, которые будут toobe для проверки подлинности в порядке tooupload его toohello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="724c4-244">Find hello public key toohello Certification Authority that issued hello client certificates that are going toobe used for authentication in order tooupload it toohello cloud service.</span></span>

<span data-ttu-id="724c4-245">Если файл hello открытым ключом hello недоступен, экспортируйте его из хранилища сертификатов hello:</span><span class="sxs-lookup"><span data-stu-id="724c4-245">If hello file with hello public key is not available, export it from hello certificate store:</span></span>

* <span data-ttu-id="724c4-246">Поиск сертификата</span><span class="sxs-lookup"><span data-stu-id="724c4-246">Find certificate</span></span>
  * <span data-ttu-id="724c4-247">Найдите сертификат клиента, выданный hello же центром сертификации</span><span class="sxs-lookup"><span data-stu-id="724c4-247">Search for a client certificate issued by hello same Certification Authority</span></span>
* <span data-ttu-id="724c4-248">Дважды щелкните сертификат hello.</span><span class="sxs-lookup"><span data-stu-id="724c4-248">Double-click hello certificate.</span></span>
* <span data-ttu-id="724c4-249">Перейдите на вкладку путь сертификации hello в диалоговом окне приветствия сертификата.</span><span class="sxs-lookup"><span data-stu-id="724c4-249">Select hello Certification Path tab in hello Certificate dialog.</span></span>
* <span data-ttu-id="724c4-250">Дважды щелкните запись ЦС hello в пути hello.</span><span class="sxs-lookup"><span data-stu-id="724c4-250">Double-click hello CA entry in hello path.</span></span>
* <span data-ttu-id="724c4-251">Запишите свойства сертификата hello.</span><span class="sxs-lookup"><span data-stu-id="724c4-251">Take notes of hello certificate properties.</span></span>
* <span data-ttu-id="724c4-252">Закрыть hello **сертификат** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="724c4-252">Close hello **Certificate** dialog.</span></span>
* <span data-ttu-id="724c4-253">Поиск сертификата</span><span class="sxs-lookup"><span data-stu-id="724c4-253">Find certificate</span></span>
  * <span data-ttu-id="724c4-254">Поиск hello ЦС, указанным выше.</span><span class="sxs-lookup"><span data-stu-id="724c4-254">Search for hello CA noted above.</span></span>
* <span data-ttu-id="724c4-255">Выберите «Действия > Все задачи > Экспортировать…»</span><span class="sxs-lookup"><span data-stu-id="724c4-255">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="724c4-256">Экспортируйте сертификат в .CER с этими параметрами:</span><span class="sxs-lookup"><span data-stu-id="724c4-256">Export certificate into a .CER with these options:</span></span>
  * <span data-ttu-id="724c4-257">**Нет, не экспортировать закрытый ключ hello**</span><span class="sxs-lookup"><span data-stu-id="724c4-257">**No, do not export hello private key**</span></span>
  * <span data-ttu-id="724c4-258">Включить по возможности все сертификаты в путь сертификации hello.</span><span class="sxs-lookup"><span data-stu-id="724c4-258">Include all certificates in hello certification path if possible.</span></span>
  * <span data-ttu-id="724c4-259">Экспортировать все расширенные свойства.</span><span class="sxs-lookup"><span data-stu-id="724c4-259">Export all extended properties.</span></span>

## <a name="upload-ca-certificate-toocloud-service"></a><span data-ttu-id="724c4-260">Отправка службы toocloud сертификата ЦС</span><span class="sxs-lookup"><span data-stu-id="724c4-260">Upload CA certificate toocloud service</span></span>
<span data-ttu-id="724c4-261">Отправьте сертификат с hello существующий или создан. CER-файл с помощью открытого ключа ЦС hello.</span><span class="sxs-lookup"><span data-stu-id="724c4-261">Upload certificate with hello existing or generated .CER file with hello CA public key.</span></span>

## <a name="update-ca-certificate-in-service-configuration-file"></a><span data-ttu-id="724c4-262">Обновление сертификата ЦС в файле конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="724c4-262">Update CA certificate in service configuration file</span></span>
<span data-ttu-id="724c4-263">Обновите значения отпечатка hello hello следующий параметр в файле конфигурации службы hello с отпечатком hello hello сертификат, переданный toohello облачной службы:</span><span class="sxs-lookup"><span data-stu-id="724c4-263">Update hello thumbprint value of hello following setting in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

<span data-ttu-id="724c4-264">Обновите значение hello hello после установки с hello же отпечаток:</span><span class="sxs-lookup"><span data-stu-id="724c4-264">Update hello value of hello following setting with hello same thumbprint:</span></span>

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a><span data-ttu-id="724c4-265">Выдача сертификатов клиентов</span><span class="sxs-lookup"><span data-stu-id="724c4-265">Issue client certificates</span></span>
<span data-ttu-id="724c4-266">Каждая служба hello отдельных авторизованным tooaccess должен иметь клиентского сертификата, выданного для his/hers монопольного использования и следует выбрать his/hers владеет закрытым ключом tooprotect надежный пароль.</span><span class="sxs-lookup"><span data-stu-id="724c4-266">Each individual authorized tooaccess hello service should have a client certificate issued for his/hers exclusive use and should choose his/hers own strong password tooprotect its private key.</span></span> 

<span data-ttu-id="724c4-267">следующие шаги Hello должен выполняться в hello же компьютере, где самоподписанный сертификат ЦС hello был автоматически и хранится:</span><span class="sxs-lookup"><span data-stu-id="724c4-267">hello following steps must be executed in hello same machine where hello self-signed CA certificate was generated and stored:</span></span>

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

<span data-ttu-id="724c4-268">Настройка.</span><span class="sxs-lookup"><span data-stu-id="724c4-268">Customizing:</span></span>

* <span data-ttu-id="724c4-269">-n с Идентификатором toohello клиента, который будет проходить проверку подлинности с помощью этого сертификата</span><span class="sxs-lookup"><span data-stu-id="724c4-269">-n with an ID for toohello client that will be authenticated with this certificate</span></span>
* <span data-ttu-id="724c4-270">-e с датой окончания срока действия сертификата hello</span><span class="sxs-lookup"><span data-stu-id="724c4-270">-e with hello certificate expiration date</span></span>
* <span data-ttu-id="724c4-271">MyID.pvk и MyID.cer с уникальными именами файлов для этого сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="724c4-271">MyID.pvk and MyID.cer with unique filenames for this client certificate</span></span>

<span data-ttu-id="724c4-272">Эта команда предложит ввести пароль toobe и затем использовать его один раз.</span><span class="sxs-lookup"><span data-stu-id="724c4-272">This command will prompt for a password toobe created and then used once.</span></span> <span data-ttu-id="724c4-273">Используйте надежный пароль.</span><span class="sxs-lookup"><span data-stu-id="724c4-273">Use a strong password.</span></span>

## <a name="create-pfx-files-for-client-certificates"></a><span data-ttu-id="724c4-274">Создание PFX-файлов для сертификатов клиента</span><span class="sxs-lookup"><span data-stu-id="724c4-274">Create PFX files for client certificates</span></span>
<span data-ttu-id="724c4-275">Для каждого созданного сертификата клиента выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="724c4-275">For each generated client certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="724c4-276">Настройка.</span><span class="sxs-lookup"><span data-stu-id="724c4-276">Customizing:</span></span>

    MyID.pvk and MyID.cer with hello filename for hello client certificate

<span data-ttu-id="724c4-277">Введите пароль, а затем экспортируйте сертификат с этими параметрами.</span><span class="sxs-lookup"><span data-stu-id="724c4-277">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="724c4-278">Да, экспортировать закрытый ключ hello</span><span class="sxs-lookup"><span data-stu-id="724c4-278">Yes, export hello private key</span></span>
* <span data-ttu-id="724c4-279">Экспортировать все расширенные свойства.</span><span class="sxs-lookup"><span data-stu-id="724c4-279">Export all extended properties</span></span>
* <span data-ttu-id="724c4-280">toowhom отдельных Hello, этот сертификат необходимо выбрать пароль экспорта hello</span><span class="sxs-lookup"><span data-stu-id="724c4-280">hello individual toowhom this certificate is being issued should choose hello export password</span></span>

## <a name="import-client-certificate"></a><span data-ttu-id="724c4-281">Импорт сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="724c4-281">Import client certificate</span></span>
<span data-ttu-id="724c4-282">Каждого пользователя, для которого была выполнена клиентский сертификат следует импортировать пару ключей hello в hello машины он будет использоваться toocommunicate со службой hello:</span><span class="sxs-lookup"><span data-stu-id="724c4-282">Each individual for whom a client certificate has been issued should import hello key pair in hello machines he/she will use toocommunicate with hello service:</span></span>

* <span data-ttu-id="724c4-283">Дважды щелкните значок "hello". PFX-файла в проводнике Windows</span><span class="sxs-lookup"><span data-stu-id="724c4-283">Double-click hello .PFX file in Windows Explorer</span></span>
* <span data-ttu-id="724c4-284">Импортируйте сертификат в личном хранилище с по крайней мере этот параметр hello:</span><span class="sxs-lookup"><span data-stu-id="724c4-284">Import certificate into hello Personal store with at least this option:</span></span>
  * <span data-ttu-id="724c4-285">Включить все расширенные свойства проверки</span><span class="sxs-lookup"><span data-stu-id="724c4-285">Include all extended properties checked</span></span>

## <a name="copy-client-certificate-thumbprints"></a><span data-ttu-id="724c4-286">Копирование отпечатков сертификатов клиента</span><span class="sxs-lookup"><span data-stu-id="724c4-286">Copy client certificate thumbprints</span></span>
<span data-ttu-id="724c4-287">Каждого пользователя, которому выдан сертификат клиента необходимо выполнить следующие действия в порядке tooobtain hello отпечаток his/hers сертификат, который будет добавлен файл конфигурации службы toohello:</span><span class="sxs-lookup"><span data-stu-id="724c4-287">Each individual for whom a client certificate has been issued must follow these steps in order tooobtain hello thumbprint of his/hers certificate which will be added toohello service configuration file:</span></span>

* <span data-ttu-id="724c4-288">Запустите certmgr.exe</span><span class="sxs-lookup"><span data-stu-id="724c4-288">Run certmgr.exe</span></span>
* <span data-ttu-id="724c4-289">Выберите вкладку личные hello</span><span class="sxs-lookup"><span data-stu-id="724c4-289">Select hello Personal tab</span></span>
* <span data-ttu-id="724c4-290">Дважды щелкните toobe, используемый для проверки подлинности сертификата клиента hello</span><span class="sxs-lookup"><span data-stu-id="724c4-290">Double-click hello client certificate toobe used for authentication</span></span>
* <span data-ttu-id="724c4-291">В диалоговом окне сертификата hello, которое открывается перейдите на вкладку сведения hello</span><span class="sxs-lookup"><span data-stu-id="724c4-291">In hello Certificate dialog that opens, select hello Details tab</span></span>
* <span data-ttu-id="724c4-292">Убедитесь, что в разделе "Показать" выбран вариант "Все"</span><span class="sxs-lookup"><span data-stu-id="724c4-292">Make sure Show is displaying All</span></span>
* <span data-ttu-id="724c4-293">Выберите hello поле с именем отпечаток в списке hello</span><span class="sxs-lookup"><span data-stu-id="724c4-293">Select hello field named Thumbprint in hello list</span></span>
* <span data-ttu-id="724c4-294">Скопируйте значение hello отпечаток hello ** удалить неотображаемых символов Юникода перед первой цифры hello ** удалите все пробелы</span><span class="sxs-lookup"><span data-stu-id="724c4-294">Copy hello value of hello thumbprint ** Delete non-visible Unicode characters in front of hello first digit ** Delete all spaces</span></span>

## <a name="configure-allowed-clients-in-hello-service-configuration-file"></a><span data-ttu-id="724c4-295">Настройка клиентов разрешено в файле конфигурации службы hello</span><span class="sxs-lookup"><span data-stu-id="724c4-295">Configure Allowed clients in hello service configuration file</span></span>
<span data-ttu-id="724c4-296">Обновите значение hello hello следующий параметр в файле конфигурации службы hello с запятыми список hello отпечатки сертификатов клиента hello допускается toohello службы доступа к:</span><span class="sxs-lookup"><span data-stu-id="724c4-296">Update hello value of hello following setting in hello service configuration file with a comma-separated list of hello thumbprints of hello client certificates allowed access toohello service:</span></span>

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a><span data-ttu-id="724c4-297">Настройка проверки отзыва сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="724c4-297">Configure client certificate revocation check</span></span>
<span data-ttu-id="724c4-298">по умолчанию Hello не проверяет с hello центра сертификации для проверки состояния отзыва сертификата клиента.</span><span class="sxs-lookup"><span data-stu-id="724c4-298">hello default setting does not check with hello Certification Authority for client certificate revocation status.</span></span> <span data-ttu-id="724c4-299">проверяет tooturn на hello, если hello центр сертификации, выдавший сертификаты клиента hello, который поддерживает такие проверки, измените следующий параметр с одним из значений hello, определенные в hello перечисления X509RevocationMode hello.</span><span class="sxs-lookup"><span data-stu-id="724c4-299">tooturn on hello checks, if hello Certification Authority which issued hello client certificates supports such checks, change hello following setting with one of hello values defined in hello X509RevocationMode Enumeration:</span></span>

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a><span data-ttu-id="724c4-300">Создание PFX-файла для самозаверяющих сертификатов шифрования</span><span class="sxs-lookup"><span data-stu-id="724c4-300">Create PFX file for self-signed encryption certificates</span></span>
<span data-ttu-id="724c4-301">Для сертификата шифрования выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="724c4-301">For an encryption certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="724c4-302">Настройка.</span><span class="sxs-lookup"><span data-stu-id="724c4-302">Customizing:</span></span>

    MyID.pvk and MyID.cer with hello filename for hello encryption certificate

<span data-ttu-id="724c4-303">Введите пароль, а затем экспортируйте сертификат с этими параметрами.</span><span class="sxs-lookup"><span data-stu-id="724c4-303">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="724c4-304">Да, экспортировать закрытый ключ hello</span><span class="sxs-lookup"><span data-stu-id="724c4-304">Yes, export hello private key</span></span>
* <span data-ttu-id="724c4-305">Экспортировать все расширенные свойства.</span><span class="sxs-lookup"><span data-stu-id="724c4-305">Export all extended properties</span></span>
* <span data-ttu-id="724c4-306">Hello пароль будет нужен при передаче hello сертификат toohello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="724c4-306">You will need hello password when uploading hello certificate toohello cloud service.</span></span>

## <a name="export-encryption-certificate-from-certificate-store"></a><span data-ttu-id="724c4-307">Экспорт сертификата шифрования из хранилища сертификатов</span><span class="sxs-lookup"><span data-stu-id="724c4-307">Export encryption certificate from certificate store</span></span>
* <span data-ttu-id="724c4-308">Поиск сертификата</span><span class="sxs-lookup"><span data-stu-id="724c4-308">Find certificate</span></span>
* <span data-ttu-id="724c4-309">Выберите «Действия > Все задачи > Экспортировать…»</span><span class="sxs-lookup"><span data-stu-id="724c4-309">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="724c4-310">Экспортируйте сертификат в PFX-файл со следующими параметрами.</span><span class="sxs-lookup"><span data-stu-id="724c4-310">Export certificate into a .PFX file with these options:</span></span> 
  * <span data-ttu-id="724c4-311">Да, экспортировать закрытый ключ hello</span><span class="sxs-lookup"><span data-stu-id="724c4-311">Yes, export hello private key</span></span>
  * <span data-ttu-id="724c4-312">Включить по возможности все сертификаты в путь сертификации hello</span><span class="sxs-lookup"><span data-stu-id="724c4-312">Include all certificates in hello certification path if possible</span></span> 
* <span data-ttu-id="724c4-313">Экспортировать все расширенные свойства.</span><span class="sxs-lookup"><span data-stu-id="724c4-313">Export all extended properties</span></span>

## <a name="upload-encryption-certificate-toocloud-service"></a><span data-ttu-id="724c4-314">Служба toocloud сертификат шифрования отправки</span><span class="sxs-lookup"><span data-stu-id="724c4-314">Upload encryption certificate toocloud service</span></span>
<span data-ttu-id="724c4-315">Отправьте сертификат с hello существующий или создан. PFX-файл с hello пару ключей шифрования:</span><span class="sxs-lookup"><span data-stu-id="724c4-315">Upload certificate with hello existing or generated .PFX file with hello encryption key pair:</span></span>

* <span data-ttu-id="724c4-316">Введите пароль hello для защиты информации о закрытом ключе hello</span><span class="sxs-lookup"><span data-stu-id="724c4-316">Enter hello password protecting hello private key information</span></span>

## <a name="update-encryption-certificate-in-service-configuration-file"></a><span data-ttu-id="724c4-317">Обновление сертификата шифрования в файле конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="724c4-317">Update encryption certificate in service configuration file</span></span>
<span data-ttu-id="724c4-318">Обновите значения отпечатка hello hello следующие параметры в файле конфигурации службы hello с отпечатком hello hello сертификат, переданный toohello облачной службы:</span><span class="sxs-lookup"><span data-stu-id="724c4-318">Update hello thumbprint value of hello following settings in hello service configuration file with hello thumbprint of hello certificate uploaded toohello cloud service:</span></span>

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a><span data-ttu-id="724c4-319">Стандартные операции сертификата</span><span class="sxs-lookup"><span data-stu-id="724c4-319">Common certificate operations</span></span>
* <span data-ttu-id="724c4-320">Настройка SSL-сертификата hello</span><span class="sxs-lookup"><span data-stu-id="724c4-320">Configure hello SSL certificate</span></span>
* <span data-ttu-id="724c4-321">Настройка сертификатов клиентов</span><span class="sxs-lookup"><span data-stu-id="724c4-321">Configure client certificates</span></span>

## <a name="find-certificate"></a><span data-ttu-id="724c4-322">Поиск сертификата</span><span class="sxs-lookup"><span data-stu-id="724c4-322">Find certificate</span></span>
<span data-ttu-id="724c4-323">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="724c4-323">Follow these steps:</span></span>

1. <span data-ttu-id="724c4-324">Запустите mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="724c4-324">Run mmc.exe.</span></span>
2. <span data-ttu-id="724c4-325">Файл -> Добавить/удалить оснастку...</span><span class="sxs-lookup"><span data-stu-id="724c4-325">File -> Add/Remove Snap-in…</span></span>
3. <span data-ttu-id="724c4-326">Выберите **Сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="724c4-326">Select **Certificates**.</span></span>
4. <span data-ttu-id="724c4-327">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="724c4-327">Click **Add**.</span></span>
5. <span data-ttu-id="724c4-328">Выберите расположение хранилища сертификатов hello.</span><span class="sxs-lookup"><span data-stu-id="724c4-328">Choose hello certificate store location.</span></span>
6. <span data-ttu-id="724c4-329">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="724c4-329">Click **Finish**.</span></span>
7. <span data-ttu-id="724c4-330">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="724c4-330">Click **OK**.</span></span>
8. <span data-ttu-id="724c4-331">Разверните узел **Сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="724c4-331">Expand **Certificates**.</span></span>
9. <span data-ttu-id="724c4-332">Разверните узел хранилища сертификатов hello.</span><span class="sxs-lookup"><span data-stu-id="724c4-332">Expand hello certificate store node.</span></span>
10. <span data-ttu-id="724c4-333">Разверните hello сертификат дочерний узел.</span><span class="sxs-lookup"><span data-stu-id="724c4-333">Expand hello Certificate child node.</span></span>
11. <span data-ttu-id="724c4-334">Выберите сертификат в списке hello.</span><span class="sxs-lookup"><span data-stu-id="724c4-334">Select a certificate in hello list.</span></span>

## <a name="export-certificate"></a><span data-ttu-id="724c4-335">Экспорт сертификата</span><span class="sxs-lookup"><span data-stu-id="724c4-335">Export certificate</span></span>
<span data-ttu-id="724c4-336">В hello **мастера экспорта сертификатов**:</span><span class="sxs-lookup"><span data-stu-id="724c4-336">In hello **Certificate Export Wizard**:</span></span>

1. <span data-ttu-id="724c4-337">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="724c4-337">Click **Next**.</span></span>
2. <span data-ttu-id="724c4-338">Выберите **Да**, затем **экспорта hello закрытый ключ**.</span><span class="sxs-lookup"><span data-stu-id="724c4-338">Select **Yes**, then **Export hello private key**.</span></span>
3. <span data-ttu-id="724c4-339">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="724c4-339">Click **Next**.</span></span>
4. <span data-ttu-id="724c4-340">Выберите формат файла hello нужный результат.</span><span class="sxs-lookup"><span data-stu-id="724c4-340">Select hello desired output file format.</span></span>
5. <span data-ttu-id="724c4-341">Проверьте параметры требуемого hello.</span><span class="sxs-lookup"><span data-stu-id="724c4-341">Check hello desired options.</span></span>
6. <span data-ttu-id="724c4-342">Проверьте **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="724c4-342">Check **Password**.</span></span>
7. <span data-ttu-id="724c4-343">Введите надежный пароль и подтвердите его.</span><span class="sxs-lookup"><span data-stu-id="724c4-343">Enter a strong password and confirm it.</span></span>
8. <span data-ttu-id="724c4-344">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="724c4-344">Click **Next**.</span></span>
9. <span data-ttu-id="724c4-345">Введите или выберите имя файла, где toostore hello сертификата (использование. Расширение PFX).</span><span class="sxs-lookup"><span data-stu-id="724c4-345">Type or browse a filename where toostore hello certificate (use a .PFX extension).</span></span>
10. <span data-ttu-id="724c4-346">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="724c4-346">Click **Next**.</span></span>
11. <span data-ttu-id="724c4-347">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="724c4-347">Click **Finish**.</span></span>
12. <span data-ttu-id="724c4-348">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="724c4-348">Click **OK**.</span></span>

## <a name="import-certificate"></a><span data-ttu-id="724c4-349">Импорт сертификата</span><span class="sxs-lookup"><span data-stu-id="724c4-349">Import certificate</span></span>
<span data-ttu-id="724c4-350">В окне приветствия мастера импорта сертификатов:</span><span class="sxs-lookup"><span data-stu-id="724c4-350">In hello Certificate Import Wizard:</span></span>

1. <span data-ttu-id="724c4-351">Выберите расположение хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="724c4-351">Select hello store location.</span></span>
   
   * <span data-ttu-id="724c4-352">Выберите **текущего пользователя** если только для процессов, выполняемых в рамках текущего пользователя будет доступ к службе hello</span><span class="sxs-lookup"><span data-stu-id="724c4-352">Select **Current User** if only processes running under current user will access hello service</span></span>
   * <span data-ttu-id="724c4-353">Выберите **локального компьютера** Если другие процессы на этом компьютере будет получить доступ к службе hello</span><span class="sxs-lookup"><span data-stu-id="724c4-353">Select **Local Machine** if other processes in this computer will access hello service</span></span>
2. <span data-ttu-id="724c4-354">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="724c4-354">Click **Next**.</span></span>
3. <span data-ttu-id="724c4-355">Если импорт из файла Проверьте путь к файлу hello.</span><span class="sxs-lookup"><span data-stu-id="724c4-355">If importing from a file, confirm hello file path.</span></span>
4. <span data-ttu-id="724c4-356">При импорте .PFX-файла:</span><span class="sxs-lookup"><span data-stu-id="724c4-356">If importing a .PFX file:</span></span>
   1. <span data-ttu-id="724c4-357">Введите пароль hello, защищающий закрытый ключ hello</span><span class="sxs-lookup"><span data-stu-id="724c4-357">Enter hello password protecting hello private key</span></span>
   2. <span data-ttu-id="724c4-358">Выберите параметры импорта</span><span class="sxs-lookup"><span data-stu-id="724c4-358">Select import options</span></span>
5. <span data-ttu-id="724c4-359">Выберите «Место», сертификаты в следующие хранилища hello</span><span class="sxs-lookup"><span data-stu-id="724c4-359">Select "Place" certificates in hello following store</span></span>
6. <span data-ttu-id="724c4-360">Щелкните **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="724c4-360">Click **Browse**.</span></span>
7. <span data-ttu-id="724c4-361">Выберите нужное хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="724c4-361">Select hello desired store.</span></span>
8. <span data-ttu-id="724c4-362">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="724c4-362">Click **Finish**.</span></span>
   
   * <span data-ttu-id="724c4-363">Если вы выбрали hello хранилище доверенных корневых центров сертификации, щелкните **Да**.</span><span class="sxs-lookup"><span data-stu-id="724c4-363">If hello Trusted Root Certification Authority store was chosen, click **Yes**.</span></span>
9. <span data-ttu-id="724c4-364">Нажмите кнопку **ОК** во всех диалоговых окнах.</span><span class="sxs-lookup"><span data-stu-id="724c4-364">Click **OK** on all dialog windows.</span></span>

## <a name="upload-certificate"></a><span data-ttu-id="724c4-365">Передача сертификата</span><span class="sxs-lookup"><span data-stu-id="724c4-365">Upload certificate</span></span>
<span data-ttu-id="724c4-366">В hello [портала Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="724c4-366">In hello [Azure Portal](https://portal.azure.com/)</span></span>

1. <span data-ttu-id="724c4-367">Выберите **Облачные службы**.</span><span class="sxs-lookup"><span data-stu-id="724c4-367">Select **Cloud Services**.</span></span>
2. <span data-ttu-id="724c4-368">Выберите облачную службу hello.</span><span class="sxs-lookup"><span data-stu-id="724c4-368">Select hello cloud service.</span></span>
3. <span data-ttu-id="724c4-369">Hello верхнего меню **сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="724c4-369">On hello top menu, click **Certificates**.</span></span>
4. <span data-ttu-id="724c4-370">На нижней панели hello щелкните **отправить**.</span><span class="sxs-lookup"><span data-stu-id="724c4-370">On hello bottom bar, click **Upload**.</span></span>
5. <span data-ttu-id="724c4-371">Выберите файл сертификата hello.</span><span class="sxs-lookup"><span data-stu-id="724c4-371">Select hello certificate file.</span></span>
6. <span data-ttu-id="724c4-372">Если это. PFX-ФАЙЛ, введите hello пароль для закрытого ключа hello.</span><span class="sxs-lookup"><span data-stu-id="724c4-372">If it is a .PFX file, enter hello password for hello private key.</span></span>
7. <span data-ttu-id="724c4-373">После завершения копирования hello отпечаток сертификата из hello новую запись в списке hello.</span><span class="sxs-lookup"><span data-stu-id="724c4-373">Once completed, copy hello certificate thumbprint from hello new entry in hello list.</span></span>

## <a name="other-security-considerations"></a><span data-ttu-id="724c4-374">Прочие вопросы по безопасности</span><span class="sxs-lookup"><span data-stu-id="724c4-374">Other security considerations</span></span>
<span data-ttu-id="724c4-375">Параметры SSL Hello, описанные в этом документе шифрования обмена данными между службой hello и клиентами, при использовании конечной точки HTTPS hello.</span><span class="sxs-lookup"><span data-stu-id="724c4-375">hello SSL settings described in this document encrypt communication between hello service and its clients when hello HTTPS endpoint is used.</span></span> <span data-ttu-id="724c4-376">Это важно, так как учетные данные для доступа к базе данных и другие конфиденциальные сведения, содержащиеся в hello связи.</span><span class="sxs-lookup"><span data-stu-id="724c4-376">This is important since credentials for database access and potentially other sensitive information are contained in hello communication.</span></span> <span data-ttu-id="724c4-377">Обратите внимание, что служба hello сохраняется внутреннего состояния, включая учетные данные, в его внутренних таблиц в базе данных Microsoft Azure SQL hello, введенным для хранения метаданных в вашей подписке Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="724c4-377">Note, however, that hello service persists internal status, including credentials, in its internal tables in hello Microsoft Azure SQL database that you have provided for metadata storage in your Microsoft Azure subscription.</span></span> <span data-ttu-id="724c4-378">Базы данных был определен как часть hello следующий параметр в файле конфигурации службы (. Файл CSCFG):</span><span class="sxs-lookup"><span data-stu-id="724c4-378">That database was defined as part of hello following setting in your service configuration file (.CSCFG file):</span></span> 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

<span data-ttu-id="724c4-379">Учетные данные, хранящиеся в этой базе данных, будут зашифрованы.</span><span class="sxs-lookup"><span data-stu-id="724c4-379">Credentials stored in this database are encrypted.</span></span> <span data-ttu-id="724c4-380">Тем не менее рекомендуется, убедитесь, что веб- и рабочих ролей развертываний службы хранятся копии toodate и безопасно, как они имеют доступ toohello метаданных базы данных и hello сертификат, используемый для шифрования и расшифровки сохраненных учетных данных.</span><span class="sxs-lookup"><span data-stu-id="724c4-380">However, as a best practice, ensure that both web and worker roles of your service deployments are kept up toodate and secure as they both have access toohello metadata database and hello certificate used for encryption and decryption of stored credentials.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

