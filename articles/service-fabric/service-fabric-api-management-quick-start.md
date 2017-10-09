---
title: "aaaAzure Service Fabric с помощью быстрого запуска управления API | Документы Microsoft"
description: "В этом руководстве показано, как tooquickly Приступая к работе с API управления Azure и фабрикой служб."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: f76f3f39a92f89892d6a02ecaab1ec3d343fe2a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-quick-start"></a><span data-ttu-id="e98b2-103">Краткое руководство по Service Fabric со службой управления API Azure</span><span class="sxs-lookup"><span data-stu-id="e98b2-103">Service Fabric with Azure API Management Quick Start</span></span>

<span data-ttu-id="e98b2-104">В этом руководстве рассказывается, как tooset управления API Azure в Service Fabric и настройка служб трафика tooback окончания первого API операции toosend в Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e98b2-104">This guide shows you how tooset up Azure API Management with Service Fabric and configure your first API operation toosend traffic tooback-end services in Service Fabric.</span></span> <span data-ttu-id="e98b2-105">toolearn Дополнительные сведения о сценариях управления API Azure в Service Fabric. в разделе hello [Обзор](service-fabric-api-management-overview.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="e98b2-105">toolearn more about Azure API Management scenarios with Service Fabric, see hello [overview](service-fabric-api-management-overview.md) article.</span></span> 

## <a name="deploy-api-management-and-service-fabric-tooazure"></a><span data-ttu-id="e98b2-106">Развертывание tooAzure управления API и Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e98b2-106">Deploy API Management and Service Fabric tooAzure</span></span>

<span data-ttu-id="e98b2-107">Hello первым шагом является toodeploy управления API и tooAzure кластера Service Fabric в общей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e98b2-107">hello first step is toodeploy API Management and a Service Fabric cluster tooAzure in a shared Virtual Network.</span></span> <span data-ttu-id="e98b2-108">Это позволяет toocommunicate API управления непосредственно в Service Fabric, можно выполнить обнаружение службы, разрешения раздела службы и перенаправлял трафик, напрямую tooany серверной службы в Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e98b2-108">This allows API Management toocommunicate directly with Service Fabric so it can perform service discovery, service partition resolution, and forward traffic directly tooany backend service in Service Fabric.</span></span>

### <a name="topology"></a><span data-ttu-id="e98b2-109">Топология</span><span class="sxs-lookup"><span data-stu-id="e98b2-109">Topology</span></span>

<span data-ttu-id="e98b2-110">В этом руководстве развертывает следующие hello tooAzure топологии, в которой API управления и структуры службы находятся в подсетях hello одной виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="e98b2-110">This guide deploys hello following topology tooAzure in which API Management and Service Fabric are in subnets of hello same Virtual Network:</span></span>

 ![Рисунок][sf-apim-topology-overview]

<span data-ttu-id="e98b2-112">tooget быстро начать работу, диспетчер ресурсов предоставляются шаблоны для каждого из шагов развертывания:</span><span class="sxs-lookup"><span data-stu-id="e98b2-112">tooget started quickly, Resource Manager templates are provided for each deployment step:</span></span>

 - <span data-ttu-id="e98b2-113">Топология сети:</span><span class="sxs-lookup"><span data-stu-id="e98b2-113">Network topology:</span></span>
    - <span data-ttu-id="e98b2-114">[network.json][network-arm]</span><span class="sxs-lookup"><span data-stu-id="e98b2-114">[network.json][network-arm]</span></span>
    - <span data-ttu-id="e98b2-115">[network.parameters.json][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="e98b2-115">[network.parameters.json][network-parameters-arm]</span></span>
 - <span data-ttu-id="e98b2-116">Кластер Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="e98b2-116">Service Fabric cluster:</span></span>
    - <span data-ttu-id="e98b2-117">[cluster.json][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="e98b2-117">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="e98b2-118">[cluster.parameters.json][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="e98b2-118">[cluster.parameters.json][cluster-parameters-arm]</span></span>
 - <span data-ttu-id="e98b2-119">Управление API</span><span class="sxs-lookup"><span data-stu-id="e98b2-119">API Management:</span></span>
    - <span data-ttu-id="e98b2-120">[apim.json][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="e98b2-120">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="e98b2-121">[apim.parameters.json][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="e98b2-121">[apim.parameters.json][apim-parameters-arm]</span></span>

### <a name="sign-in-tooazure-and-select-your-subscription"></a><span data-ttu-id="e98b2-122">Войдите в tooAzure и выберите свою подписку</span><span class="sxs-lookup"><span data-stu-id="e98b2-122">Sign in tooAzure and select your subscription</span></span>

<span data-ttu-id="e98b2-123">В этом руководстве используется [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="e98b2-123">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="e98b2-124">При запуске нового сеанса PowerShell, войдите в tooyour учетная запись Azure и выберите подписку, перед выполнением команды Azure.</span><span class="sxs-lookup"><span data-stu-id="e98b2-124">When you start a new PowerShell session, sign in tooyour Azure account and select your subscription before you execute Azure commands.</span></span>
 
<span data-ttu-id="e98b2-125">Войдите в tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="e98b2-125">Sign in tooyour Azure account:</span></span>

```powershell
PS > Login-AzureRmAccount
```

<span data-ttu-id="e98b2-126">Выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="e98b2-126">Select your subscription:</span></span>

```powershell
PS > Get-AzureRmSubscription
PS > Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="create-a-resource-group"></a><span data-ttu-id="e98b2-127">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="e98b2-127">Create a resource group</span></span>

<span data-ttu-id="e98b2-128">Создайте новую группу ресурсов для развертывания.</span><span class="sxs-lookup"><span data-stu-id="e98b2-128">Create a new resource group for your deployment.</span></span> <span data-ttu-id="e98b2-129">Назначьте ей имя и расположение.</span><span class="sxs-lookup"><span data-stu-id="e98b2-129">Give it a name and a location.</span></span>

```powershell
PS > New-AzureRmResourceGroup -Name <my-resource-group> -Location westus
```

### <a name="deploy-hello-network-topology"></a><span data-ttu-id="e98b2-130">Развертывание hello топологии сети</span><span class="sxs-lookup"><span data-stu-id="e98b2-130">Deploy hello network topology</span></span>

<span data-ttu-id="e98b2-131">Hello первый шаг — tooset копирование toowhich топологии сети hello API управления и кластера Service Fabric hello будет развертываться.</span><span class="sxs-lookup"><span data-stu-id="e98b2-131">hello first step is tooset up hello network topology toowhich API Management and hello Service Fabric cluster will be deployed.</span></span> <span data-ttu-id="e98b2-132">Hello [network.json] [ network-arm] шаблона диспетчера ресурсов является настроенным toocreate виртуальной сети (VNET) с двумя подсетями и две группы безопасности сети (NSG).</span><span class="sxs-lookup"><span data-stu-id="e98b2-132">hello [network.json][network-arm] Resource Manager template is configured toocreate a Virtual Network (VNET) with two subnets and two Network Security Groups (NSG).</span></span> 

<span data-ttu-id="e98b2-133">Hello [network.parameters.json] [ network-parameters-arm] файл параметров содержит hello имена подсетей hello и Nsg, которые будут развернуты для управления API и Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e98b2-133">hello [network.parameters.json][network-parameters-arm] parameters file contains hello names of hello subnets and NSGs that API Management and Service Fabric will be deployed to.</span></span> <span data-ttu-id="e98b2-134">В этом руководстве hello значения параметров не обязательно toobe изменен.</span><span class="sxs-lookup"><span data-stu-id="e98b2-134">For this guide, hello parameter values do not need toobe changed.</span></span> <span data-ttu-id="e98b2-135">шаблоны управления API и диспетчер ресурсов структуры службы Hello использовать эти значения, если они изменяются здесь, необходимо изменить их в другие шаблоны диспетчера ресурсов hello соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="e98b2-135">hello API Management and Service Fabric Resource Manager templates use these values, so if they are modified here, you must modify them in hello other Resource Manager templates accordingly.</span></span> 

 1. <span data-ttu-id="e98b2-136">Загрузите следующий файл шаблона и параметров диспетчера ресурсов hello:</span><span class="sxs-lookup"><span data-stu-id="e98b2-136">Download hello following Resource Manager template and parameters file:</span></span>

    - <span data-ttu-id="e98b2-137">[network.json][network-arm]</span><span class="sxs-lookup"><span data-stu-id="e98b2-137">[network.json][network-arm]</span></span>
    - <span data-ttu-id="e98b2-138">[network.parameters.json][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="e98b2-138">[network.parameters.json][network-parameters-arm]</span></span>

 2. <span data-ttu-id="e98b2-139">Используйте следующие PowerShell команды toodeploy hello диспетчера ресурсов файлы шаблонов и параметров для настройки сети hello hello.</span><span class="sxs-lookup"><span data-stu-id="e98b2-139">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files for hello network setup:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\network.json -TemplateParameterFile .\network.parameters.json -Verbose
    ```

### <a name="deploy-hello-service-fabric-cluster"></a><span data-ttu-id="e98b2-140">Развертывание кластера Service Fabric hello</span><span class="sxs-lookup"><span data-stu-id="e98b2-140">Deploy hello Service Fabric cluster</span></span>

<span data-ttu-id="e98b2-141">После hello сетевым ресурсам завершено развертывание, hello следующим шагом является toodeploy toohello кластера Service Fabric виртуальной сети в подсеть hello и NSG предназначенные для кластера Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="e98b2-141">Once hello network resources have finished deploying, hello next step is toodeploy a Service Fabric cluster toohello VNET in hello subnet and NSG designated for hello Service Fabric cluster.</span></span> <span data-ttu-id="e98b2-142">В этом учебнике шаблона диспетчера ресурсов структуры службы hello — имена hello предварительно настроенных toouse hello виртуальной сети, подсети и NSG, которая настраивается в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="e98b2-142">For this tutorial, hello Service Fabric Resource Manager template is pre-configured toouse hello names of hello VNET, subnet, and NSG that you set up in hello previous step.</span></span> 

<span data-ttu-id="e98b2-143">шаблона диспетчера ресурсов кластера Service Fabric Hello является настроенным toocreate безопасного кластера сертификат безопасности.</span><span class="sxs-lookup"><span data-stu-id="e98b2-143">hello Service Fabric cluster Resource Manager template is configured toocreate a secure cluster with certificate security.</span></span> <span data-ttu-id="e98b2-144">Hello сертификат является используется toosecure связи для узлов для кластера и кластера Service Fabric tooyour доступа пользователя toomanage.</span><span class="sxs-lookup"><span data-stu-id="e98b2-144">hello certificate is used toosecure node-to-node communication for your cluster and toomanage user access tooyour Service Fabric cluster.</span></span> <span data-ttu-id="e98b2-145">API управления использует этот сертификат tooaccess hello служба именования Service Fabric для обнаружения службы.</span><span class="sxs-lookup"><span data-stu-id="e98b2-145">API Management uses this certificate tooaccess  hello Service Fabric Naming Service for service discovery.</span></span>

<span data-ttu-id="e98b2-146">Этот шаг требует наличия сертификата в Key Vault для обеспечения безопасности кластера.</span><span class="sxs-lookup"><span data-stu-id="e98b2-146">This step requires having a certificate in Key Vault for cluster security.</span></span> <span data-ttu-id="e98b2-147">Дополнительные сведения о настройке безопасного кластера с помощью Key Vault см. в статье [Создание кластера Service Fabric в Azure с помощью Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="e98b2-147">For more information on setting up a secure cluster with Key Vault, see [this guide on creating a cluster in Azure using Resource Manager](service-fabric-cluster-creation-via-arm.md)</span></span>

> [!NOTE]
> <span data-ttu-id="e98b2-148">Проверка подлинности Azure Active Directory можно добавить в дополнение toohello сертификат, используемый для доступа к кластеру.</span><span class="sxs-lookup"><span data-stu-id="e98b2-148">You may add Azure Active Directory authentication in addition toohello certificate used for cluster access.</span></span> <span data-ttu-id="e98b2-149">Azure Active Directory рекомендуется кластера Service Fabric tooyour доступа пользователя способом toomanage hello, но не обязательно toocomplete этого учебника.</span><span class="sxs-lookup"><span data-stu-id="e98b2-149">Azure Active Directory is hello recommended way toomanage user access tooyour Service Fabric cluster, but is not necessary toocomplete this tutorial.</span></span> <span data-ttu-id="e98b2-150">Сертификат является обязательным для обеспечения безопасности кластера при обмене данными между узлами, а также для аутентификации службы управления API Azure, которая в настоящее время не поддерживает аутентификацию с помощью Azure Active Directory для серверной части Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e98b2-150">A certificate is required either way for cluster node-to-node security and for Azure API Management authentication, which currently does not support authenticating with Azure Active Directory for a Service Fabric backend.</span></span>

 1. <span data-ttu-id="e98b2-151">Загрузите следующий файл шаблона и параметров диспетчера ресурсов hello:</span><span class="sxs-lookup"><span data-stu-id="e98b2-151">Download hello following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="e98b2-152">[cluster.json][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="e98b2-152">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="e98b2-153">[cluster.parameters.json][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="e98b2-153">[cluster.parameters.json][cluster-parameters-arm]</span></span>

 2. <span data-ttu-id="e98b2-154">Заполните пустые параметры hello в hello `cluster.parameters.json` файл для развертывания, включая hello [сведения о хранилище ключей](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) сертификата кластера.</span><span class="sxs-lookup"><span data-stu-id="e98b2-154">Fill in hello empty parameters in hello `cluster.parameters.json` file for your deployment, including hello [Key Vault information](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) for your cluster certificate.</span></span>

 3. <span data-ttu-id="e98b2-155">Используйте следующие PowerShell команды toodeploy hello диспетчера ресурсов шаблонов и параметров файлы toocreate hello кластера Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="e98b2-155">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files toocreate hello Service Fabric cluster:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\cluster.json -TemplateParameterFile .\cluster.parameters.json -Verbose
    ```

### <a name="deploy-api-management"></a><span data-ttu-id="e98b2-156">Развертывание управления API</span><span class="sxs-lookup"><span data-stu-id="e98b2-156">Deploy API Management</span></span>

<span data-ttu-id="e98b2-157">Наконец можно разверните toohello API управления виртуальной сети в подсеть hello и NSG, предназначенные для управления API.</span><span class="sxs-lookup"><span data-stu-id="e98b2-157">Finally, deploy API Management toohello VNET in hello subnet and NSG designated for API Management.</span></span> <span data-ttu-id="e98b2-158">Необязательно toowait для toofinish развертывания кластера Service Fabric hello перед развертыванием управления API.</span><span class="sxs-lookup"><span data-stu-id="e98b2-158">You do not need toowait for hello Service Fabric cluster deployment toofinish before deploying API Management.</span></span> 

<span data-ttu-id="e98b2-159">В этом учебнике шаблона диспетчера ресурсов для управления API hello — имена hello предварительно настроенных toouse hello виртуальной сети, подсети и NSG, которая настраивается в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="e98b2-159">For this tutorial, hello API Management Resource Manager template is pre-configured toouse hello names of hello VNET, subnet, and NSG that you set up in hello previous step.</span></span> 

 1. <span data-ttu-id="e98b2-160">Загрузите следующий файл шаблона и параметров диспетчера ресурсов hello:</span><span class="sxs-lookup"><span data-stu-id="e98b2-160">Download hello following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="e98b2-161">[apim.json][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="e98b2-161">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="e98b2-162">[apim.parameters.json][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="e98b2-162">[apim.parameters.json][apim-parameters-arm]</span></span>

 2. <span data-ttu-id="e98b2-163">Заполните пустые параметры hello в hello `apim.parameters.json` для развертывания.</span><span class="sxs-lookup"><span data-stu-id="e98b2-163">Fill in hello empty parameters in hello `apim.parameters.json` for your deployment.</span></span>

 3. <span data-ttu-id="e98b2-164">Используйте следующие PowerShell команды toodeploy hello диспетчера ресурсов файлы шаблонов и параметров для управления API hello.</span><span class="sxs-lookup"><span data-stu-id="e98b2-164">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files for API Management:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\apim.json -TemplateParameterFile .\apim.parameters.json -Verbose
    ```

## <a name="configure-api-management"></a><span data-ttu-id="e98b2-165">Настройка управления API</span><span class="sxs-lookup"><span data-stu-id="e98b2-165">Configure API Management</span></span>

<span data-ttu-id="e98b2-166">После развертывания кластера Service Fabric и управления API можно настроить серверную часть Service Fabric в службе управления API.</span><span class="sxs-lookup"><span data-stu-id="e98b2-166">Once your API Management and Service Fabric cluster are deployed, you can configure a Service Fabric backend in API Management.</span></span> <span data-ttu-id="e98b2-167">Это позволяет toocreate политику серверной службы, которая отправляет трафик кластера Service Fabric tooyour.</span><span class="sxs-lookup"><span data-stu-id="e98b2-167">This allows you toocreate a backend service policy that sends traffic tooyour Service Fabric cluster.</span></span>

### <a name="api-management-security"></a><span data-ttu-id="e98b2-168">Безопасность управления API</span><span class="sxs-lookup"><span data-stu-id="e98b2-168">API Management Security</span></span>

<span data-ttu-id="e98b2-169">tooconfigure hello Service Fabric серверной части, необходимо сначала tooconfigure параметры безопасности управления API.</span><span class="sxs-lookup"><span data-stu-id="e98b2-169">tooconfigure hello Service Fabric backend, you first need tooconfigure API Management security settings.</span></span> <span data-ttu-id="e98b2-170">параметры безопасности tooconfigure, перейдите tooyour API службы управления в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e98b2-170">tooconfigure security settings, go tooyour API Management service in hello Azure portal.</span></span>

#### <a name="enable-hello-api-management-rest-api"></a><span data-ttu-id="e98b2-171">Включить hello API REST управления API</span><span class="sxs-lookup"><span data-stu-id="e98b2-171">Enable hello API Management REST API</span></span>

<span data-ttu-id="e98b2-172">Hello API REST управления API в настоящий момент hello единственным способом tooconfigure серверной службы.</span><span class="sxs-lookup"><span data-stu-id="e98b2-172">hello API Management REST API is currently hello only way tooconfigure a backend service.</span></span> <span data-ttu-id="e98b2-173">Первым шагом Hello — tooenable hello API REST управления API и защитить ее.</span><span class="sxs-lookup"><span data-stu-id="e98b2-173">hello first step is tooenable hello API Management REST API and secure it.</span></span>

 1. <span data-ttu-id="e98b2-174">В hello службы управления API, выберите **API управления - PREVIEW** под **безопасности**.</span><span class="sxs-lookup"><span data-stu-id="e98b2-174">In hello API Management service, select **Management API - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="e98b2-175">Проверьте hello **включить API REST управления** флажок.</span><span class="sxs-lookup"><span data-stu-id="e98b2-175">Check hello **Enable API Management REST API** checkbox.</span></span>
 3. <span data-ttu-id="e98b2-176">Обратите внимание, hello URL-адрес API управления — hello URL-адрес, мы будем использовать более поздней версии tooset копирование серверной hello Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e98b2-176">Note hello Management API URL - this is hello URL we'll use later tooset up hello Service Fabric backend</span></span>
 4. <span data-ttu-id="e98b2-177">Создание **маркер доступа** , выбрав дату окончания действия и ключ, нажмите кнопку hello **формирования** кнопку нижней hello страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="e98b2-177">Generate an **access Token** by selecting an expiry date and a key, then click hello **Generate** button toward hello bottom of hello page.</span></span>
 5. <span data-ttu-id="e98b2-178">Копировать hello **маркер доступа** и сохранить его — мы будем использовать в hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="e98b2-178">Copy hello **access token** and save it - we'll use this in hello following steps.</span></span> <span data-ttu-id="e98b2-179">Обратите внимание, что это отличается от hello первичного и вторичного ключа.</span><span class="sxs-lookup"><span data-stu-id="e98b2-179">Note this is different from hello primary key and secondary key.</span></span>

#### <a name="upload-a-service-fabric-client-certificate"></a><span data-ttu-id="e98b2-180">Отправка клиентского сертификата Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e98b2-180">Upload a Service Fabric client certificate</span></span>

<span data-ttu-id="e98b2-181">API управления должны пройти проверку подлинности с кластером Service Fabric для обнаружения службы с помощью сертификат клиента, который имеет доступ tooyour кластера.</span><span class="sxs-lookup"><span data-stu-id="e98b2-181">API Management must authenticate with your Service Fabric cluster for service discovery using a client certificate that has access tooyour cluster.</span></span> <span data-ttu-id="e98b2-182">Для простоты в этом учебнике используется hello один сертификат, указанный при создании кластера Service Fabric hello, который по умолчанию можно использовать tooaccess кластера.</span><span class="sxs-lookup"><span data-stu-id="e98b2-182">For simplicity, this tutorial uses hello same certificate specified when creating hello Service Fabric cluster, which by default can be used tooaccess your cluster.</span></span>

 1. <span data-ttu-id="e98b2-183">В hello службы управления API, выберите **сертификаты клиента — Предварительный просмотр** под **безопасности**.</span><span class="sxs-lookup"><span data-stu-id="e98b2-183">In hello API Management service, select **Client certificates - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="e98b2-184">Нажмите кнопку hello **+ добавить** кнопки</span><span class="sxs-lookup"><span data-stu-id="e98b2-184">Click hello **+ Add** button</span></span>
 2. <span data-ttu-id="e98b2-185">Выберите hello файл закрытого ключа (PFX-файл) сертификата hello кластера, указанный при создании кластера Service Fabric, присвойте ему имя и укажите пароль закрытого ключа hello.</span><span class="sxs-lookup"><span data-stu-id="e98b2-185">Select hello private key file (.pfx) of hello cluster certificate that you specified when creating your Service Fabric cluster, give it a name, and provide hello private key password.</span></span>

> [!NOTE]
> <span data-ttu-id="e98b2-186">В этом учебнике используется hello же сертификат безопасности клиента проверки подлинности и кластера узла на узел.</span><span class="sxs-lookup"><span data-stu-id="e98b2-186">This tutorial uses hello same certificate for client authentication and cluster node-to-node security.</span></span> <span data-ttu-id="e98b2-187">Может использовать сертификат отдельного клиента, при наличии одного настроенного tooaccess кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e98b2-187">You may use a separate client certificate if you have one configured tooaccess your Service Fabric cluster.</span></span>

### <a name="configure-hello-backend"></a><span data-ttu-id="e98b2-188">Настройка внутреннего hello</span><span class="sxs-lookup"><span data-stu-id="e98b2-188">Configure hello backend</span></span>

<span data-ttu-id="e98b2-189">Теперь, когда настройки параметров безопасности для управления API можно настроить внутренний Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="e98b2-189">Now that API Management security is configured, you can configure hello Service Fabric backend.</span></span> <span data-ttu-id="e98b2-190">Для серверных системах Service Fabric hello кластера Service Fabric — hello серверной части, а не конкретной службы Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e98b2-190">For Service Fabric backends, hello Service Fabric cluster is hello backend, rather than a specific Service Fabric service.</span></span> <span data-ttu-id="e98b2-191">Это позволяет toomore tooroute отдельную политику больше одной службы в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="e98b2-191">This allows a single policy tooroute toomore than one service in hello cluster.</span></span>

<span data-ttu-id="e98b2-192">Этот шаг требуется hello маркер доступа, который был создан ранее и hello отпечаток сертификата кластера отправленный tooAPI управления на предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="e98b2-192">This step requires hello access token you generated earlier and hello thumbprint for your cluster certificate you uploaded tooAPI Management in hello previous step.</span></span>

> [!NOTE]
> <span data-ttu-id="e98b2-193">Если используется отдельный клиентский сертификат на предыдущем шаге hello для управления API, необходимо hello отпечаток сертификата клиента hello отпечаток сертификата сложения toohello кластера на этом шаге.</span><span class="sxs-lookup"><span data-stu-id="e98b2-193">If you used a separate client certificate in hello previous step for API Management, you need hello thumbprint for hello client certificate in addition toohello cluster certificate thumbprint in this step.</span></span>

<span data-ttu-id="e98b2-194">Отправьте следующие toohello запрос HTTP PUT API управления URL-адрес API записанные ранее при включении hello API REST управления tooconfigure hello Service Fabric серверную службу hello.</span><span class="sxs-lookup"><span data-stu-id="e98b2-194">Send hello following HTTP PUT request toohello API Management API URL you noted earlier when enabling hello API Management REST API tooconfigure hello Service Fabric backend service.</span></span> <span data-ttu-id="e98b2-195">Вы увидите `HTTP 201 Created` ответ после успешного завершения команды hello.</span><span class="sxs-lookup"><span data-stu-id="e98b2-195">You should see an `HTTP 201 Created` response when hello command succeeds.</span></span> <span data-ttu-id="e98b2-196">Дополнительные сведения о каждом поле см. в разделе hello API управления [справочной документации по API внутреннего сервера](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span><span class="sxs-lookup"><span data-stu-id="e98b2-196">For more information on each field, see hello API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span></span>

<span data-ttu-id="e98b2-197">Команда HTTP и URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="e98b2-197">HTTP command and URL:</span></span>
```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
```

<span data-ttu-id="e98b2-198">Заголовки запроса:</span><span class="sxs-lookup"><span data-stu-id="e98b2-198">Request headers:</span></span>
```http
Authorization: SharedAccessSignature <your access token>
Content-Type: application/json
```

<span data-ttu-id="e98b2-199">Тело запроса:</span><span class="sxs-lookup"><span data-stu-id="e98b2-199">Request body:</span></span>
```http
{
    "description": "<description>",
    "url": "<fallback service name>",
    "protocol": "http",
    "resourceId": "<cluster HTTP management endpoint>",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": [ "<cluster HTTP management endpoint>" ],
            "clientCertificateThumbprint": "<client cert thumbprint>",
            "serverCertificateThumbprints": [ "<cluster cert thumbprint>" ],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

<span data-ttu-id="e98b2-200">Hello **URL-адрес** здесь является полное службы имя службы в кластере, все запросы направлено tooby по умолчанию, если имя службы не указано в политике серверной части.</span><span class="sxs-lookup"><span data-stu-id="e98b2-200">hello **url** parameter here is a fully-qualified service name of a service in your cluster that all requests are routed tooby default if no service name is specified in a backend policy.</span></span> <span data-ttu-id="e98b2-201">Может использовать имя фиктивное службы, такие как «fabric: / фиктивное/служба», если не требуется делать toohave резервной службы.</span><span class="sxs-lookup"><span data-stu-id="e98b2-201">You may use a fake service name, such as "fabric:/fake/service" if you do not intend toohave a fallback service.</span></span>

<span data-ttu-id="e98b2-202">Ссылки toohello API управления [справочной документации по API внутреннего сервера](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) Дополнительные сведения о каждом поле.</span><span class="sxs-lookup"><span data-stu-id="e98b2-202">Refer toohello API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) for more details on each field.</span></span>

#### <a name="example"></a><span data-ttu-id="e98b2-203">Пример</span><span class="sxs-lookup"><span data-stu-id="e98b2-203">Example</span></span>

```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
Authorization: SharedAccessSignature 230948023984&Ld93cRGcNU6KZ4uVz7JlfTec4eX43Q9Nu8ndatOgBzs6+f559Pkf3iHX2cSge+r42pn35qGY3TitjrIl13hwcQ==
Content-Type: application/json

{
    "description": "My Service Fabric backend",
    "url": "fabric:/myapp/myservice",
    "protocol": "http",
    "resourceId": "https://your-cluster.westus.cloudapp.azure.com:19080",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": ["https://your-cluster.westus.cloudapp.azure.com:19080"],
            "clientCertificateThumbprint": "57bc463aba3aea3a12a18f36f44154f819f0fe32",
            "serverCertificateThumbprints": ["57bc463aba3aea3a12a18f36f44154f819f0fe32"],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

## <a name="deploy-a-service-fabric-back-end-service"></a><span data-ttu-id="e98b2-204">Развертывание внутренней службы Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e98b2-204">Deploy a Service Fabric back-end service</span></span>

<span data-ttu-id="e98b2-205">Теперь, когда Service Fabric настроен в качестве серверной части tooAPI управления приветствия, можно создавать политики серверной части для собственные интерфейсы API, отправлять трафик tooyour служб Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e98b2-205">Now that you have hello Service Fabric configured as a backend tooAPI Management, you can author backend policies for your APIs that send traffic tooyour Service Fabric services.</span></span> <span data-ttu-id="e98b2-206">Но сначала необходимо к службе, запущенной в запросах tooaccept Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e98b2-206">But first you need a service running in Service Fabric tooaccept requests.</span></span>

### <a name="create-a-service-fabric-service-with-an-http-endpoint"></a><span data-ttu-id="e98b2-207">Создание службы Service Fabric с конечной точкой HTTP</span><span class="sxs-lookup"><span data-stu-id="e98b2-207">Create a Service Fabric service with an HTTP endpoint</span></span>

<span data-ttu-id="e98b2-208">В этом учебнике мы создадим базовую без сохранения состояния ASP.NET Core надежного службу с помощью шаблона проекта веб-API по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="e98b2-208">For this tutorial, we'll create a basic stateless ASP.NET Core Reliable Service using hello default Web API project template.</span></span> <span data-ttu-id="e98b2-209">Так мы получим конечную точку HTTP для службы, которую можно будет использовать через службу управления API Azure:</span><span class="sxs-lookup"><span data-stu-id="e98b2-209">This creates an HTTP endpoint for your service, which you'll expose through Azure API Management:</span></span>

```
/api/values
```

<span data-ttu-id="e98b2-210">Ознакомьтесь с разделом о [настройке среды разработки для разработки ASP.NET Core](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span><span class="sxs-lookup"><span data-stu-id="e98b2-210">Start by [setting up your development environment for ASP.NET Core development](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span></span>

<span data-ttu-id="e98b2-211">После настройки среды разработки запустите Visual Studio от имени администратора и создайте службу ASP.NET Core:</span><span class="sxs-lookup"><span data-stu-id="e98b2-211">Once your development environment is set up, start Visual Studio as Administrator and create an ASP.NET Core service:</span></span>

 1. <span data-ttu-id="e98b2-212">В Visual Studio выберите последовательно «Файл» -> «Создать проект».</span><span class="sxs-lookup"><span data-stu-id="e98b2-212">In Visual Studio, select File -> New Project.</span></span>
 2. <span data-ttu-id="e98b2-213">Выберите шаблон службы структуры приложение hello в облаке и назовите его **«ApiApplication»**.</span><span class="sxs-lookup"><span data-stu-id="e98b2-213">Select hello Service Fabric Application template under Cloud and name it **"ApiApplication"**.</span></span>
 3. <span data-ttu-id="e98b2-214">Выберите шаблон службы ASP.NET Core hello и имя проекта hello **«WebApiService»**.</span><span class="sxs-lookup"><span data-stu-id="e98b2-214">Select hello ASP.NET Core service template and name hello project **"WebApiService"**.</span></span>
 4. <span data-ttu-id="e98b2-215">Выберите шаблон проекта hello Web API ASP.NET Core 1.1.</span><span class="sxs-lookup"><span data-stu-id="e98b2-215">Select hello Web API ASP.NET Core 1.1 project template.</span></span>
 5. <span data-ttu-id="e98b2-216">После создания проекта Привет открыть `PackageRoot\ServiceManifest.xml` и удалите hello `Port` атрибут из конфигурации ресурса hello конечной точки:</span><span class="sxs-lookup"><span data-stu-id="e98b2-216">Once hello project is created, open `PackageRoot\ServiceManifest.xml` and remove hello `Port` attribute from hello endpoint resource configuration:</span></span>
 
    ```xml
    <Resources>
      <Endpoints>
        <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" />
      </Endpoints>
    </Resources>
    ```

    <span data-ttu-id="e98b2-217">Это позволяет toospecify Service Fabric порт динамически из диапазона портов приложения hello, который мы открытые с ее помощью hello сетевой группы безопасности в шаблоне диспетчер ресурсов кластера hello, предоставляя tooit tooflow трафика управления API.</span><span class="sxs-lookup"><span data-stu-id="e98b2-217">This allows Service Fabric toospecify a port dynamically from hello application port range, which we opened through hello Network Security Group in hello cluster Resource Manager template, allowing traffic tooflow tooit from API Management.</span></span>
 
 6. <span data-ttu-id="e98b2-218">Нажмите клавишу F5 в Visual Studio tooverify hello веб-API доступен локально.</span><span class="sxs-lookup"><span data-stu-id="e98b2-218">Press F5 in Visual Studio tooverify hello web API is available locally.</span></span> 

    <span data-ttu-id="e98b2-219">Откройте обозреватель Service Fabric и детализацию tooa определенного экземпляра hello, ASP.NET Core toosee hello базовый адрес hello служба выполняет прослушивание.</span><span class="sxs-lookup"><span data-stu-id="e98b2-219">Open Service Fabric Explorer and drill down tooa specific instance of hello ASP.NET Core service toosee hello base address hello service is listening on.</span></span> <span data-ttu-id="e98b2-220">Добавить `/api/values` toohello базовый адрес и откройте его в браузере.</span><span class="sxs-lookup"><span data-stu-id="e98b2-220">Add `/api/values` toohello base address and open it in a browser.</span></span> <span data-ttu-id="e98b2-221">При этом вызывается метод Get на hello ValuesController в шаблоне веб-API hello hello.</span><span class="sxs-lookup"><span data-stu-id="e98b2-221">This invokes hello Get method on hello ValuesController in hello Web API template.</span></span> <span data-ttu-id="e98b2-222">Он возвращает ответ по умолчанию hello, предоставляемого шаблоном hello, массив JSON, который содержит две строки:</span><span class="sxs-lookup"><span data-stu-id="e98b2-222">It returns hello default response that is provided by hello template, a JSON array that contains two strings:</span></span>

    ```json
    ["value1", "value2"]`
    ```

    <span data-ttu-id="e98b2-223">Это конечная точка hello, который будет предоставлять через управление API в Azure.</span><span class="sxs-lookup"><span data-stu-id="e98b2-223">This is hello endpoint that you'll expose through API Management in Azure.</span></span>

 7. <span data-ttu-id="e98b2-224">Наконец разверните кластер tooyour приложения hello в Azure.</span><span class="sxs-lookup"><span data-stu-id="e98b2-224">Finally, deploy hello application tooyour cluster in Azure.</span></span> <span data-ttu-id="e98b2-225">[С помощью Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), щелкните правой кнопкой мыши проект приложения hello и выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="e98b2-225">[Using Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), right-click hello Application project and select **Publish**.</span></span> <span data-ttu-id="e98b2-226">Укажите конечную точку кластера (например, `mycluster.westus.cloudapp.azure.com:19000`) tooyour приложения hello toodeploy Service Fabric кластер в Azure.</span><span class="sxs-lookup"><span data-stu-id="e98b2-226">Provide your cluster endpoint (for example, `mycluster.westus.cloudapp.azure.com:19000`) toodeploy hello application tooyour Service Fabric cluster in Azure.</span></span>

<span data-ttu-id="e98b2-227">В кластере Service Fabric в Azure должна запуститься служба ASP.NET Core без отслеживания состояния с именем `fabric:/ApiApplication/WebApiService`.</span><span class="sxs-lookup"><span data-stu-id="e98b2-227">An ASP.NET Core stateless service named `fabric:/ApiApplication/WebApiService` should now be running in your Service Fabric cluster in Azure.</span></span>

## <a name="create-an-api-operation"></a><span data-ttu-id="e98b2-228">Создание операции API</span><span class="sxs-lookup"><span data-stu-id="e98b2-228">Create an API operation</span></span>

<span data-ttu-id="e98b2-229">Теперь мы готовы toocreate операции в службе управления API, toocommunicate использование внешних клиентов с hello в кластер Service Fabric hello службы без отслеживания состояния ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="e98b2-229">Now we're ready toocreate an operation in API Management that external clients use toocommunicate with hello ASP.NET Core stateless service running in hello Service Fabric cluster.</span></span>

 1. <span data-ttu-id="e98b2-230">Войдите в портал Azure toohello и перейдите tooyour развертывания службы управления API.</span><span class="sxs-lookup"><span data-stu-id="e98b2-230">Log in toohello Azure portal and navigate tooyour API Management service deployment.</span></span>
 2. <span data-ttu-id="e98b2-231">В колонке службы управления API hello выберите **API-интерфейсов - Предварительный просмотр**</span><span class="sxs-lookup"><span data-stu-id="e98b2-231">In hello API Management service blade, select **APIs - Preview**</span></span>
 3. <span data-ttu-id="e98b2-232">Добавить новый API, щелкнув hello **пустой API** поле и заполнив диалоговое окно «hello»:</span><span class="sxs-lookup"><span data-stu-id="e98b2-232">Add a new API by clicking hello **Blank API** box and filling out hello dialog box:</span></span>

     - <span data-ttu-id="e98b2-233">**URL-адрес веб-службы**: для серверных систем Service Fabric это значение URL-адреса не используется.</span><span class="sxs-lookup"><span data-stu-id="e98b2-233">**Web service URL**: For Service Fabric backends, this URL value is not used.</span></span> <span data-ttu-id="e98b2-234">Здесь вы можете использовать любое значение.</span><span class="sxs-lookup"><span data-stu-id="e98b2-234">You can put any value here.</span></span> <span data-ttu-id="e98b2-235">В рамках этого руководства используйте `http://servicefabric`.</span><span class="sxs-lookup"><span data-stu-id="e98b2-235">For this tutorial, use: `http://servicefabric`.</span></span>
     - <span data-ttu-id="e98b2-236">**Имя**: укажите любое имя для API.</span><span class="sxs-lookup"><span data-stu-id="e98b2-236">**Name**: Provide any name for your API.</span></span> <span data-ttu-id="e98b2-237">В рамках этого руководства используйте `Service Fabric App`.</span><span class="sxs-lookup"><span data-stu-id="e98b2-237">For this tutorial, use `Service Fabric App`.</span></span>
     - <span data-ttu-id="e98b2-238">**Схема URL-адреса**: выберите HTTP, HTTPS или оба варианта.</span><span class="sxs-lookup"><span data-stu-id="e98b2-238">**URL scheme**: Select either HTTP, HTTPS, or both.</span></span> <span data-ttu-id="e98b2-239">В рамках этого руководства используйте `both`.</span><span class="sxs-lookup"><span data-stu-id="e98b2-239">For this tutorial, use `both`.</span></span>
     - <span data-ttu-id="e98b2-240">**API URL Suffix** (Суффикс URL-адреса API): укажите суффикс для API.</span><span class="sxs-lookup"><span data-stu-id="e98b2-240">**API URL Suffix**: Provide a suffix for our API.</span></span> <span data-ttu-id="e98b2-241">В рамках этого руководства используйте `myapp`.</span><span class="sxs-lookup"><span data-stu-id="e98b2-241">For this tutorial, use `myapp`.</span></span>
 
 4. <span data-ttu-id="e98b2-242">После создания hello API щелкните **+ добавить операцию** операции tooadd интерфейса API.</span><span class="sxs-lookup"><span data-stu-id="e98b2-242">Once hello API is created, click **+ Add operation** tooadd a front-end API operation.</span></span> <span data-ttu-id="e98b2-243">Заполните значения hello:</span><span class="sxs-lookup"><span data-stu-id="e98b2-243">Fill out hello values:</span></span>
    
     - <span data-ttu-id="e98b2-244">**URL-адрес**: выберите `GET` и укажите URL-путь для hello API.</span><span class="sxs-lookup"><span data-stu-id="e98b2-244">**URL**: Select `GET` and provide a URL path for hello API.</span></span> <span data-ttu-id="e98b2-245">В рамках этого руководства используйте `/api/values`.</span><span class="sxs-lookup"><span data-stu-id="e98b2-245">For this tutorial, use `/api/values`.</span></span>
     
       <span data-ttu-id="e98b2-246">По умолчанию hello URL-пути, здесь указывается hello URL-адрес отправляется toohello серверная служба Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e98b2-246">By default, hello URL path specified here is hello URL path sent toohello backend Service Fabric service.</span></span> <span data-ttu-id="e98b2-247">Если вы используете hello же URL-пути здесь, в этом случае служба использует `/api/values`, затем hello операция работает без дальнейших изменений.</span><span class="sxs-lookup"><span data-stu-id="e98b2-247">If you use hello same URL path here that your service uses, in this case `/api/values`, then hello operation works without further modification.</span></span> <span data-ttu-id="e98b2-248">Можно также указать URL-путь здесь, отличный от hello URL-адрес, используемый сервером службы Service Fabric в этом случае будут также toospecify необходимости измените путь в политике операцию позже.</span><span class="sxs-lookup"><span data-stu-id="e98b2-248">You may also specify a URL path here that is different from hello URL path used by your backend Service Fabric service, in which case you will also need toospecify a path rewrite in your operation policy later.</span></span>
     - <span data-ttu-id="e98b2-249">**Отображаемое имя**: Введите любое имя для hello API.</span><span class="sxs-lookup"><span data-stu-id="e98b2-249">**Display name**: Provide any name for hello API.</span></span> <span data-ttu-id="e98b2-250">В рамках этого руководства используйте `Values`.</span><span class="sxs-lookup"><span data-stu-id="e98b2-250">For this tutorial, use `Values`.</span></span>

## <a name="configure-a-backend-policy"></a><span data-ttu-id="e98b2-251">Настройка внутренней политики</span><span class="sxs-lookup"><span data-stu-id="e98b2-251">Configure a backend policy</span></span>

<span data-ttu-id="e98b2-252">политика серверной Hello объединяет все данные.</span><span class="sxs-lookup"><span data-stu-id="e98b2-252">hello backend policy ties everything together.</span></span> <span data-ttu-id="e98b2-253">Это связано с которой выполняется настройка hello серверной службы toowhich запросы направляются Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e98b2-253">This is where you configure hello backend Service Fabric service toowhich requests are routed.</span></span> <span data-ttu-id="e98b2-254">Можно применить эту операцию API tooany политики.</span><span class="sxs-lookup"><span data-stu-id="e98b2-254">You can apply this policy tooany API operation.</span></span> <span data-ttu-id="e98b2-255">Hello [Внутренняя конфигурация для Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) предоставляет hello следующий запрос маршрутизации элементов управления:</span><span class="sxs-lookup"><span data-stu-id="e98b2-255">hello [backend configuration for Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) provides hello following request routing controls:</span></span> 
 - <span data-ttu-id="e98b2-256">Службы Выбор экземпляра путем указания имени экземпляра службы Service Fabric, либо жестко закодировано (например, `"fabric:/myapp/myservice"`) или создан из запроса hello HTTP (например, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span><span class="sxs-lookup"><span data-stu-id="e98b2-256">Service instance selection by specifying a Service Fabric service instance name, either hardcoded (for example, `"fabric:/myapp/myservice"`) or generated from hello HTTP request (for example, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span></span>
 - <span data-ttu-id="e98b2-257">Разрешение раздела путем создания ключа секции с помощью любой схемы секционирования Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e98b2-257">Partition resolution by generating a partition key using any Service Fabric partitioning scheme.</span></span>
 - <span data-ttu-id="e98b2-258">Выбор реплики для служб с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="e98b2-258">Replica selection for stateful services.</span></span>
 - <span data-ttu-id="e98b2-259">Разрешение повторите условия, которые позволяют вам toospecify условиям hello повторно разрешить расположение службы и снова отправить запрос.</span><span class="sxs-lookup"><span data-stu-id="e98b2-259">Resolution retry conditions that allow you toospecify hello conditions for re-resolving a service location and resending a request.</span></span>

<span data-ttu-id="e98b2-260">В этом учебнике создайте политику серверной маршруты напрямую запрашивает toohello ASP.NET Core службы без отслеживания состояния, развернутую ранее.</span><span class="sxs-lookup"><span data-stu-id="e98b2-260">For this tutorial, create a backend policy that routes requests directly toohello ASP.NET Core stateless service deployed earlier:</span></span>

 1. <span data-ttu-id="e98b2-261">Выберите и измените hello **входящих политики** для hello `Values` операции, щелкнув значок редактирования hello и затем выбрав **в представлении кода**.</span><span class="sxs-lookup"><span data-stu-id="e98b2-261">Select and edit hello **inbound policies** for hello `Values` operation by clicking hello edit icon, and then selecting **Code View**.</span></span>
 2. <span data-ttu-id="e98b2-262">В редакторе кода hello политики, добавьте `set-backend-service` политики в разделе входящих политики, как показано ниже и нажмите кнопку hello **Сохранить** кнопки:</span><span class="sxs-lookup"><span data-stu-id="e98b2-262">In hello policy code editor, add a `set-backend-service` policy under inbound policies as shown here and click hello **Save** button:</span></span>
    
    ```xml
    <policies>
      <inbound>
        <base/>
        <set-backend-service 
           backend-id="servicefabric"
           sf-service-instance-name="fabric:/ApiApplication/WebApiService"
           sf-resolve-condition="@((int)context.Response.StatusCode != 200)" />
      </inbound>
      <backend>
        <base/>
      </backend>
      <outbound>
        <base/>
      </outbound>
    </policies>
    ```

<span data-ttu-id="e98b2-263">Полный набор атрибутов Service Fabric внутренней политики, см. в разделе toohello [документации внутреннего интерфейса API управления](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span><span class="sxs-lookup"><span data-stu-id="e98b2-263">For a full set of Service Fabric back-end policy attributes, refer toohello [API Management back-end documentation](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span></span>

### <a name="add-hello-api-tooa-product"></a><span data-ttu-id="e98b2-264">Добавьте hello API tooa продукта.</span><span class="sxs-lookup"><span data-stu-id="e98b2-264">Add hello API tooa product.</span></span> 

<span data-ttu-id="e98b2-265">Перед вызовом hello API, его необходимо добавить tooa продукта, где вы можете предоставить доступ toousers.</span><span class="sxs-lookup"><span data-stu-id="e98b2-265">Before you can call hello API, it must be added tooa product where you can grant access toousers.</span></span> 

 1. <span data-ttu-id="e98b2-266">В hello службы управления API, выберите **продуктов - PREVIEW**.</span><span class="sxs-lookup"><span data-stu-id="e98b2-266">In hello API Management service, select **Products - PREVIEW**.</span></span>
 2. <span data-ttu-id="e98b2-267">По умолчанию служба управления API предоставляет два продукта: фиксированный и без ограничений.</span><span class="sxs-lookup"><span data-stu-id="e98b2-267">By default, API Management providers two products: Starter and Unlimited.</span></span> <span data-ttu-id="e98b2-268">Выберите продукт неограниченное hello.</span><span class="sxs-lookup"><span data-stu-id="e98b2-268">Select hello Unlimited product.</span></span>
 3. <span data-ttu-id="e98b2-269">Выберите API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="e98b2-269">Select APIs.</span></span>
 4. <span data-ttu-id="e98b2-270">Нажмите кнопку hello **+ добавить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="e98b2-270">Click hello **+ Add** button.</span></span>
 5. <span data-ttu-id="e98b2-271">Выберите hello `Service Fabric App` API, созданные в предыдущих шагах hello и нажмите кнопку hello **выберите** кнопки.</span><span class="sxs-lookup"><span data-stu-id="e98b2-271">Select hello `Service Fabric App` API you created in hello previous steps and click hello **Select** button.</span></span>

### <a name="test-it"></a><span data-ttu-id="e98b2-272">Тестирование</span><span class="sxs-lookup"><span data-stu-id="e98b2-272">Test it</span></span>

<span data-ttu-id="e98b2-273">Теперь можно попробовать передачу запроса tooyour внутренней службой в Service Fabric через API управления непосредственно из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e98b2-273">You can now try sending a request tooyour back-end service in Service Fabric through API Management directly from hello Azure portal.</span></span>

 1. <span data-ttu-id="e98b2-274">В hello службы управления API, выберите **API — Предварительная версия**.</span><span class="sxs-lookup"><span data-stu-id="e98b2-274">In hello API Management service, select **API - PREVIEW**.</span></span>
 2. <span data-ttu-id="e98b2-275">В hello `Service Fabric App` API, созданный на предыдущих шагах hello, выберите hello **тест** вкладки.</span><span class="sxs-lookup"><span data-stu-id="e98b2-275">In hello `Service Fabric App` API you created in hello previous steps, select hello **Test** tab.</span></span>
 3. <span data-ttu-id="e98b2-276">Нажмите кнопку hello **отправки** toosend кнопку toohello внутреннего тестирования запроса службы.</span><span class="sxs-lookup"><span data-stu-id="e98b2-276">Click hello **Send** button toosend a test request toohello backend service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e98b2-277">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e98b2-277">Next steps</span></span>

<span data-ttu-id="e98b2-278">На этом этапе базовая установка службы управления API и Service Fabric завершена.</span><span class="sxs-lookup"><span data-stu-id="e98b2-278">At this point, you should have a basic setup with Service Fabric and API Management.</span></span>

<span data-ttu-id="e98b2-279">Для вашего tooget кластера Service Fabric, которую можно быстро настроить в этом учебнике используется обычный пользователь на основе сертификатов проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="e98b2-279">This tutorial uses basic certificate-based user authentication for your Service Fabric cluster tooget you set up quickly.</span></span> <span data-ttu-id="e98b2-280">Расширенную аутентификацию пользователя для кластера Service Fabric лучше использовать с [аутентификацией Azure Active Directory](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span><span class="sxs-lookup"><span data-stu-id="e98b2-280">More advanced user authentication for your Service Fabric cluster is preferable with [Azure Active Directory authentication](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span></span> 

<span data-ttu-id="e98b2-281">Далее, [Создание и настройка расширенных параметров продукта в службе управления API Azure](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare приложения для трафика в реальном мире.</span><span class="sxs-lookup"><span data-stu-id="e98b2-281">Next, [create and configure advanced product settings in Azure API Management](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare your application for real world traffic.</span></span>

<!-- links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/

[network-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.json
[network-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.parameters.json

[apim-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.json
[apim-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.parameters.json

[cluster-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.json
[cluster-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.parameters.json


<!-- pics -->
[sf-apim-topology-overview]: ./media/service-fabric-api-management-quickstart/sf-apim-topology-overview.png
