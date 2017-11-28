---
title: "Заметки о выпуске для Application Insights | Документация Майкрософт"
description: "Добавление маркеров развертывания или сборки для диаграмм обозревателя метрик в Application Insights."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 23173e33-d4f2-4528-a730-913a8fd5f02e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: f7eb2f3cba535eb64db5544c498289c9e895987a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a><span data-ttu-id="f1d8e-103">Заметки к диаграммам метрик в Application Insights</span><span class="sxs-lookup"><span data-stu-id="f1d8e-103">Annotations on metric charts in Application Insights</span></span>
<span data-ttu-id="f1d8e-104">Заметки к диаграммам [обозревателя метрик](app-insights-metrics-explorer.md) показывают, где развернута новая сборка, а также отображают другие важные события.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-104">Annotations on [Metrics Explorer](app-insights-metrics-explorer.md) charts show where you deployed a new build, or other significant event.</span></span> <span data-ttu-id="f1d8e-105">С их помощью легко увидеть, повлияли ли ваши изменения на производительность приложения.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-105">They make it easy to see whether your changes had any effect on your application's performance.</span></span> <span data-ttu-id="f1d8e-106">Заметки могут быть созданы автоматически [системой сборки Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span><span class="sxs-lookup"><span data-stu-id="f1d8e-106">They can be automatically created by the [Visual Studio Team Services build system](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span></span> <span data-ttu-id="f1d8e-107">Заметки можно также создавать, чтобы помечать какие-либо события, [используя PowerShell](#create-annotations-from-powershell).</span><span class="sxs-lookup"><span data-stu-id="f1d8e-107">You can also create annotations to flag any event you like by [creating them from PowerShell](#create-annotations-from-powershell).</span></span>

![Пример заметок с видимой корреляцией с временем ответа сервера](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a><span data-ttu-id="f1d8e-109">Заметки о выпуске сборки VSTS</span><span class="sxs-lookup"><span data-stu-id="f1d8e-109">Release annotations with VSTS build</span></span>

<span data-ttu-id="f1d8e-110">Заметки к выпуску являются функцией службы облачной сборки и выпуска Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-110">Release annotations are a feature of the cloud-based build and release service of Visual Studio Team Services.</span></span> 

### <a name="install-the-annotations-extension-one-time"></a><span data-ttu-id="f1d8e-111">Установка расширения заметок (однократно)</span><span class="sxs-lookup"><span data-stu-id="f1d8e-111">Install the Annotations extension (one time)</span></span>
<span data-ttu-id="f1d8e-112">Чтобы получить возможность создания заметок к выпуску, необходимо установить одно из расширений Team Service, доступных в магазине Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-112">To be able to create release annotations, you'll need to install one of the many Team Service extensions available in the Visual Studio Marketplace.</span></span>

1. <span data-ttu-id="f1d8e-113">Войдите в свой проект в [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online).</span><span class="sxs-lookup"><span data-stu-id="f1d8e-113">Sign in to your [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) project.</span></span>
2. <span data-ttu-id="f1d8e-114">В магазине Visual Studio [найдите расширение заметок к выпуску](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations)и добавьте его к своей учетной записи Team Services.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-114">In Visual Studio Marketplace, [get the Release Annotations extension](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations), and add it to your Team Services account.</span></span>

![В верхнем правом углу веб-страницы Team Services откройте "Магазин".](./media/app-insights-annotations/10.png)

<span data-ttu-id="f1d8e-117">Это необходимо сделать только один раз для учетной записи Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-117">You only need to do this once for your Visual Studio Team Services account.</span></span> <span data-ttu-id="f1d8e-118">Теперь можно настроить заметки к выпуску для любого проекта в вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-118">Release annotations can now be configured for any project in your account.</span></span> 

### <a name="configure-release-annotations"></a><span data-ttu-id="f1d8e-119">Настройка заметок к выпуску</span><span class="sxs-lookup"><span data-stu-id="f1d8e-119">Configure release annotations</span></span>

<span data-ttu-id="f1d8e-120">Для каждого шаблона выпуска VSTS необходимо получить отдельный ключ API.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-120">You need to get a separate API key for each VSTS release template.</span></span>

1. <span data-ttu-id="f1d8e-121">Выполните вход на [портал Microsoft Azure](https://portal.azure.com) и откройте ресурс Application Insights, который используется для мониторинга вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-121">Sign in to the [Microsoft Azure Portal](https://portal.azure.com) and open the Application Insights resource that monitors your application.</span></span> <span data-ttu-id="f1d8e-122">(Или [создайте новый](app-insights-overview.md), если вы этого еще не сделали.)</span><span class="sxs-lookup"><span data-stu-id="f1d8e-122">(Or [create one now](app-insights-overview.md), if you haven't done so yet.)</span></span>
2. <span data-ttu-id="f1d8e-123">Откройте **Доступ через API** и выберите **Идентификатор Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-123">Open **API Access**,  **Application Insights Id**.</span></span>
   
    ![На сайте portal.azure.com откройте ресурс Application Insights и выберите "Параметры".](./media/app-insights-annotations/20.png)

4. <span data-ttu-id="f1d8e-127">В отдельном окне браузера откройте (или создайте) шаблон выпуска, который управляет развертываниями из Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-127">In a separate browser window, open (or create) the release template that manages your deployments from Visual Studio Team Services.</span></span> 
   
    <span data-ttu-id="f1d8e-128">Добавьте задачу и выберите в меню задачу заметок к выпуску Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-128">Add a task, and select the Application Insights Release Annotation task from the menu.</span></span>
   
    <span data-ttu-id="f1d8e-129">Вставьте **идентификатор приложения** , скопированный из колонки "Доступ к API".</span><span class="sxs-lookup"><span data-stu-id="f1d8e-129">Paste the **Application Id** that you copied from the API Access blade.</span></span>
   
    ![В Visual Studio Team Services откройте "Выпуск", выберите определение выпуска и нажмите кнопку "Изменить".](./media/app-insights-annotations/30.png)
4. <span data-ttu-id="f1d8e-133">Задайте в качестве значения поля **APIKey** переменную `$(ApiKey)`.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-133">Set the **APIKey** field to a variable `$(ApiKey)`.</span></span>

5. <span data-ttu-id="f1d8e-134">В окне Azure создайте ключ API и скопируйте его.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-134">Back in the Azure window, create a new API Key and take a copy of it.</span></span>
   
    ![В колонке "Доступ к API" в окне Azure щелкните "Создать ключ API".](./media/app-insights-annotations/40.png)

6. <span data-ttu-id="f1d8e-138">Перейдите на вкладку "Конфигурация" шаблона выпуска.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-138">Open the Configuration tab of the release template.</span></span>
   
    <span data-ttu-id="f1d8e-139">Создайте определение переменной для `ApiKey`.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-139">Create a variable definition for `ApiKey`.</span></span>
   
    <span data-ttu-id="f1d8e-140">Вставьте ключ API в определение переменной ApiKey.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-140">Paste your API key to the ApiKey variable definition.</span></span>
   
    ![В окне Team Services перейдите на вкладку "Конфигурация" и щелкните "Добавить переменную".](./media/app-insights-annotations/50.png)
7. <span data-ttu-id="f1d8e-143">Наконец, **сохраните** определение выпуска.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-143">Finally, **Save** the release definition.</span></span>


## <a name="view-annotations"></a><span data-ttu-id="f1d8e-144">Просмотр заметок</span><span class="sxs-lookup"><span data-stu-id="f1d8e-144">View annotations</span></span>
<span data-ttu-id="f1d8e-145">Теперь при каждом развертывании нового выпуска с помощью шаблона выпуска заметки будут отправляться в Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-145">Now, whenever you use the release template to deploy a new release, an annotation will be sent to Application Insights.</span></span> <span data-ttu-id="f1d8e-146">Заметки будут отображаться на диаграммах в обозревателе метрик.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-146">The annotations will appear on charts in Metrics Explorer.</span></span>

<span data-ttu-id="f1d8e-147">Щелкните любой маркер заметки, чтобы открыть подробные сведения о выпуске, включая запросившую сторону, ветвь системы управления версиями, определение выпуска, среду и многое другое.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-147">Click on any annotation marker to open details about the release, including requestor, source control branch, release definition, environment, and more.</span></span>

![Щелкните любой маркер заметки о выпуске.](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a><span data-ttu-id="f1d8e-149">Создание настраиваемых заметок в PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1d8e-149">Create custom annotations from PowerShell</span></span>
<span data-ttu-id="f1d8e-150">Вы можете создать аннотации из любого процесса на свой выбор (без использования Visual Studio Team System).</span><span class="sxs-lookup"><span data-stu-id="f1d8e-150">You can also create annotations from any process you like (without using VS Team System).</span></span> 


1. <span data-ttu-id="f1d8e-151">Создайте локальную копию [сценария PowerShell из GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span><span class="sxs-lookup"><span data-stu-id="f1d8e-151">Make a local copy of the [Powershell script from GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span></span>

2. <span data-ttu-id="f1d8e-152">Получите идентификатор приложения и создайте ключ API в колонке "Доступ через API".</span><span class="sxs-lookup"><span data-stu-id="f1d8e-152">Get the Application ID and create an API key from the API Access blade.</span></span>

3. <span data-ttu-id="f1d8e-153">Вызовите сценарий следующим образом.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-153">Call the script like this:</span></span>

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

<span data-ttu-id="f1d8e-154">Сценарий легко изменить, например, чтобы создать заметки для предыдущих выпусков.</span><span class="sxs-lookup"><span data-stu-id="f1d8e-154">It's easy to modify the script, for example to create annotations for the past.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1d8e-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f1d8e-155">Next steps</span></span>

* [<span data-ttu-id="f1d8e-156">Создание рабочих элементов</span><span class="sxs-lookup"><span data-stu-id="f1d8e-156">Create work items</span></span>](app-insights-diagnostic-search.md#create-work-item)
* [<span data-ttu-id="f1d8e-157">Автоматизация с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1d8e-157">Automation with PowerShell</span></span>](app-insights-powershell.md)
