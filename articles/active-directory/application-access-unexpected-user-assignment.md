---
title: "Пользователи tooapplications aaaHow tooAssign | Документы Microsoft"
description: "Понять, как пользователи получить назначения tooan приложения в клиенте"
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
ms.openlocfilehash: 4df60c7d723140d0d1bbd6ba8b34aa4e762d1138
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-tooapplications"></a>Как tooapplications tooassign пользователей

В этой статье помогут toounderstand получить назначение пользователей tooan приложения в клиенте.

## <a name="how-do-users-get-assigned-tooan-application-in-azure-ad"></a>Как пользователей получить назначения tooan приложения в Azure AD?

Для tooaccess пользователя приложения их необходимо назначить tooit иным образом. Назначение может выполнять администратор, business делегата или в некоторых случаях пользователь hello сами. Ниже описываются способы hello, которые пользователи могут получить назначения tooapplications:

1.  Администратор [назначает пользователя](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) toohello приложению напрямую

2.  Администратор [Назначение группы](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) hello пользователя является членом toohello приложения, включая:

  * Группа, синхронизированная из локальной среды.

  * Безопасность статической группы в облаке hello

  * Объект [динамической безопасности группы](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) в облаке hello

  * Группы Office 365, созданной в облаке hello

  * Hello [всех пользователей](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) группы

3.  Администратор включает [самообслуживания доступ к приложению](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow tooadd пользователя приложения с помощью hello [панели доступа приложения](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **добавить приложение** функция **без утверждения бизнеса**

4.  Администратор включает [самообслуживания доступ к приложению](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow tooadd пользователя приложения с помощью hello [панели доступа приложения](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **добавить приложение** компонент, но только w **i-ой предварительного разрешения из выбранного набора утверждающих бизнеса**

5.  Администратор включает [Самостоятельное управление группами](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow toojoin пользователем группы, назначенный приложению слишком**без утверждения бизнеса**

6.  Администратор включает [Самостоятельное управление группами](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow toojoin пользователя, назначенный приложению в, но только группы **с предварительного разрешения из выбранного набора утверждающих бизнеса**

7.  Администратор назначает лицензии пользователя tooa непосредственно для первой стороной приложения, таких как [Microsoft Office 365](http://products.office.com/)

8.  Администратор назначает, tooa лицензионную группу, hello пользователь является членом tooa первой стороной приложения, как [Microsoft Office 365](http://products.office.com/)

9.  [Администратора согласии приложения tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe использовать все пользователи, а затем пользователь входит в приложении toohello

10. Пользователь [согласии приложения tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) сами при входе в приложение toohello

## <a name="next-steps"></a>Дальнейшие действия
[Управление приложениями с помощью Azure Active Directory](active-directory-enable-sso-scenario.md)
