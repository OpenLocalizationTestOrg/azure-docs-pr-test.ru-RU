---
title: "aaaDiagnose сбои и исключения в веб-приложений с помощью Azure Application Insights | Документы Microsoft"
description: "Регистрируйте исключения приложений ASP.NET и телеметрию запросов."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d1e98390-3ce4-4d04-9351-144314a42aa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 8930e6d2b29f83ea635c4ecb7afd11fc1d97d085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a>Диагностика исключений в веб-приложениях с помощью Application Insights
Об исключениях активного веб-приложения сообщает [Application Insights](app-insights-overview.md). Вы можете соотнести неудачных запросов с исключениями и других событий на сервер и клиент hello, чтобы быстро найти причину причины hello.

## <a name="set-up-exception-reporting"></a>Настройка создания отчетов об исключениях
* исключения toohave, полученные от сервера приложения.
  * Запрограммируйте установку [пакета SDK для Application Insights](app-insights-asp-net.md) в приложении или:
  * веб-серверы IIS: запустите [агент Application Insights](app-insights-monitor-performance-live-website-now.md) либо
  * Веб-приложениях Azure: добавить hello [расширение Application Insights](app-insights-azure-web-apps.md)
  * Веб-приложений Java: hello установки [агента Java](app-insights-java-agent.md)
* Установка hello [фрагмент JavaScript](app-insights-javascript.md) в свои исключения браузера toocatch веб-страницы.
* Некоторые платформы приложений или некоторые параметры, необходимые tootake toocatch некоторые дополнительные шаги дополнительные исключения:
  * [веб-формы](#web-forms);
  * [MVC](#mvc);
  * [веб-API 1.*](#web-api-1);
  * [веб-API 2.*](#web-api-2);
  * [WCF](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a>Диагностика исключений с помощью Visual Studio
Откройте решение для приложения hello в Visual Studio toohelp в процессе отладки.

Запустите приложение hello на сервере или на компьютере разработки, нажав клавишу F5.

Откройте окно hello поиска Application Insights в Visual Studio и задать для него toodisplay события из приложения. Во время отладки, это можно сделать, просто нажав кнопку hello Application Insights.

![Щелкните правой кнопкой мыши проект hello и Application Insights, нажмите кнопку Открыть.](./media/app-insights-asp-net-exceptions/34.png)

Обратите внимание, что hello отчетов tooshow просто исключения можно фильтровать.

*Исключения не отображаются? См. раздел [Запись исключений](#exceptions).*

Щелкните отчет исключение tooshow трассировку стека.
Щелкните Справочник по строке в трассировке стека hello, соответствующий код файла tooopen hello.  

В коде hello Обратите внимание, что CodeLens показывает данные об исключениях hello:

![Уведомление об исключениях CodeLens](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-hello-azure-portal"></a>Диагностика ошибок с помощью портала Azure hello
Из Application Insights hello Общие сведения о приложении Плитка сбоев hello отображает диаграммы для исключения и невыполненных запросов HTTP, вместе со списком hello запроса URL-адреса, которые наиболее частые ошибки hello.

![Последовательно выберите элементы "Параметры" и "Сбои".](./media/app-insights-asp-net-exceptions/012-start.png)

Щелкните по одной из hello сбой типов исключений в tooget tooindividual hello список вхождений hello исключения, где можно подробно рассмотреть hello и трассировка стека:

![Выберите экземпляр невыполненных запросов, а также в разделе сведения об исключении, получить tooinstances hello исключения.](./media/app-insights-asp-net-exceptions/030-req-drill.png)

**Кроме того** можно запустить из списка hello запросов и найти связанные tooit исключения.

*Исключения не отображаются? См. раздел [Запись исключений](#exceptions).*


## <a name="custom-tracing-and-log-data"></a>Пользовательская трассировка и данные журналов
приложение конкретных tooyour tooget диагностических данных, можно вставить код toosend данные телеметрии. Это отображаются при поиске диагностики наряду с hello запрос представления страницы и другие данные, автоматически сохраняются.

Доступно несколько параметров.

* [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) обычно используется для наблюдения за шаблонов использования, но также отправляет данных отображается под пользовательские события диагностики поиска hello. У событий есть имена и они могут содержать строковые свойства и числовые метрики, по которым можно [фильтровать результаты поиска диагностических данных](app-insights-diagnostic-search.md).
* [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) позволяет отправлять более длинные данные, например данные POST.
* [TrackException()](#exceptions) отправляет трассировки стеков. [Дополнительные сведения об исключениях](#exceptions).
* Если вы уже используете какую-либо платформу ведения журналов, например Log4Net или NLog, [эти журналы можно записывать](app-insights-asp-net-trace-logs.md) и включать в результаты поиска диагностических данных вместе с данными запросов и исключений.

Откройте эти события toosee [поиска](app-insights-diagnostic-search.md)откройте фильтра и нажмите кнопку Custom Event, трассировку или исключения.

![Детализация](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> Если приложение создает большой объем данных телеметрии, модуль адаптивной выборки hello автоматически уменьшит hello тома, отправляемое toohello портала, отправляя репрезентативной часть событий. События, которые являются частью hello одной операции будет иметь или отмену выбора как группу, так что можно перемещаться между связанными событиями. [Дополнительная информация о выборке.](app-insights-sampling.md)
>
>

### <a name="how-toosee-request-post-data"></a>Способ toosee запроса данные POST
Сведения о запросе не включайте hello данные, отправляемые tooyour приложения в вызове процедуры POST. toohave эти данные, определенные как:

* [Установка пакета SDK для hello](app-insights-asp-net.md) в проекте приложения.
* Вставьте код в вашего приложения toocall [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace). Отправьте данные POST hello в параметре сообщение hello. Нет toohello допускается ограничение на размер, поэтому попробуйте toosend hello только необходимые данные.
* При исследовании невыполненных запросов, найти связанные hello трассировок.  

![Детализация](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <a name="exceptions"></a> Запись исключений и связанных диагностических данных
Сначала вы не увидите hello портале все исключения hello, привести к сбою приложения. Вы увидите все исключения браузера (Если вы используете hello [JavaScript SDK](app-insights-javascript.md) на веб-страницах). Но большинство server исключения перехватываются службами IIS и у вас есть немного кода toosee toowrite их.

Вы можете:

* **Явно журнала исключений** путем вставки кода в tooreport hello исключение обработчиков исключений.
* **Автоматически записывать исключения** путем настройки своей платформы ASP.NET. Hello необходимых дополнений отличаются для разных типов framework.

## <a name="reporting-exceptions-explicitly"></a>Явная регистрация исключений
Hello простым способом является tooinsert tooTrackException() вызов в обработчике исключений.

JavaScript

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

C#

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send hello exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

VB

    Dim telemetry = New TelemetryClient
    ...
    Try
      ...
    Catch ex as Exception
      ' Set up some properties:
      Dim properties = New Dictionary (Of String, String)
      properties.Add("Game", currentGame.Name)

      Dim measurements = New Dictionary (Of String, Double)
      measurements.Add("Users", currentGame.Users.Count)

      ' Send hello exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

Hello свойства и значения параметров не являются обязательными, но они полезны для [фильтрацию и добавление](app-insights-diagnostic-search.md) дополнительных сведений. Например если у вас есть приложение, которое можно запустить несколько игр, можно найти все hello исключение отчеты связанные tooa конкретной игры. Можно добавить столько элементов, так как tooeach словарь.

## <a name="browser-exceptions"></a>Исключения браузера
Большинство исключений браузера регистрируются.

Если веб-страница содержит файлы скриптов из сети доставки содержимого или других доменов, убедитесь в скрипт содержит атрибут hello ```crossorigin="anonymous"```, и отправляет этот сервер hello [заголовки CORS](http://enable-cors.org/). Это позволит вам tooget трассировку стека и сведения для необработанных исключений JavaScript из этих ресурсов.

## <a name="web-forms"></a>Веб-формы
Для веб-формы hello HTTP-модуль будет может toocollect hello исключений при переадресации, не настроены CustomErrors.

Но при наличии активных переадресации, добавить следующие функции Application_Error строки toohello в Global.asax.cs hello. (Добавьте файл Global.asax, если он еще не создан).

*C#*

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a>MVC
Если hello [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) конфигурация `Off`, то исключения будут доступны для hello [HTTP-модуля](https://msdn.microsoft.com/library/ms178468.aspx) toocollect. Тем не менее если это `RemoteOnly` (по умолчанию), или `On`, hello исключение будет очищено и недоступно для Application Insights tooautomatically сбора. Можно исправить, путем переопределения hello [класса System.Web.Mvc.HandleErrorAttribute](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx)и применение hello переопределении класса, как показано для hello разные MVC версии ниже ([github источника](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):

    using System;
    using System.Web.Mvc;
    using Microsoft.ApplicationInsights;

    namespace MVC2App.Controllers
    {
      [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
      public class AiHandleErrorAttribute : HandleErrorAttribute
      {
        public override void OnException(ExceptionContext filterContext)
        {
            if (filterContext != null && filterContext.HttpContext != null && filterContext.Exception != null)
            {
                //If customError is Off, then AI HTTPModule will report hello exception
                if (filterContext.HttpContext.IsCustomErrorEnabled)
                {   //or reuse instance (recommended!). see note above  
                    var ai = new TelemetryClient();
                    ai.TrackException(filterContext.Exception);
                }
            }
            base.OnException(filterContext);
        }
      }
    }

#### <a name="mvc-2"></a>MVC 2
Замените на новый атрибут в контроллерах атрибут HandleError hello.

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[Пример](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a>MVC 3
Зарегистрируйте `AiHandleErrorAttribute` в качестве глобального фильтра в Global.asax.cs:

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[Пример](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a>MVC 4, MVC5
Зарегистрируйте AiHandleErrorAttribute в качестве глобального фильтра в FilterConfig.cs:

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with hello override tootrack unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[Пример](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a>Web API 1.x
Переопределите System.Web.Http.Filters.ExceptionFilterAttribute:

    using System.Web.Http.Filters;
    using Microsoft.ApplicationInsights;

    namespace WebAPI.App_Start
    {
      public class AiExceptionFilterAttribute : ExceptionFilterAttribute
      {
        public override void OnException(HttpActionExecutedContext actionExecutedContext)
        {
            if (actionExecutedContext != null && actionExecutedContext.Exception != null)
            {  //or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(actionExecutedContext.Exception);    
            }
            base.OnException(actionExecutedContext);
        }
      }
    }

Можно добавить этот атрибут переопределенный toospecific контроллеры, или добавить глобальный фильтр конфигурации toohello класса WebApiConfig hello:

    using System.Web.Http;
    using WebApi1.x.App_Start;

    namespace WebApi1.x
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            config.Routes.MapHttpRoute(name: "DefaultApi", routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional });
            ...
            config.EnableSystemDiagnosticsTracing();

            // Capture exceptions for Application Insights:
            config.Filters.Add(new AiExceptionFilterAttribute());
        }
      }
    }

[Пример](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

Существует несколько вариантов, не может обрабатывать hello фильтры исключений. Например:

* Исключения выброшены из конструкторов контроллеров.
* Исключения выброшены из обработчиков сообщений.
* Исключения выброшены при маршрутизации.
* Исключения выброшены при сериализации содержимого ответа.

## <a name="web-api-2x"></a>Web API 2.x
Добавьте реализацию IExceptionLogger:

    using System.Web.Http.ExceptionHandling;
    using Microsoft.ApplicationInsights;

    namespace ProductsAppPureWebAPI.App_Start
    {
      public class AiExceptionLogger : ExceptionLogger
      {
        public override void Log(ExceptionLoggerContext context)
        {
            if (context !=null && context.Exception != null)
            {//or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(context.Exception);
            }
            base.Log(context);
        }
      }
    }

При добавлении этой службы toohello WebApiConfig.

    using System.Web.Http;
    using System.Web.Http.ExceptionHandling;
    using ProductsAppPureWebAPI.App_Start;

    namespace WebApi2WithMVC
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
            config.Services.Add(typeof(IExceptionLogger), new AiExceptionLogger());
        }
      }
  }

[Пример](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

В качестве альтернативы можно выполнить следующее.

1. Замените hello только ExceptionHandler на собственную реализацию IExceptionHandler. Это только вызывается, когда инфраструктура hello это все еще может toochoose какой ответ сообщений toosend (не при прерывании hello соединения для экземпляра)
2. Не вызывается во всех случаях фильтры исключений (как описано в разделе hello контроллерах веб-API 1.x выше).

## <a name="wcf"></a>WCF
Добавьте класс, который расширяет Attribute и реализует IErrorHandler и IServiceBehavior.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.ServiceModel.Description;
    using System.ServiceModel.Dispatcher;
    using System.Web;
    using Microsoft.ApplicationInsights;

    namespace WcfService4.ErrorHandling
    {
      public class AiLogExceptionAttribute : Attribute, IErrorHandler, IServiceBehavior
      {
        public void AddBindingParameters(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase,
            System.Collections.ObjectModel.Collection<ServiceEndpoint> endpoints,
            System.ServiceModel.Channels.BindingParameterCollection bindingParameters)
        {
        }

        public void ApplyDispatchBehavior(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
            foreach (ChannelDispatcher disp in serviceHostBase.ChannelDispatchers)
            {
                disp.ErrorHandlers.Add(this);
            }
        }

        public void Validate(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
        }

        bool IErrorHandler.HandleError(Exception error)
        {//or reuse instance (recommended!). see note above
            var ai = new TelemetryClient();

            ai.TrackException(error);
            return false;
        }

        void IErrorHandler.ProvideFault(Exception error,
            System.ServiceModel.Channels.MessageVersion version,
            ref System.ServiceModel.Channels.Message fault)
        {
        }
      }
    }

Добавьте hello атрибут toohello службы реализации:

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[Пример](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a>Счетчики производительности исключений
Если у вас есть [установлен агент аналитики приложений hello](app-insights-monitor-performance-live-website-now.md) на сервере, вы можете получить диаграмму скорости исключения hello, измеренное .NET. Она включает как обработанные, так и необработанные исключения .NET.

Откройте колонку обозревателя метрик, добавьте новую диаграмму и выберите счетчик **Частота исключений**в списке "Счетчики производительности".

Hello .NET framework вычисляет скорость hello путем подсчета hello число исключений в интервал hello продолжительность интервала hello.

Обратите внимание, что он будет отличаться от вычислены порталом Application Insights hello TrackException отчеты по инвентаризации число исключений «hello». интервалов выборки Hello различаются, а hello SDK не отправляет отчеты TrackException для обработанные и необработанные исключения.

## <a name="video"></a>Видео

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a>Дальнейшие действия
* [Мониторинг REST, SQL и другие вызовы toodependencies](app-insights-asp-net-dependencies.md)
* [Мониторинг времени загрузки страниц, исключений браузера и вызовов AJAX](app-insights-javascript.md)
* [Мониторинг счетчиков производительности](app-insights-performance-counters.md)
