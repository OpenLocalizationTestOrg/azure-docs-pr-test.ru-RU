---
title: "Azure AD Privileged Identity Management aaaConfigure | Документы Microsoft"
description: "На раздел, где объясняется, что такое Azure AD Privileged Identity Management и как toouse PIM tooimprove безопасность в облаке."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: c548ed2e-06e3-4eaf-a63d-0f02ee72da25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: dbe49fe4a0f6e5b46ed5a17fc7e8dcdacafe3846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-ad-privileged-identity-management"></a>Что такое Azure AD Privileged Identity Management?
С помощью управления привилегированными пользователями в Azure Active Directory (AD) можно администрировать, контролировать и отслеживать доступ в пределах организации, Сюда входят tooresources доступа в Azure AD и других электронных услуг Microsoft, такие как Office 365 или Microsoft Intune.  

> [!NOTE]
> Служба управления привилегированными пользователями при доступных tooyour всей организации лицензии администраторов с выпуска Premium P2 hello Azure Active Directory. Дополнительные сведения см. в разделе [Выпуски Azure Active Directory](active-directory-editions.md).

Организации требуется toominimize hello число пользователей, имеющих доступ к сведениям toosecure или ресурсы, так как, уменьшает вероятность hello злоумышленникам получение доступа. Тем не менее пользователи по-прежнему должны toocarry привилегированных операций в Azure, Office 365 или SaaS-приложений. Организации предоставляют пользователям привилегированный доступ в Azure AD, не отслеживая, как именно пользователи используют свои права администратора. Azure AD Privileged Identity Management помогает tooresolve этот риск.  

Управление привилегированными пользователями Azure AD помогает:  

* видеть, какие пользователи являются администраторами Azure AD;
* Включить по запросу «по требованию» tooMicrosoft административный доступ веб-служб, таких как Office 365 и Intune
* получать отчеты по данным журнала доступа администраторов и изменениям в назначениях администраторов;
* Получать оповещения о доступа tooa привилегированной роли
* Требовать утверждения tooactivate (Предварительная версия)

Azure AD Privileged Identity Management можно управлять организации роли hello встроенных Azure AD, включая (но не ограничиваясь ими):  

* глобального администратора;
* администратора выставления счетов; 
* администратора служб;  
* администратора пользователей;
* администратора паролей.

## <a name="just-in-time-administrator-access"></a>Своевременный доступ к правам администраторов
Исторически можно назначить роль администратора tooan пользователя через hello классический портал Azure или Windows PowerShell. В результате, пользователь становится **постоянного администрирования**, всегда активен в hello назначен роли. Azure AD Privileged Identity Management введена концепция hello объекта **право администрирования**. Временные администраторы — это пользователи, которым привилегированный доступ требуется время от времени, а не каждый день. роль Hello неактивна, пока hello нужны пользователю, то для завершения процесса активации и стать администратором active для заданного периода времени.

## <a name="enable-privileged-identity-management-for-your-directory"></a>Включение управления привилегированными пользователями для каталога
Можно запустить с помощью Azure AD Privileged Identity Management в hello [портал Azure](https://portal.azure.com/).

> [!NOTE]
> Должно быть глобальным администратором с учетной записью организации (например, @yourdomain.com), не является учетной записью Майкрософт (например, @outlook.com), tooenable Azure AD Privileged Identity Management для каталога.

1. Войдите в toohello [портал Azure](https://portal.azure.com/) роли глобального администратора каталога.
2. Если ваша организация имеет несколько каталогов, выберите свое имя пользователя в верхнем правом углу hello hello портал Azure. Выберите каталог hello, где будет использовать Azure AD Privileged Identity Management.
3. Выберите **дополнительные службы** и использовать hello toosearch текстовое поле фильтра для **Azure AD Privileged Identity Management**.
4. Проверьте **toodashboard ПИН-код** и нажмите кнопку **создать**. Открывает Hello управления привилегированными пользователями приложения.

Если вы hello первого лица toouse Azure AD Privileged Identity Management в вашем каталоге, затем hello [мастер защиты](active-directory-privileged-identity-management-security-wizard.md) поможет выполнить качества начального приветствия. После этого автоматически становится hello сначала **администратор безопасности** и **привилегированной роли администратора** hello каталога.

Управлять правами доступа других администраторов может только администратор привилегированных ролей. Вы можете [присвойте toomanage возможность hello других пользователей в PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

## <a name="privileged-identity-management-admin-dashboard"></a>Панель мониторинга управления привилегированными пользователями
Диспетчер привилегированных удостоверений Azure AD предоставляет панель мониторинга администратора, на которой отображается такая важная информация, как:

* Предупреждения, иллюстрирующие возможности tooimprove безопасности
* Hello число пользователей, назначенных tooeach привилегированной роли  
* Hello количество подходящих и постоянных администраторов
* граф активации привилегированных ролей в каталоге.

![Снимок экрана: панель мониторинга управления привилегированными пользователями (PIM)][2]

## <a name="privileged-role-management"></a>Управление привилегированными ролями
Azure AD Privileged Identity Management вы можете управлять hello администраторов, добавив или удалив роли tooeach администраторов постоянными или соответствующими условиям.

![Снимок экрана: добавление и удаление администраторов PIM][3]

## <a name="configure-hello-role-activation-settings"></a>Настроить параметры активации роли hello
С помощью hello [параметры роли](active-directory-privileged-identity-management-how-to-change-default-settings.md) можно настроить свойства активации подходящие роли hello в том числе:

* Длительность периода активации роли hello Hello
* уведомление об активации роли Hello
* Hello сведения пользователь должен tooprovide во время активации роли hello
* Запрос на обслуживание или номер инцидента
* [Требования для рабочего процесса утверждения — предварительная версия](./privileged-identity-management/azure-ad-pim-approval-workflow.md)

![Снимок экрана: параметры PIM — активация администратора][4]

Обратите внимание, что в образе hello hello кнопок для **многофакторной проверки подлинности** отключены. Для некоторых ролей с высоким уровнем привилегий требуется использование MFA для дополнительной защиты.

## <a name="role-activation"></a>Активация роли
слишком[активировать роль](active-directory-privileged-identity-management-how-to-activate-role.md), соответствующих администратор запрашивает ограничением по времени «активация» для роли hello. Hello активации можно запросить с помощью hello **активация my роли** параметр в Azure AD Privileged Identity Management.

Администратор хочет tooactivate роль должна tooinitialize Azure AD Privileged Identity Management в hello портал Azure.

Активацию роли можно настраивать. В параметрах PIM hello можно определить длину hello активации hello и какие сведения Здравствуйте, администратор должен tooprovide tooactivate hello роли.

![Снимок экрана: запрос администратора — активация роли][5]

## <a name="review-role-activity"></a>Действие проверки роли
Существует два способа tootrack как сотрудники и Администраторы используют привилегированных ролей. используя первый параметр Hello [журнал аудита ролей каталога](active-directory-privileged-identity-management-how-to-use-audit-log.md). журнал аудита Hello регистрирует отслеживать изменения в назначения привилегированных ролей и журнал активации роли.

![Снимок экрана: журнал активации PIM][6]

Hello второй параметр — tooset копирование regular [проверки доступа к](active-directory-privileged-identity-management-how-to-start-security-review.md). Эти проверки доступа может быть выполненных и назначенный редактор (например, руководитель группы) или hello сотрудников можно просмотреть сами. Это hello лучшим способом toomonitor, по-прежнему требуется доступ и кто больше не происходит.

## <a name="azure-ad-pim-at-subscription-expiration"></a>Azure AD PIM по истечении срока действия подписки
Предыдущий tooreaching общие доступность Azure AD PIM, которая была в режиме предварительного просмотра, а также было лицензия не проверяет наличие toopreview клиента Azure AD PIM.  Теперь, при достижении общей доступности Azure AD PIM лицензии пробной или платной должны быть назначены администраторами toohello toocontinue клиента hello использованию PIM.  Если ваша организация не приобрели Azure AD Premium P2 или истекает срок действия пробной версии, практически все возможности Azure AD PIM hello больше не доступны в клиенте.  Можно прочитать подробнее в hello [требований к подписке Azure AD PIM](./privileged-identity-management/subscription-requirements.md)

## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-configure/PIM_Admin_Overview.png
[3]: ./media/active-directory-privileged-identity-management-configure/PIM_AddRemove.png
[4]: ./media/active-directory-privileged-identity-management-configure/PIM_Settings_w_Approval_Disabled.png
[5]: ./media/active-directory-privileged-identity-management-configure/PIM_RequestActivation.png
[6]: ./media/active-directory-privileged-identity-management-configure/PIM_ActivationHistory.png
