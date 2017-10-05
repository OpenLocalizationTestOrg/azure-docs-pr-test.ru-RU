---
title: "Отправка push-уведомлений с помощью Центров уведомлений Azure и Node.js"
description: "Узнайте, как использовать концентраторы уведомлений для отправки push-уведомлений из приложения Node.js."
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
ms.openlocfilehash: dc4987b16b2e930641c6c90eff8b65c1bf8d573c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a><span data-ttu-id="a48e9-104">Отправка push-уведомлений с помощью Центров уведомлений Azure и Node.js</span><span class="sxs-lookup"><span data-stu-id="a48e9-104">Sending push notifications with Azure Notification Hubs and Node.js</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a><span data-ttu-id="a48e9-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="a48e9-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a48e9-106">Для работы с этим учебником необходима активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="a48e9-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="a48e9-107">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="a48e9-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a48e9-108">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span><span class="sxs-lookup"><span data-stu-id="a48e9-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span></span>
> 
> 

<span data-ttu-id="a48e9-109">В этом руководстве показано, как отправлять push-уведомления с помощью Центров уведомлений Azure непосредственно из приложения Node.js.</span><span class="sxs-lookup"><span data-stu-id="a48e9-109">This guide will show you how to send push notifications with the help of Azure Notification Hubs directly from a Node.js application.</span></span> 

<span data-ttu-id="a48e9-110">Описанные сценарии включают отправку push-уведомлений в приложения на следующих платформах:</span><span class="sxs-lookup"><span data-stu-id="a48e9-110">The scenarios covered include sending push notifications to applications on the following platforms:</span></span>

* <span data-ttu-id="a48e9-111">Android</span><span class="sxs-lookup"><span data-stu-id="a48e9-111">Android</span></span>
* <span data-ttu-id="a48e9-112">iOS</span><span class="sxs-lookup"><span data-stu-id="a48e9-112">iOS</span></span>
* <span data-ttu-id="a48e9-113">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="a48e9-113">Windows Phone</span></span>
* <span data-ttu-id="a48e9-114">Универсальные приложения Windows</span><span class="sxs-lookup"><span data-stu-id="a48e9-114">Universal Windows Platform</span></span> 

<span data-ttu-id="a48e9-115">Дополнительные сведения о Центрах уведомлений см. в разделе [Дальнейшие действия](#next).</span><span class="sxs-lookup"><span data-stu-id="a48e9-115">For more information on notification hubs, see the [Next Steps](#next) section.</span></span>

## <a name="what-are-notification-hubs"></a><span data-ttu-id="a48e9-116">Что такое концентраторы уведомлений</span><span class="sxs-lookup"><span data-stu-id="a48e9-116">What are Notification Hubs?</span></span>
<span data-ttu-id="a48e9-117">Центры уведомлений Azure — это простая в использовании масштабируемая многоплатформенная инфраструктура для отправки push-уведомлений на мобильные устройства.</span><span class="sxs-lookup"><span data-stu-id="a48e9-117">Azure Notification Hubs provide an easy-to-use, multi-platform, scalable infrastructure for sending push notifications to mobile devices.</span></span> <span data-ttu-id="a48e9-118">Подробные сведения об инфраструктуре служб приведены на странице [Центры уведомлений Azure](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a48e9-118">For details on the service infrastructure, see the [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) page.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="a48e9-119">Создание приложения Node.js</span><span class="sxs-lookup"><span data-stu-id="a48e9-119">Create a Node.js Application</span></span>
<span data-ttu-id="a48e9-120">Первый шаг этого руководства представляет собой создание пустого приложения Node.js.</span><span class="sxs-lookup"><span data-stu-id="a48e9-120">The first step in this tutorial is creating a new blank Node.js application.</span></span> <span data-ttu-id="a48e9-121">Указания по созданию приложения Node.js см. в статьях [Создание и развертывание простого веб-приложения Node.js][nodejswebsite], [Построение и развертывание приложения Node.js в облачной службе Azure][Node.js Cloud Service] (с использованием Windows PowerShell) или [Создание и развертывание веб-приложения Node.js в Azure с использованием WebMatrix].</span><span class="sxs-lookup"><span data-stu-id="a48e9-121">For instructions on creating a Node.js application, see [Create and deploy a Node.js application to Azure Web Site][nodejswebsite], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or [Web Site with WebMatrix].</span></span>

## <a name="configure-your-application-to-use-notification-hubs"></a><span data-ttu-id="a48e9-122">Настройка приложения для использования центров уведомлений</span><span class="sxs-lookup"><span data-stu-id="a48e9-122">Configure Your Application to Use Notification Hubs</span></span>
<span data-ttu-id="a48e9-123">Для использования центров уведомлений Azure необходимо загрузить и использовать [пакет Azure](https://www.npmjs.com/package/azure)для Node.js, который включает встроенный набор вспомогательных библиотек, взаимодействующих со службами push-уведомлений REST.</span><span class="sxs-lookup"><span data-stu-id="a48e9-123">To use Azure Notification Hubs, you need to download and use the Node.js [azure package](https://www.npmjs.com/package/azure), which includes a built-in set of helper libraries that communicate with the push notification REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="a48e9-124">Использование диспетчера пакета Node (NPM) для получения пакета</span><span class="sxs-lookup"><span data-stu-id="a48e9-124">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="a48e9-125">В интерфейсе командной строки, например **PowerShell** (Windows), **Terminal** (Mac) или **Bash** (Linux), перейдите к папке, в которой вы создали пустое приложение.</span><span class="sxs-lookup"><span data-stu-id="a48e9-125">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Linux) and navigate to the folder where you created your blank application.</span></span>
2. <span data-ttu-id="a48e9-126">Введите в командном окне **pm install azure-sb** .</span><span class="sxs-lookup"><span data-stu-id="a48e9-126">Type **npm install azure-sb** in the command window.</span></span>
3. <span data-ttu-id="a48e9-127">Вы можете выполнить команду **ls** или **dir** вручную, чтобы проверить создание папки **node\_modules**.</span><span class="sxs-lookup"><span data-stu-id="a48e9-127">You can manually run the **ls** or **dir** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="a48e9-128">В этой папке найдите пакет **azure** , который содержит библиотеки для доступа к центру уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a48e9-128">Inside that folder, find the **azure** package, which contains the libraries you need to access the Notification Hub.</span></span>

> [!NOTE]
> <span data-ttu-id="a48e9-129">Дополнительные сведения об установке NPM доступны в официальном [блоге о NPM](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span><span class="sxs-lookup"><span data-stu-id="a48e9-129">You can learn more about installing NPM on the official [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span></span> 
> 
> 

### <a name="import-the-module"></a><span data-ttu-id="a48e9-130">Импорт модуля</span><span class="sxs-lookup"><span data-stu-id="a48e9-130">Import the module</span></span>
<span data-ttu-id="a48e9-131">С помощью текстового редактора добавьте в начало файла **server.js** приложения следующее:</span><span class="sxs-lookup"><span data-stu-id="a48e9-131">Using a text editor, add the following to the top of the **server.js** file of the application:</span></span>

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a><span data-ttu-id="a48e9-132">Настройка подключения концентратора уведомлений Azure</span><span class="sxs-lookup"><span data-stu-id="a48e9-132">Setup an Azure Notification Hub connection</span></span>
<span data-ttu-id="a48e9-133">Объект **NotificationHubService** позволяет работать с концентраторами уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a48e9-133">The **NotificationHubService** object lets you work with notification hubs.</span></span> <span data-ttu-id="a48e9-134">Следующий код создает объект **NotificationHubService** для центра уведомлений с именем **hubname**.</span><span class="sxs-lookup"><span data-stu-id="a48e9-134">The following code creates a **NotificationHubService** object for the nofication hub named **hubname**.</span></span> <span data-ttu-id="a48e9-135">Добавьте его в начало файла **server.js** после оператора импорта модуля Аzure.</span><span class="sxs-lookup"><span data-stu-id="a48e9-135">Add it near the top of the **server.js** file, after the statement to import the azure module:</span></span>

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

<span data-ttu-id="a48e9-136">Значение строки подключения **connectionstring** можно получить с помощью [портала Azure] , выполнив следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a48e9-136">The connection **connectionstring** value can be obtained from the [Azure Portal] by performing the following steps:</span></span>

1. <span data-ttu-id="a48e9-137">В области навигации слева щелкните **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="a48e9-137">In the left navigation pane, click **Browse**.</span></span>
2. <span data-ttu-id="a48e9-138">Выберите **Центры уведомлений**, затем щелкните центр, который хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="a48e9-138">Select **Notification Hubs**, and then find the hub you wish to use for the sample.</span></span> <span data-ttu-id="a48e9-139">Если вам нужна помощь в создании центра уведомлений, обратитесь к учебнику по [началу работы с центрами уведомлений для Windows](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) .</span><span class="sxs-lookup"><span data-stu-id="a48e9-139">You can refer to the [Windows Store Getting Started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) if you need help creating a new Notification Hub.</span></span>
3. <span data-ttu-id="a48e9-140">Выберите элемент **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="a48e9-140">Select **Settings**.</span></span>
4. <span data-ttu-id="a48e9-141">Щелкните **Политики доступа**.</span><span class="sxs-lookup"><span data-stu-id="a48e9-141">Click on **Access Policies**.</span></span> <span data-ttu-id="a48e9-142">Вы увидите строки подключения как для общего, так и для полного доступа.</span><span class="sxs-lookup"><span data-stu-id="a48e9-142">You will see both shared and full access connection strings.</span></span>

![Портал Azure — центры уведомлений](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> <span data-ttu-id="a48e9-144">Строку подключения можно также получить с помощью командлета **Get-AzureSbNamespace** в [Azure PowerShell](/powershell/azureps-cmdlets-docs) или команды **azure sb namespace show** в [интерфейсе командной строки Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="a48e9-144">You can also retrieve the connection string using the **Get-AzureSbNamespace** cmdlet provided by [Azure PowerShell](/powershell/azureps-cmdlets-docs) or the **azure sb namespace show** command with the [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md).</span></span>
> 
> 

## <a name="general-architecture"></a><span data-ttu-id="a48e9-145">Общая архитектура</span><span class="sxs-lookup"><span data-stu-id="a48e9-145">General architecture</span></span>
<span data-ttu-id="a48e9-146">Объект **NotificationHubService** предоставляет следующие экземпляры объекта для отправки push-уведомлений определенным устройствам и приложениям.</span><span class="sxs-lookup"><span data-stu-id="a48e9-146">The **NotificationHubService** object exposes the following object instances for sending push notifications to specific devices and applications:</span></span>

* <span data-ttu-id="a48e9-147">**Android** — используйте объект **GcmService**, доступный в **notificationHubService.gcm**;</span><span class="sxs-lookup"><span data-stu-id="a48e9-147">**Android** - use the **GcmService** object, which is available at **notificationHubService.gcm**</span></span>
* <span data-ttu-id="a48e9-148">**iOS** — используйте объект **ApnsService**, доступный в **notificationHubService.apns**;</span><span class="sxs-lookup"><span data-stu-id="a48e9-148">**iOS** - use the **ApnsService** object, which is accessible at **notificationHubService.apns**</span></span>
* <span data-ttu-id="a48e9-149">**Windows Phone** — используйте объект **MpnsService**, доступный в **notificationHubService.mpns**;</span><span class="sxs-lookup"><span data-stu-id="a48e9-149">**Windows Phone** - use the **MpnsService** object, which is available at **notificationHubService.mpns**</span></span>
* <span data-ttu-id="a48e9-150">**универсальная платформа Windows** — используйте объект **WnsService**, который доступен в **notificationHubService.wns**.</span><span class="sxs-lookup"><span data-stu-id="a48e9-150">**Universal Windows Platform** - use the **WnsService** object, which is available at **notificationHubService.wns**</span></span>

### <a name="how-to-send-push-notifications-to-android-applications"></a><span data-ttu-id="a48e9-151">Практическое руководство. Отправка push-уведомлений в приложения Android</span><span class="sxs-lookup"><span data-stu-id="a48e9-151">How to: Send push notifications to Android applications</span></span>
<span data-ttu-id="a48e9-152">Объект **GcmService** предоставляет метод **send**, который может использоваться для отправки push-уведомлений в приложения Android.</span><span class="sxs-lookup"><span data-stu-id="a48e9-152">The **GcmService** object provides a **send** method that can be used to send push notifications to Android applications.</span></span> <span data-ttu-id="a48e9-153">Метод **Отправить** принимает следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="a48e9-153">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="a48e9-154">**Tags** — идентификатор тега.</span><span class="sxs-lookup"><span data-stu-id="a48e9-154">**Tags** - the tag identifier.</span></span> <span data-ttu-id="a48e9-155">Если тег отсутствует, уведомления будут отправляться всем клиентам.</span><span class="sxs-lookup"><span data-stu-id="a48e9-155">If no tag is provided, the notification will be sent to all clients.</span></span>
* <span data-ttu-id="a48e9-156">**Payload** — полезные данные JSON или строковые полезные данные сообщения.</span><span class="sxs-lookup"><span data-stu-id="a48e9-156">**Payload** - the message's JSON or raw string payload.</span></span>
* <span data-ttu-id="a48e9-157">**Callback** — функция обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="a48e9-157">**Callback** - the callback function.</span></span>

<span data-ttu-id="a48e9-158">Дополнительные сведения о формате полезных данных см. в разделе **Payload** (Полезные данные) документа [About GCM Connection Server](http://developer.android.com/google/gcm/server.html#payload) (О сервере подключений GCM).</span><span class="sxs-lookup"><span data-stu-id="a48e9-158">For more information on the payload format, see the **Payload** section of the [Implementing GCM Server](http://developer.android.com/google/gcm/server.html#payload) document.</span></span>

<span data-ttu-id="a48e9-159">В следующем коде для отправки push-уведомления всем зарегистрированным клиентам используется экземпляр **GcmService**, предоставляемый **NotificationHubService**.</span><span class="sxs-lookup"><span data-stu-id="a48e9-159">The following code uses the **GcmService** instance exposed by the **NotificationHubService** to send a push notification to all registered clients.</span></span>

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

### <a name="how-to-send-push-notifications-to-ios-applications"></a><span data-ttu-id="a48e9-160">Практическое руководство. Отправка push-уведомлений в приложения iOS</span><span class="sxs-lookup"><span data-stu-id="a48e9-160">How to: Send push notifications to iOS applications</span></span>
<span data-ttu-id="a48e9-161">Как и в случае с описанными выше приложениями Android, объект **ApnsService** предоставляет метод **send**, который может использоваться для отправки push-уведомлений в приложения iOS.</span><span class="sxs-lookup"><span data-stu-id="a48e9-161">Same as with Android applications described above, the **ApnsService** object provides a **send** method that can be used to send push notifications to iOS applications.</span></span> <span data-ttu-id="a48e9-162">Метод **Отправить** принимает следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="a48e9-162">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="a48e9-163">**Tags** — идентификатор тега.</span><span class="sxs-lookup"><span data-stu-id="a48e9-163">**Tags** - the tag identifier.</span></span> <span data-ttu-id="a48e9-164">Если тег отсутствует, уведомления будут отправляться всем клиентам.</span><span class="sxs-lookup"><span data-stu-id="a48e9-164">If no tag is provided, the notification will be sent to all clients.</span></span>
* <span data-ttu-id="a48e9-165">**Payload** — полезные данные JSON или строковые полезные данные сообщения.</span><span class="sxs-lookup"><span data-stu-id="a48e9-165">**Payload** - the message's JSON or string payload.</span></span>
* <span data-ttu-id="a48e9-166">**Callback** — функция обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="a48e9-166">**Callback** - the callback function.</span></span>

<span data-ttu-id="a48e9-167">Дополнительные сведения о формате полезных данных см. в разделе **Notification Payload** (Полезные данные уведомления) документа [Local and Push Notification Programming Guide](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) (Руководство по программированию локальных и push-уведомлений).</span><span class="sxs-lookup"><span data-stu-id="a48e9-167">For more information the payload format, see The **Notification Payload** section of the [Local and Push Notification Programming Guide](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) document.</span></span>

<span data-ttu-id="a48e9-168">В следующем коде используется экземпляр **ApnsService**, предоставляемый **NotificationHubService**, для отправки оповещений всем клиентам:</span><span class="sxs-lookup"><span data-stu-id="a48e9-168">The following code uses the **ApnsService** instance exposed by the **NotificationHubService** to send an alert message to all clients:</span></span>

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-to-windows-phone-applications"></a><span data-ttu-id="a48e9-169">Практическое руководство. Отправка push-уведомлений в приложения Windows Phone</span><span class="sxs-lookup"><span data-stu-id="a48e9-169">How to: Send push notifications to Windows Phone applications</span></span>
<span data-ttu-id="a48e9-170">Объект **MpnsService** предоставляет метод **send**, который может использоваться для отправки push-уведомлений в приложения Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="a48e9-170">The **MpnsService** object provides a **send** method that can be used to send push notifications to Windows Phone applications.</span></span> <span data-ttu-id="a48e9-171">Метод **Отправить** принимает следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="a48e9-171">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="a48e9-172">**Tags** — идентификатор тега.</span><span class="sxs-lookup"><span data-stu-id="a48e9-172">**Tags** - the tag identifier.</span></span> <span data-ttu-id="a48e9-173">Если тег отсутствует, уведомления будут отправляться всем клиентам.</span><span class="sxs-lookup"><span data-stu-id="a48e9-173">If no tag is provided, the notification will be sent to all clients.</span></span>
* <span data-ttu-id="a48e9-174">**Payload** — полезные данные XML сообщения.</span><span class="sxs-lookup"><span data-stu-id="a48e9-174">**Payload** - the message's XML payload.</span></span>
* <span data-ttu-id="a48e9-175">**TargetName** - `toast` — уведомлений во всплывающем окне.</span><span class="sxs-lookup"><span data-stu-id="a48e9-175">**TargetName** - `toast` for toast notifications.</span></span> <span data-ttu-id="a48e9-176">`token` для уведомлений на плитке.</span><span class="sxs-lookup"><span data-stu-id="a48e9-176">`token` for tile notifications.</span></span>
* <span data-ttu-id="a48e9-177">**NotificationClass** — приоритет уведомления.</span><span class="sxs-lookup"><span data-stu-id="a48e9-177">**NotificationClass** - The priority of the notification.</span></span> <span data-ttu-id="a48e9-178">Допустимые значения см. в разделе **HTTP Header Elements** (Элементы заголовка HTTP) документа [Pushing Notifications from a Server (Windows Phone)](http://msdn.microsoft.com/library/hh221551.aspx) (Push-уведомления от сервера (Windows Phone)).</span><span class="sxs-lookup"><span data-stu-id="a48e9-178">See the **HTTP Header Elements** section of the [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) document for valid values.</span></span>
* <span data-ttu-id="a48e9-179">**Options** — необязательные заголовки запроса.</span><span class="sxs-lookup"><span data-stu-id="a48e9-179">**Options** - optional request headers.</span></span>
* <span data-ttu-id="a48e9-180">**Callback** — функция обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="a48e9-180">**Callback** - the callback function.</span></span>

<span data-ttu-id="a48e9-181">Перечень допустимых значений **TargetName**, **NotificationClass** и параметров заголовка см. на странице [Push notifications from a server (Windows Phone)](http://msdn.microsoft.com/library/hh221551.aspx) (Push-уведомления от сервера (Windows Phone)).</span><span class="sxs-lookup"><span data-stu-id="a48e9-181">For a list of valid **TargetName**, **NotificationClass** and header options, check out the [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) page.</span></span>

<span data-ttu-id="a48e9-182">В следующем примере кода для отправки всплывающего push-уведомления используется экземпляр **MpnsService**, предоставляемый **NotificationHubService**.</span><span class="sxs-lookup"><span data-stu-id="a48e9-182">The following sample code uses the **MpnsService** instance exposed by the **NotificationHubService** to send a toast push notification:</span></span>

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-to-universal-windows-platform-uwp-applications"></a><span data-ttu-id="a48e9-183">Практическое руководство. Отправка push-уведомлений в приложения универсальной платформы Windows (UWP)</span><span class="sxs-lookup"><span data-stu-id="a48e9-183">How to: Send push notifications to Universal Windows Platform (UWP) applications</span></span>
<span data-ttu-id="a48e9-184">Объект **WnsService** предоставляет метод **send**, который может использоваться для отправки push-уведомлений в приложения универсальной платформы Windows.</span><span class="sxs-lookup"><span data-stu-id="a48e9-184">The **WnsService** object provides a **send** method that can be used to send push notifications to Universal Windows Platform applications.</span></span>  <span data-ttu-id="a48e9-185">Метод **Отправить** принимает следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="a48e9-185">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="a48e9-186">**Tags** — идентификатор тега.</span><span class="sxs-lookup"><span data-stu-id="a48e9-186">**Tags** - the tag identifier.</span></span> <span data-ttu-id="a48e9-187">Если тег отсутствует, уведомления будут отправляться всем зарегистрированным клиентам.</span><span class="sxs-lookup"><span data-stu-id="a48e9-187">If no tag is provided, the notification will be sent to all registered clients.</span></span>
* <span data-ttu-id="a48e9-188">**Payload** — полезные данные XML сообщения.</span><span class="sxs-lookup"><span data-stu-id="a48e9-188">**Payload** - the XML message payload.</span></span>
* <span data-ttu-id="a48e9-189">**Type** — тип уведомления.</span><span class="sxs-lookup"><span data-stu-id="a48e9-189">**Type** - the notification type.</span></span>
* <span data-ttu-id="a48e9-190">**Options** — необязательные заголовки запроса.</span><span class="sxs-lookup"><span data-stu-id="a48e9-190">**Options** - optional request headers.</span></span>
* <span data-ttu-id="a48e9-191">**Callback** — функция обратного вызова.</span><span class="sxs-lookup"><span data-stu-id="a48e9-191">**Callback** - the callback function.</span></span>

<span data-ttu-id="a48e9-192">Список допустимых типов и заголовков запроса см. в разделе [Заголовки запроса и ответа службы push-уведомлений (приложения среды выполнения Windows)](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span><span class="sxs-lookup"><span data-stu-id="a48e9-192">For a list of valid types and request headers, see [Push notification service request and response headers](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span></span>

<span data-ttu-id="a48e9-193">В следующем примере кода для отправки всплывающего push-уведомления приложению UWP используется экземпляр **WnsService**, предоставляемый **NotificationHubService**.</span><span class="sxs-lookup"><span data-stu-id="a48e9-193">The following code uses the **WnsService** instance exposed by the **NotificationHubService** to send a toast push notification to a UWP app:</span></span>

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a><span data-ttu-id="a48e9-194">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a48e9-194">Next Steps</span></span>
<span data-ttu-id="a48e9-195">Примеры фрагментов выше позволяют легко создать инфраструктуру службы для отправки push-уведомлений на широкий спектр устройств.</span><span class="sxs-lookup"><span data-stu-id="a48e9-195">The sample snippets above allow you to easily build service infrastructure to deliver push notifications to a wide variety of devices.</span></span> <span data-ttu-id="a48e9-196">Теперь, когда вы познакомились с основами использования центров уведомлений с Node.js, используйте следующие ссылки для получения дополнительных сведений о том, как можно дальше расширить эти возможности.</span><span class="sxs-lookup"><span data-stu-id="a48e9-196">Now that you've learned the basics of using Notification Hubs with node.js, follow these links to learn more about how you can extend these capabilities further.</span></span>

* <span data-ttu-id="a48e9-197">См. статью [Общие сведения о Центрах уведомлений](https://msdn.microsoft.com/library/azure/jj927170.aspx) в справочнике MSDN.</span><span class="sxs-lookup"><span data-stu-id="a48e9-197">See the MSDN Reference for [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span></span>
* <span data-ttu-id="a48e9-198">Дополнительные примеры и сведения о реализации доступны в репозитории [пакетов SDK Azure для Node] на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="a48e9-198">Visit the [Azure SDK for Node] repository on GitHub for more samples and implementation details.</span></span>

<span data-ttu-id="a48e9-199">[пакетов SDK Azure для Node]: https://github.com/WindowsAzure/azure-sdk-for-node</span><span class="sxs-lookup"><span data-stu-id="a48e9-199">[Azure SDK for Node]: https://github.com/WindowsAzure/azure-sdk-for-node</span></span>
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain the Default Management Credentials for the Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application to Use Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages to a Topic]: #How_to_Send_Messages_to_a_Topic
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
<span data-ttu-id="a48e9-200">[Создание и развертывание веб-приложения Node.js в Azure с использованием WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/</span><span class="sxs-lookup"><span data-stu-id="a48e9-200">[Web Site with WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/</span></span>
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
<span data-ttu-id="a48e9-201">[портала Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="a48e9-201">[Azure Portal]: https://portal.azure.com</span></span>
