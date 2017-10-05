---
title: "Использование подключаемого модуля Apache Cordova для мобильных приложений Azure"
description: "Использование подключаемого модуля Apache Cordova для мобильных приложений Azure"
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
ms.openlocfilehash: ebf0e911eeada0e529f908dd3e3430c94edae763
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-apache-cordova-client-library-for-azure-mobile-apps"></a><span data-ttu-id="ec1ad-103">Как использовать клиентскую библиотеку Apache Cordova для мобильных приложений Azure</span><span class="sxs-lookup"><span data-stu-id="ec1ad-103">How to use Apache Cordova client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="ec1ad-104">В данном руководстве показано, как реализовать типичные сценарии с использованием последней версии [подключаемого модуля Apache Cordova для мобильных приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="ec1ad-104">This guide teaches you to perform common scenarios using the latest [Apache Cordova Plugin for Azure Mobile Apps].</span></span> <span data-ttu-id="ec1ad-105">Если вы не знакомы с мобильными приложениями Azure, изучите статью [Быстрый запуск мобильного приложения Azure] , чтобы создать серверную часть и таблицу, а также скачать предварительно собранный проект Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend, create a table, and download a pre-built Apache Cordova project.</span></span> <span data-ttu-id="ec1ad-106">В данном руководстве мы сосредоточимся на клиентской части подключаемого модуля Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-106">In this guide, we focus on the client-side Apache Cordova Plugin.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="ec1ad-107">Поддерживаемые платформы</span><span class="sxs-lookup"><span data-stu-id="ec1ad-107">Supported platforms</span></span>
<span data-ttu-id="ec1ad-108">Этот пакет SDK поддерживает Apache Cordova 6.0.0 и более поздних версий на устройствах iOS, Android и устройствах с Windows.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-108">This SDK supports Apache Cordova v6.0.0 and later on iOS, Android, and Windows devices.</span></span>  <span data-ttu-id="ec1ad-109">Ниже перечислены возможности, поддерживаемые платформой:</span><span class="sxs-lookup"><span data-stu-id="ec1ad-109">The platform support is as follows:</span></span>

* <span data-ttu-id="ec1ad-110">API Android 19–24 (от KitKat до Nougat);</span><span class="sxs-lookup"><span data-stu-id="ec1ad-110">Android API 19-24 (KitKat through Nougat).</span></span>
* <span data-ttu-id="ec1ad-111">iOS 8.0 и более поздних версий;</span><span class="sxs-lookup"><span data-stu-id="ec1ad-111">iOS versions 8.0 and later.</span></span>
* <span data-ttu-id="ec1ad-112">Windows Phone 8.1;</span><span class="sxs-lookup"><span data-stu-id="ec1ad-112">Windows Phone 8.1.</span></span>
* <span data-ttu-id="ec1ad-113">универсальная платформа Windows.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-113">Universal Windows Platform.</span></span>

## <span data-ttu-id="ec1ad-114"><a name="Setup"></a>Настройка и необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="ec1ad-114"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="ec1ad-115">В данном руководстве предполагается, что вы уже создали серверную часть с таблицей.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-115">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="ec1ad-116">В этом руководстве предполагается, что в таблице используется та же схему, что и в таблицах, приведенных в этих учебниках.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-116">This guide assumes that the table has the same schema as the tables in those tutorials.</span></span> <span data-ttu-id="ec1ad-117">В этом руководстве также предполагается, что подключаемый модуль Apache Cordova уже добавлен в код.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-117">This guide also assumes that you have added the Apache Cordova Plugin to your code.</span></span>  <span data-ttu-id="ec1ad-118">Если это не так, добавьте подключаемый модуль Apache Cordova в проект через командную строку:</span><span class="sxs-lookup"><span data-stu-id="ec1ad-118">If you have not done so, you may add the Apache Cordova plugin to your project on the command line:</span></span>

```
cordova plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="ec1ad-119">Дополнительные сведения о создании [первого приложения Apache Cordova] см. в соответствующей документации.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-119">For more information on creating [your first Apache Cordova app], see their documentation.</span></span>

## <span data-ttu-id="ec1ad-120"><a name="ionic"></a>Настройка приложения Ionic v2</span><span class="sxs-lookup"><span data-stu-id="ec1ad-120"><a name="ionic"></a>Setting up an Ionic v2 app</span></span>

<span data-ttu-id="ec1ad-121">Чтобы правильно настроить проект Ionic v2, создать простое приложение и добавить подключаемый модуль Cordova, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-121">To properly configure an Ionic v2 project, first create a basic app and add the Cordova plugin:</span></span>

```
ionic start projectName --v2
cd projectName
ionic plugin add cordova-plugin-ms-azure-mobile-apps
```

<span data-ttu-id="ec1ad-122">Добавьте следующие строки в `app.component.ts`, чтобы создать клиентский объект:</span><span class="sxs-lookup"><span data-stu-id="ec1ad-122">Add the following lines to `app.component.ts` to create the client object:</span></span>

```
declare var WindowsAzure: any;
var client = new WindowsAzure.MobileServiceClient("https://yoursite.azurewebsites.net");
```

<span data-ttu-id="ec1ad-123">Теперь можно создать и запустить проект в браузере.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-123">You can now build and run the project in the browser:</span></span>

```
ionic platform add browser
ionic run browser
```

<span data-ttu-id="ec1ad-124">Подключаемый модуль Cordova для мобильных приложений Azure поддерживает обе версии приложения Ionic — v1 и v2.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-124">The Azure Mobile Apps Cordova plugin supports both Ionic v1 and v2 apps.</span></span>  <span data-ttu-id="ec1ad-125">Но в приложениях Ionic v2 требуется дополнительное объявление для объекта `WindowsAzure`.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-125">Only the Ionic v2 apps require the additional declaration for the `WindowsAzure` object.</span></span>

[!INCLUDE [app-service-mobile-html-js-library.md](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="ec1ad-126"><a name="auth"></a>Практическое руководство. Проверка подлинности пользователей</span><span class="sxs-lookup"><span data-stu-id="ec1ad-126"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="ec1ad-127">Служба приложений Azure поддерживает аутентификацию и авторизацию пользователей с помощью различных внешних поставщиков удостоверений: Facebook, Google, учетная запись Майкрософт и Twitter.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-127">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="ec1ad-128">Можно задать разрешения таблиц, чтобы предоставить доступ к определенным операциям только пользователям, прошедшим проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-128">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="ec1ad-129">Удостоверения пользователей, прошедших проверку подлинности, также можно применять для реализации правил авторизации в серверных скриптах.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-129">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span></span> <span data-ttu-id="ec1ad-130">Дополнительные сведения см. в учебнике [Приступая к работе с проверкой подлинности].</span><span class="sxs-lookup"><span data-stu-id="ec1ad-130">For more information, see the [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="ec1ad-131">Если в приложении Apache Cordova используется проверка подлинности, должны быть доступны следующие подключаемые модули Cordova:</span><span class="sxs-lookup"><span data-stu-id="ec1ad-131">When using authentication in an Apache Cordova app, the following Cordova plugins must be available:</span></span>

* <span data-ttu-id="ec1ad-132">[cordova-plugin-device]</span><span class="sxs-lookup"><span data-stu-id="ec1ad-132">[cordova-plugin-device]</span></span>
* <span data-ttu-id="ec1ad-133">[cordova-plugin-inappbrowser]</span><span class="sxs-lookup"><span data-stu-id="ec1ad-133">[cordova-plugin-inappbrowser]</span></span>

<span data-ttu-id="ec1ad-134">Поддерживается два потока аутентификации: серверный и клиентский.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-134">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="ec1ad-135">Серверный поток обеспечивает самый простой способ проверки подлинности, так как он использует веб-интерфейс проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-135">The server flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span></span> <span data-ttu-id="ec1ad-136">Клиентский поток обеспечивает более тесную интеграцию с возможностями устройства, такими как единый вход, так как использует пакеты SDK конкретного поставщика для конкретного устройства.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-136">The client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific device-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library.md](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="ec1ad-137"><a name="configure-external-redirect-urls"></a>Практическое руководство. Настройка службы мобильных приложений для внешних URL-адресов перенаправления</span><span class="sxs-lookup"><span data-stu-id="ec1ad-137"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="ec1ad-138">Для обработки потоков пользовательского интерфейса OAuth некоторые типы приложений Apache Cordova используют функцию замыкания на себя.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-138">Several types of Apache Cordova applications use a loopback capability to handle OAuth UI flows.</span></span>  <span data-ttu-id="ec1ad-139">Потоки пользовательского интерфейса OAuth в localhost приводят к возникновению проблем, так как службе аутентификации известно только, как использовать вашу службу по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-139">OAuth UI flows on localhost cause problems since the authentication service only knows how to utilize your service by default.</span></span>  <span data-ttu-id="ec1ad-140">Ниже перечислены примеры проблемных потоков пользовательского интерфейса OAuth:</span><span class="sxs-lookup"><span data-stu-id="ec1ad-140">Examples of problematic OAuth UI flows include:</span></span>

* <span data-ttu-id="ec1ad-141">эмулятор Ripple;</span><span class="sxs-lookup"><span data-stu-id="ec1ad-141">The Ripple emulator.</span></span>
* <span data-ttu-id="ec1ad-142">динамическая перезагрузка с Ionic.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-142">Live Reload with Ionic.</span></span>
* <span data-ttu-id="ec1ad-143">Локальное выполнение серверной части мобильной службы</span><span class="sxs-lookup"><span data-stu-id="ec1ad-143">Running the mobile backend locally</span></span>
* <span data-ttu-id="ec1ad-144">Возможно выполнение серверной части мобильной службы в службе приложений Azure, отличной от той, которая обеспечивает аутентификацию.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-144">Running the mobile backend in a different Azure App Service than the one providing authentication.</span></span>

<span data-ttu-id="ec1ad-145">Чтобы добавить локальные параметры в конфигурацию, выполните приведенные ниже указания.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-145">Follow these instructions to add your local settings to the configuration:</span></span>

1. <span data-ttu-id="ec1ad-146">Войдите на [портал Azure]</span><span class="sxs-lookup"><span data-stu-id="ec1ad-146">Log in to the [Azure portal]</span></span>
2. <span data-ttu-id="ec1ad-147">Выберите **Все ресурсы** или **Службы приложений**, а затем щелкните имя своего мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-147">Select **All resources** or **App Services** then click the name of your Mobile App.</span></span>
3. <span data-ttu-id="ec1ad-148">Щелкните **Инструменты**</span><span class="sxs-lookup"><span data-stu-id="ec1ad-148">Click **Tools**</span></span>
4. <span data-ttu-id="ec1ad-149">В меню "Наблюдение" щелкните **Обозреватель ресурсов**, затем щелкните **Перейти**.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-149">Click **Resource explorer** in the OBSERVE menu, then click **Go**.</span></span>  <span data-ttu-id="ec1ad-150">Откроется новое окно или вкладка.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-150">A new window or tab opens.</span></span>
5. <span data-ttu-id="ec1ad-151">В левой области навигации разверните узлы **config**, **authsettings** для сайта.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-151">Expand the **config**, **authsettings** nodes for your site in the left-hand navigation.</span></span>
6. <span data-ttu-id="ec1ad-152">Щелкните **Изменить**</span><span class="sxs-lookup"><span data-stu-id="ec1ad-152">Click **Edit**</span></span>
7. <span data-ttu-id="ec1ad-153">Найдите элемент "allowedExternalRedirectUrls".</span><span class="sxs-lookup"><span data-stu-id="ec1ad-153">Look for the "allowedExternalRedirectUrls" element.</span></span>  <span data-ttu-id="ec1ad-154">Ему может быть присвоено значение NULL или массив значений.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-154">It may be set to null or an array of values.</span></span>  <span data-ttu-id="ec1ad-155">Измените его значение на следующее:</span><span class="sxs-lookup"><span data-stu-id="ec1ad-155">Change the value to the following value:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="ec1ad-156">Замените URL-адреса на URL-адреса службы.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-156">Replace the URLs with the URLs of your service.</span></span>  <span data-ttu-id="ec1ad-157">Примеры: "http://localhost:3000" (для примера службы Node.js) или "http://localhost:4400" (для службы Ripple).</span><span class="sxs-lookup"><span data-stu-id="ec1ad-157">Examples include "http://localhost:3000" (for the Node.js sample service), or "http://localhost:4400" (for the Ripple service).</span></span>  <span data-ttu-id="ec1ad-158">Это только примеры URL-адресов. Ваша ситуация, включая упомянутые в приведенных примерах службы, может быть совершенно другой.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-158">However, these URLs are examples - your situation, including for the services mentioned in the examples, may be different.</span></span>
8. <span data-ttu-id="ec1ad-159">В правом верхнем углу экрана нажмите кнопку **Чтение и запись** .</span><span class="sxs-lookup"><span data-stu-id="ec1ad-159">Click the **Read/Write** button in the top-right corner of the screen.</span></span>
9. <span data-ttu-id="ec1ad-160">Нажмите зеленую кнопку **PUT** .</span><span class="sxs-lookup"><span data-stu-id="ec1ad-160">Click the green **PUT** button.</span></span>

<span data-ttu-id="ec1ad-161">Параметры будут сохранены.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-161">The settings are saved at this point.</span></span>  <span data-ttu-id="ec1ad-162">Не закрывайте окно браузера, пока не завершится сохранение параметров.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-162">Do not close the browser window until the settings have finished saving.</span></span>
<span data-ttu-id="ec1ad-163">Кроме того, добавьте указанные URL-адреса замыкания на себя в параметры CORS своей службы приложений.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-163">Also add these loopback URLs to the CORS settings for your App Service:</span></span>

1. <span data-ttu-id="ec1ad-164">Войдите на [портал Azure]</span><span class="sxs-lookup"><span data-stu-id="ec1ad-164">Log in to the [Azure portal]</span></span>
2. <span data-ttu-id="ec1ad-165">Выберите **Все ресурсы** или **Службы приложений**, а затем щелкните имя своего мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-165">Select **All resources** or **App Services** then click the name of your Mobile App.</span></span>
3. <span data-ttu-id="ec1ad-166">Автоматически откроется колонка "Параметры".</span><span class="sxs-lookup"><span data-stu-id="ec1ad-166">The Settings blade opens automatically.</span></span>  <span data-ttu-id="ec1ad-167">В противном случае щелкните **Все параметры**.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-167">If it doesn't, click **All Settings**.</span></span>
4. <span data-ttu-id="ec1ad-168">В меню API щелкните **CORS** .</span><span class="sxs-lookup"><span data-stu-id="ec1ad-168">Click **CORS** under the API menu.</span></span>
5. <span data-ttu-id="ec1ad-169">Введите URL-адрес, который вы хотите добавить, и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-169">Enter the URL that you wish to add in the box provided and press Enter.</span></span>
6. <span data-ttu-id="ec1ad-170">При необходимости введите дополнительные URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-170">Enter additional URLs as needed.</span></span>
7. <span data-ttu-id="ec1ad-171">Нажмите кнопку **Сохранить** , чтобы сохранить параметры.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-171">Click **Save** to save the settings.</span></span>

<span data-ttu-id="ec1ad-172">Новые параметры вступят в действие приблизительно через 10–15 секунд.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-172">It takes approximately 10-15 seconds for the new settings to take effect.</span></span>

## <span data-ttu-id="ec1ad-173"><a name="register-for-push"></a>Практическое руководство. Регистрация для получения push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="ec1ad-173"><a name="register-for-push"></a>How to: Register for push notifications</span></span>
<span data-ttu-id="ec1ad-174">Для обработки push-уведомлений установите [phonegap-plugin-push] .</span><span class="sxs-lookup"><span data-stu-id="ec1ad-174">Install the [phonegap-plugin-push] to handle push notifications.</span></span>  <span data-ttu-id="ec1ad-175">Этот подключаемый модуль можно легко добавить, введя команду `cordova plugin add` в командной строке или воспользовавшись установщиком подключаемых модулей Git в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-175">This plugin can be easily added using the `cordova plugin add` command on the command line, or via the Git plugin installer within Visual Studio.</span></span>  <span data-ttu-id="ec1ad-176">Следующий код в приложении Apache Cordova регистрирует устройство для получения push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-176">The following code in your Apache Cordova app registers your device for push notifications:</span></span>

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
    // For cross-platform, you can use the device plugin to determine the device
    // Best is to use device.platform
    var name = 'gcm'; // For android - default
    if (device.platform.toLowerCase() === 'ios')
        name = 'apns';
    if (device.platform.toLowerCase().substring(0, 3) === 'win')
        name = 'wns';
    client.push.register(name, registrationId);
});

pushHandler.on('notification', function (data) {
    // data is an object and is whatever is sent by the PNS - check the format
    // for your particular PNS
});

pushHandler.on('error', function (error) {
    // Handle errors
});
```

<span data-ttu-id="ec1ad-177">Для отправки push-уведомления с сервера используется пакет SDK для центров уведомлений.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-177">Use the Notification Hubs SDK to send push notifications from the server.</span></span>  <span data-ttu-id="ec1ad-178">Никогда не следует отправлять push-уведомления непосредственно из клиентов.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-178">Never send push notifications directly from clients.</span></span> <span data-ttu-id="ec1ad-179">Это может быть использовано для атак типа "отказ в обслуживании" на центры уведомлений или PNS.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-179">Doing so could be used to trigger a denial of service attack against Notification Hubs or the PNS.</span></span>  <span data-ttu-id="ec1ad-180">PNS может заблокировать ваш трафик в результате таких атак.</span><span class="sxs-lookup"><span data-stu-id="ec1ad-180">The PNS could ban your traffic as a result of such attacks.</span></span>

## <a name="more-information"></a><span data-ttu-id="ec1ad-181">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="ec1ad-181">More information</span></span>

<span data-ttu-id="ec1ad-182">Дополнительные сведения об API можно найти в нашей [документация по API](http://azure.github.io/azure-mobile-apps-js-client/).</span><span class="sxs-lookup"><span data-stu-id="ec1ad-182">You can find detailed API details in our [API documentation](http://azure.github.io/azure-mobile-apps-js-client/).</span></span>

<!-- URLs. -->
<span data-ttu-id="ec1ad-183">[портал Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="ec1ad-183">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="ec1ad-184">[Быстрый запуск мобильного приложения Azure]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="ec1ad-184">[Azure Mobile Apps Quick Start]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="ec1ad-185">[Приступая к работе с проверкой подлинности]: app-service-mobile-cordova-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="ec1ad-185">[Get started with authentication]: app-service-mobile-cordova-get-started-users.md</span></span>
[Add authentication to your app]: app-service-mobile-cordova-get-started-users.md

<span data-ttu-id="ec1ad-186">[подключаемого модуля Apache Cordova для мобильных приложений Azure]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps</span><span class="sxs-lookup"><span data-stu-id="ec1ad-186">[Apache Cordova Plugin for Azure Mobile Apps]: https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-apps</span></span>
<span data-ttu-id="ec1ad-187">[первого приложения Apache Cordova]: http://cordova.apache.org/#getstarted</span><span class="sxs-lookup"><span data-stu-id="ec1ad-187">[your first Apache Cordova app]: http://cordova.apache.org/#getstarted</span></span>
[phonegap-facebook-plugin]: https://github.com/wizcorp/phonegap-facebook-plugin
<span data-ttu-id="ec1ad-188">[phonegap-plugin-push]: https://www.npmjs.com/package/phonegap-plugin-push</span><span class="sxs-lookup"><span data-stu-id="ec1ad-188">[phonegap-plugin-push]: https://www.npmjs.com/package/phonegap-plugin-push</span></span>
<span data-ttu-id="ec1ad-189">[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device</span><span class="sxs-lookup"><span data-stu-id="ec1ad-189">[cordova-plugin-device]: https://www.npmjs.com/package/cordova-plugin-device</span></span>
<span data-ttu-id="ec1ad-190">[cordova-plugin-inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser</span><span class="sxs-lookup"><span data-stu-id="ec1ad-190">[cordova-plugin-inappbrowser]: https://www.npmjs.com/package/cordova-plugin-inappbrowser</span></span>
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
