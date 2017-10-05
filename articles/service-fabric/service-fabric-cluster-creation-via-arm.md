---
title: "Создание кластера Azure Service Fabric из шаблона | Документация Майкрософт"
description: "В этой статье описывается настройка защищенного кластера Service Fabric в Azure с помощью Azure Resource Manager, Azure Key Vault и Azure Active Directory (Azure AD) для аутентификации клиента."
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
ms.openlocfilehash: 420ea486e626763af65a23e49ce04033ea418fb4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-fabric-cluster-by-using-azure-resource-manager"></a><span data-ttu-id="d1e77-103">Создание кластера Service Fabric в Azure с помощью Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d1e77-103">Create a Service Fabric cluster by using Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d1e77-104">Диспетчер ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="d1e77-104">Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
> * [<span data-ttu-id="d1e77-105">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="d1e77-105">Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
>
>

<span data-ttu-id="d1e77-106">Это пошаговое руководство поможет выполнить настройку защищенного кластера Azure Service Fabric в Azure с помощью Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d1e77-106">This step-by-step guide walks you through setting up a secure Azure Service Fabric cluster in Azure by using Azure Resource Manager.</span></span> <span data-ttu-id="d1e77-107">Мы понимаем, что эта статья получилась довольно объемной.</span><span class="sxs-lookup"><span data-stu-id="d1e77-107">We acknowledge that the article is long.</span></span> <span data-ttu-id="d1e77-108">Тем не менее, если вы уже хорошо знакомы с ее содержимым, убедитесь, что тщательно выполняете каждое действие.</span><span class="sxs-lookup"><span data-stu-id="d1e77-108">Nevertheless, unless you are already thoroughly familiar with the content, be sure to follow each step carefully.</span></span>

<span data-ttu-id="d1e77-109">В этом руководстве описываются следующие процедуры.</span><span class="sxs-lookup"><span data-stu-id="d1e77-109">The guide covers the following procedures:</span></span>

* <span data-ttu-id="d1e77-110">Настройка Azure Key Vault для отправки сертификатов для безопасности кластера и приложений</span><span class="sxs-lookup"><span data-stu-id="d1e77-110">Setting up an Azure key vault to upload certificates for cluster and application security</span></span>
* <span data-ttu-id="d1e77-111">Создание защищенного кластера в Azure с помощью Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d1e77-111">Creating a secured cluster in Azure by using Azure Resource Manager</span></span>
* <span data-ttu-id="d1e77-112">Аутентификация пользователей с помощью Azure Active Directory для управления кластером</span><span class="sxs-lookup"><span data-stu-id="d1e77-112">Authenticating users by using Azure Active Directory (Azure AD) for cluster management</span></span>

<span data-ttu-id="d1e77-113">Безопасный кластер — это кластер, в котором предотвращается несанкционированный доступ к операциям управления.</span><span class="sxs-lookup"><span data-stu-id="d1e77-113">A secure cluster is a cluster that prevents unauthorized access to management operations.</span></span> <span data-ttu-id="d1e77-114">Это предусматривает развертывание, обновление и удаление приложений, служб и данных, которые они содержат.</span><span class="sxs-lookup"><span data-stu-id="d1e77-114">This includes deploying, upgrading, and deleting applications, services, and the data they contain.</span></span> <span data-ttu-id="d1e77-115">Незащищенный кластер — это кластер, к которому в любое время может подключиться любой пользователь и выполнять операции управления.</span><span class="sxs-lookup"><span data-stu-id="d1e77-115">An unsecure cluster is a cluster that anyone can connect to at any time and perform management operations.</span></span> <span data-ttu-id="d1e77-116">Хотя кластер можно создать небезопасным, настоятельно рекомендуется с самого начала создать безопасный кластер.</span><span class="sxs-lookup"><span data-stu-id="d1e77-116">Although it is possible to create an unsecure cluster, we highly recommend that you create a secure cluster from the outset.</span></span> <span data-ttu-id="d1e77-117">Поскольку незащищенный кластер невозможно будет защитить позднее, нужно создать новый кластер.</span><span class="sxs-lookup"><span data-stu-id="d1e77-117">Because an unsecure cluster cannot be secured later, a new cluster must be created.</span></span>

<span data-ttu-id="d1e77-118">Концепция создания безопасного кластер в Linux или Windows ничем не отличается.</span><span class="sxs-lookup"><span data-stu-id="d1e77-118">The concept of creating secure clusters is the same, whether they are Linux or Windows clusters.</span></span> <span data-ttu-id="d1e77-119">Дополнительные сведения о создании безопасных кластеров Linux, а также вспомогательные скрипты см. в разделе [Создание безопасных кластеров в Linux](#secure-linux-clusters).</span><span class="sxs-lookup"><span data-stu-id="d1e77-119">For more information and helper scripts for creating secure Linux clusters, see [Creating secure clusters on Linux](#secure-linux-clusters).</span></span>

## <a name="sign-in-to-your-azure-account"></a><span data-ttu-id="d1e77-120">Вход в учетную запись Azure</span><span class="sxs-lookup"><span data-stu-id="d1e77-120">Sign in to your Azure account</span></span>
<span data-ttu-id="d1e77-121">В этом руководстве используется [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="d1e77-121">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="d1e77-122">При запуске нового сеанса PowerShell войдите в свою учетную запись Azure и выберите подписку перед выполнением команд Azure.</span><span class="sxs-lookup"><span data-stu-id="d1e77-122">When you start a new PowerShell session, sign in to your Azure account and select your subscription before you execute Azure commands.</span></span>

<span data-ttu-id="d1e77-123">Вход в учетную запись Azure:</span><span class="sxs-lookup"><span data-stu-id="d1e77-123">Sign in to your Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="d1e77-124">Выберите свою подписку.</span><span class="sxs-lookup"><span data-stu-id="d1e77-124">Select your subscription:</span></span>

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-a-key-vault"></a><span data-ttu-id="d1e77-125">Настройка хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="d1e77-125">Set up a key vault</span></span>
<span data-ttu-id="d1e77-126">В этом разделе описывается, как создать хранилище ключей для кластера Service Fabric в Azure и приложений Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d1e77-126">This section discusses creating a key vault for a Service Fabric cluster in Azure and for Service Fabric applications.</span></span> <span data-ttu-id="d1e77-127">Полное руководство по использованию Azure Key Vault см. в статье [Приступая к работе с хранилищем ключей Azure][key-vault-get-started].</span><span class="sxs-lookup"><span data-stu-id="d1e77-127">For a complete guide to Azure Key Vault, refer to the [Key Vault getting started guide][key-vault-get-started].</span></span>

<span data-ttu-id="d1e77-128">Service Fabric использует сертификаты X.509 для защиты кластера и обеспечения функций безопасности приложений.</span><span class="sxs-lookup"><span data-stu-id="d1e77-128">Service Fabric uses X.509 certificates to secure a cluster and provide application security features.</span></span> <span data-ttu-id="d1e77-129">Key Vault используется для управления сертификатами кластеров Service Fabric в Azure.</span><span class="sxs-lookup"><span data-stu-id="d1e77-129">You use Key Vault to manage certificates for Service Fabric clusters in Azure.</span></span> <span data-ttu-id="d1e77-130">При развертывании кластера в Azure поставщик ресурсов Azure, ответственный за создание кластеров Service Fabric, извлекает сертификаты из Key Vault и устанавливает их на виртуальные машины кластера.</span><span class="sxs-lookup"><span data-stu-id="d1e77-130">When a cluster is deployed in Azure, the Azure resource provider that's responsible for creating Service Fabric clusters pulls certificates from Key Vault and installs them on the cluster VMs.</span></span>

<span data-ttu-id="d1e77-131">На приведенной ниже схеме показана связь между Azure Key Vault, кластером Service Fabric и поставщиком ресурсов Azure, который использует сертификаты из Key Vault при создании кластера.</span><span class="sxs-lookup"><span data-stu-id="d1e77-131">The following diagram illustrates the relationship between Azure Key Vault, a Service Fabric cluster, and the Azure resource provider that uses certificates stored in a key vault when it creates a cluster:</span></span>

![Схема установки сертификата][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a><span data-ttu-id="d1e77-133">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="d1e77-133">Create a resource group</span></span>
<span data-ttu-id="d1e77-134">Первый шаг — создание группы ресурсов специально для хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="d1e77-134">The first step is to create a resource group specifically for your key vault.</span></span> <span data-ttu-id="d1e77-135">Рекомендуется поместить хранилище ключей в собственной группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d1e77-135">We recommend that you put the key vault into its own resource group.</span></span> <span data-ttu-id="d1e77-136">Так вы сможете удалять группы ресурсов для вычислений и хранения, включая группу ресурсов, в которой размещен кластер Service Fabric, без потери ключей и секретов.</span><span class="sxs-lookup"><span data-stu-id="d1e77-136">This action lets you remove the compute and storage resource groups, including the resource group that contains your Service Fabric cluster, without losing your keys and secrets.</span></span> <span data-ttu-id="d1e77-137">Группа ресурсов с хранилищем ключей _должна находиться в том же регионе_, что и кластер, который ее использует.</span><span class="sxs-lookup"><span data-stu-id="d1e77-137">The resource group that contains your key vault _must be in the same region_ as the cluster that is using it.</span></span>

<span data-ttu-id="d1e77-138">Если вы планируете развертывание кластеров в нескольких регионах, рекомендуется выбрать имя для группы ресурсов и хранилища ключей, чтобы обозначить область, к которой они относятся.</span><span class="sxs-lookup"><span data-stu-id="d1e77-138">If you plan to deploy clusters in multiple regions, we suggest that you name the resource group and the key vault in a way that indicates which region it belongs to.</span></span>  

```powershell

    New-AzureRmResourceGroup -Name westus-mykeyvault -Location 'West US'
```
<span data-ttu-id="d1e77-139">Выходные данные должны выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="d1e77-139">The output should look like this:</span></span>

```powershell

    WARNING: The output object type of this cmdlet is going to be modified in a future release.

    ResourceGroupName : westus-mykeyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/westus-mykeyvault

```
<a id="new-key-vault"></a>

### <a name="create-a-key-vault-in-the-new-resource-group"></a><span data-ttu-id="d1e77-140">Создание хранилища ключей в новой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d1e77-140">Create a key vault in the new resource group</span></span>
<span data-ttu-id="d1e77-141">Хранилище ключей _должно быть доступно для развернутой службы_. Это позволит поставщику вычислительных ресурсов получить из него сертификаты и установить их на экземплярах виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d1e77-141">The key vault _must be enabled for deployment_ to allow the compute resource provider to get certificates from it and install it on virtual machine instances:</span></span>

```powershell

    New-AzureRmKeyVault -VaultName 'mywestusvault' -ResourceGroupName 'westus-mykeyvault' -Location 'West US' -EnabledForDeployment

```

<span data-ttu-id="d1e77-142">Выходные данные должны выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="d1e77-142">The output should look like this:</span></span>

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
                                       Permissions to Keys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions to Secrets   :    all


    Tags                             :
```
<a id="existing-key-vault"></a>

## <a name="use-an-existing-key-vault"></a><span data-ttu-id="d1e77-143">Использование существующего хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="d1e77-143">Use an existing key vault</span></span>

<span data-ttu-id="d1e77-144">Чтобы использовать существующее хранилище ключей, _необходимо включить его для развернутой службы_, благодаря чему поставщик вычислительных ресурсов сможет получить из него сертификаты и установить его на узлах кластера:</span><span class="sxs-lookup"><span data-stu-id="d1e77-144">To use an existing key vault, you _must enable it for deployment_ to allow the compute resource provider to get certificates from it and install it on cluster nodes:</span></span>

```powershell

Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

```

<a id="add-certificate-to-key-vault"></a>

## <a name="add-certificates-to-your-key-vault"></a><span data-ttu-id="d1e77-145">Добавление сертификатов в хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="d1e77-145">Add certificates to your key vault</span></span>

<span data-ttu-id="d1e77-146">Сертификаты используются в Service Fabric, чтобы обеспечить функции аутентификации и шифрования для защиты различных аспектов кластера и его приложений.</span><span class="sxs-lookup"><span data-stu-id="d1e77-146">Certificates are used in Service Fabric to provide authentication and encryption to secure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="d1e77-147">Дополнительные сведения о том, как сертификаты используются в Service Fabric, см. в статье [Сценарии защиты кластера Service Fabric][service-fabric-cluster-security].</span><span class="sxs-lookup"><span data-stu-id="d1e77-147">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios][service-fabric-cluster-security].</span></span>

### <a name="cluster-and-server-certificate-required"></a><span data-ttu-id="d1e77-148">Сертификат кластера и сервера (обязательно)</span><span class="sxs-lookup"><span data-stu-id="d1e77-148">Cluster and server certificate (required)</span></span>
<span data-ttu-id="d1e77-149">Этот сертификат требуется для защиты кластера и предотвращения несанкционированного доступа к нему.</span><span class="sxs-lookup"><span data-stu-id="d1e77-149">This certificate is required to secure a cluster and prevent unauthorized access to it.</span></span> <span data-ttu-id="d1e77-150">Он обеспечивает безопасность кластера двумя способами.</span><span class="sxs-lookup"><span data-stu-id="d1e77-150">It provides cluster security in two ways:</span></span>

* <span data-ttu-id="d1e77-151">Аутентификация в кластере позволяет аутентифицировать обмен данными между узлами для федерации кластера.</span><span class="sxs-lookup"><span data-stu-id="d1e77-151">Cluster authentication: Authenticates node-to-node communication for cluster federation.</span></span> <span data-ttu-id="d1e77-152">Только узлы, которые могут подтвердить свою подлинность с помощью этого сертификата, могут присоединиться к кластеру.</span><span class="sxs-lookup"><span data-stu-id="d1e77-152">Only nodes that can prove their identity with this certificate can join the cluster.</span></span>
* <span data-ttu-id="d1e77-153">Аутентификация сервера позволяет аутентифицировать конечные точки управления кластера в клиенте управления, чтобы он "знал", что обращается к настоящему кластеру.</span><span class="sxs-lookup"><span data-stu-id="d1e77-153">Server authentication: Authenticates the cluster management endpoints to a management client, so that the management client knows it is talking to the real cluster.</span></span> <span data-ttu-id="d1e77-154">Этот сертификат также предоставляет SSL для API управления HTTPS и Service Fabric Explorer по протоколу HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d1e77-154">This certificate also provides an SSL for the HTTPS management API and for Service Fabric Explorer over HTTPS.</span></span>

<span data-ttu-id="d1e77-155">Для этого сертификат должен отвечать следующим требованиям:</span><span class="sxs-lookup"><span data-stu-id="d1e77-155">To serve these purposes, the certificate must meet the following requirements:</span></span>

* <span data-ttu-id="d1e77-156">Сертификат должен содержать закрытый ключ.</span><span class="sxs-lookup"><span data-stu-id="d1e77-156">The certificate must contain a private key.</span></span>
* <span data-ttu-id="d1e77-157">Сертификат должен быть создан для обмена ключами, которые можно экспортировать в файл обмена личной информацией (PFX-файл).</span><span class="sxs-lookup"><span data-stu-id="d1e77-157">The certificate must be created for key exchange, which is exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="d1e77-158">Имя субъекта сертификата должно совпадать с доменным именем, которое используется для обращения к кластеру Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d1e77-158">The certificate's subject name must match the domain that you use to access the Service Fabric cluster.</span></span> <span data-ttu-id="d1e77-159">Это необходимо, чтобы предоставить SSL-протокол конечным точкам управления HTTPS в кластере и Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="d1e77-159">This matching is required to provide an SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="d1e77-160">Не удается получить SSL-сертификат от центра сертификации (ЦС) в домене .cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="d1e77-160">You cannot obtain an SSL certificate from a certificate authority (CA) for the .cloudapp.azure.com domain.</span></span> <span data-ttu-id="d1e77-161">Необходимо получить имя личного домена для кластера.</span><span class="sxs-lookup"><span data-stu-id="d1e77-161">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="d1e77-162">При запросе сертификата из ЦС имя субъекта сертификата должно совпадать с именем личного домена, используемого для кластера.</span><span class="sxs-lookup"><span data-stu-id="d1e77-162">When you request a certificate from a CA, the certificate's subject name must match the custom domain name that you use for your cluster.</span></span>

### <a name="application-certificates-optional"></a><span data-ttu-id="d1e77-163">Сертификаты приложения (необязательно)</span><span class="sxs-lookup"><span data-stu-id="d1e77-163">Application certificates (optional)</span></span>
<span data-ttu-id="d1e77-164">В кластере можно установить любое количество дополнительных сертификатов для обеспечения безопасности приложений.</span><span class="sxs-lookup"><span data-stu-id="d1e77-164">Any number of additional certificates can be installed on a cluster for application security purposes.</span></span> <span data-ttu-id="d1e77-165">Перед созданием кластера рассмотрите сценарии безопасности приложений, которые требуют установки сертификатов на узлах, в том числе:</span><span class="sxs-lookup"><span data-stu-id="d1e77-165">Before creating your cluster, consider the application security scenarios that require a certificate to be installed on the nodes, such as:</span></span>

* <span data-ttu-id="d1e77-166">шифрование и расшифровка значений конфигурации приложений;</span><span class="sxs-lookup"><span data-stu-id="d1e77-166">Encryption and decryption of application configuration values.</span></span>
* <span data-ttu-id="d1e77-167">шифрование данных между узлами во время репликации.</span><span class="sxs-lookup"><span data-stu-id="d1e77-167">Encryption of data across nodes during replication.</span></span>

### <a name="formatting-certificates-for-azure-resource-provider-use"></a><span data-ttu-id="d1e77-168">форматирование сертификатов для использования поставщиком ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="d1e77-168">Formatting certificates for Azure resource provider use</span></span>
<span data-ttu-id="d1e77-169">Файлы закрытых ключей (PFX) можно добавить и использовать непосредственно в своем хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="d1e77-169">You can add and use private key files (.pfx) directly through your key vault.</span></span> <span data-ttu-id="d1e77-170">Однако для поставщика вычислительных ресурсов Azure необходимо хранить ключи в специальном формате нотации объектов JavaScript (JSON).</span><span class="sxs-lookup"><span data-stu-id="d1e77-170">However, the Azure compute resource provider requires keys to be stored in a special JavaScript Object Notation (JSON) format.</span></span> <span data-ttu-id="d1e77-171">В этом формате PFX-файл представлен в виде строки в кодировке Base64 и пароля закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="d1e77-171">The format includes the .pfx file as a base 64-encoded string and the private key password.</span></span> <span data-ttu-id="d1e77-172">Чтобы соблюсти эти требования, ключи должны быть помещены в строку JSON и сохранены как "секреты" в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="d1e77-172">To accommodate these requirements, the keys must be placed in a JSON string and then stored as "secrets" in the key vault.</span></span>

<span data-ttu-id="d1e77-173">Для упрощения этого процесса [на сайте GitHub доступен соответствующий модуль PowerShell][service-fabric-rp-helpers].</span><span class="sxs-lookup"><span data-stu-id="d1e77-173">To make this process easier, a [PowerShell module is available on GitHub][service-fabric-rp-helpers].</span></span> <span data-ttu-id="d1e77-174">Чтобы использовать этот модуль, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d1e77-174">To use the module, do the following:</span></span>

1. <span data-ttu-id="d1e77-175">Скачайте все содержимое репозитория в локальный каталог.</span><span class="sxs-lookup"><span data-stu-id="d1e77-175">Download the entire contents of the repo into a local directory.</span></span>
2. <span data-ttu-id="d1e77-176">Перейдите в локальный каталог.</span><span class="sxs-lookup"><span data-stu-id="d1e77-176">Go to the local directory.</span></span>
2. <span data-ttu-id="d1e77-177">Импортируйте модуль ServiceFabricRPHelpers в окне PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d1e77-177">Import the ServiceFabricRPHelpers module in your PowerShell window:</span></span>

```powershell

 Import-Module "C:\..\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

```

<span data-ttu-id="d1e77-178">Команда `Invoke-AddCertToKeyVault` в этом модуле PowerShell автоматически форматирует закрытый ключ сертификата в строку JSON и передает ее в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="d1e77-178">The `Invoke-AddCertToKeyVault` command in this PowerShell module automatically formats a certificate private key into a JSON string and uploads it to the key vault.</span></span> <span data-ttu-id="d1e77-179">Используйте эту команду для добавления сертификата кластера и всех дополнительных сертификатов приложения в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="d1e77-179">Use the command to add the cluster certificate and any additional application certificates to the key vault.</span></span> <span data-ttu-id="d1e77-180">Повторите этот шаг для всех дополнительных сертификатов, которые нужно установить в кластере.</span><span class="sxs-lookup"><span data-stu-id="d1e77-180">Repeat this step for any additional certificates you want to install in your cluster.</span></span>

#### <a name="uploading-an-existing-certificate"></a><span data-ttu-id="d1e77-181">Загрузка существующего сертификата</span><span class="sxs-lookup"><span data-stu-id="d1e77-181">Uploading an existing certificate</span></span>

```powershell

 Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName westus-mykeyvault -Location "West US" -VaultName mywestusvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

```

<span data-ttu-id="d1e77-182">Если появляется сообщение об ошибке, такое как показано здесь, обычно это означает наличие конфликта URL-адресов ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d1e77-182">If you get an error, such as the one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="d1e77-183">Чтобы устранить конфликт, измените имя хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="d1e77-183">To resolve the conflict, change the key vault name.</span></span>

```
Set-AzureKeyVaultSecret : The remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="d1e77-184">После устранения конфликта результат должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d1e77-184">After the conflict is resolved, the output should look like this:</span></span>

```

    Switching context to SubscriptionId <guid>
    Ensuring ResourceGroup westus-mykeyvault in West US
    WARNING: The output object type of this cmdlet is going to be modified in a future release.
    Using existing value mywestusvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret to mywestusvault in vault mywestusvault


Name  : CertificateThumbprint
Value : E21DBC64B183B5BF355C34C46E03409FEEAEF58D

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/westus-mykeyvault/providers/Microsoft.KeyVault/vaults/mywestusvault

Name  : CertificateURL
Value : https://mywestusvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

>[!NOTE]
><span data-ttu-id="d1e77-185">Чтобы настроить безопасность кластера Service Fabric и получить все сертификаты приложения, которые, возможно, будут использоваться для обеспечения безопасности приложения, необходимы три строки — CertificateThumbprint, SourceVault и CertificateURL.</span><span class="sxs-lookup"><span data-stu-id="d1e77-185">You need the three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, to set up a secure Service Fabric cluster and to obtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="d1e77-186">Если не сохранить эти строки, позднее могут возникнуть трудности с их получением путем запроса в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="d1e77-186">If you do not save the strings, it can be difficult to retrieve them by querying the key vault later.</span></span>

<a id="add-self-signed-certificate-to-key-vault"></a>

#### <a name="creating-a-self-signed-certificate-and-uploading-it-to-the-key-vault"></a><span data-ttu-id="d1e77-187">Создание самозаверяющего сертификата и передача его в хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="d1e77-187">Creating a self-signed certificate and uploading it to the key vault</span></span>

<span data-ttu-id="d1e77-188">Если сертификат уже отправлен в хранилище ключей, пропустите этот шаг.</span><span class="sxs-lookup"><span data-stu-id="d1e77-188">If you have already uploaded your certificates to the key vault, skip this step.</span></span> <span data-ttu-id="d1e77-189">На этом шаге создается новый самозаверяющий сертификат и выполняется его передача в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="d1e77-189">This step is for generating a new self-signed certificate and uploading it to your key vault.</span></span> <span data-ttu-id="d1e77-190">После изменения параметров в следующем сценарии и его выполнения вам будет предложено ввести пароль сертификата.</span><span class="sxs-lookup"><span data-stu-id="d1e77-190">After you change the parameters in the following script and then run it, you should be prompted for a certificate password.</span></span>  

```powershell

$ResourceGroup = "chackowestuskv"
$VName = "chackokv2"
$SubID = "6c653126-e4ba-42cd-a1dd-f7bf96ae7a47"
$locationRegion = "westus"
$newCertName = "chackotestcertificate1"
$dnsName = "www.mycluster.westus.mydomain.com" #The certificate's subject name must match the domain used to access the Service Fabric cluster.
$localCertPath = "C:\MyCertificates" # location where you want the .PFX to be stored

 Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResourceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath

```

<span data-ttu-id="d1e77-191">Если появляется сообщение об ошибке, такое как показано здесь, обычно это означает наличие конфликта URL-адресов ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d1e77-191">If you get an error, such as the one shown here, it usually means that you have a resource URL conflict.</span></span> <span data-ttu-id="d1e77-192">Чтобы устранить конфликт, измените имя хранилища ключей, имя группы ресурсов и т. д.</span><span class="sxs-lookup"><span data-stu-id="d1e77-192">To resolve the conflict, change the key vault name, RG name, and so forth.</span></span>

```
Set-AzureKeyVaultSecret : The remote name could not be resolved: 'westuskv.vault.azure.net'
At C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1:440 char:11
+ $secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $Certif ...
+           ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : CloseError: (:) [Set-AzureKeyVaultSecret], WebException
    + FullyQualifiedErrorId : Microsoft.Azure.Commands.KeyVault.SetAzureKeyVaultSecret

```

<span data-ttu-id="d1e77-193">После устранения конфликта результат должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d1e77-193">After the conflict is resolved, the output should look like this:</span></span>

```
PS C:\Users\chackdan\Documents\GitHub\Service-Fabric\Scripts\ServiceFabricRPHelpers> Invoke-AddCertToKeyVault -SubscriptionId $SubID -ResourceGroupName $ResouceGroup -Location $locationRegion -VaultName $VName -CertificateName $newCertName -Password $certPassword -CreateSelfSignedCertificate -DnsName $dnsName -OutputPath $localCertPath
Switching context to SubscriptionId 6c343126-e4ba-52cd-a1dd-f8bf96ae7a47
Ensuring ResourceGroup chackowestuskv in westus
WARNING: The output object type of this cmdlet will be modified in a future release.
Creating new vault westuskv1 in westus
Creating new self signed certificate at C:\MyCertificates\chackonewcertificate1.pfx
Reading pfx file from C:\MyCertificates\chackonewcertificate1.pfx
Writing secret to chackonewcertificate1 in vault westuskv1


Name  : CertificateThumbprint
Value : 96BB3CC234F9D43C25D4B547sd8DE7B569F413EE

Name  : SourceVault
Value : /subscriptions/6c653126-e4ba-52cd-a1dd-f8bf96ae7a47/resourceGroups/chackowestuskv/providers/Microsoft.KeyVault/vaults/westuskv1

Name  : CertificateURL
Value : https://westuskv1.vault.azure.net:443/secrets/chackonewcertificate1/ee247291e45d405b8c8bbf81782d12bd

```

>[!NOTE]
><span data-ttu-id="d1e77-194">Чтобы настроить безопасность кластера Service Fabric и получить все сертификаты приложения, которые, возможно, будут использоваться для обеспечения безопасности приложения, необходимы три строки — CertificateThumbprint, SourceVault и CertificateURL.</span><span class="sxs-lookup"><span data-stu-id="d1e77-194">You need the three preceding strings, CertificateThumbprint, SourceVault, and CertificateURL, to set up a secure Service Fabric cluster and to obtain any application certificates that you might be using for application security.</span></span> <span data-ttu-id="d1e77-195">Если не сохранить эти строки, позднее могут возникнуть трудности с их получением путем запроса в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="d1e77-195">If you do not save the strings, it can be difficult to retrieve them by querying the key vault later.</span></span>

 <span data-ttu-id="d1e77-196">На этом этапе должны быть доступны следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="d1e77-196">At this point, you should have the following elements in place:</span></span>

* <span data-ttu-id="d1e77-197">группа ресурсов хранилища ключей;</span><span class="sxs-lookup"><span data-stu-id="d1e77-197">The key vault resource group.</span></span>
* <span data-ttu-id="d1e77-198">хранилище ключей и его URL-адрес (вызываемое SourceVault в предыдущем выводе PowerShell);</span><span class="sxs-lookup"><span data-stu-id="d1e77-198">The key vault and its URL (called SourceVault in the preceding PowerShell output).</span></span>
* <span data-ttu-id="d1e77-199">сертификат аутентификации сервера кластера и его URL-адрес в хранилище ключей;</span><span class="sxs-lookup"><span data-stu-id="d1e77-199">The cluster server authentication certificate and its URL in the key vault.</span></span>
* <span data-ttu-id="d1e77-200">сертификаты приложений и их URL-адреса в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="d1e77-200">The application certificates and their URLs in the key vault.</span></span>


<a id="add-AAD-for-client"></a>

## <a name="set-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="d1e77-201">Настройка Azure Active Directory для проверки подлинности клиента</span><span class="sxs-lookup"><span data-stu-id="d1e77-201">Set up Azure Active Directory for client authentication</span></span>

<span data-ttu-id="d1e77-202">Azure AD позволяет организациям (известным как клиенты) управлять доступом пользователей к приложениям.</span><span class="sxs-lookup"><span data-stu-id="d1e77-202">Azure AD enables organizations (known as tenants) to manage user access to applications.</span></span> <span data-ttu-id="d1e77-203">Приложения можно разделить на две группы: те, в которых есть пользовательский веб-интерфейс входа в систему, и те, в которых вход выполняется с помощью собственного клиентского приложения.</span><span class="sxs-lookup"><span data-stu-id="d1e77-203">Applications are divided into those with a web-based sign-in UI and those with a native client experience.</span></span> <span data-ttu-id="d1e77-204">В этой статье предполагается, что клиент уже создан.</span><span class="sxs-lookup"><span data-stu-id="d1e77-204">In this article, we assume that you have already created a tenant.</span></span> <span data-ttu-id="d1e77-205">Если это не так, обратитесь к статье [Как получить клиент Azure Active Directory][active-directory-howto-tenant].</span><span class="sxs-lookup"><span data-stu-id="d1e77-205">If you have not, start by reading [How to get an Azure Active Directory tenant][active-directory-howto-tenant].</span></span>

<span data-ttu-id="d1e77-206">Кластеры Service Fabric предлагают несколько точек входа для управления функциями кластеров, включая веб-интерфейс [Service Fabric Explorer][service-fabric-visualizing-your-cluster] и [Visual Studio][service-fabric-manage-application-in-visual-studio].</span><span class="sxs-lookup"><span data-stu-id="d1e77-206">A Service Fabric cluster offers several entry points to its management functionality, including the web-based [Service Fabric Explorer][service-fabric-visualizing-your-cluster] and [Visual Studio][service-fabric-manage-application-in-visual-studio].</span></span> <span data-ttu-id="d1e77-207">В итоге вы получаете два приложения Azure AD для управления доступом к кластеру: одно веб-приложение и одно собственное приложение.</span><span class="sxs-lookup"><span data-stu-id="d1e77-207">As a result, you create two Azure AD applications to control access to the cluster, one web application and one native application.</span></span>

<span data-ttu-id="d1e77-208">Чтобы упростить некоторые шаги по настройке Azure AD с кластером Service Fabric, мы создали набор сценариев Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d1e77-208">To simplify some of the steps involved in configuring Azure AD with a Service Fabric cluster, we have created a set of Windows PowerShell scripts.</span></span>

> [!NOTE]
> <span data-ttu-id="d1e77-209">Перед созданием кластера необходимо выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d1e77-209">You must complete the following steps before you create the cluster.</span></span> <span data-ttu-id="d1e77-210">Поскольку в сценариях предварительно заданы имена кластеров и конечные точки, эти имена нужно выбрать заблаговременно, при этом они должны отличаться от созданных ранее имен.</span><span class="sxs-lookup"><span data-stu-id="d1e77-210">Because the scripts expect cluster names and endpoints, the values should be planned and not values that you have already created.</span></span>

1. <span data-ttu-id="d1e77-211">[Скачайте сценарии][sf-aad-ps-script-download] на компьютер.</span><span class="sxs-lookup"><span data-stu-id="d1e77-211">[Download the scripts][sf-aad-ps-script-download] to your computer.</span></span>
2. <span data-ttu-id="d1e77-212">Щелкните правой кнопкой мыши ZIP-файл, выберите **Свойства**, установите флажок **Разблокировать** и нажмите кнопку **Применить**.</span><span class="sxs-lookup"><span data-stu-id="d1e77-212">Right-click the zip file, select **Properties**, select the **Unblock** check box, and then click **Apply**.</span></span>
3. <span data-ttu-id="d1e77-213">Извлеките ZIP-файл.</span><span class="sxs-lookup"><span data-stu-id="d1e77-213">Extract the zip file.</span></span>
4. <span data-ttu-id="d1e77-214">Запустите `SetupApplications.ps1` и укажите TenantId (идентификатор клиента), ClusterName (имя кластера) и WebApplicationReplyUrl (URL-адрес ответа веб-приложения) в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="d1e77-214">Run `SetupApplications.ps1`, and provide the TenantId, ClusterName, and WebApplicationReplyUrl as parameters.</span></span> <span data-ttu-id="d1e77-215">Например:</span><span class="sxs-lookup"><span data-stu-id="d1e77-215">For example:</span></span>

    ```powershell
    .\SetupApplications.ps1 -TenantId '690ec069-8200-4068-9d01-5aaf188e557a' -ClusterName 'mycluster' -WebApplicationReplyUrl 'https://mycluster.westus.cloudapp.azure.com:19080/Explorer/index.html'
    ```

    <span data-ttu-id="d1e77-216">Чтобы узнать TenantId, можно выполнить команду PowerShell `Get-AzureSubscription`.</span><span class="sxs-lookup"><span data-stu-id="d1e77-216">You can find your TenantId by executing the PowerShell command `Get-AzureSubscription`.</span></span> <span data-ttu-id="d1e77-217">После выполнения этой команды для каждой подписки отображается TenantId.</span><span class="sxs-lookup"><span data-stu-id="d1e77-217">Executing this command displays the TenantId for every subscription.</span></span>

    <span data-ttu-id="d1e77-218">Значение ClusterName используется в качестве префикса для приложений Azure AD, создаваемых сценарием.</span><span class="sxs-lookup"><span data-stu-id="d1e77-218">ClusterName is used to prefix the Azure AD applications that are created by the script.</span></span> <span data-ttu-id="d1e77-219">Точное совпадение с именем реального кластера не требуется.</span><span class="sxs-lookup"><span data-stu-id="d1e77-219">It does not need to match the actual cluster name exactly.</span></span> <span data-ttu-id="d1e77-220">Оно предназначено только для упрощения сопоставления артефактов Azure AD с кластером Service Fabric, с которым они используются.</span><span class="sxs-lookup"><span data-stu-id="d1e77-220">It is intended only to make it easier to map Azure AD artifacts to the Service Fabric cluster that they're being used with.</span></span>

    <span data-ttu-id="d1e77-221">WebApplicationReplyUrl является конечной точкой по умолчанию, которую Azure AD возвращает пользователям после завершения ими входа.</span><span class="sxs-lookup"><span data-stu-id="d1e77-221">WebApplicationReplyUrl is the default endpoint that Azure AD returns to your users after they finish signing in.</span></span> <span data-ttu-id="d1e77-222">Эту конечную точку следует назначить конечной точкой Service Fabric Explorer для кластера, по умолчанию это:</span><span class="sxs-lookup"><span data-stu-id="d1e77-222">Set this endpoint as the Service Fabric Explorer endpoint for your cluster, which by default is:</span></span>

    <span data-ttu-id="d1e77-223">https://&lt;cluster_domain&gt;:19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="d1e77-223">https://&lt;cluster_domain&gt;:19080/Explorer</span></span>

    <span data-ttu-id="d1e77-224">Вам будет предложено войти в учетную запись с правами администратора для клиента Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d1e77-224">You are prompted to sign in to an account that has administrative privileges for the Azure AD tenant.</span></span> <span data-ttu-id="d1e77-225">После входа сценарий начнет создавать веб-приложение и собственное приложение для представления кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d1e77-225">After you sign in, the script creates the web and native applications to represent your Service Fabric cluster.</span></span> <span data-ttu-id="d1e77-226">Если посмотреть на список приложений клиента на [классическом портале Azure][azure-classic-portal], вы увидите два новых приложения:</span><span class="sxs-lookup"><span data-stu-id="d1e77-226">If you look at the tenant's applications in the [Azure classic portal][azure-classic-portal], you should see two new entries:</span></span>

   * <span data-ttu-id="d1e77-227">*имя_кластера*\_Кластер</span><span class="sxs-lookup"><span data-stu-id="d1e77-227">*ClusterName*\_Cluster</span></span>
   * <span data-ttu-id="d1e77-228">*имя_кластера*\_Клиент</span><span class="sxs-lookup"><span data-stu-id="d1e77-228">*ClusterName*\_Client</span></span>

   <span data-ttu-id="d1e77-229">Этот скрипт выводит код JSON для шаблона Azure Resource Manager, который вы будете использовать в следующем разделе для создания кластера. Рекомендуем не закрывать пока окно PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d1e77-229">The script prints the JSON required by the Azure Resource Manager template when you create the cluster in the next section, so it's a good idea to keep the PowerShell window open.</span></span>

```json
"azureActiveDirectory": {
  "tenantId":"<guid>",
  "clusterApplication":"<guid>",
  "clientApplication":"<guid>"
},
```

## <a name="create-a-service-fabric-cluster-resource-manager-template"></a><span data-ttu-id="d1e77-230">Создание шаблона Resource Manager для кластера Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d1e77-230">Create a Service Fabric cluster Resource Manager template</span></span>
<span data-ttu-id="d1e77-231">В этом разделе выходные данные предыдущей команды PowerShell переносятся в шаблон Resource Manager для кластера Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d1e77-231">In this section, the outputs of the preceding PowerShell commands are used in a Service Fabric cluster Resource Manager template.</span></span>

<span data-ttu-id="d1e77-232">Примеры шаблонов Resource Manager доступны в [коллекции шаблонов быстрого запуска Azure на сайте GitHub][azure-quickstart-templates].</span><span class="sxs-lookup"><span data-stu-id="d1e77-232">Sample Resource Manager templates are available in the [Azure quick-start template gallery on GitHub][azure-quickstart-templates].</span></span> <span data-ttu-id="d1e77-233">Их можно использовать в качестве отправной точки для создания шаблона кластера.</span><span class="sxs-lookup"><span data-stu-id="d1e77-233">These templates can be used as a starting point for your cluster template.</span></span>

### <a name="create-the-resource-manager-template"></a><span data-ttu-id="d1e77-234">Создание шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d1e77-234">Create the Resource Manager template</span></span>
<span data-ttu-id="d1e77-235">В этом руководстве используется пример шаблона [защищенного кластера с 5 узлами][service-fabric-secure-cluster-5-node-1-nodetype] и его параметры.</span><span class="sxs-lookup"><span data-stu-id="d1e77-235">This guide uses the [5-node secure cluster][service-fabric-secure-cluster-5-node-1-nodetype] example template and template parameters.</span></span> <span data-ttu-id="d1e77-236">Скачайте файлы `azuredeploy.json` и `azuredeploy.parameters.json` на компьютер и откройте их в текстовом редакторе.</span><span class="sxs-lookup"><span data-stu-id="d1e77-236">Download `azuredeploy.json` and `azuredeploy.parameters.json` to your computer and open both files in your favorite text editor.</span></span>

### <a name="add-certificates"></a><span data-ttu-id="d1e77-237">Добавление сертификатов</span><span class="sxs-lookup"><span data-stu-id="d1e77-237">Add certificates</span></span>
<span data-ttu-id="d1e77-238">Сертификаты добавляются в шаблон Resource Manager кластера с помощью ссылок на хранилище ключей, которое содержит ключи сертификата.</span><span class="sxs-lookup"><span data-stu-id="d1e77-238">You add certificates to a cluster Resource Manager template by referencing the key vault that contains the certificate keys.</span></span> <span data-ttu-id="d1e77-239">Рекомендуется поместить значения хранилища ключей в файл параметров шаблона Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d1e77-239">We recommend that you place the key-vault values in a Resource Manager template parameters file.</span></span> <span data-ttu-id="d1e77-240">Благодаря этому файл шаблона Resource Manager доступен для повторного использования и не зависит от значений, связанных с определенной развернутой службой.</span><span class="sxs-lookup"><span data-stu-id="d1e77-240">Doing so keeps the Resource Manager template file reusable and free of values specific to a deployment.</span></span>

#### <a name="add-all-certificates-to-the-virtual-machine-scale-set-osprofile"></a><span data-ttu-id="d1e77-241">Добавление всех сертификатов в osProfile набора масштабирования виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="d1e77-241">Add all certificates to the virtual machine scale set osProfile</span></span>
<span data-ttu-id="d1e77-242">Каждый сертификат, который устанавливается в кластере, должен быть настроен в разделе osProfile ресурса VMSS (Microsoft.Compute/virtualMachineScaleSets).</span><span class="sxs-lookup"><span data-stu-id="d1e77-242">Every certificate that's installed in the cluster must be configured in the osProfile section of the scale set resource (Microsoft.Compute/virtualMachineScaleSets).</span></span> <span data-ttu-id="d1e77-243">Это указывает, что поставщик ресурсов должен установить сертификат на виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="d1e77-243">This action instructs the resource provider to install the certificate on the VMs.</span></span> <span data-ttu-id="d1e77-244">Эта установка содержит сертификат кластера, а также все сертификаты безопасности приложений, которые планируется использовать для приложений.</span><span class="sxs-lookup"><span data-stu-id="d1e77-244">This installation includes both the cluster certificate and any application security certificates that you plan to use for your applications:</span></span>

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

#### <a name="configure-the-service-fabric-cluster-certificate"></a><span data-ttu-id="d1e77-245">Настройка сертификата кластера Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d1e77-245">Configure the Service Fabric cluster certificate</span></span>
<span data-ttu-id="d1e77-246">Сертификат аутентификации кластера должен быть настроен в ресурсе кластера Service Fabric (Microsoft.ServiceFabric/clusters) и расширении Service Fabric для масштабируемых наборов виртуальных машин в ресурсе масштабируемого набора виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d1e77-246">The cluster authentication certificate must be configured in both the Service Fabric cluster resource (Microsoft.ServiceFabric/clusters) and the Service Fabric extension for virtual machine scale sets in the virtual machine scale set resource.</span></span> <span data-ttu-id="d1e77-247">Это позволяет поставщику ресурсов Service Fabric настроить его, чтобы использовать для аутентификации кластера и сервера на конечных точках управления.</span><span class="sxs-lookup"><span data-stu-id="d1e77-247">This arrangement allows the Service Fabric resource provider to configure it for use for cluster authentication and server authentication for management endpoints.</span></span>

##### <a name="virtual-machine-scale-set-resource"></a><span data-ttu-id="d1e77-248">Ресурс масштабируемого набора виртуальных машин:</span><span class="sxs-lookup"><span data-stu-id="d1e77-248">Virtual machine scale set resource:</span></span>
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

##### <a name="service-fabric-resource"></a><span data-ttu-id="d1e77-249">Ресурс Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d1e77-249">Service Fabric resource:</span></span>
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

### <a name="insert-azure-ad-configuration"></a><span data-ttu-id="d1e77-250">Получение конфигурации Azure AD</span><span class="sxs-lookup"><span data-stu-id="d1e77-250">Insert Azure AD configuration</span></span>
<span data-ttu-id="d1e77-251">Конфигурацию Azure AD, которая была создана ранее, можно добавить непосредственно в шаблон Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d1e77-251">The Azure AD configuration that you created earlier can be inserted directly into your Resource Manager template.</span></span> <span data-ttu-id="d1e77-252">Тем не менее рекомендуется сначала извлечь значения в файл параметров, чтобы сохранить возможность повторного использования шаблона Resource Manager и не привязываться к значениям, относящимся к определенной развернутой службе.</span><span class="sxs-lookup"><span data-stu-id="d1e77-252">However, we recommended that you first extract the values into a parameters file to keep the Resource Manager template reusable and free of values specific to a deployment.</span></span>

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

### <span data-ttu-id="d1e77-253"><a "configure-arm" ></a>Настройка параметров шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d1e77-253"><a "configure-arm" ></a>Configure Resource Manager template parameters</span></span>
<!--- Loc Comment: It seems that <a "configure-arm" > must be replaced with <a name="configure-arm"></a> since the link seems not to be redirecting correctly --->
<span data-ttu-id="d1e77-254">Наконец, используйте полученные значения из хранилища ключей и с помощью команд PowerShell Azure AD для заполнения файла параметров.</span><span class="sxs-lookup"><span data-stu-id="d1e77-254">Finally, use the output values from the key vault and Azure AD PowerShell commands to populate the parameters file:</span></span>

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
<span data-ttu-id="d1e77-255">На этом этапе должны быть доступны следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="d1e77-255">At this point, you should have the following elements in place:</span></span>

* <span data-ttu-id="d1e77-256">группа ресурсов хранилища ключей;</span><span class="sxs-lookup"><span data-stu-id="d1e77-256">Key vault resource group</span></span>
  * <span data-ttu-id="d1e77-257">Хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="d1e77-257">Key vault</span></span>
  * <span data-ttu-id="d1e77-258">сертификат проверки подлинности сервера кластера;</span><span class="sxs-lookup"><span data-stu-id="d1e77-258">Cluster server authentication certificate</span></span>
  * <span data-ttu-id="d1e77-259">сертификат шифрования данных;</span><span class="sxs-lookup"><span data-stu-id="d1e77-259">Data encipherment certificate</span></span>
* <span data-ttu-id="d1e77-260">клиент Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="d1e77-260">Azure Active Directory tenant</span></span>
  * <span data-ttu-id="d1e77-261">приложение Azure AD для управления через Интернет и Service Fabric Explorer;</span><span class="sxs-lookup"><span data-stu-id="d1e77-261">Azure AD application for web-based management and Service Fabric Explorer</span></span>
  * <span data-ttu-id="d1e77-262">приложение Azure AD для управления собственными клиентами.</span><span class="sxs-lookup"><span data-stu-id="d1e77-262">Azure AD application for native client management</span></span>
  * <span data-ttu-id="d1e77-263">Пользователи и назначенные им роли</span><span class="sxs-lookup"><span data-stu-id="d1e77-263">Users and their assigned roles</span></span>
* <span data-ttu-id="d1e77-264">шаблон Resource Manager для кластера Service Fabric;</span><span class="sxs-lookup"><span data-stu-id="d1e77-264">Service Fabric cluster Resource Manager template</span></span>
  * <span data-ttu-id="d1e77-265">Сертификаты, настроенные с помощью хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="d1e77-265">Certificates configured through key vault</span></span>
  * <span data-ttu-id="d1e77-266">настроенная среда Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d1e77-266">Azure Active Directory configured</span></span>

<span data-ttu-id="d1e77-267">На приведенной ниже схеме показано, как конфигурация хранилища ключей и Azure AD помещается в шаблон Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d1e77-267">The following diagram illustrates where your key vault and Azure AD configuration fit into your Resource Manager template.</span></span>

![Сопоставление зависимостей Resource Manager][cluster-security-arm-dependency-map]

## <a name="create-the-cluster"></a><span data-ttu-id="d1e77-269">Создание кластера</span><span class="sxs-lookup"><span data-stu-id="d1e77-269">Create the cluster</span></span>
<span data-ttu-id="d1e77-270">Теперь можно создать кластер с помощью [развертывания шаблона ресурсов Azure][resource-group-template-deploy].</span><span class="sxs-lookup"><span data-stu-id="d1e77-270">You are now ready to create the cluster by using [Azure resource template deployment][resource-group-template-deploy].</span></span>

#### <a name="test-it"></a><span data-ttu-id="d1e77-271">Тестирование</span><span class="sxs-lookup"><span data-stu-id="d1e77-271">Test it</span></span>
<span data-ttu-id="d1e77-272">Используйте следующую команду PowerShell для тестирования шаблона Resource Manager с помощью файла параметров.</span><span class="sxs-lookup"><span data-stu-id="d1e77-272">Use the following PowerShell command to test your Resource Manager template with a parameters file:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

#### <a name="deploy-it"></a><span data-ttu-id="d1e77-273">Развертывание</span><span class="sxs-lookup"><span data-stu-id="d1e77-273">Deploy it</span></span>
<span data-ttu-id="d1e77-274">Если шаблон Resource Manager прошел проверку, то введите следующую команду PowerShell для развертывания этого шаблона с использованием файла параметров.</span><span class="sxs-lookup"><span data-stu-id="d1e77-274">If the Resource Manager template test passes, use the following PowerShell command to deploy your Resource Manager template with a parameters file:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myresourcegroup" -TemplateFile .\azuredeploy.json -TemplateParameterFile .\azuredeploy.parameters.json
```

<a name="assign-roles"></a>

## <a name="assign-users-to-roles"></a><span data-ttu-id="d1e77-275">Назначение пользователей ролям</span><span class="sxs-lookup"><span data-stu-id="d1e77-275">Assign users to roles</span></span>
<span data-ttu-id="d1e77-276">Создав приложения, представляющие кластер, сопоставьте пользователей с ролями, поддерживаемыми Service Fabric и разрешающими доступ на чтение и администрирование. Роли можно назначить с помощью [классического портала Azure][azure-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="d1e77-276">After you have created the applications to represent your cluster, assign your users to the roles supported by Service Fabric: read-only and admin. You can assign the roles by using the [Azure classic portal][azure-classic-portal].</span></span>

1. <span data-ttu-id="d1e77-277">На портале Azure перейдите к нужному клиенту и выберите элемент **Приложения**.</span><span class="sxs-lookup"><span data-stu-id="d1e77-277">In the Azure portal, go to your tenant, and then select **Applications**.</span></span>
2. <span data-ttu-id="d1e77-278">Выберите веб-приложение с именем вида `myTestCluster_Cluster`.</span><span class="sxs-lookup"><span data-stu-id="d1e77-278">Select the web application, which has a name like `myTestCluster_Cluster`.</span></span>
3. <span data-ttu-id="d1e77-279">Откройте вкладку **Пользователи** .</span><span class="sxs-lookup"><span data-stu-id="d1e77-279">Click the **Users** tab.</span></span>
4. <span data-ttu-id="d1e77-280">Выберите пользователя для назначения и нажмите кнопку **Назначить** в нижней части экрана.</span><span class="sxs-lookup"><span data-stu-id="d1e77-280">Select a user to assign, and then click the **Assign** button at the bottom of the screen.</span></span>

    ![Кнопка "Назначить пользователей ролям"][assign-users-to-roles-button]
5. <span data-ttu-id="d1e77-282">Выберите роль для назначения пользователю.</span><span class="sxs-lookup"><span data-stu-id="d1e77-282">Select the role to assign to the user.</span></span>

    ![Диалоговое окно "Назначить пользователей"][assign-users-to-roles-dialog]

> [!NOTE]
> <span data-ttu-id="d1e77-284">Дополнительные сведения о ролях в Service Fabric см. в статье [Контроль доступа на основе ролей для клиентов Service Fabric](service-fabric-cluster-security-roles.md).</span><span class="sxs-lookup"><span data-stu-id="d1e77-284">For more information about roles in Service Fabric, see [Role-based access control for Service Fabric clients](service-fabric-cluster-security-roles.md).</span></span>
>
>

 <a name="secure-linux-clusters"></a>
 <!--- Loc Comment: It seems that letter S in cluster was missing, which caused the wrong redirection of the link --->

## <a name="create-secure-clusters-on-linux"></a><span data-ttu-id="d1e77-285">Создание безопасных кластеров в Linux</span><span class="sxs-lookup"><span data-stu-id="d1e77-285">Create secure clusters on Linux</span></span>
<span data-ttu-id="d1e77-286">Чтобы упростить процесс, мы предоставили [вспомогательный сценарий](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span><span class="sxs-lookup"><span data-stu-id="d1e77-286">To make the process easier, we have provided a [helper script](http://github.com/ChackDan/Service-Fabric/tree/master/Scripts/CertUpload4Linux).</span></span> <span data-ttu-id="d1e77-287">Прежде чем использовать этот вспомогательный сценарий, убедитесь, что интерфейс командной строки Azure уже установлен и указан в пути.</span><span class="sxs-lookup"><span data-stu-id="d1e77-287">Before you use this helper script, ensure that you already have Azure command-line interface (CLI) installed, and it is in your path.</span></span> <span data-ttu-id="d1e77-288">Убедитесь, что скрипт имеет разрешения на выполнение, запустив `chmod +x cert_helper.py` после скачивания.</span><span class="sxs-lookup"><span data-stu-id="d1e77-288">Make sure that the script has permissions to execute by running `chmod +x cert_helper.py` after downloading it.</span></span> <span data-ttu-id="d1e77-289">Первым делом войдите в учетную запись Azure с помощью команды `azure login` интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="d1e77-289">The first step is to sign in to your Azure account by using CLI with the `azure login` command.</span></span> <span data-ttu-id="d1e77-290">Войдя в учетную запись Azure, используйте вспомогательный сценарий, передав ему подписанный сертификат ЦС, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="d1e77-290">After signing in to your Azure account, use the helper script with your CA signed certificate, as the following command shows:</span></span>

```sh
./cert_helper.py [-h] CERT_TYPE [-ifile INPUT_CERT_FILE] [-sub SUBSCRIPTION_ID] [-rgname RESOURCE_GROUP_NAME] [-kv KEY_VAULT_NAME] [-sname CERTIFICATE_NAME] [-l LOCATION] [-p PASSWORD]
```

<span data-ttu-id="d1e77-291">Параметр -ifile позволяет загрузить начальные данные из PFX-файла или PEM-файла с указанием соответствующего типа сертификата (pfx, pem или ss, если это самозаверяющий сертификат).</span><span class="sxs-lookup"><span data-stu-id="d1e77-291">The -ifile parameter can take a .pfx file or a .pem file as input, with the certificate type (pfx or pem, or ss if it is a self-signed certificate).</span></span>
<span data-ttu-id="d1e77-292">Параметр -h позволяет вывести текст справки.</span><span class="sxs-lookup"><span data-stu-id="d1e77-292">The parameter -h prints out the help text.</span></span>


<span data-ttu-id="d1e77-293">Эта команда возвращает следующие три строки выходных данных:</span><span class="sxs-lookup"><span data-stu-id="d1e77-293">This command returns the following three strings as the output:</span></span>

* <span data-ttu-id="d1e77-294">SourceVaultID — идентификатор новой группы ресурсов (KeyVault ResourceGroup), которая создана для вас;</span><span class="sxs-lookup"><span data-stu-id="d1e77-294">SourceVaultID, which is the ID for the new KeyVault ResourceGroup it created for you</span></span>
* <span data-ttu-id="d1e77-295">CertificateUrl — адрес для доступа к сертификату;</span><span class="sxs-lookup"><span data-stu-id="d1e77-295">CertificateUrl for accessing the certificate</span></span>
* <span data-ttu-id="d1e77-296">CertificateThumbprint — используется для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="d1e77-296">CertificateThumbprint, which is used for authentication</span></span>

<span data-ttu-id="d1e77-297">Ниже представлен пример использования этой команды:</span><span class="sxs-lookup"><span data-stu-id="d1e77-297">The following example shows how to use the command:</span></span>

```sh
./cert_helper.py pfx -sub "fffffff-ffff-ffff-ffff-ffffffffffff"  -rgname "mykvrg" -kv "mykevname" -ifile "/home/test/cert.pfx" -sname "mycert" -l "East US" -p "pfxtest"
```
<span data-ttu-id="d1e77-298">Представленная выше команда вернет эти три строки:</span><span class="sxs-lookup"><span data-stu-id="d1e77-298">Executing the preceding command gives you the three strings as follows:</span></span>

```sh
SourceVault: /subscriptions/fffffff-ffff-ffff-ffff-ffffffffffff/resourceGroups/mykvrg/providers/Microsoft.KeyVault/vaults/mykvname
CertificateUrl: https://myvault.vault.azure.net/secrets/mycert/00000000000000000000000000000000
CertificateThumbprint: 0xfffffffffffffffffffffffffffffffffffffffff
```

<span data-ttu-id="d1e77-299">Имя субъекта сертификата должно совпадать с доменным именем, которое используется для обращения к кластеру Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d1e77-299">The certificate's subject name must match the domain that you use to access the Service Fabric cluster.</span></span> <span data-ttu-id="d1e77-300">Это необходимо, чтобы предоставить SSL-протокол конечным точкам управления HTTPS в кластере и Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="d1e77-300">This match is required to provide an SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="d1e77-301">Не удается получить SSL-сертификат из ЦС для домена `.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="d1e77-301">You cannot obtain an SSL certificate from a CA for the `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="d1e77-302">Необходимо получить имя личного домена для кластера.</span><span class="sxs-lookup"><span data-stu-id="d1e77-302">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="d1e77-303">При запросе сертификата из ЦС имя субъекта сертификата должно совпадать с именем личного домена, используемого для кластера.</span><span class="sxs-lookup"><span data-stu-id="d1e77-303">When you request a certificate from a CA, the certificate's subject name must match the custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="d1e77-304">Эти имена субъектов являются записями, которые необходимы для создания безопасного кластера Service Fabric (без Azure AD), как описано в разделе [Настройка параметров шаблона Resource Manager](#configure-arm).</span><span class="sxs-lookup"><span data-stu-id="d1e77-304">These subject names are the entries you need to create a secure Service Fabric cluster (without Azure AD), as described at [Configure Resource Manager template parameters](#configure-arm).</span></span> <span data-ttu-id="d1e77-305">Инструкции по подключению к безопасному кластеру см. в статье [Безопасное подключение к кластеру](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="d1e77-305">You can connect to the secure cluster by following the instructions for [authenticating client access to a cluster](service-fabric-connect-to-secure-cluster.md).</span></span> <span data-ttu-id="d1e77-306">Кластеры Linux предварительной версии не поддерживают аутентификацию Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d1e77-306">Linux preview clusters do not support Azure AD authentication.</span></span> <span data-ttu-id="d1e77-307">Можно назначить роли администратора и клиента, как описано в разделе [Назначение ролей пользователям](#assign-roles).</span><span class="sxs-lookup"><span data-stu-id="d1e77-307">You can assign admin and client roles as described in the [Assign roles to users](#assign-roles) section.</span></span> <span data-ttu-id="d1e77-308">При указании роли администратора и клиента для предварительной версии кластера Linux нужно предоставить отпечатки сертификатов для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="d1e77-308">When you specify admin and client roles for a Linux preview cluster, you have to provide certificate thumbprints for authentication.</span></span> <span data-ttu-id="d1e77-309">(Отсутствует имя получателя, так как в этом предварительном выпуске не выполняется цепочка проверки или отзыва.)</span><span class="sxs-lookup"><span data-stu-id="d1e77-309">(You do not provide the subject name, because no chain validation or revocation is being performed in this preview release.)</span></span>

<span data-ttu-id="d1e77-310">Если для тестирования нужно использовать самозаверяющий сертификат, можно использовать тот же сценарий для его создания.</span><span class="sxs-lookup"><span data-stu-id="d1e77-310">If you want to use a self-signed certificate for testing, you can use the same script to generate one.</span></span> <span data-ttu-id="d1e77-311">Затем можно передать сертификат в хранилище ключей, указав флаг `ss` вместо указания пути и имени сертификата.</span><span class="sxs-lookup"><span data-stu-id="d1e77-311">You can then upload the certificate to your key vault by providing the flag `ss` instead of providing the certificate path and certificate name.</span></span> <span data-ttu-id="d1e77-312">Вот пример команды для создания и передачи самозаверяющего сертификата:</span><span class="sxs-lookup"><span data-stu-id="d1e77-312">For example, see the following command for creating and uploading a self-signed certificate:</span></span>

```sh
./cert_helper.py ss -rgname "mykvrg" -sub "fffffff-ffff-ffff-ffff-ffffffffffff" -kv "mykevname"   -sname "mycert" -l "East US" -p "selftest" -subj "mytest.eastus.cloudapp.net"
```
<span data-ttu-id="d1e77-313">Эта команда возвращает те же три строки: SourceVault, CertificateUrl и CertificateThumbprint.</span><span class="sxs-lookup"><span data-stu-id="d1e77-313">This command returns the same three strings: SourceVault, CertificateUrl, and CertificateThumbprint.</span></span> <span data-ttu-id="d1e77-314">Затем эти строки можно использовать для создания безопасного кластера Linux и расположения для размещения самозаверяющего сертификата.</span><span class="sxs-lookup"><span data-stu-id="d1e77-314">You can then use the strings to create both a secure Linux cluster and a location where the self-signed certificate is placed.</span></span> <span data-ttu-id="d1e77-315">Самозаверяющий сертификат потребуется для подключения к кластеру.</span><span class="sxs-lookup"><span data-stu-id="d1e77-315">You need the self-signed certificate to connect to the cluster.</span></span> <span data-ttu-id="d1e77-316">Инструкции по подключению к безопасному кластеру см. в статье [Безопасное подключение к кластеру](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="d1e77-316">You can connect to the secure cluster by following the instructions for [authenticating client access to a cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="d1e77-317">Имя субъекта сертификата должно совпадать с доменным именем, которое используется для обращения к кластеру Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d1e77-317">The certificate's subject name must match the domain that you use to access the Service Fabric cluster.</span></span> <span data-ttu-id="d1e77-318">Это необходимо, чтобы предоставить SSL-протокол конечным точкам управления HTTPS в кластере и Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="d1e77-318">This match is required to provide an SSL for the cluster's HTTPS management endpoints and Service Fabric Explorer.</span></span> <span data-ttu-id="d1e77-319">Не удается получить SSL-сертификат из ЦС для домена `.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="d1e77-319">You cannot obtain an SSL certificate from a CA for the `.cloudapp.azure.com` domain.</span></span> <span data-ttu-id="d1e77-320">Необходимо получить имя личного домена для кластера.</span><span class="sxs-lookup"><span data-stu-id="d1e77-320">You must obtain a custom domain name for your cluster.</span></span> <span data-ttu-id="d1e77-321">При запросе сертификата из ЦС имя субъекта сертификата должно совпадать с именем личного домена, используемого для кластера.</span><span class="sxs-lookup"><span data-stu-id="d1e77-321">When you request a certificate from a CA, the certificate's subject name must match the custom domain name that you use for your cluster.</span></span>

<span data-ttu-id="d1e77-322">Параметры можно заполнить данными из вспомогательного сценария на портале Azure, как описано в разделе [Создание кластера на портале Azure](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="d1e77-322">You can fill the parameters from the helper script in the Azure portal, as described in the [Create a cluster in the Azure portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal) section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1e77-323">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d1e77-323">Next steps</span></span>
<span data-ttu-id="d1e77-324">На этом этапе у вас имеется защищенный кластер с Azure Active Directory для аутентификации управления.</span><span class="sxs-lookup"><span data-stu-id="d1e77-324">At this point, you have a secure cluster with Azure Active Directory providing management authentication.</span></span> <span data-ttu-id="d1e77-325">Далее [подключитесь к этому кластеру](service-fabric-connect-to-secure-cluster.md) и узнайте, как [управлять секретами приложений](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="d1e77-325">Next, [connect to your cluster](service-fabric-connect-to-secure-cluster.md) and learn how to [manage application secrets](service-fabric-application-secret-management.md).</span></span>

## <a name="troubleshoot-setting-up-azure-active-directory-for-client-authentication"></a><span data-ttu-id="d1e77-326">Устранение неполадок с настройкой Azure Active Directory для проверки подлинности клиента</span><span class="sxs-lookup"><span data-stu-id="d1e77-326">Troubleshoot setting up Azure Active Directory for client authentication</span></span>
<span data-ttu-id="d1e77-327">Если при настройке Azure AD для аутентификации клиента возникли проблемы, возможные решения можно найти в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="d1e77-327">If you run into an issue while you're setting up Azure AD for client authentication, review the potential solutions in this section.</span></span>

### <a name="service-fabric-explorer-prompts-you-to-select-a-certificate"></a><span data-ttu-id="d1e77-328">Service Fabric Explorer предлагает выбрать сертификат</span><span class="sxs-lookup"><span data-stu-id="d1e77-328">Service Fabric Explorer prompts you to select a certificate</span></span>
#### <a name="problem"></a><span data-ttu-id="d1e77-329">Проблема</span><span class="sxs-lookup"><span data-stu-id="d1e77-329">Problem</span></span>
<span data-ttu-id="d1e77-330">После успешного входа в Azure AD в Service Fabric Explorer браузер отображает домашнюю страницу, но на экране отображается предложение выбрать сертификат.</span><span class="sxs-lookup"><span data-stu-id="d1e77-330">After you sign in successfully to Azure AD in Service Fabric Explorer, the browser returns to the home page but a message prompts you to select a certificate.</span></span>

![Диалоговое окно выбора сертификата в Service Fabric Explorer][sfx-select-certificate-dialog]

#### <a name="reason"></a><span data-ttu-id="d1e77-332">Причина</span><span class="sxs-lookup"><span data-stu-id="d1e77-332">Reason</span></span>
<span data-ttu-id="d1e77-333">Пользователю не назначена роль в приложении кластера Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d1e77-333">The user isn’t assigned a role in the Azure AD cluster application.</span></span> <span data-ttu-id="d1e77-334">Таким образом, аутентификация Azure AD в кластере Service Fabric завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="d1e77-334">Thus, Azure AD authentication fails on Service Fabric cluster.</span></span> <span data-ttu-id="d1e77-335">Service Fabric Explorer воспользуется проверкой подлинности на основе сертификата.</span><span class="sxs-lookup"><span data-stu-id="d1e77-335">Service Fabric Explorer falls back to certificate authentication.</span></span>

#### <a name="solution"></a><span data-ttu-id="d1e77-336">Решение</span><span class="sxs-lookup"><span data-stu-id="d1e77-336">Solution</span></span>
<span data-ttu-id="d1e77-337">Следуйте инструкциям по настройке Azure AD и назначению ролей пользователей.</span><span class="sxs-lookup"><span data-stu-id="d1e77-337">Follow the instructions for setting up Azure AD, and assign user roles.</span></span> <span data-ttu-id="d1e77-338">Кроме того, рекомендуется включить параметр "Для доступа к приложению требуется назначение пользователей", как делает сценарий `SetupApplications.ps1`.</span><span class="sxs-lookup"><span data-stu-id="d1e77-338">Also, we recommend that you turn on “User assignment required to access app,” as `SetupApplications.ps1` does.</span></span>

### <a name="connection-with-powershell-fails-with-an-error-the-specified-credentials-are-invalid"></a><span data-ttu-id="d1e77-339">Подключение с помощью PowerShell завершается ошибкой: "Указанные учетные данные недействительны".</span><span class="sxs-lookup"><span data-stu-id="d1e77-339">Connection with PowerShell fails with an error: "The specified credentials are invalid"</span></span>
#### <a name="problem"></a><span data-ttu-id="d1e77-340">Проблема</span><span class="sxs-lookup"><span data-stu-id="d1e77-340">Problem</span></span>
<span data-ttu-id="d1e77-341">После успешного входа в Azure AD при использовании PowerShell для подключения к кластеру с помощью режима безопасности AzureActiveDirectory возникла ошибка, подключение завершается с ошибкой: "Указанные учетные данные недействительны".</span><span class="sxs-lookup"><span data-stu-id="d1e77-341">When you use PowerShell to connect to the cluster by using “AzureActiveDirectory” security mode, after you sign in successfully to Azure AD, the connection fails with an error: "The specified credentials are invalid."</span></span>

#### <a name="solution"></a><span data-ttu-id="d1e77-342">Решение</span><span class="sxs-lookup"><span data-stu-id="d1e77-342">Solution</span></span>
<span data-ttu-id="d1e77-343">Решение этой проблемы такое же, как и в предыдущем случае.</span><span class="sxs-lookup"><span data-stu-id="d1e77-343">This solution is the same as the preceding one.</span></span>

### <a name="service-fabric-explorer-returns-a-failure-when-you-sign-in-aadsts50011"></a><span data-ttu-id="d1e77-344">Service Fabric Explorer при входе возвращает ошибку "AADSTS50011"</span><span class="sxs-lookup"><span data-stu-id="d1e77-344">Service Fabric Explorer returns a failure when you sign in: "AADSTS50011"</span></span>
#### <a name="problem"></a><span data-ttu-id="d1e77-345">Проблема</span><span class="sxs-lookup"><span data-stu-id="d1e77-345">Problem</span></span>
<span data-ttu-id="d1e77-346">При попытке входа на страницу Azure AD в Service Fabric Explorer выдается ошибка: "AADSTS50011: адрес ответа &lt;URL-адрес&gt; не совпадает с адресами ответа, настроенными для приложения: &lt;guid&gt;".</span><span class="sxs-lookup"><span data-stu-id="d1e77-346">When you try to sign in to Azure AD in Service Fabric Explorer, the page returns a failure: "AADSTS50011: The reply address &lt;url&gt; does not match the reply addresses configured for the application: &lt;guid&gt;."</span></span>

![Несовпадение адреса ответа в Service Fabric Explorer][sfx-reply-address-not-match]

#### <a name="reason"></a><span data-ttu-id="d1e77-348">Причина</span><span class="sxs-lookup"><span data-stu-id="d1e77-348">Reason</span></span>
<span data-ttu-id="d1e77-349">Приложение кластера (веб-приложение), представляющее Service Fabric Explorer, пытается выполнить аутентификацию в Azure AD и в составе запроса предоставляет URL-адрес ответа для перенаправления.</span><span class="sxs-lookup"><span data-stu-id="d1e77-349">The cluster (web) application that represents Service Fabric Explorer attempts to authenticate against Azure AD, and as part of the request it provides the redirect return URL.</span></span> <span data-ttu-id="d1e77-350">URL-адрес не указан в списке **URL-АДРЕС ОТВЕТА** приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d1e77-350">But the URL is not listed in the Azure AD application **REPLY URL** list.</span></span>

#### <a name="solution"></a><span data-ttu-id="d1e77-351">Решение</span><span class="sxs-lookup"><span data-stu-id="d1e77-351">Solution</span></span>
<span data-ttu-id="d1e77-352">Добавьте URL-адрес Service Fabric Explorer в список **URL-АДРЕСОВ ОТВЕТА** на вкладке **Настройки** приложения кластера (веб-приложения) или замените один из элементов в списке.</span><span class="sxs-lookup"><span data-stu-id="d1e77-352">On the **Configure** tab of the cluster (web) application, add the URL of Service Fabric Explorer to the **REPLY URL** list or replace one of the items in the list.</span></span> <span data-ttu-id="d1e77-353">После завершения сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="d1e77-353">When you have finished, save your change.</span></span>

![URL-адрес ответа веб-приложения][web-application-reply-url]

### <a name="connect-the-cluster-by-using-azure-ad-authentication-via-powershell"></a><span data-ttu-id="d1e77-355">Подключение к кластеру с помощью аутентификации Azure AD с использованием PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1e77-355">Connect the cluster by using Azure AD authentication via PowerShell</span></span>
<span data-ttu-id="d1e77-356">Чтобы подключить кластер Service Fabric, воспользуйтесь следующим примером команды PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d1e77-356">To connect the Service Fabric cluster, use the following PowerShell command example:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <endpoint> -KeepAliveIntervalInSec 10 -AzureActiveDirectory -ServerCertThumbprint <thumbprint>
```

<span data-ttu-id="d1e77-357">Дополнительные сведения о командлете Connect-ServiceFabricCluster см. в [этой статье](https://msdn.microsoft.com/library/mt125938.aspx).</span><span class="sxs-lookup"><span data-stu-id="d1e77-357">To learn about the Connect-ServiceFabricCluster cmdlet, see [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx).</span></span>

### <a name="can-i-reuse-the-same-azure-ad-tenant-in-multiple-clusters"></a><span data-ttu-id="d1e77-358">Можно ли повторно использовать один и тот же клиент Azure AD в нескольких кластерах?</span><span class="sxs-lookup"><span data-stu-id="d1e77-358">Can I reuse the same Azure AD tenant in multiple clusters?</span></span>
<span data-ttu-id="d1e77-359">Да.</span><span class="sxs-lookup"><span data-stu-id="d1e77-359">Yes.</span></span> <span data-ttu-id="d1e77-360">Не забудьте добавить URL-адрес Service Fabric Explorer в (веб-)приложение кластера.</span><span class="sxs-lookup"><span data-stu-id="d1e77-360">But remember to add the URL of Service Fabric Explorer to your cluster (web) application.</span></span> <span data-ttu-id="d1e77-361">В противном случае — Service Fabric Explorer не работает.</span><span class="sxs-lookup"><span data-stu-id="d1e77-361">Otherwise, Service Fabric Explorer doesn’t work.</span></span>

### <a name="why-do-i-still-need-a-server-certificate-while-azure-ad-is-enabled"></a><span data-ttu-id="d1e77-362">Почему мне все еще нужен сертификат сервера при включенном Azure AD?</span><span class="sxs-lookup"><span data-stu-id="d1e77-362">Why do I still need a server certificate while Azure AD is enabled?</span></span>
<span data-ttu-id="d1e77-363">FabricClient и FabricGateway выполняют взаимную аутентификацию.</span><span class="sxs-lookup"><span data-stu-id="d1e77-363">FabricClient and FabricGateway perform a mutual authentication.</span></span> <span data-ttu-id="d1e77-364">Во время аутентификации Azure AD интеграция Azure AD предоставляет удостоверение клиента серверу и для аутентификации сервера используется сертификат сервера.</span><span class="sxs-lookup"><span data-stu-id="d1e77-364">During Azure AD authentication, Azure AD integration provides a client identity to the server, and the server certificate is used to verify the server identity.</span></span> <span data-ttu-id="d1e77-365">Дополнительные сведения о сертификатах Service Fabric см. в разделе [Сертификаты X.509 и Service Fabric][x509-certificates-and-service-fabric].</span><span class="sxs-lookup"><span data-stu-id="d1e77-365">For more information about Service Fabric certificates, see [X.509 certificates and Service Fabric][x509-certificates-and-service-fabric].</span></span>

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

