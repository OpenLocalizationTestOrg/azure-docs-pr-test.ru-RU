---
title: "определения aaaCustomize Swashbuckle сгенерированные API"
description: "Узнайте, как определения Swagger API toocustomize, создаваемых Swashbuckle для приложения API в службе приложений Azure."
services: app-service\api
documentationcenter: .net
author: bradygaster
manager: erikre
editor: jimbe
ms.assetid: 6b8cbc38-d282-4a0f-b0c5-762631bae6f3
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/29/2016
ms.author: rachelap
ms.openlocfilehash: e31c665f8993533c5ec9a935e42cce34f86a5ade
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="customize-swashbuckle-generated-api-definitions"></a>Настройка определений API, создаваемых в Swashbuckle
## <a name="overview"></a>Обзор
В этой статье объясняется, как toocustomize Swashbuckle toohandle распространенные сценарии которых требуется tooalter hello поведение по умолчанию:

* Swashbuckle создает повторяющиеся идентификаторы операций в случае перегрузок методов контроллера.
* Swashbuckle предполагается, что hello только допустимый ответ от метода HTTP 200 (ОК) 

## <a name="customize-operation-identifier-generation"></a>Настройка параметров создания идентификаторов операций
Swashbuckle создает идентификаторы операций Swagger, объединяя имя контроллера и метода. Использование такого шаблона влечет возникновение проблемы при наличии нескольких перегрузок метода. Swashbuckle создает повторяющиеся идентификаторы операции, которые являются недопустимым файлом Swagger JSON.

Например следующий код контроллера hello вызывает Swashbuckle toogenerate три идентификаторы Contact_Get операций.

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsincode.png)

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsinjson.png)

Вы можете решить проблему hello вручную, предоставляя методы hello уникальные имена, такие как hello ниже в этом примере:

* Получить
* GetById;
* GetPage.

Hello альтернативой является toomake Swashbuckle tooextend, он автоматически создавать операции уникальные идентификаторы.

Hello следующие шаги показывают, как hello toocustomize Swashbuckle с помощью *SwaggerConfig.cs* файл, включенный в проект hello шаблоном проекта hello предварительной версии приложений для Visual Studio API.  Кроме того, Swashbuckle можно настроить в проекте веб-API, настроенного для развертывания в качестве приложения API.

1. Создайте пользовательскую реализацию `IOperationFilter` 
   
    Hello `IOperationFilter` интерфейс предоставляет точку расширения для Swashbuckle пользователей, желающих toocustomize различными аспектами процесса метаданных Swagger hello. Hello следующий код демонстрирует один из способов изменения поведения операции идентификатор формирования hello. Hello код добавляет имя идентификатора операции toohello имена параметра.  
   
        using Swashbuckle.Swagger;
        using System.Web.Http.Description;
   
        namespace ContactsList
        {
            public class MultipleOperationsWithSameVerbFilter : IOperationFilter
            {
                public void Apply(
                    Operation operation,
                    SchemaRegistry schemaRegistry,
                    ApiDescription apiDescription)
                {
                    if (operation.parameters != null)
                    {
                        operation.operationId += "By";
                        foreach (var parm in operation.parameters)
                        {
                            operation.operationId += string.Format("{0}",parm.name);
                        }
                    }
                }
            }
        }
2. В *App_Start\SwaggerConfig.cs* файл, вызов hello `OperationFilter` метод toocause Swashbuckle toouse hello новый `IOperationFilter` реализации.
   
        c.OperationFilter<MultipleOperationsWithSameVerbFilter>();
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/usefilter.png)
   
    Hello *SwaggerConfig.cs* файл, который удаляется пакет Swashbuckle NuGet hello содержит множество примеров закомментированных точек расширения. Дополнительные комментарии Hello здесь не показаны. 
   
    После внесения этого изменения вашего `IOperationFilter` реализация используется в результате чего создается toobe идентификаторы уникальный операции.
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/uniqueids.png)

<a id="multiple-response-codes" name="multiple-response-codes"></a>

## <a name="allow-response-codes-other-than-200"></a>Коды ответов, отличные от 200
По умолчанию Swashbuckle предполагается, что ответ HTTP 200 (ОК) hello *только* правильный ответ метода веб-API. В некоторых случаях вы можете tooreturn других кодов ответов не вызывая исключение tooraise клиента hello.  Например hello следующий код веб-API демонстрирует сценарий необходимо tooaccept клиента hello 200 или 404 как допустимые ответы.

    [ResponseType(typeof(Contact))]
    public HttpResponseMessage Get(int id)
    {
        var contacts = GetContacts();

        var requestedContact = contacts.FirstOrDefault(x => x.Id == id);

        if (requestedContact == null)
        {
            return Request.CreateResponse(HttpStatusCode.NotFound);
        }
        else
        {
            return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
        }
    }

В этом сценарии Swagger Swashbuckle, создаваемый по умолчанию hello указывает только один законный код состояния HTTP, HTTP 200.

![](./media/app-service-api-dotnet-swashbuckle-customize/http-200-output-only.png)

Поскольку Visual Studio использует hello кода toogenerate определения Swagger API для клиента hello, он создает код клиента, который вызывает исключение в любой ответ, отличный от HTTP 200. Приведенный ниже код Hello — из клиента C#, созданного для этого метода образец веб-API.

    if (statusCode != HttpStatusCode.OK)
    {
        HttpOperationException<object> ex = new HttpOperationException<object>();
        ex.Request = httpRequest;
        ex.Response = httpResponse;
        ex.Body = null;
        if (shouldTrace)
        {
            ServiceClientTracing.Error(invocationId, ex);
        }
        throw ex;
    } 

Swashbuckle предоставляет два способа настройки списка hello ожидаемый кодов HTTP-ответов, которые он создает, используя XML-комментарии или hello `SwaggerResponse` атрибута. атрибут Hello проще, но это только Swashbuckle 5.1.5 или более поздних версий. Hello приложения API Просмотр шаблона новый проект в Visual Studio 2013 включает Swashbuckle версии 5.0.0, поэтому если используется шаблон hello и не хотите tooupdate Swashbuckle, единственным вариантом toouse XML-комментарии. 

### <a name="customize-expected-response-codes-using-xml-comments"></a>Настройка ожидаемых кодов в ответах с помощью XML-комментариев
Коды ответа toospecify этот метод следует используйте, если ваш Swashbuckle версия более ранняя, чем 5.1.5.

1. Сначала добавьте комментарии XML-документации по сравнению с методами hello которых надо toospecify коды ответа HTTP. Действия hello образец веб-API, tooit документации XML показано выше и применение hello приведет к появлению следующего hello в следующем примере кода. 
   
        /// <summary>
        /// Returns hello specified contact.
        /// </summary>
        /// <param name="id">hello ID of hello contact.</param>
        /// <returns>A contact record with an HTTP 200, or null with an HTTP 404.</returns>
        /// <response code="200">OK</response>
        /// <response code="404">Not Found</response>
        [ResponseType(typeof(Contact))]
        public HttpResponseMessage Get(int id)
        {
            var contacts = GetContacts();
   
            var requestedContact = contacts.FirstOrDefault(x => x.Id == id);
   
            if (requestedContact == null)
            {
                return Request.CreateResponse(HttpStatusCode.NotFound);
            }
            else
            {
                return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
            }
        }
2. Добавьте инструкции в hello *SwaggerConfig.cs* файл toodirect Swashbuckle toomake использование hello XML-файл документации.
   
   * Откройте *SwaggerConfig.cs* и создание метода на hello *SwaggerConfig* класса toospecify hello путь toohello XML-файл документации. 
     
           private static string GetXmlCommentsPath()
           {
               return string.Format(@"{0}\XmlComments.xml", 
                   System.AppDomain.CurrentDomain.BaseDirectory);
           }
   * Прокрутите вниз hello *SwaggerConfig.cs* файл, пока не увидите hello закомментированных строку кода, приведенном ниже снимке экрана hello в виде. 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-commented-out.png)
   * Раскомментируйте hello tooenable hello XML комментариев обработки во время создания Swagger. 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-uncommented.png)
3. В порядке toogenerate hello XML-файл документации перейдите в свойства проекта hello и включите файл XML-документации hello как показано на следующем снимке экрана приветствия. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/enable-xml-documentation-file.png) 

После выполнения этих действий hello Swagger JSON, созданная по Swashbuckle отразят кодов hello HTTP-ответов, которые указаны в комментарии XML hello. Снимок экрана приветствия ниже демонстрирует этот новый полезные данные JSON. 

![](./media/app-service-api-dotnet-swashbuckle-customize/swagger-multiple-responses.png)

При использовании Visual Studio tooregenerate hello клиентский код для API-интерфейса REST hello кода C# принимает коды состояния HTTP OK и не найден обоих hello без возникновения исключения, позволяя много toomake решения для кода на как toohandle hello возвращать значения NULL Обратитесь к записи. 

        if (statusCode != HttpStatusCode.OK && statusCode != HttpStatusCode.NotFound)
        {
            HttpOperationException<object> ex = new HttpOperationException<object>();
            ex.Request = httpRequest;
            ex.Response = httpResponse;
            ex.Body = null;
            if (shouldTrace)
            {
                ServiceClientTracing.Error(invocationId, ex);
            }
                throw ex;
        }

Hello код для этого примера можно найти в [этот репозиторий GitHub](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse). Вместе с веб-API hello проект, помеченный комментарии XML-документации — проект консольного приложения, которая содержит клиент, созданный для этого API. 

### <a name="customize-expected-response-codes-using-hello-swaggerresponse-attribute"></a>Настройка с помощью атрибута SwaggerResponse hello коды ожидаемого времени ответа
Hello [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) атрибута в Swashbuckle 5.1.5 и более поздней версии. Если установлена более ранняя версия проекта, в этом разделе начинает, о том, как упаковать hello tooupdate Swashbuckle NuGet, чтобы этот атрибут можно использовать.

1. В **обозревателе решений** щелкните правой кнопкой мыши проект веб-API и выберите **Управление пакетами NuGet**. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/manage-nuget-packages.png)
2. Нажмите кнопку hello *обновление* кнопку Далее toohello *Swashbuckle* пакет NuGet. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/update-nuget-dialog.png)
3. Добавить hello *SwaggerResponse* атрибуты методы действий toohello веб-API, для которых требуется toospecify допустимых кодов ответа HTTP. 
   
        [SwaggerResponse(HttpStatusCode.OK)]
        [SwaggerResponse(HttpStatusCode.NotFound)]
        [ResponseType(typeof(Contact))]
        public HttpResponseMessage Get(int id)
        {
            var contacts = GetContacts();
   
            var requestedContact = contacts.FirstOrDefault(x => x.Id == id);
            if (requestedContact == null)
            {
                return Request.CreateResponse(HttpStatusCode.NotFound);
            }
            else
            {
                return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
            }
        }
4. Добавить `using` инструкции для hello атрибут пространства имен:
   
        using Swashbuckle.Swagger.Annotations;
5. Обзор toohello */swagger/docs/v1* URL-адрес проекта и различные коды ответа HTTP, которые будут отображаться в hello hello Swagger JSON. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/multiple-responses-post-attributes.png)

Hello код для этого примера можно найти в [этот репозиторий GitHub](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes). Вместе с hello проект веб-API декорированных hello *SwaggerResponse* атрибут является проект консольного приложения, которая содержит клиент, созданный для этого API. 

## <a name="next-steps"></a>Дальнейшие действия
В этой статье было показано, как способ hello toocustomize Swashbuckle приводит к возникновению ошибки операции идентификаторов и коды правильный ответ. Дополнительные сведения см. в статье [Swashbuckle на GitHub](https://github.com/domaindrivendev/Swashbuckle).

