---
title: "aaaAzure AD v2 Android Приступая к работе - введение | Документы Microsoft"
description: "Получение маркера доступа для приложения Android и вызов API Microsoft Graph или API, которые требуют маркер доступа, из конечной точки Azure Active Directory версии 2."
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 7c76ab8bbf1a6c934ab672cccf85ae82f03f601a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-an-android-app"></a><span data-ttu-id="c7f24-103">Вызов hello Microsoft Graph API из приложения Android</span><span class="sxs-lookup"><span data-stu-id="c7f24-103">Call hello Microsoft Graph API from an Android app</span></span>

<span data-ttu-id="c7f24-104">В этом руководстве показано, как приложение Android может получить маркер доступа и вызвать API Microsoft Graph или другие API, требующие маркеры доступа, из конечной точки Azure Active Directory версии 2.</span><span class="sxs-lookup"><span data-stu-id="c7f24-104">This guide demonstrates how a native Android application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="c7f24-105">В конце данного руководства hello приложения будет быть может toocall защищенный API, с помощью личные учетные записи (в том числе outlook.com, live.com и другие) а также рабочих и учебных учетных записей из любой компании или организации с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c7f24-105">At hello end of this guide, your application will be able toocall a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

### <a name="how-this-sample-works"></a><span data-ttu-id="c7f24-106">Как работает этот пример</span><span class="sxs-lookup"><span data-stu-id="c7f24-106">How this sample works</span></span>
![Как работает этот пример](media/active-directory-mobileanddesktopapp-android-intro/android-intro.png)

<span data-ttu-id="c7f24-108">Образец Hello, созданные в этом руководстве основан на сценарии, где используется tooquery веб-API, который принимает токены из Azure Active Directory v2 конечной точки — в этом случае Microsoft Graph API приложение.</span><span class="sxs-lookup"><span data-stu-id="c7f24-108">hello sample created by this guide is based on a scenario where an Android application is used tooquery a Web API that accepts tokens from Azure Active Directory v2 endpoint – in this case, Microsoft Graph API.</span></span> <span data-ttu-id="c7f24-109">В этом случае маркер добавляется tooHTTP запросы через заголовок Authorization hello.</span><span class="sxs-lookup"><span data-stu-id="c7f24-109">For this scenario, a token is added tooHTTP requests via hello Authorization header.</span></span> <span data-ttu-id="c7f24-110">Получение токена и обновления обрабатываются hello библиотеки проверки подлинности Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="c7f24-110">Token acquisition and renewal is handled by hello Microsoft Authentication Library (MSAL).</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="c7f24-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c7f24-111">Pre-requisites</span></span>
* <span data-ttu-id="c7f24-112">Это руководство по установке ориентировано на Android Studio, но его также можно использовать для любой другой среды разработки приложений Android.</span><span class="sxs-lookup"><span data-stu-id="c7f24-112">This guided setup is focused on Android Studio, but any other Android application development environment is also acceptable.</span></span> 
* <span data-ttu-id="c7f24-113">Необходим пакет SDK для Android версии 21 или более поздней (советуем использовать пакет SDK версии 25).</span><span class="sxs-lookup"><span data-stu-id="c7f24-113">Android SDK 21 or newer is required (SDK 25 is recommended).</span></span>
* <span data-ttu-id="c7f24-114">Для этого выпуска библиотеки проверки подлинности Майкрософт (MSAL) для Android требуется Google Chrome или браузер, поддерживающий настраиваемые вкладки.</span><span class="sxs-lookup"><span data-stu-id="c7f24-114">Google Chrome or a web browser using Custom Tabs is required for this release of Microsoft Authentication Library (MSAL) for Android.</span></span>

> <span data-ttu-id="c7f24-115">Примечание. Google Chrome не входит в эмулятор Android для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c7f24-115">Note: Google Chrome is not included on Visual Studio Emulator for Android.</span></span> <span data-ttu-id="c7f24-116">Мы рекомендуем tootest этот код в эмуляторе с API 25 или изображения, с помощью API 21 или более поздней версии, если оно с Google Chrome.</span><span class="sxs-lookup"><span data-stu-id="c7f24-116">We recommend you tootest this code on an Emulator with API 25 or an image with API 21 or newer that has with Google Chrome installed.</span></span>


### <a name="how-toohandle-token-acquisition-tooaccess-a-protected-web-api"></a><span data-ttu-id="c7f24-117">Как toohandle токен tooaccess приобретения защищенного веб-API</span><span class="sxs-lookup"><span data-stu-id="c7f24-117">How toohandle token acquisition tooaccess a protected Web API</span></span>

<span data-ttu-id="c7f24-118">После аутентификации пользователя hello пример приложения hello получает маркер, который может быть используется tooquery Microsoft Graph API или веб-API, защищенным v2 Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c7f24-118">After hello user authenticates, hello sample application receives a token that can be used tooquery Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="c7f24-119">API-интерфейсов, таких как Microsoft Graph требуют tooallow маркера доступа, доступ к определенным ресурсам — например, tooread профиля пользователя, доступ к календарю пользователя, или отправить сообщение электронной почты.</span><span class="sxs-lookup"><span data-stu-id="c7f24-119">APIs such as Microsoft Graph require an access token tooallow accessing specific resources – for example, tooread a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="c7f24-120">Приложения можно запросить маркер доступа с помощью MSAL tooaccess эти ресурсы, указав области API.</span><span class="sxs-lookup"><span data-stu-id="c7f24-120">Your application can request an access token using MSAL tooaccess these resources by specifying API scopes.</span></span> <span data-ttu-id="c7f24-121">Этот маркер доступа — то добавлены toohello заголовок авторизации HTTP для каждого вызова к hello защищенный ресурс.</span><span class="sxs-lookup"><span data-stu-id="c7f24-121">This access token is then added toohello HTTP Authorization header for every call made against hello protected resource.</span></span> 

<span data-ttu-id="c7f24-122">MSAL управляет кэшированием и обновлением маркеров доступа, поэтому вашему приложению не нужно этого делать.</span><span class="sxs-lookup"><span data-stu-id="c7f24-122">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>

### <a name="libraries"></a><span data-ttu-id="c7f24-123">Библиотеки</span><span class="sxs-lookup"><span data-stu-id="c7f24-123">Libraries</span></span>

<span data-ttu-id="c7f24-124">В этом руководстве используется hello следующие библиотеки:</span><span class="sxs-lookup"><span data-stu-id="c7f24-124">This guide uses hello following libraries:</span></span>

|<span data-ttu-id="c7f24-125">Библиотека</span><span class="sxs-lookup"><span data-stu-id="c7f24-125">Library</span></span>|<span data-ttu-id="c7f24-126">Описание</span><span class="sxs-lookup"><span data-stu-id="c7f24-126">Description</span></span>|
|---|---|
|[<span data-ttu-id="c7f24-127">com.microsoft.identity.client</span><span class="sxs-lookup"><span data-stu-id="c7f24-127">com.microsoft.identity.client</span></span>](http://javadoc.io/doc/com.microsoft.identity.client/msal)|<span data-ttu-id="c7f24-128">Библиотека проверки подлинности Майкрософт (MSAL)</span><span class="sxs-lookup"><span data-stu-id="c7f24-128">Microsoft Authentication Library (MSAL)</span></span>|
