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
# <a name="call-hello-microsoft-graph-api-from-an-android-app"></a>Вызов hello Microsoft Graph API из приложения Android

В этом руководстве показано, как приложение Android может получить маркер доступа и вызвать API Microsoft Graph или другие API, требующие маркеры доступа, из конечной точки Azure Active Directory версии 2.

В конце данного руководства hello приложения будет быть может toocall защищенный API, с помощью личные учетные записи (в том числе outlook.com, live.com и другие) а также рабочих и учебных учетных записей из любой компании или организации с Azure Active Directory.  

### <a name="how-this-sample-works"></a>Как работает этот пример
![Как работает этот пример](media/active-directory-mobileanddesktopapp-android-intro/android-intro.png)

Образец Hello, созданные в этом руководстве основан на сценарии, где используется tooquery веб-API, который принимает токены из Azure Active Directory v2 конечной точки — в этом случае Microsoft Graph API приложение. В этом случае маркер добавляется tooHTTP запросы через заголовок Authorization hello. Получение токена и обновления обрабатываются hello библиотеки проверки подлинности Microsoft (MSAL).

### <a name="pre-requisites"></a>Предварительные требования
* Это руководство по установке ориентировано на Android Studio, но его также можно использовать для любой другой среды разработки приложений Android. 
* Необходим пакет SDK для Android версии 21 или более поздней (советуем использовать пакет SDK версии 25).
* Для этого выпуска библиотеки проверки подлинности Майкрософт (MSAL) для Android требуется Google Chrome или браузер, поддерживающий настраиваемые вкладки.

> Примечание. Google Chrome не входит в эмулятор Android для Visual Studio. Мы рекомендуем tootest этот код в эмуляторе с API 25 или изображения, с помощью API 21 или более поздней версии, если оно с Google Chrome.


### <a name="how-toohandle-token-acquisition-tooaccess-a-protected-web-api"></a>Как toohandle токен tooaccess приобретения защищенного веб-API

После аутентификации пользователя hello пример приложения hello получает маркер, который может быть используется tooquery Microsoft Graph API или веб-API, защищенным v2 Microsoft Azure Active Directory.

API-интерфейсов, таких как Microsoft Graph требуют tooallow маркера доступа, доступ к определенным ресурсам — например, tooread профиля пользователя, доступ к календарю пользователя, или отправить сообщение электронной почты. Приложения можно запросить маркер доступа с помощью MSAL tooaccess эти ресурсы, указав области API. Этот маркер доступа — то добавлены toohello заголовок авторизации HTTP для каждого вызова к hello защищенный ресурс. 

MSAL управляет кэшированием и обновлением маркеров доступа, поэтому вашему приложению не нужно этого делать.

### <a name="libraries"></a>Библиотеки

В этом руководстве используется hello следующие библиотеки:

|Библиотека|Описание|
|---|---|
|[com.microsoft.identity.client](http://javadoc.io/doc/com.microsoft.identity.client/msal)|Библиотека проверки подлинности Майкрософт (MSAL)|
