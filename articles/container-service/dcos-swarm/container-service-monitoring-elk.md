---
title: "кластер Azure DC/OS - стек ELK aaaMonitor | Документы Microsoft"
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
ms.openlocfilehash: 8d81c5342616ec14880d38803cdf95f5845a669b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-elk"></a><span data-ttu-id="7fa6e-104">Мониторинг кластера службы контейнеров Azure с помощью ELK</span><span class="sxs-lookup"><span data-stu-id="7fa6e-104">Monitor an Azure Container Service cluster with ELK</span></span>
<span data-ttu-id="7fa6e-105">В этой статье показано, как стека toodeploy hello ELK (Elasticsearch Logstash, Kibana) в кластере DC/OS в контейнере службы Azure.</span><span class="sxs-lookup"><span data-stu-id="7fa6e-105">In this article, we demonstrate how toodeploy hello ELK (Elasticsearch, Logstash, Kibana) stack on a DC/OS cluster in Azure Container Service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7fa6e-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7fa6e-106">Prerequisites</span></span>
<span data-ttu-id="7fa6e-107">[Развертывание](container-service-deployment.md) и [подключение](../container-service-connect.md) кластера DC/OS, настроенного службой контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="7fa6e-107">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a DC/OS cluster configured by Azure Container Service.</span></span> <span data-ttu-id="7fa6e-108">Просматривать панели мониторинга hello DC/OS и службы Marathon [здесь](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="7fa6e-108">Explore hello DC/OS dashboard and Marathon services [here](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="7fa6e-109">Также установить hello [балансировки нагрузки Marathon](container-service-load-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="7fa6e-109">Also install hello [Marathon Load Balancer](container-service-load-balancing.md).</span></span>


## <a name="elk-elasticsearch-logstash-kibana"></a><span data-ttu-id="7fa6e-110">ELK (Elasticsearch, Logstash, Kibana)</span><span class="sxs-lookup"><span data-stu-id="7fa6e-110">ELK (Elasticsearch, Logstash, Kibana)</span></span>
<span data-ttu-id="7fa6e-111">Стек ELK представляет собой сочетание Elasticsearch Logstash, и Kibana, предоставляющий tooend конец стека, который можно использовать toomonitor и анализировать журналы в кластере.</span><span class="sxs-lookup"><span data-stu-id="7fa6e-111">ELK stack is a combination of Elasticsearch, Logstash, and Kibana that provides an end tooend stack that can be used toomonitor and analyze logs in your cluster.</span></span>

## <a name="configure-hello-elk-stack-on-a-dcos-cluster"></a><span data-ttu-id="7fa6e-112">Настройка hello ELK стека в кластере DC/OS</span><span class="sxs-lookup"><span data-stu-id="7fa6e-112">Configure hello ELK stack on a DC/OS cluster</span></span>
<span data-ttu-id="7fa6e-113">Доступ к Интерфейсу DC/OS через [http://localhost: 80 /](http://localhost:80/) один раз в hello пользовательского интерфейса DC/OS перейдите слишком**вселенной**.</span><span class="sxs-lookup"><span data-stu-id="7fa6e-113">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in hello DC/OS UI navigate too**Universe**.</span></span> <span data-ttu-id="7fa6e-114">Поиск и установка Elasticsearch, Logstash и Kibana из hello вселенной DC/OS и что-либо порядка перечисления.</span><span class="sxs-lookup"><span data-stu-id="7fa6e-114">Search and install Elasticsearch, Logstash, and Kibana from hello DC/OS Universe and in that specific order.</span></span> <span data-ttu-id="7fa6e-115">Дополнительные сведения о конфигурации в случае перехода toohello **расширенный установки** ссылку.</span><span class="sxs-lookup"><span data-stu-id="7fa6e-115">You can learn more about configuration if you go toohello **Advanced Installation** link.</span></span>

![ELK1](./media/container-service-monitoring-elk/elk1.PNG) ![ELK2](./media/container-service-monitoring-elk/elk2.PNG) ![ELK3](./media/container-service-monitoring-elk/elk3.PNG) 

<span data-ttu-id="7fa6e-119">Один раз Здравствуйте ELK контейнеры и являются запуска, необходимо получить с помощью балансировки Нагрузки Marathon toobe Kibana tooenable.</span><span class="sxs-lookup"><span data-stu-id="7fa6e-119">Once hello ELK containers and are up and running, you need tooenable Kibana toobe accessed through Marathon-LB.</span></span> <span data-ttu-id="7fa6e-120">Перейдите в слишком **службы** > **kibana**и нажмите кнопку **изменить** как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="7fa6e-120">Navigate too **Services** > **kibana**, and click **Edit** as shown below.</span></span>

![ELK4](./media/container-service-monitoring-elk/elk4.PNG)


<span data-ttu-id="7fa6e-122">Переключение слишком**режим JSON** и найдите раздел toohello метки.</span><span class="sxs-lookup"><span data-stu-id="7fa6e-122">Toggle too**JSON mode** and scroll down toohello labels section.</span></span>
<span data-ttu-id="7fa6e-123">Требуется tooadd `"HAPROXY_GROUP": "external"` здесь запись как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="7fa6e-123">You need tooadd a `"HAPROXY_GROUP": "external"` entry here as shown below.</span></span>
<span data-ttu-id="7fa6e-124">После нажатия кнопки **Deploy changes** (Развернуть изменения) контейнер будет перезагружен.</span><span class="sxs-lookup"><span data-stu-id="7fa6e-124">Once you click **Deploy changes**, your container restarts.</span></span>

![ELK5](./media/container-service-monitoring-elk/elk5.PNG)


<span data-ttu-id="7fa6e-126">Если вы хотите tooverify, Kibana зарегистрирован в качестве службы на панели мониторинга HAPROXY hello, требуется порт tooopen 9090 в кластере агент hello как HAPROXY использует порт 9090.</span><span class="sxs-lookup"><span data-stu-id="7fa6e-126">If you want tooverify that Kibana is registered as a service in hello HAPROXY dashboard, you need tooopen port 9090 on hello agent cluster as HAPROXY runs on port 9090.</span></span>
<span data-ttu-id="7fa6e-127">По умолчанию мы открывать порты 80, 8080 и 443 в hello DC/OS агента кластера.</span><span class="sxs-lookup"><span data-stu-id="7fa6e-127">By default, we open ports 80, 8080, and 443 in hello DC/OS agent cluster.</span></span>
<span data-ttu-id="7fa6e-128">Инструкции tooopen порт и предоставить открытый оценки предоставляются [здесь](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="7fa6e-128">Instructions tooopen a port and provide public assess are provided [here](container-service-enable-public-access.md).</span></span>

<span data-ttu-id="7fa6e-129">Здравствуйте, tooaccess HAPROXY панели мониторинга, откройте hello балансировки Нагрузки Marathon интерфейса администратора на: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span><span class="sxs-lookup"><span data-stu-id="7fa6e-129">tooaccess hello HAPROXY dashboard, open hello Marathon-LB admin interface at: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span></span>
<span data-ttu-id="7fa6e-130">После перейти toohello URL-адрес, вы увидите панель мониторинга HAPROXY hello, как показано ниже, и вы увидите записи службы для Kibana.</span><span class="sxs-lookup"><span data-stu-id="7fa6e-130">Once you navigate toohello URL, you should see hello HAPROXY dashboard as shown below and you should see a service entry for Kibana.</span></span>

![ELK6](./media/container-service-monitoring-elk/elk6.PNG)


<span data-ttu-id="7fa6e-132">панель Kibana hello tooaccess, в которой развертывается на порт 5601, требуется порт tooopen 5601.</span><span class="sxs-lookup"><span data-stu-id="7fa6e-132">tooaccess hello Kibana dashboard, which is deployed on port 5601, you need tooopen port 5601.</span></span> <span data-ttu-id="7fa6e-133">Инструкции см. [здесь](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="7fa6e-133">Follow instructions [here](container-service-enable-public-access.md).</span></span> <span data-ttu-id="7fa6e-134">Откройте панель мониторинга Kibana hello в: `http://localhost:5601`.</span><span class="sxs-lookup"><span data-stu-id="7fa6e-134">Then open hello Kibana dashboard at: `http://localhost:5601`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fa6e-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7fa6e-135">Next steps</span></span>

* <span data-ttu-id="7fa6e-136">Чтобы узнать о пересылке и настройке системного журнала и журнала приложений, изучите раздел [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/) (Управление журналами в DC/OS с помощью ELK).</span><span class="sxs-lookup"><span data-stu-id="7fa6e-136">For system and application log forwarding and setup, see [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/).</span></span>

* <span data-ttu-id="7fa6e-137">см. журналы toofilter [фильтрации журналов с помощью ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span><span class="sxs-lookup"><span data-stu-id="7fa6e-137">toofilter logs, see [Filtering Logs with ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span></span> 

 

