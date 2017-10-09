---
title: "aaaAzure AD v2 Windows Desktop Приступая к работе - введение | Документы Microsoft"
description: "Здесь описывается, как классические приложения для Windows .NET (XAML) могут вызвать API, требующий маркеры доступа от конечной точки Azure Active Directory версии 2."
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
ms.openlocfilehash: 89d98fc46190ba9e47b7c3095f91e32eca455fcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-windows-desktop-app"></a><span data-ttu-id="fde1a-103">Вызывать из приложения рабочего стола Windows hello Microsoft Graph API</span><span class="sxs-lookup"><span data-stu-id="fde1a-103">Call hello Microsoft Graph API from a Windows Desktop app</span></span>

<span data-ttu-id="fde1a-104">В этом руководстве описывается, как классическое приложение для Windows .NET (XAML) может получить маркер доступа и вызвать API Microsoft Graph или другие API, требующие маркеры доступа от конечной точки Azure Active Directory версии 2.</span><span class="sxs-lookup"><span data-stu-id="fde1a-104">This guide demonstrates how a native Windows Desktop .NET (XAML) application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="fde1a-105">В конце данного руководства hello приложения будет быть может toocall защищенный API, с помощью личные учетные записи (в том числе outlook.com, live.com и другие) а также рабочих и учебных учетных записей из любой компании или организации с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fde1a-105">At hello end of this guide, your application will be able toocall a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

> <span data-ttu-id="fde1a-106">Для работы с этим руководством требуется Visual Studio 2015 с обновлением 3 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="fde1a-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="fde1a-107">У вас его нет?</span><span class="sxs-lookup"><span data-stu-id="fde1a-107">Don’t have it?</span></span> [<span data-ttu-id="fde1a-108">Скачайте Visual Studio 2017 бесплатно.</span><span class="sxs-lookup"><span data-stu-id="fde1a-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

### <a name="how-this-guide-works"></a><span data-ttu-id="fde1a-109">Принцип работы с руководством</span><span class="sxs-lookup"><span data-stu-id="fde1a-109">How this guide works</span></span>

![Принцип работы с руководством](media/active-directory-mobileanddesktopapp-windowsdesktop-intro/windesktophowitworks.png)

<span data-ttu-id="fde1a-111">Пример приложения Hello, созданные в этом руководстве позволяет классическое приложение Windows tooquery Microsoft Graph API или веб-API, принимающий токены из конечной точки v2 Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fde1a-111">hello sample application created by this guide enables a Windows Desktop Application tooquery Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="fde1a-112">В этом случае маркер добавляется tooHTTP запросы через заголовок Authorization hello.</span><span class="sxs-lookup"><span data-stu-id="fde1a-112">For this scenario, a token is added tooHTTP requests via hello Authorization header.</span></span> <span data-ttu-id="fde1a-113">Получение токена и обновления обрабатываются hello библиотеки проверки подлинности Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="fde1a-113">Token acquisition and renewal is handled by hello Microsoft Authentication Library (MSAL).</span></span>


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a><span data-ttu-id="fde1a-114">Обработка получения маркера для доступа к защищенным веб-интерфейсам API</span><span class="sxs-lookup"><span data-stu-id="fde1a-114">Handling token acquisition for accessing protected Web APIs</span></span>

<span data-ttu-id="fde1a-115">После аутентификации пользователя hello пример приложения hello получает маркер, который может быть используется tooquery Microsoft Graph API или веб-API, защищенным v2 Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fde1a-115">After hello user authenticates, hello sample application receives a token that can be used tooquery Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="fde1a-116">API-интерфейсов, таких как Microsoft Graph требуют tooallow маркера доступа, доступ к определенным ресурсам — например, tooread профиля пользователя, доступ к календарю пользователя, или отправить сообщение электронной почты.</span><span class="sxs-lookup"><span data-stu-id="fde1a-116">APIs such as Microsoft Graph require an access token tooallow accessing specific resources – for example, tooread a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="fde1a-117">Приложения можно запросить маркер доступа с помощью MSAL tooaccess эти ресурсы, указав области API.</span><span class="sxs-lookup"><span data-stu-id="fde1a-117">Your application can request an access token using MSAL tooaccess these resources by specifying API scopes.</span></span> <span data-ttu-id="fde1a-118">Этот маркер доступа — то добавлены toohello заголовок авторизации HTTP для каждого вызова к hello защищенный ресурс.</span><span class="sxs-lookup"><span data-stu-id="fde1a-118">This access token is then added toohello HTTP Authorization header for every call made against hello protected resource.</span></span> 

<span data-ttu-id="fde1a-119">MSAL управляет кэшированием и обновлением маркеров доступа, поэтому вашему приложению не нужно этого делать.</span><span class="sxs-lookup"><span data-stu-id="fde1a-119">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>


### <a name="nuget-packages"></a><span data-ttu-id="fde1a-120">Пакеты NuGet</span><span class="sxs-lookup"><span data-stu-id="fde1a-120">NuGet Packages</span></span>

<span data-ttu-id="fde1a-121">В этом руководстве использует следующие пакеты NuGet hello:</span><span class="sxs-lookup"><span data-stu-id="fde1a-121">This guide uses hello following NuGet packages:</span></span>

|<span data-ttu-id="fde1a-122">Библиотека</span><span class="sxs-lookup"><span data-stu-id="fde1a-122">Library</span></span>|<span data-ttu-id="fde1a-123">Описание</span><span class="sxs-lookup"><span data-stu-id="fde1a-123">Description</span></span>|
|---|---|
|[<span data-ttu-id="fde1a-124">Microsoft.Identity.Client</span><span class="sxs-lookup"><span data-stu-id="fde1a-124">Microsoft.Identity.Client</span></span>](https://www.nuget.org/packages/Microsoft.Identity.Client)|<span data-ttu-id="fde1a-125">Библиотека проверки подлинности Майкрософт (MSAL)</span><span class="sxs-lookup"><span data-stu-id="fde1a-125">Microsoft Authentication Library (MSAL)</span></span>|

