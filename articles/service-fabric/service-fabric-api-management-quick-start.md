---
title: "Краткое руководство по управлению API и Azure Service Fabric | Документация Майкрософт"
description: "Это руководство поможет быстро начать работу со службой управления API Azure и Service Fabric."
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
ms.openlocfilehash: e9f44d8a43d274768f43261fea68f0da9c681ae1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="service-fabric-with-azure-api-management-quick-start"></a><span data-ttu-id="845a9-103">Краткое руководство по Service Fabric со службой управления API Azure</span><span class="sxs-lookup"><span data-stu-id="845a9-103">Service Fabric with Azure API Management Quick Start</span></span>

<span data-ttu-id="845a9-104">С помощью этого руководства вы узнаете, как настроить службу управления API Azure с Service Fabric, а также как настроить первую операцию API для отправки трафика к службам серверной части в Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="845a9-104">This guide shows you how to set up Azure API Management with Service Fabric and configure your first API operation to send traffic to back-end services in Service Fabric.</span></span> <span data-ttu-id="845a9-105">Дополнительные сведения о сценариях службы управления API Azure и Service Fabric см. в [обзорной статье](service-fabric-api-management-overview.md).</span><span class="sxs-lookup"><span data-stu-id="845a9-105">To learn more about Azure API Management scenarios with Service Fabric, see the [overview](service-fabric-api-management-overview.md) article.</span></span> 

## <a name="deploy-api-management-and-service-fabric-to-azure"></a><span data-ttu-id="845a9-106">Развертывание службы управления API и Service Fabric в Azure</span><span class="sxs-lookup"><span data-stu-id="845a9-106">Deploy API Management and Service Fabric to Azure</span></span>

<span data-ttu-id="845a9-107">Сначала необходимо развернуть службу управления API и кластер Service Fabric в Azure в общедоступной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="845a9-107">The first step is to deploy API Management and a Service Fabric cluster to Azure in a shared Virtual Network.</span></span> <span data-ttu-id="845a9-108">Это позволит службе управления API напрямую взаимодействовать с Service Fabric, что обеспечит обнаружение службы, разрешение раздела службы, а также перенаправление трафика прямо в любую внутреннюю службу в Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="845a9-108">This allows API Management to communicate directly with Service Fabric so it can perform service discovery, service partition resolution, and forward traffic directly to any backend service in Service Fabric.</span></span>

### <a name="topology"></a><span data-ttu-id="845a9-109">Топология</span><span class="sxs-lookup"><span data-stu-id="845a9-109">Topology</span></span>

<span data-ttu-id="845a9-110">В этом руководстве развертывается следующая топология в Azure, в которой служба управления API и Service Fabric находятся в подсетях одной виртуальной сети:</span><span class="sxs-lookup"><span data-stu-id="845a9-110">This guide deploys the following topology to Azure in which API Management and Service Fabric are in subnets of the same Virtual Network:</span></span>

 ![Рисунок][sf-apim-topology-overview]

<span data-ttu-id="845a9-112">Чтобы быстро приступить к работе, для каждого шага развертывания предоставляются шаблоны Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="845a9-112">To get started quickly, Resource Manager templates are provided for each deployment step:</span></span>

 - <span data-ttu-id="845a9-113">Топология сети:</span><span class="sxs-lookup"><span data-stu-id="845a9-113">Network topology:</span></span>
    - <span data-ttu-id="845a9-114">[network.json][network-arm]</span><span class="sxs-lookup"><span data-stu-id="845a9-114">[network.json][network-arm]</span></span>
    - <span data-ttu-id="845a9-115">[network.parameters.json][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="845a9-115">[network.parameters.json][network-parameters-arm]</span></span>
 - <span data-ttu-id="845a9-116">Кластер Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="845a9-116">Service Fabric cluster:</span></span>
    - <span data-ttu-id="845a9-117">[cluster.json][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="845a9-117">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="845a9-118">[cluster.parameters.json][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="845a9-118">[cluster.parameters.json][cluster-parameters-arm]</span></span>
 - <span data-ttu-id="845a9-119">Управление API</span><span class="sxs-lookup"><span data-stu-id="845a9-119">API Management:</span></span>
    - <span data-ttu-id="845a9-120">[apim.json][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="845a9-120">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="845a9-121">[apim.parameters.json][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="845a9-121">[apim.parameters.json][apim-parameters-arm]</span></span>

### <a name="sign-in-to-azure-and-select-your-subscription"></a><span data-ttu-id="845a9-122">Вход в Azure и выбор подписки</span><span class="sxs-lookup"><span data-stu-id="845a9-122">Sign in to Azure and select your subscription</span></span>

<span data-ttu-id="845a9-123">В этом руководстве используется [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="845a9-123">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="845a9-124">При запуске нового сеанса PowerShell войдите в свою учетную запись Azure и выберите подписку перед выполнением команд Azure.</span><span class="sxs-lookup"><span data-stu-id="845a9-124">When you start a new PowerShell session, sign in to your Azure account and select your subscription before you execute Azure commands.</span></span>
 
<span data-ttu-id="845a9-125">Вход в учетную запись Azure:</span><span class="sxs-lookup"><span data-stu-id="845a9-125">Sign in to your Azure account:</span></span>

```powershell
PS > Login-AzureRmAccount
```

<span data-ttu-id="845a9-126">Выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="845a9-126">Select your subscription:</span></span>

```powershell
PS > Get-AzureRmSubscription
PS > Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="create-a-resource-group"></a><span data-ttu-id="845a9-127">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="845a9-127">Create a resource group</span></span>

<span data-ttu-id="845a9-128">Создайте новую группу ресурсов для развертывания.</span><span class="sxs-lookup"><span data-stu-id="845a9-128">Create a new resource group for your deployment.</span></span> <span data-ttu-id="845a9-129">Назначьте ей имя и расположение.</span><span class="sxs-lookup"><span data-stu-id="845a9-129">Give it a name and a location.</span></span>

```powershell
PS > New-AzureRmResourceGroup -Name <my-resource-group> -Location westus
```

### <a name="deploy-the-network-topology"></a><span data-ttu-id="845a9-130">Развертывание топологии сети</span><span class="sxs-lookup"><span data-stu-id="845a9-130">Deploy the network topology</span></span>

<span data-ttu-id="845a9-131">Сначала необходимо настроить топологию сети, в которой будут развернуты служба управления API и кластер Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="845a9-131">The first step is to set up the network topology to which API Management and the Service Fabric cluster will be deployed.</span></span> <span data-ttu-id="845a9-132">Шаблон Resource Manager [network.json][network-arm] настроен на создание виртуальной сети (VNET) с двумя подсетями и двумя группами безопасности сети (NSG).</span><span class="sxs-lookup"><span data-stu-id="845a9-132">The [network.json][network-arm] Resource Manager template is configured to create a Virtual Network (VNET) with two subnets and two Network Security Groups (NSG).</span></span> 

<span data-ttu-id="845a9-133">Файл параметров [network.parameters.json][network-parameters-arm] содержит имена подсетей и групп безопасности сети, в которых будут развернуты служба управления API и Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="845a9-133">The [network.parameters.json][network-parameters-arm] parameters file contains the names of the subnets and NSGs that API Management and Service Fabric will be deployed to.</span></span> <span data-ttu-id="845a9-134">В рамках этого руководства изменять значения параметров не нужно.</span><span class="sxs-lookup"><span data-stu-id="845a9-134">For this guide, the parameter values do not need to be changed.</span></span> <span data-ttu-id="845a9-135">Шаблоны Resource Manager управления API и Service Fabric используют эти значения, поэтому если их изменить, вам придется их также изменить в других шаблонах Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="845a9-135">The API Management and Service Fabric Resource Manager templates use these values, so if they are modified here, you must modify them in the other Resource Manager templates accordingly.</span></span> 

 1. <span data-ttu-id="845a9-136">Скачайте шаблон Resource Manager и файл параметров:</span><span class="sxs-lookup"><span data-stu-id="845a9-136">Download the following Resource Manager template and parameters file:</span></span>

    - <span data-ttu-id="845a9-137">[network.json][network-arm]</span><span class="sxs-lookup"><span data-stu-id="845a9-137">[network.json][network-arm]</span></span>
    - <span data-ttu-id="845a9-138">[network.parameters.json][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="845a9-138">[network.parameters.json][network-parameters-arm]</span></span>

 2. <span data-ttu-id="845a9-139">Используйте следующую команду PowerShell для развертывания шаблона Resource Manager и файла параметров для настройки сети:</span><span class="sxs-lookup"><span data-stu-id="845a9-139">Use the following PowerShell command to deploy the Resource Manager template and parameter files for the network setup:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\network.json -TemplateParameterFile .\network.parameters.json -Verbose
    ```

### <a name="deploy-the-service-fabric-cluster"></a><span data-ttu-id="845a9-140">Развертывание кластера Service Fabric</span><span class="sxs-lookup"><span data-stu-id="845a9-140">Deploy the Service Fabric cluster</span></span>

<span data-ttu-id="845a9-141">Когда сетевые ресурсы развернуты, необходимо развернуть кластер Service Fabric в виртуальной сети в подсети и группе безопасности сети, используемых для кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="845a9-141">Once the network resources have finished deploying, the next step is to deploy a Service Fabric cluster to the VNET in the subnet and NSG designated for the Service Fabric cluster.</span></span> <span data-ttu-id="845a9-142">В рамках этого руководства шаблон Resource Manager Service Fabric предварительно настроен на использование имен виртуальной сети, подсети и группы безопасности сети, настроенных на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="845a9-142">For this tutorial, the Service Fabric Resource Manager template is pre-configured to use the names of the VNET, subnet, and NSG that you set up in the previous step.</span></span> 

<span data-ttu-id="845a9-143">Шаблон Resource Manager кластера Service Fabric настроен для создания безопасного кластера с сертификатом безопасности.</span><span class="sxs-lookup"><span data-stu-id="845a9-143">The Service Fabric cluster Resource Manager template is configured to create a secure cluster with certificate security.</span></span> <span data-ttu-id="845a9-144">Сертификат используется, чтобы обеспечить для кластера безопасный обмен данными между узлами, а также чтобы управлять доступом пользователя к кластеру Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="845a9-144">The certificate is used to secure node-to-node communication for your cluster and to manage user access to your Service Fabric cluster.</span></span> <span data-ttu-id="845a9-145">Управление API использует этот сертификат, чтобы получить доступ к службе именования Service Fabric для ее обнаружения.</span><span class="sxs-lookup"><span data-stu-id="845a9-145">API Management uses this certificate to access  the Service Fabric Naming Service for service discovery.</span></span>

<span data-ttu-id="845a9-146">Этот шаг требует наличия сертификата в Key Vault для обеспечения безопасности кластера.</span><span class="sxs-lookup"><span data-stu-id="845a9-146">This step requires having a certificate in Key Vault for cluster security.</span></span> <span data-ttu-id="845a9-147">Дополнительные сведения о настройке безопасного кластера с помощью Key Vault см. в статье [Создание кластера Service Fabric в Azure с помощью Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="845a9-147">For more information on setting up a secure cluster with Key Vault, see [this guide on creating a cluster in Azure using Resource Manager](service-fabric-cluster-creation-via-arm.md)</span></span>

> [!NOTE]
> <span data-ttu-id="845a9-148">Вы можете добавить аутентификацию Azure Active Directory (кроме сертификата, используемого для доступа к кластеру).</span><span class="sxs-lookup"><span data-stu-id="845a9-148">You may add Azure Active Directory authentication in addition to the certificate used for cluster access.</span></span> <span data-ttu-id="845a9-149">Azure Active Directory — рекомендуемый, но не обязательный для этого руководства способ управления доступом пользователя к кластеру Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="845a9-149">Azure Active Directory is the recommended way to manage user access to your Service Fabric cluster, but is not necessary to complete this tutorial.</span></span> <span data-ttu-id="845a9-150">Сертификат является обязательным для обеспечения безопасности кластера при обмене данными между узлами, а также для аутентификации службы управления API Azure, которая в настоящее время не поддерживает аутентификацию с помощью Azure Active Directory для серверной части Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="845a9-150">A certificate is required either way for cluster node-to-node security and for Azure API Management authentication, which currently does not support authenticating with Azure Active Directory for a Service Fabric backend.</span></span>

 1. <span data-ttu-id="845a9-151">Скачайте шаблон Resource Manager и файл параметров:</span><span class="sxs-lookup"><span data-stu-id="845a9-151">Download the following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="845a9-152">[cluster.json][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="845a9-152">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="845a9-153">[cluster.parameters.json][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="845a9-153">[cluster.parameters.json][cluster-parameters-arm]</span></span>

 2. <span data-ttu-id="845a9-154">Заполните пустые параметры в файле `cluster.parameters.json` для развертывания, включая [сведения о Key Vault](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) для сертификата кластера.</span><span class="sxs-lookup"><span data-stu-id="845a9-154">Fill in the empty parameters in the `cluster.parameters.json` file for your deployment, including the [Key Vault information](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) for your cluster certificate.</span></span>

 3. <span data-ttu-id="845a9-155">Используйте следующую команду PowerShell для развертывания шаблона Resource Manager и файла параметров для создания кластера Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="845a9-155">Use the following PowerShell command to deploy the Resource Manager template and parameter files to create the Service Fabric cluster:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\cluster.json -TemplateParameterFile .\cluster.parameters.json -Verbose
    ```

### <a name="deploy-api-management"></a><span data-ttu-id="845a9-156">Развертывание управления API</span><span class="sxs-lookup"><span data-stu-id="845a9-156">Deploy API Management</span></span>

<span data-ttu-id="845a9-157">Наконец можно развернуть управление API в виртуальной сети в подсети и группе безопасности сети, настроенных для управления API.</span><span class="sxs-lookup"><span data-stu-id="845a9-157">Finally, deploy API Management to the VNET in the subnet and NSG designated for API Management.</span></span> <span data-ttu-id="845a9-158">Для развертывания управления API вам не нужно ждать, пока завершится развертывание кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="845a9-158">You do not need to wait for the Service Fabric cluster deployment to finish before deploying API Management.</span></span> 

<span data-ttu-id="845a9-159">В рамках этого руководства шаблон Resource Manager управления API предварительно настроен на использование имен виртуальной сети, подсети и группы безопасности сети, настроенных на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="845a9-159">For this tutorial, the API Management Resource Manager template is pre-configured to use the names of the VNET, subnet, and NSG that you set up in the previous step.</span></span> 

 1. <span data-ttu-id="845a9-160">Скачайте шаблон Resource Manager и файл параметров:</span><span class="sxs-lookup"><span data-stu-id="845a9-160">Download the following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="845a9-161">[apim.json][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="845a9-161">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="845a9-162">[apim.parameters.json][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="845a9-162">[apim.parameters.json][apim-parameters-arm]</span></span>

 2. <span data-ttu-id="845a9-163">Заполните пустые параметры в файле `apim.parameters.json` для развертывания.</span><span class="sxs-lookup"><span data-stu-id="845a9-163">Fill in the empty parameters in the `apim.parameters.json` for your deployment.</span></span>

 3. <span data-ttu-id="845a9-164">Используйте следующую команду PowerShell для развертывания шаблона Resource Manager и файла параметров для управления API:</span><span class="sxs-lookup"><span data-stu-id="845a9-164">Use the following PowerShell command to deploy the Resource Manager template and parameter files for API Management:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\apim.json -TemplateParameterFile .\apim.parameters.json -Verbose
    ```

## <a name="configure-api-management"></a><span data-ttu-id="845a9-165">Настройка управления API</span><span class="sxs-lookup"><span data-stu-id="845a9-165">Configure API Management</span></span>

<span data-ttu-id="845a9-166">После развертывания кластера Service Fabric и управления API можно настроить серверную часть Service Fabric в службе управления API.</span><span class="sxs-lookup"><span data-stu-id="845a9-166">Once your API Management and Service Fabric cluster are deployed, you can configure a Service Fabric backend in API Management.</span></span> <span data-ttu-id="845a9-167">Это позволит создать политику внутренней службы, которая отправляет трафик в кластер Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="845a9-167">This allows you to create a backend service policy that sends traffic to your Service Fabric cluster.</span></span>

### <a name="api-management-security"></a><span data-ttu-id="845a9-168">Безопасность управления API</span><span class="sxs-lookup"><span data-stu-id="845a9-168">API Management Security</span></span>

<span data-ttu-id="845a9-169">Чтобы настроить серверную часть Service Fabric, сначала необходимо настроить параметры безопасности управления API.</span><span class="sxs-lookup"><span data-stu-id="845a9-169">To configure the Service Fabric backend, you first need to configure API Management security settings.</span></span> <span data-ttu-id="845a9-170">Чтобы настроить параметры безопасности, перейдите в службу управления API на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="845a9-170">To configure security settings, go to your API Management service in the Azure portal.</span></span>

#### <a name="enable-the-api-management-rest-api"></a><span data-ttu-id="845a9-171">Включение REST API службы управления API</span><span class="sxs-lookup"><span data-stu-id="845a9-171">Enable the API Management REST API</span></span>

<span data-ttu-id="845a9-172">В настоящее время REST API службы управления API является единственным способом настроить внутреннюю службу.</span><span class="sxs-lookup"><span data-stu-id="845a9-172">The API Management REST API is currently the only way to configure a backend service.</span></span> <span data-ttu-id="845a9-173">Сначала нужно включить REST API службы управления API и обеспечить ее безопасность.</span><span class="sxs-lookup"><span data-stu-id="845a9-173">The first step is to enable the API Management REST API and secure it.</span></span>

 1. <span data-ttu-id="845a9-174">В службе управления API выберите **Management API - PREVIEW** (API управления (предварительная версия)) в разделе **Безопасность**.</span><span class="sxs-lookup"><span data-stu-id="845a9-174">In the API Management service, select **Management API - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="845a9-175">Установите флажок для параметра **включения REST API службы управления API**.</span><span class="sxs-lookup"><span data-stu-id="845a9-175">Check the **Enable API Management REST API** checkbox.</span></span>
 3. <span data-ttu-id="845a9-176">Запишите URL-адрес API управления. Мы используем его позже для настройки внутренней службы Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="845a9-176">Note the Management API URL - this is the URL we'll use later to set up the Service Fabric backend</span></span>
 4. <span data-ttu-id="845a9-177">Создайте **маркер доступа**, выбрав дату окончания действия и ключ, а затем нажмите кнопку **Создать** в нижней области страницы.</span><span class="sxs-lookup"><span data-stu-id="845a9-177">Generate an **access Token** by selecting an expiry date and a key, then click the **Generate** button toward the bottom of the page.</span></span>
 5. <span data-ttu-id="845a9-178">Скопируйте **маркер доступа** и сохраните его (он нам понадобится дальше).</span><span class="sxs-lookup"><span data-stu-id="845a9-178">Copy the **access token** and save it - we'll use this in the following steps.</span></span> <span data-ttu-id="845a9-179">Обратите внимание, что он отличается от первичного и вторичного ключа.</span><span class="sxs-lookup"><span data-stu-id="845a9-179">Note this is different from the primary key and secondary key.</span></span>

#### <a name="upload-a-service-fabric-client-certificate"></a><span data-ttu-id="845a9-180">Отправка клиентского сертификата Service Fabric</span><span class="sxs-lookup"><span data-stu-id="845a9-180">Upload a Service Fabric client certificate</span></span>

<span data-ttu-id="845a9-181">Управление API должно пройти аутентификацию с помощью кластера Service Fabric для обнаружения службы с помощью сертификата клиента, у которого есть доступ к кластеру.</span><span class="sxs-lookup"><span data-stu-id="845a9-181">API Management must authenticate with your Service Fabric cluster for service discovery using a client certificate that has access to your cluster.</span></span> <span data-ttu-id="845a9-182">Для удобства в этом руководстве используется тот же сертификат, указанный при создании кластера Service Fabric, который по умолчанию может использоваться для доступа к кластеру.</span><span class="sxs-lookup"><span data-stu-id="845a9-182">For simplicity, this tutorial uses the same certificate specified when creating the Service Fabric cluster, which by default can be used to access your cluster.</span></span>

 1. <span data-ttu-id="845a9-183">В службе управления API выберите **Client certificates - PREVIEW** (Сертификаты клиента (предварительная версия)) в разделе **Безопасность**.</span><span class="sxs-lookup"><span data-stu-id="845a9-183">In the API Management service, select **Client certificates - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="845a9-184">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="845a9-184">Click the **+ Add** button</span></span>
 2. <span data-ttu-id="845a9-185">Выберите файл закрытого ключа (PFX-файл) сертификата кластера, указанного при создании кластера Service Fabric, присвойте ему имя и укажите пароль для закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="845a9-185">Select the private key file (.pfx) of the cluster certificate that you specified when creating your Service Fabric cluster, give it a name, and provide the private key password.</span></span>

> [!NOTE]
> <span data-ttu-id="845a9-186">В этом руководстве используется один сертификат для аутентификации клиента и безопасности обмена данными между узлами кластера.</span><span class="sxs-lookup"><span data-stu-id="845a9-186">This tutorial uses the same certificate for client authentication and cluster node-to-node security.</span></span> <span data-ttu-id="845a9-187">Вы можете использовать отдельный сертификат клиента, если у вас есть сертификат, настроенный для доступа к кластеру Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="845a9-187">You may use a separate client certificate if you have one configured to access your Service Fabric cluster.</span></span>

### <a name="configure-the-backend"></a><span data-ttu-id="845a9-188">Настройка внутренней службы</span><span class="sxs-lookup"><span data-stu-id="845a9-188">Configure the backend</span></span>

<span data-ttu-id="845a9-189">Теперь, когда безопасность управления API настроена, можно настроить внутреннюю службу Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="845a9-189">Now that API Management security is configured, you can configure the Service Fabric backend.</span></span> <span data-ttu-id="845a9-190">Для серверных систем кластер Service Fabric представляет собой внутреннюю службу, а не определенную службу Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="845a9-190">For Service Fabric backends, the Service Fabric cluster is the backend, rather than a specific Service Fabric service.</span></span> <span data-ttu-id="845a9-191">Это позволяет направлять политике запросы не в одну службу в кластере, а в несколько.</span><span class="sxs-lookup"><span data-stu-id="845a9-191">This allows a single policy to route to more than one service in the cluster.</span></span>

<span data-ttu-id="845a9-192">Этот шаг требует созданный ранее маркер доступа, а также отпечаток сертификата кластера, загруженный в службу управления API на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="845a9-192">This step requires the access token you generated earlier and the thumbprint for your cluster certificate you uploaded to API Management in the previous step.</span></span>

> [!NOTE]
> <span data-ttu-id="845a9-193">Если вы использовали отдельный клиентский сертификат на предыдущем шаге для управления API, на этом шаге вам потребуется отпечаток сертификата клиента в дополнение к отпечатку сертификата кластера.</span><span class="sxs-lookup"><span data-stu-id="845a9-193">If you used a separate client certificate in the previous step for API Management, you need the thumbprint for the client certificate in addition to the cluster certificate thumbprint in this step.</span></span>

<span data-ttu-id="845a9-194">Отправьте следующий HTTP-запрос PUT на URL-адрес API службы управления API, записанный ранее при включении REST API для службы управления API, для настройки внутренней службы Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="845a9-194">Send the following HTTP PUT request to the API Management API URL you noted earlier when enabling the API Management REST API to configure the Service Fabric backend service.</span></span> <span data-ttu-id="845a9-195">При успешном выполнении команды вы увидите ответ `HTTP 201 Created`.</span><span class="sxs-lookup"><span data-stu-id="845a9-195">You should see an `HTTP 201 Created` response when the command succeeds.</span></span> <span data-ttu-id="845a9-196">Дополнительные сведения о каждом свойстве серверной части см. в [справочной документации по API для серверной части](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span><span class="sxs-lookup"><span data-stu-id="845a9-196">For more information on each field, see the API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span></span>

<span data-ttu-id="845a9-197">Команда HTTP и URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="845a9-197">HTTP command and URL:</span></span>
```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
```

<span data-ttu-id="845a9-198">Заголовки запроса:</span><span class="sxs-lookup"><span data-stu-id="845a9-198">Request headers:</span></span>
```http
Authorization: SharedAccessSignature <your access token>
Content-Type: application/json
```

<span data-ttu-id="845a9-199">Тело запроса:</span><span class="sxs-lookup"><span data-stu-id="845a9-199">Request body:</span></span>
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

<span data-ttu-id="845a9-200">Параметр **URL-адреса** здесь представляет полное доменное имя службы в кластере, куда все запросы направляются по умолчанию, если во внутренней политике не указано имя службы.</span><span class="sxs-lookup"><span data-stu-id="845a9-200">The **url** parameter here is a fully-qualified service name of a service in your cluster that all requests are routed to by default if no service name is specified in a backend policy.</span></span> <span data-ttu-id="845a9-201">Вы можете использовать фиктивное имя службы, например "fabric:/fake/service", если вам не нужна резервная служба.</span><span class="sxs-lookup"><span data-stu-id="845a9-201">You may use a fake service name, such as "fabric:/fake/service" if you do not intend to have a fallback service.</span></span>

<span data-ttu-id="845a9-202">Дополнительные сведения о каждом свойстве серверной части см. в [справочной документации по API для серверной части](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span><span class="sxs-lookup"><span data-stu-id="845a9-202">Refer to the API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) for more details on each field.</span></span>

#### <a name="example"></a><span data-ttu-id="845a9-203">Пример</span><span class="sxs-lookup"><span data-stu-id="845a9-203">Example</span></span>

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

## <a name="deploy-a-service-fabric-back-end-service"></a><span data-ttu-id="845a9-204">Развертывание внутренней службы Service Fabric</span><span class="sxs-lookup"><span data-stu-id="845a9-204">Deploy a Service Fabric back-end service</span></span>

<span data-ttu-id="845a9-205">Теперь, когда Service Fabric настроена в качестве серверной части управления API, можно создать внутренние политики для API-интерфейсов, отправляющие трафик в службы Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="845a9-205">Now that you have the Service Fabric configured as a backend to API Management, you can author backend policies for your APIs that send traffic to your Service Fabric services.</span></span> <span data-ttu-id="845a9-206">Но сначала вам потребуется служба, работающая в Service Fabric, чтобы принимать запросы.</span><span class="sxs-lookup"><span data-stu-id="845a9-206">But first you need a service running in Service Fabric to accept requests.</span></span>

### <a name="create-a-service-fabric-service-with-an-http-endpoint"></a><span data-ttu-id="845a9-207">Создание службы Service Fabric с конечной точкой HTTP</span><span class="sxs-lookup"><span data-stu-id="845a9-207">Create a Service Fabric service with an HTTP endpoint</span></span>

<span data-ttu-id="845a9-208">В рамках этого руководства мы создадим базовую надежную службу ASP.NET Core без отслеживания состояния с помощью шаблона проекта веб-API по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="845a9-208">For this tutorial, we'll create a basic stateless ASP.NET Core Reliable Service using the default Web API project template.</span></span> <span data-ttu-id="845a9-209">Так мы получим конечную точку HTTP для службы, которую можно будет использовать через службу управления API Azure:</span><span class="sxs-lookup"><span data-stu-id="845a9-209">This creates an HTTP endpoint for your service, which you'll expose through Azure API Management:</span></span>

```
/api/values
```

<span data-ttu-id="845a9-210">Ознакомьтесь с разделом о [настройке среды разработки для разработки ASP.NET Core](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span><span class="sxs-lookup"><span data-stu-id="845a9-210">Start by [setting up your development environment for ASP.NET Core development](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span></span>

<span data-ttu-id="845a9-211">После настройки среды разработки запустите Visual Studio от имени администратора и создайте службу ASP.NET Core:</span><span class="sxs-lookup"><span data-stu-id="845a9-211">Once your development environment is set up, start Visual Studio as Administrator and create an ASP.NET Core service:</span></span>

 1. <span data-ttu-id="845a9-212">В Visual Studio выберите последовательно «Файл» -> «Создать проект».</span><span class="sxs-lookup"><span data-stu-id="845a9-212">In Visual Studio, select File -> New Project.</span></span>
 2. <span data-ttu-id="845a9-213">Выберите шаблон приложения Service Fabric в облаке и присвойте ему имя **ApiApplication**.</span><span class="sxs-lookup"><span data-stu-id="845a9-213">Select the Service Fabric Application template under Cloud and name it **"ApiApplication"**.</span></span>
 3. <span data-ttu-id="845a9-214">Выберите шаблон службы ASP.NET Core и назовите проект **WebApiService**.</span><span class="sxs-lookup"><span data-stu-id="845a9-214">Select the ASP.NET Core service template and name the project **"WebApiService"**.</span></span>
 4. <span data-ttu-id="845a9-215">Выберите шаблон проекта ASP.NET Core 1.1 для веб-API.</span><span class="sxs-lookup"><span data-stu-id="845a9-215">Select the Web API ASP.NET Core 1.1 project template.</span></span>
 5. <span data-ttu-id="845a9-216">После создания проекта откройте файл `PackageRoot\ServiceManifest.xml` и удалите атрибут `Port` из конфигурации ресурса конечной точки:</span><span class="sxs-lookup"><span data-stu-id="845a9-216">Once the project is created, open `PackageRoot\ServiceManifest.xml` and remove the `Port` attribute from the endpoint resource configuration:</span></span>
 
    ```xml
    <Resources>
      <Endpoints>
        <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" />
      </Endpoints>
    </Resources>
    ```

    <span data-ttu-id="845a9-217">Это позволит Service Fabric динамически указать порт из диапазона портов приложения, который мы открыли через группу безопасности сети в шаблоне Resource Manager кластера, позволяя направлять к нему трафик из службы управления API.</span><span class="sxs-lookup"><span data-stu-id="845a9-217">This allows Service Fabric to specify a port dynamically from the application port range, which we opened through the Network Security Group in the cluster Resource Manager template, allowing traffic to flow to it from API Management.</span></span>
 
 6. <span data-ttu-id="845a9-218">Нажмите клавишу F5 в Visual Studio, чтобы убедиться, что веб-API доступен локально.</span><span class="sxs-lookup"><span data-stu-id="845a9-218">Press F5 in Visual Studio to verify the web API is available locally.</span></span> 

    <span data-ttu-id="845a9-219">Откройте Service Fabric Explorer и просмотрите подробные сведения об определенном экземпляре службы ASP.NET Core, чтобы увидеть базовый адрес, который прослушивает служба.</span><span class="sxs-lookup"><span data-stu-id="845a9-219">Open Service Fabric Explorer and drill down to a specific instance of the ASP.NET Core service to see the base address the service is listening on.</span></span> <span data-ttu-id="845a9-220">Добавьте `/api/values` в базовый адрес и откройте его в браузере.</span><span class="sxs-lookup"><span data-stu-id="845a9-220">Add `/api/values` to the base address and open it in a browser.</span></span> <span data-ttu-id="845a9-221">При этом будет вызван метод Get объекта ValuesController в шаблоне веб-API.</span><span class="sxs-lookup"><span data-stu-id="845a9-221">This invokes the Get method on the ValuesController in the Web API template.</span></span> <span data-ttu-id="845a9-222">Он вернет ответ по умолчанию, предоставленный шаблоном, — массив JSON, который содержит две строки:</span><span class="sxs-lookup"><span data-stu-id="845a9-222">It returns the default response that is provided by the template, a JSON array that contains two strings:</span></span>

    ```json
    ["value1", "value2"]`
    ```

    <span data-ttu-id="845a9-223">Это конечная точка, которую вы предоставите через службу управления API в Azure.</span><span class="sxs-lookup"><span data-stu-id="845a9-223">This is the endpoint that you'll expose through API Management in Azure.</span></span>

 7. <span data-ttu-id="845a9-224">Теперь вы можете развернуть приложение в кластере в Azure.</span><span class="sxs-lookup"><span data-stu-id="845a9-224">Finally, deploy the application to your cluster in Azure.</span></span> <span data-ttu-id="845a9-225">**В Visual Studio** щелкните правой кнопкой мыши проект приложения и выберите [Опубликовать](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box).</span><span class="sxs-lookup"><span data-stu-id="845a9-225">[Using Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), right-click the Application project and select **Publish**.</span></span> <span data-ttu-id="845a9-226">Укажите конечную точку кластера (например, `mycluster.westus.cloudapp.azure.com:19000`) для развертывания приложения в кластер Service Fabric в Azure.</span><span class="sxs-lookup"><span data-stu-id="845a9-226">Provide your cluster endpoint (for example, `mycluster.westus.cloudapp.azure.com:19000`) to deploy the application to your Service Fabric cluster in Azure.</span></span>

<span data-ttu-id="845a9-227">В кластере Service Fabric в Azure должна запуститься служба ASP.NET Core без отслеживания состояния с именем `fabric:/ApiApplication/WebApiService`.</span><span class="sxs-lookup"><span data-stu-id="845a9-227">An ASP.NET Core stateless service named `fabric:/ApiApplication/WebApiService` should now be running in your Service Fabric cluster in Azure.</span></span>

## <a name="create-an-api-operation"></a><span data-ttu-id="845a9-228">Создание операции API</span><span class="sxs-lookup"><span data-stu-id="845a9-228">Create an API operation</span></span>

<span data-ttu-id="845a9-229">Теперь все готово для создания операции в службе управления API, которую внешние клиенты могут использовать для взаимодействия со службой ASP.NET Core без отслеживания состояния, выполняющейся в кластере Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="845a9-229">Now we're ready to create an operation in API Management that external clients use to communicate with the ASP.NET Core stateless service running in the Service Fabric cluster.</span></span>

 1. <span data-ttu-id="845a9-230">Войдите на портал Azure и перейдите к развертыванию службы управления API.</span><span class="sxs-lookup"><span data-stu-id="845a9-230">Log in to the Azure portal and navigate to your API Management service deployment.</span></span>
 2. <span data-ttu-id="845a9-231">В колонке службы управления API выберите **API-интерфейсы (ПРЕДВАРИТЕЛЬНАЯ ВЕРСИЯ)**.</span><span class="sxs-lookup"><span data-stu-id="845a9-231">In the API Management service blade, select **APIs - Preview**</span></span>
 3. <span data-ttu-id="845a9-232">Добавьте новый API, щелкнув поле **Blank API** (Пустой API) и заполнив следующие параметры диалогового окна:</span><span class="sxs-lookup"><span data-stu-id="845a9-232">Add a new API by clicking the **Blank API** box and filling out the dialog box:</span></span>

     - <span data-ttu-id="845a9-233">**URL-адрес веб-службы**: для серверных систем Service Fabric это значение URL-адреса не используется.</span><span class="sxs-lookup"><span data-stu-id="845a9-233">**Web service URL**: For Service Fabric backends, this URL value is not used.</span></span> <span data-ttu-id="845a9-234">Здесь вы можете использовать любое значение.</span><span class="sxs-lookup"><span data-stu-id="845a9-234">You can put any value here.</span></span> <span data-ttu-id="845a9-235">В рамках этого руководства используйте `http://servicefabric`.</span><span class="sxs-lookup"><span data-stu-id="845a9-235">For this tutorial, use: `http://servicefabric`.</span></span>
     - <span data-ttu-id="845a9-236">**Имя**: укажите любое имя для API.</span><span class="sxs-lookup"><span data-stu-id="845a9-236">**Name**: Provide any name for your API.</span></span> <span data-ttu-id="845a9-237">В рамках этого руководства используйте `Service Fabric App`.</span><span class="sxs-lookup"><span data-stu-id="845a9-237">For this tutorial, use `Service Fabric App`.</span></span>
     - <span data-ttu-id="845a9-238">**Схема URL-адреса**: выберите HTTP, HTTPS или оба варианта.</span><span class="sxs-lookup"><span data-stu-id="845a9-238">**URL scheme**: Select either HTTP, HTTPS, or both.</span></span> <span data-ttu-id="845a9-239">В рамках этого руководства используйте `both`.</span><span class="sxs-lookup"><span data-stu-id="845a9-239">For this tutorial, use `both`.</span></span>
     - <span data-ttu-id="845a9-240">**API URL Suffix** (Суффикс URL-адреса API): укажите суффикс для API.</span><span class="sxs-lookup"><span data-stu-id="845a9-240">**API URL Suffix**: Provide a suffix for our API.</span></span> <span data-ttu-id="845a9-241">В рамках этого руководства используйте `myapp`.</span><span class="sxs-lookup"><span data-stu-id="845a9-241">For this tutorial, use `myapp`.</span></span>
 
 4. <span data-ttu-id="845a9-242">После создания API щелкните **Добавить операцию**, чтобы добавить интерфейсную операцию API.</span><span class="sxs-lookup"><span data-stu-id="845a9-242">Once the API is created, click **+ Add operation** to add a front-end API operation.</span></span> <span data-ttu-id="845a9-243">Заполните следующие значения:</span><span class="sxs-lookup"><span data-stu-id="845a9-243">Fill out the values:</span></span>
    
     - <span data-ttu-id="845a9-244">**URL-адрес**: выберите `GET` и укажите URL-адрес для API.</span><span class="sxs-lookup"><span data-stu-id="845a9-244">**URL**: Select `GET` and provide a URL path for the API.</span></span> <span data-ttu-id="845a9-245">В рамках этого руководства используйте `/api/values`.</span><span class="sxs-lookup"><span data-stu-id="845a9-245">For this tutorial, use `/api/values`.</span></span>
     
       <span data-ttu-id="845a9-246">По умолчанию указанный здесь URL-адрес представляет собой URL-адрес, отправленный во внутреннюю службу Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="845a9-246">By default, the URL path specified here is the URL path sent to the backend Service Fabric service.</span></span> <span data-ttu-id="845a9-247">Если вы здесь используете тот же URL-адрес, что и служба (в этом случае `/api/values`), тогда операция будет работать без изменений.</span><span class="sxs-lookup"><span data-stu-id="845a9-247">If you use the same URL path here that your service uses, in this case `/api/values`, then the operation works without further modification.</span></span> <span data-ttu-id="845a9-248">Вы также можете указать здесь URL-адрес, отличный от URL-адреса, используемого внутренней службой Service Fabric. В этом случае вам позже нужно будет указать перезапись пути в политике операции.</span><span class="sxs-lookup"><span data-stu-id="845a9-248">You may also specify a URL path here that is different from the URL path used by your backend Service Fabric service, in which case you will also need to specify a path rewrite in your operation policy later.</span></span>
     - <span data-ttu-id="845a9-249">**Отображаемое имя**: укажите любое имя для API.</span><span class="sxs-lookup"><span data-stu-id="845a9-249">**Display name**: Provide any name for the API.</span></span> <span data-ttu-id="845a9-250">В рамках этого руководства используйте `Values`.</span><span class="sxs-lookup"><span data-stu-id="845a9-250">For this tutorial, use `Values`.</span></span>

## <a name="configure-a-backend-policy"></a><span data-ttu-id="845a9-251">Настройка внутренней политики</span><span class="sxs-lookup"><span data-stu-id="845a9-251">Configure a backend policy</span></span>

<span data-ttu-id="845a9-252">Внутренняя политика необходима для связи.</span><span class="sxs-lookup"><span data-stu-id="845a9-252">The backend policy ties everything together.</span></span> <span data-ttu-id="845a9-253">Она требуется при настройке внутренней службы Service Fabric, в которую направляются запросы.</span><span class="sxs-lookup"><span data-stu-id="845a9-253">This is where you configure the backend Service Fabric service to which requests are routed.</span></span> <span data-ttu-id="845a9-254">Вы можете применить эту политику к любой API-операции.</span><span class="sxs-lookup"><span data-stu-id="845a9-254">You can apply this policy to any API operation.</span></span> <span data-ttu-id="845a9-255">[Конфигурация серверной части для Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) предоставляет следующие элементы управления маршрутизации запросов:</span><span class="sxs-lookup"><span data-stu-id="845a9-255">The [backend configuration for Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) provides the following request routing controls:</span></span> 
 - <span data-ttu-id="845a9-256">Выбор экземпляра службы с помощью указания имени экземпляра службы Service Fabric. Оно может быть жестко запрограммированным (например, `"fabric:/myapp/myservice"`) или созданным с помощью HTTP-запроса (например, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span><span class="sxs-lookup"><span data-stu-id="845a9-256">Service instance selection by specifying a Service Fabric service instance name, either hardcoded (for example, `"fabric:/myapp/myservice"`) or generated from the HTTP request (for example, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span></span>
 - <span data-ttu-id="845a9-257">Разрешение раздела путем создания ключа секции с помощью любой схемы секционирования Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="845a9-257">Partition resolution by generating a partition key using any Service Fabric partitioning scheme.</span></span>
 - <span data-ttu-id="845a9-258">Выбор реплики для служб с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="845a9-258">Replica selection for stateful services.</span></span>
 - <span data-ttu-id="845a9-259">Условия, при которых разрешение выполняется повторно, что позволяет указать условия для повторного разрешения расположения службы и повторной отправки запроса.</span><span class="sxs-lookup"><span data-stu-id="845a9-259">Resolution retry conditions that allow you to specify the conditions for re-resolving a service location and resending a request.</span></span>

<span data-ttu-id="845a9-260">В рамках этого руководства создайте внутреннюю политику, направляющую запросы напрямую в ранее развернутую службу ASP.NET Core без отслеживания состояния.</span><span class="sxs-lookup"><span data-stu-id="845a9-260">For this tutorial, create a backend policy that routes requests directly to the ASP.NET Core stateless service deployed earlier:</span></span>

 1. <span data-ttu-id="845a9-261">Выберите и измените **входящие политики** для операции `Values`. Для этого щелкните значок редактирования, а затем выберите **Просмотр кода**.</span><span class="sxs-lookup"><span data-stu-id="845a9-261">Select and edit the **inbound policies** for the `Values` operation by clicking the edit icon, and then selecting **Code View**.</span></span>
 2. <span data-ttu-id="845a9-262">В редакторе кода политики добавьте политику `set-backend-service` в раздел входящих политик, как показано ниже, а затем нажмите кнопку **Сохранить**:</span><span class="sxs-lookup"><span data-stu-id="845a9-262">In the policy code editor, add a `set-backend-service` policy under inbound policies as shown here and click the **Save** button:</span></span>
    
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

<span data-ttu-id="845a9-263">Чтобы ознакомиться с полным набором атрибутов серверной политики Service Fabric, см. дополнительные сведения в разделе [Задание внутренней службы](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService).</span><span class="sxs-lookup"><span data-stu-id="845a9-263">For a full set of Service Fabric back-end policy attributes, refer to the [API Management back-end documentation](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span></span>

### <a name="add-the-api-to-a-product"></a><span data-ttu-id="845a9-264">Добавление API в продукт</span><span class="sxs-lookup"><span data-stu-id="845a9-264">Add the API to a product.</span></span> 

<span data-ttu-id="845a9-265">Прежде чем вызывать API, его нужно добавить в продукт, где вы можете предоставить пользователям доступ.</span><span class="sxs-lookup"><span data-stu-id="845a9-265">Before you can call the API, it must be added to a product where you can grant access to users.</span></span> 

 1. <span data-ttu-id="845a9-266">В службе управления API выберите **Products - PREVIEW** (Продукты (предварительная версия)).</span><span class="sxs-lookup"><span data-stu-id="845a9-266">In the API Management service, select **Products - PREVIEW**.</span></span>
 2. <span data-ttu-id="845a9-267">По умолчанию служба управления API предоставляет два продукта: фиксированный и без ограничений.</span><span class="sxs-lookup"><span data-stu-id="845a9-267">By default, API Management providers two products: Starter and Unlimited.</span></span> <span data-ttu-id="845a9-268">Выберите продукт без ограничений.</span><span class="sxs-lookup"><span data-stu-id="845a9-268">Select the Unlimited product.</span></span>
 3. <span data-ttu-id="845a9-269">Выберите API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="845a9-269">Select APIs.</span></span>
 4. <span data-ttu-id="845a9-270">Щелкните **+ Добавить**.</span><span class="sxs-lookup"><span data-stu-id="845a9-270">Click the **+ Add** button.</span></span>
 5. <span data-ttu-id="845a9-271">Выберите созданный на предыдущем шаге API `Service Fabric App`, а затем нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="845a9-271">Select the `Service Fabric App` API you created in the previous steps and click the **Select** button.</span></span>

### <a name="test-it"></a><span data-ttu-id="845a9-272">Тестирование</span><span class="sxs-lookup"><span data-stu-id="845a9-272">Test it</span></span>

<span data-ttu-id="845a9-273">Теперь вы можете попробовать отправить запрос к внутренней службе Service Fabric через службу управления API непосредственно из портала Azure.</span><span class="sxs-lookup"><span data-stu-id="845a9-273">You can now try sending a request to your back-end service in Service Fabric through API Management directly from the Azure portal.</span></span>

 1. <span data-ttu-id="845a9-274">В службе управления API выберите **API-интерфейсы (ПРЕДВАРИТЕЛЬНАЯ ВЕРСИЯ)**.</span><span class="sxs-lookup"><span data-stu-id="845a9-274">In the API Management service, select **API - PREVIEW**.</span></span>
 2. <span data-ttu-id="845a9-275">В созданном на предыдущем шаге API `Service Fabric App` выберите вкладку **Проверить**.</span><span class="sxs-lookup"><span data-stu-id="845a9-275">In the `Service Fabric App` API you created in the previous steps, select the **Test** tab.</span></span>
 3. <span data-ttu-id="845a9-276">Нажмите кнопку **Отправка**, чтобы отправить тестовый запрос во внутреннюю службу.</span><span class="sxs-lookup"><span data-stu-id="845a9-276">Click the **Send** button to send a test request to the backend service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="845a9-277">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="845a9-277">Next steps</span></span>

<span data-ttu-id="845a9-278">На этом этапе базовая установка службы управления API и Service Fabric завершена.</span><span class="sxs-lookup"><span data-stu-id="845a9-278">At this point, you should have a basic setup with Service Fabric and API Management.</span></span>

<span data-ttu-id="845a9-279">Для быстрой настройки в рамках этого руководства используется базовая аутентификация пользователя на основе сертификата для кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="845a9-279">This tutorial uses basic certificate-based user authentication for your Service Fabric cluster to get you set up quickly.</span></span> <span data-ttu-id="845a9-280">Расширенную аутентификацию пользователя для кластера Service Fabric лучше использовать с [аутентификацией Azure Active Directory](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span><span class="sxs-lookup"><span data-stu-id="845a9-280">More advanced user authentication for your Service Fabric cluster is preferable with [Azure Active Directory authentication](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span></span> 

<span data-ttu-id="845a9-281">Далее, чтобы подготовить приложение для реального трафика, [создайте и настройте расширенные параметры продукта в службе управления API Azure](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules).</span><span class="sxs-lookup"><span data-stu-id="845a9-281">Next, [create and configure advanced product settings in Azure API Management](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) to prepare your application for real world traffic.</span></span>

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
