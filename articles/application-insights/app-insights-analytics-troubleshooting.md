---
title: "Устранение неполадок аналитики в Azure Application Insights | Документация Майкрософт"
description: "Возникли проблемы с аналитикой Application Insights? Начните отсюда. "
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9bbd5859-3584-4d80-9b6d-d5910fa48baa
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/11/2016
ms.author: bwren
ms.openlocfilehash: 02df117908fc1790e8cfb9ec0a7218c1b8be856c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-analytics-in-application-insights"></a><span data-ttu-id="b4450-104">Устранение неполадок аналитики в Application Insights</span><span class="sxs-lookup"><span data-stu-id="b4450-104">Troubleshoot Analytics in Application Insights</span></span>
<span data-ttu-id="b4450-105">Возникли проблемы с [аналитикой Application Insights](app-insights-analytics.md)?</span><span class="sxs-lookup"><span data-stu-id="b4450-105">Problems with [Application Insights Analytics](app-insights-analytics.md)?</span></span> <span data-ttu-id="b4450-106">Начните отсюда.</span><span class="sxs-lookup"><span data-stu-id="b4450-106">Start here.</span></span> <span data-ttu-id="b4450-107">Аналитика — мощный инструмент поиска Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b4450-107">Analytics is the powerful search tool of Azure Application Insights.</span></span>

## <a name="limits"></a><span data-ttu-id="b4450-108">Ограничения</span><span class="sxs-lookup"><span data-stu-id="b4450-108">Limits</span></span>
* <span data-ttu-id="b4450-109">В настоящее время результаты запросов ограничены данными за последнюю неделю.</span><span class="sxs-lookup"><span data-stu-id="b4450-109">At present, query results are limited to just over a week of past data.</span></span>
* <span data-ttu-id="b4450-110">Тестируемые браузеры: последние выпуски Chrome, Edge и Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="b4450-110">Browsers we test on: latest editions of Chrome, Edge, and Internet Explorer.</span></span>

## <a name="known-incompatible-browser-extensions"></a><span data-ttu-id="b4450-111">Известные несовместимые расширения браузеров</span><span class="sxs-lookup"><span data-stu-id="b4450-111">Known incompatible browser extensions</span></span>
* <span data-ttu-id="b4450-112">Ghostery</span><span class="sxs-lookup"><span data-stu-id="b4450-112">Ghostery</span></span>

<span data-ttu-id="b4450-113">Отключите это расширение или используйте другой браузер.</span><span class="sxs-lookup"><span data-stu-id="b4450-113">Disable the extension or use a different browser.</span></span>

## <span data-ttu-id="b4450-114"><a name="e-a"></a> "Непредвиденная ошибка"</span><span class="sxs-lookup"><span data-stu-id="b4450-114"><a name="e-a"></a> "Unexpected error"</span></span>
![Экран непредвиденной ошибки](./media/app-insights-analytics-troubleshooting/010.png)

<span data-ttu-id="b4450-116">Произошла внутренняя ошибка во время выполнения портала — необработанное исключение.</span><span class="sxs-lookup"><span data-stu-id="b4450-116">Internal error occurred during portal runtime – unhandled exception.</span></span>

* <span data-ttu-id="b4450-117">Очистите кэш браузера.</span><span class="sxs-lookup"><span data-stu-id="b4450-117">Clean the browser's cache.</span></span> 

## <span data-ttu-id="b4450-118"><a name="e-b"></a>403… попробуйте перезагрузить</span><span class="sxs-lookup"><span data-stu-id="b4450-118"><a name="e-b"></a>403 ... please try to reload</span></span>
![403... Попробуйте перезагрузить](./media/app-insights-analytics-troubleshooting/020.png)

<span data-ttu-id="b4450-120">Произошла ошибка, связанная с проверкой подлинности (во время проверки подлинности или во время создания маркера доступа).</span><span class="sxs-lookup"><span data-stu-id="b4450-120">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="b4450-121">Возможно, для восстановления портала потребуется изменение параметров браузера.</span><span class="sxs-lookup"><span data-stu-id="b4450-121">The portal may have no way to  recover without changing browser settings.</span></span>

* <span data-ttu-id="b4450-122">Убедитесь, что в браузере [включены сторонние файлы cookie](#cookies) .</span><span class="sxs-lookup"><span data-stu-id="b4450-122">Verify [third party cookies are enabled](#cookies) in the browser.</span></span> 

## <span data-ttu-id="b4450-123"><a name="authentication"></a>403… проверьте зону безопасности</span><span class="sxs-lookup"><span data-stu-id="b4450-123"><a name="authentication"></a>403 ... verify security zone</span></span>
![403... Проверьте зону безопасности](./media/app-insights-analytics-troubleshooting/030.png)

<span data-ttu-id="b4450-125">Произошла ошибка, связанная с проверкой подлинности (во время проверки подлинности или во время создания маркера доступа).</span><span class="sxs-lookup"><span data-stu-id="b4450-125">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="b4450-126">Возможно, для восстановления портала потребуется изменение параметров браузера.</span><span class="sxs-lookup"><span data-stu-id="b4450-126">The portal may have no way to  recover without changing browser settings.</span></span>

1. <span data-ttu-id="b4450-127">Убедитесь, что в браузере [включены сторонние файлы cookie](#cookies) .</span><span class="sxs-lookup"><span data-stu-id="b4450-127">Verify [third party cookies are enabled](#cookies) in the browser.</span></span> 
2. <span data-ttu-id="b4450-128">Вы использовали элемент избранного, закладку или сохраненную ссылку для открытия портала аналитики?</span><span class="sxs-lookup"><span data-stu-id="b4450-128">Did you use a favorite, bookmark or saved link to open the Analytics portal?</span></span> <span data-ttu-id="b4450-129">Вы вошли, используя не те учетные данные, которые использовались при сохранении ссылки?</span><span class="sxs-lookup"><span data-stu-id="b4450-129">Are you signed in with different credentials than you used when you saved the link?</span></span>
3. <span data-ttu-id="b4450-130">Используйте окно браузера в закрытом или анонимном режиме (после закрытия всех окон).</span><span class="sxs-lookup"><span data-stu-id="b4450-130">Try using an in-private/incognito browser window (after closing all such windows).</span></span> <span data-ttu-id="b4450-131">Необходимо будет ввести свои учетные данные.</span><span class="sxs-lookup"><span data-stu-id="b4450-131">You'll have to provide your credentials.</span></span> 
4. <span data-ttu-id="b4450-132">Откройте другое (стандартное) окно браузера и перейдите к [Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b4450-132">Open another (ordinary) browser window and go to [Azure](https://portal.azure.com).</span></span> <span data-ttu-id="b4450-133">Выполните выход. Затем откройте ссылку и выполните вход, используя правильные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="b4450-133">Sign out. Then open your link and sign in with the correct credentials.</span></span>
5. <span data-ttu-id="b4450-134">У пользователей браузеров Edge и Internet Explorer также может возникать эта ошибка, если параметры доверенной зоны не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="b4450-134">Edge and Internet Explorer users can also get this error when trusted zone settings are not supported.</span></span>
   
    <span data-ttu-id="b4450-135">Убедитесь, что [портал аналитики](https://analytics.applicationinsights.io) и [портал Azure Active Directory](https://portal.azure.com) находятся в одной зоне безопасности.</span><span class="sxs-lookup"><span data-stu-id="b4450-135">Verify both [Analytics portal](https://analytics.applicationinsights.io) and [Azure Active Directory portal](https://portal.azure.com) are in the same security zone:</span></span>
   
   * <span data-ttu-id="b4450-136">В Internet Explorer щелкните **Свойства браузера**, **Безопасность**, **Надежные сайты**, **Узлы**.</span><span class="sxs-lookup"><span data-stu-id="b4450-136">In Internet Explorer, open **Internet Options**, **Security**, **Trusted sites**, **Sites**:</span></span>
     
     ![Диалоговое окно "Свойства браузера", добавление сайта в список надежных сайтов](./media/app-insights-analytics-troubleshooting/033.png)
     
     <span data-ttu-id="b4450-138">Если в списке веб-сайтов есть любой из следующих URL-адресов, убедитесь, чтобы и остальные адреса также были включены:</span><span class="sxs-lookup"><span data-stu-id="b4450-138">In the Websites list, if any of the following URLs are included, make sure that the others are included also:</span></span>
     
     <span data-ttu-id="b4450-139">https://analytics.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="b4450-139">https://analytics.applicationinsights.io</span></span><br/>
     <span data-ttu-id="b4450-140">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="b4450-140">https://login.microsoftonline.com</span></span><br/>
     <span data-ttu-id="b4450-141">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="b4450-141">https://login.windows.net</span></span>

## <span data-ttu-id="b4450-142"><a name="e-d"></a>404... Ресурс не найден</span><span class="sxs-lookup"><span data-stu-id="b4450-142"><a name="e-d"></a>404 ... Resource not found</span></span>
![404... Ресурс не найден](./media/app-insights-analytics-troubleshooting/040.png)

<span data-ttu-id="b4450-144">Ресурс приложения был удален из Application Insights и больше не доступен.</span><span class="sxs-lookup"><span data-stu-id="b4450-144">Application resource was deleted from Application Insights and isn’t available anymore.</span></span> <span data-ttu-id="b4450-145">Это может произойти, если сохранить URL-адрес на странице аналитики.</span><span class="sxs-lookup"><span data-stu-id="b4450-145">This can happen if you saved the URL to the Analytics page.</span></span>

## <span data-ttu-id="b4450-146"><a name="e-e"></a>403... Нет авторизации</span><span class="sxs-lookup"><span data-stu-id="b4450-146"><a name="e-e"></a>403 ... No authorization</span></span>
![403... Нет авторизации](./media/app-insights-analytics-troubleshooting/050.png)

<span data-ttu-id="b4450-148">У вас нет разрешения на открытие этого приложения в аналитике.</span><span class="sxs-lookup"><span data-stu-id="b4450-148">You don't have permission to open this application in Analytics.</span></span>

* <span data-ttu-id="b4450-149">Вы получили ссылку от другого пользователя?</span><span class="sxs-lookup"><span data-stu-id="b4450-149">Did you get the link from someone else?</span></span> <span data-ttu-id="b4450-150">Попросите, чтобы вас внесли в список [читателей или участников этой группы ресурсов](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="b4450-150">Ask them to make sure you are in the [readers or contributors for this resource group](app-insights-resources-roles-access-control.md).</span></span>
* <span data-ttu-id="b4450-151">Вы сохранили ссылку, используя другие учетные данные?</span><span class="sxs-lookup"><span data-stu-id="b4450-151">Did you save the link using different credentials?</span></span> <span data-ttu-id="b4450-152">Откройте [портал Azure](https://portal.azure.com), выполните выход, а затем повторно щелкните эту ссылку и введите правильные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="b4450-152">Open the [Azure portal](https://portal.azure.com), sign out, and then try this link again, providing the correct credentials.</span></span>

## <span data-ttu-id="b4450-153"><a name="html-storage"></a>403 ... Хранилище HTML5</span><span class="sxs-lookup"><span data-stu-id="b4450-153"><a name="html-storage"></a>403 ... HTML5 Storage</span></span>
<span data-ttu-id="b4450-154">На нашем портале используются хранилища HTML5 — localStorage и sessionStorage.</span><span class="sxs-lookup"><span data-stu-id="b4450-154">Our portal uses HTML5 localStorage and sessionStorage.</span></span>

* <span data-ttu-id="b4450-155">Chrome: Settings (Параметры), Privacy (Конфиденциальность), Content settings (Параметры содержимого).</span><span class="sxs-lookup"><span data-stu-id="b4450-155">Chrome: Settings, privacy, content settings.</span></span>
* <span data-ttu-id="b4450-156">Internet Explorer: "Свойства браузера", вкладка "Дополнительно", "Безопасность", "Включить хранилище DOM".</span><span class="sxs-lookup"><span data-stu-id="b4450-156">Internet Explorer: Internet Options, Advanced tab, Security, Enable DOM Storage</span></span>

![403... Попробуйте включить хранилище HTML5](./media/app-insights-analytics-troubleshooting/060.png)

## <span data-ttu-id="b4450-158"><a name="e-g"></a>404 ... Подписка не найдена</span><span class="sxs-lookup"><span data-stu-id="b4450-158"><a name="e-g"></a>404 ... Subscription not found</span></span>
![404... Подписка не найдена](./media/app-insights-analytics-troubleshooting/070.png)

<span data-ttu-id="b4450-160">Недопустимый URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="b4450-160">The URL is invalid.</span></span> 

* <span data-ttu-id="b4450-161">Откройте ресурс приложения на [портале Application Insights](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b4450-161">Open the app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="b4450-162">Затем используйте кнопку аналитики.</span><span class="sxs-lookup"><span data-stu-id="b4450-162">Then use the Analytics button.</span></span>

## <span data-ttu-id="b4450-163"><a name="e-h"></a>404… страница не существует</span><span class="sxs-lookup"><span data-stu-id="b4450-163"><a name="e-h"></a>404 ... page doesn't exist</span></span>
![404... Страница не существует](./media/app-insights-analytics-troubleshooting/080.png)

<span data-ttu-id="b4450-165">Недопустимый URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="b4450-165">The URL is invalid.</span></span>

* <span data-ttu-id="b4450-166">Откройте ресурс приложения на [портале Application Insights](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b4450-166">Open the app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="b4450-167">Затем используйте кнопку аналитики.</span><span class="sxs-lookup"><span data-stu-id="b4450-167">Then use the Analytics button.</span></span>

## <span data-ttu-id="b4450-168"><a name="cookies"></a>Включение сторонних файлов cookie</span><span class="sxs-lookup"><span data-stu-id="b4450-168"><a name="cookies"></a>Enable third-party cookies</span></span>
  <span data-ttu-id="b4450-169">Узнайте, [как отключить сторонние файлы cookie](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), но обратите внимание, что их необходимо **включить** .</span><span class="sxs-lookup"><span data-stu-id="b4450-169">See [how to disable third party cookies](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), but notice we need to **enable** them.</span></span>


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

