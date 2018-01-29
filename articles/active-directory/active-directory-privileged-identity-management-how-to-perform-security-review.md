---
title: "Выполнение проверки доступа | Документация Майкрософт"
description: "Сведения о выполнении проверки с помощью приложения для управления привилегированными пользователями Azure."
services: active-directory
documentationcenter: 
author: billmath
manager: mtillman
editor: 
ms.assetid: 49ee2feb-7d2e-4acf-82c1-40ff23062862
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 8ca735f04334557f40ddbe3119f7110dbcdde2a8
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="how-to-perform-an-access-review-in-azure-ad-privileged-identity-management"></a>Как выполнить проверку доступа в управлении привилегированными пользователями Azure AD
Компонент Azure Active Directory (AD) Privileged Identity Management упрощает управление привилегированным доступом пользователей к ресурсам в Azure AD и других веб-службах Майкрософт, включая Office 365 и Microsoft Intune.  

Если вам назначена роль администратора, администратор привилегированных ролей вашей организации может попросить вас регулярно подтверждать, что эта роль по-прежнему требуется вам для работы. Вы можете получить сообщение электронной почты, содержащее ссылку для подтверждения, или перейти непосредственно на [портал Azure](https://portal.azure.com). Следуйте указаниям в этой статье, чтобы выполнить самостоятельную проверку назначенных вам ролей.

Если вы администратор привилегированных ролей и вас интересуют функции проверки доступа, дополнительные сведения см. в статье [Как запустить проверку доступа в управлении привилегированными пользователями Azure AD](active-directory-privileged-identity-management-how-to-start-security-review.md).

## <a name="add-the-privileged-identity-management-application"></a>Добавление приложения для управления привилегированными пользователями
Для выполнения проверки можно использовать приложение "Управление привилегированными пользователями" (PIM) Azure AD на [портале Azure](https://portal.azure.com/) .  Если приложение Azure AD PIM еще не установлено на портале, выполните следующие действия, чтобы приступить к работе.

1. Войдите на [портале Azure](https://portal.azure.com/).
2. Щелкните свое имя пользователя в правом верхнем углу портала Azure и выберите каталог, с которым будете работать.
3. Выберите **Другие службы** и в текстовое поле "Фильтр" введите **Azure AD Privileged Identity Management**.
4. Установите флажок **Закрепить на панели мониторинга** и нажмите кнопку **Создать**. Откроется приложение "Управление привилегированными пользователями".

## <a name="approve-or-deny-access"></a>Утверждение или отклонение доступа
При утверждении или отклонении доступа вы просто сообщаете проверяющему, используете ли вы еще эту роль. Чтобы оставаться в этой роли, выберите **Утвердить**, а когда доступ вам больше не требуется — **Запретить**. Состояние роли изменится лишь тогда, когда проверяющий применит результаты.
Выполните следующие действия, чтобы найти проверку доступа и завершить ее.

1. В приложении PIM выберите **Просмотр привилегированного доступа**. Если у вас есть незавершенные проверки доступа, то они отображаются в колонке "Проверки доступа" в Azure AD.
2. Выберите проверку, которую необходимо завершить.
3. Если эта проверка создана не вами, вы должны быть единственным пользователем, отображаемым при проверке. Установите флажок рядом со своим именем.
4. Выберите **Утвердить** или **Запретить**. Возможно, в текстовом поле **Указание причины** потребуется ввести причину своего решения.  
5. Закройте колонку **Проверка ролей Azure AD** .

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
