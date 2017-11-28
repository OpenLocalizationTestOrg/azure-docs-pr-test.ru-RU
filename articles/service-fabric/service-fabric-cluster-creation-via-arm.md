---
title: "aaaCreate Azure Service Fabric кластера из шаблона | Документы Microsoft"
description: "В этой статье описывается, как tooset копирование безопасного Service Fabric кластер в Azure с помощью диспетчера ресурсов Azure, хранилище ключей Azure и Azure Active Directory (Azure AD) для проверки подлинности клиента."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: chackdan
ms.assetid: 15d0ab67-fc66-4108-8038-3584eeebabaa
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: chackdan
ms.openlocfilehash: a4563c58a68127720a8290c3be0df9d026833eb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a><span data-ttu-id="5096e-103">Создание кластера Service Fabric в Azure с помощью Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5096e-103">Create a Service Fabric cluster by using Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5096e-104">Диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="5096e-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="5096e-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="5096e-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
>
>

<span data-ttu-id="5096e-106">Это пошаговое руководство поможет выполнить настройку защищенного кластера Azure Service Fabric в Azure с помощью Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5096e-106">This step-by-step guide walks you through setting up a secure Azure Service Fabric cluster in Azure by using Azure Resource Manager.</span></span> <span data-ttu-id="5096e-107">Мы подтверждаю, что эту статью hello велика.</span><span class="sxs-lookup"><span data-stu-id="5096e-107">We acknowledge that hello article is long.</span></span> <span data-ttu-id="5096e-108">Тем не менее если вы уже знакомы тщательно с содержимым hello, быть toofollow убедиться, что каждый шаг внимательно.</span><span class="sxs-lookup"><span data-stu-id="5096e-108">Nevertheless, unless you are already thoroughly familiar with hello content, be sure toofollow each step carefully.</span></span>

<span data-ttu-id="5096e-109">Hello руководстве описываются hello следующих процедур:</span><span class="sxs-lookup"><span data-stu-id="5096e-109">hello guide covers hello following procedures:</span></span>

* <span data-ttu-id="5096e-110">Настройка сертификатов tooupload хранилища ключей Azure для обеспечения безопасности кластера и приложения</span><span class="sxs-lookup"><span data-stu-id="5096e-110">Setting up an Azure key vault tooupload certificates for cluster and application security</span></span>
* <span data-ttu-id="5096e-111">Создание защищенного кластера в Azure с помощью Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5096e-111">Creating a secured cluster in Azure by using Azure Resource Manager</span></span>
* <span data-ttu-id="5096e-112">Аутентификация пользователей с помощью Azure Active Directory для управления кластером</span><span class="sxs-lookup"><span data-stu-id="5096e-112">Authenticating users by using Azure Active Directory (Azure AD) for cluster management</span></span>

<span data-ttu-id="5096e-113">Безопасный кластер — это кластер, предотвращает несанкционированный доступ toomanagement операции.</span><span class="sxs-lookup"><span data-stu-id="5096e-113">A secure cluster is a cluster that prevents unauthorized access toomanagement operations.</span></span> <span data-ttu-id="5096e-114">Это включает в себя развертывание, обновление и удаление приложений, служб и данных hello, содержащихся в них.</span><span class="sxs-lookup"><span data-stu-id="5096e-114">This includes deploying, upgrading, and deleting applications, services, and hello data they contain.</span></span> <span data-ttu-id="5096e-115">Небезопасные кластер — это кластер, что любой пользователь может подключиться tooat в любое время и выполнять операции управления.</span><span class="sxs-lookup"><span data-stu-id="5096e-115">An unsecure cluster is a cluster that anyone can connect tooat any time and perform management operations.</span></span> <span data-ttu-id="5096e-116">Несмотря на возможные toocreate кластер небезопасным, настоятельно рекомендуется создать безопасный кластер с самого начала hello.</span><span class="sxs-lookup"><span data-stu-id="5096e-116">Although it is possible toocreate an unsecure cluster, we highly recommend that you create a secure cluster from hello outset.</span></span> <span data-ttu-id="5096e-117">Поскольку незащищенный кластер невозможно будет защитить позднее, нужно создать новый кластер.</span><span class="sxs-lookup"><span data-stu-id="5096e-117">Because an unsecure cluster cannot be secured later, a new cluster must be created.</span></span>

<span data-ttu-id="5096e-118">Понятие Hello создания защищенных кластеров является hello одинаковым, являются ли они кластеров Windows или Linux.</span><span class="sxs-lookup"><span data-stu-id="5096e-118">hello concept of creating secure clusters is hello same, whether they are Linux or Windows clusters.</span></span> <span data-ttu-id="5096e-119">Дополнительные сведения о создании безопасных кластеров Linux, а также вспомогательные скрипты см. в разделе [Создание безопасных кластеров в Linux](#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="5096e-119">For more information and helper scripts for creating secure Linux clusters, see [Creating secure clusters on Linux](#secure-linux-clusters).</span></span>

## <a name="sign-in-tooyour-azure-account"></a><span data-ttu-id="5096e-120">Войдите в tooyour учетная запись Azure</span><span class="sxs-lookup"><span data-stu-id="5096e-120">Sign in tooyour Azure account</span></span>
<span data-ttu-id="5096e-121">В этом руководстве используется [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="5096e-121">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="5096e-122">При запуске нового сеанса PowerShell, войдите в tooyour учетная запись Azure и выберите подписку, перед выполнением команды Azure.</span><span class="sxs-lookup"><span data-stu-id="5096e-122">When you start a new PowerShell session, sign in tooyour Azure account and select your subscription before you execute Azure commands.</span></span>

<span data-ttu-id="5096e-123">Войдите в tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="5096e-123">Sign in tooyour Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="5096e-124">Выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="5096e-124">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a><span data-ttu-id="5096e-125">Настройка хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="5096e-125">Set up a key vault</span></span>
<span data-ttu-id="5096e-126">В этом разделе описывается, как создать хранилище ключей для кластера Service Fabric в Azure и приложений Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5096e-126">This section discusses creating a key vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="5096e-127">Полное руководство по tooAzure хранилище ключей см. в разделе toohello [хранилище ключей Знакомство с][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="5096e-127">For a complete guide tooAzure Key Vault, refer toohello [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="5096e-128">Service Fabric использует сертификаты X.509 toosecure кластера и обеспечивает функции безопасности приложения.</span><span class="sxs-lookup"><span data-stu-id="5096e-128">Service Fabric uses X.509 certificates toosecure a cluster and provide application security features.</span></span> <span data-ttu-id="5096e-129">Использовать хранилище ключей toomanage сертификаты для кластеров Service Fabric в Azure.</span><span class="sxs-lookup"><span data-stu-id="5096e-129">You use Key Vault toomanage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="5096e-130">При развертывании в Azure, hello поставщика ресурсов Azure, который отвечает за создание кластеров Service Fabric извлекает сертификаты из хранилища ключей и устанавливает их на кластере hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5096e-130">When a cluster is deployed in Azure, hello Azure resource provider that's responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on hello cluster VMs.</span></span>

<span data-ttu-id="5096e-131">Hello следующей схеме показана связь hello хранилище ключей Azure, кластер Service Fabric и hello поставщика ресурсов Azure, которая использует сертификаты, хранящиеся в хранилище ключей при создании кластера.</span><span class="sxs-lookup"><span data-stu-id="5096e-131">hello following diagram illustrates hello relationship between Azure Key Vault, a Service Fabric cluster, and hello Azure resource provider that uses certificates stored in a key vault when it creates a cluster:</span></span>

![Схема установки сертификата][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="5096e-133">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="5096e-133">Create a resource group</span></span>
<span data-ttu-id="5096e-134">Hello первым шагом является toocreate группы ресурсов, в частности для хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="5096e-134">hello first step is toocreate a resource group specifically for your key vault.</span></span> <span data-ttu-id="5096e-135">Рекомендуется поместить hello хранилища ключей в отдельной группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5096e-135">We recommend that you put hello key vault into its own resource group.</span></span> <span data-ttu-id="5096e-136">Это действие позволяет удалить hello вычислений и хранения групп ресурсов, включая hello группы ресурсов, содержащем кластер Service Fabric, без потери ключи и секретные коды.</span><span class="sxs-lookup"><span data-stu-id="5096e-136">This action lets you remove hello compute and storage resource groups, including hello resource group that contains your Service Fabric cluster, without losing your keys and secrets.</span></span> <span data-ttu-id="5096e-137">группы ресурсов Hello, содержащий ваше хранилище ключа _должен находиться в hello одного региона_ как кластер hello, он используется.</span><span class="sxs-lookup"><span data-stu-id="5096e-137">hello resource group that contains your key vault _must be in hello same region_ as hello cluster that is using it.</span></span>

<span data-ttu-id="5096e-138">Если планируется toodeploy кластеров в нескольких регионах, мы советуем использовать имя группы ресурсов hello и hello хранилища ключей, в результате которого указывает область, которая принадлежит.</span><span class="sxs-lookup"><span data-stu-id="5096e-138">If you plan toodeploy clusters in multiple regions, we suggest that you name hello resource group and hello key vault in a way that indicates which region it belongs to.</span></span>  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
<span data-ttu-id="5096e-139">Hello вывод должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5096e-139">hello output should look like this:</span></span>

```powershell

    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-hello-new-resource-group"></a><span data-ttu-id="5096e-140">Создание хранилища ключей в новую группу ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="5096e-140">Create a key vault in hello new resource group</span></span>
<span data-ttu-id="5096e-141">хранилище ключей Hello _должна быть включена для развертывания_ tooallow hello сертификаты tooget поставщика вычислительных ресурсов от него и установите его на экземпляры виртуальной машины:</span><span class="sxs-lookup"><span data-stu-id="5096e-141">hello key vault _must be enabled for deployment_ tooallow hello compute resource provider tooget certificates from it and install it on virtual machine instances:</span></span>

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

<span data-ttu-id="5096e-142">Hello вывод должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5096e-142">hello output should look like this:</span></span>

```powershell

    Vault Name                       : mywestusvault
    Resource Group Name              : westus-mykeyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault
    Vault URI                        : https://mywestusvault.vault.azure.net
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
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a><span data-ttu-id="5096e-143">Использование существующего хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="5096e-143">Use an existing key vault</span></span>

<span data-ttu-id="5096e-144">toouse существующего хранилища ключей, вы _необходимо включить его для развертывания_ tooallow hello сертификаты tooget поставщика вычислительных ресурсов от него и установите его на узлах кластера:</span><span class="sxs-lookup"><span data-stu-id="5096e-144">toouse an existing key vault, you _must enable it for deployment_ tooallow hello compute resource provider tooget certificates from it and install it on cluster nodes:</span></span>

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-tooyour-key-vault"></a><span data-ttu-id="5096e-145">Добавление хранилища ключей tooyour сертификатов</span><span class="sxs-lookup"><span data-stu-id="5096e-145">Add certificates tooyour key vault</span></span>

<span data-ttu-id="5096e-146">Сертификаты используются в Service Fabric tooprovide проверки подлинности и шифрования toosecure различные аспекты кластера и его применения.</span><span class="sxs-lookup"><span data-stu-id="5096e-146">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="5096e-147">Дополнительные сведения о том, как сертификаты используются в Service Fabric, см. в статье [Сценарии защиты кластера Service Fabric][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="5096e-147">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="5096e-148">Сертификат кластера и сервера (обязательно)</span><span class="sxs-lookup"><span data-stu-id="5096e-148">Cluster and server certificate (required)</span></span>
<span data-ttu-id="5096e-149">Этот сертификат является обязательным toosecure кластером и предотвратить несанкционированный доступ tooit.</span><span class="sxs-lookup"><span data-stu-id="5096e-149">This certificate is required toosecure a cluster and prevent unauthorized access tooit.</span></span> <span data-ttu-id="5096e-150">Он обеспечивает безопасность кластера двумя способами.</span><span class="sxs-lookup"><span data-stu-id="5096e-150">It provides cluster security in two ways:</span></span>

* <span data-ttu-id="5096e-151">Аутентификация в кластере позволяет аутентифицировать обмен данными между узлами для федерации кластера.</span><span class="sxs-lookup"><span data-stu-id="5096e-151">Cluster authentication: Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="5096e-152">Только узлы, которые можно подтвердить свою личность с помощью этого сертификата можно соединить hello кластера.</span><span class="sxs-lookup"><span data-stu-id="5096e-152">Only nodes that can prove their identity with this certificate can join hello cluster.</span></span>
* <span data-ttu-id="5096e-153">Проверка подлинности сервера: проверяет подлинность hello кластера управления конечными точками tooa клиента управления, чтобы hello управления клиент узнает, осуществляет обмен данными toohello реальные кластера.</span><span class="sxs-lookup"><span data-stu-id="5096e-153">Server authentication: Authenticates hello cluster management endpoints tooa management client, so that hello management client knows it is talking toohello real cluster.</span></span> <span data-ttu-id="5096e-154">Этот сертификат также предоставляет SSL для hello API управления HTTPS и обозреватель Service Fabric по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5096e-154">This certificate also provides an SSL for hello HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="5096e-155">tooserve этих целей, hello сертификат должен удовлетворять hello следующие требования:</span><span class="sxs-lookup"><span data-stu-id="5096e-155">tooserve these purposes, hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="5096e-156">Hello сертификат должен содержать закрытый ключ.</span><span class="sxs-lookup"><span data-stu-id="5096e-156">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="5096e-157">необходимо создать сертификат Hello для обмена ключами, который является tooa экспортируемый файл обмена личной информацией (PFX-файл).</span><span class="sxs-lookup"><span data-stu-id="5096e-157">hello certificate must be created for key exchange, which is exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="5096e-158">Имя субъекта сертификата Hello должен соответствовать домену hello, использовать кластер Service Fabric tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="5096e-158">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="5096e-159">Это сопоставление является обязательным tooprovide SSL для конечных точек управления HTTPS hello кластера и обозреватель Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5096e-159">This matching is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="5096e-160">Не удается получить SSL-сертификат центра сертификации (ЦС), для hello. cloudapp.azure.com домена.</span><span class="sxs-lookup"><span data-stu-id="5096e-160">You cannot obtain an SSL certificate from a certificate authority (CA) for hello .cloudapp.azure.com domain.</span></span> <span data-ttu-id="5096e-161">Необходимо получить имя личного домена для кластера.</span><span class="sxs-lookup"><span data-stu-id="5096e-161">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="5096e-162">При запросить сертификат от центра сертификации, hello имя субъекта сертификата должно соответствовать hello собственное доменное имя для вашего кластера.</span><span class="sxs-lookup"><span data-stu-id="5096e-162">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

### <a name="application-certificates-optional"></a><span data-ttu-id="5096e-163">Сертификаты приложения (необязательно)</span><span class="sxs-lookup"><span data-stu-id="5096e-163">Application certificates (optional)</span></span>
<span data-ttu-id="5096e-164">В кластере можно установить любое количество дополнительных сертификатов для обеспечения безопасности приложений.</span><span class="sxs-lookup"><span data-stu-id="5096e-164">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="5096e-165">Перед созданием кластера, рассмотрим hello безопасности приложений, требующих toobe сертификатов, установленных на узлах hello, такие как:</span><span class="sxs-lookup"><span data-stu-id="5096e-165">Before creating your cluster, consider hello application security scenarios that require a certificate toobe installed on hello nodes, such as:</span></span>

* <span data-ttu-id="5096e-166">шифрование и расшифровка значений конфигурации приложений;</span><span class="sxs-lookup"><span data-stu-id="5096e-166">Encryption and decryption of application configuration values.</span></span>
* <span data-ttu-id="5096e-167">шифрование данных между узлами во время репликации.</span><span class="sxs-lookup"><span data-stu-id="5096e-167">Encryption of data across nodes during replication.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="5096e-168">форматирование сертификатов для использования поставщиком ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="5096e-168">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="5096e-169">Файлы закрытых ключей (PFX) можно добавить и использовать непосредственно в своем хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="5096e-169">You can add and use private key files (.pfx) directly through your key vault.</span></span> <span data-ttu-id="5096e-170">Однако поставщик ресурсов hello вычислений Azure требует toobe ключи, хранящиеся в специальном формате JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="5096e-170">However, hello Azure compute resource provider requires keys toobe stored in a special JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="5096e-171">Формат Hello включает hello PFX-файл как базовый строка в кодировке Base64 и hello пароль закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="5096e-171">hello format includes hello .pfx file as a base 64-encoded string and hello private key password.</span></span> <span data-ttu-id="5096e-172">tooaccommodate эти требования hello ключей необходимо поместить в строку JSON и затем сохраняются в виде «секреты» hello ключа хранилища.</span><span class="sxs-lookup"><span data-stu-id="5096e-172">tooaccommodate these requirements, hello keys must be placed in a JSON string and then stored as "secrets" in hello key vault.</span></span>

<span data-ttu-id="5096e-173">Эта процедура, toomake [модуль PowerShell можно найти в GitHub][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="5096e-173">toomake this process easier, a [PowerShell module is available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="5096e-174">модуль toouse hello, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="5096e-174">toouse hello module, do hello following:</span></span>

1. <span data-ttu-id="5096e-175">Загрузите все содержимое репозитория hello hello в локальный каталог.</span><span class="sxs-lookup"><span data-stu-id="5096e-175">Download hello entire contents of hello repo into a local directory.</span></span>
2. <span data-ttu-id="5096e-176">Последовательно выберите toohello локальный каталог.</span><span class="sxs-lookup"><span data-stu-id="5096e-176">Go toohello local directory.</span></span>
2. <span data-ttu-id="5096e-177">Импорт модуля ServiceFabricRPHelpers hello в окне PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5096e-177">Import hello ServiceFabricRPHelpers module in your PowerShell window:</span></span>

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

<span data-ttu-id="5096e-178">Hello `Invoke-AddCertToKeyVault` команды в этом модуле PowerShell автоматически форматирует закрытый ключ сертификата в строке JSON и отправляет его toohello хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="5096e-178">hello `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it toohello key vault.</span></span> <span data-ttu-id="5096e-179">Используйте hello команда tooadd hello кластера сертификат и все сертификаты дополнительное приложение toohello ключа хранилища.</span><span class="sxs-lookup"><span data-stu-id="5096e-179">Use hello command tooadd hello cluster certificate and any additional application certificates toohello key vault.</span></span> <span data-ttu-id="5096e-180">Повторите это действие другие сертификаты, требуется tooinstall в кластере.</span><span class="sxs-lookup"><span data-stu-id="5096e-180">Repeat this step for any additional certificates you want tooinstall in your cluster.</span></span>

#### <a name="uploading-an-existing-certificate"></a><span data-ttu-id="5096e-181">Загрузка существующего сертификата</span><span class="sxs-lookup"><span data-stu-id="5096e-181">Uploading an existing certificate</span></span>

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

<span data-ttu-id="5096e-182">Если возникает ошибка, например hello показанной здесь, это обычно означает, что имеется конфликт ресурсов URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="5096e-182">If you get an error, such as hello one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="5096e-183">конфликт tooresolve hello, изменить имя хранилища ключей hello.</span><span class="sxs-lookup"><span data-stu-id="5096e-183">tooresolve hello conflict, change hello key vault name.</span></span>

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="5096e-184">После устранения конфликта hello hello вывод должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5096e-184">After hello conflict is resolved, hello output should look like this:</span></span>

```

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: hello output object type of this cmdlet is going toobe modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
><span data-ttu-id="5096e-185">Необходимо hello три предыдущей строки, CertificateThumbprint, SourceVault и CertificateURL tooset безопасности кластера Service Fabric и tooobtain все сертификаты приложения, которые можно использовать для обеспечения безопасности приложения.</span><span class="sxs-lookup"><span data-stu-id="5096e-185">You need hello three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, tooset up a secure Service Fabric cluster and tooobtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="5096e-186">Если не сохранить строки hello, может быть трудно tooretrieve их с помощью запроса hello ключ в хранилище позже.</span><span class="sxs-lookup"><span data-stu-id="5096e-186">If you do not save hello strings, it can be difficult tooretrieve them by querying hello key vault later.</span></span>

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-toohello-key-vault"></a><span data-ttu-id="5096e-187">Создание самозаверяющего сертификата и передачи их в хранилище ключей toohello</span><span class="sxs-lookup"><span data-stu-id="5096e-187">Creating a self-signed certificate and uploading it toohello key vault</span></span>

<span data-ttu-id="5096e-188">Если вы уже отправили хранилища ключей toohello сертификаты, пропустите этот шаг.</span><span class="sxs-lookup"><span data-stu-id="5096e-188">If you have already uploaded your certificates toohello key vault, skip this step.</span></span> <span data-ttu-id="5096e-189">Этот шаг является создание нового самозаверяющего сертификата, и передачи их в хранилище ключей tooyour.</span><span class="sxs-lookup"><span data-stu-id="5096e-189">This step is for generating a new self-signed certificate and uploading it tooyour key vault.</span></span> <span data-ttu-id="5096e-190">После изменения параметров hello в hello, выполнив сценарий и запустите его, должен быть запрос пароль сертификата.</span><span class="sxs-lookup"><span data-stu-id="5096e-190">After you change hello parameters in hello following script and then run it, you should be prompted for a certificate password.</span></span>  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #hello certificate's subject name must match hello domain used tooaccess hello Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want hello .PFX toobe stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

<span data-ttu-id="5096e-191">Если возникает ошибка, например hello показанной здесь, это обычно означает, что имеется конфликт ресурсов URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="5096e-191">If you get an error, such as hello one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="5096e-192">конфликт tooresolve hello, изменить имя хранилища ключей hello, RG имя и т. д.</span><span class="sxs-lookup"><span data-stu-id="5096e-192">tooresolve hello conflict, change hello key vault name, RG name, and so forth.</span></span>

```
Set-AzureKeyVaultSecret : hello remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="5096e-193">После устранения конфликта hello hello вывод должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5096e-193">After hello conflict is resolved, hello output should look like this:</span></span>

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context tooSubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: hello output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret toochackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
><span data-ttu-id="5096e-194">Необходимо hello три предыдущей строки, CertificateThumbprint, SourceVault и CertificateURL tooset безопасности кластера Service Fabric и tooobtain все сертификаты приложения, которые можно использовать для обеспечения безопасности приложения.</span><span class="sxs-lookup"><span data-stu-id="5096e-194">You need hello three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, tooset up a secure Service Fabric cluster and tooobtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="5096e-195">Если не сохранить строки hello, может быть трудно tooretrieve их с помощью запроса hello ключ в хранилище позже.</span><span class="sxs-lookup"><span data-stu-id="5096e-195">If you do not save hello strings, it can be difficult tooretrieve them by querying hello key vault later.</span></span>

 <span data-ttu-id="5096e-196">На этом этапе должно быть hello следующие элементы на месте:</span><span class="sxs-lookup"><span data-stu-id="5096e-196">At this point, you should have hello following elements in place:</span></span>

* <span data-ttu-id="5096e-197">Группа ресурсов хранилища ключей Hello.</span><span class="sxs-lookup"><span data-stu-id="5096e-197">hello key vault resource group.</span></span>
* <span data-ttu-id="5096e-198">Здравствуйте, хранилище ключей и его URL-адреса (называемая SourceVault в hello, предшествующие выходные данные PowerShell).</span><span class="sxs-lookup"><span data-stu-id="5096e-198">hello key vault and its URL (called SourceVault in hello preceding PowerShell output).</span></span>
* <span data-ttu-id="5096e-199">сертификат проверки подлинности сервера Hello кластера и его URL-адреса в хранилище ключей hello.</span><span class="sxs-lookup"><span data-stu-id="5096e-199">hello cluster server authentication certificate and its URL in hello key vault.</span></span>
* <span data-ttu-id="5096e-200">Hello приложения сертификаты и их URL-адреса в хранилище ключей hello.</span><span class="sxs-lookup"><span data-stu-id="5096e-200">hello application certificates and their URLs in hello key vault.</span></span>


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="5096e-201">Настройка Azure Active Directory для проверки подлинности клиента</span><span class="sxs-lookup"><span data-stu-id="5096e-201">Set up Azure Active Directory for client authentication</span></span>

<span data-ttu-id="5096e-202">Azure AD обеспечивает tooapplications доступ пользователя toomanage организаций (это называется клиентов).</span><span class="sxs-lookup"><span data-stu-id="5096e-202">Azure AD enables organizations (known as tenants) toomanage user access tooapplications.</span></span> <span data-ttu-id="5096e-203">Приложения можно разделить на две группы: те, в которых есть пользовательский веб-интерфейс входа в систему, и те, в которых вход выполняется с помощью собственного клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="5096e-203">Applications are divided into those with a web-based sign-in UI and those with a native client experience.</span></span> <span data-ttu-id="5096e-204">В этой статье предполагается, что клиент уже создан.</span><span class="sxs-lookup"><span data-stu-id="5096e-204">In this article, we assume that you have already created a tenant.</span></span> <span data-ttu-id="5096e-205">Если нет, начните с просмотра [как для клиента Azure Active Directory tooget][active-directory-howto-tenant].</span><span class="sxs-lookup"><span data-stu-id="5096e-205">If you have not, start by reading [How tooget an Azure Active Directory tenant][active-directory-howto-tenant].</span></span>

<span data-ttu-id="5096e-206">Кластер Service Fabric предлагает несколько tooits точки входа функции управления, включая hello веб- [Service Fabric Explorer] [ service-fabric-visualizing-your-cluster] и [Visual Studio] [service-fabric-manage-application-in-visual-studio].</span><span class="sxs-lookup"><span data-stu-id="5096e-206">A Service Fabric cluster offers several entry points tooits management functionality, including hello web-based [Service Fabric Explorer][service-fabric-visualizing-your-cluster] and [Visual Studio][service-fabric-manage-application-in-visual-studio].</span></span> <span data-ttu-id="5096e-207">В результате создания кластера toohello два Azure AD приложений toocontrol доступа, одно веб-приложение и один собственное приложение.</span><span class="sxs-lookup"><span data-stu-id="5096e-207">As a result, you create two Azure AD applications toocontrol access toohello cluster, one web application and one native application.</span></span>

<span data-ttu-id="5096e-208">Некоторые шаги hello участвующих в настройке Azure AD с кластера Service Fabric toosimplify, мы создали набор сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5096e-208">toosimplify some of hello steps involved in configuring Azure AD with a Service Fabric cluster, we have created a set of Windows PowerShell scripts.</span></span>

> [!NOTE]
> <span data-ttu-id="5096e-209">Необходимо выполнить следующие действия перед созданием кластера hello hello.</span><span class="sxs-lookup"><span data-stu-id="5096e-209">You must complete hello following steps before you create hello cluster.</span></span> <span data-ttu-id="5096e-210">Поскольку hello сценарии ожидается, что имена кластеров и конечные точки, значения hello следует планировать и не значения, что вы уже создали.</span><span class="sxs-lookup"><span data-stu-id="5096e-210">Because hello scripts expect cluster names and endpoints, hello values should be planned and not values that you have already created.</span></span>

1. <span data-ttu-id="5096e-211">[Загрузите скрипты hello] [ sf-aad-ps-script-download] tooyour компьютера.</span><span class="sxs-lookup"><span data-stu-id="5096e-211">[Download hello scripts][sf-aad-ps-script-download] tooyour computer.</span></span>
2. <span data-ttu-id="5096e-212">Щелкните правой кнопкой мыши hello ZIP-файл, выберите **свойства**выберите hello **Unblock** флажок и нажмите кнопку **применить**.</span><span class="sxs-lookup"><span data-stu-id="5096e-212">Right-click hello zip file, select **Properties**, select hello **Unblock** check box, and then click **Apply**.</span></span>
3. <span data-ttu-id="5096e-213">Извлеките ZIP-файл hello.</span><span class="sxs-lookup"><span data-stu-id="5096e-213">Extract hello zip file.</span></span>
4. <span data-ttu-id="5096e-214">Запустите `SetupApplications.ps1`и укажите hello идентификатора клиента, Имя_кластера и WebApplicationReplyUrl в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="5096e-214">Run `SetupApplications.ps1`, and provide hello TenantId, ClusterName, and WebApplicationReplyUrl as parameters.</span></span> <span data-ttu-id="5096e-215">Например:</span><span class="sxs-lookup"><span data-stu-id="5096e-215">For example:</span></span>

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    <span data-ttu-id="5096e-216">Вашего идентификатора клиента можно найти, выполнив команду PowerShell hello `Get-AzureSubscription`.</span><span class="sxs-lookup"><span data-stu-id="5096e-216">You can find your TenantId by executing hello PowerShell command `Get-AzureSubscription`.</span></span> <span data-ttu-id="5096e-217">При выполнении данной команды отображение hello идентификатора клиента для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="5096e-217">Executing this command displays hello TenantId for every subscription.</span></span>

    <span data-ttu-id="5096e-218">Имя_кластера — приложения hello Azure AD используется tooprefix, созданные скриптом hello.</span><span class="sxs-lookup"><span data-stu-id="5096e-218">ClusterName is used tooprefix hello Azure AD applications that are created by hello script.</span></span> <span data-ttu-id="5096e-219">Имя фактического кластера toomatch hello не обязательно точно.</span><span class="sxs-lookup"><span data-stu-id="5096e-219">It does not need toomatch hello actual cluster name exactly.</span></span> <span data-ttu-id="5096e-220">Это предполагаемое только toomake его проще toomap Azure AD артефакты toohello кластера Service Fabric, они привыкли с.</span><span class="sxs-lookup"><span data-stu-id="5096e-220">It is intended only toomake it easier toomap Azure AD artifacts toohello Service Fabric cluster that they're being used with.</span></span>

    <span data-ttu-id="5096e-221">WebApplicationReplyUrl — конечную точку по умолчанию hello, Azure AD возвращает tooyour пользователей после их завершения вход.</span><span class="sxs-lookup"><span data-stu-id="5096e-221">WebApplicationReplyUrl is hello default endpoint that Azure AD returns tooyour users after they finish signing in.</span></span> <span data-ttu-id="5096e-222">Установите эту конечную точку в качестве конечной точки Service Fabric Explorer hello для кластера, который по умолчанию является:</span><span class="sxs-lookup"><span data-stu-id="5096e-222">Set this endpoint as hello Service Fabric Explorer endpoint for your cluster, which by default is:</span></span>

    <span data-ttu-id="5096e-223">https://&lt;cluster_domain&gt;:19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="5096e-223">https://&lt;cluster_domain&gt;:19080/Explorer</span></span>

    <span data-ttu-id="5096e-224">Все запрашиваемые toosign tooan учетной записью, имеющей права администратора для клиента hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5096e-224">You are prompted toosign in tooan account that has administrative privileges for hello Azure AD tenant.</span></span> <span data-ttu-id="5096e-225">После входа в скрипт hello создает веб-hello и собственных приложений toorepresent кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5096e-225">After you sign in, hello script creates hello web and native applications toorepresent your Service Fabric cluster.</span></span> <span data-ttu-id="5096e-226">Если взглянуть на приветствия клиента приложения в hello [классический портал Azure][azure-classic-portal], вы увидите два новых элемента:</span><span class="sxs-lookup"><span data-stu-id="5096e-226">If you look at hello tenant's applications in hello [Azure classic portal][azure-classic-portal], you should see two new entries:</span></span>

   * <span data-ttu-id="5096e-227">*имя_кластера*\_Кластер</span><span class="sxs-lookup"><span data-stu-id="5096e-227">*ClusterName*\_Cluster</span></span>
   * <span data-ttu-id="5096e-228">*имя_кластера*\_Клиент</span><span class="sxs-lookup"><span data-stu-id="5096e-228">*ClusterName*\_Client</span></span>

   <span data-ttu-id="5096e-229">сценарий Hello печатает Привет открыть JSON, необходимых для шаблона Azure Resource Manager hello, при создании кластера hello в следующем разделе hello, это окно PowerShell рекомендуется tookeep hello.</span><span class="sxs-lookup"><span data-stu-id="5096e-229">hello script prints hello JSON required by hello Azure Resource Manager template when you create hello cluster in hello next section, so it's a good idea tookeep hello PowerShell window open.</span></span>

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a><span data-ttu-id="5096e-230">Создание шаблона Resource Manager для кластера Service Fabric</span><span class="sxs-lookup"><span data-stu-id="5096e-230">Create a Service Fabric cluster Resource Manager template</span></span>
<span data-ttu-id="5096e-231">В этом разделе hello выходных данных из предыдущей hello можно использовать команды PowerShell в шаблоне диспетчер ресурсов кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5096e-231">In this section, hello outputs of hello preceding PowerShell commands are used in a Service Fabric cluster Resource Manager template.</span></span>

<span data-ttu-id="5096e-232">Пример диспетчера ресурсов шаблоны доступны в hello [коллекции Azure краткое шаблонов на GitHub][azure-quickstart-templates].</span><span class="sxs-lookup"><span data-stu-id="5096e-232">Sample Resource Manager templates are available in hello [Azure quick-start template gallery on GitHub][azure-quickstart-templates].</span></span> <span data-ttu-id="5096e-233">Их можно использовать в качестве отправной точки для создания шаблона кластера.</span><span class="sxs-lookup"><span data-stu-id="5096e-233">These templates can be used as a starting point for your cluster template.</span></span>

### <a name="create-hello-resource-manager-template"></a><span data-ttu-id="5096e-234">Создание шаблона диспетчера ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="5096e-234">Create hello Resource Manager template</span></span>
<span data-ttu-id="5096e-235">В этом руководстве используется hello [безопасного кластер 5] [ service-fabric-secure-cluster-5-node-1-nodetype] пример шаблона и параметров шаблона.</span><span class="sxs-lookup"><span data-stu-id="5096e-235">This guide uses hello [5-node secure cluster][service-fabric-secure-cluster-5-node-1-nodetype] example template and template parameters.</span></span> <span data-ttu-id="5096e-236">Загрузить `azuredeploy.json` и `azuredeploy.parameters.json` tooyour компьютер и открыть оба файла в другом текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="5096e-236">Download `azuredeploy.json` and `azuredeploy.parameters.json` tooyour computer and open both files in your favorite text editor.</span></span>

### <a name="add-certificates"></a><span data-ttu-id="5096e-237">Добавление сертификатов</span><span class="sxs-lookup"><span data-stu-id="5096e-237">Add certificates</span></span>
<span data-ttu-id="5096e-238">Добавление шаблона диспетчера ресурсов кластера tooa сертификаты, ссылаясь на хранилище ключей hello, содержащий ключи сертификатов hello.</span><span class="sxs-lookup"><span data-stu-id="5096e-238">You add certificates tooa cluster Resource Manager template by referencing hello key vault that contains hello certificate keys.</span></span> <span data-ttu-id="5096e-239">Рекомендуется размещать значения hello хранилище ключей в файле параметров шаблона диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5096e-239">We recommend that you place hello key-vault values in a Resource Manager template parameters file.</span></span> <span data-ttu-id="5096e-240">Таким образом отслеживает hello диспетчера ресурсов файл шаблона для повторного использования и не развертывания tooa конкретного значения.</span><span class="sxs-lookup"><span data-stu-id="5096e-240">Doing so keeps hello Resource Manager template file reusable and free of values specific tooa deployment.</span></span>

#### <a name="add-all-certificates-toohello-virtual-machine-scale-set-osprofile"></a><span data-ttu-id="5096e-241">Добавление набора масштабирования виртуальных машин toohello все сертификаты в osProfile</span><span class="sxs-lookup"><span data-stu-id="5096e-241">Add all certificates toohello virtual machine scale set osProfile</span></span>
<span data-ttu-id="5096e-242">Каждый сертификат, устанавливаемый в кластере hello должен быть настроен в разделе osProfile hello hello шкалы набор ресурсов (Microsoft.Compute/virtualMachineScaleSets).</span><span class="sxs-lookup"><span data-stu-id="5096e-242">Every certificate that's installed in hello cluster must be configured in hello osProfile section of hello scale set resource (Microsoft.Compute/virtualMachineScaleSets).</span></span> <span data-ttu-id="5096e-243">Это действие указывает, что сертификат hello tooinstall поставщика ресурсов hello на hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5096e-243">This action instructs hello resource provider tooinstall hello certificate on hello VMs.</span></span> <span data-ttu-id="5096e-244">Эта установка включает hello кластера сертификатов и сертификаты безопасности приложения, планирование toouse приложений:</span><span class="sxs-lookup"><span data-stu-id="5096e-244">This installation includes both hello cluster certificate and any application security certificates that you plan toouse for your applications:</span></span>

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "osProfile": {
      ...
      "secrets": [
        {
          "sourceVault": {
            "id": "[parameters('sourceVaultValue')]"
          },
          "vaultCertificates": [
            {
              "certificateStore": "[parameters('clusterCertificateStorevalue')]",
              "certificateUrl": "[parameters('clusterCertificateUrlValue')]"
            },
            {
              "certificateStore": "[parameters('applicationCertificateStorevalue')",
              "certificateUrl": "[parameters('applicationCertificateUrlValue')]"
            },
            ...
          ]
        }
      ]
    }
  }
}
```

#### <a name="configure-hello-service-fabric-cluster-certificate"></a><span data-ttu-id="5096e-245">Настройка сертификата кластера Service Fabric hello</span><span class="sxs-lookup"><span data-stu-id="5096e-245">Configure hello Service Fabric cluster certificate</span></span>
<span data-ttu-id="5096e-246">сертификат проверки подлинности Hello кластера должен быть настроен в обеих ресурса кластера Service Fabric hello (Microsoft.ServiceFabric/clusters), и задает hello расширения Service Fabric для масштабирования виртуальных машин в ресурс набор масштабирования виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="5096e-246">hello cluster authentication certificate must be configured in both hello Service Fabric cluster resource (Microsoft.ServiceFabric/clusters) and hello Service Fabric extension for virtual machine scale sets in hello virtual machine scale set resource.</span></span> <span data-ttu-id="5096e-247">Такой подход позволяет tooconfigure поставщика ресурсов Service Fabric hello его использовать для проверки подлинности для кластера и сервера для конечных точек управления.</span><span class="sxs-lookup"><span data-stu-id="5096e-247">This arrangement allows hello Service Fabric resource provider tooconfigure it for use for cluster authentication and server authentication for management endpoints.</span></span>

##### <a name="virtual-machine-scale-set-resource"></a><span data-ttu-id="5096e-248">Ресурс масштабируемого набора виртуальных машин:</span><span class="sxs-lookup"><span data-stu-id="5096e-248">Virtual machine scale set resource:</span></span>
```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  ...
  "properties": {
    ...
    "virtualMachineProfile": {
      "extensionProfile": {
        "extensions": [
          {
            "name": "[concat('ServiceFabricNodeVmExt','_vmNodeType0Name')]",
            "properties": {
              ...
              "settings": {
                ...
                "certificate": {
                  "thumbprint": "[parameters('clusterCertificateThumbprint')]",
                  "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
                },
                ...
              }
            }
          }
        ]
      }
    }
  }
}
```

##### <a name="service-fabric-resource"></a><span data-ttu-id="5096e-249">Ресурс Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5096e-249">Service Fabric resource:</span></span>
```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  "location": "[parameters('clusterLocation')]",
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('supportLogStorageAccountName'))]"
  ],
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStoreValue')]"
    },
    ...
  }
}
```

### <a name="insert-azure-ad-configuration"></a><span data-ttu-id="5096e-250">Получение конфигурации Azure AD</span><span class="sxs-lookup"><span data-stu-id="5096e-250">Insert Azure AD configuration</span></span>
<span data-ttu-id="5096e-251">Конфигурация Hello Azure AD, созданный ранее могут быть вставлены непосредственно в шаблон диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5096e-251">hello Azure AD configuration that you created earlier can be inserted directly into your Resource Manager template.</span></span> <span data-ttu-id="5096e-252">Тем не менее рекомендуется сначала извлечь значения hello в повторно используемый hello диспетчера ресурсов шаблона параметров файла tookeep и освободить развертывания tooa конкретного значения.</span><span class="sxs-lookup"><span data-stu-id="5096e-252">However, we recommended that you first extract hello values into a parameters file tookeep hello Resource Manager template reusable and free of values specific tooa deployment.</span></span>

```json
{
  "apiVersion": "2016-03-01",
  "type": "Microsoft.ServiceFabric/clusters",
  "name": "[parameters('clusterName')]",
  ...
  "properties": {
    "certificate": {
      "thumbprint": "[parameters('clusterCertificateThumbprint')]",
      "x509StoreName": "[parameters('clusterCertificateStorevalue')]"
    },
    ...
    "azureActiveDirectory": {
      "tenantId": "[parameters('aadTenantId')]",
      "clusterApplication": "[parameters('aadClusterApplicationId')]",
      "clientApplication": "[parameters('aadClientApplicationId')]"
    },
    ...
  }
}
```

### <span data-ttu-id="5096e-253"><a "configure-arm" ></a>Настройка параметров шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5096e-253"><a "configure-arm" ></a>Configure Resource Manager template parameters</span></span>
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since hello link seems not toobe redirecting correctly --->
<span data-ttu-id="5096e-254">И наконец используйте hello выходные значения из хранилища ключей hello и файле параметров hello toopopulate команды Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5096e-254">Finally, use hello output values from hello key vault and Azure AD PowerShell commands toopopulate hello parameters file:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        ...
        "clusterCertificateStoreValue": {
            "value": "My"
        },
        "clusterCertificateThumbprint": {
            "value": "<thumbprint>"
        },
        "clusterCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myclustercert/4d087088df974e869f1c0978cb100e47"
        },
        "applicationCertificateStorevalue": {
            "value": "My"
        },
        "applicationCertificateUrlValue": {
            "value": "https://myvault.vault.azure.net:443/secrets/myapplicationcert/2e035058ae274f869c4d0348ca100f08"
        },
        "sourceVaultvalue": {
            "value": "/subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault"
        },
        "aadTenantId": {
            "value": "<guid>"
        },
        "aadClusterApplicationId": {
            "value": "<guid>"
        },
        "aadClientApplicationId": {
            "value": "<guid>"
        },
        ...
    }
}
```
<span data-ttu-id="5096e-255">На этом этапе должно быть hello следующие элементы на месте:</span><span class="sxs-lookup"><span data-stu-id="5096e-255">At this point, you should have hello following elements in place:</span></span>

* <span data-ttu-id="5096e-256">группа ресурсов хранилища ключей;</span><span class="sxs-lookup"><span data-stu-id="5096e-256">Key vault resource group</span></span>
  * <span data-ttu-id="5096e-257">Хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="5096e-257">Key vault</span></span>
  * <span data-ttu-id="5096e-258">сертификат проверки подлинности сервера кластера;</span><span class="sxs-lookup"><span data-stu-id="5096e-258">Cluster server authentication certificate</span></span>
  * <span data-ttu-id="5096e-259">сертификат шифрования данных;</span><span class="sxs-lookup"><span data-stu-id="5096e-259">Data encipherment certificate</span></span>
* <span data-ttu-id="5096e-260">клиент Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="5096e-260">Azure Active Directory tenant</span></span>
  * <span data-ttu-id="5096e-261">приложение Azure AD для управления через Интернет и Service Fabric Explorer;</span><span class="sxs-lookup"><span data-stu-id="5096e-261">Azure AD application for web-based management and Service Fabric Explorer</span></span>
  * <span data-ttu-id="5096e-262">приложение Azure AD для управления собственными клиентами.</span><span class="sxs-lookup"><span data-stu-id="5096e-262">Azure AD application for native client management</span></span>
  * <span data-ttu-id="5096e-263">Пользователи и назначенные им роли</span><span class="sxs-lookup"><span data-stu-id="5096e-263">Users and their assigned roles</span></span>
* <span data-ttu-id="5096e-264">шаблон Resource Manager для кластера Service Fabric;</span><span class="sxs-lookup"><span data-stu-id="5096e-264">Service Fabric cluster Resource Manager template</span></span>
  * <span data-ttu-id="5096e-265">Сертификаты, настроенные с помощью хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="5096e-265">Certificates configured through key vault</span></span>
  * <span data-ttu-id="5096e-266">настроенная среда Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5096e-266">Azure Active Directory configured</span></span>

<span data-ttu-id="5096e-267">Привет, следующая схема иллюстрирует где хранилище ключей и конфигурации Azure AD, помещаются в шаблон диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5096e-267">hello following diagram illustrates where your key vault and Azure AD configuration fit into your Resource Manager template.</span></span>

![Сопоставление зависимостей Resource Manager][cluster-security-arm-dependency-map]

## <a name="create-hello-cluster"></a><span data-ttu-id="5096e-269">Создание кластера hello</span><span class="sxs-lookup"><span data-stu-id="5096e-269">Create hello cluster</span></span>
<span data-ttu-id="5096e-270">Теперь вы находитесь готов toocreate hello кластера с помощью [развертывания шаблона ресурсов Azure][resource-group-template-deploy].</span><span class="sxs-lookup"><span data-stu-id="5096e-270">You are now ready toocreate hello cluster by using [Azure resource template deployment][resource-group-template-deploy].</span></span>

#### <a name="test-it"></a><span data-ttu-id="5096e-271">Тестирование</span><span class="sxs-lookup"><span data-stu-id="5096e-271">Test it</span></span>
<span data-ttu-id="5096e-272">С помощью файла параметров с помощью этого шаблона диспетчера ресурсов hello, следуя tootest команды PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5096e-272">Use hello following PowerShell command tootest your Resource Manager template with a parameters file:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a><span data-ttu-id="5096e-273">Развертывание</span><span class="sxs-lookup"><span data-stu-id="5096e-273">Deploy it</span></span>
<span data-ttu-id="5096e-274">Если hello диспетчера ресурсов шаблона тест был пройден, используйте hello, следующая команда toodeploy PowerShell шаблона диспетчера ресурсов с помощью файла параметров:</span><span class="sxs-lookup"><span data-stu-id="5096e-274">If hello Resource Manager template test passes, use hello following PowerShell command toodeploy your Resource Manager template with a parameters file:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-tooroles"></a><span data-ttu-id="5096e-275">Назначить пользователей tooroles</span><span class="sxs-lookup"><span data-stu-id="5096e-275">Assign users tooroles</span></span>
<span data-ttu-id="5096e-276">После создания toorepresent приложения hello кластера, ролям пользователей toohello поддерживаемые Service Fabric: только для чтения и администрирования. Hello роли можно назначить с помощью hello [классический портал Azure][azure-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="5096e-276">After you have created hello applications toorepresent your cluster, assign your users toohello roles supported by Service Fabric: read-only and admin. You can assign hello roles by using hello [Azure classic portal][azure-classic-portal].</span></span>

1. <span data-ttu-id="5096e-277">В hello портал Azure, перейдите tooyour клиента, а затем выберите **приложений**.</span><span class="sxs-lookup"><span data-stu-id="5096e-277">In hello Azure portal, go tooyour tenant, and then select **Applications**.</span></span>
2. <span data-ttu-id="5096e-278">Выберите веб-приложения hello, который имеет имя, например `myTestCluster_Cluster`.</span><span class="sxs-lookup"><span data-stu-id="5096e-278">Select hello web application, which has a name like `myTestCluster_Cluster`.</span></span>
3. <span data-ttu-id="5096e-279">Нажмите кнопку hello **пользователей** вкладки.</span><span class="sxs-lookup"><span data-stu-id="5096e-279">Click hello **Users** tab.</span></span>
4. <span data-ttu-id="5096e-280">Выберите tooassign пользователя и нажмите кнопку hello **назначить** кнопку hello нижней части экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="5096e-280">Select a user tooassign, and then click hello **Assign** button at hello bottom of hello screen.</span></span>

    ![Назначить пользователей tooroles кнопки][assign-users-to-roles-button]
5. <span data-ttu-id="5096e-282">Выберите tooassign toohello hello роли пользователя.</span><span class="sxs-lookup"><span data-stu-id="5096e-282">Select hello role tooassign toohello user.</span></span>

    ![Диалоговое окно "Назначить пользователей"][assign-users-to-roles-dialog]

> [!NOTE]
> <span data-ttu-id="5096e-284">Дополнительные сведения о ролях в Service Fabric см. в статье [Контроль доступа на основе ролей для клиентов Service Fabric](service-fabric-cluster-security-roles.md).</span><span class="sxs-lookup"><span data-stu-id="5096e-284">For more information about roles in Service Fabric, see [Role-based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused hello wrong redirection of hello link --->

## <a name="create-secure-clusters-on-linux"></a><span data-ttu-id="5096e-285">Создание безопасных кластеров в Linux</span><span class="sxs-lookup"><span data-stu-id="5096e-285">Create secure clusters on Linux</span></span>
<span data-ttu-id="5096e-286">упрощает процесс hello toomake, мы предоставили [вспомогательный сценарий](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span><span class="sxs-lookup"><span data-stu-id="5096e-286">toomake hello process easier, we have provided a [helper script](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span></span> <span data-ttu-id="5096e-287">Прежде чем использовать этот вспомогательный сценарий, убедитесь, что интерфейс командной строки Azure уже установлен и указан в пути.</span><span class="sxs-lookup"><span data-stu-id="5096e-287">Before you use this helper script, ensure that you already have Azure command-line interface (CLI) installed, and it is in your path.</span></span> <span data-ttu-id="5096e-288">Сценарий hello оставалось tooexecute разрешения, выполнив `chmod +x cert_helper.py` после его загрузки.</span><span class="sxs-lookup"><span data-stu-id="5096e-288">Make sure that hello script has permissions tooexecute by running `chmod +x cert_helper.py` after downloading it.</span></span> <span data-ttu-id="5096e-289">Hello первым шагом является toosign в tooyour учетная запись Azure с помощью CLI с hello `azure login` команды.</span><span class="sxs-lookup"><span data-stu-id="5096e-289">hello first step is toosign in tooyour Azure account by using CLI with hello `azure login` command.</span></span> <span data-ttu-id="5096e-290">После входа в учетную запись Azure tooyour использовать hello вспомогательный сценарий с помощью центра сертификации подписанного сертификата, как hello, следующая команда показывает:</span><span class="sxs-lookup"><span data-stu-id="5096e-290">After signing in tooyour Azure account, use hello helper script with your CA signed certificate, as hello following command shows:</span></span>

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

<span data-ttu-id="5096e-291">параметр - ifile Hello может принимать в PFX-файл или PEM-файл в качестве выходных данных и hello тип сертификата (PFX-файла или pem или ss, если это самозаверяющий сертификат).</span><span class="sxs-lookup"><span data-stu-id="5096e-291">hello -ifile parameter can take a .pfx file or a .pem file as input, with hello certificate type (pfx or pem, or ss if it is a self-signed certificate).</span></span>
<span data-ttu-id="5096e-292">Hello параметр -h выводит текст справки hello.</span><span class="sxs-lookup"><span data-stu-id="5096e-292">hello parameter -h prints out hello help text.</span></span>


<span data-ttu-id="5096e-293">Эта команда возвращает следующие три строки в качестве выходных данных hello hello:</span><span class="sxs-lookup"><span data-stu-id="5096e-293">This command returns hello following three strings as hello output:</span></span>

* <span data-ttu-id="5096e-294">SourceVaultID, который является Идентификатором hello для hello новой группе ресурсов KeyVault, она создана для вас</span><span class="sxs-lookup"><span data-stu-id="5096e-294">SourceVaultID, which is hello ID for hello new KeyVault ResourceGroup it created for you</span></span>
* <span data-ttu-id="5096e-295">CertificateUrl для доступ к сертификату hello</span><span class="sxs-lookup"><span data-stu-id="5096e-295">CertificateUrl for accessing hello certificate</span></span>
* <span data-ttu-id="5096e-296">CertificateThumbprint — используется для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="5096e-296">CertificateThumbprint, which is used for authentication</span></span>

<span data-ttu-id="5096e-297">Hello в следующем примере показано, как toouse hello команды:</span><span class="sxs-lookup"><span data-stu-id="5096e-297">hello following example shows how toouse hello command:</span></span>

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
<span data-ttu-id="5096e-298">Выполнение hello предшествующий дает команду hello три строки, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="5096e-298">Executing hello preceding command gives you hello three strings as follows:</span></span>

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

<span data-ttu-id="5096e-299">Имя субъекта сертификата Hello должен соответствовать домену hello, использовать кластер Service Fabric tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="5096e-299">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="5096e-300">Это совпадение является обязательным tooprovide SSL для конечных точек управления HTTPS hello кластера и обозреватель Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5096e-300">This match is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="5096e-301">Не удается получить SSL-сертификат из ЦС для hello `.cloudapp.azure.com` домена.</span><span class="sxs-lookup"><span data-stu-id="5096e-301">You cannot obtain an SSL certificate from a CA for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="5096e-302">Необходимо получить имя личного домена для кластера.</span><span class="sxs-lookup"><span data-stu-id="5096e-302">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="5096e-303">При запросить сертификат от центра сертификации, hello имя субъекта сертификата должно соответствовать hello собственное доменное имя для вашего кластера.</span><span class="sxs-lookup"><span data-stu-id="5096e-303">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="5096e-304">Эти имена субъектов, hello записей необходимо toocreate безопасности кластера Service Fabric (без Azure AD), как описано в разделе [параметров шаблона настройки диспетчера ресурсов](#configure-arm).</span><span class="sxs-lookup"><span data-stu-id="5096e-304">These subject names are hello entries you need toocreate a secure Service Fabric cluster (without Azure AD), as described at [Configure Resource Manager template parameters](#configure-arm).</span></span> <span data-ttu-id="5096e-305">Подключении toohello безопасного кластера в соответствии с инструкциями hello для [проверки подлинности клиента доступа tooa кластера](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="5096e-305">You can connect toohello secure cluster by following hello instructions for [authenticating client access tooa cluster](service-fabric-connect-to-secure-cluster.md).</span></span> <span data-ttu-id="5096e-306">Кластеры Linux предварительной версии не поддерживают аутентификацию Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5096e-306">Linux preview clusters do not support Azure AD authentication.</span></span> <span data-ttu-id="5096e-307">Вы можете назначить роли администратора и клиента, как описано в hello [назначение ролей toousers](#assign-roles) раздела.</span><span class="sxs-lookup"><span data-stu-id="5096e-307">You can assign admin and client roles as described in hello [Assign roles toousers](#assign-roles) section.</span></span> <span data-ttu-id="5096e-308">При указании роли администратора и клиента для Linux предварительного просмотра кластера, у вас есть tooprovide отпечатки сертификатов для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="5096e-308">When you specify admin and client roles for a Linux preview cluster, you have tooprovide certificate thumbprints for authentication.</span></span> <span data-ttu-id="5096e-309">(Отсутствует имя субъекта hello, так как в этом предварительном выпуске выполняется без проверки цепочки или отзыва.)</span><span class="sxs-lookup"><span data-stu-id="5096e-309">(You do not provide hello subject name, because no chain validation or revocation is being performed in this preview release.)</span></span>

<span data-ttu-id="5096e-310">Если требуется toouse самозаверяющего сертификата для тестирования, можно использовать hello же toogenerate сценарий один.</span><span class="sxs-lookup"><span data-stu-id="5096e-310">If you want toouse a self-signed certificate for testing, you can use hello same script toogenerate one.</span></span> <span data-ttu-id="5096e-311">Затем вы можете передать хранилища ключей tooyour сертификат hello, указав флаг hello `ss` вместо предоставления hello сертификат путь и имя сертификата.</span><span class="sxs-lookup"><span data-stu-id="5096e-311">You can then upload hello certificate tooyour key vault by providing hello flag `ss` instead of providing hello certificate path and certificate name.</span></span> <span data-ttu-id="5096e-312">Например см. следующую команду для создания и передачи самозаверяющий сертификат hello:</span><span class="sxs-lookup"><span data-stu-id="5096e-312">For example, see hello following command for creating and uploading a self-signed certificate:</span></span>

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
<span data-ttu-id="5096e-313">Эта команда возвращает hello одинаковые три строки: SourceVault, CertificateUrl и CertificateThumbprint.</span><span class="sxs-lookup"><span data-stu-id="5096e-313">This command returns hello same three strings: SourceVault, CertificateUrl, and CertificateThumbprint.</span></span> <span data-ttu-id="5096e-314">Затем можно использовать строки toocreate hello безопасного кластеров Linux и расположение, куда помещается hello самозаверяющий сертификат.</span><span class="sxs-lookup"><span data-stu-id="5096e-314">You can then use hello strings toocreate both a secure Linux cluster and a location where hello self-signed certificate is placed.</span></span> <span data-ttu-id="5096e-315">Вам потребуется hello самозаверяющий сертификат tooconnect toohello кластер.</span><span class="sxs-lookup"><span data-stu-id="5096e-315">You need hello self-signed certificate tooconnect toohello cluster.</span></span> <span data-ttu-id="5096e-316">Подключении toohello безопасного кластера в соответствии с инструкциями hello для [проверки подлинности клиента доступа tooa кластера](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="5096e-316">You can connect toohello secure cluster by following hello instructions for [authenticating client access tooa cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="5096e-317">Имя субъекта сертификата Hello должен соответствовать домену hello, использовать кластер Service Fabric tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="5096e-317">hello certificate's subject name must match hello domain that you use tooaccess hello Service Fabric cluster.</span></span> <span data-ttu-id="5096e-318">Это совпадение является обязательным tooprovide SSL для конечных точек управления HTTPS hello кластера и обозреватель Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5096e-318">This match is required tooprovide an SSL for hello cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="5096e-319">Не удается получить SSL-сертификат из ЦС для hello `.cloudapp.azure.com` домена.</span><span class="sxs-lookup"><span data-stu-id="5096e-319">You cannot obtain an SSL certificate from a CA for hello `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="5096e-320">Необходимо получить имя личного домена для кластера.</span><span class="sxs-lookup"><span data-stu-id="5096e-320">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="5096e-321">При запросить сертификат от центра сертификации, hello имя субъекта сертификата должно соответствовать hello собственное доменное имя для вашего кластера.</span><span class="sxs-lookup"><span data-stu-id="5096e-321">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="5096e-322">Можно заполнить hello параметры из сценария вспомогательный hello в hello портал Azure, как описано в hello [создания кластера в hello портал Azure](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) раздела.</span><span class="sxs-lookup"><span data-stu-id="5096e-322">You can fill hello parameters from hello helper script in hello Azure portal, as described in hello [Create a cluster in hello Azure portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5096e-323">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5096e-323">Next steps</span></span>
<span data-ttu-id="5096e-324">На этом этапе у вас имеется защищенный кластер с Azure Active Directory для аутентификации управления.</span><span class="sxs-lookup"><span data-stu-id="5096e-324">At this point, you have a secure cluster with Azure Active Directory providing management authentication.</span></span> <span data-ttu-id="5096e-325">Далее, [подключения кластера tooyour](service-fabric-connect-to-secure-cluster.md) и узнайте, каким образом слишком[управление секретами приложения](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="5096e-325">Next, [connect tooyour cluster](service-fabric-connect-to-secure-cluster.md) and learn how too[manage application secrets](service-fabric-application-secret-management.md).</span></span>

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="5096e-326">Устранение неполадок с настройкой Azure Active Directory для проверки подлинности клиента</span><span class="sxs-lookup"><span data-stu-id="5096e-326">Troubleshoot setting up Azure Active Directory for client authentication</span></span>
<span data-ttu-id="5096e-327">Если возникли проблемы при установке Azure AD для проверки подлинности клиента, просмотрите hello возможные решения в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="5096e-327">If you run into an issue while you're setting up Azure AD for client authentication, review hello potential solutions in this section.</span></span>

### <a name="service-fabric-explorer-prompts-you-tooselect-a-certificate"></a><span data-ttu-id="5096e-328">Обозреватель Service Fabric предлагает tooselect сертификата</span><span class="sxs-lookup"><span data-stu-id="5096e-328">Service Fabric Explorer prompts you tooselect a certificate</span></span>
#### <a name="problem"></a><span data-ttu-id="5096e-329">Проблема</span><span class="sxs-lookup"><span data-stu-id="5096e-329">Problem</span></span>
<span data-ttu-id="5096e-330">После входа в успешно tooAzure AD в обозреватель Service Fabric hello браузера возвращает toohello домашней страницы, но появится сообщение с запросом tooselect сертификат.</span><span class="sxs-lookup"><span data-stu-id="5096e-330">After you sign in successfully tooAzure AD in Service Fabric Explorer, hello browser returns toohello home page but a message prompts you tooselect a certificate.</span></span>

![Диалоговое окно выбора сертификата в Service Fabric Explorer][sfx-select-certificate-dialog]

#### <a name="reason"></a><span data-ttu-id="5096e-332">Причина</span><span class="sxs-lookup"><span data-stu-id="5096e-332">Reason</span></span>
<span data-ttu-id="5096e-333">Hello пользователю не назначен роли в hello кластерного приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5096e-333">hello user isn’t assigned a role in hello Azure AD cluster application.</span></span> <span data-ttu-id="5096e-334">Таким образом, аутентификация Azure AD в кластере Service Fabric завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="5096e-334">Thus, Azure AD authentication fails on Service Fabric cluster.</span></span> <span data-ttu-id="5096e-335">Обозреватель Service Fabric возвращается toocertificate проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="5096e-335">Service Fabric Explorer falls back toocertificate authentication.</span></span>

#### <a name="solution"></a><span data-ttu-id="5096e-336">Решение</span><span class="sxs-lookup"><span data-stu-id="5096e-336">Solution</span></span>
<span data-ttu-id="5096e-337">Выполните инструкции hello настройки Azure AD и назначить роли пользователя.</span><span class="sxs-lookup"><span data-stu-id="5096e-337">Follow hello instructions for setting up Azure AD, and assign user roles.</span></span> <span data-ttu-id="5096e-338">Кроме того, рекомендуется включить «Приложение требуется tooaccess назначение пользователя», как `SetupApplications.ps1` does.</span><span class="sxs-lookup"><span data-stu-id="5096e-338">Also, we recommend that you turn on “User assignment required tooaccess app,” as `SetupApplications.ps1` does.</span></span>

### <a name="connection-with-powershell-fails-with-an-error-hello-specified-credentials-are-invalid"></a><span data-ttu-id="5096e-339">Подключение с помощью PowerShell завершается с ошибкой: «hello указанные учетные данные недействительны»</span><span class="sxs-lookup"><span data-stu-id="5096e-339">Connection with PowerShell fails with an error: "hello specified credentials are invalid"</span></span>
#### <a name="problem"></a><span data-ttu-id="5096e-340">Проблема</span><span class="sxs-lookup"><span data-stu-id="5096e-340">Problem</span></span>
<span data-ttu-id="5096e-341">При использовании кластера toohello tooconnect PowerShell с помощью режима безопасности «Azureactivedirectory возникла ошибка», после входа в успешно tooAzure AD hello подключение завершается с ошибкой: «hello указано недопустимые учетные данные».</span><span class="sxs-lookup"><span data-stu-id="5096e-341">When you use PowerShell tooconnect toohello cluster by using “AzureActiveDirectory” security mode, after you sign in successfully tooAzure AD, hello connection fails with an error: "hello specified credentials are invalid."</span></span>

#### <a name="solution"></a><span data-ttu-id="5096e-342">Решение</span><span class="sxs-lookup"><span data-stu-id="5096e-342">Solution</span></span>
<span data-ttu-id="5096e-343">Это решение является таким же, как hello, предшествующие, приветствия.</span><span class="sxs-lookup"><span data-stu-id="5096e-343">This solution is hello same as hello preceding one.</span></span>

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a><span data-ttu-id="5096e-344">Service Fabric Explorer при входе возвращает ошибку "AADSTS50011"</span><span class="sxs-lookup"><span data-stu-id="5096e-344">Service Fabric Explorer returns a failure when you sign in: "AADSTS50011"</span></span>
#### <a name="problem"></a><span data-ttu-id="5096e-345">Проблема</span><span class="sxs-lookup"><span data-stu-id="5096e-345">Problem</span></span>
<span data-ttu-id="5096e-346">При попытке toosign в tooAzure AD в обозреватель Service Fabric, страница приветствия возвращает ошибку: «AADSTS50011: hello обратный адрес &lt;URL-адрес&gt; не соответствует hello адреса ответа, настроенного для приложения hello: &lt;guid&gt;."</span><span class="sxs-lookup"><span data-stu-id="5096e-346">When you try toosign in tooAzure AD in Service Fabric Explorer, hello page returns a failure: "AADSTS50011: hello reply address &lt;url&gt; does not match hello reply addresses configured for hello application: &lt;guid&gt;."</span></span>

![Несовпадение адреса ответа в Service Fabric Explorer][sfx-reply-address-not-match]

#### <a name="reason"></a><span data-ttu-id="5096e-348">Причина</span><span class="sxs-lookup"><span data-stu-id="5096e-348">Reason</span></span>
<span data-ttu-id="5096e-349">приложение Hello кластера (Интернет), представляющий Service Fabric Explorer пытается tooauthenticate от Azure AD, и как часть запроса hello предоставляет hello перенаправления URL-адреса возврата.</span><span class="sxs-lookup"><span data-stu-id="5096e-349">hello cluster (web) application that represents Service Fabric Explorer attempts tooauthenticate against Azure AD, and as part of hello request it provides hello redirect return URL.</span></span> <span data-ttu-id="5096e-350">Но hello URL-адрес не указан в приложение hello Azure AD **URL-адрес ОТВЕТА** списка.</span><span class="sxs-lookup"><span data-stu-id="5096e-350">But hello URL is not listed in hello Azure AD application **REPLY URL** list.</span></span>

#### <a name="solution"></a><span data-ttu-id="5096e-351">Решение</span><span class="sxs-lookup"><span data-stu-id="5096e-351">Solution</span></span>
<span data-ttu-id="5096e-352">На hello **Настройка** вкладка hello кластера (приложение), добавьте URL-адрес из Service Fabric Explorer toohello hello **URL-адрес ОТВЕТА** списка или заменить один из элементов hello в списке hello.</span><span class="sxs-lookup"><span data-stu-id="5096e-352">On hello **Configure** tab of hello cluster (web) application, add hello URL of Service Fabric Explorer toohello **REPLY URL** list or replace one of hello items in hello list.</span></span> <span data-ttu-id="5096e-353">После завершения сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="5096e-353">When you have finished, save your change.</span></span>

![URL-адрес ответа веб-приложения][web-application-reply-url]

### <a name="connect-hello-cluster-by-using-azure-ad-authentication-via-powershell"></a><span data-ttu-id="5096e-355">Подключите hello кластер с помощью проверки подлинности Azure AD с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="5096e-355">Connect hello cluster by using Azure AD authentication via PowerShell</span></span>
<span data-ttu-id="5096e-356">кластер Service Fabric hello tooconnect, hello используйте следующий пример команды PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5096e-356">tooconnect hello Service Fabric cluster, use hello following PowerShell command example:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

<span data-ttu-id="5096e-357">toolearn командлету Connect-ServiceFabricCluster hello. в разделе [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span><span class="sxs-lookup"><span data-stu-id="5096e-357">toolearn about hello Connect-ServiceFabricCluster cmdlet, see [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span></span>

### <a name="can-i-reuse-hello-same-azure-ad-tenant-in-multiple-clusters"></a><span data-ttu-id="5096e-358">Можно использовать клиент hello же Azure AD в несколько кластеров</span><span class="sxs-lookup"><span data-stu-id="5096e-358">Can I reuse hello same Azure AD tenant in multiple clusters?</span></span>
<span data-ttu-id="5096e-359">Да.</span><span class="sxs-lookup"><span data-stu-id="5096e-359">Yes.</span></span> <span data-ttu-id="5096e-360">Но следует помнить tooadd hello URL-адрес из Service Fabric Explorer tooyour кластера (Интернет) приложения.</span><span class="sxs-lookup"><span data-stu-id="5096e-360">But remember tooadd hello URL of Service Fabric Explorer tooyour cluster (web) application.</span></span> <span data-ttu-id="5096e-361">В противном случае — Service Fabric Explorer не работает.</span><span class="sxs-lookup"><span data-stu-id="5096e-361">Otherwise, Service Fabric Explorer doesn’t work.</span></span>

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a><span data-ttu-id="5096e-362">Почему мне все еще нужен сертификат сервера при включенном Azure AD?</span><span class="sxs-lookup"><span data-stu-id="5096e-362">Why do I still need a server certificate while Azure AD is enabled?</span></span>
<span data-ttu-id="5096e-363">FabricClient и FabricGateway выполняют взаимную аутентификацию.</span><span class="sxs-lookup"><span data-stu-id="5096e-363">FabricClient and FabricGateway perform a mutual authentication.</span></span> <span data-ttu-id="5096e-364">Во время проверки подлинности Azure AD интеграция Azure AD предоставляет клиента сервер toohello удостоверений и сертификат сервера hello является удостоверение сервера используется tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="5096e-364">During Azure AD authentication, Azure AD integration provides a client identity toohello server, and hello server certificate is used tooverify hello server identity.</span></span> <span data-ttu-id="5096e-365">Дополнительные сведения о сертификатах Service Fabric см. в разделе [Сертификаты X.509 и Service Fabric][x509-certificates-and-service-fabric].</span><span class="sxs-lookup"><span data-stu-id="5096e-365">For more information about Service Fabric certificates, see [X.509 certificates and Service Fabric][x509-certificates-and-service-fabric].</span></span>

<!-- Links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[aad-graph-api-docs]:https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog
[azure-classic-portal]: https://manage.windowsazure.com
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[active-directory-howto-tenant]: ../active-directory/active-directory-howto-tenant.md
[service-fabric-visualizing-your-cluster]: service-fabric-visualizing-your-cluster.md
[service-fabric-manage-application-in-visual-studio]: service-fabric-manage-application-in-visual-studio.md
[sf-aad-ps-script-download]:http://servicefabricsdkstorage.blob.core.windows.net/publicrelease/MicrosoftAzureServiceFabric-AADHelpers.zip
[azure-quickstart-templates]: https://github.com/Azure/azure-quickstart-templates
[service-fabric-secure-cluster-5-node-1-nodetype]: https://github.com/Azure/azure-quickstart-templates/blob/master/service-fabric-secure-cluster-5-node-1-nodetype/
[resource-group-template-deploy]: https://azure.microsoft.com/documentation/articles/resource-group-template-deploy/
[x509-certificates-and-service-fabric]: service-fabric-cluster-security.md#x509-certificates-and-service-fabric

<!-- Images -->
[cluster-security-arm-dependency-map]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-arm-dependency-map.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
[assign-users-to-roles-button]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles-button.png
[assign-users-to-roles-dialog]: ./media/service-fabric-cluster-creation-via-arm/assign-users-to-roles.png
[sfx-select-certificate-dialog]: ./media/service-fabric-cluster-creation-via-arm/sfx-select-certificate-dialog.png
[sfx-reply-address-not-match]: ./media/service-fabric-cluster-creation-via-arm/sfx-reply-address-not-match.png
[web-application-reply-url]: ./media/service-fabric-cluster-creation-via-arm/web-application-reply-url.png

