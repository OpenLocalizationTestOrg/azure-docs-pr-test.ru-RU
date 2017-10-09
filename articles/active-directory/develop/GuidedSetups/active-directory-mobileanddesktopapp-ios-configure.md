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
## <a name="create-an-application-express"></a>Создание приложения (экспресс)
Теперь необходимо приложение hello tooregister *портала регистрации приложения Microsoft*:
1. Зарегистрировать приложение через hello [портала регистрации приложения Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)
2.  Введите имя для приложения и адрес электронной почты.
3.  Убедитесь, что установлен параметр hello для интерактивной установки
4.  Выполните код приложения hello tooobtain инструкции hello и вставьте его в коде

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Добавить решение tooyour сведения о регистрации приложения (Дополнительно)

1.  Go слишком[портала регистрации приложения Microsoft](https://apps.dev.microsoft.com/portal/register-app)
2.  Введите имя для приложения и адрес электронной почты.
3.  Убедитесь, что hello для интерактивной программы установки не установлен
4.  Щелкните `Add Platform`, затем выберите `Native Application` и щелкните `Save`.
5.  Вы можете вернуться tooXcode. В `ViewController.swift`, замените строку hello, начиная с "`let kClientID`" с Идентификатором приложения hello, только что зарегистрирован:

```swift
let kClientID = "Your_Application_Id_Here"
```

<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
Щелкните, удерживая нажатой <code>Info.plist</code> toobring вверх hello контекстного меню и выберите: <code>Open As</code>> <code>Source Code</code>
</li>
<li>
В разделе hello <code>dict</code> корневой узел, добавьте hello следующее:
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
Замените <i> <code>[Your_Application_Id_Here]</code> </i> с только что зарегистрирован идентификатор приложения hello
</li>
</ol>
