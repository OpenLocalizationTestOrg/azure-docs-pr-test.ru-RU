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
# <a name="call-hello-microsoft-graph-api-from-a-windows-desktop-app"></a>Вызывать из приложения рабочего стола Windows hello Microsoft Graph API

В этом руководстве описывается, как классическое приложение для Windows .NET (XAML) может получить маркер доступа и вызвать API Microsoft Graph или другие API, требующие маркеры доступа от конечной точки Azure Active Directory версии 2.

В конце данного руководства hello приложения будет быть может toocall защищенный API, с помощью личные учетные записи (в том числе outlook.com, live.com и другие) а также рабочих и учебных учетных записей из любой компании или организации с Azure Active Directory.  

> Для работы с этим руководством требуется Visual Studio 2015 с обновлением 3 или Visual Studio 2017.  У вас его нет? [Скачайте Visual Studio 2017 бесплатно.](https://www.visualstudio.com/downloads/)

### <a name="how-this-guide-works"></a>Принцип работы с руководством

![Принцип работы с руководством](media/active-directory-mobileanddesktopapp-windowsdesktop-intro/windesktophowitworks.png)

Пример приложения Hello, созданные в этом руководстве позволяет классическое приложение Windows tooquery Microsoft Graph API или веб-API, принимающий токены из конечной точки v2 Azure Active Directory. В этом случае маркер добавляется tooHTTP запросы через заголовок Authorization hello. Получение токена и обновления обрабатываются hello библиотеки проверки подлинности Microsoft (MSAL).


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a>Обработка получения маркера для доступа к защищенным веб-интерфейсам API

После аутентификации пользователя hello пример приложения hello получает маркер, который может быть используется tooquery Microsoft Graph API или веб-API, защищенным v2 Microsoft Azure Active Directory.

API-интерфейсов, таких как Microsoft Graph требуют tooallow маркера доступа, доступ к определенным ресурсам — например, tooread профиля пользователя, доступ к календарю пользователя, или отправить сообщение электронной почты. Приложения можно запросить маркер доступа с помощью MSAL tooaccess эти ресурсы, указав области API. Этот маркер доступа — то добавлены toohello заголовок авторизации HTTP для каждого вызова к hello защищенный ресурс. 

MSAL управляет кэшированием и обновлением маркеров доступа, поэтому вашему приложению не нужно этого делать.


### <a name="nuget-packages"></a>Пакеты NuGet

В этом руководстве использует следующие пакеты NuGet hello:

|Библиотека|Описание|
|---|---|
|[Microsoft.Identity.Client](https://www.nuget.org/packages/Microsoft.Identity.Client)|Библиотека проверки подлинности Майкрософт (MSAL)|

