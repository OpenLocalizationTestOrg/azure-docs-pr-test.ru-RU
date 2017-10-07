---
title: "aaaAzure AD v2 JS SPA Интерактивная установка - тестирования | Документы Microsoft"
description: "В этой статье описано, как приложения JavaScript SPA могут вызывать API, которому необходимы маркеры доступа, с помощью конечной точки Azure Active Directory версии 2."
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
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: b2339431a070b5c4ad4058e6c1a9b19b83c84c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Тестирование кода

> ### <a name="testing-with-visual-studio"></a>Тестирование с Visual Studio
> Если вы используете Visual Studio, нажмите клавишу `F5` toorun проекта: hello браузер откроется, а также указаны слишком*http://localhost: {port}* показывающий hello *вызывать Graph API Microsoft* кнопки.

<p/><!-- -->

> ### <a name="testing-with-python-or-another-web-server"></a>Тестирование с помощью Python или другого веб-сервера
> Если вы не используете Visual Studio, убедитесь, что веб-сервера запущена, и он настроен на папку, содержащую hello основе toolisten tooa TCP-порт вашей *index.html* файла. Для Python, можно начать прослушивание порта toohello, выполнив hello в hello команда prompt / терминалов, из папки приложения hello:
> 
> ```bash
> python -m http.server 8080
> ```
>  Откройте браузер hello и введите *http://localhost: 8080* или *http://localhost: {port}* — там, где hello *порт* соответствует toohello порт, на веб-сервере прослушивание. Вы увидите содержимое hello index.html страницы с hello *вызова API Graph Microsoft* кнопки.

## <a name="test-your-application"></a>Тестирование приложения

После hello браузер загружает вашей *index.html*, щелкните hello *вызова API Graph Microsoft* кнопки. Если это первый раз hello перенаправления браузера hello вы toohello v2 Microsoft Azure Active Directory конечной точки, где вы находитесь запрос toosign в.
 
![Пример снимка экрана](media/active-directory-singlepageapp-javascriptspa-test/javascriptspascreenshot1.png)


### <a name="consent"></a>Согласие на предоставление разрешений
Hello первый раз при входе в приложение tooyour решаемой согласия экрана примерно toohello следующую команду, где должны tooaccept:

 ![Экран согласия](media/active-directory-singlepageapp-javascriptspa-test/javascriptspaconsent.png)


### <a name="expected-results"></a>Ожидаемые результаты
Должны появиться сведения о профиле пользователя, возвращенный hello в ответ на вызов Microsoft Graph API.
 
 ![Результаты](media/active-directory-singlepageapp-javascriptspa-test/javascriptsparesults.png)

Также отображаются основные сведения о hello токена, полученного в hello *токена доступа* и *идентификатор токена утверждений* поля.

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Дополнительные сведения об областях и делегированных разрешениях

Hello Microsoft Graph API требует hello `user.read` области профиля пользователя tooread hello. По умолчанию эта область автоматически добавляется в каждое приложение, регистрируемое на портале регистрации. Для некоторых других API Microsoft Graph, а также пользовательских API для вашего внутреннего сервера могут потребоваться дополнительные области. Например, для Microsoft Graph hello области `Calendars.Read` является обязательным toolist hello пользовательских календарях. В порядке tooaccess hello календаря пользователя в контексте приложения hello, вы должны tooadd hello `Calendars.Read` делегировать разрешения toohello приложения регистрационную информацию, а затем добавьте hello `Calendars.Read` toohello область `acquireTokenSilent` вызова. Hello пользователей могут запрашиваться дополнительных согласие по мере увеличения количества hello областей.

Если API внутреннего сервера не требуется область (не рекомендуется), можно использовать hello `clientId` как область hello в hello `acquireTokenSilent` и/или `acquireTokenRedirect` вызовов.

<!--end-collapse-->
