---
title: "Приступая к работе aaaAzure AD v2 iOS — Настройка | Документы Microsoft"
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
ms.openlocfilehash: 537cc7f0de6cd947fe340566c9e93f8bb08d57a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="a4d34-103">Создание приложения (экспресс)</span><span class="sxs-lookup"><span data-stu-id="a4d34-103">Create an application (Express)</span></span>
<span data-ttu-id="a4d34-104">Теперь необходимо приложение hello tooregister *портала регистрации приложения Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="a4d34-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="a4d34-105">Зарегистрировать приложение через hello [портала регистрации приложения Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span><span class="sxs-lookup"><span data-stu-id="a4d34-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span></span>
2.  <span data-ttu-id="a4d34-106">Введите имя для приложения и адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="a4d34-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="a4d34-107">Убедитесь, что установлен параметр hello для интерактивной установки</span><span class="sxs-lookup"><span data-stu-id="a4d34-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="a4d34-108">Выполните код приложения hello tooobtain инструкции hello и вставьте его в коде</span><span class="sxs-lookup"><span data-stu-id="a4d34-108">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="a4d34-109">Добавить решение tooyour сведения о регистрации приложения (Дополнительно)</span><span class="sxs-lookup"><span data-stu-id="a4d34-109">Add your application registration information tooyour solution (Advanced)</span></span>

1.  <span data-ttu-id="a4d34-110">Go слишком[портала регистрации приложения Microsoft](https://apps.dev.microsoft.com/portal/register-app)</span><span class="sxs-lookup"><span data-stu-id="a4d34-110">Go too[Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app)</span></span>
2.  <span data-ttu-id="a4d34-111">Введите имя для приложения и адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="a4d34-111">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="a4d34-112">Убедитесь, что hello для интерактивной программы установки не установлен</span><span class="sxs-lookup"><span data-stu-id="a4d34-112">Make sure hello option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="a4d34-113">Щелкните `Add Platform`, затем выберите `Native Application` и щелкните `Save`.</span><span class="sxs-lookup"><span data-stu-id="a4d34-113">Click `Add Platform`, then select `Native Application` and click `Save`</span></span>
5.  <span data-ttu-id="a4d34-114">Вы можете вернуться tooXcode.</span><span class="sxs-lookup"><span data-stu-id="a4d34-114">Go back tooXcode.</span></span> <span data-ttu-id="a4d34-115">В `ViewController.swift`, замените строку hello, начиная с "`let kClientID`" с Идентификатором приложения hello, только что зарегистрирован:</span><span class="sxs-lookup"><span data-stu-id="a4d34-115">In `ViewController.swift`, replace hello line starting with '`let kClientID`' with hello application ID you just registered:</span></span>

```swift
let kClientID = "Your_Application_Id_Here"
```

<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
<span data-ttu-id="a4d34-116">Щелкните, удерживая нажатой <code>Info.plist</code> toobring вверх hello контекстного меню и выберите: <code>Open As</code>> <code>Source Code</code>
</span><span class="sxs-lookup"><span data-stu-id="a4d34-116">Control+click <code>Info.plist</code> toobring up hello contextual menu, and then click: <code>Open As</code> > <code>Source Code</code>
</span></span></li>
<li>
<span data-ttu-id="a4d34-117">В разделе hello <code>dict</code> корневой узел, добавьте hello следующее:</span><span class="sxs-lookup"><span data-stu-id="a4d34-117">Under hello <code>dict</code> root node, add hello following:</span></span>
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
<span data-ttu-id="a4d34-118">Замените <i> <code>[Your_Application_Id_Here]</code> </i> с только что зарегистрирован идентификатор приложения hello</span><span class="sxs-lookup"><span data-stu-id="a4d34-118">Replace <i><code>[Your_Application_Id_Here]</code></i> with hello Application Id you just registered</span></span>
</li>
</ol>
