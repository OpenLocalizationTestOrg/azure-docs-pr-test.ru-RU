---
title: "aaaAzure AD v2 Android начало работы — Настройка | Документы Microsoft"
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
ms.openlocfilehash: eaa41805c92212154ee8d51d3eb3aee1202eef1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a>Добавить приложение tooyour сведения о регистрации приложения hello

На этом шаге необходимо tooadd hello идентификатор клиента tooyour проекта.

1.  Откройте `MainActivity` (выберите `app` > `java` > *`{host}.{namespace}`*).
2.  Замените строку hello, начиная с `final static String CLIENT_ID` с:
```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
3. Откройте: `app` > `manifests` > `AndroidManifest.xml`.
4. Добавьте следующие действия слишком hello`manifest\application` узла. Этот регистр `BrowserTabActivity` tooallow hello ОС tooresume приложения после завершения проверки подлинности hello:

```xml
<!--Intent filter toocapture System Browser calling back tooour app after Sign In-->
<activity
    android:name="com.microsoft.identity.client.BrowserTabActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />

        <!--Add in your scheme/host from registered redirect URI-->
        <!--By default, hello scheme should be similar too'msal[appId]' -->
        <data android:scheme="msal[Enter hello application Id here]"
            android:host="auth" />
    </intent-filter>
</activity>
```

### <a name="what-is-next"></a>Дальнейшие действия

[Тестирование кода](active-directory-mobileanddesktopapp-android-test.md)
