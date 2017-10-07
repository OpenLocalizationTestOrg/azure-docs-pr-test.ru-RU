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
# <a name="create-an-azure-iot-edge-module-with-java"></a>Создание модуля Azure IoT Edge с помощью Java

В этом руководстве показано, как с помощью Java создать модуль для Azure IoT Edge.

В этом учебнике мы рассмотрим настройки среды и как toowrite [ЛЮЧИТЬ](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) модуля преобразователя данных с помощью последних пакетов Azure IoT Edge Maven hello.

## <a name="prerequisites"></a>Предварительные требования

В этом разделе настраивается среда для разработки модуля IoT Edge. Оно применяется tooboth *64-разрядной версии Windows* и *64-разрядных Linux (8 Ubuntu/Debian)* операционных систем.

Привет, следуя программного обеспечения не требуется:

* [клиент Git](https://git-scm.com/downloads);
* [**64-разрядный** пакет JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html);
* [Maven](https://maven.apache.org/install.html).

Открытие командной строки терминалов окна, а также клонировать hello следующие репозитория:

1. `git clone https://github.com/Azure-Samples/iot-edge-samples.git`.
2. `cd iot-edge-samples/java/simulated_ble`

## <a name="overall-architecture"></a>Общая архитектура

Платформа Azure IoT Edge Hello интенсивно использует hello [Von Неймана архитектура](https://en.wikipedia.org/wiki/Von_Neumann_architecture). Означающее этой архитектуры hello всей границы IoT Azure — это система, который обрабатывает ввод и вывод; и каждый отдельный модуль также является очень мала подсистемы ввода вывода. В этом учебнике вы ознакомитесь hello, следующие два модуля:

1. Модуль, который получает имитацию сигнала [BLE](https://en.wikipedia.org/wiki/Bluetooth_Low_Energy) и преобразует его в сообщение в формате [JSON](https://en.wikipedia.org/wiki/JSON).
2. Модуль, который выводит hello получил [JSON](https://en.wikipedia.org/wiki/JSON) сообщения.

Hello следующее изображение hello типичные потока данных начала до конца для этого проекта:

![Поток данных между тремя модулями](media/iot-hub-iot-edge-create-module/dataflow.png "Входные данные: имитация модуля BLE; Процессор: модуль преобразователя; Выходные данные: модуль принтера")

## <a name="understanding-hello-code"></a>Общие сведения о коде hello

### <a name="maven-project-structure"></a>Структура проекта Maven

Так как пакеты Azure IoT Edge основаны на Maven, нам нужно toocreate типичный Maven структуру проекта, который содержит `pom.xml` файла.

Hello POM наследует hello `com.microsoft.azure.gateway.gateway-module-base` пакет, который объявляет все зависимости hello, необходимые в проекте модуля, включая двоичные файлы среды выполнения hello, путь к файлу конфигурации шлюза hello и поведение при выполнении hello. Это избавляет от необходимости много времени и исключить необходимость toowrite hello и снова и снова перепишите сотни строк программного кода.

Мы должны tooupdate pom.xml файла путем объявления hello необходимые зависимости и подключаемые модули и имя hello hello конфигурации файла toobe использовать наши модулем, как показано в следующий фрагмент кода hello.

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

### <a name="basic-understanding-of-an-azure-iot-edge-module"></a>Базовое представление о модуле Azure IoT Edge

Модуль Azure IoT Edge можно рассматривать как обработчик данных, задачей которого является получение входных данных, их обработка и генерирование выходных данных.

Hello входные данные могут быть данные от оборудования (например, Детектор движения), сообщение от других модулей, и любые другие элементы (например, случайное число, периодически созданные таймер).

Hello выходные данные выглядят аналогично toohello входных данных, она может активировать поведением оборудования (например, Индикатор мигает hello), модулей tooother сообщение и любые другие элементы (например, консоль печати toohello).

Модули взаимодействуют друг с другом с помощью класса `com.microsoft.azure.gateway.messaging.Message`. Hello **содержимого** из `Message` — массив байтов, который может представлять любой тип данных, вам нравится. **Свойства** также доступны в hello `Message` и являются просто сопоставление строка строка. Можно сравнивать с **свойства** как hello заголовки в HTTP-запроса или hello метаданные файла.

В порядке toodevelop модуль Azure IoT Edge в Java, вы должны toocreate новый класс модуля, который наследуется от `com.microsoft.azure.gateway.core.GatewayModule` и реализуют абстрактный метод hello необходимые `receive()` и `destroy()`. На этом этапе можно также выбрать дополнительный hello tooimplement `start()` или `create()` также методы. Следующий фрагмент кода Hello показано, как был запущен tooget создания в модуле Azure IoT Edge.

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

### <a name="converter-module"></a>Модуль преобразователя

| Входные данные                    | Процессор                              | Выходные данные                 | Исходный файл            |
| ------------------------ | -------------------------------------- | ---------------------- | ---------------------- |
| Сообщение с данными температуры | Синтаксический анализ и создание сообщения JSON | Структурирование сообщения JSON | `ConverterModule.java` |

Этот модуль является типичным модулем Azure IoT Edge. Она принимает сообщения температуры из других модулей (аппаратного модуля или в данном случае нашей имитацию модуля ЛЮЧИТЬ); а затем нормализует сообщения hello температуры в структурированный tooa сообщение JSON (включая добавления идентификатора сообщения hello, задание для свойства hello ли мы должны tootrigger hello температуры предупреждение и так далее).

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

### <a name="printer-module"></a>Модуль принтера

| Входные данные                          | Процессор | Выходные данные                     | Исходный файл          |
| ------------------------------ | --------- | -------------------------- | -------------------- |
| Любое сообщение от других модулей | Недоступно       | Журнал tooconsole сообщение hello | `PrinterModule.java` |

Это простой, интуитивно понятными, модуль, который выводит окно терминала toohello сообщений hello получено.

```java
@Override
public void receive(Message message) {
  System.out.println(message.toString());
}
```

### <a name="azure-iot-edge-configuration"></a>Конфигурация Azure IoT Edge

Hello последним шагом перед запуском hello модулей является tooconfigure hello Azure IoT Edge и tooestablish hello соединения между модулями.

Сначала мы должны toodeclare нашей загрузчика Java (с момента загрузчиков поддерживает Azure IoT Edge на различных языках) которого может ссылаться на его `name` в разделах hello позже.

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

После объявления нашей загрузчиков мы также потребуется toodeclare также нашей модулей. Аналогичные загрузчиков hello toodeclaring, они могут также ссылаться их `name` атрибута. При объявлении модуля, нам нужно toospecify hello загрузчика следует использовать (который должен быть hello один мы определили перед) и hello точки входа (должно быть имя класса нормализованный hello нашей модуля) для каждого модуля. Hello `simulated_device` собственный модуль, включенной в пакет среды выполнения core hello Azure IoT Edge. Следует всегда включать `args` в файл JSON, даже если это hello `null`.

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

В конце конфигурации hello hello мы устанавливать подключения hello. Каждое подключение выражается с помощью `source` и `sink`. Оба этих параметра должны ссылаться на предварительно определенный модуль. Выходное сообщение Hello объекта `source` toohello входные данные будут пересылаться модуля `sink` модуля.

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

## <a name="running-hello-modules"></a>Запуск модулей hello

Используйте `mvn package` toobuild все данные в hello `target/` папки. Для чистоты сборки также рекомендуется использовать `mvn clean package`.

Используйте `mvn exec:exec` toorun hello Azure IoT Edge и вы должны соблюдаться, консоль печатной toohello по фиксированной ставке температур hello и все свойства hello.

Приложение hello tooterminate нажмите `<Enter>` ключа.

> [!IMPORTANT]
> Не рекомендуется toouse Ctrl + C tooterminate hello IoT пограничного шлюза приложения. Как это может привести к tooterminate hello процесса аварийно.

