---
title: "aaaCollect и проанализировать сообщения системного журнала в аналитику журнала OMS | Документы Microsoft"
description: "Syslog — это протокол ведения журнала событий, общие tooLinux. В этой статье описывается tooconfigure сбора сообщений Syslog в службе анализа журналов и подробные сведения о записи hello их создания в репозитории OMS hello."
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
ms.openlocfilehash: 8bfa0bca3f2f18287d1352c98bbaa2a70e41e276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="syslog-data-sources-in-log-analytics"></a><span data-ttu-id="eb3a3-104">Источники данных системного журнала в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="eb3a3-104">Syslog data sources in Log Analytics</span></span>
<span data-ttu-id="eb3a3-105">Syslog — это протокол ведения журнала событий, общие tooLinux.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-105">Syslog is an event logging protocol that is common tooLinux.</span></span>  <span data-ttu-id="eb3a3-106">Приложения будет отправлять сообщения, хранящиеся на локальном компьютере hello или доставить tooa системного журнала сборщика.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-106">Applications will send messages that may be stored on hello local machine or delivered tooa Syslog collector.</span></span>  <span data-ttu-id="eb3a3-107">При установке агента OMS для Linux hello настраивает hello локального системного журнала управляющей программы tooforward сообщения toohello агента.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-107">When hello OMS Agent for Linux is installed, it configures hello local Syslog daemon tooforward messages toohello agent.</span></span>  <span data-ttu-id="eb3a3-108">Hello агент отправляет сообщение hello tooLog Analytics которых создается соответствующая запись в репозиторий OMS hello.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-108">hello agent then sends hello message tooLog Analytics where a corresponding record is created in hello OMS repository.</span></span>  

> [!NOTE]
> <span data-ttu-id="eb3a3-109">Служба аналитики журналов поддерживает набор сообщений, отправленных rsyslog или syslog-ng, где rsyslog — управляющая программа по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-109">Log Analytics supports collection of messages sent by rsyslog or syslog-ng, where rsyslog is hello default daemon.</span></span> <span data-ttu-id="eb3a3-110">управляющая программа syslog по умолчанию Hello в версии 5 Red Hat Enterprise Linux, CentOS и Oracle Linux (sysklog) версии не поддерживается для сбора событий syslog.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-110">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="eb3a3-111">Здравствуйте, toocollect данных syslog из этой версии данных дистрибутивов [управляющую программу rsyslog](http://rsyslog.com) должен быть установлен и настроен tooreplace sysklog.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-111">toocollect syslog data from this version of these distributions, hello [rsyslog daemon](http://rsyslog.com) should be installed and configured tooreplace sysklog.</span></span>
>
>

![Сбор сообщений системного журнала](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a><span data-ttu-id="eb3a3-113">Настройка системного журнала</span><span class="sxs-lookup"><span data-stu-id="eb3a3-113">Configuring Syslog</span></span>
<span data-ttu-id="eb3a3-114">Hello агента OMS для Linux собираются только события с помощью средства hello и степени серьезности, которые указаны в его конфигурации.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-114">hello OMS Agent for Linux will only collect events with hello facilities and severities that are specified in its configuration.</span></span>  <span data-ttu-id="eb3a3-115">Syslog можно настроить с помощью портала OMS hello или управление файлами конфигурации на агенты Linux.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-115">You can configure Syslog through hello OMS portal or by managing configuration files on your Linux agents.</span></span>

### <a name="configure-syslog-in-hello-oms-portal"></a><span data-ttu-id="eb3a3-116">Настройка системного журнала на портале OMS hello</span><span class="sxs-lookup"><span data-stu-id="eb3a3-116">Configure Syslog in hello OMS portal</span></span>
<span data-ttu-id="eb3a3-117">Настроить Syslog из hello [меню данные в параметры журнала аналитика](log-analytics-data-sources.md#configuring-data-sources).</span><span class="sxs-lookup"><span data-stu-id="eb3a3-117">Configure Syslog from hello [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>  <span data-ttu-id="eb3a3-118">Эта конфигурация будет доставлено toohello файл конфигурации на каждом агенте Linux.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-118">This configuration is delivered toohello configuration file on each Linux agent.</span></span>

<span data-ttu-id="eb3a3-119">Можно добавить новое устройство, введя его имя и нажав кнопку **+**.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-119">You can add a new facility by typing in its name and clicking **+**.</span></span>  <span data-ttu-id="eb3a3-120">Для каждой территории будут собираться только сообщения с уровнем серьезности hello выбран.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-120">For each facility, only messages with hello selected severities will be collected.</span></span>  <span data-ttu-id="eb3a3-121">Проверьте hello степени серьезности для определенной территории hello, которые должны toocollect.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-121">Check hello severities for hello particular facility that you want toocollect.</span></span>  <span data-ttu-id="eb3a3-122">Любые дополнительные критерии не может предоставить toofilter сообщений.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-122">You cannot provide any additional criteria toofilter messages.</span></span>

![Настройка системного журнала](media/log-analytics-data-sources-syslog/configure.png)

<span data-ttu-id="eb3a3-124">По умолчанию все изменения конфигурации автоматически размещаемых tooall агентов.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-124">By default, all configuration changes are automatically pushed tooall agents.</span></span>  <span data-ttu-id="eb3a3-125">Если вы хотите tooconfigure Syslog вручную на каждом агенте Linux, затем снимите флажок hello *применить указанную ниже компьютеры Linux toomy конфигурации*.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-125">If you want tooconfigure Syslog manually on each Linux agent, then uncheck hello box *Apply below configuration toomy Linux machines*.</span></span>

### <a name="configure-syslog-on-linux-agent"></a><span data-ttu-id="eb3a3-126">Настройка системного журнала на агенте Linux</span><span class="sxs-lookup"><span data-stu-id="eb3a3-126">Configure Syslog on Linux agent</span></span>
<span data-ttu-id="eb3a3-127">Здравствуйте, когда [агент OMS установлен на клиентском компьютере Linux](log-analytics-linux-agents.md), он устанавливает файл конфигурации по умолчанию syslog, определяющий помещение hello и серьезность hello сообщения, которые будут собраны.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-127">When hello [OMS agent is installed on a Linux client](log-analytics-linux-agents.md), it installs a default syslog configuration file that defines hello facility and severity of hello messages that are collected.</span></span>  <span data-ttu-id="eb3a3-128">Можно изменить эту конфигурацию файла toochange hello.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-128">You can modify this file toochange hello configuration.</span></span>  <span data-ttu-id="eb3a3-129">файл конфигурации Hello отличается в зависимости от hello управляющей программы, hello клиент установил системного журнала.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-129">hello configuration file is different depending on hello Syslog daemon that hello client has installed.</span></span>

> [!NOTE]
> <span data-ttu-id="eb3a3-130">При изменении конфигурации syslog hello, необходимо перезапустить управляющая программа syslog hello для эффекта tootake изменения hello.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-130">If you edit hello syslog configuration, you must restart hello syslog daemon for hello changes tootake effect.</span></span>
>
>

#### <a name="rsyslog"></a><span data-ttu-id="eb3a3-131">rsyslog</span><span class="sxs-lookup"><span data-stu-id="eb3a3-131">rsyslog</span></span>
<span data-ttu-id="eb3a3-132">Hello rsyslog файл конфигурации расположен в **/etc/rsyslog.d/95-omsagent.conf**.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-132">hello configuration file for rsyslog is located at **/etc/rsyslog.d/95-omsagent.conf**.</span></span>  <span data-ttu-id="eb3a3-133">Его содержимое по умолчанию приведено ниже.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-133">Its default contents are shown below.</span></span>  <span data-ttu-id="eb3a3-134">В этом разделе собраны syslog-сообщения, отправленные hello локального агента для всех средств с уровнем «предупреждение» или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-134">This collects syslog messages sent from hello local agent for all facilities with a level of warning or higher.</span></span>

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

<span data-ttu-id="eb3a3-135">Это средство управления можно удалить, удалив его разделе файла конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-135">You can remove a facility by removing its section of hello configuration file.</span></span>  <span data-ttu-id="eb3a3-136">Можно ограничить hello степени серьезности, которые собираются для определенной территории, изменив запись этого средства.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-136">You can limit hello severities that are collected for a particular facility by modifying that facility's entry.</span></span>  <span data-ttu-id="eb3a3-137">Например toomessages toolimit hello пользователя территории с уровнем серьезности ошибки или более поздней версии необходимо изменить эту строку hello конфигурации файла toohello следующие:</span><span class="sxs-lookup"><span data-stu-id="eb3a3-137">For example, toolimit hello user facility toomessages with a severity of error or higher you would modify that line of hello configuration file toohello following:</span></span>

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a><span data-ttu-id="eb3a3-138">syslog-ng</span><span class="sxs-lookup"><span data-stu-id="eb3a3-138">syslog-ng</span></span>
<span data-ttu-id="eb3a3-139">файл конфигурации Hello для syslog-ng — место, в **/etc/syslog-ng/syslog-ng.conf**.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-139">hello configuration file for syslog-ng is location at **/etc/syslog-ng/syslog-ng.conf**.</span></span>  <span data-ttu-id="eb3a3-140">Его содержимое по умолчанию приведено ниже.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-140">Its default contents are shown below.</span></span>  <span data-ttu-id="eb3a3-141">В этом разделе собраны syslog-сообщения, отправленные hello локального агента для всех средств и все уровни.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-141">This collects syslog messages sent from hello local agent for all facilities and all severities.</span></span>   

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

<span data-ttu-id="eb3a3-142">Это средство управления можно удалить, удалив его разделе файла конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-142">You can remove a facility by removing its section of hello configuration file.</span></span>  <span data-ttu-id="eb3a3-143">Можно ограничить hello степени серьезности, которые собираются для определенной территории, удалив их из списка.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-143">You can limit hello severities that are collected for a particular facility by removing them from its list.</span></span>  <span data-ttu-id="eb3a3-144">Например, toolimit hello пользователя средство toojust сообщения, предупреждения и критической ситуации, необходимо изменить этот раздел hello конфигурации файла toohello следующие:</span><span class="sxs-lookup"><span data-stu-id="eb3a3-144">For example, toolimit hello user facility toojust alert and critical messages, you would modify that section of hello configuration file toohello following:</span></span>

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a><span data-ttu-id="eb3a3-145">Сбор данных из дополнительных портов системного журнала</span><span class="sxs-lookup"><span data-stu-id="eb3a3-145">Collecting data from additional Syslog ports</span></span>
<span data-ttu-id="eb3a3-146">агент OMS Здравствуй прослушивает сообщения системного журнала на локальном клиенте hello через порт 25224.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-146">hello OMS agent listens for Syslog messages on hello local client on port 25224.</span></span>  <span data-ttu-id="eb3a3-147">При установке агента hello, применяется конфигурация syslog по умолчанию и найти в следующие расположения hello:</span><span class="sxs-lookup"><span data-stu-id="eb3a3-147">When hello agent is installed, a default syslog configuration is applied and found in hello following location:</span></span>

* <span data-ttu-id="eb3a3-148">rsyslog: `/etc/rsyslog.d/95-omsagent.conf`;</span><span class="sxs-lookup"><span data-stu-id="eb3a3-148">Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`</span></span>
* <span data-ttu-id="eb3a3-149">syslog-ng: `/etc/syslog-ng/syslog-ng.conf`.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-149">Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`</span></span>

<span data-ttu-id="eb3a3-150">Можно изменить номер порта hello, создав два файла конфигурации: FluentD config rsyslog или syslog-ng файл, в зависимости от установки управляющей программы Syslog hello.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-150">You can change hello port number by creating two configuration files: a FluentD config file and a rsyslog-or-syslog-ng file depending on hello Syslog daemon you have installed.</span></span>  

* <span data-ttu-id="eb3a3-151">файл конфигурации FluentD Hello должен быть новый файл, расположенный в: `/etc/opt/microsoft/omsagent/conf/omsagent.d` и замените значение hello hello **порт** запись с вашей другой номер порта.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-151">hello FluentD config file should be a new file located in: `/etc/opt/microsoft/omsagent/conf/omsagent.d` and replace hello value in hello **port** entry with your custom port number.</span></span>

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

* <span data-ttu-id="eb3a3-152">Для rsyslog, необходимо создать новый файл конфигурации, расположенных в: `/etc/rsyslog.d/` и замените hello значение % SYSLOG_PORT % ваш собственный номер порта.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-152">For rsyslog, you should create a new configuration file located in: `/etc/rsyslog.d/` and replace hello value %SYSLOG_PORT% with your custom port number.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="eb3a3-153">Если изменить это значение в файле конфигурации hello `95-omsagent.conf`, она будет перезаписана при hello агент применяет конфигурацию по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-153">If you modify this value in hello configuration file `95-omsagent.conf`, it will be overwritten when hello agent applies a default configuration.</span></span>
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* <span data-ttu-id="eb3a3-154">Hello syslog-ng конфигурации должен быть изменен путем копирования hello пример конфигурации показан ниже и добавление toohello настраиваемые параметры, измененные hello конец файла конфигурации syslog ng.conf hello расположен в `/etc/syslog-ng/`.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-154">hello syslog-ng config should be modified by copying hello example configuration shown below and adding hello custom modified settings toohello end of hello syslog-ng.conf configuration file located in `/etc/syslog-ng/`.</span></span>  <span data-ttu-id="eb3a3-155">Сделать **не** использовать метки по умолчанию hello **% WORKSPACE_ID % _oms** или **% WORKSPACE_ID_OMS**, определить пользовательские метки toohelp отличить изменения.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-155">Do **not** use hello default label **%WORKSPACE_ID%_oms** or **%WORKSPACE_ID_OMS**, define a custom label toohelp distinguish your changes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="eb3a3-156">При изменении значения по умолчанию hello в файле конфигурации hello, они будут перезаписаны при hello агент применяет конфигурацию по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-156">If you modify hello default values in hello configuration file, they will be overwritten when hello agent applies a default configuration.</span></span>
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

<span data-ttu-id="eb3a3-157">После завершения изменения hello, hello системного журнала и hello служба агента OMS должен перезапустить toobe tooensure hello конфигурацию изменения вступят в силу.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-157">After completing hello changes, hello Syslog and hello OMS agent service needs toobe restarted tooensure hello configuration changes take effect.</span></span>   

## <a name="syslog-record-properties"></a><span data-ttu-id="eb3a3-158">Свойства записей системного журнала</span><span class="sxs-lookup"><span data-stu-id="eb3a3-158">Syslog record properties</span></span>
<span data-ttu-id="eb3a3-159">Системный журнал записей имеют тип **Syslog** и имеющих свойства hello в hello в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-159">Syslog records have a type of **Syslog** and have hello properties in hello following table.</span></span>

| <span data-ttu-id="eb3a3-160">Свойство</span><span class="sxs-lookup"><span data-stu-id="eb3a3-160">Property</span></span> | <span data-ttu-id="eb3a3-161">Описание</span><span class="sxs-lookup"><span data-stu-id="eb3a3-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="eb3a3-162">Компьютер</span><span class="sxs-lookup"><span data-stu-id="eb3a3-162">Computer</span></span> |<span data-ttu-id="eb3a3-163">Компьютер, hello события, собранные из.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-163">Computer that hello event was collected from.</span></span> |
| <span data-ttu-id="eb3a3-164">Facility</span><span class="sxs-lookup"><span data-stu-id="eb3a3-164">Facility</span></span> |<span data-ttu-id="eb3a3-165">Определяет часть hello hello системы, создавшей приветственное сообщение.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-165">Defines hello part of hello system that generated hello message.</span></span> |
| <span data-ttu-id="eb3a3-166">HostIP</span><span class="sxs-lookup"><span data-stu-id="eb3a3-166">HostIP</span></span> |<span data-ttu-id="eb3a3-167">IP-адрес hello компьютер, отправляющий сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-167">IP address of hello system sending hello message.</span></span> |
| <span data-ttu-id="eb3a3-168">HostName</span><span class="sxs-lookup"><span data-stu-id="eb3a3-168">HostName</span></span> |<span data-ttu-id="eb3a3-169">Имя системы hello отправляет сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-169">Name of hello system sending hello message.</span></span> |
| <span data-ttu-id="eb3a3-170">SeverityLevel</span><span class="sxs-lookup"><span data-stu-id="eb3a3-170">SeverityLevel</span></span> |<span data-ttu-id="eb3a3-171">Уровень серьезности события hello.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-171">Severity level of hello event.</span></span> |
| <span data-ttu-id="eb3a3-172">SyslogMessage</span><span class="sxs-lookup"><span data-stu-id="eb3a3-172">SyslogMessage</span></span> |<span data-ttu-id="eb3a3-173">Текст сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-173">Text of hello message.</span></span> |
| <span data-ttu-id="eb3a3-174">ProcessID</span><span class="sxs-lookup"><span data-stu-id="eb3a3-174">ProcessID</span></span> |<span data-ttu-id="eb3a3-175">Идентификатор процесса hello, создавшего сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-175">ID of hello process that generated hello message.</span></span> |
| <span data-ttu-id="eb3a3-176">EventTime</span><span class="sxs-lookup"><span data-stu-id="eb3a3-176">EventTime</span></span> |<span data-ttu-id="eb3a3-177">Дата и время hello событий был создан.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-177">Date and time that hello event was generated.</span></span> |

## <a name="log-queries-with-syslog-records"></a><span data-ttu-id="eb3a3-178">Запросы к журналу для получения записей системного журнала</span><span class="sxs-lookup"><span data-stu-id="eb3a3-178">Log queries with Syslog records</span></span>
<span data-ttu-id="eb3a3-179">Hello следующей таблице приведены примеры различных журнала запросов, получающих записи Syslog.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-179">hello following table provides different examples of log queries that retrieve Syslog records.</span></span>

| <span data-ttu-id="eb3a3-180">Запрос</span><span class="sxs-lookup"><span data-stu-id="eb3a3-180">Query</span></span> | <span data-ttu-id="eb3a3-181">Описание</span><span class="sxs-lookup"><span data-stu-id="eb3a3-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="eb3a3-182">Type=Syslog</span><span class="sxs-lookup"><span data-stu-id="eb3a3-182">Type=Syslog</span></span> |<span data-ttu-id="eb3a3-183">Все записи системного журнала.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-183">All Syslogs.</span></span> |
| <span data-ttu-id="eb3a3-184">Type=Syslog SeverityLevel=error</span><span class="sxs-lookup"><span data-stu-id="eb3a3-184">Type=Syslog SeverityLevel=error</span></span> |<span data-ttu-id="eb3a3-185">Все записи системного журнала с уровнем серьезности "ошибка".</span><span class="sxs-lookup"><span data-stu-id="eb3a3-185">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="eb3a3-186">Type=Syslog &#124; measure count() by Computer</span><span class="sxs-lookup"><span data-stu-id="eb3a3-186">Type=Syslog &#124; measure count() by Computer</span></span> |<span data-ttu-id="eb3a3-187">Число записей системного журнала по компьютеру.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-187">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="eb3a3-188">Type=Syslog &#124; measure count() by Facility</span><span class="sxs-lookup"><span data-stu-id="eb3a3-188">Type=Syslog &#124; measure count() by Facility</span></span> |<span data-ttu-id="eb3a3-189">Число записей системного журнала по устройству.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-189">Count of Syslog records by facility.</span></span> |

>[!NOTE]
> <span data-ttu-id="eb3a3-190">Если рабочую область был обновленного toohello [языка запросов новый журнал аналитики](log-analytics-log-search-upgrade.md), то hello выше запросы будут изменены следующие toohello.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-190">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above queries would change toohello following.</span></span>

> | <span data-ttu-id="eb3a3-191">Запрос</span><span class="sxs-lookup"><span data-stu-id="eb3a3-191">Query</span></span> | <span data-ttu-id="eb3a3-192">Описание</span><span class="sxs-lookup"><span data-stu-id="eb3a3-192">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="eb3a3-193">syslog</span><span class="sxs-lookup"><span data-stu-id="eb3a3-193">Syslog</span></span> |<span data-ttu-id="eb3a3-194">Все записи системного журнала.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-194">All Syslogs.</span></span> |
| <span data-ttu-id="eb3a3-195">Syslog &#124; where SeverityLevel == "error"</span><span class="sxs-lookup"><span data-stu-id="eb3a3-195">Syslog &#124; where SeverityLevel == "error"</span></span> |<span data-ttu-id="eb3a3-196">Все записи системного журнала с уровнем серьезности "ошибка".</span><span class="sxs-lookup"><span data-stu-id="eb3a3-196">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="eb3a3-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span><span class="sxs-lookup"><span data-stu-id="eb3a3-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span></span> |<span data-ttu-id="eb3a3-198">Число записей системного журнала по компьютеру.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-198">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="eb3a3-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span><span class="sxs-lookup"><span data-stu-id="eb3a3-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span></span> |<span data-ttu-id="eb3a3-200">Число записей системного журнала по устройству.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-200">Count of Syslog records by facility.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="eb3a3-201">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eb3a3-201">Next steps</span></span>
* <span data-ttu-id="eb3a3-202">Дополнительные сведения о [входа выполняет](log-analytics-log-searches.md) tooanalyze hello данные, собранные из источников данных и решений.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-202">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span>
* <span data-ttu-id="eb3a3-203">Используйте [настраиваемые поля](log-analytics-custom-fields.md) tooparse данных из системного журнала записей в отдельные поля.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-203">Use [Custom Fields](log-analytics-custom-fields.md) tooparse data from syslog records into individual fields.</span></span>
* <span data-ttu-id="eb3a3-204">[Настройка агентов Linux](log-analytics-linux-agents.md) toocollect других типов данных.</span><span class="sxs-lookup"><span data-stu-id="eb3a3-204">[Configure Linux agents](log-analytics-linux-agents.md) toocollect other types of data.</span></span>
