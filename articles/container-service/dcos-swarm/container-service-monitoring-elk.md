---
title: "Мониторинг кластера DC/OS Azure с помощью стека ELK | Документация Майкрософт"
description: "Мониторинг кластера DC/OS в кластере службы контейнеров Azure с помощью ELK (Elasticsearch, Logstash и Kibana)."
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Контейнеры, DC/OS, Azure, мониторинг, elk"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: fcfa277cdd0f3cebc0fbbb23e771fb23ffbe2ca6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-elk"></a><span data-ttu-id="4f40e-104">Мониторинг кластера службы контейнеров Azure с помощью ELK</span><span class="sxs-lookup"><span data-stu-id="4f40e-104">Monitor an Azure Container Service cluster with ELK</span></span>
<span data-ttu-id="4f40e-105">В этой статье показано, как развертывать стек ELK (Elasticsearch, Logstash, Kibana) в кластере DC/OS в службе контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="4f40e-105">In this article, we demonstrate how to deploy the ELK (Elasticsearch, Logstash, Kibana) stack on a DC/OS cluster in Azure Container Service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4f40e-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4f40e-106">Prerequisites</span></span>
<span data-ttu-id="4f40e-107">[Развертывание](container-service-deployment.md) и [подключение](../container-service-connect.md) кластера DC/OS, настроенного службой контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="4f40e-107">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a DC/OS cluster configured by Azure Container Service.</span></span> <span data-ttu-id="4f40e-108">Ознакомьтесь с панелью мониторинга DC/OS и службами Marathon [здесь](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="4f40e-108">Explore the DC/OS dashboard and Marathon services [here](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="4f40e-109">Кроме того, установите [Балансировщик нагрузки Marathon](container-service-load-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="4f40e-109">Also install the [Marathon Load Balancer](container-service-load-balancing.md).</span></span>


## <a name="elk-elasticsearch-logstash-kibana"></a><span data-ttu-id="4f40e-110">ELK (Elasticsearch, Logstash, Kibana)</span><span class="sxs-lookup"><span data-stu-id="4f40e-110">ELK (Elasticsearch, Logstash, Kibana)</span></span>
<span data-ttu-id="4f40e-111">Стек ELK представляет собой сочетание Elasticsearch, Logstash и Kibana, которые формируют комплекс средств, используемых для отслеживания и анализа журналов в кластере.</span><span class="sxs-lookup"><span data-stu-id="4f40e-111">ELK stack is a combination of Elasticsearch, Logstash, and Kibana that provides an end to end stack that can be used to monitor and analyze logs in your cluster.</span></span>

## <a name="configure-the-elk-stack-on-a-dcos-cluster"></a><span data-ttu-id="4f40e-112">Настройка стека ELK в кластере DC/OS</span><span class="sxs-lookup"><span data-stu-id="4f40e-112">Configure the ELK stack on a DC/OS cluster</span></span>
<span data-ttu-id="4f40e-113">Перейдите к пользовательскому интерфейсу DC/OS по адресу [http://localhost:80/](http://localhost:80/). Затем в пользовательском интерфейсе DC/OS перейдите в раздел **Universe**.</span><span class="sxs-lookup"><span data-stu-id="4f40e-113">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in the DC/OS UI navigate to **Universe**.</span></span> <span data-ttu-id="4f40e-114">Найдите и установите Elasticsearch, Logstash и Kibana из DC/OS Universe именно в этом порядке.</span><span class="sxs-lookup"><span data-stu-id="4f40e-114">Search and install Elasticsearch, Logstash, and Kibana from the DC/OS Universe and in that specific order.</span></span> <span data-ttu-id="4f40e-115">Дополнительные сведения о конфигурации см. разделе **Advanced Installation** (Дополнительные параметры установки).</span><span class="sxs-lookup"><span data-stu-id="4f40e-115">You can learn more about configuration if you go to the **Advanced Installation** link.</span></span>

![ELK1](./media/container-service-monitoring-elk/elk1.PNG) ![ELK2](./media/container-service-monitoring-elk/elk2.PNG) ![ELK3](./media/container-service-monitoring-elk/elk3.PNG) 

<span data-ttu-id="4f40e-119">После того как контейнеры ELK заработают, необходимо разрешить в Kibana доступ с помощью Marathon-LB.</span><span class="sxs-lookup"><span data-stu-id="4f40e-119">Once the ELK containers and are up and running, you need to enable Kibana to be accessed through Marathon-LB.</span></span> <span data-ttu-id="4f40e-120">Перейдите в раздел **Службы** > **kibana** и нажмите кнопку **Изменить**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="4f40e-120">Navigate to **Services** > **kibana**, and click **Edit** as shown below.</span></span>

![ELK4](./media/container-service-monitoring-elk/elk4.PNG)


<span data-ttu-id="4f40e-122">Переключитесь в **режим JSON** и перейдите ниже к разделу меток.</span><span class="sxs-lookup"><span data-stu-id="4f40e-122">Toggle to **JSON mode** and scroll down to the labels section.</span></span>
<span data-ttu-id="4f40e-123">Необходимо добавить запись `"HAPROXY_GROUP": "external"`, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="4f40e-123">You need to add a `"HAPROXY_GROUP": "external"` entry here as shown below.</span></span>
<span data-ttu-id="4f40e-124">После нажатия кнопки **Deploy changes** (Развернуть изменения) контейнер будет перезагружен.</span><span class="sxs-lookup"><span data-stu-id="4f40e-124">Once you click **Deploy changes**, your container restarts.</span></span>

![ELK5](./media/container-service-monitoring-elk/elk5.PNG)


<span data-ttu-id="4f40e-126">Чтобы проверить, что Kibana зарегистрирован как служба в панели мониторинга HAPROXY, в кластере агента необходимо открыть порт 9090, поскольку в HAPROXY используется порт 9090.</span><span class="sxs-lookup"><span data-stu-id="4f40e-126">If you want to verify that Kibana is registered as a service in the HAPROXY dashboard, you need to open port 9090 on the agent cluster as HAPROXY runs on port 9090.</span></span>
<span data-ttu-id="4f40e-127">По умолчанию в кластере агента DC/OS открыть порты 80, 8080 и 443.</span><span class="sxs-lookup"><span data-stu-id="4f40e-127">By default, we open ports 80, 8080, and 443 in the DC/OS agent cluster.</span></span>
<span data-ttu-id="4f40e-128">Инструкции по открытию портов и предоставлению открытого доступа см. [здесь](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="4f40e-128">Instructions to open a port and provide public assess are provided [here](container-service-enable-public-access.md).</span></span>

<span data-ttu-id="4f40e-129">Для доступа к панели мониторинга HAPROXY откройте интерфейс администрирования Marathon-LB по такому адресу: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span><span class="sxs-lookup"><span data-stu-id="4f40e-129">To access the HAPROXY dashboard, open the Marathon-LB admin interface at: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span></span>
<span data-ttu-id="4f40e-130">После перехода по этому URL-адресу вы увидите, как показано ниже, панель мониторинга HAPROXY и запись службы для Kibana.</span><span class="sxs-lookup"><span data-stu-id="4f40e-130">Once you navigate to the URL, you should see the HAPROXY dashboard as shown below and you should see a service entry for Kibana.</span></span>

![ELK6](./media/container-service-monitoring-elk/elk6.PNG)


<span data-ttu-id="4f40e-132">Чтобы получить доступ к панели мониторинга Kibana, которая развернута на порту 5601, необходимо открыть порт 5601.</span><span class="sxs-lookup"><span data-stu-id="4f40e-132">To access the Kibana dashboard, which is deployed on port 5601, you need to open port 5601.</span></span> <span data-ttu-id="4f40e-133">Инструкции см. [здесь](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="4f40e-133">Follow instructions [here](container-service-enable-public-access.md).</span></span> <span data-ttu-id="4f40e-134">Затем откройте панель мониторинга Kibana по этому адресу: `http://localhost:5601`.</span><span class="sxs-lookup"><span data-stu-id="4f40e-134">Then open the Kibana dashboard at: `http://localhost:5601`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f40e-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4f40e-135">Next steps</span></span>

* <span data-ttu-id="4f40e-136">Чтобы узнать о пересылке и настройке системного журнала и журнала приложений, изучите раздел [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/) (Управление журналами в DC/OS с помощью ELK).</span><span class="sxs-lookup"><span data-stu-id="4f40e-136">For system and application log forwarding and setup, see [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/).</span></span>

* <span data-ttu-id="4f40e-137">Чтобы узнать о фильтрации журналов, ознакомьтесь с разделом [Filtering Logs with ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/) (Фильтрация журналов с помощью ELK).</span><span class="sxs-lookup"><span data-stu-id="4f40e-137">To filter logs, see [Filtering Logs with ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span></span> 

 

