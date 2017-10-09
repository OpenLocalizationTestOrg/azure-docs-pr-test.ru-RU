---
title: "рабочие процессы утверждения управления привилегированных удостоверений aaaAzure | Документы Microsoft"
description: "Узнайте о рабочих процессах утверждения при управлении привилегированными пользователями (PIM)."
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: 4afaf5c138798a803eb3d3b7905b9361d65792cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="approvals-preview"></a>Утверждения (предварительная версия)

## <a name="overview"></a>Обзор

С утверждениями для управления привилегированными пользователями можно настроить утверждения ролей toorequire для активации и как делегированного утверждающих, выберите один или несколько пользователей или групп. Продолжить чтение toolearn как tooconfigure ролей и выбрать утверждающих.

>[!NOTE]
Необходимо учитывать, что эта функция еще находится в разработке, поэтому в ней могут возникать ошибки. Hello функциональные возможности, включая текст соглашения об именовании могут быть изменены и не должен рассматриваться окончательного.


## <a name="key-terminology"></a>Ключевые термины

*Право пользователя роли* — подходящие роли пользователя — это пользователь в вашей организации, которой была предоставлена роль tooan Azure AD в качестве соответствующих (роль требует активации).

*Делегированное утверждающее лицо* — это один или несколько индивидуальных пользователей или групп в Azure AD, которые отвечают за утверждение запросов на активацию ролей.

## <a name="scenarios"></a>Сценарии

Hello личной предварительной версии поддерживает hello следующие сценарии:

**В качестве администратора привилегированных ролей вы можете выполнить следующие действия:**

-   [включить утверждения для конкретных ролей](#enable-approval-for-specific-roles);

-   [Укажите утверждающего запросов tooapprove пользователей или групп](#specify-approver-users-and/or-groups-to-approve-requests)

-   [просмотреть историю запросов и утверждений для всех привилегированных ролей](#view-request-and-approval-history-for-all-privileged-roles).

**В качестве назначенного утверждающего лица вы можете выполнить следующие действия:**

-   [просмотреть запросы, ожидающие утверждения](#view-pending-approvals-requests);

-   [утвердить или отклонить запросы на повышение роли (по одному и (или) массово)](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk);

-   [указать обоснование для своего утверждения или отказа](#provide-justification-for-my-approval/rejection). 

**В качестве пользователя с временной ролью вы можете выполнить следующие действия:**

-   [запросить активацию роли, для которой требуется утверждение](#request-activation-of-a-role-that-requires-approval);

-   [Просмотр состояния hello tooactivate вашего запроса](#view-the-status-of-your-request-to-activate)

-   [выполнить задачу в Azure AD, если запрос на активацию утвержден](#complete-your-task-in-azure-ad-if-activation-was-approved).

### <a name="navigation"></a>Навигации

Мы обновили hello навигации toosupport утверждений

![](media/azure-ad-pim-approval-workflow/image001.png)

Целевая страница по умолчанию Hello предоставляет удобный доступ tooinformation о PIM и hello новой документации утверждения.

![](media/azure-ad-pim-approval-workflow/image002.png)

Мы также добавили новый раздел для всех пользователей PIM — "My Audit History" (Мой журнал аудита). Здесь вы можете найти все удостоверения tooyour соответствующие сведения hello. Это включает все ожидающие и завершенных запросов, любые решения, которые вы внесли о hello запросов, которые можно устранить и все последние роли активаций в одном месте.

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a>Включение утверждений для конкретных ролей

tooenable утверждения для определенной роли, сначала выберите роли каталога hello левой панели навигации.

![](media/azure-ad-pim-approval-workflow/image004.png)

Найти и выбрать параметры в левой области навигации роли каталога hello

![](media/azure-ad-pim-approval-workflow/image006.png)

Выберите привилегированные роли:

![](media/azure-ad-pim-approval-workflow/image009.png)

Выберите «Включить» в hello требуют утверждения раздела:

![](media/azure-ad-pim-approval-workflow/image011.png)

После включения hello колонке будет расширяться hello tooshow приведенные ниже сведения:

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
Если не указать любой утверждающих, hello PRA(s) становятся утверждающие лица по умолчанию hello. PRA(s) бы необходимые tooapprove запрашивает все активации для этой роли.

### <a name="specify-approver-users-andor-groups-tooapprove-requests"></a>Укажите утверждающего запросов tooapprove пользователей или групп

Утверждение toodelegate вариант hello слишком «выберите утверждающих»:

![](media/azure-ad-pim-approval-workflow/image015.png)

При загрузке колонке выберите утверждающих hello может найти конкретного пользователя или группы с помощью панели поиска hello в верхней hello, или при выборе из списка предварительно заполненных hello, затем нажмите кнопку «Выбрать» после завершения:

![](media/azure-ad-pim-approval-workflow/image017.png)

Примечание. За один раз можно выбрать несколько пользователей или групп.

Ваш выбор будет отображаться в списке hello выбранного утверждающих, как показано ниже:

![](media/azure-ad-pim-approval-workflow/image019.png)

tooremove утверждающего, просто щелкните имя следующего tootheir hello удаление кнопки.

Дополнительные утверждающие tooadd, процесс повторения hello.

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a>Просмотр истории запросов и утверждений для всех привилегированных ролей

Журнал tooview запроса и утверждения для всех привилегированных ролей, выберите журнал аудита hello панели мониторинга:

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
Можно сортировать данные hello действием и найти «Утверждено активации»

### <a name="view-pending-approvals-requests"></a>Просмотр запросов, ожидающих утверждения

При наличии запроса, ожидающего вашего утверждения, вы, как делегированное утверждающее лицо, получите уведомление по электронной почте. tooview эти запросы на вкладке панели мониторинга (в новый переход hello) выберите hello «ожидающие утверждения запросы» в hello портала управления персональными данными hello слева панели навигации.

![](media/azure-ad-pim-approval-workflow/image023.png)

Отобразится список запросов, ожидающих утверждения:

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a>Утверждение или отклонение запросов на повышение роли (по одному и (или) массово)

Выберите запросы hello обратиться tooapprove или запретить и нажмите кнопку "hello" в области действия, соответствующего решения:

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a>Указание обоснования для своего утверждения или отказа

Это будет открыть новый tooapprove колонке или запретить несколько запросов одновременно. Введите обоснование для такого решения и нажмите кнопку Утвердить (или запретить) в нижней hello или колонке hello:

![](media/azure-ad-pim-approval-workflow/image029.png)

По завершении процесса запроса hello символе состояния hello будут отражать принятое (в этом примере hello решение является утверждение):

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a>Запрос активации роли, для которой требуется утверждение

Запрос активации роли, которая требует утверждения могут инициироваться из старого PIM навигации hello или hello новый переход, как процесс hello остается активации роли hello таким же. Просто выберите роль из списка hello ролей для активации:

![](media/azure-ad-pim-approval-workflow/image033.png)

Если для привилегированной роли требуется выполнение Многофакторной идентификации, то сначала отобразится соответствующий запрос:

![](media/azure-ad-pim-approval-workflow/image035.png)

По завершении щелкните "Активировать" и укажите обоснование (при необходимости):

![](media/azure-ad-pim-approval-workflow/image037.png)

Запрашивающая сторона Hello будет выведено уведомление, которое hello запрос ожидает утверждения:

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-hello-status-of-your-request-tooactivate"></a>Просмотр состояния hello tooactivate вашего запроса

Просмотр состояния hello tooactivate ожидающий запрос должен осуществляться новой панели навигации. Hello левой панели навигации выберите вкладку «Мои запросы» hello.

![](media/azure-ad-pim-approval-workflow/image041.png)

состояние запроса Hello слишком по умолчанию «Ожидание», но можно переключить toosee все или отклоненных запросов.

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a>Выполнение задачи в Azure AD, если запрос на активацию утвержден

После утверждения запроса hello hello роли является активным и может продолжить работу, которую требуется эта роль.

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a>Дальнейшие действия

Ваш отзыв будет полезен toous. Вы можете бесплатно tooshare комментарии или отзывы с нами здесь!
