---
title: "aaaOffice 365 внешний общий доступ и совместная работа Azure Active Directory B2B | Документы Microsoft"
description: "Справочные материалы по сопоставлению утверждений для службы совместной работы Azure Active Directory B2B."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 60452b27b328453eda729bd839c982b479cb6f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="office-365-external-sharing-and-azure-active-directory-b2b-collaboration"></a>Внешний общий доступ Office 365 и служба совместной работы Azure Active Directory B2B

Внешний общий доступ в Office 365 (OneDrive, SharePoint Online, объединенные группы, т. д.) и Azure Active Directory (Azure AD) B2B совместной работы с технической точки зрения hello же самое. Всем внешним доступом (за исключением OneDrive или SharePoint Online), включая гостей в группах Office 365, уже использует приглашения совместной работы Azure AD B2B hello API-интерфейсы для управления доступом.

В OneDrive и SharePoint Online используется другой диспетчер приглашений. Поддержка внешнего общего доступа в OneDrive и SharePoint Online была реализована до того, как ее внедрили в Azure AD. Со временем общий доступ к OneDrive или SharePoint Online внешних начисленная несколько функций и несколько миллионов пользователей, применяющих hello продукта встроенные общий доступ к шаблону. Однако существуют незначительные различия в принципах работы внешнего общего доступа OneDrive и SharePoint Online и службы совместной работы Azure AD B2B:

- OneDrive или SharePoint Online пользователи toohello каталог добавляется после пользователи активирован приглашения. Таким образом прежде чем активации, вы не видите hello пользователя на портале Azure AD. Если другой сайт приглашает пользователя в hello это время, создается новое приглашение. При использовании службы совместной работы Azure AD B2B пользователь добавляется непосредственно после отправки приглашения, поэтому он сразу везде отображается.

- взаимодействие активации Hello в OneDrive или SharePoint Online отличается от работы hello в совместной работы Azure AD B2B. После пользователь redeems приглашение, hello взаимодействия выглядят одинаково.

- Пользователей, приглашенных в службу совместной работы Azure AD B2B, можно выбирать в диалоговых окнах общего доступа OneDrive и SharePoint Online. Приглашенные пользователи OneDrive и SharePoint Online также отображаются в Azure AD после того, как они активируют свои приглашения.

- toomanage внешнего совместного использования в OneDrive или SharePoint Online с Azure AD B2B совместной работы, задайте hello OneDrive или SharePoint Online внешнего совместного использования задание слишком**только открыть доступ для внешних пользователей уже в каталоге hello**. Пользователи могут перейти tooexternally общих сайтов и выбора с внешними участниками, Здравствуйте, администратор добавил. Здравствуйте, администратор может добавить hello внешними участниками через hello приглашения совместной работы B2B API-интерфейсы.

![OneDrive или SharePoint Online настройки общего доступа к внешней Hello](media/active-directory-b2b-o365-external-user/odsp-sharing-setting.png)

## <a name="next-steps"></a>Дальнейшие действия

Другие статьи о службе совместной работы Azure AD B2B:

* [Что такое служба совместной работы Azure AD B2B?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Свойства пользователя службы совместной работы Azure Active Directory B2B](active-directory-b2b-user-properties.md)
* [Добавление роли пользователя tooa B2B совместной работы](active-directory-b2b-add-guest-to-role.md)
* [Делегирование приглашений для службы совместной работы Azure Active Directory B2B](active-directory-b2b-delegate-invitations.md)
* [Динамические группы и служба совместной работы Azure Active Directory B2B](active-directory-b2b-dynamic-groups.md)
* [Примеры кода и команд PowerShell для службы совместной работы Azure Active Directory B2B](active-directory-b2b-code-samples.md)
* [Настройка приложений SaaS для службы совместной работы B2B](active-directory-b2b-configure-saas-apps.md)
* [Основные сведения о токенах пользователей в службе совместной работы Azure Active Directory B2B](active-directory-b2b-user-token.md)
* [Сопоставление утверждений пользователя службы совместной работы B2B в Azure Active Directory](active-directory-b2b-claims-mapping.md)
* [Текущие ограничения службы совместной работы Azure Active Directory B2B](active-directory-b2b-current-limitations.md)
