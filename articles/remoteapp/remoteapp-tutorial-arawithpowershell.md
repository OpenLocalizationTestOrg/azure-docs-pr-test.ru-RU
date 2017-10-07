---
title: "aaaUse командлеты PowerShell Azure RemoteApp. | Документы Microsoft"
description: "Узнайте, как toouse командлеты Windows PowerShell в Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 7d3d5ded-6f73-4de6-a8ac-c1d622e842a2
ms.service: remoteapp
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: a09cae2093e2c3a4a2ed673b5d148a22ceb935f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a>Использование командлетов Windows PowerShell с Azure RemoteApp
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

 Можно использовать tooadminister командлеты Azure RemoteApp PowerShell hello и поддерживать вашей коллекции. Используйте следующие сведения tooget работы hello.

## <a name="get-hello-cmdlets"></a>Получить командлеты hello
- - -
Сначала загрузить командлеты Azure Powershell hello [здесь](http://go.microsoft.com/?linkid=9811175), командлетов RemoteApp hello включены в нем. 

Извлечение hello [справки по командлетам Azure RemoteApp](/powershell/module/azure?view=azuresmps-3.7.0).

## <a name="configure-azure-cmdlets-toouse-your-subscription"></a>Настроить подписку toouse командлетов Azure
- - -
Выполните [в этом руководстве](/powershell/azure/overview) , можно использовать командлеты hello к подписке Azure.

Можно использовать эти действия tooget, быстро начать работу.

1. Загрузите и установите hello [командлетов Azure PowerShell](http://go.microsoft.com/?linkid=9811175).
2. Запустите Microsoft Azure PowerShell.
3. Запустите **Add-AzureAccount** tooauthenticate tooyour подписки Azure. При появлении запроса введите hello же имя пользователя и пароль, использовать toosign tooAzure портала.  
4. Запустите **Get-AzureSubscription** toolist hello подписок, связанных с вашей учетной записи пользователя. 
5. Запустите **Select-AzureSubscription - SubscriptionName &lt;имя подписки&gt;**  или **Select-AzureSubscription - SubscriptionId &lt;Код_подписки&gt;**  toouse подписки toospecify hello.

Поздравляем, в консоли Azure PowerShell toouse настроен и готов. Имейте в виду, что вам требуется toorepeate шаги 2 – 5 каждый раз при запуске консоли Azure PowerShell hello hello.  


## <a name="list-all-collections"></a>Список всех коллекций
- - -
     Get-AzureRemoteAppCollection

## <a name="delete-a-collection"></a>Удаление коллекции
- - -
    Remove-AzureRemoteAppCollection <enter collection name>

Пример: `Remove-AzureRemoteAppCollection ContosoProduction`.

## <a name="create-a-cloud-collection"></a>Создание облачной коллекции
- - -
Это просто, запустите hello следующую команду:

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

Hello выше команду автоматически публикует приложения Microsoft Office 365 (Excel, OneNote, Outlook, PowerPoint, Visio и Word).

Создание коллекции может занять 30 минут или дольше toocomplete. В связи с этим команда возвращает идентификатор для отслеживания, который можно использовать следующим образом:

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

После завершения hello коллекции можно добавить коллекцию toohello пользователей с hello следующую команду:

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

Готово! Этот пользователь должен быть может tooconnect toohello приложения с помощью клиента Azure RemoteApp hello найден [здесь](https://www.remoteapp.windowsazure.com/).

## <a name="available-cmdlets"></a>Доступные командлеты
Существует множество других команд, которые у нас есть, вскоре будет реализована hello документации для них:

Основные командлеты для коллекций RemoteApp 

* New-AzureRemoteAppCollection
* Get-AzureRemoteAppCollection
* Set-AzureRemoteAppCollection
* Update-AzureRemoteAppCollection
* Remove-AzureRemoteAppCollection
* Add-AzureRemoteAppUser
* Get-AzureRemoteAppUser
* Remove-AzureRemoteAppUser
* Get-AzureRemoteAppSession
* Disconnect-AzureRemoteAppSession
* Invoke-AzureRemoteAppSessionLogoff
* Send-AzureRemoteAppSessionMessage
* Get-AzureRemoteAppProgram
* Get-AzureRemoteAppStartMenuProgram
* Publish-AzureRemoteAppProgram
* Unpublish-AzureRemoteAppProgram
* Get-AzureRemoteAppCollectionUsageDetails
* Get-AzureRemoteAppCollectionUsageSummary
* Get-AzureRemoteAppPlan

Командлеты для виртуальных сетей RemoteApp:

* New-AzureRemoteAppVNet
* Get-AzureRemoteAppVNet
* Set-AzureRemoteAppVNet
* Remove-AzureRemoteAppVNet
* Get-AzureRemoteAppVpnDevice
* Get-- AzureRemoteAppVpnDeviceConfigScript
* Reset-AzureRemoteAppVpnSharedKey

Командлеты для шаблонов образов RemoteApp:

* New-AzureRemoteAppTemplateImage
* Get-AzureRemoteAppTemplateImage
* Rename-AzureRemoteAppTemplateImage
* Remove-AzureRemoteAppTemplateImage

Другие командлеты RemoteApp:

* Get-AzureRemoteAppLocation
* Get-AzureRemoteAppWorkspace
* Set-AzureRemoteAppWorkspace
* Get-AzureRemoteAppOperationResult

