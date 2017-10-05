---
title: "Сбор и анализ сообщений Syslog в OMS Log Analytics | Документация Майкрософт"
description: "Системный журнал (Syslog) — это протокол ведения журнала событий, который обычно используется в Linux. В этой статье описано, как настроить сбор сообщений системного журнала в службе Log Analytics, а также сведения о записях, создаваемых ими в репозитории OMS."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 7513f405d5c7c05a8e6e2b7b0e6313f23a319c84
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="syslog-data-sources-in-log-analytics"></a><span data-ttu-id="21305-104">Источники данных системного журнала в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="21305-104">Syslog data sources in Log Analytics</span></span>
<span data-ttu-id="21305-105">Системный журнал (Syslog) — это протокол ведения журнала событий, который обычно используется в Linux.</span><span class="sxs-lookup"><span data-stu-id="21305-105">Syslog is an event logging protocol that is common to Linux.</span></span>  <span data-ttu-id="21305-106">Приложения отправляют сообщения, которые могут храниться на локальном компьютере или передаваться в сборщик системного журнала.</span><span class="sxs-lookup"><span data-stu-id="21305-106">Applications will send messages that may be stored on the local machine or delivered to a Syslog collector.</span></span>  <span data-ttu-id="21305-107">При установке агента OMS для Linux он настраивает локальную управляющую программу системного журнала для пересылки сообщений в агент.</span><span class="sxs-lookup"><span data-stu-id="21305-107">When the OMS Agent for Linux is installed, it configures the local Syslog daemon to forward messages to the agent.</span></span>  <span data-ttu-id="21305-108">Затем агент отправляет сообщение в службу Log Analytics, где в репозитории OMS создается соответствующая запись.</span><span class="sxs-lookup"><span data-stu-id="21305-108">The agent then sends the message to Log Analytics where a corresponding record is created in the OMS repository.</span></span>  

> [!NOTE]
> <span data-ttu-id="21305-109">Log Analytics поддерживает сбор сообщений, отправленных rsyslog или syslog-ng, где rsyslog является управляющей программой по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="21305-109">Log Analytics supports collection of messages sent by rsyslog or syslog-ng, where rsyslog is the default daemon.</span></span> <span data-ttu-id="21305-110">Управляющая программа syslog по умолчанию не поддерживается для сбора событий системного журнала в Red Hat Enterprise Linux версии 5, CentOS и Oracle Linux (sysklog).</span><span class="sxs-lookup"><span data-stu-id="21305-110">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="21305-111">Чтобы собирать данные системного журнала из дистрибутивов этих версий, требуется установить и настроить [управляющую программу rsyslog](http://rsyslog.com) , которая заменит sysklog.</span><span class="sxs-lookup"><span data-stu-id="21305-111">To collect syslog data from this version of these distributions, the [rsyslog daemon](http://rsyslog.com) should be installed and configured to replace sysklog.</span></span>
>
>

![Сбор сообщений системного журнала](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a><span data-ttu-id="21305-113">Настройка системного журнала</span><span class="sxs-lookup"><span data-stu-id="21305-113">Configuring Syslog</span></span>
<span data-ttu-id="21305-114">Агент OMS для Linux будет собирать события только с тех устройств и только с тем уровнем серьезности, которые заданы в его конфигурации.</span><span class="sxs-lookup"><span data-stu-id="21305-114">The OMS Agent for Linux will only collect events with the facilities and severities that are specified in its configuration.</span></span>  <span data-ttu-id="21305-115">Системный журнал можно настроить на портале OMS или с помощью управления файлами конфигурации на агентах Linux.</span><span class="sxs-lookup"><span data-stu-id="21305-115">You can configure Syslog through the OMS portal or by managing configuration files on your Linux agents.</span></span>

### <a name="configure-syslog-in-the-oms-portal"></a><span data-ttu-id="21305-116">Настройка системного журнала на портале OMS</span><span class="sxs-lookup"><span data-stu-id="21305-116">Configure Syslog in the OMS portal</span></span>
<span data-ttu-id="21305-117">Настройте системный журнал в [меню "Данные" раздела "Параметры" Log Analytics](log-analytics-data-sources.md#configuring-data-sources).</span><span class="sxs-lookup"><span data-stu-id="21305-117">Configure Syslog from the [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>  <span data-ttu-id="21305-118">Эта конфигурация передается в файл конфигурации на каждом агенте Linux.</span><span class="sxs-lookup"><span data-stu-id="21305-118">This configuration is delivered to the configuration file on each Linux agent.</span></span>

<span data-ttu-id="21305-119">Можно добавить новое устройство, введя его имя и нажав кнопку **+**.</span><span class="sxs-lookup"><span data-stu-id="21305-119">You can add a new facility by typing in its name and clicking **+**.</span></span>  <span data-ttu-id="21305-120">Для каждого устройства будут собираться сообщения только с выбранным уровнем серьезности.</span><span class="sxs-lookup"><span data-stu-id="21305-120">For each facility, only messages with the selected severities will be collected.</span></span>  <span data-ttu-id="21305-121">Укажите уровни серьезности сообщений, которые хотите получать от соответствующего устройства.</span><span class="sxs-lookup"><span data-stu-id="21305-121">Check the severities for the particular facility that you want to collect.</span></span>  <span data-ttu-id="21305-122">Дополнительные критерии для фильтрации сообщений задавать нельзя.</span><span class="sxs-lookup"><span data-stu-id="21305-122">You cannot provide any additional criteria to filter messages.</span></span>

![Настройка системного журнала](media/log-analytics-data-sources-syslog/configure.png)

<span data-ttu-id="21305-124">По умолчанию все изменения конфигурации автоматически отправляются во все агенты.</span><span class="sxs-lookup"><span data-stu-id="21305-124">By default, all configuration changes are automatically pushed to all agents.</span></span>  <span data-ttu-id="21305-125">Если вы хотите настроить системный журнал вручную на каждом агенте Linux, снимите флажок *Apply below configuration to my Linux machines*(Применить конфигурацию ниже к моим компьютерам Linux).</span><span class="sxs-lookup"><span data-stu-id="21305-125">If you want to configure Syslog manually on each Linux agent, then uncheck the box *Apply below configuration to my Linux machines*.</span></span>

### <a name="configure-syslog-on-linux-agent"></a><span data-ttu-id="21305-126">Настройка системного журнала на агенте Linux</span><span class="sxs-lookup"><span data-stu-id="21305-126">Configure Syslog on Linux agent</span></span>
<span data-ttu-id="21305-127">При [установке агента OMS на клиент Linux](log-analytics-linux-agents.md)он устанавливает файл конфигурации системного журнала по умолчанию, который определяет устройства и уровень серьезности для собираемых сообщений.</span><span class="sxs-lookup"><span data-stu-id="21305-127">When the [OMS agent is installed on a Linux client](log-analytics-linux-agents.md), it installs a default syslog configuration file that defines the facility and severity of the messages that are collected.</span></span>  <span data-ttu-id="21305-128">Можно изменить этот файл, чтобы внести изменения в конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="21305-128">You can modify this file to change the configuration.</span></span>  <span data-ttu-id="21305-129">Файл конфигурации отличается в зависимости от того, какую управляющая программу системного журнала установил клиент.</span><span class="sxs-lookup"><span data-stu-id="21305-129">The configuration file is different depending on the Syslog daemon that the client has installed.</span></span>

> [!NOTE]
> <span data-ttu-id="21305-130">При изменении конфигурации системного журнала требуется перезапустить управляющую программу syslog, чтобы изменения вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="21305-130">If you edit the syslog configuration, you must restart the syslog daemon for the changes to take effect.</span></span>
>
>

#### <a name="rsyslog"></a><span data-ttu-id="21305-131">rsyslog</span><span class="sxs-lookup"><span data-stu-id="21305-131">rsyslog</span></span>
<span data-ttu-id="21305-132">Файл конфигурации для rsyslog находится в расположении **/etc/rsyslog.d/95-omsagent.conf**.</span><span class="sxs-lookup"><span data-stu-id="21305-132">The configuration file for rsyslog is located at **/etc/rsyslog.d/95-omsagent.conf**.</span></span>  <span data-ttu-id="21305-133">Его содержимое по умолчанию приведено ниже.</span><span class="sxs-lookup"><span data-stu-id="21305-133">Its default contents are shown below.</span></span>  <span data-ttu-id="21305-134">В данном случае собираются сообщения системного журнала, отправленные из локального агента для всех устройств и имеющие уровень серьезности "предупреждение" или выше.</span><span class="sxs-lookup"><span data-stu-id="21305-134">This collects syslog messages sent from the local agent for all facilities with a level of warning or higher.</span></span>

    kern.warning       @127.0.0.1:25224
    user.warning       @127.0.0.1:25224
    daemon.warning     @127.0.0.1:25224
    auth.warning       @127.0.0.1:25224
    syslog.warning     @127.0.0.1:25224
    uucp.warning       @127.0.0.1:25224
    authpriv.warning   @127.0.0.1:25224
    ftp.warning        @127.0.0.1:25224
    cron.warning       @127.0.0.1:25224
    local0.warning     @127.0.0.1:25224
    local1.warning     @127.0.0.1:25224
    local2.warning     @127.0.0.1:25224
    local3.warning     @127.0.0.1:25224
    local4.warning     @127.0.0.1:25224
    local5.warning     @127.0.0.1:25224
    local6.warning     @127.0.0.1:25224
    local7.warning     @127.0.0.1:25224

<span data-ttu-id="21305-135">Устройство можно удалить, выполнив удаление соответствующего раздела в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="21305-135">You can remove a facility by removing its section of the configuration file.</span></span>  <span data-ttu-id="21305-136">Можно ограничить уровни серьезности для сообщений, собираемых с конкретного устройства, изменив соответствующую запись устройства.</span><span class="sxs-lookup"><span data-stu-id="21305-136">You can limit the severities that are collected for a particular facility by modifying that facility's entry.</span></span>  <span data-ttu-id="21305-137">Например, чтобы ограничить сообщения с пользовательского устройства уровнем серьезности "ошибка" или выше, необходимо изменить соответствующую строку в файле конфигурации таким образом:</span><span class="sxs-lookup"><span data-stu-id="21305-137">For example, to limit the user facility to messages with a severity of error or higher you would modify that line of the configuration file to the following:</span></span>

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a><span data-ttu-id="21305-138">syslog-ng</span><span class="sxs-lookup"><span data-stu-id="21305-138">syslog-ng</span></span>
<span data-ttu-id="21305-139">Файл конфигурации для syslog-ng находится в расположении **/etc/syslog-ng/syslog-ng.conf**.</span><span class="sxs-lookup"><span data-stu-id="21305-139">The configuration file for syslog-ng is location at **/etc/syslog-ng/syslog-ng.conf**.</span></span>  <span data-ttu-id="21305-140">Его содержимое по умолчанию приведено ниже.</span><span class="sxs-lookup"><span data-stu-id="21305-140">Its default contents are shown below.</span></span>  <span data-ttu-id="21305-141">В данном случае собираются сообщения системного журнала, отправленные из локального агента для всех устройств и всех уровней серьезности.</span><span class="sxs-lookup"><span data-stu-id="21305-141">This collects syslog messages sent from the local agent for all facilities and all severities.</span></span>   

    #
    # Warnings (except iptables) in one file:
    #
    destination warn { file("/var/log/warn" fsync(yes)); };
    log { source(src); filter(f_warn); destination(warn); };

    #OMS_Destination
    destination d_oms { udp("127.0.0.1" port(25224)); };

    #OMS_facility = auth
    filter f_auth_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(auth); };
    log { source(src); filter(f_auth_oms); destination(d_oms); };

    #OMS_facility = authpriv
    filter f_authpriv_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(authpriv); };
    log { source(src); filter(f_authpriv_oms); destination(d_oms); };

    #OMS_facility = cron
    filter f_cron_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(cron); };
    log { source(src); filter(f_cron_oms); destination(d_oms); };

    #OMS_facility = daemon
    filter f_daemon_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(daemon); };
    log { source(src); filter(f_daemon_oms); destination(d_oms); };

    #OMS_facility = kern
    filter f_kern_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(kern); };
    log { source(src); filter(f_kern_oms); destination(d_oms); };

    #OMS_facility = local0
    filter f_local0_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local0); };
    log { source(src); filter(f_local0_oms); destination(d_oms); };

    #OMS_facility = local1
    filter f_local1_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local1); };
    log { source(src); filter(f_local1_oms); destination(d_oms); };

    #OMS_facility = mail
    filter f_mail_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(mail); };
    log { source(src); filter(f_mail_oms); destination(d_oms); };

    #OMS_facility = syslog
    filter f_syslog_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(syslog); };
    log { source(src); filter(f_syslog_oms); destination(d_oms); };

    #OMS_facility = user
    filter f_user_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };

<span data-ttu-id="21305-142">Устройство можно удалить, выполнив удаление соответствующего раздела в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="21305-142">You can remove a facility by removing its section of the configuration file.</span></span>  <span data-ttu-id="21305-143">Можно ограничить уровни серьезности для сообщений, собираемых с конкретного устройства, удалив их из его списка.</span><span class="sxs-lookup"><span data-stu-id="21305-143">You can limit the severities that are collected for a particular facility by removing them from its list.</span></span>  <span data-ttu-id="21305-144">Например, чтобы ограничить сообщения с пользовательского устройства только уровнями серьезности "оповещение" и "критический", необходимо изменить соответствующий раздел в файле конфигурации таким образом:</span><span class="sxs-lookup"><span data-stu-id="21305-144">For example, to limit the user facility to just alert and critical messages, you would modify that section of the configuration file to the following:</span></span>

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a><span data-ttu-id="21305-145">Сбор данных из дополнительных портов системного журнала</span><span class="sxs-lookup"><span data-stu-id="21305-145">Collecting data from additional Syslog ports</span></span>
<span data-ttu-id="21305-146">Агент OMS прослушивает сообщения системного журнала на локальном клиенте через порт 25224.</span><span class="sxs-lookup"><span data-stu-id="21305-146">The OMS agent listens for Syslog messages on the local client on port 25224.</span></span>  <span data-ttu-id="21305-147">При установке агента применяется конфигурация системного журнала по умолчанию. Файл конфигурации расположен в следующем расположении:</span><span class="sxs-lookup"><span data-stu-id="21305-147">When the agent is installed, a default syslog configuration is applied and found in the following location:</span></span>

* <span data-ttu-id="21305-148">rsyslog: `/etc/rsyslog.d/95-omsagent.conf`;</span><span class="sxs-lookup"><span data-stu-id="21305-148">Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`</span></span>
* <span data-ttu-id="21305-149">syslog-ng: `/etc/syslog-ng/syslog-ng.conf`.</span><span class="sxs-lookup"><span data-stu-id="21305-149">Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`</span></span>

<span data-ttu-id="21305-150">Номер порта можно изменить, создав два файла конфигурации: FluentD и rsyslog-or-syslog-ng (в зависимости от установленной управляющей программы системного журнала).</span><span class="sxs-lookup"><span data-stu-id="21305-150">You can change the port number by creating two configuration files: a FluentD config file and a rsyslog-or-syslog-ng file depending on the Syslog daemon you have installed.</span></span>  

* <span data-ttu-id="21305-151">Файл конфигурации FluentD должен быть новым и располагаться в папке `/etc/opt/microsoft/omsagent/conf/omsagent.d`. Замените значение записи **port** собственным номером порта.</span><span class="sxs-lookup"><span data-stu-id="21305-151">The FluentD config file should be a new file located in: `/etc/opt/microsoft/omsagent/conf/omsagent.d` and replace the value in the **port** entry with your custom port number.</span></span>

        <source>
          type syslog
          port %SYSLOG_PORT%
          bind 127.0.0.1
          protocol_type udp
          tag oms.syslog
        </source>
        <filter oms.syslog.**>
          type filter_syslog
        </filter>

* <span data-ttu-id="21305-152">Для rsyslog в папке `/etc/rsyslog.d/` необходимо создать файл конфигурации. Замените значение %SYSLOG_PORT% собственным номером порта.</span><span class="sxs-lookup"><span data-stu-id="21305-152">For rsyslog, you should create a new configuration file located in: `/etc/rsyslog.d/` and replace the value %SYSLOG_PORT% with your custom port number.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="21305-153">Если изменить это значение в файле конфигурации `95-omsagent.conf`, он перезаписывается, когда агент применяет конфигурацию по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="21305-153">If you modify this value in the configuration file `95-omsagent.conf`, it will be overwritten when the agent applies a default configuration.</span></span>
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* <span data-ttu-id="21305-154">Конфигурацию syslog-ng следует изменить. Для этого скопируйте пример конфигурации ниже и добавьте измененные параметры в конец файла конфигурации в папке `/etc/syslog-ng/`.</span><span class="sxs-lookup"><span data-stu-id="21305-154">The syslog-ng config should be modified by copying the example configuration shown below and adding the custom modified settings to the end of the syslog-ng.conf configuration file located in `/etc/syslog-ng/`.</span></span>  <span data-ttu-id="21305-155">**Не** используйте метку **%WORKSPACE_ID%_oms** или **%WORKSPACE_ID_OMS** по умолчанию. Чтобы различить изменения, определите собственную метку.</span><span class="sxs-lookup"><span data-stu-id="21305-155">Do **not** use the default label **%WORKSPACE_ID%_oms** or **%WORKSPACE_ID_OMS**, define a custom label to help distinguish your changes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="21305-156">Если изменить эти значения по умолчанию в файле конфигурации, он перезаписывается, когда агент применяет конфигурацию по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="21305-156">If you modify the default values in the configuration file, they will be overwritten when the agent applies a default configuration.</span></span>
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

<span data-ttu-id="21305-157">После внесения изменений системный журнал и службу агента OMS следует перезапустить, чтобы изменения вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="21305-157">After completing the changes, the Syslog and the OMS agent service needs to be restarted to ensure the configuration changes take effect.</span></span>   

## <a name="syslog-record-properties"></a><span data-ttu-id="21305-158">Свойства записей системного журнала</span><span class="sxs-lookup"><span data-stu-id="21305-158">Syslog record properties</span></span>
<span data-ttu-id="21305-159">Записи системного журнала имеют тип **Syslog** и свойства, описанные в приведенной ниже таблице.</span><span class="sxs-lookup"><span data-stu-id="21305-159">Syslog records have a type of **Syslog** and have the properties in the following table.</span></span>

| <span data-ttu-id="21305-160">Свойство</span><span class="sxs-lookup"><span data-stu-id="21305-160">Property</span></span> | <span data-ttu-id="21305-161">Описание</span><span class="sxs-lookup"><span data-stu-id="21305-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="21305-162">Компьютер</span><span class="sxs-lookup"><span data-stu-id="21305-162">Computer</span></span> |<span data-ttu-id="21305-163">Компьютер, с которого было получено событие.</span><span class="sxs-lookup"><span data-stu-id="21305-163">Computer that the event was collected from.</span></span> |
| <span data-ttu-id="21305-164">Facility</span><span class="sxs-lookup"><span data-stu-id="21305-164">Facility</span></span> |<span data-ttu-id="21305-165">Определяет часть системы, которая создала сообщение.</span><span class="sxs-lookup"><span data-stu-id="21305-165">Defines the part of the system that generated the message.</span></span> |
| <span data-ttu-id="21305-166">HostIP</span><span class="sxs-lookup"><span data-stu-id="21305-166">HostIP</span></span> |<span data-ttu-id="21305-167">IP-адрес системы, отправившей сообщение.</span><span class="sxs-lookup"><span data-stu-id="21305-167">IP address of the system sending the message.</span></span> |
| <span data-ttu-id="21305-168">HostName</span><span class="sxs-lookup"><span data-stu-id="21305-168">HostName</span></span> |<span data-ttu-id="21305-169">Имя системы, отправившей сообщение.</span><span class="sxs-lookup"><span data-stu-id="21305-169">Name of the system sending the message.</span></span> |
| <span data-ttu-id="21305-170">SeverityLevel</span><span class="sxs-lookup"><span data-stu-id="21305-170">SeverityLevel</span></span> |<span data-ttu-id="21305-171">Уровень серьезности события.</span><span class="sxs-lookup"><span data-stu-id="21305-171">Severity level of the event.</span></span> |
| <span data-ttu-id="21305-172">SyslogMessage</span><span class="sxs-lookup"><span data-stu-id="21305-172">SyslogMessage</span></span> |<span data-ttu-id="21305-173">Текст сообщения.</span><span class="sxs-lookup"><span data-stu-id="21305-173">Text of the message.</span></span> |
| <span data-ttu-id="21305-174">ProcessID</span><span class="sxs-lookup"><span data-stu-id="21305-174">ProcessID</span></span> |<span data-ttu-id="21305-175">Идентификатор процесса, создавшего сообщение.</span><span class="sxs-lookup"><span data-stu-id="21305-175">ID of the process that generated the message.</span></span> |
| <span data-ttu-id="21305-176">EventTime</span><span class="sxs-lookup"><span data-stu-id="21305-176">EventTime</span></span> |<span data-ttu-id="21305-177">Дата и время создания события.</span><span class="sxs-lookup"><span data-stu-id="21305-177">Date and time that the event was generated.</span></span> |

## <a name="log-queries-with-syslog-records"></a><span data-ttu-id="21305-178">Запросы к журналу для получения записей системного журнала</span><span class="sxs-lookup"><span data-stu-id="21305-178">Log queries with Syslog records</span></span>
<span data-ttu-id="21305-179">В следующей таблице представлены различные примеры запросов к журналу, извлекающих записи из системного журнала.</span><span class="sxs-lookup"><span data-stu-id="21305-179">The following table provides different examples of log queries that retrieve Syslog records.</span></span>

| <span data-ttu-id="21305-180">Запрос</span><span class="sxs-lookup"><span data-stu-id="21305-180">Query</span></span> | <span data-ttu-id="21305-181">Описание</span><span class="sxs-lookup"><span data-stu-id="21305-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="21305-182">Type=Syslog</span><span class="sxs-lookup"><span data-stu-id="21305-182">Type=Syslog</span></span> |<span data-ttu-id="21305-183">Все записи системного журнала.</span><span class="sxs-lookup"><span data-stu-id="21305-183">All Syslogs.</span></span> |
| <span data-ttu-id="21305-184">Type=Syslog SeverityLevel=error</span><span class="sxs-lookup"><span data-stu-id="21305-184">Type=Syslog SeverityLevel=error</span></span> |<span data-ttu-id="21305-185">Все записи системного журнала с уровнем серьезности "ошибка".</span><span class="sxs-lookup"><span data-stu-id="21305-185">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="21305-186">Type=Syslog &#124; measure count() by Computer</span><span class="sxs-lookup"><span data-stu-id="21305-186">Type=Syslog &#124; measure count() by Computer</span></span> |<span data-ttu-id="21305-187">Число записей системного журнала по компьютеру.</span><span class="sxs-lookup"><span data-stu-id="21305-187">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="21305-188">Type=Syslog &#124; measure count() by Facility</span><span class="sxs-lookup"><span data-stu-id="21305-188">Type=Syslog &#124; measure count() by Facility</span></span> |<span data-ttu-id="21305-189">Число записей системного журнала по устройству.</span><span class="sxs-lookup"><span data-stu-id="21305-189">Count of Syslog records by facility.</span></span> |

>[!NOTE]
> <span data-ttu-id="21305-190">Если ваша рабочая область переведена на [язык запросов Log Analytics](log-analytics-log-search-upgrade.md), указанные выше запросы будут изменены следующим образом.</span><span class="sxs-lookup"><span data-stu-id="21305-190">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above queries would change to the following.</span></span>

> | <span data-ttu-id="21305-191">Запрос</span><span class="sxs-lookup"><span data-stu-id="21305-191">Query</span></span> | <span data-ttu-id="21305-192">Описание</span><span class="sxs-lookup"><span data-stu-id="21305-192">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="21305-193">syslog</span><span class="sxs-lookup"><span data-stu-id="21305-193">Syslog</span></span> |<span data-ttu-id="21305-194">Все записи системного журнала.</span><span class="sxs-lookup"><span data-stu-id="21305-194">All Syslogs.</span></span> |
| <span data-ttu-id="21305-195">Syslog &#124; where SeverityLevel == "error"</span><span class="sxs-lookup"><span data-stu-id="21305-195">Syslog &#124; where SeverityLevel == "error"</span></span> |<span data-ttu-id="21305-196">Все записи системного журнала с уровнем серьезности "ошибка".</span><span class="sxs-lookup"><span data-stu-id="21305-196">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="21305-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span><span class="sxs-lookup"><span data-stu-id="21305-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span></span> |<span data-ttu-id="21305-198">Число записей системного журнала по компьютеру.</span><span class="sxs-lookup"><span data-stu-id="21305-198">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="21305-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span><span class="sxs-lookup"><span data-stu-id="21305-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span></span> |<span data-ttu-id="21305-200">Число записей системного журнала по устройству.</span><span class="sxs-lookup"><span data-stu-id="21305-200">Count of Syslog records by facility.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="21305-201">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="21305-201">Next steps</span></span>
* <span data-ttu-id="21305-202">Узнайте больше об [операциях поиска по журналу](log-analytics-log-searches.md) , которые можно применять для анализа данных, собираемых из источников данных и решений.</span><span class="sxs-lookup"><span data-stu-id="21305-202">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span>
* <span data-ttu-id="21305-203">Используйте [настраиваемые поля](log-analytics-custom-fields.md) для анализа данных из записей системного журнала в отдельных полях.</span><span class="sxs-lookup"><span data-stu-id="21305-203">Use [Custom Fields](log-analytics-custom-fields.md) to parse data from syslog records into individual fields.</span></span>
* <span data-ttu-id="21305-204">[Настройте агенты Linux](log-analytics-linux-agents.md) для сбора других типов данных.</span><span class="sxs-lookup"><span data-stu-id="21305-204">[Configure Linux agents](log-analytics-linux-agents.md) to collect other types of data.</span></span>
