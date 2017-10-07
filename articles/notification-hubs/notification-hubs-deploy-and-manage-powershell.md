---
title: "aaaDeploy и управлять концентраторов уведомлений с помощью PowerShell"
description: "Как tooCreate и управлять уведомления концентраторов с помощью PowerShell для автоматизации"
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 7c58f2c8-0399-42bc-9e1e-a7f073426451
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 8835bdefa0d360354263eab8040259ad08281771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-notification-hubs-using-powershell"></a>Развертывание и управление центров уведомлений с помощью PowerShell
## <a name="overview"></a>Обзор
В этой статье показано, как создать toouse и управлять концентраторов уведомлений Azure, с помощью PowerShell. в этом разделе показаны Hello следующих общих задач автоматизации.

* Создание центра уведомлений
* Настройка учетных данных

Если необходимо также toocreate новое пространство имен служебной шины для концентраторов уведомлений, см. раздел [управление Service Bus с помощью PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).

Управление концентраторы уведомлений не поддерживается напрямую с hello командлетов, включенных с помощью Azure PowerShell. Hello из PowerShell лучше tooreference hello Microsoft.Azure.NotificationHubs.dll сборки. сборки Hello распространяется вместе с hello [пакет NuGet концентраторы уведомлений Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

## <a name="prerequisites"></a>Предварительные требования
Прежде чем приступать к этой статье, необходимо иметь следующие hello:

* Подписка Azure. Azure — это платформа на основе подписок. Дополнительные сведения о получении подписки см. на страницах [Как приобрести Azure], [Предложения для участников] или [Создайте бесплатную учетную запись Azure уже сегодня].
* Компьютер с Azure PowerShell. Инструкции см. в статье [Установка и настройка Azure PowerShell].
* Общее представление о сценарии PowerShell, пакеты NuGet и hello .NET Framework.

## <a name="including-a-reference-toohello-net-assembly-for-service-bus"></a>Включая ссылочную сборку .NET toohello для служебной шины
Управление концентраторов уведомлений Azure еще не входят в состав hello командлеты PowerShell в Azure PowerShell. концентраторы уведомлений tooprovision, вы можете использовать клиент .NET hello в hello [пакет NuGet концентраторы уведомлений Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

Во-первых, убедитесь, что скрипт можно найти hello **Microsoft.Azure.NotificationHubs.dll** сборку, которая устанавливается как пакет NuGet в проект Visual Studio. В toobe порядке гибкие hello скрипт выполняет следующие действия.

1. Определяет путь hello, с которой он вызывается.
2. Перебирает hello пути, пока не найдет папку с именем `packages`. Эта папка создается при установке пакетов NuGet для проектов Visual Studio.
3. Рекурсивный поиск hello `packages` папка для сборки с именем **Microsoft.Azure.NotificationHubs.dll**.
4. Ссылки на hello сборки, чтобы hello типов, доступных для последующего использования.

В сценарии PowerShell эти действия выполняются следующим образом:

``` powershell

try
{
    # WARNING: Make sure tooreference hello latest version of Microsoft.Azure.NotificationHubs.dll
    Write-Output "Adding hello [Microsoft.Azure.NotificationHubs.dll] assembly toohello script..."
    $scriptPath = Split-Path (Get-Variable MyInvocation -Scope 0).Value.MyCommand.Path
    $packagesFolder = (Split-Path $scriptPath -Parent) + "\packages"
    $assembly = Get-ChildItem $packagesFolder -Include "Microsoft.Azure.NotificationHubs.dll" -Recurse
    Add-Type -Path $assembly.FullName

    Write-Output "hello [Microsoft.Azure.NotificationHubs.dll] assembly has been successfully added toohello script."
}

catch [System.Exception]
{
    Write-Error("Could not add hello Microsoft.Azure.NotificationHubs.dll assembly toohello script. Make sure you build hello solution before running hello provisioning script.")
}
```

## <a name="create-hello-namespacemanager-class"></a>Создание класса NamespaceManager hello
tooprovision концентраторов уведомлений, создайте экземпляр класса hello [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) класс из пакета SDK для hello. 

Можно использовать hello [Get AzureSBAuthorizationRule] командлет входящий в состав Azure PowerShell tooretrieve правило авторизации, который использовал tooprovide строку подключения. Мы будем хранить toohello ссылки `NamespaceManager` экземпляра в hello `$NamespaceManager` переменной. Мы будем использовать `$NamespaceManager` tooprovision концентратора уведомлений.

``` powershell
$sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
# Create hello NamespaceManager object toocreate hello hub
Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
$NamespaceManager=[Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."
```


## <a name="provisioning-a-new-notification-hub"></a>Подготовка нового центра уведомлений
новый узел уведомлений tooprovision использовать hello [API .NET для концентраторов уведомлений].

В этой части скрипта hello настроить четыре локальных переменных. 

1. `$Namespace`: Задайте toohello имя пространства имен hello место toocreate концентратора уведомлений.
2. `$Path`: Этот путь toohello имя набора hello новый узел уведомлений.  Например, MyHub.    
3. `$WnsPackageSid`: Укажите этот SID пакета toohello вам приложение Windows из hello [центра разработчиков Windows](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).
4. `$WnsSecretkey`: Укажите этот секретный ключ toohello вам приложение Windows из hello [центра разработчиков Windows](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).

Эти переменные, используемые tooconnect tooyour имен и создайте новый toohandle концентратора уведомлений настроены уведомления Windows Notification Service (WNS) с WNS учетные данные для приложения Windows. Сведения о получении hello пакета SID и секретного ключа см. в разделе hello [Приступая к работе с концентраторами уведомлений](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) учебника. 

* фрагмент кода Hello скрипт использует hello `NamespaceManager` объекта toocheck toosee, если определяется hello концентратора уведомлений `$Path` существует.
* Если он не существует, hello скрипт создает `NotificationHubDescription` с WNS учетные данные и передать этот toohello `NamespaceManager` класса `CreateNotificationHub` метод.

``` powershell

$Namespace = "<Enter your namespace>"
$Path  = "<Enter a name for your notification hub>"
$WnsPackageSid = "<your package sid>"
$WnsSecretkey = "<enter your secret key>"

$WnsCredential = New-Object -TypeName Microsoft.Azure.NotificationHubs.WnsCredential -ArgumentList $WnsPackageSid,$WnsSecretkey

# Query hello namespace
$CurrentNamespace = Get-AzureSBNamespace -Name $Namespace

# Check if hello namespace already exists
if ($CurrentNamespace)
{
    Write-Output "hello namespace [$Namespace] in hello [$($CurrentNamespace.Region)] region was found."

    # Create hello NamespaceManager object used toocreate a new notification hub
    $sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
    Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
    $NamespaceManager = [Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
    Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."

    # Check toosee if hello Notification Hub already exists
    if ($NamespaceManager.NotificationHubExists($Path))
    {
        Write-Output "hello [$Path] notification hub already exists in hello [$Namespace] namespace."  
    }
    else
    {
        Write-Output "Creating hello [$Path] notification hub in hello [$Namespace] namespace."
        $NHDescription = New-Object -TypeName Microsoft.Azure.NotificationHubs.NotificationHubDescription -ArgumentList $Path;
        $NHDescription.WnsCredential = $WnsCredential;
        $NamespaceManager.CreateNotificationHub($NHDescription);
        Write-Output "hello [$Path] notification hub was created in hello [$Namespace] namespace."
    }
}
else
{
    Write-Host "hello [$Namespace] namespace does not exist."
}
```




## <a name="additional-resources"></a>Дополнительные ресурсы
* [Управление служебной шиной с помощью PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md)
* [Как toocreate Service Bus очередей, разделов и подписок с помощью сценария PowerShell](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [Как toocreate в пространство имен служебной шины и концентратор событий с помощью сценария PowerShell](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)

Некоторые готовые сценарии доступны для скачивания:

* [Сценарии PowerShell для Service Bus](https://code.msdn.microsoft.com/windowsazure/Service-Bus-PowerShell-a46b7059)

[Как приобрести Azure]: http://azure.microsoft.com/pricing/purchase-options/
[Предложения для участников]: http://azure.microsoft.com/pricing/member-offers/
[Создайте бесплатную учетную запись Azure уже сегодня]: http://azure.microsoft.com/pricing/free-trial/
[Установка и настройка Azure PowerShell]: /powershell/azureps-cmdlets-docs
[API .NET для концентраторов уведомлений]: https://msdn.microsoft.com/library/azure/mt414893.aspx
[Get-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495122.aspx
[New-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495165.aspx
[Get AzureSBAuthorizationRule]: https://msdn.microsoft.com/library/azure/dn495113.aspx

