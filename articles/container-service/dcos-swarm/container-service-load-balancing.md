---
title: "контейнеры aaaLoad баланс в кластере Azure DC/OS | Документы Microsoft"
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
ms.openlocfilehash: 2249cb06880cdb7e9a3aa94c0750c6a27316d349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="74807-104">Балансировка нагрузки контейнеров в кластере DC/OS в Службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="74807-104">Load balance containers in an Azure Container Service DC/OS cluster</span></span>
<span data-ttu-id="74807-105">В этой статье мы расскажем, как внутренний балансировщик нагрузки в контроллер домена/OS toocreate управление контейнера службы Azure, с помощью балансировки Нагрузки Marathon.</span><span class="sxs-lookup"><span data-stu-id="74807-105">In this article, we explore how toocreate an internal load balancer in a DC/OS managed Azure Container Service using Marathon-LB.</span></span> <span data-ttu-id="74807-106">Такая конфигурация позволяет вам tooscale приложений по горизонтали.</span><span class="sxs-lookup"><span data-stu-id="74807-106">This configuration enables you tooscale your applications horizontally.</span></span> <span data-ttu-id="74807-107">Оно также позволяет tootake преимуществами кластеров открытых и закрытых агента hello размещая вашей подсистемы балансировки нагрузки на открытый кластера hello и вашего приложения контейнеры закрытый кластере hello.</span><span class="sxs-lookup"><span data-stu-id="74807-107">It also allows you tootake advantage of hello public and private agent clusters by placing your load balancers on hello public cluster and your application containers on hello private cluster.</span></span> <span data-ttu-id="74807-108">Изучив это руководство, вы:</span><span class="sxs-lookup"><span data-stu-id="74807-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="74807-109">Настройка подсистемы балансировки нагрузки Marathon</span><span class="sxs-lookup"><span data-stu-id="74807-109">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="74807-110">Развертывание приложения с помощью подсистемы балансировки нагрузки hello</span><span class="sxs-lookup"><span data-stu-id="74807-110">Deploy an application using hello load balancer</span></span>
> * <span data-ttu-id="74807-111">Настройка Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="74807-111">Configure and Azure load balancer</span></span>

<span data-ttu-id="74807-112">Вы должны ACS DC/OS hello toocomplete кластера шаги в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="74807-112">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="74807-113">При необходимости его можно создать с помощью следующего [примера сценария](./../kubernetes/scripts/container-service-cli-deploy-dcos.md).</span><span class="sxs-lookup"><span data-stu-id="74807-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="74807-114">Упражнений этого учебника требуется hello Azure CLI версия 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="74807-114">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="74807-115">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="74807-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="74807-116">Получить tooupgrade [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="74807-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a><span data-ttu-id="74807-117">Общие сведения о балансировке нагрузки</span><span class="sxs-lookup"><span data-stu-id="74807-117">Load balancing overview</span></span>

<span data-ttu-id="74807-118">В кластере DC/OS службы контейнеров Azure существует два уровня балансировки нагрузки:</span><span class="sxs-lookup"><span data-stu-id="74807-118">There are two load-balancing layers in an Azure Container Service DC/OS cluster:</span></span> 

<span data-ttu-id="74807-119">**Подсистема балансировки нагрузки Azure** предоставляет открытым точкам входа (те, что конечным пользователям доступ к hello).</span><span class="sxs-lookup"><span data-stu-id="74807-119">**Azure Load Balancer** provides public entry points (hello ones that end users access).</span></span> <span data-ttu-id="74807-120">Балансировки Нагрузки Azure автоматически обеспечивается контейнера службы Azure и по умолчанию, настроенные tooexpose порт 80, 443 и 8080.</span><span class="sxs-lookup"><span data-stu-id="74807-120">An Azure LB is provided automatically by Azure Container Service and is, by default, configured tooexpose port 80, 443 and 8080.</span></span>

<span data-ttu-id="74807-121">**Hello Marathon балансировки нагрузки (marathon фунта)** маршруты входящих запросов toocontainer экземпляров, обслуживающих эти запросы.</span><span class="sxs-lookup"><span data-stu-id="74807-121">**hello Marathon Load Balancer (marathon-lb)** routes inbound requests toocontainer instances that service these requests.</span></span> <span data-ttu-id="74807-122">Как мы масштабировать hello контейнеры, предоставляя веб-узле службы, динамически адаптируется hello marathon-балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="74807-122">As we scale hello containers providing our web service, hello marathon-lb dynamically adapts.</span></span> <span data-ttu-id="74807-123">Эта подсистема балансировки нагрузки не предоставляется по умолчанию в службе контейнера, но это просто tooinstall.</span><span class="sxs-lookup"><span data-stu-id="74807-123">This load balancer is not provided by default in your Container Service, but it is easy tooinstall.</span></span>

## <a name="configure-marathon-load-balancer"></a><span data-ttu-id="74807-124">Настройка подсистемы балансировки нагрузки Marathon</span><span class="sxs-lookup"><span data-stu-id="74807-124">Configure Marathon Load Balancer</span></span>

<span data-ttu-id="74807-125">Подсистема балансировки нагрузки Marathon динамически перенастраивает основании hello контейнеры, которые развернуты.</span><span class="sxs-lookup"><span data-stu-id="74807-125">Marathon Load Balancer dynamically reconfigures itself based on hello containers that you've deployed.</span></span> <span data-ttu-id="74807-126">Это также потери устойчивым toohello контейнер или агента -, если это происходит, Apache Mesos перезапускает hello контейнера в другом месте и балансировки нагрузки marathon адаптирует.</span><span class="sxs-lookup"><span data-stu-id="74807-126">It's also resilient toohello loss of a container or an agent - if this occurs, Apache Mesos restarts hello container elsewhere and marathon-lb adapts.</span></span>

<span data-ttu-id="74807-127">Выполнения hello следующая команда балансировки нагрузки marathon tooinstall hello в кластере hello открытый агента.</span><span class="sxs-lookup"><span data-stu-id="74807-127">Run hello following command tooinstall hello marathon load balancer on hello public agent's cluster.</span></span>

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a><span data-ttu-id="74807-128">Развертывание приложения с балансировкой нагрузки</span><span class="sxs-lookup"><span data-stu-id="74807-128">Deploy load balanced application</span></span>

<span data-ttu-id="74807-129">Теперь, когда у нас есть пакет балансировки нагрузки marathon hello, мы разверните контейнер приложения, что мы хочет tooload баланс.</span><span class="sxs-lookup"><span data-stu-id="74807-129">Now that we have hello marathon-lb package, we can deploy an application container that we wish tooload balance.</span></span> 

<span data-ttu-id="74807-130">Сначала необходимо получите полное доменное имя в открытую hello агентов hello.</span><span class="sxs-lookup"><span data-stu-id="74807-130">First, get hello FQDN of hello publicly exposed agents.</span></span>

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

<span data-ttu-id="74807-131">Создайте файл с именем *hello web.json* и копирования в hello после содержимого.</span><span class="sxs-lookup"><span data-stu-id="74807-131">Next, create a file named *hello-web.json* and copy in hello following contents.</span></span> <span data-ttu-id="74807-132">Hello `HAPROXY_0_VHOST` метки должен toobe обновляется hello полное доменное имя контроллера домена/OS агентов hello.</span><span class="sxs-lookup"><span data-stu-id="74807-132">hello `HAPROXY_0_VHOST` label needs toobe updated with hello FQDN of hello DC/OS agents.</span></span> 

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

<span data-ttu-id="74807-133">С помощью приложения hello toorun CLI DC/OS hello.</span><span class="sxs-lookup"><span data-stu-id="74807-133">Use hello DC/OS CLI toorun hello application.</span></span> <span data-ttu-id="74807-134">По умолчанию Marathon разворачивает закрытый кластера приложение hello toohello hello.</span><span class="sxs-lookup"><span data-stu-id="74807-134">By default Marathon deploys hello hello applicaton toohello private cluster.</span></span> <span data-ttu-id="74807-135">Это означает, что hello выше развертывания доступен только через балансировки нагрузки, которое обычно является hello требуемого поведения.</span><span class="sxs-lookup"><span data-stu-id="74807-135">This means that hello above deployment is only accessible via your load balancer, which is usually hello desired behavior.</span></span>

```azurecli-interactive
dcos marathon app add hello-web.json
```

<span data-ttu-id="74807-136">После развертывания приложения hello Обзор toohello полное доменное имя приложения с балансировкой нагрузки tooview кластера hello агента.</span><span class="sxs-lookup"><span data-stu-id="74807-136">Once hello application has been deployed, browse toohello FQDN of hello agent cluster tooview load balanced application.</span></span>

![Изображение приложения с балансировкой нагрузки](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a><span data-ttu-id="74807-138">Настройка Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="74807-138">Configure Azure Load Balancer</span></span>

<span data-ttu-id="74807-139">По умолчанию Azure Load Balancer использует порты 80, 8080 и 443.</span><span class="sxs-lookup"><span data-stu-id="74807-139">By default, Azure Load Balancer exposes ports 80, 8080, and 443.</span></span> <span data-ttu-id="74807-140">Если вы используете один из этих трех портов (как это было сделано в hello в приведенном выше примере), а затем не требуется toodo.</span><span class="sxs-lookup"><span data-stu-id="74807-140">If you're using one of these three ports (as we do in hello above example), then there is nothing you need toodo.</span></span> <span data-ttu-id="74807-141">Должен быть доступ toohit полное доменное имя подсистемы балансировки загрузки агента и каждый раз при обновлении будет попадании один из трех веб-серверов в циклического перебора.</span><span class="sxs-lookup"><span data-stu-id="74807-141">You should be able toohit your agent load balancer's FQDN, and each time you refresh, you'll hit one of your three web servers in a round-robin fashion.</span></span> 

<span data-ttu-id="74807-142">Если используется другой порт, требуется правило tooadd циклический перебор и проверки на hello балансировки нагрузки для hello порт, который использовался.</span><span class="sxs-lookup"><span data-stu-id="74807-142">If you use a different port, you need tooadd a round-robin rule and a probe on hello load balancer for hello port that you used.</span></span> <span data-ttu-id="74807-143">Это можно сделать из hello [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), с помощью команд hello `azure network lb rule create` и `azure network lb probe create`.</span><span class="sxs-lookup"><span data-stu-id="74807-143">You can do this from hello [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), with hello commands `azure network lb rule create` and `azure network lb probe create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74807-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="74807-144">Next steps</span></span>

<span data-ttu-id="74807-145">В этом учебнике вы узнали о балансировки нагрузки в ACS с hello Marathon и нагрузки Azure, включая балансировки нагрузки hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="74807-145">In this tutorial, you learned about load balancing in ACS with both hello Marathon and Azure load balancers including hello following actions:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="74807-146">Настройка подсистемы балансировки нагрузки Marathon</span><span class="sxs-lookup"><span data-stu-id="74807-146">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="74807-147">Развертывание приложения с помощью подсистемы балансировки нагрузки hello</span><span class="sxs-lookup"><span data-stu-id="74807-147">Deploy an application using hello load balancer</span></span>
> * <span data-ttu-id="74807-148">Настройка Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="74807-148">Configure and Azure load balancer</span></span>

<span data-ttu-id="74807-149">Переместить toohello Далее учебника toolearn об интеграции хранилища Azure с контроллера домена или ОС в Azure.</span><span class="sxs-lookup"><span data-stu-id="74807-149">Advance toohello next tutorial toolearn about integrating Azure storage with DC/OS in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="74807-150">Подключение общей папки Azure в кластере DC/OS</span><span class="sxs-lookup"><span data-stu-id="74807-150">Mount Azure File Share in DC/OS cluster</span></span>](container-service-dcos-fileshare.md)