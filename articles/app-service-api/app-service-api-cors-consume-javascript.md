---
title: "поддерживает aaaCORS в службе приложений | Документы Microsoft"
description: "Узнайте, как поддерживать toouse CORS в службе приложений Azure в Azure."
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
ms.openlocfilehash: c229378b75840bc0f7b2eefc3df3031233f9b494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-api-app-from-javascript-using-cors"></a><span data-ttu-id="9bad3-103">Использование приложения API из JavaScript с помощью CORS</span><span class="sxs-lookup"><span data-stu-id="9bad3-103">Consume an API app from JavaScript using CORS</span></span>
<span data-ttu-id="9bad3-104">Службы приложений предлагает встроенную поддержку [между общий доступ к ресурсам источника (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), что позволяет клиентам toomake JavaScript кросс доменные вызывает tooAPIs, которые размещаются в приложениях API.</span><span class="sxs-lookup"><span data-stu-id="9bad3-104">App Service offers built-in support for [Cross Origin Resource Sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), which enables JavaScript clients toomake cross-domain calls tooAPIs that are hosted in API apps.</span></span> <span data-ttu-id="9bad3-105">Службы приложений можно настроить доступ CORS tooyour API без написания кода в ваш API.</span><span class="sxs-lookup"><span data-stu-id="9bad3-105">App Service lets you configure CORS access tooyour API without writing any code in your API.</span></span>

<span data-ttu-id="9bad3-106">Эта статья содержит два раздела.</span><span class="sxs-lookup"><span data-stu-id="9bad3-106">This article contains two sections:</span></span>

* <span data-ttu-id="9bad3-107">Hello [как tooconfigure CORS](#corsconfig) разделе объясняется, как общие tooconfigure CORS для приложения API, веб-приложения и мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="9bad3-107">hello [How tooconfigure CORS](#corsconfig) section explains in general how tooconfigure CORS for any API app, web app, or mobile app.</span></span> <span data-ttu-id="9bad3-108">Он применяется в равной степени tooall платформ, которые поддерживаются службой приложений, включая .NET, Node.js и Java.</span><span class="sxs-lookup"><span data-stu-id="9bad3-108">It applies equally tooall frameworks that are supported by App Service, including .NET, Node.js, and Java.</span></span> 
* <span data-ttu-id="9bad3-109">Начиная с hello [продолжением учебники Приступая к работе .NET hello](#tutorialstart) разделе hello статья является учебник, в котором демонстрируется с опорой на это требовалось в поддержка CORS [hello первого приложения API началу работы учебника ](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9bad3-109">Starting with hello [Continuing hello .NET getting-started tutorials](#tutorialstart) section, hello article is a tutorial that demonstrates CORS support by building on what you did in [hello first API Apps getting started tutorial](app-service-api-dotnet-get-started.md).</span></span> 

## <span data-ttu-id="9bad3-110"><a id="corsconfig"></a>Как tooconfigure CORS в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="9bad3-110"><a id="corsconfig"></a> How tooconfigure CORS in Azure App Service</span></span>
<span data-ttu-id="9bad3-111">CORS можно настроить в hello портал Azure или с помощью [диспетчера ресурсов Azure](../azure-resource-manager/resource-group-overview.md) средства.</span><span class="sxs-lookup"><span data-stu-id="9bad3-111">You can configure CORS in hello Azure portal or by using [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) tools.</span></span>

#### <a name="configure-cors-in-hello-azure-portal"></a><span data-ttu-id="9bad3-112">Настройка CORS в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="9bad3-112">Configure CORS in hello Azure portal</span></span>
1. <span data-ttu-id="9bad3-113">В браузере перейдите toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9bad3-113">In a browser go toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9bad3-114">Нажмите кнопку **службы приложений**и щелкните имя приложения API hello.</span><span class="sxs-lookup"><span data-stu-id="9bad3-114">Click **App Services**, and then click hello name of your API app.</span></span>
   
    ![Выбор приложения API на портале](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="9bad3-116">В hello **параметры** колонку, которая открывает toohello правой части hello **приложения API** колонки, найти hello **API** , а затем выберите **CORS**.</span><span class="sxs-lookup"><span data-stu-id="9bad3-116">In hello **Settings** blade that opens toohello right of hello **API app** blade, find hello **API** section, and then click **CORS**.</span></span>
   
   ![Выбор CORS в колонке параметров](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="9bad3-118">Введите в поле текста hello hello URL-адрес или желаемые tooallow toocome вызовов JavaScript из URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="9bad3-118">In hello text box enter hello URL or URLs that you want tooallow JavaScript calls toocome from.</span></span>

    <span data-ttu-id="9bad3-119">Например при развертывании вашего приложения tooa веб-приложения JavaScript с именем todolistangular, введите «https://todolistangular.azurewebsites.net».</span><span class="sxs-lookup"><span data-stu-id="9bad3-119">For example, if you deployed your JavaScript application tooa web app named todolistangular, enter "https://todolistangular.azurewebsites.net".</span></span> <span data-ttu-id="9bad3-120">В качестве альтернативы можно ввести toospecify звездочка (*), что принимаются все домены-источники.</span><span class="sxs-lookup"><span data-stu-id="9bad3-120">As an alternative, you can enter an asterisk (*) toospecify that all origin domains are accepted.</span></span>


1. <span data-ttu-id="9bad3-121">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9bad3-121">Click **Save**.</span></span>
   
   ![Щелкните Сохранить](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="9bad3-123">После нажатия кнопки **Сохранить**, приложение hello API JavaScript принимает вызовы из hello указанные URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="9bad3-123">After you click **Save**, hello API app will accept JavaScript calls from hello specified URLs.</span></span>

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a><span data-ttu-id="9bad3-124">Настройка CORS с помощью средств диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="9bad3-124">Configure CORS by using Azure Resource Manager tools</span></span>
<span data-ttu-id="9bad3-125">CORS можно также настроить для приложения API с помощью [шаблоны Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) в средства командной строки, таких как [Azure PowerShell](/powershell/azureps-cmdlets-docs) и hello [Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9bad3-125">You can also configure CORS for an API app by using [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) in command line tools such as [Azure PowerShell](/powershell/azureps-cmdlets-docs) and hello [Azure CLI](../cli-install-nodejs.md).</span></span> 

<span data-ttu-id="9bad3-126">Пример шаблона Azure Resource Manager, который задает для свойства CORS hello, откройте hello [azuredeploy.json файла в репозитории hello для этого учебника образца приложения](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="9bad3-126">For an example of an Azure Resource Manager template that sets hello CORS property, open hello [azuredeploy.json file in hello repository for this tutorial's sample application](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span></span> <span data-ttu-id="9bad3-127">Найдите раздел hello hello шаблона, который выглядит как следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="9bad3-127">Find hello section of hello template that looks like hello following example:</span></span>

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <span data-ttu-id="9bad3-128"><a id="tutorialstart"></a>Приступая к работе-учебник продолжение hello .NET</span><span class="sxs-lookup"><span data-stu-id="9bad3-128"><a id="tutorialstart"></a> Continuing hello .NET getting-started tutorial</span></span>
<span data-ttu-id="9bad3-129">Если вы следуете hello Node.js или Java Приступая к работе рядов для приложений API, у вас есть завершенного hello, начало работы рядов.</span><span class="sxs-lookup"><span data-stu-id="9bad3-129">If you are following hello Node.js or Java getting-started series for API apps, you have completed hello getting started series.</span></span> <span data-ttu-id="9bad3-130">Пропустить toohello [дальнейшие действия](#next-steps) статьи toofind предложения для дальнейшего изучения приложения API.</span><span class="sxs-lookup"><span data-stu-id="9bad3-130">Skip toohello [Next steps](#next-steps) section toofind suggestions for further learning about API Apps.</span></span>

<span data-ttu-id="9bad3-131">Hello оставшейся части этой статьи является продолжением hello ряда Приступая к работе .NET и предполагается, что вы успешно выполнили [первом учебнике hello](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9bad3-131">hello remainder of this article is a continuation of hello .NET getting-started series and assumes that you successfully completed [hello first tutorial](app-service-api-dotnet-get-started.md).</span></span>

## <a name="deploy-hello-todolistangular-project-tooa-new-web-app"></a><span data-ttu-id="9bad3-132">Развертывание hello ToDoListAngular проекта tooa новое веб-приложение</span><span class="sxs-lookup"><span data-stu-id="9bad3-132">Deploy hello ToDoListAngular project tooa new web app</span></span>
<span data-ttu-id="9bad3-133">В [первом учебнике hello](app-service-api-dotnet-get-started.md), вы создали приложение среднего уровня API и приложение API уровня данных.</span><span class="sxs-lookup"><span data-stu-id="9bad3-133">In [hello first tutorial](app-service-api-dotnet-get-started.md), you created a middle tier API app and a data tier API app.</span></span> <span data-ttu-id="9bad3-134">В этом учебнике создается одностраничного приложения (SPA) веб-приложения среднего уровня API приложение hello вызовов.</span><span class="sxs-lookup"><span data-stu-id="9bad3-134">In this tutorial you create a single-page application (SPA) web app that calls hello middle tier API app.</span></span> <span data-ttu-id="9bad3-135">Hello SPA toowork имеют tooenable CORS на среднем уровне hello приложения API.</span><span class="sxs-lookup"><span data-stu-id="9bad3-135">For hello SPA toowork you have tooenable CORS on hello middle tier API app.</span></span> 

<span data-ttu-id="9bad3-136">В hello [пример приложения ToDoList](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), hello ToDoListAngular проект является простой клиент AngularJS, который вызывает проекта веб-API ToDoListAPI hello среднего уровня.</span><span class="sxs-lookup"><span data-stu-id="9bad3-136">In hello [ToDoList sample application](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), hello ToDoListAngular project is a simple AngularJS client that calls hello middle tier ToDoListAPI Web API project.</span></span> <span data-ttu-id="9bad3-137">Здравствуйте, кода JavaScript в hello *app/scripts/todoListSvc.js* файла вызывает hello API с помощью поставщика AngularJS HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="9bad3-137">hello JavaScript code in hello *app/scripts/todoListSvc.js* file calls hello API by using hello AngularJS HTTP provider.</span></span> 

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

### <a name="create-a-new-web-app-for-hello-todolistangular-project"></a><span data-ttu-id="9bad3-138">Создать новое веб-приложение для проекта ToDoListAngular hello</span><span class="sxs-lookup"><span data-stu-id="9bad3-138">Create a new web app for hello ToDoListAngular project</span></span>
<span data-ttu-id="9bad3-139">Здравствуйте процедуры toocreate новое веб-приложение служб приложений и развернуть проект tooit — примерно toowhat можно было увидеть [Создание и развертывание приложения API в первом учебнике этой серии hello](app-service-api-dotnet-get-started.md#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="9bad3-139">hello procedure toocreate a new App Service web app and deploy a project tooit is similar toowhat you saw for [creating and deploying an API app in hello first tutorial in this series](app-service-api-dotnet-get-started.md#createapiapp).</span></span> <span data-ttu-id="9bad3-140">Hello только разница будет этот тип приложения hello является **веб-приложения** вместо **приложения API**.</span><span class="sxs-lookup"><span data-stu-id="9bad3-140">hello only difference is that hello app type is **Web App** instead of **API App**.</span></span>  <span data-ttu-id="9bad3-141">Снимки экрана приветствия диалоговых окон см.</span><span class="sxs-lookup"><span data-stu-id="9bad3-141">For screen shots of hello dialogs, see</span></span> 

1. <span data-ttu-id="9bad3-142">В **обозревателе решений**, щелкните правой кнопкой мыши проект ToDoListAngular hello и нажмите кнопку **публикации**.</span><span class="sxs-lookup"><span data-stu-id="9bad3-142">In **Solution Explorer**, right-click hello ToDoListAngular project, and then click **Publish**.</span></span>
2. <span data-ttu-id="9bad3-143">В hello **профиль** вкладка hello **веб-публикация** мастера, нажмите кнопку **службу приложений Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="9bad3-143">In hello **Profile** tab of hello **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="9bad3-144">В hello **службы приложений** диалоговое окно, нажмите кнопку **New**.</span><span class="sxs-lookup"><span data-stu-id="9bad3-144">In hello **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="9bad3-145">В hello **размещения** вкладка hello **Создание приложения службы** диалогового окна введите **имя веб-приложения** является уникальным в hello *azurewebsites.net* домен.</span><span class="sxs-lookup"><span data-stu-id="9bad3-145">In hello **Hosting** tab of hello **Create App Service** dialog box, enter a **Web App Name** that is unique in hello *azurewebsites.net* domain.</span></span> 
5. <span data-ttu-id="9bad3-146">Выберите hello Azure **подписки** требуется toowork с.</span><span class="sxs-lookup"><span data-stu-id="9bad3-146">Choose hello Azure **Subscription** you want toowork with.</span></span>
6. <span data-ttu-id="9bad3-147">В hello **группы ресурсов** раскрывающегося списка выберите hello одну группу ресурсов, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="9bad3-147">In hello **Resource Group** drop-down list, choose hello same resource group you created earlier.</span></span>
7. <span data-ttu-id="9bad3-148">В hello **план обслуживания приложений** раскрывающегося списка выберите hello одного плана, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="9bad3-148">In hello **App Service Plan** drop-down list, choose hello same plan you created earlier.</span></span> 
8. <span data-ttu-id="9bad3-149">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9bad3-149">Click **Create**.</span></span>
   
    <span data-ttu-id="9bad3-150">Visual Studio создает веб-приложения hello, создает профиль публикации для него и отображает hello **подключения** шага hello **веб-публикация** мастера.</span><span class="sxs-lookup"><span data-stu-id="9bad3-150">Visual Studio creates hello web app, creates a publish profile for it, and displays hello **Connection** step of hello **Publish Web** wizard.</span></span>
   
    <span data-ttu-id="9bad3-151">Пока не нажимайте кнопку **Опубликовать** .</span><span class="sxs-lookup"><span data-stu-id="9bad3-151">Don't click **Publish** yet.</span></span> <span data-ttu-id="9bad3-152">В следующем разделе hello настройте hello нового веб-приложения toocall hello среднего уровня API приложения, запущенные в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="9bad3-152">In hello following section, you configure hello new web app toocall hello middle tier API app that is running in App Service.</span></span> 

### <a name="set-hello-middle-tier-url-in-web-app-settings"></a><span data-ttu-id="9bad3-153">Задать URL-адрес для hello среднего уровня в параметры веб-приложения</span><span class="sxs-lookup"><span data-stu-id="9bad3-153">Set hello middle tier URL in web app settings</span></span>
1. <span data-ttu-id="9bad3-154">Go toohello [портал Azure](https://portal.azure.com/)и перейдите toohello **веб-приложение** колонке hello веб-приложения, созданного проекта TodoListAngular (интерфейса) toohost hello.</span><span class="sxs-lookup"><span data-stu-id="9bad3-154">Go toohello [Azure portal](https://portal.azure.com/), and then navigate toohello **Web App** blade for hello web app that you created toohost hello TodoListAngular (front end) project.</span></span>
2. <span data-ttu-id="9bad3-155">Щелкните элементы **Параметры > Параметры приложения**.</span><span class="sxs-lookup"><span data-stu-id="9bad3-155">Click **Settings > Application Settings**.</span></span>
3. <span data-ttu-id="9bad3-156">В hello **параметры приложения** добавьте следующие hello ключ и значение:</span><span class="sxs-lookup"><span data-stu-id="9bad3-156">In hello **App settings** section, add hello following key and value:</span></span>
   
   | <span data-ttu-id="9bad3-157">Ключ</span><span class="sxs-lookup"><span data-stu-id="9bad3-157">Key</span></span> | <span data-ttu-id="9bad3-158">Значение</span><span class="sxs-lookup"><span data-stu-id="9bad3-158">Value</span></span> | <span data-ttu-id="9bad3-159">Пример</span><span class="sxs-lookup"><span data-stu-id="9bad3-159">Example</span></span> |
   | --- | --- | --- |
   | <span data-ttu-id="9bad3-160">toDoListAPIURL</span><span class="sxs-lookup"><span data-stu-id="9bad3-160">toDoListAPIURL</span></span> |<span data-ttu-id="9bad3-161">https://{имя_приложения_API_среднего_уровня}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="9bad3-161">https://{your middle tier API app name}.azurewebsites.net</span></span> |<span data-ttu-id="9bad3-162">https://todolistapi0121.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="9bad3-162">https://todolistapi0121.azurewebsites.net</span></span> |
4. <span data-ttu-id="9bad3-163">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9bad3-163">Click **Save**.</span></span>
   
    <span data-ttu-id="9bad3-164">Когда hello код работает в Azure, это значение переопределяет hello localhost URL-адрес, в hello *Web.config* файла.</span><span class="sxs-lookup"><span data-stu-id="9bad3-164">When hello code runs in Azure, this value overrides hello localhost URL that is in hello *Web.config* file.</span></span> 
   
    <span data-ttu-id="9bad3-165">возможности Hello код, который возвращает значение параметра hello *index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="9bad3-165">hello code that gets hello setting value is in *index.cshtml*:</span></span>
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    <span data-ttu-id="9bad3-166">Здравствуйте, код в *todoListSvc.js* использует приветствия:</span><span class="sxs-lookup"><span data-stu-id="9bad3-166">hello code in *todoListSvc.js* uses hello setting:</span></span>
   
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

### <a name="deploy-hello-todolistangular-web-project-toohello-new-web-app"></a><span data-ttu-id="9bad3-167">Развертывание hello ToDoListAngular web проекта toohello новое веб-приложение</span><span class="sxs-lookup"><span data-stu-id="9bad3-167">Deploy hello ToDoListAngular web project toohello new web app</span></span>
* <span data-ttu-id="9bad3-168">В Visual Studio в hello **подключения** шага hello **веб-публикация** мастера, нажмите кнопку **публикации**.</span><span class="sxs-lookup"><span data-stu-id="9bad3-168">In Visual Studio, in hello **Connection** step of hello **Publish Web** wizard, click **Publish**.</span></span>
  
   <span data-ttu-id="9bad3-169">Visual Studio развертывает hello ToDoListAngular проекта toohello новое веб-приложение и открывает обозреватель toohello URL-адрес веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9bad3-169">Visual Studio deploys hello ToDoListAngular project toohello new web app and opens a browser toohello URL of hello web app.</span></span> 

### <a name="test-hello-application-without-cors-enabled"></a><span data-ttu-id="9bad3-170">Тестирование приложения hello без CORS включен</span><span class="sxs-lookup"><span data-stu-id="9bad3-170">Test hello application without CORS enabled</span></span>
1. <span data-ttu-id="9bad3-171">В браузере средств разработчика откройте окно консоли hello.</span><span class="sxs-lookup"><span data-stu-id="9bad3-171">In your browser Developer Tools, open hello Console window.</span></span>
2. <span data-ttu-id="9bad3-172">В окне браузера hello, которое отображает hello AngularJS пользовательского интерфейса, выберите hello **tooDo списка** ссылку.</span><span class="sxs-lookup"><span data-stu-id="9bad3-172">In hello browser window that displays hello AngularJS UI, click hello **tooDo List** link.</span></span>
   
    <span data-ttu-id="9bad3-173">код JavaScript Hello пытается toocall hello среднего уровня приложения API, но вызов hello завершается ошибкой, так как hello переднего плана выполняется в разных доменах hello обратно end.</span><span class="sxs-lookup"><span data-stu-id="9bad3-173">hello JavaScript code tries toocall hello middle tier API app, but hello call fails because hello front end is running in a different domain than hello back end.</span></span> <span data-ttu-id="9bad3-174">окно консоли средств разработчика браузера Hello показано сообщение об ошибке независимо от источника.</span><span class="sxs-lookup"><span data-stu-id="9bad3-174">hello browser's Developer Tools Console window shows a cross-origin error message.</span></span>
   
    ![Сообщение об ошибке CORS](./media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-hello-middle-tier-api-app"></a><span data-ttu-id="9bad3-176">Настройка CORS для hello среднего уровня приложения API</span><span class="sxs-lookup"><span data-stu-id="9bad3-176">Configure CORS for hello middle tier API app</span></span>
<span data-ttu-id="9bad3-177">В этом разделе настройкой параметра CORS hello в Azure для hello среднего уровня приложения ToDoListAPI API.</span><span class="sxs-lookup"><span data-stu-id="9bad3-177">In this section, you configure hello CORS setting in Azure for hello middle tier ToDoListAPI API app.</span></span> <span data-ttu-id="9bad3-178">Эта настройка дает возможность hello среднего уровня приложения tooreceive JavaScript вызовы API из веб-приложения hello, созданный для проекта ToDoListAngular hello.</span><span class="sxs-lookup"><span data-stu-id="9bad3-178">This setting will allow hello middle tier API app tooreceive JavaScript calls from hello web app that you created for hello ToDoListAngular project.</span></span>

1. <span data-ttu-id="9bad3-179">В браузере перейдите toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9bad3-179">In a browser, go toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9bad3-180">Нажмите кнопку **службы приложений**, а затем нажмите кнопку приложение hello API ToDoListAPI (средний уровень).</span><span class="sxs-lookup"><span data-stu-id="9bad3-180">Click **App Services**, and then click hello ToDoListAPI (middle tier) API app.</span></span>
   
    ![Выбор приложения API на портале](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="9bad3-182">В hello **параметры** колонку, которая открывает toohello правой части hello **приложения API** колонки, найти hello **API** , а затем выберите **CORS**.</span><span class="sxs-lookup"><span data-stu-id="9bad3-182">In hello **Settings** blade that opens toohello right of hello **API app** blade, find hello **API** section, and then click **CORS**.</span></span>
   
   ![Выбор CORS на портале](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="9bad3-184">В текстовом поле hello введите hello URL-адрес для веб-приложения hello ToDoListAngular (интерфейса).</span><span class="sxs-lookup"><span data-stu-id="9bad3-184">In hello text box, enter hello URL for hello ToDoListAngular (front end) web app.</span></span> <span data-ttu-id="9bad3-185">Например, если вы развернули hello ToDoListAngular проекта tooa веб-приложения с именем todolistangular0121, разрешить вызовы от hello URL-адрес `https://todolistangular0121.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="9bad3-185">For example, if you deployed hello ToDoListAngular project tooa web app named todolistangular0121, allow calls from hello URL `https://todolistangular0121.azurewebsites.net`.</span></span>
   
   <span data-ttu-id="9bad3-186">В качестве альтернативы можно ввести toospecify звездочка (*), что принимаются все домены-источники.</span><span class="sxs-lookup"><span data-stu-id="9bad3-186">As an alternative, you can enter an asterisk (*) toospecify that all origin domains are accepted.</span></span>
5. <span data-ttu-id="9bad3-187">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9bad3-187">Click **Save**.</span></span>
   
   ![Щелкните Сохранить](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="9bad3-189">После нажатия кнопки **Сохранить**, приложение hello API JavaScript принимает вызовы из hello указан URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="9bad3-189">After you click **Save**, hello API app will accept JavaScript calls from hello specified URL.</span></span> <span data-ttu-id="9bad3-190">На этом снимке экрана приложение hello ToDoListAPI0223 API будет принимать вызовы клиента JavaScript из веб-приложения hello ToDoListAngular.</span><span class="sxs-lookup"><span data-stu-id="9bad3-190">In this screen shot, hello ToDoListAPI0223 API app will accept JavaScript client calls from hello ToDoListAngular web app.</span></span>

### <a name="test-hello-application-with-cors-enabled"></a><span data-ttu-id="9bad3-191">Тестирование приложения hello с CORS включен</span><span class="sxs-lookup"><span data-stu-id="9bad3-191">Test hello application with CORS enabled</span></span>
* <span data-ttu-id="9bad3-192">Откройте браузер toohello HTTPS URL-адрес веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9bad3-192">Open a browser toohello HTTPS URL of hello web app.</span></span> 
  
    <span data-ttu-id="9bad3-193">Это приложение hello времени позволяет просматривать, добавлять, изменять и удалять элементы задачи.</span><span class="sxs-lookup"><span data-stu-id="9bad3-193">This time hello application lets you view, add, edit, and delete to-do items.</span></span> 
  
    ![Страница списка tooDo образца приложения](./media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a><span data-ttu-id="9bad3-195">CORS службы приложений и CORS веб-API</span><span class="sxs-lookup"><span data-stu-id="9bad3-195">App Service CORS versus Web API CORS</span></span>
<span data-ttu-id="9bad3-196">В проекте веб-API можно установить hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) toospecify пакета NuGet в какие домены, будет принимать API JavaScript вызовы из кода.</span><span class="sxs-lookup"><span data-stu-id="9bad3-196">In a Web API project, you can install hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package toospecify in code which domains your API will accept JavaScript calls from.</span></span>

<span data-ttu-id="9bad3-197">Поддержка CORS веб-API более гибкая, чем поддержка CORS службы приложений.</span><span class="sxs-lookup"><span data-stu-id="9bad3-197">Web API CORS support is more flexible than App Service CORS support.</span></span> <span data-ttu-id="9bad3-198">Например, в коде можно указать различные принимаемые источники для различных методов действий, тогда как для CORS службы приложений указывается один набор принимаемых источников для всех методов приложения API.</span><span class="sxs-lookup"><span data-stu-id="9bad3-198">For example, in code you can specify different accepted origins for different action methods, while for App Service CORS you specify one set of accepted origins for all of an API app's methods.</span></span>

> [!NOTE]
> <span data-ttu-id="9bad3-199">Старайтесь не toouse Web API CORS и CORS службы приложения в одно приложение API.</span><span class="sxs-lookup"><span data-stu-id="9bad3-199">Don't try toouse both Web API CORS and App Service CORS in one API app.</span></span> <span data-ttu-id="9bad3-200">В таком случае будет использоваться CORS службы приложений, а CORS веб-API — попросту игнорироваться.</span><span class="sxs-lookup"><span data-stu-id="9bad3-200">App Service CORS will take precedence and Web API CORS will have no effect.</span></span> <span data-ttu-id="9bad3-201">Например если включен один исходный домен в службе приложений и включить все домены-источники в коде веб-API, приложение Azure API только принимать вызовы от домена hello, указанного в Azure.</span><span class="sxs-lookup"><span data-stu-id="9bad3-201">For example, if you enable one origin domain in App Service, and enable all origin domains in your Web API code, your Azure API app will only accept calls from hello domain you specified in Azure.</span></span>
> 
> 

### <a name="how-tooenable-cors-in-web-api-code"></a><span data-ttu-id="9bad3-202">Как tooenable CORS в коде веб-API</span><span class="sxs-lookup"><span data-stu-id="9bad3-202">How tooenable CORS in Web API code</span></span>
<span data-ttu-id="9bad3-203">Hello следующие шаги описывают процесс hello включения поддержки Web API CORS.</span><span class="sxs-lookup"><span data-stu-id="9bad3-203">hello following steps summarize hello process for enabling Web API CORS support.</span></span> <span data-ttu-id="9bad3-204">Дополнительные сведения см. в статье [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api) (Включение запросов независимо от источника в веб-API 2 ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="9bad3-204">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span></span>

1. <span data-ttu-id="9bad3-205">В проекте веб-API, установить hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="9bad3-205">In a Web API project, install hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package.</span></span>
2. <span data-ttu-id="9bad3-206">Включить `config.EnableCors()` строку кода в hello **зарегистрировать** метод hello **WebApiConfig** класс как следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="9bad3-206">Include a `config.EnableCors()` line of code in hello **Register** method of hello **WebApiConfig** class, as in hello following example.</span></span> 
   
        public static class WebApiConfig
        {
            public static void Register(HttpConfiguration config)
            {
                // Web API configuration and services
   
                // hello following line enables you toocontrol CORS by using Web API code
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
3. <span data-ttu-id="9bad3-207">Добавьте в контроллер веб-API `using` инструкции для hello `System.Web.Http.Cors` пространства имен и добавить hello `EnableCors` атрибута toohello класса или tooindividual методы действий контроллера.</span><span class="sxs-lookup"><span data-stu-id="9bad3-207">In your Web API controller, add a `using` statement for hello `System.Web.Http.Cors` namespace, and add hello `EnableCors` attribute toohello controller class or tooindividual action methods.</span></span> <span data-ttu-id="9bad3-208">В следующем примере hello поддержка CORS применяется toohello всего контроллера.</span><span class="sxs-lookup"><span data-stu-id="9bad3-208">In hello following example, CORS support applies toohello entire controller.</span></span>
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a><span data-ttu-id="9bad3-209">Использование службы управления API с приложениями API</span><span class="sxs-lookup"><span data-stu-id="9bad3-209">Using Azure API Management with API Apps</span></span>
<span data-ttu-id="9bad3-210">При использовании API управления Azure с помощью приложения API настройки CORS управления API, а не в API приложение hello.</span><span class="sxs-lookup"><span data-stu-id="9bad3-210">If you use Azure API Management with an API app, configure CORS in API Management instead of in hello API app.</span></span> <span data-ttu-id="9bad3-211">Дополнительные сведения см. в разделе hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="9bad3-211">For more information, see hello following resources:</span></span>

* <span data-ttu-id="9bad3-212">[Azure API Management Overview](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/) (Видеообзор службы управления API Azure). Часть о CORS начинается с 12:10 мин.</span><span class="sxs-lookup"><span data-stu-id="9bad3-212">[Azure API Management Overview (video: CORS starts at 12:10)](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/)</span></span>
* [<span data-ttu-id="9bad3-213">API Management cross domain policies</span><span class="sxs-lookup"><span data-stu-id="9bad3-213">API Management cross domain policies</span></span>](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a><span data-ttu-id="9bad3-214">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="9bad3-214">Troubleshooting</span></span>
<span data-ttu-id="9bad3-215">Если в ходе выполнения инструкций этого руководства возникнут проблемы, можно воспользоваться рекомендациями по устранению неполадок ниже.</span><span class="sxs-lookup"><span data-stu-id="9bad3-215">In case you run into a problem while going through this tutorial, here are some troubleshooting ideas.</span></span>

* <span data-ttu-id="9bad3-216">Убедитесь, что вы используете последнюю версию hello hello [Azure SDK для .NET для Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="9bad3-216">Make sure that you're using hello latest version of hello [Azure SDK for .NET for Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="9bad3-217">Убедитесь, что вы ввели `https` в hello параметр CORS и убедитесь, что вы используете `https` toorun hello интерфейсный веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="9bad3-217">Make sure that you entered `https` in hello CORS setting, and make sure that you're using `https` toorun hello front-end web app.</span></span>
* <span data-ttu-id="9bad3-218">Убедитесь, что вы ввели приветствия CORS в API приложение hello среднего уровня, а не в интерфейсном веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9bad3-218">Make sure that you entered hello CORS setting in hello middle tier API app, not in hello front-end web app.</span></span>
* <span data-ttu-id="9bad3-219">Если вы настраиваете CORS в код приложения и службы приложений Azure, обратите внимание, что параметр CORS службы приложения hello перезаписывает все, что вы выполняете в коде приложения.</span><span class="sxs-lookup"><span data-stu-id="9bad3-219">If you're configuring CORS in both application code and Azure App Service, note that hello App Service CORS setting will override whatever you're doing in application code.</span></span> 

<span data-ttu-id="9bad3-220">в разделе toolearn Дополнительные сведения о функциональных возможностях Visual Studio, которые упрощают устранение неполадок, [Устранение неполадок Azure приложений служб приложений в Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="9bad3-220">toolearn more about Visual Studio features that simplify troubleshooting, see [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9bad3-221">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9bad3-221">Next steps</span></span>
<span data-ttu-id="9bad3-222">В этой статье показано, как поддерживают tooenable CORS службы приложения, чтобы клиентский код JavaScript может вызывать API в другом домене.</span><span class="sxs-lookup"><span data-stu-id="9bad3-222">In this article, you saw how tooenable App Service CORS support so that client JavaScript code can call an API in a different domain.</span></span> <span data-ttu-id="9bad3-223">Дополнительные сведения о приложениях API, чтение hello toolearn [tooauthentication введение в службе приложений](../app-service/app-service-authentication-overview.md), и затем перейти toohello [проверки подлинности пользователя для приложения API](app-service-api-dotnet-user-principal-auth.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="9bad3-223">toolearn more about API apps, read hello [introduction tooauthentication in App Service](../app-service/app-service-authentication-overview.md), and then go toohello [user authentication for API apps](app-service-api-dotnet-user-principal-auth.md) tutorial.</span></span>

