---
title: "aaaUse черновик с контейнера службы Azure и Azure контейнер реестра | Документы Microsoft"
description: "Создание кластера служб ACS Kubernetes и toocreate реестра контейнера Azure первого приложения в Azure с черновик."
services: container-service
documentationcenter: 
author: squillace
manager: gamonroy
editor: 
tags: draft, helm, acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Kubernetes, черновик, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: f5e21cda01e5e8452bf86a5c8fa458904d89f451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-toobuild-and-deploy-an-application-tookubernetes"></a><span data-ttu-id="c8f0d-104">Использовать черновик с toobuild контейнера службы Azure и Azure контейнер реестра и развертывать приложения tooKubernetes</span><span class="sxs-lookup"><span data-stu-id="c8f0d-104">Use Draft with Azure Container Service and Azure Container Registry toobuild and deploy an application tooKubernetes</span></span>

<span data-ttu-id="c8f0d-105">[Черновик](https://aka.ms/draft) новое средство открытым исходным кодом, которое делает его легко toodevelop контейнера-приложениям и разверните tooKubernetes кластеры без знания многое о Docker и Kubernetes--или даже их установки.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-105">[Draft](https://aka.ms/draft) is a new open-source tool that makes it easy toodevelop container-based applications and deploy them tooKubernetes clusters without knowing much about Docker and Kubernetes -- or even installing them.</span></span> <span data-ttu-id="c8f0d-106">С помощью таких средств, как черновик позволяют вам и группам фокус ввода Создание приложения hello с Kubernetes, не обращая tooinfrastructure столько внимания.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-106">Using tools like Draft let you and your teams focus on building hello application with Kubernetes, not paying as much attention tooinfrastructure.</span></span>

<span data-ttu-id="c8f0d-107">Вы можете использовать черновик с любым реестром образов Docker и любым кластером Kubernetes, а также использовать его локально.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-107">You can use Draft with any Docker image registry and any Kubernetes cluster, including locally.</span></span> <span data-ttu-id="c8f0d-108">В этом учебнике показано, как toouse ACS с toocreate Kubernetes, контроля доступа и Azure DNS конвейера с помощью черновик динамической разработчик CI или компакт-диска.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-108">This tutorial shows how toouse ACS with Kubernetes, ACR, and Azure DNS toocreate a live CI/CD developer pipeline using Draft.</span></span>


## <a name="create-an-azure-container-registry"></a><span data-ttu-id="c8f0d-109">Создание реестра контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="c8f0d-109">Create an Azure Container Registry</span></span>
<span data-ttu-id="c8f0d-110">Вы можете легко [создать новый контейнер реестра Azure](../../container-registry/container-registry-get-started-azure-cli.md), но действий hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c8f0d-110">You can easily [create a new Azure Container Registry](../../container-registry/container-registry-get-started-azure-cli.md), but hello steps are as follows:</span></span>

1. <span data-ttu-id="c8f0d-111">Создайте кластер ACR реестра и hello Kubernetes toomanage группы ресурсов Azure в ACS.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-111">Create a Azure resource group toomanage your ACR registry and hello Kubernetes cluster in ACS.</span></span>
      ```azurecli
      az group create --name draft --location eastus
      ```

2. <span data-ttu-id="c8f0d-112">Создайте реестр образов ACR с помощью команды [az acr create](/cli/azure/acr#create).</span><span class="sxs-lookup"><span data-stu-id="c8f0d-112">Create an ACR image registry using [az acr create](/cli/azure/acr#create)</span></span>
      ```azurecli
      az acr create -g draft -n draftacs --sku Basic --admin-enabled true -l eastus
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a><span data-ttu-id="c8f0d-113">Создание службы контейнеров Azure с помощью Kubernetes</span><span class="sxs-lookup"><span data-stu-id="c8f0d-113">Create an Azure Container Service with Kubernetes</span></span>

<span data-ttu-id="c8f0d-114">Теперь вы готовы toouse [создать acs az](/cli/azure/acs#create) toocreate ACS кластер, использующий Kubernetes как hello `--orchestrator-type` значение.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-114">Now you're ready toouse [az acs create](/cli/azure/acs#create) toocreate an ACS cluster using Kubernetes as hello `--orchestrator-type` value.</span></span>
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes
```

> [!NOTE]
> <span data-ttu-id="c8f0d-115">Так как Kubernetes не типом orchestrator по умолчанию hello, убедитесь, что вы используете hello `--orchestrator-type kubernetes` переключения.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-115">Because Kubernetes is not hello default orchestrator type, be sure you use hello `--orchestrator-type kubernetes` switch.</span></span>

<span data-ttu-id="c8f0d-116">Вывод Hello при успешном выполнении выглядит примерно следующие toohello.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-116">hello output when successful looks similar toohello following.</span></span>

```json
waiting for AAD role toopropagate.done
{
  "id": "/subscriptions/<guid>/resourceGroups/draft/providers/Microsoft.Resources/deployments/azurecli14904.93snip09",
  "name": "azurecli1496227204.9323909",
  "properties": {
    "correlationId": "<guid>",
    "debugSetting": null,
    "dependencies": [],
    "mode": "Incremental",
    "outputs": null,
    "parameters": {
      "clientSecret": {
        "type": "SecureString"
      }
    },
    "parametersLink": null,
    "providers": [
      {
        "id": null,
        "namespace": "Microsoft.ContainerService",
        "registrationState": null,
        "resourceTypes": [
          {
            "aliases": null,
            "apiVersions": null,
            "locations": [
              "westus"
            ],
            "properties": null,
            "resourceType": "containerServices"
          }
        ]
      }
    ],
    "provisioningState": "Succeeded",
    "template": null,
    "templateLink": null,
    "timestamp": "2017-05-31T10:46:29.434095+00:00"
  },
  "resourceGroup": "draft"
}
```

<span data-ttu-id="c8f0d-117">Теперь, когда имеется кластер hello учетные данные можно импортировать с помощью hello [az kubernetes get-учетные данные acs](/cli/azure/acs/kubernetes#get-credentials) команды.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-117">Now that you have a cluster, you can import hello credentials by using hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="c8f0d-118">Теперь имеется файл локальной конфигурации для кластера, являющийся какие Helm и черновик должны tooget поставленных задач.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-118">Now you have a local configuration file for your cluster, which is what Helm and Draft need tooget their work done.</span></span>

## <a name="install-and-configure-draft"></a><span data-ttu-id="c8f0d-119">Установка и настройка черновика</span><span class="sxs-lookup"><span data-stu-id="c8f0d-119">Install and configure draft</span></span>
<span data-ttu-id="c8f0d-120">инструкции по установке Hello для черновик находятся в hello [репозитория Черновик](https://github.com/Azure/draft/blob/master/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="c8f0d-120">hello installation instructions for Draft are in hello [Draft repository](https://github.com/Azure/draft/blob/master/docs/install.md).</span></span> <span data-ttu-id="c8f0d-121">Они относительно просты, но требуют некоторые конфигурации, так как он зависит от [Helm](https://aka.ms/helm) toocreate и развернуть диаграмму Helm в кластер Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-121">They are relatively simple, but do require some configuration, as it depends on [Helm](https://aka.ms/helm) toocreate and deploy a Helm chart into hello Kubernetes cluster.</span></span>

1. <span data-ttu-id="c8f0d-122">[Скачайте и установите Helm](https://aka.ms/helm#install).</span><span class="sxs-lookup"><span data-stu-id="c8f0d-122">[Download and install Helm](https://aka.ms/helm#install).</span></span>
2. <span data-ttu-id="c8f0d-123">Используйте toosearch Helm для и установите `stable/traefik`и входящих контроллера tooenable входящие запросы для сборок.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-123">Use Helm toosearch for and install `stable/traefik`, and ingress controller tooenable inbound requests for your builds.</span></span>
    ```bash
    $ helm search traefik
    NAME            VERSION DESCRIPTION
    stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

    $ helm install stable/traefik --name ingress
    ```
    <span data-ttu-id="c8f0d-124">Теперь задать Контрольное значение для hello `ingress` контроллера toocapture hello внешнего IP значение при его развертывании.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-124">Now set a watch on hello `ingress` controller toocapture hello external IP value when it is deployed.</span></span> <span data-ttu-id="c8f0d-125">Этот IP-адрес будет hello один [сопоставления домена развертывания tooyour](#wire-up-deployment-domain) в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-125">This IP address will be hello one [mapped tooyour deployment domain](#wire-up-deployment-domain) in hello next section.</span></span>

    ```bash
    kubectl get svc -w
    NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
    kubernetes                    10.0.0.1       <none>          443/TCP                      7h
    ```

    <span data-ttu-id="c8f0d-126">В этом случае hello внешний IP-адрес развертывания домен hello `13.64.108.240`.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-126">In this case, hello external IP for hello deployment domain is `13.64.108.240`.</span></span> <span data-ttu-id="c8f0d-127">Теперь вы можете сопоставить на IP-адрес домена toothat.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-127">Now you can map your domain toothat IP.</span></span>

## <a name="wire-up-deployment-domain"></a><span data-ttu-id="c8f0d-128">Подключение домена развертывания</span><span class="sxs-lookup"><span data-stu-id="c8f0d-128">Wire up deployment domain</span></span>

<span data-ttu-id="c8f0d-129">Черновик создает выпуск для каждого чарта Helm, который он создает, в каждом приложении, над которым вы работаете.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-129">Draft creates a release for each Helm chart it creates -- each application you are working on.</span></span> <span data-ttu-id="c8f0d-130">Каждый из них возвращает сформированное имя, которое используется черновик как _поддомен_ поверх hello корневой _домена развертывания_ , можно управлять.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-130">Each one gets a generated name that is used by draft as a _subdomain_ on top of hello root _deployment domain_ that you control.</span></span> <span data-ttu-id="c8f0d-131">(В этом примере мы используем `squillace.io` как hello развертывания домен.) tooenable такое поведение дочернего домена, необходимо создать запись A для `'*'` записи DNS для домена развертывания, чтобы автоматически созданный каждого дочернего домена является перенаправленное toohello Kubernetes контроллер входящих кластера.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-131">(In this example, we use `squillace.io` as hello deployment domain.) tooenable this subdomain behavior, you must create an A record for `'*'` in your DNS entries for your deployment domain, so that each generated subdomain is routed toohello Kubernetes cluster's ingress controller.</span></span>

<span data-ttu-id="c8f0d-132">Поставщиком домена имеет свои собственные способом tooassign DNS-серверы; слишком[tooAzure nameservers вашего домена DNS делегировать](../../dns/dns-delegate-domain-azure-dns.md), принимают hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="c8f0d-132">Your own domain provider has their own way tooassign DNS servers; too[delegate your domain nameservers tooAzure DNS](../../dns/dns-delegate-domain-azure-dns.md), you take hello following steps:</span></span>

1. <span data-ttu-id="c8f0d-133">Создайте группу ресурсов для зоны.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-133">Create a resource group for your zone.</span></span>
    ```azurecli
    az group create --name squillace.io --location eastus
    {
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io",
      "location": "eastus",
      "managedBy": null,
      "name": "zones",
      "properties": {
        "provisioningState": "Succeeded"
      },
      "tags": null
    }
    ```

2. <span data-ttu-id="c8f0d-134">Создайте зону DNS для домена.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-134">Create a DNS zone for your domain.</span></span>
<span data-ttu-id="c8f0d-135">Используйте hello [создание зоны dns сети az](/cli/azure/network/dns/zone#create) команда tooobtain hello nameservers toodelegate DNS управления tooAzure DNS для домена.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-135">Use hello [az network dns zone create](/cli/azure/network/dns/zone#create) command tooobtain hello nameservers toodelegate DNS control tooAzure DNS for your domain.</span></span>
    ```azurecli
    az network dns zone create --resource-group squillace.io --name squillace.io
    {
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/zones/providers/Microsoft.Network/dnszones/squillace.io",
      "location": "global",
      "maxNumberOfRecordSets": 5000,
      "name": "squillace.io",
      "nameServers": [
        "ns1-09.azure-dns.com.",
        "ns2-09.azure-dns.net.",
        "ns3-09.azure-dns.org.",
        "ns4-09.azure-dns.info."
      ],
      "numberOfRecordSets": 2,
      "resourceGroup": "squillace.io",
      "tags": {},
      "type": "Microsoft.Network/dnszones"
    }
    ```
3. <span data-ttu-id="c8f0d-136">Добавьте hello DNS-серверы, которые заданы поставщика toohello домена для домена развертывания, который позволяет вам toouse Azure DNS toorepoint домена необходимо.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-136">Add hello DNS servers you are given toohello domain provider for your deployment domain, which enables you toouse Azure DNS toorepoint your domain as you want.</span></span>
4. <span data-ttu-id="c8f0d-137">Создайте запись A набор записей для вашего развертывания домена сопоставление toohello `ingress` IP-адрес из предыдущего раздела hello шаг 2.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-137">Create an A record-set entry for your deployment domain mapping toohello `ingress` IP from step 2 of hello previous section.</span></span>
    ```azurecli
    az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*' -g squillace.io -z squillace.io
    ```
<span data-ttu-id="c8f0d-138">выходные данные Hello выглядит примерно так:</span><span class="sxs-lookup"><span data-stu-id="c8f0d-138">hello output looks something like:</span></span>
    ```json
    {
      "arecords": [
        {
          "ipv4Address": "13.64.108.240"
        }
      ],
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io/providers/Microsoft.Network/dnszones/squillace.io/A/*",
      "metadata": null,
      "name": "*",
      "resourceGroup": "squillace.io",
      "ttl": 3600,
      "type": "Microsoft.Network/dnszones/A"
    }
    ```

5. <span data-ttu-id="c8f0d-139">Настройка toouse черновик реестра и создайте дочерние домены для каждой диаграммы Helm созданные им.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-139">Configure Draft toouse your registry and create subdomains for each Helm chart it creates.</span></span> <span data-ttu-id="c8f0d-140">tooconfigure черновик, необходимо:</span><span class="sxs-lookup"><span data-stu-id="c8f0d-140">tooconfigure Draft, you need:</span></span>
  - <span data-ttu-id="c8f0d-141">имя реестра контейнеров Azure (в этом примере — `draft`);</span><span class="sxs-lookup"><span data-stu-id="c8f0d-141">your Azure Container Registry name (in this example, `draft`)</span></span>
  - <span data-ttu-id="c8f0d-142">раздел реестра или пароль, полученный из `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`;</span><span class="sxs-lookup"><span data-stu-id="c8f0d-142">your registry key, or password, from `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.</span></span>
  - <span data-ttu-id="c8f0d-143">Развертывание Hello корневого домена, что вы настроили toomap toohello Kubernetes входящих внешний IP-адрес (здесь `squillace.io`)</span><span class="sxs-lookup"><span data-stu-id="c8f0d-143">hello root deployment domain that you have configured toomap toohello Kubernetes ingress external IP address (here, `squillace.io`)</span></span>

  <span data-ttu-id="c8f0d-144">Вызовите `draft init` и процесса настройки hello запрашивает hello значений, приведенных выше.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-144">Call `draft init` and hello configuration process prompts you for hello values above.</span></span> <span data-ttu-id="c8f0d-145">Hello процесс кажется, что-то hello следующие hello первый раз при запуске.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-145">hello process looks something like hello following hello first time you run it.</span></span>
 ```bash
    $ draft init
    Creating pack ruby...
    Creating pack node...
    Creating pack gradle...
    Creating pack maven...
    Creating pack php...
    Creating pack python...
    Creating pack dotnetcore...
    Creating pack golang...
    $DRAFT_HOME has been configured at /Users/ralphsquillace/.draft.

    In order tooinstall Draft, we need a bit more information...

    1. Enter your Docker registry URL (e.g. docker.io, quay.io, myregistry.azurecr.io): draft.azurecr.io
    2. Enter your username: draft
    3. Enter your password:
    4. Enter your org where Draft will push images [draft]: draft
    5. Enter your top-level domain for ingress (e.g. draft.example.com): squillace.io
    Draft has been installed into your Kubernetes Cluster.
    Happy Sailing!
    ```

<span data-ttu-id="c8f0d-146">Теперь вы готовы toodeploy приложения.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-146">Now you're ready toodeploy an application.</span></span>


## <a name="build-and-deploy-an-application"></a><span data-ttu-id="c8f0d-147">Сборка и развертывание приложения</span><span class="sxs-lookup"><span data-stu-id="c8f0d-147">Build and deploy an application</span></span>

<span data-ttu-id="c8f0d-148">В репозитории черновик hello, [шесть простой пример приложения](https://github.com/Azure/draft/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="c8f0d-148">In hello Draft repo are [six simple example applications](https://github.com/Azure/draft/tree/master/examples).</span></span> <span data-ttu-id="c8f0d-149">Клонировать репозиторий hello и используем hello [примере Python](https://github.com/Azure/draft/tree/master/examples/python).</span><span class="sxs-lookup"><span data-stu-id="c8f0d-149">Clone hello repo and let's use hello [Python example](https://github.com/Azure/draft/tree/master/examples/python).</span></span> <span data-ttu-id="c8f0d-150">Изменения в каталог hello примеры и Python, а тип `draft create` toobuild приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-150">Change into hello examples/Python directory, and type `draft create` toobuild hello application.</span></span> <span data-ttu-id="c8f0d-151">Оно должно иметь вид следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-151">It should look like hello following example.</span></span>
```bash
$ draft create
--> Python app detected
--> Ready toosail
```

<span data-ttu-id="c8f0d-152">Вывод Hello включает файл Dockerfile и Helm диаграммы.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-152">hello output includes a Dockerfile and a Helm chart.</span></span> <span data-ttu-id="c8f0d-153">toobuild и развертывания, просто введите `draft up`.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-153">toobuild and deploy, you just type `draft up`.</span></span> <span data-ttu-id="c8f0d-154">выходные данные Hello слишком большой, но начинается как следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-154">hello output is extensive, but begins like hello following example.</span></span>
```bash
$ draft up
--> Building Dockerfile
Step 1 : FROM python:onbuild
onbuild: Pulling from library/python
10a267c67f42: Pulling fs layer
fb5937da9414: Pulling fs layer
9021b2326a1e: Pulling fs layer
dbed9b09434e: Pulling fs layer
ea8a37f15161: Pulling fs layer
<snip>
```

<span data-ttu-id="c8f0d-155">Когда и успешно заканчивается на что-нибудь подобное toohello следующий пример.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-155">and when successful ends with something similar toohello following example.</span></span>
```bash
ab68189731eb: Pushed
53c0ab0341bee12d01be3d3c192fbd63562af7f1: digest: sha256:bb0450ec37acf67ed461c1512ef21f58a500ff9326ce3ec623ce1e4427df9765 size: 2841
--> Deploying tooKubernetes
--> Status: DEPLOYED
--> Notes:

  http://gangly-bronco.squillace.io tooaccess your application

Watching local files for changes...
```

<span data-ttu-id="c8f0d-156">Все, что указано имя на диаграмме, теперь можно `curl http://gangly-bronco.squillace.io` tooreceive hello ответ, `Hello World!`.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-156">Whatever your chart's name is, you can now `curl http://gangly-bronco.squillace.io` tooreceive hello reply, `Hello World!`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8f0d-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c8f0d-157">Next steps</span></span>

<span data-ttu-id="c8f0d-158">Теперь, когда кластер ACS Kubernetes можно изучить с помощью [реестра контейнера Azure](../../container-registry/container-registry-intro.md) toocreate дополнительные и различных развертывания этого сценария.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-158">Now that you have an ACS Kubernetes cluster, you can investigate using [Azure Container Registry](../../container-registry/container-registry-intro.md) toocreate more and different deployments of this scenario.</span></span> <span data-ttu-id="c8f0d-159">Например, вы можете создать набор записей DNS домена draft._basedomain.toplevel_, с помощью которого можно отключать функции важного поддомена для определенных развертываний ACS.</span><span class="sxs-lookup"><span data-stu-id="c8f0d-159">For example, you can create a draft._basedomain.toplevel_ domain DNS record-set that controls things off of a deeper subdomain for specific ACS deployments.</span></span>






