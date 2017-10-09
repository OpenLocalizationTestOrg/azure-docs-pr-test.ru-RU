---
title: "aaaCreate новый ресурс Azure Application Insights | Документы Microsoft"
description: "Вручную настройте мониторинг Application Insights для нового работающего приложения."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 878b007e-161c-4e36-8ab2-3d7047d8a92d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: bwren
ms.openlocfilehash: 3aba7045e1f8fe43d473f0be01dd52106ab992a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-insights-resource"></a><span data-ttu-id="f0027-103">Создание ресурса Application Insights</span><span class="sxs-lookup"><span data-stu-id="f0027-103">Create an Application Insights resource</span></span>
<span data-ttu-id="f0027-104">В Azure Application Insights данные о приложении отображаются в *ресурсе* Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f0027-104">Azure Application Insights displays data about your application in a Microsoft Azure *resource*.</span></span> <span data-ttu-id="f0027-105">Создание нового ресурса таким образом является частью [Настройка нового приложения Application Insights toomonitor][start].</span><span class="sxs-lookup"><span data-stu-id="f0027-105">Creating a new resource is therefore part of [setting up Application Insights toomonitor a new application][start].</span></span> <span data-ttu-id="f0027-106">Во многих случаях Создание ресурса может выполняться автоматически hello интегрированной среды разработки.</span><span class="sxs-lookup"><span data-stu-id="f0027-106">In many cases, creating a resource can be done automatically by hello IDE.</span></span> <span data-ttu-id="f0027-107">Но в некоторых случаях вы вручную создайте ресурс — например, toohave отдельные ресурсы для разработки и эксплуатации построений приложения.</span><span class="sxs-lookup"><span data-stu-id="f0027-107">But in some cases, you create a resource manually - for example, toohave separate resources for development and production builds of your application.</span></span>

<span data-ttu-id="f0027-108">После создания ресурса hello получить свой ключ инструментирования, а затем использовать этот tooconfigure hello SDK, в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="f0027-108">After you have created hello resource, you get its instrumentation key and use that tooconfigure hello SDK in hello application.</span></span> <span data-ttu-id="f0027-109">ссылки на ресурсы Hello ключа hello телеметрии toohello ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f0027-109">hello resource key links hello telemetry toohello resource.</span></span>

## <a name="sign-up-toomicrosoft-azure"></a><span data-ttu-id="f0027-110">Регистрация tooMicrosoft Azure</span><span class="sxs-lookup"><span data-stu-id="f0027-110">Sign up tooMicrosoft Azure</span></span>
<span data-ttu-id="f0027-111">Если у вас еще нет [учетной записи Майкрософт, получите ее сейчас](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="f0027-111">If you haven't got a [Microsoft account, get one now](http://live.com).</span></span> <span data-ttu-id="f0027-112">(Если вы используете такие службы, как Outlook.com, OneDrive, Windows Phone или XBox Live, значит, у вас уже есть учетная запись Майкрософт.)</span><span class="sxs-lookup"><span data-stu-id="f0027-112">(If you use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, you already have a Microsoft account.)</span></span>

<span data-ttu-id="f0027-113">Вам также потребуется подписка слишком[Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="f0027-113">You also need a subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="f0027-114">Если команде или организации имеет подписку Azure, владелец hello можно добавить вас tooit, с помощью идентификатора Windows Live ID.</span><span class="sxs-lookup"><span data-stu-id="f0027-114">If your team or organization has an Azure subscription, hello owner can add you tooit, using your Windows Live ID.</span></span> <span data-ttu-id="f0027-115">Плата взимается только за используемый объем,</span><span class="sxs-lookup"><span data-stu-id="f0027-115">You're only charged for what you use.</span></span> <span data-ttu-id="f0027-116">Базовый план по умолчанию Hello позволяет определенное количество экспериментальных целей бесплатно.</span><span class="sxs-lookup"><span data-stu-id="f0027-116">hello default basic plan allows for a certain amount of experimental use free of charge.</span></span>

<span data-ttu-id="f0027-117">Если у вас есть подписка tooa доступ, войдите в tooApplication аналитики в [http://portal.azure.com](https://portal.azure.com)и использовать ваш идентификатор Live ID toologin.</span><span class="sxs-lookup"><span data-stu-id="f0027-117">When you've got access tooa subscription, log in tooApplication Insights at [http://portal.azure.com](https://portal.azure.com), and use your Live ID toologin.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="f0027-118">Создание ресурса Application Insights</span><span class="sxs-lookup"><span data-stu-id="f0027-118">Create an Application Insights resource</span></span>
<span data-ttu-id="f0027-119">В hello [portal.azure.com](https://portal.azure.com), добавьте ресурс Application Insights:</span><span class="sxs-lookup"><span data-stu-id="f0027-119">In hello [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Нажмите "Создать" и "Application Insights"](./media/app-insights-create-new-resource/01-new.png)

* <span data-ttu-id="f0027-121">**Тип приложения** влияет на содержимое, отображаемое на колонки Обзор hello и hello свойств, доступных в [метрики обозреватель][metrics].</span><span class="sxs-lookup"><span data-stu-id="f0027-121">**Application type** affects what you see on hello overview blade and hello properties available in [metric explorer][metrics].</span></span> <span data-ttu-id="f0027-122">Если тип приложения не отображается, выберите пункт "Общие".</span><span class="sxs-lookup"><span data-stu-id="f0027-122">If you don't see your type of app, choose General.</span></span>
* <span data-ttu-id="f0027-123">**Подписка** представляет собой учетную запись для оплаты в Azure.</span><span class="sxs-lookup"><span data-stu-id="f0027-123">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="f0027-124">**Группа ресурсов** – удобный способ для управления свойствами наподобие контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="f0027-124">**Resource group** is a convenience for managing properties like access control.</span></span> <span data-ttu-id="f0027-125">Если вы уже создали другим ресурсам Azure, вы можете tooput этот новый ресурс в hello одной группе.</span><span class="sxs-lookup"><span data-stu-id="f0027-125">If you have already created other Azure resources, you can choose tooput this new resource in hello same group.</span></span>
* <span data-ttu-id="f0027-126">**Расположение** – это место, в котором мы храним ваши данные.</span><span class="sxs-lookup"><span data-stu-id="f0027-126">**Location** is where we keep your data.</span></span>
* <span data-ttu-id="f0027-127">**ПИН-код toodashboard** помещает плитки быстрого доступа для ресурса на Azure домашней страницы.</span><span class="sxs-lookup"><span data-stu-id="f0027-127">**Pin toodashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> <span data-ttu-id="f0027-128">(рекомендуется).</span><span class="sxs-lookup"><span data-stu-id="f0027-128">Recommended.</span></span>

<span data-ttu-id="f0027-129">После создания приложения откроется новая колонка.</span><span class="sxs-lookup"><span data-stu-id="f0027-129">When your app has been created, a new blade opens.</span></span> <span data-ttu-id="f0027-130">В этой колонке будут представлены данные о производительности и использовании приложения.</span><span class="sxs-lookup"><span data-stu-id="f0027-130">This blade is where you see performance and usage data about your app.</span></span> 

<span data-ttu-id="f0027-131">Назад tooit tooget при очередном входе в tooAzure, найдите плитку: быстрый запуск приложения на hello запустите доски (начальный экран).</span><span class="sxs-lookup"><span data-stu-id="f0027-131">tooget back tooit next time you log in tooAzure, look for your app's quick-start tile on hello start board (home screen).</span></span> <span data-ttu-id="f0027-132">Или нажмите кнопку обзора toofind его.</span><span class="sxs-lookup"><span data-stu-id="f0027-132">Or click Browse toofind it.</span></span>

## <a name="copy-hello-instrumentation-key"></a><span data-ttu-id="f0027-133">Скопируйте ключ инструментирования hello</span><span class="sxs-lookup"><span data-stu-id="f0027-133">Copy hello instrumentation key</span></span>
<span data-ttu-id="f0027-134">ключ инструментирования Hello идентифицирует созданный ресурс hello.</span><span class="sxs-lookup"><span data-stu-id="f0027-134">hello instrumentation key identifies hello resource that you created.</span></span> <span data-ttu-id="f0027-135">Вы должны toogive toohello SDK.</span><span class="sxs-lookup"><span data-stu-id="f0027-135">You need it toogive toohello SDK.</span></span>

![Установите Essentials, щелкните hello ключ инструментирования, CTRL + C](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-hello-sdk-in-your-app"></a><span data-ttu-id="f0027-137">Установка пакета SDK для hello в приложении</span><span class="sxs-lookup"><span data-stu-id="f0027-137">Install hello SDK in your app</span></span>
<span data-ttu-id="f0027-138">Установите пакет SDK Application Insights hello в вашем приложении.</span><span class="sxs-lookup"><span data-stu-id="f0027-138">Install hello Application Insights SDK in your app.</span></span> <span data-ttu-id="f0027-139">Этот шаг сильно зависит от типа приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f0027-139">This step depends heavily on hello type of your application.</span></span> 

<span data-ttu-id="f0027-140">Использовать tooconfigure ключа инструментирования hello [пакета SDK, которую можно установить в приложение hello][start].</span><span class="sxs-lookup"><span data-stu-id="f0027-140">Use hello instrumentation key tooconfigure [hello SDK that you install in your application][start].</span></span>

<span data-ttu-id="f0027-141">Hello SDK включает стандартные модули, отправка данных телеметрии без необходимости toowrite любого кода.</span><span class="sxs-lookup"><span data-stu-id="f0027-141">hello SDK includes standard modules that send telemetry without you having toowrite any code.</span></span> <span data-ttu-id="f0027-142">действия пользователя tootrack или Диагностика проблем более подробно [использовать hello API] [ api] toosend собственные телеметрии.</span><span class="sxs-lookup"><span data-stu-id="f0027-142">tootrack user actions or diagnose issues in more detail, [use hello API][api] toosend your own telemetry.</span></span>

## <span data-ttu-id="f0027-143"><a name="monitor"></a>Просмотр данных телеметрии</span><span class="sxs-lookup"><span data-stu-id="f0027-143"><a name="monitor"></a>See telemetry data</span></span>
<span data-ttu-id="f0027-144">Закрыть hello быстрый запуск колонки tooreturn tooyour приложения колонки в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f0027-144">Close hello quick start blade tooreturn tooyour application blade in hello Azure portal.</span></span>

<span data-ttu-id="f0027-145">Щелкните плитку toosee hello поиска [диагностики поиска][diagnostic], где отображаются первые события hello.</span><span class="sxs-lookup"><span data-stu-id="f0027-145">Click hello Search tile toosee [Diagnostic Search][diagnostic], where hello first events appear.</span></span> 

<span data-ttu-id="f0027-146">Нажмите кнопку **Обновить** через несколько секунд, если ожидаете дополнительные данные.</span><span class="sxs-lookup"><span data-stu-id="f0027-146">If you're expecting more data, click **Refresh** after a few seconds  .</span></span>

## <a name="creating-a-resource-automatically"></a><span data-ttu-id="f0027-147">Автоматическое создание ресурса</span><span class="sxs-lookup"><span data-stu-id="f0027-147">Creating a resource automatically</span></span>
<span data-ttu-id="f0027-148">Можно написать [сценарий PowerShell](app-insights-powershell.md) toocreate ресурс автоматически.</span><span class="sxs-lookup"><span data-stu-id="f0027-148">You can write a [PowerShell script](app-insights-powershell.md) toocreate a resource automatically.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0027-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f0027-149">Next steps</span></span>
* [<span data-ttu-id="f0027-150">Создание панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="f0027-150">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="f0027-151">Поиск по журналу диагностики</span><span class="sxs-lookup"><span data-stu-id="f0027-151">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="f0027-152">Изучение метрик</span><span class="sxs-lookup"><span data-stu-id="f0027-152">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="f0027-153">Написание запросов аналитики</span><span class="sxs-lookup"><span data-stu-id="f0027-153">Write Analytics queries</span></span>](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

