---
title: "Создание модуля Azure IoT Edge с помощью Node.js | Документация Майкрософт"
description: "В этом руководстве показано, как с помощью последних пакетов NPM для Azure IoT Edge и генератора Yeoman написать модуль преобразователя данных BLE."
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
ms.openlocfilehash: ba466f47e157d805600c41fa3d84ed5a0363969c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-iot-edge-module-with-nodejs"></a><span data-ttu-id="4633c-103">Создание модуля Azure IoT Edge с помощью Node.js</span><span class="sxs-lookup"><span data-stu-id="4633c-103">Create an Azure IoT Edge Module with Node.js</span></span>

<span data-ttu-id="4633c-104">В этом руководстве показано, как с помощью JS создать модуль для Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="4633c-104">This tutorial showcases how to create a module for Azure IoT Edge in JS.</span></span>

<span data-ttu-id="4633c-105">В этом руководстве приводятся пошаговые инструкции по настройке среды и написанию модуля преобразователя данных [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) с помощью последних пакетов NPM для Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="4633c-105">In this tutorial, we walk through environment setup and how to write a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using the latest Azure IoT Edge NPM packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4633c-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4633c-106">Prerequisites</span></span>

<span data-ttu-id="4633c-107">В этом разделе настраивается среда для разработки модуля IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="4633c-107">In this section, you set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="4633c-108">Данные настройки действительны для следующих операционных систем: *64-разрядная версия Windows* и *64-разрядная версия Linux (Ubuntu 14+)*.</span><span class="sxs-lookup"><span data-stu-id="4633c-108">It applies to both *64-bit Windows* and *64-bit Linux (Ubuntu 14+)* operating systems.</span></span>

<span data-ttu-id="4633c-109">Требуется следующее ПО:</span><span class="sxs-lookup"><span data-stu-id="4633c-109">The following software is required:</span></span>
* <span data-ttu-id="4633c-110">[клиент Git](https://git-scm.com/downloads);</span><span class="sxs-lookup"><span data-stu-id="4633c-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="4633c-111">[Node LTS](https://nodejs.org);</span><span class="sxs-lookup"><span data-stu-id="4633c-111">[Node LTS](https://nodejs.org).</span></span>
* <span data-ttu-id="4633c-112">`npm install -g yo`.</span><span class="sxs-lookup"><span data-stu-id="4633c-112">`npm install -g yo`.</span></span>
* `npm install -g generator-az-iot-gw-module`

## <a name="architecture"></a><span data-ttu-id="4633c-113">Архитектура</span><span class="sxs-lookup"><span data-stu-id="4633c-113">Architecture</span></span>

<span data-ttu-id="4633c-114">Платформа Azure IoT Edge интенсивно применяет [архитектуру фон Неймана](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span><span class="sxs-lookup"><span data-stu-id="4633c-114">The Azure IoT Edge platform heavily adopts the [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="4633c-115">Это означает, что вся архитектура Azure IoT Edge является системой, которая обрабатывает входные и создает выходные данные. А каждый отдельный модуль также является небольшой подсистемой ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="4633c-115">Which means that the entire Azure IoT Edge architecture is a system that processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="4633c-116">В этом руководстве описываются следующее два модуля:</span><span class="sxs-lookup"><span data-stu-id="4633c-116">In this tutorial, we introduce the following two modules:</span></span>

1. <span data-ttu-id="4633c-117">Модуль, который получает имитацию сигнала [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) и преобразует его в сообщение в формате [JSON](https://en.wikipedia.org/wiki/JSON).</span><span class="sxs-lookup"><span data-stu-id="4633c-117">A module that receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="4633c-118">Модуль, который выводит полученное сообщение [JSON](https://en.wikipedia.org/wiki/JSON).</span><span class="sxs-lookup"><span data-stu-id="4633c-118">A module that prints the received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="4633c-119">На следующем рисунке показан типичный сквозной поток данных для этого проекта:</span><span class="sxs-lookup"><span data-stu-id="4633c-119">The following image displays the typical end to end dataflow for this project:</span></span>

<span data-ttu-id="4633c-120">![Поток данных между тремя модулями](media/iot-hub-iot-edge-create-module/dataflow.png "Входные данные: имитация модуля BLE; Процессор: модуль преобразователя; Выходные данные: модуль принтера")</span><span class="sxs-lookup"><span data-stu-id="4633c-120">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="set-up-the-environment"></a><span data-ttu-id="4633c-121">Настройка среды</span><span class="sxs-lookup"><span data-stu-id="4633c-121">Set up the environment</span></span>
<span data-ttu-id="4633c-122">Ниже показано, как с помощью JS быстро настроить среду, необходимую для написания первого модуля преобразователя BLE.</span><span class="sxs-lookup"><span data-stu-id="4633c-122">Below we show you how to quickly set up environment to start to write your first BLE converter module with JS.</span></span>

### <a name="create-module-project"></a><span data-ttu-id="4633c-123">Создание проекта модуля</span><span class="sxs-lookup"><span data-stu-id="4633c-123">Create module project</span></span>
1. <span data-ttu-id="4633c-124">Откройте окно командной строки, выполните команду `yo az-iot-gw-module`.</span><span class="sxs-lookup"><span data-stu-id="4633c-124">Open a command-line window, run `yo az-iot-gw-module`.</span></span>
2. <span data-ttu-id="4633c-125">Следуйте инструкциям на экране, чтобы завершить инициализацию модуля проекта.</span><span class="sxs-lookup"><span data-stu-id="4633c-125">Follow the steps on the screen to finish the initialization of your module project.</span></span>

### <a name="project-structure"></a><span data-ttu-id="4633c-126">Структура проекта</span><span class="sxs-lookup"><span data-stu-id="4633c-126">Project structure</span></span>
<span data-ttu-id="4633c-127">Проект модуля состоит из следующих компонентов:</span><span class="sxs-lookup"><span data-stu-id="4633c-127">A JS module project consists of the following components:</span></span>

<span data-ttu-id="4633c-128">`modules` — настраиваемые исходные файлы модуля JS.</span><span class="sxs-lookup"><span data-stu-id="4633c-128">`modules` - The customized JS module source files.</span></span> <span data-ttu-id="4633c-129">Замените файлы `sensor.js` и `printer.js`, заданные по умолчанию, своими файлами модуля.</span><span class="sxs-lookup"><span data-stu-id="4633c-129">Replace the default `sensor.js` and `printer.js` with your own module files.</span></span>

<span data-ttu-id="4633c-130">`app.js` — вводный файл для запуска экземпляра Edge.</span><span class="sxs-lookup"><span data-stu-id="4633c-130">`app.js` - The entry file to start the Edge instance.</span></span>

<span data-ttu-id="4633c-131">`gw.config.json` — файл конфигурации для настройки модулей, загружаемых Edge.</span><span class="sxs-lookup"><span data-stu-id="4633c-131">`gw.config.json` - The configuration file to customize the modules to be loaded by Edge.</span></span>

<span data-ttu-id="4633c-132">`package.json` — сведения о метаданных для проекта модуля.</span><span class="sxs-lookup"><span data-stu-id="4633c-132">`package.json` - The metadata information for module project.</span></span>

<span data-ttu-id="4633c-133">`README.md` — базовая документация для проекта модуля.</span><span class="sxs-lookup"><span data-stu-id="4633c-133">`README.md` - The basic documentation for module project.</span></span>


### <a name="package-file"></a><span data-ttu-id="4633c-134">Файл пакета</span><span class="sxs-lookup"><span data-stu-id="4633c-134">Package file</span></span>

<span data-ttu-id="4633c-135">Данный файл `package.json` объявляет все сведения о метаданных, необходимые для проекта модуля, такие как имя, версия, вводный файл, сценарии, среда выполнения и зависимости разработки.</span><span class="sxs-lookup"><span data-stu-id="4633c-135">This `package.json` declares all the metadata information needed by a module project that includes the name, version, entry, scripts, runtime, and development dependencies.</span></span>

<span data-ttu-id="4633c-136">В следующем фрагменте кода показано, как настроить пример проекта преобразователя BLE.</span><span class="sxs-lookup"><span data-stu-id="4633c-136">Following code snippet shows how to configure for BLE converter sample project.</span></span>
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


### <a name="entry-file"></a><span data-ttu-id="4633c-137">Вводный файл</span><span class="sxs-lookup"><span data-stu-id="4633c-137">Entry file</span></span>
<span data-ttu-id="4633c-138">Файл `app.js` определяет способ инициализации экземпляра Edge.</span><span class="sxs-lookup"><span data-stu-id="4633c-138">The `app.js` defines the way to initialize the edge instance.</span></span> <span data-ttu-id="4633c-139">Здесь не требуется вносить каких-либо изменений.</span><span class="sxs-lookup"><span data-stu-id="4633c-139">Here we don't need to make any change.</span></span>

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

### <a name="interface-of-module"></a><span data-ttu-id="4633c-140">Интерфейс модуля</span><span class="sxs-lookup"><span data-stu-id="4633c-140">Interface of module</span></span>
<span data-ttu-id="4633c-141">Модуль Azure IoT Edge можно рассматривать как обработчик данных, задачей которого является получение входных данных, их обработка и генерирование выходных данных.</span><span class="sxs-lookup"><span data-stu-id="4633c-141">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="4633c-142">Входными данными могут быть данные, получаемые от оборудования (например, от детектора движения), сообщения от других модулей и любые другие данные (например, случайное число, периодически генерируемое таймером).</span><span class="sxs-lookup"><span data-stu-id="4633c-142">The input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="4633c-143">Выходные данные похожи на входные. Они могут быть триггером каких-либо действий оборудования (например, мигание светодиодного индикатора), сообщениями для других модулей или чем-то другим (например, вывод данных в консоль).</span><span class="sxs-lookup"><span data-stu-id="4633c-143">The output is similar to the input, it could trigger hardware behavior (like the blinking LED), a message to other modules, or anything else (like printing to the console).</span></span>

<span data-ttu-id="4633c-144">Модули взаимодействуют друг с другом с помощью объекта `message`.</span><span class="sxs-lookup"><span data-stu-id="4633c-144">Modules communicate with each other using `message` object.</span></span> <span data-ttu-id="4633c-145">**Содержимым** `message` является массив байтов, который может представлять любой необходимый тип данных.</span><span class="sxs-lookup"><span data-stu-id="4633c-145">The **content** of a `message` is a byte array that is capable of representing any kind of data you like.</span></span> <span data-ttu-id="4633c-146">В `message` также доступны **Свойства**, которые являются просто сопоставлением строк.</span><span class="sxs-lookup"><span data-stu-id="4633c-146">**Properties** are also available in the `message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="4633c-147">**Свойства** можно сравнить с заголовками в HTTP-запросе или метаданными файла.</span><span class="sxs-lookup"><span data-stu-id="4633c-147">You may think of **properties** as the headers in an HTTP request, or the metadata of a file.</span></span>

<span data-ttu-id="4633c-148">Чтобы разработать модуль Azure IoT Edge в JS, необходимо создать объект модуля, который реализует необходимые методы `receive()`.</span><span class="sxs-lookup"><span data-stu-id="4633c-148">In order to develop an Azure IoT Edge module in JS, you need to create a new module object that implements the required methods `receive()`.</span></span> <span data-ttu-id="4633c-149">На этом этапе также можно реализовать дополнительные методы `create()`, `start()` и `destroy()`.</span><span class="sxs-lookup"><span data-stu-id="4633c-149">At this point, you may also choose to implement the optional `create()` or `start()`, or `destroy()` methods as well.</span></span> <span data-ttu-id="4633c-150">В следующем фрагменте кода показано формирование шаблонов объекта модуля JS.</span><span class="sxs-lookup"><span data-stu-id="4633c-150">The following code snippet shows you the scaffolding of JS module object.</span></span>

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

### <a name="converter-module"></a><span data-ttu-id="4633c-151">Модуль преобразователя</span><span class="sxs-lookup"><span data-stu-id="4633c-151">Converter module</span></span>
| <span data-ttu-id="4633c-152">Входные данные</span><span class="sxs-lookup"><span data-stu-id="4633c-152">Input</span></span>                    | <span data-ttu-id="4633c-153">Процессор</span><span class="sxs-lookup"><span data-stu-id="4633c-153">Processor</span></span>                              | <span data-ttu-id="4633c-154">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="4633c-154">Output</span></span>                 | <span data-ttu-id="4633c-155">Исходный файл</span><span class="sxs-lookup"><span data-stu-id="4633c-155">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="4633c-156">Сообщение с данными температуры</span><span class="sxs-lookup"><span data-stu-id="4633c-156">Temperature data message</span></span> | <span data-ttu-id="4633c-157">Синтаксический анализ и создание сообщения JSON</span><span class="sxs-lookup"><span data-stu-id="4633c-157">Parse and construct a new JSON message</span></span> | <span data-ttu-id="4633c-158">Структурирование сообщения JSON</span><span class="sxs-lookup"><span data-stu-id="4633c-158">Structure JSON message</span></span> | `converter.js` |

<span data-ttu-id="4633c-159">Этот модуль является типичным модулем Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="4633c-159">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="4633c-160">Он принимает сообщения с данными температуры от других модулей (аппаратного модуля или, как в нашем случае, имитации модуля BLE). Затем он нормализует эти сообщения в структурированное сообщение JSON, добавляя идентификатор сообщения, задавая значение свойства (например, необходимо ли активировать предупреждение о температуре) и т. д.</span><span class="sxs-lookup"><span data-stu-id="4633c-160">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes the temperature message in to a structured JSON message (including appending the message ID, setting the property of whether we need to trigger the temperature alert, and so on).</span></span>

```javascript
receive: function (message) {
  // Initialize the messageCount in global object at first time.
  if (!global.messageCount) {
    global.messageCount = 0;
  }

  // Read the content and properties objects from message.
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

  // Publish the new message to broker.
  this.broker.publish(
    {
      properties: newProperties,
      content: new Uint8Array(Buffer.from(JSON.stringify(newContent), 'utf8'))
    }
  );
},
```

### <a name="printer-module"></a><span data-ttu-id="4633c-161">Модуль принтера</span><span class="sxs-lookup"><span data-stu-id="4633c-161">Printer module</span></span>
| <span data-ttu-id="4633c-162">Входные данные</span><span class="sxs-lookup"><span data-stu-id="4633c-162">Input</span></span>                          | <span data-ttu-id="4633c-163">Процессор</span><span class="sxs-lookup"><span data-stu-id="4633c-163">Processor</span></span> | <span data-ttu-id="4633c-164">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="4633c-164">Output</span></span>                     | <span data-ttu-id="4633c-165">Исходный файл</span><span class="sxs-lookup"><span data-stu-id="4633c-165">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="4633c-166">Любое сообщение от других модулей</span><span class="sxs-lookup"><span data-stu-id="4633c-166">Any message from other modules</span></span> | <span data-ttu-id="4633c-167">Недоступно</span><span class="sxs-lookup"><span data-stu-id="4633c-167">N/A</span></span>       | <span data-ttu-id="4633c-168">Запись сообщения в консоль</span><span class="sxs-lookup"><span data-stu-id="4633c-168">Log the message to console</span></span> | `printer.js` |

<span data-ttu-id="4633c-169">Это простой и не нуждающийся в объяснении модуль, который выводит полученные сообщения (свойство или содержимое) в окне терминала.</span><span class="sxs-lookup"><span data-stu-id="4633c-169">This module is simple, self-explanatory, which outputs the received messages(property, content) to the terminal window.</span></span>

```javascript
receive: function (message) {
  let properties = JSON.stringify(message.properties);
  let content = Buffer.from(message.content).toString('utf8');

  console.log(`printer.receive.properties - ${properties}`);
  console.log(`printer.receive.content - ${content}\n`);
}
```

### <a name="configuration"></a><span data-ttu-id="4633c-170">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="4633c-170">Configuration</span></span>
<span data-ttu-id="4633c-171">Последним шагом перед запуском модулей является настройка Azure IoT Edge и установление подключений между модулями.</span><span class="sxs-lookup"><span data-stu-id="4633c-171">The final step before running the modules is to configure the Azure IoT Edge and to establish the connections between modules.</span></span>

<span data-ttu-id="4633c-172">Сначала необходимо объявить загрузчик `node` (так как Azure IoT Edge поддерживает загрузчики для различных языков), на который можно будет ссылаться по атрибуту `name` в последующих разделах.</span><span class="sxs-lookup"><span data-stu-id="4633c-172">First we need to declare our `node` loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in the sections afterward.</span></span>

```json
"loaders": [
  {
    "type": "node",
    "name": "node"
  }
]
```

<span data-ttu-id="4633c-173">После объявления загрузчиков нам также необходимо объявить модули.</span><span class="sxs-lookup"><span data-stu-id="4633c-173">Once we have declared our loaders, we also need to declare our modules as well.</span></span> <span data-ttu-id="4633c-174">По аналогии с объявлением загрузчиков на них также можно сослаться по атрибуту `name`.</span><span class="sxs-lookup"><span data-stu-id="4633c-174">Similar to declaring the loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="4633c-175">При объявлении модуля необходимо указать загрузчик, который он должен использовать (тот, который мы определили ранее), и точку входа (это должно быть нормализованное имя класса нашего модуля) для каждого модуля.</span><span class="sxs-lookup"><span data-stu-id="4633c-175">When declaring a module, we need to specify the loader it should use (which should be the one we defined before) and the entry-point (should be the normalized class name of our module) for each module.</span></span> <span data-ttu-id="4633c-176">Модуль `simulated_device` является собственным модулем, который входит в базовый пакет среды выполнения Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="4633c-176">The `simulated_device` module is a native module that is included in the Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="4633c-177">Включите в JSON-файл аргументы `args`, даже если они имеют значение `null`.</span><span class="sxs-lookup"><span data-stu-id="4633c-177">Include `args` in the JSON file even if it is `null`.</span></span>

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

<span data-ttu-id="4633c-178">На последнем этапе настройки устанавливаются подключения.</span><span class="sxs-lookup"><span data-stu-id="4633c-178">At the end of the configuration, we establish the connections.</span></span> <span data-ttu-id="4633c-179">Каждое подключение выражается с помощью `source` и `sink`.</span><span class="sxs-lookup"><span data-stu-id="4633c-179">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="4633c-180">Оба этих параметра должны ссылаться на предварительно определенный модуль.</span><span class="sxs-lookup"><span data-stu-id="4633c-180">They should both reference a pre-defined module.</span></span> <span data-ttu-id="4633c-181">Выходное сообщение модуля `source` перенаправляется в качестве входных данных в модуль `sink`.</span><span class="sxs-lookup"><span data-stu-id="4633c-181">The output message of `source` module is forwarded to the input of `sink` module.</span></span>

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

## <a name="running-the-modules"></a><span data-ttu-id="4633c-182">Запуск модулей</span><span class="sxs-lookup"><span data-stu-id="4633c-182">Running the modules</span></span>
1. `npm install`
2. `npm start`

<span data-ttu-id="4633c-183">Чтобы завершить работу приложения, нажмите клавишу `<Enter>`.</span><span class="sxs-lookup"><span data-stu-id="4633c-183">If you want to terminate the application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4633c-184">Не рекомендуется использовать сочетание клавиш Ctrl + C для завершения работы приложения IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="4633c-184">It is not recommended to use Ctrl + C to terminate the IoT Edge application.</span></span> <span data-ttu-id="4633c-185">Это действие может вызвать аварийное завершение процесса.</span><span class="sxs-lookup"><span data-stu-id="4633c-185">As this way may cause the process to terminate abnormally.</span></span>
