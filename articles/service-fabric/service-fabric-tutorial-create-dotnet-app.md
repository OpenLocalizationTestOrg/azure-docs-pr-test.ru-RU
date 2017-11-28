---
title: "приложения .NET для службы структуры aaaCreate | Документы Microsoft"
description: "Узнайте, как службы с отслеживанием состояния серверной части toocreate приложения с ASP.NET Core переднего плана и является надежным и развернуть кластер tooa приложения hello."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: bab331b9f8616c50a2794b6c048aace15579c8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a><span data-ttu-id="c7236-103">Создание и развертывание приложения с интерфейсной службой веб-API ASP.NET Core и серверной службой с отслеживанием состояния</span><span class="sxs-lookup"><span data-stu-id="c7236-103">Create and deploy an application with an ASP.NET Core Web API front-end service and a stateful back-end service</span></span>
<span data-ttu-id="c7236-104">Это руководство представляет первую часть цикла.</span><span class="sxs-lookup"><span data-stu-id="c7236-104">This tutorial is part one of a series.</span></span>  <span data-ttu-id="c7236-105">Вы узнаете, как toocreate приложения Azure Service Fabric с веб-API ASP.NET Core частотой завершения и toostore служб с отслеживанием состояния данных.</span><span class="sxs-lookup"><span data-stu-id="c7236-105">You will learn how toocreate an Azure Service Fabric application with an ASP.NET Core Web API front end and a stateful back-end service toostore your data.</span></span> <span data-ttu-id="c7236-106">После завершения имеется голосования приложение с ASP.NET Core веб-интерфейса, который сохраняет результаты голосования в с отслеживанием состояния внутренней службы в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="c7236-106">When you're finished, you have a voting application with an ASP.NET Core web front-end that saves voting results in a stateful back-end service in hello cluster.</span></span> <span data-ttu-id="c7236-107">Если вы не хотите toomanually создать голосования приложения hello, вы можете [Загрузка исходного кода hello](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) выполнить приложение hello и пропускать слишком[перемещайтесь голосования пример приложения hello](#walkthrough_anchor).</span><span class="sxs-lookup"><span data-stu-id="c7236-107">If you don't want toomanually create hello voting application, you can [download hello source code](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) for hello completed application and skip ahead too[Walk through hello voting sample application](#walkthrough_anchor).</span></span>

![Диаграмма приложения](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="c7236-109">В первой hello рядов, вы узнаете, как:</span><span class="sxs-lookup"><span data-stu-id="c7236-109">In part one of hello series, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c7236-110">Создание службы веб-API ASP.NET Core как надежной службы с отслеживанием состояния</span><span class="sxs-lookup"><span data-stu-id="c7236-110">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="c7236-111">Создание службы веб-приложения ASP.NET Core как службы без отслеживания состояния</span><span class="sxs-lookup"><span data-stu-id="c7236-111">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="c7236-112">Использовать toocommunicate hello обратного прокси-сервера со службой с отслеживанием состояния hello</span><span class="sxs-lookup"><span data-stu-id="c7236-112">Use hello reverse proxy toocommunicate with hello stateful service</span></span>

<span data-ttu-id="c7236-113">Из этого цикла руководств вы узнаете, как выполнять такие задачи:</span><span class="sxs-lookup"><span data-stu-id="c7236-113">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="c7236-114">Создание приложения .NET Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c7236-114">Build a .NET Service Fabric application</span></span>
> * [<span data-ttu-id="c7236-115">Развертывание кластера удаленного tooa приложения hello</span><span class="sxs-lookup"><span data-stu-id="c7236-115">Deploy hello application tooa remote cluster</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * <span data-ttu-id="c7236-116">[Настройка непрерывной интеграции и непрерывного развертывания с помощью Visual Studio Team Services](service-fabric-tutorial-deploy-app-with-cicd-vsts.md).</span><span class="sxs-lookup"><span data-stu-id="c7236-116">[Configure CI/CD using Visual Studio Team Services](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7236-117">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c7236-117">Prerequisites</span></span>
<span data-ttu-id="c7236-118">Перед началом работы с этим руководством выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c7236-118">Before you begin this tutorial:</span></span>
- <span data-ttu-id="c7236-119">Если у вас еще нет подписки Azure, создайте [бесплатную учетную запись](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="c7236-119">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="c7236-120">[Установка Visual Studio 2017 г](https://www.visualstudio.com/) и установить hello **разработки Azure** и **ASP.NET и веб-разработки** рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="c7236-120">[Install Visual Studio 2017](https://www.visualstudio.com/) and install hello **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="c7236-121">Установите пакет Service Fabric SDK hello</span><span class="sxs-lookup"><span data-stu-id="c7236-121">Install hello Service Fabric SDK</span></span>](service-fabric-get-started.md)

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a><span data-ttu-id="c7236-122">Создание службы веб-API ASP.NET как надежной службы</span><span class="sxs-lookup"><span data-stu-id="c7236-122">Create an ASP.NET Web API service as a reliable service</span></span>
<span data-ttu-id="c7236-123">Сначала необходимо создаете клиентский интерфейс приложения с помощью ASP.NET Core голосования hello hello web.</span><span class="sxs-lookup"><span data-stu-id="c7236-123">First, create hello web front-end of hello voting application using ASP.NET Core.</span></span> <span data-ttu-id="c7236-124">ASP.NET Core — это платформа разработки упрощенных кросс платформенных веб-, можно использовать toocreate современного пользовательского веб-интерфейса и веб-API.</span><span class="sxs-lookup"><span data-stu-id="c7236-124">ASP.NET Core is a lightweight, cross-platform web development framework that you can use toocreate modern web UI and web APIs.</span></span> <span data-ttu-id="c7236-125">tooget полное представление об интеграции ASP.NET Core Service Fabric, настоятельно рекомендуется ознакомиться hello [ASP.NET Core в Service Fabric надежного обмена](service-fabric-reliable-services-communication-aspnetcore.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="c7236-125">tooget a complete understanding of how ASP.NET Core integrates with Service Fabric, we strongly recommend reading through hello [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) article.</span></span> <span data-ttu-id="c7236-126">Теперь вы можете использовать этот учебник tooget быстро начать работу.</span><span class="sxs-lookup"><span data-stu-id="c7236-126">For now, you can follow this tutorial tooget started quickly.</span></span> <span data-ttu-id="c7236-127">toolearn Дополнительные сведения об ASP.NET Core разделе hello [базовую документацию по ASP.NET](https://docs.microsoft.com/aspnet/core/).</span><span class="sxs-lookup"><span data-stu-id="c7236-127">toolearn more about ASP.NET Core, see hello [ASP.NET Core Documentation](https://docs.microsoft.com/aspnet/core/).</span></span>

> [!NOTE]
> <span data-ttu-id="c7236-128">Этот учебник основывается на hello [ASP.NET Core tools для Visual Studio 2017 г](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span><span class="sxs-lookup"><span data-stu-id="c7236-128">This tutorial is based on hello [ASP.NET Core tools for Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span></span> <span data-ttu-id="c7236-129">средства .NET Core Hello для Visual Studio 2015 больше не обновляются.</span><span class="sxs-lookup"><span data-stu-id="c7236-129">hello .NET Core tools for Visual Studio 2015 are no longer being updated.</span></span>

1. <span data-ttu-id="c7236-130">Запустите Visual Studio от имени **администратора**.</span><span class="sxs-lookup"><span data-stu-id="c7236-130">Launch Visual Studio as an **administrator**.</span></span>

2. <span data-ttu-id="c7236-131">Выберите **Файл**->**Создать**->**Проект**, чтобы создать проект.</span><span class="sxs-lookup"><span data-stu-id="c7236-131">Create a project with **File**->**New**->**Project**</span></span>

3. <span data-ttu-id="c7236-132">В hello **новый проект** диалоговое окно, выберите **облака > приложение Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="c7236-132">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

4. <span data-ttu-id="c7236-133">Имя приложения hello **Голосование** и нажмите клавишу **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c7236-133">Name hello application **Voting** and press **OK**.</span></span>

   ![Диалоговое окно "Новый проект" в Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. <span data-ttu-id="c7236-135">На hello **новая служба Service Fabric** выберите **без сохранения состояния ASP.NET Core**и имя службы **VotingWeb**.</span><span class="sxs-lookup"><span data-stu-id="c7236-135">On hello **New Service Fabric Service** page, choose **Stateless ASP.NET Core**, and name your service **VotingWeb**.</span></span>
   
   ![Выбор веб-службы ASP.NET в диалоговое окно создания службы hello](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. <span data-ttu-id="c7236-137">Следующая страница Hello предоставляет набор ASP.NET Core шаблоны проектов.</span><span class="sxs-lookup"><span data-stu-id="c7236-137">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="c7236-138">В этом руководстве мы будем использовать **веб-приложение**.</span><span class="sxs-lookup"><span data-stu-id="c7236-138">For this tutorial, choose **Web Application**.</span></span> 
   
   ![Выбор типа проекта ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   <span data-ttu-id="c7236-140">Visual Studio создает приложение и проект службы и отображает их в обозревателе решений.</span><span class="sxs-lookup"><span data-stu-id="c7236-140">Visual Studio creates an application and a service project and displays them in Solution Explorer.</span></span>

   ![Обозреватель решений после создания приложения и службы веб-API ASP.NET Core]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-toohello-votingweb-service"></a><span data-ttu-id="c7236-142">Добавление AngularJS toohello VotingWeb службы</span><span class="sxs-lookup"><span data-stu-id="c7236-142">Add AngularJS toohello VotingWeb service</span></span>
<span data-ttu-id="c7236-143">Добавить [AngularJS](http://angularjs.org/) tooyour службы с помощью встроенных hello [Bower поддержки](/aspnet/core/client-side/bower).</span><span class="sxs-lookup"><span data-stu-id="c7236-143">Add [AngularJS](http://angularjs.org/) tooyour service using hello built-in [Bower support](/aspnet/core/client-side/bower).</span></span> <span data-ttu-id="c7236-144">Откройте файл *bower.json* и добавьте записи для компонентов Angular и Angular Bootstrap, а затем сохраните изменения.</span><span class="sxs-lookup"><span data-stu-id="c7236-144">Open *bower.json* and add entries for angular and angular-bootstrap, then save your changes.</span></span>

```json
{
  "name": "asp.net",
  "private": true,
  "dependencies": {
    "bootstrap": "3.3.7",
    "jquery": "2.2.0",
    "jquery-validation": "1.14.0",
    "jquery-validation-unobtrusive": "3.2.6",
    "angular": "v1.6.5",
    "angular-bootstrap": "v1.1.0"
  }
}
```
<span data-ttu-id="c7236-145">При сохранении hello *bower.json* файл, угловая устанавливается в своем проекте *wwwroot/lib* папки.</span><span class="sxs-lookup"><span data-stu-id="c7236-145">Upon saving hello *bower.json* file, Angular is installed in your project's *wwwroot/lib* folder.</span></span> <span data-ttu-id="c7236-146">Кроме того, перечисленные в hello *зависимости и Bower* папки.</span><span class="sxs-lookup"><span data-stu-id="c7236-146">Additionally, it is listed within hello *Dependencies/Bower* folder.</span></span>

### <a name="update-hello-sitejs-file"></a><span data-ttu-id="c7236-147">Обновить файл site.js hello</span><span class="sxs-lookup"><span data-stu-id="c7236-147">Update hello site.js file</span></span>
<span data-ttu-id="c7236-148">Откройте hello *wwwroot/js/site.js* файла.</span><span class="sxs-lookup"><span data-stu-id="c7236-148">Open hello *wwwroot/js/site.js* file.</span></span>  <span data-ttu-id="c7236-149">Замените его содержимое hello JavaScript, используемый hello домашней представления:</span><span class="sxs-lookup"><span data-stu-id="c7236-149">Replace its contents with hello JavaScript used by hello Home views:</span></span>

```javascript
var app = angular.module('VotingApp', ['ui.bootstrap']);
app.run(function () { });

app.controller('VotingAppController', ['$rootScope', '$scope', '$http', '$timeout', function ($rootScope, $scope, $http, $timeout) {

    $scope.refresh = function () {
        $http.get('api/Votes?c=' + new Date().getTime())
            .then(function (data, status) {
                $scope.votes = data;
            }, function (data, status) {
                $scope.votes = undefined;
            });
    };

    $scope.remove = function (item) {
        $http.delete('api/Votes/' + item)
            .then(function (data, status) {
                $scope.refresh();
            })
    };

    $scope.add = function (item) {
        var fd = new FormData();
        fd.append('item', item);
        $http.put('api/Votes/' + item, fd, {
            transformRequest: angular.identity,
            headers: { 'Content-Type': undefined }
        })
            .then(function (data, status) {
                $scope.refresh();
                $scope.item = undefined;
            })
    };
}]);
```

### <a name="update-hello-indexcshtml-file"></a><span data-ttu-id="c7236-150">Обновить файл Index.cshtml hello</span><span class="sxs-lookup"><span data-stu-id="c7236-150">Update hello Index.cshtml file</span></span>
<span data-ttu-id="c7236-151">Откройте hello *Views/Home/Index.cshtml* файла, определенного контроллера toohello Home hello представления.</span><span class="sxs-lookup"><span data-stu-id="c7236-151">Open hello *Views/Home/Index.cshtml* file, hello view specific toohello Home controller.</span></span>  <span data-ttu-id="c7236-152">Замените следующие hello его содержимое, а затем сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="c7236-152">Replace its contents with hello following, then save your changes.</span></span>

```html
@{
    ViewData["Title"] = "Service Fabric Voting Sample";
}

<div ng-controller="VotingAppController" ng-init="refresh()">
    <div class="container-fluid">
        <div class="row">
            <div class="col-xs-8 col-xs-offset-2 text-center">
                <h2>Service Fabric Voting Sample</h2>
            </div>
        </div>

        <div class="row">
            <div class="col-xs-8 col-xs-offset-2">
                <form class="col-xs-12 center-block">
                    <div class="col-xs-6 form-group">
                        <input id="txtAdd" type="text" class="form-control" placeholder="Add voting option" ng-model="item" />
                    </div>
                    <button id="btnAdd" class="btn btn-default" ng-click="add(item)">
                        <span class="glyphicon glyphicon-plus" aria-hidden="true"></span>
                        Add
                    </button>
                </form>
            </div>
        </div>

        <hr />

        <div class="row">
            <div class="col-xs-8 col-xs-offset-2">
                <div class="row">
                    <div class="col-xs-4">
                        Click toovote
                    </div>
                </div>
                <div class="row top-buffer" ng-repeat="vote in votes.data">
                    <div class="col-xs-8">
                        <button class="btn btn-success text-left btn-block" ng-click="add(vote.key)">
                            <span class="pull-left">
                                {{vote.key}}
                            </span>
                            <span class="badge pull-right">
                                {{vote.value}} Votes
                            </span>
                        </button>
                    </div>
                    <div class="col-xs-4">
                        <button class="btn btn-danger pull-right btn-block" ng-click="remove(vote.key)">
                            <span class="glyphicon glyphicon-remove" aria-hidden="true"></span>
                            Remove
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
```

### <a name="update-hello-layoutcshtml-file"></a><span data-ttu-id="c7236-153">Обновить файл _Layout.cshtml hello</span><span class="sxs-lookup"><span data-stu-id="c7236-153">Update hello _Layout.cshtml file</span></span>
<span data-ttu-id="c7236-154">Откройте hello *Views/Shared/_Layout.cshtml* файл, hello макет по умолчанию для приложения ASP.NET hello.</span><span class="sxs-lookup"><span data-stu-id="c7236-154">Open hello *Views/Shared/_Layout.cshtml* file, hello default layout for hello ASP.NET app.</span></span>  <span data-ttu-id="c7236-155">Замените следующие hello его содержимое, а затем сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="c7236-155">Replace its contents with hello following, then save your changes.</span></span>

```html
<!DOCTYPE html>
<html ng-app="VotingApp" xmlns:ng="http://angularjs.org">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>@ViewData["Title"]</title>

    <link href="~/lib/bootstrap/dist/css/bootstrap.min.css" rel="stylesheet" />
    <link href="~/css/site.css" rel="stylesheet" />

</head>
<body>
    <div class="container body-content">
        @RenderBody()
    </div>

    <script src="~/lib/jquery/dist/jquery.js"></script>
    <script src="~/lib/bootstrap/dist/js/bootstrap.js"></script>
    <script src="~/lib/angular/angular.js"></script>
    <script src="~/lib/angular-bootstrap/ui-bootstrap-tpls.js"></script>
    <script src="~/js/site.js"></script>

    @RenderSection("Scripts", required: false)
</body>
</html>
```

### <a name="update-hello-votingwebcs-file"></a><span data-ttu-id="c7236-156">Обновить файл VotingWeb.cs hello</span><span class="sxs-lookup"><span data-stu-id="c7236-156">Update hello VotingWeb.cs file</span></span>
<span data-ttu-id="c7236-157">Откройте hello *VotingWeb.cs* файл, который создает hello ASP.NET Core WebHost внутри hello без сохранения состояния службы с помощью hello WebListener веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="c7236-157">Open hello *VotingWeb.cs* file, which creates hello ASP.NET Core WebHost inside hello stateless service using hello WebListener web server.</span></span>  <span data-ttu-id="c7236-158">Добавить hello `using System.Net.Http;` директив toohello верхнюю часть файла hello.</span><span class="sxs-lookup"><span data-stu-id="c7236-158">Add hello `using System.Net.Http;` directive toohello top of hello file.</span></span>  <span data-ttu-id="c7236-159">Замените hello `CreateServiceInstanceListeners()` функции hello следующее, а затем сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="c7236-159">Replace hello `CreateServiceInstanceListeners()` function with hello following, then save your changes.</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
            {
                ServiceEventSource.Current.ServiceMessage(serviceContext, $"Starting WebListener on {url}");

                return new WebHostBuilder().UseWebListener()
                            .ConfigureServices(
                                services => services
                                    .AddSingleton<StatelessServiceContext>(serviceContext)
                                    .AddSingleton<HttpClient>())
                            .UseContentRoot(Directory.GetCurrentDirectory())
                            .UseStartup<Startup>()
                            .UseApplicationInsights()
                            .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                            .UseUrls(url)
                            .Build();
            }))
    };
}
```

### <a name="add-hello-votescontrollercs-file"></a><span data-ttu-id="c7236-160">Добавьте файл VotesController.cs hello</span><span class="sxs-lookup"><span data-stu-id="c7236-160">Add hello VotesController.cs file</span></span>
<span data-ttu-id="c7236-161">Добавьте контроллер, который определяет действия голосования.</span><span class="sxs-lookup"><span data-stu-id="c7236-161">Add a controller which defines voting actions.</span></span> <span data-ttu-id="c7236-162">Щелкните правой кнопкой мыши на hello **контроллеров** папку, выберите **Добавить -> новый элемент -> класс**.</span><span class="sxs-lookup"><span data-stu-id="c7236-162">Right-click on hello **Controllers** folder, then select **Add->New item->Class**.</span></span>  <span data-ttu-id="c7236-163">Имя файла hello «VotesController.cs» и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="c7236-163">Name hello file "VotesController.cs" and click **Add**.</span></span>  <span data-ttu-id="c7236-164">Замените содержимое файла hello hello ниже, а затем сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="c7236-164">Replace hello file contents with hello following, then save your changes.</span></span>  <span data-ttu-id="c7236-165">Далее в [VotesController.cs файл обновления hello](#updatevotecontroller_anchor), этот файл будет измененный tooread и записывать голосования данные из внутренней службе hello.</span><span class="sxs-lookup"><span data-stu-id="c7236-165">Later, in [Update hello VotesController.cs file](#updatevotecontroller_anchor), this file will be modified tooread and write voting data from hello back-end service.</span></span>  <span data-ttu-id="c7236-166">На данном этапе hello возвращает представление toohello статическую строку данных.</span><span class="sxs-lookup"><span data-stu-id="c7236-166">For now, hello controller returns static string data toohello view.</span></span>

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using System.Collections.Generic;
using Newtonsoft.Json;
using System.Text;
using System.Net.Http;
using System.Net.Http.Headers;

namespace VotingWeb.Controllers
{
    [Produces("application/json")]
    [Route("api/Votes")]
    public class VotesController : Controller
    {
        private readonly HttpClient httpClient;

        public VotesController(HttpClient httpClient)
        {
            this.httpClient = httpClient;
        }

        // GET: api/Votes
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            List<KeyValuePair<string, int>> votes= new List<KeyValuePair<string, int>>();
            votes.Add(new KeyValuePair<string, int>("Pizza", 3));
            votes.Add(new KeyValuePair<string, int>("Ice cream", 4));

            return Json(votes);
        }
     }
}
```



### <a name="deploy-and-run-hello-application-locally"></a><span data-ttu-id="c7236-167">Развертывание и запуск приложения hello локально</span><span class="sxs-lookup"><span data-stu-id="c7236-167">Deploy and run hello application locally</span></span>
<span data-ttu-id="c7236-168">Теперь можно пойти дальше и запустите приложение hello.</span><span class="sxs-lookup"><span data-stu-id="c7236-168">You can now go ahead and run hello application.</span></span> <span data-ttu-id="c7236-169">В Visual Studio нажмите клавишу `F5` toodeploy hello приложения для отладки.</span><span class="sxs-lookup"><span data-stu-id="c7236-169">In Visual Studio, press `F5` toodeploy hello application for debugging.</span></span> <span data-ttu-id="c7236-170">Если Visual Studio не была открыта ранее с правами **администратора**, `F5` завершается неудачно.</span><span class="sxs-lookup"><span data-stu-id="c7236-170">`F5` fails if you didn't previously open Visual Studio as **administrator**.</span></span>

> [!NOTE]
> <span data-ttu-id="c7236-171">Hello в первый раз запустить и развернуть hello приложения локально, Visual Studio создает локального кластера для отладки.</span><span class="sxs-lookup"><span data-stu-id="c7236-171">hello first time you run and deploy hello application locally, Visual Studio creates a local cluster for debugging.</span></span>  <span data-ttu-id="c7236-172">Создание кластера может занять некоторое время.</span><span class="sxs-lookup"><span data-stu-id="c7236-172">Cluster creation may take some time.</span></span> <span data-ttu-id="c7236-173">Состояние создания кластера Hello отображается в окне вывода Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="c7236-173">hello cluster creation status is displayed in hello Visual Studio output window.</span></span>

<span data-ttu-id="c7236-174">На этом этапе веб-приложение должно выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="c7236-174">At this point, your web app should look like this:</span></span>

![Интерфейсная часть ASP.NET Core](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

<span data-ttu-id="c7236-176">Отладка приложения hello toostop вернуться tooVisual Studio и нажать клавишу **Shift + F5**.</span><span class="sxs-lookup"><span data-stu-id="c7236-176">toostop debugging hello application, go back tooVisual Studio and press **Shift+F5**.</span></span>

## <a name="add-a-stateful-back-end-service-tooyour-application"></a><span data-ttu-id="c7236-177">Добавление приложения службы с отслеживанием состояния серверной части tooyour</span><span class="sxs-lookup"><span data-stu-id="c7236-177">Add a stateful back-end service tooyour application</span></span>
<span data-ttu-id="c7236-178">Теперь, когда у нас есть службу веб-API ASP.NET, выполняемым в нашем приложении, выполним и добавьте toostore службы с отслеживанием состояния надежные данные в приложении.</span><span class="sxs-lookup"><span data-stu-id="c7236-178">Now that we have an ASP.NET Web API service running in our application, let's go ahead and add a stateful reliable service toostore some data in our application.</span></span>

<span data-ttu-id="c7236-179">Service Fabric дает tooconsistently и надежно хранить данные непосредственно в службе с помощью надежного коллекций.</span><span class="sxs-lookup"><span data-stu-id="c7236-179">Service Fabric allows you tooconsistently and reliably store your data right inside your service by using reliable collections.</span></span> <span data-ttu-id="c7236-180">Надежные коллекций — это набор классов коллекций высокой доступности и надежности, которые будут знакомы tooanyone, который использовал C# коллекций.</span><span class="sxs-lookup"><span data-stu-id="c7236-180">Reliable collections are a set of highly available and reliable collection classes that are familiar tooanyone who has used C# collections.</span></span>

<span data-ttu-id="c7236-181">В этом руководстве вы создадите службу, которая хранит значение счетчика в надежной коллекции.</span><span class="sxs-lookup"><span data-stu-id="c7236-181">In this tutorial, you create a service which stores a counter value in a reliable collection.</span></span>

1. <span data-ttu-id="c7236-182">В обозревателе решений щелкните правой кнопкой мыши **службы** в проект приложения hello и выберите **Добавить > Новая служба Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="c7236-182">In Solution Explorer, right-click **Services** within hello application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![Добавление нового tooan существующего приложения службы](./media/service-fabric-tutorial-create-dotnet-app/vs-add-new-service.png)

2. <span data-ttu-id="c7236-184">В hello **новая служба Service Fabric** диалоговое окно, выберите **с отслеживанием состояния ASP.NET Core**и служба имен hello **VotingData** и нажмите клавишу **ОК**.</span><span class="sxs-lookup"><span data-stu-id="c7236-184">In hello **New Service Fabric Service** dialog, choose **Stateful ASP.NET Core**, and name hello service **VotingData** and press **OK**.</span></span>

    ![Диалоговое окно "Новая служба" в Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    <span data-ttu-id="c7236-186">После создания проекта службы в вашем приложении будут две службы.</span><span class="sxs-lookup"><span data-stu-id="c7236-186">Once your service project is created, you have two services in your application.</span></span> <span data-ttu-id="c7236-187">По мере toobuild приложения, можно добавить дополнительные службы в hello таким же образом.</span><span class="sxs-lookup"><span data-stu-id="c7236-187">As you continue toobuild your application, you can add more services in hello same way.</span></span> <span data-ttu-id="c7236-188">Каждая из этих служб может быть отдельно обновлена, в том числе до определенной версии.</span><span class="sxs-lookup"><span data-stu-id="c7236-188">Each can be independently versioned and upgraded.</span></span>

3. <span data-ttu-id="c7236-189">Следующая страница Hello предоставляет набор ASP.NET Core шаблоны проектов.</span><span class="sxs-lookup"><span data-stu-id="c7236-189">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="c7236-190">В этом руководстве мы будем использовать **веб-API**.</span><span class="sxs-lookup"><span data-stu-id="c7236-190">For this tutorial, choose **Web API**.</span></span>

    ![Выбор типа проекта ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    <span data-ttu-id="c7236-192">Visual Studio создаст проект службы и отобразит их в обозревателе решений.</span><span class="sxs-lookup"><span data-stu-id="c7236-192">Visual Studio creates a service project and displays them in Solution Explorer.</span></span>

    ![Обозреватель решений](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-hello-votedatacontrollercs-file"></a><span data-ttu-id="c7236-194">Добавьте файл VoteDataController.cs hello</span><span class="sxs-lookup"><span data-stu-id="c7236-194">Add hello VoteDataController.cs file</span></span>

<span data-ttu-id="c7236-195">В hello **VotingData** правой кнопкой мыши проект на hello **контроллеров** папку, затем выберите **Добавить -> создать элемента -> класс**.</span><span class="sxs-lookup"><span data-stu-id="c7236-195">In hello **VotingData** project right-click on hello **Controllers** folder, then select **Add->New item->Class**.</span></span> <span data-ttu-id="c7236-196">Имя файла hello «VoteDataController.cs» и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="c7236-196">Name hello file "VoteDataController.cs" and click **Add**.</span></span> <span data-ttu-id="c7236-197">Замените содержимое файла hello hello ниже, а затем сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="c7236-197">Replace hello file contents with hello following, then save your changes.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using Microsoft.ServiceFabric.Data;
using System.Threading;
using Microsoft.ServiceFabric.Data.Collections;

namespace VotingData.Controllers
{
    [Route("api/[controller]")]
    public class VoteDataController : Controller
    {
        private readonly IReliableStateManager stateManager;

        public VoteDataController(IReliableStateManager stateManager)
        {
            this.stateManager = stateManager;
        }

        // GET api/VoteData
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            var ct = new CancellationToken();

            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                var list = await votesDictionary.CreateEnumerableAsync(tx);

                var enumerator = list.GetAsyncEnumerator();

                var result = new List<KeyValuePair<string, int>>();

                while (await enumerator.MoveNextAsync(ct))
                {
                    result.Add(enumerator.Current);
                }

                return Json(result);
            }
        }

        // PUT api/VoteData/name
        [HttpPut("{name}")]
        public async Task<IActionResult> Put(string name)
        {
            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                await votesDictionary.AddOrUpdateAsync(tx, name, 1, (key, oldvalue) => oldvalue + 1);
                await tx.CommitAsync();
            }

            return new OkResult();
        }

        // DELETE api/VoteData/name
        [HttpDelete("{name}")]
        public async Task<IActionResult> Delete(string name)
        {
            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                if (await votesDictionary.ContainsKeyAsync(tx, name))
                {
                    await votesDictionary.TryRemoveAsync(tx, name);
                    await tx.CommitAsync();
                    return new OkResult();
                }
                else
                {
                    return new NotFoundResult();
                }
            }
        }
    }
}
```


## <a name="connect-hello-services"></a><span data-ttu-id="c7236-198">Подключение служб hello</span><span class="sxs-lookup"><span data-stu-id="c7236-198">Connect hello services</span></span>
<span data-ttu-id="c7236-199">В следующем шаге мы будет подключаться hello двух служб и hello интерфейсный веб-приложения получить набор голосования сведения из hello внутренней службы.</span><span class="sxs-lookup"><span data-stu-id="c7236-199">In this next step, we will connect hello two services and make hello front-end Web application get and set voting information from hello back-end service.</span></span>

<span data-ttu-id="c7236-200">Service Fabric позволяет пользователям самим определять способ взаимодействия со службами Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="c7236-200">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="c7236-201">В составе одного приложения одни службы могут быть доступны по протоколу TCP.</span><span class="sxs-lookup"><span data-stu-id="c7236-201">Within a single application, you might have services that are accessible via TCP.</span></span> <span data-ttu-id="c7236-202">Другие службы могут быть доступны через API REST HTTP, третьи — через веб-сокеты.</span><span class="sxs-lookup"><span data-stu-id="c7236-202">Other services that might be accessible via an HTTP REST API and still other services could be accessible via web sockets.</span></span> <span data-ttu-id="c7236-203">Основные сведения о доступные варианты hello, а также соотношение hello. в разделе [взаимодействия со службами](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="c7236-203">For background on hello options available and hello tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

<span data-ttu-id="c7236-204">В этом руководстве мы используем [веб-API ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md).</span><span class="sxs-lookup"><span data-stu-id="c7236-204">In this tutorial, we are using [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-hello-votescontrollercs-file"></a><span data-ttu-id="c7236-205">Обновить файл VotesController.cs hello</span><span class="sxs-lookup"><span data-stu-id="c7236-205">Update hello VotesController.cs file</span></span>
<span data-ttu-id="c7236-206">В hello **VotingWeb** проект, откройте hello *Controllers/VotesController.cs* файла.</span><span class="sxs-lookup"><span data-stu-id="c7236-206">In hello **VotingWeb** project, open hello *Controllers/VotesController.cs* file.</span></span>  <span data-ttu-id="c7236-207">Замените hello `VotesController` класса определения содержимого hello следующее, а затем сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="c7236-207">Replace hello `VotesController` class definition contents with hello following, then save your changes.</span></span>

```csharp
    public class VotesController : Controller
    {
        private readonly HttpClient httpClient;
        string serviceProxyUrl = "http://localhost:19081/Voting/VotingData/api/VoteData";
        string partitionKind = "Int64Range";
        string partitionKey = "0";

        public VotesController(HttpClient httpClient)
        {
            this.httpClient = httpClient;
        }

        // GET: api/Votes
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            IEnumerable<KeyValuePair<string, int>> votes;

            HttpResponseMessage response = await this.httpClient.GetAsync($"{serviceProxyUrl}?PartitionKind={partitionKind}&PartitionKey={partitionKey}");

            if (response.StatusCode != System.Net.HttpStatusCode.OK)
            {
                return this.StatusCode((int)response.StatusCode);
            }

            votes = JsonConvert.DeserializeObject<List<KeyValuePair<string, int>>>(await response.Content.ReadAsStringAsync());

            return Json(votes);
        }

        // PUT: api/Votes/name
        [HttpPut("{name}")]
        public async Task<IActionResult> Put(string name)
        {
            string payload = $"{{ 'name' : '{name}' }}";
            StringContent putContent = new StringContent(payload, Encoding.UTF8, "application/json");
            putContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");

            string proxyUrl = $"{serviceProxyUrl}/{name}?PartitionKind={partitionKind}&PartitionKey={partitionKey}";

            HttpResponseMessage response = await this.httpClient.PutAsync(proxyUrl, putContent);

            return new ContentResult()
            {
                StatusCode = (int)response.StatusCode,
                Content = await response.Content.ReadAsStringAsync()
            };
        }

        // DELETE: api/Votes/name
        [HttpDelete("{name}")]
        public async Task<IActionResult> Delete(string name)
        {
            HttpResponseMessage response = await this.httpClient.DeleteAsync($"{serviceProxyUrl}/{name}?PartitionKind={partitionKind}&PartitionKey={partitionKey}");

            if (response.StatusCode != System.Net.HttpStatusCode.OK)
            {
                return this.StatusCode((int)response.StatusCode);
            }

            return new OkResult();

        }
    }
```
<a id="walkthrough" name="walkthrough_anchor"></a>

## <a name="walk-through-hello-voting-sample-application"></a><span data-ttu-id="c7236-208">Перемещайтесь голосования пример приложения hello</span><span class="sxs-lookup"><span data-stu-id="c7236-208">Walk through hello voting sample application</span></span>
<span data-ttu-id="c7236-209">Hello голосования приложения состоит из двух служб.</span><span class="sxs-lookup"><span data-stu-id="c7236-209">hello voting application consists of two services:</span></span>
- <span data-ttu-id="c7236-210">Веб-интерфейса службы (VotingWeb) — ASP.NET Core веб-интерфейса службы, который будет служить hello веб-страницы и предоставляет доступ к веб-API-интерфейсы toocommunicate с серверной службы hello.</span><span class="sxs-lookup"><span data-stu-id="c7236-210">Web front-end service (VotingWeb)- An ASP.NET Core web front-end service, which serves hello web page and exposes web APIs toocommunicate with hello backend service.</span></span>
- <span data-ttu-id="c7236-211">Внутренняя служба (VotingData)-ASP.NET Core веб-служба предоставляет один голос hello toostore API приводит к надежным словарь сохраняются на диске.</span><span class="sxs-lookup"><span data-stu-id="c7236-211">Back-end service (VotingData)- An ASP.NET Core web service, which exposes an API toostore hello vote results in a reliable dictionary persisted on disk.</span></span>

![Диаграмма приложения](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="c7236-213">Когда голосовать в следующие hello приложения hello происходят события.</span><span class="sxs-lookup"><span data-stu-id="c7236-213">When you vote in hello application hello following events occur:</span></span>
1. <span data-ttu-id="c7236-214">JavaScript отправляет toohello веб-запроса API hello голос hello веб-интерфейса службы как запрос HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="c7236-214">A JavaScript sends hello vote request toohello web API in hello web front-end service as an HTTP PUT request.</span></span>

2. <span data-ttu-id="c7236-215">Hello клиентского веб-интерфейса службы использует toolocate прокси-сервера и пересылать запрос HTTP PUT toohello внутренней службы.</span><span class="sxs-lookup"><span data-stu-id="c7236-215">hello web front-end service uses a proxy toolocate and forward an HTTP PUT request toohello back-end service.</span></span>

3. <span data-ttu-id="c7236-216">Hello внутренняя служба принимает входящий запрос hello и хранилищ hello обновил результат в надежные словаря, который получает реплицированные toomultiple узлами в кластере hello и сохраняются на диске.</span><span class="sxs-lookup"><span data-stu-id="c7236-216">hello back-end service takes hello incoming request, and stores hello updated result in a reliable dictionary, which gets replicated toomultiple nodes within hello cluster and persisted on disk.</span></span> <span data-ttu-id="c7236-217">Все приложения hello данные хранятся в кластере hello, поэтому не требуется ни одной базы данных.</span><span class="sxs-lookup"><span data-stu-id="c7236-217">All hello application's data is stored in hello cluster, so no database is needed.</span></span>

## <a name="debug-in-visual-studio"></a><span data-ttu-id="c7236-218">Отладка в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c7236-218">Debug in Visual Studio</span></span>
<span data-ttu-id="c7236-219">При отладке приложения в Visual Studio вы используете локальный кластер разработки Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c7236-219">When debugging application in Visual Studio, you are using a local Service Fabric development cluster.</span></span> <span data-ttu-id="c7236-220">У вас есть параметр tooadjust hello отладки сценария tooyour качества.</span><span class="sxs-lookup"><span data-stu-id="c7236-220">You have hello option tooadjust your debugging experience tooyour scenario.</span></span> <span data-ttu-id="c7236-221">В этом приложении мы храним данные во внутренней службе с помощью надежного словаря.</span><span class="sxs-lookup"><span data-stu-id="c7236-221">In this application, we store data in our back-end service, using a reliable dictionary.</span></span> <span data-ttu-id="c7236-222">Visual Studio удаляет приложение hello по умолчанию, при остановке отладчика hello.</span><span class="sxs-lookup"><span data-stu-id="c7236-222">Visual Studio removes hello application per default when you stop hello debugger.</span></span> <span data-ttu-id="c7236-223">Удаление приложения hello вызывает hello данных в серверной части hello tooalso службы удаляется.</span><span class="sxs-lookup"><span data-stu-id="c7236-223">Removing hello application causes hello data in hello back-end service tooalso be removed.</span></span> <span data-ttu-id="c7236-224">toopersist hello данных между сеансами отладки, можно изменить hello **режим отладки приложения** как свойство hello **Голосование** проекта в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c7236-224">toopersist hello data between debugging sessions, you can change hello **Application Debug Mode** as a property on hello **Voting** project in Visual Studio.</span></span>

<span data-ttu-id="c7236-225">toolook, что происходит в коде hello завершения hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="c7236-225">toolook at what happens in hello code, complete hello following steps:</span></span>
1. <span data-ttu-id="c7236-226">Откройте hello **VotesController.cs** файла и задать точку останова в hello веб-API **поместить** метод (строка 47 -), можно выполнить поиск файла hello в hello обозревателя решений в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c7236-226">Open hello **VotesController.cs** file and set a breakpoint in hello web API's **Put** method (line 47) - You can search for hello file in hello Solution Explorer in Visual Studio.</span></span>

2. <span data-ttu-id="c7236-227">Откройте hello **VoteDataController.cs** файл и установите точку останова в этом веб-API **поместить** метод (строка 50).</span><span class="sxs-lookup"><span data-stu-id="c7236-227">Open hello **VoteDataController.cs** file and set a breakpoint in this web API's **Put** method (line 50).</span></span>

3. <span data-ttu-id="c7236-228">Вернитесь к предыдущему окну toohello браузера и нажмите кнопку голосования параметр или добавить новую голосования.</span><span class="sxs-lookup"><span data-stu-id="c7236-228">Go back toohello browser and click a voting option or add a new voting option.</span></span> <span data-ttu-id="c7236-229">Попадании hello первой точки останова в hello веб-интерфейса контроллер api.</span><span class="sxs-lookup"><span data-stu-id="c7236-229">You hit hello first breakpoint in hello web front-end's api controller.</span></span>
    
    1. <span data-ttu-id="c7236-230">Это где hello JavaScript в браузере hello отправляет контроллер запроса toohello web API в клиентской службы hello.</span><span class="sxs-lookup"><span data-stu-id="c7236-230">This is where hello JavaScript in hello browser sends a request toohello web API controller in hello front-end service.</span></span>
    
    ![Добавление интерфейсной службы Vote](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. <span data-ttu-id="c7236-232">Сначала мы создаем URL-адрес hello toohello ReverseProxy для наших служб **(1)**.</span><span class="sxs-lookup"><span data-stu-id="c7236-232">First we construct hello URL toohello ReverseProxy for our back-end service **(1)**.</span></span>
    3. <span data-ttu-id="c7236-233">Затем мы отправляем hello запроса HTTP PUT toohello ReverseProxy **(2)**.</span><span class="sxs-lookup"><span data-stu-id="c7236-233">Then we send hello HTTP PUT Request toohello ReverseProxy **(2)**.</span></span>
    4. <span data-ttu-id="c7236-234">Наконец hello мы возвращаем hello ответа от клиента toohello внутренней службе hello **(3)**.</span><span class="sxs-lookup"><span data-stu-id="c7236-234">Finally hello we return hello response from hello back-end service toohello client **(3)**.</span></span>

4. <span data-ttu-id="c7236-235">Нажмите клавишу **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="c7236-235">Press **F5** toocontinue</span></span>
    1. <span data-ttu-id="c7236-236">Теперь вы находитесь в точке останова hello в hello внутренней службы.</span><span class="sxs-lookup"><span data-stu-id="c7236-236">You are now at hello break point in hello back-end service.</span></span>
    
    ![Добавление внутренней службы Vote](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. <span data-ttu-id="c7236-238">В первую строку hello в методе hello **(1)** мы используем hello `StateManager` tooget или добавление надежного словаря, который называется `counts`.</span><span class="sxs-lookup"><span data-stu-id="c7236-238">In hello first line in hello method **(1)** we are using hello `StateManager` tooget or add a reliable dictionary called `counts`.</span></span>
    3. <span data-ttu-id="c7236-239">Все взаимодействие с надежным словарем осуществляется с помощью транзакций. Для создания транзакции используется инструкция using **(2)**.</span><span class="sxs-lookup"><span data-stu-id="c7236-239">All interactions with values in a reliable dictionary require a transaction, this using statement **(2)** creates that transaction.</span></span>
    4. <span data-ttu-id="c7236-240">В транзакции hello, мы затем измените значение hello hello соответствующего ключа для голосования параметр hello и фиксации hello операции **(3)**.</span><span class="sxs-lookup"><span data-stu-id="c7236-240">In hello transaction, we then update hello value of hello relevant key for hello voting option and commits hello operation **(3)**.</span></span> <span data-ttu-id="c7236-241">После фиксации hello методом hello данных обновляется в словаре hello и реплицируются tooother узлов в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="c7236-241">Once hello commit method returns, hello data is updated in hello dictionary and replicated tooother nodes in hello cluster.</span></span> <span data-ttu-id="c7236-242">Hello данные теперь безопасно хранятся в кластере hello и hello внутренней службы при сбое tooother узлов, по-прежнему возникают hello данные недоступны.</span><span class="sxs-lookup"><span data-stu-id="c7236-242">hello data is now safely stored in hello cluster, and hello back-end service can fail over tooother nodes, still having hello data available.</span></span>
5. <span data-ttu-id="c7236-243">Нажмите клавишу **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="c7236-243">Press **F5** toocontinue</span></span>

<span data-ttu-id="c7236-244">hello toostop сеанса, нажмите клавишу отладки **Shift + F5**.</span><span class="sxs-lookup"><span data-stu-id="c7236-244">toostop hello debugging session, press **Shift+F5**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c7236-245">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c7236-245">Next steps</span></span>
<span data-ttu-id="c7236-246">В этой части учебника hello вы узнали, как:</span><span class="sxs-lookup"><span data-stu-id="c7236-246">In this part of hello tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c7236-247">Создание службы веб-API ASP.NET Core как надежной службы с отслеживанием состояния</span><span class="sxs-lookup"><span data-stu-id="c7236-247">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="c7236-248">Создание службы веб-приложения ASP.NET Core как службы без отслеживания состояния</span><span class="sxs-lookup"><span data-stu-id="c7236-248">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="c7236-249">Использовать toocommunicate hello обратного прокси-сервера со службой с отслеживанием состояния hello</span><span class="sxs-lookup"><span data-stu-id="c7236-249">Use hello reverse proxy toocommunicate with hello stateful service</span></span>

<span data-ttu-id="c7236-250">Предварительное toohello Далее учебник.</span><span class="sxs-lookup"><span data-stu-id="c7236-250">Advance toohello next tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="c7236-251">Развертывание tooAzure приложения hello</span><span class="sxs-lookup"><span data-stu-id="c7236-251">Deploy hello application tooAzure</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
