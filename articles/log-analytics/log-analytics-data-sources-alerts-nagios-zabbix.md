---
title: "оповещения Nagios и Zabbix aaaCollect в аналитику журнала OMS | Документы Microsoft"
description: "Nagios и Zabbix — средства мониторинга с открытым исходным кодом. Можно собирать оповещения, с помощью этих средств в службе анализа журналов в порядке tooanalyze их вместе с предупреждениями из других источников.  В этой статье описывается, как tooconfigure hello агента OMS для Linux toocollect оповещений из этих систем."
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
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 23e2252e4fed8bc87baec063694a8472ca84220d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a><span data-ttu-id="25b8c-105">Сбор оповещений Nagios и Zabbix из агента OMS для Linux в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="25b8c-105">Collect alerts from Nagios and Zabbix in Log Analytics from OMS Agent for Linux</span></span> 
<span data-ttu-id="25b8c-106">[Nagios](https://www.nagios.org/) и [Zabbix](http://www.zabbix.com/) — средства мониторинга с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="25b8c-106">[Nagios](https://www.nagios.org/) and [Zabbix](http://www.zabbix.com/) are open source monitoring tools.</span></span>  <span data-ttu-id="25b8c-107">Можно собирать оповещения, с помощью этих средств в службе анализа журналов в порядке tooanalyze их вместе с [предупреждениями из других источников](log-analytics-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="25b8c-107">You can collect alerts from these tools into Log Analytics in order tooanalyze them along with [alerts from other sources](log-analytics-alerts.md).</span></span>  <span data-ttu-id="25b8c-108">В этой статье описывается, как tooconfigure hello агента OMS для Linux toocollect оповещений из этих систем.</span><span class="sxs-lookup"><span data-stu-id="25b8c-108">This article describes how tooconfigure hello OMS Agent for Linux toocollect alerts from these systems.</span></span>
 
## <a name="configure-alert-collection"></a><span data-ttu-id="25b8c-109">Настройка сбора оповещений</span><span class="sxs-lookup"><span data-stu-id="25b8c-109">Configure alert collection</span></span>

### <a name="configuring-nagios-alert-collection"></a><span data-ttu-id="25b8c-110">Настройка сбора оповещений Nagios</span><span class="sxs-lookup"><span data-stu-id="25b8c-110">Configuring Nagios alert collection</span></span>
<span data-ttu-id="25b8c-111">Выполните следующие действия на предупреждения toocollect сервера Nagios hello hello.</span><span class="sxs-lookup"><span data-stu-id="25b8c-111">Perform hello following steps on hello Nagios server toocollect alerts.</span></span>

1. <span data-ttu-id="25b8c-112">Предоставление пользовательских hello **omsagent** файла журнала Nagios toohello доступ для чтения (т. е. `/var/log/nagios/nagios.log`).</span><span class="sxs-lookup"><span data-stu-id="25b8c-112">Grant hello user **omsagent** read access toohello Nagios log file (i.e. `/var/log/nagios/nagios.log`).</span></span> <span data-ttu-id="25b8c-113">При условии, что файл nagios.log hello принадлежит группе hello `nagios`, можно добавить пользователя hello **omsagent** toohello **nagios** группы.</span><span class="sxs-lookup"><span data-stu-id="25b8c-113">Assuming hello nagios.log file is owned by hello group `nagios`, you can add hello user **omsagent** toohello **nagios** group.</span></span> 

    <span data-ttu-id="25b8c-114">sudo usermod -a -G nagios omsagent</span><span class="sxs-lookup"><span data-stu-id="25b8c-114">sudo usermod -a -G nagios omsagent</span></span>

2.  <span data-ttu-id="25b8c-115">Изменение файла конфигурации hello в (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="25b8c-115">Modify hello configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="25b8c-116">Убедитесь, что присутствуют и не закомментированы следующие записи hello:</span><span class="sxs-lookup"><span data-stu-id="25b8c-116">Ensure hello following entries are present and not commented out:</span></span>  

        <source>  
          type tail  
          #Update path toopoint tooyour nagios.log  
          path /var/log/nagios/nagios.log  
          format none  
          tag oms.nagios  
        </source>  
      
        <filter oms.nagios>  
          type filter_nagios_log  
        </filter>  

3. <span data-ttu-id="25b8c-117">Перезапустите управляющую программу omsagent hello</span><span class="sxs-lookup"><span data-stu-id="25b8c-117">Restart hello omsagent daemon</span></span>

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a><span data-ttu-id="25b8c-118">Настройка сбора оповещений Zabbix</span><span class="sxs-lookup"><span data-stu-id="25b8c-118">Configuring Zabbix alert collection</span></span>
<span data-ttu-id="25b8c-119">toocollect предупреждения с сервера Zabbix, требуются toospecify пользователя и пароль в *открытый текст*.</span><span class="sxs-lookup"><span data-stu-id="25b8c-119">toocollect alerts from a Zabbix server, you need toospecify a user and password in *clear text*.</span></span> <span data-ttu-id="25b8c-120">Это не идеальное решение, но рекомендуется создать пользователя hello и предоставить onlu toomonitor разрешения.</span><span class="sxs-lookup"><span data-stu-id="25b8c-120">This is not ideal, but we recommend that you create hello user and grant permissions toomonitor onlu.</span></span>

<span data-ttu-id="25b8c-121">Выполните следующие действия на предупреждения toocollect сервера Nagios hello hello.</span><span class="sxs-lookup"><span data-stu-id="25b8c-121">Perform hello following steps on hello Nagios server toocollect alerts.</span></span>

1. <span data-ttu-id="25b8c-122">Изменение файла конфигурации hello в (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="25b8c-122">Modify hello configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="25b8c-123">Убедитесь, что присутствуют и не закомментированы следующие записи hello.  Изменить hello пользователя имя и пароль toovalues Zabbix среды.</span><span class="sxs-lookup"><span data-stu-id="25b8c-123">Ensure hello following entries are present and not commented out.  Change hello user name and password toovalues for your Zabbix environment.</span></span>

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. <span data-ttu-id="25b8c-124">Перезапустите управляющую программу omsagent hello</span><span class="sxs-lookup"><span data-stu-id="25b8c-124">Restart hello omsagent daemon</span></span>

    <span data-ttu-id="25b8c-125">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span><span class="sxs-lookup"><span data-stu-id="25b8c-125">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span></span>


## <a name="alert-records"></a><span data-ttu-id="25b8c-126">Записи оповещений</span><span class="sxs-lookup"><span data-stu-id="25b8c-126">Alert records</span></span>
<span data-ttu-id="25b8c-127">Записи оповещений из Nagios и Zabbix можно получить с помощью [поиска по журналам](log-analytics-log-searches.md) в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="25b8c-127">You can retrieve alert records from Nagios and Zabbix using [log searches](log-analytics-log-searches.md) in Log Analytics.</span></span>

### <a name="nagios-alert-records"></a><span data-ttu-id="25b8c-128">Записи оповещений Nagios</span><span class="sxs-lookup"><span data-stu-id="25b8c-128">Nagios Alert records</span></span>

<span data-ttu-id="25b8c-129">Для записей оповещений Nagios параметр **Type** (тип) имеет значение **Alert** (оповещение), а параметр **SourceSystem** (источник) — значение **Nagios**.</span><span class="sxs-lookup"><span data-stu-id="25b8c-129">Alert records collected by Nagios have a **Type** of **Alert** and a **SourceSystem** of **Nagios**.</span></span>  <span data-ttu-id="25b8c-130">Они имеют свойства hello в hello в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="25b8c-130">They have hello properties in hello following table.</span></span>

| <span data-ttu-id="25b8c-131">Свойство</span><span class="sxs-lookup"><span data-stu-id="25b8c-131">Property</span></span> | <span data-ttu-id="25b8c-132">Описание</span><span class="sxs-lookup"><span data-stu-id="25b8c-132">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="25b8c-133">Тип</span><span class="sxs-lookup"><span data-stu-id="25b8c-133">Type</span></span> |<span data-ttu-id="25b8c-134">*Предупреждение*</span><span class="sxs-lookup"><span data-stu-id="25b8c-134">*Alert*</span></span> |
| <span data-ttu-id="25b8c-135">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="25b8c-135">SourceSystem</span></span> |<span data-ttu-id="25b8c-136">*Nagios*</span><span class="sxs-lookup"><span data-stu-id="25b8c-136">*Nagios*</span></span> |
| <span data-ttu-id="25b8c-137">AlertName</span><span class="sxs-lookup"><span data-stu-id="25b8c-137">AlertName</span></span> |<span data-ttu-id="25b8c-138">Имя предупреждения hello.</span><span class="sxs-lookup"><span data-stu-id="25b8c-138">Name of hello alert.</span></span> |
| <span data-ttu-id="25b8c-139">AlertDescription</span><span class="sxs-lookup"><span data-stu-id="25b8c-139">AlertDescription</span></span> | <span data-ttu-id="25b8c-140">Описание предупреждения hello.</span><span class="sxs-lookup"><span data-stu-id="25b8c-140">Description of hello alert.</span></span> |
| <span data-ttu-id="25b8c-141">AlertState</span><span class="sxs-lookup"><span data-stu-id="25b8c-141">AlertState</span></span> | <span data-ttu-id="25b8c-142">Состояние узла или службы hello.</span><span class="sxs-lookup"><span data-stu-id="25b8c-142">Status of hello service or host.</span></span><br><br><span data-ttu-id="25b8c-143">ОК</span><span class="sxs-lookup"><span data-stu-id="25b8c-143">OK</span></span><br><span data-ttu-id="25b8c-144">ПРЕДУПРЕЖДЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="25b8c-144">WARNING</span></span><br><span data-ttu-id="25b8c-145">РАБОТАЕТ</span><span class="sxs-lookup"><span data-stu-id="25b8c-145">UP</span></span><br><span data-ttu-id="25b8c-146">СБОЙ</span><span class="sxs-lookup"><span data-stu-id="25b8c-146">DOWN</span></span> |
| <span data-ttu-id="25b8c-147">HostName</span><span class="sxs-lookup"><span data-stu-id="25b8c-147">HostName</span></span> | <span data-ttu-id="25b8c-148">Имя узла hello, создавшего предупреждение hello.</span><span class="sxs-lookup"><span data-stu-id="25b8c-148">Name of hello host that created hello alert.</span></span> |
| <span data-ttu-id="25b8c-149">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="25b8c-149">PriorityNumber</span></span> | <span data-ttu-id="25b8c-150">Уровень приоритета предупреждения hello.</span><span class="sxs-lookup"><span data-stu-id="25b8c-150">Priority level of hello alert.</span></span> |
| <span data-ttu-id="25b8c-151">StateType</span><span class="sxs-lookup"><span data-stu-id="25b8c-151">StateType</span></span> | <span data-ttu-id="25b8c-152">Тип состояния предупреждения hello Hello.</span><span class="sxs-lookup"><span data-stu-id="25b8c-152">hello type of state of hello alert.</span></span><br><br><span data-ttu-id="25b8c-153">SOFT — проблема, которая не проверялась повторно.</span><span class="sxs-lookup"><span data-stu-id="25b8c-153">SOFT - Issue that has not been rechecked.</span></span><br><span data-ttu-id="25b8c-154">HARD — проблема, которая проверялась повторно заданное число раз.</span><span class="sxs-lookup"><span data-stu-id="25b8c-154">HARD - Issue that has been rechecked a specified number of times.</span></span>  |
| <span data-ttu-id="25b8c-155">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="25b8c-155">TimeGenerated</span></span> |<span data-ttu-id="25b8c-156">Создания предупреждения hello даты и времени.</span><span class="sxs-lookup"><span data-stu-id="25b8c-156">Date and time hello alert was created.</span></span> |


### <a name="zabbix-alert-records"></a><span data-ttu-id="25b8c-157">Записи оповещений Zabbix</span><span class="sxs-lookup"><span data-stu-id="25b8c-157">Zabbix alert records</span></span>
<span data-ttu-id="25b8c-158">Для записей оповещений Nagios параметр **Type** (тип) имеет значение **Alert** (оповещение), а параметр **SourceSystem** (источник) — значение **Zabbix**.</span><span class="sxs-lookup"><span data-stu-id="25b8c-158">Alert records collected by Zabbix have a **Type** of **Alert** and a **SourceSystem** of **Zabbix**.</span></span>  <span data-ttu-id="25b8c-159">Они имеют свойства hello в hello в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="25b8c-159">They have hello properties in hello following table.</span></span>

| <span data-ttu-id="25b8c-160">Свойство</span><span class="sxs-lookup"><span data-stu-id="25b8c-160">Property</span></span> | <span data-ttu-id="25b8c-161">Описание</span><span class="sxs-lookup"><span data-stu-id="25b8c-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="25b8c-162">Тип</span><span class="sxs-lookup"><span data-stu-id="25b8c-162">Type</span></span> |<span data-ttu-id="25b8c-163">*Предупреждение*</span><span class="sxs-lookup"><span data-stu-id="25b8c-163">*Alert*</span></span> |
| <span data-ttu-id="25b8c-164">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="25b8c-164">SourceSystem</span></span> |<span data-ttu-id="25b8c-165">*Zabbix*</span><span class="sxs-lookup"><span data-stu-id="25b8c-165">*Zabbix*</span></span> |
| <span data-ttu-id="25b8c-166">AlertName</span><span class="sxs-lookup"><span data-stu-id="25b8c-166">AlertName</span></span> | <span data-ttu-id="25b8c-167">Имя предупреждения hello.</span><span class="sxs-lookup"><span data-stu-id="25b8c-167">Name of hello alert.</span></span> |
| <span data-ttu-id="25b8c-168">AlertPriority</span><span class="sxs-lookup"><span data-stu-id="25b8c-168">AlertPriority</span></span> | <span data-ttu-id="25b8c-169">Серьезность предупреждения hello.</span><span class="sxs-lookup"><span data-stu-id="25b8c-169">Severity of hello alert.</span></span><br><br><span data-ttu-id="25b8c-170">не определен</span><span class="sxs-lookup"><span data-stu-id="25b8c-170">not classified</span></span><br><span data-ttu-id="25b8c-171">информационный.</span><span class="sxs-lookup"><span data-stu-id="25b8c-171">information</span></span><br><span data-ttu-id="25b8c-172">Предупреждение</span><span class="sxs-lookup"><span data-stu-id="25b8c-172">warning</span></span><br><span data-ttu-id="25b8c-173">average</span><span class="sxs-lookup"><span data-stu-id="25b8c-173">average</span></span><br><span data-ttu-id="25b8c-174">высокий</span><span class="sxs-lookup"><span data-stu-id="25b8c-174">high</span></span><br><span data-ttu-id="25b8c-175">очень высокий</span><span class="sxs-lookup"><span data-stu-id="25b8c-175">disaster</span></span>  |
| <span data-ttu-id="25b8c-176">AlertState</span><span class="sxs-lookup"><span data-stu-id="25b8c-176">AlertState</span></span> | <span data-ttu-id="25b8c-177">Состояние предупреждения hello.</span><span class="sxs-lookup"><span data-stu-id="25b8c-177">State of hello alert.</span></span><br><br><span data-ttu-id="25b8c-178">0 — состояние — копирование toodate.</span><span class="sxs-lookup"><span data-stu-id="25b8c-178">0 - State is up toodate.</span></span><br><span data-ttu-id="25b8c-179">1 — состояние неизвестно.</span><span class="sxs-lookup"><span data-stu-id="25b8c-179">1 - State is unknown.</span></span>  |
| <span data-ttu-id="25b8c-180">AlertTypeNumber</span><span class="sxs-lookup"><span data-stu-id="25b8c-180">AlertTypeNumber</span></span> | <span data-ttu-id="25b8c-181">Указывает, может ли оповещение создавать несколько событий, связанных с проблемой.</span><span class="sxs-lookup"><span data-stu-id="25b8c-181">Specifies whether alert can generate multiple problem events.</span></span><br><br><span data-ttu-id="25b8c-182">0 — состояние — копирование toodate.</span><span class="sxs-lookup"><span data-stu-id="25b8c-182">0 - State is up toodate.</span></span><br><span data-ttu-id="25b8c-183">1 — состояние неизвестно.</span><span class="sxs-lookup"><span data-stu-id="25b8c-183">1 - State is unknown.</span></span>    |
| <span data-ttu-id="25b8c-184">Комментарии</span><span class="sxs-lookup"><span data-stu-id="25b8c-184">Comments</span></span> | <span data-ttu-id="25b8c-185">Дополнительные комментарии для оповещения.</span><span class="sxs-lookup"><span data-stu-id="25b8c-185">Additional comments for alert.</span></span> |
| <span data-ttu-id="25b8c-186">HostName</span><span class="sxs-lookup"><span data-stu-id="25b8c-186">HostName</span></span> | <span data-ttu-id="25b8c-187">Имя узла hello, создавшего предупреждение hello.</span><span class="sxs-lookup"><span data-stu-id="25b8c-187">Name of hello host that created hello alert.</span></span> |
| <span data-ttu-id="25b8c-188">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="25b8c-188">PriorityNumber</span></span> | <span data-ttu-id="25b8c-189">Значение, указывающее серьезность оповещения hello.</span><span class="sxs-lookup"><span data-stu-id="25b8c-189">Value indicating severity of hello alert.</span></span><br><br><span data-ttu-id="25b8c-190">0 — не определен</span><span class="sxs-lookup"><span data-stu-id="25b8c-190">0 - not classified</span></span><br><span data-ttu-id="25b8c-191">1 — информация</span><span class="sxs-lookup"><span data-stu-id="25b8c-191">1 - information</span></span><br><span data-ttu-id="25b8c-192">2 — предупреждение</span><span class="sxs-lookup"><span data-stu-id="25b8c-192">2 - warning</span></span><br><span data-ttu-id="25b8c-193">3 — средний</span><span class="sxs-lookup"><span data-stu-id="25b8c-193">3 - average</span></span><br><span data-ttu-id="25b8c-194">4 — высокий</span><span class="sxs-lookup"><span data-stu-id="25b8c-194">4 - high</span></span><br><span data-ttu-id="25b8c-195">5 — очень высокий</span><span class="sxs-lookup"><span data-stu-id="25b8c-195">5 - disaster</span></span> |
| <span data-ttu-id="25b8c-196">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="25b8c-196">TimeGenerated</span></span> |<span data-ttu-id="25b8c-197">Создания предупреждения hello даты и времени.</span><span class="sxs-lookup"><span data-stu-id="25b8c-197">Date and time hello alert was created.</span></span> |
| <span data-ttu-id="25b8c-198">TimeLastModified</span><span class="sxs-lookup"><span data-stu-id="25b8c-198">TimeLastModified</span></span> |<span data-ttu-id="25b8c-199">Дата и время hello состояние оповещения hello последнего изменения.</span><span class="sxs-lookup"><span data-stu-id="25b8c-199">Date and time hello state of hello alert was last changed.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="25b8c-200">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="25b8c-200">Next steps</span></span>
* <span data-ttu-id="25b8c-201">Ознакомьтесь с дополнительными сведениями об [оповещениях](log-analytics-alerts.md) в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="25b8c-201">Learn about [alerts](log-analytics-alerts.md) in Log Analytics.</span></span>
* <span data-ttu-id="25b8c-202">Дополнительные сведения о [входа выполняет](log-analytics-log-searches.md) tooanalyze hello данные, собранные из источников данных и решений.</span><span class="sxs-lookup"><span data-stu-id="25b8c-202">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
