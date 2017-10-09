---
title: "iOS v2 aaaAzure AD Приступая к работе — Настройка (ARP) | Документы Microsoft"
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
ms.openlocfilehash: e5087e13160243d808b1d02771fa66fb332cfad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a><span data-ttu-id="636ea-103">Добавить приложение tooyour сведения о регистрации приложения hello</span><span class="sxs-lookup"><span data-stu-id="636ea-103">Add hello application’s registration information tooyour app</span></span>

<span data-ttu-id="636ea-104">На этом шаге требуется идентификатор приложения tooyour tooadd hello проекта:</span><span class="sxs-lookup"><span data-stu-id="636ea-104">In this step, you need tooadd hello Application Id tooyour project:</span></span>

1.  <span data-ttu-id="636ea-105">В `ViewController.swift`, замените строку hello, начиная с "`let kClientID`" с:</span><span class="sxs-lookup"><span data-stu-id="636ea-105">In `ViewController.swift`, replace hello line starting with '`let kClientID`' with:</span></span>
```swift
let kClientID = "[Enter hello application Id here]"
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="636ea-106">Щелкните, удерживая нажатой <code>Info.plist</code> toobring вверх hello контекстного меню и выберите: <code>Open As</code>> <code>Source Code</code>
</span><span class="sxs-lookup"><span data-stu-id="636ea-106">Control+click <code>Info.plist</code> toobring up hello contextual menu, and then click: <code>Open As</code> > <code>Source Code</code>
</span></span></li>
<li>
<span data-ttu-id="636ea-107">В разделе hello <code>dict</code> корневой узел, добавьте hello следующее:</span><span class="sxs-lookup"><span data-stu-id="636ea-107">Under hello <code>dict</code> root node, add hello following:</span></span>
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
            <string>msal[Enter hello application Id here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
