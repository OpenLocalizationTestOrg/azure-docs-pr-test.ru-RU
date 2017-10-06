---
title: "aaaAzure AD v2 Android Приступая к работе - тестирования | Документы Microsoft"
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
ms.openlocfilehash: 499f32b46fd44cca0e52179bced49b311135d8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Тестирование кода

1. Развертывание вашего кода tooyour устройстве или эмуляторе.
2. Когда вы будете готовы tootest, используйте Microsoft Azure Active Directory (учетная запись организации) или toosign учетной записи учетную запись Майкрософт (live.com, outlook.com) в. 

![Пример снимка экрана](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
<br/><br/>
![Вход](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)

### <a name="consent"></a>Согласие на предоставление разрешений
Hello при первом входе в приложение tooyour они предоставят согласия экрана примерно toohello ниже, где они должны принимать tooexplicitly: 

![Согласие на предоставление разрешений](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a>Ожидаемые результаты
Вы увидите результаты hello tooMicrosoft вызова Graph API «me» конечной точкой, используется профиль пользователя hello tootooobtain - https://graph.microsoft.com/v1.0/me. Список распространенных конечных точек Microsoft Graph см. в [этой статье](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Дополнительные сведения об областях и делегированных разрешениях

Hello Microsoft Graph API требует hello `user.read` области профиля пользователя tooread hello. По умолчанию эта область автоматически добавляется в каждое приложение, регистрируемое на портале регистрации. Для некоторых других API Microsoft Graph, а также пользовательских API для вашего внутреннего сервера могут потребоваться дополнительные области. Например, для Microsoft Graph hello области `Calendars.Read` является обязательным toolist hello пользовательских календарях. В порядке tooaccess hello календаря пользователя в контексте приложения, вы должны tooadd hello `Calendars.Read` делегировать разрешения toohello приложения регистрационную информацию, а затем добавьте hello `Calendars.Read` toohello область `acquireTokenSilentAsync` вызова. Hello пользователей могут запрашиваться дополнительных согласие по мере увеличения количества hello областей.

<!--end-collapse-->
