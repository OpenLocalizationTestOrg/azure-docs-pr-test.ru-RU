---
title: "aaaAzure AD v2 JS SPA Интерактивная установка - введение | Документы Microsoft"
description: "В этой статье описано, как приложения JavaScript SPA могут вызывать API, которому необходимы маркеры доступа, с помощью конечной точки Azure Active Directory версии 2."
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
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 7e4250ccca837a17489a99603da167009cc2e3d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a>Вызов hello Microsoft Graph API из JavaScript одной страницы приложений (SPA)

В этом руководстве показано, как JavaScript одной страницы приложений (SPA) могут входить в личных, рабочих и учебных учетных записей, получить маркер доступа и вызвать метод hello Microsoft Graph API или других интерфейсов API, которые требуются токены доступа из hello конечной v2 Azure Active Directory.

### <a name="how-this-guide-works"></a>Принцип работы с руководством

![Как работает пример приложения hello, созданные в этом руководстве](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a>Дополнительные сведения

Пример приложения Hello, созданные в этом руководстве позволяет hello tooquery JavaScript SPA Microsoft Graph API или веб-API, принимающий токены из конечной точки v2 Azure Active Directory. В этом сценарии после того, пользователь выполняет вход, маркер доступа — tooHTTP запрошенный и добавлены запросы через заголовок authorization hello. Получение токена и обновления обрабатываются hello библиотеки проверки подлинности Microsoft (MSAL).

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a>Библиотеки

В этом руководстве используется hello следующие библиотеки:

|Библиотека|Описание|
|---|---|
|[msal.js](https://github.com/AzureAD/microsoft-authentication-library-for-js)|Библиотека аутентификации Майкрософт для JavaScript (предварительная версия)|

> [!NOTE]
> *msal.js* hello цели *конечной v2 Azure Active Directory* -которого включает toosign, учебную и личные учетные записи в и получать маркеры. Hello *конечной v2 Azure Active Directory* имеет [некоторые ограничения](..\active-directory-v2-limitations.md). Если вы заинтересованы только в учебном заведении и рабочих учетных записей, используйте *adal.js* и hello *конечной точки версии 1*. toounderstand различия между конечными точками v1 и v2 hello чтения hello [сравнения v1-v2](..\active-directory-v2-compare.md).

<!--end-collapse-->
