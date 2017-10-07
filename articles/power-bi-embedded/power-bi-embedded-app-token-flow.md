---
title: "aaaAuthenticating и авторизации с Power BI Embedded"
description: "Аутентификация и авторизация в Power BI Embedded"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 1c1369ea-7dfd-4b6e-978b-8f78908fd6f6
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 483ca0499e8d03584e1151d3d278c0179d4b8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a>Аутентификация и авторизация в Power BI Embedded

использует службы Power BI Embedded Hello **ключей** и **токенов приложения** для проверки подлинности и авторизации, вместо явного конечным пользователем проверки подлинности. В этой модели ваше приложение управляет проверкой подлинности и авторизацией пользователей. При необходимости, ваше приложение создает и отправляет токенов приложения hello, сообщает нашей службы toorender hello запрошенного отчета. Такой подход не требует toouse вашего приложения Azure Active Directory для проверки подлинности пользователя и авторизации, несмотря на то, что вы по-прежнему можете.

## <a name="two-ways-tooauthenticate"></a>Два способа tooauthenticate

**Ключи** можно использовать для всех вызовов REST API в Power BI Embedded. можно найти в hello ключи Hello **портал Azure** , щелкнув **все параметры** и затем **ключи доступа**. С ключом следует обращаться как с паролем. В этих разделах содержится toomake разрешения вызова любого API REST с коллекцией определенную рабочую область.

toouse ключ во время вызова REST добавьте после заголовка авторизации hello:            

    Authorization: AppKey {your key}

**Маркеры приложений** используются для всех запросов внедрения. Они клиентском спроектированный toobe запуска, они будут ограниченные tooa один лучший подход tooset отчета и его срок действия.

Маркеры приложения представляют собой веб-маркеры JWT, подписанные одним из ключей.

Срок действия токена приложение может содержать hello следующих утверждений:

| Утверждение | Описание |
| --- | --- |
| **ver** |версия Hello токен приложения hello. 0.2.0 — hello текущей версии. |
| **aud** |Hello предназначен получателя токена hello. Для Power BI Embedded используйте адрес https://analysis.windows.net/powerbi/api |
| **iss** |Строка, указывающая приложения hello, выдавшего токен hello. |
| **type** |Тип токена приложения, который находится в процессе создания Hello. Текущий тип hello поддерживается только **внедрить**. |
| **wcn** |Токен hello имени коллекции рабочей выдается для. |
| **wid** |Токен hello идентификатор рабочей области выдается для. |
| **rid** |Маркер идентификатора hello выдается для отчетов. |
| **username** (необязательно) |При использовании RLS, это строка, которая позволяет идентифицировать пользователя hello при применении правила RLS. |
| **roles** (необязательно) |Строка, содержащая hello ролей tooselect при применении правил безопасности уровня строк. При выборе нескольких ролей их нужно передавать в виде массива строк. |
| **scp** (необязательно) |Строка, содержащая hello области разрешений. При выборе нескольких ролей их нужно передавать в виде массива строк. |
| **exp** (необязательно) |Указывает, в какой hello токена истечет время hello. Его следует передавать в качестве метки времени Unix |
| **nbf** (необязательно) |Указывает hello запуске в какой hello токен являются допустимыми. Его следует передавать в качестве метки времени Unix |

Пример маркера приложения будет выглядеть следующим образом:

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

После декодирования он станет выглядеть примерно следующим образом:

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

Методы доступны на пакеты SDK, которые упрощают создание apptokens hello. Например, для .NET можно взглянуть на hello [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) класс и hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) методы.

Для hello .NET SDK, можно ссылаться по слишком[областей](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).

## <a name="scopes"></a>Области действия

При использовании маркеров внедрения, вы можете toorestrict использование hello ресурсы, которые обеспечивают доступ к. Для этого можно создать маркер с заданной областью разрешений.

Здесь представлены Hello hello доступные области для Power BI Embedded.

|Область|Описание|
|---|---|
|Dataset.Read|Предоставляет разрешение tooread hello указанного набора данных.|
|Dataset.Write|Предоставляет разрешение toowrite toohello указанного набора данных.|
|Dataset.ReadWrite|Предоставляет разрешение tooread и записи toohello указанного набора данных.|
|Report.Read|Предоставляет разрешение tooview hello указанного отчета.|
|Report.ReadWrite|Предоставляет разрешение tooview и измените hello указанного отчета.|
|Workspace.Report.Create|Предоставляет разрешение toocreate новый отчет в пределах указанного hello рабочей области.|
|Workspace.Report.Copy|Предоставляет разрешение tooclone существующий отчет в пределах указанного hello рабочей области.|

Можно указать несколько областей с помощью пробел между областями hello hello следующим образом.

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

**Обязательные утверждения — области**

точка подключения службы: {scopesClaim} scopesClaim может быть строку или массив строк, отметить hello допускается разрешения tooworkspace ресурсы (отчета, набора данных, и т. д.)

Декодированный маркер, с областями определен, будет выглядеть аналогично toohello следующее.

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "scp": "Report.Read",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

### <a name="operations-and-scopes"></a>Операции и области

|Операция|Целевой ресурс|Разрешения для маркеров|
|---|---|---|
|Создайте (в памяти) новый отчет на основе набора данных.|Выборка|Dataset.Read|
|Создание нового отчета, основанного на наборе данных (в памяти) и сохраните отчет hello.|Выборка|* Dataset.Read<br>* Workspace.Report.Create|
|Просмотр и изменение (в памяти) существующего отчета. Report.Read подразумевает наличие Dataset.Read. Это не позволит toosave изменения разрешений.|Отчет|Report.Read|
|Изменение и сохранение существующего отчета.|Отчет|Report.ReadWrite|
|Сохранение копии отчета ("Сохранить как").|Отчет|* Report.Read<br>* Workspace.Report.Copy|

## <a name="heres-how-hello-flow-works"></a>Вот как работает hello потока
1. Скопируйте ключи tooyour hello API приложения. Можно получить ключи hello в **портала Azure**.
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. Маркер декларирует утверждение и имеет срок действия.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. Маркер подписывается с помощью ключей доступа API.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. Пользователь запрашивает tooview отчет.
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. Маркер проверяется с помощью ключей доступа API.
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. Power BI Embedded отправляет toouser отчета.
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

После **Power BI Embedded** пользователь toohello отчета, отправляет hello пользователь может просматривать отчет hello в пользовательские приложения. Например, если вы импортировали hello [анализ PBIX данных продаж образец](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), hello образец веб-приложение будет выглядеть следующим образом:

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a>См. также

[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[Приступая к работе с примером Microsoft Power BI Embedded](power-bi-embedded-get-started-sample.md)  
[Типичные сценарии использования Microsoft Power BI Embedded](power-bi-embedded-scenarios.md)  
[Начало работы с Microsoft Power BI Embedded (предварительная версия)](power-bi-embedded-get-started.md)  
[Репозиторий PowerBI-CSharp на сайте GitHub](https://github.com/Microsoft/PowerBI-CSharp)  
У вас имеются и другие вопросы? [Повторите hello сообщества Power BI](http://community.powerbi.com/)

