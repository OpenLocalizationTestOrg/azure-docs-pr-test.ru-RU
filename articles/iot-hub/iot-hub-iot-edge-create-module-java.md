---
title: "Модуль Edge IoT Azure с Java aaaCreate | Документы Microsoft"
description: "Этот учебник демонстрирует, как преобразователь данных ЛЮЧИТЬ при помощи модуля toowrite hello последние пакеты Azure IoT Edge Maven."
services: iot-hub
author: junyi
manager: timlt
ms.service: iot-hub
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 06/28/2017
ms.author: junyi
ms.openlocfilehash: abb560933d13d133ae9a1da08b503d5735b230e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-iot-edge-module-with-java"></a><span data-ttu-id="ae384-103">Создание модуля Azure IoT Edge с помощью Java</span><span class="sxs-lookup"><span data-stu-id="ae384-103">Create an Azure IoT Edge Module with Java</span></span>

<span data-ttu-id="ae384-104">В этом руководстве показано, как с помощью Java создать модуль для Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="ae384-104">This tutorial showcases how one might build a module for Azure IoT Edge in Java.</span></span>

<span data-ttu-id="ae384-105">В этом учебнике мы рассмотрим настройки среды и как toowrite [ЛЮЧИТЬ](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) модуля преобразователя данных с помощью последних пакетов Azure IoT Edge Maven hello.</span><span class="sxs-lookup"><span data-stu-id="ae384-105">In this tutorial, we will walk through environment setup and how toowrite a [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) data converter module using hello latest Azure IoT Edge Maven packages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae384-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ae384-106">Prerequisites</span></span>

<span data-ttu-id="ae384-107">В этом разделе настраивается среда для разработки модуля IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="ae384-107">In this section, you will set up your environment for IoT Edge module development.</span></span> <span data-ttu-id="ae384-108">Оно применяется tooboth *64-разрядной версии Windows* и *64-разрядных Linux (8 Ubuntu/Debian)* операционных систем.</span><span class="sxs-lookup"><span data-stu-id="ae384-108">It applies tooboth *64-bit Windows* and *64-bit Linux (Ubuntu/Debian 8)* operating systems.</span></span>

<span data-ttu-id="ae384-109">Привет, следуя программного обеспечения не требуется:</span><span class="sxs-lookup"><span data-stu-id="ae384-109">hello following software is required:</span></span>

* <span data-ttu-id="ae384-110">[клиент Git](https://git-scm.com/downloads);</span><span class="sxs-lookup"><span data-stu-id="ae384-110">[Git Client](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="ae384-111">[**64-разрядный** пакет JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html);</span><span class="sxs-lookup"><span data-stu-id="ae384-111">[**x64** JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
* <span data-ttu-id="ae384-112">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="ae384-112">[Maven](https://maven.apache.org/install.html).</span></span>

<span data-ttu-id="ae384-113">Открытие командной строки терминалов окна, а также клонировать hello следующие репозитория:</span><span class="sxs-lookup"><span data-stu-id="ae384-113">Open a command-line terminal window and clone hello following repository:</span></span>

1. <span data-ttu-id="ae384-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span><span class="sxs-lookup"><span data-stu-id="ae384-114">`git clone https://github.com/Azure-Samples/iot-edge-samples.git`.</span></span>
2. `cd iot-edge-samples/java/simulated_ble`

## <a name="overall-architecture"></a><span data-ttu-id="ae384-115">Общая архитектура</span><span class="sxs-lookup"><span data-stu-id="ae384-115">Overall architecture</span></span>

<span data-ttu-id="ae384-116">Платформа Azure IoT Edge Hello интенсивно использует hello [Von Неймана архитектура](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span><span class="sxs-lookup"><span data-stu-id="ae384-116">hello Azure IoT Edge platform heavily adopts hello [Von Neumann architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture).</span></span> <span data-ttu-id="ae384-117">Означающее этой архитектуры hello всей границы IoT Azure — это система, который обрабатывает ввод и вывод; и каждый отдельный модуль также является очень мала подсистемы ввода вывода.</span><span class="sxs-lookup"><span data-stu-id="ae384-117">Which means that hello entire Azure IoT Edge architecture is a system which processes input and produces output; and that each individual module is also a tiny input-output subsystem.</span></span> <span data-ttu-id="ae384-118">В этом учебнике вы ознакомитесь hello, следующие два модуля:</span><span class="sxs-lookup"><span data-stu-id="ae384-118">In this tutorial, we will introduce hello following two modules:</span></span>

1. <span data-ttu-id="ae384-119">Модуль, который получает имитацию сигнала [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) и преобразует его в сообщение в формате [JSON](https://en.wikipedia.org/wiki/JSON).</span><span class="sxs-lookup"><span data-stu-id="ae384-119">A module which receives a simulated [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) signal and converts it into a formatted [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>
2. <span data-ttu-id="ae384-120">Модуль, который выводит hello получил [JSON](https://en.wikipedia.org/wiki/JSON) сообщения.</span><span class="sxs-lookup"><span data-stu-id="ae384-120">A module which prints hello received [JSON](https://en.wikipedia.org/wiki/JSON) message.</span></span>

<span data-ttu-id="ae384-121">Hello следующее изображение hello типичные потока данных начала до конца для этого проекта:</span><span class="sxs-lookup"><span data-stu-id="ae384-121">hello following image displays hello typical end-to-end dataflow for this project:</span></span>

<span data-ttu-id="ae384-122">![Поток данных между тремя модулями](media/iot-hub-iot-edge-create-module/dataflow.png "Входные данные: имитация модуля BLE; Процессор: модуль преобразователя; Выходные данные: модуль принтера")</span><span class="sxs-lookup"><span data-stu-id="ae384-122">![Dataflow between three modules](media/iot-hub-iot-edge-create-module/dataflow.png "Input: Simulated BLE Module; Processor: Converter Module; Output: Printer Module")</span></span>

## <a name="understanding-hello-code"></a><span data-ttu-id="ae384-123">Общие сведения о коде hello</span><span class="sxs-lookup"><span data-stu-id="ae384-123">Understanding hello code</span></span>

### <a name="maven-project-structure"></a><span data-ttu-id="ae384-124">Структура проекта Maven</span><span class="sxs-lookup"><span data-stu-id="ae384-124">Maven project structure</span></span>

<span data-ttu-id="ae384-125">Так как пакеты Azure IoT Edge основаны на Maven, нам нужно toocreate типичный Maven структуру проекта, который содержит `pom.xml` файла.</span><span class="sxs-lookup"><span data-stu-id="ae384-125">Since Azure IoT Edge packages are based on Maven, we need toocreate a typical Maven project structure, which contains a `pom.xml` file.</span></span>

<span data-ttu-id="ae384-126">Hello POM наследует hello `com.microsoft.azure.gateway.gateway-module-base` пакет, который объявляет все зависимости hello, необходимые в проекте модуля, включая двоичные файлы среды выполнения hello, путь к файлу конфигурации шлюза hello и поведение при выполнении hello.</span><span class="sxs-lookup"><span data-stu-id="ae384-126">hello POM inherits from hello `com.microsoft.azure.gateway.gateway-module-base` package, which declares all of hello dependencies needed by a module project which includes hello runtime binaries, hello gateway configuration file path, and hello execution behavior.</span></span> <span data-ttu-id="ae384-127">Это избавляет от необходимости много времени и исключить необходимость toowrite hello и снова и снова перепишите сотни строк программного кода.</span><span class="sxs-lookup"><span data-stu-id="ae384-127">This saves us lots of time and eliminate hello need toowrite and rewrite hundreds of lines of code over and over again.</span></span>

<span data-ttu-id="ae384-128">Мы должны tooupdate pom.xml файла путем объявления hello необходимые зависимости и подключаемые модули и имя hello hello конфигурации файла toobe использовать наши модулем, как показано в следующий фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="ae384-128">We need tooupdate the pom.xml file by declaring hello required dependencies/plugins and hello name of hello configuration file toobe used by our module as shown in hello following code snippet.</span></span>

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <!-- Inherit from parent -->
  <parent>
    <groupId>com.microsoft.azure.gateway</groupId>
    <artifactId>gateway-module-base</artifactId>
    <version>1.0.1</version>
  </parent>
  
  <groupId>com.microsoft.azure.gateway</groupId>
  <artifactId>ble-converter</artifactId>
  <version>1.0</version>
  <packaging>jar</packaging>

  <!-- Set hello filename of hello Azure IoT Edge configuration located
       under ./src/main/resources/gateway/ which is used in parent -->
  <properties>
    <gw.config.fileName>gw-config.json</gw.config.fileName>
  </properties>

  <!-- Re-declare dependencies used in parent -->
  <dependencies>
    <dependency>
      <groupId>com.microsoft.azure.gateway</groupId>
      <artifactId>gateway-java-binding</artifactId>
    </dependency>
    <dependency>
      <groupId>${dependency.runtime.group}</groupId>
      <artifactId>${dependency.runtime.name}</artifactId>
    </dependency>
  </dependencies>

  <!-- Re-declare plugins used in parent -->
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-dependency-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-resources-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-shade-plugin</artifactId>
      </plugin>
      <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>exec-maven-plugin</artifactId>
      </plugin>
    </plugins>
  </build>
</project>
```

### <a name="basic-understanding-of-an-azure-iot-edge-module"></a><span data-ttu-id="ae384-129">Базовое представление о модуле Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="ae384-129">Basic understanding of an Azure IoT Edge module</span></span>

<span data-ttu-id="ae384-130">Модуль Azure IoT Edge можно рассматривать как обработчик данных, задачей которого является получение входных данных, их обработка и генерирование выходных данных.</span><span class="sxs-lookup"><span data-stu-id="ae384-130">You can treat an Azure IoT Edge module as a data processor whose job is to: receive input, process it, and produce output.</span></span>

<span data-ttu-id="ae384-131">Hello входные данные могут быть данные от оборудования (например, Детектор движения), сообщение от других модулей, и любые другие элементы (например, случайное число, периодически созданные таймер).</span><span class="sxs-lookup"><span data-stu-id="ae384-131">hello input might be data from hardware (like a motion detector), a message from other modules, or anything else (like a random number generated periodically by a timer).</span></span>

<span data-ttu-id="ae384-132">Hello выходные данные выглядят аналогично toohello входных данных, она может активировать поведением оборудования (например, Индикатор мигает hello), модулей tooother сообщение и любые другие элементы (например, консоль печати toohello).</span><span class="sxs-lookup"><span data-stu-id="ae384-132">hello output is similar toohello input, it could trigger hardware behavior (like hello blinking LED), a message tooother modules, or anything else (like printing toohello console).</span></span>

<span data-ttu-id="ae384-133">Модули взаимодействуют друг с другом с помощью класса `com.microsoft.azure.gateway.messaging.Message`.</span><span class="sxs-lookup"><span data-stu-id="ae384-133">Modules communicate with each other using `com.microsoft.azure.gateway.messaging.Message` class.</span></span> <span data-ttu-id="ae384-134">Hello **содержимого** из `Message` — массив байтов, который может представлять любой тип данных, вам нравится.</span><span class="sxs-lookup"><span data-stu-id="ae384-134">hello **Content** of a `Message` is a byte array which is capable of representing any kind of data you like.</span></span> <span data-ttu-id="ae384-135">**Свойства** также доступны в hello `Message` и являются просто сопоставление строка строка.</span><span class="sxs-lookup"><span data-stu-id="ae384-135">**Properties** are also available in hello `Message` and are simply a string-to-string mapping.</span></span> <span data-ttu-id="ae384-136">Можно сравнивать с **свойства** как hello заголовки в HTTP-запроса или hello метаданные файла.</span><span class="sxs-lookup"><span data-stu-id="ae384-136">You may think of **Properties** as hello headers in an HTTP request, or hello metadata of a file.</span></span>

<span data-ttu-id="ae384-137">В порядке toodevelop модуль Azure IoT Edge в Java, вы должны toocreate новый класс модуля, который наследуется от `com.microsoft.azure.gateway.core.GatewayModule` и реализуют абстрактный метод hello необходимые `receive()` и `destroy()`.</span><span class="sxs-lookup"><span data-stu-id="ae384-137">In order toodevelop an Azure IoT Edge module in Java, you need toocreate a new module class which inherits from `com.microsoft.azure.gateway.core.GatewayModule` and implement hello required abstract methods `receive()` and `destroy()`.</span></span> <span data-ttu-id="ae384-138">На этом этапе можно также выбрать дополнительный hello tooimplement `start()` или `create()` также методы.</span><span class="sxs-lookup"><span data-stu-id="ae384-138">At this point, you may also choose tooimplement hello optional `start()` or `create()` methods as well.</span></span> <span data-ttu-id="ae384-139">Следующий фрагмент кода Hello показано, как был запущен tooget создания в модуле Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="ae384-139">hello following code snippet shows you how tooget started authoring an Azure IoT Edge module.</span></span>

```java
import com.microsoft.azure.gateway.core.Broker;
import com.microsoft.azure.gateway.core.GatewayModule;
import com.microsoft.azure.gateway.messaging.Message;

public class MyEdgeModule extends GatewayModule {
  public MyEdgeModule(long address, Broker broker, String configuration) {
    /* Let hello GatewayModule do hello dirty work of initialization. It's also
       a good time tooparse your own configuration defined in Azure IoT Edge
       configuration file (typically ./src/main/resources/gateway/gw-config.json) */
    super(address, broker, configuration);
  }

  @Override
  public void start() {
    /* Acquire hello resources you need. If you don't
       need any resources, you may omit this method. */
  }

  @Override
  public void destroy() {
    /* It's time toorelease all resources. This method is required. */
  }

  @Override
  public void receive(Message message) {
    /* Logic tooprocess hello input message. This method is required. */
    // ...
    /* Use publish() method toodo hello output. You are
       allowed toopublish your new Message instance. */
    this.publish(message);
  }
}
```

### <a name="converter-module"></a><span data-ttu-id="ae384-140">Модуль преобразователя</span><span class="sxs-lookup"><span data-stu-id="ae384-140">Converter module</span></span>

| <span data-ttu-id="ae384-141">Входные данные</span><span class="sxs-lookup"><span data-stu-id="ae384-141">Input</span></span>                    | <span data-ttu-id="ae384-142">Процессор</span><span class="sxs-lookup"><span data-stu-id="ae384-142">Processor</span></span>                              | <span data-ttu-id="ae384-143">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="ae384-143">Output</span></span>                 | <span data-ttu-id="ae384-144">Исходный файл</span><span class="sxs-lookup"><span data-stu-id="ae384-144">Source File</span></span>            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| <span data-ttu-id="ae384-145">Сообщение с данными температуры</span><span class="sxs-lookup"><span data-stu-id="ae384-145">Temperature data message</span></span> | <span data-ttu-id="ae384-146">Синтаксический анализ и создание сообщения JSON</span><span class="sxs-lookup"><span data-stu-id="ae384-146">Parse and construct a new JSON message</span></span> | <span data-ttu-id="ae384-147">Структурирование сообщения JSON</span><span class="sxs-lookup"><span data-stu-id="ae384-147">Structure JSON message</span></span> | `ConverterModule.java` |

<span data-ttu-id="ae384-148">Этот модуль является типичным модулем Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="ae384-148">This module is a typical Azure IoT Edge module.</span></span> <span data-ttu-id="ae384-149">Она принимает сообщения температуры из других модулей (аппаратного модуля или в данном случае нашей имитацию модуля ЛЮЧИТЬ); а затем нормализует сообщения hello температуры в структурированный tooa сообщение JSON (включая добавления идентификатора сообщения hello, задание для свойства hello ли мы должны tootrigger hello температуры предупреждение и так далее).</span><span class="sxs-lookup"><span data-stu-id="ae384-149">It accepts temperature messages from other modules (a hardware module, or in this case our simulated BLE module); and then normalizes hello temperature message in tooa structured JSON message (including appending hello message ID, setting hello property of whether we need tootrigger hello temperature alert, and so on).</span></span>

```java
@Override
public void receive(Message message) {
  try {
    JSONObject messageFromBle = new JSONObject(new String(message.getContent()));
    double temperature = messageFromBle.getDouble("temperature");
    Map<String, String> inputProperties = message.getProperties();

    HashMap<String, String> properties = new HashMap<>();
    properties.put("source", inputProperties.get("source"));
    properties.put("macAddress", inputProperties.get("macAddress"));
    properties.put("temperatureAlert", temperature > 30 ? "true" : "false");

    String content = String.format(
        "{ \"deviceId\": \"Intel NUC Gateway\", \"messageId\": %d, \"temperature\": %f }",
        ++this.messageCount, temperature);

    this.publish(new Message(content.getBytes(), properties));
  } catch (Exception ex) {
    ex.printStackTrace();
  }
}
```

### <a name="printer-module"></a><span data-ttu-id="ae384-150">Модуль принтера</span><span class="sxs-lookup"><span data-stu-id="ae384-150">Printer module</span></span>

| <span data-ttu-id="ae384-151">Входные данные</span><span class="sxs-lookup"><span data-stu-id="ae384-151">Input</span></span>                          | <span data-ttu-id="ae384-152">Процессор</span><span class="sxs-lookup"><span data-stu-id="ae384-152">Processor</span></span> | <span data-ttu-id="ae384-153">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="ae384-153">Output</span></span>                     | <span data-ttu-id="ae384-154">Исходный файл</span><span class="sxs-lookup"><span data-stu-id="ae384-154">Source File</span></span>          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| <span data-ttu-id="ae384-155">Любое сообщение от других модулей</span><span class="sxs-lookup"><span data-stu-id="ae384-155">Any message from other modules</span></span> | <span data-ttu-id="ae384-156">Недоступно</span><span class="sxs-lookup"><span data-stu-id="ae384-156">N/A</span></span>       | <span data-ttu-id="ae384-157">Журнал tooconsole сообщение hello</span><span class="sxs-lookup"><span data-stu-id="ae384-157">Log hello message tooconsole</span></span> | `PrinterModule.java` |

<span data-ttu-id="ae384-158">Это простой, интуитивно понятными, модуль, который выводит окно терминала toohello сообщений hello получено.</span><span class="sxs-lookup"><span data-stu-id="ae384-158">This is a simple, self-explanatory, module which outputs hello received messages toohello terminal window.</span></span>

```java
@Override
public void receive(Message message) {
  System.out.println(message.toString());
}
```

### <a name="azure-iot-edge-configuration"></a><span data-ttu-id="ae384-159">Конфигурация Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="ae384-159">Azure IoT Edge configuration</span></span>

<span data-ttu-id="ae384-160">Hello последним шагом перед запуском hello модулей является tooconfigure hello Azure IoT Edge и tooestablish hello соединения между модулями.</span><span class="sxs-lookup"><span data-stu-id="ae384-160">hello final step before running hello modules is tooconfigure hello Azure IoT Edge and tooestablish hello connections between modules.</span></span>

<span data-ttu-id="ae384-161">Сначала мы должны toodeclare нашей загрузчика Java (с момента загрузчиков поддерживает Azure IoT Edge на различных языках) которого может ссылаться на его `name` в разделах hello позже.</span><span class="sxs-lookup"><span data-stu-id="ae384-161">First we need toodeclare our Java loader (since Azure IoT Edge supports loaders of different languages) which could be referenced by its `name` in hello sections afterward.</span></span>

```json
"loaders": [{
  "type": "java",
  "name": "java",
  "configuration": {
    "jvm.options": {
      "library.path": "./"
    }
  }
}]
```

<span data-ttu-id="ae384-162">После объявления нашей загрузчиков мы также потребуется toodeclare также нашей модулей.</span><span class="sxs-lookup"><span data-stu-id="ae384-162">Once we have declared our loaders, we will also need toodeclare our modules as well.</span></span> <span data-ttu-id="ae384-163">Аналогичные загрузчиков hello toodeclaring, они могут также ссылаться их `name` атрибута.</span><span class="sxs-lookup"><span data-stu-id="ae384-163">Similar toodeclaring hello loaders, they can also be referenced by their `name` attribute.</span></span> <span data-ttu-id="ae384-164">При объявлении модуля, нам нужно toospecify hello загрузчика следует использовать (который должен быть hello один мы определили перед) и hello точки входа (должно быть имя класса нормализованный hello нашей модуля) для каждого модуля.</span><span class="sxs-lookup"><span data-stu-id="ae384-164">When declaring a module, we need toospecify hello loader it should use (which should be hello one we defined before) and hello entry-point (should be hello normalized class name of our module) for each module.</span></span> <span data-ttu-id="ae384-165">Hello `simulated_device` собственный модуль, включенной в пакет среды выполнения core hello Azure IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="ae384-165">hello `simulated_device` module is a native module which is included in hello Azure IoT Edge core runtime package.</span></span> <span data-ttu-id="ae384-166">Следует всегда включать `args` в файл JSON, даже если это hello `null`.</span><span class="sxs-lookup"><span data-stu-id="ae384-166">You should always include `args` in hello JSON file even if it is `null`.</span></span>

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
      "name": "java",
      "entrypoint": {
        "class.name": "com/microsoft/azure/gateway/ConverterModule",
        "class.path": "./ble-converter-1.0-with-deps.jar"
      }
    },
    "args": null
  },
  {
    "name": "print",
    "loader": {
      "name": "java",
      "entrypoint": {
        "class.name": "com/microsoft/azure/gateway/PrinterModule",
        "class.path": "./ble-converter-1.0-with-deps.jar"
      }
    },
    "args": null
  }
]
```

<span data-ttu-id="ae384-167">В конце конфигурации hello hello мы устанавливать подключения hello.</span><span class="sxs-lookup"><span data-stu-id="ae384-167">At hello end of hello configuration, we establish hello connections.</span></span> <span data-ttu-id="ae384-168">Каждое подключение выражается с помощью `source` и `sink`.</span><span class="sxs-lookup"><span data-stu-id="ae384-168">Each connection is expressed by `source` and `sink`.</span></span> <span data-ttu-id="ae384-169">Оба этих параметра должны ссылаться на предварительно определенный модуль.</span><span class="sxs-lookup"><span data-stu-id="ae384-169">They should both reference a pre-defined module.</span></span> <span data-ttu-id="ae384-170">Выходное сообщение Hello объекта `source` toohello входные данные будут пересылаться модуля `sink` модуля.</span><span class="sxs-lookup"><span data-stu-id="ae384-170">hello output message of `source` module will be forwarded toohello input of `sink` module.</span></span>

```json
"links": [
  {
    "source": "simulated_device",
    "sink": "converter"
  },
  {
    "source": "converter",
    "sink": "print"
  }
]
```

## <a name="running-hello-modules"></a><span data-ttu-id="ae384-171">Запуск модулей hello</span><span class="sxs-lookup"><span data-stu-id="ae384-171">Running hello modules</span></span>

<span data-ttu-id="ae384-172">Используйте `mvn package` toobuild все данные в hello `target/` папки.</span><span class="sxs-lookup"><span data-stu-id="ae384-172">Use `mvn package` toobuild everything into hello `target/` folder.</span></span> <span data-ttu-id="ae384-173">Для чистоты сборки также рекомендуется использовать `mvn clean package`.</span><span class="sxs-lookup"><span data-stu-id="ae384-173">`mvn clean package` is also recommended for a clean build.</span></span>

<span data-ttu-id="ae384-174">Используйте `mvn exec:exec` toorun hello Azure IoT Edge и вы должны соблюдаться, консоль печатной toohello по фиксированной ставке температур hello и все свойства hello.</span><span class="sxs-lookup"><span data-stu-id="ae384-174">Use `mvn exec:exec` toorun hello Azure IoT Edge and you should observe that hello temperature data and all hello properties are printed toohello console at a fixed rate.</span></span>

<span data-ttu-id="ae384-175">Приложение hello tooterminate нажмите `<Enter>` ключа.</span><span class="sxs-lookup"><span data-stu-id="ae384-175">If you want tooterminate hello application, press `<Enter>` key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ae384-176">Не рекомендуется toouse Ctrl + C tooterminate hello IoT пограничного шлюза приложения.</span><span class="sxs-lookup"><span data-stu-id="ae384-176">It is not recommended toouse Ctrl + C tooterminate hello IoT Edge gateway application.</span></span> <span data-ttu-id="ae384-177">Как это может привести к tooterminate hello процесса аварийно.</span><span class="sxs-lookup"><span data-stu-id="ae384-177">As this may cause hello process tooterminate abnormally.</span></span>

