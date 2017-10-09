---
title: "aaaSending Secure Push-уведомлений с концентраторами уведомлений Azure"
description: "Узнайте, как безопасные toosend push приложения Android tooan уведомления из Azure. Примеры кода написаны на Java и C#."
documentationcenter: android
keywords: "push-уведомление, push-уведомления, push-сообщения, push-уведомления android"
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: daf3de1c-f6a9-43c4-8165-a76bfaa70893
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: d07943c4691ed07acb987086228ef565e6281d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sending-secure-push-notifications-with-azure-notification-hubs"></a><span data-ttu-id="a47d4-105">Отправка безопасных push-уведомлений с помощью Центров уведомлений Azure</span><span class="sxs-lookup"><span data-stu-id="a47d4-105">Sending Secure Push Notifications with Azure Notification Hubs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a47d4-106">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="a47d4-106">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="a47d4-107">iOS</span><span class="sxs-lookup"><span data-stu-id="a47d4-107">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="a47d4-108">Android</span><span class="sxs-lookup"><span data-stu-id="a47d4-108">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="a47d4-109">Обзор</span><span class="sxs-lookup"><span data-stu-id="a47d4-109">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a47d4-110">toocomplete этого учебника необходимо иметь активную учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="a47d4-110">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="a47d4-111">Если ее нет, можно создать бесплатную пробную учетную запись всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="a47d4-111">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a47d4-112">Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="a47d4-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).</span></span>
> 
> 

<span data-ttu-id="a47d4-113">Поддержка уведомлений Push в Microsoft Azure позволяет tooaccess инфраструктура сообщения в использовании, несколькими платформами, масштабируемых принудительной значительно упрощает реализацию hello push-уведомлений для приложений потребителя и предприятия для мобильных платформ.</span><span class="sxs-lookup"><span data-stu-id="a47d4-113">Push notification support in Microsoft Azure enables you tooaccess an easy-to-use, multiplatform, scaled-out push message infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="a47d4-114">Иногда из-за ограничений tooregulatory или безопасности, приложение может возникнуть tooinclude что-нибудь в hello уведомление, которое не может передаваться через инфраструктуру hello Стандартная push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a47d4-114">Due tooregulatory or security constraints, sometimes an application might want tooinclude something in hello notification that cannot be transmitted through hello standard push notification infrastructure.</span></span> <span data-ttu-id="a47d4-115">В данном учебнике как tooachieve hello такие же возможности, отправляя конфиденциальных данных через проверку подлинности безопасное соединение между устройства Android клиента hello и внутреннего сервера приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a47d4-115">This tutorial describes how tooachieve hello same experience by sending sensitive information through a secure, authenticated connection between hello client Android device and hello app backend.</span></span>

<span data-ttu-id="a47d4-116">На высоком уровне hello поток выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a47d4-116">At a high level, hello flow is as follows:</span></span>

1. <span data-ttu-id="a47d4-117">Hello приложения внутреннего интерфейса:</span><span class="sxs-lookup"><span data-stu-id="a47d4-117">hello app back-end:</span></span>
   * <span data-ttu-id="a47d4-118">Сохраняет полезную нагрузку в базе данных серверной части.</span><span class="sxs-lookup"><span data-stu-id="a47d4-118">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="a47d4-119">Отправляет идентификатор hello этого уведомления toohello устройства Android (отправляются без защиты данных).</span><span class="sxs-lookup"><span data-stu-id="a47d4-119">Sends hello ID of this notification toohello Android device (no secure information is sent).</span></span>
2. <span data-ttu-id="a47d4-120">приложение Hello на устройстве hello, при получении уведомления hello:</span><span class="sxs-lookup"><span data-stu-id="a47d4-120">hello app on hello device, when receiving hello notification:</span></span>
   * <span data-ttu-id="a47d4-121">устройство Android Hello обращается hello серверной части запроса hello безопасного полезных данных.</span><span class="sxs-lookup"><span data-stu-id="a47d4-121">hello Android device contacts hello back-end requesting hello secure payload.</span></span>
   * <span data-ttu-id="a47d4-122">приложение Hello можно показать hello полезных данных в виде уведомлений на устройстве hello.</span><span class="sxs-lookup"><span data-stu-id="a47d4-122">hello app can show hello payload as a notification on hello device.</span></span>

<span data-ttu-id="a47d4-123">Очень важно, toonote, что предшествующий потока hello (и в этом учебнике) предполагается устройства hello склада маркер проверки подлинности в локальном хранилище после hello пользователь вошел в систему.</span><span class="sxs-lookup"><span data-stu-id="a47d4-123">It is important toonote that in hello preceding flow (and in this tutorial), we assume that hello device stores an authentication token in local storage, after hello user logs in.</span></span> <span data-ttu-id="a47d4-124">Это гарантирует полностью эффективной работы, как hello устройства можно получить полезные данные безопасного hello уведомления, с помощью этого токена.</span><span class="sxs-lookup"><span data-stu-id="a47d4-124">This guarantees a completely seamless experience, as hello device can retrieve hello notification’s secure payload using this token.</span></span> <span data-ttu-id="a47d4-125">Если приложение не хранить токены проверки подлинности на устройстве hello или может быть просрочен эти токены, приложение hello устройства, при получении push-уведомление hello отображать универсального уведомление запроса приложение hello toolaunch hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="a47d4-125">If your application does not store authentication tokens on hello device, or if these tokens can be expired, hello device app, upon receiving hello push notification should display a generic notification prompting hello user toolaunch hello app.</span></span> <span data-ttu-id="a47d4-126">Затем приложение Hello проверяет подлинность пользователя hello и приводятся полезные данные уведомления hello.</span><span class="sxs-lookup"><span data-stu-id="a47d4-126">hello app then authenticates hello user and shows hello notification payload.</span></span>

<span data-ttu-id="a47d4-127">В этом учебнике показано, как безопасные toosend push-уведомления.</span><span class="sxs-lookup"><span data-stu-id="a47d4-127">This tutorial shows how toosend secure push notifications.</span></span> <span data-ttu-id="a47d4-128">Она построена на hello [уведомить пользователей](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) учебник, поэтому следует выполнить действия hello в этом учебнике сначала, если это еще не сделано.</span><span class="sxs-lookup"><span data-stu-id="a47d4-128">It builds on hello [Notify Users](notification-hubs-aspnet-backend-gcm-android-push-to-user-google-notification.md) tutorial, so you should complete hello steps in that tutorial first if you haven't already.</span></span>

> [!NOTE]
> <span data-ttu-id="a47d4-129">В этом учебнике подразумевается, что вы создали и настроили центр уведомлений в соответствии с описанием в учебнике [Приступая к работе с центрами уведомлений (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a47d4-129">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (Android)](notification-hubs-android-push-notification-google-gcm-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-android-project"></a><span data-ttu-id="a47d4-130">Изменение проекта Android hello</span><span class="sxs-lookup"><span data-stu-id="a47d4-130">Modify hello Android project</span></span>
<span data-ttu-id="a47d4-131">Теперь, когда вы изменили вашей hello просто toosend серверной части приложения *идентификатор* push-уведомлений, у вас есть toochange вашей toohandle приложение Android, уведомления и обратный вызов к серверной части tooretrieve hello защитить toobe сообщений отображается.</span><span class="sxs-lookup"><span data-stu-id="a47d4-131">Now that you modified your app back-end toosend just hello *id* of a push notification, you have toochange your Android app toohandle that notification and call back your back-end tooretrieve hello secure message toobe displayed.</span></span>
<span data-ttu-id="a47d4-132">tooachieve этой цели, у вас есть toomake убедиться, что ваше приложение Android знает, как tooauthenticate себя настройки сервера при получении push-уведомлений hello.</span><span class="sxs-lookup"><span data-stu-id="a47d4-132">tooachieve this goal, you have toomake sure that your Android app knows how tooauthenticate itself with your back-end when it receives hello push notifications.</span></span>

<span data-ttu-id="a47d4-133">Теперь мы изменит hello *входа* потока в порядке toosave hello значение проверки подлинности заголовка hello Общие параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="a47d4-133">We will now modify hello *login* flow in order toosave hello authentication header value in hello shared preferences of your app.</span></span> <span data-ttu-id="a47d4-134">Аналог механизмы может быть используется toostore любого токена проверки подлинности (например, токены OAuth), hello приложения будет иметь toouse без использования учетных данных пользователя.</span><span class="sxs-lookup"><span data-stu-id="a47d4-134">Analogous mechanisms can be used toostore any authentication token (e.g. OAuth tokens) that hello app will have toouse without requiring user credentials.</span></span>

1. <span data-ttu-id="a47d4-135">В проекте Android приложения добавьте следующие константы вверху hello hello hello **MainActivity** класса:</span><span class="sxs-lookup"><span data-stu-id="a47d4-135">In your Android app project, add hello following constants at hello top of hello **MainActivity** class:</span></span>
   
        public static final String NOTIFY_USERS_PROPERTIES = "NotifyUsersProperties";
        public static final String AUTHORIZATION_HEADER_PROPERTY = "AuthorizationHeader";
2. <span data-ttu-id="a47d4-136">По-прежнему в hello **MainActivity** класс, обновление hello `getAuthorizationHeader()` hello toocontain метод следующий код:</span><span class="sxs-lookup"><span data-stu-id="a47d4-136">Still in hello **MainActivity** class, update hello `getAuthorizationHeader()` method toocontain hello following code:</span></span>
   
        private String getAuthorizationHeader() throws UnsupportedEncodingException {
            EditText username = (EditText) findViewById(R.id.usernameText);
            EditText password = (EditText) findViewById(R.id.passwordText);
            String basicAuthHeader = username.getText().toString()+":"+password.getText().toString();
            basicAuthHeader = Base64.encodeToString(basicAuthHeader.getBytes("UTF-8"), Base64.NO_WRAP);
   
            SharedPreferences sp = getSharedPreferences(NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            sp.edit().putString(AUTHORIZATION_HEADER_PROPERTY, basicAuthHeader).commit();
   
            return basicAuthHeader;
        }
3. <span data-ttu-id="a47d4-137">Добавьте следующее hello `import` инструкции вверху hello hello **MainActivity** файла:</span><span class="sxs-lookup"><span data-stu-id="a47d4-137">Add hello following `import` statements at hello top of hello **MainActivity** file:</span></span>
   
        import android.content.SharedPreferences;

<span data-ttu-id="a47d4-138">Теперь изменим hello обработчик, который вызывается при получении уведомления hello.</span><span class="sxs-lookup"><span data-stu-id="a47d4-138">Now we will change hello handler that is called when hello notification is received.</span></span>

1. <span data-ttu-id="a47d4-139">В hello **MyHandler** класс изменить hello `OnReceive()` toocontain метод:</span><span class="sxs-lookup"><span data-stu-id="a47d4-139">In hello **MyHandler** class change hello `OnReceive()` method toocontain:</span></span>
   
        public void onReceive(Context context, Bundle bundle) {
            ctx = context;
            String secureMessageId = bundle.getString("secureId");
            retrieveNotification(secureMessageId);
        }
2. <span data-ttu-id="a47d4-140">Затем добавьте hello `retrieveNotification()` метод, заменив заполнитель hello `{back-end endpoint}` с конечной точкой hello серверной части, полученный при развертывании серверной части:</span><span class="sxs-lookup"><span data-stu-id="a47d4-140">Then add hello `retrieveNotification()` method, replacing hello placeholder `{back-end endpoint}` with hello back-end endpoint obtained while deploying your back-end:</span></span>
   
        private void retrieveNotification(final String secureMessageId) {
            SharedPreferences sp = ctx.getSharedPreferences(MainActivity.NOTIFY_USERS_PROPERTIES, Context.MODE_PRIVATE);
            final String authorizationHeader = sp.getString(MainActivity.AUTHORIZATION_HEADER_PROPERTY, null);
   
            new AsyncTask<Object, Object, Object>() {
                @Override
                protected Object doInBackground(Object... params) {
                    try {
                        HttpUriRequest request = new HttpGet("{back-end endpoint}/api/notifications/"+secureMessageId);
                        request.addHeader("Authorization", "Basic "+authorizationHeader);
                        HttpResponse response = new DefaultHttpClient().execute(request);
                        if (response.getStatusLine().getStatusCode() != HttpStatus.SC_OK) {
                            Log.e("MainActivity", "Error retrieving secure notification" + response.getStatusLine().getStatusCode());
                            throw new RuntimeException("Error retrieving secure notification");
                        }
                        String secureNotificationJSON = EntityUtils.toString(response.getEntity());
                        JSONObject secureNotification = new JSONObject(secureNotificationJSON);
                        sendNotification(secureNotification.getString("Payload"));
                    } catch (Exception e) {
                        Log.e("MainActivity", "Failed tooretrieve secure notification - " + e.getMessage());
                        return e;
                    }
                    return null;
                }
            }.execute(null, null, null);
        }

<span data-ttu-id="a47d4-141">Этот метод вызывает hello tooretrieve серверной части приложения уведомления содержимого с помощью учетных данных hello в hello общих параметров и отображает его в виде обычных уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a47d4-141">This method calls your app back-end tooretrieve hello notification content using hello credentials stored in hello shared preferences and displays it as a normal notification.</span></span> <span data-ttu-id="a47d4-142">уведомления Hello выглядит toohello пользователя приложения так же, как любые другие push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a47d4-142">hello notification looks toohello app user exactly like any other push notification.</span></span>

<span data-ttu-id="a47d4-143">Обратите внимание, что он является более предпочтительным, чем toohandle случаях hello отсутствующее свойство Заголовок проверки подлинности или отклонение с помощью серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="a47d4-143">Note that it is preferable toohandle hello cases of missing authentication header property or rejection by hello back-end.</span></span> <span data-ttu-id="a47d4-144">Hello конкретных обработки этих вариантов основном зависят от вам целевой.</span><span class="sxs-lookup"><span data-stu-id="a47d4-144">hello specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="a47d4-145">Один из вариантов — toodisplay уведомление с универсальным запрашивать hello tooauthenticate tooretrieve hello фактическое уведомление для пользователей.</span><span class="sxs-lookup"><span data-stu-id="a47d4-145">One option is toodisplay a notification with a generic prompt for hello user tooauthenticate tooretrieve hello actual notification.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="a47d4-146">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="a47d4-146">Run hello Application</span></span>
<span data-ttu-id="a47d4-147">toorun Здравствуйте, приложения, hello следующие:</span><span class="sxs-lookup"><span data-stu-id="a47d4-147">toorun hello application, do hello following:</span></span>

1. <span data-ttu-id="a47d4-148">Убедитесь, что **AppBackend** развернут в Azure.</span><span class="sxs-lookup"><span data-stu-id="a47d4-148">Make sure **AppBackend** is deployed in Azure.</span></span> <span data-ttu-id="a47d4-149">Если с помощью Visual Studio, запустите hello **AppBackend** приложения веб-API.</span><span class="sxs-lookup"><span data-stu-id="a47d4-149">If using Visual Studio, run hello **AppBackend** Web API application.</span></span> <span data-ttu-id="a47d4-150">Отобразится веб-страница ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a47d4-150">An ASP.NET web page is displayed.</span></span>
2. <span data-ttu-id="a47d4-151">В Eclipse запустите приложение hello на физического устройства или hello эмулятор Android.</span><span class="sxs-lookup"><span data-stu-id="a47d4-151">In Eclipse, run hello app on a physical Android device or hello emulator.</span></span>
3. <span data-ttu-id="a47d4-152">В приложении Android hello пользовательского интерфейса введите имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="a47d4-152">In hello Android app UI, enter a username and password.</span></span> <span data-ttu-id="a47d4-153">Это может быть любой строкой, но они должны быть hello одинаковое значение.</span><span class="sxs-lookup"><span data-stu-id="a47d4-153">These can be any string, but they must be hello same value.</span></span>
4. <span data-ttu-id="a47d4-154">В приложении Android hello пользовательского интерфейса, выберите **входа**.</span><span class="sxs-lookup"><span data-stu-id="a47d4-154">In hello Android app UI, click **Log in**.</span></span> <span data-ttu-id="a47d4-155">Затем нажмите **Отправить push-уведомление**.</span><span class="sxs-lookup"><span data-stu-id="a47d4-155">Then click **Send push**.</span></span>

