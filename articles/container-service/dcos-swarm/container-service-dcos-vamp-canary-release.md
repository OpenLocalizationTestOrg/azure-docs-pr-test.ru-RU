---
title: "выпуск aaaCanary с Vamp на кластере Azure DC/OS | Документы Microsoft"
description: "Как toouse Vamp toocanary выпуска служб и применить фильтрацию в кластере контейнера службы Azure DC/OS смарт-трафика"
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
ms.openlocfilehash: e7b8658a161a7cddcf718e3e1c12a889a330d3d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="canary-release-microservices-with-vamp-on-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="ac269-103">Ранний выпуск микрослужб с помощью Vamp в кластере DC/OS Службы контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="ac269-103">Canary release microservices with Vamp on an Azure Container Service DC/OS cluster</span></span>

<span data-ttu-id="ac269-104">В этом пошаговом руководстве мы настраиваем Vamp в Службе контейнеров Azure, используя кластер DC/OS.</span><span class="sxs-lookup"><span data-stu-id="ac269-104">In this walkthrough, we set up Vamp on Azure Container Service with a DC/OS cluster.</span></span> <span data-ttu-id="ac269-105">Мы предохранителя выпуска hello Vamp Демонстрация службы «sava», а затем устраните несовместимость hello службы с Firefox путем применения фильтрации смарт-трафика.</span><span class="sxs-lookup"><span data-stu-id="ac269-105">We canary release hello Vamp demo service "sava", and then resolve an incompatibility of hello service with Firefox by applying smart traffic filtering.</span></span> 

> [!TIP] 
> <span data-ttu-id="ac269-106">В этом пошаговом руководстве Vamp работает на кластере DC/OS, но может также служить Vamp с Kubernetes hello orchestrator.</span><span class="sxs-lookup"><span data-stu-id="ac269-106">In this walkthrough Vamp runs on a DC/OS cluster, but you can also use Vamp with Kubernetes as hello orchestrator.</span></span>
>

## <a name="about-canary-releases-and-vamp"></a><span data-ttu-id="ac269-107">О ранних выпусках и Vamp</span><span class="sxs-lookup"><span data-stu-id="ac269-107">About canary releases and Vamp</span></span>


<span data-ttu-id="ac269-108">Функция [раннего выпуска](https://martinfowler.com/bliki/CanaryRelease.html) — это интеллектуальная стратегия развертывания, активно применяемая в таких инновационных компаниях, как Netflix, Facebook и Spotify.</span><span class="sxs-lookup"><span data-stu-id="ac269-108">[Canary releasing](https://martinfowler.com/bliki/CanaryRelease.html) is a smart deployment strategy adopted by innovative organizations like Netflix, Facebook, and Spotify.</span></span> <span data-ttu-id="ac269-109">Такой подход полностью обоснован, так как он сокращает вероятность возникновения проблем, формирует сети безопасности и повышает уровень инноваций.</span><span class="sxs-lookup"><span data-stu-id="ac269-109">It’s an approach that makes sense, because it reduces issues, introduces safety-nets, and increases innovation.</span></span> <span data-ttu-id="ac269-110">Почему же его применяют не все компании?</span><span class="sxs-lookup"><span data-stu-id="ac269-110">So why aren’t all companies using it?</span></span> <span data-ttu-id="ac269-111">Расширение конвейера CI/CD tooinclude предохранителя стратегии повышает сложность и требует широко devops знания и опыт.</span><span class="sxs-lookup"><span data-stu-id="ac269-111">Extending a CI/CD pipeline tooinclude canary strategies adds complexity, and requires extensive devops knowledge and experience.</span></span> <span data-ttu-id="ac269-112">Это достаточно tooblock небольших компаний и предприятий одинаково, прежде чем они даже приступить к работе.</span><span class="sxs-lookup"><span data-stu-id="ac269-112">That’s enough tooblock smaller companies and enterprises alike before they even get started.</span></span> 

<span data-ttu-id="ac269-113">[Vamp](http://vamp.io/) — система открытым исходным кодом, предназначенная tooease этот переход и перевести предохранителя освободить планировщик контейнера tooyour основной функции.</span><span class="sxs-lookup"><span data-stu-id="ac269-113">[Vamp](http://vamp.io/) is an open-source system designed tooease this transition and bring canary releasing features tooyour preferred container scheduler.</span></span> <span data-ttu-id="ac269-114">Функция раннего выпуска в Vamp предоставляет больше возможностей, чем выпуски на основе процентов.</span><span class="sxs-lookup"><span data-stu-id="ac269-114">Vamp’s canary functionality goes beyond percentage-based rollouts.</span></span> <span data-ttu-id="ac269-115">Трафик могут быть отфильтрованы и разбиение по широкий набор условий, например tootarget конкретных пользователей, диапазоны IP-адресов или устройств.</span><span class="sxs-lookup"><span data-stu-id="ac269-115">Traffic can be filtered and split on a wide range of conditions, for example tootarget specific users, IP-ranges, or devices.</span></span> <span data-ttu-id="ac269-116">Vamp отслеживает и анализирует метрики производительности, позволяя обеспечить автоматизацию на основе реальных данных.</span><span class="sxs-lookup"><span data-stu-id="ac269-116">Vamp tracks and analyzes performance metrics, allowing for automation based on real-world data.</span></span> <span data-ttu-id="ac269-117">Можно настроить автоматический откат в случае возникновения ошибок или масштабировать индивидуальные варианты службы на основе нагрузки или задержки.</span><span class="sxs-lookup"><span data-stu-id="ac269-117">You can set up automatic rollback on errors, or scale individual service variants based on load or latency.</span></span>

## <a name="set-up-azure-container-service-with-dcos"></a><span data-ttu-id="ac269-118">Настройка Службы контейнеров Azure с помощью DC/OS</span><span class="sxs-lookup"><span data-stu-id="ac269-118">Set up Azure Container Service with DC/OS</span></span>



1. <span data-ttu-id="ac269-119">[Разверните кластер DC/OS](container-service-deployment.md) с одним главным узлом и двумя агентами, имеющими размер по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ac269-119">[Deploy a DC/OS cluster](container-service-deployment.md) with one master and two agents of default size.</span></span> 

2. <span data-ttu-id="ac269-120">[Создать туннель SSH](../container-service-connect.md) tooconnect toohello DC/OS кластера.</span><span class="sxs-lookup"><span data-stu-id="ac269-120">[Create an SSH tunnel](../container-service-connect.md) tooconnect toohello DC/OS cluster.</span></span> <span data-ttu-id="ac269-121">В этой статье предполагается, что вы туннелирования toohello кластера на локальный порт 80.</span><span class="sxs-lookup"><span data-stu-id="ac269-121">This article assumes that you tunnel toohello cluster on local port 80.</span></span>


## <a name="set-up-vamp"></a><span data-ttu-id="ac269-122">Настройка Vamp</span><span class="sxs-lookup"><span data-stu-id="ac269-122">Set up Vamp</span></span>

<span data-ttu-id="ac269-123">Теперь, когда запущенному кластеру DC/OS Vamp можно установить из hello пользовательского интерфейса DC/OS (http://localhost: 80).</span><span class="sxs-lookup"><span data-stu-id="ac269-123">Now that you have a running DC/OS cluster, you can install Vamp from hello DC/OS UI (http://localhost:80).</span></span> 

![Пользовательский интерфейс DC/OS](./media/container-service-dcos-vamp-canary-release/01_set_up_vamp.png)

<span data-ttu-id="ac269-125">Установка выполняется в два этапа:</span><span class="sxs-lookup"><span data-stu-id="ac269-125">Installation is done in two stages:</span></span>

1. <span data-ttu-id="ac269-126">**Разверните Elasticsearch**.</span><span class="sxs-lookup"><span data-stu-id="ac269-126">**Deploy Elasticsearch**.</span></span>

2. <span data-ttu-id="ac269-127">Затем **развертывание Vamp** путем установки пакета вселенной Vamp DC/OS hello.</span><span class="sxs-lookup"><span data-stu-id="ac269-127">Then **deploy Vamp** by installing hello Vamp DC/OS universe package.</span></span>

### <a name="deploy-elasticsearch"></a><span data-ttu-id="ac269-128">Развертывание Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="ac269-128">Deploy Elasticsearch</span></span>

<span data-ttu-id="ac269-129">Vamp требуется Elasticsearch для сбора метрик и агрегации.</span><span class="sxs-lookup"><span data-stu-id="ac269-129">Vamp requires Elasticsearch for metrics collection and aggregation.</span></span> <span data-ttu-id="ac269-130">Можно использовать hello [magneticio Docker images](https://hub.docker.com/r/magneticio/elastic/) toodeploy совместимый стека Vamp Elasticsearch.</span><span class="sxs-lookup"><span data-stu-id="ac269-130">You can use hello [magneticio Docker images](https://hub.docker.com/r/magneticio/elastic/) toodeploy a compatible Vamp Elasticsearch stack.</span></span>

1. <span data-ttu-id="ac269-131">В hello DC/OS пользовательского интерфейса, перейдите слишком**службы** и нажмите кнопку **служба развертывания**.</span><span class="sxs-lookup"><span data-stu-id="ac269-131">In hello DC/OS UI, go too**Services** and click **Deploy Service**.</span></span>

2. <span data-ttu-id="ac269-132">Выберите **режим JSON** из hello **развернуть новую службу** всплывающих.</span><span class="sxs-lookup"><span data-stu-id="ac269-132">Select **JSON mode** from hello **Deploy New Service** pop-up.</span></span>

  ![Выбор режима JSON](./media/container-service-dcos-vamp-canary-release/02_deploy_service_json_mode.png)

3. <span data-ttu-id="ac269-134">Вставьте следующий JSON hello.</span><span class="sxs-lookup"><span data-stu-id="ac269-134">Paste in hello following JSON.</span></span> <span data-ttu-id="ac269-135">Эта конфигурация запускает hello контейнера с 1 ГБ ОЗУ и базовой проверки исправности через порт Elasticsearch hello.</span><span class="sxs-lookup"><span data-stu-id="ac269-135">This configuration runs hello container with 1 GB of RAM and a basic health check on hello Elasticsearch port.</span></span>
  
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
  

3. <span data-ttu-id="ac269-136">Щелкните **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="ac269-136">Click **Deploy**.</span></span>

  <span data-ttu-id="ac269-137">Контроллер домена/OS развертывает hello Elasticsearch контейнера.</span><span class="sxs-lookup"><span data-stu-id="ac269-137">DC/OS deploys hello Elasticsearch container.</span></span> <span data-ttu-id="ac269-138">Можно отслеживать ход выполнения hello **служб** страницы.</span><span class="sxs-lookup"><span data-stu-id="ac269-138">You can track progress on hello **Services** page.</span></span>  

  ![Развертывание Elasticsearch](./media/container-service-dcos-vamp-canary-release/03_deply_elasticsearch.png)

### <a name="deploy-vamp"></a><span data-ttu-id="ac269-140">Развертывание Vamp</span><span class="sxs-lookup"><span data-stu-id="ac269-140">Deploy Vamp</span></span>

<span data-ttu-id="ac269-141">После Elasticsearch отчеты в виде **под управлением**, можно добавить пакет Vamp вселенной DC/OS hello.</span><span class="sxs-lookup"><span data-stu-id="ac269-141">Once Elasticsearch reports as **Running**, you can add hello Vamp DC/OS Universe package.</span></span> 

1. <span data-ttu-id="ac269-142">Go слишком**Universe** и выполните поиск **vamp**.</span><span class="sxs-lookup"><span data-stu-id="ac269-142">Go too**Universe** and search for **vamp**.</span></span> 
  <span data-ttu-id="ac269-143">![Vamp на DC/OS Universe](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span><span class="sxs-lookup"><span data-stu-id="ac269-143">![Vamp on DC/OS universe](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span></span>

2. <span data-ttu-id="ac269-144">Нажмите кнопку **установить** Далее toohello vamp пакета и выбрать **расширенный установки**.</span><span class="sxs-lookup"><span data-stu-id="ac269-144">Click **install** next toohello vamp package, and choose **Advanced Installation**.</span></span>

3. <span data-ttu-id="ac269-145">Прокрутите список вниз и введите hello elasticsearch-URL-адреса: `http://elasticsearch.marathon.mesos:9200`.</span><span class="sxs-lookup"><span data-stu-id="ac269-145">Scroll down and enter hello following elasticsearch-url: `http://elasticsearch.marathon.mesos:9200`.</span></span> 

  ![Введение URL-адреса Elasticsearch](./media/container-service-dcos-vamp-canary-release/05_universe_elasticsearch_url.png)

4. <span data-ttu-id="ac269-147">Нажмите кнопку **просмотрите и установите**, нажмите кнопку **установить** toostart hello развертывания.</span><span class="sxs-lookup"><span data-stu-id="ac269-147">Click **Review and Install**, then click **Install** toostart hello deployment.</span></span>  

  <span data-ttu-id="ac269-148">DC/OS развертывает все необходимые компоненты Vamp.</span><span class="sxs-lookup"><span data-stu-id="ac269-148">DC/OS deploys all required Vamp components.</span></span> <span data-ttu-id="ac269-149">Можно отслеживать ход выполнения hello **служб** страницы.</span><span class="sxs-lookup"><span data-stu-id="ac269-149">You can track progress on hello **Services** page.</span></span>
  
  ![Развертывание Vamp как пакета Universe](./media/container-service-dcos-vamp-canary-release/06_deploy_vamp.png)
  
5. <span data-ttu-id="ac269-151">После завершения развертывания можно получить доступ к hello Vamp пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="ac269-151">Once deployment has completed, you can access hello Vamp UI:</span></span>

  ![Служба Vamp в DC/OS](./media/container-service-dcos-vamp-canary-release/07_deploy_vamp_complete.png)
  
  ![Пользовательский интерфейс Vamp](./media/container-service-dcos-vamp-canary-release/08_vamp_ui.png)


## <a name="deploy-your-first-service"></a><span data-ttu-id="ac269-154">Развертывание первой службы</span><span class="sxs-lookup"><span data-stu-id="ac269-154">Deploy your first service</span></span>

<span data-ttu-id="ac269-155">Теперь, когда Vamp запущена и работает, разверните службу из схемы.</span><span class="sxs-lookup"><span data-stu-id="ac269-155">Now that Vamp is up and running, deploy a service from a blueprint.</span></span> 

<span data-ttu-id="ac269-156">В простейшей форме [Vamp чертежом](http://vamp.io/documentation/using-vamp/blueprints/) описывает конечные точки hello (шлюзов), кластеры и toodeploy служб.</span><span class="sxs-lookup"><span data-stu-id="ac269-156">In its simplest form, a [Vamp blueprint](http://vamp.io/documentation/using-vamp/blueprints/) describes hello endpoints (gateways), clusters, and services toodeploy.</span></span> <span data-ttu-id="ac269-157">Vamp использует кластеров toogroup различные варианты hello же service в логические группы для предохранителя освобождение или A / B-тестирования.</span><span class="sxs-lookup"><span data-stu-id="ac269-157">Vamp uses clusters toogroup different variants of hello same service into logical groups for canary releasing or A/B testing.</span></span>  

<span data-ttu-id="ac269-158">В этом сценарии используется пример монолитного приложения с именем [**sava**](https://github.com/magneticio/sava), которое имеет версию 1.0.</span><span class="sxs-lookup"><span data-stu-id="ac269-158">This scenario uses a sample monolithic application called [**sava**](https://github.com/magneticio/sava), which is at version 1.0.</span></span> <span data-ttu-id="ac269-159">Hello монолита упаковывается в контейнере Docker, которая находится в концентраторе Docker под magneticio/sava:1.0.0.</span><span class="sxs-lookup"><span data-stu-id="ac269-159">hello monolith is packaged in a Docker container, which is in Docker Hub under magneticio/sava:1.0.0.</span></span> <span data-ttu-id="ac269-160">приложение Hello, как правило, выполняется через порт 8080, но требуется его в порт 9050 в данном случае tooexpose.</span><span class="sxs-lookup"><span data-stu-id="ac269-160">hello app normally runs on port 8080, but you want tooexpose it under port 9050 in this case.</span></span> <span data-ttu-id="ac269-161">Разверните приложение hello через Vamp с помощью простой проект.</span><span class="sxs-lookup"><span data-stu-id="ac269-161">Deploy hello app through Vamp using a simple blueprint.</span></span>

1. <span data-ttu-id="ac269-162">Go слишком**развертывания**.</span><span class="sxs-lookup"><span data-stu-id="ac269-162">Go too**Deployments**.</span></span>

2. <span data-ttu-id="ac269-163">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ac269-163">Click **Add**.</span></span>

3. <span data-ttu-id="ac269-164">Вставить в hello следующий проект YAML.</span><span class="sxs-lookup"><span data-stu-id="ac269-164">Paste in hello following blueprint YAML.</span></span> <span data-ttu-id="ac269-165">Эта схема содержит один кластер только с одним вариантом службы, который мы изменим в дальнейшем:</span><span class="sxs-lookup"><span data-stu-id="ac269-165">This blueprint contains one cluster with only one service variant, which we change in a later step:</span></span>

  ```YAML
  name: sava                        # deployment name
  gateways:
    9050: sava_cluster/webport      # stable endpoint
  clusters:
    sava_cluster:               # cluster toocreate
     services:
        -
          breed:
            name: sava:1.0.0        # service variant name
            deployable: magneticio/sava:1.0.0
            ports:
              webport: 8080/http # cluster endpoint, used for canary releasing
  ```

4. <span data-ttu-id="ac269-166">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ac269-166">Click **Save**.</span></span> <span data-ttu-id="ac269-167">Vamp инициирует развертывание hello.</span><span class="sxs-lookup"><span data-stu-id="ac269-167">Vamp initiates hello deployment.</span></span>

<span data-ttu-id="ac269-168">Развертывание Hello значится на hello **развертываний** страницы.</span><span class="sxs-lookup"><span data-stu-id="ac269-168">hello deployment is listed on hello **Deployments** page.</span></span> <span data-ttu-id="ac269-169">Нажмите кнопку развертывания toomonitor hello его состояние.</span><span class="sxs-lookup"><span data-stu-id="ac269-169">Click hello deployment toomonitor its status.</span></span>

![Пользовательский интерфейс Vamp: развертывание sava](./media/container-service-dcos-vamp-canary-release/09_sava100.png)

![Служба sava в пользовательском интерфейсе Vamp](./media/container-service-dcos-vamp-canary-release/09a_sava100.png)

<span data-ttu-id="ac269-172">Создаются два шлюза, перечислены на hello **шлюзы** страницы:</span><span class="sxs-lookup"><span data-stu-id="ac269-172">Two gateways are created, which are listed on hello **Gateways** page:</span></span>

* <span data-ttu-id="ac269-173">hello tooaccess стабильный конечной точки службы (порт 9050)</span><span class="sxs-lookup"><span data-stu-id="ac269-173">a stable endpoint tooaccess hello running service (port 9050)</span></span> 
* <span data-ttu-id="ac269-174">внутренний шлюз, управляемый Vamp (позже мы рассмотрим этот шлюз подробнее).</span><span class="sxs-lookup"><span data-stu-id="ac269-174">a Vamp-managed internal gateway (more on this gateway later).</span></span> 

![Пользовательский интерфейс Vamp: шлюзы sava](./media/container-service-dcos-vamp-canary-release/10_vamp_sava_gateways.png)

<span data-ttu-id="ac269-176">Теперь развернута служба sava Hello, но не его извне тем hello подсистемы балансировки нагрузки Azure еще не знает tooit tooforward трафика.</span><span class="sxs-lookup"><span data-stu-id="ac269-176">hello sava service has now deployed, but you can’t access it externally because hello Azure Load Balancer doesn’t know tooforward traffic tooit yet.</span></span> <span data-ttu-id="ac269-177">Служба tooaccess hello, обновление hello Azure конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="ac269-177">tooaccess hello service, update hello Azure networking configuration.</span></span>


## <a name="update-hello-azure-network-configuration"></a><span data-ttu-id="ac269-178">Обновление конфигурации сети Azure hello</span><span class="sxs-lookup"><span data-stu-id="ac269-178">Update hello Azure network configuration</span></span>

<span data-ttu-id="ac269-179">Служба sava hello vamp развернуть на узлах агента hello DC/OS, предоставляют стабильный конечную точку на порте 9050.</span><span class="sxs-lookup"><span data-stu-id="ac269-179">Vamp deployed hello sava service on hello DC/OS agent nodes, exposing a stable endpoint at port 9050.</span></span> <span data-ttu-id="ac269-180">Служба hello tooaccess из вне кластера DC/OS hello, сделать hello следующая конфигурация сети Azure toohello изменения в развертывание кластера:</span><span class="sxs-lookup"><span data-stu-id="ac269-180">tooaccess hello service from outside hello DC/OS cluster, make hello following changes toohello Azure network configuration in your cluster deployment:</span></span> 

1. <span data-ttu-id="ac269-181">**Настройка балансировки нагрузки Azure hello** hello агентов (hello ресурс с именем **dcos агента-балансировки нагрузки xxxx**) с зонда работоспособности и правило tooforward трафика через порт 9050 toohello sava экземплярами.</span><span class="sxs-lookup"><span data-stu-id="ac269-181">**Configure hello Azure Load Balancer** for hello agents (hello resource named **dcos-agent-lb-xxxx**) with a health probe and a rule tooforward traffic on port 9050 toohello sava instances.</span></span> 

2. <span data-ttu-id="ac269-182">**Группы безопасности сети hello обновление** hello общих агентов (hello ресурс с именем **XXXX-агента public-nsg-XXXX**) tooallow трафик через порт 9050.</span><span class="sxs-lookup"><span data-stu-id="ac269-182">**Update hello network security group** for hello public agents (hello resource named **XXXX-agent-public-nsg-XXXX**) tooallow traffic on port 9050.</span></span>

<span data-ttu-id="ac269-183">Для toocomplete подробное описание действий для этих задач с помощью hello Azure портала, см. в разделе [включить приложение Azure контейнера службы общего доступа tooan](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="ac269-183">For detailed steps toocomplete these tasks using hello Azure portal, see [Enable public access tooan Azure Container Service application](container-service-enable-public-access.md).</span></span> <span data-ttu-id="ac269-184">Укажите порт 9050 для всех параметров портов.</span><span class="sxs-lookup"><span data-stu-id="ac269-184">Specify port 9050 for all port settings.</span></span>


<span data-ttu-id="ac269-185">Когда все будет создана, перейдите toohello **Обзор** колонке подсистемы балансировки нагрузки агента hello DC/OS (hello ресурс с именем **dcos агента-балансировки нагрузки xxxx**).</span><span class="sxs-lookup"><span data-stu-id="ac269-185">Once everything has been created, go toohello **Overview** blade of hello DC/OS agent load balancer (hello resource named **dcos-agent-lb-xxxx**).</span></span> <span data-ttu-id="ac269-186">Найти hello **общедоступный IP-адрес**и использовать sava tooaccess hello адресов на порту 9050.</span><span class="sxs-lookup"><span data-stu-id="ac269-186">Find hello **Public IP address**, and use hello address tooaccess sava at port 9050.</span></span>

![Портал Azure: получение общедоступного IP-адреса](./media/container-service-dcos-vamp-canary-release/18_public_ip_address.png)

![sava](./media/container-service-dcos-vamp-canary-release/19_sava100.png)


## <a name="run-a-canary-release"></a><span data-ttu-id="ac269-189">Запуск раннего выпуска</span><span class="sxs-lookup"><span data-stu-id="ac269-189">Run a canary release</span></span>

<span data-ttu-id="ac269-190">Предположим, что у вас есть новая версия этого приложения, которые должны toocanary выпуска в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="ac269-190">Suppose you have a new version of this application that you want toocanary release into production.</span></span> <span data-ttu-id="ac269-191">Вы его контейнерных как magneticio/sava:1.1.0 и toogo готовности.</span><span class="sxs-lookup"><span data-stu-id="ac269-191">You have it containerized as magneticio/sava:1.1.0 and are ready toogo.</span></span> <span data-ttu-id="ac269-192">Vamp позволяет легко добавлять новые toohello служб под управлением развертывания.</span><span class="sxs-lookup"><span data-stu-id="ac269-192">Vamp lets you easily add new services toohello running deployment.</span></span> <span data-ttu-id="ac269-193">Эти службы «слияние» развернута вместе с существующими службами hello в кластере hello и вес 0%.</span><span class="sxs-lookup"><span data-stu-id="ac269-193">These "merged" services are deployed alongside hello existing services in hello cluster, and assigned a weight of 0%.</span></span> <span data-ttu-id="ac269-194">Трафик не является службой перенаправленное tooa вновь слияние, пока настроить распределение трафика hello.</span><span class="sxs-lookup"><span data-stu-id="ac269-194">No traffic is routed tooa newly merged service until you adjust hello traffic distribution.</span></span> <span data-ttu-id="ac269-195">ползунок вес Hello в hello Vamp пользовательского интерфейса дает полный контроль над распределением hello, позволяя пошаговой корректировки (предохранителя выпуск) или мгновенное отката.</span><span class="sxs-lookup"><span data-stu-id="ac269-195">hello weight slider in hello Vamp UI gives you complete control over hello distribution, allowing for incremental adjustments (canary release) or an instant rollback.</span></span>

### <a name="merge-a-new-service-variant"></a><span data-ttu-id="ac269-196">Объединение нового варианта службы</span><span class="sxs-lookup"><span data-stu-id="ac269-196">Merge a new service variant</span></span>

<span data-ttu-id="ac269-197">toomerge hello новой sava 1.1 службы с hello выполнение развертывания:</span><span class="sxs-lookup"><span data-stu-id="ac269-197">toomerge hello new sava 1.1 service with hello running deployment:</span></span>

1. <span data-ttu-id="ac269-198">В hello Vamp пользовательского интерфейса, выберите **чертежей**.</span><span class="sxs-lookup"><span data-stu-id="ac269-198">In hello Vamp UI, click **Blueprints**.</span></span>

2. <span data-ttu-id="ac269-199">Нажмите кнопку **добавить** и вставить в следующие hello чертежом YAML: этот проект описывает новые toodeploy variant (sava: 1.1.0) службы в существующий кластер hello (sava_cluster).</span><span class="sxs-lookup"><span data-stu-id="ac269-199">Click **Add** and paste in hello following blueprint YAML: This blueprint describes a new service variant (sava:1.1.0) toodeploy within hello existing cluster (sava_cluster).</span></span>

  ```YAML
  name: sava:1.1.0      # blueprint name
  clusters:
    sava_cluster:       # cluster tooupdate
      services:
        -
          breed:
            name: sava:1.1.0    # service variant name
            deployable: magneticio/sava:1.1.0    
            ports:
              webport: 8080/http # cluster endpoint tooupdate
  ```
  
3. <span data-ttu-id="ac269-200">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ac269-200">Click **Save**.</span></span> <span data-ttu-id="ac269-201">сохраняется и отображается на hello чертежом Hello **чертежей** страницы.</span><span class="sxs-lookup"><span data-stu-id="ac269-201">hello blueprint is stored and listed on hello **Blueprints** page.</span></span>

4. <span data-ttu-id="ac269-202">Привет открыть меню "действие" hello sava: 1.1 проект и выберите команду **слияние с**.</span><span class="sxs-lookup"><span data-stu-id="ac269-202">Open hello action menu on hello sava:1.1 blueprint and click **Merge to**.</span></span>

  ![Пользовательский интерфейс Vamp: схемы](./media/container-service-dcos-vamp-canary-release/20_sava110_mergeto.png)

5. <span data-ttu-id="ac269-204">Выберите hello **sava** развертывания и нажмите кнопку **слияния**.</span><span class="sxs-lookup"><span data-stu-id="ac269-204">Select hello **sava** deployment and click **Merge**.</span></span>

  ![Vamp пользовательского интерфейса — слияния toodeployment план](./media/container-service-dcos-vamp-canary-release/21_sava110_merge.png)

<span data-ttu-id="ac269-206">Vamp развертывает hello новый sava: 1.1.0 службы вариант описывается в план действий hello вместе с sava: 1.0.0 в hello **sava_cluster** из hello развернут.</span><span class="sxs-lookup"><span data-stu-id="ac269-206">Vamp deploys hello new sava:1.1.0 service variant described in hello blueprint alongside sava:1.0.0 in hello **sava_cluster** of hello running deployment.</span></span> 

![Пользовательский интерфейс Vamp: обновленное развертывание sava](./media/container-service-dcos-vamp-canary-release/22_sava_cluster.png)

<span data-ttu-id="ac269-208">Hello **sava/sava_cluster/webport** шлюза (конечная точка кластера hello) также обновляется, добавление toohello маршрута вновь установить sava: 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="ac269-208">hello **sava/sava_cluster/webport** gateway (hello cluster endpoint) is also updated, adding a route toohello newly deployed sava:1.1.0.</span></span> <span data-ttu-id="ac269-209">На этом этапе не трафик направляется здесь (hello **ВЕС** имеет значение too0%).</span><span class="sxs-lookup"><span data-stu-id="ac269-209">At this point, no traffic is routed here (hello **WEIGHT** is set too0%).</span></span>

![Пользовательский интерфейс Vamp: шлюз кластера](./media/container-service-dcos-vamp-canary-release/23_sava_cluster_webport.png)

### <a name="canary-release"></a><span data-ttu-id="ac269-211">Ранний выпуск</span><span class="sxs-lookup"><span data-stu-id="ac269-211">Canary release</span></span>

<span data-ttu-id="ac269-212">С обеими версиями sava развернутых в hello же кластера, hello распределение трафика между ними, перемещая hello **ВЕС** ползунок.</span><span class="sxs-lookup"><span data-stu-id="ac269-212">With both versions of sava deployed in hello same cluster, adjust hello distribution of traffic between them by moving hello **WEIGHT** slider.</span></span>

1. <span data-ttu-id="ac269-213">Нажмите кнопку ![Vamp пользовательского интерфейса — изменить](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) Далее слишком**ВЕС**.</span><span class="sxs-lookup"><span data-stu-id="ac269-213">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next too**WEIGHT**.</span></span>

2. <span data-ttu-id="ac269-214">Установите распространения too50%/50% hello вес и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ac269-214">Set hello weight distribution too50%/50% and click **Save**.</span></span>

  ![Пользовательский интерфейс Vamp: ползунок веса шлюза](./media/container-service-dcos-vamp-canary-release/24_sava_cluster_webport_weight.png)

3. <span data-ttu-id="ac269-216">Вернитесь tooyour браузера и обновите страницу приветствия sava еще несколько раз.</span><span class="sxs-lookup"><span data-stu-id="ac269-216">Go back tooyour browser and refresh hello sava page a few more times.</span></span> <span data-ttu-id="ac269-217">Теперь приложение Hello sava переключений между страницы sava: 1.0 и sava: 1.1.</span><span class="sxs-lookup"><span data-stu-id="ac269-217">hello sava application now switches between a sava:1.0 page and a sava:1.1 page.</span></span>

  ![чередование служб sava1.0 и sava1.1](./media/container-service-dcos-vamp-canary-release/25_sava_100_101.png)


  > [!NOTE]
  > <span data-ttu-id="ac269-219">Это чередования страницы приветствия лучше всего работает с hello «Браузера» или «Anonymous» режим браузера из-за hello кэширование статических активов.</span><span class="sxs-lookup"><span data-stu-id="ac269-219">This alternation of hello page works best with hello "Incognito" or “Anonymous” mode of your browser because of hello caching of static assets.</span></span>
  >

### <a name="filter-traffic"></a><span data-ttu-id="ac269-220">Фильтрация трафика</span><span class="sxs-lookup"><span data-stu-id="ac269-220">Filter traffic</span></span>

<span data-ttu-id="ac269-221">Предположим, что после развертывания в sava:1.1.0 обнаружилась несовместимость, которая вызывает проблемы с отображением в браузерах Firefox.</span><span class="sxs-lookup"><span data-stu-id="ac269-221">Suppose after deployment that you discovered an incompatibility in sava:1.1.0 that causes display problems in Firefox browsers.</span></span> <span data-ttu-id="ac269-222">Можно задать Vamp toofilter входящего трафика и направить все пользователи Firefox обратно toohello известные стабильный sava: 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="ac269-222">You can set Vamp toofilter incoming traffic and direct all Firefox users back toohello known stable sava:1.0.0.</span></span> <span data-ttu-id="ac269-223">Этот фильтр мгновенной разрешает hello перебоев в работе пользователей Firefox при любом другом клиенте tooenjoy преимущества hello hello повышение sava: 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="ac269-223">This filter instantly resolves hello disruption for Firefox users, while everybody else continues tooenjoy hello benefits of hello improved sava:1.1.0.</span></span>

<span data-ttu-id="ac269-224">Использует vamp **условия** toofilter трафик между маршруты в шлюз.</span><span class="sxs-lookup"><span data-stu-id="ac269-224">Vamp uses **conditions** toofilter traffic between routes in a gateway.</span></span> <span data-ttu-id="ac269-225">Трафик сначала фильтруется и направляются соответствующим toohello условия, применяемые tooeach маршрута.</span><span class="sxs-lookup"><span data-stu-id="ac269-225">Traffic is first filtered and directed according toohello conditions applied tooeach route.</span></span> <span data-ttu-id="ac269-226">Все остальные трафик распределяется в соответствии с параметром вес toohello шлюза.</span><span class="sxs-lookup"><span data-stu-id="ac269-226">All remaining traffic is distributed according toohello gateway weight setting.</span></span>

<span data-ttu-id="ac269-227">Можно создать все пользователи Firefox toofilter условие и направлять их toohello старый sava: 1.0.0:</span><span class="sxs-lookup"><span data-stu-id="ac269-227">You can create a condition toofilter all Firefox users and direct them toohello old sava:1.0.0:</span></span>

1. <span data-ttu-id="ac269-228">На hello sava/sava_cluster/webport **шлюзы** щелкните ![Vamp пользовательского интерфейса — изменить](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd **УСЛОВИЕ** sava/sava_cluster/sava:1.0.0/webport toohello маршрута.</span><span class="sxs-lookup"><span data-stu-id="ac269-228">On hello sava/sava_cluster/webport **Gateways** page, click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd a **CONDITION** toohello route sava/sava_cluster/sava:1.0.0/webport.</span></span> 

2. <span data-ttu-id="ac269-229">Введите условие hello **агент пользователя == Firefox** и нажмите кнопку ![Vamp UI - Сохранить](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span><span class="sxs-lookup"><span data-stu-id="ac269-229">Enter hello condition **user-agent == Firefox** and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span></span>

  <span data-ttu-id="ac269-230">Vamp добавляет условие hello с стойкость по умолчанию 0%.</span><span class="sxs-lookup"><span data-stu-id="ac269-230">Vamp adds hello condition with a default strength of 0%.</span></span> <span data-ttu-id="ac269-231">toostart фильтрации трафика, вы должны tooadjust hello условие силы.</span><span class="sxs-lookup"><span data-stu-id="ac269-231">toostart filtering traffic, you need tooadjust hello condition strength.</span></span>

3. <span data-ttu-id="ac269-232">Нажмите кнопку ![Vamp пользовательского интерфейса — изменить](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange hello **СТОЙКОСТЬ** применения toohello условие.</span><span class="sxs-lookup"><span data-stu-id="ac269-232">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange hello **STRENGTH** applied toohello condition.</span></span>
 
4. <span data-ttu-id="ac269-233">Набор hello **СТОЙКОСТЬ** too100% и нажмите кнопку ![Vamp UI - Сохранить](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave.</span><span class="sxs-lookup"><span data-stu-id="ac269-233">Set hello **STRENGTH** too100% and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave.</span></span>

  <span data-ttu-id="ac269-234">Теперь vamp отправляет весь трафик сопоставления toosava:1.0.0 hello условие (все пользователи Firefox).</span><span class="sxs-lookup"><span data-stu-id="ac269-234">Vamp now sends all traffic matching hello condition (all Firefox users) toosava:1.0.0.</span></span>

  ![Vamp пользовательского интерфейса — применить условие toogateway](./media/container-service-dcos-vamp-canary-release/26_apply_condition.png)

5. <span data-ttu-id="ac269-236">Наконец следует настройте все остальные трафика (все пользователи не Firefox) toohello новый sava: 1.1.0 toosend вес hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="ac269-236">Finally, adjust hello gateway weight toosend all remaining traffic (all non-Firefox users) toohello new sava:1.1.0.</span></span> <span data-ttu-id="ac269-237">Нажмите кнопку ![Vamp пользовательского интерфейса — изменить](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) Далее слишком**ВЕС** и установите распространения вес hello, направленной toohello sava/sava_cluster/sava:1.1.0/webport маршрута — 100%.</span><span class="sxs-lookup"><span data-stu-id="ac269-237">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next too**WEIGHT** and set hello weight distribution so 100% is directed toohello route sava/sava_cluster/sava:1.1.0/webport.</span></span>

  <span data-ttu-id="ac269-238">Весь трафик, не фильтруется по условию hello сейчас новый расширенный toohello sava: 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="ac269-238">All traffic not filtered by hello condition is now directed toohello new sava:1.1.0.</span></span>

6. <span data-ttu-id="ac269-239">Фильтр toosee hello в действии, откройте два различных браузеров (один Firefox и другой браузер) и службы sava hello обоих.</span><span class="sxs-lookup"><span data-stu-id="ac269-239">toosee hello filter in action, open two different browsers (one Firefox and one other browser) and access hello sava service from both.</span></span> <span data-ttu-id="ac269-240">Все запросы Firefox отправляются toosava:1.0.0, пока все другие браузеры, направленной toosava:1.1.0.</span><span class="sxs-lookup"><span data-stu-id="ac269-240">All Firefox requests are sent toosava:1.0.0, while all other browsers are directed toosava:1.1.0.</span></span>

  ![Пользовательский интерфейс Vamp: фильтрация трафика](./media/container-service-dcos-vamp-canary-release/27_filter_traffic.png)

## <a name="summing-up"></a><span data-ttu-id="ac269-242">Подведем итоги</span><span class="sxs-lookup"><span data-stu-id="ac269-242">Summing up</span></span>

<span data-ttu-id="ac269-243">Эта статья переведена tooVamp Краткое введение в кластере DC/OS.</span><span class="sxs-lookup"><span data-stu-id="ac269-243">This article was a quick introduction tooVamp on a DC/OS cluster.</span></span> <span data-ttu-id="ac269-244">Во-первых есть Vamp и запуск на контейнера службы Azure DC/ОС кластера, развернуть службу с чертежом Vamp и к нему доступ в конечной точке предоставляется hello (шлюз).</span><span class="sxs-lookup"><span data-stu-id="ac269-244">For starters, you got Vamp up and running on your Azure Container Service DC/OS cluster, deployed a service with a Vamp blueprint, and accessed it at hello exposed endpoint (gateway).</span></span>

<span data-ttu-id="ac269-245">Мы рассмотрели некоторые мощные функции Vamp: слияние новых службы variant toohello развернут и введение в постепенно, а затем фильтрации трафика tooresolve известные несовместимости.</span><span class="sxs-lookup"><span data-stu-id="ac269-245">We also touched on some powerful features of Vamp:  merging a new service variant toohello running deployment and introducing it incrementally, then filtering traffic tooresolve a known incompatibility.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ac269-246">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ac269-246">Next steps</span></span>

* <span data-ttu-id="ac269-247">Дополнительные сведения об управлении Vamp действия через hello [Vamp API-интерфейса REST](http://vamp.io/documentation/api/api-reference/).</span><span class="sxs-lookup"><span data-stu-id="ac269-247">Learn about managing Vamp actions through hello [Vamp REST API](http://vamp.io/documentation/api/api-reference/).</span></span>

* <span data-ttu-id="ac269-248">Создайте сценарии автоматизации Vamp, используя Node.js, и выполните их как [рабочие процессы Vamp](http://vamp.io/documentation/tutorials/create-a-workflow/).</span><span class="sxs-lookup"><span data-stu-id="ac269-248">Build Vamp automation scripts in Node.js and run them as [Vamp workflows](http://vamp.io/documentation/tutorials/create-a-workflow/).</span></span>

* <span data-ttu-id="ac269-249">Также ознакомьтесь с дополнительными [руководствами по VAMP](http://vamp.io/documentation/tutorials/overview/).</span><span class="sxs-lookup"><span data-stu-id="ac269-249">See additional [VAMP tutorials](http://vamp.io/documentation/tutorials/overview/).</span></span>

