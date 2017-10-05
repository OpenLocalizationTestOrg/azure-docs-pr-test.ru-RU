---
title: "Сбор данных CollectD в OMS Log Analytics | Документы Майкрософт"
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
ms.openlocfilehash: a63b15ca5126b45451f0694c9ee75d7b67b1ceaf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a><span data-ttu-id="330cd-104">Сбор данных CollectD с помощью агентов Linux в Log Analytics</span><span class="sxs-lookup"><span data-stu-id="330cd-104">Collect data from CollectD on Linux agents in Log Analytics</span></span>
<span data-ttu-id="330cd-105">[CollectD](https://collectd.org/) — управляющая программа Linux с открытым исходным кодом, которая периодически собирает метрики производительности приложений и системные данные.</span><span class="sxs-lookup"><span data-stu-id="330cd-105">[CollectD](https://collectd.org/) is an open source Linux daemon that periodically collects performance metrics from applications and system level information.</span></span> <span data-ttu-id="330cd-106">К примерам таких приложений относятся виртуальная машина Java (JVM), сервер MySQL и Nginx.</span><span class="sxs-lookup"><span data-stu-id="330cd-106">Example applications include the Java Virtual Machine (JVM), MySQL Server, and Nginx.</span></span> <span data-ttu-id="330cd-107">В этой статье приводятся сведения о сборе данных производительности CollectD в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="330cd-107">This article provides information on collecting performance data from CollectD in Log Analytics.</span></span>

<span data-ttu-id="330cd-108">Полный список доступных подключаемых модулей можно найти в [таблице подключаемых модулей](https://collectd.org/wiki/index.php/Table_of_Plugins).</span><span class="sxs-lookup"><span data-stu-id="330cd-108">A full list of available plugins can be found at [Table of Plugins](https://collectd.org/wiki/index.php/Table_of_Plugins).</span></span>

![Обзор CollectD](media/log-analytics-data-sources-collectd/overview.png)

<span data-ttu-id="330cd-110">В состав агента OMS для Linux включена следующая конфигурация CollectD, которая перенаправляет данные CollectD в агент OMS для Linux.</span><span class="sxs-lookup"><span data-stu-id="330cd-110">The following CollectD configuration is included in the OMS Agent for Linux to route  CollectD data to the OMS Agent for Linux.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

<span data-ttu-id="330cd-111">Если используется CollectD версии 5.5 или более ранней версии, используйте следующую конфигурацию вместо указанной.</span><span class="sxs-lookup"><span data-stu-id="330cd-111">Additionally, if using an versions of collectD before 5.5 use the following configuration instead.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

<span data-ttu-id="330cd-112">В конфигурации CollectD для отправки данных производительности агенту OMS для Linux через порт 26000 по умолчанию используется подключаемый модуль `write_http`.</span><span class="sxs-lookup"><span data-stu-id="330cd-112">The CollectD configuration uses the default`write_http` plugin to send performance metric data over port 26000 to OMS Agent for Linux.</span></span> 

> [!NOTE]
> <span data-ttu-id="330cd-113">При желании номер порта можно изменить.</span><span class="sxs-lookup"><span data-stu-id="330cd-113">This port can be configured to a custom-defined port if needed.</span></span>

<span data-ttu-id="330cd-114">Агент OMS для Linux также прослушивает порт 26000 для сбора метрик CollectD, а затем преобразует эти метрики в метрики схемы OMS.</span><span class="sxs-lookup"><span data-stu-id="330cd-114">The OMS Agent for Linux also listens on port 26000 for CollectD metrics and then converts them to OMS schema metrics.</span></span> <span data-ttu-id="330cd-115">Ниже приведена конфигурация агента OMS для Linux `collectd.conf`.</span><span class="sxs-lookup"><span data-stu-id="330cd-115">The following is the OMS Agent for Linux configuration  `collectd.conf`.</span></span>

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a><span data-ttu-id="330cd-116">Поддерживаемые версии</span><span class="sxs-lookup"><span data-stu-id="330cd-116">Versions supported</span></span>
- <span data-ttu-id="330cd-117">Log Analytics сейчас поддерживает CollectD версии 4.8 и более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="330cd-117">Log Analytics currently supports CollectD version 4.8 and above.</span></span>
- <span data-ttu-id="330cd-118">Для сбора метрик CollectD необходим агент OMS для Linux версии 1.1.0-217 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="330cd-118">OMS Agent for Linux v1.1.0-217 or above is required for CollectD metric collection.</span></span>


## <a name="configuration"></a><span data-ttu-id="330cd-119">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="330cd-119">Configuration</span></span>
<span data-ttu-id="330cd-120">Ниже приведены основные шаги по настройке сбора данных CollectD в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="330cd-120">The following are basic steps to configure collection of CollectD data in Log Analytics.</span></span>

1. <span data-ttu-id="330cd-121">Настройте отправку данных CollectD в агент OMS для Linux с помощью подключаемого модуля write_http.</span><span class="sxs-lookup"><span data-stu-id="330cd-121">Configure CollectD to send data to the OMS Agent for Linux using the write_http plugin.</span></span>  
2. <span data-ttu-id="330cd-122">Настройте агент OMS для Linux для прослушивания данных CollectD на соответствующем порту.</span><span class="sxs-lookup"><span data-stu-id="330cd-122">Configure the OMS Agent for Linux to listen for the CollectD data on the appropriate port.</span></span>
3. <span data-ttu-id="330cd-123">Перезапустите CollectD и агент OMS для Linux.</span><span class="sxs-lookup"><span data-stu-id="330cd-123">Restart CollectD and OMS Agent for Linux.</span></span>

### <a name="configure-collectd-to-forward-data"></a><span data-ttu-id="330cd-124">Настройка пересылки данных в CollectD</span><span class="sxs-lookup"><span data-stu-id="330cd-124">Configure CollectD to forward data</span></span> 

1. <span data-ttu-id="330cd-125">Для пересылки данных CollectD агенту OMS для Linux необходимо добавить файл `oms.conf` в каталог конфигурационных файлов CollectD.</span><span class="sxs-lookup"><span data-stu-id="330cd-125">To route CollectD data to the OMS Agent for Linux, `oms.conf` needs to be added to CollectD's configuration directory.</span></span> <span data-ttu-id="330cd-126">Местоположение этого файла зависит от используемого дистрибутива Linux.</span><span class="sxs-lookup"><span data-stu-id="330cd-126">The destination of this file depends on the Linux  distro of your machine.</span></span>

    <span data-ttu-id="330cd-127">Если конфигурационные файлы CollectD находятся в папке /etc/collectd.d/:</span><span class="sxs-lookup"><span data-stu-id="330cd-127">If your CollectD config directory is located in /etc/collectd.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    <span data-ttu-id="330cd-128">Если конфигурационные файлы CollectD находятся в папке /etc/collectd/collectd.conf.d/:</span><span class="sxs-lookup"><span data-stu-id="330cd-128">If your CollectD config directory is located in /etc/collectd/collectd.conf.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    ><span data-ttu-id="330cd-129">Если используется CollectD версии 5.5 или более ранней версии, потребуется изменить теги в `oms.conf`, как показано выше.</span><span class="sxs-lookup"><span data-stu-id="330cd-129">For CollectD versions before 5.5 you will have to modify the tags in `oms.conf` as shown above.</span></span>
    >

2. <span data-ttu-id="330cd-130">Скопируйте файл collectd.conf в конфигурационный каталог omsagent в соответствующей рабочей области.</span><span class="sxs-lookup"><span data-stu-id="330cd-130">Copy collectd.conf to the desired workspace's omsagent configuration directory.</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. <span data-ttu-id="330cd-131">Перезапустите CollectD и агент OMS для Linux, выполнив следующие команды.</span><span class="sxs-lookup"><span data-stu-id="330cd-131">Restart CollectD and OMS Agent for Linux with the following commands.</span></span>

    <span data-ttu-id="330cd-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span><span class="sxs-lookup"><span data-stu-id="330cd-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span></span>

## <a name="collectd-metrics-to-log-analytics-schema-conversion"></a><span data-ttu-id="330cd-133">Метрики CollectD для преобразования схемы Log Analytics</span><span class="sxs-lookup"><span data-stu-id="330cd-133">CollectD metrics to Log Analytics schema conversion</span></span>
<span data-ttu-id="330cd-134">Для сохранения знакомой модели между метриками инфраструктуры, уже собранными агентом OMS для Linux, и новыми метриками, собранными CollectD, используется следующая схема сопоставления:</span><span class="sxs-lookup"><span data-stu-id="330cd-134">To maintain a familiar model between infrastructure metrics already collected by OMS Agent for Linux and the new metrics collected by CollectD the following schema mapping is used:</span></span>

| <span data-ttu-id="330cd-135">Поле метрики CollectD</span><span class="sxs-lookup"><span data-stu-id="330cd-135">CollectD Metric field</span></span> | <span data-ttu-id="330cd-136">Поле Log Analytics</span><span class="sxs-lookup"><span data-stu-id="330cd-136">Log Analytics field</span></span> |
|:--|:--|
| <span data-ttu-id="330cd-137">host</span><span class="sxs-lookup"><span data-stu-id="330cd-137">host</span></span> | <span data-ttu-id="330cd-138">Компьютер</span><span class="sxs-lookup"><span data-stu-id="330cd-138">Computer</span></span> |
| <span data-ttu-id="330cd-139">plugin</span><span class="sxs-lookup"><span data-stu-id="330cd-139">plugin</span></span> | <span data-ttu-id="330cd-140">None</span><span class="sxs-lookup"><span data-stu-id="330cd-140">None</span></span> |
| <span data-ttu-id="330cd-141">plugin_instance</span><span class="sxs-lookup"><span data-stu-id="330cd-141">plugin_instance</span></span> | <span data-ttu-id="330cd-142">Имя экземпляра</span><span class="sxs-lookup"><span data-stu-id="330cd-142">Instance Name</span></span><br><span data-ttu-id="330cd-143">Если **plugin_instance** имеет значение *null*, то InstanceName="*_Total*"</span><span class="sxs-lookup"><span data-stu-id="330cd-143">If **plugin_instance** is *null* then InstanceName="*_Total*"</span></span> |
| <span data-ttu-id="330cd-144">type</span><span class="sxs-lookup"><span data-stu-id="330cd-144">type</span></span> | <span data-ttu-id="330cd-145">ObjectName</span><span class="sxs-lookup"><span data-stu-id="330cd-145">ObjectName</span></span> |
| <span data-ttu-id="330cd-146">type_instance</span><span class="sxs-lookup"><span data-stu-id="330cd-146">type_instance</span></span> | <span data-ttu-id="330cd-147">CounterName</span><span class="sxs-lookup"><span data-stu-id="330cd-147">CounterName</span></span><br><span data-ttu-id="330cd-148">Если **type_instance** имеет значение *null*, то CounterName=**blank**</span><span class="sxs-lookup"><span data-stu-id="330cd-148">If **type_instance** is *null* then CounterName=**blank**</span></span> |
| <span data-ttu-id="330cd-149">dsnames[]</span><span class="sxs-lookup"><span data-stu-id="330cd-149">dsnames[]</span></span> | <span data-ttu-id="330cd-150">CounterName</span><span class="sxs-lookup"><span data-stu-id="330cd-150">CounterName</span></span> |
| <span data-ttu-id="330cd-151">dstypes</span><span class="sxs-lookup"><span data-stu-id="330cd-151">dstypes</span></span> | <span data-ttu-id="330cd-152">None</span><span class="sxs-lookup"><span data-stu-id="330cd-152">None</span></span> |
| <span data-ttu-id="330cd-153">values[]</span><span class="sxs-lookup"><span data-stu-id="330cd-153">values[]</span></span> | <span data-ttu-id="330cd-154">CounterValue</span><span class="sxs-lookup"><span data-stu-id="330cd-154">CounterValue</span></span> |

## <a name="next-steps"></a><span data-ttu-id="330cd-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="330cd-155">Next steps</span></span>
* <span data-ttu-id="330cd-156">Узнайте больше об [операциях поиска по журналу](log-analytics-log-searches.md) , которые можно применять для анализа данных, собираемых из источников данных и решений.</span><span class="sxs-lookup"><span data-stu-id="330cd-156">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
* <span data-ttu-id="330cd-157">Используйте [настраиваемые поля](log-analytics-custom-fields.md) для анализа данных из записей системного журнала в отдельных полях.</span><span class="sxs-lookup"><span data-stu-id="330cd-157">Use [Custom Fields](log-analytics-custom-fields.md) to parse data from syslog records into individual fields.</span></span>

