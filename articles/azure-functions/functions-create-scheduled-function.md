---
title: "функция, которая выполняется по расписанию в Azure aaaCreate | Документы Microsoft"
description: "Узнайте, как toocreate функции в Azure, которая выполняется на основе определяемому вами расписанию."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: ba50ee47-58e0-4972-b67b-828f2dc48701
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 793b06a65a154466dfd4c121bcc88082227cd597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a>Создание в Azure функции, активируемой по таймеру

Узнайте, как toocreate функции Azure toouse функцию, которая выполняется на основе определяемому вами расписанию.

![Создание функции приложения в hello портал Azure](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Предварительные требования

toocomplete этого учебника:

+ Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Создание приложения-функции Azure

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Приложение-функция успешно создана.](./media/functions-create-first-azure-function/function-app-create-success.png)

Создайте функцию в приложение новые функции hello.

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a>Создание функции, активируемой по таймеру

1. Разверните приложения функции и щелкните hello  **+**  рядом слишком**функции**. Если это первая функция hello в приложении функции, выберите **пользовательские функции**. Откроется hello полный набор шаблонов функций.

    ![Страница быстрого запуска функции в hello портал Azure](./media/functions-create-scheduled-function/add-first-function.png)

2. Выберите hello **TimerTrigger** шаблона для нужный язык. Затем используйте hello параметры, как указано в таблице hello:

    ![Создайте функцию таймер запускается в hello портал Azure.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | Настройка | Рекомендуемое значение | Описание |
    |---|---|---|
    | **Имя функции** | TimerTriggerCSharp1 | Определяет имя hello этой функции запуска таймера. |
    | **[Расписание](http://en.wikipedia.org/wiki/Cron#CRON_expression)** | 0 \*/1 \* \* \* \* | Шесть полей [выражение CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) , планирует вашей toorun функция каждую минуту. |

2. Щелкните **Создать**. Будет создана функция на выбранном вами языке, которая будет выполняться каждую минуту.

3. Проверьте выполнение, просмотр сведений трассировки записываются журналы toohello.

    ![Функции просмотра журнала в hello портал Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

Теперь можно изменить расписание функции hello, чтобы он запускался реже, например один раз в час. 

## <a name="update-hello-timer-schedule"></a>Обновить расписание таймера hello

1. Разверните вашу функцию и щелкните **Интеграция**. Это где определение входных данных и вывода привязки функции, а также задать расписание hello. 

2. Введите в поле **Расписания** новое значение `0 0 */1 * * *`, а затем щелкните **Сохранить**.  

![Функции Обновить расписание таймера в hello портал Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

Теперь функция будет выполняться раз в час. 

## <a name="clean-up-resources"></a>Очистка ресурсов

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Дальнейшие действия

Вы создали функцию, которая выполняется на основе расписания.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Дополнительные сведения о триггерах см.в статье [Настройка триггеров для выполнения кода с помощью Функций Azure](functions-bindings-timer.md).