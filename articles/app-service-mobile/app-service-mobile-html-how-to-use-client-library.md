---
title: "hello tooUse aaaHow JavaScript SDK для мобильных приложений Azure"
description: "Как v tooUse для мобильных приложений Azure"
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
ms.openlocfilehash: 3fcbb0c5bd6918a285bdafa1946ba0bd47bb21b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-javascript-client-library-for-azure-mobile-apps"></a><span data-ttu-id="7db91-103">Как tooUse hello клиентская библиотека JavaScript для мобильных приложений Azure</span><span class="sxs-lookup"><span data-stu-id="7db91-103">How tooUse hello JavaScript client library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="7db91-104">Это руководство поможет tooperform распространенные сценарии, с помощью hello последней [JavaScript SDK для мобильных приложений Azure].</span><span class="sxs-lookup"><span data-stu-id="7db91-104">This guide teaches you tooperform common scenarios using hello latest [JavaScript SDK for Azure Mobile Apps].</span></span> <span data-ttu-id="7db91-105">Если новый tooAzure мобильные приложения, сначала завершите [быстрого запуска Azure мобильных приложений] toocreate серверной части и создайте таблицу.</span><span class="sxs-lookup"><span data-stu-id="7db91-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend and create a table.</span></span> <span data-ttu-id="7db91-106">В этом руководстве мы сосредоточиться на использование мобильной серверной части hello в HTML/JavaScript веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="7db91-106">In this guide, we focus on using hello mobile backend in HTML/JavaScript Web applications.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="7db91-107">Поддерживаемые платформы</span><span class="sxs-lookup"><span data-stu-id="7db91-107">Supported platforms</span></span>
<span data-ttu-id="7db91-108">Мы ограничить текущего toohello поддержки браузера и последние версии hello основные обозреватели: Google Chrome, Microsoft Edge, Microsoft Internet Explorer и Mozilla Firefox.</span><span class="sxs-lookup"><span data-stu-id="7db91-108">We limit browser support toohello current and last versions of hello major browsers:  Google Chrome, Microsoft Edge, Microsoft Internet Explorer, and Mozilla Firefox.</span></span>  <span data-ttu-id="7db91-109">Ожидается, что toofunction hello SDK с любого относительно современного браузера.</span><span class="sxs-lookup"><span data-stu-id="7db91-109">We expect hello SDK toofunction with any relatively modern browser.</span></span>

<span data-ttu-id="7db91-110">Hello пакета распространяется в виде универсального модуля JavaScript, поэтому он поддерживает globals, AMD, CommonJS формат и.</span><span class="sxs-lookup"><span data-stu-id="7db91-110">hello package is distributed as a Universal JavaScript Module, so it supports globals, AMD, and CommonJS formats.</span></span>

## <span data-ttu-id="7db91-111"><a name="Setup"></a>Настройка и необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="7db91-111"><a name="Setup"></a>Setup and prerequisites</span></span>
<span data-ttu-id="7db91-112">В данном руководстве предполагается, что вы уже создали серверную часть с таблицей.</span><span class="sxs-lookup"><span data-stu-id="7db91-112">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="7db91-113">В этом руководстве предполагается, что таблица hello имеет hello одной схеме с таблицами hello в этих учебниках.</span><span class="sxs-lookup"><span data-stu-id="7db91-113">This guide assumes that hello table has hello same schema as hello tables in those tutorials.</span></span>

<span data-ttu-id="7db91-114">Установка hello JavaScript SDK Azure Mobile приложения можно сделать с помощью hello `npm` команды:</span><span class="sxs-lookup"><span data-stu-id="7db91-114">Installing hello Azure Mobile Apps JavaScript SDK can be done via hello `npm` command:</span></span>

```
npm install azure-mobile-apps-client --save
```

<span data-ttu-id="7db91-115">Библиотека Hello также может использоваться в качестве ES2015 модуля, в средах CommonJS, например Browserify и Webpack и как библиотека AMD.</span><span class="sxs-lookup"><span data-stu-id="7db91-115">hello library can also be used as an ES2015 module, within CommonJS environments such as Browserify and Webpack and as an AMD library.</span></span>  <span data-ttu-id="7db91-116">Например:</span><span class="sxs-lookup"><span data-stu-id="7db91-116">For example:</span></span>

```
# For ECMAScript 5.1 CommonJS
var WindowsAzure = require('azure-mobile-apps-client');
# For ES2015 modules
import * as WindowsAzure from 'azure-mobile-apps-client';
```

<span data-ttu-id="7db91-117">Также можно использовать предварительно построенного версию пакета SDK для hello, загружая непосредственно из наших CDN:</span><span class="sxs-lookup"><span data-stu-id="7db91-117">You can also use a pre-built version of hello SDK by downloading directly from our CDN:</span></span>

```html
<script src="https://zumo.blob.core.windows.net/sdk/azure-mobile-apps-client.min.js"></script>
```

[!INCLUDE [app-service-mobile-html-js-library](../../includes/app-service-mobile-html-js-library.md)]

## <span data-ttu-id="7db91-118"><a name="auth"></a>Практическое руководство. Проверка подлинности пользователей</span><span class="sxs-lookup"><span data-stu-id="7db91-118"><a name="auth"></a>How to: Authenticate users</span></span>
<span data-ttu-id="7db91-119">Служба приложений Azure поддерживает аутентификацию и авторизацию пользователей с помощью различных внешних поставщиков удостоверений: Facebook, Google, учетная запись Майкрософт и Twitter.</span><span class="sxs-lookup"><span data-stu-id="7db91-119">Azure App Service supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, and Twitter.</span></span> <span data-ttu-id="7db91-120">Можно задать разрешения для таблицы toorestrict доступ для определенных операций tooonly проверку подлинности пользователей.</span><span class="sxs-lookup"><span data-stu-id="7db91-120">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="7db91-121">Hello идентификаторов правил авторизации tooimplement прошедших проверку подлинности пользователей также можно использовать в серверных скриптах.</span><span class="sxs-lookup"><span data-stu-id="7db91-121">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="7db91-122">Дополнительные сведения см. в разделе hello [приступить к работе с проверкой подлинности] учебника.</span><span class="sxs-lookup"><span data-stu-id="7db91-122">For more information, see hello [Get started with authentication] tutorial.</span></span>

<span data-ttu-id="7db91-123">Поддерживается два потока аутентификации: серверный и клиентский.</span><span class="sxs-lookup"><span data-stu-id="7db91-123">Two authentication flows are supported: a server flow and a client flow.</span></span>  <span data-ttu-id="7db91-124">поток Hello server обеспечивает hello простой проверки подлинности, как зависит от поставщика hello веб-интерфейс проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="7db91-124">hello server flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="7db91-125">Hello потока клиента обеспечивает более глубокую интеграцию с возможности определенных устройств, таких как-единого входа, зависит от конкретного поставщика SDK.</span><span class="sxs-lookup"><span data-stu-id="7db91-125">hello client flow allows for deeper integration with device-specific capabilities such as single-sign-on as it relies on provider-specific SDKs.</span></span>

[!INCLUDE [app-service-mobile-html-js-auth-library](../../includes/app-service-mobile-html-js-auth-library.md)]

### <span data-ttu-id="7db91-126"><a name="configure-external-redirect-urls"></a>Практическое руководство. Настройка службы мобильных приложений для внешних URL-адресов перенаправления</span><span class="sxs-lookup"><span data-stu-id="7db91-126"><a name="configure-external-redirect-urls"></a>How to: Configure your Mobile App Service for external redirect URLs.</span></span>
<span data-ttu-id="7db91-127">Несколько типов приложений JavaScript используйте toohandle возможность замыкания на себя, потоков пользовательского интерфейса OAuth.</span><span class="sxs-lookup"><span data-stu-id="7db91-127">Several types of JavaScript applications use a loopback capability toohandle OAuth UI flows.</span></span>  <span data-ttu-id="7db91-128">К этим возможностям относятся следующие:</span><span class="sxs-lookup"><span data-stu-id="7db91-128">These capabilities include:</span></span>

* <span data-ttu-id="7db91-129">выполнение службы в локальной среде;</span><span class="sxs-lookup"><span data-stu-id="7db91-129">Running your service locally</span></span>
* <span data-ttu-id="7db91-130">С помощью Live перезагрузить с hello платформы Ionic</span><span class="sxs-lookup"><span data-stu-id="7db91-130">Using Live Reload with hello Ionic Framework</span></span>
* <span data-ttu-id="7db91-131">Перенаправление tooApp службы для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="7db91-131">Redirecting tooApp Service for authentication.</span></span>

<span data-ttu-id="7db91-132">Локальное выполнение может вызвать проблемы, поскольку по умолчанию приложение службы проверки подлинности только в том случае tooallow доступ из мобильного приложения серверной части.</span><span class="sxs-lookup"><span data-stu-id="7db91-132">Running locally can cause problems because, by default, App Service authentication is only configured tooallow access from your Mobile App backend.</span></span> <span data-ttu-id="7db91-133">Используйте следующие hello toochange действия проверки подлинности tooenable параметров приложения службы при запуске сервера hello локально hello.</span><span class="sxs-lookup"><span data-stu-id="7db91-133">Use hello following steps toochange hello App Service settings tooenable authentication when running hello server locally:</span></span>

1. <span data-ttu-id="7db91-134">Войдите в toohello [портал Azure]</span><span class="sxs-lookup"><span data-stu-id="7db91-134">Log in toohello [Azure portal]</span></span>
2. <span data-ttu-id="7db91-135">Перейдите в серверной части tooyour мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="7db91-135">Navigate tooyour Mobile App backend.</span></span>
3. <span data-ttu-id="7db91-136">Выберите **обозреватель ресурсов** в hello **средства разработки** меню.</span><span class="sxs-lookup"><span data-stu-id="7db91-136">Select **Resource explorer** in hello **DEVELOPMENT TOOLS** menu.</span></span>
4. <span data-ttu-id="7db91-137">Нажмите кнопку **Go** обозреватель ресурсов hello tooopen для серверной части мобильных приложений в новой вкладке или окне.</span><span class="sxs-lookup"><span data-stu-id="7db91-137">Click **Go** tooopen hello resource explorer for your Mobile App backend in a new tab or window.</span></span>
5. <span data-ttu-id="7db91-138">Разверните hello **config** > **authsettings** узла приложения.</span><span class="sxs-lookup"><span data-stu-id="7db91-138">Expand hello **config** > **authsettings** node for your app.</span></span>
6. <span data-ttu-id="7db91-139">Нажмите кнопку hello **изменить** кнопку tooenable редактирование ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="7db91-139">Click hello **Edit** button tooenable editing of hello resource.</span></span>
7. <span data-ttu-id="7db91-140">Найти hello **allowedExternalRedirectUrls** элемент, который должен иметь значение null.</span><span class="sxs-lookup"><span data-stu-id="7db91-140">Find hello **allowedExternalRedirectUrls** element, which should be null.</span></span> <span data-ttu-id="7db91-141">Добавьте URL-адреса в массив.</span><span class="sxs-lookup"><span data-stu-id="7db91-141">Add your URLs in an array:</span></span>

         "allowedExternalRedirectUrls": [
             "http://localhost:3000",
             "https://localhost:3000"
         ],

    <span data-ttu-id="7db91-142">Замените URL-адреса hello в массиве hello hello URL-адреса службы, который в данном примере — `http://localhost:3000` для образца службы локального Node.js hello.</span><span class="sxs-lookup"><span data-stu-id="7db91-142">Replace hello URLs in hello array with hello URLs of your service, which in this example is `http://localhost:3000` for hello local Node.js sample service.</span></span> <span data-ttu-id="7db91-143">Можно также использовать `http://localhost:4400` для службы Ripple hello или некоторые другие URL-адрес, в зависимости от настроек приложения.</span><span class="sxs-lookup"><span data-stu-id="7db91-143">You could also use `http://localhost:4400` for hello Ripple service or some other URL, depending on how your app is configured.</span></span>
8. <span data-ttu-id="7db91-144">В начале hello страницы приветствия, нажмите кнопку **чтения и записи**, нажмите кнопку **ПОМЕСТИТЬ** toosave обновления.</span><span class="sxs-lookup"><span data-stu-id="7db91-144">At hello top of hello page, click **Read/Write**, then click **PUT** toosave your updates.</span></span>

<span data-ttu-id="7db91-145">Необходимо также tooadd hello же замыкания на себя URL-адреса toohello CORS белый список параметров:</span><span class="sxs-lookup"><span data-stu-id="7db91-145">You also need tooadd hello same loopback URLs toohello CORS whitelist settings:</span></span>

1. <span data-ttu-id="7db91-146">Перейдите назад toohello [портал Azure].</span><span class="sxs-lookup"><span data-stu-id="7db91-146">Navigate back toohello [Azure portal].</span></span>
2. <span data-ttu-id="7db91-147">Перейдите в серверной части tooyour мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="7db91-147">Navigate tooyour Mobile App backend.</span></span>
3. <span data-ttu-id="7db91-148">Нажмите кнопку **CORS** в hello **API** меню.</span><span class="sxs-lookup"><span data-stu-id="7db91-148">Click **CORS** in hello **API** menu.</span></span>
4. <span data-ttu-id="7db91-149">Введите каждый URL-адрес в пустой hello **источники, которые разрешено** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="7db91-149">Enter each URL in hello empty **Allowed Origins** text box.</span></span>  <span data-ttu-id="7db91-150">Будет создано новое текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="7db91-150">A new text box is created.</span></span>
5. <span data-ttu-id="7db91-151">Щелкните **Сохранить**</span><span class="sxs-lookup"><span data-stu-id="7db91-151">Click **SAVE**</span></span>

<span data-ttu-id="7db91-152">После обновления серверной hello, можно будет toouse hello новые замыкания на себя URL-адреса в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="7db91-152">After hello backend updates, you will be able toouse hello new loopback URLs in your app.</span></span>

<!-- URLs. -->
[быстрого запуска Azure мобильных приложений]: app-service-mobile-cordova-get-started.md
[приступить к работе с проверкой подлинности]: app-service-mobile-cordova-get-started-users.md
[Add authentication tooyour app]: app-service-mobile-cordova-get-started-users.md

[портал Azure]: https://portal.azure.com/
[JavaScript SDK для мобильных приложений Azure]: https://www.npmjs.com/package/azure-mobile-apps-client
[Query object documentation]: https://msdn.microsoft.com/en-us/library/azure/jj613353.aspx
