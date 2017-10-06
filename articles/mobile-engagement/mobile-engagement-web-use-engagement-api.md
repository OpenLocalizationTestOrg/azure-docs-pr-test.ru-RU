---
title: "aaaAzure веб-пакет SDK Mobile Engagement API | Документы Microsoft"
description: "Здравствуйте, последние обновления и процедуры для hello Web SDK для Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8a87d5ac-d8b7-4a0d-bdee-414dbcc561b2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: ec1261d6ad573b8c3ad6d5f616ab7bbe560d6fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-mobile-engagement-api-in-a-web-application"></a>Использовать hello Azure Mobile Engagement API веб-приложения
Этот документ является документом toohello сложения, информирующее о том, как слишком[интегрировать в веб-приложение Mobile Engagement](mobile-engagement-web-integrate-engagement.md). Он предоставляет подробные сведения о том, как toouse hello Azure Mobile Engagement API tooreport статистики вашего приложения.

Hello Mobile Engagement API обеспечивается hello `engagement.agent` объекта. по умолчанию, Azure Mobile Engagement Web SDK псевдоним: Hello `engagement`. Можно переопределить этот псевдоним из конфигурации пакета SDK для hello.

## <a name="mobile-engagement-concepts"></a>Основные понятия Служб мобильного взаимодействия
Hello следующие части уточнения общих [мобильного охвата понятия](mobile-engagement-concepts.md) для hello веб-платформы.

### <a name="session-and-activity"></a>`Session` и `Activity`
Если более чем на несколько секунд между двумя действиями пользователя hello кластер простаивает, hello последовательность действий пользователя разбивается на двух различных сеансах. Эти несколько секунд, называются hello тайм-аут сеанса.

Если веб-приложение не объявляет hello конец действия пользователя само по себе (путем вызова hello `engagement.agent.endActivity` функции), сервера мобильного охвата hello автоматически истекает hello сеанс пользователя в течение трех минут после закрытия страницы приложения hello. Это называется hello время ожидания сеанса сервера.

### `Crash`
Автоматические отчеты неперехваченных исключений JavaScript не создаются по умолчанию. Тем не менее, можно сообщить сбоев вручную с помощью hello `sendCrash` функцию (см. раздел hello в reporting сбоев).

## <a name="reporting-activities"></a>Создание отчетов о действиях
Отчеты о активности пользователей включает в себя при запуске нового действия и hello пользователь завершает текущее действие hello.

### <a name="user-starts-a-new-activity"></a>Пользователь запускает новое действие
    engagement.agent.startActivity("MyUserActivity");

Требуется toocall `startActivity()` каждого действий пользователя во время изменения. функции Hello первый вызов toothis начинает новый сеанс пользователя.

### <a name="user-ends-hello-current-activity"></a>Пользователь завершает текущее действие hello
    engagement.agent.endActivity();

Требуется toocall `endActivity()` по крайней мере один раз в том случае, когда пользователь hello завершается их последнее действие. Это позволяет сообщить hello Mobile Engagement Web SDK hello пользователя находится в режиме ожидания, которое, hello пользовательский сеанс должен toobe закрыто после истечения времени ожидания сеанса hello. При вызове метода `startActivity()` до истечения времени ожидания сеанса hello, просто возобновить сеанс hello.

Так как отсутствует надежный вызов для закрытия окна навигатора hello, часто бывает сложно или невозможно toocatch hello конец действия пользователя внутри веб-среды. Почему является hello мобильного охвата, сервер автоматически истекает hello сеанс пользователя в течение трех минут после закрытия страницы приложения hello.

## <a name="reporting-events"></a>Создание отчетов о событиях
Отчеты создаются о событиях сеанса и изолированных событиях.

### <a name="session-events"></a>События сеанса
События сеанса обычно являются используется tooreport hello действия, выполняемые пользователем во время сеанса пользователя hello.

**Пример без дополнительных данных:**

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

**Пример с дополнительными данными:**

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a>Изолированные события
В отличие от событий сеанса автономный события могут возникать за пределами hello контекст сеанса.

Для этого вместо метода ``engagement.agent.sendSessionEvent`` используется ``engagement.agent.sendEvent``.

## <a name="reporting-errors"></a>Создание отчетов об ошибках
Отчеты создаются об ошибках сеанса и изолированных ошибках.

### <a name="session-errors"></a>Ошибки сеанса
Сеанс ошибок обычно являются используется tooreport hello ошибок, которые оказывают влияние на hello пользователя во время сеанса пользователя hello.

**Пример без дополнительных данных:**

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

**Пример с дополнительными данными:**

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a>Изолированные ошибки
В отличие от ошибок сеансов могут возникать ошибки автономный вне контекста hello сеанса.

Для этого вместо метода `engagement.agent.sendSessionError` используется `engagement.agent.sendError`.

## <a name="reporting-jobs"></a>Создание отчетов о заданиях
Для заданий создаются отчеты об ошибках отчетов и о событиях, происходящих во время выполнения задания, а также сбои отчетов.

**Пример**

Если вы хотите toomonitor AJAX-запросом, следует использовать hello следующее:

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
      // [...]
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-errors-during-a-job"></a>Создание отчетов об ошибках при выполнении задания
Ошибки могут быть связанные tooa выполнения задания вместо toohello текущий сеанс пользователя.

**Пример**

Если требуется, чтобы tooreport ошибку, если запрос AJAX вызывает ошибку:

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
        // [...]
        if (xhr.status == 0 || xhr.status >= 400) {
          engagement.agent.sendJobError('publish_xhr', 'publish', {status: xhr.status, statusText: xhr.statusText});
        }
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-events-during-a-job"></a>Создание отчетов о событиях во время выполнения задания
События могут быть связанные tooa выполнения задания вместо toohello текущий сеанс пользователя благодаря использованию toohello `engagement.agent.sendJobEvent` функции.

Эта функция работает в точности как функция `engagement.agent.sendJobError`.

### <a name="reporting-crashes"></a>Создание отчетов о сбоях
Используйте hello `sendCrash` tooreport функция аварийно завершает работу вручную.

Hello `crashid` аргументом является строка, определяющая тип hello аварийного завершения.
Hello `crash` аргумент обычно является hello трассировка стека сбоя hello в виде строки.

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a>Дополнительные параметры
Можно присоединить событие tooan произвольные данные, ошибки, действия или задания.

Hello данных может быть любой объект JSON (но не массив или примитивного типа).

**Пример**

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a>Ограничения
Ограничения, применяемые параметры tooextra находятся в областях hello регулярных выражений для ключей, типы значений и размер.

#### <a name="keys"></a>ключей
Каждый ключ в hello объекта должно соответствовать hello следующее регулярное выражение:

    ^[a-zA-Z][a-zA-Z_0-9]*

Это означает, что ключ должен содержать не менее одной буквы, за которой следуют буквы, цифры или символы подчеркивания (\_).

#### <a name="values"></a>Значения
Значения: ограниченный toostring, номер и логических типов.

#### <a name="size"></a>Размер
Вспомогательные элементы, ограниченные too1, 024 символов на вызов (после hello Mobile Engagement Web SDK кодирует его в формате JSON).

## <a name="reporting-application-information"></a>Создание отчетов о данных приложения
Можно вручную сообщить отслеживания сведения (или другие сведения о приложении) с помощью hello `sendAppInfo()` функции.

Обратите внимание, что эти данные можно отправлять поэтапно. Hello только последнее значение для определенного раздела будут храниться для конкретного устройства.

Как дополнения событий можно использовать любые сведения приложения tooabstract объекта JSON. Обратите внимание, что массивы или вложенные объекты рассматриваются как неструктурированные строки (с использованием сериализации JSON).

**Пример**

Ниже приведен образец кода для отправки пользователя hello пол и дату рождения:

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a>Ограничения
Ограничения, применяемые tooapplication сведения находятся в областях hello регулярных выражений для ключей и размер.

#### <a name="keys"></a>ключей
Каждый ключ в hello объекта должно соответствовать hello следующее регулярное выражение:

    ^[a-zA-Z][a-zA-Z_0-9]*

Это означает, что ключ должен содержать не менее одной буквы, за которой следуют буквы, цифры или символы подчеркивания (\_).

#### <a name="size"></a>Размер
Сведения о приложении — ограниченный too1, 024 символов на вызов (после hello Mobile Engagement Web SDK кодирует его в формате JSON).

В предыдущих пример hello hello JSON отправлено toohello server 44 символов:

    {"birthdate":"1983-12-07","gender":"female"}
