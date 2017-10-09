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
ms.openlocfilehash: e14796c37ab0c30d948b6f783dac80059375afa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>Создание приложения (экспресс)
Теперь необходимо приложение hello tooregister *портала регистрации приложения Microsoft*:
1. Зарегистрировать приложение через hello [портала регистрации приложения Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)
2.  Введите имя для приложения и адрес электронной почты.
3.  Убедитесь, что установлен параметр hello для интерактивной установки
4.  Выполните код приложения hello tooobtain инструкции hello и вставьте его в коде

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Добавить решение tooyour сведения о регистрации приложения (Дополнительно)
Теперь необходимо приложение hello tooregister *портала регистрации приложения Microsoft*:
1. Go toohello [портала регистрации приложения Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister приложения
2. Введите имя для приложения и адрес электронной почты. 
3. Убедитесь, что hello для интерактивной программы установки не установлен
4. Щелкните `Add Platform`, а затем — `Native Application` и нажмите кнопку "Сохранить".
5.  Откройте `MainActivity` (выберите `app` > `java` > *`{host}.{namespace}`*).
6.  Замените hello *[Введите здесь приложение hello Id]* в строку hello, начиная с `final static String CLIENT_ID` с Идентификатором приложения hello, только что зарегистрирован:

```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
Откройте `AndroidManifest.xml` (в разделе `app`  >  `manifests`) hello добавить следующие действия слишком`manifest\application` узла. Эта строка регистрирует `BrowserTabActivity` tooallow hello ОС tooresume приложения после завершения проверки подлинности hello:
</li>
</ol>

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
<!-- Workaround for Docs conversion bug -->
<ol start="8">
<li>
В hello `BrowserTabActivity`, замените `[Enter hello application Id here]` с идентификатором hello приложения.
</li>
</ol>
