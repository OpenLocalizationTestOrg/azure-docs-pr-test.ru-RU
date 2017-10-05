---
title: "Руководство по службе \"Экземпляры контейнеров Azure\". Развертывание приложения | Документация Майкрософт"
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
ms.openlocfilehash: 54151a5c1850ab7120fe666a46dc5dc99c0f5157
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-container-to-azure-container-instances"></a><span data-ttu-id="09d84-103">Развертывание контейнера в службе "Экземпляры контейнеров Azure"</span><span class="sxs-lookup"><span data-stu-id="09d84-103">Deploy a container to Azure Container Instances</span></span>

<span data-ttu-id="09d84-104">Эта последняя часть руководства, состоящего из трех частей.</span><span class="sxs-lookup"><span data-stu-id="09d84-104">This is the last of a three-part tutorial.</span></span> <span data-ttu-id="09d84-105">В предыдущих частях мы [создали образ контейнера](container-instances-tutorial-prepare-app.md), который затем [передали в реестр контейнеров Azure](container-instances-tutorial-prepare-acr.md).</span><span class="sxs-lookup"><span data-stu-id="09d84-105">In previous sections, [a container image was created](container-instances-tutorial-prepare-app.md) and [pushed to an Azure Container Registry](container-instances-tutorial-prepare-acr.md).</span></span> <span data-ttu-id="09d84-106">Эта часть завершает руководство. Мы развернем контейнер в службе "Экземпляры контейнеров Azure".</span><span class="sxs-lookup"><span data-stu-id="09d84-106">This section completes the tutorial by deploying the container to Azure Container Instances.</span></span> <span data-ttu-id="09d84-107">В частности, рассматриваются такие шаги:</span><span class="sxs-lookup"><span data-stu-id="09d84-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="09d84-108">Определение группы контейнеров с использованием шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="09d84-108">Defining a container group using an Azure Resource Manager template</span></span>
> * <span data-ttu-id="09d84-109">Развертывание группы контейнеров с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="09d84-109">Deploying the container group using the Azure CLI</span></span>
> * <span data-ttu-id="09d84-110">Просмотр журналов контейнера</span><span class="sxs-lookup"><span data-stu-id="09d84-110">Viewing container logs</span></span>

## <a name="deploy-the-container-using-the-azure-cli"></a><span data-ttu-id="09d84-111">Развертывание контейнера с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="09d84-111">Deploy the container using the Azure CLI</span></span>

<span data-ttu-id="09d84-112">Azure CLI позволяет одной командой развернуть контейнер в службе "Экземпляры контейнеров Azure".</span><span class="sxs-lookup"><span data-stu-id="09d84-112">The Azure CLI enables deployment of a container to Azure Container Instances in a single command.</span></span> <span data-ttu-id="09d84-113">Так как образ контейнера размещается в частном реестре контейнеров Azure, необходимо включить учетные данные, необходимые для доступа к нему.</span><span class="sxs-lookup"><span data-stu-id="09d84-113">Since the container image is hosted in the private Azure Container Registry, you must include the credentials required to access it.</span></span> <span data-ttu-id="09d84-114">При необходимости их можно запросить, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="09d84-114">If necessary, you can query them as shown below.</span></span>

<span data-ttu-id="09d84-115">Сервер входа в реестр контейнеров (укажите используемое имя реестра):</span><span class="sxs-lookup"><span data-stu-id="09d84-115">Container registry login server (update with your registry name):</span></span>

```azurecli-interactive
az acr show --name <acrName> --query loginServer
```

<span data-ttu-id="09d84-116">Пароль для реестра контейнеров:</span><span class="sxs-lookup"><span data-stu-id="09d84-116">Container registry password:</span></span>

```azurecli-interactive
az acr credential show --name <acrName> --query "passwords[0].value"
```

<span data-ttu-id="09d84-117">Чтобы развернуть образ контейнера из реестра контейнеров с запросом ресурсов (одно ядро ЦП и 1 ГБ памяти), выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="09d84-117">To deploy your container image from the container registry with a resource request of 1 CPU core and 1GB of memory, run the following command:</span></span>

```azurecli-interactive
az container create --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-password <acrPassword> --ip-address public -g myResourceGroup
```

<span data-ttu-id="09d84-118">В течение нескольких секунд вы получите исходный ответ Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="09d84-118">Within a few seconds, you will receive an initial response from Azure Resource Manager.</span></span> <span data-ttu-id="09d84-119">Чтобы просмотреть состояние развертывания, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="09d84-119">To view the state of the deployment, use:</span></span>

```azurecli-interactive
az container show --name aci-tutorial-app --resource-group myResourceGroup --query state
```

<span data-ttu-id="09d84-120">Мы можем и дальше выполнять эту команду, пока состояние не изменится с *Ожидание* на *Выполняется*.</span><span class="sxs-lookup"><span data-stu-id="09d84-120">We can continue running this command until the state changes from *pending* to *running*.</span></span> <span data-ttu-id="09d84-121">Затем можно продолжить.</span><span class="sxs-lookup"><span data-stu-id="09d84-121">Then we can proceed.</span></span>

## <a name="view-the-application-and-container-logs"></a><span data-ttu-id="09d84-122">Просмотр приложения и журналов контейнера</span><span class="sxs-lookup"><span data-stu-id="09d84-122">View the application and container logs</span></span>

<span data-ttu-id="09d84-123">После успешного развертывания откройте в браузере IP-адрес, показанный в выходных данных следующей команды:</span><span class="sxs-lookup"><span data-stu-id="09d84-123">Once the deployment succeeds, open your browser to the IP address shown in the output of the following command:</span></span>

```bash
az container show --name aci-tutorial-app --resource-group myResourceGroup --query ipAddress.ip
```

```json
"13.88.176.27"
```

![Приложение Hello World в браузере][aci-app-browser]

<span data-ttu-id="09d84-125">Также можно просмотреть выходные данные журнала контейнера:</span><span class="sxs-lookup"><span data-stu-id="09d84-125">You can also view the log output of the container:</span></span>

```azurecli-interactive
az container logs --name aci-tutorial-app -g myResourceGroup
```

<span data-ttu-id="09d84-126">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="09d84-126">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://13.88.176.27/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="next-steps"></a><span data-ttu-id="09d84-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="09d84-127">Next steps</span></span>

<span data-ttu-id="09d84-128">В этом руководстве мы завершили процесс развертывания контейнеров в службе "Экземпляры контейнеров Azure".</span><span class="sxs-lookup"><span data-stu-id="09d84-128">In this tutorial, you completed the process of deploying your containers to Azure Container Instances.</span></span> <span data-ttu-id="09d84-129">Были выполнены следующие действия:</span><span class="sxs-lookup"><span data-stu-id="09d84-129">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="09d84-130">Развертывание контейнера из реестра контейнеров Azure с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="09d84-130">Deploying the container from the Azure Container Registry using the Azure CLI</span></span>
> * <span data-ttu-id="09d84-131">Просмотр приложения в браузере</span><span class="sxs-lookup"><span data-stu-id="09d84-131">Viewing the application in the browser</span></span>
> * <span data-ttu-id="09d84-132">Просмотр журналов контейнера</span><span class="sxs-lookup"><span data-stu-id="09d84-132">Viewing the container logs</span></span>

<!-- LINKS -->
[prepare-app]: ./container-instances-tutorial-prepare-app.md

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png
