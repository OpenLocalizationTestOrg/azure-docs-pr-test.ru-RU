---
title: "aaaAzure AD Обзор протокола .NET | Документы Microsoft"
description: "Как toouse HTTP сообщения tooauthorize доступ к tooweb приложений и веб-API в клиенте с помощью Azure AD."
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/21/2016
ms.author: priyamo
ms.openlocfilehash: 5bd54af028c445afd3f35d67d47d7c84b476c757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## Регистрация приложения в клиенте AD
Во-первых необходимо будет tooregister приложение с клиентом Azure Active Directory (Azure AD). Это будет предоставить идентификатора приложения для приложения, а также включить его tooreceive токены.

* Войдите в toohello [портала Azure](https://portal.azure.com).
* Выберите клиент Azure AD, щелкнув в вашей учетной записи в верхнем правом углу hello страницы приветствия.
* В области навигации слева hello, нажмите кнопку **Azure Active Directory**.
* Щелкните **Регистрация приложений** и нажмите кнопку **Добавить**.
* Следуйте инструкциям hello и создайте новое приложение. Для данного руководства не имеет значения, будет это веб-приложение или собственное приложение, но если вам нужны конкретные примеры веб-приложений или собственных приложений, ознакомьтесь с нашими [краткими руководствами](../articles/active-directory/develop/active-directory-developers-guide.md).
  * Для веб-приложений предоставляют hello **URL-адрес входа** это hello базовый URL-адрес приложения, где пользователи могут войти, например `http://localhost:12345`.
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * Для собственных приложений предоставляют **URI перенаправления**, какие Azure AD будет использовать токен ответы tooreturn. Введите приложении конкретных tooyour значение. Например, с`http://MyFirstAADApp`
* После завершения регистрации Azure AD будет назначить уникальный идентификатор клиента приложения, hello идентификатор приложения. Это значение будет требуется в следующих разделах hello, поэтому скопируйте его со страницы приложения hello.
