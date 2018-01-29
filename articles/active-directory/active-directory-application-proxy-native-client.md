---
title: "Публикация собственных клиентских приложений — Azure AD | Документация Майкрософт"
description: "В этой статье описано, как включить собственные клиентские приложения для взаимодействия с соединителем прокси приложений Azure AD, чтобы обеспечить безопасный удаленный доступ к локальным приложениям."
services: active-directory
documentationcenter: 
author: daveba
manager: mtillman
ms.assetid: f0cae145-e346-4126-948f-3f699747b96e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/31/2017
ms.author: daveba
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 2be62c00d144e47cef8ea4df5aa82554f2bbcc18
ms.sourcegitcommit: 3cdc82a5561abe564c318bd12986df63fc980a5a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/05/2018
---
# <a name="how-to-enable-native-client-apps-to-interact-with-proxy-applications"></a>Включение собственных клиентских приложений для взаимодействия с приложениями прокси

В дополнение к веб-приложениям для публикации собственных клиентских приложений, настроенных с помощью библиотеки ADAL, можно использовать прокси приложения Azure Active Directory. Приложения собственного клиента отличаются от веб-приложений, потому что они устанавливаются на устройство, а веб-приложения предоставляются через браузер. 

Прокси приложения поддерживает собственные клиентские приложения, принимая выданные маркеры Azure AD, отправляемые в заголовке. Служба прокси приложения выполняет проверку подлинности от имени пользователей. Это решение не использует маркеры приложения для проверки подлинности. 

![Связь между конечными пользователями, Azure Active Directory и опубликованными приложениями](./media/active-directory-application-proxy-native-client/richclientflow.png)

Используйте библиотеку аутентификации Azure AD, которая отвечает за аутентификацию и поддерживает многие клиентские среды, для публикации собственных приложений. Прокси приложения вписывается в [сценарий вызова веб-API собственным приложением](develop/active-directory-authentication-scenarios.md#native-application-to-web-api). 

В этой статье рассматриваются четыре действия, которые нужно выполнить, чтобы опубликовать собственное приложение с помощью прокси приложения и библиотеки аутентификации Azure AD. 

## <a name="step-1-publish-your-application"></a>Шаг 1. Публикация приложения
Опубликуйте приложение прокси, как любое другое приложение, и назначьте пользователей, имеющих доступ к вашему приложению. Дополнительные сведения см. в статье [Публикация приложений с помощью прокси приложения Azure AD](active-directory-application-proxy-publish.md).

## <a name="step-2-configure-your-application"></a>Шаг 2. Настройка приложения
Настройте собственное приложение, следуя инструкциям ниже.

1. Войдите на [портале Azure](https://portal.azure.com).
2. Выберите **Azure Active Directory** > **Регистрация приложений**.
3. Выберите **Регистрация нового приложения**.
4. Укажите имя приложения, выберите тип приложения **Машинный код** и укажите универсальный код ресурса (URI)универсальный код ресурса (URI) перенаправления для приложения. 

   ![Создание регистрации приложения](./media/active-directory-application-proxy-native-client/create.png)
5. Нажмите кнопку **Создать**.

Дополнительные сведения о создании регистрации приложения см. в разделе [Интеграция приложений с Azure Active Directory](.//develop/active-directory-integrating-applications.md).


## <a name="step-3-grant-access-to-other-applications"></a>Шаг 3. Предоставление доступа для других приложений
Включите собственное приложение, которое должно быть доступно для других приложений в каталоге.

1. На странице **Регистрация приложений** выберите только что созданное собственное приложение.
2. Выберите **Необходимые разрешения**.
3. Выберите **Добавить**.
4. Откройте первый шаг, **Выбор API**.
5. С помощью панели поиска найдите приложение прокси приложения, которое вы опубликовали в первом разделе. Выберите это приложение и щелкните **Выбрать**. 

   ![Поиск приложения прокси приложения](./media/active-directory-application-proxy-native-client/select_api.png)
6. Откройте второй шаг, **Выбор разрешений**.
7. Установите соответствующий флажок, чтобы предоставить своему собственному приложению доступ к приложению прокси, а затем щелкните **Выбрать**.

   ![Предоставление доступа к приложению прокси приложения](./media/active-directory-application-proxy-native-client/select_perms.png)
8. Нажмите кнопку **Готово**.


## <a name="step-4-edit-the-active-directory-authentication-library"></a>Шаг 4. Изменение библиотеки проверки подлинности Active Directory
Измените код собственного приложения с учетом проверки подлинности с помощью библиотеки Active Directory Authentication Library (ADAL). Для этого включите в код следующий текст:

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of the Native app>",
        new Uri("<Redirect Uri of the Native App>"),
        PromptBehavior.Never);

//Use the Access Token to access the Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

Переменные в примере кода должны быть заменены следующим образом.

* **Идентификатор клиента** находится на портале Azure. Выберите **Azure Active Directory** > **Свойства** и скопируйте идентификатор каталога. 
* **Внешний URL-адрес** — это интерфейсный URL-адрес, введенный в приложении прокси. Чтобы найти это значение, перейдите в раздел **Прокси приложения** приложения прокси.
* **Идентификатор приложения** собственного приложения находится на странице **Свойства** собственного приложения.
* Значение **Redirect URI of the native app** (URI перенаправления собственного клиента) находится на странице **URI перенаправления** собственного приложения.

После изменения этих параметров в ADAL ваши пользователи смогут выполнять проверку подлинности в собственных клиентских приложениях за пределами корпоративной сети. 

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения о блок-схеме собственного приложения см. в разделе [Из нативного приложения к веб-интерфейсу API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).

Дополнительные сведения о настройке см. в статье [Как прокси приложения Azure AD предоставляет единый вход?](application-proxy-sso-overview.md)
