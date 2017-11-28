---
title: "aaaService участника для кластера Azure Kubernetes | Документы Microsoft"
description: "Сведения о настройке субъекта-службы Azure Active Directory для кластера Kubernetes и управлении им в Службе контейнеров Azure."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 7a01624c5ac3fa717dbcbd570e05ceb4d917c53a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a><span data-ttu-id="70689-103">Настройка субъекта-службы Azure AD для кластера Kubernetes в Службе контейнеров</span><span class="sxs-lookup"><span data-stu-id="70689-103">Set up an Azure AD service principal for a Kubernetes cluster in Container Service</span></span>


<span data-ttu-id="70689-104">В контейнере службы Azure, требуется кластер Kubernetes [участника-службы Azure Active Directory](../../active-directory/develop/active-directory-application-objects.md) toointeract с API-интерфейсов Azure.</span><span class="sxs-lookup"><span data-stu-id="70689-104">In Azure Container Service, a Kubernetes cluster requires an [Azure Active Directory service principal](../../active-directory/develop/active-directory-application-objects.md) toointeract with Azure APIs.</span></span> <span data-ttu-id="70689-105">Hello участника-службы требуется toodynamically управления ресурсами, такими как [определяемых пользователем маршрутов](../../virtual-network/virtual-networks-udr-overview.md) и hello [подсистемы балансировки нагрузки уровня 4 Azure](../../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="70689-105">hello service principal is needed toodynamically manage resources such as [user-defined routes](../../virtual-network/virtual-networks-udr-overview.md) and hello [Layer 4 Azure Load Balancer](../../load-balancer/load-balancer-overview.md).</span></span> 


<span data-ttu-id="70689-106">В этой статье показано tooset различные параметры службы для кластера Kubernetes участника.</span><span class="sxs-lookup"><span data-stu-id="70689-106">This article shows different options tooset up a service principal for your Kubernetes cluster.</span></span> <span data-ttu-id="70689-107">Например, если необходимо установить и настроить hello [Azure CLI 2.0](/cli/azure/install-az-cli2), можно запустить hello [ `az acs create` ](/cli/azure/acs#create) toocreate команда hello в hello субъектом-службой кластера и hello Kubernetes то же время.</span><span class="sxs-lookup"><span data-stu-id="70689-107">For example, if you installed and set up hello [Azure CLI 2.0](/cli/azure/install-az-cli2), you can run hello [`az acs create`](/cli/azure/acs#create) command toocreate hello Kubernetes cluster and hello service principal at hello same time.</span></span>


## <a name="requirements-for-hello-service-principal"></a><span data-ttu-id="70689-108">Требования к субъекту-службе hello</span><span class="sxs-lookup"><span data-stu-id="70689-108">Requirements for hello service principal</span></span>

<span data-ttu-id="70689-109">Можно использовать существующий субъект службы Azure AD, соответствует hello следующие требования, или создать новый.</span><span class="sxs-lookup"><span data-stu-id="70689-109">You can use an existing Azure AD service principal that meets hello following requirements, or create a new one.</span></span>

* <span data-ttu-id="70689-110">**Область**: hello группы ресурсов в подписке hello используемого кластера Kubernetes toodeploy hello, или (менее restrictively) hello подписки toodeploy hello кластера.</span><span class="sxs-lookup"><span data-stu-id="70689-110">**Scope**: hello resource group in hello subscription used toodeploy hello Kubernetes cluster, or (less restrictively) hello subscription used toodeploy hello cluster.</span></span>

* <span data-ttu-id="70689-111">**Роль** — **Участник**.</span><span class="sxs-lookup"><span data-stu-id="70689-111">**Role**: **Contributor**</span></span>

* <span data-ttu-id="70689-112">**Секрет клиента** — должен быть паролем.</span><span class="sxs-lookup"><span data-stu-id="70689-112">**Client secret**: must be a password.</span></span> <span data-ttu-id="70689-113">Сейчас субъект-службу нельзя использовать для проверки подлинности сертификата.</span><span class="sxs-lookup"><span data-stu-id="70689-113">Currently, you can't use a service principal set up for certificate authentication.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="70689-114">toocreate участника-службы, необходимо иметь разрешения tooregister приложение с клиентом Azure AD и роль tooa приложения hello tooassign в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="70689-114">toocreate a service principal, you must have permissions tooregister an application with your Azure AD tenant, and tooassign hello application tooa role in your subscription.</span></span> <span data-ttu-id="70689-115">toosee при наличии разрешений требуется hello [возврата hello портала](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="70689-115">toosee if you have hello required permissions, [check in hello Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions).</span></span> 
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a><span data-ttu-id="70689-116">Вариант 1. Создание субъекта-службы в Azure AD</span><span class="sxs-lookup"><span data-stu-id="70689-116">Option 1: Create a service principal in Azure AD</span></span>

<span data-ttu-id="70689-117">Если перед развертыванием кластера Kubernetes toocreate участника-службы Azure AD, Azure предоставляет несколько методов.</span><span class="sxs-lookup"><span data-stu-id="70689-117">If you want toocreate an Azure AD service principal before you deploy your Kubernetes cluster, Azure provides several methods.</span></span> 

<span data-ttu-id="70689-118">Следующие примеры команд Hello показывается, как toodo с hello [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="70689-118">hello following example commands show you how toodo this with hello [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md).</span></span> <span data-ttu-id="70689-119">Кроме того, можно создать участника службы с помощью [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), hello [портала](../../azure-resource-manager/resource-group-create-service-principal-portal.md), или других методов.</span><span class="sxs-lookup"><span data-stu-id="70689-119">You can alternatively create a service principal using [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), hello [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), or other methods.</span></span>

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create -n "myResourceGroupName" -l "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID/resourceGroups/myResourceGroupName"
```

<span data-ttu-id="70689-120">Выходные данные выглядят примерно следующее toohello (показанных здесь исправленную):</span><span class="sxs-lookup"><span data-stu-id="70689-120">Output is similar toohello following (shown here redacted):</span></span>

![Создание субъекта-службы](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

<span data-ttu-id="70689-122">Выделены hello **идентификатор клиента** (`appId`) и hello **секрет клиента** (`password`), используемый в качестве основного параметры службы для развертывания кластера.</span><span class="sxs-lookup"><span data-stu-id="70689-122">Highlighted are hello **client ID** (`appId`) and hello **client secret** (`password`) that you use as service principal parameters for cluster deployment.</span></span>


### <a name="specify-service-principal-when-creating-hello-kubernetes-cluster"></a><span data-ttu-id="70689-123">Укажите участника-службы, при создании кластера Kubernetes hello</span><span class="sxs-lookup"><span data-stu-id="70689-123">Specify service principal when creating hello Kubernetes cluster</span></span>

<span data-ttu-id="70689-124">Укажите hello **идентификатор клиента** (также называется hello `appId`, для идентификатора приложения) и **секрет клиента** (`password`) существующей службы субъекта в качестве параметров при создании hello Kubernetes кластера.</span><span class="sxs-lookup"><span data-stu-id="70689-124">Provide hello **client ID** (also called hello `appId`, for Application ID) and **client secret** (`password`) of an existing service principal as parameters when you create hello Kubernetes cluster.</span></span> <span data-ttu-id="70689-125">Убедитесь, что субъект-служба hello требованиям hello в hello, начинающиеся в этой статье.</span><span class="sxs-lookup"><span data-stu-id="70689-125">Make sure hello service principal meets hello requirements at hello beginning this article.</span></span>

<span data-ttu-id="70689-126">Можно указать эти параметры при развертывании кластера Kubernetes hello, с помощью hello [Azure интерфейс командной строки (CLI) 2.0](container-service-kubernetes-walkthrough.md), [портал Azure](../dcos-swarm/container-service-deployment.md), или других методов.</span><span class="sxs-lookup"><span data-stu-id="70689-126">You can specify these parameters when deploying hello Kubernetes cluster using hello [Azure Command-Line Interface (CLI) 2.0](container-service-kubernetes-walkthrough.md), [Azure portal](../dcos-swarm/container-service-deployment.md), or other methods.</span></span>

>[!TIP] 
><span data-ttu-id="70689-127">При указании hello **идентификатор клиента**, быть убедиться, что hello toouse `appId`, не hello `ObjectId`, hello субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="70689-127">When specifying hello **client ID**, be sure toouse hello `appId`, not hello `ObjectId`, of hello service principal.</span></span>
>

<span data-ttu-id="70689-128">Hello примере показан один из способов toopass параметров hello hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="70689-128">hello following example shows one way toopass hello parameters with hello Azure CLI 2.0.</span></span> <span data-ttu-id="70689-129">В этом примере используется hello [Kubernetes шаблоном краткого руководства](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span><span class="sxs-lookup"><span data-stu-id="70689-129">This example uses hello [Kubernetes quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).</span></span>

1. <span data-ttu-id="70689-130">[Загрузить](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) файл параметров шаблона hello `azuredeploy.parameters.json` из GitHub.</span><span class="sxs-lookup"><span data-stu-id="70689-130">[Download](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) hello template parameters file `azuredeploy.parameters.json` from GitHub.</span></span>

2. <span data-ttu-id="70689-131">Участник, службы hello toospecify введите значения для `servicePrincipalClientId` и `servicePrincipalClientSecret` в файле hello.</span><span class="sxs-lookup"><span data-stu-id="70689-131">toospecify hello service principal, enter values for `servicePrincipalClientId` and `servicePrincipalClientSecret` in hello file.</span></span> <span data-ttu-id="70689-132">(Необходимо также tooprovide собственные значения для `dnsNamePrefix` и `sshRSAPublicKey`.</span><span class="sxs-lookup"><span data-stu-id="70689-132">(You also need tooprovide your own values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="70689-133">последний Hello — кластер hello tooaccess открытого ключа SSH, hello.) Сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="70689-133">hello latter is hello SSH public key tooaccess hello cluster.) Save hello file.</span></span>

    ![Передача параметров субъекта-службы](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. <span data-ttu-id="70689-135">Выполнения hello следующую команду, с помощью `--parameters` tooset hello путь toohello azuredeploy.parameters.json файл.</span><span class="sxs-lookup"><span data-stu-id="70689-135">Run hello following command, using `--parameters` tooset hello path toohello azuredeploy.parameters.json file.</span></span> <span data-ttu-id="70689-136">Эта команда выполняет развертывание кластера hello в группе ресурсов, вы создаете вызываемой `myResourceGroup` в hello Запад США.</span><span class="sxs-lookup"><span data-stu-id="70689-136">This command deploys hello cluster in a resource group you create called `myResourceGroup` in hello West US region.</span></span>

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus" 
    
    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-hello-cluster-with-az-acs-create"></a><span data-ttu-id="70689-137">Вариант 2: Создание субъекта-службы при создании кластера hello с`az acs create`</span><span class="sxs-lookup"><span data-stu-id="70689-137">Option 2: Generate a service principal when creating hello cluster with `az acs create`</span></span>

<span data-ttu-id="70689-138">При запуске hello [ `az acs create` ](/cli/azure/acs#create) toocreate команда Здравствуйте Kubernetes кластера, у вас есть параметр toogenerate hello участника службы автоматически.</span><span class="sxs-lookup"><span data-stu-id="70689-138">If you run hello [`az acs create`](/cli/azure/acs#create) command toocreate hello Kubernetes cluster, you have hello option toogenerate a service principal automatically.</span></span>

<span data-ttu-id="70689-139">Как и в случае с другими вариантами создания кластера Kubernetes, выполняя команду `az acs create`, вы можете указать параметры для существующего субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="70689-139">As with other Kubernetes cluster creation options, you can specify parameters for an existing service principal when you run `az acs create`.</span></span> <span data-ttu-id="70689-140">Однако при пропуске этих параметров hello Azure CLI создает одно автоматически для использования со службой контейнера.</span><span class="sxs-lookup"><span data-stu-id="70689-140">However, when you omit these parameters, hello Azure CLI creates one automatically for use with Container Service.</span></span> <span data-ttu-id="70689-141">Это происходит прозрачно во время развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="70689-141">This takes place transparently during hello deployment.</span></span> 

<span data-ttu-id="70689-142">Hello следующая команда создает кластер Kubernetes и создает ключи SSH и учетных данных участника службы:</span><span class="sxs-lookup"><span data-stu-id="70689-142">hello following command creates a Kubernetes cluster and generates both SSH keys and service principal credentials:</span></span>

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> <span data-ttu-id="70689-143">Если ваша учетная запись не имеет hello Azure AD и toocreate подписки разрешения участника службы, команда hello также создает сообщение об ошибке`Insufficient privileges toocomplete hello operation.`</span><span class="sxs-lookup"><span data-stu-id="70689-143">If your account doesn't have hello Azure AD and subscription permissions toocreate a service principal, hello command generates an error similar too`Insufficient privileges toocomplete hello operation.`</span></span>
> 

## <a name="additional-considerations"></a><span data-ttu-id="70689-144">Дополнительные замечания</span><span class="sxs-lookup"><span data-stu-id="70689-144">Additional considerations</span></span>

* <span data-ttu-id="70689-145">Если у вас нет разрешения toocreate участника службы в подписке, то может потребоваться tooask в Azure AD или tooassign администратора подписки hello необходимые разрешения или запрашивать toouse участника службы с помощью контейнера службы Azure.</span><span class="sxs-lookup"><span data-stu-id="70689-145">If you don't have permissions toocreate a service principal in your subscription, you might need tooask your Azure AD or subscription administrator tooassign hello necessary permissions, or ask them for a service principal toouse with Azure Container Service.</span></span> 

* <span data-ttu-id="70689-146">Hello субъекта-службы для Kubernetes является частью конфигурации кластера hello.</span><span class="sxs-lookup"><span data-stu-id="70689-146">hello service principal for Kubernetes is a part of hello cluster configuration.</span></span> <span data-ttu-id="70689-147">Тем не менее не следует использовать toodeploy hello hello удостоверение кластера.</span><span class="sxs-lookup"><span data-stu-id="70689-147">However, don't use hello identity toodeploy hello cluster.</span></span>

* <span data-ttu-id="70689-148">Все субъекты-службы связаны с определенными приложениями Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70689-148">Every service principal is associated with an Azure AD application.</span></span> <span data-ttu-id="70689-149">Hello участника-службы для кластера Kubernetes могут быть связаны с любой допустимый Azure AD имя приложения (например: `https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="70689-149">hello service principal for a Kubernetes cluster can be associated with any valid Azure AD application name (for example: `https://www.contoso.org/example`).</span></span> <span data-ttu-id="70689-150">Hello URL-адрес приложения hello не toobe реальных конечной точки.</span><span class="sxs-lookup"><span data-stu-id="70689-150">hello URL for hello application doesn't have toobe a real endpoint.</span></span>

* <span data-ttu-id="70689-151">При указании участника-службы hello **идентификатор клиента**, можно использовать значение hello hello `appId` (как показано в этой статье) или hello соответствующего участника службы `name` (например,`https://www.contoso.org/example`).</span><span class="sxs-lookup"><span data-stu-id="70689-151">When specifying hello service principal **Client ID**, you can use hello value of hello `appId` (as shown in this article) or hello corresponding service principal `name` (for example,`https://www.contoso.org/example`).</span></span>

* <span data-ttu-id="70689-152">Образец hello, и агент виртуальных машин в кластере Kubernetes hello учетных данных участника службы hello хранятся в /etc/kubernetes/azure.json файл hello.</span><span class="sxs-lookup"><span data-stu-id="70689-152">On hello master and agent VMs in hello Kubernetes cluster, hello service principal credentials are stored in hello file /etc/kubernetes/azure.json.</span></span>

* <span data-ttu-id="70689-153">При использовании hello `az acs create` участника-службы hello toogenerate автоматически см. в записи учетных данных участника службы hello toohello ~/.azure/acsServicePrincipal.json файл на компьютере hello используется команда toorun hello.</span><span class="sxs-lookup"><span data-stu-id="70689-153">When you use hello `az acs create` command toogenerate hello service principal automatically, hello service principal credentials are written toohello file ~/.azure/acsServicePrincipal.json on hello machine used toorun hello command.</span></span> 

* <span data-ttu-id="70689-154">При использовании hello `az acs create` автоматически команды участника-службы toogenerate hello, hello субъект-служба также позволяет проверять подлинность с [контейнер Azure реестра](../../container-registry/container-registry-intro.md) созданные hello же подписки.</span><span class="sxs-lookup"><span data-stu-id="70689-154">When you use hello `az acs create` command toogenerate hello service principal automatically, hello service principal can also authenticate with an [Azure container registry](../../container-registry/container-registry-intro.md) created in hello same subscription.</span></span>




## <a name="next-steps"></a><span data-ttu-id="70689-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="70689-155">Next steps</span></span>

* <span data-ttu-id="70689-156">Узнайте, как [начать работу с Kubernetes](container-service-kubernetes-walkthrough.md) в кластере службы контейнеров.</span><span class="sxs-lookup"><span data-stu-id="70689-156">[Get started with Kubernetes](container-service-kubernetes-walkthrough.md) in your container service cluster.</span></span>

* <span data-ttu-id="70689-157">tootroubleshoot hello субъекта-службы для Kubernetes, в разделе hello [документация по ядру СУБД ACS](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="70689-157">tootroubleshoot hello service principal for Kubernetes, see hello [ACS Engine documentation](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).</span></span>


