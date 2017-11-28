---
title: "Приступая к работе с Azure AD версии 2 для iOS. Настройка | Документация Майкрософт"
description: "В этой статье описано, как приложения iOS (Swift) могут вызывать API, которому необходимы маркеры доступа, с помощью конечной точки Azure Active Directory версии 2."
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
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 0ebca65585fc87bd4a85ba092cd423fce9540f58
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="46d09-103">Создание приложения (экспресс)</span><span class="sxs-lookup"><span data-stu-id="46d09-103">Create an application (Express)</span></span>
<span data-ttu-id="46d09-104">Теперь вам необходимо зарегистрировать приложение на *портале регистрации приложений Майкрософт*:</span><span class="sxs-lookup"><span data-stu-id="46d09-104">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="46d09-105">Зарегистрируйте свое приложение на [портале регистрации приложений Майкрософт](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure).</span><span class="sxs-lookup"><span data-stu-id="46d09-105">Register your application via the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span></span>
2.  <span data-ttu-id="46d09-106">Введите имя для приложения и адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="46d09-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="46d09-107">Выберите параметр Guided Setup (Пошаговая настройка).</span><span class="sxs-lookup"><span data-stu-id="46d09-107">Make sure the option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="46d09-108">Следуйте инструкциям, чтобы получить идентификатор приложения. Затем вставьте его в свой код.</span><span class="sxs-lookup"><span data-stu-id="46d09-108">Follow the instructions to obtain the application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-to-your-solution-advanced"></a><span data-ttu-id="46d09-109">Добавление сведений о регистрации приложения в решение (дополнительно)</span><span class="sxs-lookup"><span data-stu-id="46d09-109">Add your application registration information to your solution (Advanced)</span></span>

1.  <span data-ttu-id="46d09-110">Перейдите на [портал регистрации приложений](https://apps.dev.microsoft.com/portal/register-app)</span><span class="sxs-lookup"><span data-stu-id="46d09-110">Go to [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app)</span></span>
2.  <span data-ttu-id="46d09-111">Введите имя для приложения и адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="46d09-111">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="46d09-112">Убедитесь, что параметр Guided Setup (Пошаговая настройка) не выбран.</span><span class="sxs-lookup"><span data-stu-id="46d09-112">Make sure the option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="46d09-113">Щелкните `Add Platform`, затем выберите `Native Application` и щелкните `Save`.</span><span class="sxs-lookup"><span data-stu-id="46d09-113">Click `Add Platform`, then select `Native Application` and click `Save`</span></span>
5.  <span data-ttu-id="46d09-114">Вернитесь в Xcode.</span><span class="sxs-lookup"><span data-stu-id="46d09-114">Go back to Xcode.</span></span> <span data-ttu-id="46d09-115">В `ViewController.swift` замените строку, начинающуюся с '`let kClientID`', на зарегистрированный идентификатор приложения:</span><span class="sxs-lookup"><span data-stu-id="46d09-115">In `ViewController.swift`, replace the line starting with '`let kClientID`' with the application ID you just registered:</span></span>

```swift
let kClientID = "Your_Application_Id_Here"
```

<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
<span data-ttu-id="46d09-116">Щелкните <code>Info.plist</code>, удерживая клавишу CTRL, чтобы открыть контекстное меню, затем щелкните <code>Open As</code> > <code>Source Code</code>
.</span><span class="sxs-lookup"><span data-stu-id="46d09-116">Control+click <code>Info.plist</code> to bring up the contextual menu, and then click: <code>Open As</code> > <code>Source Code</code>
</span></span></li>
<li>
<span data-ttu-id="46d09-117">Добавьте следующий элемент в корневой узел <code>dict</code>:</span><span class="sxs-lookup"><span data-stu-id="46d09-117">Under the <code>dict</code> root node, add the following:</span></span>
</li>
</ol>

```xml
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>$(PRODUCT_BUNDLE_IDENTIFIER)</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>msal[Your_Application_Id_Here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
<ol start="8">
<li>
<span data-ttu-id="46d09-118">Замените <i><code>[Your_Application_Id_Here]</code></i> зарегистрированным идентификатором приложения.</span><span class="sxs-lookup"><span data-stu-id="46d09-118">Replace <i><code>[Your_Application_Id_Here]</code></i> with the Application Id you just registered</span></span>
</li>
</ol>
