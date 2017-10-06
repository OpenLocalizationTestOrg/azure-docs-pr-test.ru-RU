---
title: "aaaManage единого входа для прокси приложения Azure AD | Документы Microsoft"
description: "Дополнительные сведения об основах hello из единого входа с помощью прокси приложения"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: a278751a5cb1bf98c970a4e5d2eb3edc3b784096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-ad-application-proxy-provide-single-sign-on"></a>Как прокси приложения Azure AD предоставляет единый вход?

Единый вход — это ключевой элемент прокси приложения Azure AD.  Он обеспечивает hello оптимального взаимодействия с пользователем, так как пользователи имеют только toosign в tooAzure Active Directory в облаке hello. После проверки подлинности tooAzure Active Directory, соединитель прокси приложения hello обрабатывает hello проверки подлинности toohello локального приложения. внутреннее приложение Hello не может определить hello различие между удаленным пользователям вход через прокси-сервер приложения и обычного использования на устройстве, присоединенных к домену. 

для приложений,-tooyour toouse Azure Active Directory необходимо tooselect **Azure Active Directory** как hello метод предварительной проверки подлинности. При выборе **Passthrough** пользователей не аутентификации tooAzure Active Directory, но направленной прямой toohello приложения. Этот параметр можно настроить при первой публикации приложения, или перейдите tooyour приложение hello портал Azure и изменить параметры прокси-сервера приложения hello. 

toosee единого входа параметры, выполните следующие действия:

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Перейдите в слишком**Azure Active Directory** > **корпоративных приложений** > **все приложения**.
3. Приложение SELECT hello, параметры которого единого входа вы хотите toomanage.
4. Щелкните **Единый вход**.

   ![Раскрывающееся меню "Единый вход"](./media/application-proxy-sso-overview/single-sign-on-mode.png)

Раскрывающееся меню Hello показывает пять вариантов-tooyour приложения:

* Единый вход Azure AD отключен
* Единый вход по паролю
* Связанный единый вход
* Встроенная проверка подлинности Windows
* Единый входа на основе заголовка

## <a name="azure-ad-single-sign-on-disabled"></a>Единый вход Azure AD отключен

Если вы не хотите toouse интеграции Azure Active Directory для-tooyour приложения, выберите **Azure AD единый вход отключен**. Если этот параметр выбран, пользователи могут дважды проходить аутентификацию. Во-первых они проверки подлинности tooAzure Active Directory, а затем войдите в самом приложении toohello. 

Этот параметр является хорошим выбором, если локальные приложения не требует tooauthenticate пользователей, но желательно tooadd Azure Active Directory как уровень безопасности для удаленного доступа. 

## <a name="password-based-sign-on"></a>Единый вход по паролю

Если требуется toouse Azure Active Directory как хранилище паролей для локальных приложений, щелкните **пароль входа на основе**. Этот параметр удобно использовать, если для аутентификации приложение использует сочетание имени пользователя и пароля, а не маркеры доступа или заголовки. С использованием пароля входа пользователи должны toosign в toohello приложения hello первом доступе к нему. После этого Azure Active Directory предоставляет hello имя пользователя и пароль от имени пользователя hello. 

Сведения о настройке входа по паролю см. в разделе [Хранение паролей для единого входа с помощью прокси приложения](application-proxy-sso-azure-portal.md).

## <a name="linked-sign-on"></a>Связанный единый вход

Если вы уже настроили решение единого входа для своих локальных удостоверений, выберите **Вход по ссылке**. Этот параметр позволяет Azure Active Directory tooleverage существующими решениями единого входа, но по-прежнему предоставляет пользователям toohello приложение удаленного доступа. 

Дополнительные сведения о функции связанного входа (существующей функции единого входа) см. в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

## <a name="integrated-windows-authentication"></a>Встроенная проверка подлинности Windows

Если локальные приложения используют Authentication(IWA) интеграции Windows, или если требуется toouse ограниченное делегирование Kerberos (KCD) для единого входа, выберите **встроенная проверка подлинности Windows**. Этот параметр пользователи достаточно tooauthenticate tooAzure Active Directory, и затем соединитель прокси приложения hello олицетворяет пользователя hello tooget маркер Kerberos и входа в приложение toohello. 

Сведения о настройке встроенной проверки подлинности Windows см. в разделе [Реализация единого входа в приложения с помощью прокси приложения](active-directory-application-proxy-sso-using-kcd.md).

## <a name="header-based-sign-on"></a>Единый входа на основе заголовка 

Если приложения используют заголовки для аутентификации, выберите **Вход на основе заголовков**. Этот параметр пользователи должны только tooauthentication hello Azure Active Directory. Партнеры корпорации Майкрософт с помощью службы проверки подлинности сторонних вызывается PingAccess, который преобразуется в формат заголовка для приложения hello hello маркер доступа Azure Active Directory. 

Сведения о настройке аутентификации на основе заголовка см. в разделе [Публикация приложений с поддержкой аутентификации на основе заголовков с использованием прокси приложения Azure AD и PingAccess](application-proxy-ping-access.md).

## <a name="next-steps"></a>Дальнейшие действия

- [Хранение паролей для единого входа с помощью прокси приложения](application-proxy-sso-azure-portal.md)
- [Реализация единого входа в приложения с помощью прокси приложения](active-directory-application-proxy-sso-using-kcd.md)
- [Публикация приложений с поддержкой аутентификации на основе заголовков с использованием прокси приложения Azure AD и PingAccess](application-proxy-ping-access.md) 
