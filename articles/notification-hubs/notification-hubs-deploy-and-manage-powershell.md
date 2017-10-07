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
# <a name="deploy-and-manage-notification-hubs-using-powershell"></a><span data-ttu-id="8c3dc-103">Развертывание и управление центров уведомлений с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c3dc-103">Deploy and Manage Notification Hubs using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="8c3dc-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="8c3dc-104">Overview</span></span>
<span data-ttu-id="8c3dc-105">В этой статье показано, как создать toouse и управлять концентраторов уведомлений Azure, с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-105">This article shows you how toouse Create and Manage Azure Notification Hubs using PowerShell.</span></span> <span data-ttu-id="8c3dc-106">в этом разделе показаны Hello следующих общих задач автоматизации.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-106">hello following common automation tasks are shown in this topic.</span></span>

* <span data-ttu-id="8c3dc-107">Создание центра уведомлений</span><span class="sxs-lookup"><span data-stu-id="8c3dc-107">Create a Notification Hub</span></span>
* <span data-ttu-id="8c3dc-108">Настройка учетных данных</span><span class="sxs-lookup"><span data-stu-id="8c3dc-108">Set Credentials</span></span>

<span data-ttu-id="8c3dc-109">Если необходимо также toocreate новое пространство имен служебной шины для концентраторов уведомлений, см. раздел [управление Service Bus с помощью PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span><span class="sxs-lookup"><span data-stu-id="8c3dc-109">If you also need toocreate a new service bus namespace for your notification hubs, see [Manage Service Bus with PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span></span>

<span data-ttu-id="8c3dc-110">Управление концентраторы уведомлений не поддерживается напрямую с hello командлетов, включенных с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-110">Managing Notifications Hubs is not supported directly by hello cmdlets included with Azure PowerShell.</span></span> <span data-ttu-id="8c3dc-111">Hello из PowerShell лучше tooreference hello Microsoft.Azure.NotificationHubs.dll сборки.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-111">hello best approach from PowerShell is tooreference hello Microsoft.Azure.NotificationHubs.dll assembly.</span></span> <span data-ttu-id="8c3dc-112">сборки Hello распространяется вместе с hello [пакет NuGet концентраторы уведомлений Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="8c3dc-112">hello assembly is distributed with hello [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c3dc-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8c3dc-113">Prerequisites</span></span>
<span data-ttu-id="8c3dc-114">Прежде чем приступать к этой статье, необходимо иметь следующие hello:</span><span class="sxs-lookup"><span data-stu-id="8c3dc-114">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="8c3dc-115">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-115">An Azure subscription.</span></span> <span data-ttu-id="8c3dc-116">Azure — это платформа на основе подписок.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-116">Azure is a subscription-based platform.</span></span> <span data-ttu-id="8c3dc-117">Дополнительные сведения о получении подписки см. на страницах [Как приобрести Azure], [Предложения для участников] или [Создайте бесплатную учетную запись Azure уже сегодня].</span><span class="sxs-lookup"><span data-stu-id="8c3dc-117">For more information about obtaining a subscription, see [Purchase Options], [Member Offers], or [Free Trial].</span></span>
* <span data-ttu-id="8c3dc-118">Компьютер с Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-118">A computer with Azure PowerShell.</span></span> <span data-ttu-id="8c3dc-119">Инструкции см. в статье [Установка и настройка Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="8c3dc-119">For instructions, see [Install and configure Azure PowerShell].</span></span>
* <span data-ttu-id="8c3dc-120">Общее представление о сценарии PowerShell, пакеты NuGet и hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-120">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="including-a-reference-toohello-net-assembly-for-service-bus"></a><span data-ttu-id="8c3dc-121">Включая ссылочную сборку .NET toohello для служебной шины</span><span class="sxs-lookup"><span data-stu-id="8c3dc-121">Including a reference toohello .NET assembly for Service Bus</span></span>
<span data-ttu-id="8c3dc-122">Управление концентраторов уведомлений Azure еще не входят в состав hello командлеты PowerShell в Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-122">Managing Azure Notification Hubs is not yet included with hello PowerShell cmdlets in Azure PowerShell.</span></span> <span data-ttu-id="8c3dc-123">концентраторы уведомлений tooprovision, вы можете использовать клиент .NET hello в hello [пакет NuGet концентраторы уведомлений Microsoft Azure](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="8c3dc-123">tooprovision notification hubs, you can use hello .NET client provided in hello [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="8c3dc-124">Во-первых, убедитесь, что скрипт можно найти hello **Microsoft.Azure.NotificationHubs.dll** сборку, которая устанавливается как пакет NuGet в проект Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-124">First, make sure your script can locate hello **Microsoft.Azure.NotificationHubs.dll** assembly, which is installed as a NuGet package in a Visual Studio project.</span></span> <span data-ttu-id="8c3dc-125">В toobe порядке гибкие hello скрипт выполняет следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-125">In order toobe flexible, hello script performs these steps:</span></span>

1. <span data-ttu-id="8c3dc-126">Определяет путь hello, с которой он вызывается.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-126">Determines hello path at which it was invoked.</span></span>
2. <span data-ttu-id="8c3dc-127">Перебирает hello пути, пока не найдет папку с именем `packages`.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-127">Traverses hello path until it finds a folder named `packages`.</span></span> <span data-ttu-id="8c3dc-128">Эта папка создается при установке пакетов NuGet для проектов Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-128">This folder is created when you install NuGet packages for Visual Studio projects.</span></span>
3. <span data-ttu-id="8c3dc-129">Рекурсивный поиск hello `packages` папка для сборки с именем **Microsoft.Azure.NotificationHubs.dll**.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-129">Recursively searches hello `packages` folder for an assembly named **Microsoft.Azure.NotificationHubs.dll**.</span></span>
4. <span data-ttu-id="8c3dc-130">Ссылки на hello сборки, чтобы hello типов, доступных для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-130">References hello assembly so that hello types are available for later use.</span></span>

<span data-ttu-id="8c3dc-131">В сценарии PowerShell эти действия выполняются следующим образом:</span><span class="sxs-lookup"><span data-stu-id="8c3dc-131">Here's how these steps are implemented in a PowerShell script:</span></span>

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

## <a name="create-hello-namespacemanager-class"></a><span data-ttu-id="8c3dc-132">Создание класса NamespaceManager hello</span><span class="sxs-lookup"><span data-stu-id="8c3dc-132">Create hello NamespaceManager class</span></span>
<span data-ttu-id="8c3dc-133">tooprovision концентраторов уведомлений, создайте экземпляр класса hello [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) класс из пакета SDK для hello.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-133">tooprovision Notification Hubs, create an instance of hello [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) class from hello SDK.</span></span> 

<span data-ttu-id="8c3dc-134">Можно использовать hello [Get AzureSBAuthorizationRule] командлет входящий в состав Azure PowerShell tooretrieve правило авторизации, который использовал tooprovide строку подключения.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-134">You can use hello [Get-AzureSBAuthorizationRule] cmdlet included with Azure PowerShell tooretrieve an authorization rule that's used tooprovide a connection string.</span></span> <span data-ttu-id="8c3dc-135">Мы будем хранить toohello ссылки `NamespaceManager` экземпляра в hello `$NamespaceManager` переменной.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-135">We'll store a reference toohello `NamespaceManager` instance in hello `$NamespaceManager` variable.</span></span> <span data-ttu-id="8c3dc-136">Мы будем использовать `$NamespaceManager` tooprovision концентратора уведомлений.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-136">We will use `$NamespaceManager` tooprovision a notification hub.</span></span>

``` powershell
$sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
# Create hello NamespaceManager object toocreate hello hub
Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
$NamespaceManager=[Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."
```


## <a name="provisioning-a-new-notification-hub"></a><span data-ttu-id="8c3dc-137">Подготовка нового центра уведомлений</span><span class="sxs-lookup"><span data-stu-id="8c3dc-137">Provisioning a new Notification Hub</span></span>
<span data-ttu-id="8c3dc-138">новый узел уведомлений tooprovision использовать hello [API .NET для концентраторов уведомлений].</span><span class="sxs-lookup"><span data-stu-id="8c3dc-138">tooprovision a new notification hub, use hello [.NET API for Notification Hubs].</span></span>

<span data-ttu-id="8c3dc-139">В этой части скрипта hello настроить четыре локальных переменных.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-139">In this part of hello script you set up four local variables.</span></span> 

1. <span data-ttu-id="8c3dc-140">`$Namespace`: Задайте toohello имя пространства имен hello место toocreate концентратора уведомлений.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-140">`$Namespace` : Set this toohello name of hello namespace where you want toocreate a notification hub.</span></span>
2. <span data-ttu-id="8c3dc-141">`$Path`: Этот путь toohello имя набора hello новый узел уведомлений.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-141">`$Path` : Set this path toohello name of hello new notification hub.</span></span>  <span data-ttu-id="8c3dc-142">Например, MyHub.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-142">For example, "MyHub".</span></span>    
3. <span data-ttu-id="8c3dc-143">`$WnsPackageSid`: Укажите этот SID пакета toohello вам приложение Windows из hello [центра разработчиков Windows](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="8c3dc-143">`$WnsPackageSid` : Set this toohello package SID for you Windows App from hello [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>
4. <span data-ttu-id="8c3dc-144">`$WnsSecretkey`: Укажите этот секретный ключ toohello вам приложение Windows из hello [центра разработчиков Windows](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="8c3dc-144">`$WnsSecretkey`: Set this toohello secret key for you Windows App from hello [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>

<span data-ttu-id="8c3dc-145">Эти переменные, используемые tooconnect tooyour имен и создайте новый toohandle концентратора уведомлений настроены уведомления Windows Notification Service (WNS) с WNS учетные данные для приложения Windows.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-145">These variables are used tooconnect tooyour namespace and create a new Notification Hub configured toohandle Windows Notification Services (WNS) notifications with WNS credentials for a Windows App.</span></span> <span data-ttu-id="8c3dc-146">Сведения о получении hello пакета SID и секретного ключа см. в разделе hello [Приступая к работе с концентраторами уведомлений](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-146">For information on obtaining hello package SID and secret key see, hello [Getting Started with Notification Hubs](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span> 

* <span data-ttu-id="8c3dc-147">фрагмент кода Hello скрипт использует hello `NamespaceManager` объекта toocheck toosee, если определяется hello концентратора уведомлений `$Path` существует.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-147">hello script snippet uses hello `NamespaceManager` object toocheck toosee if hello Notification Hub identified by `$Path` exists.</span></span>
* <span data-ttu-id="8c3dc-148">Если он не существует, hello скрипт создает `NotificationHubDescription` с WNS учетные данные и передать этот toohello `NamespaceManager` класса `CreateNotificationHub` метод.</span><span class="sxs-lookup"><span data-stu-id="8c3dc-148">If it does not exist, hello script will create an `NotificationHubDescription` with WNS credentials and pass that toohello `NamespaceManager` class `CreateNotificationHub` method.</span></span>

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




## <a name="additional-resources"></a><span data-ttu-id="8c3dc-149">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8c3dc-149">Additional Resources</span></span>
* [<span data-ttu-id="8c3dc-150">Управление служебной шиной с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c3dc-150">Manage Service Bus with PowerShell</span></span>](../service-bus-messaging/service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="8c3dc-151">Как toocreate Service Bus очередей, разделов и подписок с помощью сценария PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c3dc-151">How toocreate Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="8c3dc-152">Как toocreate в пространство имен служебной шины и концентратор событий с помощью сценария PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c3dc-152">How toocreate a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)

<span data-ttu-id="8c3dc-153">Некоторые готовые сценарии доступны для скачивания:</span><span class="sxs-lookup"><span data-stu-id="8c3dc-153">Some ready-made scripts are also available for download:</span></span>

* [<span data-ttu-id="8c3dc-154">Сценарии PowerShell для Service Bus</span><span class="sxs-lookup"><span data-stu-id="8c3dc-154">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/windowsazure/Service-Bus-PowerShell-a46b7059)

[Как приобрести Azure]: http://azure.microsoft.com/pricing/purchase-options/
[Предложения для участников]: http://azure.microsoft.com/pricing/member-offers/
[Создайте бесплатную учетную запись Azure уже сегодня]: http://azure.microsoft.com/pricing/free-trial/
[Установка и настройка Azure PowerShell]: /powershell/azureps-cmdlets-docs
[API .NET для концентраторов уведомлений]: https://msdn.microsoft.com/library/azure/mt414893.aspx
[Get-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495122.aspx
[New-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495165.aspx
[Get AzureSBAuthorizationRule]: https://msdn.microsoft.com/library/azure/dn495113.aspx

