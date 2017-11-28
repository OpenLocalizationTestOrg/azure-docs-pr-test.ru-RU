---
title: "Учебник экземпляры контейнером aaaAzure - развертывание приложения | Документы Microsoft"
description: "Руководство по службе \"Экземпляры контейнеров Azure\". Развертывание приложения"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b9fb098d9491e1073f0be4b14a0b9b1a18f16095
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-tooazure-container-instances"></a><span data-ttu-id="64bd0-103">Разверните контейнер tooAzure экземпляры контейнером</span><span class="sxs-lookup"><span data-stu-id="64bd0-103">Deploy a container tooAzure Container Instances</span></span>

<span data-ttu-id="64bd0-104">Это hello последнего учебника трех частей.</span><span class="sxs-lookup"><span data-stu-id="64bd0-104">This is hello last of a three-part tutorial.</span></span> <span data-ttu-id="64bd0-105">В предыдущих разделах [был создан образ контейнера](container-instances-tutorial-prepare-app.md) и [помещается tooan реестра контейнера Azure](container-instances-tutorial-prepare-acr.md).</span><span class="sxs-lookup"><span data-stu-id="64bd0-105">In previous sections, [a container image was created](container-instances-tutorial-prepare-app.md) and [pushed tooan Azure Container Registry](container-instances-tutorial-prepare-acr.md).</span></span> <span data-ttu-id="64bd0-106">В этом разделе завершает учебник hello, развернув контейнер hello tooAzure экземпляры контейнером.</span><span class="sxs-lookup"><span data-stu-id="64bd0-106">This section completes hello tutorial by deploying hello container tooAzure Container Instances.</span></span> <span data-ttu-id="64bd0-107">В частности, рассматриваются такие шаги:</span><span class="sxs-lookup"><span data-stu-id="64bd0-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="64bd0-108">Определение группы контейнеров с использованием шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="64bd0-108">Defining a container group using an Azure Resource Manager template</span></span>
> * <span data-ttu-id="64bd0-109">Развертывание группы hello контейнера, с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="64bd0-109">Deploying hello container group using hello Azure CLI</span></span>
> * <span data-ttu-id="64bd0-110">Просмотр журналов контейнера</span><span class="sxs-lookup"><span data-stu-id="64bd0-110">Viewing container logs</span></span>

## <a name="deploy-hello-container-using-hello-azure-cli"></a><span data-ttu-id="64bd0-111">Развертывание с помощью Azure CLI hello контейнера hello</span><span class="sxs-lookup"><span data-stu-id="64bd0-111">Deploy hello container using hello Azure CLI</span></span>

<span data-ttu-id="64bd0-112">Hello Azure CLI обеспечивает развертывание контейнера tooAzure экземпляры контейнером с помощью одной команды.</span><span class="sxs-lookup"><span data-stu-id="64bd0-112">hello Azure CLI enables deployment of a container tooAzure Container Instances in a single command.</span></span> <span data-ttu-id="64bd0-113">Поскольку образ контейнера hello размещается в hello частного реестра контейнера Azure, следует включить tooaccess необходимые учетные данные hello его.</span><span class="sxs-lookup"><span data-stu-id="64bd0-113">Since hello container image is hosted in hello private Azure Container Registry, you must include hello credentials required tooaccess it.</span></span> <span data-ttu-id="64bd0-114">При необходимости их можно запросить, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="64bd0-114">If necessary, you can query them as shown below.</span></span>

<span data-ttu-id="64bd0-115">Сервер входа в реестр контейнеров (укажите используемое имя реестра):</span><span class="sxs-lookup"><span data-stu-id="64bd0-115">Container registry login server (update with your registry name):</span></span>

```azurecli-interactive
az acr show --name <acrName> --query loginServer
```

<span data-ttu-id="64bd0-116">Пароль для реестра контейнеров:</span><span class="sxs-lookup"><span data-stu-id="64bd0-116">Container registry password:</span></span>

```azurecli-interactive
az acr credential show --name <acrName> --query "passwords[0].value"
```

<span data-ttu-id="64bd0-117">toodeploy образ контейнера из реестра hello контейнера с ресурсом запрос 1 ядра Процессора и 1 ГБ памяти, запустите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="64bd0-117">toodeploy your container image from hello container registry with a resource request of 1 CPU core and 1GB of memory, run hello following command:</span></span>

```azurecli-interactive
az container create --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-password <acrPassword> --ip-address public -g myResourceGroup
```

<span data-ttu-id="64bd0-118">В течение нескольких секунд вы получите исходный ответ Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="64bd0-118">Within a few seconds, you will receive an initial response from Azure Resource Manager.</span></span> <span data-ttu-id="64bd0-119">состояние hello tooview hello развертывания, используйте:</span><span class="sxs-lookup"><span data-stu-id="64bd0-119">tooview hello state of hello deployment, use:</span></span>

```azurecli-interactive
az container show --name aci-tutorial-app --resource-group myResourceGroup --query state
```

<span data-ttu-id="64bd0-120">Мы можем продолжать выполнение этой команды, пока не изменится состояние hello из *ожидающие* слишком*под управлением*.</span><span class="sxs-lookup"><span data-stu-id="64bd0-120">We can continue running this command until hello state changes from *pending* too*running*.</span></span> <span data-ttu-id="64bd0-121">Затем можно продолжить.</span><span class="sxs-lookup"><span data-stu-id="64bd0-121">Then we can proceed.</span></span>

## <a name="view-hello-application-and-container-logs"></a><span data-ttu-id="64bd0-122">Просмотр журналов приложений и контейнер hello</span><span class="sxs-lookup"><span data-stu-id="64bd0-122">View hello application and container logs</span></span>

<span data-ttu-id="64bd0-123">После успешного развертывания hello, откройте браузер toohello IP-адреса в выходные данные hello hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="64bd0-123">Once hello deployment succeeds, open your browser toohello IP address shown in hello output of hello following command:</span></span>

```bash
az container show --name aci-tutorial-app --resource-group myResourceGroup --query ipAddress.ip
```

```json
"13.88.176.27"
```

![Приложение Hello world в браузере hello][aci-app-browser]

<span data-ttu-id="64bd0-125">Можно также просмотреть выходные данные журнала hello hello контейнера:</span><span class="sxs-lookup"><span data-stu-id="64bd0-125">You can also view hello log output of hello container:</span></span>

```azurecli-interactive
az container logs --name aci-tutorial-app -g myResourceGroup
```

<span data-ttu-id="64bd0-126">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="64bd0-126">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://13.88.176.27/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="next-steps"></a><span data-ttu-id="64bd0-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="64bd0-127">Next steps</span></span>

<span data-ttu-id="64bd0-128">В этом учебнике вы выполнили hello процесс развертывания вашего контейнеры tooAzure экземпляры контейнером.</span><span class="sxs-lookup"><span data-stu-id="64bd0-128">In this tutorial, you completed hello process of deploying your containers tooAzure Container Instances.</span></span> <span data-ttu-id="64bd0-129">Привет, следующие шаги были выполнены:</span><span class="sxs-lookup"><span data-stu-id="64bd0-129">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="64bd0-130">Развертывание hello контейнера с помощью реестра контейнера Azure hello hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="64bd0-130">Deploying hello container from hello Azure Container Registry using hello Azure CLI</span></span>
> * <span data-ttu-id="64bd0-131">Приложение hello для просмотра в браузере hello</span><span class="sxs-lookup"><span data-stu-id="64bd0-131">Viewing hello application in hello browser</span></span>
> * <span data-ttu-id="64bd0-132">Просмотр журналов контейнера hello</span><span class="sxs-lookup"><span data-stu-id="64bd0-132">Viewing hello container logs</span></span>

<!-- LINKS -->
[prepare-app]: ./container-instances-tutorial-prepare-app.md

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png
