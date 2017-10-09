---
title: "кластер Service Fabric aaaCreate в hello портал Azure | Документы Microsoft"
description: "В этой статье описывается, как hello tooset безопасности кластера Service Fabric в Azure с помощью портала Azure и хранилищем ключей Azure."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: vturecek
ms.assetid: 426c3d13-127a-49eb-a54c-6bde7c87a83b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: chackdan
ms.openlocfilehash: 045f71b491260e741ce7a54a75c440e1b33059a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-hello-azure-portal"></a><span data-ttu-id="732cf-103">Создание кластера Service Fabric в Azure с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="732cf-103">Create a Service Fabric cluster in Azure using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="732cf-104">Диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="732cf-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="732cf-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="732cf-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
> 
> 

<span data-ttu-id="732cf-106">Это пошаговое руководство, которое поможет выполнить действия hello настройки безопасности кластера Service Fabric в Azure с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="732cf-106">This is a step-by-step guide that walks you through hello steps of setting up a secure Service Fabric cluster in Azure using hello Azure portal.</span></span> <span data-ttu-id="732cf-107">Это руководство поможет выполнить следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="732cf-107">This guide walks you through hello following steps:</span></span>

* <span data-ttu-id="732cf-108">Настройка хранилища ключей toomanage ключей для обеспечения безопасности кластера.</span><span class="sxs-lookup"><span data-stu-id="732cf-108">Set up Key Vault toomanage keys for cluster security.</span></span>
* <span data-ttu-id="732cf-109">Создание защищенных кластеров в Azure через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="732cf-109">Create a secured cluster in Azure through hello Azure portal.</span></span>
* <span data-ttu-id="732cf-110">Аутентификация администраторов с помощью сертификатов.</span><span class="sxs-lookup"><span data-stu-id="732cf-110">Authenticate administrators using certificates.</span></span>

> [!NOTE]
> <span data-ttu-id="732cf-111">Для обеспечения дополнительных параметров безопасности, таких как аутентификация пользователей с помощью Azure Active Directory и настройка сертификатов для безопасности приложений, [создайте кластер с помощью Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="732cf-111">For more advanced security options, such as user authentication with Azure Active Directory and setting up certificates for application security, [create your cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

<span data-ttu-id="732cf-112">Безопасный кластер представляет кластер, запрещающую операции toomanagement несанкционированного доступа, включая развертывание, обновление и удаление приложений, служб и данных hello, которые они содержат.</span><span class="sxs-lookup"><span data-stu-id="732cf-112">A secure cluster is a cluster that prevents unauthorized access toomanagement operations, which includes deploying, upgrading, and deleting applications, services, and hello data they contain.</span></span> <span data-ttu-id="732cf-113">Небезопасные кластер — это кластер, что любой пользователь может подключиться tooat в любое время и выполнять операции управления.</span><span class="sxs-lookup"><span data-stu-id="732cf-113">An unsecure cluster is a cluster that anyone can connect tooat any time and perform management operations.</span></span> <span data-ttu-id="732cf-114">Хотя это возможно toocreate небезопасные кластера, это **безопасного кластера настоятельно рекомендуется toocreate**.</span><span class="sxs-lookup"><span data-stu-id="732cf-114">Although it is possible toocreate an unsecure cluster, it is **highly recommended toocreate a secure cluster**.</span></span> <span data-ttu-id="732cf-115">Незащищенный кластер **невозможно будет защитить позднее** , для этого нужно будет создать новый кластер.</span><span class="sxs-lookup"><span data-stu-id="732cf-115">An unsecure cluster **cannot be secured later** - a new cluster must be created.</span></span>

<span data-ttu-id="732cf-116">Основные понятия Hello hello же для создания защищенных кластеров hello кластеры, кластеры Linux или кластерах Windows.</span><span class="sxs-lookup"><span data-stu-id="732cf-116">hello concepts are hello same for creating secure clusters, whether hello clusters are Linux clusters or Windows clusters.</span></span> <span data-ttu-id="732cf-117">Дополнительные сведения о создании безопасных кластеров Linux, а также вспомогательные скрипты см. в статье [Создание безопасных кластеров в Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="732cf-117">For more information and helper scripts for creating secure Linux clusters, please see [Creating secure clusters on Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span></span> <span data-ttu-id="732cf-118">Hello параметры, получаемые с hello вспомогательный сценария, предоставленного могут быть введены непосредственно в портал hello как описано в разделе "hello" [создания кластера в hello портал Azure](#create-cluster-portal).</span><span class="sxs-lookup"><span data-stu-id="732cf-118">hello parameters obtained by hello helper script provided can be input directly into hello portal as described in hello section [Create a cluster in hello Azure portal](#create-cluster-portal).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="732cf-119">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="732cf-119">Log in tooAzure</span></span>
<span data-ttu-id="732cf-120">В этом руководстве используется [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="732cf-120">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="732cf-121">При запуске нового сеанса PowerShell, войдите в tooyour учетная запись Azure и выберите подписку перед выполнением команды Azure.</span><span class="sxs-lookup"><span data-stu-id="732cf-121">When starting a new PowerShell session, log in tooyour Azure account and select your subscription before executing Azure commands.</span></span>

<span data-ttu-id="732cf-122">Войдите в учетную запись tooyour azure:</span><span class="sxs-lookup"><span data-stu-id="732cf-122">Log in tooyour azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="732cf-123">Выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="732cf-123">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a><span data-ttu-id="732cf-124">Настройка хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="732cf-124">Set up Key Vault</span></span>
<span data-ttu-id="732cf-125">В этой части руководства hello описывается создание хранилища ключей для кластера Service Fabric в Azure и для приложения Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="732cf-125">This part of hello guide walks you through creating a Key Vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="732cf-126">Полное руководство по в хранилище ключей, в разделе hello [хранилище ключей Знакомство с][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="732cf-126">For a complete guide on Key Vault, see hello [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="732cf-127">Service Fabric использует сертификаты X.509 toosecure кластера.</span><span class="sxs-lookup"><span data-stu-id="732cf-127">Service Fabric uses X.509 certificates toosecure a cluster.</span></span> <span data-ttu-id="732cf-128">Хранилище ключей Azure является toomanage используемые сертификаты для кластеров Service Fabric в Azure.</span><span class="sxs-lookup"><span data-stu-id="732cf-128">Azure Key Vault is used toomanage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="732cf-129">При развертывании в Azure, ответственный за создание кластеров Service Fabric поставщика ресурсов Azure hello извлекает сертификаты из хранилища ключей и устанавливает их на hello кластера виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="732cf-129">When a cluster is deployed in Azure, hello Azure resource provider responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on hello cluster VMs.</span></span>

<span data-ttu-id="732cf-130">Hello следующей схеме показана связь hello хранилище ключей, кластер Service Fabric и hello поставщика ресурсов Azure, которая использует сертификаты, хранящиеся в хранилище ключей при создании кластера.</span><span class="sxs-lookup"><span data-stu-id="732cf-130">hello following diagram illustrates hello relationship between Key Vault, a Service Fabric cluster, and hello Azure resource provider that uses certificates stored in Key Vault when it creates a cluster:</span></span>

![Установка сертификата][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="732cf-132">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="732cf-132">Create a Resource Group</span></span>
<span data-ttu-id="732cf-133">Hello первым шагом является toocreate группы ресурсов, в частности для хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="732cf-133">hello first step is toocreate a new resource group specifically for Key Vault.</span></span> <span data-ttu-id="732cf-134">Размещение в собственной группе ресурсов хранилища ключей рекомендуется, чтобы можно было удалить вычислений и хранения групп ресурсов — например, группа ресурсов hello, имеющий кластера Service Fabric — без потери ключи и секретные коды.</span><span class="sxs-lookup"><span data-stu-id="732cf-134">Putting Key Vault into its own resource group is recommended so that you can remove compute and storage resource groups - such as hello resource group that has your Service Fabric cluster - without losing your keys and secrets.</span></span> <span data-ttu-id="732cf-135">Группа ресурсов Hello с вашего хранилища ключей должен быть в hello же регионе, что кластер hello, он используется.</span><span class="sxs-lookup"><span data-stu-id="732cf-135">hello resource group that has your Key Vault must be in hello same region as hello cluster that is using it.</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: hello output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a><span data-ttu-id="732cf-136">Создание хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="732cf-136">Create Key Vault</span></span>
<span data-ttu-id="732cf-137">Создание хранилища ключей в новую группу ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="732cf-137">Create a Key Vault in hello new resource group.</span></span> <span data-ttu-id="732cf-138">Hello хранилище ключей **должна быть включена для развертывания** tooallow hello Service Fabric сертификаты tooget поставщика ресурсов из него и установить на узлах кластера:</span><span class="sxs-lookup"><span data-stu-id="732cf-138">hello Key Vault **must be enabled for deployment** tooallow hello Service Fabric resource provider tooget certificates from it and install on cluster nodes:</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmKeyVault -VaultName 'myvault' -ResourceGroupName 'mycluster-keyvault' -Location 'West US' -EnabledForDeployment


    Vault Name                       : myvault
    Resource Group Name              : mycluster-keyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault
    Vault URI                        : https://myvault.vault.azure.net
    Tenant ID                        : <guid>
    SKU                              : Standard
    Enabled For Deployment?          : False
    Enabled For Template Deployment? : False
    Enabled For Disk Encryption?     : False
    Access Policies                  :
                                       Tenant ID                :    <guid>
                                       Object ID                :    <guid>
                                       Application ID           :
                                       Display Name             :    
                                       Permissions tooKeys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions tooSecrets   :    all


    Tags                             :
```

<span data-ttu-id="732cf-139">При наличии существующего хранилища ключей можно сделать его доступным для развертывания с помощью командной строки Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="732cf-139">If you have an existing Key Vault, you can enable it for deployment using Azure CLI:</span></span>

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-tookey-vault"></a><span data-ttu-id="732cf-140">Добавьте сертификаты tooKey хранилища</span><span class="sxs-lookup"><span data-stu-id="732cf-140">Add certificates tooKey Vault</span></span>
<span data-ttu-id="732cf-141">Сертификаты используются в Service Fabric tooprovide проверки подлинности и шифрования toosecure различные аспекты кластера и его применения.</span><span class="sxs-lookup"><span data-stu-id="732cf-141">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="732cf-142">Дополнительные сведения о том, как сертификаты используются в Service Fabric, см. в статье [Сценарии защиты кластера Service Fabric][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="732cf-142">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="732cf-143">Сертификат кластера и сервера (обязательно)</span><span class="sxs-lookup"><span data-stu-id="732cf-143">Cluster and server certificate (required)</span></span>
<span data-ttu-id="732cf-144">Этот сертификат является обязательным toosecure кластером и предотвратить несанкционированный доступ tooit.</span><span class="sxs-lookup"><span data-stu-id="732cf-144">This certificate is required toosecure a cluster and prevent unauthorized access tooit.</span></span> <span data-ttu-id="732cf-145">Он обеспечивает безопасность кластера несколькими способами.</span><span class="sxs-lookup"><span data-stu-id="732cf-145">It provides cluster security in a couple ways:</span></span>

* <span data-ttu-id="732cf-146">**Аутентификация в кластере** позволяет аутентифицировать обмен данными между узлами для федерации кластера.</span><span class="sxs-lookup"><span data-stu-id="732cf-146">**Cluster authentication:** Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="732cf-147">Только узлы, которые можно подтвердить свою личность с помощью этого сертификата можно соединить hello кластера.</span><span class="sxs-lookup"><span data-stu-id="732cf-147">Only nodes that can prove their identity with this certificate can join hello cluster.</span></span>
* <span data-ttu-id="732cf-148">**Проверка подлинности сервера:** проверяет подлинность hello кластера управления конечными точками tooa клиента управления, чтобы hello управления клиент узнает, осуществляет обмен данными toohello реальные кластера.</span><span class="sxs-lookup"><span data-stu-id="732cf-148">**Server authentication:** Authenticates hello cluster management endpoints tooa management client, so that hello management client knows it is talking toohello real cluster.</span></span> <span data-ttu-id="732cf-149">Этот сертификат также предоставляет SSL для hello API управления HTTPS и обозреватель Service Fabric по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="732cf-149">This certificate also provides SSL for hello HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="732cf-150">tooserve этих целей, hello сертификат должен удовлетворять hello следующие требования:</span><span class="sxs-lookup"><span data-stu-id="732cf-150">tooserve these purposes, hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="732cf-151">Hello сертификат должен содержать закрытый ключ.</span><span class="sxs-lookup"><span data-stu-id="732cf-151">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="732cf-152">необходимо создать сертификат Hello для обмена ключами, tooa экспортируемый файл обмена личной информацией (PFX-файл).</span><span class="sxs-lookup"><span data-stu-id="732cf-152">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="732cf-153">Hello имя субъекта сертификата должно соответствовать кластера Service Fabric hello tooaccess домен, используемый hello.</span><span class="sxs-lookup"><span data-stu-id="732cf-153">hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="732cf-154">Это обязательный tooprovide SSL для конечных точек управления HTTPS и обозреватель Service Fabric hello кластера.</span><span class="sxs-lookup"><span data-stu-id="732cf-154">This is required tooprovide SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="732cf-155">Не удается получить SSL-сертификат центра сертификации (ЦС), для hello `.cloudapp.azure.com` домена.</span><span class="sxs-lookup"><span data-stu-id="732cf-155">You cannot obtain an SSL certificate from a certificate authority (CA) for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="732cf-156">Необходимо получить имя личного домена для кластера.</span><span class="sxs-lookup"><span data-stu-id="732cf-156">Acquire a custom domain name for your cluster.</span></span> <span data-ttu-id="732cf-157">При запросе сертификата из имени субъекта сертификата hello ЦС должно соответствовать имени пользовательского домена hello, используемые для кластера.</span><span class="sxs-lookup"><span data-stu-id="732cf-157">When you request a certificate from a CA hello certificate's subject name must match hello custom domain name used for your cluster.</span></span>

### <a name="client-authentication-certificates"></a><span data-ttu-id="732cf-158">Сертификаты проверки подлинности клиента</span><span class="sxs-lookup"><span data-stu-id="732cf-158">Client authentication certificates</span></span>
<span data-ttu-id="732cf-159">Дополнительные сертификаты клиента используются для аутентификации администраторов при выполнении задач управления кластером.</span><span class="sxs-lookup"><span data-stu-id="732cf-159">Additional client certificates authenticate administrators for cluster management tasks.</span></span> <span data-ttu-id="732cf-160">Service Fabric имеет два уровня доступа: **администратор** и **пользователь только для чтения**.</span><span class="sxs-lookup"><span data-stu-id="732cf-160">Service Fabric has two access levels: **admin** and **read-only user**.</span></span> <span data-ttu-id="732cf-161">Необходимо использовать хотя бы один сертификат для административного доступа.</span><span class="sxs-lookup"><span data-stu-id="732cf-161">At minimum, a single certificate for administrative access should be used.</span></span> <span data-ttu-id="732cf-162">Для получения дополнительного доступа на уровне пользователя необходимо предоставить отдельный сертификат.</span><span class="sxs-lookup"><span data-stu-id="732cf-162">For additional user-level access, a separate certificate must be provided.</span></span> <span data-ttu-id="732cf-163">Дополнительные сведения о ролях доступа см. в статье [Контроль доступа на основе ролей для клиентов Service Fabric][service-fabric-cluster-security-roles].</span><span class="sxs-lookup"><span data-stu-id="732cf-163">For more information on access roles, see [role-based access control for Service Fabric clients][service-fabric-cluster-security-roles].</span></span>

<span data-ttu-id="732cf-164">Не обязательно tooupload клиента проверки подлинности сертификатов tooKey хранилище toowork в Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="732cf-164">You do not need tooupload Client authentication certificates tooKey Vault toowork with Service Fabric.</span></span> <span data-ttu-id="732cf-165">Эти сертификаты должны только toobe предоставленный toousers, авторизованных для управления кластером.</span><span class="sxs-lookup"><span data-stu-id="732cf-165">These certificates only need toobe provided toousers who are authorized for cluster management.</span></span> 

> [!NOTE]
> <span data-ttu-id="732cf-166">Azure Active Directory является hello рекомендуется клиентов tooauthenticate способом для кластера операций управления.</span><span class="sxs-lookup"><span data-stu-id="732cf-166">Azure Active Directory is hello recommended way tooauthenticate clients for cluster management operations.</span></span> <span data-ttu-id="732cf-167">toouse Azure Active Directory необходимо [создание кластера с помощью диспетчера ресурсов Azure][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="732cf-167">toouse Azure Active Directory, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

### <a name="application-certificates-optional"></a><span data-ttu-id="732cf-168">Сертификаты приложения (необязательно)</span><span class="sxs-lookup"><span data-stu-id="732cf-168">Application certificates (optional)</span></span>
<span data-ttu-id="732cf-169">В кластере можно установить любое количество дополнительных сертификатов для обеспечения безопасности приложений.</span><span class="sxs-lookup"><span data-stu-id="732cf-169">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="732cf-170">Перед созданием кластера, рассмотрим hello безопасности приложений, требующих toobe сертификатов, установленных на узлах hello, такие как:</span><span class="sxs-lookup"><span data-stu-id="732cf-170">Before creating your cluster, consider hello application security scenarios that require a certificate toobe installed on hello nodes, such as:</span></span>

* <span data-ttu-id="732cf-171">шифрование и расшифровка значений конфигурации приложений;</span><span class="sxs-lookup"><span data-stu-id="732cf-171">Encryption and decryption of application configuration values</span></span>
* <span data-ttu-id="732cf-172">шифрование данных между узлами во время репликации.</span><span class="sxs-lookup"><span data-stu-id="732cf-172">Encryption of data across nodes during replication</span></span> 

<span data-ttu-id="732cf-173">При создании кластера с помощью портала Azure hello сертификатов приложения нельзя настроить.</span><span class="sxs-lookup"><span data-stu-id="732cf-173">Application certificates cannot be configured when creating a cluster through hello Azure portal.</span></span> <span data-ttu-id="732cf-174">сертификаты tooconfigure приложения во время установки кластера, необходимо [создание кластера с помощью диспетчера ресурсов Azure][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="732cf-174">tooconfigure application certificates at cluster setup time, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span> <span data-ttu-id="732cf-175">Можно также добавить кластера toohello сертификаты приложения после его создания.</span><span class="sxs-lookup"><span data-stu-id="732cf-175">You can also add application certificates toohello cluster after it has been created.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="732cf-176">Форматирование сертификатов для использования поставщиком ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="732cf-176">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="732cf-177">Файлы закрытого ключа (PFX-файлы) можно добавить в хранилище ключей и использовать непосредственно из него.</span><span class="sxs-lookup"><span data-stu-id="732cf-177">Private key files (.pfx) can be added and used directly through Key Vault.</span></span> <span data-ttu-id="732cf-178">Однако hello поставщика ресурсов Azure требует toobe ключи, хранящиеся в специальном формате JSON, включающий hello PFX-файл в Base64-кодировке строки и hello пароль закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="732cf-178">However, hello Azure resource provider requires keys toobe stored in a special JSON format that includes hello .pfx as a base-64 encoded string and hello private key password.</span></span> <span data-ttu-id="732cf-179">tooaccommodate эти требования ключей необходимо поместить в строку JSON и сохраняется как *секреты* в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="732cf-179">tooaccommodate these requirements, keys must be placed in a JSON string and then stored as *secrets* in Key Vault.</span></span>

<span data-ttu-id="732cf-180">модуль PowerShell — toomake удобным это процесс, [на сайте GitHub][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="732cf-180">toomake this process easier, a PowerShell module is [available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="732cf-181">Выполните эти шаги toouse hello модуля.</span><span class="sxs-lookup"><span data-stu-id="732cf-181">Follow these steps toouse hello module:</span></span>

1. <span data-ttu-id="732cf-182">Загрузите все содержимое репозитория hello hello в локальный каталог.</span><span class="sxs-lookup"><span data-stu-id="732cf-182">Download hello entire contents of hello repo into a local directory.</span></span> 
2. <span data-ttu-id="732cf-183">Импорт модуля hello в окне PowerShell:</span><span class="sxs-lookup"><span data-stu-id="732cf-183">Import hello module in your PowerShell window:</span></span>

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

<span data-ttu-id="732cf-184">Hello `Invoke-AddCertToKeyVault` команды в этом модуле PowerShell автоматически форматирует закрытый ключ сертификата в строке JSON и отправляет его tooKey хранилища.</span><span class="sxs-lookup"><span data-stu-id="732cf-184">hello `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it tooKey Vault.</span></span> <span data-ttu-id="732cf-185">Используйте сертификат кластера hello tooadd и любые дополнительные приложения сертификаты tooKey хранилища.</span><span class="sxs-lookup"><span data-stu-id="732cf-185">Use it tooadd hello cluster certificate and any additional application certificates tooKey Vault.</span></span> <span data-ttu-id="732cf-186">Повторите это действие другие сертификаты, требуется tooinstall в кластере.</span><span class="sxs-lookup"><span data-stu-id="732cf-186">Repeat this step for any additional certificates you want tooinstall in your cluster.</span></span>

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: hello output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomyvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

<span data-ttu-id="732cf-187">Это все предварительные условия hello хранилища ключей для настройки шаблона диспетчера ресурсов кластера Service Fabric, устанавливает сертификаты для проверки подлинности узла, безопасность конечной точки управления и проверки подлинности и любые дополнительная безопасность приложений функции, которые используют сертификаты X.509.</span><span class="sxs-lookup"><span data-stu-id="732cf-187">These are all hello Key Vault prerequisites for configuring a Service Fabric cluster Resource Manager template that installs certificates for node authentication, management endpoint security and authentication, and any additional application security features that use X.509 certificates.</span></span> <span data-ttu-id="732cf-188">На этом этапе вы добавили hello, после завершения программы установки в Azure:</span><span class="sxs-lookup"><span data-stu-id="732cf-188">At this point, you should now have hello following setup in Azure:</span></span>

* <span data-ttu-id="732cf-189">группа ресурсов хранилища ключей;</span><span class="sxs-lookup"><span data-stu-id="732cf-189">Key Vault resource group</span></span>
  * <span data-ttu-id="732cf-190">хранилище ключей;</span><span class="sxs-lookup"><span data-stu-id="732cf-190">Key Vault</span></span>
    * <span data-ttu-id="732cf-191">сертификат проверки подлинности сервера кластера;</span><span class="sxs-lookup"><span data-stu-id="732cf-191">Cluster server authentication certificate</span></span>

<span data-ttu-id="732cf-192"></a "create-cluster-portal" ></a></span><span class="sxs-lookup"><span data-stu-id="732cf-192"></a "create-cluster-portal" ></a></span></span>

## <a name="create-cluster-in-hello-azure-portal"></a><span data-ttu-id="732cf-193">Создание кластера в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="732cf-193">Create cluster in hello Azure portal</span></span>
### <a name="search-for-hello-service-fabric-cluster-resource"></a><span data-ttu-id="732cf-194">Поиск hello ресурса кластера Service Fabric</span><span class="sxs-lookup"><span data-stu-id="732cf-194">Search for hello Service Fabric cluster resource</span></span>
![Поиск шаблона кластера Service Fabric на hello портал Azure.][SearchforServiceFabricClusterTemplate]

1. <span data-ttu-id="732cf-196">Войдите в toohello [портал Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="732cf-196">Sign in toohello [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="732cf-197">Нажмите кнопку **New** tooadd новый шаблон ресурсов.</span><span class="sxs-lookup"><span data-stu-id="732cf-197">Click **New** tooadd a new resource template.</span></span> <span data-ttu-id="732cf-198">Поиск шаблона кластера Service Fabric hello в hello **Marketplace** под **все**.</span><span class="sxs-lookup"><span data-stu-id="732cf-198">Search for hello Service Fabric Cluster template in hello **Marketplace** under **Everything**.</span></span>
3. <span data-ttu-id="732cf-199">Выберите **кластера Service Fabric** из списка hello.</span><span class="sxs-lookup"><span data-stu-id="732cf-199">Select **Service Fabric Cluster** from hello list.</span></span>
4. <span data-ttu-id="732cf-200">Перейдите toohello **кластера Service Fabric** колонка, щелкните **создать**,</span><span class="sxs-lookup"><span data-stu-id="732cf-200">Navigate toohello **Service Fabric Cluster** blade, click **Create**,</span></span>
5. <span data-ttu-id="732cf-201">Hello **кластера Service Fabric создать** колонке имеет hello следующие четыре шага.</span><span class="sxs-lookup"><span data-stu-id="732cf-201">hello **Create Service Fabric cluster** blade has hello following four steps.</span></span>

#### <a name="1-basics"></a><span data-ttu-id="732cf-202">1. Основы</span><span class="sxs-lookup"><span data-stu-id="732cf-202">1. Basics</span></span>
![Снимок экрана: создание группы ресурсов.][CreateRG]

<span data-ttu-id="732cf-204">В колонке основы hello необходимо tooprovide hello основные сведения для кластера.</span><span class="sxs-lookup"><span data-stu-id="732cf-204">In hello Basics blade you need tooprovide hello basic details for your cluster.</span></span>

1. <span data-ttu-id="732cf-205">Введите имя кластера hello.</span><span class="sxs-lookup"><span data-stu-id="732cf-205">Enter hello name of your cluster.</span></span>
2. <span data-ttu-id="732cf-206">Введите **имя пользователя** и **пароль** для удаленного рабочего стола для hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="732cf-206">Enter a **user name** and **password** for Remote Desktop for hello VMs.</span></span>
3. <span data-ttu-id="732cf-207">Убедитесь, что hello tooselect **подписки** требуется toobe вашего кластера, развертывания, особенно в том случае, если у вас несколько подписок.</span><span class="sxs-lookup"><span data-stu-id="732cf-207">Make sure tooselect hello **Subscription** that you want your cluster toobe deployed to, especially if you have multiple subscriptions.</span></span>
4. <span data-ttu-id="732cf-208">Создайте **новую группу ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="732cf-208">Create a **new resource group**.</span></span> <span data-ttu-id="732cf-209">Это наиболее toogive hello совпадает с именем кластера hello, так как он помогает в поиске их позднее, особенно в том случае, если выполняется развертывание tooyour toomake изменения или удаления кластера.</span><span class="sxs-lookup"><span data-stu-id="732cf-209">It is best toogive it hello same name as hello cluster, since it helps in finding them later, especially when you are trying toomake changes tooyour deployment or delete your cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="732cf-210">Несмотря на то, что toouse существующую группу ресурсов, можно определить, является хорошей практикой toocreate новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="732cf-210">Although you can decide toouse an existing resource group, it is a good practice toocreate a new resource group.</span></span> <span data-ttu-id="732cf-211">Это позволяет легко toodelete кластеры, которые не требуется.</span><span class="sxs-lookup"><span data-stu-id="732cf-211">This makes it easy toodelete clusters that you do not need.</span></span>
   > 
   > 
5. <span data-ttu-id="732cf-212">Выберите hello **область** требуется toocreate hello кластера.</span><span class="sxs-lookup"><span data-stu-id="732cf-212">Select hello **region** in which you want toocreate hello cluster.</span></span> <span data-ttu-id="732cf-213">Необходимо использовать hello не совпадают, ваш ключ в хранилище.</span><span class="sxs-lookup"><span data-stu-id="732cf-213">You must use hello same region that your Key Vault is in.</span></span>

#### <a name="2-cluster-configuration"></a><span data-ttu-id="732cf-214">2. Конфигурация кластера</span><span class="sxs-lookup"><span data-stu-id="732cf-214">2. Cluster configuration</span></span>
![Создание типа узла][CreateNodeType]

<span data-ttu-id="732cf-216">Настройте узлы кластера.</span><span class="sxs-lookup"><span data-stu-id="732cf-216">Configure your cluster nodes.</span></span> <span data-ttu-id="732cf-217">Типы узлов определяют размеры виртуальных Машин hello, hello число виртуальных машин и их свойства.</span><span class="sxs-lookup"><span data-stu-id="732cf-217">Node types define hello VM sizes, hello number of VMs, and their properties.</span></span> <span data-ttu-id="732cf-218">Кластер может иметь более одного типа узла, но тип основного узла hello (hello первое заданное вами на портале hello) должен иметь по крайней мере пять ВМ, так как этот тип узла hello там, где размещены службы структуры системных служб.</span><span class="sxs-lookup"><span data-stu-id="732cf-218">Your cluster can have more than one node type, but hello primary node type (hello first one that you define on hello portal) must have at least five VMs, as this is hello node type where Service Fabric system services are placed.</span></span> <span data-ttu-id="732cf-219">Не настраивайте параметры **Свойства размещения** , так как стандартное свойство размещения NodeTypeName добавляется автоматически.</span><span class="sxs-lookup"><span data-stu-id="732cf-219">Do not configure **Placement Properties** because a default placement property of "NodeTypeName" is added automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="732cf-220">Распространенный сценарий для нескольких типов узлов — это приложение, содержащее интерфейсную и серверную службы.</span><span class="sxs-lookup"><span data-stu-id="732cf-220">A common scenario for multiple node types is an application that contains a front-end service and a back-end service.</span></span> <span data-ttu-id="732cf-221">Вы tooput hello клиентской службы на более мелкие виртуальных машинах (размеры виртуальных Машин как D2) toohello открытых портов Интернета, но чтобы tooput hello внутренней службы на ВМ большего размера (с размеры виртуальных Машин как D4, D6, D15 и т. д) с нет открытых портов с выходом в Интернет.</span><span class="sxs-lookup"><span data-stu-id="732cf-221">You want tooput hello front-end service on smaller VMs (VM sizes like D2) with ports open toohello Internet, but you want tooput hello back-end service on larger VMs (with VM sizes like D4, D6, D15, and so on) with no Internet-facing ports open.</span></span>
> 
> 

1. <span data-ttu-id="732cf-222">Выберите имя для вашего типа узла (1 too12 знаков, содержащий только буквы и цифры).</span><span class="sxs-lookup"><span data-stu-id="732cf-222">Choose a name for your node type (1 too12 characters containing only letters and numbers).</span></span>
2. <span data-ttu-id="732cf-223">Минимальная Hello **размер** виртуальных машин для hello основном узле типа определяется hello **устойчивость** уровня, выберите для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="732cf-223">hello minimum **size** of VMs for hello primary node type is driven by hello **durability** tier you choose for hello cluster.</span></span> <span data-ttu-id="732cf-224">по умолчанию Hello hello уровень устойчивости, бронза.</span><span class="sxs-lookup"><span data-stu-id="732cf-224">hello default for hello durability tier is bronze.</span></span> <span data-ttu-id="732cf-225">Дополнительные сведения об устойчивости см. в разделе [как hello toochoose Service Fabric кластера, надежность и устойчивость][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="732cf-225">For more information on durability, see [how toochoose hello Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
3. <span data-ttu-id="732cf-226">Выберите размер виртуальной Машины hello и ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="732cf-226">Select hello VM size and pricing tier.</span></span> <span data-ttu-id="732cf-227">Виртуальные машины серии D оснащены твердотельными накопителями (SSD) и настоятельно рекомендуются для приложений с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="732cf-227">D-series VMs have SSD drives and are highly recommended for stateful applications.</span></span> <span data-ttu-id="732cf-228">Не используйте SKU виртуальной машины с частичными ядрами и менее чем 7 ГБ свободного места на диске.</span><span class="sxs-lookup"><span data-stu-id="732cf-228">Do not use any VM SKU that has partial cores or have less than 7 GB of available disk capacity.</span></span> 
4. <span data-ttu-id="732cf-229">Минимальная Hello **номер** виртуальных машин для hello основном узле типа определяется hello **надежности** выборе уровня.</span><span class="sxs-lookup"><span data-stu-id="732cf-229">hello minimum **number** of VMs for hello primary node type is driven by hello **reliability** tier you choose.</span></span> <span data-ttu-id="732cf-230">по умолчанию Hello hello уровень надежности, серебряный.</span><span class="sxs-lookup"><span data-stu-id="732cf-230">hello default for hello reliability tier is Silver.</span></span> <span data-ttu-id="732cf-231">Дополнительные сведения о надежности см. в разделе [как hello toochoose Service Fabric кластера, надежность и устойчивость][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="732cf-231">For more information on reliability, see [how toochoose hello Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
5. <span data-ttu-id="732cf-232">Выберите hello число виртуальных машин для типа узла hello.</span><span class="sxs-lookup"><span data-stu-id="732cf-232">Choose hello number of VMs for hello node type.</span></span> <span data-ttu-id="732cf-233">Можно масштабировать вверх или вниз hello число виртуальных машин в тип узла позднее, но на тип основного узла hello, минимальное hello определяется уровень надежности hello, которые были выбраны.</span><span class="sxs-lookup"><span data-stu-id="732cf-233">You can scale up or down hello number of VMs in a node type later on, but on hello primary node type, hello minimum is driven by hello reliability level that you have chosen.</span></span> <span data-ttu-id="732cf-234">Для других типов узлов можно задать минимум 1 виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="732cf-234">Other node types can have a minimum of 1 VM.</span></span>
6. <span data-ttu-id="732cf-235">Настройте пользовательские конечные точки.</span><span class="sxs-lookup"><span data-stu-id="732cf-235">Configure custom endpoints.</span></span> <span data-ttu-id="732cf-236">Это поле позволяет tooenter запятыми список портов, которые должны tooexpose через toohello подсистемы балансировки нагрузки Azure hello общедоступный Интернет для ваших приложений.</span><span class="sxs-lookup"><span data-stu-id="732cf-236">This field allows you tooenter a comma-separated list of ports that you want tooexpose through hello Azure Load Balancer toohello public Internet for your applications.</span></span> <span data-ttu-id="732cf-237">Например, если планируется toodeploy веб-приложения tooyour кластера, введите «80» здесь tooallow трафик через порт 80 в кластере.</span><span class="sxs-lookup"><span data-stu-id="732cf-237">For example, if you plan toodeploy a web application tooyour cluster, enter "80" here tooallow traffic on port 80 into your cluster.</span></span> <span data-ttu-id="732cf-238">Дополнительные сведения о конечных точках см. в статье [Подключение к службам в Service Fabric и взаимодействие с ними][service-fabric-connect-and-communicate-with-services].</span><span class="sxs-lookup"><span data-stu-id="732cf-238">For more information on endpoints, see [communicating with applications][service-fabric-connect-and-communicate-with-services]</span></span>
7. <span data-ttu-id="732cf-239">Настройте **систему диагностики** кластера.</span><span class="sxs-lookup"><span data-stu-id="732cf-239">Configure cluster **diagnostics**.</span></span> <span data-ttu-id="732cf-240">По умолчанию включены диагностические сообщения на ваш tooassist кластера при устранении неполадок.</span><span class="sxs-lookup"><span data-stu-id="732cf-240">By default, diagnostics are enabled on your cluster tooassist with troubleshooting issues.</span></span> <span data-ttu-id="732cf-241">Чтобы изменить диагностику toodisable hello **состояние** переключения слишком**Off**.</span><span class="sxs-lookup"><span data-stu-id="732cf-241">If you want toodisable diagnostics change hello **Status** toggle too**Off**.</span></span> <span data-ttu-id="732cf-242">Отключать систему диагностики **не** рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="732cf-242">Turning off diagnostics is **not** recommended.</span></span>
8. <span data-ttu-id="732cf-243">Выберите hello структуры обновление в режиме, необходимо задать кластера.</span><span class="sxs-lookup"><span data-stu-id="732cf-243">Select hello Fabric upgrade mode you want set your cluster to.</span></span> <span data-ttu-id="732cf-244">Выберите **автоматического**, если хотите hello системы tooautomatically отгрузки hello последнюю версию и повторите tooupgrade tooit вашего кластера.</span><span class="sxs-lookup"><span data-stu-id="732cf-244">Select **Automatic**, if you want hello system tooautomatically pick up hello latest available version and try tooupgrade your cluster tooit.</span></span> <span data-ttu-id="732cf-245">Установить режим hello слишком**вручную**, если вы хотите toochoose поддерживаемой версии.</span><span class="sxs-lookup"><span data-stu-id="732cf-245">Set hello mode too**Manual**, if you want toochoose a supported version.</span></span>

> [!NOTE]
> <span data-ttu-id="732cf-246">Корпорация Майкрософт поддерживает только кластеры под управлением поддерживаемых версий Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="732cf-246">We support only clusters that are running supported versions of service Fabric.</span></span> <span data-ttu-id="732cf-247">Выбрав hello **вручную** режиме делаются на tooupgrade ответственности hello поддерживается tooa версии кластера.</span><span class="sxs-lookup"><span data-stu-id="732cf-247">By selecting hello **Manual** mode, you are taking on hello responsibility tooupgrade your cluster tooa supported version.</span></span> <span data-ttu-id="732cf-248">См. Дополнительные сведения о режиме обновления Fabric hello hello [документа службы структуры-— обновления кластера.][service-fabric-cluster-upgrade]</span><span class="sxs-lookup"><span data-stu-id="732cf-248">For more details on hello Fabric upgrade mode see hello [service-fabric-cluster-upgrade document.][service-fabric-cluster-upgrade]</span></span>
> 
> 

#### <a name="3-security"></a><span data-ttu-id="732cf-249">3. Безопасность</span><span class="sxs-lookup"><span data-stu-id="732cf-249">3. Security</span></span>
![Снимок экрана: настройка безопасности на портале Azure.][SecurityConfigs]

<span data-ttu-id="732cf-251">Последний шаг Hello — tooprovide сертификата сведения toosecure hello кластера с помощью hello хранилища ключей и сертификатов, сведения, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="732cf-251">hello final step is tooprovide certificate information toosecure hello cluster using hello Key Vault and certificate information created earlier.</span></span>

* <span data-ttu-id="732cf-252">Заполнить поля основной сертификат hello hello выходные данные, полученные от передачи hello **кластера сертификат** tooKey хранилище, используя hello `Invoke-AddCertToKeyVault` команды PowerShell.</span><span class="sxs-lookup"><span data-stu-id="732cf-252">Populate hello primary certificate fields with hello output obtained from uploading hello **cluster certificate** tooKey Vault using hello `Invoke-AddCertToKeyVault` PowerShell command.</span></span>

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* <span data-ttu-id="732cf-253">Проверьте hello **Настройка дополнительных параметров** поле tooenter клиентских сертификатов для **администрирования клиента** и **клиента только для чтения**.</span><span class="sxs-lookup"><span data-stu-id="732cf-253">Check hello **Configure advanced settings** box tooenter client certificates for **admin client** and **read-only client**.</span></span> <span data-ttu-id="732cf-254">В этих полях введите отпечаток вашего сертификата клиента администратора hello и hello отпечаток сертификата клиента пользователя только для чтения, если это применимо.</span><span class="sxs-lookup"><span data-stu-id="732cf-254">In these fields, enter hello thumbprint of your admin client certificate and hello thumbprint of your read-only user client certificate, if applicable.</span></span> <span data-ttu-id="732cf-255">Когда администраторы устанавливают tooconnect toohello кластера, предоставляются доступ только в том случае, если они имеют сертификат с отпечатком, соответствующий значениям hello отпечаток введенное здесь.</span><span class="sxs-lookup"><span data-stu-id="732cf-255">When administrators attempt tooconnect toohello cluster, they are granted access only if they have a certificate with a thumbprint that matches hello thumbprint values entered here.</span></span>  

#### <a name="4-summary"></a><span data-ttu-id="732cf-256">4. Сводка</span><span class="sxs-lookup"><span data-stu-id="732cf-256">4. Summary</span></span>
![<span data-ttu-id="732cf-257">Снимок экрана доски начала hello отображение «Развертывание кластера Service Fabric».</span><span class="sxs-lookup"><span data-stu-id="732cf-257">Screen shot of hello start board displaying "Deploying Service Fabric Cluster."</span></span> ][Notifications]

<span data-ttu-id="732cf-258">Создание кластера toocomplete hello, нажмите кнопку **Сводка** toosee hello конфигураций, которые вы указали, или загрузите hello шаблона Azure Resource Manager, который используется toodeploy кластера.</span><span class="sxs-lookup"><span data-stu-id="732cf-258">toocomplete hello cluster creation, click **Summary** toosee hello configurations that you have provided, or download hello Azure Resource Manager template that that used toodeploy your cluster.</span></span> <span data-ttu-id="732cf-259">После ввода обязательные параметры hello hello **ОК** кнопка становится зеленой, и процесс создания кластера hello можно запустить, щелкнув его.</span><span class="sxs-lookup"><span data-stu-id="732cf-259">After you have provided hello mandatory settings, hello **OK** button becomes green and you can start hello cluster creation process by clicking it.</span></span>

<span data-ttu-id="732cf-260">Вы увидите ход создания hello в уведомлениях hello.</span><span class="sxs-lookup"><span data-stu-id="732cf-260">You can see hello creation progress in hello notifications.</span></span> <span data-ttu-id="732cf-261">(Щелкните значок колокольчика «hello» рядом с hello строку состояния в hello верхнем правом углу экрана.) После щелчка **tooStartboard ПИН-код** при создании кластера hello, вы увидите **развертывание кластера Service Fabric** закрепленные toohello **запустить** платы.</span><span class="sxs-lookup"><span data-stu-id="732cf-261">(Click hello "Bell" icon near hello status bar at hello upper right of your screen.) If you clicked **Pin tooStartboard** while creating hello cluster, you will see **Deploying Service Fabric Cluster** pinned toohello **Start** board.</span></span>

### <a name="view-your-cluster-status"></a><span data-ttu-id="732cf-262">Просмотр состояния кластера</span><span class="sxs-lookup"><span data-stu-id="732cf-262">View your cluster status</span></span>
![Снимок экрана: сведения о кластере в панели мониторинга hello.][ClusterDashboard]

<span data-ttu-id="732cf-264">После создания кластера можно проверить кластер на портале hello:</span><span class="sxs-lookup"><span data-stu-id="732cf-264">Once your cluster is created, you can inspect your cluster in hello portal:</span></span>

1. <span data-ttu-id="732cf-265">Go слишком**Обзор** и нажмите кнопку **кластерами структуры службы**.</span><span class="sxs-lookup"><span data-stu-id="732cf-265">Go too**Browse** and click **Service Fabric Clusters**.</span></span>
2. <span data-ttu-id="732cf-266">Найдите нужный кластер и щелкните его.</span><span class="sxs-lookup"><span data-stu-id="732cf-266">Locate your cluster and click it.</span></span>
3. <span data-ttu-id="732cf-267">Теперь можно просмотреть сведения hello кластера на панели мониторинга hello, включая общедоступную конечную точку кластера hello и ссылка tooService Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="732cf-267">You can now see hello details of your cluster in hello dashboard, including hello cluster's public endpoint and a link tooService Fabric Explorer.</span></span>

<span data-ttu-id="732cf-268">Hello **монитора узла** раздел на панели мониторинга кластера hello указывает hello число виртуальных машин, которые работоспособны и неработоспособны.</span><span class="sxs-lookup"><span data-stu-id="732cf-268">hello **Node Monitor** section on hello cluster's dashboard blade indicates hello number of VMs that are healthy and not healthy.</span></span> <span data-ttu-id="732cf-269">Можно найти дополнительные сведения о работоспособности кластера hello в [введение модель работоспособности Service Fabric][service-fabric-health-introduction].</span><span class="sxs-lookup"><span data-stu-id="732cf-269">You can find more details about hello cluster's health at [Service Fabric health model introduction][service-fabric-health-introduction].</span></span>

> [!NOTE]
> <span data-ttu-id="732cf-270">Кластеров Service Fabric требуется определенное количество узлов toobe всегда toomaintain доступности и сохранить состояние - ссылка tooas «поддержания кворума».</span><span class="sxs-lookup"><span data-stu-id="732cf-270">Service Fabric clusters require a certain number of nodes toobe up always toomaintain availability and preserve state - referred tooas "maintaining quorum".</span></span> <span data-ttu-id="732cf-271">Поэтому, это обычно не безопасном tooshut работу всех машин в кластере hello Если сначала была выполнена [полного резервного копирования состояния][service-fabric-reliable-services-backup-restore].</span><span class="sxs-lookup"><span data-stu-id="732cf-271">Therfore, it is typically not safe tooshut down all machines in hello cluster unless you have first performed a [full backup of your state][service-fabric-reliable-services-backup-restore].</span></span>
> 
> 

## <a name="remote-connect-tooa-virtual-machine-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="732cf-272">Удаленное подключение tooa набора масштабирования виртуальных машин экземпляра или узла кластера</span><span class="sxs-lookup"><span data-stu-id="732cf-272">Remote connect tooa Virtual Machine Scale Set instance or a cluster node</span></span>
<span data-ttu-id="732cf-273">Каждый из hello NodeTypes задается в результатов в наборе масштабирования виртуальных машин Приступая к настройке кластера.</span><span class="sxs-lookup"><span data-stu-id="732cf-273">Each of hello NodeTypes you specify in your cluster results in a Virtual Machine Scale Set getting set-up.</span></span> <span data-ttu-id="732cf-274">В разделе [удаленного подключения экземпляра набора масштабирования виртуальных машин tooa] [ remote-connect-to-a-vm-scale-set] подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="732cf-274">See [Remote connect tooa Virtual Machine Scale Set instance][remote-connect-to-a-vm-scale-set] for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="732cf-275">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="732cf-275">Next steps</span></span>
<span data-ttu-id="732cf-276">На этом этапе у вас имеется защищенный кластер, использующий сертификаты для аутентификации управления.</span><span class="sxs-lookup"><span data-stu-id="732cf-276">At this point, you have a secure cluster using certificates for management authentication.</span></span> <span data-ttu-id="732cf-277">Далее, [подключения кластера tooyour](service-fabric-connect-to-secure-cluster.md) и узнайте, каким образом слишком[управление секретами приложения](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="732cf-277">Next, [connect tooyour cluster](service-fabric-connect-to-secure-cluster.md) and learn how too[manage application secrets](service-fabric-application-secret-management.md).</span></span>  <span data-ttu-id="732cf-278">Кроме того, узнайте [о вариантах поддержки Service Fabric](service-fabric-support.md).</span><span class="sxs-lookup"><span data-stu-id="732cf-278">Also, learn about [Service Fabric support options](service-fabric-support.md).</span></span>

<!-- Links -->
[azure-powershell]: https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[azure-portal]: https://portal.azure.com/
[key-vault-get-started]: ../key-vault/key-vault-get-started.md
[create-cluster-arm]: service-fabric-cluster-creation-via-arm.md
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[service-fabric-cluster-security-roles]: service-fabric-cluster-security-roles.md
[service-fabric-cluster-capacity]: service-fabric-cluster-capacity.md
[service-fabric-connect-and-communicate-with-services]: service-fabric-connect-and-communicate-with-services.md
[service-fabric-health-introduction]: service-fabric-health-introduction.md
[service-fabric-reliable-services-backup-restore]: service-fabric-reliable-services-backup-restore.md
[remote-connect-to-a-vm-scale-set]: service-fabric-cluster-nodetypes.md#remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node
[service-fabric-cluster-upgrade]: service-fabric-cluster-upgrade.md

<!--Image references-->
[SearchforServiceFabricClusterTemplate]: ./media/service-fabric-cluster-creation-via-portal/SearchforServiceFabricClusterTemplate.png
[CreateRG]: ./media/service-fabric-cluster-creation-via-portal/CreateRG.png
[CreateNodeType]: ./media/service-fabric-cluster-creation-via-portal/NodeType.png
[SecurityConfigs]: ./media/service-fabric-cluster-creation-via-portal/SecurityConfigs.png
[Notifications]: ./media/service-fabric-cluster-creation-via-portal/notifications.png
[ClusterDashboard]: ./media/service-fabric-cluster-creation-via-portal/ClusterDashboard.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
