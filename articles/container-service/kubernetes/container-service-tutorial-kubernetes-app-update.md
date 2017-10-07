---
title: "Учебник aaaAzure контейнера службы - приложение обновления | Документы Microsoft"
description: "Руководство по Службе контейнеров Azure: обновление приложения"
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
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c467498bab7952926a18e45ffbb21051a98739d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="update-an-application-in-kubernetes"></a><span data-ttu-id="45436-104">Обновление приложения в Kubernetes</span><span class="sxs-lookup"><span data-stu-id="45436-104">Update an application in Kubernetes</span></span>

<span data-ttu-id="45436-105">После развертывания приложения в Kubernetes его можно обновить, указав новый образ контейнера или версию образа.</span><span class="sxs-lookup"><span data-stu-id="45436-105">After you deploy an application in Kubernetes, it can be updated by specifying a new container image or image version.</span></span> <span data-ttu-id="45436-106">При обновлении приложения hello выпуска обновлений на промежуточное хранение, чтобы одновременно обновляется только часть hello развертывания.</span><span class="sxs-lookup"><span data-stu-id="45436-106">When you update an application, hello update rollout is staged so that only a portion of hello deployment is concurrently updated.</span></span> <span data-ttu-id="45436-107">Это обновление промежуточные включает tookeep приложения hello, во время обновления hello и предоставляет механизм отката, если происходит сбой развертывания.</span><span class="sxs-lookup"><span data-stu-id="45436-107">This staged update enables hello application tookeep running during hello update, and provides a rollback mechanism if a deployment failure occurs.</span></span> 

<span data-ttu-id="45436-108">В этом учебнике обновляется часть шести семью, приложение Azure голос образец hello.</span><span class="sxs-lookup"><span data-stu-id="45436-108">In this tutorial, part six of seven, hello sample Azure Vote app is updated.</span></span> <span data-ttu-id="45436-109">Здесь будут выполнены следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="45436-109">Tasks that you complete include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="45436-110">Обновление кода клиентского приложения hello</span><span class="sxs-lookup"><span data-stu-id="45436-110">Updating hello front-end application code</span></span>
> * <span data-ttu-id="45436-111">Создание обновленного образа контейнера.</span><span class="sxs-lookup"><span data-stu-id="45436-111">Creating an updated container image</span></span>
> * <span data-ttu-id="45436-112">Образ контейнера проталкивания hello tooAzure реестра контейнера</span><span class="sxs-lookup"><span data-stu-id="45436-112">Pushing hello container image tooAzure Container Registry</span></span>
> * <span data-ttu-id="45436-113">Развертывание образа контейнера обновленные hello</span><span class="sxs-lookup"><span data-stu-id="45436-113">Deploying hello updated container image</span></span>

<span data-ttu-id="45436-114">В последующих учебники Operations Management Suite — настроенное toomonitor hello Kubernetes кластер.</span><span class="sxs-lookup"><span data-stu-id="45436-114">In subsequent tutorials, Operations Management Suite is configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="45436-115">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="45436-115">Before you begin</span></span>

<span data-ttu-id="45436-116">В предыдущих учебниках приложение было упаковано в образ контейнера, отправить изображение hello, tooAzure реестра контейнера и создания кластера Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="45436-116">In previous tutorials, an application was packaged into a container image, hello image uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="45436-117">приложение Hello затем была запущена на кластере Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="45436-117">hello application was then run on hello Kubernetes cluster.</span></span> 

<span data-ttu-id="45436-118">Если вы еще не выполнит эти действия и toofollow вдоль, возвращают слишком[учебник 1 – Создание образов контейнеров](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="45436-118">If you haven't completed these steps, and want toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

## <a name="update-application"></a><span data-ttu-id="45436-119">Обновление приложения</span><span class="sxs-lookup"><span data-stu-id="45436-119">Update application</span></span>

<span data-ttu-id="45436-120">toocomplete hello шагах данного учебника, вы должны клонировали копию hello приложения Azure голос.</span><span class="sxs-lookup"><span data-stu-id="45436-120">toocomplete hello steps in this tutorial, you must have cloned a copy of hello Azure Vote application.</span></span> <span data-ttu-id="45436-121">При необходимости создайте это Клонированная копия с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="45436-121">If necessary, create this cloned copy with hello following command:</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="45436-122">Откройте hello `config_file.cfg` файла с помощью любого редактора кода или текста.</span><span class="sxs-lookup"><span data-stu-id="45436-122">Open hello `config_file.cfg` file with any code or text editor.</span></span> <span data-ttu-id="45436-123">Можно найти этот файл в следующий каталог hello клонирования репозитория hello.</span><span class="sxs-lookup"><span data-stu-id="45436-123">You can find this file under hello following directory of hello cloned repo.</span></span>

```bash
 /azure-voting-app-redis/azure-vote/azure-vote/config_file.cfg
```

<span data-ttu-id="45436-124">Изменить значения hello `VOTE1VALUE` и `VOTE2VALUE`, а затем сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="45436-124">Change hello values for `VOTE1VALUE` and `VOTE2VALUE`, and then save hello file.</span></span>

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

<span data-ttu-id="45436-125">Используйте [составления docker](https://docs.docker.com/compose/) toore-создать изображение переднего плана hello и выполнения hello обновления приложения.</span><span class="sxs-lookup"><span data-stu-id="45436-125">Use [docker-compose](https://docs.docker.com/compose/) toore-create hello front-end image and run hello updated application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up --build -d
```

## <a name="test-application-locally"></a><span data-ttu-id="45436-126">Локальное тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="45436-126">Test application locally</span></span>

<span data-ttu-id="45436-127">Обзор слишком`http://localhost:8080` toosee hello обновленное приложение.</span><span class="sxs-lookup"><span data-stu-id="45436-127">Browse too`http://localhost:8080` toosee hello updated application.</span></span>

![Схема кластера Kubernetes в Аzure](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a><span data-ttu-id="45436-129">Пометка и отправка образов</span><span class="sxs-lookup"><span data-stu-id="45436-129">Tag and push images</span></span>

<span data-ttu-id="45436-130">Тег hello *azure голос передней панели* изображение с loginServer hello hello контейнер реестра.</span><span class="sxs-lookup"><span data-stu-id="45436-130">Tag hello *azure-vote-front* image with hello loginServer of hello container registry.</span></span>

<span data-ttu-id="45436-131">Если вы используете реестра контейнера Azure, получения имени сервера hello входа с hello [az списка контроля доступа](/cli/azure/acr#list) команды.</span><span class="sxs-lookup"><span data-stu-id="45436-131">If you're using Azure Container Registry, get hello login server name with hello [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="45436-132">Используйте [docker тега](https://docs.docker.com/engine/reference/commandline/tag/) tootag hello изображения.</span><span class="sxs-lookup"><span data-stu-id="45436-132">Use [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) tootag hello image.</span></span> <span data-ttu-id="45436-133">Замените `<acrLoginServer>` именем сервера входа реестра контейнеров Azure или именем узла общедоступного реестра.</span><span class="sxs-lookup"><span data-stu-id="45436-133">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="45436-134">Используйте [docker push](https://docs.docker.com/engine/reference/commandline/push/) tooupload hello изображения tooyour реестра.</span><span class="sxs-lookup"><span data-stu-id="45436-134">Use [docker push](https://docs.docker.com/engine/reference/commandline/push/) tooupload hello image tooyour registry.</span></span> <span data-ttu-id="45436-135">Замените `<acrLoginServer>` именем сервера входа реестра контейнеров Azure или именем узла общедоступного реестра.</span><span class="sxs-lookup"><span data-stu-id="45436-135">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a><span data-ttu-id="45436-136">Развертывание обновленного приложения</span><span class="sxs-lookup"><span data-stu-id="45436-136">Deploy update application</span></span>

<span data-ttu-id="45436-137">Максимальное время работоспособности tooensure несколько экземпляров типа pod приложения hello должна быть запущена.</span><span class="sxs-lookup"><span data-stu-id="45436-137">tooensure maximum uptime, multiple instances of hello application pod must be running.</span></span> <span data-ttu-id="45436-138">Проверьте конфигурацию hello [kubectl получить pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) команды.</span><span class="sxs-lookup"><span data-stu-id="45436-138">Verify this configuration with hello [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```bash
kubectl get pod
```

<span data-ttu-id="45436-139">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="45436-139">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

<span data-ttu-id="45436-140">Если у вас нет несколько модулей под управлением образа azure голос передней панели hello, масштабирование hello *azure голос передней панели* развертывания.</span><span class="sxs-lookup"><span data-stu-id="45436-140">If you don't have multiple pods running hello azure-vote-front image, scale hello *azure-vote-front* deployment.</span></span>


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

<span data-ttu-id="45436-141">приложение hello tooupdate, используйте hello [kubectl набора](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) команды.</span><span class="sxs-lookup"><span data-stu-id="45436-141">tooupdate hello application, use hello [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) command.</span></span> <span data-ttu-id="45436-142">Обновление `<acrLoginServer>` с hello входа сервера или имя узла в реестре контейнера.</span><span class="sxs-lookup"><span data-stu-id="45436-142">Update `<acrLoginServer>` with hello login server or host name of your container registry.</span></span>

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="45436-143">Развертывание toomonitor hello, используйте hello [kubectl получить pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) команды.</span><span class="sxs-lookup"><span data-stu-id="45436-143">toomonitor hello deployment, use hello [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span> <span data-ttu-id="45436-144">Развернуто приложение hello обновить ваш модулей завершаются и созданы повторно со hello новый образ контейнера.</span><span class="sxs-lookup"><span data-stu-id="45436-144">As hello updated application is deployed, your pods are terminated and re-created with hello new container image.</span></span>

```azurecli-interactive
kubectl get pod
```

<span data-ttu-id="45436-145">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="45436-145">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a><span data-ttu-id="45436-146">Тестирование обновленного приложения</span><span class="sxs-lookup"><span data-stu-id="45436-146">Test updated application</span></span>

<span data-ttu-id="45436-147">Получить hello внешний IP-адрес hello *azure голос передней панели* службы.</span><span class="sxs-lookup"><span data-stu-id="45436-147">Get hello external IP address of hello *azure-vote-front* service.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front
```

<span data-ttu-id="45436-148">Обзор toohello IP адрес toosee hello обновленное приложение.</span><span class="sxs-lookup"><span data-stu-id="45436-148">Browse toohello IP address toosee hello updated application.</span></span>

![Схема кластера Kubernetes в Аzure](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a><span data-ttu-id="45436-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="45436-150">Next steps</span></span>

<span data-ttu-id="45436-151">В этом учебнике обновить приложение и распространен этого обновления tooa Kubernetes кластера.</span><span class="sxs-lookup"><span data-stu-id="45436-151">In this tutorial, you updated an application and rolled out this update tooa Kubernetes cluster.</span></span> <span data-ttu-id="45436-152">были выполнены Hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="45436-152">hello following tasks were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="45436-153">Обновленные hello код клиентского приложения</span><span class="sxs-lookup"><span data-stu-id="45436-153">Updated hello front-end application code</span></span>
> * <span data-ttu-id="45436-154">Создание обновленного образа контейнера.</span><span class="sxs-lookup"><span data-stu-id="45436-154">Created an updated container image</span></span>
> * <span data-ttu-id="45436-155">Передано tooAzure образ контейнера hello реестра контейнера</span><span class="sxs-lookup"><span data-stu-id="45436-155">Pushed hello container image tooAzure Container Registry</span></span>
> * <span data-ttu-id="45436-156">Развернутое приложение hello обновление приложения</span><span class="sxs-lookup"><span data-stu-id="45436-156">Deployed hello updated application</span></span>

<span data-ttu-id="45436-157">Далее учебника toolearn toohello о том, как переместить toomonitor Kubernetes с Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="45436-157">Advance toohello next tutorial toolearn about how toomonitor Kubernetes with Operations Management Suite.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="45436-158">Мониторинг кластера Kubernetes с помощью Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="45436-158">Monitor Kubernetes with OMS</span></span>](./container-service-tutorial-kubernetes-monitor.md)