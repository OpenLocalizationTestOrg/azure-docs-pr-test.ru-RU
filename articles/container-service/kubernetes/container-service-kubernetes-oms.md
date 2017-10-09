---
title: "кластер aaaMonitor Azure Kubernetes - операции управления | Документы Microsoft"
description: "Мониторинг кластера Kubernetes в Службе контейнеров Azure с помощью Microsoft Operations Management Suite"
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
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: 7474ee1571134ffe43ff8e4041cf5a64f5635bb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a><span data-ttu-id="6724f-103">Мониторинг кластера Службы контейнеров Azure с помощью Microsoft Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="6724f-103">Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6724f-104">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6724f-104">Prerequisites</span></span>
<span data-ttu-id="6724f-105">В этом пошаговом руководстве предполагается, что вы [создали кластер Kubernetes с помощью службы контейнеров Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="6724f-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="6724f-106">Также предполагается, что имеется hello `az` Azure cli и `kubectl` установлены инструменты.</span><span class="sxs-lookup"><span data-stu-id="6724f-106">It also assumes that you have hello `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="6724f-107">Можно проверить при наличии hello `az` установить, запустив средство:</span><span class="sxs-lookup"><span data-stu-id="6724f-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="6724f-108">Если у вас нет hello `az` средство установки приведены инструкции по [здесь](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="6724f-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>  
<span data-ttu-id="6724f-109">Кроме того, можно использовать [оболочки облако Azure](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), имеющий hello `az` Azure cli и `kubectl` средства уже установлен автоматически.</span><span class="sxs-lookup"><span data-stu-id="6724f-109">Alternatively, you can use [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), which has hello `az` Azure cli and `kubectl` tools already installed for you.</span></span>  

<span data-ttu-id="6724f-110">Можно проверить при наличии hello `kubectl` установить, запустив средство:</span><span class="sxs-lookup"><span data-stu-id="6724f-110">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="6724f-111">Если средство `kubectl` не установлено, выполните команду:</span><span class="sxs-lookup"><span data-stu-id="6724f-111">If you don't have `kubectl` installed, you can run:</span></span>
```console
$ az acs kubernetes install-cli
```

<span data-ttu-id="6724f-112">tootest при наличии kubernetes ключи, установленные в средстве kubectl можно запустить:</span><span class="sxs-lookup"><span data-stu-id="6724f-112">tootest if you have kubernetes keys installed in your kubectl tool you can run:</span></span>
```console
$ kubectl get nodes
```

<span data-ttu-id="6724f-113">Если hello выше команда ошибок, tooinstall kubernetes кластера ключи требуются в средство kubectl.</span><span class="sxs-lookup"><span data-stu-id="6724f-113">If hello above command errors out, you need tooinstall kubernetes cluster keys into your kubectl tool.</span></span> <span data-ttu-id="6724f-114">Это можно сделать с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6724f-114">You can do that with hello following command:</span></span>
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a><span data-ttu-id="6724f-115">Мониторинг контейнеров с помощью Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="6724f-115">Monitoring Containers with Operations Management Suite (OMS)</span></span>

<span data-ttu-id="6724f-116">Microsoft Operations Management (OMS) — это облачное решение Майкрософт для управления ИТ-средой, которое помогает управлять локальной и облачной инфраструктурой и защищать ее.</span><span class="sxs-lookup"><span data-stu-id="6724f-116">Microsoft Operations Management (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="6724f-117">Решение контейнер — это решение в аналитику журнала OMS, служащей для просмотра данных инвентаризации контейнера hello, производительности и журналов в одном месте.</span><span class="sxs-lookup"><span data-stu-id="6724f-117">Container Solution is a solution in OMS Log Analytics, which helps you view hello container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="6724f-118">Аудит, устранение неполадок контейнеры путем просмотра журналов hello в центральном расположении и найти шумный использование лишние контейнер на узле.</span><span class="sxs-lookup"><span data-stu-id="6724f-118">You can audit, troubleshoot containers by viewing hello logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="6724f-119">Дополнительные сведения о решении контейнера можно найти toothe [анализа журналов контейнера решение](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="6724f-119">For more information about Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="installing-oms-on-kubernetes"></a><span data-ttu-id="6724f-120">Установка OMS в Kubernetes</span><span class="sxs-lookup"><span data-stu-id="6724f-120">Installing OMS on Kubernetes</span></span>

### <a name="obtain-your-workspace-id-and-key"></a><span data-ttu-id="6724f-121">Получение идентификатора и ключа рабочей области</span><span class="sxs-lookup"><span data-stu-id="6724f-121">Obtain your workspace ID and key</span></span>
<span data-ttu-id="6724f-122">Hello службы toohello tootalk агента OMS должен toobe настроены идентификатор рабочей области и ключ рабочей области.</span><span class="sxs-lookup"><span data-stu-id="6724f-122">For hello OMS agent tootalk toohello service it needs toobe configured with a workspace id and a workspace key.</span></span> <span data-ttu-id="6724f-123">идентификатор рабочей области tooget hello и toocreate OMS ключа учетной записи в <https://mms.microsoft.com>. Выполните шаги hello toocreate учетную запись.</span><span class="sxs-lookup"><span data-stu-id="6724f-123">tooget hello workspace id and key you need toocreate an OMS account at <https://mms.microsoft.com>. Please follow hello steps toocreate an account.</span></span> <span data-ttu-id="6724f-124">После завершения создания учетной записи hello, вам потребуется tooobtain идентификатор и ключ, щелкнув **параметры**, затем **подключенные источники**, а затем **серверы Linux**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="6724f-124">Once you are done creating hello account, you need tooobtain your id and key by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-hello-oms-agent-using-a-daemonset"></a><span data-ttu-id="6724f-125">Установка агента OMS hello, с помощью DaemonSet</span><span class="sxs-lookup"><span data-stu-id="6724f-125">Install hello OMS agent using a DaemonSet</span></span>
<span data-ttu-id="6724f-126">DaemonSets используются Kubernetes toorun один экземпляр контейнера на каждом узле в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="6724f-126">DaemonSets are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="6724f-127">Они идеально подходят для выполнения агентов мониторинга.</span><span class="sxs-lookup"><span data-stu-id="6724f-127">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="6724f-128">Вот hello [DaemonSet YAML файл](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span><span class="sxs-lookup"><span data-stu-id="6724f-128">Here is hello [DaemonSet YAML file](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span></span> <span data-ttu-id="6724f-129">Сохраните файл с именем файла tooa `oms-daemonset.yaml` и замените значения заполнителя hello `WSID` и `KEY` с идентификатор рабочей области и ключ в файле hello.</span><span class="sxs-lookup"><span data-stu-id="6724f-129">Save it tooa file named `oms-daemonset.yaml` and replace hello place-holder values for `WSID` and `KEY` with your workspace id and key in hello file.</span></span>

<span data-ttu-id="6724f-130">После добавления идентификатор рабочей области и ключа toohello DaemonSet конфигурации, можно установить агент OMS hello в кластере с hello `kubectl` средство командной строки:</span><span class="sxs-lookup"><span data-stu-id="6724f-130">Once you have added your workspace ID and key toohello DaemonSet configuration, you can install hello OMS agent on your cluster with hello `kubectl` command line tool:</span></span>

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-hello-oms-agent-using-a-kubernetes-secret"></a><span data-ttu-id="6724f-131">Установка агента OMS hello, с помощью Kubernetes секрета</span><span class="sxs-lookup"><span data-stu-id="6724f-131">Installing hello OMS agent using a Kubernetes Secret</span></span>
<span data-ttu-id="6724f-132">tooprotect свой идентификатор рабочей области OMS и ключ, можно использовать как часть файла DaemonSet YAML Kubernetes секрет.</span><span class="sxs-lookup"><span data-stu-id="6724f-132">tooprotect your OMS workspace ID and key you can use Kubernetes Secret as a part of DaemonSet YAML file.</span></span>

 - <span data-ttu-id="6724f-133">Скопируйте сценарий hello, файл шаблона секретный и hello DaemonSet YAML файл (из [репозитория](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) и убедитесь, что они находятся на hello один каталог.</span><span class="sxs-lookup"><span data-stu-id="6724f-133">Copy hello script, secret template file and hello DaemonSet YAML file (from [repository](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) and make sure they are on hello same directory.</span></span> 
      - <span data-ttu-id="6724f-134">Сценарий создания секретов — secret-gen.sh.</span><span class="sxs-lookup"><span data-stu-id="6724f-134">secret generating script - secret-gen.sh</span></span>
      - <span data-ttu-id="6724f-135">Шаблон секретов — secret-template.yaml.</span><span class="sxs-lookup"><span data-stu-id="6724f-135">secret template - secret-template.yaml</span></span>
   - <span data-ttu-id="6724f-136">YAML-файл DaemonSet — omsagent-ds-secrets.yaml.</span><span class="sxs-lookup"><span data-stu-id="6724f-136">DaemonSet YAML file - omsagent-ds-secrets.yaml</span></span>
 - <span data-ttu-id="6724f-137">Запустите сценарий hello.</span><span class="sxs-lookup"><span data-stu-id="6724f-137">Run hello script.</span></span> <span data-ttu-id="6724f-138">Hello скрипт будет запрашивать hello идентификатор рабочей области OMS и первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="6724f-138">hello script will ask for hello OMS Workspace ID and Primary Key.</span></span> <span data-ttu-id="6724f-139">Вставьте, и hello сценарий создаст файл секретный yaml, чтобы можно было запустить.</span><span class="sxs-lookup"><span data-stu-id="6724f-139">Please insert that and hello script will create a secret yaml file so you can run it.</span></span>   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - <span data-ttu-id="6724f-140">Создайте pod hello секретные данные, выполнив следующие hello:``` kubectl create -f omsagentsecret.yaml ```</span><span class="sxs-lookup"><span data-stu-id="6724f-140">Create hello secrets pod by running hello following: ``` kubectl create -f omsagentsecret.yaml ```</span></span>
 
   - <span data-ttu-id="6724f-141">toocheck hello следующей:</span><span class="sxs-lookup"><span data-stu-id="6724f-141">toocheck, run hello following:</span></span> 

   ``` 
   root@ubuntu16-13db:~# kubectl get secrets
   NAME                  TYPE                                  DATA      AGE
   default-token-gvl91   kubernetes.io/service-account-token   3         50d
   omsagent-secret       Opaque                                2         1d
   root@ubuntu16-13db:~# kubectl describe secrets omsagent-secret
   Name:           omsagent-secret
   Namespace:      default
   Labels:         <none>
   Annotations:    <none>

   Type:   Opaque

   Data
   ====
   WSID:   36 bytes
   KEY:    88 bytes 
   ```
 
  - <span data-ttu-id="6724f-142">Создание свой набор daemon-set omsagent, выполнив команду ``` kubectl create -f omsagent-ds-secrets.yaml ```</span><span class="sxs-lookup"><span data-stu-id="6724f-142">Create your omsagent daemon-set by running ``` kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

### <a name="conclusion"></a><span data-ttu-id="6724f-143">Заключение</span><span class="sxs-lookup"><span data-stu-id="6724f-143">Conclusion</span></span>
<span data-ttu-id="6724f-144">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="6724f-144">That's it!</span></span> <span data-ttu-id="6724f-145">Через несколько минут должно быть возможности toosee данными, поступающими tooyour мониторинга OMS.</span><span class="sxs-lookup"><span data-stu-id="6724f-145">After a few minutes, you should be able toosee data flowing tooyour OMS dashboard.</span></span>
