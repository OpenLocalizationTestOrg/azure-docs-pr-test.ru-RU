---
title: "Мониторинг кластера Azure Kubernetes с помощью Sysdig | Документация Майкрософт"
description: "Мониторинг кластера Kubernetes в Службе контейнеров Azure с помощью Sysdig."
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
ms.openlocfilehash: afe22b84015526f901111238e36baaa94694ccbf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-using-sysdig"></a><span data-ttu-id="32cfd-103">Мониторинг кластера Kubernetes в Службе контейнеров Azure с помощью Sysdig</span><span class="sxs-lookup"><span data-stu-id="32cfd-103">Monitor an Azure Container Service Kubernetes cluster using Sysdig</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32cfd-104">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="32cfd-104">Prerequisites</span></span>
<span data-ttu-id="32cfd-105">В этом пошаговом руководстве предполагается, что вы [создали кластер Kubernetes с помощью службы контейнеров Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="32cfd-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="32cfd-106">Также предполагается, что у вас установлен интерфейс командной строки Azure и средство kubectl.</span><span class="sxs-lookup"><span data-stu-id="32cfd-106">It also assumes that you have the azure cli and kubectl tools installed.</span></span>

<span data-ttu-id="32cfd-107">Чтобы проверить наличие средства `az`, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="32cfd-107">You can test if you have the `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="32cfd-108">Если средство `az` не установлено, следуйте инструкциям, приведенным [здесь](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="32cfd-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="32cfd-109">Чтобы проверить наличие средства `kubectl`, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="32cfd-109">You can test if you have the `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="32cfd-110">Если средство `kubectl` не установлено, выполните команду:</span><span class="sxs-lookup"><span data-stu-id="32cfd-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="sysdig"></a><span data-ttu-id="32cfd-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="32cfd-111">Sysdig</span></span>
<span data-ttu-id="32cfd-112">Sysdig является компанией, предоставляющей внешний мониторинг как услугу, которая может отслеживать контейнеры в кластере Kubernetes, работающем в Azure.</span><span class="sxs-lookup"><span data-stu-id="32cfd-112">Sysdig is an external monitoring as a service company which can monitor containers in your Kubernetes cluster running in Azure.</span></span> <span data-ttu-id="32cfd-113">Для использования услуг Sysdig требуется активная учетная запись Sysdig.</span><span class="sxs-lookup"><span data-stu-id="32cfd-113">Using Sysdig requires an active Sysdig account.</span></span>
<span data-ttu-id="32cfd-114">Зарегистрироваться для получения учетной записи можно на [сайте компании](https://app.sysdigcloud.com).</span><span class="sxs-lookup"><span data-stu-id="32cfd-114">You can sign up for an account on their [site](https://app.sysdigcloud.com).</span></span>

<span data-ttu-id="32cfd-115">Войдите на облачный сайт Sysdig, щелкните свое имя пользователя. На странице отобразится ваш ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="32cfd-115">Once you're logged in to the Sysdig cloud website, click on your user name, and on the page you should see your "Access Key."</span></span> 

![Sysdig: ключ API](./media/container-service-kubernetes-sysdig/sysdig2.png)

## <a name="installing-the-sysdig-agents-to-kubernetes"></a><span data-ttu-id="32cfd-117">Установка агентов Sysdig в Kubernetes</span><span class="sxs-lookup"><span data-stu-id="32cfd-117">Installing the Sysdig agents to Kubernetes</span></span>
<span data-ttu-id="32cfd-118">Для мониторинга контейнеров Sysdig запускает на каждом компьютере процесс с помощью `DaemonSet` Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="32cfd-118">To monitor your containers, Sysdig runs a process on each machine using a Kubernetes `DaemonSet`.</span></span>
<span data-ttu-id="32cfd-119">Наборы DaemonSet являются объектами API Kubernetes, которые выполняют отдельный экземпляр контейнера на каждом компьютере.</span><span class="sxs-lookup"><span data-stu-id="32cfd-119">DaemonSets are Kubernetes API objects that run a single instance of a container per machine.</span></span>
<span data-ttu-id="32cfd-120">Они идеально подходят для установки инструментов, например агента мониторинга Sysdig.</span><span class="sxs-lookup"><span data-stu-id="32cfd-120">They're perfect for installing tools like the Sysdig's monitoring agent.</span></span>

<span data-ttu-id="32cfd-121">Чтобы установить DaemonSet Sysdig, следует сначала скачать [шаблон](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) с сайта Sysdig.</span><span class="sxs-lookup"><span data-stu-id="32cfd-121">To install the Sysdig daemonset, you should first download [the template](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) from sysdig.</span></span> <span data-ttu-id="32cfd-122">Сохраните этот файл как `sysdig-daemonset.yaml`.</span><span class="sxs-lookup"><span data-stu-id="32cfd-122">Save that file as `sysdig-daemonset.yaml`.</span></span>

<span data-ttu-id="32cfd-123">В Linux и OS X можно выполнить команду:</span><span class="sxs-lookup"><span data-stu-id="32cfd-123">On Linux and OS X you can run:</span></span>

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

<span data-ttu-id="32cfd-124">В PowerShell:</span><span class="sxs-lookup"><span data-stu-id="32cfd-124">In PowerShell:</span></span>

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

<span data-ttu-id="32cfd-125">Измените этот файл, чтобы вставить в него ключ доступа, который был получен из вашей учетной записи Sysdig.</span><span class="sxs-lookup"><span data-stu-id="32cfd-125">Next edit that file to insert your Access Key, that you obtained from your Sysdig account.</span></span>

<span data-ttu-id="32cfd-126">Наконец, создайте DaemonSet.</span><span class="sxs-lookup"><span data-stu-id="32cfd-126">Finally, create the DaemonSet:</span></span>

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a><span data-ttu-id="32cfd-127">Просмотр данных мониторинга</span><span class="sxs-lookup"><span data-stu-id="32cfd-127">View your monitoring</span></span>
<span data-ttu-id="32cfd-128">После установки и запуска агенты должны передавать данные обратно в Sysdig.</span><span class="sxs-lookup"><span data-stu-id="32cfd-128">Once installed and running, the agents should pump data back to Sysdig.</span></span>  <span data-ttu-id="32cfd-129">Вернитесь к [панели мониторинга Sysdig](https://app.sysdigcloud.com), и вы должны увидеть сведения о контейнерах.</span><span class="sxs-lookup"><span data-stu-id="32cfd-129">Go back to the [sysdig dashboard](https://app.sysdigcloud.com) and you should see information about your containers.</span></span>

<span data-ttu-id="32cfd-130">Вы можете также установить панели мониторинга для Kubernetes с помощью [мастера создания панелей мониторинга](https://app.sysdigcloud.com/#/dashboards/new).</span><span class="sxs-lookup"><span data-stu-id="32cfd-130">You can also install Kubernetes-specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
