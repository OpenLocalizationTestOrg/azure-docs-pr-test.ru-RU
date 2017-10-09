---
title: "aaaAzure AD v2 ASP.NET Web Server Приступая к работе - введение | Документы Microsoft"
description: "Реализация входа Майкрософт в решении ASP.NET с традиционным браузерным приложением с использованием стандарта OpenID Connect"
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
ms.openlocfilehash: d6449926af2bdad24cbc8e91f74885a08f909103
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-with-microsoft-tooan-aspnet-web-app"></a><span data-ttu-id="94a55-103">Добавить вход с помощью веб-приложение ASP.NET tooan Microsoft</span><span class="sxs-lookup"><span data-stu-id="94a55-103">Add sign-in with Microsoft tooan ASP.NET web app</span></span>

<span data-ttu-id="94a55-104">В этом руководстве показано, как tooimplement вход с корпорацией Майкрософт, с помощью ASP.NET MVC решения с традиционной веб-браузера приложения с использованием OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="94a55-104">This guide demonstrates how tooimplement sign-in with Microsoft using an ASP.NET MVC solution with a traditional web browser-based application using OpenID Connect.</span></span> 

<span data-ttu-id="94a55-105">В конце данного руководства hello приложение будет подписываться может tooaccept модули из личные учетные записи (в том числе outlook.com, live.com и другие), а также работать и школьные учетные записи из любого компании или организации, интегрированное с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="94a55-105">At hello end of this guide, your application will be able tooaccept sign ins of personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory.</span></span> 

> <span data-ttu-id="94a55-106">Для работы с этим руководством требуется Visual Studio 2015 с обновлением 3 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="94a55-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="94a55-107">У вас его нет?</span><span class="sxs-lookup"><span data-stu-id="94a55-107">Don’t have it?</span></span>  [<span data-ttu-id="94a55-108">Скачайте Visual Studio 2017 бесплатно.</span><span class="sxs-lookup"><span data-stu-id="94a55-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a><span data-ttu-id="94a55-109">Принцип работы с руководством</span><span class="sxs-lookup"><span data-stu-id="94a55-109">How this guide works</span></span>

![Принцип работы с руководством](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

<span data-ttu-id="94a55-111">Это руководство составлено на основе сценария hello, где браузера обращается к веб-сайт ASP.NET, запрашивающего пользователя tooauthenticate по нажатию кнопки входа.</span><span class="sxs-lookup"><span data-stu-id="94a55-111">This guide is based on hello scenario where a browser accesses an ASP.NET web site, requesting a user tooauthenticate via a sign-in button.</span></span> <span data-ttu-id="94a55-112">В этом сценарии hello рабочих toorender hello веб-страницы происходит на стороне сервера hello.</span><span class="sxs-lookup"><span data-stu-id="94a55-112">In this scenario, most of hello work toorender hello web page occurs on hello server side.</span></span>

## <a name="libraries"></a><span data-ttu-id="94a55-113">Библиотеки</span><span class="sxs-lookup"><span data-stu-id="94a55-113">Libraries</span></span>

<span data-ttu-id="94a55-114">В этом руководстве используется hello следующие библиотеки:</span><span class="sxs-lookup"><span data-stu-id="94a55-114">This guide uses hello following libraries:</span></span>

|<span data-ttu-id="94a55-115">Библиотека</span><span class="sxs-lookup"><span data-stu-id="94a55-115">Library</span></span>|<span data-ttu-id="94a55-116">Описание</span><span class="sxs-lookup"><span data-stu-id="94a55-116">Description</span></span>|
|---|---|
|[<span data-ttu-id="94a55-117">Microsoft.Owin.Security.OpenIdConnect</span><span class="sxs-lookup"><span data-stu-id="94a55-117">Microsoft.Owin.Security.OpenIdConnect</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|<span data-ttu-id="94a55-118">По промежуточного слоя, позволяющий приложения toouse OpenIdConnect для проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="94a55-118">Middleware that enables an application toouse OpenIdConnect for authentication</span></span>|
|[<span data-ttu-id="94a55-119">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="94a55-119">Microsoft.Owin.Security.Cookies</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|<span data-ttu-id="94a55-120">По промежуточного слоя, позволяющий сеанса пользователя toomaintain приложения с помощью файлов cookie</span><span class="sxs-lookup"><span data-stu-id="94a55-120">Middleware that enables an application toomaintain user session using cookies</span></span>|
|[<span data-ttu-id="94a55-121">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="94a55-121">Microsoft.Owin.Host.SystemWeb</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|<span data-ttu-id="94a55-122">Включает toorun OWIN-приложений в IIS с помощью hello конвейер обработки запросов ASP.NET</span><span class="sxs-lookup"><span data-stu-id="94a55-122">Enables OWIN-based applications toorun on IIS using hello ASP.NET request pipeline</span></span>|

