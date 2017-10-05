---
title: "Развертывание контейнеров с помощью Helm в Azure Kubernetes | Документы Майкрософт"
description: "Использование средства упаковки Helm для развертывания контейнеров в кластере Kubernetes в Службе контейнеров Azure"
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
ms.openlocfilehash: 3cfcc5abbee03ca8fbbec4e4eae711e7c2d9deae
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="use-helm-to-deploy-containers-on-a-kubernetes-cluster"></a><span data-ttu-id="b8114-103">Использование Helm для развертывания контейнеров в кластере Kubernetes Helm</span><span class="sxs-lookup"><span data-stu-id="b8114-103">Use Helm to deploy containers on a Kubernetes cluster</span></span> 

<span data-ttu-id="b8114-104">[Helm](https://github.com/kubernetes/helm/) — это средство упаковки с открытым исходным кодом, которое помогает установить приложения Kubernetes и управлять их жизненным циклом.</span><span class="sxs-lookup"><span data-stu-id="b8114-104">[Helm](https://github.com/kubernetes/helm/) is an open-source packaging tool that helps you install and manage the lifecycle of Kubernetes applications.</span></span> <span data-ttu-id="b8114-105">Аналогично диспетчерам пакетов Linux, таких как Apt-get и Yum, Helm используется для управления чартами Kubernetes, представляющими собой пакеты предварительно настроенных ресурсов Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="b8114-105">Similar to Linux package managers such as Apt-get and Yum, Helm is used to manage Kubernetes charts, which are packages of preconfigured Kubernetes resources.</span></span> <span data-ttu-id="b8114-106">В этой статье показано, как работать с Helm в кластере Kubernetes, развернутом в Службе контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="b8114-106">This article shows you how to work with Helm on a Kubernetes cluster deployed in Azure Container Service.</span></span>

<span data-ttu-id="b8114-107">Helm состоит из двух компонентов:</span><span class="sxs-lookup"><span data-stu-id="b8114-107">Helm has two components:</span></span> 
* <span data-ttu-id="b8114-108">**Helm CLI** — клиент, который выполняется на компьютере локально или в облаке.</span><span class="sxs-lookup"><span data-stu-id="b8114-108">The **Helm CLI** is a client that runs on your machine locally or in the cloud</span></span>  

* <span data-ttu-id="b8114-109">**Tiller** — сервер, который выполняется в кластере Kubernetes и управляет жизненным циклом приложений Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="b8114-109">**Tiller** is a server that runs on the Kubernetes cluster and manages the lifecycle of your Kubernetes applications</span></span> 
 
## <a name="prerequisites"></a><span data-ttu-id="b8114-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b8114-110">Prerequisites</span></span>

* <span data-ttu-id="b8114-111">[Создание кластера Kubernetes](container-service-kubernetes-walkthrough.md) в Службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="b8114-111">[Create a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>

* <span data-ttu-id="b8114-112">[Установка и настройка`kubectl`](../container-service-connect.md) на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="b8114-112">[Install and configure `kubectl`](../container-service-connect.md) on a local computer</span></span>

* <span data-ttu-id="b8114-113">[Установка Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="b8114-113">[Install Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) on a local computer</span></span>

## <a name="helm-basics"></a><span data-ttu-id="b8114-114">Основы использования Helm</span><span class="sxs-lookup"><span data-stu-id="b8114-114">Helm basics</span></span> 

<span data-ttu-id="b8114-115">Чтобы просмотреть сведения о кластере Kubernetes, где вы устанавливаете Tiller и развертываете приложения, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b8114-115">To view information about the Kubernetes cluster that you are installing Tiller and deploying your applications to, type the following command:</span></span>

```bash
kubectl cluster-info 
```
![kubectl cluster-info](./media/container-service-kubernetes-helm/clusterinfo.png)
 
<span data-ttu-id="b8114-117">После установки Helm установите Tiller в кластере Kubernetes, введя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b8114-117">After you have installed Helm, install Tiller on your Kubernetes cluster by typing the following command:</span></span>

```bash
helm init --upgrade
```
<span data-ttu-id="b8114-118">После успешного завершения команды выводятся сведения следующего вида:</span><span class="sxs-lookup"><span data-stu-id="b8114-118">When it completes successfully, you see output like the following:</span></span>

![Установка Tiller](./media/container-service-kubernetes-helm/tiller-install.png)
 
 
 
 
<span data-ttu-id="b8114-120">Чтобы просмотреть все доступные чарты Helm в репозитории, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b8114-120">To view all the Helm charts available in the repository, type the following command:</span></span>

```bash 
helm search 
```

<span data-ttu-id="b8114-121">Выводятся сведения следующего вида:</span><span class="sxs-lookup"><span data-stu-id="b8114-121">You see output like the following:</span></span>

![Поиск Helm](./media/container-service-kubernetes-helm/helm-search.png)
 
<span data-ttu-id="b8114-123">Чтобы обновить чарты для использования актуальных версий, введите:</span><span class="sxs-lookup"><span data-stu-id="b8114-123">To update the charts to get the latest versions, type:</span></span>

```bash 
helm repo update 
```
## <a name="deploy-an-nginx-ingress-controller-chart"></a><span data-ttu-id="b8114-124">Развертывание чарта входящего контроллера Nginx</span><span class="sxs-lookup"><span data-stu-id="b8114-124">Deploy an Nginx ingress controller chart</span></span> 
 
<span data-ttu-id="b8114-125">Чтобы развернуть чарт входящего контроллера Nginx, введите одну команду:</span><span class="sxs-lookup"><span data-stu-id="b8114-125">To deploy an Nginx ingress controller chart, type a single command:</span></span>

```bash
helm install stable/nginx-ingress 
```
![Развертывание входящего контроллера](./media/container-service-kubernetes-helm/nginx-ingress.png)

<span data-ttu-id="b8114-127">Если ввести `kubectl get svc` для просмотра всех служб, запущенных на кластере, вы увидите, что IP-адрес назначен входящему контроллеру.</span><span class="sxs-lookup"><span data-stu-id="b8114-127">If you type `kubectl get svc` to view all services that are running on the cluster, you see that an IP address is assigned to the ingress controller.</span></span> <span data-ttu-id="b8114-128">(Пока идет назначение, отображается `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="b8114-128">(While the assignment is in progress, you see `<pending>`.</span></span> <span data-ttu-id="b8114-129">Для завершения операции требуется несколько минут.)</span><span class="sxs-lookup"><span data-stu-id="b8114-129">It takes a couple of minutes to complete.)</span></span> 

<span data-ttu-id="b8114-130">После назначения IP-адреса перейдите к значению внешнего IP-адреса, чтобы увидеть работу серверной части Nginx.</span><span class="sxs-lookup"><span data-stu-id="b8114-130">After the IP address is assigned, navigate to the value of the external IP address to see the Nginx backend running.</span></span> 
 
![Входящий IP-адрес](./media/container-service-kubernetes-helm/ingress-ip-address.png)


<span data-ttu-id="b8114-132">Чтобы просмотреть список чартов, установленных в кластере, введите:</span><span class="sxs-lookup"><span data-stu-id="b8114-132">To see a list of charts installed on your cluster, type:</span></span>

```bash
helm list 
```

<span data-ttu-id="b8114-133">Команду можно сократить до `helm ls`.</span><span class="sxs-lookup"><span data-stu-id="b8114-133">You can abbreviate the command to `helm ls`.</span></span>
 
 
 
 
## <a name="deploy-a-mariadb-chart-and-client"></a><span data-ttu-id="b8114-134">Развертывание клиента и чарта MariaDB</span><span class="sxs-lookup"><span data-stu-id="b8114-134">Deploy a MariaDB chart and client</span></span>

<span data-ttu-id="b8114-135">Разверните чарт и клиент MariaDB для подключения к базе данных.</span><span class="sxs-lookup"><span data-stu-id="b8114-135">Now deploy a MariaDB chart and a MariaDB client to connect to the database.</span></span>

<span data-ttu-id="b8114-136">Чтобы развернуть чарт MariaDB, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b8114-136">To deploy the MariaDB chart, type the following command:</span></span>

```bash
helm install --name v1 stable/mariadb
```

<span data-ttu-id="b8114-137">здесь `--name` — тег, используемый для выпусков.</span><span class="sxs-lookup"><span data-stu-id="b8114-137">where `--name` is a tag used for releases.</span></span>

> [!TIP]
> <span data-ttu-id="b8114-138">Если развертывание завершается сбоем, запустите `helm repo update` и повторите попытку.</span><span class="sxs-lookup"><span data-stu-id="b8114-138">If the deployment fails, run `helm repo update` and try again.</span></span>
>
 
 
<span data-ttu-id="b8114-139">Для просмотра всех чартов, развернутых в кластере, введите:</span><span class="sxs-lookup"><span data-stu-id="b8114-139">To view all the charts deployed on your cluster, type:</span></span>

```bash 
helm list
```
 
<span data-ttu-id="b8114-140">Для просмотра всех развертываний, запущенных в кластере, введите:</span><span class="sxs-lookup"><span data-stu-id="b8114-140">To view all deployments running on your cluster, type:</span></span>

```bash
kubectl get deployments 
``` 
 
 
<span data-ttu-id="b8114-141">Наконец, чтобы запустить pod для доступа к клиенту, введите:</span><span class="sxs-lookup"><span data-stu-id="b8114-141">Finally, to run a pod to access the client, type:</span></span>

```bash
kubectl run v1-mariadb-client --rm --tty -i --image bitnami/mariadb --command -- bash  
``` 
 
 
<span data-ttu-id="b8114-142">Чтобы подключиться к клиенту, введите следующую команду, заменив `v1-mariadb` на имя развертывания:</span><span class="sxs-lookup"><span data-stu-id="b8114-142">To connect to the client, type the following command, replacing `v1-mariadb` with the name of your deployment:</span></span>

```bash
sudo mysql –h v1-mariadb
```
 
 
<span data-ttu-id="b8114-143">Теперь можно использовать стандартные команды SQL для создания базы данных, таблиц и т. д. Например, `Create DATABASE testdb1;` создает пустую базу данных.</span><span class="sxs-lookup"><span data-stu-id="b8114-143">You can now use standard SQL commands to create databases, tables, etc. For example, `Create DATABASE testdb1;` creates an empty database.</span></span> 
 
 
 
## <a name="next-steps"></a><span data-ttu-id="b8114-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b8114-144">Next steps</span></span>

* <span data-ttu-id="b8114-145">Дополнительные сведения об управлении чартами Kubernetes см. в [документации по Helm](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span><span class="sxs-lookup"><span data-stu-id="b8114-145">For more information about managing Kubernetes charts, see the [Helm documentation](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span></span> 

