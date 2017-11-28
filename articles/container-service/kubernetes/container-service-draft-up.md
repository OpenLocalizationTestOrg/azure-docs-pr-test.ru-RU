---
title: "Использование черновика со Службой контейнеров Azure и реестром контейнеров Azure | Документация Майкрософт"
description: "Создайте кластер ACS Kubernetes и реестр контейнеров Azure, чтобы создать свое первое приложение в Azure с помощью черновика."
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
ms.openlocfilehash: e7e3ea461145571753a1a6d768b52118dcbfb507
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-to-build-and-deploy-an-application-to-kubernetes"></a><span data-ttu-id="ed854-104">Использование черновика со Службой контейнеров Azure и реестром контейнеров Azure для создания и развертывания приложения в Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ed854-104">Use Draft with Azure Container Service and Azure Container Registry to build and deploy an application to Kubernetes</span></span>

<span data-ttu-id="ed854-105">[Черновик](https://aka.ms/draft) — новое средство с открытым исходным кодом, которое упрощает разработку приложений на основе контейнера и их развертывание в кластерах Kubernetes. Чтобы использовать черновик, особые знания Docker и Kubernetes или их установка не требуются.</span><span class="sxs-lookup"><span data-stu-id="ed854-105">[Draft](https://aka.ms/draft) is a new open-source tool that makes it easy to develop container-based applications and deploy them to Kubernetes clusters without knowing much about Docker and Kubernetes -- or even installing them.</span></span> <span data-ttu-id="ed854-106">Использование таких средств, как черновик, позволит вам и вашей команде сосредоточиться на создании приложения с помощью Kubernetes, не вникая в инфраструктуру.</span><span class="sxs-lookup"><span data-stu-id="ed854-106">Using tools like Draft let you and your teams focus on building the application with Kubernetes, not paying as much attention to infrastructure.</span></span>

<span data-ttu-id="ed854-107">Вы можете использовать черновик с любым реестром образов Docker и любым кластером Kubernetes, а также использовать его локально.</span><span class="sxs-lookup"><span data-stu-id="ed854-107">You can use Draft with any Docker image registry and any Kubernetes cluster, including locally.</span></span> <span data-ttu-id="ed854-108">В рамках этого руководства вы узнаете, как использовать службу ACS с Kubernetes, запись ACR и Azure DNS, чтобы создать динамичный конвейер разработки CI/CD с помощью черновика.</span><span class="sxs-lookup"><span data-stu-id="ed854-108">This tutorial shows how to use ACS with Kubernetes, ACR, and Azure DNS to create a live CI/CD developer pipeline using Draft.</span></span>


## <a name="create-an-azure-container-registry"></a><span data-ttu-id="ed854-109">Создание реестра контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="ed854-109">Create an Azure Container Registry</span></span>
<span data-ttu-id="ed854-110">Вы можете легко [создать реестр контейнеров Azure](../../container-registry/container-registry-get-started-azure-cli.md). Для этого вам нужно выполнить следующее:</span><span class="sxs-lookup"><span data-stu-id="ed854-110">You can easily [create a new Azure Container Registry](../../container-registry/container-registry-get-started-azure-cli.md), but the steps are as follows:</span></span>

1. <span data-ttu-id="ed854-111">Создайте группу ресурсов Azure, чтобы управлять реестром ACR и кластером Kubernetes в ACS.</span><span class="sxs-lookup"><span data-stu-id="ed854-111">Create a Azure resource group to manage your ACR registry and the Kubernetes cluster in ACS.</span></span>
      ```azurecli
      az group create --name draft --location eastus
      ```

2. <span data-ttu-id="ed854-112">Создайте реестр образов ACR с помощью команды [az acr create](/cli/azure/acr#create).</span><span class="sxs-lookup"><span data-stu-id="ed854-112">Create an ACR image registry using [az acr create](/cli/azure/acr#create)</span></span>
      ```azurecli
      az acr create -g draft -n draftacs --sku Basic --admin-enabled true -l eastus
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a><span data-ttu-id="ed854-113">Создание службы контейнеров Azure с помощью Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ed854-113">Create an Azure Container Service with Kubernetes</span></span>

<span data-ttu-id="ed854-114">Теперь вы готовы использовать команду [az acs create](/cli/azure/acs#create), чтобы создать кластер ACS, используя Kubernetes в качестве значения `--orchestrator-type`.</span><span class="sxs-lookup"><span data-stu-id="ed854-114">Now you're ready to use [az acs create](/cli/azure/acs#create) to create an ACS cluster using Kubernetes as the `--orchestrator-type` value.</span></span>
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes
```

> [!NOTE]
> <span data-ttu-id="ed854-115">Так как Kubernetes не является типом оркестратора по умолчанию, вам необходимо использовать переключатель `--orchestrator-type kubernetes`.</span><span class="sxs-lookup"><span data-stu-id="ed854-115">Because Kubernetes is not the default orchestrator type, be sure you use the `--orchestrator-type kubernetes` switch.</span></span>

<span data-ttu-id="ed854-116">В случае успешного выполнения процедуры результат будет выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="ed854-116">The output when successful looks similar to the following.</span></span>

```json
waiting for AAD role to propagate.done
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

<span data-ttu-id="ed854-117">Теперь, когда у вас есть кластер, вы можете импортировать учетные данные с помощью команды [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials).</span><span class="sxs-lookup"><span data-stu-id="ed854-117">Now that you have a cluster, you can import the credentials by using the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="ed854-118">Теперь у вас есть локальный файл конфигурации для кластера, который нужен Helm и черновику для выполнения работы.</span><span class="sxs-lookup"><span data-stu-id="ed854-118">Now you have a local configuration file for your cluster, which is what Helm and Draft need to get their work done.</span></span>

## <a name="install-and-configure-draft"></a><span data-ttu-id="ed854-119">Установка и настройка черновика</span><span class="sxs-lookup"><span data-stu-id="ed854-119">Install and configure draft</span></span>
<span data-ttu-id="ed854-120">Инструкции по установке черновика находятся в [репозитории черновика](https://github.com/Azure/draft/blob/master/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="ed854-120">The installation instructions for Draft are in the [Draft repository](https://github.com/Azure/draft/blob/master/docs/install.md).</span></span> <span data-ttu-id="ed854-121">Они относительно просты, но требуют определенной настройки, так как от [Helm](https://aka.ms/helm) зависит создание и развертывание чарта Helm в кластере Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="ed854-121">They are relatively simple, but do require some configuration, as it depends on [Helm](https://aka.ms/helm) to create and deploy a Helm chart into the Kubernetes cluster.</span></span>

1. <span data-ttu-id="ed854-122">[Скачайте и установите Helm](https://aka.ms/helm#install).</span><span class="sxs-lookup"><span data-stu-id="ed854-122">[Download and install Helm](https://aka.ms/helm#install).</span></span>
2. <span data-ttu-id="ed854-123">Используйте Helm для поиска и установки `stable/traefik` и входящий контроллер, чтобы разрешить входящие запросы для сборок.</span><span class="sxs-lookup"><span data-stu-id="ed854-123">Use Helm to search for and install `stable/traefik`, and ingress controller to enable inbound requests for your builds.</span></span>
    ```bash
    $ helm search traefik
    NAME            VERSION DESCRIPTION
    stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

    $ helm install stable/traefik --name ingress
    ```
    <span data-ttu-id="ed854-124">Теперь настройте контрольное значение для контроллера `ingress`, чтобы сохранить значение внешнего IP-адреса после развертывания.</span><span class="sxs-lookup"><span data-stu-id="ed854-124">Now set a watch on the `ingress` controller to capture the external IP value when it is deployed.</span></span> <span data-ttu-id="ed854-125">Этот IP-адрес будет [сопоставлен с доменом развертывания](#wire-up-deployment-domain) в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="ed854-125">This IP address will be the one [mapped to your deployment domain](#wire-up-deployment-domain) in the next section.</span></span>

    ```bash
    kubectl get svc -w
    NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
    kubernetes                    10.0.0.1       <none>          443/TCP                      7h
    ```

    <span data-ttu-id="ed854-126">В этом случае внешний IP-адрес для домена развертывания — `13.64.108.240`.</span><span class="sxs-lookup"><span data-stu-id="ed854-126">In this case, the external IP for the deployment domain is `13.64.108.240`.</span></span> <span data-ttu-id="ed854-127">Теперь вы можете сопоставить свой домен с этим IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="ed854-127">Now you can map your domain to that IP.</span></span>

## <a name="wire-up-deployment-domain"></a><span data-ttu-id="ed854-128">Подключение домена развертывания</span><span class="sxs-lookup"><span data-stu-id="ed854-128">Wire up deployment domain</span></span>

<span data-ttu-id="ed854-129">Черновик создает выпуск для каждого чарта Helm, который он создает, в каждом приложении, над которым вы работаете.</span><span class="sxs-lookup"><span data-stu-id="ed854-129">Draft creates a release for each Helm chart it creates -- each application you are working on.</span></span> <span data-ttu-id="ed854-130">Каждый выпуск получает автоматически сформированное имя, которое используется черновиком в качестве _поддомена_ поверх _корневого домена развертывания_, которым вы управляете.</span><span class="sxs-lookup"><span data-stu-id="ed854-130">Each one gets a generated name that is used by draft as a _subdomain_ on top of the root _deployment domain_ that you control.</span></span> <span data-ttu-id="ed854-131">(В этом примере в качестве домена развертывания мы используем `squillace.io`.) Чтобы включить этот режим поддомена, вы должны создать запись А для `'*'` в записях DNS для домена развертывания, чтобы каждый автоматически сформированный поддомен направлялся во входящий контроллер кластера Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="ed854-131">(In this example, we use `squillace.io` as the deployment domain.) To enable this subdomain behavior, you must create an A record for `'*'` in your DNS entries for your deployment domain, so that each generated subdomain is routed to the Kubernetes cluster's ingress controller.</span></span>

<span data-ttu-id="ed854-132">Поставщики домена самостоятельно назначают DNS-серверы. Чтобы [делегировать назначение имен серверов домена службе Azure DNS](../../dns/dns-delegate-domain-azure-dns.md), сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="ed854-132">Your own domain provider has their own way to assign DNS servers; to [delegate your domain nameservers to Azure DNS](../../dns/dns-delegate-domain-azure-dns.md), you take the following steps:</span></span>

1. <span data-ttu-id="ed854-133">Создайте группу ресурсов для зоны.</span><span class="sxs-lookup"><span data-stu-id="ed854-133">Create a resource group for your zone.</span></span>
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

2. <span data-ttu-id="ed854-134">Создайте зону DNS для домена.</span><span class="sxs-lookup"><span data-stu-id="ed854-134">Create a DNS zone for your domain.</span></span>
<span data-ttu-id="ed854-135">Используйте команду [az network dns zone create](/cli/azure/network/dns/zone#create), чтобы получить имена серверов для делегирования элемента управления DNS службе Azure DNS для домена.</span><span class="sxs-lookup"><span data-stu-id="ed854-135">Use the [az network dns zone create](/cli/azure/network/dns/zone#create) command to obtain the nameservers to delegate DNS control to Azure DNS for your domain.</span></span>
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
3. <span data-ttu-id="ed854-136">Добавьте полученные DNS-серверы поставщику домена для домена развертывания, чтобы использовать Azure DNS для повторного указания домена.</span><span class="sxs-lookup"><span data-stu-id="ed854-136">Add the DNS servers you are given to the domain provider for your deployment domain, which enables you to use Azure DNS to repoint your domain as you want.</span></span>
4. <span data-ttu-id="ed854-137">Создайте запись набора записей A для домена развертывания, сопоставленного с IP-адресом `ingress` на шаге 2 в разделе выше.</span><span class="sxs-lookup"><span data-stu-id="ed854-137">Create an A record-set entry for your deployment domain mapping to the `ingress` IP from step 2 of the previous section.</span></span>
    ```azurecli
    az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*' -g squillace.io -z squillace.io
    ```
<span data-ttu-id="ed854-138">Результат будет выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="ed854-138">The output looks something like:</span></span>
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

5. <span data-ttu-id="ed854-139">Настройте черновик, чтобы использовать реестр и создать поддомены для каждого чарта Helm, который он создает.</span><span class="sxs-lookup"><span data-stu-id="ed854-139">Configure Draft to use your registry and create subdomains for each Helm chart it creates.</span></span> <span data-ttu-id="ed854-140">Чтобы настроить черновик, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="ed854-140">To configure Draft, you need:</span></span>
  - <span data-ttu-id="ed854-141">имя реестра контейнеров Azure (в этом примере — `draft`);</span><span class="sxs-lookup"><span data-stu-id="ed854-141">your Azure Container Registry name (in this example, `draft`)</span></span>
  - <span data-ttu-id="ed854-142">раздел реестра или пароль, полученный из `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`;</span><span class="sxs-lookup"><span data-stu-id="ed854-142">your registry key, or password, from `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.</span></span>
  - <span data-ttu-id="ed854-143">корневой домен развертывания, который вы настроили для сопоставления с входящим внешним IP-адресом Kubernetes (в этом примере — `squillace.io`).</span><span class="sxs-lookup"><span data-stu-id="ed854-143">the root deployment domain that you have configured to map to the Kubernetes ingress external IP address (here, `squillace.io`)</span></span>

  <span data-ttu-id="ed854-144">Вызовите `draft init`, и процесс настройки запросит значения, приведенные выше.</span><span class="sxs-lookup"><span data-stu-id="ed854-144">Call `draft init` and the configuration process prompts you for the values above.</span></span> <span data-ttu-id="ed854-145">При первом запуске процесс будет выглядеть приблизительно так:</span><span class="sxs-lookup"><span data-stu-id="ed854-145">The process looks something like the following the first time you run it.</span></span>
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

    In order to install Draft, we need a bit more information...

    1. Enter your Docker registry URL (e.g. docker.io, quay.io, myregistry.azurecr.io): draft.azurecr.io
    2. Enter your username: draft
    3. Enter your password:
    4. Enter your org where Draft will push images [draft]: draft
    5. Enter your top-level domain for ingress (e.g. draft.example.com): squillace.io
    Draft has been installed into your Kubernetes Cluster.
    Happy Sailing!
    ```

<span data-ttu-id="ed854-146">Теперь все готово для развертывания приложения.</span><span class="sxs-lookup"><span data-stu-id="ed854-146">Now you're ready to deploy an application.</span></span>


## <a name="build-and-deploy-an-application"></a><span data-ttu-id="ed854-147">Сборка и развертывание приложения</span><span class="sxs-lookup"><span data-stu-id="ed854-147">Build and deploy an application</span></span>

<span data-ttu-id="ed854-148">В репозитории черновика находятся [шесть простых примеров приложений](https://github.com/Azure/draft/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="ed854-148">In the Draft repo are [six simple example applications](https://github.com/Azure/draft/tree/master/examples).</span></span> <span data-ttu-id="ed854-149">Клонируйте репозиторий и используйте [пример на языке Python](https://github.com/Azure/draft/tree/master/examples/python).</span><span class="sxs-lookup"><span data-stu-id="ed854-149">Clone the repo and let's use the [Python example](https://github.com/Azure/draft/tree/master/examples/python).</span></span> <span data-ttu-id="ed854-150">Измените каталог examples/Python и введите `draft create`, чтобы создать приложение.</span><span class="sxs-lookup"><span data-stu-id="ed854-150">Change into the examples/Python directory, and type `draft create` to build the application.</span></span> <span data-ttu-id="ed854-151">Результат должен выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="ed854-151">It should look like the following example.</span></span>
```bash
$ draft create
--> Python app detected
--> Ready to sail
```

<span data-ttu-id="ed854-152">Выходные данные будут содержать файл Dockerfile и чарт Helm.</span><span class="sxs-lookup"><span data-stu-id="ed854-152">The output includes a Dockerfile and a Helm chart.</span></span> <span data-ttu-id="ed854-153">Чтобы выполнить сборку и развертывание, введите `draft up`.</span><span class="sxs-lookup"><span data-stu-id="ed854-153">To build and deploy, you just type `draft up`.</span></span> <span data-ttu-id="ed854-154">Результат будет обширным, но начальные выходные данные будут выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="ed854-154">The output is extensive, but begins like the following example.</span></span>
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

<span data-ttu-id="ed854-155">Конечные выходные данные должны выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="ed854-155">and when successful ends with something similar to the following example.</span></span>
```bash
ab68189731eb: Pushed
53c0ab0341bee12d01be3d3c192fbd63562af7f1: digest: sha256:bb0450ec37acf67ed461c1512ef21f58a500ff9326ce3ec623ce1e4427df9765 size: 2841
--> Deploying to Kubernetes
--> Status: DEPLOYED
--> Notes:

  http://gangly-bronco.squillace.io to access your application

Watching local files for changes...
```

<span data-ttu-id="ed854-156">С любым именем чарта вы можете использовать `curl http://gangly-bronco.squillace.io`, чтобы получить ответ `Hello World!`.</span><span class="sxs-lookup"><span data-stu-id="ed854-156">Whatever your chart's name is, you can now `curl http://gangly-bronco.squillace.io` to receive the reply, `Hello World!`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed854-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ed854-157">Next steps</span></span>

<span data-ttu-id="ed854-158">Теперь, когда у вас есть кластер ACS Kubernetes, вы можете использовать [реестр контейнеров Azure](../../container-registry/container-registry-intro.md), чтобы создать больше различных развертываний этого сценария.</span><span class="sxs-lookup"><span data-stu-id="ed854-158">Now that you have an ACS Kubernetes cluster, you can investigate using [Azure Container Registry](../../container-registry/container-registry-intro.md) to create more and different deployments of this scenario.</span></span> <span data-ttu-id="ed854-159">Например, вы можете создать набор записей DNS домена draft._basedomain.toplevel_, с помощью которого можно отключать функции важного поддомена для определенных развертываний ACS.</span><span class="sxs-lookup"><span data-stu-id="ed854-159">For example, you can create a draft._basedomain.toplevel_ domain DNS record-set that controls things off of a deeper subdomain for specific ACS deployments.</span></span>






