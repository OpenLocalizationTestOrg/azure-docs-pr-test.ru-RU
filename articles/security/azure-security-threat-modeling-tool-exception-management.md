---
title: "Управление исключениями. Средство моделирования угроз Microsoft Azure | Документация Майкрософт"
description: "Устранение угроз, обнаруженных с помощью средства моделирования угроз"
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
ms.openlocfilehash: bbf357b902474a1812eb7a5a2c914d0c8b91934b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="security-frame-exception-management--mitigations"></a><span data-ttu-id="7001a-103">Механизм безопасности. Управление исключениями | Устранение угроз</span><span class="sxs-lookup"><span data-stu-id="7001a-103">Security Frame: Exception Management | Mitigations</span></span> 
| <span data-ttu-id="7001a-104">Продукт или служба</span><span class="sxs-lookup"><span data-stu-id="7001a-104">Product/Service</span></span> | <span data-ttu-id="7001a-105">Статья</span><span class="sxs-lookup"><span data-stu-id="7001a-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="7001a-106">**WCF**</span><span class="sxs-lookup"><span data-stu-id="7001a-106">**WCF**</span></span> | <ul><li>[<span data-ttu-id="7001a-107">WCF — не добавляйте узел serviceDebug в файл конфигурации</span><span class="sxs-lookup"><span data-stu-id="7001a-107">WCF- Do not include serviceDebug node in configuration file</span></span>](#servicedebug)</li><li>[<span data-ttu-id="7001a-108">WCF — не добавляйте узел serviceMetadata в файл конфигурации</span><span class="sxs-lookup"><span data-stu-id="7001a-108">WCF- Do not include serviceMetadata node in configuration file</span></span>](#servicemetadata)</li></ul> |
| <span data-ttu-id="7001a-109">**Веб-интерфейс API**</span><span class="sxs-lookup"><span data-stu-id="7001a-109">**Web API**</span></span> | <ul><li>[<span data-ttu-id="7001a-110">Обеспечьте правильную обработку исключений в веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7001a-110">Ensure that proper exception handling is done in ASP.NET Web API </span></span>](#exception)</li></ul> |
| <span data-ttu-id="7001a-111">**Веб-приложение**</span><span class="sxs-lookup"><span data-stu-id="7001a-111">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="7001a-112">Не раскрывайте сведения о безопасности в сообщениях об ошибках</span><span class="sxs-lookup"><span data-stu-id="7001a-112">Do not expose security details in error messages </span></span>](#messages)</li><li>[<span data-ttu-id="7001a-113">Реализуйте страницу обработки ошибок по умолчанию</span><span class="sxs-lookup"><span data-stu-id="7001a-113">Implement Default error handling page </span></span>](#default)</li><li>[<span data-ttu-id="7001a-114">Настройте метод развертывания retail в IIS</span><span class="sxs-lookup"><span data-stu-id="7001a-114">Set Deployment Method to Retail in IIS</span></span>](#deployment)</li><li>[<span data-ttu-id="7001a-115">Обеспечьте безопасную обработку исключений</span><span class="sxs-lookup"><span data-stu-id="7001a-115">Exceptions should fail safely</span></span>](#fail)</li></ul> |

## <span data-ttu-id="7001a-116"><a id="servicedebug"></a>WCF — не добавляйте узел serviceDebug в файл конфигурации</span><span class="sxs-lookup"><span data-stu-id="7001a-116"><a id="servicedebug"></a>WCF- Do not include serviceDebug node in configuration file</span></span>

| <span data-ttu-id="7001a-117">Название</span><span class="sxs-lookup"><span data-stu-id="7001a-117">Title</span></span>                   | <span data-ttu-id="7001a-118">Сведения</span><span class="sxs-lookup"><span data-stu-id="7001a-118">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7001a-119">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="7001a-119">**Component**</span></span>               | <span data-ttu-id="7001a-120">WCF</span><span class="sxs-lookup"><span data-stu-id="7001a-120">WCF</span></span> | 
| <span data-ttu-id="7001a-121">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="7001a-121">**SDL Phase**</span></span>               | <span data-ttu-id="7001a-122">Создание</span><span class="sxs-lookup"><span data-stu-id="7001a-122">Build</span></span> |  
| <span data-ttu-id="7001a-123">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="7001a-123">**Applicable Technologies**</span></span> | <span data-ttu-id="7001a-124">Универсальные, .NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="7001a-124">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="7001a-125">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="7001a-125">**Attributes**</span></span>              | <span data-ttu-id="7001a-126">Недоступно</span><span class="sxs-lookup"><span data-stu-id="7001a-126">N/A</span></span>  |
| <span data-ttu-id="7001a-127">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="7001a-127">**References**</span></span>              | <span data-ttu-id="7001a-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="7001a-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="7001a-129">**Действия**</span><span class="sxs-lookup"><span data-stu-id="7001a-129">**Steps**</span></span> | <span data-ttu-id="7001a-130">Службы Windows Communication Framework (WCF) можно настроить для предоставления отладочной информации.</span><span class="sxs-lookup"><span data-stu-id="7001a-130">Windows Communication Framework (WCF) services can be configured to expose debugging information.</span></span> <span data-ttu-id="7001a-131">Отладочную информацию не следует использовать в рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="7001a-131">Debug information should not be used in production environments.</span></span> <span data-ttu-id="7001a-132">Тег `<serviceDebug>` определяет, включена ли функция отладочной информации для службы WCF.</span><span class="sxs-lookup"><span data-stu-id="7001a-132">The `<serviceDebug>` tag defines whether the debug information feature is enabled for a WCF service.</span></span> <span data-ttu-id="7001a-133">Если атрибуту includeExceptionDetailInFaults присвоено значение true, клиентам будут возвращены сведения об исключении из приложения.</span><span class="sxs-lookup"><span data-stu-id="7001a-133">If the attribute includeExceptionDetailInFaults is set to true, exception information from the application will be returned to clients.</span></span> <span data-ttu-id="7001a-134">Злоумышленники могут использовать дополнительные сведения, полученные из результатов отладки, для совершения целенаправленных атак на платформу, базу данных или другие ресурсы, используемые приложением.</span><span class="sxs-lookup"><span data-stu-id="7001a-134">Attackers can leverage the additional information they gain from debugging output to mount attacks targeted on the framework, database, or other resources used by the application.</span></span> |

### <a name="example"></a><span data-ttu-id="7001a-135">Пример</span><span class="sxs-lookup"><span data-stu-id="7001a-135">Example</span></span>
<span data-ttu-id="7001a-136">Следующий файл конфигурации содержит тег `<serviceDebug>`:</span><span class="sxs-lookup"><span data-stu-id="7001a-136">The following configuration file includes the `<serviceDebug>` tag:</span></span> 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
<span data-ttu-id="7001a-137">Отключите отладочную информацию в службе.</span><span class="sxs-lookup"><span data-stu-id="7001a-137">Disable debugging information in the service.</span></span> <span data-ttu-id="7001a-138">Это можно сделать, удалив тег `<serviceDebug>` в файле конфигурации приложения.</span><span class="sxs-lookup"><span data-stu-id="7001a-138">This can be accomplished by removing the `<serviceDebug>` tag from your application's configuration file.</span></span> 

## <span data-ttu-id="7001a-139"><a id="servicemetadata"></a>WCF — не добавляйте узел serviceMetadata в файл конфигурации</span><span class="sxs-lookup"><span data-stu-id="7001a-139"><a id="servicemetadata"></a>WCF- Do not include serviceMetadata node in configuration file</span></span>

| <span data-ttu-id="7001a-140">Название</span><span class="sxs-lookup"><span data-stu-id="7001a-140">Title</span></span>                   | <span data-ttu-id="7001a-141">Сведения</span><span class="sxs-lookup"><span data-stu-id="7001a-141">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7001a-142">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="7001a-142">**Component**</span></span>               | <span data-ttu-id="7001a-143">WCF</span><span class="sxs-lookup"><span data-stu-id="7001a-143">WCF</span></span> | 
| <span data-ttu-id="7001a-144">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="7001a-144">**SDL Phase**</span></span>               | <span data-ttu-id="7001a-145">Создание</span><span class="sxs-lookup"><span data-stu-id="7001a-145">Build</span></span> |  
| <span data-ttu-id="7001a-146">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="7001a-146">**Applicable Technologies**</span></span> | <span data-ttu-id="7001a-147">Универсальный</span><span class="sxs-lookup"><span data-stu-id="7001a-147">Generic</span></span> |
| <span data-ttu-id="7001a-148">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="7001a-148">**Attributes**</span></span>              | <span data-ttu-id="7001a-149">Универсальные, .NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="7001a-149">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="7001a-150">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="7001a-150">**References**</span></span>              | <span data-ttu-id="7001a-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="7001a-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="7001a-152">**Действия**</span><span class="sxs-lookup"><span data-stu-id="7001a-152">**Steps**</span></span> | <span data-ttu-id="7001a-153">В случае публичного раскрытия информации о службе злоумышленники могут получить ценные сведения о том, как ее можно использовать в своих целях.</span><span class="sxs-lookup"><span data-stu-id="7001a-153">Publicly exposing information about a service can provide attackers with valuable insight into how they might exploit the service.</span></span> <span data-ttu-id="7001a-154">Тег `<serviceMetadata>` включает функцию публикации метаданных.</span><span class="sxs-lookup"><span data-stu-id="7001a-154">The `<serviceMetadata>` tag enables the metadata publishing feature.</span></span> <span data-ttu-id="7001a-155">Метаданные службы могут содержать конфиденциальные сведения, к которым нельзя предоставлять общий доступ.</span><span class="sxs-lookup"><span data-stu-id="7001a-155">Service metadata could contain sensitive information that should not be publicly accessible.</span></span> <span data-ttu-id="7001a-156">Как минимум доступ к метаданным следует разрешать только доверенным пользователям, а также необходимо гарантировать, что ненужная информация не предоставляется.</span><span class="sxs-lookup"><span data-stu-id="7001a-156">At a minimum, only allow trusted users to access the metadata and ensure that unnecessary information is not exposed.</span></span> <span data-ttu-id="7001a-157">А еще лучше полностью отключите возможность публикации метаданных.</span><span class="sxs-lookup"><span data-stu-id="7001a-157">Better yet, entirely disable the ability to publish metadata.</span></span> <span data-ttu-id="7001a-158">Безопасная конфигурация WCF не будет содержать тег `<serviceMetadata>`.</span><span class="sxs-lookup"><span data-stu-id="7001a-158">A safe WCF configuration will not contain the `<serviceMetadata>` tag.</span></span> |

## <span data-ttu-id="7001a-159"><a id="exception"></a>Обеспечьте правильную обработку исключений в веб-API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7001a-159"><a id="exception"></a>Ensure that proper exception handling is done in ASP.NET Web API</span></span>

| <span data-ttu-id="7001a-160">Название</span><span class="sxs-lookup"><span data-stu-id="7001a-160">Title</span></span>                   | <span data-ttu-id="7001a-161">Сведения</span><span class="sxs-lookup"><span data-stu-id="7001a-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7001a-162">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="7001a-162">**Component**</span></span>               | <span data-ttu-id="7001a-163">Веб-интерфейс API</span><span class="sxs-lookup"><span data-stu-id="7001a-163">Web API</span></span> | 
| <span data-ttu-id="7001a-164">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="7001a-164">**SDL Phase**</span></span>               | <span data-ttu-id="7001a-165">Создание</span><span class="sxs-lookup"><span data-stu-id="7001a-165">Build</span></span> |  
| <span data-ttu-id="7001a-166">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="7001a-166">**Applicable Technologies**</span></span> | <span data-ttu-id="7001a-167">MVC 5, MVC 6</span><span class="sxs-lookup"><span data-stu-id="7001a-167">MVC 5, MVC 6</span></span> |
| <span data-ttu-id="7001a-168">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="7001a-168">**Attributes**</span></span>              | <span data-ttu-id="7001a-169">Недоступно</span><span class="sxs-lookup"><span data-stu-id="7001a-169">N/A</span></span>  |
| <span data-ttu-id="7001a-170">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="7001a-170">**References**</span></span>              | <span data-ttu-id="7001a-171">[Обработка исключений в веб-API ASP.NET](http://www.asp.net/web-api/overview/error-handling/exception-handling), [проверка модели в веб-API ASP.NET](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span><span class="sxs-lookup"><span data-stu-id="7001a-171">[Exception Handling in ASP.NET Web API](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Model Validation in ASP.NET Web API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span></span> |
| <span data-ttu-id="7001a-172">**Действия**</span><span class="sxs-lookup"><span data-stu-id="7001a-172">**Steps**</span></span> | <span data-ttu-id="7001a-173">По умолчанию большинство неперехваченных исключений в веб-API ASP.NET преобразовываются в HTTP-ответ с кодом состояния `500, Internal Server Error`.</span><span class="sxs-lookup"><span data-stu-id="7001a-173">By default, most uncaught exceptions in ASP.NET Web API are translated into an HTTP response with status code `500, Internal Server Error`</span></span>|

### <a name="example"></a><span data-ttu-id="7001a-174">Пример</span><span class="sxs-lookup"><span data-stu-id="7001a-174">Example</span></span>
<span data-ttu-id="7001a-175">Для управления кодом состояния, возвращенным API, можно использовать `HttpResponseException`, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="7001a-175">To control the status code returned by the API, `HttpResponseException` can be used as shown below:</span></span> 
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

### <a name="example"></a><span data-ttu-id="7001a-176">Пример</span><span class="sxs-lookup"><span data-stu-id="7001a-176">Example</span></span>
<span data-ttu-id="7001a-177">Для дальнейшего управления ответом исключения можно использовать класс `HttpResponseMessage`, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="7001a-177">For further control on the exception response, the `HttpResponseMessage` class can be used as shown below:</span></span> 
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
<span data-ttu-id="7001a-178">Чтобы перехватить необработанные исключения, которые не относятся к типу `HttpResponseException`, можно использовать фильтры исключений.</span><span class="sxs-lookup"><span data-stu-id="7001a-178">To catch unhandled exceptions that are not of the type `HttpResponseException`, Exception Filters can be used.</span></span> <span data-ttu-id="7001a-179">Они реализовывают интерфейс `System.Web.Http.Filters.IExceptionFilter`.</span><span class="sxs-lookup"><span data-stu-id="7001a-179">Exception filters implement the `System.Web.Http.Filters.IExceptionFilter` interface.</span></span> <span data-ttu-id="7001a-180">Самый простой способ создать фильтр исключений — использовать класс `System.Web.Http.Filters.ExceptionFilterAttribute` и переопределить метод OnException.</span><span class="sxs-lookup"><span data-stu-id="7001a-180">The simplest way to write an exception filter is to derive from the `System.Web.Http.Filters.ExceptionFilterAttribute` class and override the OnException method.</span></span> 

### <a name="example"></a><span data-ttu-id="7001a-181">Пример</span><span class="sxs-lookup"><span data-stu-id="7001a-181">Example</span></span>
<span data-ttu-id="7001a-182">Ниже приведен фильтр, который преобразует исключения `NotImplementedException` в код состояния HTTP `501, Not Implemented`.</span><span class="sxs-lookup"><span data-stu-id="7001a-182">Here is a filter that converts `NotImplementedException` exceptions into HTTP status code `501, Not Implemented`:</span></span> 
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

<span data-ttu-id="7001a-183">Существует несколько способов регистрации фильтра исключений веб-API:</span><span class="sxs-lookup"><span data-stu-id="7001a-183">There are several ways to register a Web API exception filter:</span></span>
- <span data-ttu-id="7001a-184">Для действия</span><span class="sxs-lookup"><span data-stu-id="7001a-184">By action</span></span>
- <span data-ttu-id="7001a-185">Для контроллера</span><span class="sxs-lookup"><span data-stu-id="7001a-185">By controller</span></span>
- <span data-ttu-id="7001a-186">Глобально</span><span class="sxs-lookup"><span data-stu-id="7001a-186">Globally</span></span>

### <a name="example"></a><span data-ttu-id="7001a-187">Пример</span><span class="sxs-lookup"><span data-stu-id="7001a-187">Example</span></span>
<span data-ttu-id="7001a-188">Чтобы применить фильтр к определенному действию, добавьте его в качестве атрибута в действие:</span><span class="sxs-lookup"><span data-stu-id="7001a-188">To apply the filter to a specific action, add the filter as an attribute to the action:</span></span> 
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
### <a name="example"></a><span data-ttu-id="7001a-189">Пример</span><span class="sxs-lookup"><span data-stu-id="7001a-189">Example</span></span>
<span data-ttu-id="7001a-190">Чтобы применить фильтр ко всем действиям в `controller`, добавьте его в качестве атрибута в класс `controller`:</span><span class="sxs-lookup"><span data-stu-id="7001a-190">To apply the filter to all of the actions on a `controller`, add the filter as an attribute to the `controller` class:</span></span> 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a><span data-ttu-id="7001a-191">Пример</span><span class="sxs-lookup"><span data-stu-id="7001a-191">Example</span></span>
<span data-ttu-id="7001a-192">Чтобы применить фильтр ко всем контроллерам веб-API глобально, добавьте экземпляр фильтра в коллекцию `GlobalConfiguration.Configuration.Filters`.</span><span class="sxs-lookup"><span data-stu-id="7001a-192">To apply the filter globally to all Web API controllers, add an instance of the filter to the `GlobalConfiguration.Configuration.Filters` collection.</span></span> <span data-ttu-id="7001a-193">В этой коллекции фильтры исключений применяются к любому действию контроллера веб-API.</span><span class="sxs-lookup"><span data-stu-id="7001a-193">Exception filters in this collection apply to any Web API controller action.</span></span> 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a><span data-ttu-id="7001a-194">Пример</span><span class="sxs-lookup"><span data-stu-id="7001a-194">Example</span></span>
<span data-ttu-id="7001a-195">Для проверки модели можно настроить передачу состояния модели методу CreateErrorResponse, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="7001a-195">For model validation, the model state can be passed to CreateErrorResponse method as shown below:</span></span> 
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

<span data-ttu-id="7001a-196">Просмотрите ссылки в разделе справочных сведений, чтобы получить дополнительные сведения об обработке исключений и проверке модели в веб-API ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="7001a-196">Check the links in the references section for additional details about exceptional handling and model validation in ASP.Net Web API</span></span> 

## <span data-ttu-id="7001a-197"><a id="messages"></a>Не раскрывайте сведения о безопасности в сообщениях об ошибках</span><span class="sxs-lookup"><span data-stu-id="7001a-197"><a id="messages"></a>Do not expose security details in error messages</span></span>

| <span data-ttu-id="7001a-198">Название</span><span class="sxs-lookup"><span data-stu-id="7001a-198">Title</span></span>                   | <span data-ttu-id="7001a-199">Сведения</span><span class="sxs-lookup"><span data-stu-id="7001a-199">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7001a-200">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="7001a-200">**Component**</span></span>               | <span data-ttu-id="7001a-201">Веб-приложение</span><span class="sxs-lookup"><span data-stu-id="7001a-201">Web Application</span></span> | 
| <span data-ttu-id="7001a-202">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="7001a-202">**SDL Phase**</span></span>               | <span data-ttu-id="7001a-203">Создание</span><span class="sxs-lookup"><span data-stu-id="7001a-203">Build</span></span> |  
| <span data-ttu-id="7001a-204">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="7001a-204">**Applicable Technologies**</span></span> | <span data-ttu-id="7001a-205">Универсальный</span><span class="sxs-lookup"><span data-stu-id="7001a-205">Generic</span></span> |
| <span data-ttu-id="7001a-206">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="7001a-206">**Attributes**</span></span>              | <span data-ttu-id="7001a-207">Недоступно</span><span class="sxs-lookup"><span data-stu-id="7001a-207">N/A</span></span>  |
| <span data-ttu-id="7001a-208">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="7001a-208">**References**</span></span>              | <span data-ttu-id="7001a-209">Недоступно</span><span class="sxs-lookup"><span data-stu-id="7001a-209">N/A</span></span>  |
| <span data-ttu-id="7001a-210">**Действия**</span><span class="sxs-lookup"><span data-stu-id="7001a-210">**Steps**</span></span> | <p><span data-ttu-id="7001a-211">Общие сообщения об ошибках предоставляются непосредственно пользователю и не содержат конфиденциальные данные приложения.</span><span class="sxs-lookup"><span data-stu-id="7001a-211">Generic error messages are provided directly to the user without including sensitive application data.</span></span> <span data-ttu-id="7001a-212">К конфиденциальным данным относятся:</span><span class="sxs-lookup"><span data-stu-id="7001a-212">Examples of sensitive data include:</span></span></p><ul><li><span data-ttu-id="7001a-213">имена серверов;</span><span class="sxs-lookup"><span data-stu-id="7001a-213">Server names</span></span></li><li><span data-ttu-id="7001a-214">Строки подключения</span><span class="sxs-lookup"><span data-stu-id="7001a-214">Connection strings</span></span></li><li><span data-ttu-id="7001a-215">имена пользователей;</span><span class="sxs-lookup"><span data-stu-id="7001a-215">Usernames</span></span></li><li><span data-ttu-id="7001a-216">Пароли</span><span class="sxs-lookup"><span data-stu-id="7001a-216">Passwords</span></span></li><li><span data-ttu-id="7001a-217">процедуры SQL;</span><span class="sxs-lookup"><span data-stu-id="7001a-217">SQL procedures</span></span></li><li><span data-ttu-id="7001a-218">подробные сведения о динамических ошибках SQL;</span><span class="sxs-lookup"><span data-stu-id="7001a-218">Details of dynamic SQL failures</span></span></li><li><span data-ttu-id="7001a-219">трассировка стека и строки кода;</span><span class="sxs-lookup"><span data-stu-id="7001a-219">Stack trace and lines of code</span></span></li><li><span data-ttu-id="7001a-220">переменные, хранимые в памяти;</span><span class="sxs-lookup"><span data-stu-id="7001a-220">Variables stored in memory</span></span></li><li><span data-ttu-id="7001a-221">расположения дисков и папок;</span><span class="sxs-lookup"><span data-stu-id="7001a-221">Drive and folder locations</span></span></li><li><span data-ttu-id="7001a-222">точки установки приложения;</span><span class="sxs-lookup"><span data-stu-id="7001a-222">Application install points</span></span></li><li><span data-ttu-id="7001a-223">параметры конфигурации узла;</span><span class="sxs-lookup"><span data-stu-id="7001a-223">Host configuration settings</span></span></li><li><span data-ttu-id="7001a-224">другие внутренние сведения о приложении.</span><span class="sxs-lookup"><span data-stu-id="7001a-224">Other internal application details</span></span></li></ul><p><span data-ttu-id="7001a-225">Перехват всех ошибок в приложении и предоставление общих сообщений об ошибках, а также включение пользовательских ошибок в службах IIS позволяют предотвратить раскрытие информации.</span><span class="sxs-lookup"><span data-stu-id="7001a-225">Trapping all errors within an application and providing generic error messages, as well as enabling custom errors within IIS will help prevent information disclosure.</span></span> <span data-ttu-id="7001a-226">Для пользователя-злоумышленника обработка исключений .NET и базы данных SQL Server, помимо других архитектур обработки ошибок, является чрезвычайно подробной и полезной при профилировании приложения.</span><span class="sxs-lookup"><span data-stu-id="7001a-226">SQL Server database and .NET Exception handling, among other error handling architectures, are especially verbose and extremely useful to a malicious user profiling your application.</span></span> <span data-ttu-id="7001a-227">Не отображайте напрямую содержимое класса, производного от класса исключений .NET, и настройте правильную обработку исключений, чтобы непредвиденное исключение случайно не было отправлено непосредственно пользователю.</span><span class="sxs-lookup"><span data-stu-id="7001a-227">Do not directly display the contents of a class derived from the .NET Exception class, and ensure that you have proper exception handling so that an unexpected exception isn't inadvertently raised directly to the user.</span></span></p><ul><li><span data-ttu-id="7001a-228">Предоставляйте общие сообщения об ошибках напрямую пользователю, который абстрагирует подробные сведения, находящиеся непосредственно в сообщении об ошибке или исключении.</span><span class="sxs-lookup"><span data-stu-id="7001a-228">Provide generic error messages directly to the user that abstract away specific details found directly in the exception/error message</span></span></li><li><span data-ttu-id="7001a-229">Не отображайте содержимое класса исключений .NET непосредственно пользователю.</span><span class="sxs-lookup"><span data-stu-id="7001a-229">Do not display the contents of a .NET exception class directly to the user</span></span></li><li><span data-ttu-id="7001a-230">Перехватывайте все сообщения об ошибках и при необходимости оповещайте пользователя с помощью общего сообщения об ошибке, отправленного клиенту приложения.</span><span class="sxs-lookup"><span data-stu-id="7001a-230">Trap all error messages and if appropriate inform the user via a generic error message sent to the application client</span></span></li><li><span data-ttu-id="7001a-231">Не предоставляйте содержимое класса исключений непосредственно пользователю, особенно значение, возвращаемое `.ToString()`, а также значения свойств сообщения или трассировки стека.</span><span class="sxs-lookup"><span data-stu-id="7001a-231">Do not expose the contents of the Exception class directly to the user, especially the return value from `.ToString()`, or the values of the Message or StackTrace properties.</span></span> <span data-ttu-id="7001a-232">Безопасно записывайте эти сведения в журнал и отображайте сообщение без конфиденциальных сведений для пользователя.</span><span class="sxs-lookup"><span data-stu-id="7001a-232">Securely log this information and display a more innocuous message to the user</span></span></li></ul>|

## <span data-ttu-id="7001a-233"><a id="default"></a>Реализуйте страницу обработки ошибок по умолчанию</span><span class="sxs-lookup"><span data-stu-id="7001a-233"><a id="default"></a>Implement Default error handling page</span></span>

| <span data-ttu-id="7001a-234">Название</span><span class="sxs-lookup"><span data-stu-id="7001a-234">Title</span></span>                   | <span data-ttu-id="7001a-235">Сведения</span><span class="sxs-lookup"><span data-stu-id="7001a-235">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7001a-236">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="7001a-236">**Component**</span></span>               | <span data-ttu-id="7001a-237">Веб-приложение</span><span class="sxs-lookup"><span data-stu-id="7001a-237">Web Application</span></span> | 
| <span data-ttu-id="7001a-238">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="7001a-238">**SDL Phase**</span></span>               | <span data-ttu-id="7001a-239">Создание</span><span class="sxs-lookup"><span data-stu-id="7001a-239">Build</span></span> |  
| <span data-ttu-id="7001a-240">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="7001a-240">**Applicable Technologies**</span></span> | <span data-ttu-id="7001a-241">Универсальный</span><span class="sxs-lookup"><span data-stu-id="7001a-241">Generic</span></span> |
| <span data-ttu-id="7001a-242">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="7001a-242">**Attributes**</span></span>              | <span data-ttu-id="7001a-243">Недоступно</span><span class="sxs-lookup"><span data-stu-id="7001a-243">N/A</span></span>  |
| <span data-ttu-id="7001a-244">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="7001a-244">**References**</span></span>              | <span data-ttu-id="7001a-245">[Сведения о диалоговом окне изменения параметров страниц ошибок ASP.NET](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="7001a-245">[Edit ASP.NET Error Pages Settings Dialog Box](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span></span> |
| <span data-ttu-id="7001a-246">**Действия**</span><span class="sxs-lookup"><span data-stu-id="7001a-246">**Steps**</span></span> | <p><span data-ttu-id="7001a-247">Если приложение ASP.NET перестает работать и приводит к возникновению ошибки "HTTP/1.x 500 — внутренняя ошибка сервера" или конфигурация компонентов (например, фильтрация запросов) предотвращает отображение страницы, создается сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="7001a-247">When an ASP.NET application fails and causes an HTTP/1.x 500 Internal Server Error, or a feature configuration (such as Request Filtering) prevents a page from being displayed, an error message will be generated.</span></span> <span data-ttu-id="7001a-248">Администраторы могут выбрать, следует ли приложению отображать понятное сообщение клиенту, подробное сообщение об ошибке клиенту или подробное сообщение только на локальном узле.</span><span class="sxs-lookup"><span data-stu-id="7001a-248">Administrators can choose whether or not the application should display a friendly message to the client, detailed error message to the client, or detailed error message to localhost only.</span></span> <span data-ttu-id="7001a-249">Тег <customErrors> в файле web.config имеет три режима:</span><span class="sxs-lookup"><span data-stu-id="7001a-249">The <customErrors> tag in the web.config has three modes:</span></span></p><ul><li><span data-ttu-id="7001a-250">**On.** Указывает, что пользовательские ошибки включены.</span><span class="sxs-lookup"><span data-stu-id="7001a-250">**On:** Specifies that custom errors are enabled.</span></span> <span data-ttu-id="7001a-251">Если атрибут defaultRedirect не указан, для пользователей отобразится общая ошибка.</span><span class="sxs-lookup"><span data-stu-id="7001a-251">If no defaultRedirect attribute is specified, users see a generic error.</span></span> <span data-ttu-id="7001a-252">Пользовательские ошибки отображаются для удаленных клиентов и на локальном узле.</span><span class="sxs-lookup"><span data-stu-id="7001a-252">The custom errors are shown to the remote clients and to the local host</span></span></li><li><span data-ttu-id="7001a-253">**Off.** Указывает, что пользовательские ошибки выключены.</span><span class="sxs-lookup"><span data-stu-id="7001a-253">**Off:** Specifies that custom errors are disabled.</span></span> <span data-ttu-id="7001a-254">Подробные ошибки ASP.NET отображаются для удаленных клиентов и на локальном узле.</span><span class="sxs-lookup"><span data-stu-id="7001a-254">The detailed ASP.NET errors are shown to the remote clients and to the local host</span></span></li><li><span data-ttu-id="7001a-255">**RemoteOnly.** Указывает, что пользовательские ошибки отображаются только для удаленных клиентов, а также что ошибки ASP.NET отображаются на локальном узле.</span><span class="sxs-lookup"><span data-stu-id="7001a-255">**RemoteOnly:** Specifies that custom errors are shown only to the remote clients, and that ASP.NET errors are shown to the local host.</span></span> <span data-ttu-id="7001a-256">Это значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="7001a-256">This is the default value</span></span></li></ul><p><span data-ttu-id="7001a-257">Откройте файл `web.config` для приложения или сайта и убедитесь, что для тега определен либо режим `<customErrors mode="RemoteOnly" />`, либо `<customErrors mode="On" />`.</span><span class="sxs-lookup"><span data-stu-id="7001a-257">Open the `web.config` file for the application/site and ensure that the tag has either `<customErrors mode="RemoteOnly" />` or `<customErrors mode="On" />` defined.</span></span></p>|

## <span data-ttu-id="7001a-258"><a id="deployment"></a>Настройте метод развертывания retail в IIS</span><span class="sxs-lookup"><span data-stu-id="7001a-258"><a id="deployment"></a>Set Deployment Method to Retail in IIS</span></span>

| <span data-ttu-id="7001a-259">Название</span><span class="sxs-lookup"><span data-stu-id="7001a-259">Title</span></span>                   | <span data-ttu-id="7001a-260">Сведения</span><span class="sxs-lookup"><span data-stu-id="7001a-260">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7001a-261">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="7001a-261">**Component**</span></span>               | <span data-ttu-id="7001a-262">Веб-приложение</span><span class="sxs-lookup"><span data-stu-id="7001a-262">Web Application</span></span> | 
| <span data-ttu-id="7001a-263">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="7001a-263">**SDL Phase**</span></span>               | <span data-ttu-id="7001a-264">Развертывание</span><span class="sxs-lookup"><span data-stu-id="7001a-264">Deployment</span></span> |  
| <span data-ttu-id="7001a-265">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="7001a-265">**Applicable Technologies**</span></span> | <span data-ttu-id="7001a-266">Универсальный</span><span class="sxs-lookup"><span data-stu-id="7001a-266">Generic</span></span> |
| <span data-ttu-id="7001a-267">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="7001a-267">**Attributes**</span></span>              | <span data-ttu-id="7001a-268">Недоступно</span><span class="sxs-lookup"><span data-stu-id="7001a-268">N/A</span></span>  |
| <span data-ttu-id="7001a-269">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="7001a-269">**References**</span></span>              | <span data-ttu-id="7001a-270">[Элемент deployment (схема параметров ASP.NET)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span><span class="sxs-lookup"><span data-stu-id="7001a-270">[deployment Element (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span></span> |
| <span data-ttu-id="7001a-271">**Действия**</span><span class="sxs-lookup"><span data-stu-id="7001a-271">**Steps**</span></span> | <p><span data-ttu-id="7001a-272">Параметр `<deployment retail>` предназначен для использования рабочими серверами IIS.</span><span class="sxs-lookup"><span data-stu-id="7001a-272">The `<deployment retail>` switch is intended for use by production IIS servers.</span></span> <span data-ttu-id="7001a-273">Он используется для выполнения приложений с максимальной производительностью и минимальной утечкой сведений о безопасности. Это возможно благодаря исключению возможностей приложения создавать выходные данные трассировки на странице, отображать подробные сообщения об ошибках для конечных пользователей и отключать параметр отладки.</span><span class="sxs-lookup"><span data-stu-id="7001a-273">This switch is used to help applications run with the best possible performance and least possible security information leakages by disabling the application's ability to generate trace output on a page, disabling the ability to display detailed error messages to end users, and disabling the debug switch.</span></span></p><p><span data-ttu-id="7001a-274">Зачастую параметры, предназначенные для разработчиков, например трассировка и отладка неудачно завершенных запросов, включаются во время активной разработки.</span><span class="sxs-lookup"><span data-stu-id="7001a-274">Often times, switches and options that are developer-focused, such as failed request tracing and debugging, are enabled during active development.</span></span> <span data-ttu-id="7001a-275">Мы советуем настроить метод развертывания retail для любого рабочего сервера.</span><span class="sxs-lookup"><span data-stu-id="7001a-275">It is recommended that the deployment method on any production server be set to retail.</span></span> <span data-ttu-id="7001a-276">Откройте файл machine.config и убедитесь, что параметру `<deployment retail="true" />` присвоено значение true.</span><span class="sxs-lookup"><span data-stu-id="7001a-276">open the machine.config file and ensure that `<deployment retail="true" />` remains set to true.</span></span></p>|

## <span data-ttu-id="7001a-277"><a id="fail"></a>Обеспечьте безопасную обработку исключений</span><span class="sxs-lookup"><span data-stu-id="7001a-277"><a id="fail"></a>Exceptions should fail safely</span></span>

| <span data-ttu-id="7001a-278">Название</span><span class="sxs-lookup"><span data-stu-id="7001a-278">Title</span></span>                   | <span data-ttu-id="7001a-279">Сведения</span><span class="sxs-lookup"><span data-stu-id="7001a-279">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="7001a-280">**Компонент**</span><span class="sxs-lookup"><span data-stu-id="7001a-280">**Component**</span></span>               | <span data-ttu-id="7001a-281">Веб-приложение</span><span class="sxs-lookup"><span data-stu-id="7001a-281">Web Application</span></span> | 
| <span data-ttu-id="7001a-282">**Этап SDL**</span><span class="sxs-lookup"><span data-stu-id="7001a-282">**SDL Phase**</span></span>               | <span data-ttu-id="7001a-283">Создание</span><span class="sxs-lookup"><span data-stu-id="7001a-283">Build</span></span> |  
| <span data-ttu-id="7001a-284">**Применимые технологии**</span><span class="sxs-lookup"><span data-stu-id="7001a-284">**Applicable Technologies**</span></span> | <span data-ttu-id="7001a-285">Универсальный</span><span class="sxs-lookup"><span data-stu-id="7001a-285">Generic</span></span> |
| <span data-ttu-id="7001a-286">**Атрибуты**</span><span class="sxs-lookup"><span data-stu-id="7001a-286">**Attributes**</span></span>              | <span data-ttu-id="7001a-287">Недоступно</span><span class="sxs-lookup"><span data-stu-id="7001a-287">N/A</span></span>  |
| <span data-ttu-id="7001a-288">**Справочные материалы**</span><span class="sxs-lookup"><span data-stu-id="7001a-288">**References**</span></span>              | [<span data-ttu-id="7001a-289">Безопасная обработка ошибок</span><span class="sxs-lookup"><span data-stu-id="7001a-289">Fail securely</span></span>](https://www.owasp.org/index.php/Fail_securely) |
| <span data-ttu-id="7001a-290">**Действия**</span><span class="sxs-lookup"><span data-stu-id="7001a-290">**Steps**</span></span> | <span data-ttu-id="7001a-291">Приложение должно безопасно обрабатывать ошибки.</span><span class="sxs-lookup"><span data-stu-id="7001a-291">Application should fail safely.</span></span> <span data-ttu-id="7001a-292">Любой метод, возвращающий логическое значение, в зависимости от принятого решения, должен содержать тщательно созданный блок исключений.</span><span class="sxs-lookup"><span data-stu-id="7001a-292">Any method that returns a Boolean value, based on which certain decision is made, should have exception block carefully created.</span></span> <span data-ttu-id="7001a-293">Существует множество логических ошибок, из-за которых возникают проблемы с безопасностью, например при наличии небрежно созданного блока исключений.</span><span class="sxs-lookup"><span data-stu-id="7001a-293">There are lot of logical errors due to which security issues creep in, when the exception block is written carelessly.</span></span>|

### <a name="example"></a><span data-ttu-id="7001a-294">Пример</span><span class="sxs-lookup"><span data-stu-id="7001a-294">Example</span></span>
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
                        //// Adding additional check to enable CMS urls if they are not hosted on same domain.
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
<span data-ttu-id="7001a-295">Если исключение произошло, приведенный выше метод всегда возвращает значение true.</span><span class="sxs-lookup"><span data-stu-id="7001a-295">The above method will always return True, if some exception happens.</span></span> <span data-ttu-id="7001a-296">Если конечный пользователь предоставляет URL-адрес неправильного формата, который поддерживает браузер, но отклоняет конструктор `Uri()`, выдается исключение и пользователь перенаправляется на допустимый URL-адрес неправильного формата.</span><span class="sxs-lookup"><span data-stu-id="7001a-296">If the end user provides a malformed URL, that the browser respects, but the `Uri()` constructor doesn't, this will throw an exception, and the victim will be taken to the valid but malformed URL.</span></span> 