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
ms.openlocfilehash: 945b09ccdb7537987da33d32d94a3ccacd829ffd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="748e5-103">Создание приложения (экспресс)</span><span class="sxs-lookup"><span data-stu-id="748e5-103">Create an application (Express)</span></span>
<span data-ttu-id="748e5-104">Теперь вам необходимо зарегистрировать приложение на *портале регистрации приложений Майкрософт*:</span><span class="sxs-lookup"><span data-stu-id="748e5-104">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="748e5-105">Зарегистрируйте свое приложение на [портале регистрации приложений Майкрософт](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure).</span><span class="sxs-lookup"><span data-stu-id="748e5-105">Register your application via the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span></span>
2.  <span data-ttu-id="748e5-106">Введите имя для приложения и адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="748e5-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="748e5-107">Выберите параметр Guided Setup (Пошаговая настройка).</span><span class="sxs-lookup"><span data-stu-id="748e5-107">Make sure the option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="748e5-108">Следуйте инструкциям, чтобы получить идентификатор приложения. Затем вставьте его в свой код.</span><span class="sxs-lookup"><span data-stu-id="748e5-108">Follow the instructions to obtain the application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-to-your-solution-advanced"></a><span data-ttu-id="748e5-109">Добавление сведений о регистрации приложения в решение (дополнительно)</span><span class="sxs-lookup"><span data-stu-id="748e5-109">Add your application registration information to your solution (Advanced)</span></span>
<span data-ttu-id="748e5-110">Теперь вам необходимо зарегистрировать приложение на *портале регистрации приложений Майкрософт*:</span><span class="sxs-lookup"><span data-stu-id="748e5-110">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="748e5-111">Перейдите на [портал регистрации приложений Майкрософт](https://apps.dev.microsoft.com/portal/register-app) для регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="748e5-111">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) to register an application</span></span>
2. <span data-ttu-id="748e5-112">Введите имя для приложения и адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="748e5-112">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="748e5-113">Убедитесь, что параметр Guided Setup (Пошаговая настройка) не выбран.</span><span class="sxs-lookup"><span data-stu-id="748e5-113">Make sure the option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="748e5-114">Щелкните `Add Platform`, а затем — `Native Application` и нажмите кнопку "Сохранить".</span><span class="sxs-lookup"><span data-stu-id="748e5-114">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5.  <span data-ttu-id="748e5-115">Откройте `MainActivity` (выберите `app` > `java` > *`{host}.{namespace}`*).</span><span class="sxs-lookup"><span data-stu-id="748e5-115">Open `MainActivity` (under `app` > `java` > *`{host}.{namespace}`*)</span></span>
6.  <span data-ttu-id="748e5-116">Замените заполнитель *[Enter the application Id here]* в строке, начинающейся с `final static String CLIENT_ID`, только что зарегистрированным идентификатором приложения:</span><span class="sxs-lookup"><span data-stu-id="748e5-116">Replace the *[Enter the application Id here]* in the line starting with `final static String CLIENT_ID` with the application ID you just registered:</span></span>

```java
final static String CLIENT_ID = "[Enter the application Id here]";
```
<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="748e5-117">Откройте файл `AndroidManifest.xml` (выбрав `app` > `manifests`) и добавьте приведенное ниже действие в узел `manifest\application`.</span><span class="sxs-lookup"><span data-stu-id="748e5-117">Open `AndroidManifest.xml` (under `app` > `manifests`) Add the following activity to `manifest\application` node.</span></span> <span data-ttu-id="748e5-118">Так вы зарегистрируете `BrowserTabActivity`, чтобы позволить операционной системе возобновить ваше приложение после завершения аутентификации.</span><span class="sxs-lookup"><span data-stu-id="748e5-118">This registers a `BrowserTabActivity` to allow the OS to resume your application after completing the authentication:</span></span>
</li>
</ol>

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
<!-- Workaround for Docs conversion bug -->
<ol start="8">
<li>
<span data-ttu-id="748e5-119">В `BrowserTabActivity` замените заполнитель `[Enter the application Id here]` идентификатором приложения.</span><span class="sxs-lookup"><span data-stu-id="748e5-119">In the `BrowserTabActivity`, replace `[Enter the application Id here]` with the application ID.</span></span>
</li>
</ol>
