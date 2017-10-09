---
title: "iOS v2 aaaAzure AD Приступая к работе - введение | Документы Microsoft"
description: "В этой статье описано, как приложения iOS (Swift) могут вызывать API, которому необходимы маркеры доступа, с помощью конечной точки Azure Active Directory версии 2."
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
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: f40aebbb75490912e533aecc7eedfb2b2dcd8c6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-an-ios-app"></a><span data-ttu-id="5c63c-103">Вызов hello Microsoft Graph API из приложения iOS</span><span class="sxs-lookup"><span data-stu-id="5c63c-103">Call hello Microsoft Graph API from an iOS app</span></span>

<span data-ttu-id="5c63c-104">В этом руководстве показано, как приложении машинным кодом iOS (Swift) можно получить маркер доступа и вызвать hello Microsoft Graph API или другие API, которые требуются токены доступа из конечной v2 Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5c63c-104">This guide demonstrates how a native iOS application (Swift) can get an access token and call hello Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="5c63c-105">В конце данного руководства hello приложения будет быть может toocall защищенный API, с помощью личные учетные записи (в том числе outlook.com, live.com и другие) а также рабочих и учебных учетных записей из любой компании или организации с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5c63c-105">At hello end of this guide, your application will be able toocall a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>

> ### <a name="pre-requisites"></a><span data-ttu-id="5c63c-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5c63c-106">Pre-requisites</span></span>
> - <span data-ttu-id="5c63c-107">Для этого руководства требуется XCode 8.x.</span><span class="sxs-lookup"><span data-stu-id="5c63c-107">XCode 8.x is required for this guide.</span></span> <span data-ttu-id="5c63c-108">Скачать XCode можно [здесь](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "URL-адрес для скачивания XCode").</span><span class="sxs-lookup"><span data-stu-id="5c63c-108">You can download XCode [from here](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "XCode Download URL").</span></span>
> - <span data-ttu-id="5c63c-109">[Carthage](https://github.com/Carthage/Carthage) для управления пакетами</span><span class="sxs-lookup"><span data-stu-id="5c63c-109">[Carthage](https://github.com/Carthage/Carthage) for package management</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="5c63c-110">Принцип работы с руководством</span><span class="sxs-lookup"><span data-stu-id="5c63c-110">How this guide works</span></span>

![Принцип работы с руководством](media/active-directory-mobileanddesktopapp-ios-introduction/iosintro.png)

<span data-ttu-id="5c63c-112">Пример приложения Hello, созданные в этом руководстве позволяет hello tooquery приложений iOS Microsoft Graph API или веб-API, принимающий токены из конечной точки v2 Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5c63c-112">hello sample application created by this guide enables an iOS application tooquery hello Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="5c63c-113">В этом случае маркер добавляется tooHTTP запросы через заголовок Authorization hello.</span><span class="sxs-lookup"><span data-stu-id="5c63c-113">For this scenario, a token is added tooHTTP requests via hello Authorization header.</span></span> <span data-ttu-id="5c63c-114">Получение токена и обновления обрабатываются hello библиотеки проверки подлинности Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="5c63c-114">Token acquisition and renewal is handled by hello Microsoft Authentication Library (MSAL).</span></span>


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a><span data-ttu-id="5c63c-115">Обработка получения маркера для доступа к защищенным веб-интерфейсам API</span><span class="sxs-lookup"><span data-stu-id="5c63c-115">Handling token acquisition for accessing protected Web APIs</span></span>

<span data-ttu-id="5c63c-116">После аутентификации пользователя hello пример приложения hello получает маркер, который можно использовать tooquery hello Microsoft Graph API или веб-API, защищенным v2 Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5c63c-116">After hello user authenticates, hello sample application receives a token that can be used tooquery hello Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="5c63c-117">API-интерфейсов, таких как Microsoft Graph требуют tooallow маркера доступа, доступ к определенным ресурсам — например, tooread профиля пользователя, доступ к календарю пользователя, или отправить сообщение электронной почты.</span><span class="sxs-lookup"><span data-stu-id="5c63c-117">APIs such as Microsoft Graph require an access token tooallow accessing specific resources – for example, tooread a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="5c63c-118">Приложение может запросить маркер доступа с помощью MSAL, указав области API.</span><span class="sxs-lookup"><span data-stu-id="5c63c-118">Your application can request an access token using MSAL by specifying API scopes.</span></span> <span data-ttu-id="5c63c-119">Этот маркер доступа — то добавлены toohello заголовок авторизации HTTP для каждого вызова к hello защищенный ресурс.</span><span class="sxs-lookup"><span data-stu-id="5c63c-119">This access token is then added toohello HTTP Authorization header for every call made against hello protected resource.</span></span>

<span data-ttu-id="5c63c-120">MSAL управляет кэшированием и обновлением маркеров доступа, поэтому вашему приложению не нужно этого делать.</span><span class="sxs-lookup"><span data-stu-id="5c63c-120">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>


### <a name="nuget-packages"></a><span data-ttu-id="5c63c-121">Пакеты NuGet</span><span class="sxs-lookup"><span data-stu-id="5c63c-121">NuGet packages</span></span>

<span data-ttu-id="5c63c-122">В этом руководстве использует следующие пакеты NuGet hello:</span><span class="sxs-lookup"><span data-stu-id="5c63c-122">This guide uses hello following NuGet packages:</span></span>

|<span data-ttu-id="5c63c-123">Библиотека</span><span class="sxs-lookup"><span data-stu-id="5c63c-123">Library</span></span>|<span data-ttu-id="5c63c-124">Описание</span><span class="sxs-lookup"><span data-stu-id="5c63c-124">Description</span></span>|
|---|---|
|[<span data-ttu-id="5c63c-125">MSAL.framework</span><span class="sxs-lookup"><span data-stu-id="5c63c-125">MSAL.framework</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-objc)|<span data-ttu-id="5c63c-126">Предварительная версия библиотеки проверки подлинности Microsoft для iOS</span><span class="sxs-lookup"><span data-stu-id="5c63c-126">Microsoft Authentication Library Preview for iOS</span></span>|

