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
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a>Создание и развертывание приложения с интерфейсной службой веб-API ASP.NET Core и серверной службой с отслеживанием состояния
Это руководство представляет первую часть цикла.  Вы узнаете, как toocreate приложения Azure Service Fabric с веб-API ASP.NET Core частотой завершения и toostore служб с отслеживанием состояния данных. После завершения имеется голосования приложение с ASP.NET Core веб-интерфейса, который сохраняет результаты голосования в с отслеживанием состояния внутренней службы в кластере hello. Если вы не хотите toomanually создать голосования приложения hello, вы можете [Загрузка исходного кода hello](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) выполнить приложение hello и пропускать слишком[перемещайтесь голосования пример приложения hello](#walkthrough_anchor).

![Диаграмма приложения](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

В первой hello рядов, вы узнаете, как:

> [!div class="checklist"]
> * Создание службы веб-API ASP.NET Core как надежной службы с отслеживанием состояния
> * Создание службы веб-приложения ASP.NET Core как службы без отслеживания состояния
> * Использовать toocommunicate hello обратного прокси-сервера со службой с отслеживанием состояния hello

Из этого цикла руководств вы узнаете, как выполнять такие задачи:
> [!div class="checklist"]
> * Создание приложения .NET Service Fabric.
> * [Развертывание кластера удаленного tooa приложения hello](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * [Настройка непрерывной интеграции и непрерывного развертывания с помощью Visual Studio Team Services](service-fabric-tutorial-deploy-app-with-cicd-vsts.md).

## <a name="prerequisites"></a>Предварительные требования
Перед началом работы с этим руководством выполните следующие действия:
- Если у вас еще нет подписки Azure, создайте [бесплатную учетную запись](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
- [Установка Visual Studio 2017 г](https://www.visualstudio.com/) и установить hello **разработки Azure** и **ASP.NET и веб-разработки** рабочих нагрузок.
- [Установите пакет Service Fabric SDK hello](service-fabric-get-started.md)

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a>Создание службы веб-API ASP.NET как надежной службы
Сначала необходимо создаете клиентский интерфейс приложения с помощью ASP.NET Core голосования hello hello web. ASP.NET Core — это платформа разработки упрощенных кросс платформенных веб-, можно использовать toocreate современного пользовательского веб-интерфейса и веб-API. tooget полное представление об интеграции ASP.NET Core Service Fabric, настоятельно рекомендуется ознакомиться hello [ASP.NET Core в Service Fabric надежного обмена](service-fabric-reliable-services-communication-aspnetcore.md) статьи. Теперь вы можете использовать этот учебник tooget быстро начать работу. toolearn Дополнительные сведения об ASP.NET Core разделе hello [базовую документацию по ASP.NET](https://docs.microsoft.com/aspnet/core/).

> [!NOTE]
> Этот учебник основывается на hello [ASP.NET Core tools для Visual Studio 2017 г](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc). средства .NET Core Hello для Visual Studio 2015 больше не обновляются.

1. Запустите Visual Studio от имени **администратора**.

2. Выберите **Файл**->**Создать**->**Проект**, чтобы создать проект.

3. В hello **новый проект** диалоговое окно, выберите **облака > приложение Service Fabric**.

4. Имя приложения hello **Голосование** и нажмите клавишу **ОК**.

   ![Диалоговое окно "Новый проект" в Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. На hello **новая служба Service Fabric** выберите **без сохранения состояния ASP.NET Core**и имя службы **VotingWeb**.
   
   ![Выбор веб-службы ASP.NET в диалоговое окно создания службы hello](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. Следующая страница Hello предоставляет набор ASP.NET Core шаблоны проектов. В этом руководстве мы будем использовать **веб-приложение**. 
   
   ![Выбор типа проекта ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   Visual Studio создает приложение и проект службы и отображает их в обозревателе решений.

   ![Обозреватель решений после создания приложения и службы веб-API ASP.NET Core]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-toohello-votingweb-service"></a>Добавление AngularJS toohello VotingWeb службы
Добавить [AngularJS](http://angularjs.org/) tooyour службы с помощью встроенных hello [Bower поддержки](/aspnet/core/client-side/bower). Откройте файл *bower.json* и добавьте записи для компонентов Angular и Angular Bootstrap, а затем сохраните изменения.

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
При сохранении hello *bower.json* файл, угловая устанавливается в своем проекте *wwwroot/lib* папки. Кроме того, перечисленные в hello *зависимости и Bower* папки.

### <a name="update-hello-sitejs-file"></a>Обновить файл site.js hello
Откройте hello *wwwroot/js/site.js* файла.  Замените его содержимое hello JavaScript, используемый hello домашней представления:

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

### <a name="update-hello-indexcshtml-file"></a>Обновить файл Index.cshtml hello
Откройте hello *Views/Home/Index.cshtml* файла, определенного контроллера toohello Home hello представления.  Замените следующие hello его содержимое, а затем сохранить изменения.

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

### <a name="update-hello-layoutcshtml-file"></a>Обновить файл _Layout.cshtml hello
Откройте hello *Views/Shared/_Layout.cshtml* файл, hello макет по умолчанию для приложения ASP.NET hello.  Замените следующие hello его содержимое, а затем сохранить изменения.

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

### <a name="update-hello-votingwebcs-file"></a>Обновить файл VotingWeb.cs hello
Откройте hello *VotingWeb.cs* файл, который создает hello ASP.NET Core WebHost внутри hello без сохранения состояния службы с помощью hello WebListener веб-сервера.  Добавить hello `using System.Net.Http;` директив toohello верхнюю часть файла hello.  Замените hello `CreateServiceInstanceListeners()` функции hello следующее, а затем сохранить изменения.

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

### <a name="add-hello-votescontrollercs-file"></a>Добавьте файл VotesController.cs hello
Добавьте контроллер, который определяет действия голосования. Щелкните правой кнопкой мыши на hello **контроллеров** папку, выберите **Добавить -> новый элемент -> класс**.  Имя файла hello «VotesController.cs» и нажмите кнопку **добавить**.  Замените содержимое файла hello hello ниже, а затем сохранить изменения.  Далее в [VotesController.cs файл обновления hello](#updatevotecontroller_anchor), этот файл будет измененный tooread и записывать голосования данные из внутренней службе hello.  На данном этапе hello возвращает представление toohello статическую строку данных.

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



### <a name="deploy-and-run-hello-application-locally"></a>Развертывание и запуск приложения hello локально
Теперь можно пойти дальше и запустите приложение hello. В Visual Studio нажмите клавишу `F5` toodeploy hello приложения для отладки. Если Visual Studio не была открыта ранее с правами **администратора**, `F5` завершается неудачно.

> [!NOTE]
> Hello в первый раз запустить и развернуть hello приложения локально, Visual Studio создает локального кластера для отладки.  Создание кластера может занять некоторое время. Состояние создания кластера Hello отображается в окне вывода Visual Studio hello.

На этом этапе веб-приложение должно выглядеть так:

![Интерфейсная часть ASP.NET Core](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

Отладка приложения hello toostop вернуться tooVisual Studio и нажать клавишу **Shift + F5**.

## <a name="add-a-stateful-back-end-service-tooyour-application"></a>Добавление приложения службы с отслеживанием состояния серверной части tooyour
Теперь, когда у нас есть службу веб-API ASP.NET, выполняемым в нашем приложении, выполним и добавьте toostore службы с отслеживанием состояния надежные данные в приложении.

Service Fabric дает tooconsistently и надежно хранить данные непосредственно в службе с помощью надежного коллекций. Надежные коллекций — это набор классов коллекций высокой доступности и надежности, которые будут знакомы tooanyone, который использовал C# коллекций.

В этом руководстве вы создадите службу, которая хранит значение счетчика в надежной коллекции.

1. В обозревателе решений щелкните правой кнопкой мыши **службы** в проект приложения hello и выберите **Добавить > Новая служба Service Fabric**.
   
    ![Добавление нового tooan существующего приложения службы](./media/service-fabric-tutorial-create-dotnet-app/vs-add-new-service.png)

2. В hello **новая служба Service Fabric** диалоговое окно, выберите **с отслеживанием состояния ASP.NET Core**и служба имен hello **VotingData** и нажмите клавишу **ОК**.

    ![Диалоговое окно "Новая служба" в Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    После создания проекта службы в вашем приложении будут две службы. По мере toobuild приложения, можно добавить дополнительные службы в hello таким же образом. Каждая из этих служб может быть отдельно обновлена, в том числе до определенной версии.

3. Следующая страница Hello предоставляет набор ASP.NET Core шаблоны проектов. В этом руководстве мы будем использовать **веб-API**.

    ![Выбор типа проекта ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    Visual Studio создаст проект службы и отобразит их в обозревателе решений.

    ![Обозреватель решений](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-hello-votedatacontrollercs-file"></a>Добавьте файл VoteDataController.cs hello

В hello **VotingData** правой кнопкой мыши проект на hello **контроллеров** папку, затем выберите **Добавить -> создать элемента -> класс**. Имя файла hello «VoteDataController.cs» и нажмите кнопку **добавить**. Замените содержимое файла hello hello ниже, а затем сохранить изменения.

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


## <a name="connect-hello-services"></a>Подключение служб hello
В следующем шаге мы будет подключаться hello двух служб и hello интерфейсный веб-приложения получить набор голосования сведения из hello внутренней службы.

Service Fabric позволяет пользователям самим определять способ взаимодействия со службами Reliable Services. В составе одного приложения одни службы могут быть доступны по протоколу TCP. Другие службы могут быть доступны через API REST HTTP, третьи — через веб-сокеты. Основные сведения о доступные варианты hello, а также соотношение hello. в разделе [взаимодействия со службами](service-fabric-connect-and-communicate-with-services.md).

В этом руководстве мы используем [веб-API ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md).

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-hello-votescontrollercs-file"></a>Обновить файл VotesController.cs hello
В hello **VotingWeb** проект, откройте hello *Controllers/VotesController.cs* файла.  Замените hello `VotesController` класса определения содержимого hello следующее, а затем сохранить изменения.

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

## <a name="walk-through-hello-voting-sample-application"></a>Перемещайтесь голосования пример приложения hello
Hello голосования приложения состоит из двух служб.
- Веб-интерфейса службы (VotingWeb) — ASP.NET Core веб-интерфейса службы, который будет служить hello веб-страницы и предоставляет доступ к веб-API-интерфейсы toocommunicate с серверной службы hello.
- Внутренняя служба (VotingData)-ASP.NET Core веб-служба предоставляет один голос hello toostore API приводит к надежным словарь сохраняются на диске.

![Диаграмма приложения](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

Когда голосовать в следующие hello приложения hello происходят события.
1. JavaScript отправляет toohello веб-запроса API hello голос hello веб-интерфейса службы как запрос HTTP PUT.

2. Hello клиентского веб-интерфейса службы использует toolocate прокси-сервера и пересылать запрос HTTP PUT toohello внутренней службы.

3. Hello внутренняя служба принимает входящий запрос hello и хранилищ hello обновил результат в надежные словаря, который получает реплицированные toomultiple узлами в кластере hello и сохраняются на диске. Все приложения hello данные хранятся в кластере hello, поэтому не требуется ни одной базы данных.

## <a name="debug-in-visual-studio"></a>Отладка в Visual Studio
При отладке приложения в Visual Studio вы используете локальный кластер разработки Service Fabric. У вас есть параметр tooadjust hello отладки сценария tooyour качества. В этом приложении мы храним данные во внутренней службе с помощью надежного словаря. Visual Studio удаляет приложение hello по умолчанию, при остановке отладчика hello. Удаление приложения hello вызывает hello данных в серверной части hello tooalso службы удаляется. toopersist hello данных между сеансами отладки, можно изменить hello **режим отладки приложения** как свойство hello **Голосование** проекта в Visual Studio.

toolook, что происходит в коде hello завершения hello, следующие шаги:
1. Откройте hello **VotesController.cs** файла и задать точку останова в hello веб-API **поместить** метод (строка 47 -), можно выполнить поиск файла hello в hello обозревателя решений в Visual Studio.

2. Откройте hello **VoteDataController.cs** файл и установите точку останова в этом веб-API **поместить** метод (строка 50).

3. Вернитесь к предыдущему окну toohello браузера и нажмите кнопку голосования параметр или добавить новую голосования. Попадании hello первой точки останова в hello веб-интерфейса контроллер api.
    
    1. Это где hello JavaScript в браузере hello отправляет контроллер запроса toohello web API в клиентской службы hello.
    
    ![Добавление интерфейсной службы Vote](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. Сначала мы создаем URL-адрес hello toohello ReverseProxy для наших служб **(1)**.
    3. Затем мы отправляем hello запроса HTTP PUT toohello ReverseProxy **(2)**.
    4. Наконец hello мы возвращаем hello ответа от клиента toohello внутренней службе hello **(3)**.

4. Нажмите клавишу **F5** toocontinue
    1. Теперь вы находитесь в точке останова hello в hello внутренней службы.
    
    ![Добавление внутренней службы Vote](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. В первую строку hello в методе hello **(1)** мы используем hello `StateManager` tooget или добавление надежного словаря, который называется `counts`.
    3. Все взаимодействие с надежным словарем осуществляется с помощью транзакций. Для создания транзакции используется инструкция using **(2)**.
    4. В транзакции hello, мы затем измените значение hello hello соответствующего ключа для голосования параметр hello и фиксации hello операции **(3)**. После фиксации hello методом hello данных обновляется в словаре hello и реплицируются tooother узлов в кластере hello. Hello данные теперь безопасно хранятся в кластере hello и hello внутренней службы при сбое tooother узлов, по-прежнему возникают hello данные недоступны.
5. Нажмите клавишу **F5** toocontinue

hello toostop сеанса, нажмите клавишу отладки **Shift + F5**.


## <a name="next-steps"></a>Дальнейшие действия
В этой части учебника hello вы узнали, как:

> [!div class="checklist"]
> * Создание службы веб-API ASP.NET Core как надежной службы с отслеживанием состояния
> * Создание службы веб-приложения ASP.NET Core как службы без отслеживания состояния
> * Использовать toocommunicate hello обратного прокси-сервера со службой с отслеживанием состояния hello

Предварительное toohello Далее учебник.
> [!div class="nextstepaction"]
> [Развертывание tooAzure приложения hello](service-fabric-tutorial-deploy-app-to-party-cluster.md)
