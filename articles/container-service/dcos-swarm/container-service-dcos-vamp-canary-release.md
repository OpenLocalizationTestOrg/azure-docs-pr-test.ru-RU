---
title: "Ранний выпуск с помощью Vamp в кластере DC/OS Azure | Документация Майкрософт"
description: "Узнайте, как использовать Vamp для раннего выпуска служб и применения интеллектуальной фильтрации трафика в кластере DC/OS Службы контейнеров Azure."
services: container-service
author: gggina
manager: rasquill
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/17/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: 4a20091b59f2643ea71cce99c159a5075706e35d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="canary-release-microservices-with-vamp-on-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="e77f4-103">Ранний выпуск микрослужб с помощью Vamp в кластере DC/OS Службы контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="e77f4-103">Canary release microservices with Vamp on an Azure Container Service DC/OS cluster</span></span>

<span data-ttu-id="e77f4-104">В этом пошаговом руководстве мы настраиваем Vamp в Службе контейнеров Azure, используя кластер DC/OS.</span><span class="sxs-lookup"><span data-stu-id="e77f4-104">In this walkthrough, we set up Vamp on Azure Container Service with a DC/OS cluster.</span></span> <span data-ttu-id="e77f4-105">Мы создаем ранний выпуск демоверсии службы Vamp "sava", а затем устраняем несовместимость этой службы с Firefox, применив интеллектуальную фильтрацию трафика.</span><span class="sxs-lookup"><span data-stu-id="e77f4-105">We canary release the Vamp demo service "sava", and then resolve an incompatibility of the service with Firefox by applying smart traffic filtering.</span></span> 

> [!TIP] 
> <span data-ttu-id="e77f4-106">В этом пошаговом руководстве Vamp выполняется в кластере DC/OS, но в качестве оркестратора для Vamp также можно использовать Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="e77f4-106">In this walkthrough Vamp runs on a DC/OS cluster, but you can also use Vamp with Kubernetes as the orchestrator.</span></span>
>

## <a name="about-canary-releases-and-vamp"></a><span data-ttu-id="e77f4-107">О ранних выпусках и Vamp</span><span class="sxs-lookup"><span data-stu-id="e77f4-107">About canary releases and Vamp</span></span>


<span data-ttu-id="e77f4-108">Функция [раннего выпуска](https://martinfowler.com/bliki/CanaryRelease.html) — это интеллектуальная стратегия развертывания, активно применяемая в таких инновационных компаниях, как Netflix, Facebook и Spotify.</span><span class="sxs-lookup"><span data-stu-id="e77f4-108">[Canary releasing](https://martinfowler.com/bliki/CanaryRelease.html) is a smart deployment strategy adopted by innovative organizations like Netflix, Facebook, and Spotify.</span></span> <span data-ttu-id="e77f4-109">Такой подход полностью обоснован, так как он сокращает вероятность возникновения проблем, формирует сети безопасности и повышает уровень инноваций.</span><span class="sxs-lookup"><span data-stu-id="e77f4-109">It’s an approach that makes sense, because it reduces issues, introduces safety-nets, and increases innovation.</span></span> <span data-ttu-id="e77f4-110">Почему же его применяют не все компании?</span><span class="sxs-lookup"><span data-stu-id="e77f4-110">So why aren’t all companies using it?</span></span> <span data-ttu-id="e77f4-111">Расширение конвейера CI/CD за счет внедрения стратегий ранних выпусков повышает сложность системы и требует значительных знаний и опыта в области разработки и выполнения операций.</span><span class="sxs-lookup"><span data-stu-id="e77f4-111">Extending a CI/CD pipeline to include canary strategies adds complexity, and requires extensive devops knowledge and experience.</span></span> <span data-ttu-id="e77f4-112">Этого достаточно для блокировки небольших компаний и предприятий еще до того, как они приступят к работе.</span><span class="sxs-lookup"><span data-stu-id="e77f4-112">That’s enough to block smaller companies and enterprises alike before they even get started.</span></span> 

<span data-ttu-id="e77f4-113">[Vamp](http://vamp.io/) — система с открытым исходным кодом, разработанная для того, чтобы упростить этот переход и реализовать функции ранних выпусков в вашем планировщике контейнеров.</span><span class="sxs-lookup"><span data-stu-id="e77f4-113">[Vamp](http://vamp.io/) is an open-source system designed to ease this transition and bring canary releasing features to your preferred container scheduler.</span></span> <span data-ttu-id="e77f4-114">Функция раннего выпуска в Vamp предоставляет больше возможностей, чем выпуски на основе процентов.</span><span class="sxs-lookup"><span data-stu-id="e77f4-114">Vamp’s canary functionality goes beyond percentage-based rollouts.</span></span> <span data-ttu-id="e77f4-115">Трафик можно отфильтровать и разделить, используя широкий диапазон условий, например для ориентирования на определенных пользователей, диапазоны IP-адресов или устройства.</span><span class="sxs-lookup"><span data-stu-id="e77f4-115">Traffic can be filtered and split on a wide range of conditions, for example to target specific users, IP-ranges, or devices.</span></span> <span data-ttu-id="e77f4-116">Vamp отслеживает и анализирует метрики производительности, позволяя обеспечить автоматизацию на основе реальных данных.</span><span class="sxs-lookup"><span data-stu-id="e77f4-116">Vamp tracks and analyzes performance metrics, allowing for automation based on real-world data.</span></span> <span data-ttu-id="e77f4-117">Можно настроить автоматический откат в случае возникновения ошибок или масштабировать индивидуальные варианты службы на основе нагрузки или задержки.</span><span class="sxs-lookup"><span data-stu-id="e77f4-117">You can set up automatic rollback on errors, or scale individual service variants based on load or latency.</span></span>

## <a name="set-up-azure-container-service-with-dcos"></a><span data-ttu-id="e77f4-118">Настройка Службы контейнеров Azure с помощью DC/OS</span><span class="sxs-lookup"><span data-stu-id="e77f4-118">Set up Azure Container Service with DC/OS</span></span>



1. <span data-ttu-id="e77f4-119">[Разверните кластер DC/OS](container-service-deployment.md) с одним главным узлом и двумя агентами, имеющими размер по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e77f4-119">[Deploy a DC/OS cluster](container-service-deployment.md) with one master and two agents of default size.</span></span> 

2. <span data-ttu-id="e77f4-120">[Создайте туннель SSH](../container-service-connect.md) для подключения к кластеру DC/OS.</span><span class="sxs-lookup"><span data-stu-id="e77f4-120">[Create an SSH tunnel](../container-service-connect.md) to connect to the DC/OS cluster.</span></span> <span data-ttu-id="e77f4-121">В этой статьей предполагается, что вы создаете туннель к кластеру на локальном порте 80.</span><span class="sxs-lookup"><span data-stu-id="e77f4-121">This article assumes that you tunnel to the cluster on local port 80.</span></span>


## <a name="set-up-vamp"></a><span data-ttu-id="e77f4-122">Настройка Vamp</span><span class="sxs-lookup"><span data-stu-id="e77f4-122">Set up Vamp</span></span>

<span data-ttu-id="e77f4-123">Теперь, когда кластер DC/OS работает, из пользовательского интерфейса DC/OS можно установить Vamp (http://localhost:80).</span><span class="sxs-lookup"><span data-stu-id="e77f4-123">Now that you have a running DC/OS cluster, you can install Vamp from the DC/OS UI (http://localhost:80).</span></span> 

![Пользовательский интерфейс DC/OS](./media/container-service-dcos-vamp-canary-release/01_set_up_vamp.png)

<span data-ttu-id="e77f4-125">Установка выполняется в два этапа:</span><span class="sxs-lookup"><span data-stu-id="e77f4-125">Installation is done in two stages:</span></span>

1. <span data-ttu-id="e77f4-126">**Разверните Elasticsearch**.</span><span class="sxs-lookup"><span data-stu-id="e77f4-126">**Deploy Elasticsearch**.</span></span>

2. <span data-ttu-id="e77f4-127">Затем **разверните Vamp**, установив пакет Vamp DC/OS Universe.</span><span class="sxs-lookup"><span data-stu-id="e77f4-127">Then **deploy Vamp** by installing the Vamp DC/OS universe package.</span></span>

### <a name="deploy-elasticsearch"></a><span data-ttu-id="e77f4-128">Развертывание Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="e77f4-128">Deploy Elasticsearch</span></span>

<span data-ttu-id="e77f4-129">Vamp требуется Elasticsearch для сбора метрик и агрегации.</span><span class="sxs-lookup"><span data-stu-id="e77f4-129">Vamp requires Elasticsearch for metrics collection and aggregation.</span></span> <span data-ttu-id="e77f4-130">Для развертывания совместимого стека Elasticsearch для Vamp можно использовать [образы Docker magneticio](https://hub.docker.com/r/magneticio/elastic/).</span><span class="sxs-lookup"><span data-stu-id="e77f4-130">You can use the [magneticio Docker images](https://hub.docker.com/r/magneticio/elastic/) to deploy a compatible Vamp Elasticsearch stack.</span></span>

1. <span data-ttu-id="e77f4-131">В пользовательском интерфейсе DC/OS перейдите к разделу **Services** (Службы) и щелкните **Deploy Service** (Развернуть службу).</span><span class="sxs-lookup"><span data-stu-id="e77f4-131">In the DC/OS UI, go to **Services** and click **Deploy Service**.</span></span>

2. <span data-ttu-id="e77f4-132">Во всплывающем окне **Deploy New Service** (Развертывание новой службы) выберите **JSON mode** (Режим JSON).</span><span class="sxs-lookup"><span data-stu-id="e77f4-132">Select **JSON mode** from the **Deploy New Service** pop-up.</span></span>

  ![Выбор режима JSON](./media/container-service-dcos-vamp-canary-release/02_deploy_service_json_mode.png)

3. <span data-ttu-id="e77f4-134">Вставьте приведенный ниже код JSON.</span><span class="sxs-lookup"><span data-stu-id="e77f4-134">Paste in the following JSON.</span></span> <span data-ttu-id="e77f4-135">Эта конфигурация запускает контейнер с ОЗУ объемом 1 ГБ и обычную проверку работоспособности на порте Elasticsearch.</span><span class="sxs-lookup"><span data-stu-id="e77f4-135">This configuration runs the container with 1 GB of RAM and a basic health check on the Elasticsearch port.</span></span>
  
  ```JSON
  {
    "id": "elasticsearch",
    "instances": 1,
    "cpus": 0.2,
    "mem": 1024.0,
    "container": {
      "docker": {
        "image": "magneticio/elastic:2.2",
        "network": "HOST",
        "forcePullImage": true
      }
    },
    "healthChecks": [
      {
        "protocol": "TCP",
        "gracePeriodSeconds": 30,
        "intervalSeconds": 10,
        "timeoutSeconds": 5,
        "port": 9200,
        "maxConsecutiveFailures": 0
      }
    ]
  }
  ```
  

3. <span data-ttu-id="e77f4-136">Щелкните **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="e77f4-136">Click **Deploy**.</span></span>

  <span data-ttu-id="e77f4-137">DC/OS развертывает контейнер Elasticsearch.</span><span class="sxs-lookup"><span data-stu-id="e77f4-137">DC/OS deploys the Elasticsearch container.</span></span> <span data-ttu-id="e77f4-138">Ход выполнения операции можно отслеживать на странице **Services** (Службы).</span><span class="sxs-lookup"><span data-stu-id="e77f4-138">You can track progress on the **Services** page.</span></span>  

  ![Развертывание Elasticsearch](./media/container-service-dcos-vamp-canary-release/03_deply_elasticsearch.png)

### <a name="deploy-vamp"></a><span data-ttu-id="e77f4-140">Развертывание Vamp</span><span class="sxs-lookup"><span data-stu-id="e77f4-140">Deploy Vamp</span></span>

<span data-ttu-id="e77f4-141">Когда в Elasticsearch отобразится состояние **Running** (Выполняется), можно добавить пакет Vamp DC/OS Universe.</span><span class="sxs-lookup"><span data-stu-id="e77f4-141">Once Elasticsearch reports as **Running**, you can add the Vamp DC/OS Universe package.</span></span> 

1. <span data-ttu-id="e77f4-142">Перейдите в раздел **Universe** и выполните поиск по слову **vamp**.</span><span class="sxs-lookup"><span data-stu-id="e77f4-142">Go to **Universe** and search for **vamp**.</span></span> 
  <span data-ttu-id="e77f4-143">![Vamp на DC/OS Universe](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span><span class="sxs-lookup"><span data-stu-id="e77f4-143">![Vamp on DC/OS universe](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span></span>

2. <span data-ttu-id="e77f4-144">Нажмите кнопку **install** (установить) напротив пакета Vamp и выберите **Advanced Installation** (Дополнительные параметры установки).</span><span class="sxs-lookup"><span data-stu-id="e77f4-144">Click **install** next to the vamp package, and choose **Advanced Installation**.</span></span>

3. <span data-ttu-id="e77f4-145">Прокрутите вниз и введите следующий адрес elasticsearch-url: `http://elasticsearch.marathon.mesos:9200`.</span><span class="sxs-lookup"><span data-stu-id="e77f4-145">Scroll down and enter the following elasticsearch-url: `http://elasticsearch.marathon.mesos:9200`.</span></span> 

  ![Введение URL-адреса Elasticsearch](./media/container-service-dcos-vamp-canary-release/05_universe_elasticsearch_url.png)

4. <span data-ttu-id="e77f4-147">Нажмите кнопку **Review and Install** (Просмотреть и установить), а затем щелкните **Install** (Установить), чтобы начать развертывание.</span><span class="sxs-lookup"><span data-stu-id="e77f4-147">Click **Review and Install**, then click **Install** to start the deployment.</span></span>  

  <span data-ttu-id="e77f4-148">DC/OS развертывает все необходимые компоненты Vamp.</span><span class="sxs-lookup"><span data-stu-id="e77f4-148">DC/OS deploys all required Vamp components.</span></span> <span data-ttu-id="e77f4-149">Ход выполнения операции можно отслеживать на странице **Services** (Службы).</span><span class="sxs-lookup"><span data-stu-id="e77f4-149">You can track progress on the **Services** page.</span></span>
  
  ![Развертывание Vamp как пакета Universe](./media/container-service-dcos-vamp-canary-release/06_deploy_vamp.png)
  
5. <span data-ttu-id="e77f4-151">По завершении развертывания можно получить доступ к пользовательскому интерфейсу Vamp.</span><span class="sxs-lookup"><span data-stu-id="e77f4-151">Once deployment has completed, you can access the Vamp UI:</span></span>

  ![Служба Vamp в DC/OS](./media/container-service-dcos-vamp-canary-release/07_deploy_vamp_complete.png)
  
  ![Пользовательский интерфейс Vamp](./media/container-service-dcos-vamp-canary-release/08_vamp_ui.png)


## <a name="deploy-your-first-service"></a><span data-ttu-id="e77f4-154">Развертывание первой службы</span><span class="sxs-lookup"><span data-stu-id="e77f4-154">Deploy your first service</span></span>

<span data-ttu-id="e77f4-155">Теперь, когда Vamp запущена и работает, разверните службу из схемы.</span><span class="sxs-lookup"><span data-stu-id="e77f4-155">Now that Vamp is up and running, deploy a service from a blueprint.</span></span> 

<span data-ttu-id="e77f4-156">Самая простая форма [схемы Vamp](http://vamp.io/documentation/using-vamp/blueprints/) описывает конечные точки (шлюзы), кластеры и службы, которые необходимо развернуть.</span><span class="sxs-lookup"><span data-stu-id="e77f4-156">In its simplest form, a [Vamp blueprint](http://vamp.io/documentation/using-vamp/blueprints/) describes the endpoints (gateways), clusters, and services to deploy.</span></span> <span data-ttu-id="e77f4-157">Vamp использует кластеры, чтобы сгруппировать различные варианты одной службы в логические группы для раннего выпуска или A/B-тестирования.</span><span class="sxs-lookup"><span data-stu-id="e77f4-157">Vamp uses clusters to group different variants of the same service into logical groups for canary releasing or A/B testing.</span></span>  

<span data-ttu-id="e77f4-158">В этом сценарии используется пример монолитного приложения с именем [**sava**](https://github.com/magneticio/sava), которое имеет версию 1.0.</span><span class="sxs-lookup"><span data-stu-id="e77f4-158">This scenario uses a sample monolithic application called [**sava**](https://github.com/magneticio/sava), which is at version 1.0.</span></span> <span data-ttu-id="e77f4-159">Монолит упакован в контейнер Docker, который находится в Docker Hub в разделе magneticio/sava:1.0.0.</span><span class="sxs-lookup"><span data-stu-id="e77f4-159">The monolith is packaged in a Docker container, which is in Docker Hub under magneticio/sava:1.0.0.</span></span> <span data-ttu-id="e77f4-160">Приложение обычно работает через порт 8080, но в нашем случае необходимо предоставить к нему доступ через порт 9050.</span><span class="sxs-lookup"><span data-stu-id="e77f4-160">The app normally runs on port 8080, but you want to expose it under port 9050 in this case.</span></span> <span data-ttu-id="e77f4-161">Разверните приложение через Vamp, используя простую схему.</span><span class="sxs-lookup"><span data-stu-id="e77f4-161">Deploy the app through Vamp using a simple blueprint.</span></span>

1. <span data-ttu-id="e77f4-162">Перейдите в раздел **Deployments** (Развертывания).</span><span class="sxs-lookup"><span data-stu-id="e77f4-162">Go to **Deployments**.</span></span>

2. <span data-ttu-id="e77f4-163">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e77f4-163">Click **Add**.</span></span>

3. <span data-ttu-id="e77f4-164">Вставьте приведенный ниже YAML-файл схемы.</span><span class="sxs-lookup"><span data-stu-id="e77f4-164">Paste in the following blueprint YAML.</span></span> <span data-ttu-id="e77f4-165">Эта схема содержит один кластер только с одним вариантом службы, который мы изменим в дальнейшем:</span><span class="sxs-lookup"><span data-stu-id="e77f4-165">This blueprint contains one cluster with only one service variant, which we change in a later step:</span></span>

  ```YAML
  name: sava                        # deployment name
  gateways:
    9050: sava_cluster/webport      # stable endpoint
  clusters:
    sava_cluster:               # cluster to create
     services:
        -
          breed:
            name: sava:1.0.0        # service variant name
            deployable: magneticio/sava:1.0.0
            ports:
              webport: 8080/http # cluster endpoint, used for canary releasing
  ```

4. <span data-ttu-id="e77f4-166">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e77f4-166">Click **Save**.</span></span> <span data-ttu-id="e77f4-167">Vamp инициирует развертывание.</span><span class="sxs-lookup"><span data-stu-id="e77f4-167">Vamp initiates the deployment.</span></span>

<span data-ttu-id="e77f4-168">Развертывание отображается на странице **Deployments** (Развертывания).</span><span class="sxs-lookup"><span data-stu-id="e77f4-168">The deployment is listed on the **Deployments** page.</span></span> <span data-ttu-id="e77f4-169">Щелкните развертывание, чтобы отследить его состояние.</span><span class="sxs-lookup"><span data-stu-id="e77f4-169">Click the deployment to monitor its status.</span></span>

![Пользовательский интерфейс Vamp: развертывание sava](./media/container-service-dcos-vamp-canary-release/09_sava100.png)

![Служба sava в пользовательском интерфейсе Vamp](./media/container-service-dcos-vamp-canary-release/09a_sava100.png)

<span data-ttu-id="e77f4-172">Создаются два шлюза, которые перечислены на странице **Gateways** (Шлюзы):</span><span class="sxs-lookup"><span data-stu-id="e77f4-172">Two gateways are created, which are listed on the **Gateways** page:</span></span>

* <span data-ttu-id="e77f4-173">стабильная конечная точка для доступа к выполняющейся службе (порт 9050);</span><span class="sxs-lookup"><span data-stu-id="e77f4-173">a stable endpoint to access the running service (port 9050)</span></span> 
* <span data-ttu-id="e77f4-174">внутренний шлюз, управляемый Vamp (позже мы рассмотрим этот шлюз подробнее).</span><span class="sxs-lookup"><span data-stu-id="e77f4-174">a Vamp-managed internal gateway (more on this gateway later).</span></span> 

![Пользовательский интерфейс Vamp: шлюзы sava](./media/container-service-dcos-vamp-canary-release/10_vamp_sava_gateways.png)

<span data-ttu-id="e77f4-176">Служба sava развернута, но внешний доступ к ней недоступен, так как Azure Load Balancer пока не может перенаправлять в нее трафик.</span><span class="sxs-lookup"><span data-stu-id="e77f4-176">The sava service has now deployed, but you can’t access it externally because the Azure Load Balancer doesn’t know to forward traffic to it yet.</span></span> <span data-ttu-id="e77f4-177">Для доступа к службе обновите конфигурацию сети Azure.</span><span class="sxs-lookup"><span data-stu-id="e77f4-177">To access the service, update the Azure networking configuration.</span></span>


## <a name="update-the-azure-network-configuration"></a><span data-ttu-id="e77f4-178">Обновление конфигурации сети Azure</span><span class="sxs-lookup"><span data-stu-id="e77f4-178">Update the Azure network configuration</span></span>

<span data-ttu-id="e77f4-179">Vamp развернула службу sava на узлах агента DC/OS, предоставив стабильную конечную точку на порте 9050.</span><span class="sxs-lookup"><span data-stu-id="e77f4-179">Vamp deployed the sava service on the DC/OS agent nodes, exposing a stable endpoint at port 9050.</span></span> <span data-ttu-id="e77f4-180">Для доступа к службе из-за пределов кластера DC/OS в развертывании кластера необходимо внести следующие изменения в конфигурацию сети Azure:</span><span class="sxs-lookup"><span data-stu-id="e77f4-180">To access the service from outside the DC/OS cluster, make the following changes to the Azure network configuration in your cluster deployment:</span></span> 

1. <span data-ttu-id="e77f4-181">**Настройте Azure Load Balancer** для агентов (ресурс с именем **dcos-agent-lb-xxxx**) с проверкой работоспособности и правилом перенаправления трафика с порта 9050 в экземпляры sava.</span><span class="sxs-lookup"><span data-stu-id="e77f4-181">**Configure the Azure Load Balancer** for the agents (the resource named **dcos-agent-lb-xxxx**) with a health probe and a rule to forward traffic on port 9050 to the sava instances.</span></span> 

2. <span data-ttu-id="e77f4-182">**Обновите группу безопасности сети** для общедоступных агентов (ресурс с именем **XXXX-agent-public-nsg-XXXX**), чтобы разрешить трафик с порта 9050.</span><span class="sxs-lookup"><span data-stu-id="e77f4-182">**Update the network security group** for the public agents (the resource named **XXXX-agent-public-nsg-XXXX**) to allow traffic on port 9050.</span></span>

<span data-ttu-id="e77f4-183">Подробные инструкции по выполнению этих задач с помощью портала Azure см. в статье [Предоставление общего доступа к приложению Службы контейнеров Azure](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="e77f4-183">For detailed steps to complete these tasks using the Azure portal, see [Enable public access to an Azure Container Service application](container-service-enable-public-access.md).</span></span> <span data-ttu-id="e77f4-184">Укажите порт 9050 для всех параметров портов.</span><span class="sxs-lookup"><span data-stu-id="e77f4-184">Specify port 9050 for all port settings.</span></span>


<span data-ttu-id="e77f4-185">Когда все создано, перейдите к колонке **Overview** (Обзор) подсистемы балансировки нагрузки агента DC/OS (ресурс с именем **dcos-agent-lb-xxxx**).</span><span class="sxs-lookup"><span data-stu-id="e77f4-185">Once everything has been created, go to the **Overview** blade of the DC/OS agent load balancer (the resource named **dcos-agent-lb-xxxx**).</span></span> <span data-ttu-id="e77f4-186">Найдите **Public IP address** (Общедоступный IP-адрес) и используйте этот адрес для доступа к службе sava через порт 9050.</span><span class="sxs-lookup"><span data-stu-id="e77f4-186">Find the **Public IP address**, and use the address to access sava at port 9050.</span></span>

![Портал Azure: получение общедоступного IP-адреса](./media/container-service-dcos-vamp-canary-release/18_public_ip_address.png)

![sava](./media/container-service-dcos-vamp-canary-release/19_sava100.png)


## <a name="run-a-canary-release"></a><span data-ttu-id="e77f4-189">Запуск раннего выпуска</span><span class="sxs-lookup"><span data-stu-id="e77f4-189">Run a canary release</span></span>

<span data-ttu-id="e77f4-190">Предположим, что у вас есть новая версия этого приложения, для которой требуется создать ранний выпуск и запустить его в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="e77f4-190">Suppose you have a new version of this application that you want to canary release into production.</span></span> <span data-ttu-id="e77f4-191">Вы поместили ее в контейнер как magneticio/sava:1.1.0, и все готово для начала процесса.</span><span class="sxs-lookup"><span data-stu-id="e77f4-191">You have it containerized as magneticio/sava:1.1.0 and are ready to go.</span></span> <span data-ttu-id="e77f4-192">Vamp позволяет легко добавлять новые службы в работающую развернутую систему.</span><span class="sxs-lookup"><span data-stu-id="e77f4-192">Vamp lets you easily add new services to the running deployment.</span></span> <span data-ttu-id="e77f4-193">Эти "объединенные" службы развертываются параллельно с существующими службами в кластере, и им назначается вес 0 %.</span><span class="sxs-lookup"><span data-stu-id="e77f4-193">These "merged" services are deployed alongside the existing services in the cluster, and assigned a weight of 0%.</span></span> <span data-ttu-id="e77f4-194">Трафик не направляется во вновь объединенные службы, пока вы не настроите распределение трафика.</span><span class="sxs-lookup"><span data-stu-id="e77f4-194">No traffic is routed to a newly merged service until you adjust the traffic distribution.</span></span> <span data-ttu-id="e77f4-195">Ползунок веса в пользовательском интерфейсе Vamp дает полный контроль над распределением, позволяя выполнять добавочные корректировки (ранний выпуск) или мгновенный откат.</span><span class="sxs-lookup"><span data-stu-id="e77f4-195">The weight slider in the Vamp UI gives you complete control over the distribution, allowing for incremental adjustments (canary release) or an instant rollback.</span></span>

### <a name="merge-a-new-service-variant"></a><span data-ttu-id="e77f4-196">Объединение нового варианта службы</span><span class="sxs-lookup"><span data-stu-id="e77f4-196">Merge a new service variant</span></span>

<span data-ttu-id="e77f4-197">Чтобы объединить новую службу sava 1.1 с работающей развернутой системой, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e77f4-197">To merge the new sava 1.1 service with the running deployment:</span></span>

1. <span data-ttu-id="e77f4-198">В пользовательском интерфейсе Vamp щелкните **Blueprints** (Схемы).</span><span class="sxs-lookup"><span data-stu-id="e77f4-198">In the Vamp UI, click **Blueprints**.</span></span>

2. <span data-ttu-id="e77f4-199">Щелкните **Add** (Добавить) и вставьте приведенный ниже YAML-файл схемы. Эта схема описывает новый вариант службы (sava:1.1.0) для развертывания в существующем кластере (sava_cluster).</span><span class="sxs-lookup"><span data-stu-id="e77f4-199">Click **Add** and paste in the following blueprint YAML: This blueprint describes a new service variant (sava:1.1.0) to deploy within the existing cluster (sava_cluster).</span></span>

  ```YAML
  name: sava:1.1.0      # blueprint name
  clusters:
    sava_cluster:       # cluster to update
      services:
        -
          breed:
            name: sava:1.1.0    # service variant name
            deployable: magneticio/sava:1.1.0    
            ports:
              webport: 8080/http # cluster endpoint to update
  ```
  
3. <span data-ttu-id="e77f4-200">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e77f4-200">Click **Save**.</span></span> <span data-ttu-id="e77f4-201">Схема сохраняется и отображается на странице **Blueprints** (Схемы).</span><span class="sxs-lookup"><span data-stu-id="e77f4-201">The blueprint is stored and listed on the **Blueprints** page.</span></span>

4. <span data-ttu-id="e77f4-202">Откройте меню действий схемы sava:1.1 и выберите команду **Merge to** (Объединить с).</span><span class="sxs-lookup"><span data-stu-id="e77f4-202">Open the action menu on the sava:1.1 blueprint and click **Merge to**.</span></span>

  ![Пользовательский интерфейс Vamp: схемы](./media/container-service-dcos-vamp-canary-release/20_sava110_mergeto.png)

5. <span data-ttu-id="e77f4-204">Выберите развертывание **sava** и нажмите кнопку **Merge** (Объединить).</span><span class="sxs-lookup"><span data-stu-id="e77f4-204">Select the **sava** deployment and click **Merge**.</span></span>

  ![Пользовательский интерфейс Vamp: объединение схемы с развертыванием](./media/container-service-dcos-vamp-canary-release/21_sava110_merge.png)

<span data-ttu-id="e77f4-206">Vamp развертывает новый вариант службы sava:1.1.0, описанный в схеме, наряду с sava:1.0.0 в кластере **sava_cluster** работающей развернутой системы.</span><span class="sxs-lookup"><span data-stu-id="e77f4-206">Vamp deploys the new sava:1.1.0 service variant described in the blueprint alongside sava:1.0.0 in the **sava_cluster** of the running deployment.</span></span> 

![Пользовательский интерфейс Vamp: обновленное развертывание sava](./media/container-service-dcos-vamp-canary-release/22_sava_cluster.png)

<span data-ttu-id="e77f4-208">Шлюз **sava/sava_cluster/webport** (конечная точка кластера) также обновляется, добавляя маршрут к развернутой службе sava:1.1.0.</span><span class="sxs-lookup"><span data-stu-id="e77f4-208">The **sava/sava_cluster/webport** gateway (the cluster endpoint) is also updated, adding a route to the newly deployed sava:1.1.0.</span></span> <span data-ttu-id="e77f4-209">На этом этапе трафик в службу не перенаправляется (параметру **WEIGHT** (Вес) задано значение 0 %).</span><span class="sxs-lookup"><span data-stu-id="e77f4-209">At this point, no traffic is routed here (the **WEIGHT** is set to 0%).</span></span>

![Пользовательский интерфейс Vamp: шлюз кластера](./media/container-service-dcos-vamp-canary-release/23_sava_cluster_webport.png)

### <a name="canary-release"></a><span data-ttu-id="e77f4-211">Ранний выпуск</span><span class="sxs-lookup"><span data-stu-id="e77f4-211">Canary release</span></span>

<span data-ttu-id="e77f4-212">Когда обе версии службы sava развернуты в одном кластере, настройте распределение трафика между ними, перемещая ползунок **WEIGHT** (Вес).</span><span class="sxs-lookup"><span data-stu-id="e77f4-212">With both versions of sava deployed in the same cluster, adjust the distribution of traffic between them by moving the **WEIGHT** slider.</span></span>

1. <span data-ttu-id="e77f4-213">Щелкните значок ![Пользовательский интерфейс Vamp: изменить](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) рядом с параметром **WEIGHT** (Вес).</span><span class="sxs-lookup"><span data-stu-id="e77f4-213">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next to **WEIGHT**.</span></span>

2. <span data-ttu-id="e77f4-214">Задайте значение распределения веса 50 %/50 % и нажмите кнопку **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="e77f4-214">Set the weight distribution to 50%/50% and click **Save**.</span></span>

  ![Пользовательский интерфейс Vamp: ползунок веса шлюза](./media/container-service-dcos-vamp-canary-release/24_sava_cluster_webport_weight.png)

3. <span data-ttu-id="e77f4-216">Вернитесь в браузер и обновите страницу sava еще несколько раз.</span><span class="sxs-lookup"><span data-stu-id="e77f4-216">Go back to your browser and refresh the sava page a few more times.</span></span> <span data-ttu-id="e77f4-217">Теперь приложение sava переключается между страницами sava:1.0 и sava:1.1.</span><span class="sxs-lookup"><span data-stu-id="e77f4-217">The sava application now switches between a sava:1.0 page and a sava:1.1 page.</span></span>

  ![чередование служб sava1.0 и sava1.1](./media/container-service-dcos-vamp-canary-release/25_sava_100_101.png)


  > [!NOTE]
  > <span data-ttu-id="e77f4-219">Это чередование страниц лучше всего работает в режиме "Инкогнито" или "Анонимный" из-за кэширования статических ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e77f4-219">This alternation of the page works best with the "Incognito" or “Anonymous” mode of your browser because of the caching of static assets.</span></span>
  >

### <a name="filter-traffic"></a><span data-ttu-id="e77f4-220">Фильтрация трафика</span><span class="sxs-lookup"><span data-stu-id="e77f4-220">Filter traffic</span></span>

<span data-ttu-id="e77f4-221">Предположим, что после развертывания в sava:1.1.0 обнаружилась несовместимость, которая вызывает проблемы с отображением в браузерах Firefox.</span><span class="sxs-lookup"><span data-stu-id="e77f4-221">Suppose after deployment that you discovered an incompatibility in sava:1.1.0 that causes display problems in Firefox browsers.</span></span> <span data-ttu-id="e77f4-222">В Vamp можно настроить фильтрацию входящего трафика и перенаправление всех пользователей Firefox обратно в известную стабильную службу sava:1.0.0.</span><span class="sxs-lookup"><span data-stu-id="e77f4-222">You can set Vamp to filter incoming traffic and direct all Firefox users back to the known stable sava:1.0.0.</span></span> <span data-ttu-id="e77f4-223">Этот фильтр мгновенно устраняет нарушение в работе для пользователей Firefox, в то время как остальные продолжают пользоваться преимуществами улучшенной службы sava:1.1.0.</span><span class="sxs-lookup"><span data-stu-id="e77f4-223">This filter instantly resolves the disruption for Firefox users, while everybody else continues to enjoy the benefits of the improved sava:1.1.0.</span></span>

<span data-ttu-id="e77f4-224">Vamp использует **условия** для фильтрации трафика между маршрутами шлюза.</span><span class="sxs-lookup"><span data-stu-id="e77f4-224">Vamp uses **conditions** to filter traffic between routes in a gateway.</span></span> <span data-ttu-id="e77f4-225">Трафик сначала фильтруется и направляется в соответствии с условиями, примененными к каждому маршруту.</span><span class="sxs-lookup"><span data-stu-id="e77f4-225">Traffic is first filtered and directed according to the conditions applied to each route.</span></span> <span data-ttu-id="e77f4-226">Весь остальной трафик распределяется в соответствии с настройками веса шлюза.</span><span class="sxs-lookup"><span data-stu-id="e77f4-226">All remaining traffic is distributed according to the gateway weight setting.</span></span>

<span data-ttu-id="e77f4-227">Можно создать условие, фильтрующее всех пользователей Firefox и направляющее их в старую службу sava:1.0.0:</span><span class="sxs-lookup"><span data-stu-id="e77f4-227">You can create a condition to filter all Firefox users and direct them to the old sava:1.0.0:</span></span>

1. <span data-ttu-id="e77f4-228">На странице **Gateways** (Шлюзы) конечной точки sava/sava_cluster/webport щелкните значок ![Пользовательский интерфейс Vamp: изменить](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png), чтобы добавить **CONDITION** (Условие) в маршрут sava/sava_cluster/sava:1.0.0/webport.</span><span class="sxs-lookup"><span data-stu-id="e77f4-228">On the sava/sava_cluster/webport **Gateways** page, click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) to add a **CONDITION** to the route sava/sava_cluster/sava:1.0.0/webport.</span></span> 

2. <span data-ttu-id="e77f4-229">Введите условие **user-agent == Firefox** и щелкните значок ![Пользовательский интерфейс Vamp: сохранить](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span><span class="sxs-lookup"><span data-stu-id="e77f4-229">Enter the condition **user-agent == Firefox** and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span></span>

  <span data-ttu-id="e77f4-230">Vamp добавляет условие со значением силы по умолчанию 0 %.</span><span class="sxs-lookup"><span data-stu-id="e77f4-230">Vamp adds the condition with a default strength of 0%.</span></span> <span data-ttu-id="e77f4-231">Чтобы начать фильтрацию трафика, необходимо настроить силу условия.</span><span class="sxs-lookup"><span data-stu-id="e77f4-231">To start filtering traffic, you need to adjust the condition strength.</span></span>

3. <span data-ttu-id="e77f4-232">Щелкните значок ![Пользовательский интерфейс Vamp: изменить](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png), чтобы изменить параметр **STRENGTH** (Сила), применяемый к условию.</span><span class="sxs-lookup"><span data-stu-id="e77f4-232">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) to change the **STRENGTH** applied to the condition.</span></span>
 
4. <span data-ttu-id="e77f4-233">Задайте параметру **STRENGTH** (Сила) значение 100% и щелкните значок ![Пользовательский интерфейс Vamp: сохранить](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png), чтобы сохранить.</span><span class="sxs-lookup"><span data-stu-id="e77f4-233">Set the **STRENGTH** to 100% and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) to save.</span></span>

  <span data-ttu-id="e77f4-234">Теперь Vamp отправляет весь трафик, соответствующий условию (все пользователи Firefox), в службу sava:1.0.0.</span><span class="sxs-lookup"><span data-stu-id="e77f4-234">Vamp now sends all traffic matching the condition (all Firefox users) to sava:1.0.0.</span></span>

  ![Пользовательский интерфейс Vamp: применение условия к шлюзу](./media/container-service-dcos-vamp-canary-release/26_apply_condition.png)

5. <span data-ttu-id="e77f4-236">Наконец, настройте вес шлюза для отправки всего остального трафика (все пользователи, отличные от Firefox) в новую службу sava:1.1.0.</span><span class="sxs-lookup"><span data-stu-id="e77f4-236">Finally, adjust the gateway weight to send all remaining traffic (all non-Firefox users) to the new sava:1.1.0.</span></span> <span data-ttu-id="e77f4-237">Щелкните значок ![Пользовательский интерфейс Vamp: изменить](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) рядом с параметром **WEIGHT** (Вес) и задайте значение распределения веса, чтобы 100 % трафика направлялось по маршруту sava/sava_cluster/sava:1.1.0/webport.</span><span class="sxs-lookup"><span data-stu-id="e77f4-237">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next to **WEIGHT** and set the weight distribution so 100% is directed to the route sava/sava_cluster/sava:1.1.0/webport.</span></span>

  <span data-ttu-id="e77f4-238">Весь трафик, который не фильтруется по условию, теперь направляется в новую службу sava:1.1.0.</span><span class="sxs-lookup"><span data-stu-id="e77f4-238">All traffic not filtered by the condition is now directed to the new sava:1.1.0.</span></span>

6. <span data-ttu-id="e77f4-239">Чтобы увидеть фильтр в действии, откройте два разных браузера (Firefox и еще один браузер) и войдите в службу sava с обоих.</span><span class="sxs-lookup"><span data-stu-id="e77f4-239">To see the filter in action, open two different browsers (one Firefox and one other browser) and access the sava service from both.</span></span> <span data-ttu-id="e77f4-240">Все запросы из Firefox отправляются в sava:1.0.0, а все прочие браузеры направляются в sava:1.1.0.</span><span class="sxs-lookup"><span data-stu-id="e77f4-240">All Firefox requests are sent to sava:1.0.0, while all other browsers are directed to sava:1.1.0.</span></span>

  ![Пользовательский интерфейс Vamp: фильтрация трафика](./media/container-service-dcos-vamp-canary-release/27_filter_traffic.png)

## <a name="summing-up"></a><span data-ttu-id="e77f4-242">Подведем итоги</span><span class="sxs-lookup"><span data-stu-id="e77f4-242">Summing up</span></span>

<span data-ttu-id="e77f4-243">В этой статье представлены краткие сведения о Vamp в кластере DC/OS.</span><span class="sxs-lookup"><span data-stu-id="e77f4-243">This article was a quick introduction to Vamp on a DC/OS cluster.</span></span> <span data-ttu-id="e77f4-244">Для начинающих показано, как установить и запустить Vamp в кластере DC/OS Службы контейнеров Azure, развернуть службу с помощью схемы Vamp, а также войти в службу через предоставленную конечную точку (шлюз).</span><span class="sxs-lookup"><span data-stu-id="e77f4-244">For starters, you got Vamp up and running on your Azure Container Service DC/OS cluster, deployed a service with a Vamp blueprint, and accessed it at the exposed endpoint (gateway).</span></span>

<span data-ttu-id="e77f4-245">Мы также рассмотрели несколько эффективных функций Vamp: объединение нового варианта службы с работающей развернутой системой и постепенное ее введение, а затем фильтрация трафика для устранения известной несовместимости.</span><span class="sxs-lookup"><span data-stu-id="e77f4-245">We also touched on some powerful features of Vamp:  merging a new service variant to the running deployment and introducing it incrementally, then filtering traffic to resolve a known incompatibility.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e77f4-246">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e77f4-246">Next steps</span></span>

* <span data-ttu-id="e77f4-247">Ознакомьтесь со сведениями об управлении действиями Vamp через интерфейс [REST API Vamp](http://vamp.io/documentation/api/api-reference/).</span><span class="sxs-lookup"><span data-stu-id="e77f4-247">Learn about managing Vamp actions through the [Vamp REST API](http://vamp.io/documentation/api/api-reference/).</span></span>

* <span data-ttu-id="e77f4-248">Создайте сценарии автоматизации Vamp, используя Node.js, и выполните их как [рабочие процессы Vamp](http://vamp.io/documentation/tutorials/create-a-workflow/).</span><span class="sxs-lookup"><span data-stu-id="e77f4-248">Build Vamp automation scripts in Node.js and run them as [Vamp workflows](http://vamp.io/documentation/tutorials/create-a-workflow/).</span></span>

* <span data-ttu-id="e77f4-249">Также ознакомьтесь с дополнительными [руководствами по VAMP](http://vamp.io/documentation/tutorials/overview/).</span><span class="sxs-lookup"><span data-stu-id="e77f4-249">See additional [VAMP tutorials](http://vamp.io/documentation/tutorials/overview/).</span></span>

