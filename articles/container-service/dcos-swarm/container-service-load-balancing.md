---
title: "Балансировка нагрузки контейнеров в кластере DC/OS Azure | Документация Майкрософт"
description: "Сведения о балансировке нагрузки нескольких контейнеров в кластере DC/OS в Службе контейнеров Azure."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Контейнеры, микрослужбы, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 78725c9d23e13d307821a188028ef573d1def038
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="573b0-104">Балансировка нагрузки контейнеров в кластере DC/OS в Службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="573b0-104">Load balance containers in an Azure Container Service DC/OS cluster</span></span>
<span data-ttu-id="573b0-105">В этой статье рассматривается создание внутренней подсистемы балансировки нагрузки в управляемой службе контейнеров Azure DC/OS с помощью средства Marathon-LB.</span><span class="sxs-lookup"><span data-stu-id="573b0-105">In this article, we explore how to create an internal load balancer in a DC/OS managed Azure Container Service using Marathon-LB.</span></span> <span data-ttu-id="573b0-106">Это позволит масштабировать приложения по горизонтали.</span><span class="sxs-lookup"><span data-stu-id="573b0-106">This configuration enables you to scale your applications horizontally.</span></span> <span data-ttu-id="573b0-107">Вы также сможете воспользоваться преимуществами кластеров общедоступных и частных агентов, поместив подсистемы балансировки нагрузки в общедоступный кластер, а контейнеры приложений в частный кластер.</span><span class="sxs-lookup"><span data-stu-id="573b0-107">It also allows you to take advantage of the public and private agent clusters by placing your load balancers on the public cluster and your application containers on the private cluster.</span></span> <span data-ttu-id="573b0-108">Изучив это руководство, вы:</span><span class="sxs-lookup"><span data-stu-id="573b0-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="573b0-109">Настройка подсистемы балансировки нагрузки Marathon</span><span class="sxs-lookup"><span data-stu-id="573b0-109">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="573b0-110">Развертывание приложения с помощью подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="573b0-110">Deploy an application using the load balancer</span></span>
> * <span data-ttu-id="573b0-111">Настройка Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="573b0-111">Configure and Azure load balancer</span></span>

<span data-ttu-id="573b0-112">Для выполнения действий, описанных в этом руководстве, потребуется кластер ACS DC/OS.</span><span class="sxs-lookup"><span data-stu-id="573b0-112">You need an ACS DC/OS cluster to complete the steps in this tutorial.</span></span> <span data-ttu-id="573b0-113">При необходимости его можно создать с помощью следующего [примера сценария](./../kubernetes/scripts/container-service-cli-deploy-dcos.md).</span><span class="sxs-lookup"><span data-stu-id="573b0-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="573b0-114">Для этого руководства требуется Azure CLI версии 2.0.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="573b0-114">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="573b0-115">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="573b0-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="573b0-116">Если вам необходимо выполнить обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="573b0-116">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a><span data-ttu-id="573b0-117">Общие сведения о балансировке нагрузки</span><span class="sxs-lookup"><span data-stu-id="573b0-117">Load balancing overview</span></span>

<span data-ttu-id="573b0-118">В кластере DC/OS службы контейнеров Azure существует два уровня балансировки нагрузки:</span><span class="sxs-lookup"><span data-stu-id="573b0-118">There are two load-balancing layers in an Azure Container Service DC/OS cluster:</span></span> 

<span data-ttu-id="573b0-119">**Azure Load Balancer** предоставляет общедоступные точки входа (к ним будут обращаться пользователи).</span><span class="sxs-lookup"><span data-stu-id="573b0-119">**Azure Load Balancer** provides public entry points (the ones that end users access).</span></span> <span data-ttu-id="573b0-120">Azure Load Balancer предоставляется автоматически службой контейнеров Azure. По умолчанию для него настроены порты 80, 443 и 8080.</span><span class="sxs-lookup"><span data-stu-id="573b0-120">An Azure LB is provided automatically by Azure Container Service and is, by default, configured to expose port 80, 443 and 8080.</span></span>

<span data-ttu-id="573b0-121">**Подсистема балансировки нагрузки Marathon (marathon-lb)** направляет входящие запросы экземплярам контейнера для обслуживания.</span><span class="sxs-lookup"><span data-stu-id="573b0-121">**The Marathon Load Balancer (marathon-lb)** routes inbound requests to container instances that service these requests.</span></span> <span data-ttu-id="573b0-122">Marathon-lb приспосабливается к изменениям по мере масштабирования контейнеров, предоставляющих веб-службу.</span><span class="sxs-lookup"><span data-stu-id="573b0-122">As we scale the containers providing our web service, the marathon-lb dynamically adapts.</span></span> <span data-ttu-id="573b0-123">Эта подсистема балансировки нагрузки не предоставляется по умолчанию в службе контейнеров, но ее легко установить.</span><span class="sxs-lookup"><span data-stu-id="573b0-123">This load balancer is not provided by default in your Container Service, but it is easy to install.</span></span>

## <a name="configure-marathon-load-balancer"></a><span data-ttu-id="573b0-124">Настройка подсистемы балансировки нагрузки Marathon</span><span class="sxs-lookup"><span data-stu-id="573b0-124">Configure Marathon Load Balancer</span></span>

<span data-ttu-id="573b0-125">Балансировщик нагрузки Marathon динамически перенастраивается на основе развернутых контейнеров.</span><span class="sxs-lookup"><span data-stu-id="573b0-125">Marathon Load Balancer dynamically reconfigures itself based on the containers that you've deployed.</span></span> <span data-ttu-id="573b0-126">Она также устойчива к сбоям в работе контейнера или агента. В этой ситуации Apache Mesos просто перезапускает контейнер в другом расположении, и подсистема балансировки нагрузки marathon-lb перенастраивается.</span><span class="sxs-lookup"><span data-stu-id="573b0-126">It's also resilient to the loss of a container or an agent - if this occurs, Apache Mesos restarts the container elsewhere and marathon-lb adapts.</span></span>

<span data-ttu-id="573b0-127">Для установки подсистемы балансировки нагрузки в кластере открытого агента выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="573b0-127">Run the following command to install the marathon load balancer on the public agent's cluster.</span></span>

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a><span data-ttu-id="573b0-128">Развертывание приложения с балансировкой нагрузки</span><span class="sxs-lookup"><span data-stu-id="573b0-128">Deploy load balanced application</span></span>

<span data-ttu-id="573b0-129">Установив пакет балансировщика нагрузки Marathon, можно развернуть контейнер приложения, который нужно сбалансировать.</span><span class="sxs-lookup"><span data-stu-id="573b0-129">Now that we have the marathon-lb package, we can deploy an application container that we wish to load balance.</span></span> 

<span data-ttu-id="573b0-130">Получите полное доменное имя открытых агентов.</span><span class="sxs-lookup"><span data-stu-id="573b0-130">First, get the FQDN of the publicly exposed agents.</span></span>

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

<span data-ttu-id="573b0-131">Создайте файл с именем *hello-web.json* и вставьте в этот файл следующее содержимое.</span><span class="sxs-lookup"><span data-stu-id="573b0-131">Next, create a file named *hello-web.json* and copy in the following contents.</span></span> <span data-ttu-id="573b0-132">Метку `HAPROXY_0_VHOST` следует заменить на полное доменное имя агентов DC/OS.</span><span class="sxs-lookup"><span data-stu-id="573b0-132">The `HAPROXY_0_VHOST` label needs to be updated with the FQDN of the DC/OS agents.</span></span> 

```json
{
  "id": "web",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "yeasy/simple-web",
      "network": "BRIDGE",
      "portMappings": [
        { "hostPort": 0, "containerPort": 80, "servicePort": 10000 }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "labels":{
    "HAPROXY_GROUP":"external",
    "HAPROXY_0_VHOST":"YOUR FQDN",
    "HAPROXY_0_MODE":"http"
  }
}
```

<span data-ttu-id="573b0-133">Для запуска приложения используйте интерфейс командной строки DC/OS.</span><span class="sxs-lookup"><span data-stu-id="573b0-133">Use the DC/OS CLI to run the application.</span></span> <span data-ttu-id="573b0-134">По умолчанию Marathon развертывает приложение в частный кластер.</span><span class="sxs-lookup"><span data-stu-id="573b0-134">By default Marathon deploys the the applicaton to the private cluster.</span></span> <span data-ttu-id="573b0-135">Это означает, что указанное выше развертывание доступно только для подсистемы балансировки нагрузки (обычно такая схема является предпочтительной).</span><span class="sxs-lookup"><span data-stu-id="573b0-135">This means that the above deployment is only accessible via your load balancer, which is usually the desired behavior.</span></span>

```azurecli-interactive
dcos marathon app add hello-web.json
```

<span data-ttu-id="573b0-136">После развертывания приложения введите в адресную строку браузера полное доменное имя кластера агента, чтобы открыть приложение с балансировкой нагрузки.</span><span class="sxs-lookup"><span data-stu-id="573b0-136">Once the application has been deployed, browse to the FQDN of the agent cluster to view load balanced application.</span></span>

![Изображение приложения с балансировкой нагрузки](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a><span data-ttu-id="573b0-138">Настройка Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="573b0-138">Configure Azure Load Balancer</span></span>

<span data-ttu-id="573b0-139">По умолчанию Azure Load Balancer использует порты 80, 8080 и 443.</span><span class="sxs-lookup"><span data-stu-id="573b0-139">By default, Azure Load Balancer exposes ports 80, 8080, and 443.</span></span> <span data-ttu-id="573b0-140">При использовании одного из этих трех портов (как это было сделано в примере выше) дополнительные действия не требуются.</span><span class="sxs-lookup"><span data-stu-id="573b0-140">If you're using one of these three ports (as we do in the above example), then there is nothing you need to do.</span></span> <span data-ttu-id="573b0-141">Будет использоваться полное доменное имя агента подсистемы балансировки нагрузки, а при каждом обновлении будет использоваться один из трех веб-серверов, выбранный с помощью циклического перебора.</span><span class="sxs-lookup"><span data-stu-id="573b0-141">You should be able to hit your agent load balancer's FQDN, and each time you refresh, you'll hit one of your three web servers in a round-robin fashion.</span></span> 

<span data-ttu-id="573b0-142">Если применяется другой порт, необходимо добавить правило циклического перебора и зонд для этого порта в подсистему балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="573b0-142">If you use a different port, you need to add a round-robin rule and a probe on the load balancer for the port that you used.</span></span> <span data-ttu-id="573b0-143">Это можно сделать в [интерфейсе командной строки Azure](../../azure-resource-manager/xplat-cli-azure-resource-manager.md) с помощью команд `azure network lb rule create` и `azure network lb probe create`.</span><span class="sxs-lookup"><span data-stu-id="573b0-143">You can do this from the [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), with the commands `azure network lb rule create` and `azure network lb probe create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="573b0-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="573b0-144">Next steps</span></span>

<span data-ttu-id="573b0-145">Из этого учебника вы узнали о балансировке нагрузки в ACS с помощью подсистемы балансировки нагрузки Marathon и Azure Load Balancer и выполнили следующие действия:</span><span class="sxs-lookup"><span data-stu-id="573b0-145">In this tutorial, you learned about load balancing in ACS with both the Marathon and Azure load balancers including the following actions:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="573b0-146">Настройка подсистемы балансировки нагрузки Marathon</span><span class="sxs-lookup"><span data-stu-id="573b0-146">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="573b0-147">Развертывание приложения с помощью подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="573b0-147">Deploy an application using the load balancer</span></span>
> * <span data-ttu-id="573b0-148">Настройка Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="573b0-148">Configure and Azure load balancer</span></span>

<span data-ttu-id="573b0-149">Чтобы узнать об интеграции хранилища Azure с DC/OS в Azure, перейдите к следующему руководству.</span><span class="sxs-lookup"><span data-stu-id="573b0-149">Advance to the next tutorial to learn about integrating Azure storage with DC/OS in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="573b0-150">Подключение общей папки Azure в кластере DC/OS</span><span class="sxs-lookup"><span data-stu-id="573b0-150">Mount Azure File Share in DC/OS cluster</span></span>](container-service-dcos-fileshare.md)