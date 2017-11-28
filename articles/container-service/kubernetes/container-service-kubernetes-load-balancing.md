---
title: "aaaLoad сбалансировать Kubernetes контейнеры в Azure | Документы Microsoft"
description: "Подключайтесь извне и выполняйте балансировку нагрузки нескольких контейнеров в кластере Kubernetes в Службе контейнеров Azure."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Контейнеры, микрослужбы, Kubernetes, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 8073c8d3a015a53a532c326749571cb2582e1bac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="863ae-104">Балансировка нагрузки контейнеров в кластере Kubernetes в Службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="863ae-104">Load balance containers in a Kubernetes cluster in Azure Container Service</span></span> 
<span data-ttu-id="863ae-105">В этой статье рассматривается балансировка нагрузки в кластере Kubernetes в Службе контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="863ae-105">This article introduces load balancing in a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="863ae-106">Балансировка нагрузки предоставляет доступном IP-адрес для службы hello и распределяет сетевой трафик между стойками hello выполнение в агенте ВМ.</span><span class="sxs-lookup"><span data-stu-id="863ae-106">Load balancing provides an externally accessible IP address for hello service and distributes network traffic among hello pods running in agent VMs.</span></span>

<span data-ttu-id="863ae-107">Можно настроить службы Kubernetes toouse [подсистемы балансировки нагрузки Azure](../../load-balancer/load-balancer-overview.md) toomanage внешний трафик сети (TCP).</span><span class="sxs-lookup"><span data-stu-id="863ae-107">You can set up a Kubernetes service toouse [Azure Load Balancer](../../load-balancer/load-balancer-overview.md) toomanage external network (TCP) traffic.</span></span> <span data-ttu-id="863ae-108">Благодаря дополнительной настройке возможна балансировка нагрузки и маршрутизация трафика HTTP или HTTPS или более сложные сценарии.</span><span class="sxs-lookup"><span data-stu-id="863ae-108">With additional configuration, load balancing and routing of HTTP or HTTPS traffic or more advanced scenarios are possible.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="863ae-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="863ae-109">Prerequisites</span></span>
* <span data-ttu-id="863ae-110">[Развертывание кластера Kubernetes](container-service-kubernetes-walkthrough.md) в Службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="863ae-110">[Deploy a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>
* <span data-ttu-id="863ae-111">[Подключите клиента](../container-service-connect.md) tooyour кластера</span><span class="sxs-lookup"><span data-stu-id="863ae-111">[Connect your client](../container-service-connect.md) tooyour cluster</span></span>

## <a name="azure-load-balancer"></a><span data-ttu-id="863ae-112">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="863ae-112">Azure load balancer</span></span>

<span data-ttu-id="863ae-113">По умолчанию Kubernetes кластер, развернутых в службе контейнера Azure включает в себя балансировки нагрузки Azure с выходом в Интернет для hello агента ВМ.</span><span class="sxs-lookup"><span data-stu-id="863ae-113">By default, a Kubernetes cluster deployed in Azure Container Service includes an Internet-facing Azure load balancer for hello agent VMs.</span></span> <span data-ttu-id="863ae-114">(Ресурс балансировки нагрузки на отдельные настроен для образца hello виртуальные машины). Azure Load Balancer является подсистемой балансировки нагрузки 4-го уровня.</span><span class="sxs-lookup"><span data-stu-id="863ae-114">(A separate load balancer resource is configured for hello master VMs.) Azure load balancer is a Layer 4 load balancer.</span></span> <span data-ttu-id="863ae-115">В настоящее время hello балансировки нагрузки поддерживает только TCP-трафика в Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="863ae-115">Currently, hello load balancer only supports TCP traffic in Kubernetes.</span></span>

<span data-ttu-id="863ae-116">При создании службы Kubernetes toohello hello нагрузки Azure балансировки tooallow доступ службы можно настроить автоматически.</span><span class="sxs-lookup"><span data-stu-id="863ae-116">When creating a Kubernetes service, you can automatically configure hello Azure load balancer tooallow access toohello service.</span></span> <span data-ttu-id="863ae-117">подсистемы балансировки нагрузки hello tooconfigure, набор hello службы `type` слишком`LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="863ae-117">tooconfigure hello load balancer, set hello service `type` too`LoadBalancer`.</span></span> <span data-ttu-id="863ae-118">Hello балансировки нагрузки создает toomap правило общедоступный IP-адрес и номер порта входящего трафика toohello частных IP-адресов службы и номера портов hello модулей в агенте виртуальных машин (и, наоборот, для ответного трафика).</span><span class="sxs-lookup"><span data-stu-id="863ae-118">hello load balancer creates a rule toomap a public IP address and port number of incoming service traffic toohello private IP addresses and port numbers of hello pods in agent VMs (and vice versa for response traffic).</span></span> 

 <span data-ttu-id="863ae-119">Ниже приведены два примера, показывающий, как tooset hello Kubernetes службы `type` слишком`LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="863ae-119">Following are two examples showing how tooset hello Kubernetes service `type` too`LoadBalancer`.</span></span> <span data-ttu-id="863ae-120">(После идет примеры hello, удалите hello развертывания, если они больше не нужны.)</span><span class="sxs-lookup"><span data-stu-id="863ae-120">(After trying hello examples, delete hello deployments if you no longer need them.)</span></span>

### <a name="example-use-hello-kubectl-expose-command"></a><span data-ttu-id="863ae-121">Пример: Используйте hello `kubectl expose` команды</span><span class="sxs-lookup"><span data-stu-id="863ae-121">Example: Use hello `kubectl expose` command</span></span> 
<span data-ttu-id="863ae-122">Hello [Kubernetes Пошаговое руководство](container-service-kubernetes-walkthrough.md) включает пример tooexpose службы с hello `kubectl expose` команды и ее `--type=LoadBalancer` флаг.</span><span class="sxs-lookup"><span data-stu-id="863ae-122">hello [Kubernetes walkthrough](container-service-kubernetes-walkthrough.md) includes an example of how tooexpose a service with hello `kubectl expose` command and its `--type=LoadBalancer` flag.</span></span> <span data-ttu-id="863ae-123">Ниже приведены шаги hello.</span><span class="sxs-lookup"><span data-stu-id="863ae-123">Here are hello steps :</span></span>

1. <span data-ttu-id="863ae-124">Запустите новое развертывание контейнера.</span><span class="sxs-lookup"><span data-stu-id="863ae-124">Start a new container deployment.</span></span> <span data-ttu-id="863ae-125">Здравствуйте, например, следующая команда запускает вызывается новое развертывание `mynginx`.</span><span class="sxs-lookup"><span data-stu-id="863ae-125">For example, hello following command starts a new deployment called `mynginx`.</span></span> <span data-ttu-id="863ae-126">Развертывание Hello состоит из трех контейнеров на основе образа Docker hello для веб-сервер Nginx hello.</span><span class="sxs-lookup"><span data-stu-id="863ae-126">hello deployment consists of three containers based on hello Docker image for hello Nginx web server.</span></span>

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. <span data-ttu-id="863ae-127">Убедитесь, что запущена hello контейнеров.</span><span class="sxs-lookup"><span data-stu-id="863ae-127">Verify that hello containers are running.</span></span> <span data-ttu-id="863ae-128">Например, если вы запрашиваете hello контейнерами с помощью `kubectl get pods`, появится примерно toohello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="863ae-128">For example, if you query for hello containers with `kubectl get pods`, you see output similar toohello following:</span></span>

    ![Получение контейнеров Nginx](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. <span data-ttu-id="863ae-130">tooconfigure hello нагрузки балансировки tooaccept внешнего трафика toohello развертывания, запустите `kubectl expose` с `--type=LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="863ae-130">tooconfigure hello load balancer tooaccept external traffic toohello deployment, run `kubectl expose` with `--type=LoadBalancer`.</span></span> <span data-ttu-id="863ae-131">Hello следующая команда предоставляет сервер Nginx hello на порт 80.</span><span class="sxs-lookup"><span data-stu-id="863ae-131">hello following command exposes hello Nginx server on port 80:</span></span>

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. <span data-ttu-id="863ae-132">Тип `kubectl get svc` toosee hello состояния служб hello в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="863ae-132">Type `kubectl get svc` toosee hello state of hello services in hello cluster.</span></span> <span data-ttu-id="863ae-133">Здравствуйте, пока балансировки нагрузки hello настраивает правила hello, `EXTERNAL-IP` из hello службы отображается как `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="863ae-133">While hello load balancer configures hello rule, hello `EXTERNAL-IP` of hello service appears as `<pending>`.</span></span> <span data-ttu-id="863ae-134">Через несколько минут hello внешнего IP-адреса:</span><span class="sxs-lookup"><span data-stu-id="863ae-134">After a few minutes, hello external IP address is configured:</span></span> 

    ![Настройка Azure Load Balancer](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. <span data-ttu-id="863ae-136">Убедитесь, что доступ к службе hello hello внешний IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="863ae-136">Verify that you can access hello service at hello external IP address.</span></span> <span data-ttu-id="863ae-137">Например откройте веб-браузер toohello IP адрес показано.</span><span class="sxs-lookup"><span data-stu-id="863ae-137">For example, open a web browser toohello IP address shown.</span></span> <span data-ttu-id="863ae-138">Hello браузер отображает веб-сервер Nginx hello, работающих в одном из контейнеров hello.</span><span class="sxs-lookup"><span data-stu-id="863ae-138">hello browser shows hello Nginx web server running in one of hello containers.</span></span> <span data-ttu-id="863ae-139">Или выполнения hello `curl` или `wget` команды.</span><span class="sxs-lookup"><span data-stu-id="863ae-139">Or, run hello `curl` or `wget` command.</span></span> <span data-ttu-id="863ae-140">Например:</span><span class="sxs-lookup"><span data-stu-id="863ae-140">For example:</span></span>

    ```
    curl 13.82.93.130
    ```

    <span data-ttu-id="863ae-141">Должен отобразиться примерно такой результат:</span><span class="sxs-lookup"><span data-stu-id="863ae-141">You should see output similar to:</span></span>

    ![Доступ к Nginx с использованием curl](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. <span data-ttu-id="863ae-143">toosee hello конфигурации подсистемы балансировки нагрузки Azure hello, последовательно выберите toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="863ae-143">toosee hello configuration of hello Azure load balancer, go toohello [Azure portal](https://portal.azure.com).</span></span>

7. <span data-ttu-id="863ae-144">Поиск hello группы ресурсов для службы кластера контейнер и выберите hello балансировки нагрузки для hello агент ВМ.</span><span class="sxs-lookup"><span data-stu-id="863ae-144">Browse for hello resource group for your container service cluster, and select hello load balancer for hello agent VMs.</span></span> <span data-ttu-id="863ae-145">То же, что контейнер службы hello следует hello его имя.</span><span class="sxs-lookup"><span data-stu-id="863ae-145">Its name should be hello same as hello container service.</span></span> <span data-ttu-id="863ae-146">(Не выбора hello подсистемы балансировки нагрузки для hello главных узлов, один, имя которого содержит hello **балансировки нагрузки master**.)</span><span class="sxs-lookup"><span data-stu-id="863ae-146">(Don't choose hello load balancer for hello master nodes, hello one whose name includes **master-lb**.)</span></span> 

    ![Балансировщик нагрузки в группе ресурсов](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. <span data-ttu-id="863ae-148">Щелкните toosee hello сведения о конфигурации подсистемы балансировки нагрузки hello, **правила подсистемы балансировки нагрузки** и hello имя правила hello, который был настроен.</span><span class="sxs-lookup"><span data-stu-id="863ae-148">toosee hello details of hello load balancer configuration, click **Load balancing rules** and hello name of hello rule that was configured.</span></span>

    ![Правила балансировщика нагрузки](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-hello-service-configuration-file"></a><span data-ttu-id="863ae-150">Пример: Задание `type: LoadBalancer` в файле конфигурации службы hello</span><span class="sxs-lookup"><span data-stu-id="863ae-150">Example: Specify `type: LoadBalancer` in hello service configuration file</span></span>

<span data-ttu-id="863ae-151">При развертывании приложения контейнера Kubernetes из YAML или JSON [файла конфигурации службы](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), укажите внешней подсистемы балансировки нагрузки, добавив hello спецификации службы toohello строки:</span><span class="sxs-lookup"><span data-stu-id="863ae-151">If you deploy a Kubernetes container app from a YAML or JSON [service configuration file](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), specify an external load balancer by adding hello following line toohello service specification:</span></span>

```YAML
 "type": "LoadBalancer"
``` 



<span data-ttu-id="863ae-152">Hello Далее используется hello Kubernetes [примере гостевую](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span><span class="sxs-lookup"><span data-stu-id="863ae-152">hello following steps use hello Kubernetes [Guestbook example](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span></span> <span data-ttu-id="863ae-153">Этот пример является многоуровневым веб-приложением на основе образов Redis и PHP Docker.</span><span class="sxs-lookup"><span data-stu-id="863ae-153">This example is a multi-tier web app based on  Redis and PHP Docker images.</span></span> <span data-ttu-id="863ae-154">Можно указать в файле конфигурации службы hello hello балансировки нагрузки Azure использует этот сервер PHP hello переднего плана.</span><span class="sxs-lookup"><span data-stu-id="863ae-154">You can specify in hello service configuration file that hello frontend PHP server uses hello Azure load balancer.</span></span>

1. <span data-ttu-id="863ae-155">Загрузите файл hello `guestbook-all-in-one.yaml` из [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span><span class="sxs-lookup"><span data-stu-id="863ae-155">Download hello file `guestbook-all-in-one.yaml` from [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span></span> 
2. <span data-ttu-id="863ae-156">Поиск hello `spec` для hello `frontend` службы.</span><span class="sxs-lookup"><span data-stu-id="863ae-156">Browse for hello `spec` for hello `frontend` service.</span></span>
3. <span data-ttu-id="863ae-157">Раскомментируйте строку hello `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="863ae-157">Uncomment hello line `type: LoadBalancer`.</span></span>

    ![Балансировщик нагрузки в конфигурации службы](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. <span data-ttu-id="863ae-159">Сохраните файл hello и разверните приложение hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="863ae-159">Save hello file, and deploy hello app by running hello following command:</span></span>

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. <span data-ttu-id="863ae-160">Тип `kubectl get svc` toosee hello состояния служб hello в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="863ae-160">Type `kubectl get svc` toosee hello state of hello services in hello cluster.</span></span> <span data-ttu-id="863ae-161">Здравствуйте, пока балансировки нагрузки hello настраивает правила hello, `EXTERNAL-IP` из hello `frontend` службы отображается как `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="863ae-161">While hello load balancer configures hello rule, hello `EXTERNAL-IP` of hello `frontend` service appears as `<pending>`.</span></span> <span data-ttu-id="863ae-162">Через несколько минут hello внешнего IP-адреса:</span><span class="sxs-lookup"><span data-stu-id="863ae-162">After a few minutes, hello external IP address is configured:</span></span> 

    ![Настройка Azure Load Balancer](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. <span data-ttu-id="863ae-164">Убедитесь, что доступ к службе hello hello внешний IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="863ae-164">Verify that you can access hello service at hello external IP address.</span></span> <span data-ttu-id="863ae-165">Например можно открыть веб браузера toohello внешний IP-адрес службы hello.</span><span class="sxs-lookup"><span data-stu-id="863ae-165">For example, you can open a web browser toohello external IP address of hello service.</span></span>

    ![Внешний доступ к гостевой книге](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    <span data-ttu-id="863ae-167">Вы можете добавить записи гостевой книги.</span><span class="sxs-lookup"><span data-stu-id="863ae-167">You can add guestbook entries.</span></span>

7. <span data-ttu-id="863ae-168">toosee hello конфигурации подсистемы балансировки нагрузки Azure hello, поиск ресурсов подсистемы балансировки нагрузки hello для кластера hello в hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="863ae-168">toosee hello configuration of hello Azure load balancer, browse for hello load balancer resource for hello cluster in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="863ae-169">См. шаги hello в предыдущем примере hello.</span><span class="sxs-lookup"><span data-stu-id="863ae-169">See hello steps in hello previous example.</span></span>

### <a name="considerations"></a><span data-ttu-id="863ae-170">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="863ae-170">Considerations</span></span>

* <span data-ttu-id="863ae-171">Создание правила подсистемы балансировки нагрузки hello происходит асинхронно, и данные балансировки hello подготовить публикуются в службе hello `status.loadBalancer` поля.</span><span class="sxs-lookup"><span data-stu-id="863ae-171">Creation of hello load balancer rule happens asynchronously, and information about hello provisioned balancer is published in hello service’s `status.loadBalancer` field.</span></span>
* <span data-ttu-id="863ae-172">Каждая служба автоматически назначается свой собственный виртуальный IP-адрес в hello балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="863ae-172">Every service is automatically assigned its own virtual IP address in hello load balancer.</span></span>
* <span data-ttu-id="863ae-173">Если требуется балансировки нагрузки hello tooreach DNS-именем, работаете с вашей toocreate поставщика службы доменных DNS-имя для правила hello IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="863ae-173">If you want tooreach hello load balancer by a DNS name, work with your domain service provider toocreate a DNS name for hello rule's IP address.</span></span>

## <a name="http-or-https-traffic"></a><span data-ttu-id="863ae-174">Трафик HTTP или HTTPS</span><span class="sxs-lookup"><span data-stu-id="863ae-174">HTTP or HTTPS traffic</span></span>

<span data-ttu-id="863ae-175">Баланс tooload HTTP или HTTPS toocontainer трафик веб-приложений и управление сертификатами для безопасности транспортного уровня (TLS), можно использовать hello Kubernetes [входящих](https://kubernetes.io/docs/user-guide/ingress/) ресурсов.</span><span class="sxs-lookup"><span data-stu-id="863ae-175">tooload balance HTTP or HTTPS traffic toocontainer web apps and manage certificates for transport layer security (TLS), you can use hello Kubernetes [Ingress](https://kubernetes.io/docs/user-guide/ingress/) resource.</span></span> <span data-ttu-id="863ae-176">Входящие — это совокупность правила, разрешающие входящие подключения службы кластеров tooreach hello.</span><span class="sxs-lookup"><span data-stu-id="863ae-176">An Ingress is a collection of rules that allow inbound connections tooreach hello cluster services.</span></span> <span data-ttu-id="863ae-177">Для входящих сообщений toowork ресурсов, hello Kubernetes кластер должен иметь [входящих контроллера](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) под управлением.</span><span class="sxs-lookup"><span data-stu-id="863ae-177">For an Ingress resource toowork, hello Kubernetes cluster must have an [Ingress controller](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) running.</span></span>

<span data-ttu-id="863ae-178">Служба контейнеров Azure не реализует контроллер Ingress Kubernetes автоматически.</span><span class="sxs-lookup"><span data-stu-id="863ae-178">Azure Container Service does not implement a Kubernetes Ingress controller automatically.</span></span> <span data-ttu-id="863ae-179">Доступны несколько реализаций контроллера.</span><span class="sxs-lookup"><span data-stu-id="863ae-179">Several controller implementations are available.</span></span> <span data-ttu-id="863ae-180">В настоящее время hello [Nginx входящих контроллера](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) рекомендуется tooconfigure входящих правил и балансировки нагрузки трафика HTTP и HTTPS.</span><span class="sxs-lookup"><span data-stu-id="863ae-180">Currently, hello [Nginx Ingress controller](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) is recommended tooconfigure Ingress rules and load balance HTTP and HTTPS traffic.</span></span> 

<span data-ttu-id="863ae-181">Дополнительные сведения см. в разделе hello [Nginx входящих контроллер документация](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span><span class="sxs-lookup"><span data-stu-id="863ae-181">For more information, see hello [Nginx Ingress controller documentation](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="863ae-182">При использовании hello контроллера Nginx входящих сообщений в службе контейнера Azure, должен предоставлять развертывания контроллера hello как служба с `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="863ae-182">When using hello Nginx Ingress controller in Azure Container Service, you must expose hello controller deployment as a service with `type: LoadBalancer`.</span></span> <span data-ttu-id="863ae-183">Это настраивает toohello hello нагрузки Azure балансировки tooroute трафика контроллера.</span><span class="sxs-lookup"><span data-stu-id="863ae-183">This configures hello Azure load balancer tooroute traffic toohello controller.</span></span> <span data-ttu-id="863ae-184">Дополнительные сведения см. в разделе hello предыдущего раздела.</span><span class="sxs-lookup"><span data-stu-id="863ae-184">For more information, see hello previous section.</span></span>


## <a name="next-steps"></a><span data-ttu-id="863ae-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="863ae-185">Next steps</span></span>

* <span data-ttu-id="863ae-186">В разделе hello [документации Kubernetes Подсистема балансировки нагрузки](https://kubernetes.io/docs/user-guide/load-balancer/)</span><span class="sxs-lookup"><span data-stu-id="863ae-186">See hello [Kubernetes LoadBalancer documentation](https://kubernetes.io/docs/user-guide/load-balancer/)</span></span>
* <span data-ttu-id="863ae-187">Узнайте больше о [контроллерах Ingress Kubernetes](https://kubernetes.io/docs/user-guide/ingress/)</span><span class="sxs-lookup"><span data-stu-id="863ae-187">Learn more about [Kubernetes Ingress and Ingress controllers](https://kubernetes.io/docs/user-guide/ingress/)</span></span>
* <span data-ttu-id="863ae-188">Ознакомьтесь с [примерами Kubernetes](https://github.com/kubernetes/kubernetes/tree/master/examples)</span><span class="sxs-lookup"><span data-stu-id="863ae-188">See [Kubernetes examples](https://github.com/kubernetes/kubernetes/tree/master/examples)</span></span>

