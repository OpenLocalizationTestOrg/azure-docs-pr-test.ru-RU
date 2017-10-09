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
## <a name="setting-up-your-web-server-or-project"></a><span data-ttu-id="5c63d-103">Настройка веб-сервера или проекта</span><span class="sxs-lookup"><span data-stu-id="5c63d-103">Setting up your web server or project</span></span>

> <span data-ttu-id="5c63d-104">Предпочтение toodownload проекта в этом примере вместо этого?</span><span class="sxs-lookup"><span data-stu-id="5c63d-104">Prefer toodownload this sample's project instead?</span></span> 
> - [<span data-ttu-id="5c63d-105">Загрузите проект Visual Studio hello</span><span class="sxs-lookup"><span data-stu-id="5c63d-105">Download hello Visual Studio project</span></span>](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/VisualStudio.zip)
>
> <span data-ttu-id="5c63d-106">или</span><span class="sxs-lookup"><span data-stu-id="5c63d-106">or</span></span>
> - <span data-ttu-id="5c63d-107">[Загрузите файлы проекта hello](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) локального веб-сервера, таких как Python</span><span class="sxs-lookup"><span data-stu-id="5c63d-107">[Download hello project files](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) for a local web server, such as Python</span></span>
>
> <span data-ttu-id="5c63d-108">И пропустите toohello [шаг настройки](#create-an-application-express) tooconfigure hello образец кода перед его выполнением.</span><span class="sxs-lookup"><span data-stu-id="5c63d-108">And then  skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing it.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c63d-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5c63d-109">Prerequisites</span></span>
<span data-ttu-id="5c63d-110">Локальный веб-сервер, таких как [Python http.server](https://www.python.org/downloads/), [http сервера](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), или IIS Express интеграция с [2017 г. Visual Studio](https://www.visualstudio.com/downloads/) является обязательным toorun интерактивной программы установки.</span><span class="sxs-lookup"><span data-stu-id="5c63d-110">A local web server such as [Python http.server](https://www.python.org/downloads/), [http-server](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), or IIS Express integration with [Visual Studio 2017](https://www.visualstudio.com/downloads/) is required toorun this guided setup.</span></span> 

<span data-ttu-id="5c63d-111">Инструкции в этом руководстве основаны на Python и Visual Studio 2017 г., но чувствовать себя свободного toouse другой среды разработки или веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="5c63d-111">Instructions in this guide are based on both Python and Visual Studio 2017, but feel free toouse any other development environment or Web Server.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="5c63d-112">Создание проекта</span><span class="sxs-lookup"><span data-stu-id="5c63d-112">Create your project</span></span> 

> ### <a name="option-1-visual-studio"></a><span data-ttu-id="5c63d-113">Вариант 1. Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5c63d-113">Option 1: Visual Studio</span></span> 
> <span data-ttu-id="5c63d-114">Если вы используете Visual Studio и создается новый проект, выполните действия hello ниже toocreate новое решение Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5c63d-114">If you are using Visual Studio and are creating a new project, follow hello steps below toocreate a new Visual Studio solution:</span></span>
> 1.    <span data-ttu-id="5c63d-115">В Visual Studio: `File` > `New` > `Project`.</span><span class="sxs-lookup"><span data-stu-id="5c63d-115">In Visual Studio:  `File` > `New` > `Project`</span></span>
> 2.    <span data-ttu-id="5c63d-116">В разделе `Visual C#\Web` выберите `ASP.NET Web Application (.NET Framework)`.</span><span class="sxs-lookup"><span data-stu-id="5c63d-116">Under `Visual C#\Web`, select `ASP.NET Web Application (.NET Framework)`</span></span>
> 3.    <span data-ttu-id="5c63d-117">Присвойте имя приложению и нажмите кнопку *ОК*.</span><span class="sxs-lookup"><span data-stu-id="5c63d-117">Name your application and click *OK*</span></span>
> 4.    <span data-ttu-id="5c63d-118">В разделе `New ASP.NET Web Application` выберите `Empty`.</span><span class="sxs-lookup"><span data-stu-id="5c63d-118">Under `New ASP.NET Web Application`, select `Empty`</span></span>

<p/><!-- -->

> ### <a name="option-2-python-other-web-servers"></a><span data-ttu-id="5c63d-119">Вариант 2. Python или другие веб-серверы</span><span class="sxs-lookup"><span data-stu-id="5c63d-119">Option 2: Python/ other web servers</span></span>
> <span data-ttu-id="5c63d-120">Убедитесь, что вы установили [Python](https://www.python.org/downloads/), выполните действие hello ниже:</span><span class="sxs-lookup"><span data-stu-id="5c63d-120">Make sure you have installed [Python](https://www.python.org/downloads/), then follow hello step below:</span></span>
> - <span data-ttu-id="5c63d-121">Создайте toohost папку приложения.</span><span class="sxs-lookup"><span data-stu-id="5c63d-121">Create a folder toohost your application.</span></span>


## <a name="create-your-single-page-applications-ui"></a><span data-ttu-id="5c63d-122">Создание пользовательского интерфейса одностраничного приложения</span><span class="sxs-lookup"><span data-stu-id="5c63d-122">Create your single page application’s UI</span></span>
1.  <span data-ttu-id="5c63d-123">Создайте файл *index.html* для своего одностраничного приложения JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5c63d-123">Create an *index.html* file for your JavaScript SPA.</span></span> <span data-ttu-id="5c63d-124">Если вы используете Visual Studio, выберите hello проектов (корневой папки проекта,), щелкните правой кнопкой мыши и выберите: `Add`  >  `New Item`  >  `HTML page` и назовите его index.html</span><span class="sxs-lookup"><span data-stu-id="5c63d-124">If you are using Visual Studio, select hello project (project root folder), right click and select: `Add` > `New Item` > `HTML page` and name it index.html</span></span>
2.  <span data-ttu-id="5c63d-125">Добавьте следующие tooyour кодовую страницу приветствия.</span><span class="sxs-lookup"><span data-stu-id="5c63d-125">Add hello following code tooyour page:</span></span>
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
