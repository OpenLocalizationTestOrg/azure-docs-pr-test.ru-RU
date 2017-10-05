---
title: "Сбор оповещений Nagios и Zabbix в OMS Log Analytics | Документы Майкрософт"
description: "Nagios и Zabbix — средства мониторинга с открытым исходным кодом. Оповещения от этих средств мониторинга можно собирать в Log Analytics для анализа вместе с оповещениями из других источников.  В этой статье описано, как настроить сбор оповещений из этих средств в агенте OMS для Linux."
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
ms.openlocfilehash: 0b64c32e1031e704d50aab0b38eaea41e27d134b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a><span data-ttu-id="8b074-105">Сбор оповещений Nagios и Zabbix из агента OMS для Linux в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="8b074-105">Collect alerts from Nagios and Zabbix in Log Analytics from OMS Agent for Linux</span></span> 
<span data-ttu-id="8b074-106">[Nagios](https://www.nagios.org/) и [Zabbix](http://www.zabbix.com/) — средства мониторинга с открытым исходным кодом.</span><span class="sxs-lookup"><span data-stu-id="8b074-106">[Nagios](https://www.nagios.org/) and [Zabbix](http://www.zabbix.com/) are open source monitoring tools.</span></span>  <span data-ttu-id="8b074-107">Оповещения от этих средств мониторинга можно собирать в Log Analytics для анализа вместе с [оповещениями из других источников](log-analytics-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="8b074-107">You can collect alerts from these tools into Log Analytics in order to analyze them along with [alerts from other sources](log-analytics-alerts.md).</span></span>  <span data-ttu-id="8b074-108">В этой статье описано, как настроить сбор оповещений из этих средств в агенте OMS для Linux.</span><span class="sxs-lookup"><span data-stu-id="8b074-108">This article describes how to configure the OMS Agent for Linux to collect alerts from these systems.</span></span>
 
## <a name="configure-alert-collection"></a><span data-ttu-id="8b074-109">Настройка сбора оповещений</span><span class="sxs-lookup"><span data-stu-id="8b074-109">Configure alert collection</span></span>

### <a name="configuring-nagios-alert-collection"></a><span data-ttu-id="8b074-110">Настройка сбора оповещений Nagios</span><span class="sxs-lookup"><span data-stu-id="8b074-110">Configuring Nagios alert collection</span></span>
<span data-ttu-id="8b074-111">Для настройки сбора оповещений на сервере Nagios выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8b074-111">Perform the following steps on the Nagios server to collect alerts.</span></span>

1. <span data-ttu-id="8b074-112">Предоставьте пользователю **omsagent** разрешение на чтение для файла журнала Nagios (`/var/log/nagios/nagios.log`).</span><span class="sxs-lookup"><span data-stu-id="8b074-112">Grant the user **omsagent** read access to the Nagios log file (i.e. `/var/log/nagios/nagios.log`).</span></span> <span data-ttu-id="8b074-113">Если файл nagios.log принадлежит группе `nagios`, можно добавить пользователя **omsagent** в группу **nagios**.</span><span class="sxs-lookup"><span data-stu-id="8b074-113">Assuming the nagios.log file is owned by the group `nagios`, you can add the user **omsagent** to the **nagios** group.</span></span> 

    <span data-ttu-id="8b074-114">sudo usermod -a -G nagios omsagent</span><span class="sxs-lookup"><span data-stu-id="8b074-114">sudo usermod -a -G nagios omsagent</span></span>

2.  <span data-ttu-id="8b074-115">Измените файл конфигурации (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="8b074-115">Modify the configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="8b074-116">Для этого введите следующие записи в незакомментированном виде:</span><span class="sxs-lookup"><span data-stu-id="8b074-116">Ensure the following entries are present and not commented out:</span></span>  

        <source>  
          type tail  
          #Update path to point to your nagios.log  
          path /var/log/nagios/nagios.log  
          format none  
          tag oms.nagios  
        </source>  
      
        <filter oms.nagios>  
          type filter_nagios_log  
        </filter>  

3. <span data-ttu-id="8b074-117">Перезапустите управляющую программу omsagent</span><span class="sxs-lookup"><span data-stu-id="8b074-117">Restart the omsagent daemon</span></span>

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a><span data-ttu-id="8b074-118">Настройка сбора оповещений Zabbix</span><span class="sxs-lookup"><span data-stu-id="8b074-118">Configuring Zabbix alert collection</span></span>
<span data-ttu-id="8b074-119">Для сбора оповещений сервера Zabbix необходимо указать имя пользователя и пароль в формате *открытого текста*.</span><span class="sxs-lookup"><span data-stu-id="8b074-119">To collect alerts from a Zabbix server, you need to specify a user and password in *clear text*.</span></span> <span data-ttu-id="8b074-120">Это не идеальное решение, но мы рекомендуем создать отдельного пользователя и предоставить ему разрешения только для мониторинга.</span><span class="sxs-lookup"><span data-stu-id="8b074-120">This is not ideal, but we recommend that you create the user and grant permissions to monitor onlu.</span></span>

<span data-ttu-id="8b074-121">Для настройки сбора оповещений на сервере Nagios выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8b074-121">Perform the following steps on the Nagios server to collect alerts.</span></span>

1. <span data-ttu-id="8b074-122">Измените файл конфигурации (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="8b074-122">Modify the configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="8b074-123">Убедитесь, что в файле есть следующие параметры и что они не закомментированы.</span><span class="sxs-lookup"><span data-stu-id="8b074-123">Ensure the following entries are present and not commented out.</span></span>  <span data-ttu-id="8b074-124">Измените имя пользователя и пароль на соответствующие значения для вашей среды Zabbix.</span><span class="sxs-lookup"><span data-stu-id="8b074-124">Change the user name and password to values for your Zabbix environment.</span></span>

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. <span data-ttu-id="8b074-125">Перезапустите управляющую программу omsagent</span><span class="sxs-lookup"><span data-stu-id="8b074-125">Restart the omsagent daemon</span></span>

    <span data-ttu-id="8b074-126">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span><span class="sxs-lookup"><span data-stu-id="8b074-126">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span></span>


## <a name="alert-records"></a><span data-ttu-id="8b074-127">Записи оповещений</span><span class="sxs-lookup"><span data-stu-id="8b074-127">Alert records</span></span>
<span data-ttu-id="8b074-128">Записи оповещений из Nagios и Zabbix можно получить с помощью [поиска по журналам](log-analytics-log-searches.md) в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="8b074-128">You can retrieve alert records from Nagios and Zabbix using [log searches](log-analytics-log-searches.md) in Log Analytics.</span></span>

### <a name="nagios-alert-records"></a><span data-ttu-id="8b074-129">Записи оповещений Nagios</span><span class="sxs-lookup"><span data-stu-id="8b074-129">Nagios Alert records</span></span>

<span data-ttu-id="8b074-130">Для записей оповещений Nagios параметр **Type** (тип) имеет значение **Alert** (оповещение), а параметр **SourceSystem** (источник) — значение **Nagios**.</span><span class="sxs-lookup"><span data-stu-id="8b074-130">Alert records collected by Nagios have a **Type** of **Alert** and a **SourceSystem** of **Nagios**.</span></span>  <span data-ttu-id="8b074-131">У них есть свойства, приведенные в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="8b074-131">They have the properties in the following table.</span></span>

| <span data-ttu-id="8b074-132">Свойство</span><span class="sxs-lookup"><span data-stu-id="8b074-132">Property</span></span> | <span data-ttu-id="8b074-133">Описание</span><span class="sxs-lookup"><span data-stu-id="8b074-133">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="8b074-134">Тип</span><span class="sxs-lookup"><span data-stu-id="8b074-134">Type</span></span> |<span data-ttu-id="8b074-135">*Предупреждение*</span><span class="sxs-lookup"><span data-stu-id="8b074-135">*Alert*</span></span> |
| <span data-ttu-id="8b074-136">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="8b074-136">SourceSystem</span></span> |<span data-ttu-id="8b074-137">*Nagios*</span><span class="sxs-lookup"><span data-stu-id="8b074-137">*Nagios*</span></span> |
| <span data-ttu-id="8b074-138">AlertName</span><span class="sxs-lookup"><span data-stu-id="8b074-138">AlertName</span></span> |<span data-ttu-id="8b074-139">Имя оповещения.</span><span class="sxs-lookup"><span data-stu-id="8b074-139">Name of the alert.</span></span> |
| <span data-ttu-id="8b074-140">AlertDescription</span><span class="sxs-lookup"><span data-stu-id="8b074-140">AlertDescription</span></span> | <span data-ttu-id="8b074-141">Описание оповещения.</span><span class="sxs-lookup"><span data-stu-id="8b074-141">Description of the alert.</span></span> |
| <span data-ttu-id="8b074-142">AlertState</span><span class="sxs-lookup"><span data-stu-id="8b074-142">AlertState</span></span> | <span data-ttu-id="8b074-143">Состояние службы или узла.</span><span class="sxs-lookup"><span data-stu-id="8b074-143">Status of the service or host.</span></span><br><br><span data-ttu-id="8b074-144">ОК</span><span class="sxs-lookup"><span data-stu-id="8b074-144">OK</span></span><br><span data-ttu-id="8b074-145">ПРЕДУПРЕЖДЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="8b074-145">WARNING</span></span><br><span data-ttu-id="8b074-146">РАБОТАЕТ</span><span class="sxs-lookup"><span data-stu-id="8b074-146">UP</span></span><br><span data-ttu-id="8b074-147">СБОЙ</span><span class="sxs-lookup"><span data-stu-id="8b074-147">DOWN</span></span> |
| <span data-ttu-id="8b074-148">HostName</span><span class="sxs-lookup"><span data-stu-id="8b074-148">HostName</span></span> | <span data-ttu-id="8b074-149">Имя узла, который создал оповещение.</span><span class="sxs-lookup"><span data-stu-id="8b074-149">Name of the host that created the alert.</span></span> |
| <span data-ttu-id="8b074-150">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="8b074-150">PriorityNumber</span></span> | <span data-ttu-id="8b074-151">Приоритет оповещения.</span><span class="sxs-lookup"><span data-stu-id="8b074-151">Priority level of the alert.</span></span> |
| <span data-ttu-id="8b074-152">StateType</span><span class="sxs-lookup"><span data-stu-id="8b074-152">StateType</span></span> | <span data-ttu-id="8b074-153">Тип состояния оповещения.</span><span class="sxs-lookup"><span data-stu-id="8b074-153">The type of state of the alert.</span></span><br><br><span data-ttu-id="8b074-154">SOFT — проблема, которая не проверялась повторно.</span><span class="sxs-lookup"><span data-stu-id="8b074-154">SOFT - Issue that has not been rechecked.</span></span><br><span data-ttu-id="8b074-155">HARD — проблема, которая проверялась повторно заданное число раз.</span><span class="sxs-lookup"><span data-stu-id="8b074-155">HARD - Issue that has been rechecked a specified number of times.</span></span>  |
| <span data-ttu-id="8b074-156">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="8b074-156">TimeGenerated</span></span> |<span data-ttu-id="8b074-157">Дата и время создания оповещения.</span><span class="sxs-lookup"><span data-stu-id="8b074-157">Date and time the alert was created.</span></span> |


### <a name="zabbix-alert-records"></a><span data-ttu-id="8b074-158">Записи оповещений Zabbix</span><span class="sxs-lookup"><span data-stu-id="8b074-158">Zabbix alert records</span></span>
<span data-ttu-id="8b074-159">Для записей оповещений Nagios параметр **Type** (тип) имеет значение **Alert** (оповещение), а параметр **SourceSystem** (источник) — значение **Zabbix**.</span><span class="sxs-lookup"><span data-stu-id="8b074-159">Alert records collected by Zabbix have a **Type** of **Alert** and a **SourceSystem** of **Zabbix**.</span></span>  <span data-ttu-id="8b074-160">У них есть свойства, приведенные в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="8b074-160">They have the properties in the following table.</span></span>

| <span data-ttu-id="8b074-161">Свойство</span><span class="sxs-lookup"><span data-stu-id="8b074-161">Property</span></span> | <span data-ttu-id="8b074-162">Описание</span><span class="sxs-lookup"><span data-stu-id="8b074-162">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="8b074-163">Тип</span><span class="sxs-lookup"><span data-stu-id="8b074-163">Type</span></span> |<span data-ttu-id="8b074-164">*Предупреждение*</span><span class="sxs-lookup"><span data-stu-id="8b074-164">*Alert*</span></span> |
| <span data-ttu-id="8b074-165">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="8b074-165">SourceSystem</span></span> |<span data-ttu-id="8b074-166">*Zabbix*</span><span class="sxs-lookup"><span data-stu-id="8b074-166">*Zabbix*</span></span> |
| <span data-ttu-id="8b074-167">AlertName</span><span class="sxs-lookup"><span data-stu-id="8b074-167">AlertName</span></span> | <span data-ttu-id="8b074-168">Имя оповещения.</span><span class="sxs-lookup"><span data-stu-id="8b074-168">Name of the alert.</span></span> |
| <span data-ttu-id="8b074-169">AlertPriority</span><span class="sxs-lookup"><span data-stu-id="8b074-169">AlertPriority</span></span> | <span data-ttu-id="8b074-170">Серьезность оповещения.</span><span class="sxs-lookup"><span data-stu-id="8b074-170">Severity of the alert.</span></span><br><br><span data-ttu-id="8b074-171">не определен</span><span class="sxs-lookup"><span data-stu-id="8b074-171">not classified</span></span><br><span data-ttu-id="8b074-172">информационный.</span><span class="sxs-lookup"><span data-stu-id="8b074-172">information</span></span><br><span data-ttu-id="8b074-173">Предупреждение</span><span class="sxs-lookup"><span data-stu-id="8b074-173">warning</span></span><br><span data-ttu-id="8b074-174">average</span><span class="sxs-lookup"><span data-stu-id="8b074-174">average</span></span><br><span data-ttu-id="8b074-175">высокий</span><span class="sxs-lookup"><span data-stu-id="8b074-175">high</span></span><br><span data-ttu-id="8b074-176">очень высокий</span><span class="sxs-lookup"><span data-stu-id="8b074-176">disaster</span></span>  |
| <span data-ttu-id="8b074-177">AlertState</span><span class="sxs-lookup"><span data-stu-id="8b074-177">AlertState</span></span> | <span data-ttu-id="8b074-178">Состояние оповещения.</span><span class="sxs-lookup"><span data-stu-id="8b074-178">State of the alert.</span></span><br><br><span data-ttu-id="8b074-179">0 — актуальное состояние.</span><span class="sxs-lookup"><span data-stu-id="8b074-179">0 - State is up to date.</span></span><br><span data-ttu-id="8b074-180">1 — состояние неизвестно.</span><span class="sxs-lookup"><span data-stu-id="8b074-180">1 - State is unknown.</span></span>  |
| <span data-ttu-id="8b074-181">AlertTypeNumber</span><span class="sxs-lookup"><span data-stu-id="8b074-181">AlertTypeNumber</span></span> | <span data-ttu-id="8b074-182">Указывает, может ли оповещение создавать несколько событий, связанных с проблемой.</span><span class="sxs-lookup"><span data-stu-id="8b074-182">Specifies whether alert can generate multiple problem events.</span></span><br><br><span data-ttu-id="8b074-183">0 — актуальное состояние.</span><span class="sxs-lookup"><span data-stu-id="8b074-183">0 - State is up to date.</span></span><br><span data-ttu-id="8b074-184">1 — состояние неизвестно.</span><span class="sxs-lookup"><span data-stu-id="8b074-184">1 - State is unknown.</span></span>    |
| <span data-ttu-id="8b074-185">Комментарии</span><span class="sxs-lookup"><span data-stu-id="8b074-185">Comments</span></span> | <span data-ttu-id="8b074-186">Дополнительные комментарии для оповещения.</span><span class="sxs-lookup"><span data-stu-id="8b074-186">Additional comments for alert.</span></span> |
| <span data-ttu-id="8b074-187">HostName</span><span class="sxs-lookup"><span data-stu-id="8b074-187">HostName</span></span> | <span data-ttu-id="8b074-188">Имя узла, который создал оповещение.</span><span class="sxs-lookup"><span data-stu-id="8b074-188">Name of the host that created the alert.</span></span> |
| <span data-ttu-id="8b074-189">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="8b074-189">PriorityNumber</span></span> | <span data-ttu-id="8b074-190">Значение, указывающее уровень серьезности оповещения.</span><span class="sxs-lookup"><span data-stu-id="8b074-190">Value indicating severity of the alert.</span></span><br><br><span data-ttu-id="8b074-191">0 — не определен</span><span class="sxs-lookup"><span data-stu-id="8b074-191">0 - not classified</span></span><br><span data-ttu-id="8b074-192">1 — информация</span><span class="sxs-lookup"><span data-stu-id="8b074-192">1 - information</span></span><br><span data-ttu-id="8b074-193">2 — предупреждение</span><span class="sxs-lookup"><span data-stu-id="8b074-193">2 - warning</span></span><br><span data-ttu-id="8b074-194">3 — средний</span><span class="sxs-lookup"><span data-stu-id="8b074-194">3 - average</span></span><br><span data-ttu-id="8b074-195">4 — высокий</span><span class="sxs-lookup"><span data-stu-id="8b074-195">4 - high</span></span><br><span data-ttu-id="8b074-196">5 — очень высокий</span><span class="sxs-lookup"><span data-stu-id="8b074-196">5 - disaster</span></span> |
| <span data-ttu-id="8b074-197">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="8b074-197">TimeGenerated</span></span> |<span data-ttu-id="8b074-198">Дата и время создания оповещения.</span><span class="sxs-lookup"><span data-stu-id="8b074-198">Date and time the alert was created.</span></span> |
| <span data-ttu-id="8b074-199">TimeLastModified</span><span class="sxs-lookup"><span data-stu-id="8b074-199">TimeLastModified</span></span> |<span data-ttu-id="8b074-200">Дата и время последнего изменения состояния оповещения.</span><span class="sxs-lookup"><span data-stu-id="8b074-200">Date and time the state of the alert was last changed.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="8b074-201">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8b074-201">Next steps</span></span>
* <span data-ttu-id="8b074-202">Ознакомьтесь с дополнительными сведениями об [оповещениях](log-analytics-alerts.md) в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="8b074-202">Learn about [alerts](log-analytics-alerts.md) in Log Analytics.</span></span>
* <span data-ttu-id="8b074-203">Узнайте больше об [операциях поиска по журналу](log-analytics-log-searches.md) , которые можно применять для анализа данных, собираемых из источников данных и решений.</span><span class="sxs-lookup"><span data-stu-id="8b074-203">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
