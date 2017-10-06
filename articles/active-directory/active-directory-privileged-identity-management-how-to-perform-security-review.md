---
title: "aaaHow tooperform доступе | Документы Microsoft"
description: "Узнайте, как tooperform отзыв с hello Azure управления привилегированными пользователями приложения."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
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
ms.openlocfilehash: 301a5e9f97b68fedfbf4954e0bd7dadb7f0fc510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-an-access-review-in-azure-ad-privileged-identity-management"></a>Как tooperform доступа просмотрите в Azure AD Privileged Identity Management
Active Directory (AD) Управление привилегированными пользователями Azure упрощает, как управлять предприятий tooresources привилегированный доступ в Azure AD и других электронных услуг Microsoft, такие как Office 365 или Microsoft Intune.  

Если вам назначена роль администратора tooan, привилегированной роли Администратор организации может попросить вас tooregularly подтверждение по-прежнему требуется этой роли для данного задания. Может появиться сообщение электронной почты, содержащее ссылку или переходе прямой toohello [портал Azure](https://portal.azure.com). Выполните действия hello в этой статье tooperform, самостоятельно просмотрите назначенных ролей.

Если вы являетесь администратором привилегированной роли интересует проверки доступа, получить более подробные сведения в [как toostart доступа просмотрите](active-directory-privileged-identity-management-how-to-start-security-review.md).

## <a name="add-hello-privileged-identity-management-application"></a>Добавить приложение hello Privileged Identity Management
Можно использовать приложение hello Azure AD Privileged Identity управления (PIM) в hello [портал Azure](https://portal.azure.com/) tooperform проверки.  При отсутствии приложения hello Azure AD Privileged Identity Management на портале, выполните эти действия, tooget работы.

1. Войдите в toohello [портал Azure](https://portal.azure.com/).
2. Выберите свое имя пользователя в верхнем правом углу hello hello портал Azure и выберите hello каталог, где можно будет работать.
3. Выберите **дополнительные службы** и использовать hello toosearch текстовое поле фильтра для **Azure AD Privileged Identity Management**.
4. Проверьте **toodashboard ПИН-код** и нажмите кнопку **создать**. Откроется Hello управления привилегированными пользователями приложения.

## <a name="approve-or-deny-access"></a>Утверждение или отклонение доступа
При утверждении или запретить доступ, вы просто сообщают, что редактор hello ли вы по-прежнему использовать роль или нет. Выберите **утвердить** Если toostay в роли hello или **Deny** Если вы не должны hello доступ больше. Состояние не изменит прямо сейчас, пока редактор hello применяются hello результаты.
Выполните эти шаги toofind, выполните проверку доступа hello.

1. В hello PIM приложения, выберите **проверки привилегированный доступ**. При наличии любой проверки ожидающих доступ, они отображаются в hello колонке проверок доступа Azure AD.
2. Выберите, требуется toocomplete проверки hello.
3. Если не был создан проверки hello, вы отображаются так, как только пользователь при проверке hello hello. Выберите имя следующего tooyour hello флажок.
4. Выберите **Утвердить** или **Запретить**. Может потребоваться tooinclude причина такого решения в hello **указать причину** текстовое поле.  
5. Закрыть hello **роли проверки Azure AD** колонку.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
