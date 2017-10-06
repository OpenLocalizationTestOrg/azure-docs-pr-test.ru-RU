---
title: "журнал аудита aaaHow toouse hello в Azure AD Privileged Identity Management | Документы Microsoft"
description: "Узнайте, как toouse hello аудита входа в расширении управления привилегированными пользователями Azure hello."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 5d13a6dd-1fcb-4e76-82fb-cb2f4f0e4357
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 36987eaab9fe02c5dd7b4f4705e487299430745d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-audit-log-in-pim"></a>Использование журнала аудита hello в PIM
Можно использовать toosee журнала аудита управления привилегированных удостоверений (PIM) hello всех назначений пользователя hello и активаций в течение заданного периода времени. Если требуется toosee hello аудита полного журнала действий в клиенте, включая администратора, пользователь и действий по синхронизации, можно использовать hello [отчеты о доступе и использовании Azure Active Directory.](active-directory-view-access-usage-reports.md)

## <a name="navigate-toohello-audit-log"></a>Перейдите в журнал аудита toohello
Из hello [портал Azure](https://portal.azure.com) панели мониторинга, выберите hello **Azure AD Privileged Identity Management** приложения. После этого доступ к журналу аудита hello, щелкнув **управление привилегированных ролей** > **журнал аудита** в панели мониторинга PIM hello.

## <a name="hello-audit-log-graph"></a>График журнала аудита Hello
Можно использовать hello аудита журнала tooview hello общее количество активаций, max активаций в день и среднее количество активаций в день в виде графика.  Можно также фильтровать данные hello по ролям при наличии более чем одной роли в журнал аудита hello.

Используйте hello **время**, **действия**, и **роли** журнала hello toosort кнопки.

## <a name="hello-audit-log-list"></a>Список журналов аудита Hello
содержит столбцы Hello hello список журналов аудита.

* **Запрашивающая сторона** -hello пользователя, запросившего активации роли hello или изменение.  Если значение hello «Azure система», проверьте журнал аудита Azure hello Дополнительные сведения.
* **Пользователь** -hello пользователя выполняется активация или tooa роль.
* **Роль** -hello роли назначения или активизации пользователем hello.
* **Действие** - hello действия, производимые hello запрашивающей стороны. Они могут включать назначение, отмену назначения, активацию или отмену активации.
* **Время** — Если выполнялось действие hello.
* **Рассуждения** -Если текст был введен в поле Причина hello во время активации, он будет отображаться здесь.
* **Срок действия** — применимо только для активации ролей.

## <a name="filter-hello-audit-log"></a>Настройте фильтрацию журнала аудита hello
Можно фильтровать информацию hello, который отображается в журнал аудита hello, щелкнув hello **фильтра** кнопки.  Hello **колонку параметров диаграммы обновления** будут отображаться.

После выбора hello фильтры, нажмите кнопку **обновление** toofilter hello данных журнала hello.  Если данные hello не отображаются прямо сейчас, обновите страницу приветствия.

### <a name="change-hello-date-range"></a>Изменить диапазон дат hello
Используйте hello **сегодня**, **прошлой неделе**, **прошлый месяц**, или **настраиваемый** кнопки toochange hello временной диапазон журнала аудита hello.

При выборе hello **настраиваемый** кнопки, вам будет предоставлена **из** поля «Дата» и **для** Дата поле toospecify диапазон дат для журнала hello.  Можно вводить даты hello в формате мм/дд/гггг или щелкнуть hello **календаря** значок и выберите hello дату из календаря.

### <a name="change-hello-roles-included-in-hello-log"></a>Изменить роли hello, включенные в журнал hello
Установите или снимите hello **роли** журнала флажок Далее tooeach роли tooinclude или исключить его из hello.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

