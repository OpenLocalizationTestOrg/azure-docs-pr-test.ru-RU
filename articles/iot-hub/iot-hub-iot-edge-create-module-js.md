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
# <a name="create-an-azure-iot-edge-module-with-nodejs"></a><span data-ttu-id="a2728-103">Создание модуля Azure IoT Edge с помощью Node.js</span><span class="sxs-lookup"><span data-stu-id="a2728-103">Create an Azure IoT Edge Module with Node.js</span></span>

<span data-ttu-id="a2728-104">Этот учебник демонстрирует способ toocreate модуль для Azure IoT край JS.</span><span class="sxs-lookup"><span data-stu-id="a2728-104">This tutorial showcases how toocreate a module for Azure IoT Edge in JS.</span></span>

<span data-ttu-id="a2728-105">В этом учебнике мы будем рассматривать настройки среды и как toowrite [ЛЮЧИТЬ](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) модуля преобразователя данных с помощью последних пакетов Azure IoT Edge NPM hello.</span><span class="sxs-lookup"><span data-stu-id="a2728-105">In this tutorial, we walk through environment setup and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest Azure IoT Edge NPM packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2728-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a2728-106">Prerequisites</span></span>

<span data-ttu-id="a2728-107">В этом разделе настраивается среда для разработки модуля IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="a2728-107">In this section, you set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="a2728-108">Оно применяется tooboth *64-разрядной версии Windows* и *Linux 64-разрядных (Ubuntu 14 +)* операционных систем.</span><span class="sxs-lookup"><span data-stu-id="a2728-108">It applies tooboth *64-bit Windows* and *64-bit Linux (Ubuntu 14+)* operating systems.</span></span>

<span data-ttu-id="a2728-109">Привет, следуя программного обеспечения не требуется:</span><span class="sxs-lookup"><span data-stu-id="a2728-109">hello following software is required:</span></span>
* <span data-ttu-id="a2728-110">[клиент Git](https://git-scm.com/downloads);</span><span class="sxs-lookup"><span data-stu-id="a2728-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="a2728-111">[Node LTS](https://nodejs.org);</span><span class="sxs-lookup"><span data-stu-id="a2728-111">[Node LTS](https://nodejs.org).</span></span>
* <span data-ttu-id="a2728-112">`npm install -g yo`.</span><span class="sxs-lookup"><span data-stu-id="a2728-112">`npm install -g yo`.</span></span>
* `npm install -g generator-az-iot-gw-module`

## <a name="architecture"></a><span data-ttu-id="a2728-113">Архитектура</span><span class="sxs-lookup"><span data-stu-id="a2728-113">Architecture</span></span>

<span data-ttu-id="a2728-114">Платформа Azure IoT Edge Hello интенсивно использует hello [Von Неймана архитектура](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span><span class="sxs-lookup"><span data-stu-id="a2728-114">hello Azure IoT Edge platform heavily adopts hello [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="a2728-115">Означающее этой архитектуры hello всей границы IoT Azure — это система, обрабатывает ввод и вывод; и каждый отдельный модуль также является очень мала подсистемы ввода вывода.</span><span class="sxs-lookup"><span data-stu-id="a2728-115">Which means that hello entire Azure IoT Edge architecture is a system that processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="a2728-116">В этом учебнике мы представляем следующие два модуля hello:</span><span class="sxs-lookup"><span data-stu-id="a2728-116">In this tutorial, we introduce hello following two modules:</span></span>

1. <span data-ttu-id="a2728-117">Модуль, который получает имитацию сигнала [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) и преобразует его в сообщение в формате [JSON](https://en.wikipedia.org/wiki/JSON).</span><span class="sxs-lookup"><span data-stu-id="a2728-117">A module that receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="a2728-118">Модуль, который выводит hello получил [JSON](https://en.wikipedia.org/wiki/JSON) сообщения.</span><span class="sxs-lookup"><span data-stu-id="a2728-118">A module that prints hello received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="a2728-119">Hello следующее изображение hello типичные конец dataflow tooend для этого проекта:</span><span class="sxs-lookup"><span data-stu-id="a2728-119">hello following image displays hello typical end tooend dataflow for this project:</span></span>

<span data-ttu-id="a2728-120">![Поток данных между тремя модулями](media/iot-hub-iot-edge-create-module/dataflow.png "Входные данные: имитация модуля BLE; Процессор: модуль преобразователя; Выходные данные: модуль принтера")</span><span class="sxs-lookup"><span data-stu-id="a2728-120">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="set-up-hello-environment"></a><span data-ttu-id="a2728-121">Настройка среды hello</span><span class="sxs-lookup"><span data-stu-id="a2728-121">Set up hello environment</span></span>
<span data-ttu-id="a2728-122">Ниже мы покажем, как tooquickly настроить среду toostart toowrite первого модуля преобразователя ЛЮЧИТЬ с JS.</span><span class="sxs-lookup"><span data-stu-id="a2728-122">Below we show you how tooquickly set up environment toostart toowrite your first BLE converter module with JS.</span></span>

### <a name="create-module-project"></a><span data-ttu-id="a2728-123">Создание проекта модуля</span><span class="sxs-lookup"><span data-stu-id="a2728-123">Create module project</span></span>
1. <span data-ttu-id="a2728-124">Откройте окно командной строки, выполните команду `yo az-iot-gw-module`.</span><span class="sxs-lookup"><span data-stu-id="a2728-124">Open a command-line window, run `yo az-iot-gw-module`.</span></span>
2. <span data-ttu-id="a2728-125">Выполните действия hello при инициализации hello toofinish экрана приветствия проекта модуля.</span><span class="sxs-lookup"><span data-stu-id="a2728-125">Follow hello steps on hello screen toofinish hello initialization of your module project.</span></span>

### <a name="project-structure"></a><span data-ttu-id="a2728-126">Структура проекта</span><span class="sxs-lookup"><span data-stu-id="a2728-126">Project structure</span></span>
<span data-ttu-id="a2728-127">Проект модуля JS состоит из hello следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="a2728-127">A JS module project consists of hello following components:</span></span>

<span data-ttu-id="a2728-128">`modules`-hello настроенные JS модуль исходных файлов.</span><span class="sxs-lookup"><span data-stu-id="a2728-128">`modules` - hello customized JS module source files.</span></span> <span data-ttu-id="a2728-129">Замените по умолчанию hello `sensor.js` и `printer.js` вместе с файлами модуля.</span><span class="sxs-lookup"><span data-stu-id="a2728-129">Replace hello default `sensor.js` and `printer.js` with your own module files.</span></span>

<span data-ttu-id="a2728-130">`app.js`-экземпляр Edge toostart hello hello записи файла.</span><span class="sxs-lookup"><span data-stu-id="a2728-130">`app.js` - hello entry file toostart hello Edge instance.</span></span>

<span data-ttu-id="a2728-131">`gw.config.json`-загрузить модули hello конфигурации файла toocustomize hello toobe край.</span><span class="sxs-lookup"><span data-stu-id="a2728-131">`gw.config.json` - hello configuration file toocustomize hello modules toobe loaded by Edge.</span></span>

<span data-ttu-id="a2728-132">`package.json`-hello сведения метаданных для модуля проекта.</span><span class="sxs-lookup"><span data-stu-id="a2728-132">`package.json` - hello metadata information for module project.</span></span>

<span data-ttu-id="a2728-133">`README.md`-hello базовую документацию для проекта модуля.</span><span class="sxs-lookup"><span data-stu-id="a2728-133">`README.md` - hello basic documentation for module project.</span></span>


### <a name="package-file"></a><span data-ttu-id="a2728-134">Файл пакета</span><span class="sxs-lookup"><span data-stu-id="a2728-134">Package file</span></span>

<span data-ttu-id="a2728-135">Это `package.json` объявляет все метаданные hello информацию, необходимую для проекта модуля, содержащего зависимости hello имя, версию, запись, скрипты, среда выполнения и разработки.</span><span class="sxs-lookup"><span data-stu-id="a2728-135">This `package.json` declares all hello metadata information needed by a module project that includes hello name, version, entry, scripts, runtime, and development dependencies.</span></span>

<span data-ttu-id="a2728-136">Следующий фрагмент кода показывает кода как tooconfigure для конвертера ЛЮЧИТЬ образца проекта.</span><span class="sxs-lookup"><span data-stu-id="a2728-136">Following code snippet shows how tooconfigure for BLE converter sample project.</span></span>
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


### <a name="entry-file"></a><span data-ttu-id="a2728-137">Вводный файл</span><span class="sxs-lookup"><span data-stu-id="a2728-137">Entry file</span></span>
<span data-ttu-id="a2728-138">Hello `app.js` определяет hello способом tooinitialize hello edge экземпляр.</span><span class="sxs-lookup"><span data-stu-id="a2728-138">hello `app.js` defines hello way tooinitialize hello edge instance.</span></span> <span data-ttu-id="a2728-139">Здесь мы не toomake любые изменения.</span><span class="sxs-lookup"><span data-stu-id="a2728-139">Here we don't need toomake any change.</span></span>

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

### <a name="interface-of-module"></a><span data-ttu-id="a2728-140">Интерфейс модуля</span><span class="sxs-lookup"><span data-stu-id="a2728-140">Interface of module</span></span>
<span data-ttu-id="a2728-141">Модуль Azure IoT Edge можно рассматривать как обработчик данных, задачей которого является получение входных данных, их обработка и генерирование выходных данных.</span><span class="sxs-lookup"><span data-stu-id="a2728-141">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="a2728-142">Hello входные данные могут быть данные от оборудования (например, Детектор движения), сообщение от других модулей, и любые другие элементы (например, случайное число, периодически созданные таймер).</span><span class="sxs-lookup"><span data-stu-id="a2728-142">hello input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="a2728-143">Hello выходные данные выглядят аналогично toohello входных данных, она может активировать поведением оборудования (например, Индикатор мигает hello), модулей tooother сообщение и любые другие элементы (например, консоль печати toohello).</span><span class="sxs-lookup"><span data-stu-id="a2728-143">hello output is similar toohello input, it could trigger hardware behavior (like hello blinking LED), a message tooother modules, or anything else (like printing toohello console).</span></span>

<span data-ttu-id="a2728-144">Модули взаимодействуют друг с другом с помощью объекта `message`.</span><span class="sxs-lookup"><span data-stu-id="a2728-144">Modules communicate with each other using `message` object.</span></span> <span data-ttu-id="a2728-145">Hello **содержимого** из `message` — массив байтов, способный представлять любых нужных данных.</span><span class="sxs-lookup"><span data-stu-id="a2728-145">hello **content** of a `message` is a byte array that is capable of representing any kind of data you like.</span></span> <span data-ttu-id="a2728-146">**Свойства** также доступны в hello `message` и являются просто сопоставление строка строка.</span><span class="sxs-lookup"><span data-stu-id="a2728-146">**Properties** are also available in hello `message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="a2728-147">Можно сравнивать с **свойства** как hello заголовки в HTTP-запроса или hello метаданные файла.</span><span class="sxs-lookup"><span data-stu-id="a2728-147">You may think of **properties** as hello headers in an HTTP request, or hello metadata of a file.</span></span>

<span data-ttu-id="a2728-148">Порядок toodevelop модуль Azure IoT Edge в JS, нужен toocreate объект модуля, реализующего методы hello необходимые `receive()`.</span><span class="sxs-lookup"><span data-stu-id="a2728-148">In order toodevelop an Azure IoT Edge module in JS, you need toocreate a new module object that implements hello required methods `receive()`.</span></span> <span data-ttu-id="a2728-149">На этом этапе можно также выбрать дополнительный hello tooimplement `create()` или `start()`, или `destroy()` также методы.</span><span class="sxs-lookup"><span data-stu-id="a2728-149">At this point, you may also choose tooimplement hello optional `create()` or `start()`, or `destroy()` methods as well.</span></span> <span data-ttu-id="a2728-150">Привет, следующий фрагмент кода показывает, что hello формирование шаблонов JS объекта модуля.</span><span class="sxs-lookup"><span data-stu-id="a2728-150">hello following code snippet shows you hello scaffolding of JS module object.</span></span>

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

### <a name="converter-module"></a><span data-ttu-id="a2728-151">Модуль преобразователя</span><span class="sxs-lookup"><span data-stu-id="a2728-151">Converter module</span></span>
| <span data-ttu-id="a2728-152">Входные данные</span><span class="sxs-lookup"><span data-stu-id="a2728-152">Input</span></span>                    | <span data-ttu-id="a2728-153">Процессор</span><span class="sxs-lookup"><span data-stu-id="a2728-153">Processor</span></span>                              | <span data-ttu-id="a2728-154">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="a2728-154">Output</span></span>                 | <span data-ttu-id="a2728-155">Исходный файл</span><span class="sxs-lookup"><span data-stu-id="a2728-155">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="a2728-156">Сообщение с данными температуры</span><span class="sxs-lookup"><span data-stu-id="a2728-156">Temperature data message</span></span> | <span data-ttu-id="a2728-157">Синтаксический анализ и создание сообщения JSON</span><span class="sxs-lookup"><span data-stu-id="a2728-157">Parse and construct a new JSON message</span></span> | <span data-ttu-id="a2728-158">Структурирование сообщения JSON</span><span class="sxs-lookup"><span data-stu-id="a2728-158">Structure JSON message</span></span> | `converter.js` |

<span data-ttu-id="a2728-159">Этот модуль является типичным модулем Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="a2728-159">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="a2728-160">Она принимает сообщения температуры из других модулей (аппаратного модуля или в данном случае нашей имитацию модуля ЛЮЧИТЬ); а затем нормализует сообщения hello температуры в структурированный tooa сообщение JSON (включая добавления идентификатора сообщения hello, задание для свойства hello ли мы должны tootrigger hello температуры предупреждение и так далее).</span><span class="sxs-lookup"><span data-stu-id="a2728-160">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes hello temperature message in tooa structured JSON message (including appending hello message ID, setting hello property of whether we need tootrigger hello temperature alert, and so on).</span></span>

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

### <a name="printer-module"></a><span data-ttu-id="a2728-161">Модуль принтера</span><span class="sxs-lookup"><span data-stu-id="a2728-161">Printer module</span></span>
| <span data-ttu-id="a2728-162">Входные данные</span><span class="sxs-lookup"><span data-stu-id="a2728-162">Input</span></span>                          | <span data-ttu-id="a2728-163">Процессор</span><span class="sxs-lookup"><span data-stu-id="a2728-163">Processor</span></span> | <span data-ttu-id="a2728-164">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="a2728-164">Output</span></span>                     | <span data-ttu-id="a2728-165">Исходный файл</span><span class="sxs-lookup"><span data-stu-id="a2728-165">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="a2728-166">Любое сообщение от других модулей</span><span class="sxs-lookup"><span data-stu-id="a2728-166">Any message from other modules</span></span> | <span data-ttu-id="a2728-167">Недоступно</span><span class="sxs-lookup"><span data-stu-id="a2728-167">N/A</span></span>       | <span data-ttu-id="a2728-168">Журнал tooconsole сообщение hello</span><span class="sxs-lookup"><span data-stu-id="a2728-168">Log hello message tooconsole</span></span> | `printer.js` |

<span data-ttu-id="a2728-169">Этот модуль является простой, интуитивно понятными, который выводит окно терминала toohello сообщений (свойства, содержимое) получил hello.</span><span class="sxs-lookup"><span data-stu-id="a2728-169">This module is simple, self-explanatory, which outputs hello received messages(property, content) toohello terminal window.</span></span>

```javascript
receive: function (message) {
  let properties = JSON.stringify(message.properties);
  let content = Buffer.from(message.content).toString('utf8');

  console.log(`printer.receive.properties - ${properties}`);
  console.log(`printer.receive.content - ${content}\n`);
}
```

### <a name="configuration"></a><span data-ttu-id="a2728-170">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="a2728-170">Configuration</span></span>
<span data-ttu-id="a2728-171">Hello последним шагом перед запуском hello модулей является tooconfigure hello Azure IoT Edge и tooestablish hello соединения между модулями.</span><span class="sxs-lookup"><span data-stu-id="a2728-171">hello final step before running hello modules is tooconfigure hello Azure IoT Edge and tooestablish hello connections between modules.</span></span>

<span data-ttu-id="a2728-172">Сначала мы должны toodeclare наших `node` загрузчика (с момента загрузчиков поддерживает Azure IoT Edge на различных языках), который может ссылаться на его `name` в разделах hello позже.</span><span class="sxs-lookup"><span data-stu-id="a2728-172">First we need toodeclare our `node` loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in hello sections afterward.</span></span>

```json
"loaders": [
  {
    "type": "node",
    "name": "node"
  }
]
```

<span data-ttu-id="a2728-173">После объявления нашей загрузчиков заключаются в toodeclare также нашей модулей.</span><span class="sxs-lookup"><span data-stu-id="a2728-173">Once we have declared our loaders, we also need toodeclare our modules as well.</span></span> <span data-ttu-id="a2728-174">Аналогичные загрузчиков hello toodeclaring, они могут также ссылаться их `name` атрибута.</span><span class="sxs-lookup"><span data-stu-id="a2728-174">Similar toodeclaring hello loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="a2728-175">При объявлении модуля, нам нужно toospecify hello загрузчика следует использовать (который должен быть hello один мы определили перед) и hello точки входа (должно быть имя класса нормализованный hello нашей модуля) для каждого модуля.</span><span class="sxs-lookup"><span data-stu-id="a2728-175">When declaring a module, we need toospecify hello loader it should use (which should be hello one we defined before) and hello entry-point (should be hello normalized class name of our module) for each module.</span></span> <span data-ttu-id="a2728-176">Hello `simulated_device` собственный модуль, включенный в пакет среды выполнения core hello Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="a2728-176">hello `simulated_device` module is a native module that is included in hello Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="a2728-177">Включить `args` в файл JSON, даже если это hello `null`.</span><span class="sxs-lookup"><span data-stu-id="a2728-177">Include `args` in hello JSON file even if it is `null`.</span></span>

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

<span data-ttu-id="a2728-178">В конце конфигурации hello hello мы устанавливать подключения hello.</span><span class="sxs-lookup"><span data-stu-id="a2728-178">At hello end of hello configuration, we establish hello connections.</span></span> <span data-ttu-id="a2728-179">Каждое подключение выражается с помощью `source` и `sink`.</span><span class="sxs-lookup"><span data-stu-id="a2728-179">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="a2728-180">Оба этих параметра должны ссылаться на предварительно определенный модуль.</span><span class="sxs-lookup"><span data-stu-id="a2728-180">They should both reference a pre-defined module.</span></span> <span data-ttu-id="a2728-181">Выходное сообщение Hello объекта `source` модуль пересылается ввода toohello `sink` модуля.</span><span class="sxs-lookup"><span data-stu-id="a2728-181">hello output message of `source` module is forwarded toohello input of `sink` module.</span></span>

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

## <a name="running-hello-modules"></a><span data-ttu-id="a2728-182">Запуск модулей hello</span><span class="sxs-lookup"><span data-stu-id="a2728-182">Running hello modules</span></span>
1. `npm install`
2. `npm start`

<span data-ttu-id="a2728-183">Приложение hello tooterminate нажмите `<Enter>` ключа.</span><span class="sxs-lookup"><span data-stu-id="a2728-183">If you want tooterminate hello application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a2728-184">Не рекомендуется toouse Ctrl + C tooterminate hello IoT Edge приложения.</span><span class="sxs-lookup"><span data-stu-id="a2728-184">It is not recommended toouse Ctrl + C tooterminate hello IoT Edge application.</span></span> <span data-ttu-id="a2728-185">Таким образом может привести к тому, tooterminate hello процесса аварийно.</span><span class="sxs-lookup"><span data-stu-id="a2728-185">As this way may cause hello process tooterminate abnormally.</span></span>
