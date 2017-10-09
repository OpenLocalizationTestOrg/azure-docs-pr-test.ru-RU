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
# <a name="container-management-with-docker-swarm"></a>Управление контейнерами с помощью Docker Swarm
Docker Swarm — это среда для развертывания контейнерной рабочей нагрузки в наборе узлов, объединенных в пул Docker. Группу мелких объектов docker использует hello собственного API Docker. Hello рабочего процесса управления контейнерами в помощью Docker Swarm имеет почти такую же toowhat, которое было бы на одном узле контейнера. Этот документ содержит простые примеры развертывания контейнерной рабочей нагрузки в экземпляре Docker Swarm, который развернут в службе контейнеров Azure. Дополнительные сведения о Docker Swarm см. в [документации по Docker Swarm на сайте Docker.com](https://docs.docker.com/swarm/).

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

Предварительные требования toohello упражнений данного документа:

[Создайте кластер Swarm в службе контейнеров Azure.](container-service-deployment.md)

[Подключение с кластером hello группу мелких объектов в контейнере службы Azure](../container-service-connect.md)

## <a name="deploy-a-new-container"></a>Развертывание нового контейнера
новый контейнер hello с помощью Docker Swarm toocreate использовать hello `docker run` команда (гарантирует, что вы открыли образцов toohello туннель SSH, согласно hello указанные выше предварительные условия). Этот пример создает контейнер из hello `yeasy/simple-web` изображения:

```bash
user@ubuntu:~$ docker run -d -p 80:80 yeasy/simple-web

4298d397b9ab6f37e2d1978ef3c8c1537c938e98a8bf096ff00def2eab04bf72
```

После создания контейнера hello `docker ps` tooreturn сведения о контейнере hello. Здесь, обратите внимание, что этот агент группу мелких объектов hello, на котором размещается контейнер hello отображается:

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   31 seconds ago      Up 9 seconds        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

Теперь можно получить доступ к hello приложение, которое выполняется в этом контейнере через hello общее DNS-имя подсистемы балансировки нагрузки агента hello группу мелких объектов. Эти сведения можно найти в hello портала Azure:  

![Результаты реального посещения](./media/container-service-docker-swarm/real-visit.jpg)  

По умолчанию hello балансировки нагрузки имеет порты 80 и открыть 8080 и 443. Если требуется, чтобы tooconnect на другой порт потребуется tooopen этот порт на hello подсистемы балансировки нагрузки Azure для hello пул агентов.

## <a name="deploy-multiple-containers"></a>Развертывание нескольких контейнеров
Запускаются несколько контейнеров, выполнив «docker выполнения» несколько раз, можно использовать hello `docker ps` toosee команду, где размещается hello контейнеров, выполняющихся на. В следующем примере hello три контейнера равномерно распределены по hello три агента группу мелких объектов:  

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
11be062ff602        yeasy/simple-web    "/bin/sh -c 'python i"   11 seconds ago      Up 10 seconds       10.0.0.6:83->80/tcp   swarm-agent-34A73819-2/clever_banach
1ff421554c50        yeasy/simple-web    "/bin/sh -c 'python i"   49 seconds ago      Up 48 seconds       10.0.0.4:82->80/tcp   swarm-agent-34A73819-0/stupefied_ride
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   2 minutes ago       Up 2 minutes        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

## <a name="deploy-containers-by-using-docker-compose"></a>Развертывание контейнеров с помощью Docker Compose
Можно использовать Docker Compose tooautomate hello развертывание и настройку несколько контейнеров. toodo таким образом, убедитесь, что для туннеля Secure Shell (SSH) будет создана, так и для задания этой переменной DOCKER_HOST hello (см. раздел предварительных требований hello выше).

Создайте на локальной системе файл docker-compose.yml. toodo, этот метод следует использовать [пример](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).

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

Запустите `docker-compose up -d` развертывания контейнера hello toostart:

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

Наконец будет возвращаться hello списка запущенных контейнеров. Этот список содержит hello контейнеров, которые были развернуты с помощью Docker Compose:

```bash
user@ubuntu:~/compose$ docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS                     NAMES
caf185d221b7        adtd/web:0.1        "apache2-foreground"   2 minutes ago       Up About a minute   10.0.0.4:80->80/tcp       swarm-agent-3B7093B8-0/compose_web_1
040efc0ea937        adtd/rest:0.1       "catalina.sh run"      3 minutes ago       Up 2 minutes        10.0.0.4:8080->8080/tcp   swarm-agent-3B7093B8-0/compose_rest_1
```

Естественно, можно использовать `docker-compose ps` tooexamine только hello контейнеров, определенных в вашей `compose.yml` файла.

## <a name="next-steps"></a>Дальнейшие действия
[Дополнительные сведения о Docker Swarm](https://docs.docker.com/swarm/)

