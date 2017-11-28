---
title: "Создание кластера Service Fabric на портале Azure | Документация Майкрософт"
description: "В этой статье описывается настройка защищенного кластера Service Fabric в Azure с помощью портала Azure и хранилища ключей Azure."
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
ms.openlocfilehash: 7dda9520ce3d93bf0e86bd2481ad06c268d087c7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-the-azure-portal"></a><span data-ttu-id="a3ba7-103">Создание кластера Service Fabric в Azure с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="a3ba7-103">Create a Service Fabric cluster in Azure using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a3ba7-104">Диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="a3ba7-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="a3ba7-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="a3ba7-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
> 
> 

<span data-ttu-id="a3ba7-106">Это пошаговое руководство поможет выполнить настройку защищенного кластера Service Fabric в Azure с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-106">This is a step-by-step guide that walks you through the steps of setting up a secure Service Fabric cluster in Azure using the Azure portal.</span></span> <span data-ttu-id="a3ba7-107">Данное руководство описывает следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a3ba7-107">This guide walks you through the following steps:</span></span>

* <span data-ttu-id="a3ba7-108">Настройка хранилища ключей для управления ключами для обеспечения безопасности кластера.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-108">Set up Key Vault to manage keys for cluster security.</span></span>
* <span data-ttu-id="a3ba7-109">Создание защищенного кластера в Azure с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-109">Create a secured cluster in Azure through the Azure portal.</span></span>
* <span data-ttu-id="a3ba7-110">Аутентификация администраторов с помощью сертификатов.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-110">Authenticate administrators using certificates.</span></span>

> [!NOTE]
> <span data-ttu-id="a3ba7-111">Для обеспечения дополнительных параметров безопасности, таких как аутентификация пользователей с помощью Azure Active Directory и настройка сертификатов для безопасности приложений, [создайте кластер с помощью Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="a3ba7-111">For more advanced security options, such as user authentication with Azure Active Directory and setting up certificates for application security, [create your cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

<span data-ttu-id="a3ba7-112">Защищенный кластер — это кластер, который предотвращает несанкционированный доступ к операциям управления, включая развертывание, обновление и удаление приложений, служб и данных, которые они содержат.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-112">A secure cluster is a cluster that prevents unauthorized access to management operations, which includes deploying, upgrading, and deleting applications, services, and the data they contain.</span></span> <span data-ttu-id="a3ba7-113">Незащищенный кластер — это кластер, к которому в любое время может подключиться любой пользователь и выполнять операции управления.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-113">An unsecure cluster is a cluster that anyone can connect to at any time and perform management operations.</span></span> <span data-ttu-id="a3ba7-114">Хотя можно создать незащищенный кластер, **настоятельно рекомендуется создать защищенный кластер**.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-114">Although it is possible to create an unsecure cluster, it is **highly recommended to create a secure cluster**.</span></span> <span data-ttu-id="a3ba7-115">Незащищенный кластер **невозможно будет защитить позднее** , для этого нужно будет создать новый кластер.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-115">An unsecure cluster **cannot be secured later** - a new cluster must be created.</span></span>

<span data-ttu-id="a3ba7-116">Принципы создания безопасных кластеров в Linux или Windows аналогичны.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-116">The concepts are the same for creating secure clusters, whether the clusters are Linux clusters or Windows clusters.</span></span> <span data-ttu-id="a3ba7-117">Дополнительные сведения о создании безопасных кластеров Linux, а также вспомогательные скрипты см. в статье [Создание безопасных кластеров в Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="a3ba7-117">For more information and helper scripts for creating secure Linux clusters, please see [Creating secure clusters on Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters).</span></span> <span data-ttu-id="a3ba7-118">Параметры, полученные с помощью вспомогательного скрипта, можно указать непосредственно на портале, как описано в разделе [Создание кластера на портале Azure](#create-cluster-portal).</span><span class="sxs-lookup"><span data-stu-id="a3ba7-118">The parameters obtained by the helper script provided can be input directly into the portal as described in the section [Create a cluster in the Azure portal](#create-cluster-portal).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="a3ba7-119">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="a3ba7-119">Log in to Azure</span></span>
<span data-ttu-id="a3ba7-120">В этом руководстве используется [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="a3ba7-120">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="a3ba7-121">При запуске нового сеанса PowerShell войдите в свою учетную запись Azure и выберите подписку перед выполнением команд Azure.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-121">When starting a new PowerShell session, log in to your Azure account and select your subscription before executing Azure commands.</span></span>

<span data-ttu-id="a3ba7-122">Войдите в свою учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-122">Log in to your azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="a3ba7-123">Выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-123">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a><span data-ttu-id="a3ba7-124">Настройка хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="a3ba7-124">Set up Key Vault</span></span>
<span data-ttu-id="a3ba7-125">В этой части руководства описывается создание хранилища ключей для кластера Service Fabric в Azure и для приложений Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-125">This part of the guide walks you through creating a Key Vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="a3ba7-126">Полное описание Key Vault см. в [руководстве по началу работы с Key Vault][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="a3ba7-126">For a complete guide on Key Vault, see the [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="a3ba7-127">Для защиты кластера Service Fabric использует сертификаты X.509.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-127">Service Fabric uses X.509 certificates to secure a cluster.</span></span> <span data-ttu-id="a3ba7-128">Хранилище ключей Azure используется для управления сертификатами кластеров Service Fabric в Azure.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-128">Azure Key Vault is used to manage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="a3ba7-129">При развертывании кластера в Azure поставщик ресурсов Azure, ответственный за создание кластеров Service Fabric, извлекает сертификаты из хранилища ключей и устанавливает их на виртуальные машины кластера.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-129">When a cluster is deployed in Azure, the Azure resource provider responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on the cluster VMs.</span></span>

<span data-ttu-id="a3ba7-130">На приведенной ниже схеме показана связь между хранилищем ключей, кластером Service Fabric и поставщиком ресурсов Azure, который использует сертификаты из хранилища ключей при создании кластера.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-130">The following diagram illustrates the relationship between Key Vault, a Service Fabric cluster, and the Azure resource provider that uses certificates stored in Key Vault when it creates a cluster:</span></span>

![Установка сертификата][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="a3ba7-132">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="a3ba7-132">Create a Resource Group</span></span>
<span data-ttu-id="a3ba7-133">Первым шагом является создание новой группы ресурсов специально для хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-133">The first step is to create a new resource group specifically for Key Vault.</span></span> <span data-ttu-id="a3ba7-134">Рекомендуется поместить хранилище ключей в собственную группу ресурсов. Это позволит удалять группы вычислительных ресурсов и ресурсов хранилища (например, группу ресурсов с кластером Service Fabric) без потери ключей и секретов.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-134">Putting Key Vault into its own resource group is recommended so that you can remove compute and storage resource groups - such as the resource group that has your Service Fabric cluster - without losing your keys and secrets.</span></span> <span data-ttu-id="a3ba7-135">Группа ресурсов с хранилищем ключей должна находиться в том же регионе, что и кластер, который ее использует.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-135">The resource group that has your Key Vault must be in the same region as the cluster that is using it.</span></span>

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: The output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a><span data-ttu-id="a3ba7-136">Создание хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="a3ba7-136">Create Key Vault</span></span>
<span data-ttu-id="a3ba7-137">Создайте хранилище ключей в новой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-137">Create a Key Vault in the new resource group.</span></span> <span data-ttu-id="a3ba7-138">Хранилище ключей **должно быть доступно для развертывания**. Это позволит поставщику ресурсов Service Fabric получить из него сертификаты и установить их на узлах кластера.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-138">The Key Vault **must be enabled for deployment** to allow the Service Fabric resource provider to get certificates from it and install on cluster nodes:</span></span>

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
                                       Permissions to Keys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions to Secrets   :    all


    Tags                             :
```

<span data-ttu-id="a3ba7-139">При наличии существующего хранилища ключей можно сделать его доступным для развертывания с помощью командной строки Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="a3ba7-139">If you have an existing Key Vault, you can enable it for deployment using Azure CLI:</span></span>

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-to-key-vault"></a><span data-ttu-id="a3ba7-140">Добавление сертификатов в хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="a3ba7-140">Add certificates to Key Vault</span></span>
<span data-ttu-id="a3ba7-141">Сертификаты используются в Service Fabric, чтобы обеспечить функции аутентификации и шифрования для защиты различных аспектов кластера и его приложений.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-141">Certificates are used in Service Fabric to provide authentication and encryption to secure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="a3ba7-142">Дополнительные сведения о том, как сертификаты используются в Service Fabric, см. в статье [Сценарии защиты кластера Service Fabric][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="a3ba7-142">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="a3ba7-143">Сертификат кластера и сервера (обязательно)</span><span class="sxs-lookup"><span data-stu-id="a3ba7-143">Cluster and server certificate (required)</span></span>
<span data-ttu-id="a3ba7-144">Этот сертификат требуется для защиты кластера и предотвращения несанкционированного доступа к нему.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-144">This certificate is required to secure a cluster and prevent unauthorized access to it.</span></span> <span data-ttu-id="a3ba7-145">Он обеспечивает безопасность кластера несколькими способами.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-145">It provides cluster security in a couple ways:</span></span>

* <span data-ttu-id="a3ba7-146">**Аутентификация в кластере** позволяет аутентифицировать обмен данными между узлами для федерации кластера.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-146">**Cluster authentication:** Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="a3ba7-147">Только узлы, которые могут подтвердить свою подлинность с помощью этого сертификата, могут присоединиться к кластеру.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-147">Only nodes that can prove their identity with this certificate can join the cluster.</span></span>
* <span data-ttu-id="a3ba7-148">**Аутентификация сервера** позволяет аутентифицировать конечные точки управления кластера в клиенте управления, чтобы он "знал", что обращается к настоящему кластеру.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-148">**Server authentication:** Authenticates the cluster management endpoints to a management client, so that the management client knows it is talking to the real cluster.</span></span> <span data-ttu-id="a3ba7-149">Этот сертификат также предоставляет SSL для API управления HTTPS и Service Fabric Explorer по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-149">This certificate also provides SSL for the HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="a3ba7-150">Для этого сертификат должен отвечать следующим требованиям:</span><span class="sxs-lookup"><span data-stu-id="a3ba7-150">To serve these purposes, the certificate must meet the following requirements:</span></span>

* <span data-ttu-id="a3ba7-151">Сертификат должен содержать закрытый ключ.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-151">The certificate must contain a private key.</span></span>
* <span data-ttu-id="a3ba7-152">Сертификат должен быть создан для обмена ключами, которые можно экспортировать в файл обмена личной информацией (PFX-файл).</span><span class="sxs-lookup"><span data-stu-id="a3ba7-152">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="a3ba7-153">Имя субъекта сертификата должно совпадать с доменным именем, которое используется для обращения к кластеру Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-153">The certificate's subject name must match the domain used to access the Service Fabric cluster.</span></span> <span data-ttu-id="a3ba7-154">Это необходимо, чтобы предоставить протокол SSL для конечных точек управления HTTPS в кластере и Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-154">This is required to provide SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="a3ba7-155">Невозможно получить SSL-сертификат от центра сертификации (ЦС) для домена `.cloudapp.azure.com` .</span><span class="sxs-lookup"><span data-stu-id="a3ba7-155">You cannot obtain an SSL certificate from a certificate authority (CA) for the `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="a3ba7-156">Необходимо получить имя личного домена для кластера.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-156">Acquire a custom domain name for your cluster.</span></span> <span data-ttu-id="a3ba7-157">При запросе сертификата из ЦС имя субъекта сертификата должно совпадать с именем личного домена, используемого для кластера.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-157">When you request a certificate from a CA the certificate's subject name must match the custom domain name used for your cluster.</span></span>

### <a name="client-authentication-certificates"></a><span data-ttu-id="a3ba7-158">Сертификаты проверки подлинности клиента</span><span class="sxs-lookup"><span data-stu-id="a3ba7-158">Client authentication certificates</span></span>
<span data-ttu-id="a3ba7-159">Дополнительные сертификаты клиента используются для аутентификации администраторов при выполнении задач управления кластером.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-159">Additional client certificates authenticate administrators for cluster management tasks.</span></span> <span data-ttu-id="a3ba7-160">Service Fabric имеет два уровня доступа: **администратор** и **пользователь только для чтения**.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-160">Service Fabric has two access levels: **admin** and **read-only user**.</span></span> <span data-ttu-id="a3ba7-161">Необходимо использовать хотя бы один сертификат для административного доступа.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-161">At minimum, a single certificate for administrative access should be used.</span></span> <span data-ttu-id="a3ba7-162">Для получения дополнительного доступа на уровне пользователя необходимо предоставить отдельный сертификат.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-162">For additional user-level access, a separate certificate must be provided.</span></span> <span data-ttu-id="a3ba7-163">Дополнительные сведения о ролях доступа см. в статье [Контроль доступа на основе ролей для клиентов Service Fabric][service-fabric-cluster-security-roles].</span><span class="sxs-lookup"><span data-stu-id="a3ba7-163">For more information on access roles, see [role-based access control for Service Fabric clients][service-fabric-cluster-security-roles].</span></span>

<span data-ttu-id="a3ba7-164">Для работы с Service Fabric не нужно передавать сертификаты проверки подлинности клиента в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-164">You do not need to upload Client authentication certificates to Key Vault to work with Service Fabric.</span></span> <span data-ttu-id="a3ba7-165">Эти сертификаты должны предоставляться только пользователям, уполномоченным осуществлять управление кластером.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-165">These certificates only need to be provided to users who are authorized for cluster management.</span></span> 

> [!NOTE]
> <span data-ttu-id="a3ba7-166">Azure Active Directory является рекомендуемым способом аутентификации клиентов при допуске к операциям управления кластером.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-166">Azure Active Directory is the recommended way to authenticate clients for cluster management operations.</span></span> <span data-ttu-id="a3ba7-167">Для использования Azure Active Directory необходимо [создать кластер с помощью Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="a3ba7-167">To use Azure Active Directory, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span>
> 
> 

### <a name="application-certificates-optional"></a><span data-ttu-id="a3ba7-168">Сертификаты приложения (необязательно)</span><span class="sxs-lookup"><span data-stu-id="a3ba7-168">Application certificates (optional)</span></span>
<span data-ttu-id="a3ba7-169">В кластере можно установить любое количество дополнительных сертификатов для обеспечения безопасности приложений.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-169">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="a3ba7-170">Перед созданием кластера рассмотрите сценарии безопасности приложений, которые требуют установки сертификатов на узлах, в том числе:</span><span class="sxs-lookup"><span data-stu-id="a3ba7-170">Before creating your cluster, consider the application security scenarios that require a certificate to be installed on the nodes, such as:</span></span>

* <span data-ttu-id="a3ba7-171">шифрование и расшифровка значений конфигурации приложений;</span><span class="sxs-lookup"><span data-stu-id="a3ba7-171">Encryption and decryption of application configuration values</span></span>
* <span data-ttu-id="a3ba7-172">шифрование данных между узлами во время репликации.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-172">Encryption of data across nodes during replication</span></span> 

<span data-ttu-id="a3ba7-173">При создании кластера с помощью портала Azure настройка сертификатов приложения недоступна.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-173">Application certificates cannot be configured when creating a cluster through the Azure portal.</span></span> <span data-ttu-id="a3ba7-174">Чтобы настроить сертификаты приложения в процессе настройки кластера, необходимо [создать кластер с помощью Azure Resource Manager][create-cluster-arm].</span><span class="sxs-lookup"><span data-stu-id="a3ba7-174">To configure application certificates at cluster setup time, you must [create a cluster using Azure Resource Manager][create-cluster-arm].</span></span> <span data-ttu-id="a3ba7-175">Также можно добавить сертификаты приложения в кластер после его создания.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-175">You can also add application certificates to the cluster after it has been created.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="a3ba7-176">Форматирование сертификатов для использования поставщиком ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="a3ba7-176">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="a3ba7-177">Файлы закрытого ключа (PFX-файлы) можно добавить в хранилище ключей и использовать непосредственно из него.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-177">Private key files (.pfx) can be added and used directly through Key Vault.</span></span> <span data-ttu-id="a3ba7-178">Тем не менее поставщику ресурсов Azure необходимо, чтобы ключи хранились в специальном формате JSON, включающем в себя PFX-файл в виде строки в кодировке Base64 и пароль закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-178">However, the Azure resource provider requires keys to be stored in a special JSON format that includes the .pfx as a base-64 encoded string and the private key password.</span></span> <span data-ttu-id="a3ba7-179">Чтобы соблюсти эти требования, ключи должны быть помещены в строку JSON и сохранены как *секреты* в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-179">To accommodate these requirements, keys must be placed in a JSON string and then stored as *secrets* in Key Vault.</span></span>

<span data-ttu-id="a3ba7-180">Для упрощения этого процесса [на сайте GitHub][service-fabric-rp-helpers] доступен соответствующий модуль PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-180">To make this process easier, a PowerShell module is [available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="a3ba7-181">Ниже приведены указания по использованию этого модуля.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-181">Follow these steps to use the module:</span></span>

1. <span data-ttu-id="a3ba7-182">Скачайте все содержимое репозитория в локальный каталог.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-182">Download the entire contents of the repo into a local directory.</span></span> 
2. <span data-ttu-id="a3ba7-183">Импортируйте модуль в окне PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-183">Import the module in your PowerShell window:</span></span>

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

<span data-ttu-id="a3ba7-184">Команда `Invoke-AddCertToKeyVault` в этом модуле PowerShell автоматически форматирует закрытый ключ сертификата в строку JSON и передает ее в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-184">The `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it to Key Vault.</span></span> <span data-ttu-id="a3ba7-185">Используйте его для добавления сертификата кластера и всех дополнительных сертификатов приложения в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-185">Use it to add the cluster certificate and any additional application certificates to Key Vault.</span></span> <span data-ttu-id="a3ba7-186">Повторите этот шаг для всех дополнительных сертификатов, которые нужно установить в кластере.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-186">Repeat this step for any additional certificates you want to install in your cluster.</span></span>

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context to SubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: The output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret to myvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

<span data-ttu-id="a3ba7-187">Это все обязательные компоненты хранилища ключей, необходимые для настройки шаблона Resource Manager кластера Service Fabric, который устанавливает сертификаты для аутентификации на узлах, защиты конечных точек управления и аутентификации на них, а также для каких-либо дополнительных функций безопасности приложений, которые используют сертификаты X.509.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-187">These are all the Key Vault prerequisites for configuring a Service Fabric cluster Resource Manager template that installs certificates for node authentication, management endpoint security and authentication, and any additional application security features that use X.509 certificates.</span></span> <span data-ttu-id="a3ba7-188">На этом этапе в Azure должна быть представлена следующая конфигурация:</span><span class="sxs-lookup"><span data-stu-id="a3ba7-188">At this point, you should now have the following setup in Azure:</span></span>

* <span data-ttu-id="a3ba7-189">группа ресурсов хранилища ключей;</span><span class="sxs-lookup"><span data-stu-id="a3ba7-189">Key Vault resource group</span></span>
  * <span data-ttu-id="a3ba7-190">хранилище ключей;</span><span class="sxs-lookup"><span data-stu-id="a3ba7-190">Key Vault</span></span>
    * <span data-ttu-id="a3ba7-191">сертификат проверки подлинности сервера кластера;</span><span class="sxs-lookup"><span data-stu-id="a3ba7-191">Cluster server authentication certificate</span></span>

<span data-ttu-id="a3ba7-192"></a "create-cluster-portal" ></a></span><span class="sxs-lookup"><span data-stu-id="a3ba7-192"></a "create-cluster-portal" ></a></span></span>

## <a name="create-cluster-in-the-azure-portal"></a><span data-ttu-id="a3ba7-193">Создание кластера на портале Azure</span><span class="sxs-lookup"><span data-stu-id="a3ba7-193">Create cluster in the Azure portal</span></span>
### <a name="search-for-the-service-fabric-cluster-resource"></a><span data-ttu-id="a3ba7-194">Поиск кластерных ресурсов Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a3ba7-194">Search for the Service Fabric cluster resource</span></span>
![поиск шаблона кластера Service Fabric на портале Azure.][SearchforServiceFabricClusterTemplate]

1. <span data-ttu-id="a3ba7-196">Войдите на [портал Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="a3ba7-196">Sign in to the [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="a3ba7-197">Щелкните **Создать** , чтобы добавить новый шаблон ресурсов.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-197">Click **New** to add a new resource template.</span></span> <span data-ttu-id="a3ba7-198">Найдите шаблон "Кластер Service Fabric" в **Marketplace** в разделе **Все**.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-198">Search for the Service Fabric Cluster template in the **Marketplace** under **Everything**.</span></span>
3. <span data-ttu-id="a3ba7-199">Выберите в списке **Кластер Service Fabric** .</span><span class="sxs-lookup"><span data-stu-id="a3ba7-199">Select **Service Fabric Cluster** from the list.</span></span>
4. <span data-ttu-id="a3ba7-200">Перейдите к колонке **Кластер Service Fabric** и выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-200">Navigate to the **Service Fabric Cluster** blade, click **Create**,</span></span>
5. <span data-ttu-id="a3ba7-201">В колонке **Создание кластера Service Fabric** необходимо выполнить четыре шага.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-201">The **Create Service Fabric cluster** blade has the following four steps.</span></span>

#### <a name="1-basics"></a><span data-ttu-id="a3ba7-202">1. Основы</span><span class="sxs-lookup"><span data-stu-id="a3ba7-202">1. Basics</span></span>
![Снимок экрана: создание группы ресурсов.][CreateRG]

<span data-ttu-id="a3ba7-204">В колонке "Основные сведения" требуется указать основные сведения для кластера.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-204">In the Basics blade you need to provide the basic details for your cluster.</span></span>

1. <span data-ttu-id="a3ba7-205">Введите имя кластера.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-205">Enter the name of your cluster.</span></span>
2. <span data-ttu-id="a3ba7-206">Введите **имя пользователя** и **пароль** для удаленного рабочего стола виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-206">Enter a **user name** and **password** for Remote Desktop for the VMs.</span></span>
3. <span data-ttu-id="a3ba7-207">Выберите **подписку** , в которой вы хотите развернуть кластер, особенно при наличии нескольких подписок.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-207">Make sure to select the **Subscription** that you want your cluster to be deployed to, especially if you have multiple subscriptions.</span></span>
4. <span data-ttu-id="a3ba7-208">Создайте **новую группу ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-208">Create a **new resource group**.</span></span> <span data-ttu-id="a3ba7-209">Рекомендуется присвоить ей имя, совпадающее с именем кластера. Это облегчит дальнейший поиск, особенно при внесении изменений в развертывание или удалении кластера.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-209">It is best to give it the same name as the cluster, since it helps in finding them later, especially when you are trying to make changes to your deployment or delete your cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a3ba7-210">Хотя вы можете использовать существующую группу ресурсов, рекомендуется создать новую.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-210">Although you can decide to use an existing resource group, it is a good practice to create a new resource group.</span></span> <span data-ttu-id="a3ba7-211">Это позволит легко удалить ненужные кластеры.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-211">This makes it easy to delete clusters that you do not need.</span></span>
   > 
   > 
5. <span data-ttu-id="a3ba7-212">Выберите **регион** , в котором требуется создать кластер.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-212">Select the **region** in which you want to create the cluster.</span></span> <span data-ttu-id="a3ba7-213">Необходимо использовать тот же регион, в котором расположено ваше хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-213">You must use the same region that your Key Vault is in.</span></span>

#### <a name="2-cluster-configuration"></a><span data-ttu-id="a3ba7-214">2) Конфигурация кластера</span><span class="sxs-lookup"><span data-stu-id="a3ba7-214">2. Cluster configuration</span></span>
![Создание типа узла][CreateNodeType]

<span data-ttu-id="a3ba7-216">Настройте узлы кластера.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-216">Configure your cluster nodes.</span></span> <span data-ttu-id="a3ba7-217">Он определяет размер виртуальных машин, их количество и свойства.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-217">Node types define the VM sizes, the number of VMs, and their properties.</span></span> <span data-ttu-id="a3ba7-218">Кластер может содержать узлы нескольких типов, однако первичный узел (тот, который вы задали на портале) должен включать не менее пяти виртуальных машин, так как на узлах такого типа расположены системные службы Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-218">Your cluster can have more than one node type, but the primary node type (the first one that you define on the portal) must have at least five VMs, as this is the node type where Service Fabric system services are placed.</span></span> <span data-ttu-id="a3ba7-219">Не настраивайте параметры **Свойства размещения** , так как стандартное свойство размещения NodeTypeName добавляется автоматически.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-219">Do not configure **Placement Properties** because a default placement property of "NodeTypeName" is added automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="a3ba7-220">Распространенный сценарий для нескольких типов узлов — это приложение, содержащее интерфейсную и серверную службы.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-220">A common scenario for multiple node types is an application that contains a front-end service and a back-end service.</span></span> <span data-ttu-id="a3ba7-221">Интерфейсную службу нужно разместить на виртуальных машинах меньшего размера (например, D2) с портами, открытыми для доступа через Интернет, а серверную службу — на более крупных виртуальных машинах (D4, D6, D15 и т. д.) без портов, имеющих выход в Интернет.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-221">You want to put the front-end service on smaller VMs (VM sizes like D2) with ports open to the Internet, but you want to put the back-end service on larger VMs (with VM sizes like D4, D6, D15, and so on) with no Internet-facing ports open.</span></span>
> 
> 

1. <span data-ttu-id="a3ba7-222">Выберите имя для типа узла (от 1 до 12 буквенно-цифровых символов).</span><span class="sxs-lookup"><span data-stu-id="a3ba7-222">Choose a name for your node type (1 to 12 characters containing only letters and numbers).</span></span>
2. <span data-ttu-id="a3ba7-223">Минимальный **размер** виртуальных машин для первичного узла зависит от выбранного для кластера уровня **устойчивости**.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-223">The minimum **size** of VMs for the primary node type is driven by the **durability** tier you choose for the cluster.</span></span> <span data-ttu-id="a3ba7-224">Значение по умолчанию для уровня устойчивости — bronze (бронзовый).</span><span class="sxs-lookup"><span data-stu-id="a3ba7-224">The default for the durability tier is bronze.</span></span> <span data-ttu-id="a3ba7-225">Дополнительные сведения об уровнях устойчивости см. в статье [Рекомендации по планированию загрузки кластера Service Fabric][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="a3ba7-225">For more information on durability, see [how to choose the Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
3. <span data-ttu-id="a3ba7-226">Выберите ценовую категорию и размер виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-226">Select the VM size and pricing tier.</span></span> <span data-ttu-id="a3ba7-227">Виртуальные машины серии D оснащены твердотельными накопителями (SSD) и настоятельно рекомендуются для приложений с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-227">D-series VMs have SSD drives and are highly recommended for stateful applications.</span></span> <span data-ttu-id="a3ba7-228">Не используйте SKU виртуальной машины с частичными ядрами и менее чем 7 ГБ свободного места на диске.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-228">Do not use any VM SKU that has partial cores or have less than 7 GB of available disk capacity.</span></span> 
4. <span data-ttu-id="a3ba7-229">Минимальное **количество** виртуальных машин для первичного узла зависит от выбранного для кластера уровня **надежности**.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-229">The minimum **number** of VMs for the primary node type is driven by the **reliability** tier you choose.</span></span> <span data-ttu-id="a3ba7-230">Значение по умолчанию для уровня надежности — Silver.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-230">The default for the reliability tier is Silver.</span></span> <span data-ttu-id="a3ba7-231">Дополнительные сведения о надежности см. в статье [Рекомендации по планированию загрузки кластера Service Fabric][service-fabric-cluster-capacity].</span><span class="sxs-lookup"><span data-stu-id="a3ba7-231">For more information on reliability, see [how to choose the Service Fabric cluster reliability and durability][service-fabric-cluster-capacity].</span></span>
5. <span data-ttu-id="a3ba7-232">Выберите количество виртуальных машин для типа узла.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-232">Choose the number of VMs for the node type.</span></span> <span data-ttu-id="a3ba7-233">Количество виртуальных машин для типа узла можно увеличить или уменьшить позже, но минимальное количество виртуальных машин на первичном узле зависит от выбранного уровня надежности.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-233">You can scale up or down the number of VMs in a node type later on, but on the primary node type, the minimum is driven by the reliability level that you have chosen.</span></span> <span data-ttu-id="a3ba7-234">Для других типов узлов можно задать минимум 1 виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-234">Other node types can have a minimum of 1 VM.</span></span>
6. <span data-ttu-id="a3ba7-235">Настройте пользовательские конечные точки.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-235">Configure custom endpoints.</span></span> <span data-ttu-id="a3ba7-236">Это поле позволяет ввести список портов с разделителями-запятыми. С помощью Azure Load Balancer для приложений будет открыт общий доступ через Интернет к указанным здесь портам.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-236">This field allows you to enter a comma-separated list of ports that you want to expose through the Azure Load Balancer to the public Internet for your applications.</span></span> <span data-ttu-id="a3ba7-237">Например, если вы планируете развернуть в своем кластере веб-приложение, то введите здесь "80", чтобы разрешить в этом кластере трафик через порт 80.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-237">For example, if you plan to deploy a web application to your cluster, enter "80" here to allow traffic on port 80 into your cluster.</span></span> <span data-ttu-id="a3ba7-238">Дополнительные сведения о конечных точках см. в статье [Подключение к службам в Service Fabric и взаимодействие с ними][service-fabric-connect-and-communicate-with-services].</span><span class="sxs-lookup"><span data-stu-id="a3ba7-238">For more information on endpoints, see [communicating with applications][service-fabric-connect-and-communicate-with-services]</span></span>
7. <span data-ttu-id="a3ba7-239">Настройте **систему диагностики** кластера.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-239">Configure cluster **diagnostics**.</span></span> <span data-ttu-id="a3ba7-240">Диагностика в кластере включена по умолчанию. Это упрощает устранение неполадок.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-240">By default, diagnostics are enabled on your cluster to assist with troubleshooting issues.</span></span> <span data-ttu-id="a3ba7-241">Если вы хотите отключить систему диагностики, установите переключатель **Состояние** в положение **Выкл**.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-241">If you want to disable diagnostics change the **Status** toggle to **Off**.</span></span> <span data-ttu-id="a3ba7-242">Отключать систему диагностики **не** рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-242">Turning off diagnostics is **not** recommended.</span></span>
8. <span data-ttu-id="a3ba7-243">Выберите режим обновления Service Fabric, который необходимо задать для кластера.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-243">Select the Fabric upgrade mode you want set your cluster to.</span></span> <span data-ttu-id="a3ba7-244">Если требуется, чтобы система автоматически получала последнюю версию и выполняла попытку обновить до нее кластер, выберите пункт **Автоматически**.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-244">Select **Automatic**, if you want the system to automatically pick up the latest available version and try to upgrade your cluster to it.</span></span> <span data-ttu-id="a3ba7-245">Если вы хотите выбирать поддерживаемую версию, задайте режим **Вручную**.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-245">Set the mode to **Manual**, if you want to choose a supported version.</span></span>

> [!NOTE]
> <span data-ttu-id="a3ba7-246">Корпорация Майкрософт поддерживает только кластеры под управлением поддерживаемых версий Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-246">We support only clusters that are running supported versions of service Fabric.</span></span> <span data-ttu-id="a3ba7-247">Выбрав режим **Вручную**, вы принимаете на себя ответственность за обновление кластера до поддерживаемой версии.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-247">By selecting the **Manual** mode, you are taking on the responsibility to upgrade your cluster to a supported version.</span></span> <span data-ttu-id="a3ba7-248">Дополнительные сведения о режиме обновления Service Fabric см. в статье [Обновление кластера Service Fabric][service-fabric-cluster-upgrade].</span><span class="sxs-lookup"><span data-stu-id="a3ba7-248">For more details on the Fabric upgrade mode see the [service-fabric-cluster-upgrade document.][service-fabric-cluster-upgrade]</span></span>
> 
> 

#### <a name="3-security"></a><span data-ttu-id="a3ba7-249">3. Безопасность</span><span class="sxs-lookup"><span data-stu-id="a3ba7-249">3. Security</span></span>
![Снимок экрана: настройка безопасности на портале Azure.][SecurityConfigs]

<span data-ttu-id="a3ba7-251">Последним шагом является предоставление сведений о сертификате для защиты кластера с помощью хранилища ключей, а также ранее созданных сведений о сертификате.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-251">The final step is to provide certificate information to secure the cluster using the Key Vault and certificate information created earlier.</span></span>

* <span data-ttu-id="a3ba7-252">Заполните поля основного сертификата, используя выходные данные, полученные при передаче **сертификата кластера** в хранилище ключей с помощью команды PowerShell `Invoke-AddCertToKeyVault`.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-252">Populate the primary certificate fields with the output obtained from uploading the **cluster certificate** to Key Vault using the `Invoke-AddCertToKeyVault` PowerShell command.</span></span>

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* <span data-ttu-id="a3ba7-253">Установите флажок **Настройка дополнительных параметров**, чтобы ввести сертификаты клиента в поля **Клиент администратора** и **Клиент только для чтения**.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-253">Check the **Configure advanced settings** box to enter client certificates for **admin client** and **read-only client**.</span></span> <span data-ttu-id="a3ba7-254">В эти поля введите отпечаток сертификата клиента администратора и отпечаток сертификата клиента только для чтения (при наличии).</span><span class="sxs-lookup"><span data-stu-id="a3ba7-254">In these fields, enter the thumbprint of your admin client certificate and the thumbprint of your read-only user client certificate, if applicable.</span></span> <span data-ttu-id="a3ba7-255">Когда администраторы пытаются подключиться к кластеру, им предоставляется доступ только в том случае, если у них есть сертификат с отпечатком, соответствующим указанным здесь значениям.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-255">When administrators attempt to connect to the cluster, they are granted access only if they have a certificate with a thumbprint that matches the thumbprint values entered here.</span></span>  

#### <a name="4-summary"></a><span data-ttu-id="a3ba7-256">4. Сводка</span><span class="sxs-lookup"><span data-stu-id="a3ba7-256">4. Summary</span></span>
![<span data-ttu-id="a3ba7-257">Снимок экрана: начальная доска с заголовком "Развертывание кластера Service Fabric".</span><span class="sxs-lookup"><span data-stu-id="a3ba7-257">Screen shot of the start board displaying "Deploying Service Fabric Cluster."</span></span> ][Notifications]

<span data-ttu-id="a3ba7-258">Чтобы завершить создание кластера, выберите **Сводка** и проверьте указанные параметры или скачайте шаблон Azure Resource Manager, который используется для развертывания кластера.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-258">To complete the cluster creation, click **Summary** to see the configurations that you have provided, or download the Azure Resource Manager template that that used to deploy your cluster.</span></span> <span data-ttu-id="a3ba7-259">После указания обязательных параметров активируется кнопка **ОК**. Нажав ее, вы сможете начать процесс создания кластера.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-259">After you have provided the mandatory settings, the **OK** button becomes green and you can start the cluster creation process by clicking it.</span></span>

<span data-ttu-id="a3ba7-260">Ход создания кластера будет отображаться в области уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-260">You can see the creation progress in the notifications.</span></span> <span data-ttu-id="a3ba7-261">(Щелкните значок колокольчика рядом со строкой состояния в правом верхнем углу экрана). Если при создании кластера вы установили флажок **Закрепить на начальной панели**, то на **начальной доске** вы увидите закрепленный элемент **Развертывание кластера Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-261">(Click the "Bell" icon near the status bar at the upper right of your screen.) If you clicked **Pin to Startboard** while creating the cluster, you will see **Deploying Service Fabric Cluster** pinned to the **Start** board.</span></span>

### <a name="view-your-cluster-status"></a><span data-ttu-id="a3ba7-262">Просмотр состояния кластера</span><span class="sxs-lookup"><span data-stu-id="a3ba7-262">View your cluster status</span></span>
![Снимок экрана: сведения о кластере на панели мониторинга.][ClusterDashboard]

<span data-ttu-id="a3ba7-264">После создания кластера его можно просмотреть на портале.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-264">Once your cluster is created, you can inspect your cluster in the portal:</span></span>

1. <span data-ttu-id="a3ba7-265">Щелкните **Обзор** и выберите **Кластеры Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-265">Go to **Browse** and click **Service Fabric Clusters**.</span></span>
2. <span data-ttu-id="a3ba7-266">Найдите нужный кластер и щелкните его.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-266">Locate your cluster and click it.</span></span>
3. <span data-ttu-id="a3ba7-267">На панели мониторинга отобразятся подробные сведения о кластере, включая общедоступную конечную точку кластера и ссылку на Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-267">You can now see the details of your cluster in the dashboard, including the cluster's public endpoint and a link to Service Fabric Explorer.</span></span>

<span data-ttu-id="a3ba7-268">В разделе **Монитор узла** колонки панели мониторинга кластера отображается количество работоспособных и неработоспособных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-268">The **Node Monitor** section on the cluster's dashboard blade indicates the number of VMs that are healthy and not healthy.</span></span> <span data-ttu-id="a3ba7-269">Дополнительные сведения о состоянии работоспособности кластеров см. в статье [Общие сведения о наблюдении за работоспособностью системы в Service Fabric][service-fabric-health-introduction].</span><span class="sxs-lookup"><span data-stu-id="a3ba7-269">You can find more details about the cluster's health at [Service Fabric health model introduction][service-fabric-health-introduction].</span></span>

> [!NOTE]
> <span data-ttu-id="a3ba7-270">Для постоянной работы кластеров Service Fabric требуется определенное количество узлов, чтобы все время поддерживать доступность и сохранять состояние, которое называется "поддержание кворума".</span><span class="sxs-lookup"><span data-stu-id="a3ba7-270">Service Fabric clusters require a certain number of nodes to be up always to maintain availability and preserve state - referred to as "maintaining quorum".</span></span> <span data-ttu-id="a3ba7-271">Поэтому обычно не рекомендуется завершать работу всех виртуальных машин в кластере, пока не будет выполнена [полная архивация состояния][service-fabric-reliable-services-backup-restore], так как это может быть небезопасно.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-271">Therfore, it is typically not safe to shut down all machines in the cluster unless you have first performed a [full backup of your state][service-fabric-reliable-services-backup-restore].</span></span>
> 
> 

## <a name="remote-connect-to-a-virtual-machine-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="a3ba7-272">Удаленное подключение к экземпляру из набора масштабирования виртуальных машин или узлу кластера</span><span class="sxs-lookup"><span data-stu-id="a3ba7-272">Remote connect to a Virtual Machine Scale Set instance or a cluster node</span></span>
<span data-ttu-id="a3ba7-273">Каждый из типов узлов, задаваемый в кластере, отражается на конфигурации масштабируемого набора виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-273">Each of the NodeTypes you specify in your cluster results in a Virtual Machine Scale Set getting set-up.</span></span> <span data-ttu-id="a3ba7-274">Подробные сведения см. в разделе [Удаленное подключение к экземпляру из масштабируемого набора виртуальных машин][remote-connect-to-a-vm-scale-set].</span><span class="sxs-lookup"><span data-stu-id="a3ba7-274">See [Remote connect to a Virtual Machine Scale Set instance][remote-connect-to-a-vm-scale-set] for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3ba7-275">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a3ba7-275">Next steps</span></span>
<span data-ttu-id="a3ba7-276">На этом этапе у вас имеется защищенный кластер, использующий сертификаты для аутентификации управления.</span><span class="sxs-lookup"><span data-stu-id="a3ba7-276">At this point, you have a secure cluster using certificates for management authentication.</span></span> <span data-ttu-id="a3ba7-277">Далее [подключитесь к этому кластеру](service-fabric-connect-to-secure-cluster.md) и узнайте, как [управлять секретами приложений](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="a3ba7-277">Next, [connect to your cluster](service-fabric-connect-to-secure-cluster.md) and learn how to [manage application secrets](service-fabric-application-secret-management.md).</span></span>  <span data-ttu-id="a3ba7-278">Кроме того, узнайте [о вариантах поддержки Service Fabric](service-fabric-support.md).</span><span class="sxs-lookup"><span data-stu-id="a3ba7-278">Also, learn about [Service Fabric support options](service-fabric-support.md).</span></span>

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
