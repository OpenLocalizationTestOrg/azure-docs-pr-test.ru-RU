---
title: "aaaManage Azure Kubernetes кластер с веб-Интерфейсе | Документы Microsoft"
description: "С помощью hello Kubernetes веб-интерфейсом пользователя в службе контейнера Azure"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/21/2017
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: e24ea0b82c94d2fd4610e4442699ef756590e6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-kubernetes-web-ui-with-azure-container-service"></a><span data-ttu-id="13fbf-103">С помощью hello Kubernetes веб-интерфейсом пользователя с помощью контейнера службы Azure</span><span class="sxs-lookup"><span data-stu-id="13fbf-103">Using hello Kubernetes web UI with Azure Container Service</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13fbf-104">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="13fbf-104">Prerequisites</span></span>
<span data-ttu-id="13fbf-105">В этом пошаговом руководстве предполагается, что вы [создали кластер Kubernetes с помощью службы контейнеров Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="13fbf-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>


<span data-ttu-id="13fbf-106">Также предполагается, что имеется hello Azure CLI 2.0 и `kubectl` установлены инструменты.</span><span class="sxs-lookup"><span data-stu-id="13fbf-106">It also assumes that you have hello Azure CLI 2.0 and `kubectl` tools installed.</span></span>

<span data-ttu-id="13fbf-107">Можно проверить при наличии hello `az` установить, запустив средство:</span><span class="sxs-lookup"><span data-stu-id="13fbf-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="13fbf-108">Если у вас нет hello `az` средство установки приведены инструкции по [здесь](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="13fbf-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="13fbf-109">Можно проверить при наличии hello `kubectl` установить, запустив средство:</span><span class="sxs-lookup"><span data-stu-id="13fbf-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="13fbf-110">Если средство `kubectl` не установлено, выполните команду:</span><span class="sxs-lookup"><span data-stu-id="13fbf-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="overview"></a><span data-ttu-id="13fbf-111">Обзор</span><span class="sxs-lookup"><span data-stu-id="13fbf-111">Overview</span></span>

### <a name="connect-toohello-web-ui"></a><span data-ttu-id="13fbf-112">Подключиться к Интернету toohello пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="13fbf-112">Connect toohello web UI</span></span>
<span data-ttu-id="13fbf-113">Hello Kubernetes пользовательского веб-интерфейса можно запустить с помощью команды:</span><span class="sxs-lookup"><span data-stu-id="13fbf-113">You can launch hello Kubernetes web UI by running:</span></span>

```console
$ az acs kubernetes browse -g [Resource Group] -n [Container service instance name]
```

<span data-ttu-id="13fbf-114">Откроется веб-браузер настроен tootalk tooa безопасного прокси подключения на локальном компьютере toohello Kubernetes веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="13fbf-114">This should open a web browser configured tootalk tooa secure proxy connecting your local machine toohello Kubernetes web UI.</span></span>

### <a name="create-and-expose-a-service"></a><span data-ttu-id="13fbf-115">Создание и предоставление службы</span><span class="sxs-lookup"><span data-stu-id="13fbf-115">Create and expose a service</span></span>
1. <span data-ttu-id="13fbf-116">В веб-Kubernetes hello пользовательского интерфейса, нажмите кнопку **создать** кнопка в верхнем правом окне приветствия.</span><span class="sxs-lookup"><span data-stu-id="13fbf-116">In hello Kubernetes web UI, click **Create** button in hello upper right window.</span></span>

    ![Кнопка Create (Создать) в веб-интерфейсе Kubernetes](./media/container-service-kubernetes-ui/create.png)

    <span data-ttu-id="13fbf-118">При этом откроется диалоговое окно, в котором можно приступить к созданию приложения.</span><span class="sxs-lookup"><span data-stu-id="13fbf-118">A dialog box opens where you can start creating your application.</span></span>

2. <span data-ttu-id="13fbf-119">Присвойте ему имя hello `hello-nginx`.</span><span class="sxs-lookup"><span data-stu-id="13fbf-119">Give it hello name `hello-nginx`.</span></span> <span data-ttu-id="13fbf-120">Используйте hello [ `nginx` контейнера Docker](https://hub.docker.com/_/nginx/) и развернуть три реплики этой веб-службы.</span><span class="sxs-lookup"><span data-stu-id="13fbf-120">Use hello [`nginx` container from Docker](https://hub.docker.com/_/nginx/) and deploy three replicas of this web service.</span></span>

    ![Диалоговое окно создания модуля Kubernetes](./media/container-service-kubernetes-ui/nginx.png)

3. <span data-ttu-id="13fbf-122">В разделе **Service** (Служба) выберите вариант **External** (Внешняя) и укажите порт 80.</span><span class="sxs-lookup"><span data-stu-id="13fbf-122">Under **Service**, select **External** and enter port 80.</span></span>

    <span data-ttu-id="13fbf-123">Этот параметр балансировку нагрузки трафика toohello три реплики.</span><span class="sxs-lookup"><span data-stu-id="13fbf-123">This setting load-balances traffic toohello three replicas.</span></span>

    ![Диалоговое окно создания службы Kubernetes](./media/container-service-kubernetes-ui/service.png)

4. <span data-ttu-id="13fbf-125">Нажмите кнопку **развернуть** toodeploy эти контейнеры и службы.</span><span class="sxs-lookup"><span data-stu-id="13fbf-125">Click **Deploy** toodeploy these containers and services.</span></span>

    ![Развертывание Kubernetes](./media/container-service-kubernetes-ui/deploy.png)

### <a name="view-your-containers"></a><span data-ttu-id="13fbf-127">Просмотр контейнеров</span><span class="sxs-lookup"><span data-stu-id="13fbf-127">View your containers</span></span>
<span data-ttu-id="13fbf-128">После нажатия кнопки **развернуть**, hello пользовательского интерфейса показано представление в виде службы, как развертывания:</span><span class="sxs-lookup"><span data-stu-id="13fbf-128">After you click **Deploy**, hello UI shows a view of your service as it deploys:</span></span>

![Состояние Kubernetes](./media/container-service-kubernetes-ui/status.png)

<span data-ttu-id="13fbf-130">Состояние каждого объекта Kubernetes в кружке hello hello hello левой части пользовательского интерфейса, можно отслеживать в разделе **модулей**.</span><span class="sxs-lookup"><span data-stu-id="13fbf-130">You can see hello status of each Kubernetes object in hello circle on hello left-hand side of the UI, under **Pods**.</span></span> <span data-ttu-id="13fbf-131">Если это частично полный круг hello объекта по-прежнему развертывание.</span><span class="sxs-lookup"><span data-stu-id="13fbf-131">If it is a partially full circle, then hello object is still deploying.</span></span> <span data-ttu-id="13fbf-132">Когда объект будет полностью развернут, отобразится зеленая галочка:</span><span class="sxs-lookup"><span data-stu-id="13fbf-132">When an object is fully deployed, it displays a green check mark:</span></span>

![Объект Kubernetes развернут](./media/container-service-kubernetes-ui/deployed.png)

<span data-ttu-id="13fbf-134">Как только все работает, выберите один из модулей toosee подробные сведения о hello выполнение веб-службы.</span><span class="sxs-lookup"><span data-stu-id="13fbf-134">Once everything is running, click one of your pods toosee details about hello running web service.</span></span>

![Модули Kubernetes](./media/container-service-kubernetes-ui/pods.png)

<span data-ttu-id="13fbf-136">В hello **модулей** представления, можно просмотреть информацию о контейнерах hello в hello pod, а также hello ЦП и памяти ресурсы, используемые в этих контейнерах:</span><span class="sxs-lookup"><span data-stu-id="13fbf-136">In hello **Pods** view, you can see information about hello containers in hello pod as well as hello CPU and memory resources used by those containers:</span></span>

![Ресурсы Kubernetes](./media/container-service-kubernetes-ui/resources.png)

<span data-ttu-id="13fbf-138">Если вы не видите hello ресурсы, может потребоваться toowait через несколько минут для мониторинга данных toopropagate hello.</span><span class="sxs-lookup"><span data-stu-id="13fbf-138">If you don't see hello resources, you may need toowait a few minutes for hello monitoring data toopropagate.</span></span>

<span data-ttu-id="13fbf-139">toosee hello журналы для контейнера, нажмите кнопку **Просмотр журналов**.</span><span class="sxs-lookup"><span data-stu-id="13fbf-139">toosee hello logs for your container, click **View logs**.</span></span>

![Журналы Kubernetes](./media/container-service-kubernetes-ui/logs.png)

### <a name="viewing-your-service"></a><span data-ttu-id="13fbf-141">Просмотр службы</span><span class="sxs-lookup"><span data-stu-id="13fbf-141">Viewing your service</span></span>
<span data-ttu-id="13fbf-142">В дополнение toorunning вашей контейнеры hello Kubernetes пользовательского интерфейса создал внешней `Service` которого подготавливает контейнерам нагрузки балансировки toobring трафика toohello в кластере.</span><span class="sxs-lookup"><span data-stu-id="13fbf-142">In addition toorunning your containers, hello Kubernetes UI has created an external `Service` which provisions a load balancer toobring traffic toohello containers in your cluster.</span></span>

<span data-ttu-id="13fbf-143">Hello панели навигации слева щелкните **службы** tooview все службы (должна быть только одна).</span><span class="sxs-lookup"><span data-stu-id="13fbf-143">In hello left navigation pane, click **Services** tooview all services (there should be only one).</span></span>

![Службы Kubernetes](./media/container-service-kubernetes-ui/service-deployed.png)

<span data-ttu-id="13fbf-145">В этом представлении вы увидите внешнюю конечную точку (IP-адрес), занятый tooyour службы.</span><span class="sxs-lookup"><span data-stu-id="13fbf-145">In that view, you should see an external endpoint (IP address) that has been allocated tooyour service.</span></span>
<span data-ttu-id="13fbf-146">Если щелкнуть этот IP-адрес, то отобразится контейнер Nginx, выполняющийся за подсистемой балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="13fbf-146">If you click that IP address, you should see your Nginx container running behind the load balancer.</span></span>

![Представление nginx](./media/container-service-kubernetes-ui/nginx-page.png)

### <a name="resizing-your-service"></a><span data-ttu-id="13fbf-148">Изменение размеров службы</span><span class="sxs-lookup"><span data-stu-id="13fbf-148">Resizing your service</span></span>
<span data-ttu-id="13fbf-149">В дополнение tooviewing объектов в Здравствуйте пользовательского интерфейса, можно изменить и обновить объекты Kubernetes API hello.</span><span class="sxs-lookup"><span data-stu-id="13fbf-149">In addition tooviewing your objects in hello UI, you can edit and update hello Kubernetes API objects.</span></span>

<span data-ttu-id="13fbf-150">Во-первых, нажмите кнопку **развертываний** в hello слева развертывания hello toosee панель навигации для службы.</span><span class="sxs-lookup"><span data-stu-id="13fbf-150">First, click **Deployments** in hello left navigation pane toosee hello deployment for your service.</span></span>

<span data-ttu-id="13fbf-151">После входа в это представление, щелкните на наборе реплик hello и нажмите кнопку **изменить** hello верхней навигационной панели:</span><span class="sxs-lookup"><span data-stu-id="13fbf-151">Once you are in that view, click on hello replica set, and then click **Edit** in hello upper navigation bar:</span></span>

![Окно изменения в Kubernetes](./media/container-service-kubernetes-ui/edit.png)

<span data-ttu-id="13fbf-153">Изменить hello `spec.replicas` toobe поле `2`и нажмите кнопку **обновление**.</span><span class="sxs-lookup"><span data-stu-id="13fbf-153">Edit hello `spec.replicas` field toobe `2`, and click **Update**.</span></span>

<span data-ttu-id="13fbf-154">В этом случае hello число tootwo toodrop реплик, удалив один из вашего модулей.</span><span class="sxs-lookup"><span data-stu-id="13fbf-154">This causes hello number of replicas toodrop tootwo by deleting one of your pods.</span></span>

 

