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
# <a name="create-container-images-toobe-used-with-azure-container-service"></a><span data-ttu-id="abc96-104">Создание контейнера изображения toobe со службой контейнера Azure</span><span class="sxs-lookup"><span data-stu-id="abc96-104">Create container images toobe used with Azure Container Service</span></span>

<span data-ttu-id="abc96-105">В этом руководстве (часть 1 из 7) выполняется подготовка многоконтейнерного приложения к использованию в Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="abc96-105">In this tutorial, part one of seven, a multi-container application is prepared for use in Kubernetes.</span></span> <span data-ttu-id="abc96-106">В частности, рассматриваются такие шаги:</span><span class="sxs-lookup"><span data-stu-id="abc96-106">Steps completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="abc96-107">Клонирование источника приложения из GitHub.</span><span class="sxs-lookup"><span data-stu-id="abc96-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="abc96-108">Создание образа контейнера на основе источника приложения hello</span><span class="sxs-lookup"><span data-stu-id="abc96-108">Creating a container image from hello application source</span></span>
> * <span data-ttu-id="abc96-109">Тестирование приложения hello в локальной среде Docker</span><span class="sxs-lookup"><span data-stu-id="abc96-109">Testing hello application in a local Docker environment</span></span>

<span data-ttu-id="abc96-110">После завершения следующие приложения hello доступен в локальной среде разработки.</span><span class="sxs-lookup"><span data-stu-id="abc96-110">Once completed, hello following application is accessible in your local development environment.</span></span>

![Схема кластера Kubernetes в Аzure](media/container-service-kubernetes-tutorials/azure-vote.png)

<span data-ttu-id="abc96-112">В последующих учебники hello образ контейнера — отправленного tooan реестра контейнера Azure, а затем запуска в Azure размещенных Kubernetes кластера.</span><span class="sxs-lookup"><span data-stu-id="abc96-112">In subsequent tutorials, hello container image is uploaded tooan Azure Container Registry, and then run in an Azure hosted Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="abc96-113">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="abc96-113">Before you begin</span></span>

<span data-ttu-id="abc96-114">Для выполнения действий, описанных в этом руководстве, необходимо базовое понимание основных понятий Docker, таких как контейнеры, образы контейнеров и основные команды Docker.</span><span class="sxs-lookup"><span data-stu-id="abc96-114">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="abc96-115">При необходимости см. статью о [начале работы с Docker]( https://docs.docker.com/get-started/), чтобы ознакомиться с основами работы с контейнерами.</span><span class="sxs-lookup"><span data-stu-id="abc96-115">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="abc96-116">toocomplete этого учебника требуется среда разработки Docker.</span><span class="sxs-lookup"><span data-stu-id="abc96-116">toocomplete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="abc96-117">Docker содержит пакеты, которые позволяют быстро настроить Docker в любой системе [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) или [Linux](https://docs.docker.com/engine/installation/#supported-platforms).</span><span class="sxs-lookup"><span data-stu-id="abc96-117">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="abc96-118">Получение кода приложения</span><span class="sxs-lookup"><span data-stu-id="abc96-118">Get application code</span></span>

<span data-ttu-id="abc96-119">Пример приложения Hello, используемые в этом учебнике будет голосования базовое приложение.</span><span class="sxs-lookup"><span data-stu-id="abc96-119">hello sample application used in this tutorial is a basic voting app.</span></span> <span data-ttu-id="abc96-120">приложение Hello состоит из интерфейсный веб-компонент и экземпляр Redis серверной части.</span><span class="sxs-lookup"><span data-stu-id="abc96-120">hello application consists of a front-end web component and a back-end Redis instance.</span></span> <span data-ttu-id="abc96-121">веб-компонент Hello упаковывается в пользовательские образы.</span><span class="sxs-lookup"><span data-stu-id="abc96-121">hello web component is packaged into a custom container image.</span></span> <span data-ttu-id="abc96-122">экземпляр Hello Redis использует неизмененного образ из Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="abc96-122">hello Redis instance uses an unmodified image from Docker Hub.</span></span>  

<span data-ttu-id="abc96-123">Используйте git toodownload копии среды разработки tooyour приложения hello.</span><span class="sxs-lookup"><span data-stu-id="abc96-123">Use git toodownload a copy of hello application tooyour development environment.</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="abc96-124">Точная копия каталога внутри hello исходный код приложения hello, предварительно созданную Docker compose файл и файл манифеста Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="abc96-124">Inside hello cloned directory is hello application source code, a pre-created Docker compose file, and a Kubernetes manifest file.</span></span> <span data-ttu-id="abc96-125">Эти файлы, используемые toocreate активы hello учебника по набору.</span><span class="sxs-lookup"><span data-stu-id="abc96-125">These files are used toocreate assets throughout hello tutorial set.</span></span> 

## <a name="create-container-images"></a><span data-ttu-id="abc96-126">Создание образов контейнеров</span><span class="sxs-lookup"><span data-stu-id="abc96-126">Create container images</span></span>

<span data-ttu-id="abc96-127">[Docker Compose](https://docs.docker.com/compose/) можно использовать tooautomate hello сборки из образов контейнеров и hello развертывание нескольких контейнера приложений.</span><span class="sxs-lookup"><span data-stu-id="abc96-127">[Docker Compose](https://docs.docker.com/compose/) can be used tooautomate hello build out of container images and hello deployment of multi-container applications.</span></span>

<span data-ttu-id="abc96-128">Запустить hello hello docker compose.yml файл toocreate образ контейнера, hello загрузки Redis образ и запустите приложение hello.</span><span class="sxs-lookup"><span data-stu-id="abc96-128">Run hello docker-compose.yml file toocreate hello container image, download hello Redis image, and start hello application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up -d
```

<span data-ttu-id="abc96-129">После завершения использования hello [образов docker](https://docs.docker.com/engine/reference/commandline/images/) команды toosee hello создания образов.</span><span class="sxs-lookup"><span data-stu-id="abc96-129">When completed, use hello [docker images](https://docs.docker.com/engine/reference/commandline/images/) command toosee hello created images.</span></span>

```bash
docker images
```

<span data-ttu-id="abc96-130">Вы увидите, что были скачаны или созданы три образа.</span><span class="sxs-lookup"><span data-stu-id="abc96-130">Notice that three images have been downloaded or created.</span></span> <span data-ttu-id="abc96-131">Hello *azure голос передней панели* образ содержит приложение hello.</span><span class="sxs-lookup"><span data-stu-id="abc96-131">hello *azure-vote-front* image contains hello application.</span></span> <span data-ttu-id="abc96-132">Он был производным от hello *nginx термосе* изображения.</span><span class="sxs-lookup"><span data-stu-id="abc96-132">It was derived from hello *nginx-flask* image.</span></span> <span data-ttu-id="abc96-133">изображение Redis Hello была загружена из Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="abc96-133">hello Redis image was downloaded from Docker Hub.</span></span>

```bash
REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="abc96-134">Запустите hello [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) команда toosee hello запущенных контейнеров.</span><span class="sxs-lookup"><span data-stu-id="abc96-134">Run hello [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) command toosee hello running containers.</span></span>

```bash
docker ps
```

<span data-ttu-id="abc96-135">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="abc96-135">Output:</span></span>

```bash
CONTAINER ID        IMAGE             COMMAND                  CREATED             STATUS              PORTS                           NAMES
82411933e8f9        azure-vote-front  "/usr/bin/supervisord"   57 seconds ago      Up 30 seconds       443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
b68fed4b66b6        redis             "docker-entrypoint..."   57 seconds ago      Up 30 seconds       0.0.0.0:6379->6379/tcp          azure-vote-back
```

## <a name="test-application-locally"></a><span data-ttu-id="abc96-136">Локальное тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="abc96-136">Test application locally</span></span>

<span data-ttu-id="abc96-137">Обзор hello toosee toohttp://localhost:8080 запущено приложение.</span><span class="sxs-lookup"><span data-stu-id="abc96-137">Browse toohttp://localhost:8080 toosee hello running application.</span></span>

![Схема кластера Kubernetes в Аzure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="clean-up-resources"></a><span data-ttu-id="abc96-139">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="abc96-139">Clean up resources</span></span>

<span data-ttu-id="abc96-140">Теперь, когда был проверен функциональных возможностей приложения hello запущенные контейнеры можно останавливать и удалены.</span><span class="sxs-lookup"><span data-stu-id="abc96-140">Now that application functionality has been validated, hello running containers can be stopped and removed.</span></span> <span data-ttu-id="abc96-141">Не удаляйте hello образы контейнеров.</span><span class="sxs-lookup"><span data-stu-id="abc96-141">Do not delete hello container images.</span></span> <span data-ttu-id="abc96-142">Hello *azure голос передней панели* изображения — экземпляр отправленного tooan реестра контейнера Azure в следующем уроке hello.</span><span class="sxs-lookup"><span data-stu-id="abc96-142">hello *azure-vote-front* image is uploaded tooan Azure Container Registry instance in hello next tutorial.</span></span>

<span data-ttu-id="abc96-143">Запустите следующие hello toostop запущенные контейнеры hello.</span><span class="sxs-lookup"><span data-stu-id="abc96-143">Run hello following toostop hello running containers.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml stop
```

<span data-ttu-id="abc96-144">Удаление контейнеров hello остановлена с hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="abc96-144">Delete hello stopped containers with hello following command.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml rm
```

<span data-ttu-id="abc96-145">По завершении у вас есть образ контейнера, содержащего приложение hello Azure голос.</span><span class="sxs-lookup"><span data-stu-id="abc96-145">At completion, you have a container image that contains hello Azure Vote application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="abc96-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="abc96-146">Next steps</span></span>

<span data-ttu-id="abc96-147">В этом учебнике приложения было проверено и образы контейнеров, созданного для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="abc96-147">In this tutorial, an application was tested and container images created for hello application.</span></span> <span data-ttu-id="abc96-148">Привет, следующие шаги были выполнены:</span><span class="sxs-lookup"><span data-stu-id="abc96-148">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="abc96-149">Клонирование источника приложения hello из GitHub</span><span class="sxs-lookup"><span data-stu-id="abc96-149">Cloning hello application source from GitHub</span></span>  
> * <span data-ttu-id="abc96-150">Создание образа контейнера из источника приложения.</span><span class="sxs-lookup"><span data-stu-id="abc96-150">Created a container image from application source</span></span>
> * <span data-ttu-id="abc96-151">Протестированные hello приложения в локальной среде Docker</span><span class="sxs-lookup"><span data-stu-id="abc96-151">Tested hello application in a local Docker environment</span></span>

<span data-ttu-id="abc96-152">Переместить следующий учебник toolearn toohello о хранении образы контейнеров в контейнер Azure реестра.</span><span class="sxs-lookup"><span data-stu-id="abc96-152">Advance toohello next tutorial toolearn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="abc96-153">Принудительная tooAzure образов контейнера реестра</span><span class="sxs-lookup"><span data-stu-id="abc96-153">Push images tooAzure Container Registry</span></span>](./container-service-tutorial-kubernetes-prepare-acr.md)
