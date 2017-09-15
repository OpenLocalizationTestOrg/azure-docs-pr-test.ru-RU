---
title: "Интерактивная настройка Azure AD версии 2 для приложений JS SPA. Введение | Документация Майкрософт"
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
ms.openlocfilehash: 3d195d0d67f8f82c9450ffd93767917698addee3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="call-the-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a><span data-ttu-id="75eea-103">Вызов API Microsoft Graph из одностраничного приложения JavaScript</span><span class="sxs-lookup"><span data-stu-id="75eea-103">Call the Microsoft Graph API from a JavaScript Single Page Application (SPA)</span></span>

<span data-ttu-id="75eea-104">В этом руководстве показано, как одностраничное приложение JavaScript может выполнять вход с помощью личных, рабочих или учебных учетных записей, получать маркер доступа и вызывать API Microsoft Graph или другие API, требующие маркеры доступа, из конечной точки Azure Active Directory версии 2.</span><span class="sxs-lookup"><span data-stu-id="75eea-104">This guide demonstrates how a JavaScript Single Page Application (SPA) can sign in personal, work and school accounts, get an access token, and call the Microsoft Graph API or other APIs that require access tokens from the Azure Active Directory v2 endpoint.</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="75eea-105">Принцип работы с руководством</span><span class="sxs-lookup"><span data-stu-id="75eea-105">How this guide works</span></span>

![Как работает пример приложения, созданный в этом руководстве](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="75eea-107">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="75eea-107">More Information</span></span>

<span data-ttu-id="75eea-108">Пример приложения, созданный в этом руководстве, позволяет одностраничному приложению JavaScript выполнять запрос к API Microsoft Graph или веб-API, принимающему маркеры от конечной точки Azure Active Directory версии 2.</span><span class="sxs-lookup"><span data-stu-id="75eea-108">The sample application created by this guide enables a JavaScript SPA to query the Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="75eea-109">В этом сценарии после выполнения входа в систему маркер доступа запрашивается и добавляется в запросы HTTP с помощью заголовка авторизации.</span><span class="sxs-lookup"><span data-stu-id="75eea-109">For this scenario, after a user signs-in, an access token is requested and added to HTTP requests via the authorization header.</span></span> <span data-ttu-id="75eea-110">Получение маркера и его обновление выполняет библиотека проверки подлинности Майкрософт (MSAL).</span><span class="sxs-lookup"><span data-stu-id="75eea-110">Token acquisition and renewal are handled by the Microsoft Authentication Library (MSAL).</span></span>

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a><span data-ttu-id="75eea-111">Библиотеки</span><span class="sxs-lookup"><span data-stu-id="75eea-111">Libraries</span></span>

<span data-ttu-id="75eea-112">В этом руководстве используется следующая библиотека:</span><span class="sxs-lookup"><span data-stu-id="75eea-112">This guide uses the following library:</span></span>

|<span data-ttu-id="75eea-113">Библиотека</span><span class="sxs-lookup"><span data-stu-id="75eea-113">Library</span></span>|<span data-ttu-id="75eea-114">Описание</span><span class="sxs-lookup"><span data-stu-id="75eea-114">Description</span></span>|
|---|---|
|[<span data-ttu-id="75eea-115">msal.js</span><span class="sxs-lookup"><span data-stu-id="75eea-115">msal.js</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-js)|<span data-ttu-id="75eea-116">Библиотека аутентификации Майкрософт для JavaScript (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="75eea-116">Microsoft Authentication Library for JavaScript Preview</span></span>|

> [!NOTE]
> <span data-ttu-id="75eea-117">В качестве целевого объекта в библиотеке *msal.js* задана *конечная точка Azure Active Directory версии 2*, что позволяет выполнять вход и запрашивать маркеры, используя личные, рабочие и учебные учетные записи.</span><span class="sxs-lookup"><span data-stu-id="75eea-117">*msal.js* targets the *Azure Active Directory v2 endpoint* - which enables personal, school and work accounts to sign in and acquire tokens.</span></span> <span data-ttu-id="75eea-118">В отношении *конечной точки Azure Active Directory версии 2* применяется [ряд ограничений](..\active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="75eea-118">The *Azure Active Directory v2 endpoint* has [some limitations](..\active-directory-v2-limitations.md).</span></span> <span data-ttu-id="75eea-119">Если вы заинтересованы только в учебной и рабочей учетных записях, используйте библиотеку *adal.js* и *конечную точку версии 1*.</span><span class="sxs-lookup"><span data-stu-id="75eea-119">If you are interested only in school and work accounts, use *adal.js* and the *V1 endpoint*.</span></span> <span data-ttu-id="75eea-120">Чтобы понять различия между конечными точками версий 1 и 2, ознакомьтесь со [сравнением версий 1 и 2](..\active-directory-v2-compare.md).</span><span class="sxs-lookup"><span data-stu-id="75eea-120">To understand differences between the v1 and v2 endpoints read the [v1-v2 comparison](..\active-directory-v2-compare.md).</span></span>

<!--end-collapse-->
