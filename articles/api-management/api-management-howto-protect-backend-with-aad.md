---
title: "aaaProtect серверной части веб-API с Azure Active Directory и управление API | Документы Microsoft"
description: "Узнайте, как tooprotect серверной части веб-API с Azure Active Directory и управления API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: f856ff03-64a1-4548-9ec4-c0ec4cc1600f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: f4b323034354aa09579c643bade47257fbf1e5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-a-web-api-backend-with-azure-active-directory-and-api-management"></a>Как tooprotect серверной части веб-API с Azure Active Directory и управления API
Здравствуйте, следуя видео показано, как toobuild серверной части веб-API и защитите его с использованием протокола OAuth 2.0 с Azure Active Directory и управления API.  В этой статье содержатся общие сведения и Дополнительные сведения о hello шагах в видео hello. Посмотрев этот 24-минутный ролик, вы познакомитесь со следующими темами.

* Создание серверной части веб-API и обеспечение ее безопасности при помощи AAD ― с 1:30
* Импорт hello API управления API - начиная с 7:10
* Настройка hello разработчика портала toocall hello API — начиная с 9:09
* Настройка типа hello toocall классического приложения API — начиная с 18:08
* Настройка политики toopre JWT проверки-авторизации запросов — начиная с 20:47

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a>Создание каталога Azure AD
toosecure резервного веб-API с помощью Azure Active Directory, следует сначала создать клиент AAD. В этом видеоролике используется клиент с именем **APIMDemo** . toocreate клиент AAD toohello входа [классический портал Azure](https://manage.windowsazure.com) и нажмите кнопку **New**->**службы приложений**->**Active Каталог**->**каталога**->**настраиваемое создание**. 

![Azure Active Directory][api-management-create-aad-menu]

В этом примере каталог с именем **APIMDemo** создается в домене по умолчанию с именем **DemoAPIM.onmicrosoft.com**. Этот каталог используется во всех hello видео.

![Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a>Создание службы веб-API, защищенной с помощью Azure Active Directory
На этом шаге создается внутренняя служба веб-API с помощью Visual Studio 2013. На этом шаге hello видео начинается с 1:30. toocreate веб-API серверного проекта в Visual Studio щелкните **файл**->**New**->**проекта**и выберите **ASP.NET Web Приложение** из hello **Web** списка шаблонов. В этом видео hello проект называется **APIMAADDemo**. Нажмите кнопку **ОК** toocreate hello проекта. 

![Visual Studio][api-management-new-web-app]

Нажмите кнопку **веб-API** из hello **выберите список шаблонов** toocreate проект веб-API. Нажмите кнопку проверки подлинности Azure Directory tooconfigure **изменить аутентификацию**.

![Новый проект][api-management-new-project]

Нажмите кнопку **учетные записи организации**и укажите hello **домена** клиента AAD. В этом примере hello домен является **DemoAPIM.onmicrosoft.com**. hello домена каталога можно получить из hello **домены** вашего каталога.

![Домены][api-management-aad-domains]

Настройте параметры требуемого hello в hello **изменить аутентификацию** диалоговое окно и нажмите кнопку **ОК**.

![Изменить проверку подлинности][api-management-change-authentication]

При нажатии кнопки **ОК** Visual Studio попытается tooregister приложения с каталогом Azure AD и может быть запрос toosign в средой Visual Studio. Войдите с помощью учетной записи администратора вашего каталога.

![Войдите в Studio tooVisual][api-management-sign-in-vidual-studio]

tooconfigure этот проект как hello Azure веб-API проверьте поле для **узлов в облаке hello** и нажмите кнопку **ОК**.

![Новый проект][api-management-new-project-cloud]

Может быть запрос toosign в tooAzure и настройте hello веб-приложения.

![Настройка][api-management-configure-web-app]

В этом примере создается новый **план службы приложений** с именем **APIMAADDemo**.

Нажмите кнопку **ОК** tooconfigure hello веб-приложения и создайте проект hello.

## <a name="add-hello-code-toohello-web-api-project"></a>Добавление проекта веб-API toohello кода hello
Hello следующим шагом в видео hello добавляет проект веб-API toohello кода hello. Этот шаг начинается с отметки времени 4:35.

Hello веб-API в этом примере реализуется базовой службы калькулятора с помощью модели и контроллера. Щелкните правой кнопкой мыши модель hello tooadd для службы hello **моделей** в **обозревателе решений** и выберите **добавить**, **класса**. Имя класса hello `CalcInput` и нажмите кнопку **добавить**.

Добавьте следующее hello `using` инструкции toohello вверху hello `CalcInput.cs` файла.

```c#
using Newtonsoft.Json;
```

Замените класс создан hello hello, следующий код.

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

Щелкните правой кнопкой мыши **Контроллеры** в **обозревателе решений** и выберите **Добавить**->**Контроллер**. Выберите элемент **Контроллер Web API 2 – пустой** и нажмите кнопку **Добавить**. Тип **CalcController** hello контроллера имя и нажмите кнопку **добавить**.

![Добавление контролера][api-management-add-controller]

Добавьте следующее hello `using` инструкции toohello вверху hello `CalcController.cs` файла.

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

Замените класс контроллера hello создается после кода hello. Этот код реализует hello `Add`, `Subtract`, `Multiply`, и `Divide` операций hello базовый API-Интерфейс калькулятора.

```c#
[Authorize]
public class CalcController : ApiController
{
    [Route("api/add")]
    [HttpGet]
    public HttpResponseMessage GetSum([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a + b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/sub")]
    [HttpGet]
    public HttpResponseMessage GetDiff([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a - b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/mul")]
    [HttpGet]
    public HttpResponseMessage GetProduct([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a * b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/div")]
    [HttpGet]
    public HttpResponseMessage GetDiv([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a / b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }
}
```

Нажмите клавишу **F6** toobuild и проверить решение hello.

## <a name="publish-hello-project-tooazure"></a>Публикация проекта tooAzure hello
В этом шаге hello Visual Studio проект является опубликованным tooAzure. На этом шаге hello видео начинается 5:45.

toopublish Здравствуйте tooAzure проекта, щелкните правой кнопкой мыши hello **APIMAADDemo** проекта в Visual Studio и выберите **публикации**. Оставьте параметры по умолчанию hello в hello **веб-публикация** диалоговое окно и нажмите кнопку **публикации**.

![Веб-публикация][api-management-web-publish]

## <a name="grant-permissions-toohello-azure-ad-backend-service-application"></a>Предоставление разрешений приложения-службы внутренних toohello Azure AD
Новое приложение hello серверной службы создается в каталоге Azure AD как часть настройки hello и процесс публикации проекта веб-API. На этом шаге hello видео начиная с 6:13, разрешения предоставляются серверной части toohello веб-API.

![Приложение][api-management-aad-backend-app]

Щелкните имя hello hello приложения tooconfigure hello необходимые разрешения. Перейдите toohello **Настройка** вкладку и прокрутите вниз toohello **tooother разрешения приложений** раздела. Нажмите кнопку hello **разрешения приложения** раскрывающегося списка рядом с **Windows** **Azure Active Directory**, установите флажок "hello" для **читать данные каталога**и нажмите кнопку **Сохранить**.

![Добавление разрешений][api-management-aad-add-permissions]

> [!NOTE]
> Если **Windows** **Azure Active Directory** — не указан в списке разрешения tooother приложений, щелкните **добавить приложение** и добавьте его из списка hello.
> 
> 

Запишите hello **URI идентификатора приложения** для использования на следующем шаге при настройке приложения Azure AD портал разработчика управления API hello.

![URI идентификатора приложения][api-management-aad-sso-uri]

## <a name="import-hello-web-api-into-api-management"></a>Импортировать hello веб-API в службе управления API
API-интерфейсы настроены из портала издателя hello API, который можно получить с помощью портала Azure hello. tooreach его, нажмите кнопку **портал издателя** из инструментов hello службы управления API. Если вы еще не создали экземпляра службы управления API, см. раздел [создания экземпляра службы управления API] [ Create an API Management service instance] в hello [управление первый API] [ Manage your first API] учебника.

![Портал издателя][api-management-management-console]

Операции могут быть [вручную добавить tooAPIs](api-management-howto-add-operations.md), или они могут быть импортированы. В этом видео операции импортируются в формате Swagger начиная с отметки времени 6:40.

Создайте файл с именем `calcapi.json` с следующие содержимое и сохраните его tooyour компьютера. Убедитесь, что hello `host` атрибут указывает серверной части tooyour веб-API. В этом примере используется `"host": "apimaaddemo.azurewebsites.net"` .

```json
{
  "swagger": "2.0",
  "info": {
    "title": "Calculator",
    "description": "Arithmetics over HTTP!",
    "version": "1.0"
  },
  "host": "apimaaddemo.azurewebsites.net",
  "basePath": "/api",
  "schemes": [
    "http"
  ],
  "paths": {
    "/add?a={a}&b={b}": {
      "get": {
        "description": "Responds with a sum of two numbers.",
        "operationId": "Add two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>51</code>.",
            "required": true,
            "type": "string",
            "default": "51",
            "enum": [
              "51"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>49</code>.",
            "required": true,
            "type": "string",
            "default": "49",
            "enum": [
              "49"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/sub?a={a}&b={b}": {
      "get": {
        "description": "Responds with a difference between two numbers.",
        "operationId": "Subtract two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>50</code>.",
            "required": true,
            "type": "string",
            "default": "50",
            "enum": [
              "50"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/div?a={a}&b={b}": {
      "get": {
        "description": "Responds with a quotient of two numbers.",
        "operationId": "Divide two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/mul?a={a}&b={b}": {
      "get": {
        "description": "Responds with a product of two numbers.",
        "operationId": "Multiply two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>5</code>.",
            "required": true,
            "type": "string",
            "default": "5",
            "enum": [
              "5"
            ]
          }
        ],
        "responses": { }
      }
    }
  }
}
```

Калькулятор hello tooimport API, нажмите кнопку **API-интерфейсы** из hello **API управления** меню hello слева, а затем нажмите **импорта API**.

![Кнопка импорта API][api-management-import-api]

Выполните следующие шаги tooconfigure hello калькулятора API hello.

1. Нажмите кнопку **из файла**, Обзор toohello `calculator.json` файл был сохранен и нажмите кнопку hello **Swagger** переключатель.
2. Тип **calc** в hello **суффикс URL-адрес API** текстового поля.
3. Нажмите кнопку в hello **продуктов (необязательно)** и выберите **начальный**.
4. Нажмите кнопку **Сохранить** tooimport hello API.

![Добавление нового API][api-management-import-new-api]

После импорта hello API hello сводной страницы для hello API отображается в портал издателя hello.

## <a name="call-hello-api-unsuccessfully-from-hello-developer-portal"></a>Вызвать hello API неудачно с портала разработчиков hello
На этом этапе hello API была импортирована в API управления, но еще невозможен успешно с портала разработчиков hello поскольку hello серверная служба защищена с помощью проверки подлинности Azure AD. Это показано в видео hello, начиная с 7:40 с помощью hello следующие шаги.

Нажмите кнопку **портал разработчиков** из hello правой верхней части портала издателя hello.

![Портал разработчика][api-management-developer-portal-menu]

Нажмите кнопку **API-интерфейсы** и нажмите кнопку hello **калькулятора** API.

![Портал разработчика][api-management-dev-portal-apis]

Щелкните **Попробовать**.

![Попробовать][api-management-dev-portal-try-it]

Нажмите кнопку **отправки** и записать состояние ответа hello **проверки подлинности 401**.

![Отправка][api-management-dev-portal-send-401]

Hello запрос не авторизован, так как API внутреннего сервера hello защищен службой Azure Active Directory. До успешного вызова hello API портал разработчика hello должен иметь настроенное tooauthorize разработчиков, использующих OAuth 2.0. Этот процесс описан в следующих разделах hello.

## <a name="register-hello-developer-portal-as-an-aad-application"></a>Зарегистрировать портал разработчиков hello как приложение AAD
Hello первым шагом в настройке hello разработчика tooauthorize портала разработчиков, использующих OAuth 2.0 — портал разработчиков hello tooregister как приложение AAD. Это продемонстрировано начиная с 8:27 в видео hello.

Клиент Azure AD toohello из hello первым шагом этого видео, в этом примере перейдите **APIMDemo** и перейдите toohello **приложений** вкладки.

![Новое приложение][api-management-aad-new-application-devportal]

Нажмите кнопку hello **добавить** toocreate новое приложение Azure Active Directory, а кнопку **добавить приложение, разрабатываемое моей организацией**.

![Новое приложение][api-management-new-aad-application-menu]

Выберите **веб-приложение или веб-API**, введите имя и щелкните стрелку hello. В этом примере используется **APIMDeveloperPortal** .

![Новое приложение][api-management-aad-new-application-devportal-1]

Для **URL-адрес входа** введите hello URL-адрес службы управления API и добавьте `/signin`. В этом примере используется `https://contoso5.portal.azure-api.net/signin` .

Для **URL ИД приложения** введите hello URL-адрес службы управления API и добавьте несколько уникальных знаков. Это могут быть любые знаки. В данном примере используется `https://contoso5.portal.azure-api.net/dp`. При необходимости hello **свойства приложения** будут настроены, нажмите кнопку приложения hello toocreate флажок hello.

![Новое приложение][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a>Настройка сервера авторизации OAuth 2.0 в управлении API
Hello следующим шагом является tooconfigure сервера авторизации OAuth 2.0 в службе управления API. Здесь демонстрируется hello видео, начиная с 9:43.

Нажмите кнопку **безопасности** меню управления API hello hello левой части экрана выберите **OAuth 2.0**и нажмите кнопку **добавьте авторизацию** сервера.

![Добавление сервера авторизации][api-management-add-authorization-server]

Введите имя и описание (необязательно) в hello **имя** и **описание** поля. Эти поля обязательны для сервера авторизации OAuth 2.0 hello используется tooidentify в пределах экземпляра службы управления API hello. В этом примере используется **демоверсия сервера авторизации** . Позже при указании сервера toobe OAuth 2.0, используемый для проверки подлинности для API будет выбрать это имя.

Для hello **URL-адрес страницы регистрации клиента** введите значение заполнителя, например `http://localhost`.  Hello **URL-адрес страницы регистрации клиента** точки toohello страницы, что у пользователей, можно использовать toocreate и настроить свои собственные учетные записи для поставщиков OAuth 2.0, которые поддерживают управление учетными записями пользователей. В этом примере пользователи не создают и не настраивают собственные учетные записи, поэтому используется заполнитель.

![Добавление сервера авторизации][api-management-add-authorization-server-1]

Затем укажите **URL-адрес конечной точки авторизации** и **URL-адрес конечной точки маркера**.

![Сервер авторизации][api-management-add-authorization-server-1a]

Эти значения могут быть получены из hello **конечные точки приложения** страница hello AAD приложения, созданного для hello портал разработчиков. конечные точки hello tooaccess перейдите toohello **Настройка** для AAD приложения hello и нажмите кнопку **просмотреть конечные точки**.

![Приложение][api-management-aad-devportal-application]

![Просмотреть конечные точки][api-management-aad-view-endpoints]

Копировать hello **конечная точка авторизации OAuth 2.0** и вставьте его в hello **URL-адрес конечной точки авторизации** текстового поля.

![Добавление сервера авторизации][api-management-add-authorization-server-2]

Копировать hello **конечная точка маркера OAuth 2.0** и вставьте его в hello **токен URL-адрес конечной точки** текстового поля.

![Добавление сервера авторизации][api-management-add-authorization-server-2a]

Кроме toopasting в конечную точку токена hello, добавить дополнительный текст параметр с именем **ресурсов** используйте для значение hello hello **URI идентификатора приложения** из AAD приложения hello серверной службы, которая была hello создается, когда проект Visual Studio hello был опубликован.

![URI идентификатора приложения][api-management-aad-sso-uri]

Затем укажите учетные данные клиента hello. Hello учетные данные для hello ресурс, tooaccess, в этом случае hello портал разработчиков.

![Учетные данные клиента][api-management-client-credentials]

tooget hello **идентификатор клиента**, перейдите toohello **Настройка** вкладка hello приложения AAD для разработчика hello портала и скопируйте hello **идентификатор клиента**.

tooget hello **секрет клиента** щелкните hello **выберите длительность** раскрывающееся меню в hello **ключей** статьи и указать интервал. В данном примере используется интервал 1 год.

![Идентификатор клиента][api-management-aad-client-id]

Нажмите кнопку **Сохранить** toosave hello конфигурации и отображения hello ключ. 

> [!IMPORTANT]
> Запишите этот ключ. После закрытия окна конфигурации hello Azure Active Directory hello ключ не будет отображаться в дальнейшем.
> 
> 

Hello ключа toohello Копировать буфер, портал издателя задней toohello коммутатора, вставьте ключ hello в hello **секрет клиента** в текстовое поле и нажмите кнопку **Сохранить**.

![Добавление сервера авторизации][api-management-add-authorization-server-3]

Сразу после hello учетных данных клиента является предоставления кода авторизации. Скопируйте этот код авторизации и задней tooyour коммутатора приложения портала Azure AD разработчик страницы и вставьте предоставления авторизации hello в hello **URL-адрес ответа** , а щелкните **Сохранить** еще раз.

![URL-адрес ответа][api-management-aad-reply-url]

Hello следующим шагом является tooconfigure hello разрешения для портала разработчиков hello AAD приложения. Нажмите кнопку **разрешения приложения** и установите флажок "hello" для **читать данные каталога**. Нажмите кнопку **Сохранить** toosave это изменить и нажмите кнопку **добавить приложение**.

![Добавление разрешений][api-management-add-devportal-permissions]

Щелкните значок поиска hello, тип **APIM** в hello начиная с выбора **APIMAADDemo**и щелкните флажок toosave hello.

![Добавление разрешений][api-management-aad-add-app-permissions]

Нажмите кнопку **делегированные разрешения** для **APIMAADDemo** и установите флажок "hello" для **APIMAADDemo доступа**и нажмите кнопку **Сохранить**. Это позволяет hello разработчика приложения портала tooaccess hello серверной службы.

![Добавление разрешений][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-hello-calculator-api"></a>Включение авторизации пользователя OAuth 2.0 для hello калькулятора API
Теперь, когда hello OAuth 2.0 сервер настроен, можно указать его в hello параметры безопасности для API. Здесь демонстрируется hello видео, начиная с 14:30.

Нажмите кнопку **API-интерфейсы** в hello в левом меню и нажмите кнопку **калькулятора** tooview и настроить его параметры.

![API «Калькулятор»][api-management-calc-api]

Перейдите toohello **безопасности** проверьте hello **OAuth 2.0** флажок, выберите hello требуемой авторизации сервера из hello **сервер авторизации** раскрывающегося списка и нажмите кнопку **Сохранить**.

![API «Калькулятор»][api-management-enable-aad-calculator]

## <a name="successfully-call-hello-calculator-api-from-hello-developer-portal"></a>Успешно вызовите hello API калькулятора с портала разработчиков hello
Теперь, когда на hello API настроено авторизации hello OAuth 2.0, из центра разработчиков hello его операции могут вызываться успешно. Здесь демонстрируется hello видео, начиная с 15:00.

Перейдите назад toohello **добавьте два целых числа** операции службы калькулятора hello в портал разработчиков hello и нажмите кнопку **опробовать**. Примечание hello новый элемент в hello **авторизации** соответствующий сервер авторизации toohello, только что добавленные статьи.

![API «Калькулятор»][api-management-calc-authorization-server]

Выберите **код авторизации** из авторизации hello раскрывающемся списке и введите учетные данные учетной записи toouse hello hello. Если вы уже вошли в учетную запись hello не потребуется.

![API «Калькулятор»][api-management-devportal-authorization-code]

Нажмите кнопку **отправки** и Примечание hello **состояние ответа** из **200 ОК** и hello результатов операции hello в ответ содержимого hello.

![API «Калькулятор»][api-management-devportal-response]

## <a name="configure-a-desktop-application-toocall-hello-api"></a>Настройка типа hello toocall классического приложения API
Hello Далее процедура hello видео начинается с 16:30 и настраивает hello toocall простое классическое приложение API. Первым шагом Hello — tooregister hello классическое приложение в Azure AD и присвойте ему доступа toohello каталога и toohello серверной службы. В 18:25 отсутствует Демонстрация классического приложения hello вызова операции калькулятора hello API.

## <a name="configure-a-jwt-validation-policy-toopre-authorize-requests"></a>Настройка политики toopre JWT проверки-авторизации запросов
Hello заключительную процедуру в видео hello начинается с 20:48 и показано, как toouse hello [проверка JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) toopre политики-авторизации запросов путем проверки hello токены доступа для каждого входящего запроса. Если запрос hello не проверяется по hello политики проверки JWT, запрос hello заблокирован управления API и не будут передаваться toohello серверной части.

```xml
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">
    <openid-config url="https://login.microsoftonline.com/DemoAPIM.onmicrosoft.com/.well-known/openid-configuration" />
    <required-claims>
        <claim name="aud">
            <value>https://DemoAPIM.NOTonmicrosoft.com/APIMAADDemo</value>
        </claim>
    </required-claims>
</validate-jwt>
```

Другой демонстрации настройки и использования этой политики см. [177 серии охватывают облачные: более функции API-Интерфейсов управления](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) и too13:50 Перемотка вперед. Перемотка вперед too15:00 toosee hello политики, настроенные в редакторе hello политики и затем too18:50 демонстрацию вызова операции из портала разработчиков hello как с и без hello требуется маркер авторизации.

## <a name="next-steps"></a>Дальнейшие действия
* См. другие [видео](https://azure.microsoft.com/documentation/videos/index/?services=api-management) об управлении API.
* Для других способов toosecure безопасности внутренней службы. в разделе [взаимной проверки подлинности сертификатов](api-management-howto-mutual-certificates.md).

[api-management-management-console]: ./media/api-management-howto-protect-backend-with-aad/api-management-management-console.png

[api-management-import-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-new-api.png
[api-management-create-aad-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad-menu.png
[api-management-create-aad]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad.png
[api-management-new-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-web-app.png
[api-management-new-project]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project.png
[api-management-new-project-cloud]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project-cloud.png
[api-management-change-authentication]: ./media/api-management-howto-protect-backend-with-aad/api-management-change-authentication.png
[api-management-sign-in-vidual-studio]: ./media/api-management-howto-protect-backend-with-aad/api-management-sign-in-vidual-studio.png
[api-management-configure-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-configure-web-app.png
[api-management-aad-domains]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-domains.png
[api-management-add-controller]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-controller.png
[api-management-web-publish]: ./media/api-management-howto-protect-backend-with-aad/api-management-web-publish.png
[api-management-aad-backend-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-backend-app.png
[api-management-aad-add-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-permissions.png
[api-management-developer-portal-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-developer-portal-menu.png
[api-management-dev-portal-apis]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-apis.png
[api-management-dev-portal-try-it]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-try-it.png
[api-management-dev-portal-send-401]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-send-401.png
[api-management-aad-new-application-devportal]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal.png
[api-management-aad-new-application-devportal-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-1.png
[api-management-aad-new-application-devportal-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-2.png
[api-management-aad-devportal-application]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-devportal-application.png
[api-management-add-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server.png
[api-management-aad-sso-uri]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-sso-uri.png
[api-management-aad-view-endpoints]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-view-endpoints.png
[api-management-aad-client-id]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-client-id.png
[api-management-add-authorization-server-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1.png
[api-management-add-authorization-server-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2.png
[api-management-add-authorization-server-2a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2a.png
[api-management-add-authorization-server-3]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-3.png
[api-management-aad-reply-url]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-reply-url.png
[api-management-add-devportal-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-devportal-permissions.png
[api-management-aad-add-app-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-app-permissions.png
[api-management-aad-add-delegated-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-delegated-permissions.png
[api-management-calc-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-api.png
[api-management-enable-aad-calculator]: ./media/api-management-howto-protect-backend-with-aad/api-management-enable-aad-calculator.png
[api-management-devportal-authorization-code]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-authorization-code.png
[api-management-devportal-response]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-response.png
[api-management-calc-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-authorization-server.png
[api-management-add-authorization-server-1a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1a.png
[api-management-client-credentials]: ./media/api-management-howto-protect-backend-with-aad/api-management-client-credentials.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-aad-application-menu.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Manage your first API]: api-management-get-started.md
