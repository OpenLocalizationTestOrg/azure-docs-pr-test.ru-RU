---
title: "Подготовка приложения Azure AD tooan коллекции пользователей tooconfigure aaaHow | Документы Microsoft"
description: "Как можно быстро настроить многофункциональном пользовательском запись подготовки и отзыва tooapplications уже присутствует в коллекции приложений Azure AD hello"
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
ms.openlocfilehash: 2c28e59a3ac8f221ed93b2f6b0b1221f7604af23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-user-provisioning-tooan-azure-ad-gallery-application"></a>Способ подготовки приложения Azure AD tooan коллекции пользователей tooconfigure

*Подготовка учетной записи пользователя* это hello act, создание, обновление или отключение учетных записях пользователя в хранилище профилей локальных пользователей приложения. Большинство облака и приложений SaaS сохранить hello роли пользователей и разрешения в магазин профиль локального пользователя и наличие такой записи пользователя в локальном хранилище является *необходимые* для единого входа и доступа toowork.

В hello портал Azure, hello **Provisioning** вкладке hello левой панели навигации для корпоративного приложения отображаются какие подготовки режимы поддерживаются для данного приложения. На ней может быть указано одно из двух значений:

## <a name="configuring-an-application-for-manual-provisioning"></a>Настройка приложения для подготовки вручную

*Вручную* подготовки означает, что учетные записи пользователей должна быть создана вручную с помощью hello методы, предоставляемые этого приложения. Например, может потребоваться войти на портал администратора для этого приложения и добавить пользователей с помощью веб-интерфейса. Или отправить электронную таблицу со сведениями об учетной записи пользователя с помощью соответствующего механизма, который предоставляется приложением. В документации hello предоставляемых приложение hello, или приложение hello контакта разработчика toodetermine wat механизмы доступны.

Если вручную только режим hello отображается для данного приложения, это означает, что был создан без подготовки соединитель автоматического Azure AD для приложения hello еще. Или это означает, что приложение hello не не поддержки hello необходимого пользователя API управления после какие toobuild соединителя автоматической подготовки.

Если требуется поддержка toorequest автоматическую подготовку для данного приложения, можете заполнить запрос на <http://aka.ms/aadapprequest>.

## <a name="configuring-an-application-for-automatic-provisioning"></a>Настройка приложения для автоматической подготовки

*Автоматическая подготовка* означает, что для этого приложения был разработан соединитель для подготовки Azure AD. Дополнительные сведения о hello Azure AD на подготовку службы и как он работает, в разделе [tooSaaS автоматизировать подготовку пользователей и их отзыва приложений с Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning).

Дополнительные сведения о статье tooprovision определенных пользователей и групп tooan приложения, [управление Подготовка учетной записи пользователя для корпоративных приложений](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning).

Здравствуйте tooenable необходимые процедуры и настройте автоматическую подготовку различаются в зависимости от приложения hello.

>[!NOTE]
>Необходимо начать с поиск hello установки учебника конкретных toosetting копирование подготовки для приложения и после этих шагов tooconfigure приложение hello и Azure AD toocreate hello инициализации подключения. 
>
>

Учебники приложения можно найти на [список учебников по tooIntegrate приложений SaaS в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-tutorial-list).

Tooconsider важно при настройке подготовки быть tooreview и настроить сопоставления атрибутов hello и рабочие процессы, определяющие, какой поток свойства пользователь (или группа) из toohello приложения Azure AD. Сюда входят свойства hello «сопоставления», будет использоваться toouniquely определить, соответствуют пользователи и группы, между системами двух hello. Дополнительные сведения об этом важном процессе см. в разделах, указанных ниже.

## <a name="next-steps"></a>Дальнейшие действия
[Настройка сопоставлений атрибутов для подготовки пользователей для приложений SaaS в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-customizing-attribute-mappings)

