---
title: "ключи доступа службы мультимедиа aaaUpdate после отката хранилища | Документы Microsoft"
description: "Рекомендации по как ключи доступа службы мультимедиа tooupdate после отката хранилища предоставляют этой статьи."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a892ebb0-0ea0-4fc8-b715-60347cc5c95b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: milanga;cenkdin;juliako
ms.openlocfilehash: 26fa7a75a73397842aaebda59516a00f68ab97f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="update-media-services-after-rolling-storage-access-keys"></a><span data-ttu-id="f78fa-103">Обновление служб мультимедиа после оборота ключей доступа к хранилищу</span><span class="sxs-lookup"><span data-stu-id="f78fa-103">Update Media Services after rolling storage access keys</span></span>

<span data-ttu-id="f78fa-104">При создании новой учетной записи служб мультимедиа Azure (AMS), также предлагается tooselect учетной записи хранилища Azure, то есть использовать toostore мультимедийного содержимого.</span><span class="sxs-lookup"><span data-stu-id="f78fa-104">When you create a new Azure Media Services (AMS) account, you are also asked tooselect an Azure Storage account that is used toostore your media content.</span></span> <span data-ttu-id="f78fa-105">Можно добавить несколько tooyour учетных записей хранилища учетной записи служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="f78fa-105">You can add more than one storage accounts tooyour Media Services account.</span></span> <span data-ttu-id="f78fa-106">В этом разделе показано, как toorotate хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="f78fa-106">This topic shows how toorotate storage keys.</span></span> <span data-ttu-id="f78fa-107">Здесь также показано, как учетные записи хранения tooadd учетной записи tooa мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="f78fa-107">It also shows how tooadd storage accounts tooa media account.</span></span> 

<span data-ttu-id="f78fa-108">tooperform hello действия, описанные в этом разделе, вы должны использовать [API-интерфейсы ARM](https://docs.microsoft.com/rest/api/media/mediaservice) и [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).</span><span class="sxs-lookup"><span data-stu-id="f78fa-108">tooperform hello actions described in this topic, you should be using [ARM APIs](https://docs.microsoft.com/rest/api/media/mediaservice) and [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).</span></span>  <span data-ttu-id="f78fa-109">Дополнительные сведения см. в разделе [как toomanage Azure ресурсы с помощью PowerShell и диспетчера ресурсов](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f78fa-109">For more information, see [How toomanage Azure resources with PowerShell and Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

## <a name="overview"></a><span data-ttu-id="f78fa-110">Обзор</span><span class="sxs-lookup"><span data-stu-id="f78fa-110">Overview</span></span>

<span data-ttu-id="f78fa-111">При создании новой учетной записи хранения Azure создает два 512-разрядных ключа доступа, являющиеся используется tooauthenticate доступ к учетной записи хранилища tooyour.</span><span class="sxs-lookup"><span data-stu-id="f78fa-111">When a new storage account is created, Azure generates two 512-bit storage access keys, which are used tooauthenticate access tooyour storage account.</span></span> <span data-ttu-id="f78fa-112">tookeep безопаснее, рекомендуется tooperiodically вашего подключения к хранилищу повторно создать и сменить ваш ключ доступа хранилища.</span><span class="sxs-lookup"><span data-stu-id="f78fa-112">tookeep your storage connections more secure, it is recommended tooperiodically regenerate and rotate your storage access key.</span></span> <span data-ttu-id="f78fa-113">Предоставляются в порядке tooenable toomaintain подключений toohello учетной записи хранилища с помощью одного доступ к ключу при повторном создании hello другого ключа доступа, два ключа доступа (первичная и Вторичная).</span><span class="sxs-lookup"><span data-stu-id="f78fa-113">Two access keys (primary and secondary) are provided in order tooenable you toomaintain connections toohello storage account using one access key while you regenerate hello other access key.</span></span> <span data-ttu-id="f78fa-114">Этот процесс называется "оборот ключей доступа".</span><span class="sxs-lookup"><span data-stu-id="f78fa-114">This procedure is also called "rolling access keys".</span></span>

<span data-ttu-id="f78fa-115">Службы мультимедиа зависит от ключа хранилища, предоставляемые tooit.</span><span class="sxs-lookup"><span data-stu-id="f78fa-115">Media Services depends on a storage key provided tooit.</span></span> <span data-ttu-id="f78fa-116">В частности hello указатели, которые используется toostream или загрузить активов зависят от ключа доступа hello указанное хранилище.</span><span class="sxs-lookup"><span data-stu-id="f78fa-116">Specifically, hello locators that are used toostream or download your assets depend on hello specified storage access key.</span></span> <span data-ttu-id="f78fa-117">При создании учетной записи AMS он зависит от ключа доступа hello основного хранилища по умолчанию, но имени пользователя можно обновить ключ хранилища hello с AMS.</span><span class="sxs-lookup"><span data-stu-id="f78fa-117">When an AMS account is created it takes a dependency on hello primary storage access key by default but as a user you can update hello storage key that AMS has.</span></span> <span data-ttu-id="f78fa-118">Необходимо убедиться, что toolet Media Services известны какие toouse ключа, выполнив действия, описанные в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="f78fa-118">You must make sure toolet Media Services know which key toouse by following steps described in this topic.</span></span>  

>[!NOTE]
> <span data-ttu-id="f78fa-119">Если используется несколько учетных записей хранения, необходимо выполнить эту процедуру для каждой из них.</span><span class="sxs-lookup"><span data-stu-id="f78fa-119">If you have multiple storage accounts, you would perform this procedure with each storage account.</span></span> <span data-ttu-id="f78fa-120">Hello порядок, в котором вы смена ключей хранилища не является фиксированным.</span><span class="sxs-lookup"><span data-stu-id="f78fa-120">hello order in which you rotate storage keys is not fixed.</span></span> <span data-ttu-id="f78fa-121">Можно сначала поворот hello вторичного ключа и затем hello первичного ключа или наоборот.</span><span class="sxs-lookup"><span data-stu-id="f78fa-121">You can rotate hello secondary key first and then hello primary key or vice versa.</span></span>
>
> <span data-ttu-id="f78fa-122">Перед выполнением действия описанные в этом разделе для рабочей учетной записи, убедитесь, что tootest их с подготовительной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f78fa-122">Before executing steps described in this topic on a production account, make sure tootest them on a pre-production account.</span></span>
>

## <a name="steps-toorotate-storage-keys"></a><span data-ttu-id="f78fa-123">Действия toorotate хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="f78fa-123">Steps toorotate storage keys</span></span> 
 
 1. <span data-ttu-id="f78fa-124">Изменение hello ключ учетной записи хранения основной посредством командлета powershell hello или [Azure](https://portal.azure.com/) портала.</span><span class="sxs-lookup"><span data-stu-id="f78fa-124">Change hello storage account Primary key through hello powershell cmdlet or [Azure](https://portal.azure.com/) portal.</span></span>
 2. <span data-ttu-id="f78fa-125">Вызовите командлет AzureRmMediaServiceStorageKeys синхронизации с toopick учетной записи media соответствующие params tooforce копирование ключи учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="f78fa-125">Call Sync-AzureRmMediaServiceStorageKeys cmdlet with appropriate params tooforce media account toopick up storage account keys</span></span>
 
    <span data-ttu-id="f78fa-126">Hello в следующем примере показано, как toosync ключей toostorage учетные записи.</span><span class="sxs-lookup"><span data-stu-id="f78fa-126">hello following example shows how toosync keys toostorage accounts.</span></span>
  
         Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId
  
 3. <span data-ttu-id="f78fa-127">Подождите один час или около того.</span><span class="sxs-lookup"><span data-stu-id="f78fa-127">Wait an hour or so.</span></span> <span data-ttu-id="f78fa-128">Убедитесь, что работаете hello сценариев работы с потоками.</span><span class="sxs-lookup"><span data-stu-id="f78fa-128">Verify hello streaming scenarios are working.</span></span>
 4. <span data-ttu-id="f78fa-129">Изменение вторичного ключа учетной записи хранения через портал Azure или командлет powershell hello.</span><span class="sxs-lookup"><span data-stu-id="f78fa-129">Change storage account secondary key through hello powershell cmdlet or Azure portal.</span></span>
 5. <span data-ttu-id="f78fa-130">Вызов powershell AzureRmMediaServiceStorageKeys синхронизации с toopick учетной записи media соответствующие params tooforce копирование новых ключей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="f78fa-130">Call Sync-AzureRmMediaServiceStorageKeys powershell with appropriate params tooforce media account toopick up new storage account keys.</span></span> 
 6. <span data-ttu-id="f78fa-131">Подождите один час или около того.</span><span class="sxs-lookup"><span data-stu-id="f78fa-131">Wait an hour or so.</span></span> <span data-ttu-id="f78fa-132">Убедитесь, что работаете hello сценариев работы с потоками.</span><span class="sxs-lookup"><span data-stu-id="f78fa-132">Verify hello streaming scenarios are working.</span></span>
 
### <a name="a-powershell-cmdlet-example"></a><span data-ttu-id="f78fa-133">Примеры использования командлетов PowerShell</span><span class="sxs-lookup"><span data-stu-id="f78fa-133">A powershell cmdlet example</span></span> 

<span data-ttu-id="f78fa-134">Hello в примере демонстрируется tooget hello учетной записи хранилища и синхронизировать его с учетной записью hello AMS.</span><span class="sxs-lookup"><span data-stu-id="f78fa-134">hello following example demonstrates how tooget hello storage account and sync it with hello AMS account.</span></span>

    $regionName = "West US"
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccountName = "skystorage"
    $storageAccountId = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccountName"

    Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId

 
## <a name="steps-tooadd-storage-accounts-tooyour-ams-account"></a><span data-ttu-id="f78fa-135">Действия tooadd учетных записей хранения tooyour AMS учетной записи</span><span class="sxs-lookup"><span data-stu-id="f78fa-135">Steps tooadd storage accounts tooyour AMS account</span></span>

<span data-ttu-id="f78fa-136">Hello следующем разделе показано, как учетные записи хранения tooadd tooyour AMS учетной записи: [присоединить несколько tooa учетных записей хранилища учетной записи служб мультимедиа](meda-services-managing-multiple-storage-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="f78fa-136">hello following topic shows how tooadd storage accounts tooyour AMS account: [Attach multiple storage accounts tooa Media Services account](meda-services-managing-multiple-storage-accounts.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="f78fa-137">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="f78fa-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f78fa-138">Отзывы</span><span class="sxs-lookup"><span data-stu-id="f78fa-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="f78fa-139">Благодарности</span><span class="sxs-lookup"><span data-stu-id="f78fa-139">Acknowledgments</span></span>
<span data-ttu-id="f78fa-140">Мы хотели бы tooacknowledge hello, выполнив специалистами по созданию этого документа, влияющая: Seva Titov Cenk Dingiloglu, Milan Gada.</span><span class="sxs-lookup"><span data-stu-id="f78fa-140">We would like tooacknowledge hello following people who contributed towards creating this document: Cenk Dingiloglu, Milan Gada, Seva Titov.</span></span>
