---
title: "aaaHow tooconfigure единого входа tooan приложения прокси приложения | Документы Microsoft"
description: "Как быстро настроить-tooyour приложения прокси приложения"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: e1289203177c77b3a8bcc9058c5c0b8ae50f243e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-single-sign-on-tooan-application-proxy-application"></a>Как tooconfigure единого входа tooan приложения прокси приложения

Единого входа (SSO) позволяет вашей tooaccess пользователей приложения без проверки подлинности несколько раз. Он позволяет toooccur hello одной проверки подлинности в облаке hello, в Azure Active Directory и службу hello или соединитель tooimpersonate hello пользователя toocomplete возможные проблемы дополнительной проверки подлинности из приложения hello;

## <a name="how-tooconfigure-single-sign-on"></a>Как tooconfigure единого входа
tooconfigure единого входа, сначала убедитесь, что приложение настроено для предварительной проверки подлинности через Azure Active Directory. toodo, перейдите слишком**Azure Active Directory**  - &gt; **корпоративных приложений**  - &gt; **все приложения**  - &gt; Приложения ** - &gt; прокси приложения**. На этой странице отображается «Предварительной проверки подлинности» hello поле и убедитесь, что слишком «Azure Active Directory. 

Дополнительные сведения о методах hello предварительной проверки подлинности см. шаг 4 hello [документе публикации приложения](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).

   ![Метод предварительной проверки подлинности на портале Azure](./media/application-proxy-config-sso-how-to/app-proxy.png)

## <a name="configuring-single-sign-on-modes-for-application-proxy-applications"></a>Настройка режимов единого входа для приложения прокси приложения
Далее мы настраиваем hello определенный тип единого входа. методы входа Hello классификации на основе того, какой тип проверки подлинности hello внутреннее приложение использует. Приложения прокси приложений поддерживают три типа входа:

-   **Пароль входа на основе**: пароль входа на основе может использоваться для любого приложения, использующего поля имя пользователя и пароль на toosign. Действия по настройке описаны в [документации по настройке единого входа на основе пароля](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#bring-your-own-password-sso-applications).

-   **Встроенная проверка подлинности Windows**: для приложений, использующих встроенную проверку подлинности Windows, единый вход выполняется с использованием ограниченного делегирования Kerberos. Это обеспечивает разрешение соединителей прокси приложения в tooimpersonate Active Directory-пользователи и toosend и получать от их имени маркеры. Подробные сведения о настройке проверки подлинности Kerberos можно найти в hello [единого входа с документацией KCD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd).

-   **Вход на основе заголовка**: обеспечивается с помощью партнерства и требует дополнительной настройки. Дополнительные сведения о партнерстве hello и пошаговые инструкции по настройке-tooan приложение, которое использует заголовки для проверки подлинности, в разделе hello [PingAccess для документации по Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).

Каждый из этих параметров можно найти, перейдя tooyour приложений в «Корпоративных приложений» и открытие hello **Single Sign-On** страницы в левом меню hello. Обратите внимание, что если приложение создано в старый портал hello, может не отобразиться все эти параметры.

На этой странице отображается еще один дополнительный вариант единого входа: связанный единый вход. Этот вариант также поддерживается прокси приложения. Тем не менее Обратите внимание, что этот параметр не добавляет-toohello приложения. С другой стороны, что приложение hello возможно, уже есть единый вход реализован с помощью другой службы, такие как службы федерации Active Directory. 

Этот параметр позволяет администратору toocreate приложения tooan связи, который пользователи сначала поступить в при доступе к приложения hello. Например если это приложение, настроить пользователей tooauthenticate, с помощью служб федерации Active Directory 2.0, администратор может использовать hello связанного на «вход» параметр toocreate tooit ссылку на панели доступа hello.

## <a name="next-steps"></a>Дальнейшие действия
[Создавайте приложения tooyour, прокси-сервера приложений](active-directory-application-proxy-sso-using-kcd.md)
