---
title: "aaaAzure AD v2 JS SPA интерактивной установки — Настройка (ARP) | Документы Microsoft"
description: "В этой статье описано, как приложения JavaScript SPA могут вызывать API, которому необходимы маркеры доступа, с помощью конечной точки Azure Active Directory версии 2 (ARP)."
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
ms.openlocfilehash: 157f4e342cd684294e24da6ee1fad8a7c2fc266a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a><span data-ttu-id="b7884-103">Добавить tooyour сведения о регистрации приложения hello приложения</span><span class="sxs-lookup"><span data-stu-id="b7884-103">Add hello application’s registration information tooyour App</span></span>

<span data-ttu-id="b7884-104">На этом шаге требуется tooconfigure hello перенаправления URL-адрес приложения регистрационную информацию и затем добавить приложения JavaScript SPA tooyour идентификатор приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b7884-104">In this step, you need tooconfigure hello Redirect URL of your application registration information and then add hello Application Id tooyour JavaScript SPA application.</span></span>

### <a name="configure-redirect-url"></a><span data-ttu-id="b7884-105">Настройка URL-адреса перенаправления</span><span class="sxs-lookup"><span data-stu-id="b7884-105">Configure redirect URL</span></span>

<span data-ttu-id="b7884-106">Настройка hello `Redirect URL` поле выше URL-адрес hello index.html страницы на основе веб-сервера, а затем щелкните *обновление*.</span><span class="sxs-lookup"><span data-stu-id="b7884-106">Configure hello `Redirect URL` field above with hello URL for your index.html page based on your web server, then click *Update*.</span></span>


> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="b7884-107">Инструкции Visual Studio для получения URL-адреса перенаправления</span><span class="sxs-lookup"><span data-stu-id="b7884-107">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="b7884-108">tooobtain перенаправления URL-адрес, выполните приведенные ниже инструкции hello:</span><span class="sxs-lookup"><span data-stu-id="b7884-108">tooobtain your redirect URL, follow hello instructions below:</span></span>
> 1.    <span data-ttu-id="b7884-109">В *обозревателе решений*, выберите проект hello и просмотрите hello `Properties` окна (Если вы не видите окно «Свойства», нажмите клавишу `F4`)</span><span class="sxs-lookup"><span data-stu-id="b7884-109">In *Solution Explorer*, select hello project and look at hello `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="b7884-110">Скопируйте значение hello из `URL` toohello буфер обмена:</span><span class="sxs-lookup"><span data-stu-id="b7884-110">Copy hello value from `URL` toohello clipboard:</span></span><br/> <span data-ttu-id="b7884-111">![Свойства проекта](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="b7884-111">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="b7884-112">Вставьте значение hello как `Redirect URL` на hello верхней части этой страницы, нажмите кнопку`Update`</span><span class="sxs-lookup"><span data-stu-id="b7884-112">Paste hello value as a `Redirect URL` on hello top of this page, then click `Update`</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="b7884-113">Настройка URL-адреса перенаправления для Python</span><span class="sxs-lookup"><span data-stu-id="b7884-113">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="b7884-114">Для Python можно задать порт веб-сервера hello через командную строку.</span><span class="sxs-lookup"><span data-stu-id="b7884-114">For Python, you can set hello web server port via command line.</span></span> <span data-ttu-id="b7884-115">Эта интерактивная программа установки использует hello порт 8080 для ссылки, но чувствовать себя свободного toouse все порты доступны.</span><span class="sxs-lookup"><span data-stu-id="b7884-115">This guided setup uses hello port 8080 for reference but feel free toouse any other port available.</span></span> <span data-ttu-id="b7884-116">В любом случае следуйте инструкциям hello ниже tooset копирование URL-адрес перенаправления сведения о регистрации приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b7884-116">In any case, follow hello instructions below tooset up a redirect URL in hello application registration information:</span></span><br/>
> <span data-ttu-id="b7884-117">Задать `http://localhost:8080/` как `Redirect URL` hello верхней части этой страницы, или использовать `http://localhost:[port]/` при использовании другой номер порта TCP (где *[порт]* — hello пользовательский номер порта TCP) и нажмите кнопку «Обновить»</span><span class="sxs-lookup"><span data-stu-id="b7884-117">Set `http://localhost:8080/` as a `Redirect URL` on hello top of this page, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is hello custom TCP port number), and then click 'Update'</span></span>

### <a name="configure-your-javascript-spa-application"></a><span data-ttu-id="b7884-118">Настройка одностраничного приложения JavaScript</span><span class="sxs-lookup"><span data-stu-id="b7884-118">Configure your JavaScript SPA application</span></span>

1.  <span data-ttu-id="b7884-119">Создайте файл с именем `msalconfig.js` со сведениями о регистрации приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b7884-119">Create a file named `msalconfig.js` containing hello application registration information.</span></span> <span data-ttu-id="b7884-120">Если вы используете Visual Studio, выберите hello проектов (корневой папки проекта,), щелкните правой кнопкой мыши и выберите: `Add`  >  `New Item`  >  `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="b7884-120">If you are using Visual Studio, select hello project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="b7884-121">Назовите класс `msalconfig.js`.</span><span class="sxs-lookup"><span data-stu-id="b7884-121">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="b7884-122">Добавьте следующий код tooyour hello `msalconfig.js` файла:</span><span class="sxs-lookup"><span data-stu-id="b7884-122">Add hello following code tooyour `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "[Enter hello application Id here]",
    redirectUri: location.origin
};
``` 
