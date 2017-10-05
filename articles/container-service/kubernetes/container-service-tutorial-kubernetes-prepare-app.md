---
title: "Руководство по службе контейнеров Azure — подготовка приложения | Документация Майкрософт"
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
ms.openlocfilehash: f02ee61ef1cd3b3dfaa051cfabe52866e3e7e838
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-container-images-to-be-used-with-azure-container-service"></a><span data-ttu-id="98a2a-104">Создание образов контейнеров для использования со службой контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="98a2a-104">Create container images to be used with Azure Container Service</span></span>

<span data-ttu-id="98a2a-105">В этом руководстве (часть 1 из 7) выполняется подготовка многоконтейнерного приложения к использованию в Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="98a2a-105">In this tutorial, part one of seven, a multi-container application is prepared for use in Kubernetes.</span></span> <span data-ttu-id="98a2a-106">В частности, рассматриваются такие шаги:</span><span class="sxs-lookup"><span data-stu-id="98a2a-106">Steps completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="98a2a-107">Клонирование источника приложения из GitHub.</span><span class="sxs-lookup"><span data-stu-id="98a2a-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="98a2a-108">Создание образа контейнера из источника приложения.</span><span class="sxs-lookup"><span data-stu-id="98a2a-108">Creating a container image from the application source</span></span>
> * <span data-ttu-id="98a2a-109">Тестирование приложения в локальной среде Docker.</span><span class="sxs-lookup"><span data-stu-id="98a2a-109">Testing the application in a local Docker environment</span></span>

<span data-ttu-id="98a2a-110">После выполнения всех действий в вашей локальной среде разработки станет доступным следующее приложение:</span><span class="sxs-lookup"><span data-stu-id="98a2a-110">Once completed, the following application is accessible in your local development environment.</span></span>

![Схема кластера Kubernetes в Аzure](media/container-service-kubernetes-tutorials/azure-vote.png)

<span data-ttu-id="98a2a-112">В последующих руководствах образ контейнера передается в реестр контейнеров Azure, а затем выполняется в кластере Kubernetes, размещенном в Azure.</span><span class="sxs-lookup"><span data-stu-id="98a2a-112">In subsequent tutorials, the container image is uploaded to an Azure Container Registry, and then run in an Azure hosted Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="98a2a-113">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="98a2a-113">Before you begin</span></span>

<span data-ttu-id="98a2a-114">Для выполнения действий, описанных в этом руководстве, необходимо базовое понимание основных понятий Docker, таких как контейнеры, образы контейнеров и основные команды Docker.</span><span class="sxs-lookup"><span data-stu-id="98a2a-114">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="98a2a-115">При необходимости см. статью о [начале работы с Docker]( https://docs.docker.com/get-started/), чтобы ознакомиться с основами работы с контейнерами.</span><span class="sxs-lookup"><span data-stu-id="98a2a-115">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="98a2a-116">Для работы с этим руководством требуется среда разработки Docker.</span><span class="sxs-lookup"><span data-stu-id="98a2a-116">To complete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="98a2a-117">Docker содержит пакеты, которые позволяют быстро настроить Docker в любой системе [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) или [Linux](https://docs.docker.com/engine/installation/#supported-platforms).</span><span class="sxs-lookup"><span data-stu-id="98a2a-117">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="98a2a-118">Получение кода приложения</span><span class="sxs-lookup"><span data-stu-id="98a2a-118">Get application code</span></span>

<span data-ttu-id="98a2a-119">В этом руководстве используется простое приложение для голосования.</span><span class="sxs-lookup"><span data-stu-id="98a2a-119">The sample application used in this tutorial is a basic voting app.</span></span> <span data-ttu-id="98a2a-120">Приложение состоит из веб-компонента интерфейсной части и серверного экземпляра Redis.</span><span class="sxs-lookup"><span data-stu-id="98a2a-120">The application consists of a front-end web component and a back-end Redis instance.</span></span> <span data-ttu-id="98a2a-121">Веб-компонент упаковывается в пользовательский образ контейнера,</span><span class="sxs-lookup"><span data-stu-id="98a2a-121">The web component is packaged into a custom container image.</span></span> <span data-ttu-id="98a2a-122">а для экземпляра Redis используется неизмененный образ из Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="98a2a-122">The Redis instance uses an unmodified image from Docker Hub.</span></span>  

<span data-ttu-id="98a2a-123">Используйте git, чтобы скачать копию приложения в среду разработки.</span><span class="sxs-lookup"><span data-stu-id="98a2a-123">Use git to download a copy of the application to your development environment.</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="98a2a-124">Внутри клонированного каталога содержится исходный код приложения, предварительно созданный файл Docker Compose, а также файл манифеста Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="98a2a-124">Inside the cloned directory is the application source code, a pre-created Docker compose file, and a Kubernetes manifest file.</span></span> <span data-ttu-id="98a2a-125">Эти файлы используются для создания ресурсов в руководстве.</span><span class="sxs-lookup"><span data-stu-id="98a2a-125">These files are used to create assets throughout the tutorial set.</span></span> 

## <a name="create-container-images"></a><span data-ttu-id="98a2a-126">Создание образов контейнеров</span><span class="sxs-lookup"><span data-stu-id="98a2a-126">Create container images</span></span>

<span data-ttu-id="98a2a-127">С помощью [Docker Compose](https://docs.docker.com/compose/) можно автоматизировать создание дополнительных образов контейнеров и развертывание многоконтейнерных приложений.</span><span class="sxs-lookup"><span data-stu-id="98a2a-127">[Docker Compose](https://docs.docker.com/compose/) can be used to automate the build out of container images and the deployment of multi-container applications.</span></span>

<span data-ttu-id="98a2a-128">Выполните файл docker-compose.yml, чтобы создать образ контейнера, скачать образ Redis и запустить приложение.</span><span class="sxs-lookup"><span data-stu-id="98a2a-128">Run the docker-compose.yml file to create the container image, download the Redis image, and start the application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up -d
```

<span data-ttu-id="98a2a-129">После завершения выполните команду [docker images](https://docs.docker.com/engine/reference/commandline/images/), чтобы увидеть созданные образы.</span><span class="sxs-lookup"><span data-stu-id="98a2a-129">When completed, use the [docker images](https://docs.docker.com/engine/reference/commandline/images/) command to see the created images.</span></span>

```bash
docker images
```

<span data-ttu-id="98a2a-130">Вы увидите, что были скачаны или созданы три образа.</span><span class="sxs-lookup"><span data-stu-id="98a2a-130">Notice that three images have been downloaded or created.</span></span> <span data-ttu-id="98a2a-131">Образ *azure-vote-front* содержит приложение.</span><span class="sxs-lookup"><span data-stu-id="98a2a-131">The *azure-vote-front* image contains the application.</span></span> <span data-ttu-id="98a2a-132">Он был создан на основе образа *nginx-flask*.</span><span class="sxs-lookup"><span data-stu-id="98a2a-132">It was derived from the *nginx-flask* image.</span></span> <span data-ttu-id="98a2a-133">Образ Redis был скачан из Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="98a2a-133">The Redis image was downloaded from Docker Hub.</span></span>

```bash
REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="98a2a-134">Выполните команду [docker ps](https://docs.docker.com/engine/reference/commandline/ps/), чтобы просмотреть выполняемые контейнеры.</span><span class="sxs-lookup"><span data-stu-id="98a2a-134">Run the [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) command to see the running containers.</span></span>

```bash
docker ps
```

<span data-ttu-id="98a2a-135">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="98a2a-135">Output:</span></span>

```bash
CONTAINER ID        IMAGE             COMMAND                  CREATED             STATUS              PORTS                           NAMES
82411933e8f9        azure-vote-front  "/usr/bin/supervisord"   57 seconds ago      Up 30 seconds       443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
b68fed4b66b6        redis             "docker-entrypoint..."   57 seconds ago      Up 30 seconds       0.0.0.0:6379->6379/tcp          azure-vote-back
```

## <a name="test-application-locally"></a><span data-ttu-id="98a2a-136">Локальное тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="98a2a-136">Test application locally</span></span>

<span data-ttu-id="98a2a-137">Перейдите по адресу http://localhost:8080, чтобы просмотреть запущенное приложение.</span><span class="sxs-lookup"><span data-stu-id="98a2a-137">Browse to http://localhost:8080 to see the running application.</span></span>

![Схема кластера Kubernetes в Аzure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="clean-up-resources"></a><span data-ttu-id="98a2a-139">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="98a2a-139">Clean up resources</span></span>

<span data-ttu-id="98a2a-140">Теперь, когда функциональные возможности приложения проверены, запущенные контейнеры можно остановить и удалить.</span><span class="sxs-lookup"><span data-stu-id="98a2a-140">Now that application functionality has been validated, the running containers can be stopped and removed.</span></span> <span data-ttu-id="98a2a-141">Не удаляйте образы контейнеров.</span><span class="sxs-lookup"><span data-stu-id="98a2a-141">Do not delete the container images.</span></span> <span data-ttu-id="98a2a-142">Образ *azure-vote-front* будет отправлен в экземпляр реестра контейнеров Azure в следующем руководстве.</span><span class="sxs-lookup"><span data-stu-id="98a2a-142">The *azure-vote-front* image is uploaded to an Azure Container Registry instance in the next tutorial.</span></span>

<span data-ttu-id="98a2a-143">Чтобы остановить запущенные контейнеры, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="98a2a-143">Run the following to stop the running containers.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml stop
```

<span data-ttu-id="98a2a-144">Чтобы удалить остановленные контейнеры, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="98a2a-144">Delete the stopped containers with the following command.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml rm
```

<span data-ttu-id="98a2a-145">По завершении у вас будет образ контейнера, содержащий приложение Azure Vote.</span><span class="sxs-lookup"><span data-stu-id="98a2a-145">At completion, you have a container image that contains the Azure Vote application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98a2a-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="98a2a-146">Next steps</span></span>

<span data-ttu-id="98a2a-147">В этом руководстве вы протестировали приложение и создали для него образы контейнеров.</span><span class="sxs-lookup"><span data-stu-id="98a2a-147">In this tutorial, an application was tested and container images created for the application.</span></span> <span data-ttu-id="98a2a-148">Были выполнены следующие действия:</span><span class="sxs-lookup"><span data-stu-id="98a2a-148">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="98a2a-149">Клонирование источника приложения из GitHub.</span><span class="sxs-lookup"><span data-stu-id="98a2a-149">Cloning the application source from GitHub</span></span>  
> * <span data-ttu-id="98a2a-150">Создание образа контейнера из источника приложения.</span><span class="sxs-lookup"><span data-stu-id="98a2a-150">Created a container image from application source</span></span>
> * <span data-ttu-id="98a2a-151">Тестирование приложения в локальной среде Docker.</span><span class="sxs-lookup"><span data-stu-id="98a2a-151">Tested the application in a local Docker environment</span></span>

<span data-ttu-id="98a2a-152">Переходите к следующему руководству, чтобы узнать о хранении образов контейнеров в реестре контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="98a2a-152">Advance to the next tutorial to learn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="98a2a-153">Развертывание реестра контейнеров Azure и его использование</span><span class="sxs-lookup"><span data-stu-id="98a2a-153">Push images to Azure Container Registry</span></span>](./container-service-tutorial-kubernetes-prepare-acr.md)