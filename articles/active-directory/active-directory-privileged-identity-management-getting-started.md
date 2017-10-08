---
title: "aaaGet работы с Azure AD Privileged Identity Management | Документы Microsoft"
description: "Узнайте, как toomanage привилегированных удостоверений с приложением hello Azure Active Directory Privileged Identity Management на портале Azure."
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
ms.openlocfilehash: a89205023a8dbcc3649fa732735ca927e64736ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="start-using-azure-ad-privileged-identity-management"></a>Приступая к использованию Azure AD Privileged Identity Management
С помощью управления привилегированными пользователями в Azure Active Directory (AD) можно администрировать, контролировать и отслеживать доступ в пределах организации, Эта область включает tooresources доступа в Azure AD и других электронных услуг Microsoft, такие как Office 365 или Microsoft Intune.

В этой статье рассказывается о том, как tooadd hello tooyour приложения Azure AD PIM Azure панели мониторинга портала.

## <a name="add-hello-privileged-identity-management-application"></a>Добавить приложение hello Privileged Identity Management
Прежде чем использовать Azure AD Privileged Identity Management, необходимо tooyour приложения hello tooadd Azure панели мониторинга портала.

1. Войдите в toohello [портал Azure](https://portal.azure.com/) роли глобального администратора каталога.
2. Если ваша организация имеет несколько каталогов, выберите свое имя пользователя в верхнем правом углу hello hello портал Azure. Выберите каталог hello место toouse PIM.
3. Выберите **дополнительные службы** и использовать hello toosearch текстовое поле фильтра для **Azure AD Privileged Identity Management**.
4. Проверьте **toodashboard ПИН-код** и нажмите кнопку **создать**. Открывает Hello управления привилегированными пользователями приложения.

Если вы hello первого лица toouse Azure AD Privileged Identity Management в вашем каталоге, автоматически назначаются hello **администратор безопасности** и **привилегированной роли администратора** ролей в каталоге hello. Только администраторы привилегированных ролей могут управлять назначением ролей пользователей. Кроме того, вы можете toorun hello [мастер безопасности.](active-directory-privileged-identity-management-security-wizard.md) которое поможет выполнить hello первого обнаружения и назначение опыта работы.

## <a name="navigate-tooyour-tasks"></a>Перейдите tooyour задачи
После настройки Azure AD Privileged Identity Management вы видите колонке навигации hello каждый раз при открытии приложения hello. Используйте этот tooaccomplish колонке идентификаторов задач управления.

![Задачи верхнего уровня для управления привилегированными пользователями — снимок экрана](./media/active-directory-privileged-identity-management-getting-started/PIM_Tasks_New.png)

* **Мои ролей** осуществляется tooa список ролей, назначенных tooyou. Здесь можно активировать любую назначенную вам роль.
* В разделе **Approve Requests (Preview)** (Утверждение запросов (предварительная версия)) приведен список ожидающих запросов на активацию от пользователей в каталоге. [Подробнее.](./privileged-identity-management/azure-ad-pim-approval-workflow.md)
* **Ожидающие запросы (Предварительная версия)** отображает любое текущее tooactivate toohave внесенные запросов.
* **Проверьте доступ** принимает tooany ожидающих доступ рассматриваются необходимые toocomplete, ли анализа доступа самостоятельно или другому человеку.
* **Роли каталога Azure AD** расположенный в разделе «Управление» hello — hello панель мониторинга для назначения ролей toomanage привилегированной роли "Администраторы", изменить параметры активации роли, запуск проверки доступа и многое другое. Hello параметры на этой панели мониторинга будут отключены для тех, кто не является администратором привилегированной роли.

## <a name="next-steps"></a>Дальнейшие действия
Hello [Обзор Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md) включает дополнительные сведения об управлении административного доступа в вашей организации.

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
