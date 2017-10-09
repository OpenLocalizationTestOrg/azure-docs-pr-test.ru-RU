---
title: "aaaAzure AD v2 JS SPA Интерактивная установка - установки | Документы Microsoft"
description: "В этой статье описано, как приложения JavaScript SPA могут вызывать API, которому необходимы маркеры доступа, с помощью конечной точки Azure Active Directory версии 2."
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 19e15c6c8db8bea2975f30e7505af79ccad17e02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="setting-up-your-web-server-or-project"></a>Настройка веб-сервера или проекта

> Предпочтение toodownload проекта в этом примере вместо этого? 
> - [Загрузите проект Visual Studio hello](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/VisualStudio.zip)
>
> или
> - [Загрузите файлы проекта hello](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) локального веб-сервера, таких как Python
>
> И пропустите toohello [шаг настройки](#create-an-application-express) tooconfigure hello образец кода перед его выполнением.

## <a name="prerequisites"></a>Предварительные требования
Локальный веб-сервер, таких как [Python http.server](https://www.python.org/downloads/), [http сервера](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), или IIS Express интеграция с [2017 г. Visual Studio](https://www.visualstudio.com/downloads/) является обязательным toorun интерактивной программы установки. 

Инструкции в этом руководстве основаны на Python и Visual Studio 2017 г., но чувствовать себя свободного toouse другой среды разработки или веб-сервера.

## <a name="create-your-project"></a>Создание проекта 

> ### <a name="option-1-visual-studio"></a>Вариант 1. Visual Studio 
> Если вы используете Visual Studio и создается новый проект, выполните действия hello ниже toocreate новое решение Visual Studio.
> 1.    В Visual Studio: `File` > `New` > `Project`.
> 2.    В разделе `Visual C#\Web` выберите `ASP.NET Web Application (.NET Framework)`.
> 3.    Присвойте имя приложению и нажмите кнопку *ОК*.
> 4.    В разделе `New ASP.NET Web Application` выберите `Empty`.

<p/><!-- -->

> ### <a name="option-2-python-other-web-servers"></a>Вариант 2. Python или другие веб-серверы
> Убедитесь, что вы установили [Python](https://www.python.org/downloads/), выполните действие hello ниже:
> - Создайте toohost папку приложения.


## <a name="create-your-single-page-applications-ui"></a>Создание пользовательского интерфейса одностраничного приложения
1.  Создайте файл *index.html* для своего одностраничного приложения JavaScript. Если вы используете Visual Studio, выберите hello проектов (корневой папки проекта,), щелкните правой кнопкой мыши и выберите: `Add`  >  `New Item`  >  `HTML page` и назовите его index.html
2.  Добавьте следующие tooyour кодовую страницу приветствия.
```html
<!DOCTYPE html>
<html>
<head>
    <!-- bootstrap reference used for styling hello page -->
    <link href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <title>JavaScript SPA Guided Setup</title>
</head>
<body style="margin: 40px">
    <button id="callGraphButton" type="button" class="btn btn-primary" onclick="callGraphApi()">Call Microsoft Graph API</button>
    <div id="errorMessage" class="text-danger"></div>
    <div class="hidden">
        <h3>Graph API Call Response</h3>
        <pre class="well" id="graphResponse"></pre>
    </div>
    <div class="hidden">
        <h3>Access Token</h3>
        <pre class="well" id="accessToken"></pre>
    </div>
    <div class="hidden">
        <h3>ID Token Claims</h3>
        <pre class="well" id="userInfo"></pre>
    </div>
    <button id="signOutButton" type="button" class="btn btn-primary hidden" onclick="signOut()">Sign out</button>

    <!-- This app uses cdn tooreference msal.js (recommended). 
         You can also download it from: https://github.com/AzureAD/microsoft-authentication-library-for-js -->
    <script src="https://secure.aadcdn.microsoftonline-p.com/lib/0.1.1/js/msal.min.js"></script>

    <!-- hello 'bluebird' and 'fetch' references below are required if you need toorun this application on Internet Explorer -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/bluebird/3.3.4/bluebird.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/fetch/2.0.3/fetch.min.js"></script>

    <script type="text/javascript" src="msalconfig.js"></script>
    <script type="text/javascript" src="app.js"></script>
</body>
</html>
````
