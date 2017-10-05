---
title: "Приступая к работе с управлением привилегированными пользователями Azure AD | Документация Майкрософт"
description: "Сведения о том, как управлять привилегированными удостоверениями с помощью приложения для управления привилегированными пользователями Azure Active Directory на портале Azure."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2299db7d-bee7-40d0-b3c6-8d628ac61071
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: 17cdff033cc3dbb199d11c3b8ac1acbc92499877
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="start-using-azure-ad-privileged-identity-management"></a>Приступая к использованию Azure AD Privileged Identity Management
С помощью управления привилегированными пользователями в Azure Active Directory (AD) можно администрировать, контролировать и отслеживать доступ в пределах организации, в том числе доступ к ресурсам в Azure AD и остальным веб-службам Microsoft, таким как Office 365 или Microsoft Intune.

В этой статье рассказывается, как добавить приложение Azure AD PIM на панель мониторинга портала Azure.

## <a name="add-the-privileged-identity-management-application"></a>Добавление приложения для управления привилегированными пользователями
Прежде чем вы сможете работать с приложением для управления привилегированными пользователями Azure AD, его необходимо добавить на панель мониторинга портала Azure.

1. Войдите на [портал Azure](https://portal.azure.com/) как глобальный администратор нужного каталога.
2. Если в организации имеется несколько каталогов, выберите свое имя пользователя в правом верхнем углу на портале Azure. Выберите каталог, где необходимо использовать PIM.
3. Выберите **Другие службы** и в текстовое поле "Фильтр" введите **Azure AD Privileged Identity Management**.
4. Установите флажок **Закрепить на панели мониторинга** и нажмите кнопку **Создать**. Откроется приложение Privileged Identity Management.

Если вы первый пользователь, использующий Azure Active Directory Privileged Identity Management в каталоге, вам автоматически назначаются роли **Администратор безопасности** и **Администратор привилегированных ролей** в этом каталоге. Только администраторы привилегированных ролей могут управлять назначением ролей пользователей. Кроме того, вы можете запустить [мастер защиты](active-directory-privileged-identity-management-security-wizard.md), который поможет вам выполнить первое обнаружение и назначение.

## <a name="navigate-to-your-tasks"></a>Переход к задачам
После настройки приложения Azure AD Privileged Identity Management при каждом его запуске будет отображаться колонка навигации. Ее можно использовать для выполнения задач по управлению пользователями.

![Задачи верхнего уровня для управления привилегированными пользователями — снимок экрана](./media/active-directory-privileged-identity-management-getting-started/PIM_Tasks_New.png)

* В разделе **Мои роли** приведен список назначенных вам ролей. Здесь можно активировать любую назначенную вам роль.
* В разделе **Approve Requests (Preview)** (Утверждение запросов (предварительная версия)) приведен список ожидающих запросов на активацию от пользователей в каталоге. [Подробнее.](./privileged-identity-management/azure-ad-pim-approval-workflow.md)
* В разделе **Pending Requests (Preview)** (Запросы в ожидании (предварительная версия)) отображаются все запросы, ожидающие активации.
* Раздел **Проверка доступа** перенаправляет вас к незавершенным проверкам доступа (для себя или для кого-то другого), которые нужно завершить.
* Параметр **Роли каталога Azure AD** расположен в разделе "Управление". Это панель мониторинга, где администраторы привилегированных ролей могут управлять назначением ролей, изменять параметры активации роли, выполнять проверки доступа и многое другое. Параметры на этой панели мониторинга отключены для всех, кто не является администратором привилегированных ролей.

## <a name="next-steps"></a>Дальнейшие действия
В разделе, посвященном [обзору управления привилегированными пользователями Azure AD](active-directory-privileged-identity-management-configure.md) , содержатся дополнительные сведения об управлении административным доступом в организации.

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
