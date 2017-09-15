---
title: "Приступая к работе с Azure AD версии 2 для классического приложения для Windows. Общие сведения | Документация Майкрософт"
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
ms.openlocfilehash: 4a695c00fce4deb02261ba58ec95469746bb1486
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="call-the-microsoft-graph-api-from-a-windows-desktop-app"></a><span data-ttu-id="db210-103">Вызов API Microsoft Graph из классического приложения для Windows</span><span class="sxs-lookup"><span data-stu-id="db210-103">Call the Microsoft Graph API from a Windows Desktop app</span></span>

<span data-ttu-id="db210-104">В этом руководстве описывается, как классическое приложение для Windows .NET (XAML) может получить маркер доступа и вызвать API Microsoft Graph или другие API, требующие маркеры доступа от конечной точки Azure Active Directory версии 2.</span><span class="sxs-lookup"><span data-stu-id="db210-104">This guide demonstrates how a native Windows Desktop .NET (XAML) application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="db210-105">В конце этого руководства ваше приложение сможет вызывать защищенный API с помощью личных учетных записей (включая outlook.com, live.com и другие), а также рабочих и учебных учетных записей из любой компании или организации, которая использует Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="db210-105">At the end of this guide, your application will be able to call a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

> <span data-ttu-id="db210-106">Для работы с этим руководством требуется Visual Studio 2015 с обновлением 3 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="db210-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="db210-107">У вас его нет?</span><span class="sxs-lookup"><span data-stu-id="db210-107">Don’t have it?</span></span> [<span data-ttu-id="db210-108">Скачайте Visual Studio 2017 бесплатно.</span><span class="sxs-lookup"><span data-stu-id="db210-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

### <a name="how-this-guide-works"></a><span data-ttu-id="db210-109">Принцип работы с руководством</span><span class="sxs-lookup"><span data-stu-id="db210-109">How this guide works</span></span>

![Принцип работы с руководством](media/active-directory-mobileanddesktopapp-windowsdesktop-intro/windesktophowitworks.png)

<span data-ttu-id="db210-111">Пример приложения, созданный в этом руководстве, позволяет классическому приложению для Windows выполнять запрос к API Microsoft Graph или веб-API, принимающему маркеры от конечной точки Azure Active Directory версии 2.</span><span class="sxs-lookup"><span data-stu-id="db210-111">The sample application created by this guide enables a Windows Desktop Application to query Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="db210-112">В этом сценарии маркер добавляется в запросы HTTP с помощью заголовка авторизации.</span><span class="sxs-lookup"><span data-stu-id="db210-112">For this scenario, a token is added to HTTP requests via the Authorization header.</span></span> <span data-ttu-id="db210-113">Получение маркера и его обновление выполняет библиотека проверки подлинности Майкрософт (MSAL).</span><span class="sxs-lookup"><span data-stu-id="db210-113">Token acquisition and renewal is handled by the Microsoft Authentication Library (MSAL).</span></span>


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a><span data-ttu-id="db210-114">Обработка получения маркера для доступа к защищенным веб-интерфейсам API</span><span class="sxs-lookup"><span data-stu-id="db210-114">Handling token acquisition for accessing protected Web APIs</span></span>

<span data-ttu-id="db210-115">После того как пользователь пройдет проверку подлинности, пример приложения получит маркер, который может использоваться для запроса API Microsoft Graph или веб-API, защищенного Microsoft Azure Active Directory версии 2.</span><span class="sxs-lookup"><span data-stu-id="db210-115">After the user authenticates, the sample application receives a token that can be used to query Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="db210-116">API, такие как Microsoft Graph, требуют маркер доступа для доступа к определенным ресурсам. Например, для чтения профиля пользователя, доступа к календарю пользователя или отправки почты.</span><span class="sxs-lookup"><span data-stu-id="db210-116">APIs such as Microsoft Graph require an access token to allow accessing specific resources – for example, to read a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="db210-117">Приложение может запросить маркер доступа с помощью MSAL, чтобы получить доступ к этим ресурсам, указав определенные области API.</span><span class="sxs-lookup"><span data-stu-id="db210-117">Your application can request an access token using MSAL to access these resources by specifying API scopes.</span></span> <span data-ttu-id="db210-118">Затем этот маркер доступа добавляется в заголовок авторизации HTTP для каждого вызова к защищенному ресурсу.</span><span class="sxs-lookup"><span data-stu-id="db210-118">This access token is then added to the HTTP Authorization header for every call made against the protected resource.</span></span> 

<span data-ttu-id="db210-119">MSAL управляет кэшированием и обновлением маркеров доступа, поэтому вашему приложению не нужно этого делать.</span><span class="sxs-lookup"><span data-stu-id="db210-119">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>


### <a name="nuget-packages"></a><span data-ttu-id="db210-120">Пакеты NuGet</span><span class="sxs-lookup"><span data-stu-id="db210-120">NuGet Packages</span></span>

<span data-ttu-id="db210-121">В этом руководстве используются следующие пакеты NuGet:</span><span class="sxs-lookup"><span data-stu-id="db210-121">This guide uses the following NuGet packages:</span></span>

|<span data-ttu-id="db210-122">Библиотека</span><span class="sxs-lookup"><span data-stu-id="db210-122">Library</span></span>|<span data-ttu-id="db210-123">Описание</span><span class="sxs-lookup"><span data-stu-id="db210-123">Description</span></span>|
|---|---|
|[<span data-ttu-id="db210-124">Microsoft.Identity.Client</span><span class="sxs-lookup"><span data-stu-id="db210-124">Microsoft.Identity.Client</span></span>](https://www.nuget.org/packages/Microsoft.Identity.Client)|<span data-ttu-id="db210-125">Библиотека проверки подлинности Майкрософт (MSAL)</span><span class="sxs-lookup"><span data-stu-id="db210-125">Microsoft Authentication Library (MSAL)</span></span>|

