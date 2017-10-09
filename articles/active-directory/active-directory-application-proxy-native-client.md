---
title: "приложения native client aaaPublish - Azure AD | Документы Microsoft"
description: "Рассматриваются как tooenable toocommunicate приложения собственного клиента с tooyour безопасный удаленный доступ соединитель прокси приложения Azure AD tooprovide локальных приложений."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f0cae145-e346-4126-948f-3f699747b96e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 0ed2be217bf992f034d8321d5e66569b4cace24f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-native-client-apps-toointeract-with-proxy-applications"></a>Как tooenable toointeract приложения собственного клиента с помощью прокси приложения

В приложениях tooweb сложения прокси приложения Azure Active Directory также может быть используется toopublish приложения native client. Приложения собственного клиента отличаются от веб-приложений, потому что они устанавливаются на устройство, а веб-приложения предоставляются через браузер. 

Прокси приложения поддерживает приложения собственного клиента, принимая выданные маркеры Azure AD, отправляемые в стандартных заголовках HTTP "Authorize".

![Связь между конечными пользователями, Azure Active Directory и опубликованными приложениями](./media/active-directory-application-proxy-native-client/richclientflow.png)

Используйте hello библиотеки аутентификации Azure AD, который отвечает за проверку подлинности и поддерживает многие клиентские среды, toopublish собственных приложений. Прокси приложения попадают hello [сценарий tooWeb API собственного приложения](develop/active-directory-authentication-scenarios.md#native-application-to-web-api). В этой статье рассматриваются четыре шага hello toopublish собственное приложение с помощью прокси приложения и hello библиотеки аутентификации Azure AD. 

## <a name="step-1-publish-your-application"></a>Шаг 1. Публикация приложения
Опубликовать приложение прокси-сервера, как и любое другое приложение и назначьте tooaccess пользователей приложения. Дополнительные сведения см. в статье [Публикация приложений с помощью прокси приложения Azure AD](active-directory-application-proxy-publish.md).

## <a name="step-2-configure-your-application"></a>Шаг 2. Настройка приложения
Настройте собственное приложение, следуя инструкциям ниже.

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Перейдите в слишком**Azure Active Directory** > **регистрации приложения**.
3. Выберите **Регистрация нового приложения**.
4. Укажите имя для приложения, установите **собственного** как тип приложения hello и укажите hello URI перенаправления для приложения. 

   ![Создание регистрации приложения](./media/active-directory-application-proxy-native-client/create.png)
5. Нажмите кнопку **Создать**.

Дополнительные сведения о создании регистрации приложения см. в разделе [Интеграция приложений с Azure Active Directory](.//develop/active-directory-integrating-applications.md).


## <a name="step-3-grant-access-tooother-applications"></a>Шаг 3: Предоставление доступа tooother приложений
Включение приложений tooother toobe предоставляется собственное приложение hello в каталоге:

1. В по-прежнему **регистрации приложения**, выберите hello новый собственным приложением, которое вы только что создали.
2. Выберите **Необходимые разрешения**.
3. Выберите **Добавить**.
4. Сначала откройте hello **выберите API**.
5. Используйте hello поиска панели toofind прокси приложения приложение hello, которые опубликованы в первом разделе hello. Выберите это приложение и щелкните **Выбрать**. 

   ![Найдите приложение hello прокси-сервера](./media/active-directory-application-proxy-native-client/select_api.png)
6. Привет открыть второй этап, **разрешений Select**.
7. Используйте флажок toogrant hello прокси приложения tooyour доступа собственное приложение, затем нажмите кнопку **выберите**.

   ![Предоставление доступа tooproxy приложения](./media/active-directory-application-proxy-native-client/select_perms.png)
8. Нажмите кнопку **Готово**.


## <a name="step-4-edit-hello-active-directory-authentication-library"></a>Шаг 4: Изменение hello библиотеку аутентификации Active Directory
Изменение кода собственное приложение hello в контекста проверки подлинности hello hello библиотеку проверки подлинности Active Directory (ADAL) tooinclude hello следующий текст:

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of hello Native app>",
        new Uri("<Redirect Uri of hello Native App>"),
        PromptBehavior.Never);

//Use hello Access Token tooaccess hello Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

переменные Hello в примере кода hello следует заменить следующим образом:

* **Идентификатор клиента** можно найти в hello портал Azure. Перейдите в слишком**Azure Active Directory** > **свойства** и копирования hello идентификатор каталога. 
* **Внешний URL-адрес** является hello переднего плана введенного URL-адреса в hello прокси приложения. toofind это значение, перейдите toohello **прокси приложения** раздел приложение hello прокси-сервера.
* **Идентификатор приложения** hello собственное приложение можно найти на hello **свойства** страница hello собственного приложения.
* **URI перенаправления собственного приложения hello** можно найти на hello **URI перенаправления** страница hello собственного приложения.


## <a name="see-also"></a>См. также

Дополнительные сведения о потоке собственное приложение hello см. в разделе [tooweb собственное приложение API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)

Для получения hello последние новости и обновления, посетите hello [блога прокси приложения](http://blogs.technet.com/b/applicationproxyblog/)
