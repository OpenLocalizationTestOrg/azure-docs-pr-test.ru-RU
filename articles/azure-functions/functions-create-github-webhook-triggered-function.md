---
title: "функция в Azure, активируемых веб-перехватчика GitHub aaaCreate | Документы Microsoft"
description: "Используйте функции Azure toocreate без сервера функция, вызываемая веб-перехватчика GitHub."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 36ef34b8-3729-4940-86d2-cb8e176fcc06
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 8ffcde82c9310d749159ed53eab113658e38a030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-a-github-webhook"></a>Создание функции, активируемой объектом webhook GitHub

Узнайте, как toocreate функцию, которая инициируется с полезными данными GitHub конкретного веб-перехватчика HTTP-запроса.

![Веб-перехватчика Github активации функции hello портал Azure](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Предварительные требования

+ Учетная запись GitHub с хотя бы одним проектом.
+ Подписка Azure. Если у вас еще нет подписки Azure, создайте [бесплатную учетную запись](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начать работу.

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Создание приложения-функции Azure

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Приложение-функция успешно создана.](./media/functions-create-first-azure-function/function-app-create-success.png)

Создайте функцию в приложение новые функции hello.

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a>Создание функции, активируемой объектом webhook GitHub

1. Разверните приложения функции и щелкните hello  **+**  рядом слишком**функции**. Если это первая функция hello в приложении функции, выберите **пользовательские функции**. Откроется hello полный набор шаблонов функций.

    ![Страница быстрого запуска функции в hello портал Azure](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. Выберите hello **GitHub веб-перехватчика** шаблона для нужный язык. **Присвойте функции имя** и щелкните **Создать**.

     ![Создайте функцию запуска веб-перехватчика GitHub в hello портал Azure](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

3. В новые функции, щелкните **URL-адрес функции <> / Get**, затем скопируйте и сохраните значения hello. Здравствуйте, такие же действия **<> / GitHub получить секрет**. Используйте эти веб-перехватчика значения tooconfigure hello в GitHub.

    ![Просмотрите код функции hello](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

Затем создайте объект webhook в репозитории GitHub.

## <a name="configure-hello-webhook"></a>Настройка веб-перехватчика hello

1. На портале GitHub перейдите tooa репозитория, вы являетесь владельцем. Вы можете использовать любые репозитории, для которых создали ответвления. Toofork репозиторий используйте <https://github.com/Azure-Samples/functions-quickstart>.

1. Щелкните **Параметры**, **Веб-перехватчики**, а затем — **Добавить веб-перехватчик**.

    ![Добавление объекта webhook GitHub](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. Использовать параметры, как указано в таблице hello, а затем нажмите кнопку **добавить веб-перехватчика**.

    ![Задать URL-адрес веб-перехватчика hello и секрет](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| Настройка | Рекомендуемое значение | Описание |
|---|---|---|
| **Payload URL** (URL-адрес полезных данных) | Скопированное значение | Используйте значение hello, возвращенное **URL-адрес функции <> / Get**. |
| **Секрет**   | Скопированное значение | Используйте значение hello, возвращенное **<> / GitHub получить секрет**. |
| **Тип содержимого** | приложение/json | функция Hello ожидает полезные данные JSON. |
| Триггеры событий | Let me select individual events (Я выбираю отдельные события) | Нам нужен только tootrigger на проблему комментирования событий.  |
| | Issue comment (Примечание к вопросу) |  |

Теперь hello веб-перехватчика имеет настроенный tootrigger функции при добавлении нового комментария проблему.

## <a name="test-hello-function"></a>Проверка функции hello

1. В репозитории GitHub откройте hello **проблемы** вкладку в новом окне браузера.

1. В новом окне приветствия щелкните **новая проблема**, введите заголовок и нажмите кнопку **отправить новый выпуск**.

1. В выпуске hello, введите комментарий и нажмите кнопку **комментарий**.

    ![Добавление примечания к вопросу GitHub](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. Вернитесь к предыдущему окну toohello портал и просмотрите журналы hello. Должна появиться запись трассировки hello новым текстом комментария.

     ![Просмотр текста hello комментария в журналах hello.](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a>Очистка ресурсов

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Дальнейшие действия

Вы создали функцию, которая выполняется при получении запроса объекта webhook GitHub.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Дополнительные сведения см. в статье [Привязки HTTP и веб-перехватчика в функциях Azure](functions-bindings-http-webhook.md).
