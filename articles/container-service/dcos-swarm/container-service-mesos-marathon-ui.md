---
title: "Управление кластером DC/OS Azure с помощью пользовательского интерфейса Marathon | Документация Майкрософт"
description: "Развертывание контейнеров в кластере службы контейнеров Azure с помощью веб-интерфейса Marathon."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: b00088bb005519dc5d533433308c0e3e33c7f433
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-the-marathon-web-ui"></a><span data-ttu-id="181d8-104">Управление контейнером DC/OS службы контейнеров Azure с помощью веб-интерфейса Marathon</span><span class="sxs-lookup"><span data-stu-id="181d8-104">Manage an Azure Container Service DC/OS cluster through the Marathon web UI</span></span>
<span data-ttu-id="181d8-105">DC/OS — это среда для развертывания и масштабирования кластерных рабочих нагрузок, в которой используемое оборудование рассматривается абстрактно.</span><span class="sxs-lookup"><span data-stu-id="181d8-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting the underlying hardware.</span></span> <span data-ttu-id="181d8-106">На базе DC/OS работает платформа, которая управляет планированием и выполнением вычислительных рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="181d8-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span>

<span data-ttu-id="181d8-107">Хотя доступны платформы для многих популярных рабочих нагрузок, в этом документе описывается, как приступить к развертыванию контейнеров с помощью Marathon.</span><span class="sxs-lookup"><span data-stu-id="181d8-107">While frameworks are available for many popular workloads, this document describes how to get started deploying containers with Marathon.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="181d8-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="181d8-108">Prerequisites</span></span>
<span data-ttu-id="181d8-109">Для выполнения этих примеров вам потребуется кластер DC/OS, настроенный в службе контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="181d8-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="181d8-110">Необходимо также удаленное подключение к этому кластеру.</span><span class="sxs-lookup"><span data-stu-id="181d8-110">You also need to have remote connectivity to this cluster.</span></span> <span data-ttu-id="181d8-111">Дополнительные сведения об этих компонентах см. в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="181d8-111">For more information on these items, see the following articles:</span></span>

* [<span data-ttu-id="181d8-112">Развертывание кластера службы контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="181d8-112">Deploy an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="181d8-113">Подключение к кластеру службы контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="181d8-113">Connect to an Azure Container Service cluster</span></span>](../container-service-connect.md)

> [!NOTE]
> <span data-ttu-id="181d8-114">В этой статье предполагается, что туннельное подключение к кластеру DC/OS устанавливается через локальный порт 80.</span><span class="sxs-lookup"><span data-stu-id="181d8-114">This article assumes you are tunneling to the DC/OS cluster through your local port 80.</span></span>
>

## <a name="explore-the-dcos-ui"></a><span data-ttu-id="181d8-115">Изучение пользовательского интерфейса DC/OS</span><span class="sxs-lookup"><span data-stu-id="181d8-115">Explore the DC/OS UI</span></span>
<span data-ttu-id="181d8-116">[Установив](../container-service-connect.md) туннель Secure Shell (SSH), перейдите по адресу http://localhost/.</span><span class="sxs-lookup"><span data-stu-id="181d8-116">With a Secure Shell (SSH) tunnel [established](../container-service-connect.md), browse to http://localhost/.</span></span> <span data-ttu-id="181d8-117">Загрузится веб-интерфейс DC/OS, а затем вы увидите сведения о кластере, в том числе об используемых ресурсах, активных агентах и запущенных службах.</span><span class="sxs-lookup"><span data-stu-id="181d8-117">This loads the DC/OS web UI and shows information about the cluster, such as used resources, active agents, and running services.</span></span>

![Пользовательский интерфейс DC/OS](./media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-the-marathon-ui"></a><span data-ttu-id="181d8-119">Изучение пользовательского интерфейса Marathon</span><span class="sxs-lookup"><span data-stu-id="181d8-119">Explore the Marathon UI</span></span>
<span data-ttu-id="181d8-120">Чтобы открыть пользовательский интерфейс Marathon, перейдите по адресу http://localhost/marathon.</span><span class="sxs-lookup"><span data-stu-id="181d8-120">To see the Marathon UI, browse to http://localhost/marathon.</span></span> <span data-ttu-id="181d8-121">На этом экране можно запустить новый контейнер или другие приложения в кластере DC/OS службы контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="181d8-121">From this screen, you can start a new container or another application on the Azure Container Service DC/OS cluster.</span></span> <span data-ttu-id="181d8-122">Здесь вы также можете просмотреть информацию о работе контейнеров и приложений.</span><span class="sxs-lookup"><span data-stu-id="181d8-122">You can also see information about running containers and applications.</span></span>  

![Пользовательский интерфейс Marathon](./media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="181d8-124">Развертывание контейнера формата Docker</span><span class="sxs-lookup"><span data-stu-id="181d8-124">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="181d8-125">Чтобы развернуть новый контейнер с помощью Marathon, нажмите кнопку **Create Application** (Создать приложение) и заполните форму следующим образом.</span><span class="sxs-lookup"><span data-stu-id="181d8-125">To deploy a new container by using Marathon, click **Create Application**, and enter the following information into the form tabs:</span></span>

| <span data-ttu-id="181d8-126">Поле</span><span class="sxs-lookup"><span data-stu-id="181d8-126">Field</span></span> | <span data-ttu-id="181d8-127">Значение</span><span class="sxs-lookup"><span data-stu-id="181d8-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="181d8-128">ИД</span><span class="sxs-lookup"><span data-stu-id="181d8-128">ID</span></span> |<span data-ttu-id="181d8-129">nginx</span><span class="sxs-lookup"><span data-stu-id="181d8-129">nginx</span></span> |
| <span data-ttu-id="181d8-130">Память</span><span class="sxs-lookup"><span data-stu-id="181d8-130">Memory</span></span> | <span data-ttu-id="181d8-131">32</span><span class="sxs-lookup"><span data-stu-id="181d8-131">32</span></span> |
| <span data-ttu-id="181d8-132">Образ —</span><span class="sxs-lookup"><span data-stu-id="181d8-132">Image</span></span> |<span data-ttu-id="181d8-133">nginx</span><span class="sxs-lookup"><span data-stu-id="181d8-133">nginx</span></span> |
| <span data-ttu-id="181d8-134">Сеть</span><span class="sxs-lookup"><span data-stu-id="181d8-134">Network</span></span> |<span data-ttu-id="181d8-135">Bridged (Мостовая)</span><span class="sxs-lookup"><span data-stu-id="181d8-135">Bridged</span></span> |
| <span data-ttu-id="181d8-136">Host Port (Порт узла)</span><span class="sxs-lookup"><span data-stu-id="181d8-136">Host Port</span></span> |<span data-ttu-id="181d8-137">80</span><span class="sxs-lookup"><span data-stu-id="181d8-137">80</span></span> |
| <span data-ttu-id="181d8-138">Протокол</span><span class="sxs-lookup"><span data-stu-id="181d8-138">Protocol</span></span> |<span data-ttu-id="181d8-139">TCP</span><span class="sxs-lookup"><span data-stu-id="181d8-139">TCP</span></span> |

![Пользовательский интерфейс нового приложения: вкладка "Общие"](./media/container-service-mesos-marathon-ui/dcos4.png)

![Пользовательский интерфейс нового приложения: контейнер Docker](./media/container-service-mesos-marathon-ui/dcos5.png)

![Пользовательский интерфейс нового приложения: обнаружение служб и портов](./media/container-service-mesos-marathon-ui/dcos6.png)

<span data-ttu-id="181d8-143">Статически сопоставить порт контейнера с портом на агенте можно в режиме JSON.</span><span class="sxs-lookup"><span data-stu-id="181d8-143">If you want to statically map the container port to a port on the agent, you need to use JSON Mode.</span></span> <span data-ttu-id="181d8-144">Для этого с помощью переключателя перейдите в мастере создания приложений в **режим JSON** .</span><span class="sxs-lookup"><span data-stu-id="181d8-144">To do so, switch the New Application wizard to **JSON Mode** by using the toggle.</span></span> <span data-ttu-id="181d8-145">Затем введите следующее в разделе `portMappings` определения приложения.</span><span class="sxs-lookup"><span data-stu-id="181d8-145">Then enter the following setting under the `portMappings` section of the application definition.</span></span> <span data-ttu-id="181d8-146">В этом примере порт 80 контейнера привязывается к порту 80 агента DC/OS.</span><span class="sxs-lookup"><span data-stu-id="181d8-146">This example binds port 80 of the container to port 80 of the DC/OS agent.</span></span> <span data-ttu-id="181d8-147">Когда изменение будет внесено, мастер можно перевести в другой режим.</span><span class="sxs-lookup"><span data-stu-id="181d8-147">You can switch this wizard out of JSON Mode after you make this change.</span></span>

```none
"hostPort": 80,
```

![Пользовательский интерфейс нового приложения: пример порта 80](./media/container-service-mesos-marathon-ui/dcos13.png)

<span data-ttu-id="181d8-149">Если вы хотите включить проверку работоспособности, задайте путь на вкладке **Health Checks** (Проверки работоспособности).</span><span class="sxs-lookup"><span data-stu-id="181d8-149">If you want to enable health checks, set a path on the **Health Checks** tab.</span></span>

![Пользовательский интерфейс "Новое приложение", вкладка "Проверки работоспособности"](./media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

<span data-ttu-id="181d8-151">Кластер DC/OS развертывается с использованием набора частных и общедоступных агентов.</span><span class="sxs-lookup"><span data-stu-id="181d8-151">The DC/OS cluster is deployed with set of private and public agents.</span></span> <span data-ttu-id="181d8-152">Чтобы кластер мог получать доступ к приложениям из Интернета, развертывание необходимо выполнять на общедоступном агенте.</span><span class="sxs-lookup"><span data-stu-id="181d8-152">For the cluster to be able to access applications from the Internet, you need to deploy the applications to a public agent.</span></span> <span data-ttu-id="181d8-153">Для этого в мастере создания приложений перейдите на вкладку **Optional** (Дополнительно) и присвойте параметру **Accepted Resource Roles** (Принятые роли ресурсов) значение **slave_public**.</span><span class="sxs-lookup"><span data-stu-id="181d8-153">To do so, select the **Optional** tab of the New Application wizard and enter **slave_public** for the **Accepted Resource Roles**.</span></span>

<span data-ttu-id="181d8-154">Затем щелкните **Create Application** (Создать приложение).</span><span class="sxs-lookup"><span data-stu-id="181d8-154">Then click **Create Application**.</span></span>

![Пользовательский интерфейс нового приложения: параметры общедоступного агента](./media/container-service-mesos-marathon-ui/dcos14.png)

<span data-ttu-id="181d8-156">Вернитесь на главную страницу Marathon, чтобы просмотреть состояние развертывания контейнера.</span><span class="sxs-lookup"><span data-stu-id="181d8-156">Back on the Marathon main page, you can see the deployment status for the container.</span></span> <span data-ttu-id="181d8-157">Сначала отобразится состояние **Deploying** (Развертывание).</span><span class="sxs-lookup"><span data-stu-id="181d8-157">Initially you see a status of **Deploying**.</span></span> <span data-ttu-id="181d8-158">После успешного развертывания состояние изменится на **Running** (Работает).</span><span class="sxs-lookup"><span data-stu-id="181d8-158">After a successful deployment, the status changes to **Running**.</span></span>

![Пользовательский интерфейс главной страницы Marathon: состояние развертывания контейнера](./media/container-service-mesos-marathon-ui/dcos7.png)

<span data-ttu-id="181d8-160">При переключении обратно к пользовательскому веб-интерфейсу DC/OS (http://localhost/) вы увидите, что задача (в нашем случае это контейнер в формате Docker) выполняется в кластере DC/OS.</span><span class="sxs-lookup"><span data-stu-id="181d8-160">When you switch back to the DC/OS web UI (http://localhost/), you see that a task (in this case, a Docker-formatted container) is running on the DC/OS cluster.</span></span>

![Пользовательский веб-интерфейс DC/OS: выполнение задачи в кластере](./media/container-service-mesos-marathon-ui/dcos8.png)

<span data-ttu-id="181d8-162">Чтобы увидеть узел кластера, на котором выполняется задача, щелкните вкладку **Nodes** (Узлы).</span><span class="sxs-lookup"><span data-stu-id="181d8-162">To see the cluster node that the task is running on, click the **Nodes** tab.</span></span>

![Пользовательский веб-интерфейс DC/OS: узел кластера, на котором выполняется задача](./media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-the-container"></a><span data-ttu-id="181d8-164">Обращение к контейнеру</span><span class="sxs-lookup"><span data-stu-id="181d8-164">Reach the container</span></span>

<span data-ttu-id="181d8-165">В этом примере приложение выполняется на узле общедоступного агента.</span><span class="sxs-lookup"><span data-stu-id="181d8-165">In this example, the application is running on a public agent node.</span></span> <span data-ttu-id="181d8-166">Доступ к приложению вы осуществляете из Интернета, перейдя по полному доменному имени агента кластера `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, где:</span><span class="sxs-lookup"><span data-stu-id="181d8-166">You reach the application from the internet by browsing to the agent FQDN of the cluster: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, where:</span></span>

* <span data-ttu-id="181d8-167">**DNSPREFIX** — префикс DNS, указанный при развертывании кластера.</span><span class="sxs-lookup"><span data-stu-id="181d8-167">**DNSPREFIX** is the DNS prefix that you provided when you deployed the cluster.</span></span>
* <span data-ttu-id="181d8-168">**REGION** — регион, в котором расположена ваша группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="181d8-168">**REGION** is the region in which your resource group is located.</span></span>

    ![Доступ к Nginx из Интернета](./media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a><span data-ttu-id="181d8-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="181d8-170">Next steps</span></span>
* [<span data-ttu-id="181d8-171">Работа с API для Marathon и API для DC/OS</span><span class="sxs-lookup"><span data-stu-id="181d8-171">Work with DC/OS and the Marathon API</span></span>](container-service-mesos-marathon-rest.md)

* <span data-ttu-id="181d8-172">Подробное изучение службы контейнеров Azure с Mesos</span><span class="sxs-lookup"><span data-stu-id="181d8-172">Deep dive on the Azure Container Service with Mesos</span></span>

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 
