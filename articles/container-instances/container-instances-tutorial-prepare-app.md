---
title: "aaaAzure экземпляры контейнером учебника - Подготовка приложения к | Azure документы"
description: "Подготовка приложения для развертывания tooAzure экземпляры контейнером"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 406ba796e5fefb1527f2e894cc3f7bbd8f7a5fd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-for-deployment-tooazure-container-instances"></a><span data-ttu-id="828a9-103">Создание контейнера для развертывания tooAzure экземпляры контейнером</span><span class="sxs-lookup"><span data-stu-id="828a9-103">Create container for deployment tooAzure Container Instances</span></span>

<span data-ttu-id="828a9-104">Служба "Экземпляры контейнеров Azure" позволяет развертывать контейнеры Docker в инфраструктуре Azure без подготовки виртуальных машин или применения службы более высокого уровня.</span><span class="sxs-lookup"><span data-stu-id="828a9-104">Azure Container Instances enables deployment of Docker containers onto Azure infrastructure without provisioning any virtual machines or adopting any higher-level service.</span></span> <span data-ttu-id="828a9-105">В этом руководстве мы создадим простое веб-приложение на Node.js и упакуем его в контейнер, который можно запустить в службе "Экземпляры контейнеров Azure".</span><span class="sxs-lookup"><span data-stu-id="828a9-105">In this tutorial, you will build a simple web application in Node.js and package it in a container that can be run using Azure Container Instances.</span></span> <span data-ttu-id="828a9-106">Мы рассмотрим:</span><span class="sxs-lookup"><span data-stu-id="828a9-106">We will cover:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="828a9-107">Клонирование источника приложения из GitHub.</span><span class="sxs-lookup"><span data-stu-id="828a9-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="828a9-108">Создание образов контейнеров из источника приложения.</span><span class="sxs-lookup"><span data-stu-id="828a9-108">Creating container images from application source</span></span>
> * <span data-ttu-id="828a9-109">Тестирование изображения hello в локальной среде Docker</span><span class="sxs-lookup"><span data-stu-id="828a9-109">Testing hello images in a local Docker environment</span></span>

<span data-ttu-id="828a9-110">В последующих учебниках можно отправить ваш образ tooan реестра контейнера Azure и развернуть их tooAzure экземпляры контейнером.</span><span class="sxs-lookup"><span data-stu-id="828a9-110">In subsequent tutorials, you will upload your image tooan Azure Container Registry, and then deploy them tooAzure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="828a9-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="828a9-111">Before you begin</span></span>

<span data-ttu-id="828a9-112">Для выполнения действий, описанных в этом руководстве, необходимо базовое понимание основных понятий Docker, таких как контейнеры, образы контейнеров и основные команды Docker.</span><span class="sxs-lookup"><span data-stu-id="828a9-112">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="828a9-113">При необходимости см. статью о [начале работы с Docker]( https://docs.docker.com/get-started/), чтобы ознакомиться с основами работы с контейнерами.</span><span class="sxs-lookup"><span data-stu-id="828a9-113">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="828a9-114">toocomplete этого учебника требуется среда разработки Docker.</span><span class="sxs-lookup"><span data-stu-id="828a9-114">toocomplete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="828a9-115">Docker содержит пакеты, которые позволяют быстро настроить Docker в любой системе [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) или [Linux](https://docs.docker.com/engine/installation/#supported-platforms).</span><span class="sxs-lookup"><span data-stu-id="828a9-115">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="828a9-116">Получение кода приложения</span><span class="sxs-lookup"><span data-stu-id="828a9-116">Get application code</span></span>

<span data-ttu-id="828a9-117">Образец Hello в этом учебнике включает простое веб-приложение [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="828a9-117">hello sample in this tutorial includes a simple web application built in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="828a9-118">приложение Hello служит статических HTML-страницы и выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="828a9-118">hello app serves a static HTML page and looks like this:</span></span>

![Приложение из руководства, отображающееся в браузере][aci-tutorial-app]

<span data-ttu-id="828a9-120">Использование образца hello toodownload git:</span><span class="sxs-lookup"><span data-stu-id="828a9-120">Use git toodownload hello sample:</span></span>

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

## <a name="build-hello-container-image"></a><span data-ttu-id="828a9-121">Создать образ контейнера hello</span><span class="sxs-lookup"><span data-stu-id="828a9-121">Build hello container image</span></span>

<span data-ttu-id="828a9-122">Hello Dockerfile, предоставленный в репозитории образец hello показано построение hello контейнера.</span><span class="sxs-lookup"><span data-stu-id="828a9-122">hello Dockerfile provided in hello sample repo shows how hello container is built.</span></span> <span data-ttu-id="828a9-123">Он начинается с [официальный изображения Node.js] [ dockerhub-nodeimage] на основе [Alpine Linux](https://alpinelinux.org/), небольшой распределение, которое является хорошо подходит toouse с контейнерами.</span><span class="sxs-lookup"><span data-stu-id="828a9-123">It starts from an [official Node.js image][dockerhub-nodeimage] based on [Alpine Linux](https://alpinelinux.org/), a small distribution that is well suited toouse with containers.</span></span> <span data-ttu-id="828a9-124">Затем копирует файлы приложения hello в контейнер hello, устанавливает зависимостей с помощью диспетчера пакетов Node hello и затем запускает приложение hello.</span><span class="sxs-lookup"><span data-stu-id="828a9-124">It then copies hello application files into hello container, installs dependencies using hello Node Package Manager, and finally starts hello application.</span></span>

```
FROM node:8.2.0-alpine
RUN mkdir -p /usr/src/app
COPY ./app/* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

<span data-ttu-id="828a9-125">Используйте hello `docker build` команда toocreate hello образ контейнера, как теги *aci учебника приложения*:</span><span class="sxs-lookup"><span data-stu-id="828a9-125">Use hello `docker build` command toocreate hello container image, tagging it as *aci-tutorial-app*:</span></span>

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

<span data-ttu-id="828a9-126">Используйте hello `docker images` toosee hello построения образа:</span><span class="sxs-lookup"><span data-stu-id="828a9-126">Use hello `docker images` toosee hello built image:</span></span>

```bash
docker images
```

<span data-ttu-id="828a9-127">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="828a9-127">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

## <a name="run-hello-container-locally"></a><span data-ttu-id="828a9-128">Запустите контейнер hello локально</span><span class="sxs-lookup"><span data-stu-id="828a9-128">Run hello container locally</span></span>

<span data-ttu-id="828a9-129">Прежде чем развертывание tooAzure контейнера hello экземпляров контейнера, запустите его локально tooconfirm его работы.</span><span class="sxs-lookup"><span data-stu-id="828a9-129">Before you try deploying hello container tooAzure Container Instances, run it locally tooconfirm that it works.</span></span> <span data-ttu-id="828a9-130">Hello `-d` коммутатора позволяет контейнера hello выполняются в фоновом режиме hello, пока `-p` позволяет toomap порту произвольный вашей вычислений tooport 80 в контейнере hello.</span><span class="sxs-lookup"><span data-stu-id="828a9-130">hello `-d` switch lets hello container run in hello background, while `-p` allows you toomap an arbitrary port on your compute tooport 80 in hello container.</span></span>

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

<span data-ttu-id="828a9-131">Привет открыть браузер toohttp://localhost:8080 tooconfirm, hello контейнер работает под управлением.</span><span class="sxs-lookup"><span data-stu-id="828a9-131">Open hello browser toohttp://localhost:8080 tooconfirm that hello container is running.</span></span>

![Выполняемого приложения hello локально в браузере hello][aci-tutorial-app-local]

## <a name="next-steps"></a><span data-ttu-id="828a9-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="828a9-133">Next steps</span></span>

<span data-ttu-id="828a9-134">В этом учебнике вы создали образа контейнера, который может быть экземпляров развернутых tooAzure контейнера.</span><span class="sxs-lookup"><span data-stu-id="828a9-134">In this tutorial, you created a container image that can be deployed tooAzure Container Instances.</span></span> <span data-ttu-id="828a9-135">Привет, следующие шаги были выполнены:</span><span class="sxs-lookup"><span data-stu-id="828a9-135">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="828a9-136">Клонирование источника приложения hello из GitHub</span><span class="sxs-lookup"><span data-stu-id="828a9-136">Cloning hello application source from GitHub</span></span>  
> * <span data-ttu-id="828a9-137">Создание образов контейнеров из источника приложения.</span><span class="sxs-lookup"><span data-stu-id="828a9-137">Creating container images from application source</span></span>
> * <span data-ttu-id="828a9-138">Тестирование локально контейнера hello</span><span class="sxs-lookup"><span data-stu-id="828a9-138">Testing hello container locally</span></span>

<span data-ttu-id="828a9-139">Переместить следующий учебник toolearn toohello о хранении образы контейнеров в контейнер Azure реестра.</span><span class="sxs-lookup"><span data-stu-id="828a9-139">Advance toohello next tutorial toolearn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="828a9-140">Принудительная tooAzure образов контейнера реестра</span><span class="sxs-lookup"><span data-stu-id="828a9-140">Push images tooAzure Container Registry</span></span>](./container-instances-tutorial-prepare-acr.md)

<!-- LINKS -->
[dockerhub-nodeimage]: https://hub.docker.com/r/library/node/tags/8.2.0-alpine/

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png