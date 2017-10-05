---
title: "Приступая к работе с Azure AD версии 2 для Android. Настройка | Документация Майкрософт"
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
ms.openlocfilehash: c09937582118ebcc5b8cbc1f43a0a2019f2f7a89
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
## <a name="add-the-applications-registration-information-to-your-app"></a><span data-ttu-id="a4958-103">Добавление в приложение сведений о его регистрации</span><span class="sxs-lookup"><span data-stu-id="a4958-103">Add the application’s registration information to your app</span></span>

<span data-ttu-id="a4958-104">На этом шаге вам нужно добавить идентификатор клиента в свой проект.</span><span class="sxs-lookup"><span data-stu-id="a4958-104">In this step, you need to add the Client ID to your project.</span></span>

1.  <span data-ttu-id="a4958-105">Откройте `MainActivity` (выберите `app` > `java` > *`{host}.{namespace}`*).</span><span class="sxs-lookup"><span data-stu-id="a4958-105">Open `MainActivity` (under `app` > `java` > *`{host}.{namespace}`*)</span></span>
2.  <span data-ttu-id="a4958-106">Замените строку, начинающуюся с `final static String CLIENT_ID`, следующей:</span><span class="sxs-lookup"><span data-stu-id="a4958-106">Replace the line starting with `final static String CLIENT_ID` with:</span></span>
```java
final static String CLIENT_ID = "[Enter the application Id here]";
```
3. <span data-ttu-id="a4958-107">Откройте: `app` > `manifests` > `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="a4958-107">Open: `app` > `manifests` > `AndroidManifest.xml`</span></span>
4. <span data-ttu-id="a4958-108">Добавьте следующее действие в узел `manifest\application`.</span><span class="sxs-lookup"><span data-stu-id="a4958-108">Add the following activity to `manifest\application` node.</span></span> <span data-ttu-id="a4958-109">Так вы зарегистрируете `BrowserTabActivity`, чтобы позволить операционной системе возобновить ваше приложение после завершения аутентификации.</span><span class="sxs-lookup"><span data-stu-id="a4958-109">This register a `BrowserTabActivity` to allow the OS to resume your application after completing the authentication:</span></span>

```xml
<!--Intent filter to capture System Browser calling back to our app after Sign In-->
<activity
    android:name="com.microsoft.identity.client.BrowserTabActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />

        <!--Add in your scheme/host from registered redirect URI-->
        <!--By default, the scheme should be similar to 'msal[appId]' -->
        <data android:scheme="msal[Enter the application Id here]"
            android:host="auth" />
    </intent-filter>
</activity>
```

### <a name="what-is-next"></a><span data-ttu-id="a4958-110">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a4958-110">What is Next</span></span>

[<span data-ttu-id="a4958-111">Тестирование кода</span><span class="sxs-lookup"><span data-stu-id="a4958-111">Test and Validate</span></span>](active-directory-mobileanddesktopapp-android-test.md)
