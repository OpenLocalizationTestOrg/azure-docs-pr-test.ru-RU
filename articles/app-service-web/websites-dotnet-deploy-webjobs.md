---
title: "Развертывание веб-заданий с помощью Visual Studio"
description: "Узнайте, как развернуть веб-задания Azure в веб-приложениях службы приложений Azure с помощью Visual Studio."
services: app-service
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: a3a9d320-1201-4ac8-9398-b4c9535ba755
ms.service: app-service
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2016
ms.author: glenga
ms.openlocfilehash: 5b0808afdadcf4d86a9a2d07ee6fc63b80b22993
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a><span data-ttu-id="21d5c-103">Развертывание веб-заданий с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="21d5c-103">Deploy WebJobs using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="21d5c-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="21d5c-104">Overview</span></span>
<span data-ttu-id="21d5c-105">В этом разделе объясняется, как использовать Visual Studio для развертывания проекта консольного приложения в веб-приложении [службы приложений](http://go.microsoft.com/fwlink/?LinkId=529714) в качестве [веб-задания Azure](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="21d5c-105">This topic explains how to use Visual Studio to deploy a Console Application project to a web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) as an [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span> <span data-ttu-id="21d5c-106">Дополнительную информацию о развертывании веб-заданий с помощью [портала Azure](https://portal.azure.com) см. в разделе [Выполнение фоновых задач с помощью веб-заданий](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="21d5c-106">For information about how to deploy WebJobs by using the [Azure Portal](https://portal.azure.com), see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

<span data-ttu-id="21d5c-107">При развертывании в Visual Studio проекта консольного приложения с поддержкой веб-заданий выполняются две задачи.</span><span class="sxs-lookup"><span data-stu-id="21d5c-107">When Visual Studio deploys a WebJobs-enabled Console Application project, it performs two tasks:</span></span>

* <span data-ttu-id="21d5c-108">Копирование файлов среды выполнения в соответствующую папку в веб-приложении (*App_Data/jobs/continuous* для постоянных веб-заданий, *App_Data/jobs/triggered* для запланированных веб-заданий и веб-заданий по запросу).</span><span class="sxs-lookup"><span data-stu-id="21d5c-108">Copies runtime files to the appropriate folder in the web app (*App_Data/jobs/continuous* for continuous WebJobs, *App_Data/jobs/triggered* for scheduled and on-demand WebJobs).</span></span>
* <span data-ttu-id="21d5c-109">Указание [заданий планировщика Azure](#scheduler) для веб-заданий, которые запланированы на выполнение в определенное время.</span><span class="sxs-lookup"><span data-stu-id="21d5c-109">Sets up [Azure Scheduler jobs](#scheduler) for WebJobs that are scheduled to run at particular times.</span></span> <span data-ttu-id="21d5c-110">(Это не требуется для постоянных веб-заданий.)</span><span class="sxs-lookup"><span data-stu-id="21d5c-110">(This is not needed for continuous WebJobs.)</span></span>

<span data-ttu-id="21d5c-111">Проект с поддержкой веб-заданий содержит следующие добавленные элементы.</span><span class="sxs-lookup"><span data-stu-id="21d5c-111">A WebJobs-enabled project has the following items added to it:</span></span>

* <span data-ttu-id="21d5c-112">Пакет NuGet [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) .</span><span class="sxs-lookup"><span data-stu-id="21d5c-112">The [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package.</span></span>
* <span data-ttu-id="21d5c-113">Файл [webjob-publish-settings.json](#publishsettings) , который содержит параметры развертывания и планировщика.</span><span class="sxs-lookup"><span data-stu-id="21d5c-113">A [webjob-publish-settings.json](#publishsettings) file that contains deployment and scheduler settings.</span></span> 

![Диаграмма, отображающая добавленные элементы в приложение консоли для реализации развертывания как веб-задания](./media/websites-dotnet-deploy-webjobs/convert.png)

<span data-ttu-id="21d5c-115">Вы можете добавить эти элементы в существующий проект приложения консоли или использовать шаблон для создания нового проекта приложения консоли с поддержкой веб-заданий.</span><span class="sxs-lookup"><span data-stu-id="21d5c-115">You can add these items to an existing Console Application project or use a template to create a new WebJobs-enabled Console Application project.</span></span> 

<span data-ttu-id="21d5c-116">Можно развернуть проект как веб-задание или связать его с веб-проектом для автоматического развертывания при каждом развертывании веб-проекта.</span><span class="sxs-lookup"><span data-stu-id="21d5c-116">You can deploy a project as a WebJob by itself, or link it to a web project so that it automatically deploys whenever you deploy the web project.</span></span> <span data-ttu-id="21d5c-117">Чтобы связать проекты, Visual Studio включает имя проекта с поддержкой веб-заданий в файле [webjobs-list.json](#webjobslist) веб-проекта.</span><span class="sxs-lookup"><span data-stu-id="21d5c-117">To link projects, Visual Studio includes the name of the WebJobs-enabled project in a [webjobs-list.json](#webjobslist) file in the web project.</span></span>

![Диаграмма, отображающая проект веб-задания, связанный с веб-проектом](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a><span data-ttu-id="21d5c-119">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="21d5c-119">Prerequisites</span></span>
<span data-ttu-id="21d5c-120">Функции развертывания веб-заданий доступны в Visual Studio при установке пакета SDK Azure для .NET:</span><span class="sxs-lookup"><span data-stu-id="21d5c-120">WebJobs deployment features are available in Visual Studio when you install the Azure SDK for .NET:</span></span>

* <span data-ttu-id="21d5c-121">[Пакет SDK Azure для .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="21d5c-121">[Azure SDK for .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span></span>

## <span data-ttu-id="21d5c-122"><a id="convert"></a>Включение развертывания веб-заданий для существующего проекта консольного приложения</span><span class="sxs-lookup"><span data-stu-id="21d5c-122"><a id="convert"></a>Enable WebJobs deployment for an existing Console Application project</span></span>
<span data-ttu-id="21d5c-123">Существует два варианта.</span><span class="sxs-lookup"><span data-stu-id="21d5c-123">You have two options:</span></span>

* <span data-ttu-id="21d5c-124">[Включение автоматического развертывания с веб-проектом](#convertlink).</span><span class="sxs-lookup"><span data-stu-id="21d5c-124">[Enable automatic deployment with a web project](#convertlink).</span></span>
  
    <span data-ttu-id="21d5c-125">Настройка существующего проекта приложения консоли для автоматического развертывания в качестве веб-приложения при развертывании веб-проекта.</span><span class="sxs-lookup"><span data-stu-id="21d5c-125">Configure an existing Console Application project so that it automatically deploys as a WebJob when you deploy a web project.</span></span> <span data-ttu-id="21d5c-126">Используйте этот параметр, если нужно запустить веб-задание в том же веб-приложении, в котором запущено связанное веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="21d5c-126">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span></span>
* <span data-ttu-id="21d5c-127">[Включение развертывания без веб-проекта](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="21d5c-127">[Enable deployment without a web project](#convertnolink).</span></span>
  
    <span data-ttu-id="21d5c-128">Настройка существующего проекта приложения консоли для развертывания в качестве веб-задания без ссылки на веб-проект.</span><span class="sxs-lookup"><span data-stu-id="21d5c-128">Configure an existing Console Application project to deploy as a WebJob by itself, with no link to a web project.</span></span> <span data-ttu-id="21d5c-129">Используйте этот параметр, если нужно запустить веб-задание в веб-приложении самостоятельно, без веб-приложения, запущенного в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="21d5c-129">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span></span> <span data-ttu-id="21d5c-130">Это может понадобиться для независимого масштабирования ресурсов веб-заданий ресурсов веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="21d5c-130">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span></span>

### <span data-ttu-id="21d5c-131"><a id="convertlink"></a> Включение автоматического развертывания веб-заданий с помощью веб-проекта</span><span class="sxs-lookup"><span data-stu-id="21d5c-131"><a id="convertlink"></a> Enable automatic WebJobs deployment with a web project</span></span>
1. <span data-ttu-id="21d5c-132">Щелкните правой кнопкой мыши проект в **обозревателе решений** и выберите **Добавить** > **Существующий проект как веб-задание Azure**.</span><span class="sxs-lookup"><span data-stu-id="21d5c-132">Right-click the web project in **Solution Explorer**, and then click **Add** > **Existing Project as Azure WebJob**.</span></span>
   
    ![Существующий проект как веб-задание Azure](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    <span data-ttu-id="21d5c-134">Откроется диалоговое окно [Добавление веб-задания Azure](#configure) .</span><span class="sxs-lookup"><span data-stu-id="21d5c-134">The [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="21d5c-135">В раскрывающемся списке **Имя проекта** выберите проект приложения консоли для добавления в качестве веб-задания.</span><span class="sxs-lookup"><span data-stu-id="21d5c-135">In the **Project name** drop-down list, select the Console Application project to add as a WebJob.</span></span>
   
    ![Выбор проекта в диалоговом окне "Добавление веб-задания Azure"](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. <span data-ttu-id="21d5c-137">Заполните диалоговое окно [Добавление веб-задания Azure](#configure) и щелкните кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="21d5c-137">Complete the [Add Azure WebJob](#configure) dialog, and then click **OK**.</span></span> 

### <span data-ttu-id="21d5c-138"><a id="convertnolink"></a> Включение развертывания веб-заданий без веб-проекта</span><span class="sxs-lookup"><span data-stu-id="21d5c-138"><a id="convertnolink"></a> Enable WebJobs deployment without a web project</span></span>
1. <span data-ttu-id="21d5c-139">Щелкните правой кнопкой мыши проект консольного приложения в **обозревателе решений** и выберите **Опубликовать как веб-задание Azure…**.</span><span class="sxs-lookup"><span data-stu-id="21d5c-139">Right-click the Console Application project in **Solution Explorer**, and then click **Publish as Azure WebJob...**.</span></span> 
   
    ![Опубликовать как веб-задание Azure](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    <span data-ttu-id="21d5c-141">Появится диалоговое окно [Добавление веб-задания Azure](#configure) с проектом, выбранным в поле **Имя проекта** .</span><span class="sxs-lookup"><span data-stu-id="21d5c-141">The [Add Azure WebJob](#configure) dialog box appears, with the project selected in the **Project name** box.</span></span>
2. <span data-ttu-id="21d5c-142">Заполните диалоговое окно [Добавление веб-задания Azure](#configure) и щелкните кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="21d5c-142">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>
   
   <span data-ttu-id="21d5c-143">Откроется мастер **веб-публикации** .</span><span class="sxs-lookup"><span data-stu-id="21d5c-143">The **Publish Web** wizard appears.</span></span>  <span data-ttu-id="21d5c-144">Если вы не хотите сразу выполнить публикацию, закройте мастер.</span><span class="sxs-lookup"><span data-stu-id="21d5c-144">If you do not want to publish immediately, close the wizard.</span></span> <span data-ttu-id="21d5c-145">Указанные параметры сохраняются до момента [развертывания проекта](#deploy).</span><span class="sxs-lookup"><span data-stu-id="21d5c-145">The settings that you've entered are saved for when you do want to [deploy the project](#deploy).</span></span>

## <span data-ttu-id="21d5c-146"><a id="create"></a>Создание нового проекта с поддержкой веб-заданий</span><span class="sxs-lookup"><span data-stu-id="21d5c-146"><a id="create"></a>Create a new WebJobs-enabled project</span></span>
<span data-ttu-id="21d5c-147">Чтобы создать проект с поддержкой веб-заданий, можно использовать шаблон проекта приложения консоли и включить развертывание веб-заданий, как показано в [предыдущем разделе](#convert).</span><span class="sxs-lookup"><span data-stu-id="21d5c-147">To create a new WebJobs-enabled project, you can use the Console Application project template and enable WebJobs deployment as explained in [the previous section](#convert).</span></span> <span data-ttu-id="21d5c-148">В качестве альтернативы можно использовать шаблон создания проекта с поддержкой веб-заданий:</span><span class="sxs-lookup"><span data-stu-id="21d5c-148">As an alternative, you can use the WebJobs new-project template:</span></span>

* [<span data-ttu-id="21d5c-149">Использование шаблона создания проекта веб-заданий для отдельного веб-задания</span><span class="sxs-lookup"><span data-stu-id="21d5c-149">Use the WebJobs new-project template for an independent WebJob</span></span>](#createnolink)
  
    <span data-ttu-id="21d5c-150">Создайте проект и настройте его для развертывания в качестве веб-задания без ссылки на веб-проект.</span><span class="sxs-lookup"><span data-stu-id="21d5c-150">Create a project and configure it to deploy by itself as a WebJob, with no link to a web project.</span></span> <span data-ttu-id="21d5c-151">Используйте этот параметр, если нужно запустить веб-задание в веб-приложении самостоятельно, без веб-приложения, запущенного в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="21d5c-151">Use this option when you want to run a WebJob in a web app by itself, with no web application running in the web app.</span></span> <span data-ttu-id="21d5c-152">Это может понадобиться для независимого масштабирования ресурсов веб-заданий ресурсов веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="21d5c-152">You might want to do this in order to be able to scale your WebJob resources independently of your web application resources.</span></span>
* [<span data-ttu-id="21d5c-153">Использование шаблона создания проекта с поддержкой веб-заданий для веб-задания, связанного с веб-проектом</span><span class="sxs-lookup"><span data-stu-id="21d5c-153">Use the WebJobs new-project template for a WebJob linked to a web project</span></span>](#createlink)
  
    <span data-ttu-id="21d5c-154">Создайте проект, настроенный для автоматического развертывания, как веб-задание при развертывании веб-проекта в том же решении.</span><span class="sxs-lookup"><span data-stu-id="21d5c-154">Create a project that is configured to deploy automatically as a WebJob when a web project in the same solution is deployed.</span></span> <span data-ttu-id="21d5c-155">Используйте этот параметр, если нужно запустить веб-задание в том же веб-приложении, в котором запущено связанное веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="21d5c-155">Use this option when you want to run your WebJob in the same web app in which you run the related web application.</span></span>

> [!NOTE]
> <span data-ttu-id="21d5c-156">Шаблон нового проекта веб-задания автоматически устанавливает пакеты NuGet и включает в файл *Program.cs* код для [пакета SDK веб-заданий](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span><span class="sxs-lookup"><span data-stu-id="21d5c-156">The WebJobs new-project template automatically installs NuGet packages and includes code in *Program.cs* for the [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span></span> <span data-ttu-id="21d5c-157">Если вы не хотите использовать пакет SDK для веб-заданий, удалите или измените инструкцию `host.RunAndBlock` в файле *Program.cs*.</span><span class="sxs-lookup"><span data-stu-id="21d5c-157">If you don't want to use the WebJobs SDK, remove or change the `host.RunAndBlock` statement in *Program.cs*.</span></span>
> 
> 

### <span data-ttu-id="21d5c-158"><a id="createnolink"></a> Использование шаблона создания проекта веб-заданий для отдельного веб-задания</span><span class="sxs-lookup"><span data-stu-id="21d5c-158"><a id="createnolink"></a> Use the WebJobs new-project template for an independent WebJob</span></span>
1. <span data-ttu-id="21d5c-159">Щелкните **Файл** > **Создать проект**, а затем в диалоговом окне **Новый проект** выберите **Облако** > **Веб-задание Azure (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="21d5c-159">Click **File** > **New Project**, and then in the **New Project** dialog box click **Cloud** > **Azure WebJob (.NET Framework)**.</span></span>
   
    ![Диалоговое окно "Новый проект", отображающее шаблон веб-заданий](./media/websites-dotnet-deploy-webjobs/np.png)
2. <span data-ttu-id="21d5c-161">Следуйте инструкциям, показанным ранее, чтобы [сделать проект приложения консоли независимым проектом веб-заданий](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="21d5c-161">Follow the directions shown earlier to [make the Console Application project an independent WebJobs project](#convertnolink).</span></span>

### <span data-ttu-id="21d5c-162"><a id="createlink"></a> Использование шаблона создания проекта с поддержкой веб-заданий для веб-задания, связанного с веб-проектом</span><span class="sxs-lookup"><span data-stu-id="21d5c-162"><a id="createlink"></a> Use the WebJobs new-project template for a WebJob linked to a web project</span></span>
1. <span data-ttu-id="21d5c-163">Щелкните правой кнопкой мыши проект в **обозревателе решений** и выберите **Добавить** > **Новый проект веб-задания Azure**.</span><span class="sxs-lookup"><span data-stu-id="21d5c-163">Right-click the web project in **Solution Explorer**, and then click **Add** > **New Azure WebJob Project**.</span></span>
   
    ![Запись меню "Новый проект веб-задания Azure"](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    <span data-ttu-id="21d5c-165">Откроется диалоговое окно [Добавление веб-задания Azure](#configure) .</span><span class="sxs-lookup"><span data-stu-id="21d5c-165">The [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="21d5c-166">Заполните диалоговое окно [Добавление веб-задания Azure](#configure) и щелкните кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="21d5c-166">Complete the [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>

## <span data-ttu-id="21d5c-167"><a id="configure"></a>Диалоговое окно "Добавление веб-заданий Azure"</span><span class="sxs-lookup"><span data-stu-id="21d5c-167"><a id="configure"></a>The Add Azure WebJob dialog</span></span>
<span data-ttu-id="21d5c-168">В диалогом окне **Добавить веб-задание Azure** можно указать имя веб-задания и настроить режим его выполнения.</span><span class="sxs-lookup"><span data-stu-id="21d5c-168">The **Add Azure WebJob** dialog lets you enter the WebJob name and run mode setting for your WebJob.</span></span> 

![Диалоговое окно "Добавление веб-заданий Azure"](./media/websites-dotnet-deploy-webjobs/aaw2.png)

<span data-ttu-id="21d5c-170">Поля в этом диалоговом окне соответствуют полям в диалоговом окне **Новое задание** портала Azure.</span><span class="sxs-lookup"><span data-stu-id="21d5c-170">The fields in this dialog correspond to fields on the **New Job** dialog of the Azure Portal.</span></span> <span data-ttu-id="21d5c-171">Дополнительные сведения см. в разделе [Выполнение фоновых задач с помощью веб-заданий](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="21d5c-171">For more information, see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="21d5c-172">Дополнительные сведения о развертывании из командной строки см. в разделе [Включение предоставления веб-заданий Azure из командной строки или постоянно](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span><span class="sxs-lookup"><span data-stu-id="21d5c-172">For information about command-line deployment, see [Enabling Command-line or Continuous Delivery of Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span></span>
> * <span data-ttu-id="21d5c-173">Если после развертывания веб-задания принимается решение о необходимости изменить его тип и развернуть веб-задание повторно, нужно будет удалить файл webjobs-publish-settings.json.</span><span class="sxs-lookup"><span data-stu-id="21d5c-173">If you deploy a WebJob and then decide you want to change the type of WebJob and redeploy, you'll need to delete the webjobs-publish-settings.json file.</span></span> <span data-ttu-id="21d5c-174">При этом Visual Studio снова покажет параметры публикации и можно будет изменить тип веб-задания.</span><span class="sxs-lookup"><span data-stu-id="21d5c-174">This will make Visual Studio show the publishing options again, so you can change the type of WebJob.</span></span>
> * <span data-ttu-id="21d5c-175">Если вы развертываете веб-задание, а затем изменяете режим выполнения с постоянного на непостоянный или наоборот, Visual Studio создаст новое веб-задание в Azure при повторном развертывании.</span><span class="sxs-lookup"><span data-stu-id="21d5c-175">If you deploy a WebJob and later change the run mode from continuous to non-continuous or vice versa, Visual Studio creates a new WebJob in Azure when you redeploy.</span></span> <span data-ttu-id="21d5c-176">При изменении других параметров планирования но сохранении режима выполнения или при переключении между режимами "Запланировано" и "По запросу" Visual Studio обновляет существующее задание, а не создает новое.</span><span class="sxs-lookup"><span data-stu-id="21d5c-176">If you change other scheduling settings but leave run mode the same or switch between Scheduled and On Demand, Visual Studio updates the existing job rather than create a new one.</span></span>
> 
> 

## <span data-ttu-id="21d5c-177"><a id="publishsettings"></a>webjob-publish-settings.json</span><span class="sxs-lookup"><span data-stu-id="21d5c-177"><a id="publishsettings"></a>webjob-publish-settings.json</span></span>
<span data-ttu-id="21d5c-178">При настройке консольного приложения для развертывания веб-заданий Visual Studio устанавливает пакет NuGet [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) и сохраняет сведения о планировании в файле *webjob-publish-settings.json* в папке *Properties* проекта веб-заданий.</span><span class="sxs-lookup"><span data-stu-id="21d5c-178">When you configure a Console Application for WebJobs deployment, Visual Studio installs the [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package and stores scheduling information in a *webjob-publish-settings.json* file in the project *Properties* folder of the WebJobs project.</span></span> <span data-ttu-id="21d5c-179">Вот пример этого файла:</span><span class="sxs-lookup"><span data-stu-id="21d5c-179">Here is an example of that file:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

<span data-ttu-id="21d5c-180">Вы можете изменить этот файл напрямую, и Visual Studio предоставит IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="21d5c-180">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="21d5c-181">Схема файла сохранена на сайте [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) , и ее можно просмотреть здесь.</span><span class="sxs-lookup"><span data-stu-id="21d5c-181">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) and can be viewed there.</span></span>  

## <span data-ttu-id="21d5c-182"><a id="webjobslist"></a>webjobs-list.json</span><span class="sxs-lookup"><span data-stu-id="21d5c-182"><a id="webjobslist"></a>webjobs-list.json</span></span>
<span data-ttu-id="21d5c-183">При связывании проекта с поддержкой веб-заданий с веб-проектом Visual Studio сохраняет имя проекта веб-заданий в файле *webjobs-list.json* в папке веб-проекта *Properties*.</span><span class="sxs-lookup"><span data-stu-id="21d5c-183">When you link a WebJobs-enabled project to a web project, Visual Studio stores the name of the WebJobs project in a *webjobs-list.json* file in the web project's *Properties* folder.</span></span> <span data-ttu-id="21d5c-184">Список может содержать несколько проектов веб-заданий, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="21d5c-184">The list might contain multiple WebJobs projects, as shown in the following example:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjobs-list.json",
          "WebJobs": [
            {
              "filePath": "../ConsoleApplication1/ConsoleApplication1.csproj"
            },
            {
              "filePath": "../WebJob1/WebJob1.csproj"
            }
          ]
        }

<span data-ttu-id="21d5c-185">Вы можете изменить этот файл напрямую, и Visual Studio предоставит IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="21d5c-185">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="21d5c-186">Схема файла сохранена на сайте [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) , и ее можно просмотреть здесь.</span><span class="sxs-lookup"><span data-stu-id="21d5c-186">The file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) and can be viewed there.</span></span>

## <span data-ttu-id="21d5c-187"><a id="deploy"></a>Развертывание проекта веб-заданий</span><span class="sxs-lookup"><span data-stu-id="21d5c-187"><a id="deploy"></a>Deploy a WebJobs project</span></span>
<span data-ttu-id="21d5c-188">Проект веб-заданий, связанный с веб-проектом, развертывается автоматически с веб-проектом.</span><span class="sxs-lookup"><span data-stu-id="21d5c-188">A WebJobs project that you have linked to a web project deploys automatically with the web project.</span></span> <span data-ttu-id="21d5c-189">Информацию о развертывании веб-проектов см. в разделе [Развертывание приложения в службе приложений Azure](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="21d5c-189">For information about web project deployment, see [How to deploy to Web Apps](web-sites-deploy.md).</span></span>

<span data-ttu-id="21d5c-190">Чтобы развернуть проект веб-заданий, щелкните правой кнопкой мыши проект в **обозревателе решений** и выберите **Опубликовать как веб-задание Azure…**.</span><span class="sxs-lookup"><span data-stu-id="21d5c-190">To deploy a WebJobs project by itself, right-click the project in **Solution Explorer** and click **Publish as Azure WebJob...**.</span></span> 

![Опубликовать как веб-задание Azure](./media/websites-dotnet-deploy-webjobs/paw.png)

<span data-ttu-id="21d5c-192">Для независимого веб-задания отобразится тот же мастер **веб-публикации** , который использовался для веб-проектов, но некоторые параметры будут недоступны для изменения.</span><span class="sxs-lookup"><span data-stu-id="21d5c-192">For an independent WebJob, the same **Publish Web** wizard that is used for web projects appears, but with fewer settings available to change.</span></span>

## <span data-ttu-id="21d5c-193"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="21d5c-193"><a id="nextsteps"></a>Next Steps</span></span>
<span data-ttu-id="21d5c-194">В этой статье показано, как развернуть WebJob с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="21d5c-194">This article has explained how to deploy WebJobs by using Visual Studio.</span></span> <span data-ttu-id="21d5c-195">Дополнительные сведения о развертывании веб-заданий Azure см. в статье [Документация по веб-заданиям Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span><span class="sxs-lookup"><span data-stu-id="21d5c-195">For more information about how to deploy Azure WebJobs, see [Azure WebJobs - Recommended Resources - Deployment](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span></span>

