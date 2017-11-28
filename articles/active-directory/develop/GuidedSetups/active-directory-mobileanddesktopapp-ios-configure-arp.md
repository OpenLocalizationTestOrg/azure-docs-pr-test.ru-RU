---
title: "Приступая к работе с Azure AD версии 2 для iOS. Настройка (ARP) | Документация Майкрософт"
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
ms.openlocfilehash: 50cb4a2803b6aebe8b39ec9fb02da2293c1065fa
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
## <a name="add-the-applications-registration-information-to-your-app"></a><span data-ttu-id="0af26-103">Добавление в приложение сведений о его регистрации</span><span class="sxs-lookup"><span data-stu-id="0af26-103">Add the application’s registration information to your app</span></span>

<span data-ttu-id="0af26-104">На этом шаге вам нужно добавить в свой проект идентификатор приложения:</span><span class="sxs-lookup"><span data-stu-id="0af26-104">In this step, you need to add the Application Id to your project:</span></span>

1.  <span data-ttu-id="0af26-105">В `ViewController.swift` замените строку, начинающуюся с '`let kClientID`', на следующую:</span><span class="sxs-lookup"><span data-stu-id="0af26-105">In `ViewController.swift`, replace the line starting with '`let kClientID`' with:</span></span>
```swift
let kClientID = "[Enter the application Id here]"
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="0af26-106">Щелкните <code>Info.plist</code>, удерживая клавишу CTRL, чтобы открыть контекстное меню, затем щелкните <code>Open As</code> > <code>Source Code</code>
.</span><span class="sxs-lookup"><span data-stu-id="0af26-106">Control+click <code>Info.plist</code> to bring up the contextual menu, and then click: <code>Open As</code> > <code>Source Code</code>
</span></span></li>
<li>
<span data-ttu-id="0af26-107">Добавьте следующий элемент в корневой узел <code>dict</code>:</span><span class="sxs-lookup"><span data-stu-id="0af26-107">Under the <code>dict</code> root node, add the following:</span></span>
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
            <string>msal[Enter the application Id here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
