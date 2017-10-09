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
# <a name="add-sign-in-with-microsoft-tooan-aspnet-web-app"></a>Добавить вход с помощью веб-приложение ASP.NET tooan Microsoft

В этом руководстве показано, как tooimplement вход с корпорацией Майкрософт, с помощью ASP.NET MVC решения с традиционной веб-браузера приложения с использованием OpenID Connect. 

В конце данного руководства hello приложение будет подписываться может tooaccept модули из личные учетные записи (в том числе outlook.com, live.com и другие), а также работать и школьные учетные записи из любого компании или организации, интегрированное с Azure Active Directory. 

> Для работы с этим руководством требуется Visual Studio 2015 с обновлением 3 или Visual Studio 2017.  У вас его нет?  [Скачайте Visual Studio 2017 бесплатно.](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a>Принцип работы с руководством

![Принцип работы с руководством](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

Это руководство составлено на основе сценария hello, где браузера обращается к веб-сайт ASP.NET, запрашивающего пользователя tooauthenticate по нажатию кнопки входа. В этом сценарии hello рабочих toorender hello веб-страницы происходит на стороне сервера hello.

## <a name="libraries"></a>Библиотеки

В этом руководстве используется hello следующие библиотеки:

|Библиотека|Описание|
|---|---|
|[Microsoft.Owin.Security.OpenIdConnect](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|По промежуточного слоя, позволяющий приложения toouse OpenIdConnect для проверки подлинности|
|[Microsoft.Owin.Security.Cookies](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|По промежуточного слоя, позволяющий сеанса пользователя toomaintain приложения с помощью файлов cookie|
|[Microsoft.Owin.Host.SystemWeb](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|Включает toorun OWIN-приложений в IIS с помощью hello конвейер обработки запросов ASP.NET|

