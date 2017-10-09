---
title: "приложения, использующие aaaClaims - прокси приложения Azure AD | Документы Microsoft"
description: "Как toopublish локального приложения ASP.NET, принимающие утверждений служб федерации Active Directory для безопасного удаленного доступа пользователей."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 91e6211b-fe6a-42c6-bdb3-1fff0312db15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7be633225de700226c7c94815eb91b3de2b61cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a>Работа с приложениями, поддерживающими утверждения, в прокси приложения
[Приложения с поддержкой утверждений](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) выполнить перенаправление toohello службы маркеров безопасности (STS). Hello STS запрашивает учетные данные пользователя hello в обмен на токен и затем перенаправляет toohello приложение hello пользователя. Существует несколько способов tooenable прокси приложения toowork с такие перенаправления. Используйте этот tooconfigure статьи развертывания для приложений, поддерживающих утверждения. 

## <a name="prerequisites"></a>Предварительные требования
Убедитесь, что hello STS, hello приложение, поддерживающее утверждения перенаправляет toois доступны за пределами локальной сети. Можно сделать hello STS доступных путем предоставления доступа к через прокси-сервер или, позволяя за пределами соединения. 

## <a name="publish-your-application"></a>Публикация приложения

1. Опубликуйте приложение в соответствии с toohello инструкциям, описанным в [публикации приложений с помощью прокси приложения](application-proxy-publish-azure-portal.md).
2. Перейдите toohello приложение-страница hello портала и выберите **единого входа**.
3. Если для параметра **Метод предварительной проверки подлинности** выбрано значение **Azure Active Directory**, выберите для параметра **Метод внутренней проверки подлинности** значение **Единый вход Azure AD отключен**. Если вы выбрали **Passthrough** как вашей **метод предварительной проверки подлинности**, не требуется toochange всего.

## <a name="configure-adfs"></a>Настройка AD FS

AD FS можно настроить для приложений, поддерживающих утверждения, одним из двух способов. Привет, сначала при помощи пользовательских доменов. Во-вторых, Hello — с WS-Federation. 

### <a name="option-1-custom-domains"></a>Вариант 1. Личные домены

Если все hello внутренние URL-адреса для приложения: полный доменные имена (FQDN), то можно настроить [пользовательских доменов](active-directory-application-proxy-custom-domains.md) для ваших приложений. Используйте hello пользовательских доменов toocreate внешние URL-адреса, являются hello так же, как hello внутренние URL-адреса. Если внешний URL-адресов совпадают, внутренний URL-адресов, перенаправлений STS hello работать ли пользователи являются локального или удаленного. 

### <a name="option-2-ws-federation"></a>Вариант 2. WS-Federation

1. Откройте оснастку управления AD FS.
2. Go слишком**доверия с проверяющей стороной**, щелкните правой кнопкой мыши приложение hello публикации с помощью прокси приложения и выберите **свойства**.  

   ![Щелчок правой кнопкой мыши имени приложения в разделе "Отношения доверия проверяющей стороны" (снимок экрана)](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. На hello **конечные точки** в разделе **тип конечной точки**выберите **WS-Federation**.
4. В разделе **доверенные URL-адрес**, введите URL-адрес hello, введенного в hello прокси приложения в разделе **внешний URL-адрес** и нажмите кнопку **ОК**.  

   ![Добавление конечной точки: задайте значение в поле «Доверенный URL-адрес» (снимок экрана)](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a>Дальнейшие действия
* [Включение единого входа](application-proxy-sso-overview.md) для приложений, не поддерживающих утверждения.
* [Включить toointeract собственного клиентского приложения с прокси-сервера приложений](active-directory-application-proxy-native-client.md)


