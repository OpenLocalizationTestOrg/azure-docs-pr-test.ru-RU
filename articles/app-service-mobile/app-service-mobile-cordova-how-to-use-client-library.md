---
title: "aaaHow tooUse подключаемый модуль Cordova Apache для мобильных приложений Azure"
description: "Как tooUse подключаемый модуль Cordova Apache для мобильных приложений Azure"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: a56a1ce4-de0c-4f3c-8763-66252c52aa59
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: d3e0639e6478c409132af25304a2fb0f28401e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-apache-cordova-client-library-for-azure-mobile-apps"></a><span data-ttu-id="4b4ee-103">Как toouse Apache Cordova клиентскую библиотеку для мобильных приложений Azure</span><span class="sxs-lookup"><span data-stu-id="4b4ee-103">How toouse Apache Cordova client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="4b4ee-104">Это руководство поможет tooperform распространенные сценарии, с помощью hello последней [подключаемый модуль Cordova Apache для мобильных приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="4b4ee-104">This guide teaches you tooperform common scenarios using hello latest [Apache Cordova Plugin for Azure Mobile Apps].</span></span> <span data-ttu-id="4b4ee-105">Если новый tooAzure мобильные приложения, сначала завершите [быстрого запуска Azure мобильных приложений] toocreate серверной части, создайте таблицу и загрузить предварительно построенного проекта Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend, create a table, and download a pre-built Apache Cordova project.</span></span> <span data-ttu-id="4b4ee-106">В этом руководстве мы сосредоточиться на стороне клиента hello подключаемых модулей Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-106">In this guide, we focus on hello client-side Apache Cordova Plugin.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="4b4ee-107">Поддерживаемые платформы</span><span class="sxs-lookup"><span data-stu-id="4b4ee-107">Supported platforms</span></span>
<span data-ttu-id="4b4ee-108">Этот пакет SDK поддерживает Apache Cordova 6.0.0 и более поздних версий на устройствах iOS, Android и устройствах с Windows.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-108">This SDK supports Apache Cordova v6.0.0 and later on iOS, Android, and Windows devices.</span></span>  <span data-ttu-id="4b4ee-109">Поддержка платформы Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4b4ee-109">hello platform support is as follows:</span></span>

* <span data-ttu-id="4b4ee-110">API Android 19–24 (от KitKat до Nougat);</span><span class="sxs-lookup"><span data-stu-id="4b4ee-110">Android API 19-24 (KitKat through Nougat).</span></span>
* <span data-ttu-id="4b4ee-111">iOS 8.0 и более поздних версий;</span><span class="sxs-lookup"><span data-stu-id="4b4ee-111">iOS versions 8.0 and later.</span></span>
* <span data-ttu-id="4b4ee-112">Windows Phone 8.1;</span><span class="sxs-lookup"><span data-stu-id="4b4ee-112">Windows Phone 8.1.</span></span>
* <span data-ttu-id="4b4ee-113">универсальная платформа Windows.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-113">Universal Windows Platform.</span></span>

## <span data-ttu-id="4b4ee-114"><a name="Setup"></a>Настройка и необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="4b4ee-114"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="4b4ee-115">В данном руководстве предполагается, что вы уже создали серверную часть с таблицей.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-115">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="4b4ee-116">В этом руководстве предполагается, что таблица hello имеет hello одной схеме с таблицами hello в этих учебниках.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-116">This guide assumes that hello table has hello same schema as hello tables in those tutorials.</span></span> <span data-ttu-id="4b4ee-117">В этом руководстве также предполагается, были добавлены кода tooyour hello подключаемого модуля Cordova Apache.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-117">This guide also assumes that you have added hello Apache Cordova Plugin tooyour code.</span></span>  <span data-ttu-id="4b4ee-118">Если этого не делали, можно добавить проект tooyour подключаемых модулей Apache Cordova hello hello в командной строке:</span><span class="sxs-lookup"><span data-stu-id="4b4ee-118">If you have not done so, you may add hello Apache Cordova plugin tooyour project on hello command line:</span></span>

```
cordova plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="4b4ee-119">Дополнительные сведения о создании [первого приложения Apache Cordova] см. в соответствующей документации.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-119">For more information on creating [your first Apache Cordova app], see their documentation.</span></span>

## <span data-ttu-id="4b4ee-120"><a name="ionic"></a>Настройка приложения Ionic v2</span><span class="sxs-lookup"><span data-stu-id="4b4ee-120"><a name="ionic"></a>Setting up an Ionic v2 app</span></span>

<span data-ttu-id="4b4ee-121">tooproperly настроить проект Ionic v2, сначала создайте простое приложение и добавьте hello подключаемого модуля Cordova:</span><span class="sxs-lookup"><span data-stu-id="4b4ee-121">tooproperly configure an Ionic v2 project, first create a basic app and add hello Cordova plugin:</span></span>

```
ionic start projectName --v2
cd projectName
ionic plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="4b4ee-122">Добавьте следующие строки слишком hello`app.component.ts` toocreate hello клиентского объекта:</span><span class="sxs-lookup"><span data-stu-id="4b4ee-122">Add hello following lines too`app.component.ts` toocreate hello client object:</span></span>

```
declare var WindowsAzure: any;
var client = new WindowsAzure.MobileServiceClient("https://yoursite.azurewebsites.net");
```

<span data-ttu-id="4b4ee-123">Теперь, можно собрать и запустить проект hello в браузере hello:</span><span class="sxs-lookup"><span data-stu-id="4b4ee-123">You can now build and run hello project in hello browser:</span></span>

```
ionic platform add browser
ionic run browser
```

<span data-ttu-id="4b4ee-124">Подключаемый модуль Cordova приложения Azure Mobile Hello поддерживает оба Ionic приложения v1 и v2.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-124">hello Azure Mobile Apps Cordova plugin supports both Ionic v1 and v2 apps.</span></span>  <span data-ttu-id="4b4ee-125">Только для приложения hello Ionic v2 требуют дополнительных объявление для hello `WindowsAzure` объекта.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-125">Only hello Ionic v2 apps require the additional declaration for hello `WindowsAzure` object.</span></span>

[!INCLUDE [app-service-mobile-html-js-library.md](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="4b4ee-126"><a name="auth"></a>Практическое руководство. Проверка подлинности пользователей</span><span class="sxs-lookup"><span data-stu-id="4b4ee-126"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="4b4ee-127">Служба приложений Azure поддерживает аутентификацию и авторизацию пользователей с помощью различных внешних поставщиков удостоверений: Facebook, Google, учетная запись Майкрософт и Twitter.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-127">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="4b4ee-128">Можно задать разрешения для таблицы toorestrict доступ для определенных операций tooonly проверку подлинности пользователей.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-128">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="4b4ee-129">Hello идентификаторов правил авторизации tooimplement прошедших проверку подлинности пользователей также можно использовать в серверных скриптах.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-129">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="4b4ee-130">Дополнительные сведения см. в разделе hello [приступить к работе с проверкой подлинности] учебника.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-130">For more information, see hello [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="4b4ee-131">При использовании проверки подлинности в приложении Apache Cordova, должны быть доступны следующие подключаемые модули Cordova hello:</span><span class="sxs-lookup"><span data-stu-id="4b4ee-131">When using authentication in an Apache Cordova app, hello following Cordova plugins must be available:</span></span>

* <span data-ttu-id="4b4ee-132">[cordova-plugin-device]</span><span class="sxs-lookup"><span data-stu-id="4b4ee-132">[cordova-plugin-device]</span></span>
* <span data-ttu-id="4b4ee-133">[cordova-plugin-inappbrowser]</span><span class="sxs-lookup"><span data-stu-id="4b4ee-133">[cordova-plugin-inappbrowser]</span></span>

<span data-ttu-id="4b4ee-134">Поддерживается два потока аутентификации: серверный и клиентский.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-134">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="4b4ee-135">поток Hello server обеспечивает hello простой проверки подлинности, как зависит от поставщика hello веб-интерфейс проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-135">hello server flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="4b4ee-136">Hello потока клиента обеспечивает более глубокую интеграцию с возможности определенных устройств, таких как-единого входа, зависит от поставщика SDK конкретного устройства.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-136">hello client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific device-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library.md](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="4b4ee-137"><a name="configure-external-redirect-urls"></a>Практическое руководство. Настройка службы мобильных приложений для внешних URL-адресов перенаправления</span><span class="sxs-lookup"><span data-stu-id="4b4ee-137"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="4b4ee-138">Несколько типов приложений Apache Cordova используйте toohandle возможность замыкания на себя, потоков пользовательского интерфейса OAuth.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-138">Several types of Apache Cordova applications use a loopback capability toohandle OAuth UI flows.</span></span>  <span data-ttu-id="4b4ee-139">Потоки пользовательского интерфейса OAuth на localhost вызвать проблемы, поскольку служба проверки подлинности hello только известны как tooutilize службы по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-139">OAuth UI flows on localhost cause problems since hello authentication service only knows how tooutilize your service by default.</span></span>  <span data-ttu-id="4b4ee-140">Ниже перечислены примеры проблемных потоков пользовательского интерфейса OAuth:</span><span class="sxs-lookup"><span data-stu-id="4b4ee-140">Examples of problematic OAuth UI flows include:</span></span>

* <span data-ttu-id="4b4ee-141">Эмулятор Ripple Hello.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-141">hello Ripple emulator.</span></span>
* <span data-ttu-id="4b4ee-142">динамическая перезагрузка с Ionic.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-142">Live Reload with Ionic.</span></span>
* <span data-ttu-id="4b4ee-143">Локальное выполнение hello мобильной серверной части</span><span class="sxs-lookup"><span data-stu-id="4b4ee-143">Running hello mobile backend locally</span></span>
* <span data-ttu-id="4b4ee-144">Под управлением серверной части мобильных hello в другой службе приложений Azure, чем проверка подлинности обеспечивает один hello.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-144">Running hello mobile backend in a different Azure App Service than hello one providing authentication.</span></span>

<span data-ttu-id="4b4ee-145">Выполните эти инструкции tooadd toohello локальные параметры конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-145">Follow these instructions tooadd your local settings toohello configuration:</span></span>

1. <span data-ttu-id="4b4ee-146">Войдите в toohello [портал Azure]</span><span class="sxs-lookup"><span data-stu-id="4b4ee-146">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="4b4ee-147">Выберите **все ресурсы** или **службы приложений** щелкните имя мобильного приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-147">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="4b4ee-148">Щелкните **Инструменты**</span><span class="sxs-lookup"><span data-stu-id="4b4ee-148">Click **Tools**</span></span>
4. <span data-ttu-id="4b4ee-149">Нажмите кнопку **обозреватель ресурсов** hello OBSERVE меню, а затем нажмите кнопку **Go**.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-149">Click **Resource explorer** in hello OBSERVE menu, then click **Go**.</span></span>  <span data-ttu-id="4b4ee-150">Откроется новое окно или вкладка.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-150">A new window or tab opens.</span></span>
5. <span data-ttu-id="4b4ee-151">Разверните hello **config**, **authsettings** узлов на сайте в левой навигационной hello.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-151">Expand hello **config**, **authsettings** nodes for your site in hello left-hand navigation.</span></span>
6. <span data-ttu-id="4b4ee-152">Щелкните **Изменить**</span><span class="sxs-lookup"><span data-stu-id="4b4ee-152">Click **Edit**</span></span>
7. <span data-ttu-id="4b4ee-153">Найдите элемент «allowedExternalRedirectUrls» hello.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-153">Look for hello "allowedExternalRedirectUrls" element.</span></span>  <span data-ttu-id="4b4ee-154">Его можно задать toonull или массив значений.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-154">It may be set toonull or an array of values.</span></span>  <span data-ttu-id="4b4ee-155">Измените значение toohello hello, следующие значения:</span><span class="sxs-lookup"><span data-stu-id="4b4ee-155">Change hello value toohello following value:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="4b4ee-156">Замените URL-адреса hello hello URL-адреса службы.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-156">Replace hello URLs with hello URLs of your service.</span></span>  <span data-ttu-id="4b4ee-157">Примерами являются «http://localhost:3000» (для hello Node.js образца службы) или «http://localhost:4400» (для службы Ripple hello).</span><span class="sxs-lookup"><span data-stu-id="4b4ee-157">Examples include "http://localhost:3000" (for hello Node.js sample service), or "http://localhost:4400" (for hello Ripple service).</span></span>  <span data-ttu-id="4b4ee-158">Тем не менее эти URL-адреса — это примеры — вашей ситуации, включая служб hello, упомянутые в примерах hello, может отличаться.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-158">However, these URLs are examples - your situation, including for hello services mentioned in hello examples, may be different.</span></span>
8. <span data-ttu-id="4b4ee-159">Нажмите кнопку hello **чтения и записи** кнопки в hello правом верхнем углу экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-159">Click hello **Read/Write** button in hello top-right corner of hello screen.</span></span>
9. <span data-ttu-id="4b4ee-160">Щелкните зеленый hello **ПОМЕСТИТЬ** кнопки.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-160">Click hello green **PUT** button.</span></span>

<span data-ttu-id="4b4ee-161">на этом этапе сохраняются параметры Hello.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-161">hello settings are saved at this point.</span></span>  <span data-ttu-id="4b4ee-162">Не закрывайте окно браузера hello до завершения hello параметры сохранения.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-162">Do not close hello browser window until hello settings have finished saving.</span></span>
<span data-ttu-id="4b4ee-163">Также можно добавьте эти параметры замыкания на себя URL-адреса toohello CORS для службы приложений:</span><span class="sxs-lookup"><span data-stu-id="4b4ee-163">Also add these loopback URLs toohello CORS settings for your App Service:</span></span>

1. <span data-ttu-id="4b4ee-164">Войдите в toohello [портал Azure]</span><span class="sxs-lookup"><span data-stu-id="4b4ee-164">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="4b4ee-165">Выберите **все ресурсы** или **службы приложений** щелкните имя мобильного приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-165">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="4b4ee-166">автоматически открывает колонку параметров Hello.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-166">hello Settings blade opens automatically.</span></span>  <span data-ttu-id="4b4ee-167">В противном случае щелкните **Все параметры**.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-167">If it doesn't, click **All Settings**.</span></span>
4. <span data-ttu-id="4b4ee-168">Нажмите кнопку **CORS** меню hello API.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-168">Click **CORS** under hello API menu.</span></span>
5. <span data-ttu-id="4b4ee-169">Введите URL-адрес hello, на котором необходимо tooadd в hello поле и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-169">Enter hello URL that you wish tooadd in hello box provided and press Enter.</span></span>
6. <span data-ttu-id="4b4ee-170">При необходимости введите дополнительные URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-170">Enter additional URLs as needed.</span></span>
7. <span data-ttu-id="4b4ee-171">Нажмите кнопку **Сохранить** toosave hello параметры.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-171">Click **Save** toosave hello settings.</span></span>

<span data-ttu-id="4b4ee-172">Занимает около 10 – 15 секунд hello новые параметры tootake эффект.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-172">It takes approximately 10-15 seconds for hello new settings tootake effect.</span></span>

## <span data-ttu-id="4b4ee-173"><a name="register-for-push"></a>Практическое руководство. Регистрация для получения push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="4b4ee-173"><a name="register-for-push"></a>How to: Register for push notifications</span></span>
<span data-ttu-id="4b4ee-174">Установка hello [phonegap-plugin-push] toohandle push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-174">Install hello [phonegap-plugin-push] toohandle push notifications.</span></span>  <span data-ttu-id="4b4ee-175">Этот подключаемый модуль можно легко добавить с помощью `cordova plugin add` команду в командной строке приветствия или с помощью установщика подключаемого модуля Git hello в среде Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-175">This plugin can be easily added using the `cordova plugin add` command on hello command line, or via hello Git plugin installer within Visual Studio.</span></span>  <span data-ttu-id="4b4ee-176">Следующий код в приложении Apache Cordova регистрирует устройство для получения push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-176">The following code in your Apache Cordova app registers your device for push notifications:</span></span>

```
var pushOptions = {
    android: {
        senderId: '<from-gcm-console>'
    },
    ios: {
        alert: true,
        badge: true,
        sound: true
    },
    windows: {
    }
};
pushHandler = PushNotification.init(pushOptions);

pushHandler.on('registration', function (data) {
    registrationId = data.registrationId;
    // For cross-platform, you can use hello device plugin toodetermine hello device
    // Best is toouse device.platform
    var name = 'gcm'; // For android - default
    if (device.platform.toLowerCase() === 'ios')
        name = 'apns';
    if (device.platform.toLowerCase().substring(0, 3) === 'win')
        name = 'wns';
    client.push.register(name, registrationId);
});

pushHandler.on('notification', function (data) {
    // data is an object and is whatever is sent by hello PNS - check hello format
    // for your particular PNS
});

pushHandler.on('error', function (error) {
    // Handle errors
});
```

<span data-ttu-id="4b4ee-177">Используйте hello toosend SDK концентраторы уведомлений push-уведомления с сервера hello.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-177">Use hello Notification Hubs SDK toosend push notifications from hello server.</span></span>  <span data-ttu-id="4b4ee-178">Никогда не следует отправлять push-уведомления непосредственно из клиентов.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-178">Never send push notifications directly from clients.</span></span> <span data-ttu-id="4b4ee-179">Поэтому это может быть используется tootrigger отказ в обслуживании, направленную на концентраторы уведомлений или hello PNS.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-179">Doing so could be used tootrigger a denial of service attack against Notification Hubs or hello PNS.</span></span>  <span data-ttu-id="4b4ee-180">Hello PNS удалось ban трафика в результате таких атак.</span><span class="sxs-lookup"><span data-stu-id="4b4ee-180">hello PNS could ban your traffic as a result of such attacks.</span></span>

## <a name="more-information"></a><span data-ttu-id="4b4ee-181">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="4b4ee-181">More information</span></span>

<span data-ttu-id="4b4ee-182">Дополнительные сведения об API можно найти в нашей [документация по API](http://azure.github.io/azure-mobile-apps-js-client/).</span><span class="sxs-lookup"><span data-stu-id="4b4ee-182">You can find detailed API details in our [API documentation](http://azure.github.io/azure-mobile-apps-js-client/).</span></span>

<!-- URLs. -->
[портал Azure]: https://portal.azure.com
[быстрого запуска Azure мобильных приложений]: app-service-mobile-cordova-get-started.md
[приступить к работе с проверкой подлинности]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[подключаемый модуль Cordova Apache для мобильных приложений Azure]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps
[первого приложения Apache Cordova]: http://cordova.apache.org/#getstarted
[phonegap-facebook-plugin]: https://github.com/wizcorp/phonegap-facebook-plugin
[phonegap-plugin-push]: https://www.npmjs.com/package/phonegap-plugin-push
[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device
[cordova-plugin-inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
