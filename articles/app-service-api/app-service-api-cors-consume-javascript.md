---
title: "Поддержка CORS в службе приложений | Документация Майкрософт"
description: "Узнайте, как использовать поддержку CORS в службе приложений Azure."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 4f980a97-b9f5-4d1d-87ab-82b60bb96e1c
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/27/2016
ms.author: alkarche
ms.openlocfilehash: f8373cf5b2e06e6c71bce51cd9e9d5123eea7cfd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="consume-an-api-app-from-javascript-using-cors"></a><span data-ttu-id="c3757-103">Использование приложения API из JavaScript с помощью CORS</span><span class="sxs-lookup"><span data-stu-id="c3757-103">Consume an API app from JavaScript using CORS</span></span>
<span data-ttu-id="c3757-104">В службе приложений реализована встроенная поддержка технологии [общего доступа к ресурсам независимо от источника (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), что позволяет клиентам JavaScript выполнять междоменные вызовы к API, размещенным в приложениях API.</span><span class="sxs-lookup"><span data-stu-id="c3757-104">App Service offers built-in support for [Cross Origin Resource Sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), which enables JavaScript clients to make cross-domain calls to APIs that are hosted in API apps.</span></span> <span data-ttu-id="c3757-105">С помощью службы приложений можно настроить доступ CORS без написания кода в API.</span><span class="sxs-lookup"><span data-stu-id="c3757-105">App Service lets you configure CORS access to your API without writing any code in your API.</span></span>

<span data-ttu-id="c3757-106">Эта статья содержит два раздела.</span><span class="sxs-lookup"><span data-stu-id="c3757-106">This article contains two sections:</span></span>

* <span data-ttu-id="c3757-107">В разделе [Настройка CORS](#corsconfig) описывается общая настройка CORS для любого приложения API, веб-приложения или мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="c3757-107">The [How to configure CORS](#corsconfig) section explains in general how to configure CORS for any API app, web app, or mobile app.</span></span> <span data-ttu-id="c3757-108">Инструкции из этого раздела применимы ко всем платформам, которые поддерживает служба приложений, включая .NET, Node.js и Java.</span><span class="sxs-lookup"><span data-stu-id="c3757-108">It applies equally to all frameworks that are supported by App Service, including .NET, Node.js, and Java.</span></span> 
* <span data-ttu-id="c3757-109">Начиная с раздела [Продолжение руководства по началу работы с .NET](#tutorialstart) в статье описывается использование CORS. Для работы с этой частью необходимо выполнить инструкции, приведенные [в первом руководстве по началу работы с приложениями API](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c3757-109">Starting with the [Continuing the .NET getting-started tutorials](#tutorialstart) section, the article is a tutorial that demonstrates CORS support by building on what you did in [the first API Apps getting started tutorial](app-service-api-dotnet-get-started.md).</span></span> 

## <span data-ttu-id="c3757-110"><a id="corsconfig"></a> Настройка CORS в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="c3757-110"><a id="corsconfig"></a> How to configure CORS in Azure App Service</span></span>
<span data-ttu-id="c3757-111">CORS можно настроить на портале Azure или с помощью средств [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c3757-111">You can configure CORS in the Azure portal or by using [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) tools.</span></span>

#### <a name="configure-cors-in-the-azure-portal"></a><span data-ttu-id="c3757-112">Настройка CORS на портале Azure</span><span class="sxs-lookup"><span data-stu-id="c3757-112">Configure CORS in the Azure portal</span></span>
1. <span data-ttu-id="c3757-113">В браузере перейдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c3757-113">In a browser go to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c3757-114">Щелкните **Службы приложений**и выберите имя приложения API.</span><span class="sxs-lookup"><span data-stu-id="c3757-114">Click **App Services**, and then click the name of your API app.</span></span>
   
    ![Выбор приложения API на портале](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="c3757-116">В колонке **Параметры**, расположенной справа от колонки **Приложение API**, найдите раздел **API** и щелкните элемент **CORS**.</span><span class="sxs-lookup"><span data-stu-id="c3757-116">In the **Settings** blade that opens to the right of the **API app** blade, find the **API** section, and then click **CORS**.</span></span>
   
   ![Выбор CORS в колонке параметров](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="c3757-118">В текстовое поле введите URL-адреса, с которых следует разрешить вызовы JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c3757-118">In the text box enter the URL or URLs that you want to allow JavaScript calls to come from.</span></span>

    <span data-ttu-id="c3757-119">Например, если вы развернули приложение JavaScript в веб-приложении с именем todolistangular, введите https://todolistangular.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="c3757-119">For example, if you deployed your JavaScript application to a web app named todolistangular, enter "https://todolistangular.azurewebsites.net".</span></span> <span data-ttu-id="c3757-120">Вместо URL-адресов можно ввести символ звездочки (*). В таком случае будут приниматься вызовы из всех исходных доменов.</span><span class="sxs-lookup"><span data-stu-id="c3757-120">As an alternative, you can enter an asterisk (*) to specify that all origin domains are accepted.</span></span>


1. <span data-ttu-id="c3757-121">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c3757-121">Click **Save**.</span></span>
   
   ![Щелкните Сохранить](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="c3757-123">После нажатия кнопки **Сохранить**приложение API начнет принимать вызовы JavaScript с указанных URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="c3757-123">After you click **Save**, the API app will accept JavaScript calls from the specified URLs.</span></span>

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a><span data-ttu-id="c3757-124">Настройка CORS с помощью средств диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="c3757-124">Configure CORS by using Azure Resource Manager tools</span></span>
<span data-ttu-id="c3757-125">CORS для приложения API можно также настроить с помощью [шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md), используя такие программы командной строки, как [Azure PowerShell](/powershell/azureps-cmdlets-docs) и [интерфейс командной строки Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c3757-125">You can also configure CORS for an API app by using [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) in command line tools such as [Azure PowerShell](/powershell/azureps-cmdlets-docs) and the [Azure CLI](../cli-install-nodejs.md).</span></span> 

<span data-ttu-id="c3757-126">Чтобы просмотреть пример шаблона Azure Resource Manager, который задает свойство CORS, откройте [в репозитории файл azuredeploy.json, пример приложения для этого руководства](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="c3757-126">For an example of an Azure Resource Manager template that sets the CORS property, open the [azuredeploy.json file in the repository for this tutorial's sample application](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span></span> <span data-ttu-id="c3757-127">Найдите раздел шаблона, который выглядит так:</span><span class="sxs-lookup"><span data-stu-id="c3757-127">Find the section of the template that looks like the following example:</span></span>

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <span data-ttu-id="c3757-128"><a id="tutorialstart"></a> Продолжение руководства по началу работы с .NET</span><span class="sxs-lookup"><span data-stu-id="c3757-128"><a id="tutorialstart"></a> Continuing the .NET getting-started tutorial</span></span>
<span data-ttu-id="c3757-129">Если вы изучаете серию руководств для приложений API по началу работы с Node.js или Java, на этом этапе данная серия заканчивается.</span><span class="sxs-lookup"><span data-stu-id="c3757-129">If you are following the Node.js or Java getting-started series for API apps, you have completed the getting started series.</span></span> <span data-ttu-id="c3757-130">Перейдите к разделу [Дальнейшие действия](#next-steps) , в котором предложены дополнительные статьи о приложениях API.</span><span class="sxs-lookup"><span data-stu-id="c3757-130">Skip to the [Next steps](#next-steps) section to find suggestions for further learning about API Apps.</span></span>

<span data-ttu-id="c3757-131">Оставшаяся часть статьи — это продолжение серии руководств по началу работы с .NET, для работы с которой вам нужно сначала выполнить инструкции, приведенные в [первом руководстве](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c3757-131">The remainder of this article is a continuation of the .NET getting-started series and assumes that you successfully completed [the first tutorial](app-service-api-dotnet-get-started.md).</span></span>

## <a name="deploy-the-todolistangular-project-to-a-new-web-app"></a><span data-ttu-id="c3757-132">Развертывание проекта ToDoListAngular в новом веб-приложении</span><span class="sxs-lookup"><span data-stu-id="c3757-132">Deploy the ToDoListAngular project to a new web app</span></span>
<span data-ttu-id="c3757-133">Следуя инструкциям из [первого руководства](app-service-api-dotnet-get-started.md), вы создали приложение API среднего уровня и приложение API уровня данных.</span><span class="sxs-lookup"><span data-stu-id="c3757-133">In [the first tutorial](app-service-api-dotnet-get-started.md), you created a middle tier API app and a data tier API app.</span></span> <span data-ttu-id="c3757-134">Изучив это руководство, вы создадите одностраничное веб-приложение (SPA), которое вызывает приложение API среднего уровня.</span><span class="sxs-lookup"><span data-stu-id="c3757-134">In this tutorial you create a single-page application (SPA) web app that calls the middle tier API app.</span></span> <span data-ttu-id="c3757-135">Для работы SPA следует включить поддержку CORS в приложении API среднего уровня.</span><span class="sxs-lookup"><span data-stu-id="c3757-135">For the SPA to work you have to enable CORS on the middle tier API app.</span></span> 

<span data-ttu-id="c3757-136">В [примере приложения ToDoList](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list)проект ToDoListAngular является простым клиентом AngularJS, который используется для вызова проекта веб-API среднего уровня ToDoListAPI.</span><span class="sxs-lookup"><span data-stu-id="c3757-136">In the [ToDoList sample application](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), the ToDoListAngular project is a simple AngularJS client that calls the middle tier ToDoListAPI Web API project.</span></span> <span data-ttu-id="c3757-137">Код JavaScript в файле *app/scripts/todoListSvc.js* вызывает API с использованием поставщика HTTP AngularJS.</span><span class="sxs-lookup"><span data-stu-id="c3757-137">The JavaScript code in the *app/scripts/todoListSvc.js* file calls the API by using the AngularJS HTTP provider.</span></span> 

        angular.module('todoApp')
        .factory('todoListSvc', ['$http', function ($http) {

            $http.defaults.useXDomain = true;
            delete $http.defaults.headers.common['X-Requested-With']; 

            return {
                getItems : function(){
                    return $http.get(apiEndpoint + '/api/TodoList');
                },

                /* Get by ID, Put, and Delete methods not shown */

                postItem : function(item){
                    return $http.post(apiEndpoint + '/api/TodoList', item);
                }
            };
        }]);

### <a name="create-a-new-web-app-for-the-todolistangular-project"></a><span data-ttu-id="c3757-138">Создание нового веб-приложения для проекта ToDoListAngular</span><span class="sxs-lookup"><span data-stu-id="c3757-138">Create a new web app for the ToDoListAngular project</span></span>
<span data-ttu-id="c3757-139">Процедура создания веб-приложения службы приложений и развертывания в нем проекта похожа [на аналогичную процедуру для приложения API в первом руководстве этой серии](app-service-api-dotnet-get-started.md#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="c3757-139">The procedure to create a new App Service web app and deploy a project to it is similar to what you saw for [creating and deploying an API app in the first tutorial in this series](app-service-api-dotnet-get-started.md#createapiapp).</span></span> <span data-ttu-id="c3757-140">Разница только в том, что приложение относится к типу **Веб-приложение**, а не **Приложение API**.</span><span class="sxs-lookup"><span data-stu-id="c3757-140">The only difference is that the app type is **Web App** instead of **API App**.</span></span>  <span data-ttu-id="c3757-141">Снимки экрана диалоговых окон можно просмотреть, выполнив следующее.</span><span class="sxs-lookup"><span data-stu-id="c3757-141">For screen shots of the dialogs, see</span></span> 

1. <span data-ttu-id="c3757-142">В **обозревателе решений** щелкните правой кнопкой мыши проект ToDoListAngular и выберите пункт **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="c3757-142">In **Solution Explorer**, right-click the ToDoListAngular project, and then click **Publish**.</span></span>
2. <span data-ttu-id="c3757-143">В мастере **Публикация веб-сайта** на вкладке **Профиль** щелкните **Служба приложений Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="c3757-143">In the **Profile** tab of the **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="c3757-144">В диалоговом окне **Служба приложений** нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c3757-144">In the **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="c3757-145">На вкладке **Размещение** в диалоговом окне **Создание службы приложений** укажите **имя веб-приложения** (оно должно быть уникальным в домене *azurewebsites.net*).</span><span class="sxs-lookup"><span data-stu-id="c3757-145">In the **Hosting** tab of the **Create App Service** dialog box, enter a **Web App Name** that is unique in the *azurewebsites.net* domain.</span></span> 
5. <span data-ttu-id="c3757-146">В поле **Подписка** выберите подписку Azure, которую нужно использовать.</span><span class="sxs-lookup"><span data-stu-id="c3757-146">Choose the Azure **Subscription** you want to work with.</span></span>
6. <span data-ttu-id="c3757-147">В раскрывающемся списке **Группа ресурсов** выберите созданную ранее группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c3757-147">In the **Resource Group** drop-down list, choose the same resource group you created earlier.</span></span>
7. <span data-ttu-id="c3757-148">В раскрывающемся списке **План службы приложений** выберите созданный ранее план.</span><span class="sxs-lookup"><span data-stu-id="c3757-148">In the **App Service Plan** drop-down list, choose the same plan you created earlier.</span></span> 
8. <span data-ttu-id="c3757-149">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c3757-149">Click **Create**.</span></span>
   
    <span data-ttu-id="c3757-150">В Visual Studio создается веб-приложение и профиль публикации для него, а также отображается шаг **Подключение** мастера **веб-публикации**.</span><span class="sxs-lookup"><span data-stu-id="c3757-150">Visual Studio creates the web app, creates a publish profile for it, and displays the **Connection** step of the **Publish Web** wizard.</span></span>
   
    <span data-ttu-id="c3757-151">Пока не нажимайте кнопку **Опубликовать** .</span><span class="sxs-lookup"><span data-stu-id="c3757-151">Don't click **Publish** yet.</span></span> <span data-ttu-id="c3757-152">В следующем разделе вы настроите новое веб-приложение, чтобы вызвать приложение API среднего уровня, которое выполняется в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="c3757-152">In the following section, you configure the new web app to call the middle tier API app that is running in App Service.</span></span> 

### <a name="set-the-middle-tier-url-in-web-app-settings"></a><span data-ttu-id="c3757-153">Указание URL-адреса среднего уровня в параметрах веб-приложения</span><span class="sxs-lookup"><span data-stu-id="c3757-153">Set the middle tier URL in web app settings</span></span>
1. <span data-ttu-id="c3757-154">На [портале Azure](https://portal.azure.com/)откройте колонку **Веб-приложение** веб-приложения, созданного для размещения проекта ToDoListAngular (внешнее приложение).</span><span class="sxs-lookup"><span data-stu-id="c3757-154">Go to the [Azure portal](https://portal.azure.com/), and then navigate to the **Web App** blade for the web app that you created to host the TodoListAngular (front end) project.</span></span>
2. <span data-ttu-id="c3757-155">Щелкните элементы **Параметры > Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="c3757-155">Click **Settings > Application Settings**.</span></span>
3. <span data-ttu-id="c3757-156">В разделе **Параметры приложения** добавьте следующий ключ и значение:</span><span class="sxs-lookup"><span data-stu-id="c3757-156">In the **App settings** section, add the following key and value:</span></span>
   
   | <span data-ttu-id="c3757-157">Ключ</span><span class="sxs-lookup"><span data-stu-id="c3757-157">Key</span></span> | <span data-ttu-id="c3757-158">Значение</span><span class="sxs-lookup"><span data-stu-id="c3757-158">Value</span></span> | <span data-ttu-id="c3757-159">Пример</span><span class="sxs-lookup"><span data-stu-id="c3757-159">Example</span></span> |
   | --- | --- | --- |
   | <span data-ttu-id="c3757-160">toDoListAPIURL</span><span class="sxs-lookup"><span data-stu-id="c3757-160">toDoListAPIURL</span></span> |<span data-ttu-id="c3757-161">https://{имя_приложения_API_среднего_уровня}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="c3757-161">https://{your middle tier API app name}.azurewebsites.net</span></span> |<span data-ttu-id="c3757-162">https://todolistapi0121.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="c3757-162">https://todolistapi0121.azurewebsites.net</span></span> |
4. <span data-ttu-id="c3757-163">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c3757-163">Click **Save**.</span></span>
   
    <span data-ttu-id="c3757-164">Если код выполняется в среде Azure, это значение теперь будет переопределять URL-адрес локального узла, который находится в файле *Web.config* .</span><span class="sxs-lookup"><span data-stu-id="c3757-164">When the code runs in Azure, this value overrides the localhost URL that is in the *Web.config* file.</span></span> 
   
    <span data-ttu-id="c3757-165">Код, который получает значение параметра, находится в файле *index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="c3757-165">The code that gets the setting value is in *index.cshtml*:</span></span>
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    <span data-ttu-id="c3757-166">Код в файле *todoListSvc.js* использует этот параметр:</span><span class="sxs-lookup"><span data-stu-id="c3757-166">The code in *todoListSvc.js* uses the setting:</span></span>
   
        return {
            getItems : function(){
                return $http.get(apiEndpoint + '/api/TodoList');
            },
            getItem : function(id){
                return $http.get(apiEndpoint + '/api/TodoList/' + id);
            },
            postItem : function(item){
                return $http.post(apiEndpoint + '/api/TodoList', item);
            },
            putItem : function(item){
                return $http.put(apiEndpoint + '/api/TodoList/', item);
            },
            deleteItem : function(id){
                return $http({
                    method: 'DELETE',
                    url: apiEndpoint + '/api/TodoList/' + id
                });
            }
        };

### <a name="deploy-the-todolistangular-web-project-to-the-new-web-app"></a><span data-ttu-id="c3757-167">Развертывание веб-проекта ToDoListAngular в новом веб-приложении</span><span class="sxs-lookup"><span data-stu-id="c3757-167">Deploy the ToDoListAngular web project to the new web app</span></span>
* <span data-ttu-id="c3757-168">В Visual Studio на шаге **Подключение** мастера **веб-публикации** нажмите кнопку **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="c3757-168">In Visual Studio, in the **Connection** step of the **Publish Web** wizard, click **Publish**.</span></span>
  
   <span data-ttu-id="c3757-169">Visual Studio развернет проект ToDoListAngular в новое веб-приложение и откроет в браузере URL-адрес веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="c3757-169">Visual Studio deploys the ToDoListAngular project to the new web app and opens a browser to the URL of the web app.</span></span> 

### <a name="test-the-application-without-cors-enabled"></a><span data-ttu-id="c3757-170">Тестирование приложения с выключенным механизмом CORS</span><span class="sxs-lookup"><span data-stu-id="c3757-170">Test the application without CORS enabled</span></span>
1. <span data-ttu-id="c3757-171">В средствах разработчика браузера откройте окно консоли.</span><span class="sxs-lookup"><span data-stu-id="c3757-171">In your browser Developer Tools, open the Console window.</span></span>
2. <span data-ttu-id="c3757-172">В окне браузера с пользовательским интерфейсом AngularJS щелкните ссылку **To Do List** .</span><span class="sxs-lookup"><span data-stu-id="c3757-172">In the browser window that displays the AngularJS UI, click the **To Do List** link.</span></span>
   
    <span data-ttu-id="c3757-173">Код JavaScript попытается вызвать приложение API среднего уровня. Вызов завершится сбоем, так как внешнее приложение выполняется в домене, который отличается от домена внутреннего приложения.</span><span class="sxs-lookup"><span data-stu-id="c3757-173">The JavaScript code tries to call the middle tier API app, but the call fails because the front end is running in a different domain than the back end.</span></span> <span data-ttu-id="c3757-174">В окне браузера "Консоль средств разработчика" сообщение об ошибке отображается независимо от источника.</span><span class="sxs-lookup"><span data-stu-id="c3757-174">The browser's Developer Tools Console window shows a cross-origin error message.</span></span>
   
    ![Сообщение об ошибке CORS](./media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-the-middle-tier-api-app"></a><span data-ttu-id="c3757-176">Настройка CORS для приложения API среднего уровня</span><span class="sxs-lookup"><span data-stu-id="c3757-176">Configure CORS for the middle tier API app</span></span>
<span data-ttu-id="c3757-177">В этом разделе рассматривается настройка параметра CORS в Azure для приложения API среднего уровня ToDoListAP.</span><span class="sxs-lookup"><span data-stu-id="c3757-177">In this section, you configure the CORS setting in Azure for the middle tier ToDoListAPI API app.</span></span> <span data-ttu-id="c3757-178">Этот параметр позволит приложению API среднего уровня получать вызовы JavaScript из веб-приложения, созданного для проекта ToDoListAngular.</span><span class="sxs-lookup"><span data-stu-id="c3757-178">This setting will allow the middle tier API app to receive JavaScript calls from the web app that you created for the ToDoListAngular project.</span></span>

1. <span data-ttu-id="c3757-179">В браузере перейдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c3757-179">In a browser, go to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c3757-180">Щелкните **Службы приложений**, а затем выберите приложение API ToDoListAPI (среднего уровня).</span><span class="sxs-lookup"><span data-stu-id="c3757-180">Click **App Services**, and then click the ToDoListAPI (middle tier) API app.</span></span>
   
    ![Выбор приложения API на портале](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="c3757-182">В колонке **Параметры**, расположенной справа от колонки **Приложение API**, найдите раздел **API** и щелкните элемент **CORS**.</span><span class="sxs-lookup"><span data-stu-id="c3757-182">In the **Settings** blade that opens to the right of the **API app** blade, find the **API** section, and then click **CORS**.</span></span>
   
   ![Выбор CORS на портале](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="c3757-184">Введите в текстовое поле URL-адрес веб-приложения ToDoListAngular (внешнее приложение).</span><span class="sxs-lookup"><span data-stu-id="c3757-184">In the text box, enter the URL for the ToDoListAngular (front end) web app.</span></span> <span data-ttu-id="c3757-185">Например, если вы развернули проект ToDoListAngular в веб-приложении с именем todolistangular0121, разрешите вызовы с URL-адреса `https://todolistangular0121.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="c3757-185">For example, if you deployed the ToDoListAngular project to a web app named todolistangular0121, allow calls from the URL `https://todolistangular0121.azurewebsites.net`.</span></span>
   
   <span data-ttu-id="c3757-186">Вместо URL-адресов можно ввести символ звездочки (*). В таком случае будут приниматься вызовы из всех исходных доменов.</span><span class="sxs-lookup"><span data-stu-id="c3757-186">As an alternative, you can enter an asterisk (*) to specify that all origin domains are accepted.</span></span>
5. <span data-ttu-id="c3757-187">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c3757-187">Click **Save**.</span></span>
   
   ![Щелкните Сохранить](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="c3757-189">Когда вы нажмете кнопку **Сохранить**, приложение API начнет принимать вызовы JavaScript с указанного URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="c3757-189">After you click **Save**, the API app will accept JavaScript calls from the specified URL.</span></span> <span data-ttu-id="c3757-190">Из этого снимка экрана видно, что приложение API ToDoListAPI0223 будет принимать клиентские вызовы JavaScript из веб-приложения ToDoListAngular.</span><span class="sxs-lookup"><span data-stu-id="c3757-190">In this screen shot, the ToDoListAPI0223 API app will accept JavaScript client calls from the ToDoListAngular web app.</span></span>

### <a name="test-the-application-with-cors-enabled"></a><span data-ttu-id="c3757-191">Тестирование приложения с включенным механизмом CORS</span><span class="sxs-lookup"><span data-stu-id="c3757-191">Test the application with CORS enabled</span></span>
* <span data-ttu-id="c3757-192">Откройте в браузере URL-адрес HTTPS своего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="c3757-192">Open a browser to the HTTPS URL of the web app.</span></span> 
  
    <span data-ttu-id="c3757-193">На этот раз в приложении можно просматривать, добавлять, изменять и удалять элементы списка дел.</span><span class="sxs-lookup"><span data-stu-id="c3757-193">This time the application lets you view, add, edit, and delete to-do items.</span></span> 
  
    ![Страница To Do List в примере приложения](./media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a><span data-ttu-id="c3757-195">CORS службы приложений и CORS веб-API</span><span class="sxs-lookup"><span data-stu-id="c3757-195">App Service CORS versus Web API CORS</span></span>
<span data-ttu-id="c3757-196">В проекте веб-API можно установить пакет NuGet [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/). Так вы сможете указывать в коде домены, из которых API будет принимать вызовы JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c3757-196">In a Web API project, you can install the [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package to specify in code which domains your API will accept JavaScript calls from.</span></span>

<span data-ttu-id="c3757-197">Поддержка CORS веб-API более гибкая, чем поддержка CORS службы приложений.</span><span class="sxs-lookup"><span data-stu-id="c3757-197">Web API CORS support is more flexible than App Service CORS support.</span></span> <span data-ttu-id="c3757-198">Например, в коде можно указать различные принимаемые источники для различных методов действий, тогда как для CORS службы приложений указывается один набор принимаемых источников для всех методов приложения API.</span><span class="sxs-lookup"><span data-stu-id="c3757-198">For example, in code you can specify different accepted origins for different action methods, while for App Service CORS you specify one set of accepted origins for all of an API app's methods.</span></span>

> [!NOTE]
> <span data-ttu-id="c3757-199">Не пытайтесь использовать CORS веб-API и CORS службы приложений в одном приложении API.</span><span class="sxs-lookup"><span data-stu-id="c3757-199">Don't try to use both Web API CORS and App Service CORS in one API app.</span></span> <span data-ttu-id="c3757-200">В таком случае будет использоваться CORS службы приложений, а CORS веб-API — попросту игнорироваться.</span><span class="sxs-lookup"><span data-stu-id="c3757-200">App Service CORS will take precedence and Web API CORS will have no effect.</span></span> <span data-ttu-id="c3757-201">Например, если указать один исходный домен в службе приложений и все исходные домены в коде веб-API, приложение API Azure будет принимать вызовы только из домена, указанного в Azure.</span><span class="sxs-lookup"><span data-stu-id="c3757-201">For example, if you enable one origin domain in App Service, and enable all origin domains in your Web API code, your Azure API app will only accept calls from the domain you specified in Azure.</span></span>
> 
> 

### <a name="how-to-enable-cors-in-web-api-code"></a><span data-ttu-id="c3757-202">Включение CORS в коде веб-API</span><span class="sxs-lookup"><span data-stu-id="c3757-202">How to enable CORS in Web API code</span></span>
<span data-ttu-id="c3757-203">Ниже кратко описано, как включить поддержку CORS веб-API.</span><span class="sxs-lookup"><span data-stu-id="c3757-203">The following steps summarize the process for enabling Web API CORS support.</span></span> <span data-ttu-id="c3757-204">Дополнительные сведения см. в статье [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api) (Включение запросов независимо от источника в веб-API 2 ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="c3757-204">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span></span>

1. <span data-ttu-id="c3757-205">В проекте веб-API установите пакет NuGet [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) .</span><span class="sxs-lookup"><span data-stu-id="c3757-205">In a Web API project, install the [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package.</span></span>
2. <span data-ttu-id="c3757-206">Включите строку кода `config.EnableCors()` в метод **Register** класса **WebApiConfig**, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="c3757-206">Include a `config.EnableCors()` line of code in the **Register** method of the **WebApiConfig** class, as in the following example.</span></span> 
   
        public static class WebApiConfig
        {
            public static void Register(HttpConfiguration config)
            {
                // Web API configuration and services
   
                // The following line enables you to control CORS by using Web API code
                config.EnableCors();
   
                // Web API routes
                config.MapHttpAttributeRoutes();
   
                config.Routes.MapHttpRoute(
                    name: "DefaultApi",
                    routeTemplate: "api/{controller}/{id}",
                    defaults: new { id = RouteParameter.Optional }
                );
            }
        }
3. <span data-ttu-id="c3757-207">В контроллере веб-API добавьте инструкцию `using` для пространства имен `System.Web.Http.Cors`, а также добавьте атрибут `EnableCors` в класс контроллера или отдельные методы действий.</span><span class="sxs-lookup"><span data-stu-id="c3757-207">In your Web API controller, add a `using` statement for the `System.Web.Http.Cors` namespace, and add the `EnableCors` attribute to the controller class or to individual action methods.</span></span> <span data-ttu-id="c3757-208">В следующем примере поддержка CORS действует для всего контроллера.</span><span class="sxs-lookup"><span data-stu-id="c3757-208">In the following example, CORS support applies to the entire controller.</span></span>
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a><span data-ttu-id="c3757-209">Использование службы управления API с приложениями API</span><span class="sxs-lookup"><span data-stu-id="c3757-209">Using Azure API Management with API Apps</span></span>
<span data-ttu-id="c3757-210">Если вы используете службу управления API Azure с приложением API, настраивайте CORS в службе управления API, а не в приложении API.</span><span class="sxs-lookup"><span data-stu-id="c3757-210">If you use Azure API Management with an API app, configure CORS in API Management instead of in the API app.</span></span> <span data-ttu-id="c3757-211">Для получения дополнительных сведений см. следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="c3757-211">For more information, see the following resources:</span></span>

* <span data-ttu-id="c3757-212">[Azure API Management Overview](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/) (Видеообзор службы управления API Azure). Часть о CORS начинается с 12:10 мин.</span><span class="sxs-lookup"><span data-stu-id="c3757-212">[Azure API Management Overview (video: CORS starts at 12:10)](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/)</span></span>
* [<span data-ttu-id="c3757-213">API Management cross domain policies</span><span class="sxs-lookup"><span data-stu-id="c3757-213">API Management cross domain policies</span></span>](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a><span data-ttu-id="c3757-214">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="c3757-214">Troubleshooting</span></span>
<span data-ttu-id="c3757-215">Если в ходе выполнения инструкций этого руководства возникнут проблемы, можно воспользоваться рекомендациями по устранению неполадок ниже.</span><span class="sxs-lookup"><span data-stu-id="c3757-215">In case you run into a problem while going through this tutorial, here are some troubleshooting ideas.</span></span>

* <span data-ttu-id="c3757-216">Убедитесь, что используется последняя версия пакета [Azure SDK для .NET для Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="c3757-216">Make sure that you're using the latest version of the [Azure SDK for .NET for Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="c3757-217">Проверьте, что в параметре CORS указан протокол `https`, а также что для запуска внешнего веб-приложения используется протокол `https`.</span><span class="sxs-lookup"><span data-stu-id="c3757-217">Make sure that you entered `https` in the CORS setting, and make sure that you're using `https` to run the front-end web app.</span></span>
* <span data-ttu-id="c3757-218">Убедитесь, что вы ввели параметр CORS в приложении API среднего уровня, а не во внешнем веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="c3757-218">Make sure that you entered the CORS setting in the middle tier API app, not in the front-end web app.</span></span>
* <span data-ttu-id="c3757-219">Если вы настраиваете CORS в коде приложения и службе приложений Azure, учтите, что параметр CORS службы приложений переопределит все изменения в коде приложения.</span><span class="sxs-lookup"><span data-stu-id="c3757-219">If you're configuring CORS in both application code and Azure App Service, note that the App Service CORS setting will override whatever you're doing in application code.</span></span> 

<span data-ttu-id="c3757-220">Дополнительные сведения о функциях Visual Studio, которые упрощают устранение неполадок, см. в статье [Устранение неполадок веб-приложения в службе приложений Azure с помощью Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="c3757-220">To learn more about Visual Studio features that simplify troubleshooting, see [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3757-221">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c3757-221">Next steps</span></span>
<span data-ttu-id="c3757-222">В этой статье показано, как включить поддержку CORS в службе приложений, чтобы вызывать приложение API, выполняющееся в другом домене, с помощью клиентского кода JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c3757-222">In this article, you saw how to enable App Service CORS support so that client JavaScript code can call an API in a different domain.</span></span> <span data-ttu-id="c3757-223">Дополнительные сведения о приложениях API см. в руководствах по [введению в проверку подлинности службы приложений](../app-service/app-service-authentication-overview.md) и [проверке подлинности пользователя для приложений API](app-service-api-dotnet-user-principal-auth.md).</span><span class="sxs-lookup"><span data-stu-id="c3757-223">To learn more about API apps, read the [introduction to authentication in App Service](../app-service/app-service-authentication-overview.md), and then go to the [user authentication for API apps](app-service-api-dotnet-user-principal-auth.md) tutorial.</span></span>

