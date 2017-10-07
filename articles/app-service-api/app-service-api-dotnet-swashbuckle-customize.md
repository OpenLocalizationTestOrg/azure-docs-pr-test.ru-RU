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
# <a name="customize-swashbuckle-generated-api-definitions"></a><span data-ttu-id="8bba8-103">Настройка определений API, создаваемых в Swashbuckle</span><span class="sxs-lookup"><span data-stu-id="8bba8-103">Customize Swashbuckle-generated API definitions</span></span>
## <a name="overview"></a><span data-ttu-id="8bba8-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="8bba8-104">Overview</span></span>
<span data-ttu-id="8bba8-105">В этой статье объясняется, как toocustomize Swashbuckle toohandle распространенные сценарии которых требуется tooalter hello поведение по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="8bba8-105">This article explains how toocustomize Swashbuckle toohandle common scenarios where you may want tooalter hello default behavior:</span></span>

* <span data-ttu-id="8bba8-106">Swashbuckle создает повторяющиеся идентификаторы операций в случае перегрузок методов контроллера.</span><span class="sxs-lookup"><span data-stu-id="8bba8-106">Swashbuckle generates duplicate operation identifiers for overloads of controller methods</span></span>
* <span data-ttu-id="8bba8-107">Swashbuckle предполагается, что hello только допустимый ответ от метода HTTP 200 (ОК)</span><span class="sxs-lookup"><span data-stu-id="8bba8-107">Swashbuckle assumes that hello only valid response from a method is HTTP 200 (OK)</span></span> 

## <a name="customize-operation-identifier-generation"></a><span data-ttu-id="8bba8-108">Настройка параметров создания идентификаторов операций</span><span class="sxs-lookup"><span data-stu-id="8bba8-108">Customize operation identifier generation</span></span>
<span data-ttu-id="8bba8-109">Swashbuckle создает идентификаторы операций Swagger, объединяя имя контроллера и метода.</span><span class="sxs-lookup"><span data-stu-id="8bba8-109">Swashbuckle generates Swagger operation identifiers by concatenating controller name and method name.</span></span> <span data-ttu-id="8bba8-110">Использование такого шаблона влечет возникновение проблемы при наличии нескольких перегрузок метода. Swashbuckle создает повторяющиеся идентификаторы операции, которые являются недопустимым файлом Swagger JSON.</span><span class="sxs-lookup"><span data-stu-id="8bba8-110">This pattern creates a problem when you have multiple overloads of a method: Swashbuckle generates duplicate operation ids, which is invalid Swagger JSON.</span></span>

<span data-ttu-id="8bba8-111">Например следующий код контроллера hello вызывает Swashbuckle toogenerate три идентификаторы Contact_Get операций.</span><span class="sxs-lookup"><span data-stu-id="8bba8-111">For example, hello following controller code causes Swashbuckle toogenerate three Contact_Get operation ids.</span></span>

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsincode.png)

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsinjson.png)

<span data-ttu-id="8bba8-112">Вы можете решить проблему hello вручную, предоставляя методы hello уникальные имена, такие как hello ниже в этом примере:</span><span class="sxs-lookup"><span data-stu-id="8bba8-112">You can solve hello problem manually by giving hello methods unique names, such as hello following for this example:</span></span>

* <span data-ttu-id="8bba8-113">Получить</span><span class="sxs-lookup"><span data-stu-id="8bba8-113">Get</span></span>
* <span data-ttu-id="8bba8-114">GetById;</span><span class="sxs-lookup"><span data-stu-id="8bba8-114">GetById</span></span>
* <span data-ttu-id="8bba8-115">GetPage.</span><span class="sxs-lookup"><span data-stu-id="8bba8-115">GetPage</span></span>

<span data-ttu-id="8bba8-116">Hello альтернативой является toomake Swashbuckle tooextend, он автоматически создавать операции уникальные идентификаторы.</span><span class="sxs-lookup"><span data-stu-id="8bba8-116">hello alternative is tooextend Swashbuckle toomake it automatically generate unique operation ids.</span></span>

<span data-ttu-id="8bba8-117">Hello следующие шаги показывают, как hello toocustomize Swashbuckle с помощью *SwaggerConfig.cs* файл, включенный в проект hello шаблоном проекта hello предварительной версии приложений для Visual Studio API.</span><span class="sxs-lookup"><span data-stu-id="8bba8-117">hello following steps show how toocustomize Swashbuckle by using hello *SwaggerConfig.cs* file that is included in hello project by hello Visual Studio API Apps Preview project template.</span></span>  <span data-ttu-id="8bba8-118">Кроме того, Swashbuckle можно настроить в проекте веб-API, настроенного для развертывания в качестве приложения API.</span><span class="sxs-lookup"><span data-stu-id="8bba8-118">You can also customize Swashbuckle in a Web API project that you configure for deployment as an API app.</span></span>

1. <span data-ttu-id="8bba8-119">Создайте пользовательскую реализацию `IOperationFilter`</span><span class="sxs-lookup"><span data-stu-id="8bba8-119">Create a custom `IOperationFilter` implementation</span></span> 
   
    <span data-ttu-id="8bba8-120">Hello `IOperationFilter` интерфейс предоставляет точку расширения для Swashbuckle пользователей, желающих toocustomize различными аспектами процесса метаданных Swagger hello.</span><span class="sxs-lookup"><span data-stu-id="8bba8-120">hello `IOperationFilter` interface provides an extensibility point for Swashbuckle users who want toocustomize various aspects of hello Swagger metadata process.</span></span> <span data-ttu-id="8bba8-121">Hello следующий код демонстрирует один из способов изменения поведения операции идентификатор формирования hello.</span><span class="sxs-lookup"><span data-stu-id="8bba8-121">hello following code demonstrates one method of changing hello operation-id-generation behavior.</span></span> <span data-ttu-id="8bba8-122">Hello код добавляет имя идентификатора операции toohello имена параметра.</span><span class="sxs-lookup"><span data-stu-id="8bba8-122">hello code appends parameter names toohello operation id name.</span></span>  
   
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
2. <span data-ttu-id="8bba8-123">В *App_Start\SwaggerConfig.cs* файл, вызов hello `OperationFilter` метод toocause Swashbuckle toouse hello новый `IOperationFilter` реализации.</span><span class="sxs-lookup"><span data-stu-id="8bba8-123">In *App_Start\SwaggerConfig.cs* file, call hello `OperationFilter` method toocause Swashbuckle toouse hello new `IOperationFilter` implementation.</span></span>
   
        c.OperationFilter<MultipleOperationsWithSameVerbFilter>();
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/usefilter.png)
   
    <span data-ttu-id="8bba8-124">Hello *SwaggerConfig.cs* файл, который удаляется пакет Swashbuckle NuGet hello содержит множество примеров закомментированных точек расширения.</span><span class="sxs-lookup"><span data-stu-id="8bba8-124">hello *SwaggerConfig.cs* file that is dropped in by hello Swashbuckle NuGet package contains many commented-out examples of extensibility points.</span></span> <span data-ttu-id="8bba8-125">Дополнительные комментарии Hello здесь не показаны.</span><span class="sxs-lookup"><span data-stu-id="8bba8-125">hello additional comments are not shown here.</span></span> 
   
    <span data-ttu-id="8bba8-126">После внесения этого изменения вашего `IOperationFilter` реализация используется в результате чего создается toobe идентификаторы уникальный операции.</span><span class="sxs-lookup"><span data-stu-id="8bba8-126">After you make this change, your `IOperationFilter` implementation is used and causes unique operation ids toobe generated.</span></span>
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/uniqueids.png)

<a id="multiple-response-codes" name="multiple-response-codes"></a>

## <a name="allow-response-codes-other-than-200"></a><span data-ttu-id="8bba8-127">Коды ответов, отличные от 200</span><span class="sxs-lookup"><span data-stu-id="8bba8-127">Allow response codes other than 200</span></span>
<span data-ttu-id="8bba8-128">По умолчанию Swashbuckle предполагается, что ответ HTTP 200 (ОК) hello *только* правильный ответ метода веб-API.</span><span class="sxs-lookup"><span data-stu-id="8bba8-128">By default, Swashbuckle assumes that an HTTP 200 (OK) response is hello *only* legitimate response from a Web API method.</span></span> <span data-ttu-id="8bba8-129">В некоторых случаях вы можете tooreturn других кодов ответов не вызывая исключение tooraise клиента hello.</span><span class="sxs-lookup"><span data-stu-id="8bba8-129">In some cases, you may want tooreturn other response codes without causing hello client tooraise an exception.</span></span>  <span data-ttu-id="8bba8-130">Например hello следующий код веб-API демонстрирует сценарий необходимо tooaccept клиента hello 200 или 404 как допустимые ответы.</span><span class="sxs-lookup"><span data-stu-id="8bba8-130">For example, hello following Web API code demonstrates a scenario in which you would want hello client tooaccept either a 200 or a 404 as valid responses.</span></span>

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

<span data-ttu-id="8bba8-131">В этом сценарии Swagger Swashbuckle, создаваемый по умолчанию hello указывает только один законный код состояния HTTP, HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="8bba8-131">In this scenario, hello Swagger that Swashbuckle generates by default specifies only one legitimate HTTP status code, HTTP 200.</span></span>

![](./media/app-service-api-dotnet-swashbuckle-customize/http-200-output-only.png)

<span data-ttu-id="8bba8-132">Поскольку Visual Studio использует hello кода toogenerate определения Swagger API для клиента hello, он создает код клиента, который вызывает исключение в любой ответ, отличный от HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="8bba8-132">Since Visual Studio uses hello Swagger API definition toogenerate code for hello client, it creates client code that raises an exception for any response other than an HTTP 200.</span></span> <span data-ttu-id="8bba8-133">Приведенный ниже код Hello — из клиента C#, созданного для этого метода образец веб-API.</span><span class="sxs-lookup"><span data-stu-id="8bba8-133">hello code below is from a C# client generated for this sample Web API method.</span></span>

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

<span data-ttu-id="8bba8-134">Swashbuckle предоставляет два способа настройки списка hello ожидаемый кодов HTTP-ответов, которые он создает, используя XML-комментарии или hello `SwaggerResponse` атрибута.</span><span class="sxs-lookup"><span data-stu-id="8bba8-134">Swashbuckle provides two ways of customizing hello list of expected HTTP response codes that it generates, using XML comments or hello `SwaggerResponse` attribute.</span></span> <span data-ttu-id="8bba8-135">атрибут Hello проще, но это только Swashbuckle 5.1.5 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="8bba8-135">hello attribute is easier, but it is only available in Swashbuckle 5.1.5 or later.</span></span> <span data-ttu-id="8bba8-136">Hello приложения API Просмотр шаблона новый проект в Visual Studio 2013 включает Swashbuckle версии 5.0.0, поэтому если используется шаблон hello и не хотите tooupdate Swashbuckle, единственным вариантом toouse XML-комментарии.</span><span class="sxs-lookup"><span data-stu-id="8bba8-136">hello API Apps preview new-project template in Visual Studio 2013 includes Swashbuckle version 5.0.0, so if you used hello template and don't want tooupdate Swashbuckle, your only option is toouse XML comments.</span></span> 

### <a name="customize-expected-response-codes-using-xml-comments"></a><span data-ttu-id="8bba8-137">Настройка ожидаемых кодов в ответах с помощью XML-комментариев</span><span class="sxs-lookup"><span data-stu-id="8bba8-137">Customize expected response codes using XML comments</span></span>
<span data-ttu-id="8bba8-138">Коды ответа toospecify этот метод следует используйте, если ваш Swashbuckle версия более ранняя, чем 5.1.5.</span><span class="sxs-lookup"><span data-stu-id="8bba8-138">Use this method toospecify response codes if your Swashbuckle version is earlier than 5.1.5.</span></span>

1. <span data-ttu-id="8bba8-139">Сначала добавьте комментарии XML-документации по сравнению с методами hello которых надо toospecify коды ответа HTTP.</span><span class="sxs-lookup"><span data-stu-id="8bba8-139">First, add XML documentation comments over hello methods you wish toospecify HTTP response codes for.</span></span> <span data-ttu-id="8bba8-140">Действия hello образец веб-API, tooit документации XML показано выше и применение hello приведет к появлению следующего hello в следующем примере кода.</span><span class="sxs-lookup"><span data-stu-id="8bba8-140">Taking hello sample Web API action shown above and applying hello XML documentation tooit would result in code like hello following example.</span></span> 
   
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
2. <span data-ttu-id="8bba8-141">Добавьте инструкции в hello *SwaggerConfig.cs* файл toodirect Swashbuckle toomake использование hello XML-файл документации.</span><span class="sxs-lookup"><span data-stu-id="8bba8-141">Add instructions in hello *SwaggerConfig.cs* file toodirect Swashbuckle toomake use of hello XML documentation file.</span></span>
   
   * <span data-ttu-id="8bba8-142">Откройте *SwaggerConfig.cs* и создание метода на hello *SwaggerConfig* класса toospecify hello путь toohello XML-файл документации.</span><span class="sxs-lookup"><span data-stu-id="8bba8-142">Open *SwaggerConfig.cs* and create a method on hello *SwaggerConfig* class toospecify hello path toohello documentation XML file.</span></span> 
     
           private static string GetXmlCommentsPath()
           {
               return string.Format(@"{0}\XmlComments.xml", 
                   System.AppDomain.CurrentDomain.BaseDirectory);
           }
   * <span data-ttu-id="8bba8-143">Прокрутите вниз hello *SwaggerConfig.cs* файл, пока не увидите hello закомментированных строку кода, приведенном ниже снимке экрана hello в виде.</span><span class="sxs-lookup"><span data-stu-id="8bba8-143">Scroll down in hello *SwaggerConfig.cs* file until you see hello commented-out line of code resembling hello screen shot below.</span></span> 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-commented-out.png)
   * <span data-ttu-id="8bba8-144">Раскомментируйте hello tooenable hello XML комментариев обработки во время создания Swagger.</span><span class="sxs-lookup"><span data-stu-id="8bba8-144">Uncomment hello line tooenable hello XML comments processing during Swagger generation.</span></span> 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-uncommented.png)
3. <span data-ttu-id="8bba8-145">В порядке toogenerate hello XML-файл документации перейдите в свойства проекта hello и включите файл XML-документации hello как показано на следующем снимке экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="8bba8-145">In order toogenerate hello XML documentation file, go into hello project's properties and enable hello XML documentation file as shown in hello screenshot below.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/enable-xml-documentation-file.png) 

<span data-ttu-id="8bba8-146">После выполнения этих действий hello Swagger JSON, созданная по Swashbuckle отразят кодов hello HTTP-ответов, которые указаны в комментарии XML hello.</span><span class="sxs-lookup"><span data-stu-id="8bba8-146">Once you perform these steps, hello Swagger JSON generated by Swashbuckle will reflect hello HTTP response codes that you specified in hello XML comments.</span></span> <span data-ttu-id="8bba8-147">Снимок экрана приветствия ниже демонстрирует этот новый полезные данные JSON.</span><span class="sxs-lookup"><span data-stu-id="8bba8-147">hello screenshot below demonstrates this new JSON payload.</span></span> 

![](./media/app-service-api-dotnet-swashbuckle-customize/swagger-multiple-responses.png)

<span data-ttu-id="8bba8-148">При использовании Visual Studio tooregenerate hello клиентский код для API-интерфейса REST hello кода C# принимает коды состояния HTTP OK и не найден обоих hello без возникновения исключения, позволяя много toomake решения для кода на как toohandle hello возвращать значения NULL Обратитесь к записи.</span><span class="sxs-lookup"><span data-stu-id="8bba8-148">When you use Visual Studio tooregenerate hello client code for your REST API, hello C# code accepts both hello HTTP OK and Not Found status codes without raising an exception, allowing your consuming code toomake decisions on how toohandle hello return of a null Contact record.</span></span> 

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

<span data-ttu-id="8bba8-149">Hello код для этого примера можно найти в [этот репозиторий GitHub](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse).</span><span class="sxs-lookup"><span data-stu-id="8bba8-149">hello code for this demonstration can be found in [this GitHub repository](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse).</span></span> <span data-ttu-id="8bba8-150">Вместе с веб-API hello проект, помеченный комментарии XML-документации — проект консольного приложения, которая содержит клиент, созданный для этого API.</span><span class="sxs-lookup"><span data-stu-id="8bba8-150">Along with hello Web API project marked up with XML documentation comments is a Console Application project that contains a generated client for this API.</span></span> 

### <a name="customize-expected-response-codes-using-hello-swaggerresponse-attribute"></a><span data-ttu-id="8bba8-151">Настройка с помощью атрибута SwaggerResponse hello коды ожидаемого времени ответа</span><span class="sxs-lookup"><span data-stu-id="8bba8-151">Customize expected response codes using hello SwaggerResponse attribute</span></span>
<span data-ttu-id="8bba8-152">Hello [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) атрибута в Swashbuckle 5.1.5 и более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="8bba8-152">hello [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) attribute is available in Swashbuckle 5.1.5 and later.</span></span> <span data-ttu-id="8bba8-153">Если установлена более ранняя версия проекта, в этом разделе начинает, о том, как упаковать hello tooupdate Swashbuckle NuGet, чтобы этот атрибут можно использовать.</span><span class="sxs-lookup"><span data-stu-id="8bba8-153">In case you have an earlier version in your project, this section starts by explaining how tooupdate hello Swashbuckle NuGet package so that you can use this attribute.</span></span>

1. <span data-ttu-id="8bba8-154">В **обозревателе решений** щелкните правой кнопкой мыши проект веб-API и выберите **Управление пакетами NuGet**.</span><span class="sxs-lookup"><span data-stu-id="8bba8-154">In **Solution Explorer**, right-click your Web API project and click **Manage NuGet Packages**.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/manage-nuget-packages.png)
2. <span data-ttu-id="8bba8-155">Нажмите кнопку hello *обновление* кнопку Далее toohello *Swashbuckle* пакет NuGet.</span><span class="sxs-lookup"><span data-stu-id="8bba8-155">Click hello *Update* button next toohello *Swashbuckle* NuGet package.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/update-nuget-dialog.png)
3. <span data-ttu-id="8bba8-156">Добавить hello *SwaggerResponse* атрибуты методы действий toohello веб-API, для которых требуется toospecify допустимых кодов ответа HTTP.</span><span class="sxs-lookup"><span data-stu-id="8bba8-156">Add hello *SwaggerResponse* attributes toohello Web API action methods for which you want toospecify valid HTTP response codes.</span></span> 
   
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
4. <span data-ttu-id="8bba8-157">Добавить `using` инструкции для hello атрибут пространства имен:</span><span class="sxs-lookup"><span data-stu-id="8bba8-157">Add a `using` statement for hello attribute's namespace:</span></span>
   
        using Swashbuckle.Swagger.Annotations;
5. <span data-ttu-id="8bba8-158">Обзор toohello */swagger/docs/v1* URL-адрес проекта и различные коды ответа HTTP, которые будут отображаться в hello hello Swagger JSON.</span><span class="sxs-lookup"><span data-stu-id="8bba8-158">Browse toohello */swagger/docs/v1* URL of your project and hello various HTTP response codes will be visible in hello Swagger JSON.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/multiple-responses-post-attributes.png)

<span data-ttu-id="8bba8-159">Hello код для этого примера можно найти в [этот репозиторий GitHub](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes).</span><span class="sxs-lookup"><span data-stu-id="8bba8-159">hello code for this demonstration can be found in [this GitHub repository](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes).</span></span> <span data-ttu-id="8bba8-160">Вместе с hello проект веб-API декорированных hello *SwaggerResponse* атрибут является проект консольного приложения, которая содержит клиент, созданный для этого API.</span><span class="sxs-lookup"><span data-stu-id="8bba8-160">Along with hello Web API project decorated with hello *SwaggerResponse* attribute is a Console Application project that contains a generated client for this API.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8bba8-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8bba8-161">Next steps</span></span>
<span data-ttu-id="8bba8-162">В этой статье было показано, как способ hello toocustomize Swashbuckle приводит к возникновению ошибки операции идентификаторов и коды правильный ответ.</span><span class="sxs-lookup"><span data-stu-id="8bba8-162">This article has shown how toocustomize hello way Swashbuckle generates operation ids and valid response codes.</span></span> <span data-ttu-id="8bba8-163">Дополнительные сведения см. в статье [Swashbuckle на GitHub](https://github.com/domaindrivendev/Swashbuckle).</span><span class="sxs-lookup"><span data-stu-id="8bba8-163">For more information, see [Swashbuckle on GitHub](https://github.com/domaindrivendev/Swashbuckle).</span></span>

