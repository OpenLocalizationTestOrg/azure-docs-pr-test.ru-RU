---
title: "aaaAdd проверки подлинности на Apache Cordova с помощью мобильных приложений | Документы Microsoft"
description: "Узнайте, как toouse мобильные приложения в службе приложений Azure tooauthenticate пользователей приложения Apache Cordova с помощью различных поставщиков удостоверений, включая Google, Facebook, Twitter и Microsoft."
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 10dd6dc9-ddf5-423d-8205-00ad74929f0d
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 61a05c5ac67fd0f0bc4c9d6920954a9b464a0a8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-apache-cordova-app"></a><span data-ttu-id="01f02-103">Добавление приложения Apache Cordova tooyour проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="01f02-103">Add authentication tooyour Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="01f02-104">Сводка</span><span class="sxs-lookup"><span data-stu-id="01f02-104">Summary</span></span>
<span data-ttu-id="01f02-105">В этом учебнике добавьте проект краткое руководство todolist toohello проверки подлинности на Apache Cordova с помощью поставщика удостоверений, поддерживаемых.</span><span class="sxs-lookup"><span data-stu-id="01f02-105">In this tutorial, you add authentication toohello todolist quickstart project on Apache Cordova using a supported identity provider.</span></span> <span data-ttu-id="01f02-106">Этот учебник основывается на hello [начало работы с мобильным приложениям] руководство, в котором необходимо выполнять первой.</span><span class="sxs-lookup"><span data-stu-id="01f02-106">This tutorial is based on hello [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="01f02-107"><a name="register"></a>Регистрация приложения для проверки подлинности и настройка hello службы приложений</span><span class="sxs-lookup"><span data-stu-id="01f02-107"><a name="register"></a>Register your app for authentication and configure hello App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[<span data-ttu-id="01f02-108">Видео, демонстрирующее аналогичные действия</span><span class="sxs-lookup"><span data-stu-id="01f02-108">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <span data-ttu-id="01f02-109"><a name="permissions"></a>Ограничить разрешения пользователей tooauthenticated</span><span class="sxs-lookup"><span data-stu-id="01f02-109"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="01f02-110">Теперь вы можете подтвердить этой серверной tooyour анонимный доступ отключен.</span><span class="sxs-lookup"><span data-stu-id="01f02-110">Now, you can verify that anonymous access tooyour backend has been disabled.</span></span> <span data-ttu-id="01f02-111">В Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="01f02-111">In Visual Studio:</span></span>

* <span data-ttu-id="01f02-112">Привет открыть проект, созданный после завершения учебника hello [начало работы с мобильным приложениям].</span><span class="sxs-lookup"><span data-stu-id="01f02-112">Open hello project that you created when you completed hello tutorial [Get started with Mobile Apps].</span></span>
* <span data-ttu-id="01f02-113">Запустите приложение в hello **эмулятор Android Google**.</span><span class="sxs-lookup"><span data-stu-id="01f02-113">Run your application in hello **Google Android Emulator**.</span></span>
* <span data-ttu-id="01f02-114">Непредвиденный сбой соединения проверьте, отображается ли после запуска приложение hello.</span><span class="sxs-lookup"><span data-stu-id="01f02-114">Verify that an Unexpected Connection Failure is shown after hello app starts.</span></span>

<span data-ttu-id="01f02-115">Затем обновите пользователи tooauthenticate приложения hello, прежде чем запрашивать ресурсы из внутреннего сервера мобильного приложения hello.</span><span class="sxs-lookup"><span data-stu-id="01f02-115">Next, update hello app tooauthenticate users before requesting resources from hello Mobile App backend.</span></span>

## <span data-ttu-id="01f02-116"><a name="add-authentication"></a>Добавить приложение toohello проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="01f02-116"><a name="add-authentication"></a>Add authentication toohello app</span></span>
1. <span data-ttu-id="01f02-117">Откройте проект в **Visual Studio**, затем откройте hello `www/index.html` файл для редактирования.</span><span class="sxs-lookup"><span data-stu-id="01f02-117">Open your project in **Visual Studio**, then open hello `www/index.html` file for editing.</span></span>
2. <span data-ttu-id="01f02-118">Найдите hello `Content-Security-Policy` метатег в раздел head hello.</span><span class="sxs-lookup"><span data-stu-id="01f02-118">Locate hello `Content-Security-Policy` meta tag in hello head section.</span></span>  <span data-ttu-id="01f02-119">Добавьте hello узла OAuth toohello список разрешенных источников.</span><span class="sxs-lookup"><span data-stu-id="01f02-119">Add hello OAuth host toohello list of allowed sources.</span></span>

   | <span data-ttu-id="01f02-120">Поставщик</span><span class="sxs-lookup"><span data-stu-id="01f02-120">Provider</span></span> | <span data-ttu-id="01f02-121">Имя поставщика SDK</span><span class="sxs-lookup"><span data-stu-id="01f02-121">SDK Provider Name</span></span> | <span data-ttu-id="01f02-122">Узел OAuth</span><span class="sxs-lookup"><span data-stu-id="01f02-122">OAuth Host</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="01f02-123">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="01f02-123">Azure Active Directory</span></span> | <span data-ttu-id="01f02-124">aad</span><span class="sxs-lookup"><span data-stu-id="01f02-124">aad</span></span> | <span data-ttu-id="01f02-125">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="01f02-125">https://login.microsoftonline.com</span></span> |
   | <span data-ttu-id="01f02-126">Facebook</span><span class="sxs-lookup"><span data-stu-id="01f02-126">Facebook</span></span> | <span data-ttu-id="01f02-127">Facebook</span><span class="sxs-lookup"><span data-stu-id="01f02-127">facebook</span></span> | <span data-ttu-id="01f02-128">https://www.facebook.com</span><span class="sxs-lookup"><span data-stu-id="01f02-128">https://www.facebook.com</span></span> |
   | <span data-ttu-id="01f02-129">Google</span><span class="sxs-lookup"><span data-stu-id="01f02-129">Google</span></span> | <span data-ttu-id="01f02-130">Google</span><span class="sxs-lookup"><span data-stu-id="01f02-130">google</span></span> | <span data-ttu-id="01f02-131">https://accounts.google.com</span><span class="sxs-lookup"><span data-stu-id="01f02-131">https://accounts.google.com</span></span> |
   | <span data-ttu-id="01f02-132">Microsoft</span><span class="sxs-lookup"><span data-stu-id="01f02-132">Microsoft</span></span> | <span data-ttu-id="01f02-133">microsoftaccount</span><span class="sxs-lookup"><span data-stu-id="01f02-133">microsoftaccount</span></span> | <span data-ttu-id="01f02-134">https://login.live.com</span><span class="sxs-lookup"><span data-stu-id="01f02-134">https://login.live.com</span></span> |
   | <span data-ttu-id="01f02-135">Twitter</span><span class="sxs-lookup"><span data-stu-id="01f02-135">Twitter</span></span> | <span data-ttu-id="01f02-136">Twitter</span><span class="sxs-lookup"><span data-stu-id="01f02-136">twitter</span></span> | <span data-ttu-id="01f02-137">https://api.twitter.com</span><span class="sxs-lookup"><span data-stu-id="01f02-137">https://api.twitter.com</span></span> |

    <span data-ttu-id="01f02-138">Пример политики безопасности содержимого (для Azure Active Directory):</span><span class="sxs-lookup"><span data-stu-id="01f02-138">An example Content-Security-Policy (implemented for Azure Active Directory) is as follows:</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.microsoftonline.com https://yourapp.azurewebsites.net; style-src 'self'">

    <span data-ttu-id="01f02-139">Замените `https://login.microsoftonline.com` с узлом OAuth hello из hello предшествующей таблице.</span><span class="sxs-lookup"><span data-stu-id="01f02-139">Replace `https://login.microsoftonline.com` with hello OAuth host from hello preceding table.</span></span>  <span data-ttu-id="01f02-140">Дополнительные сведения о метатег политики безопасности содержимого hello. в разделе hello [документации политики безопасности содержимого].</span><span class="sxs-lookup"><span data-stu-id="01f02-140">For more information about hello content-security-policy meta tag, see hello [Content-Security-Policy documentation].</span></span>

    <span data-ttu-id="01f02-141">Некоторые поставщики аутентификации не требуют изменений в политике безопасности содержимого при использовании на соответствующих мобильных устройствах.</span><span class="sxs-lookup"><span data-stu-id="01f02-141">Some authentication providers do not require Content-Security-Policy changes when used on appropriate mobile devices.</span></span>  <span data-ttu-id="01f02-142">Например, изменения в политики безопасности содержимого не требуются, если на устройстве Android используется проверка подлинности Google.</span><span class="sxs-lookup"><span data-stu-id="01f02-142">For example, no Content-Security-Policy changes are required when using Google authentication on an Android device.</span></span>

3. <span data-ttu-id="01f02-143">Откройте hello `www/js/index.js` файл для редактирования, найдите hello `onDeviceReady()` метод, и создание клиента hello кода добавьте hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="01f02-143">Open hello `www/js/index.js` file for editing, locate hello `onDeviceReady()` method, and under hello client  creation code add hello following code:</span></span>

        // Login toohello service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    <span data-ttu-id="01f02-144">Этот код заменяет hello существующий код, который создает ссылку на таблицу hello и обновляет hello пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="01f02-144">This code replaces hello existing code that creates hello table reference and refreshes hello UI.</span></span>

    <span data-ttu-id="01f02-145">метод login() Hello запускает проверку подлинности с поставщиком hello.</span><span class="sxs-lookup"><span data-stu-id="01f02-145">hello login() method starts authentication with hello provider.</span></span> <span data-ttu-id="01f02-146">метод login() Hello является асинхронной функции, которая возвращает объект Promise в JavaScript.</span><span class="sxs-lookup"><span data-stu-id="01f02-146">hello login() method is an async function that returns a JavaScript Promise.</span></span>  <span data-ttu-id="01f02-147">Hello остальная часть инициализации hello помещается внутри hello promise ответа, чтобы он не выполняется до завершения метода login() hello.</span><span class="sxs-lookup"><span data-stu-id="01f02-147">hello rest of hello initialization is placed inside hello promise response so that it is not executed until hello login() method completes.</span></span>

4. <span data-ttu-id="01f02-148">В коде hello только что добавленную замените `SDK_Provider_Name` с именем hello поставщика входа.</span><span class="sxs-lookup"><span data-stu-id="01f02-148">In hello code that you just added, replace `SDK_Provider_Name` with hello name of your login provider.</span></span> <span data-ttu-id="01f02-149">Например, для Azure Active Directory используйте `client.login('aad')`.</span><span class="sxs-lookup"><span data-stu-id="01f02-149">For example, for Azure Active Directory, use `client.login('aad')`.</span></span>
5. <span data-ttu-id="01f02-150">Запустите проект.</span><span class="sxs-lookup"><span data-stu-id="01f02-150">Run your project.</span></span>  <span data-ttu-id="01f02-151">После завершения инициализации hello проекта приложения показана страница входа hello OAuth для hello выбранного поставщика проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="01f02-151">When hello project has finished initializing, your application shows hello OAuth login page for hello chosen authentication provider.</span></span>

## <span data-ttu-id="01f02-152"><a name="next-steps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="01f02-152"><a name="next-steps"></a>Next Steps</span></span>
* <span data-ttu-id="01f02-153">Узнайте больше об [аутентификации] с использованием службы приложений Azure.</span><span class="sxs-lookup"><span data-stu-id="01f02-153">Learn more [About Authentication] with Azure App Service.</span></span>
* <span data-ttu-id="01f02-154">Продолжить работу с учебником hello, добавив [Push-уведомления] tooyour приложения Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="01f02-154">Continue hello tutorial by adding [Push Notifications] tooyour Apache Cordova app.</span></span>

<span data-ttu-id="01f02-155">Узнайте, как toouse hello пакетов SDK.</span><span class="sxs-lookup"><span data-stu-id="01f02-155">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="01f02-156">[Пакет SDK для Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="01f02-156">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="01f02-157">[Серверный пакет SDK для ASP.NET]</span><span class="sxs-lookup"><span data-stu-id="01f02-157">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="01f02-158">[Серверный пакет SDK для Node.js]</span><span class="sxs-lookup"><span data-stu-id="01f02-158">[Node.js Server SDK]</span></span>

<!-- URLs. -->
[начало работы с мобильным приложениям]: app-service-mobile-cordova-get-started.md
[документации политики безопасности содержимого]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html
[Push-уведомления]: app-service-mobile-cordova-get-started-push.md
[аутентификации]: app-service-mobile-auth.md
[Пакет SDK для Apache Cordova]: app-service-mobile-cordova-how-to-use-client-library.md
[Серверный пакет SDK для ASP.NET]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Серверный пакет SDK для Node.js]: app-service-mobile-node-backend-how-to-use-server-sdk.md
