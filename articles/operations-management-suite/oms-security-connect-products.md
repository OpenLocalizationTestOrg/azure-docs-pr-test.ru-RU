---
title: "aaaConnecting вашего решения аудита и безопасности продуктов toohello безопасности Operations Management Suite (OMS) | Документы Microsoft"
description: "В этом документе помогает вам tooconnect вашей безопасности продуктов tooOperations Management Suite безопасности и аудита решения, с помощью общего формата событий."
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
ms.openlocfilehash: 0f4b372d0379987c4e249628a3c8d52733be65c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-your-security-products-toohello-operations-management-suite-oms-security-and-audit-solution"></a><span data-ttu-id="0f3f1-103">Подключение вашего решения аудита и безопасности продуктов toohello безопасности Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="0f3f1-103">Connecting your security products toohello Operations Management Suite (OMS) Security and Audit Solution</span></span> 
<span data-ttu-id="0f3f1-104">В этом документе помогает подключить продуктов безопасности в hello OMS безопасности и аудита решения.</span><span class="sxs-lookup"><span data-stu-id="0f3f1-104">This document helps you connect your security products into hello OMS Security and Audit Solution.</span></span> <span data-ttu-id="0f3f1-105">поддерживаются следующие источники Hello:</span><span class="sxs-lookup"><span data-stu-id="0f3f1-105">hello following sources are supported:</span></span>

- <span data-ttu-id="0f3f1-106">события CEF;</span><span class="sxs-lookup"><span data-stu-id="0f3f1-106">Common Event Format (CEF) events</span></span>
- <span data-ttu-id="0f3f1-107">события Cisco ASA.</span><span class="sxs-lookup"><span data-stu-id="0f3f1-107">Cisco ASA events</span></span>


## <a name="what-is-cef"></a><span data-ttu-id="0f3f1-108">Что такое CEF?</span><span class="sxs-lookup"><span data-stu-id="0f3f1-108">What is CEF?</span></span>
<span data-ttu-id="0f3f1-109">Общий формат событий (CEF) является стандартизированный формат на основе сообщения системного журнала, используемые многие поставщики tooallow событий взаимодействие с безопасностью между разными платформами.</span><span class="sxs-lookup"><span data-stu-id="0f3f1-109">Common Event Format (CEF) is an industry standard format on top of Syslog messages, used by many security vendors tooallow event interoperability among different platforms.</span></span> <span data-ttu-id="0f3f1-110">OMS поддержка безопасности и аудита решения с помощью CEF, позволяющий tooconnect продуктов безопасности OMS безопасности приема данных.</span><span class="sxs-lookup"><span data-stu-id="0f3f1-110">OMS Security and Audit Solution support data ingestion using CEF, which enables you tooconnect your security products with OMS Security.</span></span> 

<span data-ttu-id="0f3f1-111">Подключившись к tooOMS источника данных, являются может tootake преимуществами hello следующие возможности, которые являются частью этой платформе:</span><span class="sxs-lookup"><span data-stu-id="0f3f1-111">By connecting your data source tooOMS, you are able tootake advantage of hello following capabilities that are part of this platform:</span></span>

- <span data-ttu-id="0f3f1-112">поиск и корреляция;</span><span class="sxs-lookup"><span data-stu-id="0f3f1-112">Search & Correlation</span></span>
- <span data-ttu-id="0f3f1-113">Аудит</span><span class="sxs-lookup"><span data-stu-id="0f3f1-113">Auditing</span></span>
- <span data-ttu-id="0f3f1-114">Предупреждение</span><span class="sxs-lookup"><span data-stu-id="0f3f1-114">Alert</span></span>
- <span data-ttu-id="0f3f1-115">Аналитика угроз</span><span class="sxs-lookup"><span data-stu-id="0f3f1-115">Threat Intelligence</span></span>
- <span data-ttu-id="0f3f1-116">Важные проблемы</span><span class="sxs-lookup"><span data-stu-id="0f3f1-116">Notable Issues</span></span>

## <a name="collection-of-security-solution-logs"></a><span data-ttu-id="0f3f1-117">сбор журналов решения для защиты.</span><span class="sxs-lookup"><span data-stu-id="0f3f1-117">Collection of security solution logs</span></span>

<span data-ttu-id="0f3f1-118">Решение для защиты OMS поддерживает сбор журналов с использованием CEF в системных журналах и журналах [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/).</span><span class="sxs-lookup"><span data-stu-id="0f3f1-118">OMS Security supports collection of logs using CEF over Syslogs and [Cisco ASA](https://blogs.technet.microsoft.com/msoms/2016/08/25/add-your-cisco-asa-logs-to-oms-security/) logs.</span></span> <span data-ttu-id="0f3f1-119">В этом примере hello источник (компьютер, который создает журналы hello) — управляющая программа syslog-ng компьютере Linux и hello целевой объект — безопасность OMS.</span><span class="sxs-lookup"><span data-stu-id="0f3f1-119">In this example, hello source (computer that generates hello logs) is a Linux computer running syslog-ng daemon and hello target is OMS Security.</span></span> <span data-ttu-id="0f3f1-120">компьютер Linux tooprepare hello, вам потребуется hello tooperform следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="0f3f1-120">tooprepare hello Linux computer you will need tooperform hello following tasks:</span></span>

- <span data-ttu-id="0f3f1-121">Загрузите hello агента OMS для Linux, версии 1.2.0-25 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="0f3f1-121">Download hello OMS Agent for Linux, version 1.2.0-25 or above.</span></span>
- <span data-ttu-id="0f3f1-122">Выполните раздел hello **краткое руководство по установке** из [в этой статье](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall и рабочая область tooyour встроенного hello агента.</span><span class="sxs-lookup"><span data-stu-id="0f3f1-122">Follow hello section **Quick Install Guide** from [this article](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux) tooinstall and onboard hello agent tooyour workspace.</span></span>

<span data-ttu-id="0f3f1-123">Как правило hello агент установлен на компьютере, отличном от hello, на какие журналы hello создаются.</span><span class="sxs-lookup"><span data-stu-id="0f3f1-123">Typically, hello agent is installed on a different computer from hello one on which hello logs are generated.</span></span> <span data-ttu-id="0f3f1-124">Компьютер агента toohello журналы hello пересылки обычно требуют hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="0f3f1-124">Forwarding hello logs toohello agent machine will usually require hello following steps:</span></span>

- <span data-ttu-id="0f3f1-125">Настройка ведения журнала продукта/machine tooforward hello необходимые события toohello управляющая программа syslog (rsyslog или syslog-ng) hello на компьютере агента hello.</span><span class="sxs-lookup"><span data-stu-id="0f3f1-125">Configure hello logging product/machine tooforward hello required events toohello syslog daemon (rsyslog or syslog-ng) on hello agent machine.</span></span>
- <span data-ttu-id="0f3f1-126">Включите управляющая программа syslog hello в сообщений hello агента машины tooreceive из удаленной системы.</span><span class="sxs-lookup"><span data-stu-id="0f3f1-126">Enable hello syslog daemon on hello agent machine tooreceive messages from a remote system.</span></span>

<span data-ttu-id="0f3f1-127">На компьютере агента hello hello события должны toobe, отправленных из системного журнала управляющей программы hello toolocal UDP-порт 25226.</span><span class="sxs-lookup"><span data-stu-id="0f3f1-127">On hello agent machine, hello events need toobe sent from hello syslog daemon toolocal UDP port 25226.</span></span> <span data-ttu-id="0f3f1-128">агент Здравствуй прослушивает входящие события для этого порта.</span><span class="sxs-lookup"><span data-stu-id="0f3f1-128">hello agent is listening for incoming events on this port.</span></span> <span data-ttu-id="0f3f1-129">Hello ниже приведен пример конфигурации для отправки всех событий из hello локальной системы toohello агента (можно изменить конфигурации toofit hello локальные параметры).</span><span class="sxs-lookup"><span data-stu-id="0f3f1-129">hello following is an example configuration for sending all events from hello local system toohello agent (you can modify hello configuration toofit your local settings):</span></span>

1. <span data-ttu-id="0f3f1-130">Hello откройте окно терминала и перейдите toohello directory */etc/syslog-ng /*</span><span class="sxs-lookup"><span data-stu-id="0f3f1-130">Open hello terminal window, and go toohello directory */etc/syslog-ng/*</span></span> 
2. <span data-ttu-id="0f3f1-131">Создайте новый файл *безопасности конфигурации omsagent.conf* и добавьте следующие содержимое hello: OMS_facility = local4</span><span class="sxs-lookup"><span data-stu-id="0f3f1-131">Create a new file *security-config-omsagent.conf* and add hello following content:  OMS_facility = local4</span></span>
    
    <span data-ttu-id="0f3f1-132">filter f_local4_oms { facility(local4); };</span><span class="sxs-lookup"><span data-stu-id="0f3f1-132">filter f_local4_oms { facility(local4); };</span></span>

    <span data-ttu-id="0f3f1-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span><span class="sxs-lookup"><span data-stu-id="0f3f1-133">destination security_oms { tcp("127.0.0.1" port(25226)); };</span></span>

    <span data-ttu-id="0f3f1-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span><span class="sxs-lookup"><span data-stu-id="0f3f1-134">log { source(src); filter(f_local4_oms); destination(security_oms); };</span></span>
    
3. <span data-ttu-id="0f3f1-135">Загрузите файл hello *security_events.conf* и поместите его в */etc/opt/microsoft/omsagent/conf/omsagent.d/* на компьютере агента OMS hello.</span><span class="sxs-lookup"><span data-stu-id="0f3f1-135">Download hello file *security_events.conf* and place at */etc/opt/microsoft/omsagent/conf/omsagent.d/* in hello OMS Agent computer.</span></span>
4. <span data-ttu-id="0f3f1-136">Введите команду hello ниже управляющая программа syslog hello toorestart: *для запуска syslog-ng:*</span><span class="sxs-lookup"><span data-stu-id="0f3f1-136">Type hello command below toorestart hello syslog daemon:  *For syslog-ng run:*</span></span>
    
    ```
    sudo service rsyslog restart
    ```

    <span data-ttu-id="0f3f1-137">*Для rsyslog выполните следующую команду:*</span><span class="sxs-lookup"><span data-stu-id="0f3f1-137">*For rsyslog run:*</span></span>
    
    ```
    /etc/init.d/syslog-ng restart
    ```
5. <span data-ttu-id="0f3f1-138">Введите команду hello ниже toorestart hello агента OMS.</span><span class="sxs-lookup"><span data-stu-id="0f3f1-138">Type hello command below toorestart hello OMS Agent:</span></span>

    <span data-ttu-id="0f3f1-139">*Для syslog-ng выполните следующую команду:*</span><span class="sxs-lookup"><span data-stu-id="0f3f1-139">*For syslog-ng run:*</span></span>
    
    ```
    sudo service omsagent restart
    ```

    <span data-ttu-id="0f3f1-140">*Для rsyslog выполните следующую команду:*</span><span class="sxs-lookup"><span data-stu-id="0f3f1-140">*For rsyslog run:*</span></span>
    
    ```
    systemctl restart omsagent
    ```
6. <span data-ttu-id="0f3f1-141">Введите следующую команду hello и просмотрите tooconfirm результат hello, отсутствии ошибок в журнале агента OMS hello:</span><span class="sxs-lookup"><span data-stu-id="0f3f1-141">Type hello command below and review hello result tooconfirm that there are no errors in hello OMS Agent log:</span></span>

    ``` 
    tail /var/opt/microsoft/omsagent/log/omsagent.log
    ```

## <a name="reviewing-collected-security-events"></a><span data-ttu-id="0f3f1-142">Просмотр собранных событий безопасности</span><span class="sxs-lookup"><span data-stu-id="0f3f1-142">Reviewing collected security events</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

<span data-ttu-id="0f3f1-143">После hello конфигурации находится над, событий безопасности hello запустится toobe, полученный системой безопасности OMS.</span><span class="sxs-lookup"><span data-stu-id="0f3f1-143">After hello configuration is over, hello security event will start toobe ingested by OMS Security.</span></span> <span data-ttu-id="0f3f1-144">toovisualize эти события, откройте hello поиска журналов, введите команду hello *тип = CommonSecurityLog* в hello поле поиска и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="0f3f1-144">toovisualize those events, open hello Log Search, type hello command *Type=CommonSecurityLog* in hello search field and press ENTER.</span></span> <span data-ttu-id="0f3f1-145">Hello примере показан результат hello этой команды Обратите внимание на то что в этом случае OMS безопасности уже полученный журналы безопасности от разных поставщиков:</span><span class="sxs-lookup"><span data-stu-id="0f3f1-145">hello following example shows hello result of this command, notice that in this case OMS Security already ingested security logs from multiple vendors:</span></span>
   
![Оценка базовых показателей в решении OMS "Безопасность и аудит"](./media/oms-security-connect-products/oms-security-connect-products-fig1.png)

<span data-ttu-id="0f3f1-147">Можно уточнить поиск для одного поставщика, например, журналы документации Cisco toovisualize, тип: *тип = CommonSecurityLog DeviceVendor = Cisco*.</span><span class="sxs-lookup"><span data-stu-id="0f3f1-147">You can refine this search for one single vendor, for example, toovisualize online Cisco logs, type: *Type=CommonSecurityLog DeviceVendor=Cisco*.</span></span> <span data-ttu-id="0f3f1-148">Hello «CommonSecurityLog» стандартные поля для любой заголовок CEF, включая основные extensios hello, во время любого другого расширения, является ли она «Пользовательского модуля», будет вставлен в поле «AdditionalExtensions».</span><span class="sxs-lookup"><span data-stu-id="0f3f1-148">hello “CommonSecurityLog” has predefined fields for any CEF header including hello basic extensios, while any other extension whether it’s “Custom Extension” or not, will be inserted into "AdditionalExtensions" field.</span></span> <span data-ttu-id="0f3f1-149">Можно использовать поля tooget выделенной функции hello настраиваемые поля из него.</span><span class="sxs-lookup"><span data-stu-id="0f3f1-149">You can use hello Custom Fields feature tooget dedicated fields from it.</span></span> 

### <a name="accessing-computers-missing-baseline-assessment"></a><span data-ttu-id="0f3f1-150">Просмотр сведений о компьютерах с отсутствующей базовой оценкой</span><span class="sxs-lookup"><span data-stu-id="0f3f1-150">Accessing computers missing baseline assessment</span></span>
<span data-ttu-id="0f3f1-151">OMS поддерживает профиль базового члена домена hello в Windows Server 2008 R2 до tooWindows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="0f3f1-151">OMS supports hello domain member baseline profile on Windows Server 2008 R2 up tooWindows Server 2012 R2.</span></span> <span data-ttu-id="0f3f1-152">Эта возможность для Windows Server 2016 находится на этапе разработки и будет добавлена после публикации.</span><span class="sxs-lookup"><span data-stu-id="0f3f1-152">Windows Server 2016 baseline isn’t final yet and will be added as soon as it is published.</span></span> <span data-ttu-id="0f3f1-153">Все другие операционные системы, проверенных через базовые оценки OMS безопасность и аудит отображаются под hello **компьютеры с недостающими базовых показателей оценки** раздела.</span><span class="sxs-lookup"><span data-stu-id="0f3f1-153">All other operating systems scanned via OMS Security and Audit baseline assessment appear under hello **Computers missing baseline assessment** section.</span></span>

## <a name="see-also"></a><span data-ttu-id="0f3f1-154">См. также</span><span class="sxs-lookup"><span data-stu-id="0f3f1-154">See also</span></span>
<span data-ttu-id="0f3f1-155">В этом документе вы узнали, каким образом tooconnect вашей tooOMS CEF решения.</span><span class="sxs-lookup"><span data-stu-id="0f3f1-155">In this document, you learned how tooconnect your CEF solution tooOMS.</span></span> <span data-ttu-id="0f3f1-156">toolearn Дополнительные сведения о безопасности OMS см. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="0f3f1-156">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="0f3f1-157">Общие сведения об Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="0f3f1-157">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="0f3f1-158">Мониторинг и реагирование tooSecurity оповещения в Operations Management Suite безопасности и аудита решения</span><span class="sxs-lookup"><span data-stu-id="0f3f1-158">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="0f3f1-159">Мониторинг ресурсов в решении "Безопасность и аудит" Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="0f3f1-159">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

