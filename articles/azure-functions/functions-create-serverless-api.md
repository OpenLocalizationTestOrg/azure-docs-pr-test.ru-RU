---
title: "aaaCreate без сервера API, с помощью функции Azure | Документы Microsoft"
description: "Как toocreate без сервера API, с помощью функции Azure"
services: functions
author: mattchenderson
manager: erikre
ms.service: functions
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: mahender
ms.custom: mvc
ms.openlocfilehash: 877e3b229d5477fc5fec594ccd284fb55d7f3c07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-serverless-api-using-azure-functions"></a>Создание бессерверного API с помощью Функций Azure

В этом учебнике вы узнаете, как функции Azure обеспечивает toobuild высокомасштабируемых API-интерфейсы. Функции Azure сочетается с набором встроенных триггеров HTTP и привязками, что позволяет легко tooauthor конечную точку в различных языках, включая Node.JS, C# и многое другое. В этом учебнике будет выполнена настройка триггера HTTP toohandle определенных действий в конструкции своего API. Вы также подготовите ваш API к увеличению размеров, интегрировав его с прокси-серверами Функций Azure и установив макет API. Все это можно сделать поверх hello функции без сервера вычислительную среду, поэтому tooworry о масштабировании ресурсов не нужно — просто позволяет сосредоточиться на логике API.

## <a name="prerequisites"></a>Предварительные требования 

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

Полученная функция Hello будет использоваться для hello конца данного учебника.

### <a name="sign-in-tooazure"></a>Войдите в tooAzure

Здравствуйте, откройте портал Azure. toodo, вход слишком[https://portal.azure.com](https://portal.azure.com) с учетной записью Azure.

## <a name="customize-your-http-function"></a>Настройка функции HTTP

По умолчанию функции активации HTTP является настроенным tooaccept любой метод HTTP. Отсутствует URL-адрес по умолчанию hello формы `http://<yourapp>.azurewebsites.net/api/<funcname>?code=<functionkey>`. Если вы следовали hello краткое руководство, затем `<funcname>` , скорее всего, будет выглядеть примерно так «HttpTriggerJS1». В этом разделе будет изменить hello функция toorespond только tooGET запросов к `/api/hello` вместо маршрутизации. 

Перейдите tooyour функции hello портал Azure. Выберите **Интеграция** в hello навигации слева.

![Настройка функции HTTP](./media/functions-create-serverless-api/customizing-http.png)

Используйте параметры триггера HTTP, как указано в таблице hello.

| Поле | Образец значения | Описание |
|---|---|---|
| Разрешенные методы HTTP | Выбранные методы | Определяет, какие методы HTTP может быть tooinvoke используется эта функция |
| Выбранные методы HTTP | ПОЛУЧЕНИЕ | Разрешает только выбранных toobe методы HTTP, используемых tooinvoke этой функции |
| Шаблон маршрута | /hello | Определяет, какие маршрута используется tooinvoke этой функции |

Обратите внимание, что не содержит hello `/api` основной префикс пути в шаблоне маршрута hello, как обрабатывается глобальный параметр.

Щелкните **Сохранить**.

Дополнительные сведения см. в статье [Привязки HTTP и webhook в функциях Azure](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#customizing-the-http-endpoint).

### <a name="test-your-api"></a>Тестирование API

Теперь необходимо проверьте на toosee функция его работа с hello новую поверхность API.

Перейдите назад toohello разработки страницы, щелкнув имя функции hello в hello навигации слева.

Нажмите кнопку **получить URL-адрес функции** и скопируйте URL-адрес hello. Вы увидите, что он использует hello `/api/hello` теперь маршрутизации.

Скопируйте URL-адрес hello в новую вкладку браузера или предпочтительный клиент REST. По умолчанию браузер использует функцию GET.

Запустите функции hello и убедитесь, что он работает. Параметр «name» hello tooprovide может потребоваться как краткое руководство кода hello toosatisfy строку запроса.

Можно также попытаться вызова hello конечной точки с другой tooconfirm метод HTTP, что функция hello не выполняется. Для этого потребуется toouse клиента REST, например перелистывание, почтальон или Fiddler.

## <a name="proxies-overview"></a>Общие сведения о прокси-серверах

В следующем разделе hello обнаружатся API через прокси-сервер. Azure функции прокси имеет функцию предварительного просмотра, позволяющая ресурсы tooother tooforward запросов. Так же, как определить конечную точку HTTP с триггером HTTP, но вместо написания кода tooexecute при вызове этой конечной точки, можно предоставить реализацию удаленного tooa URL-адрес. Это позволяет toocompose API нескольких источников в одну область API, которой могут легко tooconsume клиентов. Это особенно полезно в том случае, если вы хотите toobuild API как микрослужбами.

Прокси-сервер может указывать ресурсов tooany HTTP, такие как:
- Функции Azure 
- Приложения API в [службе приложений Azure](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is).
- Контейнеры Docker в [службе приложений под управлением Linux](https://docs.microsoft.com/azure/app-service/app-service-linux-readme).
- Любой другой размещенный API.

toolearn Дополнительные сведения о прокси-серверы, в разделе [работа с прокси-серверы функции Azure (Предварительная версия)].

## <a name="create-your-first-proxy"></a>Создание первого прокси-сервера

В этом разделе вы создадите новый прокси какие служит в качестве tooyour переднего плана общий API. 

### <a name="setting-up-hello-frontend-environment"></a>Настройка среды hello переднего плана

Повторите шаги hello слишком[создать приложение функция](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function#create-a-function-app) toocreate новое приложение функции, в которой будет создан прокси-сервера. Это новое приложение будет служить hello переднего плана для наших API и приложение hello функция, которую вы редактировали будет служить в качестве серверной части.

Перейдите в новое приложение функция переднего плана tooyour hello портала.

Выберите элемент **Параметры**. Затем переключать **включить Azure функции прокси-серверов (Предварительная версия)** слишком «On».

Выберите **Platform Settings** (Параметры платформы), а затем — **Параметры приложения**.

Прокрутите список вниз слишком**параметры приложения** и создать новый параметр с ключом «HELLO_HOST». Задать ведущим toohello значение серверной части функции приложения, например `<YourApp>.azurewebsites.net`. Это часть URL-адреса hello, скопированное ранее при тестировании функции HTTP. Будет ссылаться этот параметр в конфигурации hello позже.

> [!NOTE] 
> Параметры приложения рекомендуется использовать tooprevent конфигурации узла hello зависимость жестко среды для hello прокси-сервера. С помощью параметров приложения означает, что hello конфигурация прокси-сервера можно переместить между средами и будут применены параметры среды приложения hello.

Щелкните **Сохранить**.

### <a name="creating-a-proxy-on-hello-frontend"></a>Создание учетной записи-посредника на сервере переднего плана hello

Перейдите назад tooyour переднего плана функции приложения hello портала.

В левой области навигации hello щелкните hello знак плюс «+» Далее слишком «Прокси-сервер (Предварительная версия)».

![Создание прокси](./media/functions-create-serverless-api/creating-proxy.png)

Используйте параметры прокси-сервера, как указано в таблице hello.

| Поле | Образец значения | Описание |
|---|---|---|
| Имя | HelloProxy | Понятное имя, используемое только для управления |
| Шаблон маршрута | /api/hello | Определяет, какие маршрута используется tooinvoke этот прокси-сервер |
| Внутренний URL-адрес | https://%HELLO_HOST%/api/hello | Указывает, что запроса hello toowhich hello конечной точки должно быть прокси |

Обратите внимание, что учетные записи-посредники не предоставляет hello `/api` префикс пути к базовой папке и это должно быть включено в шаблон маршрута hello.

Hello `%HELLO_HOST%` синтаксис будет ссылаться на параметр приложения hello, созданного ранее. Hello разрешен URL-адрес будет указывать tooyour исходной функции.

Щелкните **Создать**.

Можно опробовать новый прокси-сервера путем копирования hello URL-адрес прокси-сервера и его тестирование в браузере hello или с HTTP клиента по вашему выбору.

## <a name="create-a-mock-api"></a>Создание макета API

Далее будет использовать прокси-сервер toocreate макетов API для вашего решения. Это позволяет Разработка клиентских приложений tooprogress без необходимости полностью реализован серверной hello. Позже при разработке можно создать новое приложение функция, которая поддерживает эту логику и перенаправления вашей tooit прокси-сервера.

toocreate данный макет API, мы создадим новый прокси-сервер, с применением hello [редактор службы приложения](https://github.com/projectkudu/kudu/wiki/App-Service-Editor). tooget к работе, перейдите tooyour функции приложения hello портала. Выберите **Функции платформы** и найдите **редактор службы приложений**. При нажатии этой кнопки открывается редактор службы приложения hello в новой вкладке.

Выберите `proxies.json` в hello навигации слева. Это файл hello, в котором хранятся hello конфигурации для всех прокси. При использовании hello [функции методы развертывания](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), это файл hello будут обслуживаться в системе управления версиями. toolearn более об этом файле см [учетные записи-посредники Расширенная конфигурация](https://docs.microsoft.com/azure/azure-functions/functions-proxies#advanced-configuration).

Если вы выполнили моменту, ваш proxies.json должен выглядеть hello следующим образом:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        }
    }
}
```

Затем добавьте макет API. Замените файл proxies.json hello следующее:

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "HelloProxy": {
            "matchCondition": {
                "route": "/api/hello"
            },
            "backendUri": "https://%HELLO_HOST%/api/hello"
        },
        "GetUserByName" : {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/users/{username}"
            },
            "responseOverrides": {
                "response.statusCode": "200",
                "response.headers.Content-Type" : "application/json",
                "response.body": {
                    "name": "{username}",
                    "description": "Awesome developer and master of serverless APIs",
                    "skills": [
                        "Serverless",
                        "APIs",
                        "Azure",
                        "Cloud"
                    ]
                }
            }
        }
    }
}
```

При этом добавляется новый прокси, «GetUserByName» без свойства backendUri hello. Вместо того чтобы вызывать другой ресурс, она изменяет hello ответа по умолчанию из прокси-серверы, используя переопределения ответа. Переопределение запроса и ответа может также использоваться в сочетании с URL-адресом внутреннего сервера. Это особенно полезно, когда перенаправление tooa устаревших систем, требующие toomodify заголовки, параметры запроса, toolearn т. д. Дополнительные сведения о переопределения запроса и ответа, в разделе [изменение запросов и ответов в прокси-](https://docs.microsoft.com/azure/azure-functions/functions-proxies#a-namemodify-requests-responsesamodifying-requests-and-responses).

Протестируйте макетов API, вызывающему Привет `/api/users/{username}` конечную точку с помощью браузера или REST клиента по вашему выбору. Быть убедиться, что tooreplace _{username}_ с строковое значение, представляющее имя пользователя.

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике вы узнали, как toobuild и настраивать API для функций Azure. Вы также узнали, как toobring несколько API, в том числе фиктивных, друг с другом виде единой рабочей области API. Можно использовать эти методы toobuild out API-интерфейсы любой сложности, все время работы на hello без сервера вычислений модели, предоставляемой функций Azure.

Hello следующие ссылки могут пригодиться при разработке дальнейшей API:

- [Привязки HTTP и webhook в функциях Azure](https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook)
- [работа с прокси-серверы функции Azure (Предварительная версия)]
- [Создание метаданных OpenAPI 2.0 (Swagger) для приложения-функции (предварительная версия)](https://docs.microsoft.com/azure/azure-functions/functions-api-definition-getting-started)


[Create your first function]: https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function
[работа с прокси-серверы функции Azure (Предварительная версия)]: https://docs.microsoft.com/azure/azure-functions/functions-proxies
