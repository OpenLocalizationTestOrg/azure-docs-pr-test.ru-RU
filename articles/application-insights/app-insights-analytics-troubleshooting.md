---
title: "aaaTroubleshoot аналитика в Azure Application Insights | Документы Microsoft"
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
ms.openlocfilehash: e3be2fbc0237440d3b8a736484434a9f276296c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-analytics-in-application-insights"></a><span data-ttu-id="8ac4b-104">Устранение неполадок аналитики в Application Insights</span><span class="sxs-lookup"><span data-stu-id="8ac4b-104">Troubleshoot Analytics in Application Insights</span></span>
<span data-ttu-id="8ac4b-105">Возникли проблемы с [аналитикой Application Insights](app-insights-analytics.md)?</span><span class="sxs-lookup"><span data-stu-id="8ac4b-105">Problems with [Application Insights Analytics](app-insights-analytics.md)?</span></span> <span data-ttu-id="8ac4b-106">Начните отсюда.</span><span class="sxs-lookup"><span data-stu-id="8ac4b-106">Start here.</span></span> <span data-ttu-id="8ac4b-107">Аналитика является средством мощное средство поиска hello Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8ac4b-107">Analytics is hello powerful search tool of Azure Application Insights.</span></span>

## <a name="limits"></a><span data-ttu-id="8ac4b-108">Ограничения</span><span class="sxs-lookup"><span data-stu-id="8ac4b-108">Limits</span></span>
* <span data-ttu-id="8ac4b-109">В настоящее результаты запроса — ограниченный toojust за неделя за прошлые периоды.</span><span class="sxs-lookup"><span data-stu-id="8ac4b-109">At present, query results are limited toojust over a week of past data.</span></span>
* <span data-ttu-id="8ac4b-110">Тестируемые браузеры: последние выпуски Chrome, Edge и Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="8ac4b-110">Browsers we test on: latest editions of Chrome, Edge, and Internet Explorer.</span></span>

## <a name="known-incompatible-browser-extensions"></a><span data-ttu-id="8ac4b-111">Известные несовместимые расширения браузеров</span><span class="sxs-lookup"><span data-stu-id="8ac4b-111">Known incompatible browser extensions</span></span>
* <span data-ttu-id="8ac4b-112">Ghostery</span><span class="sxs-lookup"><span data-stu-id="8ac4b-112">Ghostery</span></span>

<span data-ttu-id="8ac4b-113">Отключить расширение hello, или используйте другой браузер.</span><span class="sxs-lookup"><span data-stu-id="8ac4b-113">Disable hello extension or use a different browser.</span></span>

## <span data-ttu-id="8ac4b-114"><a name="e-a"></a> "Непредвиденная ошибка"</span><span class="sxs-lookup"><span data-stu-id="8ac4b-114"><a name="e-a"></a> "Unexpected error"</span></span>
![Экран непредвиденной ошибки](./media/app-insights-analytics-troubleshooting/010.png)

<span data-ttu-id="8ac4b-116">Произошла внутренняя ошибка во время выполнения портала — необработанное исключение.</span><span class="sxs-lookup"><span data-stu-id="8ac4b-116">Internal error occurred during portal runtime – unhandled exception.</span></span>

* <span data-ttu-id="8ac4b-117">Очистите кэш браузера hello.</span><span class="sxs-lookup"><span data-stu-id="8ac4b-117">Clean hello browser's cache.</span></span> 

## <span data-ttu-id="8ac4b-118"><a name="e-b"></a>403... Повторите tooreload</span><span class="sxs-lookup"><span data-stu-id="8ac4b-118"><a name="e-b"></a>403 ... please try tooreload</span></span>
![403... Повторите tooreload](./media/app-insights-analytics-troubleshooting/020.png)

<span data-ttu-id="8ac4b-120">Произошла ошибка, связанная с проверкой подлинности (во время проверки подлинности или во время создания маркера доступа).</span><span class="sxs-lookup"><span data-stu-id="8ac4b-120">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="8ac4b-121">Hello портала может не имеют возможности слишком восстановить без изменения параметров браузера.</span><span class="sxs-lookup"><span data-stu-id="8ac4b-121">hello portal may have no way too recover without changing browser settings.</span></span>

* <span data-ttu-id="8ac4b-122">Проверьте [сторонние файлы Cookie включены](#cookies) в браузере hello.</span><span class="sxs-lookup"><span data-stu-id="8ac4b-122">Verify [third party cookies are enabled](#cookies) in hello browser.</span></span> 

## <span data-ttu-id="8ac4b-123"><a name="authentication"></a>403… проверьте зону безопасности</span><span class="sxs-lookup"><span data-stu-id="8ac4b-123"><a name="authentication"></a>403 ... verify security zone</span></span>
![403... Проверьте зону безопасности](./media/app-insights-analytics-troubleshooting/030.png)

<span data-ttu-id="8ac4b-125">Произошла ошибка, связанная с проверкой подлинности (во время проверки подлинности или во время создания маркера доступа).</span><span class="sxs-lookup"><span data-stu-id="8ac4b-125">An authentication related error occurred (during authentication or during access token generation).</span></span> <span data-ttu-id="8ac4b-126">Hello портала может не имеют возможности слишком восстановить без изменения параметров браузера.</span><span class="sxs-lookup"><span data-stu-id="8ac4b-126">hello portal may have no way too recover without changing browser settings.</span></span>

1. <span data-ttu-id="8ac4b-127">Проверьте [сторонние файлы Cookie включены](#cookies) в браузере hello.</span><span class="sxs-lookup"><span data-stu-id="8ac4b-127">Verify [third party cookies are enabled](#cookies) in hello browser.</span></span> 
2. <span data-ttu-id="8ac4b-128">Вы использовали избранного, закладки или сохраненная ссылка tooopen hello Analytics портала?</span><span class="sxs-lookup"><span data-stu-id="8ac4b-128">Did you use a favorite, bookmark or saved link tooopen hello Analytics portal?</span></span> <span data-ttu-id="8ac4b-129">Вы вошли в другие учетные данные, которые использовались при сохранении hello ссылку?</span><span class="sxs-lookup"><span data-stu-id="8ac4b-129">Are you signed in with different credentials than you used when you saved hello link?</span></span>
3. <span data-ttu-id="8ac4b-130">Используйте окно браузера в закрытом или анонимном режиме (после закрытия всех окон).</span><span class="sxs-lookup"><span data-stu-id="8ac4b-130">Try using an in-private/incognito browser window (after closing all such windows).</span></span> <span data-ttu-id="8ac4b-131">У вас будет tooprovide учетные данные.</span><span class="sxs-lookup"><span data-stu-id="8ac4b-131">You'll have tooprovide your credentials.</span></span> 
4. <span data-ttu-id="8ac4b-132">Открытие другого окна браузера (обычный) и перейдите в слишком[Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8ac4b-132">Open another (ordinary) browser window and go too[Azure](https://portal.azure.com).</span></span> <span data-ttu-id="8ac4b-133">Выполните выход. Затем откройте ссылка на приложение и войти с помощью hello правильные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="8ac4b-133">Sign out. Then open your link and sign in with hello correct credentials.</span></span>
5. <span data-ttu-id="8ac4b-134">У пользователей браузеров Edge и Internet Explorer также может возникать эта ошибка, если параметры доверенной зоны не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="8ac4b-134">Edge and Internet Explorer users can also get this error when trusted zone settings are not supported.</span></span>
   
    <span data-ttu-id="8ac4b-135">Проверьте оба [портала службы анализа](https://analytics.applicationinsights.io) и [портал Azure Active Directory](https://portal.azure.com) в hello же зоны безопасности:</span><span class="sxs-lookup"><span data-stu-id="8ac4b-135">Verify both [Analytics portal](https://analytics.applicationinsights.io) and [Azure Active Directory portal](https://portal.azure.com) are in hello same security zone:</span></span>
   
   * <span data-ttu-id="8ac4b-136">В Internet Explorer щелкните **Свойства браузера**, **Безопасность**, **Надежные сайты**, **Узлы**.</span><span class="sxs-lookup"><span data-stu-id="8ac4b-136">In Internet Explorer, open **Internet Options**, **Security**, **Trusted sites**, **Sites**:</span></span>
     
     ![Диалоговое окно свойств обозревателя, добавление узла tooTrusted сайтов](./media/app-insights-analytics-troubleshooting/033.png)
     
     <span data-ttu-id="8ac4b-138">В списке веб-сайтов hello, если hello следующие URL-адреса включены, убедитесь, что hello другие включены также:</span><span class="sxs-lookup"><span data-stu-id="8ac4b-138">In hello Websites list, if any of hello following URLs are included, make sure that hello others are included also:</span></span>
     
     <span data-ttu-id="8ac4b-139">https://analytics.applicationinsights.io</span><span class="sxs-lookup"><span data-stu-id="8ac4b-139">https://analytics.applicationinsights.io</span></span><br/>
     <span data-ttu-id="8ac4b-140">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="8ac4b-140">https://login.microsoftonline.com</span></span><br/>
     <span data-ttu-id="8ac4b-141">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="8ac4b-141">https://login.windows.net</span></span>

## <span data-ttu-id="8ac4b-142"><a name="e-d"></a>404... Ресурс не найден</span><span class="sxs-lookup"><span data-stu-id="8ac4b-142"><a name="e-d"></a>404 ... Resource not found</span></span>
![404... Ресурс не найден](./media/app-insights-analytics-troubleshooting/040.png)

<span data-ttu-id="8ac4b-144">Ресурс приложения был удален из Application Insights и больше не доступен.</span><span class="sxs-lookup"><span data-stu-id="8ac4b-144">Application resource was deleted from Application Insights and isn’t available anymore.</span></span> <span data-ttu-id="8ac4b-145">Это может произойти, если вы сохранили toohello Analytics hello URL-адрес страницы.</span><span class="sxs-lookup"><span data-stu-id="8ac4b-145">This can happen if you saved hello URL toohello Analytics page.</span></span>

## <span data-ttu-id="8ac4b-146"><a name="e-e"></a>403 ... Нет авторизации</span><span class="sxs-lookup"><span data-stu-id="8ac4b-146"><a name="e-e"></a>403 ... No authorization</span></span>
![403... Нет авторизации](./media/app-insights-analytics-troubleshooting/050.png)

<span data-ttu-id="8ac4b-148">Не нужно разрешение tooopen этого приложения в аналитике.</span><span class="sxs-lookup"><span data-stu-id="8ac4b-148">You don't have permission tooopen this application in Analytics.</span></span>

* <span data-ttu-id="8ac4b-149">Был ли получен hello ссылку от кого-нибудь?</span><span class="sxs-lookup"><span data-stu-id="8ac4b-149">Did you get hello link from someone else?</span></span> <span data-ttu-id="8ac4b-150">Попросите их убедиться, что вы находитесь в hello toomake [модулей чтения или участники, эта группа ресурсов](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="8ac4b-150">Ask them toomake sure you are in hello [readers or contributors for this resource group](app-insights-resources-roles-access-control.md).</span></span>
* <span data-ttu-id="8ac4b-151">Сохраненных hello ссылку, используя другие учетные данные?</span><span class="sxs-lookup"><span data-stu-id="8ac4b-151">Did you save hello link using different credentials?</span></span> <span data-ttu-id="8ac4b-152">Откройте hello [портал Azure](https://portal.azure.com), выйдите из системы, а затем повторите эту ссылку еще раз, указав правильные учетные данные hello.</span><span class="sxs-lookup"><span data-stu-id="8ac4b-152">Open hello [Azure portal](https://portal.azure.com), sign out, and then try this link again, providing hello correct credentials.</span></span>

## <span data-ttu-id="8ac4b-153"><a name="html-storage"></a>403 ... Хранилище HTML5</span><span class="sxs-lookup"><span data-stu-id="8ac4b-153"><a name="html-storage"></a>403 ... HTML5 Storage</span></span>
<span data-ttu-id="8ac4b-154">На нашем портале используются хранилища HTML5 — localStorage и sessionStorage.</span><span class="sxs-lookup"><span data-stu-id="8ac4b-154">Our portal uses HTML5 localStorage and sessionStorage.</span></span>

* <span data-ttu-id="8ac4b-155">Chrome: Settings (Параметры), Privacy (Конфиденциальность), Content settings (Параметры содержимого).</span><span class="sxs-lookup"><span data-stu-id="8ac4b-155">Chrome: Settings, privacy, content settings.</span></span>
* <span data-ttu-id="8ac4b-156">Internet Explorer: "Свойства браузера", вкладка "Дополнительно", "Безопасность", "Включить хранилище DOM".</span><span class="sxs-lookup"><span data-stu-id="8ac4b-156">Internet Explorer: Internet Options, Advanced tab, Security, Enable DOM Storage</span></span>

![403... Повторите tooenable HTML5 хранилища](./media/app-insights-analytics-troubleshooting/060.png)

## <span data-ttu-id="8ac4b-158"><a name="e-g"></a>404 ... Подписка не найдена</span><span class="sxs-lookup"><span data-stu-id="8ac4b-158"><a name="e-g"></a>404 ... Subscription not found</span></span>
![404... Подписка не найдена](./media/app-insights-analytics-troubleshooting/070.png)

<span data-ttu-id="8ac4b-160">Недопустимый URL-адрес Hello.</span><span class="sxs-lookup"><span data-stu-id="8ac4b-160">hello URL is invalid.</span></span> 

* <span data-ttu-id="8ac4b-161">Открытие ресурса приложения hello в [портале Application Insights](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8ac4b-161">Open hello app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="8ac4b-162">Затем используйте кнопку Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="8ac4b-162">Then use hello Analytics button.</span></span>

## <span data-ttu-id="8ac4b-163"><a name="e-h"></a>404… страница не существует</span><span class="sxs-lookup"><span data-stu-id="8ac4b-163"><a name="e-h"></a>404 ... page doesn't exist</span></span>
![404... Страница не существует](./media/app-insights-analytics-troubleshooting/080.png)

<span data-ttu-id="8ac4b-165">Недопустимый URL-адрес Hello.</span><span class="sxs-lookup"><span data-stu-id="8ac4b-165">hello URL is invalid.</span></span>

* <span data-ttu-id="8ac4b-166">Открытие ресурса приложения hello в [портале Application Insights](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8ac4b-166">Open hello app resource in [Application Insights portal](https://portal.azure.com).</span></span> <span data-ttu-id="8ac4b-167">Затем используйте кнопку Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="8ac4b-167">Then use hello Analytics button.</span></span>

## <span data-ttu-id="8ac4b-168"><a name="cookies"></a>Включение сторонних файлов cookie</span><span class="sxs-lookup"><span data-stu-id="8ac4b-168"><a name="cookies"></a>Enable third-party cookies</span></span>
  <span data-ttu-id="8ac4b-169">В разделе [как сторонний файлы cookie toodisable](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), но Обратите внимание на то, мы должны слишком**включить** их.</span><span class="sxs-lookup"><span data-stu-id="8ac4b-169">See [how toodisable third party cookies](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), but notice we need too**enable** them.</span></span>


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

