---
title: "aaaSingle tooapps входа с помощью прокси приложения Azure AD | Документы Microsoft"
description: "Включение единого входа для опубликованных локальных приложений с помощью прокси приложения Azure AD в hello портал Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5ff288d36163b74215677d9e34c93c985ac33d54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a>Хранение паролей для единого входа с помощью прокси приложения

Прокси приложения Azure Active Directory помогает повысить производительность путем публикации локальных приложений, чтобы предоставить удаленным сотрудникам безопасный доступ к ним. В hello портал Azure можно также настроить единого входа (SSO) toothese приложений. Вашим пользователям требуется только tooauthenticate с Azure AD, и они могут получать корпоративные приложения без toosign еще раз.

Прокси приложения поддерживает несколько [режимов единого входа](application-proxy-sso-overview.md). Вход по паролю предназначен для приложений, использующих для аутентификации сочетание имени пользователя и пароля. После завершения настройки паролю единого входа для приложения, пользователей toosign в toohello локального приложения один раз. После этого Azure Active Directory сохраняет hello входа в систему и автоматически предоставляет ему toohello приложения при пользователей удаленного доступа к нему. 

Вы должны были опубликовать и протестировать свое приложение с помощью прокси приложения. В противном случае выполните действия hello в [публикация приложений с помощью прокси приложения Azure AD](application-proxy-publish-azure-portal.md) возобновить вернитесь сюда. 

## <a name="set-up-password-vaulting-for-your-application"></a>Настройка хранения пароля для приложения

1. Войдите в toohello [портал Azure](https://portal.azure.com) с правами администратора.
2. Выберите **Azure Active Directory** > **Корпоративные приложения** > **Все приложения**.
3. Выберите из списка hello приложение hello, что требуется tooset копирование с помощью единого входа.  
4. Щелкните **Единый вход**.

   ![Выбор пункта "Единый вход"](./media/application-proxy-sso-azure-portal/select-sso.png)

5. Режим единого входа hello, выберите **пароль входа на основе**.
6. Hello входа URL-адрес введите URL-адрес hello для страницы приветствия ввода toosign свои имя пользователя и пароль в приложении tooyour за пределами корпоративной сети hello. Это может быть hello внешний URL-адрес, созданный при публикации приложения hello через прокси-сервера приложения. 

   ![Выбор входа по паролю и ввод URL-адрес](./media/application-proxy-sso-azure-portal/password-sso.png)

7. Щелкните **Сохранить**.

<!-- Need toorepro?
7. hello page should tell you that a sign-in form was successfully detected at hello provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow hello instructions toopoint out where hello sign-in credentials go. 
-->

## <a name="test-your-app"></a>Тестирование приложения

Go tooexternal URL-адрес, который настроен для удаленного доступа tooyour приложения. Вход, учетные данные для этого приложения (hello учетные данные тестовой учетной записи, которую вы настроили доступ). После успешного входа в необходимо будет tooleave приложение hello и возвращаться без повторного ввода учетных данных. 

## <a name="next-steps"></a>Дальнейшие действия

- Узнайте, как другие способы tooimplement [единого входа с помощью прокси приложения](application-proxy-sso-overview.md)
- Изучите [вопросы безопасности при удаленном доступе к приложениям через прокси приложения Azure AD](application-proxy-security-considerations.md).