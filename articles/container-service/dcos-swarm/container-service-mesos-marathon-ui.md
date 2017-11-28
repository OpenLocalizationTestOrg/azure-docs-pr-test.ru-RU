---
title: "aaaManage Azure DC/OS кластера с пользовательским Интерфейсом Marathon | Документы Microsoft"
description: "Развертывание службы кластеров контейнеры tooan контейнера службы Azure с помощью hello Marathon пользовательского веб-интерфейса."
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
ms.openlocfilehash: a90180e1b4763e6d2ddfa699ed4b7269f209f728
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-hello-marathon-web-ui"></a><span data-ttu-id="0747a-104">Управление контейнера службы Azure DC/OS кластера с помощью hello Marathon пользовательского веб-интерфейса</span><span class="sxs-lookup"><span data-stu-id="0747a-104">Manage an Azure Container Service DC/OS cluster through hello Marathon web UI</span></span>
<span data-ttu-id="0747a-105">Контроллер домена/OS предоставляет среду для развертывания и масштабирования кластерных рабочих нагрузок сталкиваясь аппаратным обеспечением hello.</span><span class="sxs-lookup"><span data-stu-id="0747a-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting hello underlying hardware.</span></span> <span data-ttu-id="0747a-106">На базе DC/OS работает платформа, которая управляет планированием и выполнением вычислительных рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="0747a-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span>

<span data-ttu-id="0747a-107">Хотя платформы доступны для многих распространенных рабочих нагрузок, в этом документе описывается, как tooget запущена развертывания контейнеров с Marathon.</span><span class="sxs-lookup"><span data-stu-id="0747a-107">While frameworks are available for many popular workloads, this document describes how tooget started deploying containers with Marathon.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="0747a-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0747a-108">Prerequisites</span></span>
<span data-ttu-id="0747a-109">Для выполнения этих примеров вам потребуется кластер DC/OS, настроенный в службе контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="0747a-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="0747a-110">Необходимо также кластера toothis toohave возможности удаленного подключения.</span><span class="sxs-lookup"><span data-stu-id="0747a-110">You also need toohave remote connectivity toothis cluster.</span></span> <span data-ttu-id="0747a-111">Дополнительные сведения об этих элементах см. следующие статьи hello:</span><span class="sxs-lookup"><span data-stu-id="0747a-111">For more information on these items, see hello following articles:</span></span>

* [<span data-ttu-id="0747a-112">Развертывание кластера службы контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="0747a-112">Deploy an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="0747a-113">Подключите кластер tooan контейнера службы Azure</span><span class="sxs-lookup"><span data-stu-id="0747a-113">Connect tooan Azure Container Service cluster</span></span>](../container-service-connect.md)

> [!NOTE]
> <span data-ttu-id="0747a-114">В этой статье предполагается, что toohello DC/OS кластера туннелирования через локальный порт 80.</span><span class="sxs-lookup"><span data-stu-id="0747a-114">This article assumes you are tunneling toohello DC/OS cluster through your local port 80.</span></span>
>

## <a name="explore-hello-dcos-ui"></a><span data-ttu-id="0747a-115">Просмотр hello DC/OS пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="0747a-115">Explore hello DC/OS UI</span></span>
<span data-ttu-id="0747a-116">Secure Shell (SSH) туннелю [установить](../container-service-connect.md), Обзор toohttp://localhost/.</span><span class="sxs-lookup"><span data-stu-id="0747a-116">With a Secure Shell (SSH) tunnel [established](../container-service-connect.md), browse toohttp://localhost/.</span></span> <span data-ttu-id="0747a-117">Это загружает hello DC/OS пользовательского веб-интерфейса и отображает сведения о кластере hello, например используемых ресурсов, агенты active и работу служб.</span><span class="sxs-lookup"><span data-stu-id="0747a-117">This loads hello DC/OS web UI and shows information about hello cluster, such as used resources, active agents, and running services.</span></span>

![Пользовательский интерфейс DC/OS](./media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-hello-marathon-ui"></a><span data-ttu-id="0747a-119">Просмотр hello Marathon пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="0747a-119">Explore hello Marathon UI</span></span>
<span data-ttu-id="0747a-120">Здравствуйте, toosee Marathon пользовательского интерфейса, toohttp://localhost/marathon обзора.</span><span class="sxs-lookup"><span data-stu-id="0747a-120">toosee hello Marathon UI, browse toohttp://localhost/marathon.</span></span> <span data-ttu-id="0747a-121">На этом экране можно запустить новый контейнер или другое приложение hello контейнера службы Azure DC/OS кластера.</span><span class="sxs-lookup"><span data-stu-id="0747a-121">From this screen, you can start a new container or another application on hello Azure Container Service DC/OS cluster.</span></span> <span data-ttu-id="0747a-122">Здесь вы также можете просмотреть информацию о работе контейнеров и приложений.</span><span class="sxs-lookup"><span data-stu-id="0747a-122">You can also see information about running containers and applications.</span></span>  

![Пользовательский интерфейс Marathon](./media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="0747a-124">Развертывание контейнера формата Docker</span><span class="sxs-lookup"><span data-stu-id="0747a-124">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="0747a-125">Щелкните новый контейнер с помощью Marathon, toodeploy **Создание приложения**и введите следующую информацию в вкладок формы hello hello:</span><span class="sxs-lookup"><span data-stu-id="0747a-125">toodeploy a new container by using Marathon, click **Create Application**, and enter hello following information into hello form tabs:</span></span>

| <span data-ttu-id="0747a-126">Поле</span><span class="sxs-lookup"><span data-stu-id="0747a-126">Field</span></span> | <span data-ttu-id="0747a-127">Значение</span><span class="sxs-lookup"><span data-stu-id="0747a-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0747a-128">ИД</span><span class="sxs-lookup"><span data-stu-id="0747a-128">ID</span></span> |<span data-ttu-id="0747a-129">nginx</span><span class="sxs-lookup"><span data-stu-id="0747a-129">nginx</span></span> |
| <span data-ttu-id="0747a-130">Память</span><span class="sxs-lookup"><span data-stu-id="0747a-130">Memory</span></span> | <span data-ttu-id="0747a-131">32</span><span class="sxs-lookup"><span data-stu-id="0747a-131">32</span></span> |
| <span data-ttu-id="0747a-132">Образ —</span><span class="sxs-lookup"><span data-stu-id="0747a-132">Image</span></span> |<span data-ttu-id="0747a-133">nginx</span><span class="sxs-lookup"><span data-stu-id="0747a-133">nginx</span></span> |
| <span data-ttu-id="0747a-134">Сеть</span><span class="sxs-lookup"><span data-stu-id="0747a-134">Network</span></span> |<span data-ttu-id="0747a-135">Bridged (Мостовая)</span><span class="sxs-lookup"><span data-stu-id="0747a-135">Bridged</span></span> |
| <span data-ttu-id="0747a-136">Host Port (Порт узла)</span><span class="sxs-lookup"><span data-stu-id="0747a-136">Host Port</span></span> |<span data-ttu-id="0747a-137">80</span><span class="sxs-lookup"><span data-stu-id="0747a-137">80</span></span> |
| <span data-ttu-id="0747a-138">Протокол</span><span class="sxs-lookup"><span data-stu-id="0747a-138">Protocol</span></span> |<span data-ttu-id="0747a-139">TCP</span><span class="sxs-lookup"><span data-stu-id="0747a-139">TCP</span></span> |

![Пользовательский интерфейс нового приложения: вкладка "Общие"](./media/container-service-mesos-marathon-ui/dcos4.png)

![Пользовательский интерфейс нового приложения: контейнер Docker](./media/container-service-mesos-marathon-ui/dcos5.png)

![Пользовательский интерфейс нового приложения: обнаружение служб и портов](./media/container-service-mesos-marathon-ui/dcos6.png)

<span data-ttu-id="0747a-143">Если требуется порт toostatically карты hello порт контейнера tooa hello агента необходимо toouse режим JSON.</span><span class="sxs-lookup"><span data-stu-id="0747a-143">If you want toostatically map hello container port tooa port on hello agent, you need toouse JSON Mode.</span></span> <span data-ttu-id="0747a-144">toodo таким образом, переключение мастер новое приложение hello слишком**JSON режим** с помощью переключателя hello.</span><span class="sxs-lookup"><span data-stu-id="0747a-144">toodo so, switch hello New Application wizard too**JSON Mode** by using hello toggle.</span></span> <span data-ttu-id="0747a-145">Затем введите следующий параметр в разделе hello hello `portMappings` раздел определения приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0747a-145">Then enter hello following setting under hello `portMappings` section of hello application definition.</span></span> <span data-ttu-id="0747a-146">В этом примере привязывает портом 80 контейнера hello tooport 80 hello DC/OS агента.</span><span class="sxs-lookup"><span data-stu-id="0747a-146">This example binds port 80 of hello container tooport 80 of hello DC/OS agent.</span></span> <span data-ttu-id="0747a-147">Когда изменение будет внесено, мастер можно перевести в другой режим.</span><span class="sxs-lookup"><span data-stu-id="0747a-147">You can switch this wizard out of JSON Mode after you make this change.</span></span>

```none
"hostPort": 80,
```

![Пользовательский интерфейс нового приложения: пример порта 80](./media/container-service-mesos-marathon-ui/dcos13.png)

<span data-ttu-id="0747a-149">Проверку работоспособности tooenable следует задать путь на hello **работоспособности проверяет** вкладки.</span><span class="sxs-lookup"><span data-stu-id="0747a-149">If you want tooenable health checks, set a path on hello **Health Checks** tab.</span></span>

![Пользовательский интерфейс "Новое приложение", вкладка "Проверки работоспособности"](./media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

<span data-ttu-id="0747a-151">с набором агентов частных и общедоступных развернут кластер DC/OS Hello.</span><span class="sxs-lookup"><span data-stu-id="0747a-151">hello DC/OS cluster is deployed with set of private and public agents.</span></span> <span data-ttu-id="0747a-152">Для hello кластера toobe может tooaccess приложений из Интернета hello необходимо toodeploy приложения hello tooa открытый агента.</span><span class="sxs-lookup"><span data-stu-id="0747a-152">For hello cluster toobe able tooaccess applications from hello Internet, you need toodeploy hello applications tooa public agent.</span></span> <span data-ttu-id="0747a-153">toodo таким образом, выберите hello **необязательно** вкладке Мастер новое приложение hello и введите **slave_public** для hello **принят ролей ресурса**.</span><span class="sxs-lookup"><span data-stu-id="0747a-153">toodo so, select hello **Optional** tab of hello New Application wizard and enter **slave_public** for hello **Accepted Resource Roles**.</span></span>

<span data-ttu-id="0747a-154">Затем щелкните **Create Application** (Создать приложение).</span><span class="sxs-lookup"><span data-stu-id="0747a-154">Then click **Create Application**.</span></span>

![Пользовательский интерфейс нового приложения: параметры общедоступного агента](./media/container-service-mesos-marathon-ui/dcos14.png)

<span data-ttu-id="0747a-156">На главной странице Marathon hello можно просмотреть состояние развертывания hello для контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="0747a-156">Back on hello Marathon main page, you can see hello deployment status for hello container.</span></span> <span data-ttu-id="0747a-157">Сначала отобразится состояние **Deploying** (Развертывание).</span><span class="sxs-lookup"><span data-stu-id="0747a-157">Initially you see a status of **Deploying**.</span></span> <span data-ttu-id="0747a-158">После успешного развертывания hello изменения состояния слишком**под управлением**.</span><span class="sxs-lookup"><span data-stu-id="0747a-158">After a successful deployment, hello status changes too**Running**.</span></span>

![Пользовательский интерфейс главной страницы Marathon: состояние развертывания контейнера](./media/container-service-mesos-marathon-ui/dcos7.png)

<span data-ttu-id="0747a-160">При переходе назад toohello DC/OS пользовательского веб-интерфейса (http://localhost/), вы видите, что задачи (в данном случае контейнер Docker в формате) работает на кластере DC/OS hello.</span><span class="sxs-lookup"><span data-stu-id="0747a-160">When you switch back toohello DC/OS web UI (http://localhost/), you see that a task (in this case, a Docker-formatted container) is running on hello DC/OS cluster.</span></span>

![Контроллер домена/OS веб-Интерфейс — задачи, выполняемой в кластере hello](./media/container-service-mesos-marathon-ui/dcos8.png)

<span data-ttu-id="0747a-162">узел кластера hello toosee, hello задача выполняется на приветствия щелкните **узлы** вкладки.</span><span class="sxs-lookup"><span data-stu-id="0747a-162">toosee hello cluster node that hello task is running on, click hello **Nodes** tab.</span></span>

![Пользовательский веб-интерфейс DC/OS: узел кластера, на котором выполняется задача](./media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-hello-container"></a><span data-ttu-id="0747a-164">Достижения контейнера hello</span><span class="sxs-lookup"><span data-stu-id="0747a-164">Reach hello container</span></span>

<span data-ttu-id="0747a-165">В этом примере hello приложение выполняется на узле открытого агента.</span><span class="sxs-lookup"><span data-stu-id="0747a-165">In this example, hello application is running on a public agent node.</span></span> <span data-ttu-id="0747a-166">Достичь приложение hello из hello Интернет путем просмотра агента toohello полное доменное имя кластера hello: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, где:</span><span class="sxs-lookup"><span data-stu-id="0747a-166">You reach hello application from hello internet by browsing toohello agent FQDN of hello cluster: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, where:</span></span>

* <span data-ttu-id="0747a-167">**DNSPREFIX** — префикс DNS hello, указанный при развертывании кластера hello.</span><span class="sxs-lookup"><span data-stu-id="0747a-167">**DNSPREFIX** is hello DNS prefix that you provided when you deployed hello cluster.</span></span>
* <span data-ttu-id="0747a-168">**ОБЛАСТЬ** — hello область, в которой находится в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0747a-168">**REGION** is hello region in which your resource group is located.</span></span>

    ![Доступ к Nginx из Интернета](./media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a><span data-ttu-id="0747a-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0747a-170">Next steps</span></span>
* [<span data-ttu-id="0747a-171">Работа с контроллера домена/OS и hello Marathon API</span><span class="sxs-lookup"><span data-stu-id="0747a-171">Work with DC/OS and hello Marathon API</span></span>](container-service-mesos-marathon-rest.md)

* <span data-ttu-id="0747a-172">Близкое знакомство с hello контейнера службы Azure с Mesos</span><span class="sxs-lookup"><span data-stu-id="0747a-172">Deep dive on hello Azure Container Service with Mesos</span></span>

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 
