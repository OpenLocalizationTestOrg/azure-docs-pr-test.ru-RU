---
title: "Как использовать пакет SDK JavaScript для мобильных приложений Azure"
description: "Как использовать v для мобильных приложений Azure"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 53b78965-caa3-4b22-bb67-5bd5c19d03c4
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 0c4b4de560d70592f5bbdee28b56a7686b5689f4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-javascript-client-library-for-azure-mobile-apps"></a><span data-ttu-id="b52c2-103">Как использовать клиентскую библиотеку JavaScript для мобильных приложений Azure</span><span class="sxs-lookup"><span data-stu-id="b52c2-103">How to Use the JavaScript client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="b52c2-104">В этом руководстве показано, как реализовать типичные сценарии с использованием последней версии [пакета SDK JavaScript для мобильных приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="b52c2-104">This guide teaches you to perform common scenarios using the latest [JavaScript SDK for Azure Mobile Apps].</span></span> <span data-ttu-id="b52c2-105">Если вы не знакомы с мобильными приложениями Azure, сначала изучите статью [Быстрый запуск мобильного приложения Azure] , чтобы создать серверную часть и таблицу.</span><span class="sxs-lookup"><span data-stu-id="b52c2-105">If you are new to Azure Mobile Apps, first complete [Azure Mobile Apps Quick Start] to create a backend and create a table.</span></span> <span data-ttu-id="b52c2-106">В этом руководстве мы рассмотрим использование мобильного внутреннего сервера в веб-приложениях HTML и JavaScript.</span><span class="sxs-lookup"><span data-stu-id="b52c2-106">In this guide, we focus on using the mobile backend in HTML/JavaScript Web applications.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="b52c2-107">Поддерживаемые платформы</span><span class="sxs-lookup"><span data-stu-id="b52c2-107">Supported platforms</span></span>
<span data-ttu-id="b52c2-108">Для текущей и последней версий поддерживаются основные браузеры: Google Chrome, Microsoft Edge, Microsoft Internet Explorer и Mozilla Firefox.</span><span class="sxs-lookup"><span data-stu-id="b52c2-108">We limit browser support to the current and last versions of the major browsers:  Google Chrome, Microsoft Edge, Microsoft Internet Explorer, and Mozilla Firefox.</span></span>  <span data-ttu-id="b52c2-109">Ожидается, что пакет SDK будет работать с любым относительно современным браузером.</span><span class="sxs-lookup"><span data-stu-id="b52c2-109">We expect the SDK to function with any relatively modern browser.</span></span>

<span data-ttu-id="b52c2-110">Этот пакет распространяется в виде универсального модуля JavaScript, поэтому он поддерживает глобальные переменные, AMD и форматы CommonJS.</span><span class="sxs-lookup"><span data-stu-id="b52c2-110">The package is distributed as a Universal JavaScript Module, so it supports globals, AMD, and CommonJS formats.</span></span>

## <span data-ttu-id="b52c2-111"><a name="Setup"></a>Настройка и необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="b52c2-111"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="b52c2-112">В данном руководстве предполагается, что вы уже создали серверную часть с таблицей.</span><span class="sxs-lookup"><span data-stu-id="b52c2-112">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="b52c2-113">В этом руководстве предполагается, что в таблице используется та же схему, что и в таблицах, приведенных в этих учебниках.</span><span class="sxs-lookup"><span data-stu-id="b52c2-113">This guide assumes that the table has the same schema as the tables in those tutorials.</span></span>

<span data-ttu-id="b52c2-114">Установить пакет SDK JavaScript для мобильных приложений Azure можно с помощью команды `npm` .</span><span class="sxs-lookup"><span data-stu-id="b52c2-114">Installing the Azure Mobile Apps JavaScript SDK can be done via the `npm` command:</span></span>

```
npm install azure-mobile-apps-client --save
```

<span data-ttu-id="b52c2-115">Библиотеку также можно использовать как модуль ES2015 в средах CommonJS, таких как Browserify и Webpack, а также как библиотеку AMD.</span><span class="sxs-lookup"><span data-stu-id="b52c2-115">The library can also be used as an ES2015 module, within CommonJS environments such as Browserify and Webpack and as an AMD library.</span></span>  <span data-ttu-id="b52c2-116">Например:</span><span class="sxs-lookup"><span data-stu-id="b52c2-116">For example:</span></span>

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

<span data-ttu-id="b52c2-117">Можно также использовать готовую версию пакета SDK, скачав ее непосредственно из нашей сети CDN.</span><span class="sxs-lookup"><span data-stu-id="b52c2-117">You can also use a pre-built version of the SDK by downloading directly from our CDN:</span></span>

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="b52c2-118"><a name="auth"></a>Практическое руководство. Проверка подлинности пользователей</span><span class="sxs-lookup"><span data-stu-id="b52c2-118"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="b52c2-119">Служба приложений Azure поддерживает аутентификацию и авторизацию пользователей с помощью различных внешних поставщиков удостоверений: Facebook, Google, учетная запись Майкрософт и Twitter.</span><span class="sxs-lookup"><span data-stu-id="b52c2-119">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="b52c2-120">Можно задать разрешения таблиц, чтобы предоставить доступ к определенным операциям только пользователям, прошедшим проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="b52c2-120">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="b52c2-121">Удостоверения пользователей, прошедших проверку подлинности, также можно применять для реализации правил авторизации в серверных скриптах.</span><span class="sxs-lookup"><span data-stu-id="b52c2-121">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span></span> <span data-ttu-id="b52c2-122">Дополнительные сведения см. в учебнике [Приступая к работе с проверкой подлинности].</span><span class="sxs-lookup"><span data-stu-id="b52c2-122">For more information, see the [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="b52c2-123">Поддерживается два потока аутентификации: серверный и клиентский.</span><span class="sxs-lookup"><span data-stu-id="b52c2-123">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="b52c2-124">Серверный поток обеспечивает самый простой способ проверки подлинности, так как он использует веб-интерфейс проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="b52c2-124">The server flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span></span> <span data-ttu-id="b52c2-125">Клиентский поток обеспечивает более тесную интеграцию с возможностями устройства, такими как единый вход, так как использует пакеты SDK конкретного поставщика.</span><span class="sxs-lookup"><span data-stu-id="b52c2-125">The client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="b52c2-126"><a name="configure-external-redirect-urls"></a>Практическое руководство. Настройка службы мобильных приложений для внешних URL-адресов перенаправления</span><span class="sxs-lookup"><span data-stu-id="b52c2-126"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="b52c2-127">Для обработки потоков пользовательского интерфейса OAuth некоторые типы приложений JavaScript используют функцию замыкания на себя.</span><span class="sxs-lookup"><span data-stu-id="b52c2-127">Several types of JavaScript applications use a loopback capability to handle OAuth UI flows.</span></span>  <span data-ttu-id="b52c2-128">К этим возможностям относятся следующие:</span><span class="sxs-lookup"><span data-stu-id="b52c2-128">These capabilities include:</span></span>

* <span data-ttu-id="b52c2-129">выполнение службы в локальной среде;</span><span class="sxs-lookup"><span data-stu-id="b52c2-129">Running your service locally</span></span>
* <span data-ttu-id="b52c2-130">использование динамической перезагрузки с платформой Ionic;</span><span class="sxs-lookup"><span data-stu-id="b52c2-130">Using Live Reload with the Ionic Framework</span></span>
* <span data-ttu-id="b52c2-131">перенаправление в службу приложений для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="b52c2-131">Redirecting to App Service for authentication.</span></span>

<span data-ttu-id="b52c2-132">Выполнение в локальной среде может вызвать проблемы, так как по умолчанию аутентификация службы приложений настроена только для доступа из серверной части мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="b52c2-132">Running locally can cause problems because, by default, App Service authentication is only configured to allow access from your Mobile App backend.</span></span> <span data-ttu-id="b52c2-133">Следуйте инструкциям ниже, чтобы изменить параметры службы приложений для включения аутентификации при выполнении сервера в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="b52c2-133">Use the following steps to change the App Service settings to enable authentication when running the server locally:</span></span>

1. <span data-ttu-id="b52c2-134">Войдите на [портал Azure]</span><span class="sxs-lookup"><span data-stu-id="b52c2-134">Log in to the [Azure portal]</span></span>
2. <span data-ttu-id="b52c2-135">Перейдите к серверной части мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="b52c2-135">Navigate to your Mobile App backend.</span></span>
3. <span data-ttu-id="b52c2-136">В меню **Средства разработки** выберите **Обозреватель ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="b52c2-136">Select **Resource explorer** in the **DEVELOPMENT TOOLS** menu.</span></span>
4. <span data-ttu-id="b52c2-137">Щелкните **Перейти** , чтобы открыть обозреватель ресурсов для серверной части мобильного приложения в новой вкладке или окне.</span><span class="sxs-lookup"><span data-stu-id="b52c2-137">Click **Go** to open the resource explorer for your Mobile App backend in a new tab or window.</span></span>
5. <span data-ttu-id="b52c2-138">Разверните узел **config** > **authsettings** для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="b52c2-138">Expand the **config** > **authsettings** node for your app.</span></span>
6. <span data-ttu-id="b52c2-139">Нажмите кнопку **Изменить** , чтобы включить режим редактирования ресурса.</span><span class="sxs-lookup"><span data-stu-id="b52c2-139">Click the **Edit** button to enable editing of the resource.</span></span>
7. <span data-ttu-id="b52c2-140">Найдите элемент **allowedExternalRedirectUrls** , который должен иметь значение NULL.</span><span class="sxs-lookup"><span data-stu-id="b52c2-140">Find the **allowedExternalRedirectUrls** element, which should be null.</span></span> <span data-ttu-id="b52c2-141">Добавьте URL-адреса в массив.</span><span class="sxs-lookup"><span data-stu-id="b52c2-141">Add your URLs in an array:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="b52c2-142">Замените URL-адреса в массиве URL-адресами службы. В данном примере — это `http://localhost:3000` для локального примера службы Node.js.</span><span class="sxs-lookup"><span data-stu-id="b52c2-142">Replace the URLs in the array with the URLs of your service, which in this example is `http://localhost:3000` for the local Node.js sample service.</span></span> <span data-ttu-id="b52c2-143">Можно также использовать адрес `http://localhost:4400` для службы Ripple или для других URL-адресов, в зависимости от настроек приложения.</span><span class="sxs-lookup"><span data-stu-id="b52c2-143">You could also use `http://localhost:4400` for the Ripple service or some other URL, depending on how your app is configured.</span></span>
8. <span data-ttu-id="b52c2-144">В верхней части страницы щелкните **Чтение и запись**, затем щелкните **PUT**, чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="b52c2-144">At the top of the page, click **Read/Write**, then click **PUT** to save your updates.</span></span>

<span data-ttu-id="b52c2-145">Вам также необходимо добавить URL-адреса замыкания на себя в настройках списка разрешений CORS.</span><span class="sxs-lookup"><span data-stu-id="b52c2-145">You also need to add the same loopback URLs to the CORS whitelist settings:</span></span>

1. <span data-ttu-id="b52c2-146">Вернитесь на [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="b52c2-146">Navigate back to the [Azure portal].</span></span>
2. <span data-ttu-id="b52c2-147">Перейдите к серверной части мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="b52c2-147">Navigate to your Mobile App backend.</span></span>
3. <span data-ttu-id="b52c2-148">В меню **API** щелкните **CORS**.</span><span class="sxs-lookup"><span data-stu-id="b52c2-148">Click **CORS** in the **API** menu.</span></span>
4. <span data-ttu-id="b52c2-149">Введите каждый URL-адрес в пустое текстовое поле **Разрешенные источники** .</span><span class="sxs-lookup"><span data-stu-id="b52c2-149">Enter each URL in the empty **Allowed Origins** text box.</span></span>  <span data-ttu-id="b52c2-150">Будет создано новое текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="b52c2-150">A new text box is created.</span></span>
5. <span data-ttu-id="b52c2-151">Щелкните **Сохранить**</span><span class="sxs-lookup"><span data-stu-id="b52c2-151">Click **SAVE**</span></span>

<span data-ttu-id="b52c2-152">После обновления серверной части мобильного приложения вы сможете использовать новые URL-адреса замыкания на себя в приложении.</span><span class="sxs-lookup"><span data-stu-id="b52c2-152">After the backend updates, you will be able to use the new loopback URLs in your app.</span></span>

<!-- URLs. -->
<span data-ttu-id="b52c2-153">[Быстрый запуск мобильного приложения Azure]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="b52c2-153">[Azure Mobile Apps Quick Start]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="b52c2-154">[Приступая к работе с проверкой подлинности]: app-service-mobile-cordova-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="b52c2-154">[Get started with authentication]: app-service-mobile-cordova-get-started-users.md</span></span>
[Add authentication to your app]: app-service-mobile-cordova-get-started-users.md

<span data-ttu-id="b52c2-155">[портал Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="b52c2-155">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="b52c2-156">[пакета SDK JavaScript для мобильных приложений Azure]: https://www.npmjs.com/package/azure-mobile-apps-client</span><span class="sxs-lookup"><span data-stu-id="b52c2-156">[JavaScript SDK for Azure Mobile Apps]: https://www.npmjs.com/package/azure-mobile-apps-client</span></span>
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
