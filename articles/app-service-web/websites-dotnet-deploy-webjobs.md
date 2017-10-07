---
title: "aaaDeploy веб-заданий с помощью Visual Studio"
description: "Узнайте, как веб-заданий Azure toodeploy tooAzure приложения службы веб-приложений с помощью Visual Studio."
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
ms.openlocfilehash: 5fc5d9562e8836348f5ab6844fb6c23ff40a321c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-webjobs-using-visual-studio"></a><span data-ttu-id="98d6a-103">Развертывание веб-заданий с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="98d6a-103">Deploy WebJobs using Visual Studio</span></span>
## <a name="overview"></a><span data-ttu-id="98d6a-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="98d6a-104">Overview</span></span>
<span data-ttu-id="98d6a-105">В этом разделе объясняется, как Visual Studio toouse toodeploy консольного приложения проекта tooa веб-приложения в [службы приложений](http://go.microsoft.com/fwlink/?LinkId=529714) как [веб-задания Azure](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="98d6a-105">This topic explains how toouse Visual Studio toodeploy a Console Application project tooa web app in [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) as an [Azure WebJob](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span> <span data-ttu-id="98d6a-106">Сведения о как hello toodeploy веб-заданий с помощью [портала Azure](https://portal.azure.com), в разделе [запуск фоновых задач с веб-задания](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="98d6a-106">For information about how toodeploy WebJobs by using hello [Azure Portal](https://portal.azure.com), see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

<span data-ttu-id="98d6a-107">При развертывании в Visual Studio проекта консольного приложения с поддержкой веб-заданий выполняются две задачи.</span><span class="sxs-lookup"><span data-stu-id="98d6a-107">When Visual Studio deploys a WebJobs-enabled Console Application project, it performs two tasks:</span></span>

* <span data-ttu-id="98d6a-108">Файлы среды выполнения копии toohello соответствующую папку в веб-приложения hello (*App_Data и задания и непрерывной* для непрерывные веб-задания *App_Data и заданий и запуске* веб-заданиях расписанию и по запросу).</span><span class="sxs-lookup"><span data-stu-id="98d6a-108">Copies runtime files toohello appropriate folder in hello web app (*App_Data/jobs/continuous* for continuous WebJobs, *App_Data/jobs/triggered* for scheduled and on-demand WebJobs).</span></span>
* <span data-ttu-id="98d6a-109">Настраивает [заданий планировщика Azure](#scheduler) для веб-заданий, запланированных toorun в определенные промежутки времени.</span><span class="sxs-lookup"><span data-stu-id="98d6a-109">Sets up [Azure Scheduler jobs](#scheduler) for WebJobs that are scheduled toorun at particular times.</span></span> <span data-ttu-id="98d6a-110">(Это не требуется для постоянных веб-заданий.)</span><span class="sxs-lookup"><span data-stu-id="98d6a-110">(This is not needed for continuous WebJobs.)</span></span>

<span data-ttu-id="98d6a-111">Включить веб-заданий проект содержит следующие элементы добавлены tooit hello:</span><span class="sxs-lookup"><span data-stu-id="98d6a-111">A WebJobs-enabled project has hello following items added tooit:</span></span>

* <span data-ttu-id="98d6a-112">Hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="98d6a-112">hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package.</span></span>
* <span data-ttu-id="98d6a-113">Файл [webjob-publish-settings.json](#publishsettings) , который содержит параметры развертывания и планировщика.</span><span class="sxs-lookup"><span data-stu-id="98d6a-113">A [webjob-publish-settings.json](#publishsettings) file that contains deployment and scheduler settings.</span></span> 

![Схема, показывающая, что добавляется развертывания tooenable tooa консольного приложения как веб-задания](./media/websites-dotnet-deploy-webjobs/convert.png)

<span data-ttu-id="98d6a-115">Можно добавить эти элементы, tooan существующий проект консольного приложения или использовать шаблон toocreate новый проект консольного приложения с поддержкой веб-заданий.</span><span class="sxs-lookup"><span data-stu-id="98d6a-115">You can add these items tooan existing Console Application project or use a template toocreate a new WebJobs-enabled Console Application project.</span></span> 

<span data-ttu-id="98d6a-116">Можно развернуть проект как веб-задания сам по себе или свяжите его tooa веб-проекта, чтобы автоматически развертывает при каждом развертывании hello веб-проекта.</span><span class="sxs-lookup"><span data-stu-id="98d6a-116">You can deploy a project as a WebJob by itself, or link it tooa web project so that it automatically deploys whenever you deploy hello web project.</span></span> <span data-ttu-id="98d6a-117">проекты toolink Visual Studio включает имя hello hello включен веб-задания проекта в [list.json веб-заданий](#webjobslist) файл в проекте веб-hello.</span><span class="sxs-lookup"><span data-stu-id="98d6a-117">toolink projects, Visual Studio includes hello name of hello WebJobs-enabled project in a [webjobs-list.json](#webjobslist) file in hello web project.</span></span>

![Схема, показывающая связи tooweb проекта проектов веб-задания](./media/websites-dotnet-deploy-webjobs/link.png)

## <a name="prerequisites"></a><span data-ttu-id="98d6a-119">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="98d6a-119">Prerequisites</span></span>
<span data-ttu-id="98d6a-120">Средства развертывания веб-заданий доступны в Visual Studio при установке hello Azure SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="98d6a-120">WebJobs deployment features are available in Visual Studio when you install hello Azure SDK for .NET:</span></span>

* <span data-ttu-id="98d6a-121">[Пакет SDK Azure для .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="98d6a-121">[Azure SDK for .NET (Visual Studio)](https://azure.microsoft.com/downloads/).</span></span>

## <span data-ttu-id="98d6a-122"><a id="convert"></a>Включение развертывания веб-заданий для существующего проекта консольного приложения</span><span class="sxs-lookup"><span data-stu-id="98d6a-122"><a id="convert"></a>Enable WebJobs deployment for an existing Console Application project</span></span>
<span data-ttu-id="98d6a-123">Существует два варианта.</span><span class="sxs-lookup"><span data-stu-id="98d6a-123">You have two options:</span></span>

* <span data-ttu-id="98d6a-124">[Включение автоматического развертывания с веб-проектом](#convertlink).</span><span class="sxs-lookup"><span data-stu-id="98d6a-124">[Enable automatic deployment with a web project](#convertlink).</span></span>
  
    <span data-ttu-id="98d6a-125">Настройка существующего проекта приложения консоли для автоматического развертывания в качестве веб-приложения при развертывании веб-проекта.</span><span class="sxs-lookup"><span data-stu-id="98d6a-125">Configure an existing Console Application project so that it automatically deploys as a WebJob when you deploy a web project.</span></span> <span data-ttu-id="98d6a-126">Используйте этот параметр, если нужно toorun веб-задание в hello веб-приложения, связанные с одной веб-приложения, в котором выполняются hello.</span><span class="sxs-lookup"><span data-stu-id="98d6a-126">Use this option when you want toorun your WebJob in hello same web app in which you run hello related web application.</span></span>
* <span data-ttu-id="98d6a-127">[Включение развертывания без веб-проекта](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="98d6a-127">[Enable deployment without a web project](#convertnolink).</span></span>
  
    <span data-ttu-id="98d6a-128">Настройте существующие toodeploy проекта консольного приложения как веб-задания сама по себе с нет ссылок tooa веб-проекта.</span><span class="sxs-lookup"><span data-stu-id="98d6a-128">Configure an existing Console Application project toodeploy as a WebJob by itself, with no link tooa web project.</span></span> <span data-ttu-id="98d6a-129">Используйте этот параметр при необходимости toorun веб-задание в веб-приложения с веб-приложений, не работает в веб-приложения hello сама по себе.</span><span class="sxs-lookup"><span data-stu-id="98d6a-129">Use this option when you want toorun a WebJob in a web app by itself, with no web application running in hello web app.</span></span> <span data-ttu-id="98d6a-130">Может потребоваться toodo это в заказ может tooscale toobe ресурсам веб-задание, независимо от ресурсам веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="98d6a-130">You might want toodo this in order toobe able tooscale your WebJob resources independently of your web application resources.</span></span>

### <span data-ttu-id="98d6a-131"><a id="convertlink"></a> Включение автоматического развертывания веб-заданий с помощью веб-проекта</span><span class="sxs-lookup"><span data-stu-id="98d6a-131"><a id="convertlink"></a> Enable automatic WebJobs deployment with a web project</span></span>
1. <span data-ttu-id="98d6a-132">Щелкните правой кнопкой мыши проект веб-hello в **обозревателе решений**, а затем нажмите кнопку **добавить** > **существующий проект как веб-задания Azure**.</span><span class="sxs-lookup"><span data-stu-id="98d6a-132">Right-click hello web project in **Solution Explorer**, and then click **Add** > **Existing Project as Azure WebJob**.</span></span>
   
    ![Существующий проект как веб-задание Azure](./media/websites-dotnet-deploy-webjobs/eawj.png)
   
    <span data-ttu-id="98d6a-134">Hello [добавить веб-задание Azure](#configure) откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="98d6a-134">hello [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="98d6a-135">В hello **имя проекта** раскрывающегося списка, выберите hello tooadd проекта консольного приложения как веб-задания.</span><span class="sxs-lookup"><span data-stu-id="98d6a-135">In hello **Project name** drop-down list, select hello Console Application project tooadd as a WebJob.</span></span>
   
    ![Выбор проекта в диалоговом окне "Добавление веб-задания Azure"](./media/websites-dotnet-deploy-webjobs/aaw1.png)
3. <span data-ttu-id="98d6a-137">Полный hello [добавить веб-задание Azure](#configure) диалогового окна, а затем щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="98d6a-137">Complete hello [Add Azure WebJob](#configure) dialog, and then click **OK**.</span></span> 

### <span data-ttu-id="98d6a-138"><a id="convertnolink"></a> Включение развертывания веб-заданий без веб-проекта</span><span class="sxs-lookup"><span data-stu-id="98d6a-138"><a id="convertnolink"></a> Enable WebJobs deployment without a web project</span></span>
1. <span data-ttu-id="98d6a-139">Щелкните правой кнопкой мыши проект консольного приложения hello в **обозревателе решений**, а затем нажмите кнопку **опубликовать как веб-задания Azure...** .</span><span class="sxs-lookup"><span data-stu-id="98d6a-139">Right-click hello Console Application project in **Solution Explorer**, and then click **Publish as Azure WebJob...**.</span></span> 
   
    ![Опубликовать как веб-задание Azure](./media/websites-dotnet-deploy-webjobs/paw.png)
   
    <span data-ttu-id="98d6a-141">Hello [добавить веб-задание Azure](#configure) появится диалоговое окно с проект hello в hello **имя проекта** поле.</span><span class="sxs-lookup"><span data-stu-id="98d6a-141">hello [Add Azure WebJob](#configure) dialog box appears, with hello project selected in hello **Project name** box.</span></span>
2. <span data-ttu-id="98d6a-142">Полный hello [добавить веб-задание Azure](#configure) диалоговое окно, а затем щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="98d6a-142">Complete hello [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>
   
   <span data-ttu-id="98d6a-143">Hello **веб-публикация** откроется окно мастера.</span><span class="sxs-lookup"><span data-stu-id="98d6a-143">hello **Publish Web** wizard appears.</span></span>  <span data-ttu-id="98d6a-144">Если вы не хотите toopublish немедленно, закройте мастер hello.</span><span class="sxs-lookup"><span data-stu-id="98d6a-144">If you do not want toopublish immediately, close hello wizard.</span></span> <span data-ttu-id="98d6a-145">Hello параметры, которые вы ввели сохраняются для при необходимости слишком[развертывание проекта hello](#deploy).</span><span class="sxs-lookup"><span data-stu-id="98d6a-145">hello settings that you've entered are saved for when you do want too[deploy hello project](#deploy).</span></span>

## <span data-ttu-id="98d6a-146"><a id="create"></a>Создание нового проекта с поддержкой веб-заданий</span><span class="sxs-lookup"><span data-stu-id="98d6a-146"><a id="create"></a>Create a new WebJobs-enabled project</span></span>
<span data-ttu-id="98d6a-147">toocreate новый проект с поддержкой веб-заданий можно использовать hello консольного приложения проекта шаблона и включить веб-задания развертывания как описано в [hello предыдущего раздела](#convert).</span><span class="sxs-lookup"><span data-stu-id="98d6a-147">toocreate a new WebJobs-enabled project, you can use hello Console Application project template and enable WebJobs deployment as explained in [hello previous section](#convert).</span></span> <span data-ttu-id="98d6a-148">В качестве альтернативы можно использовать шаблон нового проекта веб-заданий hello:</span><span class="sxs-lookup"><span data-stu-id="98d6a-148">As an alternative, you can use hello WebJobs new-project template:</span></span>

* [<span data-ttu-id="98d6a-149">Используйте шаблон нового проекта веб-заданий hello для независимых веб-задания</span><span class="sxs-lookup"><span data-stu-id="98d6a-149">Use hello WebJobs new-project template for an independent WebJob</span></span>](#createnolink)
  
    <span data-ttu-id="98d6a-150">Создайте проект и настройте его toodeploy сам по себе как веб-задание с нет ссылок tooa веб-проекта.</span><span class="sxs-lookup"><span data-stu-id="98d6a-150">Create a project and configure it toodeploy by itself as a WebJob, with no link tooa web project.</span></span> <span data-ttu-id="98d6a-151">Используйте этот параметр при необходимости toorun веб-задание в веб-приложения с веб-приложений, не работает в веб-приложения hello сама по себе.</span><span class="sxs-lookup"><span data-stu-id="98d6a-151">Use this option when you want toorun a WebJob in a web app by itself, with no web application running in hello web app.</span></span> <span data-ttu-id="98d6a-152">Может потребоваться toodo это в заказ может tooscale toobe ресурсам веб-задание, независимо от ресурсам веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="98d6a-152">You might want toodo this in order toobe able tooscale your WebJob resources independently of your web application resources.</span></span>
* [<span data-ttu-id="98d6a-153">Используйте шаблон нового проекта веб-заданий hello связанного tooa веб-проекта веб-задания</span><span class="sxs-lookup"><span data-stu-id="98d6a-153">Use hello WebJobs new-project template for a WebJob linked tooa web project</span></span>](#createlink)
  
    <span data-ttu-id="98d6a-154">Создание проекта, настроенного toodeploy автоматически как веб-задание при веб-проекта в одно решение развертывается приветствия.</span><span class="sxs-lookup"><span data-stu-id="98d6a-154">Create a project that is configured toodeploy automatically as a WebJob when a web project in hello same solution is deployed.</span></span> <span data-ttu-id="98d6a-155">Используйте этот параметр, если нужно toorun веб-задание в hello веб-приложения, связанные с одной веб-приложения, в котором выполняются hello.</span><span class="sxs-lookup"><span data-stu-id="98d6a-155">Use this option when you want toorun your WebJob in hello same web app in which you run hello related web application.</span></span>

> [!NOTE]
> <span data-ttu-id="98d6a-156">шаблон нового проекта веб-заданий Hello автоматически устанавливает пакеты NuGet и включает код в *Program.cs* для hello [SDK веб-задания](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span><span class="sxs-lookup"><span data-stu-id="98d6a-156">hello WebJobs new-project template automatically installs NuGet packages and includes code in *Program.cs* for hello [WebJobs SDK](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/getting-started-with-windows-azure-webjobs).</span></span> <span data-ttu-id="98d6a-157">Если вы не хотите toouse hello SDK веб-заданий, удалить или изменить hello `host.RunAndBlock` инструкции в *Program.cs*.</span><span class="sxs-lookup"><span data-stu-id="98d6a-157">If you don't want toouse hello WebJobs SDK, remove or change hello `host.RunAndBlock` statement in *Program.cs*.</span></span>
> 
> 

### <span data-ttu-id="98d6a-158"><a id="createnolink"></a>Используйте шаблон нового проекта веб-заданий hello для независимых веб-задания</span><span class="sxs-lookup"><span data-stu-id="98d6a-158"><a id="createnolink"></a> Use hello WebJobs new-project template for an independent WebJob</span></span>
1. <span data-ttu-id="98d6a-159">Нажмите кнопку **файл** > **новый проект**, а затем в hello **новый проект** диалоговом окне **облака**  >   **Веб-задание Azure (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="98d6a-159">Click **File** > **New Project**, and then in hello **New Project** dialog box click **Cloud** > **Azure WebJob (.NET Framework)**.</span></span>
   
    ![Диалоговое окно "Новый проект", отображающее шаблон веб-заданий](./media/websites-dotnet-deploy-webjobs/np.png)
2. <span data-ttu-id="98d6a-161">Следуйте приведенным инструкциям hello, показанного выше слишком[сделать hello проект консольного приложения в проект веб-заданий независимым](#convertnolink).</span><span class="sxs-lookup"><span data-stu-id="98d6a-161">Follow hello directions shown earlier too[make hello Console Application project an independent WebJobs project](#convertnolink).</span></span>

### <span data-ttu-id="98d6a-162"><a id="createlink"></a>Используйте шаблон нового проекта веб-заданий hello связанного tooa веб-проекта веб-задания</span><span class="sxs-lookup"><span data-stu-id="98d6a-162"><a id="createlink"></a> Use hello WebJobs new-project template for a WebJob linked tooa web project</span></span>
1. <span data-ttu-id="98d6a-163">Щелкните правой кнопкой мыши проект веб-hello в **обозревателе решений**, а затем нажмите кнопку **добавить** > **новый проект веб-задания Azure**.</span><span class="sxs-lookup"><span data-stu-id="98d6a-163">Right-click hello web project in **Solution Explorer**, and then click **Add** > **New Azure WebJob Project**.</span></span>
   
    ![Запись меню "Новый проект веб-задания Azure"](./media/websites-dotnet-deploy-webjobs/nawj.png)
   
    <span data-ttu-id="98d6a-165">Hello [добавить веб-задание Azure](#configure) откроется диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="98d6a-165">hello [Add Azure WebJob](#configure) dialog box appears.</span></span>
2. <span data-ttu-id="98d6a-166">Полный hello [добавить веб-задание Azure](#configure) диалоговое окно, а затем щелкните **ОК**.</span><span class="sxs-lookup"><span data-stu-id="98d6a-166">Complete hello [Add Azure WebJob](#configure) dialog box, and then click **OK**.</span></span>

## <span data-ttu-id="98d6a-167"><a id="configure"></a>диалоговое окно Добавить веб-задание Azure Hello</span><span class="sxs-lookup"><span data-stu-id="98d6a-167"><a id="configure"></a>hello Add Azure WebJob dialog</span></span>
<span data-ttu-id="98d6a-168">Hello **добавить веб-задание Azure** диалоговое окно позволяет вводить имя веб-задания hello и выполнить настройку режима для вашего веб-задания.</span><span class="sxs-lookup"><span data-stu-id="98d6a-168">hello **Add Azure WebJob** dialog lets you enter hello WebJob name and run mode setting for your WebJob.</span></span> 

![Диалоговое окно "Добавление веб-заданий Azure"](./media/websites-dotnet-deploy-webjobs/aaw2.png)

<span data-ttu-id="98d6a-170">Hello поля в этом диалоговом окне соответствуют toofields на hello **новое задание** диалогового окна hello портала Azure.</span><span class="sxs-lookup"><span data-stu-id="98d6a-170">hello fields in this dialog correspond toofields on hello **New Job** dialog of hello Azure Portal.</span></span> <span data-ttu-id="98d6a-171">Дополнительные сведения см. в разделе [Выполнение фоновых задач с помощью веб-заданий](web-sites-create-web-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="98d6a-171">For more information, see [Run Background tasks with WebJobs](web-sites-create-web-jobs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="98d6a-172">Дополнительные сведения о развертывании из командной строки см. в разделе [Включение предоставления веб-заданий Azure из командной строки или постоянно](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span><span class="sxs-lookup"><span data-stu-id="98d6a-172">For information about command-line deployment, see [Enabling Command-line or Continuous Delivery of Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/).</span></span>
> * <span data-ttu-id="98d6a-173">Если развертывается веб-задания, а затем решить, что следует toochange типа hello веб-задания и повторного развертывания, вам потребуется файл публикации settings.json веб-заданий toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="98d6a-173">If you deploy a WebJob and then decide you want toochange hello type of WebJob and redeploy, you'll need toodelete hello webjobs-publish-settings.json file.</span></span> <span data-ttu-id="98d6a-174">Благодаря Visual Studio представления hello, параметры публикации, поэтому можно изменить тип hello веб-задания.</span><span class="sxs-lookup"><span data-stu-id="98d6a-174">This will make Visual Studio show hello publishing options again, so you can change hello type of WebJob.</span></span>
> * <span data-ttu-id="98d6a-175">При развертывании веб-задания, если впоследствии изменить hello режиме выполнения из непрерывного toonon непрерывные или наоборот, Visual Studio создает новый веб-задание в Azure, при повторном развертывании.</span><span class="sxs-lookup"><span data-stu-id="98d6a-175">If you deploy a WebJob and later change hello run mode from continuous toonon-continuous or vice versa, Visual Studio creates a new WebJob in Azure when you redeploy.</span></span> <span data-ttu-id="98d6a-176">Если изменить другие параметры планирования или расписания, но режим запуска оставьте hello таким же или переключаться между расписанию и по запросу, обновлений Visual Studio hello существующее задание вместо создания нового.</span><span class="sxs-lookup"><span data-stu-id="98d6a-176">If you change other scheduling settings but leave run mode hello same or switch between Scheduled and On Demand, Visual Studio updates hello existing job rather than create a new one.</span></span>
> 
> 

## <span data-ttu-id="98d6a-177"><a id="publishsettings"></a>webjob-publish-settings.json</span><span class="sxs-lookup"><span data-stu-id="98d6a-177"><a id="publishsettings"></a>webjob-publish-settings.json</span></span>
<span data-ttu-id="98d6a-178">При настройке консольное приложение для развертывания веб-заданий Visual Studio устанавливает hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet пакета и хранилищ, планирование сведения в *публикации settings.json веб-задания*  файл в проекте hello *свойства* папки проекта веб-заданий hello.</span><span class="sxs-lookup"><span data-stu-id="98d6a-178">When you configure a Console Application for WebJobs deployment, Visual Studio installs hello [Microsoft.Web.WebJobs.Publish](http://www.nuget.org/packages/Microsoft.Web.WebJobs.Publish/) NuGet package and stores scheduling information in a *webjob-publish-settings.json* file in hello project *Properties* folder of hello WebJobs project.</span></span> <span data-ttu-id="98d6a-179">Вот пример этого файла:</span><span class="sxs-lookup"><span data-stu-id="98d6a-179">Here is an example of that file:</span></span>

        {
          "$schema": "http://schemastore.org/schemas/json/webjob-publish-settings.json",
          "webJobName": "WebJob1",
          "startTime": "null",
          "endTime": "null",
          "jobRecurrenceFrequency": "null",
          "interval": null,
          "runMode": "Continuous"
        }

<span data-ttu-id="98d6a-180">Вы можете изменить этот файл напрямую, и Visual Studio предоставит IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="98d6a-180">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="98d6a-181">схема файла Hello хранится на [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) и доступны для просмотра.</span><span class="sxs-lookup"><span data-stu-id="98d6a-181">hello file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjob-publish-settings.json) and can be viewed there.</span></span>  

## <span data-ttu-id="98d6a-182"><a id="webjobslist"></a>webjobs-list.json</span><span class="sxs-lookup"><span data-stu-id="98d6a-182"><a id="webjobslist"></a>webjobs-list.json</span></span>
<span data-ttu-id="98d6a-183">При связывании tooa проекта с поддержкой веб-заданий веб-проекта Visual Studio сохраняет hello имя проекта веб-заданий hello в *веб-заданий list.json* файла в проекте веб-hello *свойства* папки.</span><span class="sxs-lookup"><span data-stu-id="98d6a-183">When you link a WebJobs-enabled project tooa web project, Visual Studio stores hello name of hello WebJobs project in a *webjobs-list.json* file in hello web project's *Properties* folder.</span></span> <span data-ttu-id="98d6a-184">Hello список может содержать несколько проектов веб-задания, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="98d6a-184">hello list might contain multiple WebJobs projects, as shown in hello following example:</span></span>

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

<span data-ttu-id="98d6a-185">Вы можете изменить этот файл напрямую, и Visual Studio предоставит IntelliSense.</span><span class="sxs-lookup"><span data-stu-id="98d6a-185">You can edit this file directly, and Visual Studio provides IntelliSense.</span></span> <span data-ttu-id="98d6a-186">схема файла Hello хранится на [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) и доступны для просмотра.</span><span class="sxs-lookup"><span data-stu-id="98d6a-186">hello file schema is stored at [http://schemastore.org](http://schemastore.org/schemas/json/webjobs-list.json) and can be viewed there.</span></span>

## <span data-ttu-id="98d6a-187"><a id="deploy"></a>Развертывание проекта веб-заданий</span><span class="sxs-lookup"><span data-stu-id="98d6a-187"><a id="deploy"></a>Deploy a WebJobs project</span></span>
<span data-ttu-id="98d6a-188">Проект веб-заданий, вы связали tooa веб-проекта автоматически развертывает с hello веб-проекта.</span><span class="sxs-lookup"><span data-stu-id="98d6a-188">A WebJobs project that you have linked tooa web project deploys automatically with hello web project.</span></span> <span data-ttu-id="98d6a-189">Сведения о развертывании веб-проектов см. в разделе [как toodeploy tooWeb приложения](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="98d6a-189">For information about web project deployment, see [How toodeploy tooWeb Apps](web-sites-deploy.md).</span></span>

<span data-ttu-id="98d6a-190">toodeploy проект веб-заданий самостоятельно, щелкните правой кнопкой мыши проект hello в **обозревателе решений** и нажмите кнопку **опубликовать как веб-задания Azure...** .</span><span class="sxs-lookup"><span data-stu-id="98d6a-190">toodeploy a WebJobs project by itself, right-click hello project in **Solution Explorer** and click **Publish as Azure WebJob...**.</span></span> 

![Опубликовать как веб-задание Azure](./media/websites-dotnet-deploy-webjobs/paw.png)

<span data-ttu-id="98d6a-192">Для независимых веб-задания hello же **веб-публикация** мастер, используемый для веб-проектов отображается, но с меньшим числом toochange доступные параметры.</span><span class="sxs-lookup"><span data-stu-id="98d6a-192">For an independent WebJob, hello same **Publish Web** wizard that is used for web projects appears, but with fewer settings available toochange.</span></span>

## <span data-ttu-id="98d6a-193"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="98d6a-193"><a id="nextsteps"></a>Next Steps</span></span>
<span data-ttu-id="98d6a-194">В этой статье показано как toodeploy веб-заданий с помощью Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="98d6a-194">This article has explained how toodeploy WebJobs by using Visual Studio.</span></span> <span data-ttu-id="98d6a-195">Дополнительные сведения о том, как toodeploy веб-задания Azure, отображается [веб-заданий Azure — рекомендуется использовать ресурсы - развертывания](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span><span class="sxs-lookup"><span data-stu-id="98d6a-195">For more information about how toodeploy Azure WebJobs, see [Azure WebJobs - Recommended Resources - Deployment](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/azure-webjobs-recommended-resources#deploying).</span></span>

