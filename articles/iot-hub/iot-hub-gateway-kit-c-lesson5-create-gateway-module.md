---
title: "aaaCreate модуля первого шлюза Azure IoT | Документы Microsoft"
description: "Создайте модуль и добавьте его tooa образец приложения toocustomize модуль поведения."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: 
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cd7660f4-7b8b-4091-8d71-bb8723165b0b
ms.service: iot-hub
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 48996fc026c8b708e328b5629801465810e5b6a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a>Урок 5. Создание первого модуля шлюза Azure IoT
Край IoT Azure позволяет toobuild модули, написанные на языке Java, Node.js или .NET, этот учебник знакомит hello действия по созданию модуля на языке C.

## <a name="what-you-will-do"></a>Выполняемая задача

- Скомпилируйте и запустите пример приложения hello hello_world на Intel NUC.
- Создание модуля и его компиляция на Intel NUC.
- Добавьте пример приложения hello новый модуль toohello hello_world и запустите образец hello Intel NUC. новый модуль Hello выводит сообщения «hello_world» с меткой времени.

## <a name="what-you-will-learn"></a>Новые знания

- Как toocompile и выполнение примера приложения на Intel NUC.
- Как toocreate модуля.
- Как tooa модуль tooadd пример приложения.

## <a name="what-you-need"></a>Необходимые элементы

Edge Интернета вещей Azure, установленный на главном компьютере.

## <a name="folder-structure"></a>Структура папок

Hello занятия 5 во вложенной папке hello примером кода, который клонировать на занятии 1, является `module` папки и `sample` папки.

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- Hello `module/my_module` папка содержит hello исходного кода и сценариев toobuild hello модуля.
- Hello `sample` папка содержит hello исходного кода и сценариев toobuild hello образца приложения.

## <a name="compile-and-run-hello-helloworld-sample-app-on-intel-nuc"></a>Компиляция и выполнение примера приложения hello hello_world на Intel NUC

Hello `hello_world` образец создает шлюз, на основании hello `hello_world.json` файл, который указывает стандартные модули, два hello связанные с приложение hello. Hello журналы событий шлюза файл tooa сообщение «hello world» каждые 5 секунд. В этом разделе, компиляцией и выполнением hello `hello_world` приложения с ее модуля по умолчанию.

toocompile и выполнения hello `hello_world` приложения, выполните следующие действия на компьютере узла:

1. Инициализируйте hello файлы конфигурации, выполнив следующие команды hello:

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. Измените файл конфигурации шлюза hello hello Intel NUC MAC-адрес. Пропустите этот шаг, если вы прошли занятие hello слишком[настройки и запуска образца приложения ЛЮЧИТЬ][config_ble].

   1. Откройте файл конфигурации шлюза hello, выполнив следующую команду hello:

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. Обновление hello шлюза MAC-адресов при вы [Настройка NUC Intel как шлюз IoT][setup_nuc], а затем сохраните файл hello.

1. Скомпилируйте исходный код образца hello, выполнив следующую команду hello:

   ```bash
   gulp compile
   ```

   Hello команда передает hello Образец исходного кода tooIntel NUC и выполняет `build.sh` toocompile его.

1. Запустите hello `hello_world` приложение на Intel NUC, выполнив следующую команду hello:

   ```bash
   gulp run
   ```

   Здравствуйте, команда запускает `../Tools/run-hello-world.js` , указанным в `config.json` toostart hello пример приложения на Intel NUC.

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a>Создание нового модуля и его компиляция на Intel NUC

Приведенные ниже действия Hello поможет создать новый модуль и его компиляция Intel NUC. модуль Hello выводит сообщения с меткой времени после их получения. В этом разделе вы создадите первый настроенный модуль шлюза.

Любой модуль Azure IoT Edge необходимо реализовать hello следующие интерфейсы:

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

При необходимости можно реализовать следующий интерфейс hello.

   ```C
   pfModule_Start Module_Start
   ```

Hello следующей диаграмме показаны пути hello важные состояния модуля. Hello квадратный прямоугольники представляют методы, которые реализуют операции tooperform при перемещении модуля hello между состояниями. Hello овалы-это основной номер состояния, hello модуля может находиться в.

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

Теперь давайте создадим на основе шаблона hello модуля:

1. Откройте папку hello шаблона, выполнив следующую команду hello:

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - `src/my_module.c`служит в качестве шаблона, который упрощает создание hello модуля. Hello шаблона объявляет hello интерфейсов. Все что нужно toodo — toohello логику tooadd `MyModule_Receive` функции.
   - `build.sh`Представляет модуль hello toocompile скрипт построения hello на Intel NUC.
1. Откройте hello `src/my_module.c` файла и ввести два файла заголовков:

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. Добавьте следующий код toohello hello `MyModule_Receive` функции:

   ```C
   if (message == NULL)
   {
      LogError("invalid arg message");
   }
   else
   {
      // get hello message content
      const CONSTBUFFER * content = Message_GetContent(message);
      // get hello local time and format it
      time_t temp = time(NULL);
      if (temp == (time_t)-1)
      {
          LogError("time function failed");
      }
      else
      {
          struct tm* t = localtime(&temp);
          if (t == NULL)
          {
              LogError("localtime failed");
          }
          else
          {
              char timetemp[80] = { 0 };
              if (strftime(timetemp, sizeof(timetemp) / sizeof(timetemp[0]), "%c", t) == 0)
              {
                  LogError("unable toostrftime");
              }
              else
              {
                  printf("[%s] %.*s\r\n", timetemp, (int)content->size, content->buffer);
              }
          }
      }
   }
   ```

1. Обновление hello `config.json` файл toospecify hello `workspace` папку на путь узла компьютера и hello развертывания на Intel NUC. Во время компиляции, hello файлы в hello `workspace` папка будет переносятся toohello пути развертывания.

   1. Откройте hello `config.json` файл, выполнив следующую команду hello:

      ```bash
      code config.json
      ```

   1. Обновление `config.json` с hello следующая конфигурация:

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. Скомпилируйте модуль hello, выполнив следующую команду hello:

   ```bash
   gulp compile
   ```

   Hello команда передает hello исходного кода tooIntel NUC и выполняет `build.sh` toocompile hello модуля.

## <a name="add-hello-module-toohello-helloworld-sample-app-and-run-hello-app-on-intel-nuc"></a>Добавить hello модуля toohello hello_world пример приложения и запустить приложение hello на Intel NUC

tooperform это задача, выполните следующие действия:

1. Перечислить все двоичные файлы модуля доступны hello (.so-файлы) на Intel NUC, выполнив следующую команду hello:

   ```bash
   gulp modules --list
   ```

   Hello путь к двоичным файлам `my_module` , скомпилирован должен быть указан как показано ниже:

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   При изменении пользователя для входа по умолчанию hello в `config-gateway.json`, путь к двоичным файлам hello начинается с `home/<your username>` вместо `root`.

1. Добавить `my_module` toohello `hello_world` пример приложения:

   1. Откройте hello `hello_world.json` файл, выполнив следующую команду hello:

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. Добавьте следующий код toohello hello `modules` раздела:

      ```json
      {
       "name": "my_module",
       "loader": {
       "name": "native",
       "entrypoint": {
       "module.path": "/root/gateway_sample/module/my_module/build/libmy_module.so"
         }
        },
       "args": null
      }
      ```

      Здравствуйте, значение `module.path` должно быть `/root/gateway_sample/module/my_module/build/libmy_module.so`. Hello код объявляет `my_module` toobe, связанный с hello шлюза, а также расположение hello hello двоичного модуля, указанного в `module.path`.
   1. Добавьте следующий код toohello hello `links` раздела:

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      Этот код указывает, что сообщения передаются из hello `hello_world` модуль слишком`my_module`.

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. Запустите hello `hello_world` пример приложения, выполнив следующую команду hello:

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   Hello `--config` параметр предписывает hello `run-hello-world.js` сценария с помощью hello toorun `hello_world.json` файл.

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

Поздравляем! Теперь можно увидеть поведение hello этого модуля, он просто выводит сообщения «hello world» с меткой времени, другой результат от исходного модуля «hello_world» hello.

## <a name="next-steps"></a>Дальнейшие действия

Создан новый модуль, добавленные его образец hello_world toohello и toorun get hello пример приложения hello новый модуль на шлюзе. Дополнительные сведения о модулях шлюза Azure IoT toolearn следует Дополнительные примеры модуля здесь можно найти: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
