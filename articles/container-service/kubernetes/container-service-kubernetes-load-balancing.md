---
title: "Балансировка нагрузки контейнеров Kubernetes в Azure | Документация Майкрософт"
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
ms.openlocfilehash: ab46bb204f14424e394ced499ffbc0ef1cada15b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="44faa-104">Балансировка нагрузки контейнеров в кластере Kubernetes в Службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="44faa-104">Load balance containers in a Kubernetes cluster in Azure Container Service</span></span> 
<span data-ttu-id="44faa-105">В этой статье рассматривается балансировка нагрузки в кластере Kubernetes в Службе контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="44faa-105">This article introduces load balancing in a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="44faa-106">При балансировке нагрузки предоставляется доступный через Интернет IP-адрес для службы и распределяется сетевой трафик между модулями, запущенными в виртуальных машинах агента.</span><span class="sxs-lookup"><span data-stu-id="44faa-106">Load balancing provides an externally accessible IP address for the service and distributes network traffic among the pods running in agent VMs.</span></span>

<span data-ttu-id="44faa-107">Службу Kubernetes можно настроить для использования [Azure Load Balancer](../../load-balancer/load-balancer-overview.md), чтобы управлять трафиком внешней сети (TCP).</span><span class="sxs-lookup"><span data-stu-id="44faa-107">You can set up a Kubernetes service to use [Azure Load Balancer](../../load-balancer/load-balancer-overview.md) to manage external network (TCP) traffic.</span></span> <span data-ttu-id="44faa-108">Благодаря дополнительной настройке возможна балансировка нагрузки и маршрутизация трафика HTTP или HTTPS или более сложные сценарии.</span><span class="sxs-lookup"><span data-stu-id="44faa-108">With additional configuration, load balancing and routing of HTTP or HTTPS traffic or more advanced scenarios are possible.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44faa-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="44faa-109">Prerequisites</span></span>
* <span data-ttu-id="44faa-110">[Развертывание кластера Kubernetes](container-service-kubernetes-walkthrough.md) в Службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="44faa-110">[Deploy a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>
* <span data-ttu-id="44faa-111">[Подключение клиента](../container-service-connect.md) к кластеру</span><span class="sxs-lookup"><span data-stu-id="44faa-111">[Connect your client](../container-service-connect.md) to your cluster</span></span>

## <a name="azure-load-balancer"></a><span data-ttu-id="44faa-112">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="44faa-112">Azure load balancer</span></span>

<span data-ttu-id="44faa-113">По умолчанию кластер Kubernetes, развернутый в Службе контейнеров Azure, включает Azure Load Balancer с выходом в Интернет для виртуальных машин агента.</span><span class="sxs-lookup"><span data-stu-id="44faa-113">By default, a Kubernetes cluster deployed in Azure Container Service includes an Internet-facing Azure load balancer for the agent VMs.</span></span> <span data-ttu-id="44faa-114">(Для главных виртуальных машин настраивается отдельный ресурс балансировщика нагрузки.) Azure Load Balancer является подсистемой балансировки нагрузки 4-го уровня.</span><span class="sxs-lookup"><span data-stu-id="44faa-114">(A separate load balancer resource is configured for the master VMs.) Azure load balancer is a Layer 4 load balancer.</span></span> <span data-ttu-id="44faa-115">В настоящее время подсистема балансировки нагрузки поддерживает в Kubernetes только трафик TCP.</span><span class="sxs-lookup"><span data-stu-id="44faa-115">Currently, the load balancer only supports TCP traffic in Kubernetes.</span></span>

<span data-ttu-id="44faa-116">При создании службы Kubernetes можно автоматически настроить балансировщик нагрузки Azure, чтобы обеспечить доступ к службе.</span><span class="sxs-lookup"><span data-stu-id="44faa-116">When creating a Kubernetes service, you can automatically configure the Azure load balancer to allow access to the service.</span></span> <span data-ttu-id="44faa-117">Чтобы настроить балансировщик нагрузки, задайте для параметра `type` службы значение `LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="44faa-117">To configure the load balancer, set the service `type` to `LoadBalancer`.</span></span> <span data-ttu-id="44faa-118">Балансировщик нагрузки создает правило для сопоставления открытого IP-адреса и номера порта для входящего трафика службы с закрытыми IP-адресами и номерами портов в модулях виртуальных машин (и наоборот для ответного трафика).</span><span class="sxs-lookup"><span data-stu-id="44faa-118">The load balancer creates a rule to map a public IP address and port number of incoming service traffic to the private IP addresses and port numbers of the pods in agent VMs (and vice versa for response traffic).</span></span> 

 <span data-ttu-id="44faa-119">Ниже приведены два примера задания для параметра `type` службы Kubernetes значения `LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="44faa-119">Following are two examples showing how to set the Kubernetes service `type` to `LoadBalancer`.</span></span> <span data-ttu-id="44faa-120">(После выполнения примеров удалите развертывания, если они больше не нужны.)</span><span class="sxs-lookup"><span data-stu-id="44faa-120">(After trying the examples, delete the deployments if you no longer need them.)</span></span>

### <a name="example-use-the-kubectl-expose-command"></a><span data-ttu-id="44faa-121">Пример. Использование команды `kubectl expose`</span><span class="sxs-lookup"><span data-stu-id="44faa-121">Example: Use the `kubectl expose` command</span></span> 
<span data-ttu-id="44faa-122">В статье [Обработчик службы контейнеров Microsoft Azure. Пошаговое руководство по использованию Kubernetes](container-service-kubernetes-walkthrough.md) содержится пример предоставления службы с командой `kubectl expose` и ее параметром `--type=LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="44faa-122">The [Kubernetes walkthrough](container-service-kubernetes-walkthrough.md) includes an example of how to expose a service with the `kubectl expose` command and its `--type=LoadBalancer` flag.</span></span> <span data-ttu-id="44faa-123">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="44faa-123">Here are the steps :</span></span>

1. <span data-ttu-id="44faa-124">Запустите новое развертывание контейнера.</span><span class="sxs-lookup"><span data-stu-id="44faa-124">Start a new container deployment.</span></span> <span data-ttu-id="44faa-125">Например, следующая команда запускает новое развертывание с именем `mynginx`.</span><span class="sxs-lookup"><span data-stu-id="44faa-125">For example, the following command starts a new deployment called `mynginx`.</span></span> <span data-ttu-id="44faa-126">Оно состоит из трех контейнеров на основе образа Docker для веб-сервера Nginx.</span><span class="sxs-lookup"><span data-stu-id="44faa-126">The deployment consists of three containers based on the Docker image for the Nginx web server.</span></span>

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. <span data-ttu-id="44faa-127">Убедитесь, что контейнеры запущены.</span><span class="sxs-lookup"><span data-stu-id="44faa-127">Verify that the containers are running.</span></span> <span data-ttu-id="44faa-128">Например, если выполнить запрос на контейнеры, используя команду `kubectl get pods`, должен появиться результат, аналогичный следующему:</span><span class="sxs-lookup"><span data-stu-id="44faa-128">For example, if you query for the containers with `kubectl get pods`, you see output similar to the following:</span></span>

    ![Получение контейнеров Nginx](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. <span data-ttu-id="44faa-130">Чтобы настроить балансировщик нагрузки для принятия внешнего трафика в развертывание, выполните команду `kubectl expose` со значением `--type=LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="44faa-130">To configure the load balancer to accept external traffic to the deployment, run `kubectl expose` with `--type=LoadBalancer`.</span></span> <span data-ttu-id="44faa-131">Следующая команда предоставляет сервер Nginx через порт 80:</span><span class="sxs-lookup"><span data-stu-id="44faa-131">The following command exposes the Nginx server on port 80:</span></span>

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. <span data-ttu-id="44faa-132">Введите `kubectl get svc`, чтобы просмотреть сведения о состоянии служб в кластере.</span><span class="sxs-lookup"><span data-stu-id="44faa-132">Type `kubectl get svc` to see the state of the services in the cluster.</span></span> <span data-ttu-id="44faa-133">Пока балансировщик нагрузки настраивает правило, `EXTERNAL-IP` службы отображается как `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="44faa-133">While the load balancer configures the rule, the `EXTERNAL-IP` of the service appears as `<pending>`.</span></span> <span data-ttu-id="44faa-134">Через несколько минут настройка внешнего IP-адреса будет завершена:</span><span class="sxs-lookup"><span data-stu-id="44faa-134">After a few minutes, the external IP address is configured:</span></span> 

    ![Настройка Azure Load Balancer](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. <span data-ttu-id="44faa-136">Убедитесь, что у вас есть доступ к службе по внешнему IP-адресу.</span><span class="sxs-lookup"><span data-stu-id="44faa-136">Verify that you can access the service at the external IP address.</span></span> <span data-ttu-id="44faa-137">Например, откройте веб-браузер и используйте отображаемый IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="44faa-137">For example, open a web browser to the IP address shown.</span></span> <span data-ttu-id="44faa-138">В браузере отображается веб-сервер Nginx, запущенный в одном из контейнеров.</span><span class="sxs-lookup"><span data-stu-id="44faa-138">The browser shows the Nginx web server running in one of the containers.</span></span> <span data-ttu-id="44faa-139">Или выполните команду `curl` либо `wget`.</span><span class="sxs-lookup"><span data-stu-id="44faa-139">Or, run the `curl` or `wget` command.</span></span> <span data-ttu-id="44faa-140">Например:</span><span class="sxs-lookup"><span data-stu-id="44faa-140">For example:</span></span>

    ```
    curl 13.82.93.130
    ```

    <span data-ttu-id="44faa-141">Должен отобразиться примерно такой результат:</span><span class="sxs-lookup"><span data-stu-id="44faa-141">You should see output similar to:</span></span>

    ![Доступ к Nginx с использованием curl](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. <span data-ttu-id="44faa-143">Чтобы просмотреть конфигурацию Azure Load Balancer, перейдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="44faa-143">To see the configuration of the Azure load balancer, go to the [Azure portal](https://portal.azure.com).</span></span>

7. <span data-ttu-id="44faa-144">Перейдите к группе ресурсов для кластера службы контейнеров и выберите балансировщик нагрузки для виртуальных машин агента.</span><span class="sxs-lookup"><span data-stu-id="44faa-144">Browse for the resource group for your container service cluster, and select the load balancer for the agent VMs.</span></span> <span data-ttu-id="44faa-145">Его имя должно совпадать с именем службы контейнеров.</span><span class="sxs-lookup"><span data-stu-id="44faa-145">Its name should be the same as the container service.</span></span> <span data-ttu-id="44faa-146">(Не выбирайте балансировщик нагрузки для главных узлов, имя которого содержит **master-lb**.)</span><span class="sxs-lookup"><span data-stu-id="44faa-146">(Don't choose the load balancer for the master nodes, the one whose name includes **master-lb**.)</span></span> 

    ![Балансировщик нагрузки в группе ресурсов](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. <span data-ttu-id="44faa-148">Чтобы просмотреть сведения о конфигурации балансировщика нагрузки, выберите параметр **Правила балансировки нагрузки** и имя настроенного правила.</span><span class="sxs-lookup"><span data-stu-id="44faa-148">To see the details of the load balancer configuration, click **Load balancing rules** and the name of the rule that was configured.</span></span>

    ![Правила балансировщика нагрузки](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-the-service-configuration-file"></a><span data-ttu-id="44faa-150">Пример. Указание `type: LoadBalancer` в файле конфигурации службы</span><span class="sxs-lookup"><span data-stu-id="44faa-150">Example: Specify `type: LoadBalancer` in the service configuration file</span></span>

<span data-ttu-id="44faa-151">При развертывании приложения контейнера Kubernetes из [файла конфигурации службы](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file) YAML или JSON укажите внешний балансировщик нагрузки, добавив следующую строку в спецификацию службы:</span><span class="sxs-lookup"><span data-stu-id="44faa-151">If you deploy a Kubernetes container app from a YAML or JSON [service configuration file](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), specify an external load balancer by adding the following line to the service specification:</span></span>

```YAML
 "type": "LoadBalancer"
``` 



<span data-ttu-id="44faa-152">В следующих действиях используется [пример гостевой книги](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook) Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="44faa-152">The following steps use the Kubernetes [Guestbook example](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span></span> <span data-ttu-id="44faa-153">Этот пример является многоуровневым веб-приложением на основе образов Redis и PHP Docker.</span><span class="sxs-lookup"><span data-stu-id="44faa-153">This example is a multi-tier web app based on  Redis and PHP Docker images.</span></span> <span data-ttu-id="44faa-154">В файле конфигурации службы можно указать, что сервер переднего плана PHP использует Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="44faa-154">You can specify in the service configuration file that the frontend PHP server uses the Azure load balancer.</span></span>

1. <span data-ttu-id="44faa-155">Скачайте файл `guestbook-all-in-one.yaml` с сайта [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span><span class="sxs-lookup"><span data-stu-id="44faa-155">Download the file `guestbook-all-in-one.yaml` from [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span></span> 
2. <span data-ttu-id="44faa-156">Перейдите к параметру `spec` для службы `frontend`.</span><span class="sxs-lookup"><span data-stu-id="44faa-156">Browse for the `spec` for the `frontend` service.</span></span>
3. <span data-ttu-id="44faa-157">Раскомментируйте строку `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="44faa-157">Uncomment the line `type: LoadBalancer`.</span></span>

    ![Балансировщик нагрузки в конфигурации службы](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. <span data-ttu-id="44faa-159">Сохраните файл и разверните приложение, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="44faa-159">Save the file, and deploy the app by running the following command:</span></span>

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. <span data-ttu-id="44faa-160">Введите `kubectl get svc`, чтобы просмотреть сведения о состоянии служб в кластере.</span><span class="sxs-lookup"><span data-stu-id="44faa-160">Type `kubectl get svc` to see the state of the services in the cluster.</span></span> <span data-ttu-id="44faa-161">Пока балансировщик нагрузки настраивает правило, `EXTERNAL-IP` службы `frontend` отображается как `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="44faa-161">While the load balancer configures the rule, the `EXTERNAL-IP` of the `frontend` service appears as `<pending>`.</span></span> <span data-ttu-id="44faa-162">Через несколько минут настройка внешнего IP-адреса будет завершена:</span><span class="sxs-lookup"><span data-stu-id="44faa-162">After a few minutes, the external IP address is configured:</span></span> 

    ![Настройка Azure Load Balancer](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. <span data-ttu-id="44faa-164">Убедитесь, что у вас есть доступ к службе по внешнему IP-адресу.</span><span class="sxs-lookup"><span data-stu-id="44faa-164">Verify that you can access the service at the external IP address.</span></span> <span data-ttu-id="44faa-165">Например, можно открыть веб-браузер и использовать внешний IP-адрес службы.</span><span class="sxs-lookup"><span data-stu-id="44faa-165">For example, you can open a web browser to the external IP address of the service.</span></span>

    ![Внешний доступ к гостевой книге](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    <span data-ttu-id="44faa-167">Вы можете добавить записи гостевой книги.</span><span class="sxs-lookup"><span data-stu-id="44faa-167">You can add guestbook entries.</span></span>

7. <span data-ttu-id="44faa-168">Чтобы просмотреть конфигурацию Azure Load Balancer, перейдите к ресурсу балансировщика нагрузки для кластера на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="44faa-168">To see the configuration of the Azure load balancer, browse for the load balancer resource for the cluster in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="44faa-169">Ознакомьтесь с действиями в предыдущем примере.</span><span class="sxs-lookup"><span data-stu-id="44faa-169">See the steps in the previous example.</span></span>

### <a name="considerations"></a><span data-ttu-id="44faa-170">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="44faa-170">Considerations</span></span>

* <span data-ttu-id="44faa-171">Создание правила балансировки нагрузки выполняется асинхронно, и сведения о подготовленном балансировщике нагрузки публикуются в поле `status.loadBalancer` службы.</span><span class="sxs-lookup"><span data-stu-id="44faa-171">Creation of the load balancer rule happens asynchronously, and information about the provisioned balancer is published in the service’s `status.loadBalancer` field.</span></span>
* <span data-ttu-id="44faa-172">Каждой службе автоматически назначается собственный виртуальный IP-адрес в балансировщике нагрузки.</span><span class="sxs-lookup"><span data-stu-id="44faa-172">Every service is automatically assigned its own virtual IP address in the load balancer.</span></span>
* <span data-ttu-id="44faa-173">Если вы хотите получить доступ к балансировщику нагрузки с помощью DNS-имени, используйте поставщик службы доменных имен, чтобы создать DNS-имя для IP-адреса правила.</span><span class="sxs-lookup"><span data-stu-id="44faa-173">If you want to reach the load balancer by a DNS name, work with your domain service provider to create a DNS name for the rule's IP address.</span></span>

## <a name="http-or-https-traffic"></a><span data-ttu-id="44faa-174">Трафик HTTP или HTTPS</span><span class="sxs-lookup"><span data-stu-id="44faa-174">HTTP or HTTPS traffic</span></span>

<span data-ttu-id="44faa-175">Чтобы выполнить балансировку нагрузки трафика HTTP или HTTPS в веб-приложениях контейнера и управлять сертификатами для протокола TLS, можно использовать ресурс [Ingress](https://kubernetes.io/docs/user-guide/ingress/) Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="44faa-175">To load balance HTTP or HTTPS traffic to container web apps and manage certificates for transport layer security (TLS), you can use the Kubernetes [Ingress](https://kubernetes.io/docs/user-guide/ingress/) resource.</span></span> <span data-ttu-id="44faa-176">Ingress — это коллекция правил, которые обеспечивают входящие подключения для доступа к службам кластера.</span><span class="sxs-lookup"><span data-stu-id="44faa-176">An Ingress is a collection of rules that allow inbound connections to reach the cluster services.</span></span> <span data-ttu-id="44faa-177">Для работы ресурса Ingress в кластере Kubernetes должен быть запущен [контроллер Ingress](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers).</span><span class="sxs-lookup"><span data-stu-id="44faa-177">For an Ingress resource to work, the Kubernetes cluster must have an [Ingress controller](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) running.</span></span>

<span data-ttu-id="44faa-178">Служба контейнеров Azure не реализует контроллер Ingress Kubernetes автоматически.</span><span class="sxs-lookup"><span data-stu-id="44faa-178">Azure Container Service does not implement a Kubernetes Ingress controller automatically.</span></span> <span data-ttu-id="44faa-179">Доступны несколько реализаций контроллера.</span><span class="sxs-lookup"><span data-stu-id="44faa-179">Several controller implementations are available.</span></span> <span data-ttu-id="44faa-180">Сейчас мы рекомендуем настроить в [контроллере Ingress Nginx](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) правила Ingress и выполнить балансировку нагрузки трафика HTTP и HTTPS.</span><span class="sxs-lookup"><span data-stu-id="44faa-180">Currently, the [Nginx Ingress controller](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) is recommended to configure Ingress rules and load balance HTTP and HTTPS traffic.</span></span> 

<span data-ttu-id="44faa-181">Дополнительные сведения см. в [документации по контроллеру Ingress Nginx](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span><span class="sxs-lookup"><span data-stu-id="44faa-181">For more information, see the [Nginx Ingress controller documentation](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44faa-182">При использовании контроллера Ingress Nginx в Службе контейнеров Azure необходимо предоставить развертывание контроллера как службу с помощью `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="44faa-182">When using the Nginx Ingress controller in Azure Container Service, you must expose the controller deployment as a service with `type: LoadBalancer`.</span></span> <span data-ttu-id="44faa-183">При этом Azure Load Balancer будет настроен для маршрутизации трафика в контроллер.</span><span class="sxs-lookup"><span data-stu-id="44faa-183">This configures the Azure load balancer to route traffic to the controller.</span></span> <span data-ttu-id="44faa-184">Дополнительные сведения см. в предыдущем разделе.</span><span class="sxs-lookup"><span data-stu-id="44faa-184">For more information, see the previous section.</span></span>


## <a name="next-steps"></a><span data-ttu-id="44faa-185">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="44faa-185">Next steps</span></span>

* <span data-ttu-id="44faa-186">Ознакомьтесь с [документацией по Kubernetes LoadBalancer](https://kubernetes.io/docs/user-guide/load-balancer/)</span><span class="sxs-lookup"><span data-stu-id="44faa-186">See the [Kubernetes LoadBalancer documentation](https://kubernetes.io/docs/user-guide/load-balancer/)</span></span>
* <span data-ttu-id="44faa-187">Узнайте больше о [контроллерах Ingress Kubernetes](https://kubernetes.io/docs/user-guide/ingress/)</span><span class="sxs-lookup"><span data-stu-id="44faa-187">Learn more about [Kubernetes Ingress and Ingress controllers](https://kubernetes.io/docs/user-guide/ingress/)</span></span>
* <span data-ttu-id="44faa-188">Ознакомьтесь с [примерами Kubernetes](https://github.com/kubernetes/kubernetes/tree/master/examples)</span><span class="sxs-lookup"><span data-stu-id="44faa-188">See [Kubernetes examples](https://github.com/kubernetes/kubernetes/tree/master/examples)</span></span>

