---
title: "Учебник контейнера службы aaaAzure - Подготовка приложения | Документы Microsoft"
description: "Руководство по службе контейнеров Azure — подготовка приложения"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b537ecc9ff50358fb65b128bfe6eb894dd088cc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-images-toobe-used-with-azure-container-service"></a>Создание контейнера изображения toobe со службой контейнера Azure

В этом руководстве (часть 1 из 7) выполняется подготовка многоконтейнерного приложения к использованию в Kubernetes. В частности, рассматриваются такие шаги:  

> [!div class="checklist"]
> * Клонирование источника приложения из GitHub.  
> * Создание образа контейнера на основе источника приложения hello
> * Тестирование приложения hello в локальной среде Docker

После завершения следующие приложения hello доступен в локальной среде разработки.

![Схема кластера Kubernetes в Аzure](media/container-service-kubernetes-tutorials/azure-vote.png)

В последующих учебники hello образ контейнера — отправленного tooan реестра контейнера Azure, а затем запуска в Azure размещенных Kubernetes кластера.

## <a name="before-you-begin"></a>Перед началом работы

Для выполнения действий, описанных в этом руководстве, необходимо базовое понимание основных понятий Docker, таких как контейнеры, образы контейнеров и основные команды Docker. При необходимости см. статью о [начале работы с Docker]( https://docs.docker.com/get-started/), чтобы ознакомиться с основами работы с контейнерами. 

toocomplete этого учебника требуется среда разработки Docker. Docker содержит пакеты, которые позволяют быстро настроить Docker в любой системе [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) или [Linux](https://docs.docker.com/engine/installation/#supported-platforms).

## <a name="get-application-code"></a>Получение кода приложения

Пример приложения Hello, используемые в этом учебнике будет голосования базовое приложение. приложение Hello состоит из интерфейсный веб-компонент и экземпляр Redis серверной части. веб-компонент Hello упаковывается в пользовательские образы. экземпляр Hello Redis использует неизмененного образ из Docker Hub.  

Используйте git toodownload копии среды разработки tooyour приложения hello.

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

Точная копия каталога внутри hello исходный код приложения hello, предварительно созданную Docker compose файл и файл манифеста Kubernetes. Эти файлы, используемые toocreate активы hello учебника по набору. 

## <a name="create-container-images"></a>Создание образов контейнеров

[Docker Compose](https://docs.docker.com/compose/) можно использовать tooautomate hello сборки из образов контейнеров и hello развертывание нескольких контейнера приложений.

Запустить hello hello docker compose.yml файл toocreate образ контейнера, hello загрузки Redis образ и запустите приложение hello.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up -d
```

После завершения использования hello [образов docker](https://docs.docker.com/engine/reference/commandline/images/) команды toosee hello создания образов.

```bash
docker images
```

Вы увидите, что были скачаны или созданы три образа. Hello *azure голос передней панели* образ содержит приложение hello. Он был производным от hello *nginx термосе* изображения. изображение Redis Hello была загружена из Docker Hub.

```bash
REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

Запустите hello [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) команда toosee hello запущенных контейнеров.

```bash
docker ps
```

Выходные данные:

```bash
CONTAINER ID        IMAGE             COMMAND                  CREATED             STATUS              PORTS                           NAMES
82411933e8f9        azure-vote-front  "/usr/bin/supervisord"   57 seconds ago      Up 30 seconds       443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
b68fed4b66b6        redis             "docker-entrypoint..."   57 seconds ago      Up 30 seconds       0.0.0.0:6379->6379/tcp          azure-vote-back
```

## <a name="test-application-locally"></a>Локальное тестирование приложения

Обзор hello toosee toohttp://localhost:8080 запущено приложение.

![Схема кластера Kubernetes в Аzure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="clean-up-resources"></a>Очистка ресурсов

Теперь, когда был проверен функциональных возможностей приложения hello запущенные контейнеры можно останавливать и удалены. Не удаляйте hello образы контейнеров. Hello *azure голос передней панели* изображения — экземпляр отправленного tooan реестра контейнера Azure в следующем уроке hello.

Запустите следующие hello toostop запущенные контейнеры hello.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml stop
```

Удаление контейнеров hello остановлена с hello следующую команду.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml rm
```

По завершении у вас есть образ контейнера, содержащего приложение hello Azure голос.

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике приложения было проверено и образы контейнеров, созданного для приложения hello. Привет, следующие шаги были выполнены:

> [!div class="checklist"]
> * Клонирование источника приложения hello из GitHub  
> * Создание образа контейнера из источника приложения.
> * Протестированные hello приложения в локальной среде Docker

Переместить следующий учебник toolearn toohello о хранении образы контейнеров в контейнер Azure реестра.

> [!div class="nextstepaction"]
> [Принудительная tooAzure образов контейнера реестра](./container-service-tutorial-kubernetes-prepare-acr.md)
