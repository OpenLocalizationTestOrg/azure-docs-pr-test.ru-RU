---
title: "aaaException управления - Microsoft средства моделирования угроз - Azure | Документы Microsoft"
description: "защиту от угроз, которые представлены в hello средства моделирования угроз"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 247096c10deeca94ebb9b19df7ba60e442ca1e4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-exception-management--mitigations"></a><span data-ttu-id="4587d-103">Механизм безопасности. Управление исключениями | Устранение угроз</span><span class="sxs-lookup"><span data-stu-id="4587d-103">Security Frame: Exception Management | Mitigations</span></span> 
| <span data-ttu-id="4587d-104">Продукт или служба</span><span class="sxs-lookup"><span data-stu-id="4587d-104">Product/Service</span></span> | <span data-ttu-id="4587d-105">Статья</span><span class="sxs-lookup"><span data-stu-id="4587d-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="4587d-106">**WCF**</span><span class="sxs-lookup"><span data-stu-id="4587d-106">**WCF**</span></span> | <ul><li>[<span data-ttu-id="4587d-107">WCF — не добавляйте узел serviceDebug в файл конфигурации</span><span class="sxs-lookup"><span data-stu-id="4587d-107">WCF- Do not include serviceDebug node in configuration file</span></span>](#servicedebug)</li><li>[<span data-ttu-id="4587d-108">WCF — не добавляйте узел serviceMetadata в файл конфигурации</span><span class="sxs-lookup"><span data-stu-id="4587d-108">WCF- Do not include serviceMetadata node in configuration file</span></span>](#servicemetadata)</li></ul> |
| <span data-ttu-id="4587d-109">**Веб-интерфейс API**</span><span class="sxs-lookup"><span data-stu-id="4587d-109">**Web API**</span></span> | <ul><li>[<span data-ttu-id="4587d-110">Обеспечьте правильную обработку исключений в веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4587d-110">Ensure that proper exception handling is done in ASP.NET Web API </span></span>](#exception)</li></ul> |
| <span data-ttu-id="4587d-111">**Веб-приложение**</span><span class="sxs-lookup"><span data-stu-id="4587d-111">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="4587d-112">Не раскрывайте сведения о безопасности в сообщениях об ошибках</span><span class="sxs-lookup"><span data-stu-id="4587d-112">Do not expose security details in error messages </span></span>](#messages)</li><li>[<span data-ttu-id="4587d-113">Реализуйте страницу обработки ошибок по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4587d-113">Implement Default error handling page </span></span>](#default)</li><li>[<span data-ttu-id="4587d-114">Задайте способ развертывания tooRetail в службах IIS</span><span class="sxs-lookup"><span data-stu-id="4587d-114">Set Deployment Method tooRetail in IIS</span></span>](#deployment)</li><li>[<span data-ttu-id="4587d-115">Обеспечьте безопасную обработку исключений</span><span class="sxs-lookup"><span data-stu-id="4587d-115">Exceptions should fail safely</span></span>](#fail)</li></ul> |

## <span data-ttu-id="4587d-116"><a id="servicedebug"></a>WCF — не добавляйте узел serviceDebug в файл конфигурации</span><span class="sxs-lookup"><span data-stu-id="4587d-116"><a id="servicedebug"></a>WCF- Do not include serviceDebug node in configuration file</span></span>

| <span data-ttu-id="4587d-117">Название</span><span class="sxs-lookup"><span data-stu-id="4587d-117">Title</span></span>                   | <span data-ttu-id="4587d-118">Сведения</span><span class="sxs-lookup"><span data-stu-id="4587d-118">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="4587d-119">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="4587d-119">**Component**</span></span>               | <span data-ttu-id="4587d-120">WCF</span><span class="sxs-lookup"><span data-stu-id="4587d-120">WCF</span></span> | 
| <span data-ttu-id="4587d-121">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="4587d-121">**SDL Phase**</span></span>               | <span data-ttu-id="4587d-122">Создание</span><span class="sxs-lookup"><span data-stu-id="4587d-122">Build</span></span> |  
| <span data-ttu-id="4587d-123">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="4587d-123">**Applicable Technologies**</span></span> | <span data-ttu-id="4587d-124">Универсальные, .NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="4587d-124">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="4587d-125">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="4587d-125">**Attributes**</span></span>              | <span data-ttu-id="4587d-126">Недоступно</span><span class="sxs-lookup"><span data-stu-id="4587d-126">N/A</span></span>  |
| <span data-ttu-id="4587d-127">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="4587d-127">**References**</span></span>              | <span data-ttu-id="4587d-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="4587d-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="4587d-129">**Действия**</span><span class="sxs-lookup"><span data-stu-id="4587d-129">**Steps**</span></span> | <span data-ttu-id="4587d-130">Службы Windows Communication Framework (WCF) могут быть настроенный tooexpose отладочную информацию.</span><span class="sxs-lookup"><span data-stu-id="4587d-130">Windows Communication Framework (WCF) services can be configured tooexpose debugging information.</span></span> <span data-ttu-id="4587d-131">Отладочную информацию не следует использовать в рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="4587d-131">Debug information should not be used in production environments.</span></span> <span data-ttu-id="4587d-132">Hello `<serviceDebug>` тег определяет, включена ли функция сведения отладки hello для службы WCF.</span><span class="sxs-lookup"><span data-stu-id="4587d-132">hello `<serviceDebug>` tag defines whether hello debug information feature is enabled for a WCF service.</span></span> <span data-ttu-id="4587d-133">Если атрибут includeExceptionDetailInFaults hello tootrue, сведения об исключении из приложения hello будет возвращаться tooclients.</span><span class="sxs-lookup"><span data-stu-id="4587d-133">If hello attribute includeExceptionDetailInFaults is set tootrue, exception information from hello application will be returned tooclients.</span></span> <span data-ttu-id="4587d-134">Злоумышленники могут использовать hello дополнительных сведений, которые он получает из отлаживаемого вывода toomount атак нацелена на hello framework, базы данных или другие ресурсы, используемые приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4587d-134">Attackers can leverage hello additional information they gain from debugging output toomount attacks targeted on hello framework, database, or other resources used by hello application.</span></span> |

### <a name="example"></a><span data-ttu-id="4587d-135">Пример</span><span class="sxs-lookup"><span data-stu-id="4587d-135">Example</span></span>
<span data-ttu-id="4587d-136">Hello следующий файл конфигурации содержит hello `<serviceDebug>` тег:</span><span class="sxs-lookup"><span data-stu-id="4587d-136">hello following configuration file includes hello `<serviceDebug>` tag:</span></span> 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
<span data-ttu-id="4587d-137">Отключение отладочной информации в службе hello.</span><span class="sxs-lookup"><span data-stu-id="4587d-137">Disable debugging information in hello service.</span></span> <span data-ttu-id="4587d-138">Это можно сделать, удалив hello `<serviceDebug>` тег из файла конфигурации приложения.</span><span class="sxs-lookup"><span data-stu-id="4587d-138">This can be accomplished by removing hello `<serviceDebug>` tag from your application's configuration file.</span></span> 

## <span data-ttu-id="4587d-139"><a id="servicemetadata"></a>WCF — не добавляйте узел serviceMetadata в файл конфигурации</span><span class="sxs-lookup"><span data-stu-id="4587d-139"><a id="servicemetadata"></a>WCF- Do not include serviceMetadata node in configuration file</span></span>

| <span data-ttu-id="4587d-140">Название</span><span class="sxs-lookup"><span data-stu-id="4587d-140">Title</span></span>                   | <span data-ttu-id="4587d-141">Сведения</span><span class="sxs-lookup"><span data-stu-id="4587d-141">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="4587d-142">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="4587d-142">**Component**</span></span>               | <span data-ttu-id="4587d-143">WCF</span><span class="sxs-lookup"><span data-stu-id="4587d-143">WCF</span></span> | 
| <span data-ttu-id="4587d-144">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="4587d-144">**SDL Phase**</span></span>               | <span data-ttu-id="4587d-145">Создание</span><span class="sxs-lookup"><span data-stu-id="4587d-145">Build</span></span> |  
| <span data-ttu-id="4587d-146">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="4587d-146">**Applicable Technologies**</span></span> | <span data-ttu-id="4587d-147">Универсальный</span><span class="sxs-lookup"><span data-stu-id="4587d-147">Generic</span></span> |
| <span data-ttu-id="4587d-148">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="4587d-148">**Attributes**</span></span>              | <span data-ttu-id="4587d-149">Универсальные, .NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="4587d-149">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="4587d-150">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="4587d-150">**References**</span></span>              | <span data-ttu-id="4587d-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="4587d-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="4587d-152">**Действия**</span><span class="sxs-lookup"><span data-stu-id="4587d-152">**Steps**</span></span> | <span data-ttu-id="4587d-153">Публично раскрытия сведений о службе можно предоставляют злоумышленникам ценных сведений о того, как они могут воспользоваться hello службы.</span><span class="sxs-lookup"><span data-stu-id="4587d-153">Publicly exposing information about a service can provide attackers with valuable insight into how they might exploit hello service.</span></span> <span data-ttu-id="4587d-154">Hello `<serviceMetadata>` тег включает средство публикации метаданных hello.</span><span class="sxs-lookup"><span data-stu-id="4587d-154">hello `<serviceMetadata>` tag enables hello metadata publishing feature.</span></span> <span data-ttu-id="4587d-155">Метаданные службы могут содержать конфиденциальные сведения, к которым нельзя предоставлять общий доступ.</span><span class="sxs-lookup"><span data-stu-id="4587d-155">Service metadata could contain sensitive information that should not be publicly accessible.</span></span> <span data-ttu-id="4587d-156">Как минимум разрешается только доверенные пользователи tooaccess hello метаданных и убедитесь, что ненужные сведения не предоставляются.</span><span class="sxs-lookup"><span data-stu-id="4587d-156">At a minimum, only allow trusted users tooaccess hello metadata and ensure that unnecessary information is not exposed.</span></span> <span data-ttu-id="4587d-157">Что еще лучше полностью отключите hello возможность toopublish метаданных.</span><span class="sxs-lookup"><span data-stu-id="4587d-157">Better yet, entirely disable hello ability toopublish metadata.</span></span> <span data-ttu-id="4587d-158">Безопасные конфигурации WCF не будет содержать hello `<serviceMetadata>` тег.</span><span class="sxs-lookup"><span data-stu-id="4587d-158">A safe WCF configuration will not contain hello `<serviceMetadata>` tag.</span></span> |

## <span data-ttu-id="4587d-159"><a id="exception"></a>Обеспечьте правильную обработку исключений в веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4587d-159"><a id="exception"></a>Ensure that proper exception handling is done in ASP.NET Web API</span></span>

| <span data-ttu-id="4587d-160">Название</span><span class="sxs-lookup"><span data-stu-id="4587d-160">Title</span></span>                   | <span data-ttu-id="4587d-161">Сведения</span><span class="sxs-lookup"><span data-stu-id="4587d-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="4587d-162">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="4587d-162">**Component**</span></span>               | <span data-ttu-id="4587d-163">Веб-интерфейс API</span><span class="sxs-lookup"><span data-stu-id="4587d-163">Web API</span></span> | 
| <span data-ttu-id="4587d-164">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="4587d-164">**SDL Phase**</span></span>               | <span data-ttu-id="4587d-165">Создание</span><span class="sxs-lookup"><span data-stu-id="4587d-165">Build</span></span> |  
| <span data-ttu-id="4587d-166">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="4587d-166">**Applicable Technologies**</span></span> | <span data-ttu-id="4587d-167">MVC 5, MVC 6</span><span class="sxs-lookup"><span data-stu-id="4587d-167">MVC 5, MVC 6</span></span> |
| <span data-ttu-id="4587d-168">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="4587d-168">**Attributes**</span></span>              | <span data-ttu-id="4587d-169">Недоступно</span><span class="sxs-lookup"><span data-stu-id="4587d-169">N/A</span></span>  |
| <span data-ttu-id="4587d-170">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="4587d-170">**References**</span></span>              | <span data-ttu-id="4587d-171">[Обработка исключений в веб-API ASP.NET](http://www.asp.net/web-api/overview/error-handling/exception-handling), [проверка модели в веб-API ASP.NET](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span><span class="sxs-lookup"><span data-stu-id="4587d-171">[Exception Handling in ASP.NET Web API](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Model Validation in ASP.NET Web API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span></span> |
| <span data-ttu-id="4587d-172">**Действия**</span><span class="sxs-lookup"><span data-stu-id="4587d-172">**Steps**</span></span> | <span data-ttu-id="4587d-173">По умолчанию большинство неперехваченных исключений в веб-API ASP.NET преобразовываются в HTTP-ответ с кодом состояния `500, Internal Server Error`.</span><span class="sxs-lookup"><span data-stu-id="4587d-173">By default, most uncaught exceptions in ASP.NET Web API are translated into an HTTP response with status code `500, Internal Server Error`</span></span>|

### <a name="example"></a><span data-ttu-id="4587d-174">Пример</span><span class="sxs-lookup"><span data-stu-id="4587d-174">Example</span></span>
<span data-ttu-id="4587d-175">Код состояния toocontrol hello, hello API, `HttpResponseException` можно использовать, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="4587d-175">toocontrol hello status code returned by hello API, `HttpResponseException` can be used as shown below:</span></span> 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        throw new HttpResponseException(HttpStatusCode.NotFound);
    }
    return item;
}
```

### <a name="example"></a><span data-ttu-id="4587d-176">Пример</span><span class="sxs-lookup"><span data-stu-id="4587d-176">Example</span></span>
<span data-ttu-id="4587d-177">Для дальнейшего управления ответе исключение hello hello `HttpResponseMessage` класс может использоваться, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="4587d-177">For further control on hello exception response, hello `HttpResponseMessage` class can be used as shown below:</span></span> 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        var resp = new HttpResponseMessage(HttpStatusCode.NotFound)
        {
            Content = new StringContent(string.Format("No product with ID = {0}", id)),
            ReasonPhrase = "Product ID Not Found"
        }
        throw new HttpResponseException(resp);
    }
    return item;
}
```
<span data-ttu-id="4587d-178">toocatch необработанные исключения, которые не относятся к типу hello `HttpResponseException`, можно использовать фильтры исключений.</span><span class="sxs-lookup"><span data-stu-id="4587d-178">toocatch unhandled exceptions that are not of hello type `HttpResponseException`, Exception Filters can be used.</span></span> <span data-ttu-id="4587d-179">Фильтры исключений реализовать hello `System.Web.Http.Filters.IExceptionFilter` интерфейса.</span><span class="sxs-lookup"><span data-stu-id="4587d-179">Exception filters implement hello `System.Web.Http.Filters.IExceptionFilter` interface.</span></span> <span data-ttu-id="4587d-180">Hello простейший способ toowrite фильтра исключений является tooderive из hello `System.Web.Http.Filters.ExceptionFilterAttribute` класса и переопределить метод OnException hello.</span><span class="sxs-lookup"><span data-stu-id="4587d-180">hello simplest way toowrite an exception filter is tooderive from hello `System.Web.Http.Filters.ExceptionFilterAttribute` class and override hello OnException method.</span></span> 

### <a name="example"></a><span data-ttu-id="4587d-181">Пример</span><span class="sxs-lookup"><span data-stu-id="4587d-181">Example</span></span>
<span data-ttu-id="4587d-182">Ниже приведен фильтр, который преобразует исключения `NotImplementedException` в код состояния HTTP `501, Not Implemented`.</span><span class="sxs-lookup"><span data-stu-id="4587d-182">Here is a filter that converts `NotImplementedException` exceptions into HTTP status code `501, Not Implemented`:</span></span> 
```C#
namespace ProductStore.Filters
{
    using System;
    using System.Net;
    using System.Net.Http;
    using System.Web.Http.Filters;

    public class NotImplExceptionFilterAttribute : ExceptionFilterAttribute 
    {
        public override void OnException(HttpActionExecutedContext context)
        {
            if (context.Exception is NotImplementedException)
            {
                context.Response = new HttpResponseMessage(HttpStatusCode.NotImplemented);
            }
        }
    }
}
```

<span data-ttu-id="4587d-183">Существует несколько способов tooregister в фильтре исключений веб-API.</span><span class="sxs-lookup"><span data-stu-id="4587d-183">There are several ways tooregister a Web API exception filter:</span></span>
- <span data-ttu-id="4587d-184">Для действия</span><span class="sxs-lookup"><span data-stu-id="4587d-184">By action</span></span>
- <span data-ttu-id="4587d-185">Для контроллера</span><span class="sxs-lookup"><span data-stu-id="4587d-185">By controller</span></span>
- <span data-ttu-id="4587d-186">Глобально</span><span class="sxs-lookup"><span data-stu-id="4587d-186">Globally</span></span>

### <a name="example"></a><span data-ttu-id="4587d-187">Пример</span><span class="sxs-lookup"><span data-stu-id="4587d-187">Example</span></span>
<span data-ttu-id="4587d-188">tooapply hello фильтрации tooa определенное действие, добавить фильтр hello в качестве атрибута toohello действия:</span><span class="sxs-lookup"><span data-stu-id="4587d-188">tooapply hello filter tooa specific action, add hello filter as an attribute toohello action:</span></span> 
```C#
public class ProductsController : ApiController
{
    [NotImplExceptionFilter]
    public Contact GetContact(int id)
    {
        throw new NotImplementedException("This method is not implemented");
    }
}
```
### <a name="example"></a><span data-ttu-id="4587d-189">Пример</span><span class="sxs-lookup"><span data-stu-id="4587d-189">Example</span></span>
<span data-ttu-id="4587d-190">tooapply tooall фильтра hello hello действий над `controller`, добавить фильтр hello в качестве атрибута toohello `controller` класса:</span><span class="sxs-lookup"><span data-stu-id="4587d-190">tooapply hello filter tooall of hello actions on a `controller`, add hello filter as an attribute toohello `controller` class:</span></span> 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a><span data-ttu-id="4587d-191">Пример</span><span class="sxs-lookup"><span data-stu-id="4587d-191">Example</span></span>
<span data-ttu-id="4587d-192">tooapply hello глобально фильтрации tooall контроллеров веб-API, добавьте экземпляр фильтра toohello hello `GlobalConfiguration.Configuration.Filters` коллекции.</span><span class="sxs-lookup"><span data-stu-id="4587d-192">tooapply hello filter globally tooall Web API controllers, add an instance of hello filter toohello `GlobalConfiguration.Configuration.Filters` collection.</span></span> <span data-ttu-id="4587d-193">Фильтры исключений в этой коллекции применяются tooany действие контроллера Web API.</span><span class="sxs-lookup"><span data-stu-id="4587d-193">Exception filters in this collection apply tooany Web API controller action.</span></span> 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a><span data-ttu-id="4587d-194">Пример</span><span class="sxs-lookup"><span data-stu-id="4587d-194">Example</span></span>
<span data-ttu-id="4587d-195">Проверка модели hello состояние модели могут передаваться метод tooCreateErrorResponse, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="4587d-195">For model validation, hello model state can be passed tooCreateErrorResponse method as shown below:</span></span> 
```C#
public HttpResponseMessage PostProduct(Product item)
{
    if (!ModelState.IsValid)
    {
        return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ModelState);
    }
    // Implementation not shown...
}
```

<span data-ttu-id="4587d-196">Проверьте hello ссылки в разделе hello ссылки на дополнительные сведения об обработке исключительные и проверка модели в ASP.Net Web API</span><span class="sxs-lookup"><span data-stu-id="4587d-196">Check hello links in hello references section for additional details about exceptional handling and model validation in ASP.Net Web API</span></span> 

## <span data-ttu-id="4587d-197"><a id="messages"></a>Не раскрывайте сведения о безопасности в сообщениях об ошибках</span><span class="sxs-lookup"><span data-stu-id="4587d-197"><a id="messages"></a>Do not expose security details in error messages</span></span>

| <span data-ttu-id="4587d-198">Название</span><span class="sxs-lookup"><span data-stu-id="4587d-198">Title</span></span>                   | <span data-ttu-id="4587d-199">Сведения</span><span class="sxs-lookup"><span data-stu-id="4587d-199">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="4587d-200">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="4587d-200">**Component**</span></span>               | <span data-ttu-id="4587d-201">Веб-приложение</span><span class="sxs-lookup"><span data-stu-id="4587d-201">Web Application</span></span> | 
| <span data-ttu-id="4587d-202">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="4587d-202">**SDL Phase**</span></span>               | <span data-ttu-id="4587d-203">Создание</span><span class="sxs-lookup"><span data-stu-id="4587d-203">Build</span></span> |  
| <span data-ttu-id="4587d-204">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="4587d-204">**Applicable Technologies**</span></span> | <span data-ttu-id="4587d-205">Универсальный</span><span class="sxs-lookup"><span data-stu-id="4587d-205">Generic</span></span> |
| <span data-ttu-id="4587d-206">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="4587d-206">**Attributes**</span></span>              | <span data-ttu-id="4587d-207">Недоступно</span><span class="sxs-lookup"><span data-stu-id="4587d-207">N/A</span></span>  |
| <span data-ttu-id="4587d-208">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="4587d-208">**References**</span></span>              | <span data-ttu-id="4587d-209">Недоступно</span><span class="sxs-lookup"><span data-stu-id="4587d-209">N/A</span></span>  |
| <span data-ttu-id="4587d-210">**Действия**</span><span class="sxs-lookup"><span data-stu-id="4587d-210">**Steps**</span></span> | <p><span data-ttu-id="4587d-211">Общие сообщения об ошибке предоставляются непосредственно пользователю toohello без включения конфиденциальных данных.</span><span class="sxs-lookup"><span data-stu-id="4587d-211">Generic error messages are provided directly toohello user without including sensitive application data.</span></span> <span data-ttu-id="4587d-212">К конфиденциальным данным относятся:</span><span class="sxs-lookup"><span data-stu-id="4587d-212">Examples of sensitive data include:</span></span></p><ul><li><span data-ttu-id="4587d-213">имена серверов;</span><span class="sxs-lookup"><span data-stu-id="4587d-213">Server names</span></span></li><li><span data-ttu-id="4587d-214">Строки подключения</span><span class="sxs-lookup"><span data-stu-id="4587d-214">Connection strings</span></span></li><li><span data-ttu-id="4587d-215">имена пользователей;</span><span class="sxs-lookup"><span data-stu-id="4587d-215">Usernames</span></span></li><li><span data-ttu-id="4587d-216">Пароли</span><span class="sxs-lookup"><span data-stu-id="4587d-216">Passwords</span></span></li><li><span data-ttu-id="4587d-217">процедуры SQL;</span><span class="sxs-lookup"><span data-stu-id="4587d-217">SQL procedures</span></span></li><li><span data-ttu-id="4587d-218">подробные сведения о динамических ошибках SQL;</span><span class="sxs-lookup"><span data-stu-id="4587d-218">Details of dynamic SQL failures</span></span></li><li><span data-ttu-id="4587d-219">трассировка стека и строки кода;</span><span class="sxs-lookup"><span data-stu-id="4587d-219">Stack trace and lines of code</span></span></li><li><span data-ttu-id="4587d-220">переменные, хранимые в памяти;</span><span class="sxs-lookup"><span data-stu-id="4587d-220">Variables stored in memory</span></span></li><li><span data-ttu-id="4587d-221">расположения дисков и папок;</span><span class="sxs-lookup"><span data-stu-id="4587d-221">Drive and folder locations</span></span></li><li><span data-ttu-id="4587d-222">точки установки приложения;</span><span class="sxs-lookup"><span data-stu-id="4587d-222">Application install points</span></span></li><li><span data-ttu-id="4587d-223">параметры конфигурации узла;</span><span class="sxs-lookup"><span data-stu-id="4587d-223">Host configuration settings</span></span></li><li><span data-ttu-id="4587d-224">другие внутренние сведения о приложении.</span><span class="sxs-lookup"><span data-stu-id="4587d-224">Other internal application details</span></span></li></ul><p><span data-ttu-id="4587d-225">Перехват всех ошибок в приложении и предоставление общих сообщений об ошибках, а также включение пользовательских ошибок в службах IIS позволяют предотвратить раскрытие информации.</span><span class="sxs-lookup"><span data-stu-id="4587d-225">Trapping all errors within an application and providing generic error messages, as well as enabling custom errors within IIS will help prevent information disclosure.</span></span> <span data-ttu-id="4587d-226">База данных SQL Server и .NET обработка исключений, среди других ошибок архитектур, являются особенно verbose и чрезвычайно полезна tooa злоумышленник профилирование приложения.</span><span class="sxs-lookup"><span data-stu-id="4587d-226">SQL Server database and .NET Exception handling, among other error handling architectures, are especially verbose and extremely useful tooa malicious user profiling your application.</span></span> <span data-ttu-id="4587d-227">Сделайте не напрямую hello отображения содержимого класса, производным от класса исключения .NET hello и убедитесь, что правильной обработкой исключений, чтобы случайно не произошло непредвиденное исключение возникает непосредственно toohello пользователя.</span><span class="sxs-lookup"><span data-stu-id="4587d-227">Do not directly display hello contents of a class derived from hello .NET Exception class, and ensure that you have proper exception handling so that an unexpected exception isn't inadvertently raised directly toohello user.</span></span></p><ul><li><span data-ttu-id="4587d-228">Укажите общее сообщение об ошибке непосредственно сообщения toohello пользователя, который абстрактного дальней конкретные сведения непосредственно в сообщение hello исключение или ошибка</span><span class="sxs-lookup"><span data-stu-id="4587d-228">Provide generic error messages directly toohello user that abstract away specific details found directly in hello exception/error message</span></span></li><li><span data-ttu-id="4587d-229">Отображаемое содержимое hello исключения .NET класса напрямую toohello пользователя</span><span class="sxs-lookup"><span data-stu-id="4587d-229">Do not display hello contents of a .NET exception class directly toohello user</span></span></li><li><span data-ttu-id="4587d-230">Отслеживать все сообщения об ошибках и если соответствующее сообщение hello пользователя с помощью клиента приложения сообщение отправлено toohello универсальное сообщение об ошибке</span><span class="sxs-lookup"><span data-stu-id="4587d-230">Trap all error messages and if appropriate inform hello user via a generic error message sent toohello application client</span></span></li><li><span data-ttu-id="4587d-231">Не предоставляйте hello содержимого hello исключение класса напрямую пользователя toohello особенно hello возвращаемое значение из `.ToString()`, или hello значений свойств сообщений или StackTrace hello.</span><span class="sxs-lookup"><span data-stu-id="4587d-231">Do not expose hello contents of hello Exception class directly toohello user, especially hello return value from `.ToString()`, or hello values of hello Message or StackTrace properties.</span></span> <span data-ttu-id="4587d-232">Безопасно этого данные журнала и отображение более кроется пользователя toohello сообщения</span><span class="sxs-lookup"><span data-stu-id="4587d-232">Securely log this information and display a more innocuous message toohello user</span></span></li></ul>|

## <span data-ttu-id="4587d-233"><a id="default"></a>Реализуйте страницу обработки ошибок по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4587d-233"><a id="default"></a>Implement Default error handling page</span></span>

| <span data-ttu-id="4587d-234">Название</span><span class="sxs-lookup"><span data-stu-id="4587d-234">Title</span></span>                   | <span data-ttu-id="4587d-235">Сведения</span><span class="sxs-lookup"><span data-stu-id="4587d-235">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="4587d-236">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="4587d-236">**Component**</span></span>               | <span data-ttu-id="4587d-237">Веб-приложение</span><span class="sxs-lookup"><span data-stu-id="4587d-237">Web Application</span></span> | 
| <span data-ttu-id="4587d-238">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="4587d-238">**SDL Phase**</span></span>               | <span data-ttu-id="4587d-239">Создание</span><span class="sxs-lookup"><span data-stu-id="4587d-239">Build</span></span> |  
| <span data-ttu-id="4587d-240">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="4587d-240">**Applicable Technologies**</span></span> | <span data-ttu-id="4587d-241">Универсальный</span><span class="sxs-lookup"><span data-stu-id="4587d-241">Generic</span></span> |
| <span data-ttu-id="4587d-242">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="4587d-242">**Attributes**</span></span>              | <span data-ttu-id="4587d-243">Недоступно</span><span class="sxs-lookup"><span data-stu-id="4587d-243">N/A</span></span>  |
| <span data-ttu-id="4587d-244">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="4587d-244">**References**</span></span>              | <span data-ttu-id="4587d-245">[Сведения о диалоговом окне изменения параметров страниц ошибок ASP.NET](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="4587d-245">[Edit ASP.NET Error Pages Settings Dialog Box](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span></span> |
| <span data-ttu-id="4587d-246">**Действия**</span><span class="sxs-lookup"><span data-stu-id="4587d-246">**Steps**</span></span> | <p><span data-ttu-id="4587d-247">Если приложение ASP.NET перестает работать и приводит к возникновению ошибки "HTTP/1.x 500 — внутренняя ошибка сервера" или конфигурация компонентов (например, фильтрация запросов) предотвращает отображение страницы, создается сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="4587d-247">When an ASP.NET application fails and causes an HTTP/1.x 500 Internal Server Error, or a feature configuration (such as Request Filtering) prevents a page from being displayed, an error message will be generated.</span></span> <span data-ttu-id="4587d-248">Администраторы могут выбрать, отображать ли приложение hello понятное сообщение toohello клиента, клиент toohello сообщений подробные сведения об ошибке или только toolocalhost сообщения подробные сведения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="4587d-248">Administrators can choose whether or not hello application should display a friendly message toohello client, detailed error message toohello client, or detailed error message toolocalhost only.</span></span> <span data-ttu-id="4587d-249">Hello <customErrors> тег в файле web.config hello имеет три режима:</span><span class="sxs-lookup"><span data-stu-id="4587d-249">hello <customErrors> tag in hello web.config has three modes:</span></span></p><ul><li><span data-ttu-id="4587d-250">**On.** Указывает, что пользовательские ошибки включены.</span><span class="sxs-lookup"><span data-stu-id="4587d-250">**On:** Specifies that custom errors are enabled.</span></span> <span data-ttu-id="4587d-251">Если атрибут defaultRedirect не указан, для пользователей отобразится общая ошибка.</span><span class="sxs-lookup"><span data-stu-id="4587d-251">If no defaultRedirect attribute is specified, users see a generic error.</span></span> <span data-ttu-id="4587d-252">пользовательские ошибки Hello отображаются toohello удаленные клиенты и toohello локального узла</span><span class="sxs-lookup"><span data-stu-id="4587d-252">hello custom errors are shown toohello remote clients and toohello local host</span></span></li><li><span data-ttu-id="4587d-253">**Off.** Указывает, что пользовательские ошибки выключены.</span><span class="sxs-lookup"><span data-stu-id="4587d-253">**Off:** Specifies that custom errors are disabled.</span></span> <span data-ttu-id="4587d-254">Hello подробные сведения об ошибках ASP.NET отображаются toohello удаленные клиенты и toohello локального узла</span><span class="sxs-lookup"><span data-stu-id="4587d-254">hello detailed ASP.NET errors are shown toohello remote clients and toohello local host</span></span></li><li><span data-ttu-id="4587d-255">**RemoteOnly:** указывает, что настраиваемые ошибки отображаются только toohello удаленных клиентов, а ошибки ASP.NET отображаются toohello локального узла.</span><span class="sxs-lookup"><span data-stu-id="4587d-255">**RemoteOnly:** Specifies that custom errors are shown only toohello remote clients, and that ASP.NET errors are shown toohello local host.</span></span> <span data-ttu-id="4587d-256">Это значение по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="4587d-256">This is hello default value</span></span></li></ul><p><span data-ttu-id="4587d-257">Откройте hello `web.config` файл для узла приложения hello и убедитесь, что тег hello либо `<customErrors mode="RemoteOnly" />` или `<customErrors mode="On" />` определен.</span><span class="sxs-lookup"><span data-stu-id="4587d-257">Open hello `web.config` file for hello application/site and ensure that hello tag has either `<customErrors mode="RemoteOnly" />` or `<customErrors mode="On" />` defined.</span></span></p>|

## <span data-ttu-id="4587d-258"><a id="deployment"></a>Задайте способ развертывания tooRetail в службах IIS</span><span class="sxs-lookup"><span data-stu-id="4587d-258"><a id="deployment"></a>Set Deployment Method tooRetail in IIS</span></span>

| <span data-ttu-id="4587d-259">Название</span><span class="sxs-lookup"><span data-stu-id="4587d-259">Title</span></span>                   | <span data-ttu-id="4587d-260">Сведения</span><span class="sxs-lookup"><span data-stu-id="4587d-260">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="4587d-261">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="4587d-261">**Component**</span></span>               | <span data-ttu-id="4587d-262">Веб-приложение</span><span class="sxs-lookup"><span data-stu-id="4587d-262">Web Application</span></span> | 
| <span data-ttu-id="4587d-263">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="4587d-263">**SDL Phase**</span></span>               | <span data-ttu-id="4587d-264">Развертывание</span><span class="sxs-lookup"><span data-stu-id="4587d-264">Deployment</span></span> |  
| <span data-ttu-id="4587d-265">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="4587d-265">**Applicable Technologies**</span></span> | <span data-ttu-id="4587d-266">Универсальный</span><span class="sxs-lookup"><span data-stu-id="4587d-266">Generic</span></span> |
| <span data-ttu-id="4587d-267">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="4587d-267">**Attributes**</span></span>              | <span data-ttu-id="4587d-268">Недоступно</span><span class="sxs-lookup"><span data-stu-id="4587d-268">N/A</span></span>  |
| <span data-ttu-id="4587d-269">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="4587d-269">**References**</span></span>              | <span data-ttu-id="4587d-270">[Элемент deployment (схема параметров ASP.NET)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span><span class="sxs-lookup"><span data-stu-id="4587d-270">[deployment Element (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span></span> |
| <span data-ttu-id="4587d-271">**Действия**</span><span class="sxs-lookup"><span data-stu-id="4587d-271">**Steps**</span></span> | <p><span data-ttu-id="4587d-272">Hello `<deployment retail>` коммутатора предназначена для использования в производственных серверах IIS.</span><span class="sxs-lookup"><span data-stu-id="4587d-272">hello `<deployment retail>` switch is intended for use by production IIS servers.</span></span> <span data-ttu-id="4587d-273">Этот параметр является используется toohelp приложения, выполняемые с наилучшей возможной производительности hello и наименьший возможный сведения о безопасности, что leakages, отключив hello вывод трассировки toogenerate возможности приложения на странице, отключение toodisplay возможность hello подробное сообщение об ошибке Пользователи tooend сообщений и отключение переключатель отладки hello.</span><span class="sxs-lookup"><span data-stu-id="4587d-273">This switch is used toohelp applications run with hello best possible performance and least possible security information leakages by disabling hello application's ability toogenerate trace output on a page, disabling hello ability toodisplay detailed error messages tooend users, and disabling hello debug switch.</span></span></p><p><span data-ttu-id="4587d-274">Зачастую параметры, предназначенные для разработчиков, например трассировка и отладка неудачно завершенных запросов, включаются во время активной разработки.</span><span class="sxs-lookup"><span data-stu-id="4587d-274">Often times, switches and options that are developer-focused, such as failed request tracing and debugging, are enabled during active development.</span></span> <span data-ttu-id="4587d-275">Рекомендуется, задать tooretail hello метода развертывания на любом сервере в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="4587d-275">It is recommended that hello deployment method on any production server be set tooretail.</span></span> <span data-ttu-id="4587d-276">Откройте файл machine.config hello и убедитесь, что `<deployment retail="true" />` остается установленным tootrue.</span><span class="sxs-lookup"><span data-stu-id="4587d-276">open hello machine.config file and ensure that `<deployment retail="true" />` remains set tootrue.</span></span></p>|

## <span data-ttu-id="4587d-277"><a id="fail"></a>Обеспечьте безопасную обработку исключений</span><span class="sxs-lookup"><span data-stu-id="4587d-277"><a id="fail"></a>Exceptions should fail safely</span></span>

| <span data-ttu-id="4587d-278">Название</span><span class="sxs-lookup"><span data-stu-id="4587d-278">Title</span></span>                   | <span data-ttu-id="4587d-279">Сведения</span><span class="sxs-lookup"><span data-stu-id="4587d-279">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="4587d-280">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="4587d-280">**Component**</span></span>               | <span data-ttu-id="4587d-281">Веб-приложение</span><span class="sxs-lookup"><span data-stu-id="4587d-281">Web Application</span></span> | 
| <span data-ttu-id="4587d-282">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="4587d-282">**SDL Phase**</span></span>               | <span data-ttu-id="4587d-283">Создание</span><span class="sxs-lookup"><span data-stu-id="4587d-283">Build</span></span> |  
| <span data-ttu-id="4587d-284">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="4587d-284">**Applicable Technologies**</span></span> | <span data-ttu-id="4587d-285">Универсальный</span><span class="sxs-lookup"><span data-stu-id="4587d-285">Generic</span></span> |
| <span data-ttu-id="4587d-286">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="4587d-286">**Attributes**</span></span>              | <span data-ttu-id="4587d-287">Недоступно</span><span class="sxs-lookup"><span data-stu-id="4587d-287">N/A</span></span>  |
| <span data-ttu-id="4587d-288">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="4587d-288">**References**</span></span>              | [<span data-ttu-id="4587d-289">Безопасная обработка ошибок</span><span class="sxs-lookup"><span data-stu-id="4587d-289">Fail securely</span></span>](https://www.owasp.org/index.php/Fail_securely) |
| <span data-ttu-id="4587d-290">**Действия**</span><span class="sxs-lookup"><span data-stu-id="4587d-290">**Steps**</span></span> | <span data-ttu-id="4587d-291">Приложение должно безопасно обрабатывать ошибки.</span><span class="sxs-lookup"><span data-stu-id="4587d-291">Application should fail safely.</span></span> <span data-ttu-id="4587d-292">Любой метод, возвращающий логическое значение, в зависимости от принятого решения, должен содержать тщательно созданный блок исключений.</span><span class="sxs-lookup"><span data-stu-id="4587d-292">Any method that returns a Boolean value, based on which certain decision is made, should have exception block carefully created.</span></span> <span data-ttu-id="4587d-293">Существует большое число логических ошибок из-за toowhich смещения проблемы безопасности в при записи блока исключений hello высока.</span><span class="sxs-lookup"><span data-stu-id="4587d-293">There are lot of logical errors due toowhich security issues creep in, when hello exception block is written carelessly.</span></span>|

### <a name="example"></a><span data-ttu-id="4587d-294">Пример</span><span class="sxs-lookup"><span data-stu-id="4587d-294">Example</span></span>
```C#
        public static bool ValidateDomain(string pathToValidate, Uri currentUrl)
        {
            try
            {
                if (!string.IsNullOrWhiteSpace(pathToValidate))
                {
                    var domain = RetrieveDomain(currentUrl);
                    var replyPath = new Uri(pathToValidate);
                    var replyDomain = RetrieveDomain(replyPath);

                    if (string.Compare(domain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                    {
                        //// Adding additional check tooenable CMS urls if they are not hosted on same domain.
                        if (!string.IsNullOrWhiteSpace(Utilities.CmsBase))
                        {
                            var cmsDomain = RetrieveDomain(new Uri(Utilities.Base.Trim()));
                            if (string.Compare(cmDomain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                            {
                                return false;
                            }
                            else
                            {
                                return true;
                            }
                        }

                        return false;
                    }
                }

                return true;
            }
            catch (UriFormatException ex)
            {
                LogHelper.LogException("Utilities:ValidateDomain", ex);
                return true;
            }
        }
```
<span data-ttu-id="4587d-295">Hello выше метод всегда возвращает значение True, если произошло исключение.</span><span class="sxs-lookup"><span data-stu-id="4587d-295">hello above method will always return True, if some exception happens.</span></span> <span data-ttu-id="4587d-296">Если hello конечный пользователь вводит неверный URL-адрес, где hello отношениях браузера, но hello `Uri()` конструктор не, то будет создано исключение и жертвы hello будут выполнены toohello допустимо, но имеет неправильный формат URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="4587d-296">If hello end user provides a malformed URL, that hello browser respects, but hello `Uri()` constructor doesn't, this will throw an exception, and hello victim will be taken toohello valid but malformed URL.</span></span> 
