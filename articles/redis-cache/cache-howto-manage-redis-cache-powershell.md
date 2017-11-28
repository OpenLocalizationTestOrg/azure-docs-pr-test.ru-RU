---
title: "Кэш Redis для Azure с помощью Azure PowerShell aaaManage | Документы Microsoft"
description: "Узнайте, как tooperform административных задач для кэша Redis для Azure с помощью Azure PowerShell."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1136efe5-1e33-4d91-bb49-c8e2a6dca475
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: 1d526ce65c4bc05345cd6c3ff370211ed562cab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-redis-cache-with-azure-powershell"></a><span data-ttu-id="d9f1e-103">Управление кэшем Redis для Azure с использованием Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9f1e-103">Manage Azure Redis Cache with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d9f1e-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9f1e-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="d9f1e-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="d9f1e-105">Azure CLI</span></span>](cache-manage-cli.md)
> 
> 

<span data-ttu-id="d9f1e-106">В этом разделе показано, как tooperform общие задачи, такие как создание, обновление и масштабирования ваших экземпляров кэша Redis для Azure как tooregenerate клавиши доступа и как tooview сведения о ваших кэшей.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-106">This topic shows you how tooperform common tasks such as create, update, and scale your Azure Redis Cache instances, how tooregenerate access keys, and how tooview information about your caches.</span></span> <span data-ttu-id="d9f1e-107">См. полный список [командлетов PowerShell для работы с кэшем Redis для Azure](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span><span class="sxs-lookup"><span data-stu-id="d9f1e-107">For a complete list of Azure Redis Cache PowerShell cmdlets, see [Azure Redis Cache cmdlets](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="d9f1e-108">Дополнительные сведения о hello классической модели развертывания см. в разделе [диспетчера ресурсов Azure и классическое развертывание: Обзор модели развертывания и hello состояния ресурсов](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span><span class="sxs-lookup"><span data-stu-id="d9f1e-108">For more information about hello classic deployment model, see [Azure Resource Manager vs. classic deployment: Understand deployment models and hello state of your resources](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9f1e-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d9f1e-109">Prerequisites</span></span>
<span data-ttu-id="d9f1e-110">Если вы уже установили Azure PowerShell, необходимо использовать Azure PowerShell 1.0.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-110">If you have already installed Azure PowerShell, you must have Azure PowerShell version 1.0.0 or later.</span></span> <span data-ttu-id="d9f1e-111">Можно проверить версию hello Azure PowerShell, установленный с помощью этой команды в командной строке Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-111">You can check hello version of Azure PowerShell that you have installed with this command at hello Azure PowerShell command prompt.</span></span>

    Get-Module azure | format-table version


<span data-ttu-id="d9f1e-112">Во-первых необходимо войти в tooAzure с помощью этой команды.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-112">First, you must log in tooAzure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="d9f1e-113">Укажите адрес электронной почты hello учетную запись Azure и пароль в диалоговом окне приветствия вход в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-113">Specify hello email address of your Azure account and its password in hello Microsoft Azure sign-in dialog.</span></span>

<span data-ttu-id="d9f1e-114">Затем Если у вас несколько подписок Azure, следует записать tooset подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-114">Next, if you have multiple Azure subscriptions, you need tooset your Azure subscription.</span></span> <span data-ttu-id="d9f1e-115">toosee список ваши текущие подписки, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-115">toosee a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="d9f1e-116">toospecify подписка hello, запустите следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-116">toospecify hello subscription, run hello following command.</span></span> <span data-ttu-id="d9f1e-117">В следующем примере hello, — имя подписки hello `ContosoSubscription`.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-117">In hello following example, hello subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

<span data-ttu-id="d9f1e-118">Прежде чем использовать Windows PowerShell с помощью диспетчера ресурсов Azure, требуется hello следующее:</span><span class="sxs-lookup"><span data-stu-id="d9f1e-118">Before you can use Windows PowerShell with Azure Resource Manager, you need hello following:</span></span>

* <span data-ttu-id="d9f1e-119">Windows PowerShell версии 3.0 или 4.0.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-119">Windows PowerShell, Version 3.0 or 4.0.</span></span> <span data-ttu-id="d9f1e-120">toofind hello версии Windows PowerShell, введите:`$PSVersionTable` и проверьте значение hello `PSVersion` 3.0 или 4.0.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-120">toofind hello version of Windows PowerShell, type:`$PSVersionTable` and verify hello value of `PSVersion` is 3.0 or 4.0.</span></span> <span data-ttu-id="d9f1e-121">tooinstall совместимую версию в разделе [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) или [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span><span class="sxs-lookup"><span data-stu-id="d9f1e-121">tooinstall a compatible version, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

<span data-ttu-id="d9f1e-122">tooget подробную справку для любого командлета, отображаемые в этом учебнике, используйте командлет Get-Help hello.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-122">tooget detailed help for any cmdlet you see in this tutorial, use hello Get-Help cmdlet.</span></span>

    Get-Help <cmdlet-name> -Detailed

<span data-ttu-id="d9f1e-123">Например, tooget справку для hello `New-AzureRmRedisCache` командлета введите:</span><span class="sxs-lookup"><span data-stu-id="d9f1e-123">For example, tooget help for hello `New-AzureRmRedisCache` cmdlet, type:</span></span>

    Get-Help New-AzureRmRedisCache -Detailed

### <a name="how-tooconnect-tooother-clouds"></a><span data-ttu-id="d9f1e-124">Как tooconnect tooother облака</span><span class="sxs-lookup"><span data-stu-id="d9f1e-124">How tooconnect tooother clouds</span></span>
<span data-ttu-id="d9f1e-125">По умолчанию hello Azure — среды `AzureCloud`, которое представляет hello облако Azure как глобальный экземпляр.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-125">By default hello Azure environment is `AzureCloud`, which represents hello global Azure cloud instance.</span></span> <span data-ttu-id="d9f1e-126">другой экземпляр tooa tooconnect, используйте hello `Add-AzureRmAccount` с hello `-Environment` или -`EnvironmentName` переключатель командной строки с требуемой среде hello или имя среды.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-126">tooconnect tooa different instance, use hello `Add-AzureRmAccount` command with hello `-Environment` or -`EnvironmentName` command line switch with hello desired environment or environment name.</span></span>

<span data-ttu-id="d9f1e-127">Список доступных сред, запустите hello hello toosee `Get-AzureRmEnvironment` командлета.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-127">toosee hello list of available environments, run hello `Get-AzureRmEnvironment` cmdlet.</span></span>

### <a name="tooconnect-toohello-azure-government-cloud"></a><span data-ttu-id="d9f1e-128">tooconnect toohello облако Azure государственных организаций</span><span class="sxs-lookup"><span data-stu-id="d9f1e-128">tooconnect toohello Azure Government Cloud</span></span>
<span data-ttu-id="d9f1e-129">toohello tooconnect государственных облако Azure, выполните одну из следующих команд hello.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-129">tooconnect toohello Azure Government Cloud, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureUSGovernment

<span data-ttu-id="d9f1e-130">или</span><span class="sxs-lookup"><span data-stu-id="d9f1e-130">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureUSGovernment)

<span data-ttu-id="d9f1e-131">toocreate кэша в hello государственных облако Azure, используйте один из следующих элементов hello.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-131">toocreate a cache in hello Azure Government Cloud, use one of hello following locations.</span></span>

* <span data-ttu-id="d9f1e-132">Правительство штата Вирджиния</span><span class="sxs-lookup"><span data-stu-id="d9f1e-132">USGov Virginia</span></span>
* <span data-ttu-id="d9f1e-133">Правительство штата Айова</span><span class="sxs-lookup"><span data-stu-id="d9f1e-133">USGov Iowa</span></span>

<span data-ttu-id="d9f1e-134">Дополнительные сведения о hello государственных облако Azure. в разделе [Microsoft Azure для государственных](https://azure.microsoft.com/features/gov/) и [руководстве разработчика Microsoft Azure государственных](../azure-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="d9f1e-134">For more information about hello Azure Government Cloud, see [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) and [Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>

### <a name="tooconnect-toohello-azure-china-cloud"></a><span data-ttu-id="d9f1e-135">tooconnect toohello Китая облако Azure</span><span class="sxs-lookup"><span data-stu-id="d9f1e-135">tooconnect toohello Azure China Cloud</span></span>
<span data-ttu-id="d9f1e-136">toohello tooconnect облако Azure Китая, используйте один из следующих команд hello.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-136">tooconnect toohello Azure China Cloud, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureChinaCloud

<span data-ttu-id="d9f1e-137">или</span><span class="sxs-lookup"><span data-stu-id="d9f1e-137">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureChinaCloud)

<span data-ttu-id="d9f1e-138">toocreate кэша в облако Azure Китая, используйте один из следующих элементов hello hello.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-138">toocreate a cache in hello Azure China Cloud, use one of hello following locations.</span></span>

* <span data-ttu-id="d9f1e-139">Восток Китая</span><span class="sxs-lookup"><span data-stu-id="d9f1e-139">China East</span></span>
* <span data-ttu-id="d9f1e-140">Север Китая</span><span class="sxs-lookup"><span data-stu-id="d9f1e-140">China North</span></span>

<span data-ttu-id="d9f1e-141">Дополнительные сведения о hello облако Azure China. в разделе [AzureChinaCloud для Azure обслуживается 21Vianet в Китае](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="d9f1e-141">For more information about hello Azure China Cloud, see [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span>

### <a name="tooconnect-toomicrosoft-azure-germany"></a><span data-ttu-id="d9f1e-142">tooconnect tooMicrosoft Германия Azure</span><span class="sxs-lookup"><span data-stu-id="d9f1e-142">tooconnect tooMicrosoft Azure Germany</span></span>
<span data-ttu-id="d9f1e-143">tooMicrosoft tooconnect Германии Azure, выполните одну из следующих команд hello.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-143">tooconnect tooMicrosoft Azure Germany, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureGermanCloud


<span data-ttu-id="d9f1e-144">или</span><span class="sxs-lookup"><span data-stu-id="d9f1e-144">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureGermanCloud)

<span data-ttu-id="d9f1e-145">toocreate кэша в Германии Microsoft Azure, используйте одну из следующих ссылок hello.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-145">toocreate a cache in Microsoft Azure Germany, use one of hello following locations.</span></span>

* <span data-ttu-id="d9f1e-146">Центральная Германия</span><span class="sxs-lookup"><span data-stu-id="d9f1e-146">Germany Central</span></span>
* <span data-ttu-id="d9f1e-147">Северо-восточная Германия</span><span class="sxs-lookup"><span data-stu-id="d9f1e-147">Germany Northeast</span></span>

<span data-ttu-id="d9f1e-148">Дополнительные сведения о Microsoft Azure для Германии см. [здесь](https://azure.microsoft.com/overview/clouds/germany/).</span><span class="sxs-lookup"><span data-stu-id="d9f1e-148">For more information about Microsoft Azure Germany, see [Microsoft Azure Germany](https://azure.microsoft.com/overview/clouds/germany/).</span></span>

### <a name="properties-used-for-azure-redis-cache-powershell"></a><span data-ttu-id="d9f1e-149">Свойства, используемые в командлетах PowerShell кэша Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="d9f1e-149">Properties used for Azure Redis Cache PowerShell</span></span>
<span data-ttu-id="d9f1e-150">в следующей таблице Hello содержит свойства и описания для часто используемых параметров при создании и управления экземплярами кэша Redis для Azure с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-150">hello following table contains properties and descriptions for commonly used parameters when creating and managing your Azure Redis Cache instances using Azure PowerShell.</span></span>

| <span data-ttu-id="d9f1e-151">Параметр</span><span class="sxs-lookup"><span data-stu-id="d9f1e-151">Parameter</span></span> | <span data-ttu-id="d9f1e-152">Описание</span><span class="sxs-lookup"><span data-stu-id="d9f1e-152">Description</span></span> | <span data-ttu-id="d9f1e-153">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d9f1e-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d9f1e-154">Имя</span><span class="sxs-lookup"><span data-stu-id="d9f1e-154">Name</span></span> |<span data-ttu-id="d9f1e-155">Имя кэша hello</span><span class="sxs-lookup"><span data-stu-id="d9f1e-155">Name of hello cache</span></span> | |
| <span data-ttu-id="d9f1e-156">Расположение</span><span class="sxs-lookup"><span data-stu-id="d9f1e-156">Location</span></span> |<span data-ttu-id="d9f1e-157">Расположение кэша hello</span><span class="sxs-lookup"><span data-stu-id="d9f1e-157">Location of hello cache</span></span> | |
| <span data-ttu-id="d9f1e-158">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="d9f1e-158">ResourceGroupName</span></span> |<span data-ttu-id="d9f1e-159">Имя группы ресурсов, в какой кэш toocreate hello</span><span class="sxs-lookup"><span data-stu-id="d9f1e-159">Resource group name in which toocreate hello cache</span></span> | |
| <span data-ttu-id="d9f1e-160">Размер</span><span class="sxs-lookup"><span data-stu-id="d9f1e-160">Size</span></span> |<span data-ttu-id="d9f1e-161">размер кэша hello Hello.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-161">hello size of hello cache.</span></span> <span data-ttu-id="d9f1e-162">Допустимые значения: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250 МБ, 1 ГБ, 2,5 ГБ, 6 ГБ, 13 ГБ, 26 ГБ, 53 ГБ</span><span class="sxs-lookup"><span data-stu-id="d9f1e-162">Valid values are: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB</span></span> |<span data-ttu-id="d9f1e-163">1 ГБ</span><span class="sxs-lookup"><span data-stu-id="d9f1e-163">1GB</span></span> |
| <span data-ttu-id="d9f1e-164">ShardCount</span><span class="sxs-lookup"><span data-stu-id="d9f1e-164">ShardCount</span></span> |<span data-ttu-id="d9f1e-165">Количество сегментов toocreate при создании кэша premium с включенной кластеризацией Hello.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-165">hello number of shards toocreate when creating a premium cache with clustering enabled.</span></span> <span data-ttu-id="d9f1e-166">Допустимые значения: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span><span class="sxs-lookup"><span data-stu-id="d9f1e-166">Valid values are: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span></span> | |
| <span data-ttu-id="d9f1e-167">SKU</span><span class="sxs-lookup"><span data-stu-id="d9f1e-167">SKU</span></span> |<span data-ttu-id="d9f1e-168">Указывает hello SKU hello кэша.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-168">Specifies hello SKU of hello cache.</span></span> <span data-ttu-id="d9f1e-169">Допустимые значения: Basic, Standard, Premium</span><span class="sxs-lookup"><span data-stu-id="d9f1e-169">Valid values are: Basic, Standard, Premium</span></span> |<span data-ttu-id="d9f1e-170">Стандарт</span><span class="sxs-lookup"><span data-stu-id="d9f1e-170">Standard</span></span> |
| <span data-ttu-id="d9f1e-171">RedisConfiguration</span><span class="sxs-lookup"><span data-stu-id="d9f1e-171">RedisConfiguration</span></span> |<span data-ttu-id="d9f1e-172">Задает параметры конфигурации кластера Redis.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-172">Specifies Redis configuration settings.</span></span> <span data-ttu-id="d9f1e-173">Сведения о каждом параметре см. ниже hello [RedisConfiguration свойства](#redisconfiguration-properties) таблицы.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-173">For details on each setting, see hello following [RedisConfiguration properties](#redisconfiguration-properties) table.</span></span> | |
| <span data-ttu-id="d9f1e-174">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="d9f1e-174">EnableNonSslPort</span></span> |<span data-ttu-id="d9f1e-175">Указывает, включен ли hello не SSL-порт.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-175">Indicates whether hello non-SSL port is enabled.</span></span> |<span data-ttu-id="d9f1e-176">Ложь</span><span class="sxs-lookup"><span data-stu-id="d9f1e-176">False</span></span> |
| <span data-ttu-id="d9f1e-177">MaxMemoryPolicy</span><span class="sxs-lookup"><span data-stu-id="d9f1e-177">MaxMemoryPolicy</span></span> |<span data-ttu-id="d9f1e-178">Этот параметр устарел, вместо него используется параметр RedisConfiguration.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-178">This parameter has been deprecated - use RedisConfiguration instead.</span></span> | |
| <span data-ttu-id="d9f1e-179">StaticIP</span><span class="sxs-lookup"><span data-stu-id="d9f1e-179">StaticIP</span></span> |<span data-ttu-id="d9f1e-180">При размещении вашего кэша в виртуальной сети, указывает уникальный IP-адрес в подсети hello для кэша hello.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-180">When hosting your cache in a VNET, specifies a unique IP address in hello subnet for hello cache.</span></span> <span data-ttu-id="d9f1e-181">Если не указано, одна из подсети hello выбирается автоматически.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-181">If not provided, one is chosen for you from hello subnet.</span></span> | |
| <span data-ttu-id="d9f1e-182">Подсеть</span><span class="sxs-lookup"><span data-stu-id="d9f1e-182">Subnet</span></span> |<span data-ttu-id="d9f1e-183">При размещении вашего кэша в виртуальной сети, указывает имя hello hello подсети, в какой кэш toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-183">When hosting your cache in a VNET, specifies hello name of hello subnet in which toodeploy hello cache.</span></span> | |
| <span data-ttu-id="d9f1e-184">Виртуальная сеть</span><span class="sxs-lookup"><span data-stu-id="d9f1e-184">VirtualNetwork</span></span> |<span data-ttu-id="d9f1e-185">Если размещение кэша в виртуальной сети, задает идентификатор ресурса hello hello виртуальной сети, в какой кэш toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-185">When hosting your cache in a VNET, specifies hello resource ID of hello VNET in which toodeploy hello cache.</span></span> | |
| <span data-ttu-id="d9f1e-186">KeyType</span><span class="sxs-lookup"><span data-stu-id="d9f1e-186">KeyType</span></span> |<span data-ttu-id="d9f1e-187">Указывает, какой ключ доступа tooregenerate при обновлении ключей доступа.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-187">Specifies which access key tooregenerate when renewing access keys.</span></span> <span data-ttu-id="d9f1e-188">Допустимые значения: Primary, Secondary</span><span class="sxs-lookup"><span data-stu-id="d9f1e-188">Valid values are: Primary, Secondary</span></span> | |

### <a name="redisconfiguration-properties"></a><span data-ttu-id="d9f1e-189">Свойства RedisConfiguration</span><span class="sxs-lookup"><span data-stu-id="d9f1e-189">RedisConfiguration properties</span></span>
| <span data-ttu-id="d9f1e-190">Свойство</span><span class="sxs-lookup"><span data-stu-id="d9f1e-190">Property</span></span> | <span data-ttu-id="d9f1e-191">Описание</span><span class="sxs-lookup"><span data-stu-id="d9f1e-191">Description</span></span> | <span data-ttu-id="d9f1e-192">Ценовые категории</span><span class="sxs-lookup"><span data-stu-id="d9f1e-192">Pricing tiers</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d9f1e-193">rdb-backup-enabled</span><span class="sxs-lookup"><span data-stu-id="d9f1e-193">rdb-backup-enabled</span></span> |<span data-ttu-id="d9f1e-194">Указывает на то, включен ли параметр [Сохраняемость данных Redis](cache-how-to-premium-persistence.md) .</span><span class="sxs-lookup"><span data-stu-id="d9f1e-194">Whether [Redis data persistence](cache-how-to-premium-persistence.md) is enabled</span></span> |<span data-ttu-id="d9f1e-195">Только "Премиум"</span><span class="sxs-lookup"><span data-stu-id="d9f1e-195">Premium only</span></span> |
| <span data-ttu-id="d9f1e-196">rdb-storage-connection-string</span><span class="sxs-lookup"><span data-stu-id="d9f1e-196">rdb-storage-connection-string</span></span> |<span data-ttu-id="d9f1e-197">Здравствуйте, учетная запись хранения строки подключения с toohello для [сохраняемости данных Redis](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="d9f1e-197">hello connection string toohello storage account for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="d9f1e-198">Только "Премиум"</span><span class="sxs-lookup"><span data-stu-id="d9f1e-198">Premium only</span></span> |
| <span data-ttu-id="d9f1e-199">rdb-backup-frequency</span><span class="sxs-lookup"><span data-stu-id="d9f1e-199">rdb-backup-frequency</span></span> |<span data-ttu-id="d9f1e-200">Здравствуйте, интервал резервного копирования для [сохраняемости данных Redis](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="d9f1e-200">hello backup frequency for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="d9f1e-201">Только "Премиум"</span><span class="sxs-lookup"><span data-stu-id="d9f1e-201">Premium only</span></span> |
| <span data-ttu-id="d9f1e-202">maxmemory-reserved</span><span class="sxs-lookup"><span data-stu-id="d9f1e-202">maxmemory-reserved</span></span> |<span data-ttu-id="d9f1e-203">Настраивает hello [памяти, зарезервированной](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) для процессов не из кэша</span><span class="sxs-lookup"><span data-stu-id="d9f1e-203">Configures hello [memory reserved](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for non-cache processes</span></span> |<span data-ttu-id="d9f1e-204">"Стандартный" и "Премиум"</span><span class="sxs-lookup"><span data-stu-id="d9f1e-204">Standard and Premium</span></span> |
| <span data-ttu-id="d9f1e-205">maxmemory-policy</span><span class="sxs-lookup"><span data-stu-id="d9f1e-205">maxmemory-policy</span></span> |<span data-ttu-id="d9f1e-206">Настраивает hello [политика вытеснения](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) для кэша hello</span><span class="sxs-lookup"><span data-stu-id="d9f1e-206">Configures hello [eviction policy](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for hello cache</span></span> |<span data-ttu-id="d9f1e-207">Все ценовые категории</span><span class="sxs-lookup"><span data-stu-id="d9f1e-207">All pricing tiers</span></span> |
| <span data-ttu-id="d9f1e-208">notify-keyspace-events</span><span class="sxs-lookup"><span data-stu-id="d9f1e-208">notify-keyspace-events</span></span> |<span data-ttu-id="d9f1e-209">Настраивает [уведомления пространства ключей](cache-configure.md#keyspace-notifications-advanced-settings)</span><span class="sxs-lookup"><span data-stu-id="d9f1e-209">Configures [keyspace notifications](cache-configure.md#keyspace-notifications-advanced-settings)</span></span> |<span data-ttu-id="d9f1e-210">"Стандартный" и "Премиум"</span><span class="sxs-lookup"><span data-stu-id="d9f1e-210">Standard and Premium</span></span> |
| <span data-ttu-id="d9f1e-211">hash-max-ziplist-entries</span><span class="sxs-lookup"><span data-stu-id="d9f1e-211">hash-max-ziplist-entries</span></span> |<span data-ttu-id="d9f1e-212">Настраивает [оптимизацию памяти](http://redis.io/topics/memory-optimization) для небольших сводных данных.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-212">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="d9f1e-213">"Стандартный" и "Премиум"</span><span class="sxs-lookup"><span data-stu-id="d9f1e-213">Standard and Premium</span></span> |
| <span data-ttu-id="d9f1e-214">hash-max-ziplist-value</span><span class="sxs-lookup"><span data-stu-id="d9f1e-214">hash-max-ziplist-value</span></span> |<span data-ttu-id="d9f1e-215">Настраивает [оптимизацию памяти](http://redis.io/topics/memory-optimization) для небольших сводных данных.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-215">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="d9f1e-216">"Стандартный" и "Премиум"</span><span class="sxs-lookup"><span data-stu-id="d9f1e-216">Standard and Premium</span></span> |
| <span data-ttu-id="d9f1e-217">set-max-intset-entries</span><span class="sxs-lookup"><span data-stu-id="d9f1e-217">set-max-intset-entries</span></span> |<span data-ttu-id="d9f1e-218">Настраивает [оптимизацию памяти](http://redis.io/topics/memory-optimization) для небольших сводных данных.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-218">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="d9f1e-219">"Стандартный" и "Премиум"</span><span class="sxs-lookup"><span data-stu-id="d9f1e-219">Standard and Premium</span></span> |
| <span data-ttu-id="d9f1e-220">zset-max-ziplist-entries</span><span class="sxs-lookup"><span data-stu-id="d9f1e-220">zset-max-ziplist-entries</span></span> |<span data-ttu-id="d9f1e-221">Настраивает [оптимизацию памяти](http://redis.io/topics/memory-optimization) для небольших сводных данных.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-221">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="d9f1e-222">"Стандартный" и "Премиум"</span><span class="sxs-lookup"><span data-stu-id="d9f1e-222">Standard and Premium</span></span> |
| <span data-ttu-id="d9f1e-223">zset-max-ziplist-value</span><span class="sxs-lookup"><span data-stu-id="d9f1e-223">zset-max-ziplist-value</span></span> |<span data-ttu-id="d9f1e-224">Настраивает [оптимизацию памяти](http://redis.io/topics/memory-optimization) для небольших сводных данных.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-224">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="d9f1e-225">"Стандартный" и "Премиум"</span><span class="sxs-lookup"><span data-stu-id="d9f1e-225">Standard and Premium</span></span> |
| <span data-ttu-id="d9f1e-226">databases</span><span class="sxs-lookup"><span data-stu-id="d9f1e-226">databases</span></span> |<span data-ttu-id="d9f1e-227">Настраивает hello число баз данных.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-227">Configures hello number of databases.</span></span> <span data-ttu-id="d9f1e-228">Это свойство можно настроить только в момент создания кэша.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-228">This property can be configured only at cache creation.</span></span> |<span data-ttu-id="d9f1e-229">"Стандартный" и "Премиум"</span><span class="sxs-lookup"><span data-stu-id="d9f1e-229">Standard and Premium</span></span> |

## <a name="toocreate-a-redis-cache"></a><span data-ttu-id="d9f1e-230">toocreate кэша Redis</span><span class="sxs-lookup"><span data-stu-id="d9f1e-230">toocreate a Redis Cache</span></span>
<span data-ttu-id="d9f1e-231">Создаются новые экземпляры кэша Redis для Azure с помощью hello [New AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-231">New Azure Redis Cache instances are created using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d9f1e-232">Hello первом создании кэша Redis в подписку с помощью портала Azure hello hello портала регистрирует hello `Microsoft.Cache` пространство имен для этой подписки.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-232">hello first time you create a Redis cache in a subscription using hello Azure portal, hello portal registers hello `Microsoft.Cache` namespace for that subscription.</span></span> <span data-ttu-id="d9f1e-233">При попытке toocreate hello сначала Redis кэша в подписке с помощью PowerShell, необходимо сначала зарегистрировать это пространство имен, используя следующую команду; hello в противном случае командлеты, такие как `New-AzureRmRedisCache` и `Get-AzureRmRedisCache` ошибкой.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-233">If you attempt toocreate hello first Redis cache in a subscription using PowerShell, you must first register that namespace using hello following command; otherwise cmdlets such as `New-AzureRmRedisCache` and `Get-AzureRmRedisCache` fail.</span></span>
> 
> `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Cache"`
> 
> 

<span data-ttu-id="d9f1e-234">Список доступных параметров и их описания для toosee `New-AzureRmRedisCache`, запустите hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-234">toosee a list of available parameters and their descriptions for `New-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help New-AzureRmRedisCache -detailed

    NAME
        New-AzureRmRedisCache

    SYNOPSIS
        Creates a new redis cache.


    SYNTAX
        New-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Location <String> [-RedisVersion <String>]
        [-Size <String>] [-Sku <String>] [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort
        <Boolean>] [-ShardCount <Integer>] [-VirtualNetwork <String>] [-Subnet <String>] [-StaticIP <String>]
        [<CommonParameters>]


    DESCRIPTION
        hello New-AzureRmRedisCache cmdlet creates a new redis cache.


    PARAMETERS
        -Name <String>
            Name of hello redis cache toocreate.

        -ResourceGroupName <String>
            Name of resource group in which toocreate hello redis cache.

        -Location <String>
            Location in which toocreate hello redis cache.

        -RedisVersion <String>
            RedisVersion is deprecated and will be removed in future release.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value, databases.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. If no value is provided, hello default value is false and the
            non-SSL port will be disabled. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        -VirtualNetwork <String>
            hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{
            subid}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicNetwork/VirtualNetworks/{vnetName}

        -Subnet <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        -StaticIP <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="d9f1e-235">toocreate кэш с параметрами по умолчанию, запустите следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-235">toocreate a cache with default parameters, run hello following command.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US"

<span data-ttu-id="d9f1e-236">`ResourceGroupName`, `Name`, и `Location` являются обязательными параметрами, но hello rest являются необязательными и принимают значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-236">`ResourceGroupName`, `Name`, and `Location` are required parameters, but hello rest are optional and have default values.</span></span> <span data-ttu-id="d9f1e-237">Запущена предыдущая команда hello создает экземпляр кэша Redis для Azure стандартные SKU с указанным именем hello, расположение и группу ресурсов, составляет 1 ГБ емкости hello не SSL-порт отключен.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-237">Running hello previous command creates a Standard SKU Azure Redis Cache instance with hello specified name, location, and resource group, that is 1 GB in size with hello non-SSL port disabled.</span></span>

<span data-ttu-id="d9f1e-238">размер P1 (6 ГБ — 60 ГБ), P2 (13-130 ГБ), укажите toocreate кэша premium P3 (26-260 ГБ), или P4 (53-530 ГБ).</span><span class="sxs-lookup"><span data-stu-id="d9f1e-238">toocreate a premium cache, specify a size of P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), P3 (26 GB - 260 GB), or P4 (53 GB - 530 GB).</span></span> <span data-ttu-id="d9f1e-239">tooenable кластеризации, укажите количество сегментов, с помощью hello `ShardCount` параметра.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-239">tooenable clustering, specify a shard count using hello `ShardCount` parameter.</span></span> <span data-ttu-id="d9f1e-240">Hello следующий пример создает кэша premium P1 с 3 сегментов.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-240">hello following example creates a P1 premium cache with 3 shards.</span></span> <span data-ttu-id="d9f1e-241">Размера кэша premium P1 — 6 ГБ, размер, и поскольку мы указали, что три сегментов hello общий размер 18 ГБ (3 x 6 ГБ).</span><span class="sxs-lookup"><span data-stu-id="d9f1e-241">A P1 premium cache is 6 GB in size, and since we specified three shards hello total size is 18 GB (3 x 6 GB).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P1 -ShardCount 3

<span data-ttu-id="d9f1e-242">toospecify значения для hello `RedisConfiguration` параметра, заключите hello значения внутри `{}` как ключ значение как пары `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-242">toospecify values for hello `RedisConfiguration` parameter, enclose hello values inside `{}` as key/value pairs like `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span></span> <span data-ttu-id="d9f1e-243">Hello следующий пример создает стандартный 1 ГБ кэша с `allkeys-random` maxmemory политики и пространство ключей уведомлений, настроенной с `KEA`.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-243">hello following example creates a standard 1 GB cache with `allkeys-random` maxmemory policy and keyspace notifications configured with `KEA`.</span></span> <span data-ttu-id="d9f1e-244">Дополнительные сведения см. в разделах [Уведомления пространства ключей (дополнительные параметры)](cache-configure.md#keyspace-notifications-advanced-settings) и [Политики памяти](cache-configure.md#memory-policies).</span><span class="sxs-lookup"><span data-stu-id="d9f1e-244">For more information, see [Keyspace notifications (advanced settings)](cache-configure.md#keyspace-notifications-advanced-settings) and [Memory policies](cache-configure.md#memory-policies).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}

<a name="databases"></a>

## <a name="tooconfigure-hello-databases-setting-during-cache-creation"></a><span data-ttu-id="d9f1e-245">hello tooconfigure баз данных, можно задать во время создания кэша</span><span class="sxs-lookup"><span data-stu-id="d9f1e-245">tooconfigure hello databases setting during cache creation</span></span>
<span data-ttu-id="d9f1e-246">Hello `databases` параметр можно настроить только во время создания кэша.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-246">hello `databases` setting can be configured only during cache creation.</span></span> <span data-ttu-id="d9f1e-247">Hello следующий пример создает premium P3 (26 ГБ) кэш с 48 баз данных, с помощью hello [New AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-247">hello following example creates a premium P3 (26 GB) cache with 48 databases using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P3 -RedisConfiguration @{"databases" = "48"}

<span data-ttu-id="d9f1e-248">Дополнительные сведения о hello `databases` свойство, в разделе [конфигурации сервера по умолчанию кэш Azure Redis](cache-configure.md#default-redis-server-configuration).</span><span class="sxs-lookup"><span data-stu-id="d9f1e-248">For more information on hello `databases` property, see [Default Azure Redis Cache server configuration](cache-configure.md#default-redis-server-configuration).</span></span> <span data-ttu-id="d9f1e-249">Дополнительные сведения о создании кэша с использованием hello [New AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) командлета, см. предыдущие hello [toocreate кэша Redis](#to-create-a-redis-cache) раздела.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-249">For more information on creating a cache using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet, see hello previous [toocreate a Redis Cache](#to-create-a-redis-cache) section.</span></span>

## <a name="tooupdate-a-redis-cache"></a><span data-ttu-id="d9f1e-250">tooupdate кэш Redis</span><span class="sxs-lookup"><span data-stu-id="d9f1e-250">tooupdate a Redis cache</span></span>
<span data-ttu-id="d9f1e-251">Экземпляры кэша Redis для Azure обновляются с помощью hello [AzureRmRedisCache набор](https://msdn.microsoft.com/library/azure/mt634518.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-251">Azure Redis Cache instances are updated using hello [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet.</span></span>

<span data-ttu-id="d9f1e-252">Список доступных параметров и их описания для toosee `Set-AzureRmRedisCache`, запустите hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-252">toosee a list of available parameters and their descriptions for `Set-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Set-AzureRmRedisCache -detailed

    NAME
        Set-AzureRmRedisCache

    SYNOPSIS
        Set redis cache updatable parameters.

    SYNTAX
        Set-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Size <String>] [-Sku <String>]
        [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort <Boolean>] [-ShardCount
        <Integer>] [<CommonParameters>]

    DESCRIPTION
        hello Set-AzureRmRedisCache cmdlet sets redis cache parameters.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooupdate.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. hello default value is null and no change will be made toothe
            currently configured value. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="d9f1e-253">Hello `Set-AzureRmRedisCache` командлет можно использовать tooupdate свойств, таких как `Size`, `Sku`, `EnableNonSslPort`и hello `RedisConfiguration` значения.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-253">hello `Set-AzureRmRedisCache` cmdlet can be used tooupdate properties such as `Size`, `Sku`, `EnableNonSslPort`, and hello `RedisConfiguration` values.</span></span> 

<span data-ttu-id="d9f1e-254">Hello следующую команду, что политика максимальной памяти для кэша Redis hello hello обновления с именем myCache.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-254">hello following command updates hello maxmemory-policy for hello Redis Cache named myCache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName "myGroup" -Name "myCache" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random"}

<a name="scale"></a>

## <a name="tooscale-a-redis-cache"></a><span data-ttu-id="d9f1e-255">tooscale кэш Redis</span><span class="sxs-lookup"><span data-stu-id="d9f1e-255">tooscale a Redis cache</span></span>
<span data-ttu-id="d9f1e-256">`Set-AzureRmRedisCache`может быть tooscale используется экземпляр кэша redis для Azure — при hello `Size`, `Sku`, или `ShardCount` свойства изменяются.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-256">`Set-AzureRmRedisCache` can be used tooscale an Azure Redis cache instance when hello `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> 

> [!NOTE]
> <span data-ttu-id="d9f1e-257">Масштабирование кэша, с помощью PowerShell — тема toohello такие же ограничения и правила, что масштабирование кэша из hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-257">Scaling a cache using PowerShell is subject toohello same limits and guidelines as scaling a cache from hello Azure portal.</span></span> <span data-ttu-id="d9f1e-258">Можно масштабировать tooa различных ценовой категории с hello следующие ограничения.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-258">You can scale tooa different pricing tier with hello following restrictions.</span></span>
> 
> * <span data-ttu-id="d9f1e-259">Нельзя масштабировать из выше ценовой уровень tooa ниже ценовой категории.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-259">You can't scale from a higher pricing tier tooa lower pricing tier.</span></span>
> * <span data-ttu-id="d9f1e-260">Нельзя масштабировать из **Premium** кэша вниз tooa **Стандартная** или **основные** кэша.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-260">You can't scale from a **Premium** cache down tooa **Standard** or a **Basic** cache.</span></span>
> * <span data-ttu-id="d9f1e-261">Нельзя масштабировать из **Стандартная** кэша вниз tooa **основные** кэша.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-261">You can't scale from a **Standard** cache down tooa **Basic** cache.</span></span>
> * <span data-ttu-id="d9f1e-262">Можно масштабировать от **основные** кэшировать tooa **Стандартная** кэш, но не может изменить размер hello в hello то же время.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-262">You can scale from a **Basic** cache tooa **Standard** cache but you can't change hello size at hello same time.</span></span> <span data-ttu-id="d9f1e-263">Если требуется другой размер, можно сделать последующих размер toohello требуемой операции масштабирования.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-263">If you need a different size, you can do a subsequent scaling operation toohello desired size.</span></span>
> * <span data-ttu-id="d9f1e-264">Нельзя масштабировать из **основные** кэшировать непосредственно tooa **Premium** кэша.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-264">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="d9f1e-265">Требуется расширение из **основные** слишком**Стандартная** за одну операцию масштабирования, а затем с **Стандартная** слишком**Premium** последующих масштабирования операция.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-265">You must scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
> * <span data-ttu-id="d9f1e-266">Нельзя масштабировать от большего вниз toohello **C0 (250 МБ)** размер.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-266">You can't scale from a larger size down toohello **C0 (250 MB)** size.</span></span>
> 
> <span data-ttu-id="d9f1e-267">Дополнительные сведения см. в разделе [как tooScale Redis для Azure кэшировать](cache-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="d9f1e-267">For more information, see [How tooScale Azure Redis Cache](cache-how-to-scale.md).</span></span>
> 
> 

<span data-ttu-id="d9f1e-268">Hello следующем примере показано, как tooscale кэш именоваться `myCache` tooa 2,5 ГБ кэша.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-268">hello following example shows how tooscale a cache named `myCache` tooa 2.5 GB cache.</span></span> <span data-ttu-id="d9f1e-269">Обратите внимание, что команда будет работать в кэше уровня "Базовый" или "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="d9f1e-269">Note that this command works for both a Basic or a Standard cache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="d9f1e-270">После этого команды, возвращается состояние hello hello кэша (аналогично toocalling `Get-AzureRmRedisCache`).</span><span class="sxs-lookup"><span data-stu-id="d9f1e-270">After this command is issued, hello status of hello cache is returned (similar toocalling `Get-AzureRmRedisCache`).</span></span> <span data-ttu-id="d9f1e-271">Обратите внимание, что hello `ProvisioningState` — `Scaling`.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-271">Note that hello `ProvisioningState` is `Scaling`.</span></span>

    PS C:\> Set-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup -Size 2.5GB


    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/mygroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Scaling
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 150], [notify-keyspace-events, KEA],
                         [maxmemory-delta, 150]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : mygroup
    PrimaryKey         : ....
    SecondaryKey       : ....
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

<span data-ttu-id="d9f1e-272">По завершении hello операция масштабирования hello `ProvisioningState` изменяет слишком`Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-272">When hello scaling operation is complete, hello `ProvisioningState` changes too`Succeeded`.</span></span> <span data-ttu-id="d9f1e-273">При необходимости toomake последующей операции масштабирования, таких как изменение из основных tooStandard и затем изменив размер hello, необходимо дождаться завершения предыдущей операции hello или появится ошибка примерно toohello следующее.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-273">If you need toomake a subsequent scaling operation, such as changing from Basic tooStandard and then changing hello size, you must wait until hello previous operation is complete or you receive an error similar toohello following.</span></span>

    Set-AzureRmRedisCache : Conflict: hello resource '...' is not in a stable state, and is currently unable tooaccept hello update request.

## <a name="tooget-information-about-a-redis-cache"></a><span data-ttu-id="d9f1e-274">tooget сведения о кэше Redis</span><span class="sxs-lookup"><span data-stu-id="d9f1e-274">tooget information about a Redis cache</span></span>
<span data-ttu-id="d9f1e-275">Можно получить сведения о кэше, используя hello [Get AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-275">You can retrieve information about a cache using hello [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet.</span></span>

<span data-ttu-id="d9f1e-276">Список доступных параметров и их описания для toosee `Get-AzureRmRedisCache`, запустите hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-276">toosee a list of available parameters and their descriptions for `Get-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCache -detailed

    NAME
        Get-AzureRmRedisCache

    SYNOPSIS
        Gets details about a single cache or all caches in hello specified resource group or all caches in hello current
        subscription.

    SYNTAX
        Get-AzureRmRedisCache [-Name <String>] [-ResourceGroupName <String>] [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCache cmdlet gets hello details about a cache or caches depending on input parameters. If both
        ResourceGroupName and Name parameters are provided then Get-AzureRmRedisCache will return details about the
        specific cache name provided.

        If only ResourceGroupName is provided than it will return details about all caches in hello specified resource group.

        If no parameters are given than it will return details about all caches hello current subscription.

    PARAMETERS
        -Name <String>
            hello name of hello cache. When this parameter is provided along with ResourceGroupName, Get-AzureRmRedisCache
            returns hello details for hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache or caches. If ResourceGroupName is provided with Name
            then Get-AzureRmRedisCache returns hello details of hello cache specified by Name. If only hello ResourceGroup
            parameter is provided, then details for all caches in hello resource group are returned.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="d9f1e-277">Запустите tooreturn сведения о всех кэшей в текущей подписке hello, `Get-AzureRmRedisCache` без параметров.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-277">tooreturn information about all caches in hello current subscription, run `Get-AzureRmRedisCache` without any parameters.</span></span>

    Get-AzureRmRedisCache

<span data-ttu-id="d9f1e-278">Запустите tooreturn сведения о всех кэшей в определенной группе ресурсов, `Get-AzureRmRedisCache` с hello `ResourceGroupName` параметра.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-278">tooreturn information about all caches in a specific resource group, run `Get-AzureRmRedisCache` with hello `ResourceGroupName` parameter.</span></span>

    Get-AzureRmRedisCache -ResourceGroupName myGroup

<span data-ttu-id="d9f1e-279">Запустите tooreturn сведения о конкретных кэш, `Get-AzureRmRedisCache` с hello `Name` параметр, содержащий имя hello кэша hello и hello `ResourceGroupName` параметр с группой ресурсов hello, содержащей этот кэш.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-279">tooreturn information about a specific cache, run `Get-AzureRmRedisCache` with hello `Name` parameter containing hello name of hello cache, and hello `ResourceGroupName` parameter with hello resource group containing that cache.</span></span>

    PS C:\> Get-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/myGroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Succeeded
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 62], [notify-keyspace-events, KEA],
                         [maxclients, 1000]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : myGroup
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

## <a name="tooretrieve-hello-access-keys-for-a-redis-cache"></a><span data-ttu-id="d9f1e-280">клавиши доступа hello tooretrieve для кэша Redis</span><span class="sxs-lookup"><span data-stu-id="d9f1e-280">tooretrieve hello access keys for a Redis cache</span></span>
<span data-ttu-id="d9f1e-281">tooretrieve hello ключи доступа для кэша, можно использовать hello [Get AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-281">tooretrieve hello access keys for your cache, you can use hello [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet.</span></span>

<span data-ttu-id="d9f1e-282">Список доступных параметров и их описания для toosee `Get-AzureRmRedisCacheKey`, запустите hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-282">toosee a list of available parameters and their descriptions for `Get-AzureRmRedisCacheKey`, run hello following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCacheKey -detailed

    NAME
        Get-AzureRmRedisCacheKey

    SYNOPSIS
        Gets hello accesskeys for hello specified redis cache.


    SYNTAX
        Get-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCacheKey cmdlet gets hello access keys for hello specified cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="d9f1e-283">tooretrieve hello ключи для кэша, вызов hello `Get-AzureRmRedisCacheKey` командлета и передайте имя hello кэша hello имя группы ресурсов hello, содержащий кэш hello.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-283">tooretrieve hello keys for your cache, call hello `Get-AzureRmRedisCacheKey` cmdlet and pass in hello name of your cache hello name of hello resource group that contains hello cache.</span></span>

    PS C:\> Get-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup

    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : ABhfB757JgjIgt785JgKH9865eifmekfnn649303JKL=

## <a name="tooregenerate-access-keys-for-your-redis-cache"></a><span data-ttu-id="d9f1e-284">tooregenerate клавиши доступа для кэша Redis</span><span class="sxs-lookup"><span data-stu-id="d9f1e-284">tooregenerate access keys for your Redis cache</span></span>
<span data-ttu-id="d9f1e-285">tooregenerate hello ключи доступа для кэша, можно использовать hello [New AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-285">tooregenerate hello access keys for your cache, you can use hello [New-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet.</span></span>

<span data-ttu-id="d9f1e-286">Список доступных параметров и их описания для toosee `New-AzureRmRedisCacheKey`, запустите hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-286">toosee a list of available parameters and their descriptions for `New-AzureRmRedisCacheKey`, run hello following command.</span></span>

    PS C:\> Get-Help New-AzureRmRedisCacheKey -detailed

    NAME
        New-AzureRmRedisCacheKey

    SYNOPSIS
        Regenerates hello access key of a redis cache.

    SYNTAX
        New-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> -KeyType <String> [-Force] [<CommonParameters>]

    DESCRIPTION
        hello New-AzureRmRedisCacheKey cmdlet regenerate hello access key of a redis cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -KeyType <String>
            Specifies whether tooregenerate hello primary or secondary access key. Possible values are Primary or Secondary.

        -Force
            When hello Force parameter is provided, hello specified access key is regenerated without any confirmation prompts.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="d9f1e-287">tooregenerate hello первичный или вторичный ключ для кэша, вызов hello `New-AzureRmRedisCacheKey` командлета передайте hello, группа ресурсов и имя либо укажите `Primary` или `Secondary` для hello `KeyType` параметра.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-287">tooregenerate hello primary or secondary key for your cache, call hello `New-AzureRmRedisCacheKey` cmdlet and pass in hello name, resource group, and specify either `Primary` or `Secondary` for hello `KeyType` parameter.</span></span> <span data-ttu-id="d9f1e-288">В следующем примере hello генерируется hello вторичный ключ доступа для кэша.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-288">In hello following example, hello secondary access key for a cache is regenerated.</span></span>

    PS C:\> New-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup -KeyType Secondary

    Confirm
    Are you sure you want tooregenerate Secondary key for redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : c53hj3kh4jhHjPJk8l0jji785JgKH9865eifmekfnn6=

## <a name="toodelete-a-redis-cache"></a><span data-ttu-id="d9f1e-289">toodelete кэш Redis</span><span class="sxs-lookup"><span data-stu-id="d9f1e-289">toodelete a Redis cache</span></span>
<span data-ttu-id="d9f1e-290">кэш Redis, toodelete использовать hello [AzureRmRedisCache удаление](https://msdn.microsoft.com/library/azure/mt634515.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-290">toodelete a Redis cache, use hello [Remove-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet.</span></span>

<span data-ttu-id="d9f1e-291">Список доступных параметров и их описания для toosee `Remove-AzureRmRedisCache`, запустите hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-291">toosee a list of available parameters and their descriptions for `Remove-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Remove-AzureRmRedisCache -detailed

    NAME
        Remove-AzureRmRedisCache

    SYNOPSIS
        Remove redis cache if exists.

    SYNTAX
        Remove-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Force] [-PassThru] [<CommonParameters>

    DESCRIPTION
        hello Remove-AzureRmRedisCache cmdlet removes a redis cache if it exists.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooremove.

        -ResourceGroupName <String>
            Name of hello resource group of hello cache tooremove.

        -Force
            When hello Force parameter is provided, hello cache is removed without any confirmation prompts.

        -PassThru
            By default Remove-AzureRmRedisCache removes hello cache and does not return any value. If hello PassThru par
            is provided then Remove-AzureRmRedisCache returns a boolean value indicating hello success of hello operatio

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="d9f1e-292">В следующем примере hello, hello кэша с именем `myCache` удаляется.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-292">In hello following example, hello cache named `myCache` is removed.</span></span>

    PS C:\> Remove-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Confirm
    Are you sure you want tooremove redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


## <a name="tooimport-a-redis-cache"></a><span data-ttu-id="d9f1e-293">tooimport кэш Redis</span><span class="sxs-lookup"><span data-stu-id="d9f1e-293">tooimport a Redis cache</span></span>
<span data-ttu-id="d9f1e-294">Можно импортировать данные в экземпляр кэша Redis для Azure, с помощью hello `Import-AzureRmRedisCache` командлета.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-294">You can import data into an Azure Redis Cache instance using hello `Import-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d9f1e-295">Функция импорта и экспорта доступна только для кэшей категории [Премиум](cache-premium-tier-intro.md).</span><span class="sxs-lookup"><span data-stu-id="d9f1e-295">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="d9f1e-296">Дополнительные сведения об импорте и экспорте см. в статье [Импорт и экспорт данных в кэше Redis для Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="d9f1e-296">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="d9f1e-297">Список доступных параметров и их описания для toosee `Import-AzureRmRedisCache`, запустите hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-297">toosee a list of available parameters and their descriptions for `Import-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Import-AzureRmRedisCache -detailed

    NAME
        Import-AzureRmRedisCache

    SYNOPSIS
        Import data from blobs tooAzure Redis Cache.


    SYNTAX
        Import-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Files <String[]> [-Format <String>] [-Force]
        [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Import-AzureRmRedisCache cmdlet imports data from hello specified blobs into Azure Redis Cache.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Files <String[]>
            SAS urls of blobs whose content should be imported into hello cache.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -Force
            When hello Force parameter is provided, import will be performed without any confirmation prompts.

        -PassThru
            By default Import-AzureRmRedisCache imports data in cache and does not return any value. If hello PassThru
            parameter is provided then Import-AzureRmRedisCache returns a boolean value indicating hello success of the
            operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="d9f1e-298">Hello следующая команда импортирует данные из большого двоичного объекта hello указанного hello SAS uri в кэше Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-298">hello following command imports data from hello blob specified by hello SAS uri into Azure Redis Cache.</span></span>

    PS C:\>Import-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Files @("https://mystorageaccount.blob.core.windows.net/mycontainername/blobname?sv=2015-04-05&sr=b&sig=caIwutG2uDa0NZ8mjdNJdgOY8%2F8mhwRuGNdICU%2B0pI4%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwd") -Force

## <a name="tooexport-a-redis-cache"></a><span data-ttu-id="d9f1e-299">tooexport кэш Redis</span><span class="sxs-lookup"><span data-stu-id="d9f1e-299">tooexport a Redis cache</span></span>
<span data-ttu-id="d9f1e-300">Можно экспортировать данные из экземпляра кэша Redis для Azure с помощью hello `Export-AzureRmRedisCache` командлета.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-300">You can export data from an Azure Redis Cache instance using hello `Export-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d9f1e-301">Функция импорта и экспорта доступна только для кэшей категории [Премиум](cache-premium-tier-intro.md).</span><span class="sxs-lookup"><span data-stu-id="d9f1e-301">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="d9f1e-302">Дополнительные сведения об импорте и экспорте см. в статье [Импорт и экспорт данных в кэше Redis для Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="d9f1e-302">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="d9f1e-303">Список доступных параметров и их описания для toosee `Export-AzureRmRedisCache`, запустите hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-303">toosee a list of available parameters and their descriptions for `Export-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Export-AzureRmRedisCache -detailed

    NAME
        Export-AzureRmRedisCache

    SYNOPSIS
        Exports data from Azure Redis Cache tooa specified container.


    SYNTAX
        Export-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Prefix <String> -Container <String> [-Format
        <String>] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Export-AzureRmRedisCache cmdlet exports data from Azure Redis Cache tooa specified container.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Prefix <String>
            Prefix toouse for blob names.

        -Container <String>
            SAS url of container where data should be exported.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -PassThru
            By default Export-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Export-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="d9f1e-304">Hello следующая команда экспортирует данные из экземпляра кэша Redis для Azure в контейнер hello указанного hello SAS uri.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-304">hello following command exports data from an Azure Redis Cache instance into hello container specified by hello SAS uri.</span></span>

        PS C:\>Export-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Prefix "blobprefix"
        -Container "https://mystorageaccount.blob.core.windows.net/mycontainer?sv=2015-04-05&sr=c&sig=HezZtBZ3DURmEGDduauE7
        pvETY4kqlPI8JCNa8ATmaw%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwdl"

## <a name="tooreboot-a-redis-cache"></a><span data-ttu-id="d9f1e-305">tooreboot кэш Redis</span><span class="sxs-lookup"><span data-stu-id="d9f1e-305">tooreboot a Redis cache</span></span>
<span data-ttu-id="d9f1e-306">Можно перезагрузить экземпляр кэша Redis для Azure с помощью hello `Reset-AzureRmRedisCache` командлета.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-306">You can reboot your Azure Redis Cache instance using hello `Reset-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d9f1e-307">Функция перезагрузки доступна только для кэшей [уровня "Премиум"](cache-premium-tier-intro.md).</span><span class="sxs-lookup"><span data-stu-id="d9f1e-307">Reboot is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="d9f1e-308">Дополнительные сведения о перезапуске кэша см. в разделе [Reboot](cache-administration.md#reboot) статьи "Администрирование кэша Redis для Azure".</span><span class="sxs-lookup"><span data-stu-id="d9f1e-308">For more information about rebooting your cache, see [Cache administration - reboot](cache-administration.md#reboot).</span></span>
> 
> 

<span data-ttu-id="d9f1e-309">Список доступных параметров и их описания для toosee `Reset-AzureRmRedisCache`, запустите hello следующую команду.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-309">toosee a list of available parameters and their descriptions for `Reset-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Reset-AzureRmRedisCache -detailed

    NAME
        Reset-AzureRmRedisCache

    SYNOPSIS
        Reboot specified node(s) of an Azure Redis Cache instance.


    SYNTAX
        Reset-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -RebootType <String> [-ShardId <Integer>]
        [-Force] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Reset-AzureRmRedisCache cmdlet reboots hello specified node(s) of an Azure Redis Cache instance.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -RebootType <String>
            Which node tooreboot. Possible values are "PrimaryNode", "SecondaryNode", "AllNodes".

        -ShardId <Integer>
            Which shard tooreboot when rebooting a premium cache with clustering enabled.

        -Force
            When hello Force parameter is provided, reset will be performed without any confirmation prompts.

        -PassThru
            By default Reset-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Reset-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="d9f1e-310">Hello следующая команда перезагружает обоих узлов hello указанного кэша.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-310">hello following command reboots both nodes of hello specified cache.</span></span>

        PS C:\>Reset-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -RebootType "AllNodes"
        -Force


## <a name="next-steps"></a><span data-ttu-id="d9f1e-311">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d9f1e-311">Next steps</span></span>
<span data-ttu-id="d9f1e-312">toolearn Подробнее об использовании Windows PowerShell с помощью Azure см. следующие ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-312">toolearn more about using Windows PowerShell with Azure, see hello following resources:</span></span>

* [<span data-ttu-id="d9f1e-313">Документация по командлету кэша Redis для Azure на MSDN</span><span class="sxs-lookup"><span data-stu-id="d9f1e-313">Azure Redis Cache cmdlet documentation on MSDN</span></span>](https://msdn.microsoft.com/library/azure/mt634513.aspx)
* <span data-ttu-id="d9f1e-314">[Командлеты диспетчера ресурсов Azure](http://go.microsoft.com/fwlink/?LinkID=394765): узнать toouse hello командлеты в модуле Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-314">[Azure Resource Manager Cmdlets](http://go.microsoft.com/fwlink/?LinkID=394765): Learn toouse hello cmdlets in hello Azure Resource Manager module.</span></span>
* <span data-ttu-id="d9f1e-315">[С помощью ресурса группы toomanage ресурсам Azure](../azure-resource-manager/resource-group-template-deploy-portal.md): Узнайте, как toocreate групп ресурсов в hello портал Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-315">[Using Resource groups toomanage your Azure resources](../azure-resource-manager/resource-group-template-deploy-portal.md): Learn how toocreate and manage resource groups in hello Azure portal.</span></span>
* <span data-ttu-id="d9f1e-316">[Блог Azure](http://blogs.msdn.com/windowsazure): узнайте о новых возможностях в Azure.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-316">[Azure blog](http://blogs.msdn.com/windowsazure): Learn about new features in Azure.</span></span>
* <span data-ttu-id="d9f1e-317">[Блог Windows PowerShell](http://blogs.msdn.com/powershell): узнайте о новых возможностях в Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-317">[Windows PowerShell blog](http://blogs.msdn.com/powershell): Learn about new features in Windows PowerShell.</span></span>
* <span data-ttu-id="d9f1e-318">[Блог "Hey, Scripting Блог](http://blogs.technet.com/b/heyscriptingguy/): получить советы реальных из hello сообщества Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d9f1e-318">["Hey, Scripting Guy!" Blog](http://blogs.technet.com/b/heyscriptingguy/): Get real-world tips and tricks from hello Windows PowerShell community.</span></span>

