---
title: "aaaAzure регистрации приложения Active Directory | Документы Microsoft"
description: "В этой статье описывается, как toouse hello Azure портала tooregister приложения с Azure Active Directory"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 7dc7b89f-653f-405a-b5f4-2c1288720c15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: priyamo
ms.reviewer: elisol
ms.openlocfilehash: 0134e299dcc53919a6f789a0878a1cf64a8e244d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="register-your-application-with-your-azure-active-directory-tenant"></a>Регистрация приложения в клиенте Azure Active Directory

Можно использовать приложение hello Azure портала tooregister с вашим клиентом Azure Active Directory (Azure AD). Это создает идентификатора приложения для приложения hello и включает ее tooreceive маркеры.

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Выберите клиент Azure AD, выбрав вашей учетной записи в верхнем правом углу hello страницы приветствия.
3. Hello левой панели навигации, выберите **более служб**, нажмите кнопку **регистрации приложения**и нажмите кнопку **добавить**.
4. Следуйте инструкциям hello и создайте новое приложение. Конкретные примеры для веб-приложений или собственных приложений см. в наших [примерах использования](active-directory-developers-guide.md).
  * Для веб-приложений предоставляют hello **URL-адрес входа**, который является hello базовый URL-адрес приложения, где пользователи могут войти, например `http://localhost:12345`.
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * Для собственных приложений предоставляют **URI перенаправления**, какие Azure AD использует tooreturn маркера ответов. Введите приложении конкретных tooyour значение. Например, с`http://MyFirstAADApp`
5. После завершения регистрации Azure AD присваивает приложения это уникальный идентификатор клиента, hello идентификатор приложения.

## <a name="update-application-settings-from-hello-azure-portal"></a>Обновлять параметры приложения из hello портал Azure

Можно легко изменить параметры существующего приложения с помощью портала Azure hello. Например может потребоваться tooconfigure ответ URL-адрес, где Azure AD выдает токен ответов. Вы также можете tooconfigure разрешения tooother приложений, для экземпляра tooallow tooaccess вашего приложения hello Microsoft Graph API. Можно сделать все этого с помощью страницы параметров приложения hello.

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Выберите клиент Azure AD, выбрав вашей учетной записи в верхнем правом углу hello страницы приветствия.
3. Hello левой панели навигации, выберите **более служб**, нажмите кнопку **регистрации приложения**и выберите приложение из списка hello.
4. Нажмите кнопку **параметры** tooopen hello страницы параметров приложения hello.
  * Hello **свойства** страница позволяет изменять hello Общие сведения для приложения hello. Это включает имя приложения hello, hello URL-адрес входа и URL-адрес выхода hello.
  * Hello **URL-адреса ответа** страница позволяет tooadd ответ URL-адрес, где Azure AD отправляет ответы токена.
  * Hello **владельцев** страница позволяет tooadd владельцы приложений.
  * Hello **разрешений** страница позволяет tooconfigure разрешения для приложения hello. Например, щелкните tooaccess hello Microsoft Graph API, **добавить** и выберите **Microsoft Graph** в селекторе hello API, затем выберите hello необходимые разрешения, например **чтение данных каталога** .
  * Hello **ключей** страница позволяет tooadd секреты приложения. Hello секрет будет отображаться только один раз непосредственно после создания, поэтому следует убедиться, что toocopy его для дальнейшего использования.

## <a name="use-hello-inline-manifest-editor"></a>С помощью редактора манифеста встроенного hello

Можно использовать hello встроенный редактор манифестов toomodify определенные свойства приложения, которые не предоставляются непосредственно в hello портал Azure. Например его можно использовать URI идентификатора приложения hello toomodify приложения или tooenable hello неявного потока OAuth2.0 вместо авторизации по умолчанию hello предоставления поток кода.

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Выберите клиент Azure AD, выбрав вашей учетной записи в верхнем правом углу hello страницы приветствия.
3. Hello левой панели навигации, выберите **более служб**, нажмите кнопку **регистрации приложения**и выберите приложение из списка hello.
4. Нажмите кнопку **манифеста** из hello приложения страницы tooopen hello встроенный редактор манифестов.
5. Можно сделать непосредственно toohello изменения манифеста и сохраните его, когда вы будете готовы. Кроме того, вы можете загрузить манифеста tooopen hello в вашего любимого редактора и загрузки hello обновить манифест.

## <a name="next-steps"></a>Дальнейшие действия

1. Извлечение hello [краткие руководства](active-directory-developers-guide.md) подробные пошаговые руководства приложений при проверке подлинности с помощью Azure AD.
2. Изучите полный список примеров кода в репозитории [GitHub](https://github.com/azure-samples).
