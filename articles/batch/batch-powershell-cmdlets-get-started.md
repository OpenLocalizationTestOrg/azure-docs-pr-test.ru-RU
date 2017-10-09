---
title: "aaaGet работы с PowerShell для пакета Azure | Документы Microsoft"
description: "Краткое введение toohello toomanage ресурсы пакета можно использовать командлеты Azure PowerShell."
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
ms.openlocfilehash: 3e4d12e9c1e52a5b2db2dd44346edda93b7ef92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-powershell-cmdlets"></a><span data-ttu-id="c53b4-103">Управление ресурсами пакетной службы с помощью командлетов PowerShell</span><span class="sxs-lookup"><span data-stu-id="c53b4-103">Manage Batch resources with PowerShell cmdlets</span></span>

<span data-ttu-id="c53b4-104">С hello командлеты PowerShell Azure пакета, можно выполнять и многие hello скрипт такие же задачи, выполняемые с hello пакетных API, hello портал Azure и hello Azure интерфейс командной строки (CLI).</span><span class="sxs-lookup"><span data-stu-id="c53b4-104">With hello Azure Batch PowerShell cmdlets, you can perform and script many of hello same tasks you carry out with hello Batch APIs, hello Azure portal, and hello Azure Command-Line Interface (CLI).</span></span> <span data-ttu-id="c53b4-105">Это краткое введение toohello командлеты можно использовать учетные записи пакетного toomanage и работать с ресурсами пакета пулов, заданий и задач.</span><span class="sxs-lookup"><span data-stu-id="c53b4-105">This is a quick introduction toohello cmdlets you can use toomanage your Batch accounts and work with your Batch resources such as pools, jobs, and tasks.</span></span>

<span data-ttu-id="c53b4-106">Полный список пакета командлетов и синтаксиса подробные командлета см hello [Справочник по командлетам Azure пакета](/powershell/module/azurerm.batch/#batch).</span><span class="sxs-lookup"><span data-stu-id="c53b4-106">For a complete list of Batch cmdlets and detailed cmdlet syntax, see hello [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>

<span data-ttu-id="c53b4-107">В этой статье описаны командлеты Azure PowerShell 3.0.0.</span><span class="sxs-lookup"><span data-stu-id="c53b4-107">This article is based on cmdlets in Azure PowerShell version 3.0.0.</span></span> <span data-ttu-id="c53b4-108">Рекомендуется обновить ваш Azure PowerShell часто tootake преимуществами службы обновления и улучшения.</span><span class="sxs-lookup"><span data-stu-id="c53b4-108">We recommend that you update your Azure PowerShell frequently tootake advantage of service updates and enhancements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c53b4-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c53b4-109">Prerequisites</span></span>
<span data-ttu-id="c53b4-110">Выполните следующие операции toouse Azure PowerShell toomanage hello ресурсы пакета.</span><span class="sxs-lookup"><span data-stu-id="c53b4-110">Perform hello following operations toouse Azure PowerShell toomanage your Batch resources.</span></span>

* [<span data-ttu-id="c53b4-111">Установка и настройка Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c53b4-111">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* <span data-ttu-id="c53b4-112">Запустите hello **AzureRmAccount входа** командлет tooconnect tooyour подписки (hello Azure пакетной отгрузки командлеты в модуле Azure Resource Manager hello):</span><span class="sxs-lookup"><span data-stu-id="c53b4-112">Run hello **Login-AzureRmAccount** cmdlet tooconnect tooyour subscription (hello Azure Batch cmdlets ship in hello Azure Resource Manager module):</span></span>
  
    `Login-AzureRmAccount`
* <span data-ttu-id="c53b4-113">**Зарегистрировать в пространство имен поставщика пакета hello**.</span><span class="sxs-lookup"><span data-stu-id="c53b4-113">**Register with hello Batch provider namespace**.</span></span> <span data-ttu-id="c53b4-114">Эта операция должна выполнить toobe **один раз для каждой подписки**.</span><span class="sxs-lookup"><span data-stu-id="c53b4-114">This operation only needs toobe performed **once per subscription**.</span></span>
  
    `Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch`

## <a name="manage-batch-accounts-and-keys"></a><span data-ttu-id="c53b4-115">Управление учетными записями пакетной службы и ключами</span><span class="sxs-lookup"><span data-stu-id="c53b4-115">Manage Batch accounts and keys</span></span>
### <a name="create-a-batch-account"></a><span data-ttu-id="c53b4-116">Создание учетной записи Пакетной службы</span><span class="sxs-lookup"><span data-stu-id="c53b4-116">Create a Batch account</span></span>
<span data-ttu-id="c53b4-117">Командлет **New-AzureRmBatchAccount** создает учетную запись пакетной службы в указанной группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c53b4-117">**New-AzureRmBatchAccount** creates a Batch account in a specified resource group.</span></span> <span data-ttu-id="c53b4-118">Если у вас еще нет группы ресурсов, создайте его, выполнив hello [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) командлета.</span><span class="sxs-lookup"><span data-stu-id="c53b4-118">If you don't already have a resource group, create one by running hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span> <span data-ttu-id="c53b4-119">Укажите один из hello Azure областей в hello **расположение** параметр, например «Центральной части США».</span><span class="sxs-lookup"><span data-stu-id="c53b4-119">Specify one of hello Azure regions in hello **Location** parameter, such as "Central US".</span></span> <span data-ttu-id="c53b4-120">Например:</span><span class="sxs-lookup"><span data-stu-id="c53b4-120">For example:</span></span>

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"

<span data-ttu-id="c53b4-121">Создайте учетную запись пакета в группе ресурсов hello, указав имя учетной записи hello в <*account_name*> расположением hello и имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c53b4-121">Then, create a Batch account in hello resource group, specifying a name for hello account in <*account_name*> and hello location and name of your resource group.</span></span> <span data-ttu-id="c53b4-122">Создание учетной записи пакетной hello может занять некоторое время toocomplete.</span><span class="sxs-lookup"><span data-stu-id="c53b4-122">Creating hello Batch account can take some time toocomplete.</span></span> <span data-ttu-id="c53b4-123">Например:</span><span class="sxs-lookup"><span data-stu-id="c53b4-123">For example:</span></span>

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName <res_group_name>

> [!NOTE]
> <span data-ttu-id="c53b4-124">Учетная запись пакетной Hello имя должно быть уникальным toohello регион Azure для группы ресурсов hello, содержать от 3 до 24 символов и использовать только строчные буквы и цифры.</span><span class="sxs-lookup"><span data-stu-id="c53b4-124">hello Batch account name must be unique toohello Azure region for hello resource group, contain between 3 and 24 characters, and use lowercase letters and numbers only.</span></span>
> 
> 

### <a name="get-account-access-keys"></a><span data-ttu-id="c53b4-125">Получение ключей доступа к учетной записи</span><span class="sxs-lookup"><span data-stu-id="c53b4-125">Get account access keys</span></span>
<span data-ttu-id="c53b4-126">**Get-AzureRmBatchAccountKeys** отображаются hello ключи доступа, связанном с учетной записью пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="c53b4-126">**Get-AzureRmBatchAccountKeys** shows hello access keys associated with an Azure Batch account.</span></span> <span data-ttu-id="c53b4-127">Например выполните следующие tooget hello первичный и вторичный ключи hello учетной записи, которую вы создали hello.</span><span class="sxs-lookup"><span data-stu-id="c53b4-127">For example, run hello following tooget hello primary and secondary keys of hello account you created.</span></span>

    $Account = Get-AzureRmBatchAccountKeys –AccountName <account_name>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey

### <a name="generate-a-new-access-key"></a><span data-ttu-id="c53b4-128">Создание нового ключа доступа</span><span class="sxs-lookup"><span data-stu-id="c53b4-128">Generate a new access key</span></span>
<span data-ttu-id="c53b4-129">**New-AzureRmBatchAccountKey** создает новый первичный или вторичный ключ учетной записи пакетной службы Azure.</span><span class="sxs-lookup"><span data-stu-id="c53b4-129">**New-AzureRmBatchAccountKey** generates a new primary or secondary account key for an Azure Batch account.</span></span> <span data-ttu-id="c53b4-130">В примере toogenerate новый первичный ключ для учетной записи пакета, введите:</span><span class="sxs-lookup"><span data-stu-id="c53b4-130">For example, toogenerate a new primary key for your Batch account, type:</span></span>

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary

> [!NOTE]
> <span data-ttu-id="c53b4-131">toogenerate новый вторичный ключ, укажите «Получатель» для hello **KeyType** параметра.</span><span class="sxs-lookup"><span data-stu-id="c53b4-131">toogenerate a new secondary key, specify "Secondary" for hello **KeyType** parameter.</span></span> <span data-ttu-id="c53b4-132">У вас tooregenerate hello первичный и вторичный ключи отдельно.</span><span class="sxs-lookup"><span data-stu-id="c53b4-132">You have tooregenerate hello primary and secondary keys separately.</span></span>
> 
> 

### <a name="delete-a-batch-account"></a><span data-ttu-id="c53b4-133">Удаление учетной записи Пакетной службы</span><span class="sxs-lookup"><span data-stu-id="c53b4-133">Delete a Batch account</span></span>
<span data-ttu-id="c53b4-134">**Remove-AzureRmBatchAccount** удаляет учетную запись пакетной службы.</span><span class="sxs-lookup"><span data-stu-id="c53b4-134">**Remove-AzureRmBatchAccount** deletes a Batch account.</span></span> <span data-ttu-id="c53b4-135">Например:</span><span class="sxs-lookup"><span data-stu-id="c53b4-135">For example:</span></span>

    Remove-AzureRmBatchAccount -AccountName <account_name>

<span data-ttu-id="c53b4-136">При появлении запроса подтвердите учетную запись tooremove hello.</span><span class="sxs-lookup"><span data-stu-id="c53b4-136">When prompted, confirm you want tooremove hello account.</span></span> <span data-ttu-id="c53b4-137">Удаление учетной записи может занять некоторое время toocomplete.</span><span class="sxs-lookup"><span data-stu-id="c53b4-137">Account removal can take some time toocomplete.</span></span>

## <a name="create-a-batchaccountcontext-object"></a><span data-ttu-id="c53b4-138">Создание объекта BatchAccountContext</span><span class="sxs-lookup"><span data-stu-id="c53b4-138">Create a BatchAccountContext object</span></span>
<span data-ttu-id="c53b4-139">с помощью tooauthenticate hello командлеты PowerShell пакета при создании и управлении пакета пулы, заданий, задач, и другие ресурсы, сначала создайте объект BatchAccountContext toostore имя учетной записи и ключи:</span><span class="sxs-lookup"><span data-stu-id="c53b4-139">tooauthenticate using hello Batch PowerShell cmdlets when you create and manage Batch pools, jobs, tasks, and other resources, first create a BatchAccountContext object toostore your account name and keys:</span></span>

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

<span data-ttu-id="c53b4-140">Можно передать объект BatchAccountContext hello в командлеты, используйте hello **BatchContext** параметра.</span><span class="sxs-lookup"><span data-stu-id="c53b4-140">You pass hello BatchAccountContext object into cmdlets that use hello **BatchContext** parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="c53b4-141">По умолчанию учетная запись hello первичный ключ используется для проверки подлинности, однако можно явно выбрать hello ключа toouse путем изменения объекта BatchAccountContext **KeyInUse** свойство: `$context.KeyInUse = "Secondary"`.</span><span class="sxs-lookup"><span data-stu-id="c53b4-141">By default, hello account's primary key is used for authentication, but you can explicitly select hello key toouse by changing your BatchAccountContext object’s **KeyInUse** property: `$context.KeyInUse = "Secondary"`.</span></span>
> 
> 

## <a name="create-and-modify-batch-resources"></a><span data-ttu-id="c53b4-142">Создание и изменение ресурсов пакетной службы</span><span class="sxs-lookup"><span data-stu-id="c53b4-142">Create and modify Batch resources</span></span>
<span data-ttu-id="c53b4-143">Использовать командлеты, такие как **New AzureBatchPool**, **New AzureBatchJob**, и **New AzureBatchTask** toocreate ресурсами под учетной записью пакета.</span><span class="sxs-lookup"><span data-stu-id="c53b4-143">Use cmdlets such as **New-AzureBatchPool**, **New-AzureBatchJob**, and **New-AzureBatchTask** toocreate resources under a Batch account.</span></span> <span data-ttu-id="c53b4-144">Существуют соответствующие **Get -** и **Set -** командлеты tooupdate hello свойств существующих ресурсов и **Remove -** командлеты tooremove ресурсы учетной записи пакета.</span><span class="sxs-lookup"><span data-stu-id="c53b4-144">There are corresponding **Get-** and **Set-** cmdlets tooupdate hello properties of existing resources, and  **Remove-** cmdlets tooremove resources under a Batch account.</span></span>

<span data-ttu-id="c53b4-145">При использовании многие из этих командлетов в дополнение toopassing BatchContext объекта, необходима toocreate или передать объекты, содержащие параметры подробные ресурсов, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="c53b4-145">When using many of these cmdlets, in addition toopassing a BatchContext object, you need toocreate or pass objects that contain detailed resource settings, as shown in hello following example.</span></span> <span data-ttu-id="c53b4-146">В разделе hello подробную справку по каждому командлету Дополнительные примеры.</span><span class="sxs-lookup"><span data-stu-id="c53b4-146">See hello detailed help for each cmdlet for additional examples.</span></span>

### <a name="create-a-batch-pool"></a><span data-ttu-id="c53b4-147">Создание пула пакетной службы</span><span class="sxs-lookup"><span data-stu-id="c53b4-147">Create a Batch pool</span></span>
<span data-ttu-id="c53b4-148">При создании или обновлении пула пакета, выберите конфигурацию hello облачной службы или конфигурации виртуальной машины hello для hello операционной системы на hello вычислительных узлов (в разделе [Обзор возможностей пакетной](batch-api-basics.md#pool)).</span><span class="sxs-lookup"><span data-stu-id="c53b4-148">When creating or updating a Batch pool, you select either hello cloud service configuration or hello virtual machine configuration for hello operating system on hello compute nodes (see [Batch feature overview](batch-api-basics.md#pool)).</span></span> <span data-ttu-id="c53b4-149">При указании hello конфигурацию облачной службы с одним hello записи образа вычислительных узлов [выпусками гостевых ОС Azure](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span><span class="sxs-lookup"><span data-stu-id="c53b4-149">If you specify hello cloud service configuration, your compute nodes are imaged with one of hello [Azure Guest OS releases](../cloud-services/cloud-services-guestos-update-matrix.md#releases).</span></span> <span data-ttu-id="c53b4-150">При указании hello конфигурации виртуальной машины, можно указать одно из hello поддерживается Linux или виртуальной Машины Windows изображений в hello [виртуальных машин Azure Marketplace][vm_marketplace], или предоставить пользовательский изображение, которое вы подготовили.</span><span class="sxs-lookup"><span data-stu-id="c53b4-150">If you specify hello virtual machine configuration, you can either specify one of hello supported Linux or Windows VM images listed in hello [Azure Virtual Machines Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span>

<span data-ttu-id="c53b4-151">При запуске **New AzureBatchPool**, передав объект PSCloudServiceConfiguration или PSVirtualMachineConfiguration hello параметры операционной системы.</span><span class="sxs-lookup"><span data-stu-id="c53b4-151">When you run **New-AzureBatchPool**, pass hello operating system settings in a PSCloudServiceConfiguration or PSVirtualMachineConfiguration object.</span></span> <span data-ttu-id="c53b4-152">Например hello следующий командлет создает новый пул пакета с небольших вычислительных узлов размера в hello конфигурацию облачной службы, восстановленных из образа с последней версией операционной системы hello семейства 3 (Windows Server 2012).</span><span class="sxs-lookup"><span data-stu-id="c53b4-152">For example, hello following cmdlet creates a new Batch pool with size Small compute nodes in hello cloud service configuration, imaged with hello latest operating system version of family 3 (Windows Server 2012).</span></span> <span data-ttu-id="c53b4-153">Здравствуйте, **CloudServiceConfiguration** указывает hello *$configuration* переменной как объект PSCloudServiceConfiguration hello.</span><span class="sxs-lookup"><span data-stu-id="c53b4-153">Here, hello **CloudServiceConfiguration** parameter specifies hello *$configuration* variable as hello PSCloudServiceConfiguration object.</span></span> <span data-ttu-id="c53b4-154">Hello **BatchContext** параметр указывает, ранее определенную переменную *$context* как объект BatchAccountContext hello.</span><span class="sxs-lookup"><span data-stu-id="c53b4-154">hello **BatchContext** parameter specifies a previously defined variable *$context* as hello BatchAccountContext object.</span></span>

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(4,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

<span data-ttu-id="c53b4-155">Hello целевое количество вычислительных узлов в новый пул hello определяется по формуле автоматического масштабирования.</span><span class="sxs-lookup"><span data-stu-id="c53b4-155">hello target number of compute nodes in hello new pool is determined by an autoscaling formula.</span></span> <span data-ttu-id="c53b4-156">В этом случае hello формула является просто **$TargetDedicated = 4**, количеству hello вычислительных узлов в пуле hello не более: 4.</span><span class="sxs-lookup"><span data-stu-id="c53b4-156">In this case, hello formula is simply **$TargetDedicated=4**, indicating hello number of compute nodes in hello pool is 4 at most.</span></span>

## <a name="query-for-pools-jobs-tasks-and-other-details"></a><span data-ttu-id="c53b4-157">Запрос на получение сведений о пулах, заданиях, задачах и другой информации</span><span class="sxs-lookup"><span data-stu-id="c53b4-157">Query for pools, jobs, tasks, and other details</span></span>
<span data-ttu-id="c53b4-158">Используйте командлеты, такие как **Get AzureBatchPool**, **Get AzureBatchJob**, и **Get AzureBatchTask** tooquery для сущности, созданные в учетной записи пакета.</span><span class="sxs-lookup"><span data-stu-id="c53b4-158">Use cmdlets such as **Get-AzureBatchPool**, **Get-AzureBatchJob**, and **Get-AzureBatchTask** tooquery for entities created under a Batch account.</span></span>

### <a name="query-for-data"></a><span data-ttu-id="c53b4-159">Запрос данных</span><span class="sxs-lookup"><span data-stu-id="c53b4-159">Query for data</span></span>
<span data-ttu-id="c53b4-160">Например, используйте **Get AzureBatchPools** toofind пулов.</span><span class="sxs-lookup"><span data-stu-id="c53b4-160">As an example, use **Get-AzureBatchPools** toofind your pools.</span></span> <span data-ttu-id="c53b4-161">По умолчанию это запросы для всех пулов в рамках учетной записи, при условии, что вы уже хранимые hello объекта BatchAccountContext в *$context*:</span><span class="sxs-lookup"><span data-stu-id="c53b4-161">By default this queries for all pools under your account, assuming you already stored hello BatchAccountContext object in *$context*:</span></span>

    Get-AzureBatchPool -BatchContext $context

### <a name="use-an-odata-filter"></a><span data-ttu-id="c53b4-162">Использование фильтра OData</span><span class="sxs-lookup"><span data-stu-id="c53b4-162">Use an OData filter</span></span>
<span data-ttu-id="c53b4-163">Можно указать фильтр OData с помощью hello **фильтра** toofind параметр hello только объекты, которые вас интересуют.</span><span class="sxs-lookup"><span data-stu-id="c53b4-163">You can supply an OData filter using hello **Filter** parameter toofind only hello objects you’re interested in.</span></span> <span data-ttu-id="c53b4-164">Например, можно найти все пулы с идентификаторами, начинающимися с myPool:</span><span class="sxs-lookup"><span data-stu-id="c53b4-164">For example, you can find all pools with ids starting with “myPool”:</span></span>

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context

<span data-ttu-id="c53b4-165">Этот способ не такой гибкий, как использование "Where-Object" в локальном конвейере.</span><span class="sxs-lookup"><span data-stu-id="c53b4-165">This method is not as flexible as using “Where-Object” in a local pipeline.</span></span> <span data-ttu-id="c53b4-166">Однако hello отправку запроса toohello пакетной службы непосредственно, чтобы все Фильтрация происходит на серверной стороне hello, экономя пропускную способность Интернета.</span><span class="sxs-lookup"><span data-stu-id="c53b4-166">However, hello query gets sent toohello Batch service directly so that all filtering happens on hello server side, saving Internet bandwidth.</span></span>

### <a name="use-hello-id-parameter"></a><span data-ttu-id="c53b4-167">Используйте параметр идентификатора hello</span><span class="sxs-lookup"><span data-stu-id="c53b4-167">Use hello Id parameter</span></span>
<span data-ttu-id="c53b4-168">Фильтр OData альтернативных tooan — toouse hello **идентификатор** параметра.</span><span class="sxs-lookup"><span data-stu-id="c53b4-168">An alternative tooan OData filter is toouse hello **Id** parameter.</span></span> <span data-ttu-id="c53b4-169">tooquery для конкретного пула с myPool «идентификатор»:</span><span class="sxs-lookup"><span data-stu-id="c53b4-169">tooquery for a specific pool with id "myPool":</span></span>

    Get-AzureBatchPool -Id "myPool" -BatchContext $context

<span data-ttu-id="c53b4-170">Hello **идентификатор** параметр поддерживает поиск полного кода, не подстановочные знаки или OData стиль фильтры.</span><span class="sxs-lookup"><span data-stu-id="c53b4-170">hello **Id** parameter supports only full-id search, not wildcards or OData-style filters.</span></span>

### <a name="use-hello-maxcount-parameter"></a><span data-ttu-id="c53b4-171">Использование параметра MaxCount hello</span><span class="sxs-lookup"><span data-stu-id="c53b4-171">Use hello MaxCount parameter</span></span>
<span data-ttu-id="c53b4-172">По умолчанию каждый командлет возвращает максимум 1000 объектов.</span><span class="sxs-lookup"><span data-stu-id="c53b4-172">By default, each cmdlet returns a maximum of 1000 objects.</span></span> <span data-ttu-id="c53b4-173">Если этот предел достигнут, уточнить ваш фильтр toobring обратно меньше объектов либо явно задать максимальное использование hello **MaxCount** параметра.</span><span class="sxs-lookup"><span data-stu-id="c53b4-173">If you reach this limit, either refine your filter toobring back fewer objects, or explicitly set a maximum using hello **MaxCount** parameter.</span></span> <span data-ttu-id="c53b4-174">Например:</span><span class="sxs-lookup"><span data-stu-id="c53b4-174">For example:</span></span>

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

<span data-ttu-id="c53b4-175">задать верхнюю границу hello tooremove, **MaxCount** too0 или меньше.</span><span class="sxs-lookup"><span data-stu-id="c53b4-175">tooremove hello upper bound, set **MaxCount** too0 or less.</span></span>

### <a name="use-hello-powershell-pipeline"></a><span data-ttu-id="c53b4-176">Использовать конвейер PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="c53b4-176">Use hello PowerShell pipeline</span></span>
<span data-ttu-id="c53b4-177">Командлеты пакета можно использовать hello PowerShell конвейера toosend данных между командлетами.</span><span class="sxs-lookup"><span data-stu-id="c53b4-177">Batch cmdlets can leverage hello PowerShell pipeline toosend data between cmdlets.</span></span> <span data-ttu-id="c53b4-178">Это имеет тот же эффект, что и при указании параметра, но упрощает работу с несколькими сущностями проще hello.</span><span class="sxs-lookup"><span data-stu-id="c53b4-178">This has hello same effect as specifying a parameter, but makes working with multiple entities easier.</span></span>

<span data-ttu-id="c53b4-179">Например, поиск и вывод всех задач в учетной записи:</span><span class="sxs-lookup"><span data-stu-id="c53b4-179">For example, find and display all tasks under your account:</span></span>

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context

<span data-ttu-id="c53b4-180">Перезапуск (перезагрузка) каждого вычислительного узла в пуле:</span><span class="sxs-lookup"><span data-stu-id="c53b4-180">Restart (reboot) every compute node in a pool:</span></span>

    Get-AzureBatchComputeNode -PoolId "myPool" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

## <a name="application-package-management"></a><span data-ttu-id="c53b4-181">Управление пакетами приложений</span><span class="sxs-lookup"><span data-stu-id="c53b4-181">Application package management</span></span>
<span data-ttu-id="c53b4-182">Пакеты приложений предоставляют упрощенный способ toohello приложений toodeploy вычислительных узлов в пулов.</span><span class="sxs-lookup"><span data-stu-id="c53b4-182">Application packages provide a simplified way toodeploy applications toohello compute nodes in your pools.</span></span> <span data-ttu-id="c53b4-183">Hello командлеты PowerShell для пакета можно отправить и управлять пакетами приложений в вашей учетной записи пакета и развертывание узлов toocompute версии пакета.</span><span class="sxs-lookup"><span data-stu-id="c53b4-183">With hello Batch PowerShell cmdlets, you can upload and manage application packages in your Batch account, and deploy package versions toocompute nodes.</span></span>

<span data-ttu-id="c53b4-184">**Создайте** приложение:</span><span class="sxs-lookup"><span data-stu-id="c53b4-184">**Create** an application:</span></span>

    New-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

<span data-ttu-id="c53b4-185">**Добавьте** пакет приложения:</span><span class="sxs-lookup"><span data-stu-id="c53b4-185">**Add** an application package:</span></span>

    New-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0" -Format zip -FilePath package001.zip

<span data-ttu-id="c53b4-186">Набор hello **версия по умолчанию** для приложения hello:</span><span class="sxs-lookup"><span data-stu-id="c53b4-186">Set hello **default version** for hello application:</span></span>

    Set-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -DefaultVersion "1.0"

<span data-ttu-id="c53b4-187">**Выведите список** пакетов приложения:</span><span class="sxs-lookup"><span data-stu-id="c53b4-187">**List** an application's packages</span></span>

    $application = Get-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

    $application.ApplicationPackages

<span data-ttu-id="c53b4-188">**Удалите** пакет приложения:</span><span class="sxs-lookup"><span data-stu-id="c53b4-188">**Delete** an application package</span></span>

    Remove-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0"

<span data-ttu-id="c53b4-189">**Удалите** приложение:</span><span class="sxs-lookup"><span data-stu-id="c53b4-189">**Delete** an application</span></span>

    Remove-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

> [!NOTE]
> <span data-ttu-id="c53b4-190">Все версии пакета приложения для приложения необходимо удалить перед удалением приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c53b4-190">You must delete all of an application's application package versions before you delete hello application.</span></span> <span data-ttu-id="c53b4-191">При попытке toodelete приложение, которое в настоящее время имеет пакетов приложений, вы получите ошибку «Конфликт».</span><span class="sxs-lookup"><span data-stu-id="c53b4-191">You will receive a 'Conflict' error if you try toodelete an application that currently has application packages.</span></span>
> 
> 

### <a name="deploy-an-application-package"></a><span data-ttu-id="c53b4-192">Развертывание пакета приложения</span><span class="sxs-lookup"><span data-stu-id="c53b4-192">Deploy an application package</span></span>
<span data-ttu-id="c53b4-193">Вы можете указать один или несколько пакетов приложений для развертывания при создании пула.</span><span class="sxs-lookup"><span data-stu-id="c53b4-193">You can specify one or more application packages for deployment when you create a pool.</span></span> <span data-ttu-id="c53b4-194">При указании пакета во время создания пула это развернутой tooeach узел в качестве пула соединений hello узла.</span><span class="sxs-lookup"><span data-stu-id="c53b4-194">When you specify a package at pool creation time, it is deployed tooeach node as hello node joins pool.</span></span> <span data-ttu-id="c53b4-195">Кроме того, развертывание пакетов выполняется при перезагрузке узла или пересоздании образа узла.</span><span class="sxs-lookup"><span data-stu-id="c53b4-195">Packages are also deployed when a node is rebooted or reimaged.</span></span>

<span data-ttu-id="c53b4-196">Укажите hello `-ApplicationPackageReference` параметр при создании пула приложений пакета toohello узлов toodeploy пул, как они присоединиться к пулу hello.</span><span class="sxs-lookup"><span data-stu-id="c53b4-196">Specify hello `-ApplicationPackageReference` option when creating a pool toodeploy an application package toohello pool's nodes as they join hello pool.</span></span> <span data-ttu-id="c53b4-197">Сначала создайте **PSApplicationPackageReference** и настройте его с hello идентификатор и пакета версии приложения необходимо toodeploy toohello пул вычислительных узлов:</span><span class="sxs-lookup"><span data-stu-id="c53b4-197">First, create a **PSApplicationPackageReference** object, and configure it with hello application Id and package version you want toodeploy toohello pool's compute nodes:</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "1.0"

<span data-ttu-id="c53b4-198">Теперь создайте пул hello и указать ссылку объекта hello пакета, как hello аргумент toohello `ApplicationPackageReferences` параметр:</span><span class="sxs-lookup"><span data-stu-id="c53b4-198">Now create hello pool, and specify hello package reference object as hello argument toohello `ApplicationPackageReferences` option:</span></span>

    New-AzureBatchPool -Id "PoolWithAppPackage" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -BatchContext $context -ApplicationPackageReferences $appPackageReference

<span data-ttu-id="c53b4-199">Можно найти дополнительные сведения о пакетах приложения в [развертывания приложений toocompute узлов с пакетами приложения пакета](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="c53b4-199">You can find more information on application packages in [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c53b4-200">Вы должны [связать учетную запись хранилища Azure](#linked-storage-account-autostorage) tooyour пакетной учетной записи toouse пакетов приложений.</span><span class="sxs-lookup"><span data-stu-id="c53b4-200">You must [link an Azure Storage account](#linked-storage-account-autostorage) tooyour Batch account toouse application packages.</span></span>
> 
> 

### <a name="update-a-pools-application-packages"></a><span data-ttu-id="c53b4-201">Обновление пакетов приложений пула</span><span class="sxs-lookup"><span data-stu-id="c53b4-201">Update a pool's application packages</span></span>
<span data-ttu-id="c53b4-202">tooupdate приложения hello, назначенные tooan существующий пул, сначала создайте объект PSApplicationPackageReference hello требуемого свойства (Id и пакета версии приложения):</span><span class="sxs-lookup"><span data-stu-id="c53b4-202">tooupdate hello applications assigned tooan existing pool, first create a PSApplicationPackageReference object with hello desired properties (application Id and package version):</span></span>

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "2.0"

<span data-ttu-id="c53b4-203">Затем получить пул hello из пакета, очистить все существующие пакеты, добавлять нашей новой ссылки на пакет и обновлять hello пакетная служба с новыми настройками пула hello:</span><span class="sxs-lookup"><span data-stu-id="c53b4-203">Next, get hello pool from Batch, clear out any existing packages, add our new package reference, and update hello Batch service with hello new pool settings:</span></span>

    $pool = Get-AzureBatchPool -BatchContext $context -Id "PoolWithAppPackage"

    $pool.ApplicationPackageReferences.Clear()

    $pool.ApplicationPackageReferences.Add($appPackageReference)

    Set-AzureBatchPool -BatchContext $context -Pool $pool

<span data-ttu-id="c53b4-204">Теперь вы обновили свойства пула hello в пакетной службе hello.</span><span class="sxs-lookup"><span data-stu-id="c53b4-204">You've now updated hello pool's properties in hello Batch service.</span></span> <span data-ttu-id="c53b4-205">tooactually развертывание hello новый пакет toocompute узлов приложения в пуле hello, тем не менее, необходимо перезапустить или повторного создания образа этих узлов.</span><span class="sxs-lookup"><span data-stu-id="c53b4-205">tooactually deploy hello new application package toocompute nodes in hello pool, however, you must restart or reimage those nodes.</span></span> <span data-ttu-id="c53b4-206">Чтобы перезапустить каждый узел в пуле, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c53b4-206">You can restart every node in a pool with this command:</span></span>

    Get-AzureBatchComputeNode -PoolId "PoolWithAppPackage" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

> [!TIP]
> <span data-ttu-id="c53b4-207">Можно развернуть несколько вычислительных узлов toohello приложения пакеты в пуле.</span><span class="sxs-lookup"><span data-stu-id="c53b4-207">You can deploy multiple application packages toohello compute nodes in a pool.</span></span> <span data-ttu-id="c53b4-208">Если вы хотите слишком*добавить* пакета приложения вместо замены hello развернутые пакеты, пропустите hello `$pool.ApplicationPackageReferences.Clear()` строку выше.</span><span class="sxs-lookup"><span data-stu-id="c53b4-208">If you'd like too*add* an application package instead of replacing hello currently deployed packages, omit hello `$pool.ApplicationPackageReferences.Clear()` line above.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c53b4-209">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c53b4-209">Next steps</span></span>
* <span data-ttu-id="c53b4-210">Подробные сведения о синтаксисе командлетов и их примеры см. в [справке по командлетам пакетной службы Azure](/powershell/module/azurerm.batch/#batch).</span><span class="sxs-lookup"><span data-stu-id="c53b4-210">For detailed cmdlet syntax and examples, see [Azure Batch cmdlet reference](/powershell/module/azurerm.batch/#batch).</span></span>
* <span data-ttu-id="c53b4-211">Дополнительные сведения о приложениях и пакеты приложений в пакете см. в разделе [развертывания приложений toocompute узлов с пакетами приложения пакета](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="c53b4-211">For more information about applications and application packages in Batch, see [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/