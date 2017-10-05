---
title: "Подключение средств обеспечения безопасности к решению для защиты и аудита Operations Management Suite (OMS) | Документация Майкрософт"
description: "Этот документ поможет вам подключить средства обеспечения безопасности к решению для защиты и аудита Operations Management Suite с использованием CEF."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 46eee484-e078-4bad-8c89-c88a3508f6aa
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 710a1fe0ce2b7a1841187cf75f4ffb090cc161e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="connecting-your-security-products-to-the-operations-management-suite-oms-security-and-audit-solution"></a><span data-ttu-id="a465a-103">Подключение средств обеспечения безопасности к решению для защиты и аудита Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="a465a-103">Connecting your security products to the Operations Management Suite (OMS) Security and Audit Solution</span></span> 
<span data-ttu-id="a465a-104">Этот документ поможет вам подключить свои средства обеспечения безопасности к решению для защиты и аудита OMS.</span><span class="sxs-lookup"><span data-stu-id="a465a-104">This document helps you connect your security products into the OMS Security and Audit Solution.</span></span> <span data-ttu-id="a465a-105">Поддерживаются следующие источники:</span><span class="sxs-lookup"><span data-stu-id="a465a-105">The following sources are supported:</span></span>

- <span data-ttu-id="a465a-106">события CEF;</span><span class="sxs-lookup"><span data-stu-id="a465a-106">Common Event Format (CEF) events</span></span>
- <span data-ttu-id="a465a-107">события Cisco ASA.</span><span class="sxs-lookup"><span data-stu-id="a465a-107">Cisco ASA events</span></span>


## <a name="what-is-cef"></a><span data-ttu-id="a465a-108">Что такое CEF?</span><span class="sxs-lookup"><span data-stu-id="a465a-108">What is CEF?</span></span>
<span data-ttu-id="a465a-109">CEF — это отраслевой стандартный формат на основе сообщений системного журнала, который используют многие поставщики средств безопасности, чтобы обеспечить взаимодействие событий на разных платформах.</span><span class="sxs-lookup"><span data-stu-id="a465a-109">Common Event Format (CEF) is an industry standard format on top of Syslog messages, used by many security vendors to allow event interoperability among different platforms.</span></span> <span data-ttu-id="a465a-110">Решение для защиты и аудита OMS поддерживает принятие данных с использованием CEF, что позволяет подключить собственные решения для обеспечения безопасности к решению для защиты OMS.</span><span class="sxs-lookup"><span data-stu-id="a465a-110">OMS Security and Audit Solution support data ingestion using CEF, which enables you to connect your security products with OMS Security.</span></span> 

<span data-ttu-id="a465a-111">Подключив свой источник данных к OMS, вы можете воспользоваться следующими преимуществами, предлагаемыми этой платформой:</span><span class="sxs-lookup"><span data-stu-id="a465a-111">By connecting your data source to OMS, you are able to take advantage of the following capabilities that are part of this platform:</span></span>

- <span data-ttu-id="a465a-112">поиск и корреляция;</span><span class="sxs-lookup"><span data-stu-id="a465a-112">Search & Correlation</span></span>
- <span data-ttu-id="a465a-113">Аудит</span><span class="sxs-lookup"><span data-stu-id="a465a-113">Auditing</span></span>
- <span data-ttu-id="a465a-114">Предупреждение</span><span class="sxs-lookup"><span data-stu-id="a465a-114">Alert</span></span>
- <span data-ttu-id="a465a-115">Аналитика угроз</span><span class="sxs-lookup"><span data-stu-id="a465a-115">Threat Intelligence</span></span>
- <span data-ttu-id="a465a-116">Важные проблемы</span><span class="sxs-lookup"><span data-stu-id="a465a-116">Notable Issues</span></span>

## <a name="collection-of-security-solution-logs"></a><span data-ttu-id="a465a-117">сбор журналов решения для защиты.</span><span class="sxs-lookup"><span data-stu-id="a465a-117">Collection of security solution logs</span></span>

<span data-ttu-id="a465a-118">Решение для защиты OMS поддерживает сбор журналов с использованием CEF в системных журналах и журналах [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/).</span><span class="sxs-lookup"><span data-stu-id="a465a-118">OMS Security supports collection of logs using CEF over Syslogs and [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/) logs.</span></span> <span data-ttu-id="a465a-119">В этом примере источник (компьютер, создающий журналы) — компьютер Linux, на котором выполняется управляющая программа syslog-ng, а целевой объект — решение для защиты OMS.</span><span class="sxs-lookup"><span data-stu-id="a465a-119">In this example, the source (computer that generates the logs) is a Linux computer running syslog-ng daemon and the target is OMS Security.</span></span> <span data-ttu-id="a465a-120">Чтобы подготовить компьютер Linux, необходимо сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="a465a-120">To prepare the Linux computer you will need to perform the following tasks:</span></span>

- <span data-ttu-id="a465a-121">Скачайте агент OMS для Linux версии 1.2.0-25 или более.</span><span class="sxs-lookup"><span data-stu-id="a465a-121">Download the OMS Agent for Linux, version 1.2.0-25 or above.</span></span>
- <span data-ttu-id="a465a-122">Выполните инструкции раздела **Краткое руководство по установке** [в этой статье](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux), чтобы установить и внедрить агент в рабочей области.</span><span class="sxs-lookup"><span data-stu-id="a465a-122">Follow the section **Quick Install Guide** from [this article](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) to install and onboard the agent to your workspace.</span></span>

<span data-ttu-id="a465a-123">Как правило агент устанавливается на компьютере, отличном от того, на котором создаются журналы.</span><span class="sxs-lookup"><span data-stu-id="a465a-123">Typically, the agent is installed on a different computer from the one on which the logs are generated.</span></span> <span data-ttu-id="a465a-124">Как правило, для перенаправления журналов на компьютер агента необходимо сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="a465a-124">Forwarding the logs to the agent machine will usually require the following steps:</span></span>

- <span data-ttu-id="a465a-125">Настроить решение или компьютер, на котором выполняется ведение журналов, для перенаправления требуемых событий управляющей программы системного журнала (rsyslog или syslog-ng) на компьютере агента.</span><span class="sxs-lookup"><span data-stu-id="a465a-125">Configure the logging product/machine to forward the required events to the syslog daemon (rsyslog or syslog-ng) on the agent machine.</span></span>
- <span data-ttu-id="a465a-126">Включить управляющую программу системного журнала на компьютере агента для получения сообщений из удаленной системы.</span><span class="sxs-lookup"><span data-stu-id="a465a-126">Enable the syslog daemon on the agent machine to receive messages from a remote system.</span></span>

<span data-ttu-id="a465a-127">На компьютере агента события должны отправляться из управляющей программы системного журнала на локальный порт UDP 25226.</span><span class="sxs-lookup"><span data-stu-id="a465a-127">On the agent machine, the events need to be sent from the syslog daemon to local UDP port 25226.</span></span> <span data-ttu-id="a465a-128">Агент прослушивает входящие события на этом порте.</span><span class="sxs-lookup"><span data-stu-id="a465a-128">The agent is listening for incoming events on this port.</span></span> <span data-ttu-id="a465a-129">Ниже приведен пример конфигурации для отправки всех событий из локальной системы в агент (конфигурацию можно изменить в соответствии с локальными параметрами):</span><span class="sxs-lookup"><span data-stu-id="a465a-129">The following is an example configuration for sending all events from the local system to the agent (you can modify the configuration to fit your local settings):</span></span>

1. <span data-ttu-id="a465a-130">Откройте окно терминала и перейдите в каталог */etc/syslog-ng/*.</span><span class="sxs-lookup"><span data-stu-id="a465a-130">Open the terminal window, and go to the directory */etc/syslog-ng/*</span></span> 
2. <span data-ttu-id="a465a-131">Создайте файл *security-config-omsagent.conf* и добавьте следующее содержимое: OMS_facility = local4</span><span class="sxs-lookup"><span data-stu-id="a465a-131">Create a new file *security-config-omsagent.conf* and add the following content:  OMS_facility = local4</span></span>
    
    <span data-ttu-id="a465a-132">filter f_local4_oms { facility(local4); };</span><span class="sxs-lookup"><span data-stu-id="a465a-132">filter f_local4_oms { facility(local4); };</span></span>

    <span data-ttu-id="a465a-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span><span class="sxs-lookup"><span data-stu-id="a465a-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span></span>

    <span data-ttu-id="a465a-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span><span class="sxs-lookup"><span data-stu-id="a465a-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span></span>
    
3. <span data-ttu-id="a465a-135">Скачайте файл *security_events.conf* и поместить его в каталог */etc/opt/microsoft/omsagent/conf/omsagent.d/* на компьютере агента OMS.</span><span class="sxs-lookup"><span data-stu-id="a465a-135">Download the file *security_events.conf* and place at */etc/opt/microsoft/omsagent/conf/omsagent.d/* in the OMS Agent computer.</span></span>
4. <span data-ttu-id="a465a-136">Введите следующую команду, чтобы перезапустить управляющую программу syslog: *для запуска syslog-ng:*</span><span class="sxs-lookup"><span data-stu-id="a465a-136">Type the command below to restart the syslog daemon:  *For syslog-ng run:*</span></span>
    
    ```
    sudo service rsyslog restart
    ```

    <span data-ttu-id="a465a-137">*Для rsyslog выполните следующую команду:*</span><span class="sxs-lookup"><span data-stu-id="a465a-137">*For rsyslog run:*</span></span>
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. <span data-ttu-id="a465a-138">Введите следующую команду, чтобы перезапустить агент OMS:</span><span class="sxs-lookup"><span data-stu-id="a465a-138">Type the command below to restart the OMS Agent:</span></span>

    <span data-ttu-id="a465a-139">*Для syslog-ng выполните следующую команду:*</span><span class="sxs-lookup"><span data-stu-id="a465a-139">*For syslog-ng run:*</span></span>
    
    ```
    sudo service omsagent restart
    ```

    <span data-ttu-id="a465a-140">*Для rsyslog выполните следующую команду:*</span><span class="sxs-lookup"><span data-stu-id="a465a-140">*For rsyslog run:*</span></span>
    
    ```
    systemctl restart omsagent
    ```
6. <span data-ttu-id="a465a-141">Введите следующую команду и проверьте результат, чтобы убедиться, что в журнале агента OMS нет ошибок:</span><span class="sxs-lookup"><span data-stu-id="a465a-141">Type the command below and review the result to confirm that there are no errors in the OMS Agent log:</span></span>

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a><span data-ttu-id="a465a-142">Просмотр собранных событий безопасности</span><span class="sxs-lookup"><span data-stu-id="a465a-142">Reviewing collected security events</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

<span data-ttu-id="a465a-143">После завершения конфигурации решение для защиты OMS начнет принимать события безопасности.</span><span class="sxs-lookup"><span data-stu-id="a465a-143">After the configuration is over, the security event will start to be ingested by OMS Security.</span></span> <span data-ttu-id="a465a-144">Чтобы визуализировать эти события, откройте поиск по журналам, введите в поле поиска команду *Type=CommonSecurityLog* и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="a465a-144">To visualize those events, open the Log Search, type the command *Type=CommonSecurityLog* in the search field and press ENTER.</span></span> <span data-ttu-id="a465a-145">В следующем примере показан результат выполнения этой команды. Обратите внимание, что в этом случае решение для защиты OMS уже приняло журналы безопасности от нескольких поставщиков:</span><span class="sxs-lookup"><span data-stu-id="a465a-145">The following example shows the result of this command, notice that in this case OMS Security already ingested security logs from multiple vendors:</span></span>
   
![Оценка базовых показателей в решении OMS "Безопасность и аудит"](./media/oms-security-connect-products/oms-security-connect-products-fig1.png)

<span data-ttu-id="a465a-147">Вы можете уточнить условия поиска для одного поставщика, например, для визуализации веб-журналов Cisco. Для этого введите *Type=CommonSecurityLog DeviceVendor=Cisco*.</span><span class="sxs-lookup"><span data-stu-id="a465a-147">You can refine this search for one single vendor, for example, to visualize online Cisco logs, type: *Type=CommonSecurityLog DeviceVendor=Cisco*.</span></span> <span data-ttu-id="a465a-148">В CommonSecurityLog предусмотрены стандартные поля для любых заголовков CEF, включая базовые расширения. Другие же расширения, независимо от того, являются ли они настраиваемыми или нет, будут вставлены в поле AdditionalExtensions.</span><span class="sxs-lookup"><span data-stu-id="a465a-148">The “CommonSecurityLog” has predefined fields for any CEF header including the basic extensios, while any other extension whether it’s “Custom Extension” or not, will be inserted into "AdditionalExtensions" field.</span></span> <span data-ttu-id="a465a-149">Чтобы получить выделенные поля, можно воспользоваться функцией настраиваемых полей.</span><span class="sxs-lookup"><span data-stu-id="a465a-149">You can use the Custom Fields feature to get dedicated fields from it.</span></span> 

### <a name="accessing-computers-missing-baseline-assessment"></a><span data-ttu-id="a465a-150">Просмотр сведений о компьютерах с отсутствующей базовой оценкой</span><span class="sxs-lookup"><span data-stu-id="a465a-150">Accessing computers missing baseline assessment</span></span>
<span data-ttu-id="a465a-151">OMS поддерживает профиль базовых показателей участника домена в Windows Server от версии 2008 R2 до 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="a465a-151">OMS supports the domain member baseline profile on Windows Server 2008 R2 up to Windows Server 2012 R2.</span></span> <span data-ttu-id="a465a-152">Эта возможность для Windows Server 2016 находится на этапе разработки и будет добавлена после публикации.</span><span class="sxs-lookup"><span data-stu-id="a465a-152">Windows Server 2016 baseline isn’t final yet and will be added as soon as it is published.</span></span> <span data-ttu-id="a465a-153">Остальные операционные системы, проверенные в ходе оценки базовых показателей решением для защиты и аудита OMS, приведены в разделе **Компьютеры с отсутствующей базовой оценкой**.</span><span class="sxs-lookup"><span data-stu-id="a465a-153">All other operating systems scanned via OMS Security and Audit baseline assessment appear under the **Computers missing baseline assessment** section.</span></span>

## <a name="see-also"></a><span data-ttu-id="a465a-154">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="a465a-154">See also</span></span>
<span data-ttu-id="a465a-155">В этом документе вы узнали, как подключить решение CEF к OMS.</span><span class="sxs-lookup"><span data-stu-id="a465a-155">In this document, you learned how to connect your CEF solution to OMS.</span></span> <span data-ttu-id="a465a-156">Дополнительные сведения о функциях безопасности OMS см. в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="a465a-156">To learn more about OMS Security, see the following articles:</span></span>

* [<span data-ttu-id="a465a-157">Общие сведения об Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="a465a-157">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="a465a-158">Мониторинг и реагирование на оповещения безопасности в решении "Безопасность и аудит" Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="a465a-158">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="a465a-159">Мониторинг ресурсов в решении "Безопасность и аудит" Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="a465a-159">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

