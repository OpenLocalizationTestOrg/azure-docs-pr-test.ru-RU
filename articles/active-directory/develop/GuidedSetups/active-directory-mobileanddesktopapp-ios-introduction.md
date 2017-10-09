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
# <a name="call-hello-microsoft-graph-api-from-an-ios-app"></a>Вызов hello Microsoft Graph API из приложения iOS

В этом руководстве показано, как приложении машинным кодом iOS (Swift) можно получить маркер доступа и вызвать hello Microsoft Graph API или другие API, которые требуются токены доступа из конечной v2 Azure Active Directory.

В конце данного руководства hello приложения будет быть может toocall защищенный API, с помощью личные учетные записи (в том числе outlook.com, live.com и другие) а также рабочих и учебных учетных записей из любой компании или организации с Azure Active Directory.

> ### <a name="pre-requisites"></a>Предварительные требования
> - Для этого руководства требуется XCode 8.x. Скачать XCode можно [здесь](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "URL-адрес для скачивания XCode").
> - [Carthage](https://github.com/Carthage/Carthage) для управления пакетами

### <a name="how-this-guide-works"></a>Принцип работы с руководством

![Принцип работы с руководством](media/active-directory-mobileanddesktopapp-ios-introduction/iosintro.png)

Пример приложения Hello, созданные в этом руководстве позволяет hello tooquery приложений iOS Microsoft Graph API или веб-API, принимающий токены из конечной точки v2 Azure Active Directory. В этом случае маркер добавляется tooHTTP запросы через заголовок Authorization hello. Получение токена и обновления обрабатываются hello библиотеки проверки подлинности Microsoft (MSAL).


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a>Обработка получения маркера для доступа к защищенным веб-интерфейсам API

После аутентификации пользователя hello пример приложения hello получает маркер, который можно использовать tooquery hello Microsoft Graph API или веб-API, защищенным v2 Microsoft Azure Active Directory.

API-интерфейсов, таких как Microsoft Graph требуют tooallow маркера доступа, доступ к определенным ресурсам — например, tooread профиля пользователя, доступ к календарю пользователя, или отправить сообщение электронной почты. Приложение может запросить маркер доступа с помощью MSAL, указав области API. Этот маркер доступа — то добавлены toohello заголовок авторизации HTTP для каждого вызова к hello защищенный ресурс.

MSAL управляет кэшированием и обновлением маркеров доступа, поэтому вашему приложению не нужно этого делать.


### <a name="nuget-packages"></a>Пакеты NuGet

В этом руководстве использует следующие пакеты NuGet hello:

|Библиотека|Описание|
|---|---|
|[MSAL.framework](https://github.com/AzureAD/microsoft-authentication-library-for-objc)|Предварительная версия библиотеки проверки подлинности Microsoft для iOS|

