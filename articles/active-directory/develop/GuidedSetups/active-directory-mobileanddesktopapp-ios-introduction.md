---
title: "Приступая к работе с Azure AD версии 2 для iOS. Введение | Документация Майкрософт"
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
ms.openlocfilehash: 948693c8501ecc46a1508e5ea085846d0910783e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="call-the-microsoft-graph-api-from-an-ios-app"></a><span data-ttu-id="85359-103">Вызов API Microsoft Graph из приложения iOS</span><span class="sxs-lookup"><span data-stu-id="85359-103">Call the Microsoft Graph API from an iOS app</span></span>

<span data-ttu-id="85359-104">В этом руководстве показано, как собственное приложение iOS (Swift) может получить маркер доступа и вызвать API Microsoft Graph или другие API, для которых требуются маркеры доступа, из конечной точки Azure Active Directory версии 2.</span><span class="sxs-lookup"><span data-stu-id="85359-104">This guide demonstrates how a native iOS application (Swift) can get an access token and call the Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="85359-105">В конце этого руководства ваше приложение сможет вызывать защищенный API с помощью личных учетных записей (включая outlook.com, live.com и другие), а также рабочих и учебных учетных записей из любой компании или организации, которая использует Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="85359-105">At the end of this guide, your application will be able to call a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>

> ### <a name="pre-requisites"></a><span data-ttu-id="85359-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="85359-106">Pre-requisites</span></span>
> - <span data-ttu-id="85359-107">Для этого руководства требуется XCode 8.x.</span><span class="sxs-lookup"><span data-stu-id="85359-107">XCode 8.x is required for this guide.</span></span> <span data-ttu-id="85359-108">Скачать XCode можно [здесь](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "URL-адрес для скачивания XCode").</span><span class="sxs-lookup"><span data-stu-id="85359-108">You can download XCode [from here](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "XCode Download URL").</span></span>
> - <span data-ttu-id="85359-109">[Carthage](https://github.com/Carthage/Carthage) для управления пакетами</span><span class="sxs-lookup"><span data-stu-id="85359-109">[Carthage](https://github.com/Carthage/Carthage) for package management</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="85359-110">Принцип работы с руководством</span><span class="sxs-lookup"><span data-stu-id="85359-110">How this guide works</span></span>

![Принцип работы с руководством](media/active-directory-mobileanddesktopapp-ios-introduction/iosintro.png)

<span data-ttu-id="85359-112">Пример приложения, созданный в этом руководстве, позволяет приложению iOS выполнять запрос к API Microsoft Graph или веб-API, который принимает маркеры от конечной точки Azure Active Directory версии 2.</span><span class="sxs-lookup"><span data-stu-id="85359-112">The sample application created by this guide enables an iOS application to query the Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="85359-113">В этом сценарии маркер добавляется в запросы HTTP с помощью заголовка авторизации.</span><span class="sxs-lookup"><span data-stu-id="85359-113">For this scenario, a token is added to HTTP requests via the Authorization header.</span></span> <span data-ttu-id="85359-114">Получение маркера и его обновление выполняет библиотека проверки подлинности Майкрософт (MSAL).</span><span class="sxs-lookup"><span data-stu-id="85359-114">Token acquisition and renewal is handled by the Microsoft Authentication Library (MSAL).</span></span>


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a><span data-ttu-id="85359-115">Обработка получения маркера для доступа к защищенным веб-интерфейсам API</span><span class="sxs-lookup"><span data-stu-id="85359-115">Handling token acquisition for accessing protected Web APIs</span></span>

<span data-ttu-id="85359-116">После того как пользователь пройдет проверку подлинности, приложение получит маркер, который может использоваться для запроса к API Microsoft Graph или к веб-API, защищенному Microsoft Azure Active Directory версии 2.</span><span class="sxs-lookup"><span data-stu-id="85359-116">After the user authenticates, the sample application receives a token that can be used to query the Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="85359-117">API, такие как Microsoft Graph, требуют маркер доступа для доступа к определенным ресурсам. Например, для чтения профиля пользователя, доступа к календарю пользователя или отправки почты.</span><span class="sxs-lookup"><span data-stu-id="85359-117">APIs such as Microsoft Graph require an access token to allow accessing specific resources – for example, to read a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="85359-118">Приложение может запросить маркер доступа с помощью MSAL, указав области API.</span><span class="sxs-lookup"><span data-stu-id="85359-118">Your application can request an access token using MSAL by specifying API scopes.</span></span> <span data-ttu-id="85359-119">Затем этот маркер доступа добавляется в заголовок авторизации HTTP для каждого вызова к защищенному ресурсу.</span><span class="sxs-lookup"><span data-stu-id="85359-119">This access token is then added to the HTTP Authorization header for every call made against the protected resource.</span></span>

<span data-ttu-id="85359-120">MSAL управляет кэшированием и обновлением маркеров доступа, поэтому вашему приложению не нужно этого делать.</span><span class="sxs-lookup"><span data-stu-id="85359-120">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>


### <a name="nuget-packages"></a><span data-ttu-id="85359-121">Пакеты NuGet</span><span class="sxs-lookup"><span data-stu-id="85359-121">NuGet packages</span></span>

<span data-ttu-id="85359-122">В этом руководстве используются следующие пакеты NuGet:</span><span class="sxs-lookup"><span data-stu-id="85359-122">This guide uses the following NuGet packages:</span></span>

|<span data-ttu-id="85359-123">Библиотека</span><span class="sxs-lookup"><span data-stu-id="85359-123">Library</span></span>|<span data-ttu-id="85359-124">Описание</span><span class="sxs-lookup"><span data-stu-id="85359-124">Description</span></span>|
|---|---|
|[<span data-ttu-id="85359-125">MSAL.framework</span><span class="sxs-lookup"><span data-stu-id="85359-125">MSAL.framework</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-objc)|<span data-ttu-id="85359-126">Предварительная версия библиотеки проверки подлинности Microsoft для iOS</span><span class="sxs-lookup"><span data-stu-id="85359-126">Microsoft Authentication Library Preview for iOS</span></span>|

