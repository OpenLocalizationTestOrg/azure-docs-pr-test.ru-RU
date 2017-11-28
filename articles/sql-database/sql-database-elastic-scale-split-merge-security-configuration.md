---
title: "Настройка параметров безопасности для службы разбиения и объединения | Документация Майкрософт"
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
ms.openlocfilehash: 7e6ccf51a4b75eef16a7df5c1a1018954af8e5dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="split-merge-security-configuration"></a><span data-ttu-id="11f89-103">Настройка параметров безопасности для службы разделения и объединения</span><span class="sxs-lookup"><span data-stu-id="11f89-103">Split-merge security configuration</span></span>
<span data-ttu-id="11f89-104">Для использования службы разделения и объединения необходимо правильно настроить параметры безопасности.</span><span class="sxs-lookup"><span data-stu-id="11f89-104">To use the Split/Merge service, you must correctly configure security.</span></span> <span data-ttu-id="11f89-105">Эта служба является частью компонента эластичного масштабирования базы данных Microsoft Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="11f89-105">The service is part of the Elastic Scale feature of Microsoft Azure SQL Database.</span></span> <span data-ttu-id="11f89-106">Дополнительные сведения см. в [руководстве по эластичному масштабированию службы разбиения и объединения](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span><span class="sxs-lookup"><span data-stu-id="11f89-106">For more information, see [Elastic Scale Split and Merge Service Tutorial](sql-database-elastic-scale-configure-deploy-split-and-merge.md).</span></span>

## <a name="configuring-certificates"></a><span data-ttu-id="11f89-107">Настройка сертификатов</span><span class="sxs-lookup"><span data-stu-id="11f89-107">Configuring certificates</span></span>
<span data-ttu-id="11f89-108">Сертификаты настраиваются двумя способами.</span><span class="sxs-lookup"><span data-stu-id="11f89-108">Certificates are configured in two ways.</span></span> 

1. [<span data-ttu-id="11f89-109">Настройка SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="11f89-109">To Configure the SSL Certificate</span></span>](#to-configure-the-ssl-certificate)
2. [<span data-ttu-id="11f89-110">Настройка сертификатов клиентов</span><span class="sxs-lookup"><span data-stu-id="11f89-110">To Configure Client Certificates</span></span>](#to-configure-client-certificates) 

## <a name="to-obtain-certificates"></a><span data-ttu-id="11f89-111">Получение сертификатов</span><span class="sxs-lookup"><span data-stu-id="11f89-111">To obtain certificates</span></span>
<span data-ttu-id="11f89-112">Сертификаты можно получать от общих центров сертификации (ЦС) или в [службе сертификации Windows](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span><span class="sxs-lookup"><span data-stu-id="11f89-112">Certificates can be obtained from public Certificate Authorities (CAs) or from the [Windows Certificate Service](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx).</span></span> <span data-ttu-id="11f89-113">Это наиболее предпочтительные способы получения сертификатов.</span><span class="sxs-lookup"><span data-stu-id="11f89-113">These are the preferred methods to obtain certificates.</span></span>

<span data-ttu-id="11f89-114">Если эти варианты недоступны, можно создавать **самозаверяющие сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="11f89-114">If those options are not available, you can generate **self-signed certificates**.</span></span>

## <a name="tools-to-generate-certificates"></a><span data-ttu-id="11f89-115">Инструменты для создания сертификатов</span><span class="sxs-lookup"><span data-stu-id="11f89-115">Tools to generate certificates</span></span>
* [<span data-ttu-id="11f89-116">makecert.exe</span><span class="sxs-lookup"><span data-stu-id="11f89-116">makecert.exe</span></span>](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [<span data-ttu-id="11f89-117">pvk2pfx.exe</span><span class="sxs-lookup"><span data-stu-id="11f89-117">pvk2pfx.exe</span></span>](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="to-run-the-tools"></a><span data-ttu-id="11f89-118">Запуск инструментов</span><span class="sxs-lookup"><span data-stu-id="11f89-118">To run the tools</span></span>
* <span data-ttu-id="11f89-119">Сведения о запуске инструментов из командной строки разработчика для Visual Studio см. в статье [Командная строка разработчика для Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx).</span><span class="sxs-lookup"><span data-stu-id="11f89-119">From a Developer Command Prompt for Visual Studios, see [Visual Studio Command Prompt](http://msdn.microsoft.com/library/ms229859.aspx)</span></span> 
  
    <span data-ttu-id="11f89-120">Если ПО установлено, перейдите к:</span><span class="sxs-lookup"><span data-stu-id="11f89-120">If installed, go to:</span></span>
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* <span data-ttu-id="11f89-121">Пакет WDK можно загрузить в разделе [Windows 8.1: загрузка пакетов и средств](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span><span class="sxs-lookup"><span data-stu-id="11f89-121">Get the WDK from [Windows 8.1: Download kits and tools](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)</span></span>

## <a name="to-configure-the-ssl-certificate"></a><span data-ttu-id="11f89-122">Настройка SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="11f89-122">To configure the SSL certificate</span></span>
<span data-ttu-id="11f89-123">SSL-сертификат требуется для шифрования при обмене данными и для проверки подлинности сервера.</span><span class="sxs-lookup"><span data-stu-id="11f89-123">A SSL certificate is required to encrypt the communication and authenticate the server.</span></span> <span data-ttu-id="11f89-124">Выберите наиболее подходящий из этих трех сценариев и выполните все шаги.</span><span class="sxs-lookup"><span data-stu-id="11f89-124">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="create-a-new-self-signed-certificate"></a><span data-ttu-id="11f89-125">Создание самозаверяющего сертификата</span><span class="sxs-lookup"><span data-stu-id="11f89-125">Create a new self-signed certificate</span></span>
1. [<span data-ttu-id="11f89-126">Создание самозаверяющего сертификата</span><span class="sxs-lookup"><span data-stu-id="11f89-126">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="11f89-127">Создание PFX-файла для самозаверяющего SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="11f89-127">Create PFX file for Self-Signed SSL Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="11f89-128">Передача SSL-сертификата в облачную службу</span><span class="sxs-lookup"><span data-stu-id="11f89-128">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
4. [<span data-ttu-id="11f89-129">Обновление SSL-сертификата в файле конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="11f89-129">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)
5. [<span data-ttu-id="11f89-130">Импорт центра сертификации SSL</span><span class="sxs-lookup"><span data-stu-id="11f89-130">Import SSL Certification Authority</span></span>](#import-ssl-certification-authority)

### <a name="to-use-an-existing-certificate-from-the-certificate-store"></a><span data-ttu-id="11f89-131">Использование существующего сертификата из хранилища сертификатов</span><span class="sxs-lookup"><span data-stu-id="11f89-131">To use an existing certificate from the certificate store</span></span>
1. [<span data-ttu-id="11f89-132">Экспорт SSL-сертификата из хранилища сертификатов</span><span class="sxs-lookup"><span data-stu-id="11f89-132">Export SSL Certificate From Certificate Store</span></span>](#export-ssl-certificate-from-certificate-store)
2. [<span data-ttu-id="11f89-133">Передача SSL-сертификата в облачную службу</span><span class="sxs-lookup"><span data-stu-id="11f89-133">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
3. [<span data-ttu-id="11f89-134">Обновление SSL-сертификата в файле конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="11f89-134">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

### <a name="to-use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="11f89-135">Использование существующего сертификата в PFX-файле</span><span class="sxs-lookup"><span data-stu-id="11f89-135">To use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="11f89-136">Передача SSL-сертификата в облачную службу</span><span class="sxs-lookup"><span data-stu-id="11f89-136">Upload SSL Certificate to Cloud Service</span></span>](#upload-ssl-certificate-to-cloud-service)
2. [<span data-ttu-id="11f89-137">Обновление SSL-сертификата в файле конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="11f89-137">Update SSL Certificate in Service Configuration File</span></span>](#update-ssl-certificate-in-service-configuration-file)

## <a name="to-configure-client-certificates"></a><span data-ttu-id="11f89-138">Настройка сертификатов клиентов</span><span class="sxs-lookup"><span data-stu-id="11f89-138">To configure client certificates</span></span>
<span data-ttu-id="11f89-139">Для проверки подлинности запросов к службе требуются сертификаты клиентов.</span><span class="sxs-lookup"><span data-stu-id="11f89-139">Client certificates are required in order to authenticate requests to the service.</span></span> <span data-ttu-id="11f89-140">Выберите наиболее подходящий из этих трех сценариев и выполните все шаги.</span><span class="sxs-lookup"><span data-stu-id="11f89-140">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="turn-off-client-certificates"></a><span data-ttu-id="11f89-141">Отключение сертификатов клиента</span><span class="sxs-lookup"><span data-stu-id="11f89-141">Turn off client certificates</span></span>
1. [<span data-ttu-id="11f89-142">Отключение аутентификации на основе сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="11f89-142">Turn Off Client Certificate-Based Authentication</span></span>](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a><span data-ttu-id="11f89-143">Выдача новых самозаверяющих сертификатов клиента</span><span class="sxs-lookup"><span data-stu-id="11f89-143">Issue new self-signed client certificates</span></span>
1. [<span data-ttu-id="11f89-144">Создание центра самозаверяющей сертификации</span><span class="sxs-lookup"><span data-stu-id="11f89-144">Create a Self-Signed Certification Authority</span></span>](#create-a-self-signed-certification-authority)
2. [<span data-ttu-id="11f89-145">Передача сертификата ЦС в облачную службу</span><span class="sxs-lookup"><span data-stu-id="11f89-145">Upload CA Certificate to Cloud Service</span></span>](#upload-ca-certificate-to-cloud-service)
3. [<span data-ttu-id="11f89-146">Обновление сертификата ЦС в файле конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="11f89-146">Update CA Certificate in Service Configuration File</span></span>](#update-ca-certificate-in-service-configuration-file)
4. [<span data-ttu-id="11f89-147">Выдача сертификатов клиентов</span><span class="sxs-lookup"><span data-stu-id="11f89-147">Issue Client Certificates</span></span>](#issue-client-certificates)
5. [<span data-ttu-id="11f89-148">Создание PFX-файлов для сертификатов клиента</span><span class="sxs-lookup"><span data-stu-id="11f89-148">Create PFX files for Client Certificates</span></span>](#create-pfx-files-for-client-certificates)
6. [<span data-ttu-id="11f89-149">Импорт сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="11f89-149">Import Client Certificate</span></span>](#Import-Client-Certificate)
7. [<span data-ttu-id="11f89-150">Копирование отпечатков сертификатов клиента</span><span class="sxs-lookup"><span data-stu-id="11f89-150">Copy Client Certificate Thumbprints</span></span>](#copy-client-certificate-thumbprints)
8. [<span data-ttu-id="11f89-151">Настройка разрешенных клиентов в файле конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="11f89-151">Configure Allowed Clients in the Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a><span data-ttu-id="11f89-152">Использование существующих сертификатов клиентов</span><span class="sxs-lookup"><span data-stu-id="11f89-152">Use existing client certificates</span></span>
1. [<span data-ttu-id="11f89-153">Find CA Public Key</span><span class="sxs-lookup"><span data-stu-id="11f89-153">Find CA Public Key</span></span>](#find-ca-public-key)
2. [<span data-ttu-id="11f89-154">Передача сертификата ЦС в облачную службу</span><span class="sxs-lookup"><span data-stu-id="11f89-154">Upload CA Certificate to Cloud Service</span></span>](#Upload-CA-certificate-to-cloud-service)
3. [<span data-ttu-id="11f89-155">Обновление сертификата ЦС в файле конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="11f89-155">Update CA Certificate in Service Configuration File</span></span>](#Update-CA-Certificate-in-Service-Configuration-File)
4. [<span data-ttu-id="11f89-156">Копирование отпечатков сертификатов клиента</span><span class="sxs-lookup"><span data-stu-id="11f89-156">Copy Client Certificate Thumbprints</span></span>](#Copy-Client-Certificate-Thumbprints)
5. [<span data-ttu-id="11f89-157">Настройка разрешенных клиентов в файле конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="11f89-157">Configure Allowed Clients in the Service Configuration File</span></span>](#configure-allowed-clients-in-the-service-configuration-file)
6. [<span data-ttu-id="11f89-158">Настройка проверки отзыва сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="11f89-158">Configure Client Certificate Revocation Check</span></span>](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a><span data-ttu-id="11f89-159">Разрешенные IP-адреса</span><span class="sxs-lookup"><span data-stu-id="11f89-159">Allowed IP addresses</span></span>
<span data-ttu-id="11f89-160">Доступ к конечным точкам службы может быть ограничен для определенных диапазонов IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="11f89-160">Access to the service endpoints can be restricted to specific ranges of IP addresses.</span></span>

## <a name="to-configure-encryption-for-the-store"></a><span data-ttu-id="11f89-161">Настройка шифрования для хранилища</span><span class="sxs-lookup"><span data-stu-id="11f89-161">To configure encryption for the store</span></span>
<span data-ttu-id="11f89-162">Сертификат необходим для шифрования учетных данных, которые хранятся в хранилище метаданных.</span><span class="sxs-lookup"><span data-stu-id="11f89-162">A certificate is required to encrypt the credentials that are stored in the metadata store.</span></span> <span data-ttu-id="11f89-163">Выберите наиболее подходящий из этих трех сценариев и выполните все шаги.</span><span class="sxs-lookup"><span data-stu-id="11f89-163">Choose the most applicable of the three scenarios below, and execute all its steps:</span></span>

### <a name="use-a-new-self-signed-certificate"></a><span data-ttu-id="11f89-164">Использование нового самозаверяющего сертификата</span><span class="sxs-lookup"><span data-stu-id="11f89-164">Use a new self-signed certificate</span></span>
1. [<span data-ttu-id="11f89-165">Создание самозаверяющего сертификата</span><span class="sxs-lookup"><span data-stu-id="11f89-165">Create a Self-Signed Certificate</span></span>](#create-a-self-signed-certificate)
2. [<span data-ttu-id="11f89-166">Создание PFX-файла для самозаверяющего сертификата шифрования</span><span class="sxs-lookup"><span data-stu-id="11f89-166">Create PFX file for Self-Signed Encryption Certificate</span></span>](#create-pfx-file-for-self-signed-ssl-certificate)
3. [<span data-ttu-id="11f89-167">Передача сертификата шифрования в облачную службу</span><span class="sxs-lookup"><span data-stu-id="11f89-167">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
4. [<span data-ttu-id="11f89-168">Обновление сертификата шифрования в файле конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="11f89-168">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-the-certificate-store"></a><span data-ttu-id="11f89-169">Использование существующего сертификата из хранилища сертификатов</span><span class="sxs-lookup"><span data-stu-id="11f89-169">Use an existing certificate from the certificate store</span></span>
1. [<span data-ttu-id="11f89-170">Экспорт сертификата шифрования из хранилища сертификатов</span><span class="sxs-lookup"><span data-stu-id="11f89-170">Export Encryption Certificate From Certificate Store</span></span>](#export-encryption-certificate-from-certificate-store)
2. [<span data-ttu-id="11f89-171">Передача сертификата шифрования в облачную службу</span><span class="sxs-lookup"><span data-stu-id="11f89-171">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
3. [<span data-ttu-id="11f89-172">Обновление сертификата шифрования в файле конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="11f89-172">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a><span data-ttu-id="11f89-173">Использование существующего сертификата в PFX-файле</span><span class="sxs-lookup"><span data-stu-id="11f89-173">Use an existing certificate in a PFX file</span></span>
1. [<span data-ttu-id="11f89-174">Передача сертификата шифрования в облачную службу</span><span class="sxs-lookup"><span data-stu-id="11f89-174">Upload Encryption Certificate to Cloud Service</span></span>](#upload-encryption-certificate-to-cloud-service)
2. [<span data-ttu-id="11f89-175">Обновление сертификата шифрования в файле конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="11f89-175">Update Encryption Certificate in Service Configuration File</span></span>](#update-encryption-certificate-in-service-configuration-file)

## <a name="the-default-configuration"></a><span data-ttu-id="11f89-176">Конфигурация по умолчанию</span><span class="sxs-lookup"><span data-stu-id="11f89-176">The default configuration</span></span>
<span data-ttu-id="11f89-177">В конфигурации по умолчанию запрещен любой доступ к конечной точке HTTP.</span><span class="sxs-lookup"><span data-stu-id="11f89-177">The default configuration denies all access to the HTTP endpoint.</span></span> <span data-ttu-id="11f89-178">Это рекомендуемый параметр, так как запросы к этим конечным точкам могут содержать конфиденциальную информацию, например учетные данные базы данных.</span><span class="sxs-lookup"><span data-stu-id="11f89-178">This is the recommended setting, since the requests to these endpoints may carry sensitive information like database credentials.</span></span>
<span data-ttu-id="11f89-179">В конфигурации по умолчанию разрешен доступ к конечной точке HTTPS.</span><span class="sxs-lookup"><span data-stu-id="11f89-179">The default configuration allows all access to the HTTPS endpoint.</span></span> <span data-ttu-id="11f89-180">Этот параметр в дальнейшем может быть ограничен.</span><span class="sxs-lookup"><span data-stu-id="11f89-180">This setting may be restricted further.</span></span>

### <a name="changing-the-configuration"></a><span data-ttu-id="11f89-181">Изменение конфигурации</span><span class="sxs-lookup"><span data-stu-id="11f89-181">Changing the Configuration</span></span>
<span data-ttu-id="11f89-182">Применяемые группы правил контроля доступа и конечная точка настраиваются в разделе **<EndpointAcls>** **файла конфигурации службы**.</span><span class="sxs-lookup"><span data-stu-id="11f89-182">The group of access control rules that apply to and endpoint are configured in the **<EndpointAcls>** section in the **service configuration file**.</span></span>

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

<span data-ttu-id="11f89-183">Правила в группе управления доступом настраиваются в разделе <AccessControl name=""> файла конфигурации службы.</span><span class="sxs-lookup"><span data-stu-id="11f89-183">The rules in an access control group are configured in a <AccessControl name=""> section of the service configuration file.</span></span> 

<span data-ttu-id="11f89-184">Описание формата содержится в документации по спискам управления сетевым доступом.</span><span class="sxs-lookup"><span data-stu-id="11f89-184">The format is explained in Network Access Control Lists documentation.</span></span>
<span data-ttu-id="11f89-185">Например, правила, позволяющие разрешить получение доступа к конечной точке HTTPS только IP-адресам в диапазоне от 100.100.0.0 до 100.100.255.255, будут выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="11f89-185">For example, to allow only IPs in the range 100.100.0.0 to 100.100.255.255 to access the HTTPS endpoint, the rules would look like this:</span></span>

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a><span data-ttu-id="11f89-186">Предотвращение отказа в обслуживании</span><span class="sxs-lookup"><span data-stu-id="11f89-186">Denial of service prevention</span></span>
<span data-ttu-id="11f89-187">Существует два различных механизма, поддерживаемых для выявления и предотвращения атак в виде отказа в обслуживании.</span><span class="sxs-lookup"><span data-stu-id="11f89-187">There are two different mechanisms supported to detect and prevent Denial of Service attacks:</span></span>

* <span data-ttu-id="11f89-188">Ограничение количества одновременных запросов на удаленный узел (по умолчанию отключено)</span><span class="sxs-lookup"><span data-stu-id="11f89-188">Restrict number of concurrent requests per remote host (off by default)</span></span>
* <span data-ttu-id="11f89-189">Ограничение частоты доступа в расчете на удаленный узел (включено по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="11f89-189">Restrict rate of access per remote host (on by default)</span></span>

<span data-ttu-id="11f89-190">Они основаны на функциях, более подробно документированных в Dynamic IP Security в IIS.</span><span class="sxs-lookup"><span data-stu-id="11f89-190">These are based on the features further documented in Dynamic IP Security in IIS.</span></span> <span data-ttu-id="11f89-191">При изменении этой конфигурации имейте в виду следующие факторы.</span><span class="sxs-lookup"><span data-stu-id="11f89-191">When changing this configuration beware of the following factors:</span></span>

* <span data-ttu-id="11f89-192">Поведение прокси-серверов и устройств преобразования сетевых адресов в отношении информации удаленного хоста (узла)</span><span class="sxs-lookup"><span data-stu-id="11f89-192">The behavior of proxies and Network Address Translation devices over the remote host information</span></span>
* <span data-ttu-id="11f89-193">Учитывается каждый запрос к любому ресурсу в веб-роли (например, загрузки скриптов, изображений и т. д.)</span><span class="sxs-lookup"><span data-stu-id="11f89-193">Each request to any resource in the web role is considered (e.g. loading scripts, images, etc)</span></span>

## <a name="restricting-number-of-concurrent-accesses"></a><span data-ttu-id="11f89-194">Ограничение числа одновременных обращений</span><span class="sxs-lookup"><span data-stu-id="11f89-194">Restricting number of concurrent accesses</span></span>
<span data-ttu-id="11f89-195">Ниже перечислены параметры, с помощью которых настраивается их действие.</span><span class="sxs-lookup"><span data-stu-id="11f89-195">The settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

<span data-ttu-id="11f89-196">Измените значение DynamicIpRestrictionDenyByConcurrentRequests на true, чтобы включить эту защиту.</span><span class="sxs-lookup"><span data-stu-id="11f89-196">Change DynamicIpRestrictionDenyByConcurrentRequests to true to enable this protection.</span></span>

## <a name="restricting-rate-of-access"></a><span data-ttu-id="11f89-197">Ограничение частоты доступа</span><span class="sxs-lookup"><span data-stu-id="11f89-197">Restricting rate of access</span></span>
<span data-ttu-id="11f89-198">Ниже перечислены параметры, с помощью которых настраивается их действие.</span><span class="sxs-lookup"><span data-stu-id="11f89-198">The settings that configure this behavior are:</span></span>

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-the-response-to-a-denied-request"></a><span data-ttu-id="11f89-199">Настройка ответа на отклоненный запрос</span><span class="sxs-lookup"><span data-stu-id="11f89-199">Configuring the response to a denied request</span></span>
<span data-ttu-id="11f89-200">Следующий параметр позволяет настроить ответ на отклоненный запрос.</span><span class="sxs-lookup"><span data-stu-id="11f89-200">The following setting configures the response to a denied request:</span></span>

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
<span data-ttu-id="11f89-201">По вопросу иных поддерживаемых значений обратитесь к документации по динамической IP-безопасности в IIS.</span><span class="sxs-lookup"><span data-stu-id="11f89-201">Refer to the documentation for Dynamic IP Security in IIS for other supported values.</span></span>

## <a name="operations-for-configuring-service-certificates"></a><span data-ttu-id="11f89-202">Операции настройки службы сертификатов</span><span class="sxs-lookup"><span data-stu-id="11f89-202">Operations for configuring service certificates</span></span>
<span data-ttu-id="11f89-203">Этот раздел предназначен только для справки.</span><span class="sxs-lookup"><span data-stu-id="11f89-203">This topic is for reference only.</span></span> <span data-ttu-id="11f89-204">Выполните этапы настройки, описанные в:</span><span class="sxs-lookup"><span data-stu-id="11f89-204">Please follow the configuration steps outlined in:</span></span>

* <span data-ttu-id="11f89-205">Настройка SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="11f89-205">Configure the SSL certificate</span></span>
* <span data-ttu-id="11f89-206">Настройка сертификатов клиентов</span><span class="sxs-lookup"><span data-stu-id="11f89-206">Configure client certificates</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="11f89-207">Создание самозаверяющего сертификата</span><span class="sxs-lookup"><span data-stu-id="11f89-207">Create a self-signed certificate</span></span>
<span data-ttu-id="11f89-208">Выполните:</span><span class="sxs-lookup"><span data-stu-id="11f89-208">Execute:</span></span>

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

<span data-ttu-id="11f89-209">Чтобы настроить:</span><span class="sxs-lookup"><span data-stu-id="11f89-209">To customize:</span></span>

* <span data-ttu-id="11f89-210">-n с URL-адресом службы.</span><span class="sxs-lookup"><span data-stu-id="11f89-210">-n with the service URL.</span></span> <span data-ttu-id="11f89-211">Поддерживаются подстановочные знаки ("CN=*.cloudapp.net") и альтернативные имена ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net").</span><span class="sxs-lookup"><span data-stu-id="11f89-211">Wildcards ("CN=*.cloudapp.net") and alternative names ("CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net") are supported.</span></span>
* <span data-ttu-id="11f89-212">-e со сроком действия сертификата Создайте надежный пароль и укажите его при появлении запроса.</span><span class="sxs-lookup"><span data-stu-id="11f89-212">-e with the certificate expiration date Create a strong password and specify it when prompted.</span></span>

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a><span data-ttu-id="11f89-213">Создание PFX-файла для самозаверяющего SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="11f89-213">Create PFX file for self-signed SSL certificate</span></span>
<span data-ttu-id="11f89-214">Выполните:</span><span class="sxs-lookup"><span data-stu-id="11f89-214">Execute:</span></span>

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

<span data-ttu-id="11f89-215">Введите пароль, а затем экспортируйте сертификат с этими параметрами.</span><span class="sxs-lookup"><span data-stu-id="11f89-215">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="11f89-216">Да, экспортировать закрытый ключ</span><span class="sxs-lookup"><span data-stu-id="11f89-216">Yes, export the private key</span></span>
* <span data-ttu-id="11f89-217">Экспортировать все расширенные свойства.</span><span class="sxs-lookup"><span data-stu-id="11f89-217">Export all extended properties</span></span>

## <a name="export-ssl-certificate-from-certificate-store"></a><span data-ttu-id="11f89-218">Экспорт SSL-сертификата из хранилища сертификатов</span><span class="sxs-lookup"><span data-stu-id="11f89-218">Export SSL certificate from certificate store</span></span>
* <span data-ttu-id="11f89-219">Поиск сертификата</span><span class="sxs-lookup"><span data-stu-id="11f89-219">Find certificate</span></span>
* <span data-ttu-id="11f89-220">Выберите «Действия > Все задачи > Экспортировать…»</span><span class="sxs-lookup"><span data-stu-id="11f89-220">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="11f89-221">Экспортируйте сертификат в PFX-файл со следующими параметрами.</span><span class="sxs-lookup"><span data-stu-id="11f89-221">Export certificate into a .PFX file with these options:</span></span>
  * <span data-ttu-id="11f89-222">Да, экспортировать закрытый ключ</span><span class="sxs-lookup"><span data-stu-id="11f89-222">Yes, export the private key</span></span>
  * <span data-ttu-id="11f89-223">По возможности включите все сертификаты в путь сертификации *Экспортировать все расширенные свойства.</span><span class="sxs-lookup"><span data-stu-id="11f89-223">Include all certificates in the certification path if possible *Export all extended properties</span></span>

## <a name="upload-ssl-certificate-to-cloud-service"></a><span data-ttu-id="11f89-224">Передача SSL-сертификата в облачную службу</span><span class="sxs-lookup"><span data-stu-id="11f89-224">Upload SSL certificate to cloud service</span></span>
<span data-ttu-id="11f89-225">Отправьте сертификат с существующим или созданным .PFX-файлом с помощью пары ключей SSL.</span><span class="sxs-lookup"><span data-stu-id="11f89-225">Upload certificate with the existing or generated .PFX file with the SSL key pair:</span></span>

* <span data-ttu-id="11f89-226">Введите пароль, защищающий данные закрытого ключа</span><span class="sxs-lookup"><span data-stu-id="11f89-226">Enter the password protecting the private key information</span></span>

## <a name="update-ssl-certificate-in-service-configuration-file"></a><span data-ttu-id="11f89-227">Обновление SSL-сертификата в файле конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="11f89-227">Update SSL certificate in service configuration file</span></span>
<span data-ttu-id="11f89-228">Обновите значения отпечатка следующего параметра в файле конфигурации службы значением отпечатка сертификата, отправленного в облачную службу.</span><span class="sxs-lookup"><span data-stu-id="11f89-228">Update the thumbprint value of the following setting in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a><span data-ttu-id="11f89-229">Импорт центра сертификации SSL</span><span class="sxs-lookup"><span data-stu-id="11f89-229">Import SSL certification authority</span></span>
<span data-ttu-id="11f89-230">Выполните эти шаги на всех учетных записях или компьютерах, которые будут взаимодействовать со службой.</span><span class="sxs-lookup"><span data-stu-id="11f89-230">Follow these steps in all account/machine that will communicate with the service:</span></span>

* <span data-ttu-id="11f89-231">Дважды нажмите файл .CER в проводнике Windows</span><span class="sxs-lookup"><span data-stu-id="11f89-231">Double-click the .CER file in Windows Explorer</span></span>
* <span data-ttu-id="11f89-232">В диалоговом окне сертификата нажмите «Установить сертификат...»</span><span class="sxs-lookup"><span data-stu-id="11f89-232">In the Certificate dialog, click Install Certificate…</span></span>
* <span data-ttu-id="11f89-233">Импортируйте сертификат в хранилище доверенных корневых центров сертификации</span><span class="sxs-lookup"><span data-stu-id="11f89-233">Import certificate into the Trusted Root Certification Authorities store</span></span>

## <a name="turn-off-client-certificate-based-authentication"></a><span data-ttu-id="11f89-234">Отключение аутентификации на основе сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="11f89-234">Turn off client certificate-based authentication</span></span>
<span data-ttu-id="11f89-235">Проверка подлинности клиента поддерживается только на основе сертификата, и ее отключение откроет общий доступ к конечным точкам службы, если только не используются другие механизмы (например, виртуальная сеть Microsoft Azure).</span><span class="sxs-lookup"><span data-stu-id="11f89-235">Only client certificate-based authentication is supported and disabling it will allow for public access to the service endpoints, unless other mechanisms are in place (e.g. Microsoft Azure Virtual Network).</span></span>

<span data-ttu-id="11f89-236">Присвойте этим параметрам значение false в файле конфигурации службы, если нужно отключить эту функцию.</span><span class="sxs-lookup"><span data-stu-id="11f89-236">Change these settings to false in the service configuration file to turn the feature off:</span></span>

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

<span data-ttu-id="11f89-237">Затем скопируйте тот же отпечаток, что и SSL-сертификат, в параметр сертификата ЦС.</span><span class="sxs-lookup"><span data-stu-id="11f89-237">Then, copy the same thumbprint as the SSL certificate in the CA certificate setting:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a><span data-ttu-id="11f89-238">Создание центра самозаверяющей сертификации</span><span class="sxs-lookup"><span data-stu-id="11f89-238">Create a self-signed certification authority</span></span>
<span data-ttu-id="11f89-239">Выполните следующие шаги для создания самозаверяющего сертификата, выступающего в качестве центра сертификации.</span><span class="sxs-lookup"><span data-stu-id="11f89-239">Execute the following steps to create a self-signed certificate to act as a Certification Authority:</span></span>

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

<span data-ttu-id="11f89-240">Как настроить</span><span class="sxs-lookup"><span data-stu-id="11f89-240">To customize it</span></span>

* <span data-ttu-id="11f89-241">-e с датой окончания срока действия сертификации</span><span class="sxs-lookup"><span data-stu-id="11f89-241">-e with the certification expiration date</span></span>

## <a name="find-ca-public-key"></a><span data-ttu-id="11f89-242">Поиск открытого ключа ЦС</span><span class="sxs-lookup"><span data-stu-id="11f89-242">Find CA public key</span></span>
<span data-ttu-id="11f89-243">Все сертификаты клиента должны быть выданы центром сертификации, уполномоченным данной службой.</span><span class="sxs-lookup"><span data-stu-id="11f89-243">All client certificates must have been issued by a Certification Authority trusted by the service.</span></span> <span data-ttu-id="11f89-244">Найдите открытый ключ в том центре сертификации, который выдал сертификаты клиента, использование которых предусмотрено для проверки подлинности, чтобы передать его в облачную службу.</span><span class="sxs-lookup"><span data-stu-id="11f89-244">Find the public key to the Certification Authority that issued the client certificates that are going to be used for authentication in order to upload it to the cloud service.</span></span>

<span data-ttu-id="11f89-245">Если файл с открытым ключом недоступен, экспортируйте его из хранилища сертификатов:</span><span class="sxs-lookup"><span data-stu-id="11f89-245">If the file with the public key is not available, export it from the certificate store:</span></span>

* <span data-ttu-id="11f89-246">Поиск сертификата</span><span class="sxs-lookup"><span data-stu-id="11f89-246">Find certificate</span></span>
  * <span data-ttu-id="11f89-247">Поиск сертификата клиента, выданного этим же центром сертификации</span><span class="sxs-lookup"><span data-stu-id="11f89-247">Search for a client certificate issued by the same Certification Authority</span></span>
* <span data-ttu-id="11f89-248">Дважды щелкните сертификат.</span><span class="sxs-lookup"><span data-stu-id="11f89-248">Double-click the certificate.</span></span>
* <span data-ttu-id="11f89-249">Перейдите на вкладку "Путь сертификации" в диалоговом окне "Сертификат".</span><span class="sxs-lookup"><span data-stu-id="11f89-249">Select the Certification Path tab in the Certificate dialog.</span></span>
* <span data-ttu-id="11f89-250">Дважды щелкните запись центра сертификации в пути.</span><span class="sxs-lookup"><span data-stu-id="11f89-250">Double-click the CA entry in the path.</span></span>
* <span data-ttu-id="11f89-251">Запишите свойства сертификата.</span><span class="sxs-lookup"><span data-stu-id="11f89-251">Take notes of the certificate properties.</span></span>
* <span data-ttu-id="11f89-252">Закройте диалоговое окно **Сертификат** .</span><span class="sxs-lookup"><span data-stu-id="11f89-252">Close the **Certificate** dialog.</span></span>
* <span data-ttu-id="11f89-253">Поиск сертификата</span><span class="sxs-lookup"><span data-stu-id="11f89-253">Find certificate</span></span>
  * <span data-ttu-id="11f89-254">Найдите центр сертификации, записанный ранее.</span><span class="sxs-lookup"><span data-stu-id="11f89-254">Search for the CA noted above.</span></span>
* <span data-ttu-id="11f89-255">Выберите «Действия > Все задачи > Экспортировать…»</span><span class="sxs-lookup"><span data-stu-id="11f89-255">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="11f89-256">Экспортируйте сертификат в .CER с этими параметрами:</span><span class="sxs-lookup"><span data-stu-id="11f89-256">Export certificate into a .CER with these options:</span></span>
  * <span data-ttu-id="11f89-257">**Нет, не экспортировать закрытый ключ**</span><span class="sxs-lookup"><span data-stu-id="11f89-257">**No, do not export the private key**</span></span>
  * <span data-ttu-id="11f89-258">По возможности включить все сертификаты в путь сертификации.</span><span class="sxs-lookup"><span data-stu-id="11f89-258">Include all certificates in the certification path if possible.</span></span>
  * <span data-ttu-id="11f89-259">Экспортировать все расширенные свойства.</span><span class="sxs-lookup"><span data-stu-id="11f89-259">Export all extended properties.</span></span>

## <a name="upload-ca-certificate-to-cloud-service"></a><span data-ttu-id="11f89-260">Передача сертификата ЦС в облачную службу</span><span class="sxs-lookup"><span data-stu-id="11f89-260">Upload CA certificate to cloud service</span></span>
<span data-ttu-id="11f89-261">Передайте сертификат с существующим или созданным файлом .CER при помощи открытого ключа центра сертификации.</span><span class="sxs-lookup"><span data-stu-id="11f89-261">Upload certificate with the existing or generated .CER file with the CA public key.</span></span>

## <a name="update-ca-certificate-in-service-configuration-file"></a><span data-ttu-id="11f89-262">Обновление сертификата ЦС в файле конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="11f89-262">Update CA certificate in service configuration file</span></span>
<span data-ttu-id="11f89-263">Обновите значения отпечатка следующего параметра в файле конфигурации службы значением отпечатка сертификата, отправленного в облачную службу.</span><span class="sxs-lookup"><span data-stu-id="11f89-263">Update the thumbprint value of the following setting in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

<span data-ttu-id="11f89-264">Обновите значение следующего параметра значением того же отпечатка.</span><span class="sxs-lookup"><span data-stu-id="11f89-264">Update the value of the following setting with the same thumbprint:</span></span>

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a><span data-ttu-id="11f89-265">Выдача сертификатов клиентов</span><span class="sxs-lookup"><span data-stu-id="11f89-265">Issue client certificates</span></span>
<span data-ttu-id="11f89-266">Каждое лицо, получившее разрешение на доступ к службе, должно иметь сертификат клиента, выданный для исключительного использования данным лицом. При этом такому лицу требуется выбрать надежный пароль для защиты своего закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="11f89-266">Each individual authorized to access the service should have a client certificate issued for his/hers exclusive use and should choose his/hers own strong password to protect its private key.</span></span> 

<span data-ttu-id="11f89-267">На том же компьютере, где был создан и хранился самозаверяющий сертификат ЦС, необходимо выполнить следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="11f89-267">The following steps must be executed in the same machine where the self-signed CA certificate was generated and stored:</span></span>

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

<span data-ttu-id="11f89-268">Настройка.</span><span class="sxs-lookup"><span data-stu-id="11f89-268">Customizing:</span></span>

* <span data-ttu-id="11f89-269">-n с идентификатором клиента, который будет проходить проверку подлинности с этим сертификатом</span><span class="sxs-lookup"><span data-stu-id="11f89-269">-n with an ID for to the client that will be authenticated with this certificate</span></span>
* <span data-ttu-id="11f89-270">-e с датой окончания срока действия сертификата</span><span class="sxs-lookup"><span data-stu-id="11f89-270">-e with the certificate expiration date</span></span>
* <span data-ttu-id="11f89-271">MyID.pvk и MyID.cer с уникальными именами файлов для этого сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="11f89-271">MyID.pvk and MyID.cer with unique filenames for this client certificate</span></span>

<span data-ttu-id="11f89-272">Эта команда запросит создать пароль и однократно его использовать.</span><span class="sxs-lookup"><span data-stu-id="11f89-272">This command will prompt for a password to be created and then used once.</span></span> <span data-ttu-id="11f89-273">Используйте надежный пароль.</span><span class="sxs-lookup"><span data-stu-id="11f89-273">Use a strong password.</span></span>

## <a name="create-pfx-files-for-client-certificates"></a><span data-ttu-id="11f89-274">Создание PFX-файлов для сертификатов клиента</span><span class="sxs-lookup"><span data-stu-id="11f89-274">Create PFX files for client certificates</span></span>
<span data-ttu-id="11f89-275">Для каждого созданного сертификата клиента выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="11f89-275">For each generated client certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="11f89-276">Настройка.</span><span class="sxs-lookup"><span data-stu-id="11f89-276">Customizing:</span></span>

    MyID.pvk and MyID.cer with the filename for the client certificate

<span data-ttu-id="11f89-277">Введите пароль, а затем экспортируйте сертификат с этими параметрами.</span><span class="sxs-lookup"><span data-stu-id="11f89-277">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="11f89-278">Да, экспортировать закрытый ключ</span><span class="sxs-lookup"><span data-stu-id="11f89-278">Yes, export the private key</span></span>
* <span data-ttu-id="11f89-279">Экспортировать все расширенные свойства.</span><span class="sxs-lookup"><span data-stu-id="11f89-279">Export all extended properties</span></span>
* <span data-ttu-id="11f89-280">Лицо, которому выдается данный сертификат, должно выбрать пароль экспорта</span><span class="sxs-lookup"><span data-stu-id="11f89-280">The individual to whom this certificate is being issued should choose the export password</span></span>

## <a name="import-client-certificate"></a><span data-ttu-id="11f89-281">Импорт сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="11f89-281">Import client certificate</span></span>
<span data-ttu-id="11f89-282">Каждое лицо, которому был выдан сертификат клиента, должно импортировать пару ключей в те компьютеры, которые данное лицо будет использовать для взаимодействия со службой:</span><span class="sxs-lookup"><span data-stu-id="11f89-282">Each individual for whom a client certificate has been issued should import the key pair in the machines he/she will use to communicate with the service:</span></span>

* <span data-ttu-id="11f89-283">Дважды щелкните .PFX-файл в проводнике Windows</span><span class="sxs-lookup"><span data-stu-id="11f89-283">Double-click the .PFX file in Windows Explorer</span></span>
* <span data-ttu-id="11f89-284">Импортируйте сертификат в личное хранилище по крайней мере с этим параметром:</span><span class="sxs-lookup"><span data-stu-id="11f89-284">Import certificate into the Personal store with at least this option:</span></span>
  * <span data-ttu-id="11f89-285">Включить все расширенные свойства проверки</span><span class="sxs-lookup"><span data-stu-id="11f89-285">Include all extended properties checked</span></span>

## <a name="copy-client-certificate-thumbprints"></a><span data-ttu-id="11f89-286">Копирование отпечатков сертификатов клиента</span><span class="sxs-lookup"><span data-stu-id="11f89-286">Copy client certificate thumbprints</span></span>
<span data-ttu-id="11f89-287">Каждое лицо, которому был выдан сертификат клиента, должно выполнить следующие шаги для получения отпечатка своего сертификата, который будет добавлен в файл конфигурации службы:</span><span class="sxs-lookup"><span data-stu-id="11f89-287">Each individual for whom a client certificate has been issued must follow these steps in order to obtain the thumbprint of his/hers certificate which will be added to the service configuration file:</span></span>

* <span data-ttu-id="11f89-288">Запустите certmgr.exe</span><span class="sxs-lookup"><span data-stu-id="11f89-288">Run certmgr.exe</span></span>
* <span data-ttu-id="11f89-289">Выберите вкладку Личные</span><span class="sxs-lookup"><span data-stu-id="11f89-289">Select the Personal tab</span></span>
* <span data-ttu-id="11f89-290">Дважды щелкните сертификат клиента, который будет использоваться для проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="11f89-290">Double-click the client certificate to be used for authentication</span></span>
* <span data-ttu-id="11f89-291">В открывшемся диалоговом окне сертификата перейдите на вкладку "Подробности"</span><span class="sxs-lookup"><span data-stu-id="11f89-291">In the Certificate dialog that opens, select the Details tab</span></span>
* <span data-ttu-id="11f89-292">Убедитесь, что в разделе "Показать" выбран вариант "Все"</span><span class="sxs-lookup"><span data-stu-id="11f89-292">Make sure Show is displaying All</span></span>
* <span data-ttu-id="11f89-293">Выберите в списке поле с именем "Отпечаток"</span><span class="sxs-lookup"><span data-stu-id="11f89-293">Select the field named Thumbprint in the list</span></span>
* <span data-ttu-id="11f89-294">Скопируйте значение отпечатка. ** Удалите неотображаемые знаки Юникода перед первой цифрой. ** Удалите все пробелы.</span><span class="sxs-lookup"><span data-stu-id="11f89-294">Copy the value of the thumbprint ** Delete non-visible Unicode characters in front of the first digit ** Delete all spaces</span></span>

## <a name="configure-allowed-clients-in-the-service-configuration-file"></a><span data-ttu-id="11f89-295">Настройка разрешенных клиентов в файле конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="11f89-295">Configure Allowed clients in the service configuration file</span></span>
<span data-ttu-id="11f89-296">Обновите значение следующего параметра в файле конфигурации службы списком отпечатков сертификатов клиента, разделенных запятыми, которым разрешен доступ к службе.</span><span class="sxs-lookup"><span data-stu-id="11f89-296">Update the value of the following setting in the service configuration file with a comma-separated list of the thumbprints of the client certificates allowed access to the service:</span></span>

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a><span data-ttu-id="11f89-297">Настройка проверки отзыва сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="11f89-297">Configure client certificate revocation check</span></span>
<span data-ttu-id="11f89-298">При значении по умолчанию проверка статуса отзыва сертификата клиента в центре сертификации не выполняется.</span><span class="sxs-lookup"><span data-stu-id="11f89-298">The default setting does not check with the Certification Authority for client certificate revocation status.</span></span> <span data-ttu-id="11f89-299">Чтобы включить проверку при ее поддержке центром сертификации, выдавшим сертификат клиента, измените следующий параметр одним из значений, определенных в перечислении X509RevocationMode:</span><span class="sxs-lookup"><span data-stu-id="11f89-299">To turn on the checks, if the Certification Authority which issued the client certificates supports such checks, change the following setting with one of the values defined in the X509RevocationMode Enumeration:</span></span>

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a><span data-ttu-id="11f89-300">Создание PFX-файла для самозаверяющих сертификатов шифрования</span><span class="sxs-lookup"><span data-stu-id="11f89-300">Create PFX file for self-signed encryption certificates</span></span>
<span data-ttu-id="11f89-301">Для сертификата шифрования выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="11f89-301">For an encryption certificate, execute:</span></span>

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

<span data-ttu-id="11f89-302">Настройка.</span><span class="sxs-lookup"><span data-stu-id="11f89-302">Customizing:</span></span>

    MyID.pvk and MyID.cer with the filename for the encryption certificate

<span data-ttu-id="11f89-303">Введите пароль, а затем экспортируйте сертификат с этими параметрами.</span><span class="sxs-lookup"><span data-stu-id="11f89-303">Enter password and then export certificate with these options:</span></span>

* <span data-ttu-id="11f89-304">Да, экспортировать закрытый ключ</span><span class="sxs-lookup"><span data-stu-id="11f89-304">Yes, export the private key</span></span>
* <span data-ttu-id="11f89-305">Экспортировать все расширенные свойства.</span><span class="sxs-lookup"><span data-stu-id="11f89-305">Export all extended properties</span></span>
* <span data-ttu-id="11f89-306">При отправке сертификата в облачную службу потребуется пароль.</span><span class="sxs-lookup"><span data-stu-id="11f89-306">You will need the password when uploading the certificate to the cloud service.</span></span>

## <a name="export-encryption-certificate-from-certificate-store"></a><span data-ttu-id="11f89-307">Экспорт сертификата шифрования из хранилища сертификатов</span><span class="sxs-lookup"><span data-stu-id="11f89-307">Export encryption certificate from certificate store</span></span>
* <span data-ttu-id="11f89-308">Поиск сертификата</span><span class="sxs-lookup"><span data-stu-id="11f89-308">Find certificate</span></span>
* <span data-ttu-id="11f89-309">Выберите «Действия > Все задачи > Экспортировать…»</span><span class="sxs-lookup"><span data-stu-id="11f89-309">Click Actions -> All tasks -> Export…</span></span>
* <span data-ttu-id="11f89-310">Экспортируйте сертификат в PFX-файл со следующими параметрами.</span><span class="sxs-lookup"><span data-stu-id="11f89-310">Export certificate into a .PFX file with these options:</span></span> 
  * <span data-ttu-id="11f89-311">Да, экспортировать закрытый ключ</span><span class="sxs-lookup"><span data-stu-id="11f89-311">Yes, export the private key</span></span>
  * <span data-ttu-id="11f89-312">Включить, по возможности, все сертификаты в путь сертификации</span><span class="sxs-lookup"><span data-stu-id="11f89-312">Include all certificates in the certification path if possible</span></span> 
* <span data-ttu-id="11f89-313">Экспортировать все расширенные свойства.</span><span class="sxs-lookup"><span data-stu-id="11f89-313">Export all extended properties</span></span>

## <a name="upload-encryption-certificate-to-cloud-service"></a><span data-ttu-id="11f89-314">Передача сертификата шифрования в облачную службу</span><span class="sxs-lookup"><span data-stu-id="11f89-314">Upload encryption certificate to cloud service</span></span>
<span data-ttu-id="11f89-315">Отправьте сертификат с существующим или созданным .PFX-файлом с помощью пары ключей SSL.</span><span class="sxs-lookup"><span data-stu-id="11f89-315">Upload certificate with the existing or generated .PFX file with the encryption key pair:</span></span>

* <span data-ttu-id="11f89-316">Введите пароль, защищающий данные закрытого ключа</span><span class="sxs-lookup"><span data-stu-id="11f89-316">Enter the password protecting the private key information</span></span>

## <a name="update-encryption-certificate-in-service-configuration-file"></a><span data-ttu-id="11f89-317">Обновление сертификата шифрования в файле конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="11f89-317">Update encryption certificate in service configuration file</span></span>
<span data-ttu-id="11f89-318">Замените значения отпечатка следующих параметров в файле конфигурации службы значением отпечатка сертификата, отправленного в облачную службу.</span><span class="sxs-lookup"><span data-stu-id="11f89-318">Update the thumbprint value of the following settings in the service configuration file with the thumbprint of the certificate uploaded to the cloud service:</span></span>

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a><span data-ttu-id="11f89-319">Стандартные операции сертификата</span><span class="sxs-lookup"><span data-stu-id="11f89-319">Common certificate operations</span></span>
* <span data-ttu-id="11f89-320">Настройка SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="11f89-320">Configure the SSL certificate</span></span>
* <span data-ttu-id="11f89-321">Настройка сертификатов клиентов</span><span class="sxs-lookup"><span data-stu-id="11f89-321">Configure client certificates</span></span>

## <a name="find-certificate"></a><span data-ttu-id="11f89-322">Поиск сертификата</span><span class="sxs-lookup"><span data-stu-id="11f89-322">Find certificate</span></span>
<span data-ttu-id="11f89-323">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="11f89-323">Follow these steps:</span></span>

1. <span data-ttu-id="11f89-324">Запустите mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="11f89-324">Run mmc.exe.</span></span>
2. <span data-ttu-id="11f89-325">Файл -> Добавить/удалить оснастку...</span><span class="sxs-lookup"><span data-stu-id="11f89-325">File -> Add/Remove Snap-in…</span></span>
3. <span data-ttu-id="11f89-326">Выберите **Сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="11f89-326">Select **Certificates**.</span></span>
4. <span data-ttu-id="11f89-327">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="11f89-327">Click **Add**.</span></span>
5. <span data-ttu-id="11f89-328">Выберите расположение хранилища сертификатов.</span><span class="sxs-lookup"><span data-stu-id="11f89-328">Choose the certificate store location.</span></span>
6. <span data-ttu-id="11f89-329">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="11f89-329">Click **Finish**.</span></span>
7. <span data-ttu-id="11f89-330">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="11f89-330">Click **OK**.</span></span>
8. <span data-ttu-id="11f89-331">Разверните узел **Сертификаты**.</span><span class="sxs-lookup"><span data-stu-id="11f89-331">Expand **Certificates**.</span></span>
9. <span data-ttu-id="11f89-332">Разверните хранилище сертификатов.</span><span class="sxs-lookup"><span data-stu-id="11f89-332">Expand the certificate store node.</span></span>
10. <span data-ttu-id="11f89-333">Разверните дочерний узел сертификата.</span><span class="sxs-lookup"><span data-stu-id="11f89-333">Expand the Certificate child node.</span></span>
11. <span data-ttu-id="11f89-334">Выберите сертификат из списка.</span><span class="sxs-lookup"><span data-stu-id="11f89-334">Select a certificate in the list.</span></span>

## <a name="export-certificate"></a><span data-ttu-id="11f89-335">Экспорт сертификата</span><span class="sxs-lookup"><span data-stu-id="11f89-335">Export certificate</span></span>
<span data-ttu-id="11f89-336">В **мастере экспорта сертификатов**:</span><span class="sxs-lookup"><span data-stu-id="11f89-336">In the **Certificate Export Wizard**:</span></span>

1. <span data-ttu-id="11f89-337">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="11f89-337">Click **Next**.</span></span>
2. <span data-ttu-id="11f89-338">Выберите **Да**, а затем — **Export the private key** (Экспортировать закрытый ключ).</span><span class="sxs-lookup"><span data-stu-id="11f89-338">Select **Yes**, then **Export the private key**.</span></span>
3. <span data-ttu-id="11f89-339">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="11f89-339">Click **Next**.</span></span>
4. <span data-ttu-id="11f89-340">Выберите нужный формат выходного файла.</span><span class="sxs-lookup"><span data-stu-id="11f89-340">Select the desired output file format.</span></span>
5. <span data-ttu-id="11f89-341">Проверьте необходимые параметры.</span><span class="sxs-lookup"><span data-stu-id="11f89-341">Check the desired options.</span></span>
6. <span data-ttu-id="11f89-342">Проверьте **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="11f89-342">Check **Password**.</span></span>
7. <span data-ttu-id="11f89-343">Введите надежный пароль и подтвердите его.</span><span class="sxs-lookup"><span data-stu-id="11f89-343">Enter a strong password and confirm it.</span></span>
8. <span data-ttu-id="11f89-344">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="11f89-344">Click **Next**.</span></span>
9. <span data-ttu-id="11f89-345">Введите или выберите имя файла, в котором будет храниться сертификат (используйте расширение .PFX).</span><span class="sxs-lookup"><span data-stu-id="11f89-345">Type or browse a filename where to store the certificate (use a .PFX extension).</span></span>
10. <span data-ttu-id="11f89-346">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="11f89-346">Click **Next**.</span></span>
11. <span data-ttu-id="11f89-347">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="11f89-347">Click **Finish**.</span></span>
12. <span data-ttu-id="11f89-348">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="11f89-348">Click **OK**.</span></span>

## <a name="import-certificate"></a><span data-ttu-id="11f89-349">Импорт сертификата</span><span class="sxs-lookup"><span data-stu-id="11f89-349">Import certificate</span></span>
<span data-ttu-id="11f89-350">В мастере импорта сертификатов:</span><span class="sxs-lookup"><span data-stu-id="11f89-350">In the Certificate Import Wizard:</span></span>

1. <span data-ttu-id="11f89-351">Выберите расположение хранилища.</span><span class="sxs-lookup"><span data-stu-id="11f89-351">Select the store location.</span></span>
   
   * <span data-ttu-id="11f89-352">Выберите **Текущий пользователь** , если доступ к службе будет только у тех процессов, которые запущены под учетной записью текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="11f89-352">Select **Current User** if only processes running under current user will access the service</span></span>
   * <span data-ttu-id="11f89-353">Выберите **Локальный компьютер** , если доступ к службе будет и у других процессов на этом компьютере.</span><span class="sxs-lookup"><span data-stu-id="11f89-353">Select **Local Machine** if other processes in this computer will access the service</span></span>
2. <span data-ttu-id="11f89-354">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="11f89-354">Click **Next**.</span></span>
3. <span data-ttu-id="11f89-355">При импорте из файла подтвердите путь к файлу.</span><span class="sxs-lookup"><span data-stu-id="11f89-355">If importing from a file, confirm the file path.</span></span>
4. <span data-ttu-id="11f89-356">При импорте .PFX-файла:</span><span class="sxs-lookup"><span data-stu-id="11f89-356">If importing a .PFX file:</span></span>
   1. <span data-ttu-id="11f89-357">Введите пароль, защищающий закрытый ключ</span><span class="sxs-lookup"><span data-stu-id="11f89-357">Enter the password protecting the private key</span></span>
   2. <span data-ttu-id="11f89-358">Выберите параметры импорта</span><span class="sxs-lookup"><span data-stu-id="11f89-358">Select import options</span></span>
5. <span data-ttu-id="11f89-359">Выберите "Разместить" сертификаты в следующее хранилище.</span><span class="sxs-lookup"><span data-stu-id="11f89-359">Select "Place" certificates in the following store</span></span>
6. <span data-ttu-id="11f89-360">Щелкните **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="11f89-360">Click **Browse**.</span></span>
7. <span data-ttu-id="11f89-361">Выберите нужное хранилище.</span><span class="sxs-lookup"><span data-stu-id="11f89-361">Select the desired store.</span></span>
8. <span data-ttu-id="11f89-362">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="11f89-362">Click **Finish**.</span></span>
   
   * <span data-ttu-id="11f89-363">Если хранилище доверенного корневого центра сертификации выбрано, щелкните **Да**.</span><span class="sxs-lookup"><span data-stu-id="11f89-363">If the Trusted Root Certification Authority store was chosen, click **Yes**.</span></span>
9. <span data-ttu-id="11f89-364">Нажмите кнопку **ОК** во всех диалоговых окнах.</span><span class="sxs-lookup"><span data-stu-id="11f89-364">Click **OK** on all dialog windows.</span></span>

## <a name="upload-certificate"></a><span data-ttu-id="11f89-365">Передача сертификата</span><span class="sxs-lookup"><span data-stu-id="11f89-365">Upload certificate</span></span>
<span data-ttu-id="11f89-366">На [портале Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="11f89-366">In the [Azure Portal](https://portal.azure.com/)</span></span>

1. <span data-ttu-id="11f89-367">Выберите **Облачные службы**.</span><span class="sxs-lookup"><span data-stu-id="11f89-367">Select **Cloud Services**.</span></span>
2. <span data-ttu-id="11f89-368">Выберите облачную службу.</span><span class="sxs-lookup"><span data-stu-id="11f89-368">Select the cloud service.</span></span>
3. <span data-ttu-id="11f89-369">Щелкните **Сертификаты**в верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="11f89-369">On the top menu, click **Certificates**.</span></span>
4. <span data-ttu-id="11f89-370">На нижней панели щелкните **Передать**.</span><span class="sxs-lookup"><span data-stu-id="11f89-370">On the bottom bar, click **Upload**.</span></span>
5. <span data-ttu-id="11f89-371">Выберите файл сертификата.</span><span class="sxs-lookup"><span data-stu-id="11f89-371">Select the certificate file.</span></span>
6. <span data-ttu-id="11f89-372">Если это PFX-файл, введите пароль для закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="11f89-372">If it is a .PFX file, enter the password for the private key.</span></span>
7. <span data-ttu-id="11f89-373">После завершения скопируйте отпечаток сертификата из новой записи в списке.</span><span class="sxs-lookup"><span data-stu-id="11f89-373">Once completed, copy the certificate thumbprint from the new entry in the list.</span></span>

## <a name="other-security-considerations"></a><span data-ttu-id="11f89-374">Прочие вопросы по безопасности</span><span class="sxs-lookup"><span data-stu-id="11f89-374">Other security considerations</span></span>
<span data-ttu-id="11f89-375">Описанные в этом документе параметры SSL выполняют шифрование обмена данными между службой и ее клиентами при использовании в конечной точке HTTPS.</span><span class="sxs-lookup"><span data-stu-id="11f89-375">The SSL settings described in this document encrypt communication between the service and its clients when the HTTPS endpoint is used.</span></span> <span data-ttu-id="11f89-376">Это важно, поскольку учетные данные для доступа к базе данных и другие конфиденциальные сведения передаются по каналу связи.</span><span class="sxs-lookup"><span data-stu-id="11f89-376">This is important since credentials for database access and potentially other sensitive information are contained in the communication.</span></span> <span data-ttu-id="11f89-377">Обратите внимание, что служба сохраняет внутренний статус, включая учетные данные, в своих внутренних таблицах базы данных SQL Microsoft Azure, предоставленной вам для хранения метаданных при получении подписки на Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="11f89-377">Note, however, that the service persists internal status, including credentials, in its internal tables in the Microsoft Azure SQL database that you have provided for metadata storage in your Microsoft Azure subscription.</span></span> <span data-ttu-id="11f89-378">База данных была определена как часть следующего параметра в вашем файле конфигурации службы (файл .CSCFG):</span><span class="sxs-lookup"><span data-stu-id="11f89-378">That database was defined as part of the following setting in your service configuration file (.CSCFG file):</span></span> 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

<span data-ttu-id="11f89-379">Учетные данные, хранящиеся в этой базе данных, будут зашифрованы.</span><span class="sxs-lookup"><span data-stu-id="11f89-379">Credentials stored in this database are encrypted.</span></span> <span data-ttu-id="11f89-380">Однако рекомендуется убедиться что веб-роли и рабочие роли развертываний службы актуальны и защищены, так как имеют доступ к базе данных метаданных и сертификату, используемому для шифрования и расшифровки сохраненных учетных данных.</span><span class="sxs-lookup"><span data-stu-id="11f89-380">However, as a best practice, ensure that both web and worker roles of your service deployments are kept up to date and secure as they both have access to the metadata database and the certificate used for encryption and decryption of stored credentials.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

