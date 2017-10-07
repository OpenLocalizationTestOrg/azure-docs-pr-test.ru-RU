---
title: "aaaCommunicate с любой конечной точке по протоколу HTTP - приложения логики Azure | Документы Microsoft"
description: "Создание приложений логики, которые обмениваются данными с любой конечной точкой по протоколу HTTP."
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: e11c6b4d-65a5-4d2d-8e13-38150db09c0b
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: 9793601839437a2b880bdb81e15881270cacc963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http-action"></a>Приступая к работе с hello действия HTTP

С hello действия HTTP можно расширить рабочие процессы для вашей организации и передачи конечной точки tooany по протоколу HTTP.

Вы можете:

* Создайте рабочие процессы приложений логики, которые будут активироваться, когда управляемый вами веб-сайт выйдет из строя.
* Связь tooany конечной точки через HTTP tooextend рабочие процессы в другие службы.

tooget к работе с помощью действия hello HTTP в приложении логику в разделе [создания логики приложения](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-http-trigger"></a>Использование триггера hello HTTP
Триггер — это событие, которое может быть hello используется toostart рабочий процесс, который определен в приложение логики. [Дополнительные сведения о триггерах](connectors-overview.md).

Вот пример последовательность как триггер tooset копирование hello HTTP в конструктор логику приложения hello.

1. Добавьте триггер HTTP hello в логике приложения.
2. Заполните параметры hello для hello HTTP конечной точки, которые должны toopoll.
3. Измените интервал повторения hello на том, как часто должна опрашивать.

   приложения логики Hello теперь срабатывает содержимым, который возвращается при каждой проверке.

   ![Триггер HTTP](./media/connectors-native-http/using-trigger.png)

### <a name="how-hello-http-trigger-works"></a>Как работает триггер HTTP hello

триггер Hello HTTP отправляет конечную точку tooHTTP вызов через заданный интервал. По умолчанию любой код HTTP-ответа, которое меньше 300 вызывает toorun логику приложения. toospecify ли приложение hello логики должен срабатывать, можно изменить логику приложение hello в окне просмотра кода и добавьте условие, которое принимает после hello вызовов HTTP. Ниже приведен пример HTTP триггер, срабатывающий при hello вернул код состояния, больше или равно слишком`400`.

```javascript
"Http":
{
    "conditions": [
        {
            "expression": "@greaterOrEquals(triggerOutputs()['statusCode'], 400)"
        }
    ],
    "inputs": {
        "method": "GET",
        "uri": "https://blogs.msdn.microsoft.com/logicapps/",
        "headers": {
            "accept-language": "en"
        }
    },
    "recurrence": {
        "frequency": "Second",
        "interval": 15
    },
    "type": "Http"
}
```

Полные сведения о параметрах триггер hello HTTP доступны на [MSDN](https://msdn.microsoft.com/library/azure/mt643939.aspx#HTTP-trigger).

## <a name="use-hello-http-action"></a>Используйте действие hello HTTP

Действие — это операции, выполняемые hello рабочего процесса, определенные в приложение логики. 
[Дополнительные сведения о действиях](connectors-overview.md).

1. Выберите **Новый шаг** > **Добавить действие**.
3. Введите в поле поиска действие hello **http** действия toolist hello HTTP.
   
    ![Выберите действие hello HTTP](./media/connectors-native-http/using-action-1.png)

4. Добавьте все необходимые параметры для вызова hello HTTP.
   
    ![Полный hello действия HTTP](./media/connectors-native-http/using-action-2.png)

5. На панели инструментов конструктора hello, нажмите кнопку **Сохранить**. Логику приложения будет сохранен и опубликован (активированной) на hello то же время.

## <a name="http-trigger"></a>Триггер HTTP
Ниже приведены сведения hello для hello триггера, который поддерживает этот соединитель. Соединитель Hello HTTP имеет один триггер.

| Триггер | Описание |
| --- | --- |
| HTTP |Отправляет вызов HTTP и возвращает содержимое ответа hello. |

## <a name="http-action"></a>Действие HTTP
Ниже приведены hello сведения для действия hello, поддерживающий этот соединитель. Соединитель Hello HTTP имеет один возможным действием.

| Действие | Описание |
| --- | --- |
| HTTP |Отправляет вызов HTTP и возвращает содержимое ответа hello. |

## <a name="http-details"></a>Сведения о HTTP
Hello следующих таблицах описаны необходимые hello и необязательные поля ввода для действия hello и hello соответствующие сведения о выходных данных, связанных с помощью hello действия.

#### <a name="http-request"></a>HTTP-запрос
Здесь представлены Hello поля входных данных для действия hello, поэтому исходящих HTTP-запроса.
Звездочка (*) означает, что это поле обязательное для заполнения.

| Отображаемое имя | Имя свойства | Описание |
| --- | --- | --- |
| Метод* |метод |Команда toouse Hello HTTP |
| URI* |uri |Hello URI для hello HTTP-запроса |
| Заголовки |headers |Объект JSON tooinclude заголовки HTTP |
| Текст |текст |Hello HTTP-запроса |
| Аутентификация |authentication |Сведения в hello [проверки подлинности](#authentication) раздела |

<br>

#### <a name="output-details"></a>Сведения о выходных данных
Hello ниже приведены сведения о выходных данных для hello HTTP-ответа.

| Имя свойства | Тип данных | Описание |
| --- | --- | --- |
| Заголовки |object |Заголовки ответов |
| Текст |object |Объект ответа |
| Код состояния |int |HTTP status code (Код состояния HTTP) |

## <a name="authentication"></a>Аутентификация
функция логики приложения Hello позволяет toouse разные типы проверки подлинности на основе конечных точек HTTP. Способ проверки подлинности можно использовать с hello **HTTP**,  **[HTTP + Swagger](connectors-native-http-swagger.md)**, и  **[HTTP веб-перехватчика](connectors-native-webhook.md)**  соединители. Привет, следующие типы проверки подлинности можно настроить:

* [Обычная аутентификация](#basic-authentication)
* [Аутентификация на основе сертификата клиента](#client-certificate-authentication)
* [Аутентификация Azure Active Directory (Azure AD) OAuth](#azure-active-directory-oauth-authentication)

#### <a name="basic-authentication"></a>Обычная аутентификация

для обычной проверки подлинности требуется Hello следующий объект проверки подлинности.
Звездочка (*) означает, что это поле обязательное для заполнения.

| Имя свойства | Тип данных | Описание |
| --- | --- | --- |
| Тип* |type |Тип аутентификации (для обычной аутентификации значение должно быть `Basic`) |
| Имя пользователя* |Имя пользователя |Tooauthenticate имя пользователя |
| Пароль* |пароль |Пароль tooauthenticate |

> [!TIP]
> Пароль, который не удается получить из определения hello toouse используйте `securestring` параметр и hello `@parameters()`  
>  [функции определения рабочего процесса](http://aka.ms/logicappdocs).

Например:

```javascript
{
    "type": "Basic",
    "username": "user",
    "password": "test"
}
```

#### <a name="client-certificate-authentication"></a>Аутентификация на основе сертификата клиента

Hello следующий объект проверки подлинности требуется для проверки подлинности сертификата клиента. Звездочка (*) означает, что это поле обязательное для заполнения.

| Имя свойства | Тип данных | Описание |
| --- | --- | --- |
| Тип* |type |Здравствуйте, тип проверки подлинности (должно быть `ClientCertificate` для SSL-сертификатов клиента) |
| PFX* |pfx |Hello кодировке Base64 содержимое файла обмена личной информацией (PFX) hello |
| Пароль* |пароль |Здравствуйте, tooaccess Hello пароль PFX-файла |

> [!TIP]
> toouse параметр, который невозможен в определении hello после сохранения приложения hello логики, можно использовать `securestring` параметр и hello `@parameters()`  
>  [функции определения рабочего процесса](http://aka.ms/logicappdocs).

Например:

```javascript
{
    "type": "ClientCertificate",
    "pfx": "aGVsbG8g...d29ybGQ=",
    "password": "@parameters('myPassword')"
}
```

#### <a name="azure-ad-oauth-authentication"></a>Аутентификация Azure AD OAuth
После проверки подлинности объекта Hello необходим для проверки подлинности Azure AD OAuth. Звездочка (*) означает, что это поле обязательное для заполнения.

| Имя свойства | Тип данных | Описание |
| --- | --- | --- |
| Тип* |type |Здравствуйте, тип проверки подлинности (должно быть `ActiveDirectoryOAuth` для Azure AD OAuth) |
| Клиент* |tenant |Здравствуйте, идентификатор клиента для клиента hello Azure AD |
| Аудитория* |audience |Hello ресурс запрашивается toouse авторизации. Например: `https://management.core.windows.net/` |
| Идентификатор клиента* |clientid |Здравствуйте, идентификатор клиента приложения hello Azure AD |
| Секрет* |secret |секрет Hello hello клиента, который запрашивает токен hello |

> [!TIP]
> Можно использовать `securestring` параметр и hello `@parameters()` [функции определения рабочего процесса](http://aka.ms/logicappdocs) toouse параметр, который не будет доступной для чтения в определении hello после сохранения.
> 
> 

Например:

```javascript
{
    "type": "ActiveDirectoryOAuth",
    "tenant": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "audience": "https://management.core.windows.net/",
    "clientId": "34750e0b-72d1-4e4f-bbbe-664f6d04d411",
    "secret": "hcqgkYc9ebgNLA5c+GDg7xl9ZJMD88TmTJiJBgZ8dFo="
}
```

## <a name="next-steps"></a>Дальнейшие действия
Теперь попробуйте платформы hello и [создания логики приложения](../logic-apps/logic-apps-create-a-logic-app.md). Вы можете просматривать hello другие доступные соединители в приложениях для логики, просмотрев нашей [список API-интерфейсы](apis-list.md).

