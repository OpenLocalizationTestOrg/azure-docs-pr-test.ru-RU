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
# <a name="consume-an-api-app-from-javascript-using-cors"></a>Использование приложения API из JavaScript с помощью CORS
Службы приложений предлагает встроенную поддержку [между общий доступ к ресурсам источника (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), что позволяет клиентам toomake JavaScript кросс доменные вызывает tooAPIs, которые размещаются в приложениях API. Службы приложений можно настроить доступ CORS tooyour API без написания кода в ваш API.

Эта статья содержит два раздела.

* Hello [как tooconfigure CORS](#corsconfig) разделе объясняется, как общие tooconfigure CORS для приложения API, веб-приложения и мобильного приложения. Он применяется в равной степени tooall платформ, которые поддерживаются службой приложений, включая .NET, Node.js и Java. 
* Начиная с hello [продолжением учебники Приступая к работе .NET hello](#tutorialstart) разделе hello статья является учебник, в котором демонстрируется с опорой на это требовалось в поддержка CORS [hello первого приложения API началу работы учебника ](app-service-api-dotnet-get-started.md). 

## <a id="corsconfig"></a>Как tooconfigure CORS в службе приложений Azure
CORS можно настроить в hello портал Azure или с помощью [диспетчера ресурсов Azure](../azure-resource-manager/resource-group-overview.md) средства.

#### <a name="configure-cors-in-hello-azure-portal"></a>Настройка CORS в hello портал Azure
1. В браузере перейдите toohello [портал Azure](https://portal.azure.com/).
2. Нажмите кнопку **службы приложений**и щелкните имя приложения API hello.
   
    ![Выбор приложения API на портале](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. В hello **параметры** колонку, которая открывает toohello правой части hello **приложения API** колонки, найти hello **API** , а затем выберите **CORS**.
   
   ![Выбор CORS в колонке параметров](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. Введите в поле текста hello hello URL-адрес или желаемые tooallow toocome вызовов JavaScript из URL-адреса.

    Например при развертывании вашего приложения tooa веб-приложения JavaScript с именем todolistangular, введите «https://todolistangular.azurewebsites.net». В качестве альтернативы можно ввести toospecify звездочка (*), что принимаются все домены-источники.


1. Щелкните **Сохранить**.
   
   ![Щелкните Сохранить](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   После нажатия кнопки **Сохранить**, приложение hello API JavaScript принимает вызовы из hello указанные URL-адреса.

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a>Настройка CORS с помощью средств диспетчера ресурсов Azure
CORS можно также настроить для приложения API с помощью [шаблоны Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) в средства командной строки, таких как [Azure PowerShell](/powershell/azureps-cmdlets-docs) и hello [Azure CLI](../cli-install-nodejs.md). 

Пример шаблона Azure Resource Manager, который задает для свойства CORS hello, откройте hello [azuredeploy.json файла в репозитории hello для этого учебника образца приложения](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json). Найдите раздел hello hello шаблона, который выглядит как следующий пример hello.

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <a id="tutorialstart"></a>Приступая к работе-учебник продолжение hello .NET
Если вы следуете hello Node.js или Java Приступая к работе рядов для приложений API, у вас есть завершенного hello, начало работы рядов. Пропустить toohello [дальнейшие действия](#next-steps) статьи toofind предложения для дальнейшего изучения приложения API.

Hello оставшейся части этой статьи является продолжением hello ряда Приступая к работе .NET и предполагается, что вы успешно выполнили [первом учебнике hello](app-service-api-dotnet-get-started.md).

## <a name="deploy-hello-todolistangular-project-tooa-new-web-app"></a>Развертывание hello ToDoListAngular проекта tooa новое веб-приложение
В [первом учебнике hello](app-service-api-dotnet-get-started.md), вы создали приложение среднего уровня API и приложение API уровня данных. В этом учебнике создается одностраничного приложения (SPA) веб-приложения среднего уровня API приложение hello вызовов. Hello SPA toowork имеют tooenable CORS на среднем уровне hello приложения API. 

В hello [пример приложения ToDoList](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), hello ToDoListAngular проект является простой клиент AngularJS, который вызывает проекта веб-API ToDoListAPI hello среднего уровня. Здравствуйте, кода JavaScript в hello *app/scripts/todoListSvc.js* файла вызывает hello API с помощью поставщика AngularJS HTTP hello. 

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

### <a name="create-a-new-web-app-for-hello-todolistangular-project"></a>Создать новое веб-приложение для проекта ToDoListAngular hello
Здравствуйте процедуры toocreate новое веб-приложение служб приложений и развернуть проект tooit — примерно toowhat можно было увидеть [Создание и развертывание приложения API в первом учебнике этой серии hello](app-service-api-dotnet-get-started.md#createapiapp). Hello только разница будет этот тип приложения hello является **веб-приложения** вместо **приложения API**.  Снимки экрана приветствия диалоговых окон см. 

1. В **обозревателе решений**, щелкните правой кнопкой мыши проект ToDoListAngular hello и нажмите кнопку **публикации**.
2. В hello **профиль** вкладка hello **веб-публикация** мастера, нажмите кнопку **службу приложений Microsoft Azure**.
3. В hello **службы приложений** диалоговое окно, нажмите кнопку **New**.
4. В hello **размещения** вкладка hello **Создание приложения службы** диалогового окна введите **имя веб-приложения** является уникальным в hello *azurewebsites.net* домен. 
5. Выберите hello Azure **подписки** требуется toowork с.
6. В hello **группы ресурсов** раскрывающегося списка выберите hello одну группу ресурсов, созданного ранее.
7. В hello **план обслуживания приложений** раскрывающегося списка выберите hello одного плана, созданного ранее. 
8. Щелкните **Создать**.
   
    Visual Studio создает веб-приложения hello, создает профиль публикации для него и отображает hello **подключения** шага hello **веб-публикация** мастера.
   
    Пока не нажимайте кнопку **Опубликовать** . В следующем разделе hello настройте hello нового веб-приложения toocall hello среднего уровня API приложения, запущенные в службе приложений. 

### <a name="set-hello-middle-tier-url-in-web-app-settings"></a>Задать URL-адрес для hello среднего уровня в параметры веб-приложения
1. Go toohello [портал Azure](https://portal.azure.com/)и перейдите toohello **веб-приложение** колонке hello веб-приложения, созданного проекта TodoListAngular (интерфейса) toohost hello.
2. Щелкните элементы **Параметры > Параметры приложения**.
3. В hello **параметры приложения** добавьте следующие hello ключ и значение:
   
   | Ключ | Значение | Пример |
   | --- | --- | --- |
   | toDoListAPIURL |https://{имя_приложения_API_среднего_уровня}.azurewebsites.net |https://todolistapi0121.azurewebsites.net |
4. Щелкните **Сохранить**.
   
    Когда hello код работает в Azure, это значение переопределяет hello localhost URL-адрес, в hello *Web.config* файла. 
   
    возможности Hello код, который возвращает значение параметра hello *index.cshtml*:
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    Здравствуйте, код в *todoListSvc.js* использует приветствия:
   
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

### <a name="deploy-hello-todolistangular-web-project-toohello-new-web-app"></a>Развертывание hello ToDoListAngular web проекта toohello новое веб-приложение
* В Visual Studio в hello **подключения** шага hello **веб-публикация** мастера, нажмите кнопку **публикации**.
  
   Visual Studio развертывает hello ToDoListAngular проекта toohello новое веб-приложение и открывает обозреватель toohello URL-адрес веб-приложения hello. 

### <a name="test-hello-application-without-cors-enabled"></a>Тестирование приложения hello без CORS включен
1. В браузере средств разработчика откройте окно консоли hello.
2. В окне браузера hello, которое отображает hello AngularJS пользовательского интерфейса, выберите hello **tooDo списка** ссылку.
   
    код JavaScript Hello пытается toocall hello среднего уровня приложения API, но вызов hello завершается ошибкой, так как hello переднего плана выполняется в разных доменах hello обратно end. окно консоли средств разработчика браузера Hello показано сообщение об ошибке независимо от источника.
   
    ![Сообщение об ошибке CORS](./media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-hello-middle-tier-api-app"></a>Настройка CORS для hello среднего уровня приложения API
В этом разделе настройкой параметра CORS hello в Azure для hello среднего уровня приложения ToDoListAPI API. Эта настройка дает возможность hello среднего уровня приложения tooreceive JavaScript вызовы API из веб-приложения hello, созданный для проекта ToDoListAngular hello.

1. В браузере перейдите toohello [портал Azure](https://portal.azure.com/).
2. Нажмите кнопку **службы приложений**, а затем нажмите кнопку приложение hello API ToDoListAPI (средний уровень).
   
    ![Выбор приложения API на портале](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. В hello **параметры** колонку, которая открывает toohello правой части hello **приложения API** колонки, найти hello **API** , а затем выберите **CORS**.
   
   ![Выбор CORS на портале](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. В текстовом поле hello введите hello URL-адрес для веб-приложения hello ToDoListAngular (интерфейса). Например, если вы развернули hello ToDoListAngular проекта tooa веб-приложения с именем todolistangular0121, разрешить вызовы от hello URL-адрес `https://todolistangular0121.azurewebsites.net`.
   
   В качестве альтернативы можно ввести toospecify звездочка (*), что принимаются все домены-источники.
5. Щелкните **Сохранить**.
   
   ![Щелкните Сохранить](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   После нажатия кнопки **Сохранить**, приложение hello API JavaScript принимает вызовы из hello указан URL-адрес. На этом снимке экрана приложение hello ToDoListAPI0223 API будет принимать вызовы клиента JavaScript из веб-приложения hello ToDoListAngular.

### <a name="test-hello-application-with-cors-enabled"></a>Тестирование приложения hello с CORS включен
* Откройте браузер toohello HTTPS URL-адрес веб-приложения hello. 
  
    Это приложение hello времени позволяет просматривать, добавлять, изменять и удалять элементы задачи. 
  
    ![Страница списка tooDo образца приложения](./media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a>CORS службы приложений и CORS веб-API
В проекте веб-API можно установить hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) toospecify пакета NuGet в какие домены, будет принимать API JavaScript вызовы из кода.

Поддержка CORS веб-API более гибкая, чем поддержка CORS службы приложений. Например, в коде можно указать различные принимаемые источники для различных методов действий, тогда как для CORS службы приложений указывается один набор принимаемых источников для всех методов приложения API.

> [!NOTE]
> Старайтесь не toouse Web API CORS и CORS службы приложения в одно приложение API. В таком случае будет использоваться CORS службы приложений, а CORS веб-API — попросту игнорироваться. Например если включен один исходный домен в службе приложений и включить все домены-источники в коде веб-API, приложение Azure API только принимать вызовы от домена hello, указанного в Azure.
> 
> 

### <a name="how-tooenable-cors-in-web-api-code"></a>Как tooenable CORS в коде веб-API
Hello следующие шаги описывают процесс hello включения поддержки Web API CORS. Дополнительные сведения см. в статье [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api) (Включение запросов независимо от источника в веб-API 2 ASP.NET).

1. В проекте веб-API, установить hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) пакет NuGet.
2. Включить `config.EnableCors()` строку кода в hello **зарегистрировать** метод hello **WebApiConfig** класс как следующий пример hello. 
   
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
3. Добавьте в контроллер веб-API `using` инструкции для hello `System.Web.Http.Cors` пространства имен и добавить hello `EnableCors` атрибута toohello класса или tooindividual методы действий контроллера. В следующем примере hello поддержка CORS применяется toohello всего контроллера.
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a>Использование службы управления API с приложениями API
При использовании API управления Azure с помощью приложения API настройки CORS управления API, а не в API приложение hello. Дополнительные сведения см. в разделе hello следующие ресурсы:

* [Azure API Management Overview](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/) (Видеообзор службы управления API Azure). Часть о CORS начинается с 12:10 мин.
* [API Management cross domain policies](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a>Устранение неполадок
Если в ходе выполнения инструкций этого руководства возникнут проблемы, можно воспользоваться рекомендациями по устранению неполадок ниже.

* Убедитесь, что вы используете последнюю версию hello hello [Azure SDK для .NET для Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).
* Убедитесь, что вы ввели `https` в hello параметр CORS и убедитесь, что вы используете `https` toorun hello интерфейсный веб-приложения.
* Убедитесь, что вы ввели приветствия CORS в API приложение hello среднего уровня, а не в интерфейсном веб-приложения hello.
* Если вы настраиваете CORS в код приложения и службы приложений Azure, обратите внимание, что параметр CORS службы приложения hello перезаписывает все, что вы выполняете в коде приложения. 

в разделе toolearn Дополнительные сведения о функциональных возможностях Visual Studio, которые упрощают устранение неполадок, [Устранение неполадок Azure приложений служб приложений в Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).

## <a name="next-steps"></a>Дальнейшие действия
В этой статье показано, как поддерживают tooenable CORS службы приложения, чтобы клиентский код JavaScript может вызывать API в другом домене. Дополнительные сведения о приложениях API, чтение hello toolearn [tooauthentication введение в службе приложений](../app-service/app-service-authentication-overview.md), и затем перейти toohello [проверки подлинности пользователя для приложения API](app-service-api-dotnet-user-principal-auth.md) учебника.

