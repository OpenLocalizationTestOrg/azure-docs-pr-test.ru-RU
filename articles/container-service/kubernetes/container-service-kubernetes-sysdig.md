---
title: "кластер Azure Kubernetes aaaMonitor - Sysdig | Документы Microsoft"
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
ms.openlocfilehash: a27813d01ee4624b9e993f6185169ad73aeec3a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-using-sysdig"></a><span data-ttu-id="657ba-103">Мониторинг кластера Kubernetes в Службе контейнеров Azure с помощью Sysdig</span><span class="sxs-lookup"><span data-stu-id="657ba-103">Monitor an Azure Container Service Kubernetes cluster using Sysdig</span></span>

## <a name="prerequisites"></a><span data-ttu-id="657ba-104">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="657ba-104">Prerequisites</span></span>
<span data-ttu-id="657ba-105">В этом пошаговом руководстве предполагается, что вы [создали кластер Kubernetes с помощью службы контейнеров Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="657ba-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="657ba-106">Он также предполагается, что hello azure cli и kubectl установлены инструменты.</span><span class="sxs-lookup"><span data-stu-id="657ba-106">It also assumes that you have hello azure cli and kubectl tools installed.</span></span>

<span data-ttu-id="657ba-107">Можно проверить при наличии hello `az` установить, запустив средство:</span><span class="sxs-lookup"><span data-stu-id="657ba-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="657ba-108">Если у вас нет hello `az` средство установки приведены инструкции по [здесь](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="657ba-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="657ba-109">Можно проверить при наличии hello `kubectl` установить, запустив средство:</span><span class="sxs-lookup"><span data-stu-id="657ba-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="657ba-110">Если средство `kubectl` не установлено, выполните команду:</span><span class="sxs-lookup"><span data-stu-id="657ba-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="sysdig"></a><span data-ttu-id="657ba-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="657ba-111">Sysdig</span></span>
<span data-ttu-id="657ba-112">Sysdig является компанией, предоставляющей внешний мониторинг как услугу, которая может отслеживать контейнеры в кластере Kubernetes, работающем в Azure.</span><span class="sxs-lookup"><span data-stu-id="657ba-112">Sysdig is an external monitoring as a service company which can monitor containers in your Kubernetes cluster running in Azure.</span></span> <span data-ttu-id="657ba-113">Для использования услуг Sysdig требуется активная учетная запись Sysdig.</span><span class="sxs-lookup"><span data-stu-id="657ba-113">Using Sysdig requires an active Sysdig account.</span></span>
<span data-ttu-id="657ba-114">Зарегистрироваться для получения учетной записи можно на [сайте компании](https://app.sysdigcloud.com).</span><span class="sxs-lookup"><span data-stu-id="657ba-114">You can sign up for an account on their [site](https://app.sysdigcloud.com).</span></span>

<span data-ttu-id="657ba-115">После входа в toohello Sysdig облачные и веб-сайт, щелкните имя пользователя, и на странице приветствия вы увидите «Ключа доступа.»</span><span class="sxs-lookup"><span data-stu-id="657ba-115">Once you're logged in toohello Sysdig cloud website, click on your user name, and on hello page you should see your "Access Key."</span></span> 

![Sysdig: ключ API](./media/container-service-kubernetes-sysdig/sysdig2.png)

## <a name="installing-hello-sysdig-agents-tookubernetes"></a><span data-ttu-id="657ba-117">Установка агентов tooKubernetes hello Sysdig</span><span class="sxs-lookup"><span data-stu-id="657ba-117">Installing hello Sysdig agents tooKubernetes</span></span>
<span data-ttu-id="657ba-118">toomonitor вашей контейнеры Sysdig запускается процесс на каждом компьютере, с помощью Kubernetes `DaemonSet`.</span><span class="sxs-lookup"><span data-stu-id="657ba-118">toomonitor your containers, Sysdig runs a process on each machine using a Kubernetes `DaemonSet`.</span></span>
<span data-ttu-id="657ba-119">Наборы DaemonSet являются объектами API Kubernetes, которые выполняют отдельный экземпляр контейнера на каждом компьютере.</span><span class="sxs-lookup"><span data-stu-id="657ba-119">DaemonSets are Kubernetes API objects that run a single instance of a container per machine.</span></span>
<span data-ttu-id="657ba-120">Они идеально подходит для установки средства, такие как hello Sysdig агент мониторинга.</span><span class="sxs-lookup"><span data-stu-id="657ba-120">They're perfect for installing tools like hello Sysdig's monitoring agent.</span></span>

<span data-ttu-id="657ba-121">tooinstall hello Sysdig daemonset, следует сначала загрузить [шаблона hello](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) из sysdig.</span><span class="sxs-lookup"><span data-stu-id="657ba-121">tooinstall hello Sysdig daemonset, you should first download [hello template](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) from sysdig.</span></span> <span data-ttu-id="657ba-122">Сохраните этот файл как `sysdig-daemonset.yaml`.</span><span class="sxs-lookup"><span data-stu-id="657ba-122">Save that file as `sysdig-daemonset.yaml`.</span></span>

<span data-ttu-id="657ba-123">В Linux и OS X можно выполнить команду:</span><span class="sxs-lookup"><span data-stu-id="657ba-123">On Linux and OS X you can run:</span></span>

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

<span data-ttu-id="657ba-124">В PowerShell:</span><span class="sxs-lookup"><span data-stu-id="657ba-124">In PowerShell:</span></span>

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

<span data-ttu-id="657ba-125">Далее следует Измените свой ключ доступа, который получен из вашей учетной записи Sysdig tooinsert этого файла.</span><span class="sxs-lookup"><span data-stu-id="657ba-125">Next edit that file tooinsert your Access Key, that you obtained from your Sysdig account.</span></span>

<span data-ttu-id="657ba-126">Наконец создайте hello DaemonSet:</span><span class="sxs-lookup"><span data-stu-id="657ba-126">Finally, create hello DaemonSet:</span></span>

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a><span data-ttu-id="657ba-127">Просмотр данных мониторинга</span><span class="sxs-lookup"><span data-stu-id="657ba-127">View your monitoring</span></span>
<span data-ttu-id="657ba-128">После установки и запуска агентов hello должен выдавать задней tooSysdig данных.</span><span class="sxs-lookup"><span data-stu-id="657ba-128">Once installed and running, hello agents should pump data back tooSysdig.</span></span>  <span data-ttu-id="657ba-129">Вернитесь к предыдущему окну toothe [sysdig мониторинга](https://app.sysdigcloud.com) и вы увидите сведения о вашей контейнерах.</span><span class="sxs-lookup"><span data-stu-id="657ba-129">Go back toothe [sysdig dashboard](https://app.sysdigcloud.com) and you should see information about your containers.</span></span>

<span data-ttu-id="657ba-130">Вы можете также установить панели мониторинга для Kubernetes с помощью [мастера создания панелей мониторинга](https://app.sysdigcloud.com/#/dashboards/new).</span><span class="sxs-lookup"><span data-stu-id="657ba-130">You can also install Kubernetes-specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
