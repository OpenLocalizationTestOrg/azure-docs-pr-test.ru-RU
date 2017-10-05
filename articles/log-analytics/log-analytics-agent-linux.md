---
title: "Подключение компьютеров Linux к Operations Management Suite (OMS) | Документация Майкрософт"
description: "В этой статье описывается подключение компьютеров Linux, размещенных в Azure, другой облачной службе или локальной среде, к OMS с помощью агента OMS для Linux."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: magoedte
ms.openlocfilehash: 1c05f68235aafd0fa098a3b0edaba1258df09380
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-linux-computers-to-operations-management-suite-oms"></a><span data-ttu-id="3b8c3-103">Подключение компьютеров Linux к Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="3b8c3-103">Connect your Linux Computers to Operations Management Suite (OMS)</span></span> 

<span data-ttu-id="3b8c3-104">С помощью Microsoft Operations Management Suite (OMS) можно собирать и использовать данные, созданные на компьютерах под управлением Linux и в контейнерах (например, Docker), расположенных в локальном центре обработки данных как физические серверы или виртуальные машины либо виртуальные машины в облачной службе (например, Amazon Web Services (AWS) или Microsoft Azure).</span><span class="sxs-lookup"><span data-stu-id="3b8c3-104">With Microsoft Operations Management Suite (OMS), you can collect and act on data generated from Linux computers and container solutions like Docker, residing in your on-premises data center as physical servers or virtual machines, virtual machines in a cloud-hosted service like Amazon Web Services (AWS) or Microsoft Azure.</span></span> <span data-ttu-id="3b8c3-105">Также можно использовать доступные в OMS решения для управления: например функцию отслеживания изменений конфигурации и функцию управления обновлениями программного обеспечения. Эти решения позволяют выполнять упреждающее управление жизненным циклом виртуальных машин Linux.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-105">You can also use management solutions available in OMS such as Change Tracking, to identify configuration changes, and Update Management to manage software updates to proactively manage the lifecycle of your Linux VMs.</span></span> 

<span data-ttu-id="3b8c3-106">Агент OMS для Linux обменивается исходящими данными со службой OMS через TCP-порт 443. Если компьютер подключен к брандмауэру или прокси-серверу для обмена данными через Интернет, ознакомьтесь с разделом [Настройка агента для использования со шлюзом OMS или прокси-сервером HTTP](#configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway), чтобы применить необходимые изменения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-106">The OMS Agent for Linux communicates outbound with the OMS service over TCP port 443, and if the computer connects to a firewall or proxy server to communicate over the Internet, review [Configuring the agent for use with an HTTP proxy server or OMS Gateway](#configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway) to understand what configuration changes will need to be applied.</span></span>  <span data-ttu-id="3b8c3-107">Компьютер, отслеживаемый решением System Center 2016 Operations Manager или Operations Manager 2012 R2, может использоваться как многосетевой: с помощью службы OMS будет выполняться сбор данных и их пересылка в службу, а компьютер по-прежнему будет отслеживаться решением Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-107">If you are monitoring the computer with System Center 2016 - Operations Manager or Operations Manager 2012 R2, it can be multi-homed with the OMS service to collect data and forward to the service and still be monitored by Operations Manager.</span></span>  <span data-ttu-id="3b8c3-108">Компьютеры Linux, отслеживаемые группой управления Operations Manager, интегрированной с OMS, не получают конфигурацию для источников данных. Они пересылают собранные данные через группы управления.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-108">Linux computers monitored by an Operations Manager management group that is integrated with OMS do not receive configuration for data sources and forward collected data through the management group.</span></span>  <span data-ttu-id="3b8c3-109">Агент OMS нельзя настроить для отправки отчетов в несколько рабочих областей.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-109">The OMS agent cannot be configured to report to more than one workspace.</span></span>  

<span data-ttu-id="3b8c3-110">Если политики ИТ-безопасности запрещают подключение компьютеров в сети к Интернету, агент можно настроить для подключения к шлюзу OMS. Так он сможет получать сведения о конфигурации и отправлять собранные данные в зависимости от включенного решения.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-110">If your IT security policies do not allow computers on your network to connect to the Internet, the agent can be configured to connect to the OMS Gateway to receive configuration information and send collected data depending on the solution you have enabled.</span></span> <span data-ttu-id="3b8c3-111">Дополнительные сведения и инструкции по настройке агента OMS Linux для обмена данными со службой OMS через шлюз OMS см. в статье [Подключения компьютеров к OMS с помощью шлюза OMS без доступа к Интернету](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="3b8c3-111">For more information and steps on how to configure your OMS Linux Agent to communicate through an OMS Gateway to the OMS service, see [Connect computers to OMS using the OMS Gateway](log-analytics-oms-gateway.md).</span></span>  

<span data-ttu-id="3b8c3-112">Ниже представлена схема подключения между компьютерами Linux, управляемыми агентом, и OMS, включая направление и порты.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-112">The following diagram depicts the connection between the agent-managed Linux computers and OMS, including the direction and ports.</span></span>

![Схема взаимодействия прямого агента с OMS](./media/log-analytics-agent-linux/log-analytics-agent-linux-communication.png)

## <a name="system-requirements"></a><span data-ttu-id="3b8c3-114">Требования к системе</span><span class="sxs-lookup"><span data-stu-id="3b8c3-114">System requirements</span></span>
<span data-ttu-id="3b8c3-115">Сначала необходимо выполнить следующие требования.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-115">Before starting, review the following details to verify you meet the prerequisites.</span></span>

### <a name="supported-linux-operating-systems"></a><span data-ttu-id="3b8c3-116">Поддерживаемые операционные системы Linux</span><span class="sxs-lookup"><span data-stu-id="3b8c3-116">Supported Linux operating systems</span></span>
<span data-ttu-id="3b8c3-117">Официально поддерживаются следующие дистрибутивы Linux.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-117">The following Linux distributions are officially supported.</span></span>  <span data-ttu-id="3b8c3-118">Однако агент OMS для Linux может выполняться и на других дистрибутивах, помимо следующих:</span><span class="sxs-lookup"><span data-stu-id="3b8c3-118">However, the OMS Agent for Linux might also run on other distributions not listed.</span></span>

* <span data-ttu-id="3b8c3-119">Amazon Linux 2012.09–2015.09 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="3b8c3-119">Amazon Linux 2012.09 to 2015.09 (x86/x64)</span></span>
* <span data-ttu-id="3b8c3-120">CentOS Linux 5, 6 и 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="3b8c3-120">CentOS Linux 5, 6, and 7 (x86/x64)</span></span>
* <span data-ttu-id="3b8c3-121">Oracle Linux 5, 6 и 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="3b8c3-121">Oracle Linux 5, 6, and 7 (x86/x64)</span></span>
* <span data-ttu-id="3b8c3-122">Red Hat Enterprise Linux Server 5, 6 и 7 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="3b8c3-122">Red Hat Enterprise Linux Server 5, 6 and 7 (x86/x64)</span></span>
* <span data-ttu-id="3b8c3-123">Debian GNU/Linux 6, 7 и 8 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="3b8c3-123">Debian GNU/Linux 6, 7, and 8 (x86/x64)</span></span>
* <span data-ttu-id="3b8c3-124">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="3b8c3-124">Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10, 16.04 LTS (x86/x64)</span></span>
* <span data-ttu-id="3b8c3-125">SUSE Linux Enterprise Server 11 и 12 (x86/x64)</span><span class="sxs-lookup"><span data-stu-id="3b8c3-125">SUSE Linux Enterprise Server 11 and 12 (x86/x64)</span></span>

### <a name="network"></a><span data-ttu-id="3b8c3-126">Сеть</span><span class="sxs-lookup"><span data-stu-id="3b8c3-126">Network</span></span>
<span data-ttu-id="3b8c3-127">Ниже приводятся сведения о конфигурации прокси-сервера и брандмауэра, необходимые для взаимодействия агента Linux с OMS.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-127">The information below list the proxy and firewall configuration information required for the Linux agent to communicate with OMS.</span></span> <span data-ttu-id="3b8c3-128">Трафик является исходящим из локальной сети к службе OMS.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-128">Traffic is outbound from your network to the OMS service.</span></span> 

|<span data-ttu-id="3b8c3-129">Ресурс агента</span><span class="sxs-lookup"><span data-stu-id="3b8c3-129">Agent Resource</span></span>| <span data-ttu-id="3b8c3-130">порты;</span><span class="sxs-lookup"><span data-stu-id="3b8c3-130">Ports</span></span> |  
|------|---------|  
|<span data-ttu-id="3b8c3-131">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="3b8c3-131">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="3b8c3-132">Порт 443</span><span class="sxs-lookup"><span data-stu-id="3b8c3-132">Port 443</span></span>|   
|<span data-ttu-id="3b8c3-133">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="3b8c3-133">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="3b8c3-134">Порт 443</span><span class="sxs-lookup"><span data-stu-id="3b8c3-134">Port 443</span></span>|   
|<span data-ttu-id="3b8c3-135">*.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="3b8c3-135">*.blob.core.windows.net/</span></span> | <span data-ttu-id="3b8c3-136">Порт 443</span><span class="sxs-lookup"><span data-stu-id="3b8c3-136">Port 443</span></span>|   
|<span data-ttu-id="3b8c3-137">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="3b8c3-137">*.azure-automation.net</span></span> | <span data-ttu-id="3b8c3-138">Порт 443</span><span class="sxs-lookup"><span data-stu-id="3b8c3-138">Port 443</span></span>|  

### <a name="package-requirements"></a><span data-ttu-id="3b8c3-139">Требования к пакетам</span><span class="sxs-lookup"><span data-stu-id="3b8c3-139">Package requirements</span></span>

 <span data-ttu-id="3b8c3-140">**Требуемый пакет**</span><span class="sxs-lookup"><span data-stu-id="3b8c3-140">**Required package**</span></span>   | <span data-ttu-id="3b8c3-141">**Описание**</span><span class="sxs-lookup"><span data-stu-id="3b8c3-141">**Description**</span></span>   | <span data-ttu-id="3b8c3-142">**Минимальная версия**</span><span class="sxs-lookup"><span data-stu-id="3b8c3-142">**Minimum version**</span></span>
--------------------- | --------------------- | -------------------
<span data-ttu-id="3b8c3-143">Glibc</span><span class="sxs-lookup"><span data-stu-id="3b8c3-143">Glibc</span></span> | <span data-ttu-id="3b8c3-144">Библиотека C GNU</span><span class="sxs-lookup"><span data-stu-id="3b8c3-144">GNU C Library</span></span>   | <span data-ttu-id="3b8c3-145">2.5-12</span><span class="sxs-lookup"><span data-stu-id="3b8c3-145">2.5-12</span></span> 
<span data-ttu-id="3b8c3-146">Openssl</span><span class="sxs-lookup"><span data-stu-id="3b8c3-146">Openssl</span></span> | <span data-ttu-id="3b8c3-147">Библиотеки OpenSSL</span><span class="sxs-lookup"><span data-stu-id="3b8c3-147">OpenSSL Libraries</span></span> | <span data-ttu-id="3b8c3-148">0.9.8e или 1.0</span><span class="sxs-lookup"><span data-stu-id="3b8c3-148">0.9.8e or 1.0</span></span>
<span data-ttu-id="3b8c3-149">Curl</span><span class="sxs-lookup"><span data-stu-id="3b8c3-149">Curl</span></span> | <span data-ttu-id="3b8c3-150">Веб-клиент cURL</span><span class="sxs-lookup"><span data-stu-id="3b8c3-150">cURL web client</span></span> | <span data-ttu-id="3b8c3-151">7.15.5</span><span class="sxs-lookup"><span data-stu-id="3b8c3-151">7.15.5</span></span>
<span data-ttu-id="3b8c3-152">Python-ctypes</span><span class="sxs-lookup"><span data-stu-id="3b8c3-152">Python-ctypes</span></span> | | 
<span data-ttu-id="3b8c3-153">PAM</span><span class="sxs-lookup"><span data-stu-id="3b8c3-153">PAM</span></span> | <span data-ttu-id="3b8c3-154">Подключаемые модули аутентификации</span><span class="sxs-lookup"><span data-stu-id="3b8c3-154">Pluggable authentication Modules</span></span> | 

> [!NOTE]
>  <span data-ttu-id="3b8c3-155">Для сбора сообщений системного журнала требуется rsyslog или syslog-ng.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-155">Either rsyslog or syslog-ng are required to collect syslog messages.</span></span> <span data-ttu-id="3b8c3-156">Управляющая программа syslog по умолчанию не поддерживается для сбора событий системного журнала в Red Hat Enterprise Linux версии 5, CentOS и Oracle Linux (sysklog).</span><span class="sxs-lookup"><span data-stu-id="3b8c3-156">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="3b8c3-157">Чтобы собирать данные системного журнала из дистрибутивов этих версий, требуется установить и настроить управляющую программу rsyslog, которая заменит sysklog.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-157">To collect syslog data from this version of these distributions, the rsyslog daemon should be installed and configured to replace sysklog,</span></span> 

<span data-ttu-id="3b8c3-158">Этот агент включает в себя несколько пакетов.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-158">The agent includes multiple packages.</span></span> <span data-ttu-id="3b8c3-159">Файл выпуска содержит указанные ниже пакеты, доступ к которым можно получить, запустив пакет оболочки с помощью команды `--extract`.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-159">The release file contains the following packages, available by running the shell bundle with `--extract`:</span></span>

<span data-ttu-id="3b8c3-160">**Package**</span><span class="sxs-lookup"><span data-stu-id="3b8c3-160">**Package**</span></span> | <span data-ttu-id="3b8c3-161">**Версия**</span><span class="sxs-lookup"><span data-stu-id="3b8c3-161">**Version**</span></span> | <span data-ttu-id="3b8c3-162">**Описание**</span><span class="sxs-lookup"><span data-stu-id="3b8c3-162">**Description**</span></span>
----------- | ----------- | --------------
<span data-ttu-id="3b8c3-163">omsagent</span><span class="sxs-lookup"><span data-stu-id="3b8c3-163">omsagent</span></span> | <span data-ttu-id="3b8c3-164">1.4.0</span><span class="sxs-lookup"><span data-stu-id="3b8c3-164">1.4.0</span></span> | <span data-ttu-id="3b8c3-165">Агент Operations Management Suite для Linux</span><span class="sxs-lookup"><span data-stu-id="3b8c3-165">The Operations Management Suite Agent for Linux</span></span>
<span data-ttu-id="3b8c3-166">omsconfig</span><span class="sxs-lookup"><span data-stu-id="3b8c3-166">omsconfig</span></span> | <span data-ttu-id="3b8c3-167">1.1.1</span><span class="sxs-lookup"><span data-stu-id="3b8c3-167">1.1.1</span></span> | <span data-ttu-id="3b8c3-168">Агент конфигурации для агента OMS</span><span class="sxs-lookup"><span data-stu-id="3b8c3-168">Configuration agent for the OMS Agent</span></span>
<span data-ttu-id="3b8c3-169">omi</span><span class="sxs-lookup"><span data-stu-id="3b8c3-169">omi</span></span> | <span data-ttu-id="3b8c3-170">1.2.0</span><span class="sxs-lookup"><span data-stu-id="3b8c3-170">1.2.0</span></span> | <span data-ttu-id="3b8c3-171">OMI (Open Management Infrastructure) — облегченная версия сервера CIM</span><span class="sxs-lookup"><span data-stu-id="3b8c3-171">Open Management Infrastructure (OMI) - a lightweight CIM Server</span></span>
<span data-ttu-id="3b8c3-172">scx</span><span class="sxs-lookup"><span data-stu-id="3b8c3-172">scx</span></span> | <span data-ttu-id="3b8c3-173">1.6.3</span><span class="sxs-lookup"><span data-stu-id="3b8c3-173">1.6.3</span></span> | <span data-ttu-id="3b8c3-174">Поставщики OMI CIM для метрик производительности операционной системы</span><span class="sxs-lookup"><span data-stu-id="3b8c3-174">OMI CIM Providers for operating system performance metrics</span></span>
<span data-ttu-id="3b8c3-175">apache-cimprov</span><span class="sxs-lookup"><span data-stu-id="3b8c3-175">apache-cimprov</span></span> | <span data-ttu-id="3b8c3-176">1.0.1</span><span class="sxs-lookup"><span data-stu-id="3b8c3-176">1.0.1</span></span> | <span data-ttu-id="3b8c3-177">Поставщик мониторинга производительности сервера Apache HTTP Server для OMI.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-177">Apache HTTP Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="3b8c3-178">Устанавливается при обнаружении сервера Apache HTTP Server.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-178">Installed if Apache HTTP Server is detected.</span></span>
<span data-ttu-id="3b8c3-179">mysql-cimprov</span><span class="sxs-lookup"><span data-stu-id="3b8c3-179">mysql-cimprov</span></span> | <span data-ttu-id="3b8c3-180">1.0.1</span><span class="sxs-lookup"><span data-stu-id="3b8c3-180">1.0.1</span></span> | <span data-ttu-id="3b8c3-181">Поставщик мониторинга производительности сервера MySQL для OMI.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-181">MySQL Server performance monitoring provider for OMI.</span></span> <span data-ttu-id="3b8c3-182">Устанавливается при обнаружении сервера MySQL или MariaDB.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-182">Installed if MySQL/MariaDB server is detected.</span></span>
<span data-ttu-id="3b8c3-183">docker-cimprov</span><span class="sxs-lookup"><span data-stu-id="3b8c3-183">docker-cimprov</span></span> | <span data-ttu-id="3b8c3-184">1.0.0</span><span class="sxs-lookup"><span data-stu-id="3b8c3-184">1.0.0</span></span> | <span data-ttu-id="3b8c3-185">Поставщик Docker для OMI.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-185">Docker provider for OMI.</span></span> <span data-ttu-id="3b8c3-186">Устанавливается при обнаружении Docker.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-186">Installed if Docker is detected.</span></span>

### <a name="compatibility-with-system-center-operations-manager"></a><span data-ttu-id="3b8c3-187">Совместимость с System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="3b8c3-187">Compatibility with System Center Operations Manager</span></span>
<span data-ttu-id="3b8c3-188">Агент OMS для Linux совместно использует двоичные файлы агента с агентом System Center Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-188">The OMS Agent for Linux shares agent binaries with the System Center Operations Manager agent.</span></span> <span data-ttu-id="3b8c3-189">При установке агента OMS для Linux в системе под управлением Operations Manager пакеты OMI и SCX на компьютере обновляются до более новой версии.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-189">If you install the OMS Agent for Linux on a system currently managed by Operations Manager, it the OMI and SCX packages on the computer to a newer version.</span></span> <span data-ttu-id="3b8c3-190">В этом выпуске агенты OMS и System Center 2016 Operations Manager или Operations Manager 2012 R2 для Linux являются совместимыми.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-190">In this release, the OMS and System Center 2016 - Operations Manager/Operations Manager 2012 R2 agents for Linux are compatible.</span></span> 

> [!NOTE]
> <span data-ttu-id="3b8c3-191">Сейчас System Center 2012 с пакетом обновления 1 (SP1) и более ранние версии не совместимы с агентом OMS для Linux и не поддерживаются им.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-191">System Center 2012 SP1 and earlier versions are currently not compatible or supported with the OMS Agent for Linux.</span></span><br>
> <span data-ttu-id="3b8c3-192">Если агент OMS для Linux устанавливается на компьютер, который сейчас не отслеживается решением Operations Manager, но такое отслеживание требуется в будущем, нужно изменить [конфигурацию OMI](#enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager) до обнаружения компьютера.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-192">If the OMS Agent for Linux is installed to a computer that is not currently monitored by Operations Manager, and you then wish to monitor the computer with Operations Manager, you must modify the [OMI configuration](#enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager) prior to discovering the computer.</span></span> <span data-ttu-id="3b8c3-193">**Этот шаг *не* нужно выполнять, если агент Operations Manager установлен ранее, чем агент OMS для Linux.**</span><span class="sxs-lookup"><span data-stu-id="3b8c3-193">**This step is *not* needed if the Operations Manager agent is installed before the OMS Agent for Linux.**</span></span>

### <a name="system-configuration-changes"></a><span data-ttu-id="3b8c3-194">Изменения конфигурации системы</span><span class="sxs-lookup"><span data-stu-id="3b8c3-194">System configuration changes</span></span>
<span data-ttu-id="3b8c3-195">После установки пакетов агента OMS для Linux применяются следующие изменения конфигурации системы.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-195">After installing the OMS Agent for Linux packages, the following additional system-wide configuration changes are applied.</span></span> <span data-ttu-id="3b8c3-196">Эти артефакты удаляются после удаления пакета omsagent.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-196">These artifacts are removed when the omsagent package is uninstalled.</span></span>

* <span data-ttu-id="3b8c3-197">Создается непривилегированный пользователь с именем `omsagent` .</span><span class="sxs-lookup"><span data-stu-id="3b8c3-197">A non-privileged user named: `omsagent` is created.</span></span> <span data-ttu-id="3b8c3-198">Это учетная запись, от имени которой запускается управляющая программа omsagent.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-198">This is the account the omsagent daemon runs as.</span></span>
* <span data-ttu-id="3b8c3-199">В каталоге /etc/sudoers.d/omsagent создается файл sudoers с директивами include.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-199">A sudoers “include” file is created at /etc/sudoers.d/omsagent.</span></span> <span data-ttu-id="3b8c3-200">Так пользователь omsagent получает право на перезапуск управляющих программ syslog и omsagent.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-200">This authorizes omsagent to restart the syslog and omsagent daemons.</span></span> <span data-ttu-id="3b8c3-201">Если директивы sudo "include" не поддерживаются в установленной версии sudo, эти записи будут записываться в каталог /etc/sudoers.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-201">If sudo “include” directives are not supported in the installed version of sudo, these entries are written to /etc/sudoers.</span></span>
* <span data-ttu-id="3b8c3-202">Конфигурация системного журнала настраивается для перенаправления подмножества событий агенту.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-202">The syslog configuration is modified to forward a subset of events to the agent.</span></span> <span data-ttu-id="3b8c3-203">Дополнительные сведения см. в разделе о **настройке сбора данных** ниже.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-203">For more information, see the **Configuring Data Collection** section below</span></span>

### <a name="upgrade-from-a-previous-release"></a><span data-ttu-id="3b8c3-204">Обновление предыдущей версии</span><span class="sxs-lookup"><span data-stu-id="3b8c3-204">Upgrade from a previous release</span></span>
<span data-ttu-id="3b8c3-205">В этом выпуске поддерживаются обновления версий ниже 1.0.0-47.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-205">Upgrade from versions earlier than 1.0.0-47 is supported in this release.</span></span> <span data-ttu-id="3b8c3-206">При установке с помощью команды `--upgrade` все компоненты агента будут обновлены до последней версии.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-206">Performing the installation with the `--upgrade` command upgrades all components of the agent to the latest version.</span></span>

## <a name="installing-the-agent"></a><span data-ttu-id="3b8c3-207">Установка агента</span><span class="sxs-lookup"><span data-stu-id="3b8c3-207">Installing the agent</span></span>

<span data-ttu-id="3b8c3-208">В этом разделе описывается, как установить агент OMS для Linux с помощью пакета, который содержит пакеты Debian и RPM для каждого из компонентов агента.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-208">This section describes how to install the OMS Agent for Linux using a bunndle, which contains Debian and RPM packages for each of the agent components.</span></span>  <span data-ttu-id="3b8c3-209">Его можно установить полностью или можно извлечь его содержимое, чтобы получить отдельные пакеты.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-209">It can be installed directly or extracted to retrieve the individual packages.</span></span>  

<span data-ttu-id="3b8c3-210">Сначала необходимо получить идентификатор и ключ рабочей области OMS, которые можно найти, переключившись на [классический портал OMS](https://mms.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="3b8c3-210">First you need your OMS workspace ID and key, which you can find by switching to the [OMS classic portal](https://mms.microsoft.com).</span></span>  <span data-ttu-id="3b8c3-211">На странице **Обзор** в верхнем меню выберите **Параметры** и перейдите в раздел **Подключенные источники\Серверы с Linux**.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-211">On the **Overview** page, from the top menu select **Settings**, and then navigate to **Connected Sources\Linux Servers**.</span></span>  <span data-ttu-id="3b8c3-212">Вы увидите необходимые значения справа от полей **Идентификатор рабочей области** и **Первичный ключ**.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-212">You see the value to the right of **Workspace ID** and **Primary Key**.</span></span>  <span data-ttu-id="3b8c3-213">Скопируйте их и вставьте в любой удобный для вас редактор.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-213">Copy and paste both into your favorite editor.</span></span>    

1. <span data-ttu-id="3b8c3-214">Скачайте последнюю версию [агента OMS для Linux (x64)](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x64.sh) или [агента OMS для Linux (x86)](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x86.sh) с сайта GitHub.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-214">Download the latest [OMS Agent for Linux (x64)](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x64.sh) or [OMS Agent for Linux x86](https://github.com/Microsoft/OMS-Agent-for-Linux/releases/download/OMSAgent_GA_v1.4.0-45/omsagent-1.4.0-45.universal.x86.sh) from GitHub.</span></span>  
2. <span data-ttu-id="3b8c3-215">Перенесите соответствующий пакет (x86 или x64) на компьютер Linux с помощью scp или sftp.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-215">Transfer the appropriate bundle (x86 or x64) to your Linux computer using scp/sftp.</span></span>
3. <span data-ttu-id="3b8c3-216">Установите пакет, используя аргумент `--install` или `--upgrade`.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-216">Install the bundle by using the `--install` or `--upgrade` argument.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="3b8c3-217">Используйте аргумент `--upgrade`, если все существующие пакеты (например, агент System Center Operations Manager для Linux) уже установлены.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-217">If any existing packages are installed such as when the System Center Operations Manager agent for Linux is already installed, use the `--upgrade` argument.</span></span> <span data-ttu-id="3b8c3-218">Чтобы подключиться к Operations Management Suite во время установки, используйте параметры `-w <WorkspaceID>` и `-s <Shared Key>`.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-218">To connect to Operations Management Suite during installation, provide the `-w <WorkspaceID>` and `-s <Shared Key>` parameters.</span></span>


#### <a name="to-install-and-onboard-directly"></a><span data-ttu-id="3b8c3-219">Для установки и прямого подключения</span><span class="sxs-lookup"><span data-stu-id="3b8c3-219">To install and onboard directly</span></span>
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key>
```

#### <a name="to-upgrade-the-agent-package"></a><span data-ttu-id="3b8c3-220">Для обновления пакета агента</span><span class="sxs-lookup"><span data-stu-id="3b8c3-220">To upgrade the agent package</span></span>
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade
```

#### <a name="to-install-and-onboard-to-a-workspace-in-us-government-cloud"></a><span data-ttu-id="3b8c3-221">Для установки и подключения к рабочей области в облаке правительства США</span><span class="sxs-lookup"><span data-stu-id="3b8c3-221">To install and onboard to a workspace in US Government Cloud</span></span>
```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -w <workspace id> -s <shared key> -d opinsights.azure.us
```

## <a name="configuring-the-agent-for-use-with-an-http-proxy-server-or-oms-gateway"></a><span data-ttu-id="3b8c3-222">Настройка агента для использования со шлюзом OMS или прокси-сервером HTTP</span><span class="sxs-lookup"><span data-stu-id="3b8c3-222">Configuring the agent for use with an HTTP proxy server or OMS Gateway</span></span>
<span data-ttu-id="3b8c3-223">Агент OMS для Linux поддерживает обмен данными со службой OMS через прокси-сервер HTTP или HTTPS либо шлюз OMS.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-223">The OMS Agent for Linux supports communicating either through an HTTP or HTTPS proxy server or OMS Gateway to the OMS service.</span></span>  <span data-ttu-id="3b8c3-224">Поддерживается анонимная и базовая аутентификация (с именем пользователя и паролем).</span><span class="sxs-lookup"><span data-stu-id="3b8c3-224">Both anonymous and basic authentication (username/password) is supported.</span></span>  

### <a name="proxy-configuration"></a><span data-ttu-id="3b8c3-225">Конфигурация прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="3b8c3-225">Proxy configuration</span></span>
<span data-ttu-id="3b8c3-226">Значение конфигурации прокси-сервера имеет следующий синтаксис:</span><span class="sxs-lookup"><span data-stu-id="3b8c3-226">The proxy configuration value has the following syntax:</span></span>

`[protocol://][user:password@]proxyhost[:port]`

<span data-ttu-id="3b8c3-227">Свойство</span><span class="sxs-lookup"><span data-stu-id="3b8c3-227">Property</span></span>|<span data-ttu-id="3b8c3-228">Описание</span><span class="sxs-lookup"><span data-stu-id="3b8c3-228">Description</span></span>
-|-
<span data-ttu-id="3b8c3-229">Протокол</span><span class="sxs-lookup"><span data-stu-id="3b8c3-229">Protocol</span></span>|<span data-ttu-id="3b8c3-230">HTTP или HTTPS</span><span class="sxs-lookup"><span data-stu-id="3b8c3-230">http or https</span></span>
<span data-ttu-id="3b8c3-231">user</span><span class="sxs-lookup"><span data-stu-id="3b8c3-231">user</span></span>|<span data-ttu-id="3b8c3-232">Необязательное имя пользователя для аутентификации прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="3b8c3-232">Optional username for proxy authentication</span></span>
<span data-ttu-id="3b8c3-233">пароль</span><span class="sxs-lookup"><span data-stu-id="3b8c3-233">password</span></span>|<span data-ttu-id="3b8c3-234">Необязательный пароль для аутентификации прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="3b8c3-234">Optional password for proxy authentication</span></span>
<span data-ttu-id="3b8c3-235">proxyhost</span><span class="sxs-lookup"><span data-stu-id="3b8c3-235">proxyhost</span></span>|<span data-ttu-id="3b8c3-236">Адрес или полное доменное имя прокси-сервера или шлюза OMS</span><span class="sxs-lookup"><span data-stu-id="3b8c3-236">Address or FQDN of the proxy server/OMS Gateway</span></span>
<span data-ttu-id="3b8c3-237">порт</span><span class="sxs-lookup"><span data-stu-id="3b8c3-237">port</span></span>|<span data-ttu-id="3b8c3-238">Номер дополнительного порта для прокси сервера или OMS шлюза</span><span class="sxs-lookup"><span data-stu-id="3b8c3-238">Optional port number for the proxy server/OMS Gateway</span></span>

<span data-ttu-id="3b8c3-239">Например: `http://user01:password@proxy01.contoso.com:8080`</span><span class="sxs-lookup"><span data-stu-id="3b8c3-239">For example: `http://user01:password@proxy01.contoso.com:8080`</span></span>

<span data-ttu-id="3b8c3-240">Прокси-сервер можно указать во время установки или при изменении файла конфигурации proxy.conf после установки.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-240">The proxy server can be specified during installation or by modifying the proxy.conf configuration file after installation.</span></span>   

### <a name="specify-proxy-configuration-during-installation"></a><span data-ttu-id="3b8c3-241">Определение конфигурации прокси-сервера во время установки</span><span class="sxs-lookup"><span data-stu-id="3b8c3-241">Specify proxy configuration during installation</span></span>
<span data-ttu-id="3b8c3-242">Аргумент `-p` или `--proxy` для установки пакета omsagent определяет используемую конфигурацию прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-242">The `-p` or `--proxy` argument for the omsagent installation bundle specifies the proxy configuration to use.</span></span> 

```
sudo sh ./omsagent-<version>.universal.x64.sh --upgrade -p http://<proxy user>:<proxy password>@<proxy address>:<proxy port> -w <workspace id> -s <shared key>
```

### <a name="define-the-proxy-configuration-in-a-file"></a><span data-ttu-id="3b8c3-243">Определение конфигурации прокси-сервера в файле</span><span class="sxs-lookup"><span data-stu-id="3b8c3-243">Define the proxy configuration in a file</span></span>
<span data-ttu-id="3b8c3-244">Конфигурацию прокси-сервера можно задать в файлах `/etc/opt/microsoft/omsagent/proxy.conf` и `/etc/opt/microsoft/omsagent/conf/proxy.conf `.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-244">The proxy configuration can be set in the files `/etc/opt/microsoft/omsagent/proxy.conf`  and `/etc/opt/microsoft/omsagent/conf/proxy.conf `.</span></span> <span data-ttu-id="3b8c3-245">Файлы можно создать или изменить напрямую, но необходимо обновить их разрешения, чтобы предоставить пользователю omiuser право на чтение файлов.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-245">The files can be directly created or edited, but their permissions must be updated to grant the omiuser user read permission on the files.</span></span> <span data-ttu-id="3b8c3-246">Например:</span><span class="sxs-lookup"><span data-stu-id="3b8c3-246">For example:</span></span>
```
proxyconf="https://proxyuser:proxypassword@proxyserver01:8080"
sudo echo $proxyconf >>/etc/opt/microsoft/omsagent/proxy.conf
sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/proxy.conf
sudo chmod 600 /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf  
sudo /opt/microsoft/omsagent/bin/service_control restart [<workspace id>]
```

### <a name="removing-the-proxy-configuration"></a><span data-ttu-id="3b8c3-247">Удаление конфигурации прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-247">Removing the proxy configuration</span></span>
<span data-ttu-id="3b8c3-248">Чтобы удалить ранее заданную конфигурацию прокси-сервера и вернуться к прямому подключению, удалите файл proxy.conf:</span><span class="sxs-lookup"><span data-stu-id="3b8c3-248">To remove a previously defined proxy configuration and revert to direct connectivity, remove the proxy.conf file:</span></span>
```
sudo rm /etc/opt/microsoft/omsagent/proxy.conf /etc/opt/microsoft/omsagent/conf/proxy.conf
sudo /opt/microsoft/omsagent/bin/service_control restart 
```

## <a name="onboarding-with-operations-management-suite"></a><span data-ttu-id="3b8c3-249">Подключение к Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="3b8c3-249">Onboarding with Operations Management Suite</span></span>
<span data-ttu-id="3b8c3-250">Если идентификатор и ключ рабочей области не предоставлены во время установки пакета, агент нужно впоследствии зарегистрировать с использованием Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-250">If a workspace ID and key were not provided during the bundle installation, the agent must be subsequently registered with Operations Management Suite.</span></span>

### <a name="onboarding-using-the-command-line"></a><span data-ttu-id="3b8c3-251">Подключение с помощью командной строки</span><span class="sxs-lookup"><span data-stu-id="3b8c3-251">Onboarding using the command line</span></span>
<span data-ttu-id="3b8c3-252">Выполните команду omsadmin.sh, указав идентификатор и ключ для рабочей области.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-252">Run the omsadmin.sh command supplying the workspace id and key for your workspace.</span></span> <span data-ttu-id="3b8c3-253">Эту команду должен выполнять привилегированный пользователь (sudo):</span><span class="sxs-lookup"><span data-stu-id="3b8c3-253">This command must be run as root (with sudo elevation):</span></span>
```
cd /opt/microsoft/omsagent/bin
sudo ./omsadmin.sh -w <WorkspaceID> -s <Shared Key>
```

### <a name="onboarding-using-a-file"></a><span data-ttu-id="3b8c3-254">Подключение с помощью файла</span><span class="sxs-lookup"><span data-stu-id="3b8c3-254">Onboarding using a file</span></span>
1.  <span data-ttu-id="3b8c3-255">Создайте файл `/etc/omsagent-onboard.conf`.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-255">Create the file `/etc/omsagent-onboard.conf`.</span></span> <span data-ttu-id="3b8c3-256">Файл должен быть доступным для чтения и записи для привилегированного пользователя.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-256">The file must be readable and writable for root.</span></span>
`sudo vi /etc/omsagent-onboard.conf`
2.  <span data-ttu-id="3b8c3-257">Вставьте следующие строки в файл, используя идентификатор рабочей области и общий ключ:</span><span class="sxs-lookup"><span data-stu-id="3b8c3-257">Insert the following lines in the file with your Workspace ID and Shared Key:</span></span>

        WORKSPACE_ID=<WorkspaceID>  
        SHARED_KEY=<Shared Key>  
   
3.  <span data-ttu-id="3b8c3-258">Чтобы подключиться к OMS, выполните следующую команду: `sudo /opt/microsoft/omsagent/bin/omsadmin.sh`.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-258">Run the following command to Onboard to OMS: `sudo /opt/microsoft/omsagent/bin/omsadmin.sh`</span></span>
4.  <span data-ttu-id="3b8c3-259">Файл будет удален после успешного подключения.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-259">The file is deleted on successful onboarding.</span></span>

## <a name="enable-the-oms-agent-for-linux-to-report-to-system-center-operations-manager"></a><span data-ttu-id="3b8c3-260">Включение агента OMS для Linux для передачи отчета в System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="3b8c3-260">Enable the OMS Agent for Linux to report to System Center Operations Manager</span></span>
<span data-ttu-id="3b8c3-261">Чтобы настроить агент OMS для Linux и передать отчет в группу управления System Center Operations Manager, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-261">Perform the following steps to configure the OMS Agent for Linux to report to a System Center Operations Manager management group.</span></span>  

1. <span data-ttu-id="3b8c3-262">Измените файл `/etc/opt/omi/conf/omiserver.conf`</span><span class="sxs-lookup"><span data-stu-id="3b8c3-262">Edit the file `/etc/opt/omi/conf/omiserver.conf`</span></span>
2. <span data-ttu-id="3b8c3-263">Укажите для **httpsport=** номер порта 1270.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-263">Ensure that the line beginning with **httpsport=** defines the port 1270.</span></span> <span data-ttu-id="3b8c3-264">Например: `httpsport=1270`.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-264">Such as: `httpsport=1270`</span></span>
3. <span data-ttu-id="3b8c3-265">Перезапустите сервер OMI: `sudo /opt/omi/bin/service_control restart`.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-265">Restart the OMI server: `sudo /opt/omi/bin/service_control restart`</span></span>

## <a name="agent-logs"></a><span data-ttu-id="3b8c3-266">Журналы агента</span><span class="sxs-lookup"><span data-stu-id="3b8c3-266">Agent logs</span></span>
<span data-ttu-id="3b8c3-267">Журналы для агента OMS для Linux доступны здесь: `/var/opt/microsoft/omsagent/<workspace id>/log/`. Журналы для программы omsconfig (конфигурация агента) доступны здесь: `/var/opt/microsoft/omsconfig/log/`. Журналы для компонентов OMI и SCX (предоставляют данные метрик производительности) доступны здесь: `/var/opt/omi/log/ and /var/opt/microsoft/scx/log`.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-267">The logs for the OMS Agent for Linux can be found at: `/var/opt/microsoft/omsagent/<workspace id>/log/` The logs for the omsconfig (agent configuration) program can be found at: `/var/opt/microsoft/omsconfig/log/` Logs for the OMI and SCX components (which provide performance metrics data) can be found at: `/var/opt/omi/log/ and /var/opt/microsoft/scx/log`</span></span>

### <a name="log-rotation-configuration"></a><span data-ttu-id="3b8c3-268">Конфигурация чередования журналов##</span><span class="sxs-lookup"><span data-stu-id="3b8c3-268">Log rotation configuration##</span></span>
<span data-ttu-id="3b8c3-269">Конфигурация чередования журналов для omsagent доступна здесь: `/etc/logrotate.d/omsagent-<workspace id>`.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-269">The log rotate configuration for omsagent can be found at: `/etc/logrotate.d/omsagent-<workspace id>`</span></span>

<span data-ttu-id="3b8c3-270">Параметры по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="3b8c3-270">The default settings are:</span></span> 
```
/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log {
    rotate 5
    missingok
    notifempty
    compress
    size 50k
    copytruncate
}
```

## <a name="uninstalling-the-oms-agent-for-linux"></a><span data-ttu-id="3b8c3-271">Удаление агента OMS для Linux</span><span class="sxs-lookup"><span data-stu-id="3b8c3-271">Uninstalling the OMS Agent for Linux</span></span>
<span data-ttu-id="3b8c3-272">Пакеты агента можно удалить, запустив SH-файл пакета с аргументом `--purge`, полностью удаляющий агент и его конфигурации с компьютера.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-272">The agent packages can be uninstalled by running the bundle .sh file with the `--purge` argument, which completely removes the agent and its configuration from the computer.</span></span>   

```
> sudo rpm -e omsconfig
> sudo rpm -e omsagent
> sudo /opt/microsoft/scx/bin/uninstall
```

## <a name="troubleshooting"></a><span data-ttu-id="3b8c3-273">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="3b8c3-273">Troubleshooting</span></span>

### <a name="issue-unable-to-connect-through-proxy-to-oms"></a><span data-ttu-id="3b8c3-274">Проблема. Не удается подключиться к OMS через прокси-сервер</span><span class="sxs-lookup"><span data-stu-id="3b8c3-274">Issue: Unable to connect through proxy to OMS</span></span>

#### <a name="probable-causes"></a><span data-ttu-id="3b8c3-275">Возможные причины</span><span class="sxs-lookup"><span data-stu-id="3b8c3-275">Probable causes</span></span>
* <span data-ttu-id="3b8c3-276">При подключении указан недопустимый прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-276">The proxy specified during onboarding was incorrect</span></span>
* <span data-ttu-id="3b8c3-277">Конечные точки службы OMS не включены в список разрешенных в вашем центре обработки данных.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-277">The OMS Service Endpoints are not whitelistested in your datacenter</span></span> 

#### <a name="resolutions"></a><span data-ttu-id="3b8c3-278">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="3b8c3-278">Resolutions</span></span>
1. <span data-ttu-id="3b8c3-279">Повторно подключитесь к службе OMS, используя службу OMS для Linux и следующую команду с включенным параметром `-v`.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-279">Reonboard to the OMS Service with the OMS Agent for Linux by using the following command with the option `-v` enabled.</span></span> <span data-ttu-id="3b8c3-280">За счет этого подробные выходные данные агента могут подключиться к службе OMS через прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-280">This allows verbose output of the agent connecting through the proxy to the OMS Service.</span></span> 
`/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`

2. <span data-ttu-id="3b8c3-281">Просмотрите раздел [Настройка агента для использования со шлюзом OMS или прокси-сервером HTTP(#configuring the-agent-for-use-with-a-http-proxy-server), чтобы убедиться в правильности настройки агента для обмена данными через прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-281">Review the section [Configuring the agent for use with an HTTP proxy server(#configuring the-agent-for-use-with-a-http-proxy-server) to verify you have properly configured the agent to communicate through a proxy server.</span></span>    
* <span data-ttu-id="3b8c3-282">Также проверьте включение в список разрешенных следующих конечных точек службы OMS:</span><span class="sxs-lookup"><span data-stu-id="3b8c3-282">Double check that the following OMS Service endpoints are whitelisted:</span></span>

    |<span data-ttu-id="3b8c3-283">Ресурс агента</span><span class="sxs-lookup"><span data-stu-id="3b8c3-283">Agent Resource</span></span>| <span data-ttu-id="3b8c3-284">порты;</span><span class="sxs-lookup"><span data-stu-id="3b8c3-284">Ports</span></span> |  
    |------|---------|  
    |<span data-ttu-id="3b8c3-285">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="3b8c3-285">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="3b8c3-286">Порт 443</span><span class="sxs-lookup"><span data-stu-id="3b8c3-286">Port 443</span></span>|   
    |<span data-ttu-id="3b8c3-287">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="3b8c3-287">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="3b8c3-288">Порт 443</span><span class="sxs-lookup"><span data-stu-id="3b8c3-288">Port 443</span></span>|   
    |<span data-ttu-id="3b8c3-289">ods.systemcenteradvisor.com</span><span class="sxs-lookup"><span data-stu-id="3b8c3-289">ods.systemcenteradvisor.com</span></span> | <span data-ttu-id="3b8c3-290">Порт 443</span><span class="sxs-lookup"><span data-stu-id="3b8c3-290">Port 443</span></span>|   
    |<span data-ttu-id="3b8c3-291">*.blob.core.windows.net/</span><span class="sxs-lookup"><span data-stu-id="3b8c3-291">*.blob.core.windows.net/</span></span> | <span data-ttu-id="3b8c3-292">Порт 443</span><span class="sxs-lookup"><span data-stu-id="3b8c3-292">Port 443</span></span>|   

### <a name="issue-you-receive-a-403-error-when-trying-to-onboard"></a><span data-ttu-id="3b8c3-293">Проблема. При попытке подключения возникает ошибка 403.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-293">Issue: You receive a 403 error when trying to onboard</span></span>

#### <a name="probable-causes"></a><span data-ttu-id="3b8c3-294">Возможные причины</span><span class="sxs-lookup"><span data-stu-id="3b8c3-294">Probable causes</span></span>
* <span data-ttu-id="3b8c3-295">На сервере Linux установлены неправильные время и дата.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-295">Date and Time is incorrect on Linux Server</span></span> 
* <span data-ttu-id="3b8c3-296">Используется недопустимый идентификатор или ключ рабочей области.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-296">Workspace ID and Workspace Key used are not correct</span></span>

#### <a name="resolution"></a><span data-ttu-id="3b8c3-297">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="3b8c3-297">Resolution</span></span>

1. <span data-ttu-id="3b8c3-298">Проверьте время на своем сервере Linux с помощью команды.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-298">Check the time on your Linux server with the command date.</span></span> <span data-ttu-id="3b8c3-299">Если время отличается от текущего на 15 минут, подключение завершится сбоем.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-299">If the time is +/- 15 minutes from current time, then onboarding fails.</span></span> <span data-ttu-id="3b8c3-300">Чтобы исправить это, обновите дату и (или) часовой пояс на сервере Linux.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-300">To correct this update the date and/or timezone of your Linux server.</span></span> 
2. <span data-ttu-id="3b8c3-301">Убедитесь, что установлена последняя версия агента OMS для Linux.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-301">Verify you have installed the latest version of the OMS Agent for Linux.</span></span>  <span data-ttu-id="3b8c3-302">В последней версии вы получаете уведомления, если разница во времени приводит к сбою подключения.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-302">The newest version now notifies you if time skew is causing the onboarding failure.</span></span>
3. <span data-ttu-id="3b8c3-303">Выполните повторное подключение, используя правильный идентификатор и ключ рабочей области и следуя инструкциям по установке, приведенным ранее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-303">Reonboard using correct Workspace ID and Workspace Key following the installation instructions earlier in this topic.</span></span>

### <a name="issue-you-see-a-500-and-404-error-in-the-log-file-right-after-onboarding"></a><span data-ttu-id="3b8c3-304">Проблема. Сразу после подключения в файле журнала появляется ошибка 500 и 404.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-304">Issue: You see a 500 and 404 error in the log file right after onboarding</span></span>
<span data-ttu-id="3b8c3-305">Это известная проблема, которая возникает при первой передаче данных Linux в рабочую область OMS.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-305">This is a known issue that occurs on first upload of Linux data into an OMS workspace.</span></span> <span data-ttu-id="3b8c3-306">Это не влияет на отправляемые данные и не мешает работе службы.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-306">This does not affect data being sent or service experience.</span></span>

### <a name="issue--you-are-not-seeing-any-data-in-the-oms-portal"></a><span data-ttu-id="3b8c3-307">Проблема. На портале OMS не отображаются данные.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-307">Issue:  You are not seeing any data in the OMS portal</span></span>

#### <a name="probable-causes"></a><span data-ttu-id="3b8c3-308">Возможные причины</span><span class="sxs-lookup"><span data-stu-id="3b8c3-308">Probable causes</span></span>

- <span data-ttu-id="3b8c3-309">Сбой при подключении к службе OMS.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-309">Onboarding to the OMS Service failed</span></span>
- <span data-ttu-id="3b8c3-310">Подключение к службе OMS заблокировано.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-310">Connection to the OMS Service is blocked</span></span>
- <span data-ttu-id="3b8c3-311">Создана резервная копия данных агента OMS для Linux.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-311">OMS Agent for Linux data is backed up</span></span>

#### <a name="resolutions"></a><span data-ttu-id="3b8c3-312">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="3b8c3-312">Resolutions</span></span>
1. <span data-ttu-id="3b8c3-313">Проверьте состояние подключения для службы OMS, убедившись в наличии следующего файла: `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-313">Check if onboarding the OMS Service was successful by checking if the following file exists: `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`</span></span>
2. <span data-ttu-id="3b8c3-314">Повторно подключитесь, используя инструкции командной строки `omsadmin.sh`</span><span class="sxs-lookup"><span data-stu-id="3b8c3-314">Reonboard using the `omsadmin.sh` command-line instructions</span></span>
3. <span data-ttu-id="3b8c3-315">Если используется прокси-сервер, см. описанные выше шаги по разрешению прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-315">If using a proxy, refer to the proxy resolution steps provided earlier.</span></span>
4. <span data-ttu-id="3b8c3-316">В некоторых случаях сбой подключения между агентом OMS для Linux и службой OMS связан с тем, что в буфере достигнут максимальный размер запросов к данным агента (50 МБ).</span><span class="sxs-lookup"><span data-stu-id="3b8c3-316">In some cases, when the OMS Agent for Linux cannot communicate with the OMS Service, data on the agent is queued to the full buffer size, which is 50 MB.</span></span> <span data-ttu-id="3b8c3-317">Следует перезапустить агент OMS для Linux, выполнив следующую команду: `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-317">The OMS Agent for Linux should be restarted by running the following command: `/opt/microsoft/omsagent/bin/service_control restart [<workspace id>]`.</span></span> 

    >[!NOTE]
    ><span data-ttu-id="3b8c3-318">Эта проблема исправлена в агенте версии 1.1.0-28 и выше.</span><span class="sxs-lookup"><span data-stu-id="3b8c3-318">This issue is fixed in agent version 1.1.0-28 and later.</span></span>
> 