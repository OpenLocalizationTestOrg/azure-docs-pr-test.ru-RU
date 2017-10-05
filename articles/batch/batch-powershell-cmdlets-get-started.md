---
title: "Приступая к работе с модулем PowerShell пакетной службы Azure | Документация Майкрософт"
description: "Краткое описание командлетов Azure PowerShell, используемых для управления ресурсами пакетной службы."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: f9ad62c5-27bf-4e6b-a5bf-c5f5914e6199
ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: powershell
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e33be6ed658e00250ea1e80cd7da4d348fb18296
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="manage-batch-resources-with-powershell-cmdlets"></a><span data-ttu-id="b6eef-103">Управление ресурсами пакетной службы с помощью командлетов PowerShell</span><span class="sxs-lookup"><span data-stu-id="b6eef-103">Manage Batch resources with PowerShell cmdlets</span></span>

<span data-ttu-id="b6eef-104">С помощью командлетов PowerShell пакетной службы Azure можно выполнять те же задачи, которые выполняются с помощью API-интерфейсов пакетной службы, портала Azure и интерфейса командной строки (CLI).</span><span class="sxs-lookup"><span data-stu-id="b6eef-104">With the Azure Batch PowerShell cmdlets, you can perform and script many of the same tasks you carry out with the Batch APIs, the Azure portal, and the Azure Command-Line Interface (CLI).</span></span> <span data-ttu-id="b6eef-105">Эта статья содержит краткие сведения о командлетах, используемых для управления учетными записями пакетной службы и работы с ее ресурсами, включая пулы, задания и задачи.</span><span class="sxs-lookup"><span data-stu-id="b6eef-105">This is a quick introduction to the cmdlets you can use to manage your Batch accounts and work with your Batch resources such as pools, jobs, and tasks.</span></span>

<span data-ttu-id="b6eef-106">Полный список командлетов пакетной службы Azure и их синтаксис см. в [этой справке](/powershell/module/azurerm.batch/#batch).</span><span class="sxs-lookup"><span data-stu-id="b6eef-106">For a complete list of Batch cmdlets and detailed cmdlet syntax, see the [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>

<span data-ttu-id="b6eef-107">В этой статье описаны командлеты Azure PowerShell 3.0.0.</span><span class="sxs-lookup"><span data-stu-id="b6eef-107">This article is based on cmdlets in Azure PowerShell version 3.0.0.</span></span> <span data-ttu-id="b6eef-108">Рекомендуется часто обновлять Azure PowerShell, чтобы пользоваться всеми преимуществами службы.</span><span class="sxs-lookup"><span data-stu-id="b6eef-108">We recommend that you update your Azure PowerShell frequently to take advantage of service updates and enhancements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6eef-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b6eef-109">Prerequisites</span></span>
<span data-ttu-id="b6eef-110">Чтобы управлять ресурсами пакетной службы с помощью Azure PowerShell, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b6eef-110">Perform the following operations to use Azure PowerShell to manage your Batch resources.</span></span>

* [<span data-ttu-id="b6eef-111">Установка и настройка Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b6eef-111">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* <span data-ttu-id="b6eef-112">Выполните командлет **Login-AzureRmAccount**, чтобы подключиться к своей подписке (командлеты пакетной службы Azure входят в состав модуля Azure Resource Manager):</span><span class="sxs-lookup"><span data-stu-id="b6eef-112">Run the **Login-AzureRmAccount** cmdlet to connect to your subscription (the Azure Batch cmdlets ship in the Azure Resource Manager module):</span></span>
  
    `Login-AzureRmAccount`
* <span data-ttu-id="b6eef-113">**Зарегистрируйте пространство имен поставщика пакетной службы.**</span><span class="sxs-lookup"><span data-stu-id="b6eef-113">**Register with the Batch provider namespace**.</span></span> <span data-ttu-id="b6eef-114">Эту операцию достаточно выполнить **раз для каждой подписки**.</span><span class="sxs-lookup"><span data-stu-id="b6eef-114">This operation only needs to be performed **once per subscription**.</span></span>
  
    `Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch`

## <a name="manage-batch-accounts-and-keys"></a><span data-ttu-id="b6eef-115">Управление учетными записями пакетной службы и ключами</span><span class="sxs-lookup"><span data-stu-id="b6eef-115">Manage Batch accounts and keys</span></span>
### <a name="create-a-batch-account"></a><span data-ttu-id="b6eef-116">Создание учетной записи Пакетной службы</span><span class="sxs-lookup"><span data-stu-id="b6eef-116">Create a Batch account</span></span>
<span data-ttu-id="b6eef-117">Командлет **New-AzureRmBatchAccount** создает учетную запись пакетной службы в указанной группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b6eef-117">**New-AzureRmBatchAccount** creates a Batch account in a specified resource group.</span></span> <span data-ttu-id="b6eef-118">Если у вас еще нет группы ресурсов, создайте ее, выполнив командлет [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="b6eef-118">If you don't already have a resource group, create one by running the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span> <span data-ttu-id="b6eef-119">Укажите один из регионов Azure в параметре **Location**, например Central US.</span><span class="sxs-lookup"><span data-stu-id="b6eef-119">Specify one of the Azure regions in the **Location** parameter, such as "Central US".</span></span> <span data-ttu-id="b6eef-120">Например:</span><span class="sxs-lookup"><span data-stu-id="b6eef-120">For example:</span></span>

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"

<span data-ttu-id="b6eef-121">Затем создайте учетную запись пакетной службы в группе ресурсов, указав имя учетной записи вместо <*account_name*>, а также расположение и имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b6eef-121">Then, create a Batch account in the resource group, specifying a name for the account in <*account_name*> and the location and name of your resource group.</span></span> <span data-ttu-id="b6eef-122">Создание учетной записи пакетной службы может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="b6eef-122">Creating the Batch account can take some time to complete.</span></span> <span data-ttu-id="b6eef-123">Например:</span><span class="sxs-lookup"><span data-stu-id="b6eef-123">For example:</span></span>

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName <res_group_name>

> [!NOTE]
> <span data-ttu-id="b6eef-124">Имя учетной записи пакетной службы должно быть уникальным для региона Azure группы ресурсов, содержать от 3 до 24 символов и состоять только из строчных букв и цифр.</span><span class="sxs-lookup"><span data-stu-id="b6eef-124">The Batch account name must be unique to the Azure region for the resource group, contain between 3 and 24 characters, and use lowercase letters and numbers only.</span></span>
> 
> 

### <a name="get-account-access-keys"></a><span data-ttu-id="b6eef-125">Получение ключей доступа к учетной записи</span><span class="sxs-lookup"><span data-stu-id="b6eef-125">Get account access keys</span></span>
<span data-ttu-id="b6eef-126">**Get-AzureRmBatchAccountKeys** выводит клавиши доступа, связанные с учетной записью пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="b6eef-126">**Get-AzureRmBatchAccountKeys** shows the access keys associated with an Azure Batch account.</span></span> <span data-ttu-id="b6eef-127">Например, выполните следующую команду, чтобы получить первичные и вторичные ключи созданной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b6eef-127">For example, run the following to get the primary and secondary keys of the account you created.</span></span>

    $Account = Get-AzureRmBatchAccountKeys –AccountName <account_name>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey

### <a name="generate-a-new-access-key"></a><span data-ttu-id="b6eef-128">Создание нового ключа доступа</span><span class="sxs-lookup"><span data-stu-id="b6eef-128">Generate a new access key</span></span>
<span data-ttu-id="b6eef-129">**New-AzureRmBatchAccountKey** создает новый первичный или вторичный ключ учетной записи пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="b6eef-129">**New-AzureRmBatchAccountKey** generates a new primary or secondary account key for an Azure Batch account.</span></span> <span data-ttu-id="b6eef-130">Например, чтобы создать новый первичный ключ для учетной записи Пакетной службы, введите:</span><span class="sxs-lookup"><span data-stu-id="b6eef-130">For example, to generate a new primary key for your Batch account, type:</span></span>

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary

> [!NOTE]
> <span data-ttu-id="b6eef-131">Чтобы создать новый вторичный ключ, введите "Вторичный" в параметре **KeyType** .</span><span class="sxs-lookup"><span data-stu-id="b6eef-131">To generate a new secondary key, specify "Secondary" for the **KeyType** parameter.</span></span> <span data-ttu-id="b6eef-132">Повторно создавать первичный и вторичный ключи нужно отдельно.</span><span class="sxs-lookup"><span data-stu-id="b6eef-132">You have to regenerate the primary and secondary keys separately.</span></span>
> 
> 

### <a name="delete-a-batch-account"></a><span data-ttu-id="b6eef-133">Удаление учетной записи Пакетной службы</span><span class="sxs-lookup"><span data-stu-id="b6eef-133">Delete a Batch account</span></span>
<span data-ttu-id="b6eef-134">**Remove-AzureRmBatchAccount** удаляет учетную запись пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="b6eef-134">**Remove-AzureRmBatchAccount** deletes a Batch account.</span></span> <span data-ttu-id="b6eef-135">Например:</span><span class="sxs-lookup"><span data-stu-id="b6eef-135">For example:</span></span>

    Remove-AzureRmBatchAccount -AccountName <account_name>

<span data-ttu-id="b6eef-136">При появлении запроса на удаление учетной записи подтвердите удаление.</span><span class="sxs-lookup"><span data-stu-id="b6eef-136">When prompted, confirm you want to remove the account.</span></span> <span data-ttu-id="b6eef-137">Удаление учетной записи может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="b6eef-137">Account removal can take some time to complete.</span></span>

## <a name="create-a-batchaccountcontext-object"></a><span data-ttu-id="b6eef-138">Создание объекта BatchAccountContext</span><span class="sxs-lookup"><span data-stu-id="b6eef-138">Create a BatchAccountContext object</span></span>
<span data-ttu-id="b6eef-139">Чтобы выполнить проверки подлинности с помощью командлетов PowerShell пакетной службы во время создания пулов, заданий, задач и других ресурсов, а также управления ими, вам необходимо сначала создать объект BatchAccountContext для хранения ключей и имени учетной записи.</span><span class="sxs-lookup"><span data-stu-id="b6eef-139">To authenticate using the Batch PowerShell cmdlets when you create and manage Batch pools, jobs, tasks, and other resources, first create a BatchAccountContext object to store your account name and keys:</span></span>

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

<span data-ttu-id="b6eef-140">Передайте объект BatchAccountContext в командлеты, которые используют параметр **BatchContext** .</span><span class="sxs-lookup"><span data-stu-id="b6eef-140">You pass the BatchAccountContext object into cmdlets that use the **BatchContext** parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="b6eef-141">По умолчанию первичный ключ учетной записи используется для проверки подлинности, но вы можете явно выбрать ключ, который нужно использовать, изменив свойство **KeyInUse** объекта BatchAccountContext: `$context.KeyInUse = "Secondary"`.</span><span class="sxs-lookup"><span data-stu-id="b6eef-141">By default, the account's primary key is used for authentication, but you can explicitly select the key to use by changing your BatchAccountContext object’s **KeyInUse** property: `$context.KeyInUse = "Secondary"`.</span></span>
> 
> 

## <a name="create-and-modify-batch-resources"></a><span data-ttu-id="b6eef-142">Создание и изменение ресурсов пакетной службы</span><span class="sxs-lookup"><span data-stu-id="b6eef-142">Create and modify Batch resources</span></span>
<span data-ttu-id="b6eef-143">Чтобы создать ресурсы в учетной записи пакетной службы, используйте командлеты **New-AzureBatchPool**, **New-AzureBatchJob** и **New-AzureBatchTask**.</span><span class="sxs-lookup"><span data-stu-id="b6eef-143">Use cmdlets such as **New-AzureBatchPool**, **New-AzureBatchJob**, and **New-AzureBatchTask** to create resources under a Batch account.</span></span> <span data-ttu-id="b6eef-144">Чтобы обновить свойства ресурсов в учетной записи пакетной службы, используйте соответствующие командлеты **Get-** и **Set-**, а чтобы удалить ресурсы — командлет **Remove-**.</span><span class="sxs-lookup"><span data-stu-id="b6eef-144">There are corresponding **Get-** and **Set-** cmdlets to update the properties of existing resources, and  **Remove-** cmdlets to remove resources under a Batch account.</span></span>

<span data-ttu-id="b6eef-145">При использовании этих командлетов вам нужно не только передать объект BatchContext, но также создать или передать объекты, которые содержат параметры с подробными настройками ресурсов, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="b6eef-145">When using many of these cmdlets, in addition to passing a BatchContext object, you need to create or pass objects that contain detailed resource settings, as shown in the following example.</span></span> <span data-ttu-id="b6eef-146">Дополнительные примеры доступны в справочных материалах по каждому командлету.</span><span class="sxs-lookup"><span data-stu-id="b6eef-146">See the detailed help for each cmdlet for additional examples.</span></span>

### <a name="create-a-batch-pool"></a><span data-ttu-id="b6eef-147">Создание пула пакетной службы</span><span class="sxs-lookup"><span data-stu-id="b6eef-147">Create a Batch pool</span></span>
<span data-ttu-id="b6eef-148">Создавая или обновляя пул пакетной службы, вам нужно выбрать конфигурацию облачной службы или виртуальной машины для операционной системы на вычислительных узлах (см. [обзор функций пакетной службы](batch-api-basics.md#pool)).</span><span class="sxs-lookup"><span data-stu-id="b6eef-148">When creating or updating a Batch pool, you select either the cloud service configuration or the virtual machine configuration for the operating system on the compute nodes (see [Batch feature overview](batch-api-basics.md#pool)).</span></span> <span data-ttu-id="b6eef-149">Если вы указываете конфигурацию облачной службы, образы вычислительных узлов будут созданы на основе одного из [выпуска гостевых ОС Azure](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span><span class="sxs-lookup"><span data-stu-id="b6eef-149">If you specify the cloud service configuration, your compute nodes are imaged with one of the [Azure Guest OS releases](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span></span> <span data-ttu-id="b6eef-150">Если вы указываете конфигурацию виртуальной машины, можно выбрать один из поддерживаемых образов виртуальных машин Linux или Windows, доступных в [магазине виртуальных машин Azure Marketplace][vm_marketplace], или предоставить настраиваемый образ, подготовленный вами.</span><span class="sxs-lookup"><span data-stu-id="b6eef-150">If you specify the virtual machine configuration, you can either specify one of the supported Linux or Windows VM images listed in the [Azure Virtual Machines Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span>

<span data-ttu-id="b6eef-151">При выполнении командлета **New-AzureBatchPool** передайте параметры операционной системы в объекте PSCloudServiceConfiguration или PSVirtualMachineConfiguration.</span><span class="sxs-lookup"><span data-stu-id="b6eef-151">When you run **New-AzureBatchPool**, pass the operating system settings in a PSCloudServiceConfiguration or PSVirtualMachineConfiguration object.</span></span> <span data-ttu-id="b6eef-152">Например, следующий командлет создает новый пул пакетной службы с вычислительными узлами малого размера в конфигурации облачной службы. При этом образ создан с использованием последней версии операционной системы семейства 3 (Windows Server 2012).</span><span class="sxs-lookup"><span data-stu-id="b6eef-152">For example, the following cmdlet creates a new Batch pool with size Small compute nodes in the cloud service configuration, imaged with the latest operating system version of family 3 (Windows Server 2012).</span></span> <span data-ttu-id="b6eef-153">Здесь параметр **CloudServiceConfiguration** определяет переменную *$configuration* как объект PSCloudServiceConfiguration.</span><span class="sxs-lookup"><span data-stu-id="b6eef-153">Here, the **CloudServiceConfiguration** parameter specifies the *$configuration* variable as the PSCloudServiceConfiguration object.</span></span> <span data-ttu-id="b6eef-154">Параметр **BatchContext** определяет ранее заданную переменную *$context* как объект BatchAccountContext.</span><span class="sxs-lookup"><span data-stu-id="b6eef-154">The **BatchContext** parameter specifies a previously defined variable *$context* as the BatchAccountContext object.</span></span>

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(4,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

<span data-ttu-id="b6eef-155">Целевое число вычислительных узлов в новом пуле определяется по формуле автоматического масштабирования.</span><span class="sxs-lookup"><span data-stu-id="b6eef-155">The target number of compute nodes in the new pool is determined by an autoscaling formula.</span></span> <span data-ttu-id="b6eef-156">В этом случае формула выглядит так: **$TargetDedicated=4**. Это значит, что в пуле будет не более 4 вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="b6eef-156">In this case, the formula is simply **$TargetDedicated=4**, indicating the number of compute nodes in the pool is 4 at most.</span></span>

## <a name="query-for-pools-jobs-tasks-and-other-details"></a><span data-ttu-id="b6eef-157">Запрос на получение сведений о пулах, заданиях, задачах и другой информации</span><span class="sxs-lookup"><span data-stu-id="b6eef-157">Query for pools, jobs, tasks, and other details</span></span>
<span data-ttu-id="b6eef-158">Чтобы отправить запрос о сущностях, созданных в учетной записи пакетной службы, используйте командлеты **Get-AzureBatchPool**, **Get-AzureBatchJob** и **Get-AzureBatchTask**.</span><span class="sxs-lookup"><span data-stu-id="b6eef-158">Use cmdlets such as **Get-AzureBatchPool**, **Get-AzureBatchJob**, and **Get-AzureBatchTask** to query for entities created under a Batch account.</span></span>

### <a name="query-for-data"></a><span data-ttu-id="b6eef-159">Запрос данных</span><span class="sxs-lookup"><span data-stu-id="b6eef-159">Query for data</span></span>
<span data-ttu-id="b6eef-160">Например, для поиска пулов используйте **Get AzureBatchPools** .</span><span class="sxs-lookup"><span data-stu-id="b6eef-160">As an example, use **Get-AzureBatchPools** to find your pools.</span></span> <span data-ttu-id="b6eef-161">По умолчанию этот командлет опрашивает все пулы вашей учетной записи при условии, что вы уже сохранили объект BatchAccountContext в *$context*.</span><span class="sxs-lookup"><span data-stu-id="b6eef-161">By default this queries for all pools under your account, assuming you already stored the BatchAccountContext object in *$context*:</span></span>

    Get-AzureBatchPool -BatchContext $context

### <a name="use-an-odata-filter"></a><span data-ttu-id="b6eef-162">Использование фильтра OData</span><span class="sxs-lookup"><span data-stu-id="b6eef-162">Use an OData filter</span></span>
<span data-ttu-id="b6eef-163">Чтобы найти объекты, которые вас интересуют, установите фильтр OData в параметре **Фильтр** .</span><span class="sxs-lookup"><span data-stu-id="b6eef-163">You can supply an OData filter using the **Filter** parameter to find only the objects you’re interested in.</span></span> <span data-ttu-id="b6eef-164">Например, можно найти все пулы с идентификаторами, начинающимися с myPool:</span><span class="sxs-lookup"><span data-stu-id="b6eef-164">For example, you can find all pools with ids starting with “myPool”:</span></span>

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context

<span data-ttu-id="b6eef-165">Этот способ не такой гибкий, как использование "Where-Object" в локальном конвейере.</span><span class="sxs-lookup"><span data-stu-id="b6eef-165">This method is not as flexible as using “Where-Object” in a local pipeline.</span></span> <span data-ttu-id="b6eef-166">Но запрос отправляется непосредственно Пакетной службе, чтобы вся фильтрация выполнялась на стороне сервера, сохраняя пропускную способность Интернета.</span><span class="sxs-lookup"><span data-stu-id="b6eef-166">However, the query gets sent to the Batch service directly so that all filtering happens on the server side, saving Internet bandwidth.</span></span>

### <a name="use-the-id-parameter"></a><span data-ttu-id="b6eef-167">Используйте параметр Id</span><span class="sxs-lookup"><span data-stu-id="b6eef-167">Use the Id parameter</span></span>
<span data-ttu-id="b6eef-168">Альтернативой использования фильтра OData является использование параметра **Id** .</span><span class="sxs-lookup"><span data-stu-id="b6eef-168">An alternative to an OData filter is to use the **Id** parameter.</span></span> <span data-ttu-id="b6eef-169">Для запроса конкретного пула с идентификатором myPool сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="b6eef-169">To query for a specific pool with id "myPool":</span></span>

    Get-AzureBatchPool -Id "myPool" -BatchContext $context

<span data-ttu-id="b6eef-170">Параметр **Id** поддерживает поиск только полного идентификатора без подстановочных знаков или фильтров в стиле OData.</span><span class="sxs-lookup"><span data-stu-id="b6eef-170">The **Id** parameter supports only full-id search, not wildcards or OData-style filters.</span></span>

### <a name="use-the-maxcount-parameter"></a><span data-ttu-id="b6eef-171">Использование параметра MaxCount</span><span class="sxs-lookup"><span data-stu-id="b6eef-171">Use the MaxCount parameter</span></span>
<span data-ttu-id="b6eef-172">По умолчанию каждый командлет возвращает максимум 1000 объектов.</span><span class="sxs-lookup"><span data-stu-id="b6eef-172">By default, each cmdlet returns a maximum of 1000 objects.</span></span> <span data-ttu-id="b6eef-173">Если этот предел достигнут, уточните параметры фильтра, чтобы он возвращал меньшее количество объектов, или явно задайте максимальное значение с помощью параметра **MaxCount** .</span><span class="sxs-lookup"><span data-stu-id="b6eef-173">If you reach this limit, either refine your filter to bring back fewer objects, or explicitly set a maximum using the **MaxCount** parameter.</span></span> <span data-ttu-id="b6eef-174">Например:</span><span class="sxs-lookup"><span data-stu-id="b6eef-174">For example:</span></span>

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

<span data-ttu-id="b6eef-175">Чтобы удалить верхнюю границу, задайте **MaxCount** значение "0" или меньше.</span><span class="sxs-lookup"><span data-stu-id="b6eef-175">To remove the upper bound, set **MaxCount** to 0 or less.</span></span>

### <a name="use-the-powershell-pipeline"></a><span data-ttu-id="b6eef-176">Использование конвейера PowerShell</span><span class="sxs-lookup"><span data-stu-id="b6eef-176">Use the PowerShell pipeline</span></span>
<span data-ttu-id="b6eef-177">Командлеты Пакетной службы могут использовать конвейер PowerShell для передачи данных между командлетами.</span><span class="sxs-lookup"><span data-stu-id="b6eef-177">Batch cmdlets can leverage the PowerShell pipeline to send data between cmdlets.</span></span> <span data-ttu-id="b6eef-178">Вы получаете тот же результат, что и при указании параметра, но работа с несколькими сущностями упрощается.</span><span class="sxs-lookup"><span data-stu-id="b6eef-178">This has the same effect as specifying a parameter, but makes working with multiple entities easier.</span></span>

<span data-ttu-id="b6eef-179">Например, поиск и вывод всех задач в учетной записи:</span><span class="sxs-lookup"><span data-stu-id="b6eef-179">For example, find and display all tasks under your account:</span></span>

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context

<span data-ttu-id="b6eef-180">Перезапуск (перезагрузка) каждого вычислительного узла в пуле:</span><span class="sxs-lookup"><span data-stu-id="b6eef-180">Restart (reboot) every compute node in a pool:</span></span>

    Get-AzureBatchComputeNode -PoolId "myPool" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

## <a name="application-package-management"></a><span data-ttu-id="b6eef-181">Управление пакетами приложений</span><span class="sxs-lookup"><span data-stu-id="b6eef-181">Application package management</span></span>
<span data-ttu-id="b6eef-182">Пакеты приложений упрощают развертывание приложений на вычислительных узлах пулов.</span><span class="sxs-lookup"><span data-stu-id="b6eef-182">Application packages provide a simplified way to deploy applications to the compute nodes in your pools.</span></span> <span data-ttu-id="b6eef-183">С помощью командлетов PowerShell для пакетной службы можно передать пакеты приложений в учетной записи пакетной службы и управлять ими, а также развертывать версии пакетов в вычислительных узлах.</span><span class="sxs-lookup"><span data-stu-id="b6eef-183">With the Batch PowerShell cmdlets, you can upload and manage application packages in your Batch account, and deploy package versions to compute nodes.</span></span>

<span data-ttu-id="b6eef-184">**Создайте** приложение:</span><span class="sxs-lookup"><span data-stu-id="b6eef-184">**Create** an application:</span></span>

    New-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

<span data-ttu-id="b6eef-185">**Добавьте** пакет приложения:</span><span class="sxs-lookup"><span data-stu-id="b6eef-185">**Add** an application package:</span></span>

    New-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0" -Format zip -FilePath package001.zip

<span data-ttu-id="b6eef-186">Задайте для приложения **версию по умолчанию**:</span><span class="sxs-lookup"><span data-stu-id="b6eef-186">Set the **default version** for the application:</span></span>

    Set-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -DefaultVersion "1.0"

<span data-ttu-id="b6eef-187">**Выведите список** пакетов приложения:</span><span class="sxs-lookup"><span data-stu-id="b6eef-187">**List** an application's packages</span></span>

    $application = Get-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

    $application.ApplicationPackages

<span data-ttu-id="b6eef-188">**Удалите** пакет приложения:</span><span class="sxs-lookup"><span data-stu-id="b6eef-188">**Delete** an application package</span></span>

    Remove-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0"

<span data-ttu-id="b6eef-189">**Удалите** приложение:</span><span class="sxs-lookup"><span data-stu-id="b6eef-189">**Delete** an application</span></span>

    Remove-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

> [!NOTE]
> <span data-ttu-id="b6eef-190">Прежде чем удалять приложения, удалите все версии пакетов приложения.</span><span class="sxs-lookup"><span data-stu-id="b6eef-190">You must delete all of an application's application package versions before you delete the application.</span></span> <span data-ttu-id="b6eef-191">При попытке удалить приложение, в котором в настоящий момент содержатся пакеты приложения, появится ошибка о конфликте.</span><span class="sxs-lookup"><span data-stu-id="b6eef-191">You will receive a 'Conflict' error if you try to delete an application that currently has application packages.</span></span>
> 
> 

### <a name="deploy-an-application-package"></a><span data-ttu-id="b6eef-192">Развертывание пакета приложения</span><span class="sxs-lookup"><span data-stu-id="b6eef-192">Deploy an application package</span></span>
<span data-ttu-id="b6eef-193">Вы можете указать один или несколько пакетов приложений для развертывания при создании пула.</span><span class="sxs-lookup"><span data-stu-id="b6eef-193">You can specify one or more application packages for deployment when you create a pool.</span></span> <span data-ttu-id="b6eef-194">Когда вы указываете пакет во время создания пула, он развертывается на каждом из узлов, присоединяющихся к пулу.</span><span class="sxs-lookup"><span data-stu-id="b6eef-194">When you specify a package at pool creation time, it is deployed to each node as the node joins pool.</span></span> <span data-ttu-id="b6eef-195">Кроме того, развертывание пакетов выполняется при перезагрузке узла или пересоздании образа узла.</span><span class="sxs-lookup"><span data-stu-id="b6eef-195">Packages are also deployed when a node is rebooted or reimaged.</span></span>

<span data-ttu-id="b6eef-196">При создании пула укажите параметр `-ApplicationPackageReference`, чтобы развернуть пакет приложения для узлов во время их присоединения к пулу.</span><span class="sxs-lookup"><span data-stu-id="b6eef-196">Specify the `-ApplicationPackageReference` option when creating a pool to deploy an application package to the pool's nodes as they join the pool.</span></span> <span data-ttu-id="b6eef-197">Сначала создайте объект **PSApplicationPackageReference** и настройте для него идентификатор и версию пакета приложения, которую нужно развернуть в вычислительных узлах пула:</span><span class="sxs-lookup"><span data-stu-id="b6eef-197">First, create a **PSApplicationPackageReference** object, and configure it with the application Id and package version you want to deploy to the pool's compute nodes:</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "1.0"

<span data-ttu-id="b6eef-198">Теперь создайте пул и укажите ссылочный объект пакета в качестве аргумента в параметре `ApplicationPackageReferences`:</span><span class="sxs-lookup"><span data-stu-id="b6eef-198">Now create the pool, and specify the package reference object as the argument to the `ApplicationPackageReferences` option:</span></span>

    New-AzureBatchPool -Id "PoolWithAppPackage" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -BatchContext $context -ApplicationPackageReferences $appPackageReference

<span data-ttu-id="b6eef-199">Дополнительные сведения о пакетах приложений см. в статье [Развертывание приложений на вычислительных узлах с помощью пакетов приложений пакетной службы](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="b6eef-199">You can find more information on application packages in [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b6eef-200">Чтобы использовать пакеты приложений, вам сначала нужно [связать учетную запись хранения Azure](#linked-storage-account-autostorage) со своей учетной записью пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="b6eef-200">You must [link an Azure Storage account](#linked-storage-account-autostorage) to your Batch account to use application packages.</span></span>
> 
> 

### <a name="update-a-pools-application-packages"></a><span data-ttu-id="b6eef-201">Обновление пакетов приложений пула</span><span class="sxs-lookup"><span data-stu-id="b6eef-201">Update a pool's application packages</span></span>
<span data-ttu-id="b6eef-202">Чтобы обновить приложения, назначенные существующему пулу, сначала создайте объект PSApplicationPackageReference с нужными свойствами (идентификатор и версия пакета приложения):</span><span class="sxs-lookup"><span data-stu-id="b6eef-202">To update the applications assigned to an existing pool, first create a PSApplicationPackageReference object with the desired properties (application Id and package version):</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "2.0"

<span data-ttu-id="b6eef-203">Затем извлеките нужный пул из пакетной службы, очистите все существующие пакеты, добавьте ссылку на новый пакет и обновите пакетную службу с использованием новых параметров пула:</span><span class="sxs-lookup"><span data-stu-id="b6eef-203">Next, get the pool from Batch, clear out any existing packages, add our new package reference, and update the Batch service with the new pool settings:</span></span>

    $pool = Get-AzureBatchPool -BatchContext $context -Id "PoolWithAppPackage"

    $pool.ApplicationPackageReferences.Clear()

    $pool.ApplicationPackageReferences.Add($appPackageReference)

    Set-AzureBatchPool -BatchContext $context -Pool $pool

<span data-ttu-id="b6eef-204">Свойства пула в пакетной службе обновлены.</span><span class="sxs-lookup"><span data-stu-id="b6eef-204">You've now updated the pool's properties in the Batch service.</span></span> <span data-ttu-id="b6eef-205">Чтобы фактически развернуть новый пакет приложения на вычислительных узлах в пуле, необходимо перезапустить эти узлы или пересоздать образы для них.</span><span class="sxs-lookup"><span data-stu-id="b6eef-205">To actually deploy the new application package to compute nodes in the pool, however, you must restart or reimage those nodes.</span></span> <span data-ttu-id="b6eef-206">Чтобы перезапустить каждый узел в пуле, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b6eef-206">You can restart every node in a pool with this command:</span></span>

    Get-AzureBatchComputeNode -PoolId "PoolWithAppPackage" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

> [!TIP]
> <span data-ttu-id="b6eef-207">На вычислительных узлах в пуле можно развернуть несколько пакетов приложений.</span><span class="sxs-lookup"><span data-stu-id="b6eef-207">You can deploy multiple application packages to the compute nodes in a pool.</span></span> <span data-ttu-id="b6eef-208">Если нужно *добавить* пакет приложения, а не заменить развернутые пакеты, не указывайте строку `$pool.ApplicationPackageReferences.Clear()`, приведенную выше.</span><span class="sxs-lookup"><span data-stu-id="b6eef-208">If you'd like to *add* an application package instead of replacing the currently deployed packages, omit the `$pool.ApplicationPackageReferences.Clear()` line above.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b6eef-209">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b6eef-209">Next steps</span></span>
* <span data-ttu-id="b6eef-210">Подробные сведения о синтаксисе командлетов и их примеры см. в [справке по командлетам пакетной службы Azure](/powershell/module/azurerm.batch/#batch).</span><span class="sxs-lookup"><span data-stu-id="b6eef-210">For detailed cmdlet syntax and examples, see [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>
* <span data-ttu-id="b6eef-211">Дополнительные сведения о приложениях и пакетах приложений в пакетной службе см. в статье [Развертывание приложений на вычислительных узлах с помощью пакетов приложений пакетной службы](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="b6eef-211">For more information about applications and application packages in Batch, see [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md).</span></span>

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/