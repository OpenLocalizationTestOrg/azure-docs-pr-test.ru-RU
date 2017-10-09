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
## <a name="create-an-application-express"></a><span data-ttu-id="adc95-103">Создание приложения (экспресс)</span><span class="sxs-lookup"><span data-stu-id="adc95-103">Create an application (Express)</span></span>
<span data-ttu-id="adc95-104">Теперь необходимо приложение hello tooregister *портала регистрации приложения Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="adc95-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="adc95-105">Зарегистрировать приложение через hello [портала регистрации приложения Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span><span class="sxs-lookup"><span data-stu-id="adc95-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span></span>
2.  <span data-ttu-id="adc95-106">Введите имя для приложения и адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="adc95-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="adc95-107">Убедитесь, что установлен параметр hello для интерактивной установки</span><span class="sxs-lookup"><span data-stu-id="adc95-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="adc95-108">Выполните код приложения hello tooobtain инструкции hello и вставьте его в коде</span><span class="sxs-lookup"><span data-stu-id="adc95-108">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="adc95-109">Добавить решение tooyour сведения о регистрации приложения (Дополнительно)</span><span class="sxs-lookup"><span data-stu-id="adc95-109">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="adc95-110">Теперь необходимо приложение hello tooregister *портала регистрации приложения Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="adc95-110">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="adc95-111">Go toohello [портала регистрации приложения Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister приложения</span><span class="sxs-lookup"><span data-stu-id="adc95-111">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="adc95-112">Введите имя для приложения и адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="adc95-112">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="adc95-113">Убедитесь, что hello для интерактивной программы установки не установлен</span><span class="sxs-lookup"><span data-stu-id="adc95-113">Make sure hello option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="adc95-114">Щелкните `Add Platform`, а затем — `Native Application` и нажмите кнопку "Сохранить".</span><span class="sxs-lookup"><span data-stu-id="adc95-114">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5.  <span data-ttu-id="adc95-115">Откройте `MainActivity` (выберите `app` > `java` > *`{host}.{namespace}`*).</span><span class="sxs-lookup"><span data-stu-id="adc95-115">Open `MainActivity` (under `app` > `java` > *`{host}.{namespace}`*)</span></span>
6.  <span data-ttu-id="adc95-116">Замените hello *[Введите здесь приложение hello Id]* в строку hello, начиная с `final static String CLIENT_ID` с Идентификатором приложения hello, только что зарегистрирован:</span><span class="sxs-lookup"><span data-stu-id="adc95-116">Replace hello *[Enter hello application Id here]* in hello line starting with `final static String CLIENT_ID` with hello application ID you just registered:</span></span>

```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="adc95-117">Откройте `AndroidManifest.xml` (в разделе `app`  >  `manifests`) hello добавить следующие действия слишком`manifest\application` узла.</span><span class="sxs-lookup"><span data-stu-id="adc95-117">Open `AndroidManifest.xml` (under `app` > `manifests`) Add hello following activity too`manifest\application` node.</span></span> <span data-ttu-id="adc95-118">Эта строка регистрирует `BrowserTabActivity` tooallow hello ОС tooresume приложения после завершения проверки подлинности hello:</span><span class="sxs-lookup"><span data-stu-id="adc95-118">This registers a `BrowserTabActivity` tooallow hello OS tooresume your application after completing hello authentication:</span></span>
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
<span data-ttu-id="adc95-119">В hello `BrowserTabActivity`, замените `[Enter hello application Id here]` с идентификатором hello приложения.</span><span class="sxs-lookup"><span data-stu-id="adc95-119">In hello `BrowserTabActivity`, replace `[Enter hello application Id here]` with hello application ID.</span></span>
</li>
</ol>
