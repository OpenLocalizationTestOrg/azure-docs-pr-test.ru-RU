---
title: "контейнеры aaaDeploy с Helm в Azure Kubernetes | Документы Microsoft"
description: "Используйте hello Helm упаковки средство toodeploy контейнеры в кластере Kubernetes в контейнере службы Azure"
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/10/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: c7bd780afe00084ebe4e3a14873e1e340a29d144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-helm-toodeploy-containers-on-a-kubernetes-cluster"></a><span data-ttu-id="e65d2-103">Использование контейнеров toodeploy Helm в кластере Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e65d2-103">Use Helm toodeploy containers on a Kubernetes cluster</span></span> 

<span data-ttu-id="e65d2-104">[Helm](https://github.com/kubernetes/helm/) — это средство упаковки с открытым исходным кодом, которое поможет вам установить и управление жизненным циклом hello Kubernetes приложений.</span><span class="sxs-lookup"><span data-stu-id="e65d2-104">[Helm](https://github.com/kubernetes/helm/) is an open-source packaging tool that helps you install and manage hello lifecycle of Kubernetes applications.</span></span> <span data-ttu-id="e65d2-105">Аналогичные tooLinux пакета диспетчерами, например Apt get и Yum, Helm — используется toomanage Kubernetes диаграммы, которые являются пакетами предварительно настроенных Kubernetes ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e65d2-105">Similar tooLinux package managers such as Apt-get and Yum, Helm is used toomanage Kubernetes charts, which are packages of preconfigured Kubernetes resources.</span></span> <span data-ttu-id="e65d2-106">В этой статье показано, как toowork с Helm на кластере Kubernetes развертывание в службе контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="e65d2-106">This article shows you how toowork with Helm on a Kubernetes cluster deployed in Azure Container Service.</span></span>

<span data-ttu-id="e65d2-107">Helm состоит из двух компонентов:</span><span class="sxs-lookup"><span data-stu-id="e65d2-107">Helm has two components:</span></span> 
* <span data-ttu-id="e65d2-108">Hello **Helm CLI** клиента, который работает на компьютере, локально или в облаке hello</span><span class="sxs-lookup"><span data-stu-id="e65d2-108">hello **Helm CLI** is a client that runs on your machine locally or in hello cloud</span></span>  

* <span data-ttu-id="e65d2-109">**Tiller** — это сервер, работающий на кластере Kubernetes hello и управление жизненным циклом приложений Kubernetes hello</span><span class="sxs-lookup"><span data-stu-id="e65d2-109">**Tiller** is a server that runs on hello Kubernetes cluster and manages hello lifecycle of your Kubernetes applications</span></span> 
 
## <a name="prerequisites"></a><span data-ttu-id="e65d2-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e65d2-110">Prerequisites</span></span>

* <span data-ttu-id="e65d2-111">[Создание кластера Kubernetes](container-service-kubernetes-walkthrough.md) в Службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="e65d2-111">[Create a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>

* <span data-ttu-id="e65d2-112">[Установка и настройка`kubectl`](../container-service-connect.md) на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="e65d2-112">[Install and configure `kubectl`](../container-service-connect.md) on a local computer</span></span>

* <span data-ttu-id="e65d2-113">[Установка Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="e65d2-113">[Install Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) on a local computer</span></span>

## <a name="helm-basics"></a><span data-ttu-id="e65d2-114">Основы использования Helm</span><span class="sxs-lookup"><span data-stu-id="e65d2-114">Helm basics</span></span> 

<span data-ttu-id="e65d2-115">tooview сведения о hello Kubernetes кластера, установке Tiller и развертывания приложений введите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e65d2-115">tooview information about hello Kubernetes cluster that you are installing Tiller and deploying your applications to, type hello following command:</span></span>

```bash
kubectl cluster-info 
```
![kubectl cluster-info](./media/container-service-kubernetes-helm/clusterinfo.png)
 
<span data-ttu-id="e65d2-117">После установки Helm установки Tiller в кластере Kubernetes введите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e65d2-117">After you have installed Helm, install Tiller on your Kubernetes cluster by typing hello following command:</span></span>

```bash
helm init --upgrade
```
<span data-ttu-id="e65d2-118">После успешного завершения, вывод имеет hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e65d2-118">When it completes successfully, you see output like hello following:</span></span>

![Установка Tiller](./media/container-service-kubernetes-helm/tiller-install.png)
 
 
 
 
<span data-ttu-id="e65d2-120">tooview все hello Helm диаграммы доступен в репозитории hello, тип hello следующих команд:</span><span class="sxs-lookup"><span data-stu-id="e65d2-120">tooview all hello Helm charts available in hello repository, type hello following command:</span></span>

```bash 
helm search 
```

<span data-ttu-id="e65d2-121">Вывод hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e65d2-121">You see output like hello following:</span></span>

![Поиск Helm](./media/container-service-kubernetes-helm/helm-search.png)
 
<span data-ttu-id="e65d2-123">tooupdate hello диаграммы tooget hello последние версии, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e65d2-123">tooupdate hello charts tooget hello latest versions, type:</span></span>

```bash 
helm repo update 
```
## <a name="deploy-an-nginx-ingress-controller-chart"></a><span data-ttu-id="e65d2-124">Развертывание чарта входящего контроллера Nginx</span><span class="sxs-lookup"><span data-stu-id="e65d2-124">Deploy an Nginx ingress controller chart</span></span> 
 
<span data-ttu-id="e65d2-125">toodeploy диаграммы контроллера входящих Nginx, введите одну команду:</span><span class="sxs-lookup"><span data-stu-id="e65d2-125">toodeploy an Nginx ingress controller chart, type a single command:</span></span>

```bash
helm install stable/nginx-ingress 
```
![Развертывание входящего контроллера](./media/container-service-kubernetes-helm/nginx-ingress.png)

<span data-ttu-id="e65d2-127">Если ввести `kubectl get svc` tooview всех служб, выполняющихся на кластере hello, вы видите, что IP-адрес назначается toohello входящих контроллера.</span><span class="sxs-lookup"><span data-stu-id="e65d2-127">If you type `kubectl get svc` tooview all services that are running on hello cluster, you see that an IP address is assigned toohello ingress controller.</span></span> <span data-ttu-id="e65d2-128">(Hello назначения во время выполнения, вы видите `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="e65d2-128">(While hello assignment is in progress, you see `<pending>`.</span></span> <span data-ttu-id="e65d2-129">Она принимает ряд toocomplete мин.)</span><span class="sxs-lookup"><span data-stu-id="e65d2-129">It takes a couple of minutes toocomplete.)</span></span> 

<span data-ttu-id="e65d2-130">После назначения IP-адрес hello перейдите toohello значение hello внешнего IP адрес toosee hello Nginx серверной под управлением.</span><span class="sxs-lookup"><span data-stu-id="e65d2-130">After hello IP address is assigned, navigate toohello value of hello external IP address toosee hello Nginx backend running.</span></span> 
 
![Входящий IP-адрес](./media/container-service-kubernetes-helm/ingress-ip-address.png)


<span data-ttu-id="e65d2-132">toosee списка установлены в кластере типа диаграмм:</span><span class="sxs-lookup"><span data-stu-id="e65d2-132">toosee a list of charts installed on your cluster, type:</span></span>

```bash
helm list 
```

<span data-ttu-id="e65d2-133">Можно сократить команда hello слишком`helm ls`.</span><span class="sxs-lookup"><span data-stu-id="e65d2-133">You can abbreviate hello command too`helm ls`.</span></span>
 
 
 
 
## <a name="deploy-a-mariadb-chart-and-client"></a><span data-ttu-id="e65d2-134">Развертывание клиента и чарта MariaDB</span><span class="sxs-lookup"><span data-stu-id="e65d2-134">Deploy a MariaDB chart and client</span></span>

<span data-ttu-id="e65d2-135">Теперь можно разверните диаграмму MariaDB и tooconnect toohello MariaDB клиентской базе данных.</span><span class="sxs-lookup"><span data-stu-id="e65d2-135">Now deploy a MariaDB chart and a MariaDB client tooconnect toohello database.</span></span>

<span data-ttu-id="e65d2-136">Диаграмма MariaDB hello toodeploy, тип hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e65d2-136">toodeploy hello MariaDB chart, type hello following command:</span></span>

```bash
helm install --name v1 stable/mariadb
```

<span data-ttu-id="e65d2-137">здесь `--name` — тег, используемый для выпусков.</span><span class="sxs-lookup"><span data-stu-id="e65d2-137">where `--name` is a tag used for releases.</span></span>

> [!TIP]
> <span data-ttu-id="e65d2-138">Если происходит сбой развертывания hello, запустите `helm repo update` и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="e65d2-138">If hello deployment fails, run `helm repo update` and try again.</span></span>
>
 
 
<span data-ttu-id="e65d2-139">tooview развернуть все hello диаграммы кластера, тип:</span><span class="sxs-lookup"><span data-stu-id="e65d2-139">tooview all hello charts deployed on your cluster, type:</span></span>

```bash 
helm list
```
 
<span data-ttu-id="e65d2-140">tooview всех развертываний, работающих в кластере, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e65d2-140">tooview all deployments running on your cluster, type:</span></span>

```bash
kubectl get deployments 
``` 
 
 
<span data-ttu-id="e65d2-141">Наконец toorun клиент hello tooaccess pod, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e65d2-141">Finally, toorun a pod tooaccess hello client, type:</span></span>

```bash
kubectl run v1-mariadb-client --rm --tty -i --image bitnami/mariadb --command -- bash  
``` 
 
 
<span data-ttu-id="e65d2-142">Клиент toohello tooconnect, тип hello следующую команду, заменив `v1-mariadb` с именем hello развертывания:</span><span class="sxs-lookup"><span data-stu-id="e65d2-142">tooconnect toohello client, type hello following command, replacing `v1-mariadb` with hello name of your deployment:</span></span>

```bash
sudo mysql –h v1-mariadb
```
 
 
<span data-ttu-id="e65d2-143">Теперь можно использовать обычные БД toocreate команды SQL, таблицы и т. д. Например, `Create DATABASE testdb1;` создает пустую базу данных.</span><span class="sxs-lookup"><span data-stu-id="e65d2-143">You can now use standard SQL commands toocreate databases, tables, etc. For example, `Create DATABASE testdb1;` creates an empty database.</span></span> 
 
 
 
## <a name="next-steps"></a><span data-ttu-id="e65d2-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e65d2-144">Next steps</span></span>

* <span data-ttu-id="e65d2-145">Дополнительные сведения об управлении Kubernetes диаграммы см. в разделе hello [Helm документации](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span><span class="sxs-lookup"><span data-stu-id="e65d2-145">For more information about managing Kubernetes charts, see hello [Helm documentation](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span></span> 

