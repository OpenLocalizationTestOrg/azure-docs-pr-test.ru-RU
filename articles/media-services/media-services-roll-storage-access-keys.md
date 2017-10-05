---
title: "Обновление служб мультимедиа после оборота ключей доступа к хранилищу | Документация Майкрософт"
description: "В этой статье содержится руководство по обновлению служб мультимедиа после оборота ключей доступа к хранилищу."
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
ms.openlocfilehash: 304e72e0d2d4a7e95df513e6d5481def9eae3f68
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="update-media-services-after-rolling-storage-access-keys"></a><span data-ttu-id="7a2d0-103">Обновление служб мультимедиа после оборота ключей доступа к хранилищу</span><span class="sxs-lookup"><span data-stu-id="7a2d0-103">Update Media Services after rolling storage access keys</span></span>

<span data-ttu-id="7a2d0-104">При создании новой учетной записи служб мультимедиа Azure (AMS) пользователю предлагается выбрать учетную запись хранения Azure, которая используется для хранения мультимедийного содержимого.</span><span class="sxs-lookup"><span data-stu-id="7a2d0-104">When you create a new Azure Media Services (AMS) account, you are also asked to select an Azure Storage account that is used to store your media content.</span></span> <span data-ttu-id="7a2d0-105">К учетной записи служб мультимедиа можно добавить несколько учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="7a2d0-105">You can add more than one storage accounts to your Media Services account.</span></span> <span data-ttu-id="7a2d0-106">В этом разделе показано, как чередовать ключи к хранилищу данных.</span><span class="sxs-lookup"><span data-stu-id="7a2d0-106">This topic shows how to rotate storage keys.</span></span> <span data-ttu-id="7a2d0-107">В нем также показано, как добавлять учетные записи хранения в учетную запись служб мультимедиа.</span><span class="sxs-lookup"><span data-stu-id="7a2d0-107">It also shows how to add storage accounts to a media account.</span></span> 

<span data-ttu-id="7a2d0-108">Чтобы выполнить действия, описанные в этом разделе, необходимо использовать [интерфейсы API ARM](https://docs.microsoft.com/rest/api/media/mediaservice) и [PowerShell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).</span><span class="sxs-lookup"><span data-stu-id="7a2d0-108">To perform the actions described in this topic, you should be using [ARM APIs](https://docs.microsoft.com/rest/api/media/mediaservice) and [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).</span></span>  <span data-ttu-id="7a2d0-109">Дополнительные сведения см. в разделе [Использование Azure PowerShell с диспетчером ресурсов Azure](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="7a2d0-109">For more information, see [How to manage Azure resources with PowerShell and Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

## <a name="overview"></a><span data-ttu-id="7a2d0-110">Обзор</span><span class="sxs-lookup"><span data-stu-id="7a2d0-110">Overview</span></span>

<span data-ttu-id="7a2d0-111">При создании новой учетной записи хранения служба Azure создает два 512-разрядных ключа доступа к хранилищу, используемые для проверки подлинности во время доступа к вашей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="7a2d0-111">When a new storage account is created, Azure generates two 512-bit storage access keys, which are used to authenticate access to your storage account.</span></span> <span data-ttu-id="7a2d0-112">Для безопасности подключений к хранилищу рекомендуется периодически повторно создавать и менять ключи доступа к хранилищу.</span><span class="sxs-lookup"><span data-stu-id="7a2d0-112">To keep your storage connections more secure, it is recommended to periodically regenerate and rotate your storage access key.</span></span> <span data-ttu-id="7a2d0-113">Два ключа доступа (основной и дополнительный) дают возможность поддерживать подключение к учетной записи хранения с помощью одного ключа доступа в то время, как выполняется повторное создание второго ключа доступа.</span><span class="sxs-lookup"><span data-stu-id="7a2d0-113">Two access keys (primary and secondary) are provided in order to enable you to maintain connections to the storage account using one access key while you regenerate the other access key.</span></span> <span data-ttu-id="7a2d0-114">Этот процесс называется "оборот ключей доступа".</span><span class="sxs-lookup"><span data-stu-id="7a2d0-114">This procedure is also called "rolling access keys".</span></span>

<span data-ttu-id="7a2d0-115">Службы мультимедиа зависят от предоставленного ключа к хранилищу данных.</span><span class="sxs-lookup"><span data-stu-id="7a2d0-115">Media Services depends on a storage key provided to it.</span></span> <span data-ttu-id="7a2d0-116">В частности, от ключа доступа к хранилищу зависят указатели, используемые для потоковой передачи или скачивания ресурсов-контейнеров.</span><span class="sxs-lookup"><span data-stu-id="7a2d0-116">Specifically, the locators that are used to stream or download your assets depend on the specified storage access key.</span></span> <span data-ttu-id="7a2d0-117">При создании учетная запись AMS по умолчанию зависит от ключа доступа к основному хранилищу, но пользователь может обновить ключ хранилища в AMS.</span><span class="sxs-lookup"><span data-stu-id="7a2d0-117">When an AMS account is created it takes a dependency on the primary storage access key by default but as a user you can update the storage key that AMS has.</span></span> <span data-ttu-id="7a2d0-118">Необходимо указать службам мультимедиа, какой ключ использовать, выполнив шаги, описанные в данном разделе.</span><span class="sxs-lookup"><span data-stu-id="7a2d0-118">You must make sure to let Media Services know which key to use by following steps described in this topic.</span></span>  

>[!NOTE]
> <span data-ttu-id="7a2d0-119">Если используется несколько учетных записей хранения, необходимо выполнить эту процедуру для каждой из них.</span><span class="sxs-lookup"><span data-stu-id="7a2d0-119">If you have multiple storage accounts, you would perform this procedure with each storage account.</span></span> <span data-ttu-id="7a2d0-120">Порядок, в котором следует чередовать ключи к хранилищу данных, не является фиксированным.</span><span class="sxs-lookup"><span data-stu-id="7a2d0-120">The order in which you rotate storage keys is not fixed.</span></span> <span data-ttu-id="7a2d0-121">Можно сначала сменить вторичный ключ, а затем первичный ключ, или наоборот.</span><span class="sxs-lookup"><span data-stu-id="7a2d0-121">You can rotate the secondary key first and then the primary key or vice versa.</span></span>
>
> <span data-ttu-id="7a2d0-122">Перед выполнением описанных в этом разделе действий с рабочей учетной записью попробуйте выполнить их на подготовительной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="7a2d0-122">Before executing steps described in this topic on a production account, make sure to test them on a pre-production account.</span></span>
>

## <a name="steps-to-rotate-storage-keys"></a><span data-ttu-id="7a2d0-123">Инструкции по чередованию ключей к хранилищу данных</span><span class="sxs-lookup"><span data-stu-id="7a2d0-123">Steps to rotate storage keys</span></span> 
 
 1. <span data-ttu-id="7a2d0-124">Измените первичный ключ учетной записи хранения с помощью командлета PowerShell или портала [Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7a2d0-124">Change the storage account Primary key through the powershell cmdlet or [Azure](https://portal.azure.com/) portal.</span></span>
 2. <span data-ttu-id="7a2d0-125">Вызовите командлет Sync-AzureRmMediaServiceStorageKeys с соответствующими параметрами, чтобы принудительно применить к учетной записи служб мультимедиа ключи учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="7a2d0-125">Call Sync-AzureRmMediaServiceStorageKeys cmdlet with appropriate params to force media account to pick up storage account keys</span></span>
 
    <span data-ttu-id="7a2d0-126">Следующий пример демонстрирует, как синхронизировать ключи с учетными записями хранения.</span><span class="sxs-lookup"><span data-stu-id="7a2d0-126">The following example shows how to sync keys to storage accounts.</span></span>
  
         Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId
  
 3. <span data-ttu-id="7a2d0-127">Подождите один час или около того.</span><span class="sxs-lookup"><span data-stu-id="7a2d0-127">Wait an hour or so.</span></span> <span data-ttu-id="7a2d0-128">Проверьте работу потоковой передачи там, где она используется.</span><span class="sxs-lookup"><span data-stu-id="7a2d0-128">Verify the streaming scenarios are working.</span></span>
 4. <span data-ttu-id="7a2d0-129">Измените вторичный ключ учетной записи хранения с помощью командлета PowerShell или портала Azure.</span><span class="sxs-lookup"><span data-stu-id="7a2d0-129">Change storage account secondary key through the powershell cmdlet or Azure portal.</span></span>
 5. <span data-ttu-id="7a2d0-130">Вызовите командлет PowerShell Sync-AzureRmMediaServiceStorageKeys с соответствующими параметрами, чтобы принудительно применить к учетной записи служб мультимедиа новые ключи учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="7a2d0-130">Call Sync-AzureRmMediaServiceStorageKeys powershell with appropriate params to force media account to pick up new storage account keys.</span></span> 
 6. <span data-ttu-id="7a2d0-131">Подождите один час или около того.</span><span class="sxs-lookup"><span data-stu-id="7a2d0-131">Wait an hour or so.</span></span> <span data-ttu-id="7a2d0-132">Проверьте работу потоковой передачи там, где она используется.</span><span class="sxs-lookup"><span data-stu-id="7a2d0-132">Verify the streaming scenarios are working.</span></span>
 
### <a name="a-powershell-cmdlet-example"></a><span data-ttu-id="7a2d0-133">Примеры использования командлетов PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a2d0-133">A powershell cmdlet example</span></span> 

<span data-ttu-id="7a2d0-134">Ниже приведен пример, демонстрирующий, как получить учетную запись хранилища и синхронизировать ее с учетной записью AMS.</span><span class="sxs-lookup"><span data-stu-id="7a2d0-134">The following example demonstrates how to get the storage account and sync it with the AMS account.</span></span>

    $regionName = "West US"
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccountName = "skystorage"
    $storageAccountId = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccountName"

    Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId

 
## <a name="steps-to-add-storage-accounts-to-your-ams-account"></a><span data-ttu-id="7a2d0-135">Инструкции по добавлению учетных записей хранения в учетную запись AMS</span><span class="sxs-lookup"><span data-stu-id="7a2d0-135">Steps to add storage accounts to your AMS account</span></span>

<span data-ttu-id="7a2d0-136">В следующем разделе показано, как добавить учетные записи хранения в учетную запись AMS: [Управление активами служб мультимедиа в нескольких учетных записях хранения](meda-services-managing-multiple-storage-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="7a2d0-136">The following topic shows how to add storage accounts to your AMS account: [Attach multiple storage accounts to a Media Services account](meda-services-managing-multiple-storage-accounts.md).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="7a2d0-137">Схемы обучения работе со службами мультимедиа</span><span class="sxs-lookup"><span data-stu-id="7a2d0-137">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7a2d0-138">Отзывы</span><span class="sxs-lookup"><span data-stu-id="7a2d0-138">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="7a2d0-139">Благодарности</span><span class="sxs-lookup"><span data-stu-id="7a2d0-139">Acknowledgments</span></span>
<span data-ttu-id="7a2d0-140">Мы выражаем признательность тем, кто помог нам в составлении этого документа, — это Сенк Динджилоглу (Cenk Dingiloglu), Милан Гада (Milan Gada) и Сева Титов.</span><span class="sxs-lookup"><span data-stu-id="7a2d0-140">We would like to acknowledge the following people who contributed towards creating this document: Cenk Dingiloglu, Milan Gada, Seva Titov.</span></span>
