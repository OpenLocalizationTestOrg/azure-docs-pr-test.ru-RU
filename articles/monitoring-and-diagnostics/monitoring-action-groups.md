---
title: "aaaCreate и управление группами действий в hello портал Azure | Документы Microsoft"
description: "Узнайте, как toocreate групп действий в hello портал Azure и управление ими."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: ancav
ms.openlocfilehash: 97e0b22bea7787fff6856f895a7e6256c177efd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-action-groups-in-hello-azure-portal"></a>Создание и управление группами действий в hello портал Azure
## <a name="overview"></a>Обзор ##
В этой статье показано, как toocreate групп действий в hello портал Azure и управление ими.

Группы действий дают возможность настроить список действий. Затем эти группы можно использовать при определении оповещений журнала действий. Эти группы можно повторно использовать предупреждения журнала каждого действия, определяют, обеспечивая этой же действия выполняются каждый раз, когда оповещения hello активности журнала приветствия.

Группа действий можно создать до too10 каждого типа действия. Каждое действие состоит из hello следующие свойства:

* **Имя**: Уникальный идентификатор в пределах группы действие hello.  
* **Тип действия:** отправка SMS, электронного сообщения или вызов веб-перехватчика.  
* **Сведения о**: hello соответствующий номер телефона, адрес электронной почты или веб-перехватчика URI.

Сведения о том, как группы действий tooconfigure шаблоны Azure Resource Manager toouse, в разделе [шаблоны диспетчера ресурсов группы действий](monitoring-create-action-group-with-resource-manager-template.md).

## <a name="create-an-action-group-by-using-hello-azure-portal"></a>Создать группу действий с помощью портала Azure hello ##
1. В hello [портала](https://portal.azure.com)выберите **монитора**. Hello **монитор** колонке объединяет все мониторинга параметров и данных в одном представлении.

    ![Hello «Монитор» службы](./media/monitoring-action-groups/home-monitor.png)
2. В hello **журнал действий** выберите **группы действий**.

    ![Вкладка «Группы действий» Hello](./media/monitoring-action-groups/action-groups-blade.png)
3. Выберите **добавить действие группу**и заполните поля hello.

    ![Здравствуйте, команда «Добавить группу действий»](./media/monitoring-action-groups/add-action-group.png)
4. Введите имя в hello **имя группы действий** поле и введите имя в hello **короткое имя** поле. Краткое имя Hello используется вместо действие полное имя группы, при отправке уведомлений с использованием этой группы.

      ![диалоговое окно Добавление действие Hello группы»](./media/monitoring-action-groups/action-group-define.png)

5. Hello **подписки** поле autofills с вашей текущей подписки. Эта подписка hello один находится в какой группе действие hello сохраняется.

6. Выберите hello **группы ресурсов** в действие, которое hello сохранить группу.

7. Определите список действий, указав для каждого из них следующие данные:

    а. **Имя.** Введите уникальный идентификатор для этого действия.

    b. **Тип действия.** Выберите SMS, электронную почту или веб-перехватчик.

    c. **Сведения о**: в зависимости от типа действия hello, введите номер телефона, адрес электронной почты или веб-перехватчика URI.

8. Выберите **ОК** группа действий toocreate hello.

## <a name="manage-your-action-groups"></a>Управление группами действий ##
После создания группу действий, он отображается в hello **группы действий** раздел hello **монитор** колонку. Выберите группу действие hello нужные toomanage для:

* добавлять, изменять или удалять действия;
* Удалите группу действие hello.

## <a name="next-steps"></a>Дальнейшие действия ##
* Дополнительные сведения о поведении SMS-оповещений в группе действий см. в [этой статье](monitoring-sms-alert-behavior.md).  
* Получить [понимания схемы предупреждения веб-перехватчика журнала действие hello](monitoring-activity-log-alerts-webhook.md).  
* Дополнительные сведения о лимитах для оповещений см. в статье [Ограничение частоты отправки для SMS, сообщений электронной почты и вызовов Webhook](monitoring-alerts-rate-limiting.md). 
* Получить [Обзор оповещения журнала действий](monitoring-overview-alerts.md)и узнайте, как tooreceive предупреждения.  
* Узнайте, каким образом слишком[настроить оповещения при изменении отправленных уведомление о работоспособности службы](monitoring-activity-log-alerts-on-service-notifications.md).
