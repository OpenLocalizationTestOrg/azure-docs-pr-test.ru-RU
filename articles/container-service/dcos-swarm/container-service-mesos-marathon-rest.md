---
title: "aaaManage Azure DC/OS кластера с помощью Marathon REST API | Документы Microsoft"
description: "Развертывание кластера контейнера службы Azure DC/OS tooan контейнеры с помощью API-интерфейса REST Marathon hello."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Mesos, Azure"
ms.assetid: c7175446-4507-4a33-a7a2-63583e5996e3
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: d926b9b90f5d4eda85a015d9ea0d96fea2c4b566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-container-management-through-hello-marathon-rest-api"></a><span data-ttu-id="7c8aa-104">Управление контейнерами DC/OS через API-Интерфейс REST Marathon hello</span><span class="sxs-lookup"><span data-stu-id="7c8aa-104">DC/OS container management through hello Marathon REST API</span></span>
<span data-ttu-id="7c8aa-105">Контроллер домена/OS предоставляет среду для развертывания и масштабирования кластерных рабочих нагрузок сталкиваясь аппаратным обеспечением hello.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting hello underlying hardware.</span></span> <span data-ttu-id="7c8aa-106">На базе DC/OS работает платформа, которая управляет планированием и выполнением вычислительных рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span> <span data-ttu-id="7c8aa-107">Несмотря на то, что платформы доступны для многих распространенных рабочих нагрузок, в этом документе позволяет начать создание и масштабирование развертывания контейнера с помощью API-интерфейса REST Marathon hello.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-107">Although frameworks are available for many popular workloads, this document gets you started creating and scaling container deployments by using hello Marathon REST API.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7c8aa-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7c8aa-108">Prerequisites</span></span>

<span data-ttu-id="7c8aa-109">Для выполнения этих примеров вам потребуется кластер DC/OS, настроенный в службе контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="7c8aa-110">Необходимо также кластера toothis toohave возможности удаленного подключения.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-110">You also need toohave remote connectivity toothis cluster.</span></span> <span data-ttu-id="7c8aa-111">Дополнительные сведения об этих элементах см. следующие статьи hello:</span><span class="sxs-lookup"><span data-stu-id="7c8aa-111">For more information on these items, see hello following articles:</span></span>

* [<span data-ttu-id="7c8aa-112">Развертывание кластера службы контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-112">Deploying an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="7c8aa-113">Подключение кластера tooan контейнера службы Azure</span><span class="sxs-lookup"><span data-stu-id="7c8aa-113">Connecting tooan Azure Container Service cluster</span></span>](../container-service-connect.md)

## <a name="access-hello-dcos-apis"></a><span data-ttu-id="7c8aa-114">Доступ к API-интерфейсы DC/OS hello</span><span class="sxs-lookup"><span data-stu-id="7c8aa-114">Access hello DC/OS APIs</span></span>
<span data-ttu-id="7c8aa-115">После toohello подключенных кластера контейнера службы Azure, доступны hello DC/OS и связанные API REST через порт http://localhost:local.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-115">After you are connected toohello Azure Container Service cluster, you can access hello DC/OS and related REST APIs through http://localhost:local-port.</span></span> <span data-ttu-id="7c8aa-116">Hello примерах в этом документе предполагается, что туннелирование на порт 80.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-116">hello examples in this document assume that you are tunneling on port 80.</span></span> <span data-ttu-id="7c8aa-117">Например, можно получить конечные точки Marathon hello в URI начиная с версии `http://localhost/marathon/v2/`.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-117">For example, hello Marathon endpoints can be reached at URIs beginning with `http://localhost/marathon/v2/`.</span></span> 

<span data-ttu-id="7c8aa-118">Дополнительные сведения о hello различных API-интерфейсов документации hello Mesosphere hello [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) и [Chronos API](https://mesos.github.io/chronos/docs/api.html)и в документации Apache hello [Mesos API планировщика ](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span><span class="sxs-lookup"><span data-stu-id="7c8aa-118">For more information on hello various APIs, see hello Mesosphere documentation for hello [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) and the [Chronos API](https://mesos.github.io/chronos/docs/api.html), and the Apache documentation for hello [Mesos Scheduler API](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span></span>

## <a name="gather-information-from-dcos-and-marathon"></a><span data-ttu-id="7c8aa-119">Сбор сведений из DC/OS и Marathon</span><span class="sxs-lookup"><span data-stu-id="7c8aa-119">Gather information from DC/OS and Marathon</span></span>
<span data-ttu-id="7c8aa-120">Перед развертыванием кластера DC/OS toohello контейнеры получить некоторые сведения о кластере DC/OS hello, такие как имена hello и состояние агентов DC/OS hello.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-120">Before you deploy containers toohello DC/OS cluster, gather some information about hello DC/OS cluster, such as hello names and status of hello DC/OS agents.</span></span> <span data-ttu-id="7c8aa-121">toodo таким образом, запрос hello `master/slaves` конечной точке API REST DC/OS hello.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-121">toodo so, query hello `master/slaves` endpoint of hello DC/OS REST API.</span></span> <span data-ttu-id="7c8aa-122">Если все пойдет хорошо hello запрос возвращает список агентов DC/OS и несколько свойств для каждого.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-122">If everything goes well, hello query returns a list of DC/OS agents and several properties for each.</span></span>

```bash
curl http://localhost/mesos/master/slaves
```

<span data-ttu-id="7c8aa-123">Теперь воспользуйтесь hello Marathon `/apps` toocheck конечной точки для текущего кластера DC/OS toohello развертывания приложения.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-123">Now, use hello Marathon `/apps` endpoint toocheck for current application deployments toohello DC/OS cluster.</span></span> <span data-ttu-id="7c8aa-124">Если это новый кластер, вы увидите пустой массив приложений.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-124">If this is a new cluster, you see an empty array for apps.</span></span>

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="7c8aa-125">Развертывание контейнера формата Docker</span><span class="sxs-lookup"><span data-stu-id="7c8aa-125">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="7c8aa-126">Контейнеры Docker формате через API-Интерфейс REST Marathon hello развертывание с помощью JSON-файл, описывающий hello предназначен развертывания.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-126">You deploy Docker-formatted containers through hello Marathon REST API by using a JSON file that describes hello intended deployment.</span></span> <span data-ttu-id="7c8aa-127">Hello следующий пример развертывает Nginx контейнера tooa закрытый агент в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-127">hello following sample deploys an Nginx container tooa private agent in hello cluster.</span></span> 

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

<span data-ttu-id="7c8aa-128">toodeploy контейнер Docker в формате хранения hello JSON-файла в доступном расположении.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-128">toodeploy a Docker-formatted container, store hello JSON file in an accessible location.</span></span> <span data-ttu-id="7c8aa-129">Далее, toodeploy hello контейнер, запустите следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-129">Next, toodeploy hello container, run hello following command.</span></span> <span data-ttu-id="7c8aa-130">Укажите имя hello hello JSON-файла (`marathon.json` в этом примере).</span><span class="sxs-lookup"><span data-stu-id="7c8aa-130">Specify hello name of hello JSON file (`marathon.json` in this example).</span></span>

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

<span data-ttu-id="7c8aa-131">Hello выходные данные выглядят аналогично toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="7c8aa-131">hello output is similar toohello following:</span></span>

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

<span data-ttu-id="7c8aa-132">Теперь при выполнении запроса Marathon для приложений, это новое приложение появляется в выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-132">Now, if you query Marathon for applications, this new application appears in hello output.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-hello-container"></a><span data-ttu-id="7c8aa-133">Достижения контейнера hello</span><span class="sxs-lookup"><span data-stu-id="7c8aa-133">Reach hello container</span></span>

<span data-ttu-id="7c8aa-134">Вы можете проверить, hello Nginx, запущенного на одном из агентов закрытый hello в кластере hello в контейнере.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-134">You can verify that hello Nginx is running in a container on one of hello private agents in hello cluster.</span></span> <span data-ttu-id="7c8aa-135">toofind hello узел и порт, где запущен контейнер hello, запросить Marathon hello запуска задач:</span><span class="sxs-lookup"><span data-stu-id="7c8aa-135">toofind hello host and port where hello container is running, query Marathon for hello running tasks:</span></span> 

```bash
curl localhost/marathon/v2/tasks
```

<span data-ttu-id="7c8aa-136">Найдите значение hello `host` в выходных данных hello (IP-адресов примерно слишком`10.32.0.x`), а значение hello `ports`.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-136">Find hello value of `host` in hello output (an IP address similar too`10.32.0.x`), and hello value of `ports`.</span></span>


<span data-ttu-id="7c8aa-137">Теперь можно проверить SSH терминалов (туннельного подключения) toohello Управление соединениями полное доменное имя кластера hello.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-137">Now make an SSH terminal connection (not a tunneled connection) toohello management FQDN of hello cluster.</span></span> <span data-ttu-id="7c8aa-138">После подключения сделать hello следующий запрос, заменив hello правильные значения `host` и `ports`:</span><span class="sxs-lookup"><span data-stu-id="7c8aa-138">Once connected, make hello following request, substituting hello correct values of `host` and `ports`:</span></span>

```bash
curl http://host:ports
```

<span data-ttu-id="7c8aa-139">Hello вывод server Nginx — аналогичные toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="7c8aa-139">hello Nginx server output is similar toohello following:</span></span>

![Доступ к Nginx из контейнера](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a><span data-ttu-id="7c8aa-141">Масштабирование контейнеров</span><span class="sxs-lookup"><span data-stu-id="7c8aa-141">Scale your containers</span></span>
<span data-ttu-id="7c8aa-142">В развертывании приложений можно использовать tooscale Marathon API hello out или масштаб.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-142">You can use hello Marathon API tooscale out or scale in application deployments.</span></span> <span data-ttu-id="7c8aa-143">В предыдущем примере hello развернут один экземпляр приложения.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-143">In hello previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="7c8aa-144">Давайте масштаба toothree экземпляров приложения.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-144">Let's scale this out toothree instances of an application.</span></span> <span data-ttu-id="7c8aa-145">Таким образом, toodo создания JSON-файла с помощью hello после текста JSON и сохранить ее в доступном расположении.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-145">toodo so, create a JSON file by using hello following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="7c8aa-146">Запустите из туннеля, следующая команда tooscale out приложения hello hello.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-146">From your tunneled connection, run hello following command tooscale out hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="7c8aa-147">Hello URI является http://localhost/marathon/v2/apps/ следуют идентификатор hello tooscale приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-147">hello URI is http://localhost/marathon/v2/apps/ followed by hello ID of hello application tooscale.</span></span> <span data-ttu-id="7c8aa-148">Если вы используете образец hello Nginx, предоставленная здесь, hello URI будет http://localhost/marathon/v2/apps/nginx.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-148">If you are using hello Nginx sample that is provided here, hello URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

<span data-ttu-id="7c8aa-149">Наконец запроса конечной точки Marathon hello для приложений.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-149">Finally, query hello Marathon endpoint for applications.</span></span> <span data-ttu-id="7c8aa-150">вы увидите, что теперь есть три контейнера Nginx.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-150">You see that there are now three Nginx containers.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a><span data-ttu-id="7c8aa-151">Аналогичные команды PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c8aa-151">Equivalent PowerShell commands</span></span>
<span data-ttu-id="7c8aa-152">Эти же действия можно выполнить с помощью команд PowerShell в системе Windows.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-152">You can perform these same actions by using PowerShell commands on a Windows system.</span></span>

<span data-ttu-id="7c8aa-153">toogather сведения о кластере DC/OS hello, например имена агентов и состояние агентов, выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-153">toogather information about hello DC/OS cluster, such as agent names and agent status, run hello following command:</span></span>

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

<span data-ttu-id="7c8aa-154">Контейнеры Docker формате через Marathon развертывание с помощью JSON-файл, описывающий hello предназначен развертывания.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-154">You deploy Docker-formatted containers through Marathon by using a JSON file that describes hello intended deployment.</span></span> <span data-ttu-id="7c8aa-155">Hello следующий пример развертывает контейнера Nginx hello, привязки контроллера домена/OS hello агента tooport 80 контейнера hello порт 80.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-155">hello following sample deploys hello Nginx container, binding port 80 of hello DC/OS agent tooport 80 of hello container.</span></span>

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

<span data-ttu-id="7c8aa-156">toodeploy контейнер Docker в формате хранения hello JSON-файла в доступном расположении.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-156">toodeploy a Docker-formatted container, store hello JSON file in an accessible location.</span></span> <span data-ttu-id="7c8aa-157">Далее, toodeploy hello контейнер, запустите следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-157">Next, toodeploy hello container, run hello following command.</span></span> <span data-ttu-id="7c8aa-158">Укажите путь toohello hello JSON-файла (`marathon.json` в этом примере).</span><span class="sxs-lookup"><span data-stu-id="7c8aa-158">Specify hello path toohello JSON file (`marathon.json` in this example).</span></span>

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

<span data-ttu-id="7c8aa-159">Также можно использовать tooscale Marathon API hello out или масштаб в развертывании приложений.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-159">You can also use hello Marathon API tooscale out or scale in application deployments.</span></span> <span data-ttu-id="7c8aa-160">В предыдущем примере hello развернут один экземпляр приложения.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-160">In hello previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="7c8aa-161">Давайте масштаба toothree экземпляров приложения.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-161">Let's scale this out toothree instances of an application.</span></span> <span data-ttu-id="7c8aa-162">Таким образом, toodo создания JSON-файла с помощью hello после текста JSON и сохранить ее в доступном расположении.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-162">toodo so, create a JSON file by using hello following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="7c8aa-163">Следующая команда tooscale out приложения hello выполнения hello:</span><span class="sxs-lookup"><span data-stu-id="7c8aa-163">Run hello following command tooscale out hello application:</span></span>

> [!NOTE]
> <span data-ttu-id="7c8aa-164">Hello URI является http://localhost/marathon/v2/apps/ следуют идентификатор hello tooscale приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-164">hello URI is http://localhost/marathon/v2/apps/ followed by hello ID of hello application tooscale.</span></span> <span data-ttu-id="7c8aa-165">Если вы используете пример hello Nginx, описанный здесь, hello URI будет http://localhost/marathon/v2/apps/nginx.</span><span class="sxs-lookup"><span data-stu-id="7c8aa-165">If you are using hello Nginx sample provided here, hello URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a><span data-ttu-id="7c8aa-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7c8aa-166">Next steps</span></span>
* [<span data-ttu-id="7c8aa-167">Дополнительные сведения о конечных точек Mesos HTTP hello</span><span class="sxs-lookup"><span data-stu-id="7c8aa-167">Read more about hello Mesos HTTP endpoints</span></span>](http://mesos.apache.org/documentation/latest/endpoints/)
* [<span data-ttu-id="7c8aa-168">Дополнительные сведения об API-интерфейса REST Marathon hello</span><span class="sxs-lookup"><span data-stu-id="7c8aa-168">Read more about hello Marathon REST API</span></span>](https://mesosphere.github.io/marathon/docs/rest-api.html)

