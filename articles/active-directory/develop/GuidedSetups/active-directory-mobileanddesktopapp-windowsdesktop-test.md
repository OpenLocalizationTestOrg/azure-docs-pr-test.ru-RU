---
title: "aaaAzure AD v2 Windows Desktop Приступая к работе - тестирования | Документы Microsoft"
description: "Здесь описывается, как классические приложения для Windows .NET (XAML) могут вызвать API, требующий маркеры доступа от конечной точки Azure Active Directory версии 2."
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
ms.openlocfilehash: 0ae9612e1585c54a3fe35ba9d18f92554099b2c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Тестирование кода

Чтобы tootest приложение, нажмите клавишу `F5` toorun свой проект в Visual Studio. Откроется главное окно.

![Пример снимка экрана](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

Когда будете готовы tootest щелкните *вызывать Graph API Microsoft* и использовать Microsoft Azure Active Directory (учетная запись организации) либо toosign учетную запись учетной записью Майкрософт (live.com, outlook.com) в. Он впервые hello, появится окно с запросом пользователя toosign в:

![Вход](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a>Согласие на предоставление разрешений
Hello при первом входе в приложение tooyour откроется с согласия экрана примерно toohello ниже, где необходимо принять tooexplicitly:

![Экран согласия](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a>Ожидаемые результаты
Должны появиться сведения о профиле пользователя, возвращенный вызовом Microsoft Graph API hello на экране приветствия результатов вызова API.

Вы также увидите основные сведения о hello токена, полученного через `AcquireTokenAsync` или `AcquireTokenSilentAsync` hello маркера информационной панели:

|Свойство  |Формат  |Описание |
|---------|---------|---------|
|Имя | {Полное имя пользователя} |пользователь Hello и фамилию имя|
|Имя пользователя |<span>user@domain.com</span> |Hello имя пользователя, используемое tooidentify hello пользователя|
|Истечение срока действия маркера |{дата и время}         |время Hello, на какие hello истечения срока действия маркера. MSAL продлить срок действия hello можно, обновив hello токен при необходимости|
|Маркер доступа |{Строка}         |Строка токена Hello отправлено, будут отправлены tooHTTP запросы, требующие заголовок авторизации|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Дополнительные сведения об областях и делегированных разрешениях
Graph API требуется hello `user.read` область tooread профиля пользователя. По умолчанию эта область автоматически добавляется в каждое приложение, регистрируемое на портале регистрации. Некоторые другие API Graph, а также пользовательские API для вашего внутреннего сервера требуют дополнительные области. Например, граф `Calendars.Read` является обязательным toolist пользовательских календарях. В порядке tooaccess Здравствуйте календаря пользователя в контексте приложения, необходимо tooadd `Calendars.Read` делегировать сведения о регистрации приложения, а затем добавьте `Calendars.Read` toohello `AcquireTokenAsync` вызова. Пользователя запрашивается согласие дополнительных, при увеличении числа hello областей.

<!--end-collapse-->



