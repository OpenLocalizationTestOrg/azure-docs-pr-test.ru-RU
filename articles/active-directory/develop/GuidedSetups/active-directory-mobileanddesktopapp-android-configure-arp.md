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
## <a name="add-hello-applications-registration-information-tooyour-app"></a><span data-ttu-id="3b5de-103">Добавить приложение tooyour сведения о регистрации приложения hello</span><span class="sxs-lookup"><span data-stu-id="3b5de-103">Add hello application’s registration information tooyour app</span></span>

<span data-ttu-id="3b5de-104">На этом шаге необходимо tooadd hello идентификатор клиента tooyour проекта.</span><span class="sxs-lookup"><span data-stu-id="3b5de-104">In this step, you need tooadd hello Client ID tooyour project.</span></span>

1.  <span data-ttu-id="3b5de-105">Откройте `MainActivity` (выберите `app` > `java` > *`{host}.{namespace}`*).</span><span class="sxs-lookup"><span data-stu-id="3b5de-105">Open `MainActivity` (under `app` > `java` > *`{host}.{namespace}`*)</span></span>
2.  <span data-ttu-id="3b5de-106">Замените строку hello, начиная с `final static String CLIENT_ID` с:</span><span class="sxs-lookup"><span data-stu-id="3b5de-106">Replace hello line starting with `final static String CLIENT_ID` with:</span></span>
```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
3. <span data-ttu-id="3b5de-107">Откройте: `app` > `manifests` > `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="3b5de-107">Open: `app` > `manifests` > `AndroidManifest.xml`</span></span>
4. <span data-ttu-id="3b5de-108">Добавьте следующие действия слишком hello`manifest\application` узла.</span><span class="sxs-lookup"><span data-stu-id="3b5de-108">Add hello following activity too`manifest\application` node.</span></span> <span data-ttu-id="3b5de-109">Этот регистр `BrowserTabActivity` tooallow hello ОС tooresume приложения после завершения проверки подлинности hello:</span><span class="sxs-lookup"><span data-stu-id="3b5de-109">This register a `BrowserTabActivity` tooallow hello OS tooresume your application after completing hello authentication:</span></span>

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

### <a name="what-is-next"></a><span data-ttu-id="3b5de-110">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3b5de-110">What is Next</span></span>

[<span data-ttu-id="3b5de-111">Тестирование кода</span><span class="sxs-lookup"><span data-stu-id="3b5de-111">Test and Validate</span></span>](active-directory-mobileanddesktopapp-android-test.md)
