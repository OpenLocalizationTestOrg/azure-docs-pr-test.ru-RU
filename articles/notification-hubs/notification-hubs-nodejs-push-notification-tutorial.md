---
title: "aaaSending push-уведомлений с концентраторами уведомлений Azure и Node.js"
description: "Узнайте, как toosend toouse концентраторы уведомлений push-уведомления из приложения Node.js."
keywords: "push-уведомление, push-уведомления, push-уведомления node.js, push-уведомления ios"
services: notification-hubs
documentationcenter: nodejs
author: ysxu
manager: erikre
editor: 
ms.assetid: ded4749c-6c39-4ff8-b2cf-1927b3e92f93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 10/25/2016
ms.author: yuaxu
ms.openlocfilehash: 151d224fa6dd07e4acdc3a4887c4e95ee03168c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a><span data-ttu-id="f57f5-104">Отправка push-уведомлений с помощью Центров уведомлений Azure и Node.js</span><span class="sxs-lookup"><span data-stu-id="f57f5-104">Sending push notifications with Azure Notification Hubs and Node.js</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a><span data-ttu-id="f57f5-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="f57f5-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f57f5-106">toocomplete этого учебника необходимо иметь активную учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="f57f5-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="f57f5-107">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="f57f5-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f57f5-108">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span><span class="sxs-lookup"><span data-stu-id="f57f5-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span></span>
> 
> 

<span data-ttu-id="f57f5-109">В этом руководстве будет показано, как toosend push-уведомления с помощью hello концентраторов уведомлений Azure непосредственно из приложения Node.js.</span><span class="sxs-lookup"><span data-stu-id="f57f5-109">This guide will show you how toosend push notifications with hello help of Azure Notification Hubs directly from a Node.js application.</span></span> 

<span data-ttu-id="f57f5-110">Hello сценарии включают, отправка уведомлений tooapplications принудительной на следующих платформах hello:</span><span class="sxs-lookup"><span data-stu-id="f57f5-110">hello scenarios covered include sending push notifications tooapplications on hello following platforms:</span></span>

* <span data-ttu-id="f57f5-111">Android</span><span class="sxs-lookup"><span data-stu-id="f57f5-111">Android</span></span>
* <span data-ttu-id="f57f5-112">iOS</span><span class="sxs-lookup"><span data-stu-id="f57f5-112">iOS</span></span>
* <span data-ttu-id="f57f5-113">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="f57f5-113">Windows Phone</span></span>
* <span data-ttu-id="f57f5-114">Универсальные приложения Windows</span><span class="sxs-lookup"><span data-stu-id="f57f5-114">Universal Windows Platform</span></span> 

<span data-ttu-id="f57f5-115">Дополнительные сведения о концентраторах уведомлений см. в разделе hello [дальнейшие действия](#next) раздела.</span><span class="sxs-lookup"><span data-stu-id="f57f5-115">For more information on notification hubs, see hello [Next Steps](#next) section.</span></span>

## <a name="what-are-notification-hubs"></a><span data-ttu-id="f57f5-116">Что такое концентраторы уведомлений</span><span class="sxs-lookup"><span data-stu-id="f57f5-116">What are Notification Hubs?</span></span>
<span data-ttu-id="f57f5-117">Концентраторы уведомлений Azure предоставляют простой в использовании мультиплатформенную, масштабируемую инфраструктуру для Отправка push-уведомления toomobile устройств.</span><span class="sxs-lookup"><span data-stu-id="f57f5-117">Azure Notification Hubs provide an easy-to-use, multi-platform, scalable infrastructure for sending push notifications toomobile devices.</span></span> <span data-ttu-id="f57f5-118">В инфраструктуре службы hello подробнее hello [концентраторов уведомлений Azure](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) страницы.</span><span class="sxs-lookup"><span data-stu-id="f57f5-118">For details on hello service infrastructure, see hello [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) page.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="f57f5-119">Создание приложения Node.js</span><span class="sxs-lookup"><span data-stu-id="f57f5-119">Create a Node.js Application</span></span>
<span data-ttu-id="f57f5-120">Hello первым шагом в этом учебнике используется для создания нового пустого приложения Node.js.</span><span class="sxs-lookup"><span data-stu-id="f57f5-120">hello first step in this tutorial is creating a new blank Node.js application.</span></span> <span data-ttu-id="f57f5-121">Инструкции по созданию приложений Node.js см. в разделе [создать и развернуть tooAzure приложений Node.js веб-сайт][nodejswebsite], [Node.js облачной службы] [ Node.js Cloud Service] с помощью Windows PowerShell или [веб-сайт в WebMatrix].</span><span class="sxs-lookup"><span data-stu-id="f57f5-121">For instructions on creating a Node.js application, see [Create and deploy a Node.js application tooAzure Web Site][nodejswebsite], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or [Web Site with WebMatrix].</span></span>

## <a name="configure-your-application-toouse-notification-hubs"></a><span data-ttu-id="f57f5-122">Настройка концентраторов уведомлений tooUse приложения</span><span class="sxs-lookup"><span data-stu-id="f57f5-122">Configure Your Application tooUse Notification Hubs</span></span>
<span data-ttu-id="f57f5-123">toouse концентраторов уведомлений Azure требуются toodownload и используйте hello Node.js [пакеты azure](https://www.npmjs.com/package/azure), включая встроенный набор вспомогательных библиотек, взаимодействующих со службами REST уведомлений push hello.</span><span class="sxs-lookup"><span data-stu-id="f57f5-123">toouse Azure Notification Hubs, you need toodownload and use hello Node.js [azure package](https://www.npmjs.com/package/azure), which includes a built-in set of helper libraries that communicate with hello push notification REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="f57f5-124">С помощью диспетчера пакетов узла (NPM) tooobtain hello пакета</span><span class="sxs-lookup"><span data-stu-id="f57f5-124">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="f57f5-125">Использовать интерфейс командной строки, такие как **PowerShell** (Windows), **терминалов** (Mac), или **Bash** (Linux) и перейдите в папку toohello, где создан пустого приложения .</span><span class="sxs-lookup"><span data-stu-id="f57f5-125">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Linux) and navigate toohello folder where you created your blank application.</span></span>
2. <span data-ttu-id="f57f5-126">Тип **npm установить azure sb** в командном окне приветствия.</span><span class="sxs-lookup"><span data-stu-id="f57f5-126">Type **npm install azure-sb** in hello command window.</span></span>
3. <span data-ttu-id="f57f5-127">Вы можете вручную запустить hello **ls** или **dir** tooverify команды, **узел\_модули** папка была создана.</span><span class="sxs-lookup"><span data-stu-id="f57f5-127">You can manually run hello **ls** or **dir** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="f57f5-128">В этой папке найти hello **azure** пакет, который содержит необходимые tooaccess библиотеки hello hello концентратора уведомлений.</span><span class="sxs-lookup"><span data-stu-id="f57f5-128">Inside that folder, find hello **azure** package, which contains hello libraries you need tooaccess hello Notification Hub.</span></span>

> [!NOTE]
> <span data-ttu-id="f57f5-129">Дополнительные сведения об установке на официальные hello NPM [NPM блог](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span><span class="sxs-lookup"><span data-stu-id="f57f5-129">You can learn more about installing NPM on hello official [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span></span> 
> 
> 

### <a name="import-hello-module"></a><span data-ttu-id="f57f5-130">Импорт модуля hello</span><span class="sxs-lookup"><span data-stu-id="f57f5-130">Import hello module</span></span>
<span data-ttu-id="f57f5-131">В текстовом редакторе, добавьте следующие toohello вверху hello hello **server.js** файл приложения hello:</span><span class="sxs-lookup"><span data-stu-id="f57f5-131">Using a text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a><span data-ttu-id="f57f5-132">Настройка подключения концентратора уведомлений Azure</span><span class="sxs-lookup"><span data-stu-id="f57f5-132">Setup an Azure Notification Hub connection</span></span>
<span data-ttu-id="f57f5-133">Hello **NotificationHubService** объектов позволяет работать с концентраторами уведомлений.</span><span class="sxs-lookup"><span data-stu-id="f57f5-133">hello **NotificationHubService** object lets you work with notification hubs.</span></span> <span data-ttu-id="f57f5-134">Hello следующий код создает **NotificationHubService** объект с именем концентратора nofication hello **hubname**.</span><span class="sxs-lookup"><span data-stu-id="f57f5-134">hello following code creates a **NotificationHubService** object for hello nofication hub named **hubname**.</span></span> <span data-ttu-id="f57f5-135">Добавьте его вверху hello hello **server.js** файла после tooimport hello azure hello инструкции модуля:</span><span class="sxs-lookup"><span data-stu-id="f57f5-135">Add it near hello top of hello **server.js** file, after hello statement tooimport hello azure module:</span></span>

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

<span data-ttu-id="f57f5-136">Здравствуйте, подключение **connectionstring** значение можно получить из hello [портала Azure] , выполнив следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="f57f5-136">hello connection **connectionstring** value can be obtained from hello [Azure Portal] by performing hello following steps:</span></span>

1. <span data-ttu-id="f57f5-137">Hello панели навигации слева щелкните **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="f57f5-137">In hello left navigation pane, click **Browse**.</span></span>
2. <span data-ttu-id="f57f5-138">Выберите **концентраторы уведомлений**, затем найти hello-концентратор и вы хотите toouse для образца hello.</span><span class="sxs-lookup"><span data-stu-id="f57f5-138">Select **Notification Hubs**, and then find hello hub you wish toouse for hello sample.</span></span> <span data-ttu-id="f57f5-139">Можно ссылаться toohello [Приступая к работе Windows Store учебника](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) Если вам нужна помощь при создании нового концентратора уведомлений.</span><span class="sxs-lookup"><span data-stu-id="f57f5-139">You can refer toohello [Windows Store Getting Started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) if you need help creating a new Notification Hub.</span></span>
3. <span data-ttu-id="f57f5-140">Выберите элемент **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="f57f5-140">Select **Settings**.</span></span>
4. <span data-ttu-id="f57f5-141">Щелкните **Политики доступа**.</span><span class="sxs-lookup"><span data-stu-id="f57f5-141">Click on **Access Policies**.</span></span> <span data-ttu-id="f57f5-142">Вы увидите строки подключения как для общего, так и для полного доступа.</span><span class="sxs-lookup"><span data-stu-id="f57f5-142">You will see both shared and full access connection strings.</span></span>

![Портал Azure — центры уведомлений](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> <span data-ttu-id="f57f5-144">Вы также можете получить hello строки соединения, использующей hello **Get-AzureSbNamespace** командлета, предоставляемые [Azure PowerShell](/powershell/azureps-cmdlets-docs) или hello **Показать пространства имен azure sb** с Hello [интерфейса командной строки Azure (Azure CLI)](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f57f5-144">You can also retrieve hello connection string using hello **Get-AzureSbNamespace** cmdlet provided by [Azure PowerShell](/powershell/azureps-cmdlets-docs) or hello **azure sb namespace show** command with hello [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md).</span></span>
> 
> 

## <a name="general-architecture"></a><span data-ttu-id="f57f5-145">Общая архитектура</span><span class="sxs-lookup"><span data-stu-id="f57f5-145">General architecture</span></span>
<span data-ttu-id="f57f5-146">Hello **NotificationHubService** объект предоставляет следующие экземпляры объекта для отправки push уведомления toospecific устройства и приложения hello:</span><span class="sxs-lookup"><span data-stu-id="f57f5-146">hello **NotificationHubService** object exposes hello following object instances for sending push notifications toospecific devices and applications:</span></span>

* <span data-ttu-id="f57f5-147">**Android** -использовать hello **GcmService** объекта, который доступен на **notificationHubService.gcm**</span><span class="sxs-lookup"><span data-stu-id="f57f5-147">**Android** - use hello **GcmService** object, which is available at **notificationHubService.gcm**</span></span>
* <span data-ttu-id="f57f5-148">**iOS** -использовать hello **ApnsService** объекта, который доступен по **notificationHubService.apns**</span><span class="sxs-lookup"><span data-stu-id="f57f5-148">**iOS** - use hello **ApnsService** object, which is accessible at **notificationHubService.apns**</span></span>
* <span data-ttu-id="f57f5-149">**Windows Phone** -использовать hello **MpnsService** объекта, который доступен на **notificationHubService.mpns**</span><span class="sxs-lookup"><span data-stu-id="f57f5-149">**Windows Phone** - use hello **MpnsService** object, which is available at **notificationHubService.mpns**</span></span>
* <span data-ttu-id="f57f5-150">**Универсальная платформа Windows** -использовать hello **WnsService** объекта, который доступен на **notificationHubService.wns**</span><span class="sxs-lookup"><span data-stu-id="f57f5-150">**Universal Windows Platform** - use hello **WnsService** object, which is available at **notificationHubService.wns**</span></span>

### <a name="how-to-send-push-notifications-tooandroid-applications"></a><span data-ttu-id="f57f5-151">Как: отправлять push уведомления tooAndroid приложения</span><span class="sxs-lookup"><span data-stu-id="f57f5-151">How to: Send push notifications tooAndroid applications</span></span>
<span data-ttu-id="f57f5-152">Hello **GcmService** объект предоставляет **отправки** метод, который может быть используется toosend принудительной уведомления tooAndroid приложений.</span><span class="sxs-lookup"><span data-stu-id="f57f5-152">hello **GcmService** object provides a **send** method that can be used toosend push notifications tooAndroid applications.</span></span> <span data-ttu-id="f57f5-153">Hello **отправки** метод принимает hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="f57f5-153">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="f57f5-154">**Теги** -hello идентификатор тега.</span><span class="sxs-lookup"><span data-stu-id="f57f5-154">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="f57f5-155">Если ни один тег, hello уведомления будут отправляться tooall клиентов.</span><span class="sxs-lookup"><span data-stu-id="f57f5-155">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="f57f5-156">**Полезные данные** -hello JSON или необработанные строковые полезные данные сообщения.</span><span class="sxs-lookup"><span data-stu-id="f57f5-156">**Payload** - hello message's JSON or raw string payload.</span></span>
* <span data-ttu-id="f57f5-157">**Обратный вызов** -hello функции обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="f57f5-157">**Callback** - hello callback function.</span></span>

<span data-ttu-id="f57f5-158">Дополнительные сведения о формате полезных данных hello см. в разделе hello **полезных данных** раздел hello [реализация сервера GCM](http://developer.android.com/google/gcm/server.html#payload) документа.</span><span class="sxs-lookup"><span data-stu-id="f57f5-158">For more information on hello payload format, see hello **Payload** section of hello [Implementing GCM Server](http://developer.android.com/google/gcm/server.html#payload) document.</span></span>

<span data-ttu-id="f57f5-159">Hello следующий код использует hello **GcmService** экземпляра, предоставляемые hello **NotificationHubService** toosend tooall уведомления принудительной регистрации клиентов.</span><span class="sxs-lookup"><span data-stu-id="f57f5-159">hello following code uses hello **GcmService** instance exposed by hello **NotificationHubService** toosend a push notification tooall registered clients.</span></span>

    var payload = {
      data: {
        message: 'Hello!'
      }
    };
    notificationHubService.gcm.send(null, payload, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-tooios-applications"></a><span data-ttu-id="f57f5-160">Как: отправлять push уведомления tooiOS приложения</span><span class="sxs-lookup"><span data-stu-id="f57f5-160">How to: Send push notifications tooiOS applications</span></span>
<span data-ttu-id="f57f5-161">Таким же как и для приложений Android, описанной выше, hello **ApnsService** объект предоставляет **отправки** метод, который может быть используется toosend принудительной уведомления tooiOS приложений.</span><span class="sxs-lookup"><span data-stu-id="f57f5-161">Same as with Android applications described above, hello **ApnsService** object provides a **send** method that can be used toosend push notifications tooiOS applications.</span></span> <span data-ttu-id="f57f5-162">Hello **отправки** метод принимает hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="f57f5-162">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="f57f5-163">**Теги** -hello идентификатор тега.</span><span class="sxs-lookup"><span data-stu-id="f57f5-163">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="f57f5-164">Если ни один тег, hello уведомления будут отправляться tooall клиентов.</span><span class="sxs-lookup"><span data-stu-id="f57f5-164">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="f57f5-165">**Полезные данные** - hello сообщения JSON или строки полезных данных.</span><span class="sxs-lookup"><span data-stu-id="f57f5-165">**Payload** - hello message's JSON or string payload.</span></span>
* <span data-ttu-id="f57f5-166">**Обратный вызов** -hello функции обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="f57f5-166">**Callback** - hello callback function.</span></span>

<span data-ttu-id="f57f5-167">Дополнительные сведения о формате hello полезных данных. в разделе hello **полезные данные уведомления** раздел hello [локальный и Push-уведомлений руководство по программированию на](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) документа.</span><span class="sxs-lookup"><span data-stu-id="f57f5-167">For more information hello payload format, see hello **Notification Payload** section of hello [Local and Push Notification Programming Guide](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) document.</span></span>

<span data-ttu-id="f57f5-168">Hello следующий код использует hello **ApnsService** экземпляра, предоставляемые hello **NotificationHubService** toosend оповещение сообщения tooall клиентов:</span><span class="sxs-lookup"><span data-stu-id="f57f5-168">hello following code uses hello **ApnsService** instance exposed by hello **NotificationHubService** toosend an alert message tooall clients:</span></span>

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-toowindows-phone-applications"></a><span data-ttu-id="f57f5-169">Как: отправлять push приложения телефона tooWindows уведомления</span><span class="sxs-lookup"><span data-stu-id="f57f5-169">How to: Send push notifications tooWindows Phone applications</span></span>
<span data-ttu-id="f57f5-170">Hello **MpnsService** объект предоставляет **отправки** метод, который может быть tooWindows уведомлений используется toosend принудительной телефонных приложений.</span><span class="sxs-lookup"><span data-stu-id="f57f5-170">hello **MpnsService** object provides a **send** method that can be used toosend push notifications tooWindows Phone applications.</span></span> <span data-ttu-id="f57f5-171">Hello **отправки** метод принимает hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="f57f5-171">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="f57f5-172">**Теги** -hello идентификатор тега.</span><span class="sxs-lookup"><span data-stu-id="f57f5-172">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="f57f5-173">Если ни один тег, hello уведомления будут отправляться tooall клиентов.</span><span class="sxs-lookup"><span data-stu-id="f57f5-173">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="f57f5-174">**Полезные данные** -hello полезные данные сообщения XML.</span><span class="sxs-lookup"><span data-stu-id="f57f5-174">**Payload** - hello message's XML payload.</span></span>
* <span data-ttu-id="f57f5-175">**TargetName** - `toast` — уведомлений во всплывающем окне.</span><span class="sxs-lookup"><span data-stu-id="f57f5-175">**TargetName** - `toast` for toast notifications.</span></span> <span data-ttu-id="f57f5-176">`token` для уведомлений на плитке.</span><span class="sxs-lookup"><span data-stu-id="f57f5-176">`token` for tile notifications.</span></span>
* <span data-ttu-id="f57f5-177">**NotificationClass** -hello приоритет hello уведомления.</span><span class="sxs-lookup"><span data-stu-id="f57f5-177">**NotificationClass** - hello priority of hello notification.</span></span> <span data-ttu-id="f57f5-178">. В разделе hello **элементов заголовка HTTP** раздел hello [Push-уведомления с сервера](http://msdn.microsoft.com/library/hh221551.aspx) документа для допустимых значений.</span><span class="sxs-lookup"><span data-stu-id="f57f5-178">See hello **HTTP Header Elements** section of hello [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) document for valid values.</span></span>
* <span data-ttu-id="f57f5-179">**Options** — необязательные заголовки запроса.</span><span class="sxs-lookup"><span data-stu-id="f57f5-179">**Options** - optional request headers.</span></span>
* <span data-ttu-id="f57f5-180">**Обратный вызов** -hello функции обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="f57f5-180">**Callback** - hello callback function.</span></span>

<span data-ttu-id="f57f5-181">Список допустимых **TargetName**, **NotificationClass** параметры заголовка, извлечение и возврат hello [Push-уведомления с сервера](http://msdn.microsoft.com/library/hh221551.aspx) страницы.</span><span class="sxs-lookup"><span data-stu-id="f57f5-181">For a list of valid **TargetName**, **NotificationClass** and header options, check out hello [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) page.</span></span>

<span data-ttu-id="f57f5-182">Hello, следующий пример кода использует hello **MpnsService** экземпляра, предоставляемые hello **NotificationHubService** toosend принудительной всплывающее уведомление:</span><span class="sxs-lookup"><span data-stu-id="f57f5-182">hello following sample code uses hello **MpnsService** instance exposed by hello **NotificationHubService** toosend a toast push notification:</span></span>

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-toouniversal-windows-platform-uwp-applications"></a><span data-ttu-id="f57f5-183">Как: отправлять push приложения платформы Windows (UWP), tooUniversal уведомления</span><span class="sxs-lookup"><span data-stu-id="f57f5-183">How to: Send push notifications tooUniversal Windows Platform (UWP) applications</span></span>
<span data-ttu-id="f57f5-184">Hello **WnsService** объект предоставляет **отправки** метода, могут быть используется toosend принудительной уведомления tooUniversal платформы Windows приложения.</span><span class="sxs-lookup"><span data-stu-id="f57f5-184">hello **WnsService** object provides a **send** method that can be used toosend push notifications tooUniversal Windows Platform applications.</span></span>  <span data-ttu-id="f57f5-185">Hello **отправки** метод принимает hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="f57f5-185">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="f57f5-186">**Теги** -hello идентификатор тега.</span><span class="sxs-lookup"><span data-stu-id="f57f5-186">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="f57f5-187">Если ни один тег, hello уведомления будут отправляться tooall зарегистрированных клиентов.</span><span class="sxs-lookup"><span data-stu-id="f57f5-187">If no tag is provided, hello notification will be sent tooall registered clients.</span></span>
* <span data-ttu-id="f57f5-188">**Полезные данные** -полезные данные сообщения hello XML.</span><span class="sxs-lookup"><span data-stu-id="f57f5-188">**Payload** - hello XML message payload.</span></span>
* <span data-ttu-id="f57f5-189">**Тип** -hello тип уведомления.</span><span class="sxs-lookup"><span data-stu-id="f57f5-189">**Type** - hello notification type.</span></span>
* <span data-ttu-id="f57f5-190">**Options** — необязательные заголовки запроса.</span><span class="sxs-lookup"><span data-stu-id="f57f5-190">**Options** - optional request headers.</span></span>
* <span data-ttu-id="f57f5-191">**Обратный вызов** -hello функции обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="f57f5-191">**Callback** - hello callback function.</span></span>

<span data-ttu-id="f57f5-192">Список допустимых типов и заголовков запроса см. в разделе [Заголовки запроса и ответа службы push-уведомлений (приложения среды выполнения Windows)](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span><span class="sxs-lookup"><span data-stu-id="f57f5-192">For a list of valid types and request headers, see [Push notification service request and response headers](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span></span>

<span data-ttu-id="f57f5-193">Hello следующий код использует hello **WnsService** экземпляра, предоставляемые hello **NotificationHubService** toosend приложения UWP tooa всплывающих принудительной уведомления:</span><span class="sxs-lookup"><span data-stu-id="f57f5-193">hello following code uses hello **WnsService** instance exposed by hello **NotificationHubService** toosend a toast push notification tooa UWP app:</span></span>

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a><span data-ttu-id="f57f5-194">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f57f5-194">Next Steps</span></span>
<span data-ttu-id="f57f5-195">фрагменты кода образца Hello выше позволяют вы tooeasily сборки службы инфраструктуры toodeliver принудительной уведомления tooa широкого спектра устройств.</span><span class="sxs-lookup"><span data-stu-id="f57f5-195">hello sample snippets above allow you tooeasily build service infrastructure toodeliver push notifications tooa wide variety of devices.</span></span> <span data-ttu-id="f57f5-196">Теперь, когда вы узнали основы использования концентраторов уведомлений с node.js hello, выполните следующие дополнительные сведения о том, как можно расширить эти возможности дальнейшего toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="f57f5-196">Now that you've learned hello basics of using Notification Hubs with node.js, follow these links toolearn more about how you can extend these capabilities further.</span></span>

* <span data-ttu-id="f57f5-197">В разделе hello ссылка MSDN для [концентраторов уведомлений Azure](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span><span class="sxs-lookup"><span data-stu-id="f57f5-197">See hello MSDN Reference for [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span></span>
* <span data-ttu-id="f57f5-198">Посетите hello [Azure SDK для узла] репозитория в GitHub дополнительные образцы и сведения о реализации.</span><span class="sxs-lookup"><span data-stu-id="f57f5-198">Visit hello [Azure SDK for Node] repository on GitHub for more samples and implementation details.</span></span>

[Azure SDK для узла]: https://github.com/WindowsAzure/azure-sdk-for-node
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain hello Default Management Credentials for hello Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application tooUse Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages tooa Topic]: #How_to_Send_Messages_to_a_Topic
[How to: Receive Messages from a Subscription]: #How_to_Receive_Messages_from_a_Subscription
[How to: Handle Application Crashes and Unreadable Messages]: #How_to_Handle_Application_Crashes_and_Unreadable_Messages
[How to: Delete Topics and Subscriptions]: #How_to_Delete_Topics_and_Subscriptions
[1]: #Next_Steps
[Topic Concepts]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-topics-01.png
[Azure Classic Portal]: http://manage.windowsazure.com
[image]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-03.png
[2]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-04.png
[3]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-05.png
[4]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-06.png
[5]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-07.png
[SqlFilter.SqlExpression]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.sqlexpression.aspx
[Azure Service Bus Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/jj927170.aspx
[SqlFilter]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.aspx
[веб-сайт в WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
[портала Azure]: https://portal.azure.com
