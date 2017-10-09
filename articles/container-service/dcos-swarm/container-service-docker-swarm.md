---
title: "кластер aaaManage скапливаются Azure с Docker API | Документы Microsoft"
description: "Развертывание кластера tooa помощью Docker Swarm контейнеры в контейнере службы Azure"
services: container-service
documentationcenter: 
author: rgardler
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: bb9b07c82a7b48caeb2e351455797cbf2a6e7480
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="container-management-with-docker-swarm"></a><span data-ttu-id="16d27-104">Управление контейнерами с помощью Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="16d27-104">Container management with Docker Swarm</span></span>
<span data-ttu-id="16d27-105">Docker Swarm — это среда для развертывания контейнерной рабочей нагрузки в наборе узлов, объединенных в пул Docker.</span><span class="sxs-lookup"><span data-stu-id="16d27-105">Docker Swarm provides an environment for deploying containerized workloads across a pooled set of Docker hosts.</span></span> <span data-ttu-id="16d27-106">Группу мелких объектов docker использует hello собственного API Docker.</span><span class="sxs-lookup"><span data-stu-id="16d27-106">Docker Swarm uses hello native Docker API.</span></span> <span data-ttu-id="16d27-107">Hello рабочего процесса управления контейнерами в помощью Docker Swarm имеет почти такую же toowhat, которое было бы на одном узле контейнера.</span><span class="sxs-lookup"><span data-stu-id="16d27-107">hello workflow for managing containers on a Docker Swarm is almost identical toowhat it would be on a single container host.</span></span> <span data-ttu-id="16d27-108">Этот документ содержит простые примеры развертывания контейнерной рабочей нагрузки в экземпляре Docker Swarm, который развернут в службе контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="16d27-108">This document provides simple examples of deploying containerized workloads in an Azure Container Service instance of Docker Swarm.</span></span> <span data-ttu-id="16d27-109">Дополнительные сведения о Docker Swarm см. в [документации по Docker Swarm на сайте Docker.com](https://docs.docker.com/swarm/).</span><span class="sxs-lookup"><span data-stu-id="16d27-109">For more in-depth documentation on Docker Swarm, see [Docker Swarm on Docker.com](https://docs.docker.com/swarm/).</span></span>

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="16d27-110">Предварительные требования toohello упражнений данного документа:</span><span class="sxs-lookup"><span data-stu-id="16d27-110">Prerequisites toohello exercises in this document:</span></span>

[<span data-ttu-id="16d27-111">Создайте кластер Swarm в службе контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="16d27-111">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)

[<span data-ttu-id="16d27-112">Подключение с кластером hello группу мелких объектов в контейнере службы Azure</span><span class="sxs-lookup"><span data-stu-id="16d27-112">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)

## <a name="deploy-a-new-container"></a><span data-ttu-id="16d27-113">Развертывание нового контейнера</span><span class="sxs-lookup"><span data-stu-id="16d27-113">Deploy a new container</span></span>
<span data-ttu-id="16d27-114">новый контейнер hello с помощью Docker Swarm toocreate использовать hello `docker run` команда (гарантирует, что вы открыли образцов toohello туннель SSH, согласно hello указанные выше предварительные условия).</span><span class="sxs-lookup"><span data-stu-id="16d27-114">toocreate a new container in hello Docker Swarm, use hello `docker run` command (ensuring that you have opened an SSH tunnel toohello masters as per hello prerequisites above).</span></span> <span data-ttu-id="16d27-115">Этот пример создает контейнер из hello `yeasy/simple-web` изображения:</span><span class="sxs-lookup"><span data-stu-id="16d27-115">This example creates a container from hello `yeasy/simple-web` image:</span></span>

```bash
user@ubuntu:~$ docker run -d -p 80:80 yeasy/simple-web

4298d397b9ab6f37e2d1978ef3c8c1537c938e98a8bf096ff00def2eab04bf72
```

<span data-ttu-id="16d27-116">После создания контейнера hello `docker ps` tooreturn сведения о контейнере hello.</span><span class="sxs-lookup"><span data-stu-id="16d27-116">After hello container has been created, use `docker ps` tooreturn information about hello container.</span></span> <span data-ttu-id="16d27-117">Здесь, обратите внимание, что этот агент группу мелких объектов hello, на котором размещается контейнер hello отображается:</span><span class="sxs-lookup"><span data-stu-id="16d27-117">Notice here that hello Swarm agent that is hosting hello container is listed:</span></span>

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   31 seconds ago      Up 9 seconds        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

<span data-ttu-id="16d27-118">Теперь можно получить доступ к hello приложение, которое выполняется в этом контейнере через hello общее DNS-имя подсистемы балансировки нагрузки агента hello группу мелких объектов.</span><span class="sxs-lookup"><span data-stu-id="16d27-118">You can now access hello application that is running in this container through hello public DNS name of hello Swarm agent load balancer.</span></span> <span data-ttu-id="16d27-119">Эти сведения можно найти в hello портала Azure:</span><span class="sxs-lookup"><span data-stu-id="16d27-119">You can find this information in hello Azure portal:</span></span>  

![Результаты реального посещения](./media/container-service-docker-swarm/real-visit.jpg)  

<span data-ttu-id="16d27-121">По умолчанию hello балансировки нагрузки имеет порты 80 и открыть 8080 и 443.</span><span class="sxs-lookup"><span data-stu-id="16d27-121">By default hello Load Balancer has ports 80, 8080 and 443 open.</span></span> <span data-ttu-id="16d27-122">Если требуется, чтобы tooconnect на другой порт потребуется tooopen этот порт на hello подсистемы балансировки нагрузки Azure для hello пул агентов.</span><span class="sxs-lookup"><span data-stu-id="16d27-122">If you want tooconnect on another port you will need tooopen that port on hello Azure Load Balancer for hello Agent Pool.</span></span>

## <a name="deploy-multiple-containers"></a><span data-ttu-id="16d27-123">Развертывание нескольких контейнеров</span><span class="sxs-lookup"><span data-stu-id="16d27-123">Deploy multiple containers</span></span>
<span data-ttu-id="16d27-124">Запускаются несколько контейнеров, выполнив «docker выполнения» несколько раз, можно использовать hello `docker ps` toosee команду, где размещается hello контейнеров, выполняющихся на.</span><span class="sxs-lookup"><span data-stu-id="16d27-124">As multiple containers are started, by executing 'docker run' multiple times, you can use hello `docker ps` command toosee which hosts hello containers are running on.</span></span> <span data-ttu-id="16d27-125">В следующем примере hello три контейнера равномерно распределены по hello три агента группу мелких объектов:</span><span class="sxs-lookup"><span data-stu-id="16d27-125">In hello example below, three containers are spread evenly across hello three Swarm agents:</span></span>  

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
11be062ff602        yeasy/simple-web    "/bin/sh -c 'python i"   11 seconds ago      Up 10 seconds       10.0.0.6:83->80/tcp   swarm-agent-34A73819-2/clever_banach
1ff421554c50        yeasy/simple-web    "/bin/sh -c 'python i"   49 seconds ago      Up 48 seconds       10.0.0.4:82->80/tcp   swarm-agent-34A73819-0/stupefied_ride
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   2 minutes ago       Up 2 minutes        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

## <a name="deploy-containers-by-using-docker-compose"></a><span data-ttu-id="16d27-126">Развертывание контейнеров с помощью Docker Compose</span><span class="sxs-lookup"><span data-stu-id="16d27-126">Deploy containers by using Docker Compose</span></span>
<span data-ttu-id="16d27-127">Можно использовать Docker Compose tooautomate hello развертывание и настройку несколько контейнеров.</span><span class="sxs-lookup"><span data-stu-id="16d27-127">You can use Docker Compose tooautomate hello deployment and configuration of multiple containers.</span></span> <span data-ttu-id="16d27-128">toodo таким образом, убедитесь, что для туннеля Secure Shell (SSH) будет создана, так и для задания этой переменной DOCKER_HOST hello (см. раздел предварительных требований hello выше).</span><span class="sxs-lookup"><span data-stu-id="16d27-128">toodo so, ensure that a Secure Shell (SSH) tunnel has been created and that hello DOCKER_HOST variable has been set (see hello pre-requisites above).</span></span>

<span data-ttu-id="16d27-129">Создайте на локальной системе файл docker-compose.yml.</span><span class="sxs-lookup"><span data-stu-id="16d27-129">Create a docker-compose.yml file on your local system.</span></span> <span data-ttu-id="16d27-130">toodo, этот метод следует использовать [пример](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span><span class="sxs-lookup"><span data-stu-id="16d27-130">toodo this, use this [sample](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span></span>

```bash
web:
  image: adtd/web:0.1
  ports:
    - "80:80"
  links:
    - rest:rest-demo-azure.marathon.mesos
rest:
  image: adtd/rest:0.1
  ports:
    - "8080:8080"

```

<span data-ttu-id="16d27-131">Запустите `docker-compose up -d` развертывания контейнера hello toostart:</span><span class="sxs-lookup"><span data-stu-id="16d27-131">Run `docker-compose up -d` toostart hello container deployments:</span></span>

```bash
user@ubuntu:~/compose$ docker-compose up -d
Pulling rest (adtd/rest:0.1)...
swarm-agent-3B7093B8-0: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-3: Pulling adtd/rest:0.1... : downloaded
Creating compose_rest_1
Pulling web (adtd/web:0.1)...
swarm-agent-3B7093B8-3: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-0: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/web:0.1... : downloaded
Creating compose_web_1
```

<span data-ttu-id="16d27-132">Наконец будет возвращаться hello списка запущенных контейнеров.</span><span class="sxs-lookup"><span data-stu-id="16d27-132">Finally, hello list of running containers will be returned.</span></span> <span data-ttu-id="16d27-133">Этот список содержит hello контейнеров, которые были развернуты с помощью Docker Compose:</span><span class="sxs-lookup"><span data-stu-id="16d27-133">This list reflects hello containers that were deployed by using Docker Compose:</span></span>

```bash
user@ubuntu:~/compose$ docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS                     NAMES
caf185d221b7        adtd/web:0.1        "apache2-foreground"   2 minutes ago       Up About a minute   10.0.0.4:80->80/tcp       swarm-agent-3B7093B8-0/compose_web_1
040efc0ea937        adtd/rest:0.1       "catalina.sh run"      3 minutes ago       Up 2 minutes        10.0.0.4:8080->8080/tcp   swarm-agent-3B7093B8-0/compose_rest_1
```

<span data-ttu-id="16d27-134">Естественно, можно использовать `docker-compose ps` tooexamine только hello контейнеров, определенных в вашей `compose.yml` файла.</span><span class="sxs-lookup"><span data-stu-id="16d27-134">Naturally, you can use `docker-compose ps` tooexamine only hello containers defined in your `compose.yml` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16d27-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="16d27-135">Next steps</span></span>
[<span data-ttu-id="16d27-136">Дополнительные сведения о Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="16d27-136">Learn more about Docker Swarm</span></span>](https://docs.docker.com/swarm/)

