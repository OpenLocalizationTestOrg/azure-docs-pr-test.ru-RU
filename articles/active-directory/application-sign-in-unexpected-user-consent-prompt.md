---
title: "Запрос согласия aaaUnexpected при входе в приложение tooan | Документы Microsoft"
description: "Как tootroubleshoot, когда пользователь видит запрос согласия для приложения, интегрированы с Azure AD, вы не ожидали"
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
ms.openlocfilehash: 32b7a5e6256faee0dcfe2e1644da3d3428812d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-tooan-application"></a>Запрос согласия Непредвиденная, при входе в приложение tooan

Многие приложения, которые интегрируются с Azure Active Directory требуют разрешения toovarious ресурсы в toorun порядке. Когда эти ресурсы также интегрированы с Azure Active Directory, разрешения tooaccess их запрашивается при помощи hello Azure AD разрешения framework. 

Это приведет к запрос согласия, показывается hello при первом запуске приложения используется, что часто является единовременной операцией. 

## <a name="scenarios-in-which-users-see-consent-prompts"></a>Сценарии, в которых пользователи видят запрос на согласие

Дополнительные запросы можно ожидать в разных сценариях:

* набор разрешений, необходимые приложения hello Hello изменились.

* Hello пользователя, изначально согласие toohello приложения не являлся администратором, а теперь различных (без прав администратора) пользователь использует приложение hello для hello первый раз.

* Hello пользователя, изначально согласие toohello приложения являлся администратором, но они не согласие от имени hello всей организации.

* Использование приложения Hello [добавочного, так и динамические согласия](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) toorequest дополнительных разрешений после предоставления согласия изначально. Такой подход часто применяется, когда расширенным функциям приложения нужны дополнительные разрешения сверх базового набора.

* Согласие было отозвано после первоначального предоставления.

* Каждый раз при его использовании developer Привет настроил toorequire приложения hello запрос согласия (Примечание: это не лучшее решение).

## <a name="next-steps"></a>Дальнейшие действия

-   [Приложения, разрешения и согласие в Azure Active Directory (конечная точка версии 1.0)](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [Области, разрешения и разрешения в hello Azure Active Directory (конечная точка версии 2.0)](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


