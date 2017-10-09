---
title: "aaaCreate ASP.NET веб-приложения в Azure | Документы Microsoft"
description: "Узнайте, как toorun веб-приложений в службе приложений Azure путем развертывания по умолчанию hello ASP.NET веб-приложения."
services: app-service\web
documentationcenter: 
author: cephalin
manager: wpickett
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 06/14/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: eec916b3c32b6c8b68083177938c5c822a9782b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-in-azure"></a><span data-ttu-id="28a7a-103">Создание веб-приложения ASP.NET в Azure</span><span class="sxs-lookup"><span data-stu-id="28a7a-103">Create an ASP.NET web app in Azure</span></span>

<span data-ttu-id="28a7a-104">[Веб-приложения Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) — это служба веб-размещения с самостоятельной установкой исправлений и высоким уровнем масштабируемости.</span><span class="sxs-lookup"><span data-stu-id="28a7a-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="28a7a-105">Краткого руководства показано, как toodeploy первый ASP.NET веб-приложения tooAzure веб-приложений.</span><span class="sxs-lookup"><span data-stu-id="28a7a-105">This quickstart shows how toodeploy your first ASP.NET web app tooAzure Web Apps.</span></span> <span data-ttu-id="28a7a-106">В результате будет создана группа ресурсов, состоящая из плана службы приложений и развернутого веб-приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="28a7a-106">When you're finished, you'll have a resource group that consists of an App Service plan and an Azure web app with a deployed web application.</span></span>

<span data-ttu-id="28a7a-107">Посмотрите видео toosee hello краткого руководства в действии, а затем следуйте hello шаги самостоятельно toopublish своего первого приложения .NET в Azure.</span><span class="sxs-lookup"><span data-stu-id="28a7a-107">Watch hello video toosee this quickstart in action and then follow hello steps yourself toopublish your first .NET app on Azure.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-NET-Developers/Create-a-NET-app-in-Azure-Quickstart/player]

## <a name="prerequisites"></a><span data-ttu-id="28a7a-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="28a7a-108">Prerequisites</span></span>

<span data-ttu-id="28a7a-109">toocomplete этого учебника:</span><span class="sxs-lookup"><span data-stu-id="28a7a-109">toocomplete this tutorial:</span></span>

* <span data-ttu-id="28a7a-110">Установка [2017 г. Visual Studio](https://www.visualstudio.com/downloads/) с hello следующие рабочие нагрузки:</span><span class="sxs-lookup"><span data-stu-id="28a7a-110">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello following workloads:</span></span>
    - <span data-ttu-id="28a7a-111">**ASP.NET и веб-разработка;**</span><span class="sxs-lookup"><span data-stu-id="28a7a-111">**ASP.NET and web development**</span></span>
    - <span data-ttu-id="28a7a-112">**разработка Azure.**</span><span class="sxs-lookup"><span data-stu-id="28a7a-112">**Azure development**</span></span>

    ![ASP.NET и веб-разработка, разработка Azure (в разделе Web & Cloud (Сеть и облако))](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="28a7a-114">Создание веб-приложения ASP.NET</span><span class="sxs-lookup"><span data-stu-id="28a7a-114">Create an ASP.NET web app</span></span>

<span data-ttu-id="28a7a-115">Создайте проект в Visual Studio, последовательно выбрав пункты **Файл > Создать > Проект**.</span><span class="sxs-lookup"><span data-stu-id="28a7a-115">In Visual Studio, create a project by selecting **File > New > Project**.</span></span> 

<span data-ttu-id="28a7a-116">В hello **новый проект** диалогового окна выберите **Visual C# > Web > веб-приложения ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="28a7a-116">In hello **New Project** dialog, select **Visual C# > Web > ASP.NET Web Application (.NET Framework)**.</span></span>

<span data-ttu-id="28a7a-117">Имя приложения hello _myFirstAzureWebApp_, а затем выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="28a7a-117">Name hello application _myFirstAzureWebApp_, and then select **OK**.</span></span>
   
![Диалоговое окно "Новый проект"](./media/app-service-web-get-started-dotnet/new-project.png)

<span data-ttu-id="28a7a-119">Вы можете развернуть любого типа tooAzure приложения ASP.NET web.</span><span class="sxs-lookup"><span data-stu-id="28a7a-119">You can deploy any type of ASP.NET web app tooAzure.</span></span> <span data-ttu-id="28a7a-120">Для краткого руководства, выберите hello **MVC** шаблона и убедитесь, что проверка подлинности задано слишком**без проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="28a7a-120">For this quickstart, select hello **MVC** template, and make sure authentication is set too**No Authentication**.</span></span>
      
<span data-ttu-id="28a7a-121">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="28a7a-121">Select **OK**.</span></span>

![Диалоговое окно "Новый проект ASP.NET"](./media/app-service-web-get-started-dotnet/select-mvc-template.png)

<span data-ttu-id="28a7a-123">Меню "hello" выберите **Отладка > Начать без отладки** toorun hello веб-приложения локально.</span><span class="sxs-lookup"><span data-stu-id="28a7a-123">From hello menu, select **Debug > Start without Debugging** toorun hello web app locally.</span></span>

![Локальный запуск приложения](./media/app-service-web-get-started-dotnet/local-web-app.png)

## <a name="publish-tooazure"></a><span data-ttu-id="28a7a-125">Публикация tooAzure</span><span class="sxs-lookup"><span data-stu-id="28a7a-125">Publish tooAzure</span></span>

<span data-ttu-id="28a7a-126">В hello **обозревателе решений**, щелкните правой кнопкой мыши hello **myFirstAzureWebApp** проект и выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="28a7a-126">In hello **Solution Explorer**, right-click hello **myFirstAzureWebApp** project and select **Publish**.</span></span>

![Публикация в обозревателе решений](./media/app-service-web-get-started-dotnet/solution-explorer-publish.png)

<span data-ttu-id="28a7a-128">Выберите **Служба приложений Microsoft Azure** и нажмите кнопку **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="28a7a-128">Make sure that **Microsoft Azure App Service** is selected and select **Publish**.</span></span>

![Публикация с помощью страницы обзора проекта](./media/app-service-web-get-started-dotnet/publish-to-app-service.png)

<span data-ttu-id="28a7a-130">При этом откроется hello **Создание приложения службы** диалоговое окно, которое служит для создания всех hello необходимые ресурсы Azure toorun hello, ASP.NET веб-приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="28a7a-130">This opens hello **Create App Service** dialog, which helps you create all hello necessary Azure resources toorun hello ASP.NET web app in Azure.</span></span>

## <a name="sign-in-tooazure"></a><span data-ttu-id="28a7a-131">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="28a7a-131">Sign in tooAzure</span></span>

<span data-ttu-id="28a7a-132">В hello **Создание приложения службы** диалогового окна выберите **добавить учетную запись**и выполните вход tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="28a7a-132">In hello **Create App Service** dialog, select **Add an account**, and sign in tooyour Azure subscription.</span></span> <span data-ttu-id="28a7a-133">Если вы уже выполнили вход, выберите hello учетной записи, содержащей hello правильно подписку из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="28a7a-133">If you're already signed in, select hello account containing hello desired subscription from hello dropdown.</span></span>

> [!NOTE]
> <span data-ttu-id="28a7a-134">Если вы уже выполнили вход, пока не нажимайте кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="28a7a-134">If you're already signed in, don't select **Create** yet.</span></span>
>
>
   
![Войдите в tooAzure](./media/app-service-web-get-started-dotnet/sign-in-azure.png)

## <a name="create-a-resource-group"></a><span data-ttu-id="28a7a-136">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="28a7a-136">Create a resource group</span></span>

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

<span data-ttu-id="28a7a-137">Далее слишком**группы ресурсов**выберите **New**.</span><span class="sxs-lookup"><span data-stu-id="28a7a-137">Next too**Resource Group**, select **New**.</span></span>

<span data-ttu-id="28a7a-138">Имя группы ресурсов hello **myResourceGroup** и выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="28a7a-138">Name hello resource group **myResourceGroup** and select **OK**.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="28a7a-139">Создание плана службы приложений</span><span class="sxs-lookup"><span data-stu-id="28a7a-139">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="28a7a-140">Далее слишком**план служб приложений**выберите **New**.</span><span class="sxs-lookup"><span data-stu-id="28a7a-140">Next too**App Service Plan**, select **New**.</span></span> 

<span data-ttu-id="28a7a-141">В hello **настроить план служб приложений** диалогового окна, используйте параметры hello в таблице hello следующий снимок экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="28a7a-141">In hello **Configure App Service Plan** dialog, use hello settings in hello table following hello screenshot.</span></span>

![Создание плана службы приложений](./media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

| <span data-ttu-id="28a7a-143">Настройка</span><span class="sxs-lookup"><span data-stu-id="28a7a-143">Setting</span></span> | <span data-ttu-id="28a7a-144">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="28a7a-144">Suggested Value</span></span> | <span data-ttu-id="28a7a-145">Описание</span><span class="sxs-lookup"><span data-stu-id="28a7a-145">Description</span></span> |
|-|-|-|
|<span data-ttu-id="28a7a-146">План обслуживания приложения</span><span class="sxs-lookup"><span data-stu-id="28a7a-146">App Service Plan</span></span>| <span data-ttu-id="28a7a-147">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="28a7a-147">myAppServicePlan</span></span> | <span data-ttu-id="28a7a-148">Имя плана служб приложений hello.</span><span class="sxs-lookup"><span data-stu-id="28a7a-148">Name of hello App Service plan.</span></span> |
| <span data-ttu-id="28a7a-149">Расположение</span><span class="sxs-lookup"><span data-stu-id="28a7a-149">Location</span></span> | <span data-ttu-id="28a7a-150">Западная Европа</span><span class="sxs-lookup"><span data-stu-id="28a7a-150">West Europe</span></span> | <span data-ttu-id="28a7a-151">Hello центра обработки данных, где размещается веб-приложение hello.</span><span class="sxs-lookup"><span data-stu-id="28a7a-151">hello datacenter where hello web app is hosted.</span></span> |
| <span data-ttu-id="28a7a-152">Размер</span><span class="sxs-lookup"><span data-stu-id="28a7a-152">Size</span></span> | <span data-ttu-id="28a7a-153">Free</span><span class="sxs-lookup"><span data-stu-id="28a7a-153">Free</span></span> | <span data-ttu-id="28a7a-154">[Ценовая категория](https://azure.microsoft.com/pricing/details/app-service/) определяет возможности размещения.</span><span class="sxs-lookup"><span data-stu-id="28a7a-154">[Pricing tier](https://azure.microsoft.com/pricing/details/app-service/) determines hosting features.</span></span> |

<span data-ttu-id="28a7a-155">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="28a7a-155">Select **OK**.</span></span>

## <a name="create-and-publish-hello-web-app"></a><span data-ttu-id="28a7a-156">Создание и публикация веб-приложения hello</span><span class="sxs-lookup"><span data-stu-id="28a7a-156">Create and publish hello web app</span></span>

<span data-ttu-id="28a7a-157">В **имя веб-приложения**, введите имя уникальным приложения (допустимые символы — `a-z`, `0-9`, и `-`), или примите hello автоматически создается уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="28a7a-157">In **Web App Name**, type a unique app name (valid characters are `a-z`, `0-9`, and `-`), or accept hello automatically generated unique name.</span></span> <span data-ttu-id="28a7a-158">Hello URL-адрес веб-приложения hello `http://<app_name>.azurewebsites.net`, где `<app_name>` является имя вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="28a7a-158">hello URL of hello web app is `http://<app_name>.azurewebsites.net`, where `<app_name>` is your web app name.</span></span>

<span data-ttu-id="28a7a-159">Выберите **создать** toostart Создание hello ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="28a7a-159">Select **Create** toostart creating hello Azure resources.</span></span>

![Настройка имени веб-приложения](./media/app-service-web-get-started-dotnet/web-app-name.png)

<span data-ttu-id="28a7a-161">После завершения работы мастера hello, он публикует hello ASP.NET web app tooAzure и затем запускает hello приложение в браузере по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="28a7a-161">Once hello wizard completes, it publishes hello ASP.NET web app tooAzure, and then launches hello app in hello default browser.</span></span>

![Опубликованное веб-приложение ASP.NET в Azure](./media/app-service-web-get-started-dotnet/published-azure-web-app.png)

<span data-ttu-id="28a7a-163">Имя веб-приложения Hello, указанный в hello [Создание и публикация шаг](#create-and-publish-the-web-app) используется как префикс URL-адреса в формате hello hello `http://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="28a7a-163">hello web app name specified in hello [create and publish step](#create-and-publish-the-web-app) is used as hello URL prefix in hello format `http://<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="28a7a-164">Поздравляем, ваше веб-приложение ASP.NET работает в службе приложений Azure в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="28a7a-164">Congratulations, your ASP.NET web app is running live in Azure App Service.</span></span>

## <a name="update-hello-app-and-redeploy"></a><span data-ttu-id="28a7a-165">Приложение hello обновления и повторного развертывания</span><span class="sxs-lookup"><span data-stu-id="28a7a-165">Update hello app and redeploy</span></span>

<span data-ttu-id="28a7a-166">Из hello **обозревателе решений**откройте _Views\Home\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="28a7a-166">From hello **Solution Explorer**, open _Views\Home\Index.cshtml_.</span></span>

<span data-ttu-id="28a7a-167">Найти hello `<div class="jumbotron">` HTML тег верхней hello и замените весь элемент hello hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="28a7a-167">Find hello `<div class="jumbotron">` HTML tag near hello top, and replace hello entire element with hello following code:</span></span>

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how toodeploy a .NET app tooAzure App Service.</p>
</div>
```

<span data-ttu-id="28a7a-168">tooAzure tooredeploy, щелкните правой кнопкой мыши hello **myFirstAzureWebApp** проекта в **обозревателе решений** и выберите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="28a7a-168">tooredeploy tooAzure, right-click hello **myFirstAzureWebApp** project in **Solution Explorer** and select **Publish**.</span></span>

<span data-ttu-id="28a7a-169">Страница "Публикация" hello, установите **публикации**.</span><span class="sxs-lookup"><span data-stu-id="28a7a-169">In hello publish page, select **Publish**.</span></span>

<span data-ttu-id="28a7a-170">По завершении публикации Visual Studio запускает браузер toohello URL-адрес веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="28a7a-170">When publishing completes, Visual Studio launches a browser toohello URL of hello web app.</span></span>

![Обновленное веб-приложение ASP.NET в Azure](./media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="manage-hello-azure-web-app"></a><span data-ttu-id="28a7a-172">Управление hello Azure веб-приложения</span><span class="sxs-lookup"><span data-stu-id="28a7a-172">Manage hello Azure web app</span></span>

<span data-ttu-id="28a7a-173">Go toohello <a href="https://portal.azure.com" target="_blank">портал Azure</a> toomanage hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="28a7a-173">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app.</span></span>

<span data-ttu-id="28a7a-174">Hello в левом меню, выберите **службы приложений**, а затем выберите имя hello Azure веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="28a7a-174">From hello left menu, select **App Services**, and then select hello name of your Azure web app.</span></span>

![Веб-приложения портала навигации tooAzure](./media/app-service-web-get-started-dotnet/access-portal.png)

<span data-ttu-id="28a7a-176">Отобразится страница обзора вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="28a7a-176">You see your web app's Overview page.</span></span> <span data-ttu-id="28a7a-177">Вы можете выполнять базовые задачи управления: обзор, завершение, запуск, перезагрузку и удаление.</span><span class="sxs-lookup"><span data-stu-id="28a7a-177">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Колонка службы приложений на портале Azure](./media/app-service-web-get-started-dotnet/web-app-blade.png)

<span data-ttu-id="28a7a-179">меню слева Hello предоставляет различные страницы для настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="28a7a-179">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="28a7a-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="28a7a-180">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="28a7a-181">Создание приложения ASP.NET в Azure с подключением к базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="28a7a-181">ASP.NET with SQL Database</span></span>](app-service-web-tutorial-dotnet-sqldatabase.md)
