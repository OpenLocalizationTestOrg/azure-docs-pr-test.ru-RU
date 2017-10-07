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
# <a name="update-media-services-after-rolling-storage-access-keys"></a>Обновление служб мультимедиа после оборота ключей доступа к хранилищу

При создании новой учетной записи служб мультимедиа Azure (AMS), также предлагается tooselect учетной записи хранилища Azure, то есть использовать toostore мультимедийного содержимого. Можно добавить несколько tooyour учетных записей хранилища учетной записи служб мультимедиа. В этом разделе показано, как toorotate хранилища ключей. Здесь также показано, как учетные записи хранения tooadd учетной записи tooa мультимедиа. 

tooperform hello действия, описанные в этом разделе, вы должны использовать [API-интерфейсы ARM](https://docs.microsoft.com/rest/api/media/mediaservice) и [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).  Дополнительные сведения см. в разделе [как toomanage Azure ресурсы с помощью PowerShell и диспетчера ресурсов](../azure-resource-manager/powershell-azure-resource-manager.md).

## <a name="overview"></a>Обзор

При создании новой учетной записи хранения Azure создает два 512-разрядных ключа доступа, являющиеся используется tooauthenticate доступ к учетной записи хранилища tooyour. tookeep безопаснее, рекомендуется tooperiodically вашего подключения к хранилищу повторно создать и сменить ваш ключ доступа хранилища. Предоставляются в порядке tooenable toomaintain подключений toohello учетной записи хранилища с помощью одного доступ к ключу при повторном создании hello другого ключа доступа, два ключа доступа (первичная и Вторичная). Этот процесс называется "оборот ключей доступа".

Службы мультимедиа зависит от ключа хранилища, предоставляемые tooit. В частности hello указатели, которые используется toostream или загрузить активов зависят от ключа доступа hello указанное хранилище. При создании учетной записи AMS он зависит от ключа доступа hello основного хранилища по умолчанию, но имени пользователя можно обновить ключ хранилища hello с AMS. Необходимо убедиться, что toolet Media Services известны какие toouse ключа, выполнив действия, описанные в этом разделе.  

>[!NOTE]
> Если используется несколько учетных записей хранения, необходимо выполнить эту процедуру для каждой из них. Hello порядок, в котором вы смена ключей хранилища не является фиксированным. Можно сначала поворот hello вторичного ключа и затем hello первичного ключа или наоборот.
>
> Перед выполнением действия описанные в этом разделе для рабочей учетной записи, убедитесь, что tootest их с подготовительной учетной записи.
>

## <a name="steps-toorotate-storage-keys"></a>Действия toorotate хранилища ключей 
 
 1. Изменение hello ключ учетной записи хранения основной посредством командлета powershell hello или [Azure](https://portal.azure.com/) портала.
 2. Вызовите командлет AzureRmMediaServiceStorageKeys синхронизации с toopick учетной записи media соответствующие params tooforce копирование ключи учетной записи хранения
 
    Hello в следующем примере показано, как toosync ключей toostorage учетные записи.
  
         Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId
  
 3. Подождите один час или около того. Убедитесь, что работаете hello сценариев работы с потоками.
 4. Изменение вторичного ключа учетной записи хранения через портал Azure или командлет powershell hello.
 5. Вызов powershell AzureRmMediaServiceStorageKeys синхронизации с toopick учетной записи media соответствующие params tooforce копирование новых ключей учетной записи хранилища. 
 6. Подождите один час или около того. Убедитесь, что работаете hello сценариев работы с потоками.
 
### <a name="a-powershell-cmdlet-example"></a>Примеры использования командлетов PowerShell 

Hello в примере демонстрируется tooget hello учетной записи хранилища и синхронизировать его с учетной записью hello AMS.

    $regionName = "West US"
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccountName = "skystorage"
    $storageAccountId = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccountName"

    Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId

 
## <a name="steps-tooadd-storage-accounts-tooyour-ams-account"></a>Действия tooadd учетных записей хранения tooyour AMS учетной записи

Hello следующем разделе показано, как учетные записи хранения tooadd tooyour AMS учетной записи: [присоединить несколько tooa учетных записей хранилища учетной записи служб мультимедиа](meda-services-managing-multiple-storage-accounts.md).

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a>Благодарности
Мы хотели бы tooacknowledge hello, выполнив специалистами по созданию этого документа, влияющая: Seva Titov Cenk Dingiloglu, Milan Gada.
