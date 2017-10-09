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
# <a name="security-frame-exception-management--mitigations"></a>Механизм безопасности. Управление исключениями | Устранение угроз 
| Продукт или служба | Статья |
| --------------- | ------- |
| **WCF** | <ul><li>[WCF — не добавляйте узел serviceDebug в файл конфигурации](#servicedebug)</li><li>[WCF — не добавляйте узел serviceMetadata в файл конфигурации](#servicemetadata)</li></ul> |
| **Веб-интерфейс API** | <ul><li>[Обеспечьте правильную обработку исключений в веб-API ASP.NET](#exception)</li></ul> |
| **Веб-приложение** | <ul><li>[Не раскрывайте сведения о безопасности в сообщениях об ошибках](#messages)</li><li>[Реализуйте страницу обработки ошибок по умолчанию](#default)</li><li>[Задайте способ развертывания tooRetail в службах IIS](#deployment)</li><li>[Обеспечьте безопасную обработку исключений](#fail)</li></ul> |

## <a id="servicedebug"></a>WCF — не добавляйте узел serviceDebug в файл конфигурации

| Название                   | Сведения      |
| ----------------------- | ------------ |
| **Компонент**               | WCF | 
| **Этап SDL**               | Создание |  
| **Применимые технологии** | Универсальные, .NET Framework 3 |
| **Атрибуты**              | Недоступно  |
| **Справочные материалы**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Действия** | Службы Windows Communication Framework (WCF) могут быть настроенный tooexpose отладочную информацию. Отладочную информацию не следует использовать в рабочих средах. Hello `<serviceDebug>` тег определяет, включена ли функция сведения отладки hello для службы WCF. Если атрибут includeExceptionDetailInFaults hello tootrue, сведения об исключении из приложения hello будет возвращаться tooclients. Злоумышленники могут использовать hello дополнительных сведений, которые он получает из отлаживаемого вывода toomount атак нацелена на hello framework, базы данных или другие ресурсы, используемые приложения hello. |

### <a name="example"></a>Пример
Hello следующий файл конфигурации содержит hello `<serviceDebug>` тег: 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
Отключение отладочной информации в службе hello. Это можно сделать, удалив hello `<serviceDebug>` тег из файла конфигурации приложения. 

## <a id="servicemetadata"></a>WCF — не добавляйте узел serviceMetadata в файл конфигурации

| Название                   | Сведения      |
| ----------------------- | ------------ |
| **Компонент**               | WCF | 
| **Этап SDL**               | Создание |  
| **Применимые технологии** | Универсальный |
| **Атрибуты**              | Универсальные, .NET Framework 3 |
| **Справочные материалы**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Действия** | Публично раскрытия сведений о службе можно предоставляют злоумышленникам ценных сведений о того, как они могут воспользоваться hello службы. Hello `<serviceMetadata>` тег включает средство публикации метаданных hello. Метаданные службы могут содержать конфиденциальные сведения, к которым нельзя предоставлять общий доступ. Как минимум разрешается только доверенные пользователи tooaccess hello метаданных и убедитесь, что ненужные сведения не предоставляются. Что еще лучше полностью отключите hello возможность toopublish метаданных. Безопасные конфигурации WCF не будет содержать hello `<serviceMetadata>` тег. |

## <a id="exception"></a>Обеспечьте правильную обработку исключений в веб-API ASP.NET

| Название                   | Сведения      |
| ----------------------- | ------------ |
| **Компонент**               | Веб-интерфейс API | 
| **Этап SDL**               | Создание |  
| **Применимые технологии** | MVC 5, MVC 6 |
| **Атрибуты**              | Недоступно  |
| **Справочные материалы**              | [Обработка исключений в веб-API ASP.NET](http://www.asp.net/web-api/overview/error-handling/exception-handling), [проверка модели в веб-API ASP.NET](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api) |
| **Действия** | По умолчанию большинство неперехваченных исключений в веб-API ASP.NET преобразовываются в HTTP-ответ с кодом состояния `500, Internal Server Error`.|

### <a name="example"></a>Пример
Код состояния toocontrol hello, hello API, `HttpResponseException` можно использовать, как показано ниже: 
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

### <a name="example"></a>Пример
Для дальнейшего управления ответе исключение hello hello `HttpResponseMessage` класс может использоваться, как показано ниже: 
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
toocatch необработанные исключения, которые не относятся к типу hello `HttpResponseException`, можно использовать фильтры исключений. Фильтры исключений реализовать hello `System.Web.Http.Filters.IExceptionFilter` интерфейса. Hello простейший способ toowrite фильтра исключений является tooderive из hello `System.Web.Http.Filters.ExceptionFilterAttribute` класса и переопределить метод OnException hello. 

### <a name="example"></a>Пример
Ниже приведен фильтр, который преобразует исключения `NotImplementedException` в код состояния HTTP `501, Not Implemented`. 
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

Существует несколько способов tooregister в фильтре исключений веб-API.
- Для действия
- Для контроллера
- Глобально

### <a name="example"></a>Пример
tooapply hello фильтрации tooa определенное действие, добавить фильтр hello в качестве атрибута toohello действия: 
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
### <a name="example"></a>Пример
tooapply tooall фильтра hello hello действий над `controller`, добавить фильтр hello в качестве атрибута toohello `controller` класса: 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a>Пример
tooapply hello глобально фильтрации tooall контроллеров веб-API, добавьте экземпляр фильтра toohello hello `GlobalConfiguration.Configuration.Filters` коллекции. Фильтры исключений в этой коллекции применяются tooany действие контроллера Web API. 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a>Пример
Проверка модели hello состояние модели могут передаваться метод tooCreateErrorResponse, как показано ниже: 
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

Проверьте hello ссылки в разделе hello ссылки на дополнительные сведения об обработке исключительные и проверка модели в ASP.Net Web API 

## <a id="messages"></a>Не раскрывайте сведения о безопасности в сообщениях об ошибках

| Название                   | Сведения      |
| ----------------------- | ------------ |
| **Компонент**               | Веб-приложение | 
| **Этап SDL**               | Создание |  
| **Применимые технологии** | Универсальный |
| **Атрибуты**              | Недоступно  |
| **Справочные материалы**              | Недоступно  |
| **Действия** | <p>Общие сообщения об ошибке предоставляются непосредственно пользователю toohello без включения конфиденциальных данных. К конфиденциальным данным относятся:</p><ul><li>имена серверов;</li><li>Строки подключения</li><li>имена пользователей;</li><li>Пароли</li><li>процедуры SQL;</li><li>подробные сведения о динамических ошибках SQL;</li><li>трассировка стека и строки кода;</li><li>переменные, хранимые в памяти;</li><li>расположения дисков и папок;</li><li>точки установки приложения;</li><li>параметры конфигурации узла;</li><li>другие внутренние сведения о приложении.</li></ul><p>Перехват всех ошибок в приложении и предоставление общих сообщений об ошибках, а также включение пользовательских ошибок в службах IIS позволяют предотвратить раскрытие информации. База данных SQL Server и .NET обработка исключений, среди других ошибок архитектур, являются особенно verbose и чрезвычайно полезна tooa злоумышленник профилирование приложения. Сделайте не напрямую hello отображения содержимого класса, производным от класса исключения .NET hello и убедитесь, что правильной обработкой исключений, чтобы случайно не произошло непредвиденное исключение возникает непосредственно toohello пользователя.</p><ul><li>Укажите общее сообщение об ошибке непосредственно сообщения toohello пользователя, который абстрактного дальней конкретные сведения непосредственно в сообщение hello исключение или ошибка</li><li>Отображаемое содержимое hello исключения .NET класса напрямую toohello пользователя</li><li>Отслеживать все сообщения об ошибках и если соответствующее сообщение hello пользователя с помощью клиента приложения сообщение отправлено toohello универсальное сообщение об ошибке</li><li>Не предоставляйте hello содержимого hello исключение класса напрямую пользователя toohello особенно hello возвращаемое значение из `.ToString()`, или hello значений свойств сообщений или StackTrace hello. Безопасно этого данные журнала и отображение более кроется пользователя toohello сообщения</li></ul>|

## <a id="default"></a>Реализуйте страницу обработки ошибок по умолчанию

| Название                   | Сведения      |
| ----------------------- | ------------ |
| **Компонент**               | Веб-приложение | 
| **Этап SDL**               | Создание |  
| **Применимые технологии** | Универсальный |
| **Атрибуты**              | Недоступно  |
| **Справочные материалы**              | [Сведения о диалоговом окне изменения параметров страниц ошибок ASP.NET](https://technet.microsoft.com/library/dd569096(WS.10).aspx) |
| **Действия** | <p>Если приложение ASP.NET перестает работать и приводит к возникновению ошибки "HTTP/1.x 500 — внутренняя ошибка сервера" или конфигурация компонентов (например, фильтрация запросов) предотвращает отображение страницы, создается сообщение об ошибке. Администраторы могут выбрать, отображать ли приложение hello понятное сообщение toohello клиента, клиент toohello сообщений подробные сведения об ошибке или только toolocalhost сообщения подробные сведения об ошибке. Hello <customErrors> тег в файле web.config hello имеет три режима:</p><ul><li>**On.** Указывает, что пользовательские ошибки включены. Если атрибут defaultRedirect не указан, для пользователей отобразится общая ошибка. пользовательские ошибки Hello отображаются toohello удаленные клиенты и toohello локального узла</li><li>**Off.** Указывает, что пользовательские ошибки выключены. Hello подробные сведения об ошибках ASP.NET отображаются toohello удаленные клиенты и toohello локального узла</li><li>**RemoteOnly:** указывает, что настраиваемые ошибки отображаются только toohello удаленных клиентов, а ошибки ASP.NET отображаются toohello локального узла. Это значение по умолчанию hello</li></ul><p>Откройте hello `web.config` файл для узла приложения hello и убедитесь, что тег hello либо `<customErrors mode="RemoteOnly" />` или `<customErrors mode="On" />` определен.</p>|

## <a id="deployment"></a>Задайте способ развертывания tooRetail в службах IIS

| Название                   | Сведения      |
| ----------------------- | ------------ |
| **Компонент**               | Веб-приложение | 
| **Этап SDL**               | Развертывание |  
| **Применимые технологии** | Универсальный |
| **Атрибуты**              | Недоступно  |
| **Справочные материалы**              | [Элемент deployment (схема параметров ASP.NET)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx) |
| **Действия** | <p>Hello `<deployment retail>` коммутатора предназначена для использования в производственных серверах IIS. Этот параметр является используется toohelp приложения, выполняемые с наилучшей возможной производительности hello и наименьший возможный сведения о безопасности, что leakages, отключив hello вывод трассировки toogenerate возможности приложения на странице, отключение toodisplay возможность hello подробное сообщение об ошибке Пользователи tooend сообщений и отключение переключатель отладки hello.</p><p>Зачастую параметры, предназначенные для разработчиков, например трассировка и отладка неудачно завершенных запросов, включаются во время активной разработки. Рекомендуется, задать tooretail hello метода развертывания на любом сервере в рабочей среде. Откройте файл machine.config hello и убедитесь, что `<deployment retail="true" />` остается установленным tootrue.</p>|

## <a id="fail"></a>Обеспечьте безопасную обработку исключений

| Название                   | Сведения      |
| ----------------------- | ------------ |
| **Компонент**               | Веб-приложение | 
| **Этап SDL**               | Создание |  
| **Применимые технологии** | Универсальный |
| **Атрибуты**              | Недоступно  |
| **Справочные материалы**              | [Безопасная обработка ошибок](https://www.owasp.org/index.php/Fail_securely) |
| **Действия** | Приложение должно безопасно обрабатывать ошибки. Любой метод, возвращающий логическое значение, в зависимости от принятого решения, должен содержать тщательно созданный блок исключений. Существует большое число логических ошибок из-за toowhich смещения проблемы безопасности в при записи блока исключений hello высока.|

### <a name="example"></a>Пример
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
Hello выше метод всегда возвращает значение True, если произошло исключение. Если hello конечный пользователь вводит неверный URL-адрес, где hello отношениях браузера, но hello `Uri()` конструктор не, то будет создано исключение и жертвы hello будут выполнены toohello допустимо, но имеет неправильный формат URL-адреса. 
