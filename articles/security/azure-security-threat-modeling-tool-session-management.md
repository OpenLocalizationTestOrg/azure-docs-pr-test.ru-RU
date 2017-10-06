---
title: "aaaSession управления - Microsoft средства моделирования угроз - Azure | Документы Microsoft"
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
ms.openlocfilehash: 915ffae3f775ca6902fcfb93e7e1952ce85612f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-session-management--articles"></a>Механизм безопасности. Управление сеансами | Статьи 
| Продукт или служба | Статья |
| --------------- | ------- |
| **Azure AD**    | <ul><li>[Реализуйте надлежащее событие выхода с помощью методов ADAL при использовании Azure AD](#logout-adal)</li></ul> |
| Устройства Интернета вещей | <ul><li>[Используйте токены SaS с ограниченным временем существования](#finite-tokens)</li></ul> |
| **Azure DocumentDB** | <ul><li>[Используйте токены ресурсов с минимальным временем существования](#resource-tokens)</li></ul> |
| **ADFS** | <ul><li>[Реализуйте надлежащее событие выхода с помощью методов WsFederation при использовании ADFS](#wsfederation-logout)</li></ul> |
| **Сервер удостоверений** | <ul><li>[Реализуйте надлежащее событие выхода при использовании сервера удостоверений](#proper-logout)</li></ul> |
| **Веб-приложение** | <ul><li>[Используйте защищенные файлы cookie в приложениях, использующих протокол HTTPS](#https-secure-cookies)</li><li>[Укажите атрибут httpOnly в определении файла cookie всех приложений на основе протокола HTTP](#cookie-definition)</li><li>[Уменьшите риск атак с подделкой межсайтовых запросов на веб-страницах ASP.NET](#csrf-asp)</li><li>[Настройте период бездействия сеанса](#inactivity-lifetime)</li><li>[Реализация правильную выхода из приложения hello](#proper-app-logout)</li></ul> |
| **Веб-интерфейс API** | <ul><li>[Уменьшите риск атак с подделкой межсайтовых запросов в веб-интерфейсах API ASP.NET](#csrf-api)</li></ul> |

## <a id="logout-adal"></a>Реализуйте надлежащее событие выхода с помощью методов ADAL при использовании Azure AD

| Название                   | Сведения      |
| ----------------------- | ------------ |
| **Компонент**               | Azure AD | 
| **Этап SDL**               | Создание |  
| **Применимые технологии** | Универсальный |
| **Атрибуты**              | Недоступно  |
| **Справочные материалы**              | Недоступно  |
| **Действия** | Если приложение hello использует маркер доступа, выданный Azure AD, должен вызывать обработчик события выхода hello |

### <a name="example"></a>Пример
```C#
HttpContext.GetOwinContext().Authentication.SignOut(OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType)
```

### <a name="example"></a>Пример
Кроме того, также необходимо уничтожить сеанс пользователя путем вызова метода Session.Abandon(). Ниже приведен метод безопасной реализации события выхода пользователя.
```C#
    [HttpPost]
        [ValidateAntiForgeryToken]
        public void LogOff()
        {
            string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            AuthenticationContext authContext = new AuthenticationContext(Authority + TenantId, new NaiveSessionCache(userObjectID));
            authContext.TokenCache.Clear();
            Session.Clear();
            Session.Abandon();
            Response.SetCookie(new HttpCookie("ASP.NET_SessionId", string.Empty));
            HttpContext.GetOwinContext().Authentication.SignOut(
                OpenIdConnectAuthenticationDefaults.AuthenticationType,
                CookieAuthenticationDefaults.AuthenticationType);
        } 
```

## <a id="finite-tokens"></a>Используйте токены SaS с ограниченным временем существования

| Название                   | Сведения      |
| ----------------------- | ------------ |
| **Компонент**               | Устройства Интернета вещей | 
| **Этап SDL**               | Создание |  
| **Применимые технологии** | Универсальный |
| **Атрибуты**              | Недоступно  |
| **Справочные материалы**              | Недоступно  |
| **Действия** | SaS токены, созданные для проверки подлинности tooAzure центр IoT должен иметь ограничение срока. Сохраните hello SaS времени жизни токенов tooa минимальные toolimit hello количество раз, когда они могут быть воспроизведены в случае компрометации токены hello.|

## <a id="resource-tokens"></a>Используйте токены ресурсов с минимальным временем существования

| Название                   | Сведения      |
| ----------------------- | ------------ |
| **Компонент**               | Azure DocumentDB | 
| **Этап SDL**               | Создание |  
| **Применимые технологии** | Универсальный |
| **Атрибуты**              | Недоступно  |
| **Справочные материалы**              | Недоступно  |
| **Действия** | Уменьшите время существования hello ресурсов маркера tooa минимальное значение. Допустимый интервал времени по умолчанию для маркеров ресурсов составляет 1 час.|

## <a id="wsfederation-logout"></a>Реализуйте надлежащее событие выхода с помощью методов WsFederation при использовании ADFS

| Название                   | Сведения      |
| ----------------------- | ------------ |
| **Компонент**               | ADFS | 
| **Этап SDL**               | Создание |  
| **Применимые технологии** | Универсальный |
| **Атрибуты**              | Недоступно  |
| **Справочные материалы**              | Недоступно  |
| **Действия** | Если приложения hello зависит от службы маркеров безопасности маркера, выданного службой ADFS, обработчик событий выхода hello следует вызывать toolog метод WSFederationAuthenticationModule.FederatedSignOut() выход пользователя hello. Также hello текущего сеанса должен быть уничтожен, и значение маркера сеанса hello следует сбросить и nullified.|

### <a name="example"></a>Пример
```C#
        [HttpPost, ValidateAntiForgeryToken]
        [Authorization]
        public ActionResult SignOut(string redirectUrl)
        {
            if (!this.User.Identity.IsAuthenticated)
            {
                return this.View("LogOff", null);
            }

            // Removes hello user profile.
            this.Session.Clear();
            this.Session.Abandon();
            HttpContext.Current.Response.Cookies.Add(new System.Web.HttpCookie("ASP.NET_SessionId", string.Empty)
                {
                    Expires = DateTime.Now.AddDays(-1D),
                    Secure = true,
                    HttpOnly = true
                });

            // Signs out at hello specified security token service (STS) by using hello WS-Federation protocol.
            Uri signOutUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Issuer);
            Uri replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm);
            if (!string.IsNullOrEmpty(redirectUrl))
            {
                replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm + redirectUrl);
            }
           //     Signs out of hello current session and raises hello appropriate events.
            var authModule = FederatedAuthentication.WSFederationAuthenticationModule;
            authModule.SignOut(false);
        //     Signs out at hello specified security token service (STS) by using hello WS-Federation
        //     protocol.            
            WSFederationAuthenticationModule.FederatedSignOut(signOutUrl, replyUrl);
            return new RedirectResult(redirectUrl);
        }
```

## <a id="proper-logout"></a>Реализуйте надлежащее событие выхода при использовании сервера удостоверений

| Название                   | Сведения      |
| ----------------------- | ------------ |
| **Компонент**               | Сервер удостоверений | 
| **Этап SDL**               | Создание |  
| **Применимые технологии** | Универсальный |
| **Атрибуты**              | Недоступно  |
| **Справочные материалы**              | [Сведения о федеративном выходе на платформе IdentityServer3](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html) |
| **Действия** | IdentityServer поддерживает toofederate возможность hello с внешних поставщиков. Когда пользователь выходит из поставщика удостоверений вышестоящего, зависимости hello протокол, используемый, его может быть возможных tooreceive уведомление при hello пользователь выходит из системы. Она позволяет toonotify IdentityServer, ее клиентов, чтобы они могли войти hello пользователя. Просмотрите документацию hello в разделе references hello hello сведения о реализации.|

## <a id="https-secure-cookies"></a>Используйте защищенные файлы cookie в приложениях, использующих протокол HTTPS

| Название                   | Сведения      |
| ----------------------- | ------------ |
| **Компонент**               | Веб-приложение | 
| **Этап SDL**               | Создание |  
| **Применимые технологии** | Универсальный |
| **Атрибуты**              | EnvironmentType: OnPrem |
| **Справочные материалы**              | [Элемент httpCookies (схема параметров ASP.NET)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [Свойство HttpCookie.Secure](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx) |
| **Действия** | Файлы cookie обычно являются только домен доступен toohello, для которого было ограничено. К сожалению определение hello «домен» не включает протокол hello, файлы cookie, которые создаются по протоколу HTTPS, доступны по протоколу HTTP. атрибут «безопасность» Hello указывает, что браузер toohello, hello cookie только стало доступным по протоколу HTTPS. Убедитесь, что все файлы Сookie по протоколу HTTPS используют hello **безопасного** атрибута. требование Hello может применяться в файле web.config hello, задав tootrue атрибут requireSSL hello. Это hello основной подход, так как он будет обеспечивать hello **безопасного** любой дополнительный код изменения атрибутов для всех текущих и будущих куки-файлов без необходимости toomake hello.|

### <a name="example"></a>Пример
```C#
<configuration>
  <system.web>
    <httpCookies requireSSL="true"/>
  </system.web>
</configuration>
```
параметр Hello применяется, даже если протокол HTTP является приложение hello используется tooaccess. Если используется протокол HTTP tooaccess hello приложения, hello параметр переводов, которые приложение hello так, как файлы cookie hello устанавливаются с помощью hello защищенный атрибут и hello браузер не будет отправлять их снова toohello приложения.

| Название                   | Сведения      |
| ----------------------- | ------------ |
| **Компонент**               | Веб-приложение | 
| **Этап SDL**               | Создание |  
| **Применимые технологии** | Веб-формы, MVC 5 |
| **Атрибуты**              | EnvironmentType: OnPrem |
| **Справочные материалы**              | Недоступно  |
| **Действия** | Когда веб-приложение hello hello проверяющая сторона, который hello поставщика удостоверений сервер ADFS, атрибут hello FedAuth маркер безопасности можно настроить с параметра requireSSL tooTrue в `system.identityModel.services` файла Web.config:|

### <a name="example"></a>Пример
```C#
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:20:0" />
    ....  
    </federationConfiguration>
  </system.identityModel.services>
```

## <a id="cookie-definition"></a>Укажите атрибут httpOnly в определении файла cookie всех приложений на основе протокола HTTP

| Название                   | Сведения      |
| ----------------------- | ------------ |
| **Компонент**               | Веб-приложение | 
| **Этап SDL**               | Создание |  
| **Применимые технологии** | Универсальный |
| **Атрибуты**              | Недоступно  |
| **Справочные материалы**              | [Сведения об атрибуте secure в файлах cookie](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie) |
| **Действия** | toomitigate hello риск раскрытия информации с атаке межсайтовых сценариев (XSS), новый атрибут - httpOnly - было введено toocookies и поддерживается всеми основными браузерами. атрибут Hello указывает, что куки-файл недоступен через сценарий. С помощью файлов cookie HttpOnly, веб-приложении снижает вероятность hello можно, конфиденциальные данные, содержащиеся в файле cookie hello кражи через сценарий и отправленных веб-сайта злоумышленника tooan. |

### <a name="example"></a>Пример
Все HTTP-приложений, которые используют файлы cookie следует указать HttpOnly в определении cookie hello, путем реализации следующие конфигурации в файле web.config:
```XML
<system.web>
.
.
   <httpCookies requireSSL="false" httpOnlyCookies="true"/>
.
.
</system.web>
```

| Название                   | Сведения      |
| ----------------------- | ------------ |
| **Компонент**               | Веб-приложение | 
| **Этап SDL**               | Создание |  
| **Применимые технологии** | Веб-формы |
| **Атрибуты**              | Недоступно  |
| **Справочные материалы**              | [Свойство FormsAuthentication.RequireSSL](https://msdn.microsoft.com/library/system.web.security.formsauthentication.requiressl.aspx) |
| **Действия** | Hello RequireSSL значение свойства задается в файле конфигурации hello для приложения ASP.NET с помощью атрибут requireSSL hello hello элемента конфигурации. Вы можно указать в файле Web.config hello для приложения ASP.NET ли протокол SSL (Secure Sockets Layer) сервера требуется tooreturn hello проверки подлинности форм cookie toohello атрибутом requireSSL параметр hello.|

### <a name="example"></a>Пример 
Hello следующий пример кода задает атрибут requireSSL hello в файле Web.config hello.
```XML
<authentication mode="Forms">
  <forms loginUrl="member_login.aspx" cookieless="UseCookies" requireSSL="true"/>
</authentication>
```

| Название                   | Сведения      |
| ----------------------- | ------------ |
| **Компонент**               | Веб-приложение | 
| **Этап SDL**               | Создание |  
| **Применимые технологии** | MVC5 |
| **Атрибуты**              | EnvironmentType: OnPrem |
| **Справочные материалы**              | [Запись блога о конфигурации Windows Identity Foundation (WIF). Часть 2](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/) |
| **Действия** | атрибут httpOnly tooset для файлов cookie FedAuth, hideFromCsript атрибут должен иметь значение tooTrue. |

### <a name="example"></a>Пример
В конфигурации ниже показано hello правильной конфигурации:
```XML
<federatedAuthentication>
<cookieHandler mode="Custom"
                       hideFromScript="true"
                       name="FedAuth"
                       path="/"
                       requireSsl="true"
                       persistentSessionLifetime="25">
</cookieHandler>
</federatedAuthentication>
```

## <a id="csrf-asp"></a>Уменьшите риск атак с подделкой межсайтовых запросов на веб-страницах ASP.NET

| Название                   | Сведения      |
| ----------------------- | ------------ |
| **Компонент**               | Веб-приложение | 
| **Этап SDL**               | Создание |  
| **Применимые технологии** | Универсальный |
| **Атрибуты**              | Недоступно  |
| **Справочные материалы**              | Недоступно  |
| **Действия** | Подделки межсайтовых запросов (CSRF или XSRF) — это тип атаки, в котором злоумышленник может выполнять действия в контексте безопасности hello установленного сеанса другого пользователя на веб-сайте. Цель Hello является toomodify или удалить содержимое, если указанный веб-узел hello основывается только на запрос получен tooauthenticate файлы cookie сеанса. Злоумышленник может воспользоваться этой уязвимостью, получая URL-адрес с помощью команды tooload браузера другого пользователя с уязвимым сайта, на котором hello пользователь уже вошел в. Существует множество способов для toodo злоумышленник, такие как с помощью предоставления различных веб-сайта, загружает ресурс hello уязвимым сервера или получении tooclick пользователя hello ссылку. Если hello сервер отправляет клиенту дополнительных маркеров toohello, требует hello этого токена все последующие запросы клиента tooinclude и проверяет, что все последующие запросы включать маркер, который соответствует toohello текущего сеанса, например, можно предотвратить атаки Hello с помощью hello ASP.NET AntiForgeryToken или ViewState. |

| Название                   | Сведения      |
| ----------------------- | ------------ |
| **Компонент**               | Веб-приложение | 
| **Этап SDL**               | Создание |  
| **Применимые технологии** | MVC 5, MVC 6 |
| **Атрибуты**              | Недоступно  |
| **Справочные материалы**              | [Сведения о предотвращении подделки межсайтовых запросов в ASP.NET MVC и на веб-страницах ASP.NET](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) |
| **Действия** | Формы CSRF защиты и ASP.NET MVC - hello используйте `AntiForgeryToken` вспомогательный метод для представлений; заключите `Html.AntiForgeryToken()` в форму hello, например,|

### <a name="example"></a>Пример
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
```

### <a name="example"></a>Пример
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a>Пример
В hello же время, Html.AntiForgeryToken() дает hello посетитель куки-файл называется __RequestVerificationToken с hello совпадает со значением в hello случайного скрытые значения показано выше. Toovalidate входящих формы post, добавьте метод hello [ValidateAntiForgeryToken] фильтр toohello целевого действия. Например:
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
Фильтр авторизации, проверяющий, что:
* входящий запрос Hello имеет файл cookie, вызывается __RequestVerificationToken
* Hello во входящем запросе есть `Request.Form` под названием __RequestVerificationToken
* Этих файлов cookie и `Request.Form` значения совпадают, при условии, что все хорошо, hello запрос проходит через в обычном режиме. В противном случае проверка подлинности завершается ошибкой и отображается следующее сообщение: "Обязательный маркер против подделки не был предоставлен или был недопустимым". 

### <a name="example"></a>Пример
CSRF защиты и AJAX: hello маркера формы может вызвать проблемы для запросов AJAX, так как запрос AJAX может отправить данные JSON, а не данные HTML-формы. Одним из решений является toosend hello токенов в заголовок HTTP. Hello следующий код использует токены hello toogenerate синтаксис Razor, а затем добавляет маркеры tooan hello AJAX-запросом. 
```C#
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }

    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a>Пример
При обработке запроса hello, извлеките hello токены из заголовка запроса hello. Затем метод hello AntiForgery.Validate toovalidate hello маркеры. метод Validate Hello вызывает исключение, если маркеры hello не допускаются.
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

| Название                   | Сведения      |
| ----------------------- | ------------ |
| **Компонент**               | Веб-приложение | 
| **Этап SDL**               | Создание |  
| **Применимые технологии** | Веб-формы |
| **Атрибуты**              | Недоступно  |
| **Справочные материалы**              | [Использовать преимущества от встроенных функций ASP.NET tooFend Off Web атак](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2) |
| **Действия** | Атаки CSRF в приложениях на основе веб-форма можно устранить путем настройки произвольная строка tooa ViewStateUserKey, изменяющийся для каждого пользователя - идентификатор пользователя или лучше, идентификатор сеанса. По разным техническим и социальным причинам идентификатор сеанса подходит гораздо лучше, так как его нельзя предсказать, время его ожидания истекает и он уникальный для каждого пользователя.|

### <a name="example"></a>Пример
Ниже приведен код hello необходимо toohave во всех веб-страниц.
```C#
void Page_Init (object sender, EventArgs e) {
   ViewStateUserKey = Session.SessionID;
   :
}
```

## <a id="inactivity-lifetime"></a>Настройте период бездействия сеанса

| Название                   | Сведения      |
| ----------------------- | ------------ |
| **Компонент**               | Веб-приложение | 
| **Этап SDL**               | Создание |  
| **Применимые технологии** | Универсальный |
| **Атрибуты**              | Недоступно  |
| **Справочные материалы**              | [Свойство HttpSessionState.Timeout](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx) |
| **Действия** | Время ожидания сеанса представляет hello событий возникающая, если пользователь не выполняет никаких действий на веб-сайте на протяжении интервала (определяемые веб-сервера). Здравствуйте событий на стороне сервера, изменить статус hello too'invalid сеанса пользователя hello "(например «больше не используются») и сообщить hello web server toodestroy (удаление всех данных, содержащихся в ней). Hello следующий пример кода задает время ожидания сеанса hello атрибута в минутах too15 в файле Web.config hello.|

### <a name="example"></a>Пример
```XML-код <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration>
```

## <a id="threat-detection"></a>Enable Threat detection on Azure SQL
```

| Название                   | Сведения      |
| ----------------------- | ------------ |
| **Компонент**               | Веб-приложение | 
| **Этап SDL**               | Создание |  
| **Применимые технологии** | Веб-формы |
| **Атрибуты**              | Недоступно  |
| **Справочные материалы**              | [Элемент forms для элемента credentials для элемента authentication (схема параметров ASP.NET)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx) |
| **Действия** | Значение минут hello too15 времени ожидания билета проверки подлинности форм куки-файл|

### <a name="example"></a>Пример
``` XML-код <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms>
```

| Title                   | Details      |
| ----------------------- | ------------ |
| **Component**               | Web Application | 
| **SDL Phase**               | Build |  
| **Applicable Technologies** | Web Forms, MVC5 |
| **Attributes**              | EnvironmentType - OnPrem |
| **References**              | [asdeqa](https://skf.azurewebsites.net/Mitigations/Details/wefr) |
| **Steps** | When hello web application is Relying Party and ADFS is hello STS, hello lifetime of hello authentication cookies - FedAuth tokens - can be set by hello following configuration in web.config:|

### Example
```XML
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:15:0" />
      <!-- Set requireHttps=true; -->
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:39529/" realm="https://localhost:44302/" reply="https://localhost:44302/" requireHttps="true"/>
      <!--
      Use hello code below tooenable encryption-decryption of claims received from ADFS. Thumbprint value varies based on hello certificate being used.
      <serviceCertificate>
        <certificateReference findValue="4FBBBA33A1D11A9022A5BF3492FF83320007686A" storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" />
      </serviceCertificate>
      -->
    </federationConfiguration>
  </system.identityModel.services>
```

### <a name="example"></a>Пример
Также hello, выданных время жизни токена SAML утверждения служб федерации Active Directory должно быть установлено too15 минут, выполнив следующую команду powershell на сервере ADFS hello hello:
```C#
Set-ADFSRelyingPartyTrust -TargetName “<RelyingPartyWebApp>” -ClaimsProviderName @(“Active Directory”) -TokenLifetime 15 -AlwaysRequireAuthentication $true
```

## <a id="proper-app-logout"></a>Реализация правильную выхода из приложения hello

| Название                   | Сведения      |
| ----------------------- | ------------ |
| **Компонент**               | Веб-приложение | 
| **Этап SDL**               | Создание |  
| **Применимые технологии** | Универсальный |
| **Атрибуты**              | Недоступно  |
| **Справочные материалы**              | Недоступно  |
| **Действия** | Выполните правильную выйти из приложения hello, когда пользователь нажимает выход кнопки. То есть оно должно уничтожить сеанс пользователя, а также сбросить и обнулить значение файла cookie сеанса и файла cookie проверки подлинности. Кроме того когда несколько сеансов равноценных tooa одного пользователя удостоверения, они должна совокупности заканчиваться на стороне сервера hello во время ожидания или выхода из системы. Наконец, убедитесь, что функция выхода доступна на каждой странице. |

## <a id="csrf-api"></a>Уменьшите риск атак с подделкой межсайтовых запросов в веб-интерфейсах API ASP.NET

| Название                   | Сведения      |
| ----------------------- | ------------ |
| **Компонент**               | Веб-интерфейс API | 
| **Этап SDL**               | Создание |  
| **Применимые технологии** | Универсальный |
| **Атрибуты**              | Недоступно  |
| **Справочные материалы**              | Недоступно  |
| **Действия** | Подделки межсайтовых запросов (CSRF или XSRF) — это тип атаки, в котором злоумышленник может выполнять действия в контексте безопасности hello установленного сеанса другого пользователя на веб-сайте. Цель Hello является toomodify или удалить содержимое, если указанный веб-узел hello основывается только на запрос получен tooauthenticate файлы cookie сеанса. Злоумышленник может воспользоваться этой уязвимостью, получая URL-адрес с помощью команды tooload браузера другого пользователя с уязвимым сайта, на котором hello пользователь уже вошел в. Существует множество способов для toodo злоумышленник, такие как с помощью предоставления различных веб-сайта, загружает ресурс hello уязвимым сервера или получении tooclick пользователя hello ссылку. Если hello сервер отправляет клиенту дополнительных маркеров toohello, требует hello этого токена все последующие запросы клиента tooinclude и проверяет, что все последующие запросы включать маркер, который соответствует toohello текущего сеанса, например, можно предотвратить атаки Hello с помощью hello ASP.NET AntiForgeryToken или ViewState. |

| Название                   | Сведения      |
| ----------------------- | ------------ |
| **Компонент**               | Веб-интерфейс API | 
| **Этап SDL**               | Создание |  
| **Применимые технологии** | MVC 5, MVC 6 |
| **Атрибуты**              | Недоступно  |
| **Справочные материалы**              | [Статья о предотвращении риска атак с подделкой межсайтовых запросов в веб-интерфейсах API ASP.NET](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks) |
| **Действия** | CSRF защиты и AJAX: hello маркера формы может вызвать проблемы для запросов AJAX, так как запрос AJAX может отправить данные JSON, а не данные HTML-формы. Одним из решений является toosend hello токенов в заголовок HTTP. Hello следующий код использует токены hello toogenerate синтаксис Razor, а затем добавляет маркеры tooan hello AJAX-запросом. |

### <a name="example"></a>Пример
```Javascript
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }
    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a>Пример
При обработке запроса hello, извлеките hello токены из заголовка запроса hello. Затем метод hello AntiForgery.Validate toovalidate hello маркеры. метод Validate Hello вызывает исключение, если маркеры hello не допускаются.
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

### <a name="example"></a>Пример
CSRF защиты и форм ASP.NET MVC - hello использование вспомогательного метода AntiForgeryToken для представлений; Например, поместите Html.AntiForgeryToken() в форму hello
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
}
```

### <a name="example"></a>Пример
приведенном выше примере Hello выдаст примерно hello следующим образом:
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a>Пример
В hello же время, Html.AntiForgeryToken() дает hello посетитель куки-файл называется __RequestVerificationToken с hello совпадает со значением в hello случайного скрытые значения показано выше. Toovalidate входящих формы post, добавьте метод hello [ValidateAntiForgeryToken] фильтр toohello целевого действия. Например:
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
Фильтр авторизации, проверяющий, что:
* входящий запрос Hello имеет файл cookie, вызывается __RequestVerificationToken
* Hello во входящем запросе есть `Request.Form` под названием __RequestVerificationToken
* Этих файлов cookie и `Request.Form` значения совпадают, при условии, что все хорошо, hello запрос проходит через в обычном режиме. В противном случае проверка подлинности завершается ошибкой и отображается следующее сообщение: "Обязательный маркер против подделки не был предоставлен или был недопустимым".

| Название                   | Сведения      |
| ----------------------- | ------------ |
| **Компонент**               | Веб-интерфейс API | 
| **Этап SDL**               | Создание |  
| **Применимые технологии** | MVC 5, MVC 6 |
| **Атрибуты**              | Поставщик удостоверений — ADFS или Azure AD |
| **Справочные материалы**              | [Статья об обеспечении безопасности веб-интерфейсов API с помощью отдельной учетной записи и локального имени входа в веб-API ASP.NET 2.2](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api) |
| **Действия** | Если веб-API hello защищена с помощью OAuth 2.0, затем ожидается, что токен носителя в запросе авторизации в запрос заголовок и предоставляет доступ toohello только в том случае, если маркер hello является действительным. В отличие от проверки подлинности на основе файла cookie браузеры не подключайте toorequests токенов предъявителя hello. Клиент должен tooexplicitly запросом Hello присоединить hello токена носителя в заголовке запроса hello. Таким образом, в веб-интерфейсах API ASP.NET, защищенных с помощью OAuth 2.0, токены носителя используются для защиты от подделки межсайтовых запросов. Пожалуйста Обратите внимание, что если hello MVC часть приложения hello использует проверку подлинности форм (т. е. Использование куки-файлы), маркеров защиты от подделки toobe, используемые веб-приложения MVC hello. |

### <a name="example"></a>Пример
Hello веб-API имеет toobe проинформировать toorely только на токены носителя, а не на файлы cookie. Это можно сделать путем hello следующая конфигурация в `WebApiConfig.Register` метод: '' "Си-шарп кода конфигурации. SuppressDefaultHostAuthentication(); Конфигурация. Filters.Add (новый HostAuthenticationFilter(OAuthDefaults.AuthenticationType));
```
hello SuppressDefaultHostAuthentication method tells Web API tooignore any authentication that happens before hello request reaches hello Web API pipeline, either by IIS or by OWIN middleware. That way, we can restrict Web API tooauthenticate only using bearer tokens.
