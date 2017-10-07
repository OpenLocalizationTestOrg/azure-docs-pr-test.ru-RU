---
title: "aaaCreate функции первого из hello портал Azure | Документы Microsoft"
description: "Узнайте, как первый Azure функции для выполнения без сервера с помощью toocreate hello портал Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 96cf87b9-8db6-41a8-863a-abb828e3d06d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/07/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 84283d7d4bc6015061946af4589f9a70ae61f36b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-in-hello-azure-portal"></a>Создание первой функции в hello портал Azure

Функции Azure позволяет выполнять код в среде без сервера без необходимости toofirst создания виртуальной Машины или публикации веб-приложения. В этом разделе рассказано, как toouse функционирует toocreate функции «hello world» в hello портал Azure.

![Создание функции приложения в hello портал Azure](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-tooazure"></a>Войдите в tooAzure

Войдите в toohello [портал Azure](https://portal.azure.com/).

## <a name="create-a-function-app"></a>Создание приложения-функции

Требуется выполнение функции приложения toohost hello функций. позволяющее группировать функции в логические единицы и упростить развертывание и совместное использование ресурсов, а также управление ими. 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

Создайте функцию в приложение новые функции hello.

## <a name="create-function"></a>Создание функции, активируемой HTTP

1. Разверните приложение новые функции, а затем щелкните hello  **+**  рядом слишком**функции**.

2.  В hello **быстро приступить к работе** выберите **веб-перехватчика + API**, **выбрать язык** функции, а затем щелкните **создания этой функции** . 
   
    ![Примеры использования функций в hello портал Azure.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

Функция создается в выбранный язык с помощью шаблона hello для функции активации HTTP. Можно запустить новые функции hello, отправив запрос HTTP.

## <a name="test-hello-function"></a>Проверка функции hello

1. В новой функции щелкните **</> Получить URL-адрес функции**, выберите **По умолчанию (ключ функции)**и нажмите кнопку **Копировать**. 

    ![Скопируйте URL-адрес функции hello из hello портал Azure](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. Вставьте URL-адрес функции hello в адресной строке браузера. Добавить строку hello запроса `&name=<yourname>` toothis hello URL-адрес и нажмите клавишу `Enter` ключа запроса hello tooexecute клавиатуры. Hello ниже приведен пример hello ответ, возвращаемый функцией "hello" в браузере Edge hello:

    ![Функция ответа в браузер hello.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    URL-адрес содержит ключ, который требуется, по умолчанию tooaccess запрос Hello работу по протоколу HTTP.   

3. При выполнении функции сведения трассировки записываются журналы toohello. выходные данные трассировки hello toosee из предыдущего выполнения hello, вернитесь tooyour функции hello портала и нажмите кнопку hello стрелкой hello нижней части экрана tooexpand hello **журналы**. 

   ![Функции просмотра журнала в hello портал Azure.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a>Очистка ресурсов

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Дальнейшие действия

Вы создали приложение-функцию с простой функцией, активируемой HTTP.  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Дополнительные сведения см. в статье [Привязки HTTP и webhook в функциях Azure](functions-bindings-http-webhook.md).



