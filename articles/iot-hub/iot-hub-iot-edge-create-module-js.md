---
title: "Модуль Edge Azure IoT с Node.js aaaCreate | Документы Microsoft"
description: "Этот учебник демонстрирует, как отключить данных преобразователь модуля с помощью toowrite hello последние пакеты Azure IoT Edge NPM и Yeoman генератора."
services: iot-hub
author: sushi
manager: timlt
ms.service: iot-hub
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: js
ms.topic: article
ms.date: 06/28/2017
ms.author: sushi
ms.openlocfilehash: d3e696b5a310377ffb8e99998ff0714bf7c0bb41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-nodejs"></a>Создание модуля Azure IoT Edge с помощью Node.js

Этот учебник демонстрирует способ toocreate модуль для Azure IoT край JS.

В этом учебнике мы будем рассматривать настройки среды и как toowrite [ЛЮЧИТЬ](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) модуля преобразователя данных с помощью последних пакетов Azure IoT Edge NPM hello.

## <a name="prerequisites"></a>Предварительные требования

В этом разделе настраивается среда для разработки модуля IoT Edge. Оно применяется tooboth *64-разрядной версии Windows* и *Linux 64-разрядных (Ubuntu 14 +)* операционных систем.

Привет, следуя программного обеспечения не требуется:
* [клиент Git](https://git-scm.com/downloads);
* [Node LTS](https://nodejs.org);
* `npm install -g yo`.
* `npm install -g generator-az-iot-gw-module`

## <a name="architecture"></a>Архитектура

Платформа Azure IoT Edge Hello интенсивно использует hello [Von Неймана архитектура](https://en.wikipedia.org/wiki/Von_Neumann_architecture). Означающее этой архитектуры hello всей границы IoT Azure — это система, обрабатывает ввод и вывод; и каждый отдельный модуль также является очень мала подсистемы ввода вывода. В этом учебнике мы представляем следующие два модуля hello:

1. Модуль, который получает имитацию сигнала [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) и преобразует его в сообщение в формате [JSON](https://en.wikipedia.org/wiki/JSON).
2. Модуль, который выводит hello получил [JSON](https://en.wikipedia.org/wiki/JSON) сообщения.

Hello следующее изображение hello типичные конец dataflow tooend для этого проекта:

![Поток данных между тремя модулями](media/iot-hub-iot-edge-create-module/dataflow.png "Входные данные: имитация модуля BLE; Процессор: модуль преобразователя; Выходные данные: модуль принтера")

## <a name="set-up-hello-environment"></a>Настройка среды hello
Ниже мы покажем, как tooquickly настроить среду toostart toowrite первого модуля преобразователя ЛЮЧИТЬ с JS.

### <a name="create-module-project"></a>Создание проекта модуля
1. Откройте окно командной строки, выполните команду `yo az-iot-gw-module`.
2. Выполните действия hello при инициализации hello toofinish экрана приветствия проекта модуля.

### <a name="project-structure"></a>Структура проекта
Проект модуля JS состоит из hello следующие компоненты:

`modules`-hello настроенные JS модуль исходных файлов. Замените по умолчанию hello `sensor.js` и `printer.js` вместе с файлами модуля.

`app.js`-экземпляр Edge toostart hello hello записи файла.

`gw.config.json`-загрузить модули hello конфигурации файла toocustomize hello toobe край.

`package.json`-hello сведения метаданных для модуля проекта.

`README.md`-hello базовую документацию для проекта модуля.


### <a name="package-file"></a>Файл пакета

Это `package.json` объявляет все метаданные hello информацию, необходимую для проекта модуля, содержащего зависимости hello имя, версию, запись, скрипты, среда выполнения и разработки.

Следующий фрагмент кода показывает кода как tooconfigure для конвертера ЛЮЧИТЬ образца проекта.
```json
{
  "name": "converter",
  "version": "1.0.0",
  "description": "BLE data converter sample for Azure IoT Edge.",
  "repository": {
    "type": "git",
    "url": "https://github.com/Azure-Samples/iot-edge-samples"
  },
  "main": "app.js",
  "scripts": {
    "start": "node app.js"
  },
  "author": "Microsoft Corporation",
  "license": "MIT",
  "dependencies": {
  },
  "devDependencies": {
    "azure-iot-gateway": "~1.1.3"
  }
}
```


### <a name="entry-file"></a>Вводный файл
Hello `app.js` определяет hello способом tooinitialize hello edge экземпляр. Здесь мы не toomake любые изменения.

```javascript
(function() {
  'use strict';

  const Gateway = require('azure-iot-gateway');
  let config_path = './gw.config.json';

  // node app.js
  if (process.argv.length < 2) {
    throw 'Calling pattern should be node app.js.';
  }

  const gw = new Gateway(config_path);
  gw.run();
})();
```

### <a name="interface-of-module"></a>Интерфейс модуля
Модуль Azure IoT Edge можно рассматривать как обработчик данных, задачей которого является получение входных данных, их обработка и генерирование выходных данных.

Hello входные данные могут быть данные от оборудования (например, Детектор движения), сообщение от других модулей, и любые другие элементы (например, случайное число, периодически созданные таймер).

Hello выходные данные выглядят аналогично toohello входных данных, она может активировать поведением оборудования (например, Индикатор мигает hello), модулей tooother сообщение и любые другие элементы (например, консоль печати toohello).

Модули взаимодействуют друг с другом с помощью объекта `message`. Hello **содержимого** из `message` — массив байтов, способный представлять любых нужных данных. **Свойства** также доступны в hello `message` и являются просто сопоставление строка строка. Можно сравнивать с **свойства** как hello заголовки в HTTP-запроса или hello метаданные файла.

Порядок toodevelop модуль Azure IoT Edge в JS, нужен toocreate объект модуля, реализующего методы hello необходимые `receive()`. На этом этапе можно также выбрать дополнительный hello tooimplement `create()` или `start()`, или `destroy()` также методы. Привет, следующий фрагмент кода показывает, что hello формирование шаблонов JS объекта модуля.

```javascript
'use strict';

module.exports = {
  broker: null,
  configuration: null,

  create: function (broker, configuration) {
    // Default implementation.
    this.broker = broker;
    this.configuration = configuration;

    return true;
  },

  start: function () {
    // Produce
  },

  receive: function (message) {
    // Consume
  },

  destroy: function () {
  }
};
```

### <a name="converter-module"></a>Модуль преобразователя
| Входные данные                    | Процессор                              | Выходные данные                 | Исходный файл            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| Сообщение с данными температуры | Синтаксический анализ и создание сообщения JSON | Структурирование сообщения JSON | `converter.js` |

Этот модуль является типичным модулем Azure IoT Edge. Она принимает сообщения температуры из других модулей (аппаратного модуля или в данном случае нашей имитацию модуля ЛЮЧИТЬ); а затем нормализует сообщения hello температуры в структурированный tooa сообщение JSON (включая добавления идентификатора сообщения hello, задание для свойства hello ли мы должны tootrigger hello температуры предупреждение и так далее).

```javascript
receive: function (message) {
  // Initialize hello messageCount in global object at first time.
  if (!global.messageCount) {
    global.messageCount = 0;
  }

  // Read hello content and properties objects from message.
  let rawContent = JSON.parse(Buffer.from(message.content).toString('utf8'));
  let rawProperties = message.properties;

  // Generate new properties object.
  let newProperties = {
    source: rawProperties.source,
    macAddress: rawProperties.macAddress,
    temperatureAlert: rawContent.temperature > 30 ? 'true' : 'false'
  };

  // Generate new content object.
  let newContent = {
    deviceId: 'Intel NUC Gateway',
    messageId: ++global.messageCount,
    temperature: rawContent.temperature
  };

  // Publish hello new message toobroker.
  this.broker.publish(
    {
      properties: newProperties,
      content: new Uint8Array(Buffer.from(JSON.stringify(newContent), 'utf8'))
    }
  );
},
```

### <a name="printer-module"></a>Модуль принтера
| Входные данные                          | Процессор | Выходные данные                     | Исходный файл          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| Любое сообщение от других модулей | Недоступно       | Журнал tooconsole сообщение hello | `printer.js` |

Этот модуль является простой, интуитивно понятными, который выводит окно терминала toohello сообщений (свойства, содержимое) получил hello.

```javascript
receive: function (message) {
  let properties = JSON.stringify(message.properties);
  let content = Buffer.from(message.content).toString('utf8');

  console.log(`printer.receive.properties - ${properties}`);
  console.log(`printer.receive.content - ${content}\n`);
}
```

### <a name="configuration"></a>Конфигурация
Hello последним шагом перед запуском hello модулей является tooconfigure hello Azure IoT Edge и tooestablish hello соединения между модулями.

Сначала мы должны toodeclare наших `node` загрузчика (с момента загрузчиков поддерживает Azure IoT Edge на различных языках), который может ссылаться на его `name` в разделах hello позже.

```json
"loaders": [
  {
    "type": "node",
    "name": "node"
  }
]
```

После объявления нашей загрузчиков заключаются в toodeclare также нашей модулей. Аналогичные загрузчиков hello toodeclaring, они могут также ссылаться их `name` атрибута. При объявлении модуля, нам нужно toospecify hello загрузчика следует использовать (который должен быть hello один мы определили перед) и hello точки входа (должно быть имя класса нормализованный hello нашей модуля) для каждого модуля. Hello `simulated_device` собственный модуль, включенный в пакет среды выполнения core hello Azure IoT Edge. Включить `args` в файл JSON, даже если это hello `null`.

```json
"modules": [
  {
    "name": "simulated_device",
    "loader": {
      "name": "native",
      "entrypoint": {
        "module.path": "simulated_device"
      }
    },
    "args": {
      "macAddress": "01:02:03:03:02:01",
      "messagePeriod": 500
    }
  },
  {
    "name": "converter",
    "loader": {
      "name": "node",
      "entrypoint": {
        "main.path": "modules/converter.js"
      }
    },
    "args": null
  },
  {
    "name": "printer",
    "loader": {
      "name": "node",
      "entrypoint": {
        "main.path": "modules/printer.js"
      }
    },
    "args": null
  }
]
```

В конце конфигурации hello hello мы устанавливать подключения hello. Каждое подключение выражается с помощью `source` и `sink`. Оба этих параметра должны ссылаться на предварительно определенный модуль. Выходное сообщение Hello объекта `source` модуль пересылается ввода toohello `sink` модуля.

```json
"links": [
  {
    "source": "simulated_device",
    "sink": "converter"
  },
  {
    "source": "converter",
    "sink": "printer"
  }
]
```

## <a name="running-hello-modules"></a>Запуск модулей hello
1. `npm install`
2. `npm start`

Приложение hello tooterminate нажмите `<Enter>` ключа.

> [!IMPORTANT]
> Не рекомендуется toouse Ctrl + C tooterminate hello IoT Edge приложения. Таким образом может привести к тому, tooterminate hello процесса аварийно.
