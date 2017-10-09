---
title: "aaaRelease заметки для Application Insights | Документы Microsoft"
description: "Добавление развертывания или построения маркеры диаграммы обозревателя метрик tooyour в Application Insights."
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
ms.openlocfilehash: e802d22701cb69e96fd1a6b469ea67454195f77a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a><span data-ttu-id="86dd6-103">Заметки к диаграммам метрик в Application Insights</span><span class="sxs-lookup"><span data-stu-id="86dd6-103">Annotations on metric charts in Application Insights</span></span>
<span data-ttu-id="86dd6-104">Заметки к диаграммам [обозревателя метрик](app-insights-metrics-explorer.md) показывают, где развернута новая сборка, а также отображают другие важные события.</span><span class="sxs-lookup"><span data-stu-id="86dd6-104">Annotations on [Metrics Explorer](app-insights-metrics-explorer.md) charts show where you deployed a new build, or other significant event.</span></span> <span data-ttu-id="86dd6-105">Они позволяют легко toosee ли изменения имели никакого воздействия на производительность приложения.</span><span class="sxs-lookup"><span data-stu-id="86dd6-105">They make it easy toosee whether your changes had any effect on your application's performance.</span></span> <span data-ttu-id="86dd6-106">Они могут создаваться автоматически с hello [системы сборки Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span><span class="sxs-lookup"><span data-stu-id="86dd6-106">They can be automatically created by hello [Visual Studio Team Services build system](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span></span> <span data-ttu-id="86dd6-107">Можно также создать заметки tooflag любого события, например по [создание их на основе PowerShell](#create-annotations-from-powershell).</span><span class="sxs-lookup"><span data-stu-id="86dd6-107">You can also create annotations tooflag any event you like by [creating them from PowerShell](#create-annotations-from-powershell).</span></span>

![Пример заметок с видимой корреляцией с временем ответа сервера](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a><span data-ttu-id="86dd6-109">Заметки о выпуске сборки VSTS</span><span class="sxs-lookup"><span data-stu-id="86dd6-109">Release annotations with VSTS build</span></span>

<span data-ttu-id="86dd6-110">Выпуск заметки являются компонентом облачной сборки hello и выпуска службы из Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="86dd6-110">Release annotations are a feature of hello cloud-based build and release service of Visual Studio Team Services.</span></span> 

### <a name="install-hello-annotations-extension-one-time"></a><span data-ttu-id="86dd6-111">Установка расширения заметок hello (один раз)</span><span class="sxs-lookup"><span data-stu-id="86dd6-111">Install hello Annotations extension (one time)</span></span>
<span data-ttu-id="86dd6-112">заметки выпуска может toocreate toobe, вам потребуется tooinstall один из hello многие службы Team расширения, доступные в hello Visual Studio Marketplace.</span><span class="sxs-lookup"><span data-stu-id="86dd6-112">toobe able toocreate release annotations, you'll need tooinstall one of hello many Team Service extensions available in hello Visual Studio Marketplace.</span></span>

1. <span data-ttu-id="86dd6-113">Войдите в tooyour [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) проекта.</span><span class="sxs-lookup"><span data-stu-id="86dd6-113">Sign in tooyour [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) project.</span></span>
2. <span data-ttu-id="86dd6-114">В Visual Studio Marketplace [расширение заметок выпуска hello](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations)и добавить его учетную запись Team Services tooyour.</span><span class="sxs-lookup"><span data-stu-id="86dd6-114">In Visual Studio Marketplace, [get hello Release Annotations extension](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations), and add it tooyour Team Services account.</span></span>

![В верхнем правом углу веб-страницы Team Services откройте "Магазин".](./media/app-insights-annotations/10.png)

<span data-ttu-id="86dd6-117">Требуется только toodo этом один раз для учетной записи Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="86dd6-117">You only need toodo this once for your Visual Studio Team Services account.</span></span> <span data-ttu-id="86dd6-118">Теперь можно настроить заметки к выпуску для любого проекта в вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="86dd6-118">Release annotations can now be configured for any project in your account.</span></span> 

### <a name="configure-release-annotations"></a><span data-ttu-id="86dd6-119">Настройка заметок к выпуску</span><span class="sxs-lookup"><span data-stu-id="86dd6-119">Configure release annotations</span></span>

<span data-ttu-id="86dd6-120">Для каждого шаблона выпуска VSTS необходим ключ tooget отдельный API.</span><span class="sxs-lookup"><span data-stu-id="86dd6-120">You need tooget a separate API key for each VSTS release template.</span></span>

1. <span data-ttu-id="86dd6-121">Войдите в toohello [портал Microsoft Azure](https://portal.azure.com) и открыть ресурс Application Insights hello, осуществляющее мониторинг приложения.</span><span class="sxs-lookup"><span data-stu-id="86dd6-121">Sign in toohello [Microsoft Azure Portal](https://portal.azure.com) and open hello Application Insights resource that monitors your application.</span></span> <span data-ttu-id="86dd6-122">(Или [создайте новый](app-insights-overview.md), если вы этого еще не сделали.)</span><span class="sxs-lookup"><span data-stu-id="86dd6-122">(Or [create one now](app-insights-overview.md), if you haven't done so yet.)</span></span>
2. <span data-ttu-id="86dd6-123">Откройте **Доступ через API** и выберите **Идентификатор Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="86dd6-123">Open **API Access**,  **Application Insights Id**.</span></span>
   
    ![На сайте portal.azure.com откройте ресурс Application Insights и выберите "Параметры".](./media/app-insights-annotations/20.png)

4. <span data-ttu-id="86dd6-127">В отдельном окне браузера откройте (или создайте) hello шаблон выпуска, который управляет развертываний из Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="86dd6-127">In a separate browser window, open (or create) hello release template that manages your deployments from Visual Studio Team Services.</span></span> 
   
    <span data-ttu-id="86dd6-128">Добавьте задачу и выберите задачу заметки выпуска аналитики приложения hello меню "hello".</span><span class="sxs-lookup"><span data-stu-id="86dd6-128">Add a task, and select hello Application Insights Release Annotation task from hello menu.</span></span>
   
    <span data-ttu-id="86dd6-129">Вставить hello **идентификатор приложения** , скопированный из hello колонке доступа к API.</span><span class="sxs-lookup"><span data-stu-id="86dd6-129">Paste hello **Application Id** that you copied from hello API Access blade.</span></span>
   
    ![В Visual Studio Team Services откройте "Выпуск", выберите определение выпуска и нажмите кнопку "Изменить".](./media/app-insights-annotations/30.png)
4. <span data-ttu-id="86dd6-133">Набор hello **APIKey** переменной tooa поля `$(ApiKey)`.</span><span class="sxs-lookup"><span data-stu-id="86dd6-133">Set hello **APIKey** field tooa variable `$(ApiKey)`.</span></span>

5. <span data-ttu-id="86dd6-134">Обратно в hello Azure окна создайте новый ключ API и сделайте его копию.</span><span class="sxs-lookup"><span data-stu-id="86dd6-134">Back in hello Azure window, create a new API Key and take a copy of it.</span></span>
   
    ![В hello колонке доступа к API в Azure окно приветствия нажмите кнопку Создать ключ API.](./media/app-insights-annotations/40.png)

6. <span data-ttu-id="86dd6-138">Перейдите на вкладку конфигурации hello hello шаблона выпуска.</span><span class="sxs-lookup"><span data-stu-id="86dd6-138">Open hello Configuration tab of hello release template.</span></span>
   
    <span data-ttu-id="86dd6-139">Создайте определение переменной для `ApiKey`.</span><span class="sxs-lookup"><span data-stu-id="86dd6-139">Create a variable definition for `ApiKey`.</span></span>
   
    <span data-ttu-id="86dd6-140">Вставьте определение переменной ApiKey ключа toohello ваш API.</span><span class="sxs-lookup"><span data-stu-id="86dd6-140">Paste your API key toohello ApiKey variable definition.</span></span>
   
    ![В окне Team Services hello перейдите на вкладку конфигурации hello и нажмите кнопку Добавить переменную.](./media/app-insights-annotations/50.png)
7. <span data-ttu-id="86dd6-143">Наконец **Сохранить** hello определения выпуска.</span><span class="sxs-lookup"><span data-stu-id="86dd6-143">Finally, **Save** hello release definition.</span></span>


## <a name="view-annotations"></a><span data-ttu-id="86dd6-144">Просмотр заметок</span><span class="sxs-lookup"><span data-stu-id="86dd6-144">View annotations</span></span>
<span data-ttu-id="86dd6-145">Теперь при использовании toodeploy шаблона выпуска hello нового выпуска заметки будут отправляться tooApplication аналитики.</span><span class="sxs-lookup"><span data-stu-id="86dd6-145">Now, whenever you use hello release template toodeploy a new release, an annotation will be sent tooApplication Insights.</span></span> <span data-ttu-id="86dd6-146">Hello заметки будут отображаться на диаграммах в обозревателе метрик.</span><span class="sxs-lookup"><span data-stu-id="86dd6-146">hello annotations will appear on charts in Metrics Explorer.</span></span>

<span data-ttu-id="86dd6-147">Щелкните любой заметки маркер tooopen подробности hello выпуска, включая запрашивающей стороны, ветвь системы управления версиями, определение выпуска, среды и многое другое.</span><span class="sxs-lookup"><span data-stu-id="86dd6-147">Click on any annotation marker tooopen details about hello release, including requestor, source control branch, release definition, environment, and more.</span></span>

![Щелкните любой маркер заметки о выпуске.](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a><span data-ttu-id="86dd6-149">Создание настраиваемых заметок в PowerShell</span><span class="sxs-lookup"><span data-stu-id="86dd6-149">Create custom annotations from PowerShell</span></span>
<span data-ttu-id="86dd6-150">Вы можете создать аннотации из любого процесса на свой выбор (без использования Visual Studio Team System).</span><span class="sxs-lookup"><span data-stu-id="86dd6-150">You can also create annotations from any process you like (without using VS Team System).</span></span> 


1. <span data-ttu-id="86dd6-151">Создать локальную копию hello [сценарий Powershell из GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span><span class="sxs-lookup"><span data-stu-id="86dd6-151">Make a local copy of hello [Powershell script from GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span></span>

2. <span data-ttu-id="86dd6-152">Получить идентификатор приложения hello и создайте ключ API из hello колонке доступа к API.</span><span class="sxs-lookup"><span data-stu-id="86dd6-152">Get hello Application ID and create an API key from hello API Access blade.</span></span>

3. <span data-ttu-id="86dd6-153">Вызов скрипта hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="86dd6-153">Call hello script like this:</span></span>

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

<span data-ttu-id="86dd6-154">Это легко toomodify hello скрипт, например toocreate заметок для прошлых hello.</span><span class="sxs-lookup"><span data-stu-id="86dd6-154">It's easy toomodify hello script, for example toocreate annotations for hello past.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86dd6-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="86dd6-155">Next steps</span></span>

* [<span data-ttu-id="86dd6-156">Создание рабочих элементов</span><span class="sxs-lookup"><span data-stu-id="86dd6-156">Create work items</span></span>](app-insights-diagnostic-search.md#create-work-item)
* [<span data-ttu-id="86dd6-157">Автоматизация с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="86dd6-157">Automation with PowerShell</span></span>](app-insights-powershell.md)
