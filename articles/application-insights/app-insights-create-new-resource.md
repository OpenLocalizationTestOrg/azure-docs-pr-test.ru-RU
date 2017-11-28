---
title: "Создание ресурса Azure Application Insights | Документация Майкрософт"
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
ms.openlocfilehash: 5f8814ee943424c1c278ab3732129d4459f83819
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-insights-resource"></a><span data-ttu-id="b72eb-103">Создание ресурса Application Insights</span><span class="sxs-lookup"><span data-stu-id="b72eb-103">Create an Application Insights resource</span></span>
<span data-ttu-id="b72eb-104">В Azure Application Insights данные о приложении отображаются в *ресурсе* Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b72eb-104">Azure Application Insights displays data about your application in a Microsoft Azure *resource*.</span></span> <span data-ttu-id="b72eb-105">Таким образом, создание ресурса является частью [настройки Application Insights для мониторинга нового приложения][start].</span><span class="sxs-lookup"><span data-stu-id="b72eb-105">Creating a new resource is therefore part of [setting up Application Insights to monitor a new application][start].</span></span> <span data-ttu-id="b72eb-106">Во многих случаях создать ресурс можно автоматически с помощью IDE.</span><span class="sxs-lookup"><span data-stu-id="b72eb-106">In many cases, creating a resource can be done automatically by the IDE.</span></span> <span data-ttu-id="b72eb-107">Однако в некоторых случаях создавать ресурс необходимо вручную. Например, чтобы иметь отдельные ресурсы для сборок разработки и производственных сборок приложения.</span><span class="sxs-lookup"><span data-stu-id="b72eb-107">But in some cases, you create a resource manually - for example, to have separate resources for development and production builds of your application.</span></span>

<span data-ttu-id="b72eb-108">После создания ресурса можно получить его ключ инструментирования и использовать этот ключ для настройки пакета SDK в приложении.</span><span class="sxs-lookup"><span data-stu-id="b72eb-108">After you have created the resource, you get its instrumentation key and use that to configure the SDK in the application.</span></span> <span data-ttu-id="b72eb-109">Ключ ресурса позволяет связать данные телеметрии с ресурсом.</span><span class="sxs-lookup"><span data-stu-id="b72eb-109">The resource key links the telemetry to the resource.</span></span>

## <a name="sign-up-to-microsoft-azure"></a><span data-ttu-id="b72eb-110">Регистрация в Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b72eb-110">Sign up to Microsoft Azure</span></span>
<span data-ttu-id="b72eb-111">Если у вас еще нет [учетной записи Майкрософт, получите ее сейчас](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="b72eb-111">If you haven't got a [Microsoft account, get one now](http://live.com).</span></span> <span data-ttu-id="b72eb-112">(Если вы используете такие службы, как Outlook.com, OneDrive, Windows Phone или XBox Live, значит, у вас уже есть учетная запись Майкрософт.)</span><span class="sxs-lookup"><span data-stu-id="b72eb-112">(If you use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, you already have a Microsoft account.)</span></span>

<span data-ttu-id="b72eb-113">Вам также потребуется подписка [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="b72eb-113">You also need a subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="b72eb-114">Если у вашей группы или организации есть подписка Azure, владелец может добавить вас в нее с помощью вашей учетной записи Windows Live ID.</span><span class="sxs-lookup"><span data-stu-id="b72eb-114">If your team or organization has an Azure subscription, the owner can add you to it, using your Windows Live ID.</span></span> <span data-ttu-id="b72eb-115">Плата взимается только за используемый объем,</span><span class="sxs-lookup"><span data-stu-id="b72eb-115">You're only charged for what you use.</span></span> <span data-ttu-id="b72eb-116">а базовый план по умолчанию предусматривает бесплатное использование определенного объема в экспериментальных целях.</span><span class="sxs-lookup"><span data-stu-id="b72eb-116">The default basic plan allows for a certain amount of experimental use free of charge.</span></span>

<span data-ttu-id="b72eb-117">Если у вас есть доступ к подписке, войдите в Application Insights по адресу [http://portal.azure.com](https://portal.azure.com)и используйте свой Live ID для входа.</span><span class="sxs-lookup"><span data-stu-id="b72eb-117">When you've got access to a subscription, log in to Application Insights at [http://portal.azure.com](https://portal.azure.com), and use your Live ID to login.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="b72eb-118">Создание ресурса Application Insights</span><span class="sxs-lookup"><span data-stu-id="b72eb-118">Create an Application Insights resource</span></span>
<span data-ttu-id="b72eb-119">Перейдите по адресу [portal.azure.com](https://portal.azure.com)и добавьте новый ресурс Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b72eb-119">In the [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Нажмите "Создать" и "Application Insights"](./media/app-insights-create-new-resource/01-new.png)

* <span data-ttu-id="b72eb-121">**Тип приложения** определяет содержимое колонки "Обзор" и свойства, доступные в [обозревателе метрик][metrics].</span><span class="sxs-lookup"><span data-stu-id="b72eb-121">**Application type** affects what you see on the overview blade and the properties available in [metric explorer][metrics].</span></span> <span data-ttu-id="b72eb-122">Если тип приложения не отображается, выберите пункт "Общие".</span><span class="sxs-lookup"><span data-stu-id="b72eb-122">If you don't see your type of app, choose General.</span></span>
* <span data-ttu-id="b72eb-123">**Подписка** представляет собой учетную запись для оплаты в Azure.</span><span class="sxs-lookup"><span data-stu-id="b72eb-123">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="b72eb-124">**Группа ресурсов** – удобный способ для управления свойствами наподобие контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="b72eb-124">**Resource group** is a convenience for managing properties like access control.</span></span> <span data-ttu-id="b72eb-125">Если вы уже создали другие ресурсы Azure, можно поместить новый ресурс в ту же группу.</span><span class="sxs-lookup"><span data-stu-id="b72eb-125">If you have already created other Azure resources, you can choose to put this new resource in the same group.</span></span>
* <span data-ttu-id="b72eb-126">**Расположение** – это место, в котором мы храним ваши данные.</span><span class="sxs-lookup"><span data-stu-id="b72eb-126">**Location** is where we keep your data.</span></span>
* <span data-ttu-id="b72eb-127">Установив флажок **Закрепить на панели мониторинга**, вы сможете поместить плитку для быстрого доступа к ресурсу на главную страницу Azure.</span><span class="sxs-lookup"><span data-stu-id="b72eb-127">**Pin to dashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> <span data-ttu-id="b72eb-128">(рекомендуется).</span><span class="sxs-lookup"><span data-stu-id="b72eb-128">Recommended.</span></span>

<span data-ttu-id="b72eb-129">После создания приложения откроется новая колонка.</span><span class="sxs-lookup"><span data-stu-id="b72eb-129">When your app has been created, a new blade opens.</span></span> <span data-ttu-id="b72eb-130">В этой колонке будут представлены данные о производительности и использовании приложения.</span><span class="sxs-lookup"><span data-stu-id="b72eb-130">This blade is where you see performance and usage data about your app.</span></span> 

<span data-ttu-id="b72eb-131">Чтобы перейти сюда после следующего входа в Azure,используйте плитку быстрого доступа на начальной доске (на начальном экране).</span><span class="sxs-lookup"><span data-stu-id="b72eb-131">To get back to it next time you log in to Azure, look for your app's quick-start tile on the start board (home screen).</span></span> <span data-ttu-id="b72eb-132">Ее также можно открыть, щелкнув «Обзор».</span><span class="sxs-lookup"><span data-stu-id="b72eb-132">Or click Browse to find it.</span></span>

## <a name="copy-the-instrumentation-key"></a><span data-ttu-id="b72eb-133">Копирование ключа инструментирования</span><span class="sxs-lookup"><span data-stu-id="b72eb-133">Copy the instrumentation key</span></span>
<span data-ttu-id="b72eb-134">Ключ инструментирования идентифицирует созданный вами ресурс.</span><span class="sxs-lookup"><span data-stu-id="b72eb-134">The instrumentation key identifies the resource that you created.</span></span> <span data-ttu-id="b72eb-135">Он должен указываться в SDK.</span><span class="sxs-lookup"><span data-stu-id="b72eb-135">You need it to give to the SDK.</span></span>

![Щелкните Essentials, выделите ключ инструментирования и нажмите клавиши CTRL + C.](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-the-sdk-in-your-app"></a><span data-ttu-id="b72eb-137">Установка пакета SDK в приложении</span><span class="sxs-lookup"><span data-stu-id="b72eb-137">Install the SDK in your app</span></span>
<span data-ttu-id="b72eb-138">Установите пакет SDK Application Insights в приложении.</span><span class="sxs-lookup"><span data-stu-id="b72eb-138">Install the Application Insights SDK in your app.</span></span> <span data-ttu-id="b72eb-139">Выполнение этого шага зависит от типа приложения.</span><span class="sxs-lookup"><span data-stu-id="b72eb-139">This step depends heavily on the type of your application.</span></span> 

<span data-ttu-id="b72eb-140">Используйте ключ инструментирования для настройки [пакета SDK, который можно установить в приложении][start].</span><span class="sxs-lookup"><span data-stu-id="b72eb-140">Use the instrumentation key to configure [the SDK that you install in your application][start].</span></span>

<span data-ttu-id="b72eb-141">Пакет SDK включает стандартные модули, которые отправляют данные телеметрии, не требуя написания кода.</span><span class="sxs-lookup"><span data-stu-id="b72eb-141">The SDK includes standard modules that send telemetry without you having to write any code.</span></span> <span data-ttu-id="b72eb-142">Для более подробного отслеживания действий пользователей или диагностики неполадок отправляйте собственные данные телеметрии, [используя API][api].</span><span class="sxs-lookup"><span data-stu-id="b72eb-142">To track user actions or diagnose issues in more detail, [use the API][api] to send your own telemetry.</span></span>

## <span data-ttu-id="b72eb-143"><a name="monitor"></a>Просмотр данных телеметрии</span><span class="sxs-lookup"><span data-stu-id="b72eb-143"><a name="monitor"></a>See telemetry data</span></span>
<span data-ttu-id="b72eb-144">Закройте колонку быстрого доступа, чтобы вернуться к колонке приложения на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="b72eb-144">Close the quick start blade to return to your application blade in the Azure portal.</span></span>

<span data-ttu-id="b72eb-145">Щелкните элемент "Поиск", чтобы открыть [Diagnostic Search][diagnostic] (Поиск по журналу диагностики), где отображаются первые события.</span><span class="sxs-lookup"><span data-stu-id="b72eb-145">Click the Search tile to see [Diagnostic Search][diagnostic], where the first events appear.</span></span> 

<span data-ttu-id="b72eb-146">Нажмите кнопку **Обновить** через несколько секунд, если ожидаете дополнительные данные.</span><span class="sxs-lookup"><span data-stu-id="b72eb-146">If you're expecting more data, click **Refresh** after a few seconds  .</span></span>

## <a name="creating-a-resource-automatically"></a><span data-ttu-id="b72eb-147">Автоматическое создание ресурса</span><span class="sxs-lookup"><span data-stu-id="b72eb-147">Creating a resource automatically</span></span>
<span data-ttu-id="b72eb-148">Вы можете написать [Сценарий PowerShell](app-insights-powershell.md) для автоматического создания ресурса.</span><span class="sxs-lookup"><span data-stu-id="b72eb-148">You can write a [PowerShell script](app-insights-powershell.md) to create a resource automatically.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b72eb-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b72eb-149">Next steps</span></span>
* [<span data-ttu-id="b72eb-150">Создание панели мониторинга</span><span class="sxs-lookup"><span data-stu-id="b72eb-150">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="b72eb-151">Поиск по журналу диагностики</span><span class="sxs-lookup"><span data-stu-id="b72eb-151">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="b72eb-152">Изучение метрик</span><span class="sxs-lookup"><span data-stu-id="b72eb-152">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="b72eb-153">Написание запросов аналитики</span><span class="sxs-lookup"><span data-stu-id="b72eb-153">Write Analytics queries</span></span>](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

