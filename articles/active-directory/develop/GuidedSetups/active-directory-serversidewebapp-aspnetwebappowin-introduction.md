---
title: "Приступая к работе с Azure AD версии 2 для веб-сервера ASP.NET. Обзор | Документация Майкрософт"
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
ms.openlocfilehash: 8062923b6270ec6253dc231a3db4333cf4666b42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-with-microsoft-to-an-aspnet-web-app"></a><span data-ttu-id="3a2df-103">Добавление возможности входа в веб-приложение ASP.NET с помощью учетной записи Майкрософт</span><span class="sxs-lookup"><span data-stu-id="3a2df-103">Add sign-in with Microsoft to an ASP.NET web app</span></span>

<span data-ttu-id="3a2df-104">В этом руководстве описывается, как реализовать вход через учетную запись Майкрософт, используя решение ASP.NET MVC с традиционным браузерным приложением с помощью OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="3a2df-104">This guide demonstrates how to implement sign-in with Microsoft using an ASP.NET MVC solution with a traditional web browser-based application using OpenID Connect.</span></span> 

<span data-ttu-id="3a2df-105">В конце этого руководства ваше приложение сможет принимать операции входа с помощью личных учетных записей (включая outlook.com, live.com и другие), а также рабочих и учебных учетных записей из любой компании или организации, которая использует Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3a2df-105">At the end of this guide, your application will be able to accept sign ins of personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory.</span></span> 

> <span data-ttu-id="3a2df-106">Для работы с этим руководством требуется Visual Studio 2015 с обновлением 3 или Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="3a2df-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="3a2df-107">У вас его нет?</span><span class="sxs-lookup"><span data-stu-id="3a2df-107">Don’t have it?</span></span>  [<span data-ttu-id="3a2df-108">Скачайте Visual Studio 2017 бесплатно.</span><span class="sxs-lookup"><span data-stu-id="3a2df-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a><span data-ttu-id="3a2df-109">Принцип работы с руководством</span><span class="sxs-lookup"><span data-stu-id="3a2df-109">How this guide works</span></span>

![Принцип работы с руководством](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

<span data-ttu-id="3a2df-111">Это руководство основано на сценарии, в котором браузер обращается к веб-сайту ASP.NET. При этом пользователь должен выполнить проверку подлинности с помощью кнопки входа.</span><span class="sxs-lookup"><span data-stu-id="3a2df-111">This guide is based on the scenario where a browser accesses an ASP.NET web site, requesting a user to authenticate via a sign-in button.</span></span> <span data-ttu-id="3a2df-112">В этом сценарии большая часть работы по отображению веб-страницы происходит на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="3a2df-112">In this scenario, most of the work to render the web page occurs on the server side.</span></span>

## <a name="libraries"></a><span data-ttu-id="3a2df-113">Библиотеки</span><span class="sxs-lookup"><span data-stu-id="3a2df-113">Libraries</span></span>

<span data-ttu-id="3a2df-114">В этом руководстве используются следующие библиотеки:</span><span class="sxs-lookup"><span data-stu-id="3a2df-114">This guide uses the following libraries:</span></span>

|<span data-ttu-id="3a2df-115">Библиотека</span><span class="sxs-lookup"><span data-stu-id="3a2df-115">Library</span></span>|<span data-ttu-id="3a2df-116">Описание</span><span class="sxs-lookup"><span data-stu-id="3a2df-116">Description</span></span>|
|---|---|
|[<span data-ttu-id="3a2df-117">Microsoft.Owin.Security.OpenIdConnect</span><span class="sxs-lookup"><span data-stu-id="3a2df-117">Microsoft.Owin.Security.OpenIdConnect</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|<span data-ttu-id="3a2df-118">Промежуточный слой, который позволяет приложению использовать OpenIDConnect для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="3a2df-118">Middleware that enables an application to use OpenIdConnect for authentication</span></span>|
|[<span data-ttu-id="3a2df-119">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="3a2df-119">Microsoft.Owin.Security.Cookies</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|<span data-ttu-id="3a2df-120">Промежуточный слой, который позволяет приложению поддерживать пользовательский сеанс с помощью файлов cookie.</span><span class="sxs-lookup"><span data-stu-id="3a2df-120">Middleware that enables an application to maintain user session using cookies</span></span>|
|[<span data-ttu-id="3a2df-121">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="3a2df-121">Microsoft.Owin.Host.SystemWeb</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|<span data-ttu-id="3a2df-122">Позволяет приложениям на основе OWIN работать на платформе IIS с помощью конвейера запросов ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="3a2df-122">Enables OWIN-based applications to run on IIS using the ASP.NET request pipeline</span></span>|

