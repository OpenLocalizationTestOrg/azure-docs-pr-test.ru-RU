---
title: "iOS v2 aaaAzure AD Приступая к работе - тестирования | Документы Microsoft"
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
ms.openlocfilehash: 98c73eddabf9664feb19ac6878e9d7315b9aa79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="test-querying-hello-microsoft-graph-api-from-your-ios-application"></a>Тестирование запросов hello Microsoft Graph API из приложения iOS

Нажмите клавишу `Command`  +  `R` toorun кода hello в симуляторе hello.

![Пример снимка экрана](media/active-directory-mobileanddesktopapp-ios-test/iostestscreenshot.png)

Когда вы будете готовы tootest, коснитесь *«Вызвать API Microsoft Graph»* и будет tootype запрос имени пользователя и пароля.

### <a name="consent"></a>Согласие на предоставление разрешений
Hello при первом входе в приложение tooyour откроется с согласия экрана примерно toohello ниже, где необходимо принять tooexplicitly:

![Экран согласия](media/active-directory-mobileanddesktopapp-ios-test/iosconsentscreen.png)

### <a name="expected-results"></a>Ожидаемые результаты
Вы увидите сведения о профиле пользователя, возвращаемый в результате вызова Microsoft Graph API hello в hello *входа* раздела.

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Дополнительные сведения об областях и делегированных разрешениях

Hello Microsoft Graph API требует hello `user.read` области профиля пользователя tooread hello. По умолчанию эта область автоматически добавляется в каждое приложение, регистрируемое на портале регистрации. Для некоторых других API Microsoft Graph, а также пользовательских API для вашего внутреннего сервера могут потребоваться дополнительные области. Например, для Microsoft Graph hello области `Calendars.Read` является обязательным toolist hello пользовательских календарях. В порядке tooaccess hello календаря пользователя в контексте приложения, вы должны tooadd hello `Calendars.Read` делегировать разрешения toohello приложения регистрационную информацию, а затем добавьте hello `Calendars.Read` toohello область `acquireTokenSilent` вызова. Hello пользователей могут запрашиваться дополнительных согласие по мере увеличения количества hello областей.

<!--end-collapse-->



