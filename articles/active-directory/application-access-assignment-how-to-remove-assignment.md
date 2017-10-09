---
title: "aaaHow tooremove пользователя на доступ к приложению tooan | Документы Microsoft"
description: "Понять, как tooremove пользователя на доступ к приложению tooan"
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
ms.openlocfilehash: 17017bddb73aad5a0ef3a411ac91bf0423f0b600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooremove-a-users-access-tooan-application"></a>Как tooremove пользователя на доступ к приложению tooan

В этой статье помогут toounderstand как tooremove пользователя на доступ к приложению tooan.

## <a name="i-want-tooremove-a-specific-users-or-groups-assignment-tooan-application"></a>Я хочу tooremove приложения tooan назначения определенного пользователя или группы

tooremove пользователь или группа назначения tooan приложении, выполните действия hello, перечисленные в hello [удалить назначение пользователя или группу из корпоративного приложения в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) статьи.

. ## требуется toodisable все приложения tooan доступа для каждого пользователя

toodisable все приложение tooan входа в систему пользователя, выполните шаги hello, указанные в hello [отключить пользователя войти в приложение в Azure Active Directory предприятия](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) статьи.

## <a name="i-want-toodelete-an-application-entirely"></a>Я хочу toodelete приложение полностью

слишком**удалить приложение**, следуйте приведенным ниже инструкциям hello:

1.  Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**

2.  Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.

3.  Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.

4.  Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.

5.  Нажмите кнопку **все приложения** tooview список всех приложений.

   * Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**

6.  Выберите hello приложение toodelete.

7.  После загрузки приложения hello щелкните **удалить** значок в верхнем приложения hello **Обзор** колонку.

## <a name="i-want-toodisable-all-future-user-consent-operations-tooany-application"></a>Я хочу toodisable все будущие пользовательского согласия операций tooany приложения

Отключение согласие пользователя для конечных пользователей из приложения tooany соглашаетесь предотвратить всего каталога. Администратор сохранит возможность предоставлять согласие от имени пользователя. согласие toolearn Дополнительные сведения о приложении, и почему может или не можете toodo, прочитайте [пользователя понимание и согласие администратора](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).

слишком**отключить все операции согласия будущих пользователя в каталоге всей**, следуйте приведенным ниже инструкциям hello:

1.  Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**

2.  Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.

3.  Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.

4.  Нажмите кнопку **пользователей и групп** в меню навигации hello.

5.  Щелкните **Параметры пользователя**.

6.  Отключите все операции согласия пользователя в будущем, установка hello **пользователи разрешают приложениям tooaccess свои данные** переключения слишком**нет** и нажмите кнопку hello **Сохранить** кнопки.


# <a name="next-steps"></a>Дальнейшие действия
[Управление доступом tooapps](active-directory-managing-access-to-apps.md)
