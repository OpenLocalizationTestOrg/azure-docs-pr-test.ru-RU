---
title: "aaaCollect данные из CollectD в аналитику журнала OMS | Документы Microsoft"
description: "CollectD — управляющая программа Linux с открытым исходным кодом, которая периодически собирает данные приложений и системные данные.  В этой статье приведены сведения о сборе данных CollectD в OMS Log Analytics."
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
ms.date: 05/02/2017
ms.author: magoedte
ms.openlocfilehash: 7ad82c9c67a664aabd44f08bef2253d84cd2dfba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a><span data-ttu-id="b743a-104">Сбор данных CollectD с помощью агентов Linux в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="b743a-104">Collect data from CollectD on Linux agents in Log Analytics</span></span>
<span data-ttu-id="b743a-105">[CollectD](https://collectd.org/) — управляющая программа Linux с открытым исходным кодом, которая периодически собирает метрики производительности приложений и системные данные.</span><span class="sxs-lookup"><span data-stu-id="b743a-105">[CollectD](https://collectd.org/) is an open source Linux daemon that periodically collects performance metrics from applications and system level information.</span></span> <span data-ttu-id="b743a-106">Пример приложения включают hello виртуальной машины Java (JVM), сервер MySQL и Nginx.</span><span class="sxs-lookup"><span data-stu-id="b743a-106">Example applications include hello Java Virtual Machine (JVM), MySQL Server, and Nginx.</span></span> <span data-ttu-id="b743a-107">В этой статье приводятся сведения о сборе данных производительности CollectD в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="b743a-107">This article provides information on collecting performance data from CollectD in Log Analytics.</span></span>

<span data-ttu-id="b743a-108">Полный список доступных подключаемых модулей можно найти в [таблице подключаемых модулей](https://collectd.org/wiki/index.php/Table_of_Plugins).</span><span class="sxs-lookup"><span data-stu-id="b743a-108">A full list of available plugins can be found at [Table of Plugins](https://collectd.org/wiki/index.php/Table_of_Plugins).</span></span>

![Обзор CollectD](media/log-analytics-data-sources-collectd/overview.png)

<span data-ttu-id="b743a-110">Hello следующая конфигурация CollectD включается в hello агента OMS для Linux tooroute CollectD данные toohello агента OMS для Linux.</span><span class="sxs-lookup"><span data-stu-id="b743a-110">hello following CollectD configuration is included in hello OMS Agent for Linux tooroute  CollectD data toohello OMS Agent for Linux.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

<span data-ttu-id="b743a-111">Кроме того Если с помощью версии collectD, прежде чем 5.5 используется следующая конфигурация вместо hello.</span><span class="sxs-lookup"><span data-stu-id="b743a-111">Additionally, if using an versions of collectD before 5.5 use hello following configuration instead.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

<span data-ttu-id="b743a-112">Hello CollectD конфигурации используется по умолчанию hello`write_http` подключаемый модуль toosend метрики производительности через порт 26000 tooOMS агент для Linux.</span><span class="sxs-lookup"><span data-stu-id="b743a-112">hello CollectD configuration uses hello default`write_http` plugin toosend performance metric data over port 26000 tooOMS Agent for Linux.</span></span> 

> [!NOTE]
> <span data-ttu-id="b743a-113">Это может быть настроенный tooa настраиваемого порт при необходимости.</span><span class="sxs-lookup"><span data-stu-id="b743a-113">This port can be configured tooa custom-defined port if needed.</span></span>

<span data-ttu-id="b743a-114">Hello агента OMS для Linux также прослушивает порт 26000 для CollectD метрик и преобразует их tooOMS схемы метрики.</span><span class="sxs-lookup"><span data-stu-id="b743a-114">hello OMS Agent for Linux also listens on port 26000 for CollectD metrics and then converts them tooOMS schema metrics.</span></span> <span data-ttu-id="b743a-115">Hello Вот hello агента OMS для Linux конфигурации `collectd.conf`.</span><span class="sxs-lookup"><span data-stu-id="b743a-115">hello following is hello OMS Agent for Linux configuration  `collectd.conf`.</span></span>

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a><span data-ttu-id="b743a-116">Поддерживаемые версии</span><span class="sxs-lookup"><span data-stu-id="b743a-116">Versions supported</span></span>
- <span data-ttu-id="b743a-117">Log Analytics сейчас поддерживает CollectD версии 4.8 и более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="b743a-117">Log Analytics currently supports CollectD version 4.8 and above.</span></span>
- <span data-ttu-id="b743a-118">Для сбора метрик CollectD необходим агент OMS для Linux версии 1.1.0-217 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="b743a-118">OMS Agent for Linux v1.1.0-217 or above is required for CollectD metric collection.</span></span>


## <a name="configuration"></a><span data-ttu-id="b743a-119">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="b743a-119">Configuration</span></span>
<span data-ttu-id="b743a-120">Hello ниже приведены основные шаги коллекции tooconfigure CollectD данных в службе анализа журналов.</span><span class="sxs-lookup"><span data-stu-id="b743a-120">hello following are basic steps tooconfigure collection of CollectD data in Log Analytics.</span></span>

1. <span data-ttu-id="b743a-121">Настройка CollectD toosend данные toohello агента OMS для Linux с помощью подключаемого модуля write_http hello.</span><span class="sxs-lookup"><span data-stu-id="b743a-121">Configure CollectD toosend data toohello OMS Agent for Linux using hello write_http plugin.</span></span>  
2. <span data-ttu-id="b743a-122">Настройте hello агента OMS для Linux toolisten для hello CollectD данных на соответствующий порт hello.</span><span class="sxs-lookup"><span data-stu-id="b743a-122">Configure hello OMS Agent for Linux toolisten for hello CollectD data on hello appropriate port.</span></span>
3. <span data-ttu-id="b743a-123">Перезапустите CollectD и агент OMS для Linux.</span><span class="sxs-lookup"><span data-stu-id="b743a-123">Restart CollectD and OMS Agent for Linux.</span></span>

### <a name="configure-collectd-tooforward-data"></a><span data-ttu-id="b743a-124">Настройка данных tooforward CollectD</span><span class="sxs-lookup"><span data-stu-id="b743a-124">Configure CollectD tooforward data</span></span> 

1. <span data-ttu-id="b743a-125">tooroute CollectD данные toohello агента OMS для Linux, `oms.conf` toobe потребностей добавить каталог tooCollectD элемента конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b743a-125">tooroute CollectD data toohello OMS Agent for Linux, `oms.conf` needs toobe added tooCollectD's configuration directory.</span></span> <span data-ttu-id="b743a-126">Hello назначения этого файла зависит от дистрибутив Linux hello вашего компьютера.</span><span class="sxs-lookup"><span data-stu-id="b743a-126">hello destination of this file depends on hello Linux  distro of your machine.</span></span>

    <span data-ttu-id="b743a-127">Если конфигурационные файлы CollectD находятся в папке /etc/collectd.d/:</span><span class="sxs-lookup"><span data-stu-id="b743a-127">If your CollectD config directory is located in /etc/collectd.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    <span data-ttu-id="b743a-128">Если конфигурационные файлы CollectD находятся в папке /etc/collectd/collectd.conf.d/:</span><span class="sxs-lookup"><span data-stu-id="b743a-128">If your CollectD config directory is located in /etc/collectd/collectd.conf.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    ><span data-ttu-id="b743a-129">Для версий CollectD перед 5.5 имеется toomodify hello теги `oms.conf` как показано выше.</span><span class="sxs-lookup"><span data-stu-id="b743a-129">For CollectD versions before 5.5 you will have toomodify hello tags in `oms.conf` as shown above.</span></span>
    >

2. <span data-ttu-id="b743a-130">Скопируйте каталог конфигурации рабочей области toohello требуемого collectd.conf omsagent.</span><span class="sxs-lookup"><span data-stu-id="b743a-130">Copy collectd.conf toohello desired workspace's omsagent configuration directory.</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. <span data-ttu-id="b743a-131">Перезапустите CollectD и агента OMS для Linux с помощью следующих команд hello.</span><span class="sxs-lookup"><span data-stu-id="b743a-131">Restart CollectD and OMS Agent for Linux with hello following commands.</span></span>

    <span data-ttu-id="b743a-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span><span class="sxs-lookup"><span data-stu-id="b743a-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span></span>

## <a name="collectd-metrics-toolog-analytics-schema-conversion"></a><span data-ttu-id="b743a-133">Метрики CollectD tooLog преобразование схемы аналитика</span><span class="sxs-lookup"><span data-stu-id="b743a-133">CollectD metrics tooLog Analytics schema conversion</span></span>
<span data-ttu-id="b743a-134">toomaintain знакомую модель между метрики инфраструктуры уже собранных агентом OMS для Linux и hello новых показателей собранные CollectD hello после сопоставления схемы используется:</span><span class="sxs-lookup"><span data-stu-id="b743a-134">toomaintain a familiar model between infrastructure metrics already collected by OMS Agent for Linux and hello new metrics collected by CollectD hello following schema mapping is used:</span></span>

| <span data-ttu-id="b743a-135">Поле метрики CollectD</span><span class="sxs-lookup"><span data-stu-id="b743a-135">CollectD Metric field</span></span> | <span data-ttu-id="b743a-136">Поле Log Analytics</span><span class="sxs-lookup"><span data-stu-id="b743a-136">Log Analytics field</span></span> |
|:--|:--|
| <span data-ttu-id="b743a-137">host</span><span class="sxs-lookup"><span data-stu-id="b743a-137">host</span></span> | <span data-ttu-id="b743a-138">Компьютер</span><span class="sxs-lookup"><span data-stu-id="b743a-138">Computer</span></span> |
| <span data-ttu-id="b743a-139">plugin</span><span class="sxs-lookup"><span data-stu-id="b743a-139">plugin</span></span> | <span data-ttu-id="b743a-140">None</span><span class="sxs-lookup"><span data-stu-id="b743a-140">None</span></span> |
| <span data-ttu-id="b743a-141">plugin_instance</span><span class="sxs-lookup"><span data-stu-id="b743a-141">plugin_instance</span></span> | <span data-ttu-id="b743a-142">Имя экземпляра</span><span class="sxs-lookup"><span data-stu-id="b743a-142">Instance Name</span></span><br><span data-ttu-id="b743a-143">Если **plugin_instance** имеет значение *null*, то InstanceName="*_Total*"</span><span class="sxs-lookup"><span data-stu-id="b743a-143">If **plugin_instance** is *null* then InstanceName="*_Total*"</span></span> |
| <span data-ttu-id="b743a-144">type</span><span class="sxs-lookup"><span data-stu-id="b743a-144">type</span></span> | <span data-ttu-id="b743a-145">ObjectName</span><span class="sxs-lookup"><span data-stu-id="b743a-145">ObjectName</span></span> |
| <span data-ttu-id="b743a-146">type_instance</span><span class="sxs-lookup"><span data-stu-id="b743a-146">type_instance</span></span> | <span data-ttu-id="b743a-147">CounterName</span><span class="sxs-lookup"><span data-stu-id="b743a-147">CounterName</span></span><br><span data-ttu-id="b743a-148">Если **type_instance** имеет значение *null*, то CounterName=**blank**</span><span class="sxs-lookup"><span data-stu-id="b743a-148">If **type_instance** is *null* then CounterName=**blank**</span></span> |
| <span data-ttu-id="b743a-149">dsnames[]</span><span class="sxs-lookup"><span data-stu-id="b743a-149">dsnames[]</span></span> | <span data-ttu-id="b743a-150">CounterName</span><span class="sxs-lookup"><span data-stu-id="b743a-150">CounterName</span></span> |
| <span data-ttu-id="b743a-151">dstypes</span><span class="sxs-lookup"><span data-stu-id="b743a-151">dstypes</span></span> | <span data-ttu-id="b743a-152">None</span><span class="sxs-lookup"><span data-stu-id="b743a-152">None</span></span> |
| <span data-ttu-id="b743a-153">values[]</span><span class="sxs-lookup"><span data-stu-id="b743a-153">values[]</span></span> | <span data-ttu-id="b743a-154">CounterValue</span><span class="sxs-lookup"><span data-stu-id="b743a-154">CounterValue</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b743a-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b743a-155">Next steps</span></span>
* <span data-ttu-id="b743a-156">Дополнительные сведения о [входа выполняет](log-analytics-log-searches.md) tooanalyze hello данные, собранные из источников данных и решений.</span><span class="sxs-lookup"><span data-stu-id="b743a-156">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
* <span data-ttu-id="b743a-157">Используйте [настраиваемые поля](log-analytics-custom-fields.md) tooparse данных из системного журнала записей в отдельные поля.</span><span class="sxs-lookup"><span data-stu-id="b743a-157">Use [Custom Fields](log-analytics-custom-fields.md) tooparse data from syslog records into individual fields.</span></span>

