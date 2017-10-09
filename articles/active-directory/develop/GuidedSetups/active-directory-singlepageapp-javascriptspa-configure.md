---
title: "aaaAzure AD v2 JS SPA интерактивной установки — Настройка | Документы Microsoft"
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
ms.openlocfilehash: 1b93298d4bd4e17dd261dbb75502a122c30aac97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="register-your-application"></a><span data-ttu-id="c8d47-103">Регистрация приложения</span><span class="sxs-lookup"><span data-stu-id="c8d47-103">Register your application</span></span>

<span data-ttu-id="c8d47-104">Существует несколько способов toocreate приложения, выберите один из них:</span><span class="sxs-lookup"><span data-stu-id="c8d47-104">There are multiple ways toocreate an application, please select one of them:</span></span>

### <a name="option-1-register-your-application-express-mode"></a><span data-ttu-id="c8d47-105">Вариант 1. Регистрация приложения (экспресс-режим).</span><span class="sxs-lookup"><span data-stu-id="c8d47-105">Option 1: Register your application (Express mode)</span></span>
<span data-ttu-id="c8d47-106">Теперь необходимо приложение hello tooregister *портала регистрации приложения Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="c8d47-106">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>

1.  <span data-ttu-id="c8d47-107">Зарегистрировать приложение через hello [портала регистрации приложения Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)</span><span class="sxs-lookup"><span data-stu-id="c8d47-107">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)</span></span>
2.  <span data-ttu-id="c8d47-108">Введите имя для приложения и адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="c8d47-108">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="c8d47-109">Убедитесь, что параметр hello *интерактивной установки* проверяется</span><span class="sxs-lookup"><span data-stu-id="c8d47-109">Make sure hello option for *Guided Setup* is checked</span></span>
4.  <span data-ttu-id="c8d47-110">Выполните код приложения hello tooobtain инструкции hello и вставьте его в коде</span><span class="sxs-lookup"><span data-stu-id="c8d47-110">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="option-2-register-your-application-advanced-mode"></a><span data-ttu-id="c8d47-111">Вариант 2. Регистрация приложения (расширенный режим).</span><span class="sxs-lookup"><span data-stu-id="c8d47-111">Option 2: Register your application (Advanced mode)</span></span>

1. <span data-ttu-id="c8d47-112">Go toohello [портала регистрации приложения Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister приложения</span><span class="sxs-lookup"><span data-stu-id="c8d47-112">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="c8d47-113">Введите имя для приложения и адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="c8d47-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="c8d47-114">Убедитесь, что параметр hello *интерактивной установки* не установлен</span><span class="sxs-lookup"><span data-stu-id="c8d47-114">Make sure hello option for *Guided Setup* is unchecked</span></span>
4.  <span data-ttu-id="c8d47-115">Щелкните `Add Platform`, а затем выберите `Web`.</span><span class="sxs-lookup"><span data-stu-id="c8d47-115">Click `Add Platform`, then select `Web`</span></span>
5. <span data-ttu-id="c8d47-116">Добавить hello `Redirect URL` , соответствующие URL-адрес toohello приложения на основе веб-сервера.</span><span class="sxs-lookup"><span data-stu-id="c8d47-116">Add hello `Redirect URL` that correspond toohello application's URL based on your web server.</span></span> <span data-ttu-id="c8d47-117">В разделах hello ниже инструкции о том, как tooset / получить URL-адрес перенаправления hello в Visual Studio и Python.</span><span class="sxs-lookup"><span data-stu-id="c8d47-117">See hello sections below for instructions on how tooset/ obtain hello redirect URL in Visual Studio and Python.</span></span>
6. <span data-ttu-id="c8d47-118">Нажмите кнопку *Сохранить*</span><span class="sxs-lookup"><span data-stu-id="c8d47-118">Click *Save*</span></span>

> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="c8d47-119">Инструкции Visual Studio для получения URL-адреса перенаправления</span><span class="sxs-lookup"><span data-stu-id="c8d47-119">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="c8d47-120">Выполните инструкции tooobtain hello перенаправление URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="c8d47-120">Follow hello instructions tooobtain your redirect URL:</span></span>
> 1.    <span data-ttu-id="c8d47-121">В *обозревателе решений*, выберите проект hello и просмотрите hello `Properties` окна (Если вы не видите окно «Свойства», нажмите клавишу `F4`)</span><span class="sxs-lookup"><span data-stu-id="c8d47-121">In *Solution Explorer*, select hello project and look at hello `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="c8d47-122">Скопируйте значение hello из `URL` toohello буфер обмена:</span><span class="sxs-lookup"><span data-stu-id="c8d47-122">Copy hello value from `URL` toohello clipboard:</span></span><br/> <span data-ttu-id="c8d47-123">![Свойства проекта](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="c8d47-123">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="c8d47-124">Перейдите назад toohello *портала регистрации приложения* и вставьте значение hello как `Redirect URL` и нажмите кнопку «Сохранить»</span><span class="sxs-lookup"><span data-stu-id="c8d47-124">Switch back toohello *Application Registration Portal* and paste hello value as a `Redirect URL` and click 'Save'</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="c8d47-125">Настройка URL-адреса перенаправления для Python</span><span class="sxs-lookup"><span data-stu-id="c8d47-125">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="c8d47-126">Для Python можно задать порт веб-сервера hello через командную строку.</span><span class="sxs-lookup"><span data-stu-id="c8d47-126">For Python, you can set hello web server port via command line.</span></span> <span data-ttu-id="c8d47-127">Эта интерактивная программа установки использует hello порт 8080 для ссылки, но чувствовать себя свободного toouse все порты доступны.</span><span class="sxs-lookup"><span data-stu-id="c8d47-127">This guided setup uses hello port 8080 for reference but feel free toouse any other port available.</span></span> <span data-ttu-id="c8d47-128">В любом случае следуйте инструкциям hello ниже tooset копирование URL-адрес перенаправления сведения о регистрации приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c8d47-128">In any case, follow hello instructions below tooset up a redirect URL in hello application registration information:</span></span><br/>
> - <span data-ttu-id="c8d47-129">Переключиться назад toohello *портала регистрации приложения* и задайте `http://localhost:8080/` как `Redirect URL`, или используйте `http://localhost:[port]/` при использовании другой номер порта TCP (где *[порт]* — hello пользовательские TCP-порт номер) и нажмите кнопку «Сохранить»</span><span class="sxs-lookup"><span data-stu-id="c8d47-129">Switch back toohello *Application Registration Portal* and set `http://localhost:8080/` as a `Redirect URL`, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is hello custom TCP port number) and click 'Save'</span></span>


#### <a name="configure-your-javascript-spa"></a><span data-ttu-id="c8d47-130">Настройка одностраничного приложения JavaScript</span><span class="sxs-lookup"><span data-stu-id="c8d47-130">Configure your JavaScript SPA</span></span>

1.  <span data-ttu-id="c8d47-131">Создайте файл с именем `msalconfig.js` со сведениями о регистрации приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c8d47-131">Create a file named `msalconfig.js` containing hello application registration information.</span></span> <span data-ttu-id="c8d47-132">Если вы используете Visual Studio, выберите hello проектов (корневой папки проекта,), щелкните правой кнопкой мыши и выберите: `Add`  >  `New Item`  >  `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="c8d47-132">If you are using Visual Studio, select hello project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="c8d47-133">Назовите класс `msalconfig.js`.</span><span class="sxs-lookup"><span data-stu-id="c8d47-133">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="c8d47-134">Добавьте следующий код tooyour hello `msalconfig.js` файла:</span><span class="sxs-lookup"><span data-stu-id="c8d47-134">Add hello following code tooyour `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "Enter_the_Application_Id_here",
    redirectUri: location.origin
};
```
<ol start="3">
<li>
<span data-ttu-id="c8d47-135">Замените <code>Enter_the_Application_Id_here</code> с только что зарегистрирован идентификатор приложения hello</span><span class="sxs-lookup"><span data-stu-id="c8d47-135">Replace <code>Enter_the_Application_Id_here</code> with hello Application Id you just registered</span></span>
</li>
</ol>
