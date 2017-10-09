---
title: "aaaAzure AD v2 JS SPA Интерактивная установка - введение | Документы Microsoft"
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
ms.openlocfilehash: 7e4250ccca837a17489a99603da167009cc2e3d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a><span data-ttu-id="58de4-103">Вызов hello Microsoft Graph API из JavaScript одной страницы приложений (SPA)</span><span class="sxs-lookup"><span data-stu-id="58de4-103">Call hello Microsoft Graph API from a JavaScript Single Page Application (SPA)</span></span>

<span data-ttu-id="58de4-104">В этом руководстве показано, как JavaScript одной страницы приложений (SPA) могут входить в личных, рабочих и учебных учетных записей, получить маркер доступа и вызвать метод hello Microsoft Graph API или других интерфейсов API, которые требуются токены доступа из hello конечной v2 Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="58de4-104">This guide demonstrates how a JavaScript Single Page Application (SPA) can sign in personal, work and school accounts, get an access token, and call hello Microsoft Graph API or other APIs that require access tokens from hello Azure Active Directory v2 endpoint.</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="58de4-105">Принцип работы с руководством</span><span class="sxs-lookup"><span data-stu-id="58de4-105">How this guide works</span></span>

![Как работает пример приложения hello, созданные в этом руководстве](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="58de4-107">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="58de4-107">More Information</span></span>

<span data-ttu-id="58de4-108">Пример приложения Hello, созданные в этом руководстве позволяет hello tooquery JavaScript SPA Microsoft Graph API или веб-API, принимающий токены из конечной точки v2 Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="58de4-108">hello sample application created by this guide enables a JavaScript SPA tooquery hello Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="58de4-109">В этом сценарии после того, пользователь выполняет вход, маркер доступа — tooHTTP запрошенный и добавлены запросы через заголовок authorization hello.</span><span class="sxs-lookup"><span data-stu-id="58de4-109">For this scenario, after a user signs-in, an access token is requested and added tooHTTP requests via hello authorization header.</span></span> <span data-ttu-id="58de4-110">Получение токена и обновления обрабатываются hello библиотеки проверки подлинности Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="58de4-110">Token acquisition and renewal are handled by hello Microsoft Authentication Library (MSAL).</span></span>

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a><span data-ttu-id="58de4-111">Библиотеки</span><span class="sxs-lookup"><span data-stu-id="58de4-111">Libraries</span></span>

<span data-ttu-id="58de4-112">В этом руководстве используется hello следующие библиотеки:</span><span class="sxs-lookup"><span data-stu-id="58de4-112">This guide uses hello following library:</span></span>

|<span data-ttu-id="58de4-113">Библиотека</span><span class="sxs-lookup"><span data-stu-id="58de4-113">Library</span></span>|<span data-ttu-id="58de4-114">Описание</span><span class="sxs-lookup"><span data-stu-id="58de4-114">Description</span></span>|
|---|---|
|[<span data-ttu-id="58de4-115">msal.js</span><span class="sxs-lookup"><span data-stu-id="58de4-115">msal.js</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-js)|<span data-ttu-id="58de4-116">Библиотека аутентификации Майкрософт для JavaScript (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="58de4-116">Microsoft Authentication Library for JavaScript Preview</span></span>|

> [!NOTE]
> <span data-ttu-id="58de4-117">*msal.js* hello цели *конечной v2 Azure Active Directory* -которого включает toosign, учебную и личные учетные записи в и получать маркеры.</span><span class="sxs-lookup"><span data-stu-id="58de4-117">*msal.js* targets hello *Azure Active Directory v2 endpoint* - which enables personal, school and work accounts toosign in and acquire tokens.</span></span> <span data-ttu-id="58de4-118">Hello *конечной v2 Azure Active Directory* имеет [некоторые ограничения](..\active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="58de4-118">hello *Azure Active Directory v2 endpoint* has [some limitations](..\active-directory-v2-limitations.md).</span></span> <span data-ttu-id="58de4-119">Если вы заинтересованы только в учебном заведении и рабочих учетных записей, используйте *adal.js* и hello *конечной точки версии 1*.</span><span class="sxs-lookup"><span data-stu-id="58de4-119">If you are interested only in school and work accounts, use *adal.js* and hello *V1 endpoint*.</span></span> <span data-ttu-id="58de4-120">toounderstand различия между конечными точками v1 и v2 hello чтения hello [сравнения v1-v2](..\active-directory-v2-compare.md).</span><span class="sxs-lookup"><span data-stu-id="58de4-120">toounderstand differences between hello v1 and v2 endpoints read hello [v1-v2 comparison](..\active-directory-v2-compare.md).</span></span>

<!--end-collapse-->
