---
title: "Учебник контейнера службы aaaAzure - развертывание приложений | Документы Microsoft"
description: "Руководство по Службе контейнеров Azure: развертывание приложения"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7e2fa06d359caf83e684df3966624a6e9a8e7efa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-applications-in-kubernetes"></a><span data-ttu-id="167de-104">Запуск приложений в Kubernetes</span><span class="sxs-lookup"><span data-stu-id="167de-104">Run applications in Kubernetes</span></span>

<span data-ttu-id="167de-105">В этом руководстве (часть 4 из 7) выполняется развертывание примера приложения в кластер Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="167de-105">In this tutorial, part four of seven, a sample application is deployed into a Kubernetes cluster.</span></span> <span data-ttu-id="167de-106">В частности, рассматриваются такие шаги:</span><span class="sxs-lookup"><span data-stu-id="167de-106">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="167de-107">скачивание файлов манифестов Kubernetes;</span><span class="sxs-lookup"><span data-stu-id="167de-107">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="167de-108">выполнение приложения в Kubernetes;</span><span class="sxs-lookup"><span data-stu-id="167de-108">Run application in Kubernetes</span></span>
> * <span data-ttu-id="167de-109">Тестирование приложения hello</span><span class="sxs-lookup"><span data-stu-id="167de-109">Test hello application</span></span>

<span data-ttu-id="167de-110">В последующих учебники это приложение является горизонтального масштабирования, обновления и Operations Management Suite настраивается toomonitor hello Kubernetes кластера.</span><span class="sxs-lookup"><span data-stu-id="167de-110">In subsequent tutorials, this application is scaled out, updated, and Operations Management Suite configured toomonitor hello Kubernetes cluster.</span></span>

<span data-ttu-id="167de-111">В этом учебнике предполагается основные понятия Kubernetes см. подробные сведения о Kubernetes hello [Kubernetes документации](https://kubernetes.io/docs/home/).</span><span class="sxs-lookup"><span data-stu-id="167de-111">This tutorial assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see hello [Kubernetes documentation](https://kubernetes.io/docs/home/).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="167de-112">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="167de-112">Before you begin</span></span>

<span data-ttu-id="167de-113">В предыдущих учебниках приложение было упаковано в образ контейнера, этот образ был отправленного tooAzure реестре контейнеров и Kubernetes кластера был создан.</span><span class="sxs-lookup"><span data-stu-id="167de-113">In previous tutorials, an application was packaged into a container image, this image was uploaded tooAzure Container Registry, and a Kubernetes cluster was created.</span></span> <span data-ttu-id="167de-114">Если вы не были выполнены следующие действия и хотите toofollow вдоль, возвращают слишком[учебник 1 – Создание образов контейнеров](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="167de-114">If you have not done these steps, and would like toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="167de-115">Для изучения данного руководства как минимум необходим кластер Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="167de-115">At minimum, this tutorial requires a Kubernetes cluster.</span></span>

## <a name="get-manifest-file"></a><span data-ttu-id="167de-116">Получение файла манифеста</span><span class="sxs-lookup"><span data-stu-id="167de-116">Get manifest file</span></span>

<span data-ttu-id="167de-117">В этом руководстве [объекты Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) развертываются с помощью манифеста Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="167de-117">For this tutorial, [Kubernetes objects](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) are deployed using a Kubernetes manifest.</span></span> <span data-ttu-id="167de-118">Манифест Kubernetes — это файл формата YAML или JSON, содержащий инструкции по развертыванию и настройке объектов Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="167de-118">A Kubernetes manifest is a YAML or JSON formatted file containing Kubernetes object deployment and configuration instructions.</span></span>

<span data-ttu-id="167de-119">файл манифеста приложения Hello для этого учебника доступен в репозитории приложения hello голос Azure, которая была клонирована в предыдущем учебнике.</span><span class="sxs-lookup"><span data-stu-id="167de-119">hello application manifest file for this tutorial is available in hello Azure Vote application repo, which was cloned in a previous tutorial.</span></span> <span data-ttu-id="167de-120">Если вы еще не сделали клонируйте репозиторий hello с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="167de-120">If you have not already done so, clone hello repo with hello following command:</span></span> 

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="167de-121">файл манифеста Hello находится в следующий каталог hello клонирования репозитория hello.</span><span class="sxs-lookup"><span data-stu-id="167de-121">hello manifest file is found in hello following directory of hello cloned repo.</span></span>

```bash
/azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

## <a name="update-manifest-file"></a><span data-ttu-id="167de-122">Обновление файла манифеста</span><span class="sxs-lookup"><span data-stu-id="167de-122">Update manifest file</span></span>

<span data-ttu-id="167de-123">При использовании образов контейнеров hello toostore реестра контейнера Azure, toobe манифеста потребностей hello дополнен hello loginServer имя записи контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="167de-123">If using Azure Container Registry toostore hello container images, hello manifest needs toobe updated with hello ACR loginServer name.</span></span>

<span data-ttu-id="167de-124">Получить имя входа сервера hello контроля доступа с hello [списка контроля доступа az](/cli/azure/acr#list) команды.</span><span class="sxs-lookup"><span data-stu-id="167de-124">Get hello ACR login server name with hello [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli-interactive
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="167de-125">Hello манифест образец был предварительно созданную с именем репозитория *microsoft*.</span><span class="sxs-lookup"><span data-stu-id="167de-125">hello sample manifest has been pre-created with a repository name of *microsoft*.</span></span> <span data-ttu-id="167de-126">Откройте файл hello в любом текстовом редакторе и замените hello *microsoft* значение с именем входа сервера hello, контроля доступа экземпляра.</span><span class="sxs-lookup"><span data-stu-id="167de-126">Open hello file with any text editor, and replace hello *microsoft* value with hello login server name of your ACR instance.</span></span>

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

## <a name="deploy-application"></a><span data-ttu-id="167de-127">Развертывание приложения</span><span class="sxs-lookup"><span data-stu-id="167de-127">Deploy application</span></span>

<span data-ttu-id="167de-128">Используйте hello [kubectl создания](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) команды toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="167de-128">Use hello [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) command toorun hello application.</span></span> <span data-ttu-id="167de-129">Это команда hello производит синтаксический анализ файла манифеста и создания объектов Kubernetes определенные hello.</span><span class="sxs-lookup"><span data-stu-id="167de-129">This command parses hello manifest file and create hello defined Kubernetes objects.</span></span>

```azurecli-interactive
kubectl create -f ./azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

<span data-ttu-id="167de-130">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="167de-130">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a><span data-ttu-id="167de-131">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="167de-131">Test application</span></span>

<span data-ttu-id="167de-132">Объект [Kubernetes службы](https://kubernetes.io/docs/concepts/services-networking/service/) создается в результате чего предоставляется toohello приложения hello Интернета.</span><span class="sxs-lookup"><span data-stu-id="167de-132">A [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created which exposes hello application toohello internet.</span></span> <span data-ttu-id="167de-133">Это может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="167de-133">This process can take a few minutes.</span></span> 

<span data-ttu-id="167de-134">toomonitor о ходе выполнения, используйте hello [kubectl получить службу](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) с hello `--watch` аргумент.</span><span class="sxs-lookup"><span data-stu-id="167de-134">toomonitor progress, use hello [kubectl get service](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) command with hello `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="167de-135">Здравствуйте, изначально **внешний IP-** для hello *azure голос передней панели* службы отображается как *ожидающие*.</span><span class="sxs-lookup"><span data-stu-id="167de-135">Initially, hello **EXTERNAL-IP** for hello *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="167de-136">После hello внешний IP-адрес отличается от *ожидающие* tooan *IP-адрес*, используйте `CTRL-C` toostop hello kubectl Контрольные значения процесса.</span><span class="sxs-lookup"><span data-stu-id="167de-136">Once hello EXTERNAL-IP address has changed from *pending* tooan *IP address*, use `CTRL-C` toostop hello kubectl watch process.</span></span>

```bash
NAME               CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   10.0.42.158   <pending>     80:31873/TCP   1m
azure-vote-front   10.0.42.158   52.179.23.131 80:31873/TCP   2m
```

<span data-ttu-id="167de-137">приложение hello toosee, обзора toohello внешний IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="167de-137">toosee hello application, browse toohello external IP address.</span></span>

![Схема кластера Kubernetes в Аzure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a><span data-ttu-id="167de-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="167de-139">Next steps</span></span>

<span data-ttu-id="167de-140">В этом учебнике hello приложения Azure голос был кластера развернутой tooan Kubernetes службы контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="167de-140">In this tutorial, hello Azure vote application was deployed tooan Azure Container Service Kubernetes cluster.</span></span> <span data-ttu-id="167de-141">Вам предстоят следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="167de-141">Tasks completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="167de-142">скачивание файлов манифестов Kubernetes;</span><span class="sxs-lookup"><span data-stu-id="167de-142">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="167de-143">Запустите приложение hello в Kubernetes</span><span class="sxs-lookup"><span data-stu-id="167de-143">Run hello application in Kubernetes</span></span>
> * <span data-ttu-id="167de-144">Протестированные hello приложения</span><span class="sxs-lookup"><span data-stu-id="167de-144">Tested hello application</span></span>

<span data-ttu-id="167de-145">Переместить Далее учебника toolearn toohello о масштабировании hello базовой инфраструктуры Kubernetes и Kubernetes приложения.</span><span class="sxs-lookup"><span data-stu-id="167de-145">Advance toohello next tutorial toolearn about scaling both a Kubernetes application and hello underlying Kubernetes infrastructure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="167de-146">Масштабирование pod и инфраструктуры Kubernetes</span><span class="sxs-lookup"><span data-stu-id="167de-146">Scale Kubernetes application and infrastructure</span></span>](./container-service-tutorial-kubernetes-scale.md)