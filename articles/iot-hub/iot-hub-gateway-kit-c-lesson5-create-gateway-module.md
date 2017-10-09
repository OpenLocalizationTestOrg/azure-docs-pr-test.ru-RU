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
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a><span data-ttu-id="eb108-103">Урок 5. Создание первого модуля шлюза Azure IoT</span><span class="sxs-lookup"><span data-stu-id="eb108-103">Lesson 5: Create your first Azure IoT Gateway module</span></span>
<span data-ttu-id="eb108-104">Край IoT Azure позволяет toobuild модули, написанные на языке Java, Node.js или .NET, этот учебник знакомит hello действия по созданию модуля на языке C.</span><span class="sxs-lookup"><span data-stu-id="eb108-104">While Azure IoT Edge allows you toobuild modules written in Java, .NET, or Node.js, this tutorial walks you through hello steps for building a module in C.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="eb108-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="eb108-105">What you will do</span></span>

- <span data-ttu-id="eb108-106">Скомпилируйте и запустите пример приложения hello hello_world на Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="eb108-106">Compile and run hello hello_world sample app on Intel NUC.</span></span>
- <span data-ttu-id="eb108-107">Создание модуля и его компиляция на Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="eb108-107">Create a module and compile it on Intel NUC.</span></span>
- <span data-ttu-id="eb108-108">Добавьте пример приложения hello новый модуль toohello hello_world и запустите образец hello Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="eb108-108">Add hello new module toohello hello_world sample app and then run hello sample on Intel NUC.</span></span> <span data-ttu-id="eb108-109">новый модуль Hello выводит сообщения «hello_world» с меткой времени.</span><span class="sxs-lookup"><span data-stu-id="eb108-109">hello new module prints out "hello_world" messages with a timestamp.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="eb108-110">Новые знания</span><span class="sxs-lookup"><span data-stu-id="eb108-110">What you will learn</span></span>

- <span data-ttu-id="eb108-111">Как toocompile и выполнение примера приложения на Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="eb108-111">How toocompile and run a sample app on Intel NUC.</span></span>
- <span data-ttu-id="eb108-112">Как toocreate модуля.</span><span class="sxs-lookup"><span data-stu-id="eb108-112">How toocreate a module.</span></span>
- <span data-ttu-id="eb108-113">Как tooa модуль tooadd пример приложения.</span><span class="sxs-lookup"><span data-stu-id="eb108-113">How tooadd module tooa sample app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="eb108-114">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="eb108-114">What you need</span></span>

<span data-ttu-id="eb108-115">Edge Интернета вещей Azure, установленный на главном компьютере.</span><span class="sxs-lookup"><span data-stu-id="eb108-115">Azure IoT Edge that has been installed on your host computer.</span></span>

## <a name="folder-structure"></a><span data-ttu-id="eb108-116">Структура папок</span><span class="sxs-lookup"><span data-stu-id="eb108-116">Folder structure</span></span>

<span data-ttu-id="eb108-117">Hello занятия 5 во вложенной папке hello примером кода, который клонировать на занятии 1, является `module` папки и `sample` папки.</span><span class="sxs-lookup"><span data-stu-id="eb108-117">In hello Lesson 5 subfolder of hello sample code which you cloned in lesson 1, there is a `module` folder and a `sample` folder.</span></span>

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- <span data-ttu-id="eb108-119">Hello `module/my_module` папка содержит hello исходного кода и сценариев toobuild hello модуля.</span><span class="sxs-lookup"><span data-stu-id="eb108-119">hello `module/my_module` folder contains hello source code and script toobuild hello module.</span></span>
- <span data-ttu-id="eb108-120">Hello `sample` папка содержит hello исходного кода и сценариев toobuild hello образца приложения.</span><span class="sxs-lookup"><span data-stu-id="eb108-120">hello `sample` folder contains hello source code and script toobuild hello sample app.</span></span>

## <a name="compile-and-run-hello-helloworld-sample-app-on-intel-nuc"></a><span data-ttu-id="eb108-121">Компиляция и выполнение примера приложения hello hello_world на Intel NUC</span><span class="sxs-lookup"><span data-stu-id="eb108-121">Compile and run hello hello_world sample app on Intel NUC</span></span>

<span data-ttu-id="eb108-122">Hello `hello_world` образец создает шлюз, на основании hello `hello_world.json` файл, который указывает стандартные модули, два hello связанные с приложение hello.</span><span class="sxs-lookup"><span data-stu-id="eb108-122">hello `hello_world` sample creates a gateway based on hello `hello_world.json` file which specifies hello two predefined modules associated with hello app.</span></span> <span data-ttu-id="eb108-123">Hello журналы событий шлюза файл tooa сообщение «hello world» каждые 5 секунд.</span><span class="sxs-lookup"><span data-stu-id="eb108-123">hello gateway logs a "hello world" message tooa file every 5 seconds.</span></span> <span data-ttu-id="eb108-124">В этом разделе, компиляцией и выполнением hello `hello_world` приложения с ее модуля по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="eb108-124">In this section, you compile and run hello `hello_world` app with its default module.</span></span>

<span data-ttu-id="eb108-125">toocompile и выполнения hello `hello_world` приложения, выполните следующие действия на компьютере узла:</span><span class="sxs-lookup"><span data-stu-id="eb108-125">toocompile and run hello `hello_world` app, follow these steps on your host computer:</span></span>

1. <span data-ttu-id="eb108-126">Инициализируйте hello файлы конфигурации, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="eb108-126">Initialize hello configuration files by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. <span data-ttu-id="eb108-127">Измените файл конфигурации шлюза hello hello Intel NUC MAC-адрес.</span><span class="sxs-lookup"><span data-stu-id="eb108-127">Update hello gateway configuration file with hello MAC address of Intel NUC.</span></span> <span data-ttu-id="eb108-128">Пропустите этот шаг, если вы прошли занятие hello слишком[настройки и запуска образца приложения ЛЮЧИТЬ][config_ble].</span><span class="sxs-lookup"><span data-stu-id="eb108-128">Skip this step if you have gone through hello lesson too[configure and run a BLE sample application][config_ble].</span></span>

   1. <span data-ttu-id="eb108-129">Откройте файл конфигурации шлюза hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="eb108-129">Open hello gateway configuration file by running hello following command:</span></span>

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. <span data-ttu-id="eb108-130">Обновление hello шлюза MAC-адресов при вы [Настройка NUC Intel как шлюз IoT][setup_nuc], а затем сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="eb108-130">Update hello gateway's MAC address when you [set up Intel NUC as a IoT gateway][setup_nuc], and then save hello file.</span></span>

1. <span data-ttu-id="eb108-131">Скомпилируйте исходный код образца hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="eb108-131">Compile hello sample source code by running hello following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="eb108-132">Hello команда передает hello Образец исходного кода tooIntel NUC и выполняет `build.sh` toocompile его.</span><span class="sxs-lookup"><span data-stu-id="eb108-132">hello command transfers hello sample source code tooIntel NUC and runs `build.sh` toocompile it.</span></span>

1. <span data-ttu-id="eb108-133">Запустите hello `hello_world` приложение на Intel NUC, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="eb108-133">Run hello `hello_world` app on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp run
   ```

   <span data-ttu-id="eb108-134">Здравствуйте, команда запускает `../Tools/run-hello-world.js` , указанным в `config.json` toostart hello пример приложения на Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="eb108-134">hello command runs `../Tools/run-hello-world.js` that is specified in `config.json` toostart hello sample app on Intel NUC.</span></span>

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a><span data-ttu-id="eb108-136">Создание нового модуля и его компиляция на Intel NUC</span><span class="sxs-lookup"><span data-stu-id="eb108-136">Create a new module and compile it on Intel NUC</span></span>

<span data-ttu-id="eb108-137">Приведенные ниже действия Hello поможет создать новый модуль и его компиляция Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="eb108-137">hello steps below walk you through creating a new module and compile it on Intel NUC.</span></span> <span data-ttu-id="eb108-138">модуль Hello выводит сообщения с меткой времени после их получения.</span><span class="sxs-lookup"><span data-stu-id="eb108-138">hello module prints out messages with a timestamp upon receiving them.</span></span> <span data-ttu-id="eb108-139">В этом разделе вы создадите первый настроенный модуль шлюза.</span><span class="sxs-lookup"><span data-stu-id="eb108-139">You will create your first customized gateway module in this section.</span></span>

<span data-ttu-id="eb108-140">Любой модуль Azure IoT Edge необходимо реализовать hello следующие интерфейсы:</span><span class="sxs-lookup"><span data-stu-id="eb108-140">Any Azure IoT Edge module must implement hello following interfaces:</span></span>

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

<span data-ttu-id="eb108-141">При необходимости можно реализовать следующий интерфейс hello.</span><span class="sxs-lookup"><span data-stu-id="eb108-141">You can optionally implement hello following interface:</span></span>

   ```C
   pfModule_Start Module_Start
   ```

<span data-ttu-id="eb108-142">Hello следующей диаграмме показаны пути hello важные состояния модуля.</span><span class="sxs-lookup"><span data-stu-id="eb108-142">hello following diagram shows hello important state paths of a module.</span></span> <span data-ttu-id="eb108-143">Hello квадратный прямоугольники представляют методы, которые реализуют операции tooperform при перемещении модуля hello между состояниями.</span><span class="sxs-lookup"><span data-stu-id="eb108-143">hello square rectangles represent methods you implement tooperform operations when hello module moves between states.</span></span> <span data-ttu-id="eb108-144">Hello овалы-это основной номер состояния, hello модуля может находиться в.</span><span class="sxs-lookup"><span data-stu-id="eb108-144">hello ovals are major states hello module can be in.</span></span>

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

<span data-ttu-id="eb108-146">Теперь давайте создадим на основе шаблона hello модуля:</span><span class="sxs-lookup"><span data-stu-id="eb108-146">Now let’s create a module based on hello template:</span></span>

1. <span data-ttu-id="eb108-147">Откройте папку hello шаблона, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="eb108-147">Open hello template folder by running hello following command:</span></span>

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - <span data-ttu-id="eb108-149">`src/my_module.c`служит в качестве шаблона, который упрощает создание hello модуля.</span><span class="sxs-lookup"><span data-stu-id="eb108-149">`src/my_module.c` serves as a template that facilitates hello creation of a module.</span></span> <span data-ttu-id="eb108-150">Hello шаблона объявляет hello интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="eb108-150">hello template declares hello interfaces.</span></span> <span data-ttu-id="eb108-151">Все что нужно toodo — toohello логику tooadd `MyModule_Receive` функции.</span><span class="sxs-lookup"><span data-stu-id="eb108-151">All you need toodo is tooadd logic toohello `MyModule_Receive` function.</span></span>
   - <span data-ttu-id="eb108-152">`build.sh`Представляет модуль hello toocompile скрипт построения hello на Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="eb108-152">`build.sh` is hello build script toocompile hello module on Intel NUC.</span></span>
1. <span data-ttu-id="eb108-153">Откройте hello `src/my_module.c` файла и ввести два файла заголовков:</span><span class="sxs-lookup"><span data-stu-id="eb108-153">Open hello `src/my_module.c` file and include two header files:</span></span>

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. <span data-ttu-id="eb108-154">Добавьте следующий код toohello hello `MyModule_Receive` функции:</span><span class="sxs-lookup"><span data-stu-id="eb108-154">Add hello following code toohello `MyModule_Receive` function:</span></span>

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

1. <span data-ttu-id="eb108-155">Обновление hello `config.json` файл toospecify hello `workspace` папку на путь узла компьютера и hello развертывания на Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="eb108-155">Update hello `config.json` file toospecify hello `workspace` folder on your host computer and hello deployment path on Intel NUC.</span></span> <span data-ttu-id="eb108-156">Во время компиляции, hello файлы в hello `workspace` папка будет переносятся toohello пути развертывания.</span><span class="sxs-lookup"><span data-stu-id="eb108-156">During compiling, hello files in hello `workspace` folder will be transferred toohello deployment path.</span></span>

   1. <span data-ttu-id="eb108-157">Откройте hello `config.json` файл, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="eb108-157">Open hello `config.json` file by running hello following command:</span></span>

      ```bash
      code config.json
      ```

   1. <span data-ttu-id="eb108-158">Обновление `config.json` с hello следующая конфигурация:</span><span class="sxs-lookup"><span data-stu-id="eb108-158">Update `config.json` with hello following configuration:</span></span>

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. <span data-ttu-id="eb108-160">Скомпилируйте модуль hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="eb108-160">Compile hello module by running hello following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="eb108-161">Hello команда передает hello исходного кода tooIntel NUC и выполняет `build.sh` toocompile hello модуля.</span><span class="sxs-lookup"><span data-stu-id="eb108-161">hello command transfers hello source code tooIntel NUC and runs `build.sh` toocompile hello module.</span></span>

## <a name="add-hello-module-toohello-helloworld-sample-app-and-run-hello-app-on-intel-nuc"></a><span data-ttu-id="eb108-162">Добавить hello модуля toohello hello_world пример приложения и запустить приложение hello на Intel NUC</span><span class="sxs-lookup"><span data-stu-id="eb108-162">Add hello module toohello hello_world sample app and run hello app on Intel NUC</span></span>

<span data-ttu-id="eb108-163">tooperform это задача, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="eb108-163">tooperform this task, follow these steps:</span></span>

1. <span data-ttu-id="eb108-164">Перечислить все двоичные файлы модуля доступны hello (.so-файлы) на Intel NUC, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="eb108-164">List all hello available module binaries (.so files) on Intel NUC by running hello following command:</span></span>

   ```bash
   gulp modules --list
   ```

   <span data-ttu-id="eb108-165">Hello путь к двоичным файлам `my_module` , скомпилирован должен быть указан как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="eb108-165">hello binary path of `my_module` that you compiled should be listed as below:</span></span>

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   <span data-ttu-id="eb108-166">При изменении пользователя для входа по умолчанию hello в `config-gateway.json`, путь к двоичным файлам hello начинается с `home/<your username>` вместо `root`.</span><span class="sxs-lookup"><span data-stu-id="eb108-166">If you change hello default login username in `config-gateway.json`, hello binary path will start with `home/<your username>` instead of `root`.</span></span>

1. <span data-ttu-id="eb108-167">Добавить `my_module` toohello `hello_world` пример приложения:</span><span class="sxs-lookup"><span data-stu-id="eb108-167">Add `my_module` toohello `hello_world` sample app:</span></span>

   1. <span data-ttu-id="eb108-168">Откройте hello `hello_world.json` файл, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="eb108-168">Open hello `hello_world.json` file by running hello following command:</span></span>

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. <span data-ttu-id="eb108-169">Добавьте следующий код toohello hello `modules` раздела:</span><span class="sxs-lookup"><span data-stu-id="eb108-169">Add hello following code toohello `modules` section:</span></span>

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

      <span data-ttu-id="eb108-170">Здравствуйте, значение `module.path` должно быть `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span><span class="sxs-lookup"><span data-stu-id="eb108-170">hello value of `module.path` should be `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span></span> <span data-ttu-id="eb108-171">Hello код объявляет `my_module` toobe, связанный с hello шлюза, а также расположение hello hello двоичного модуля, указанного в `module.path`.</span><span class="sxs-lookup"><span data-stu-id="eb108-171">hello code declares `my_module` toobe associated with hello gateway as well as hello location of hello module binary specified in `module.path`.</span></span>
   1. <span data-ttu-id="eb108-172">Добавьте следующий код toohello hello `links` раздела:</span><span class="sxs-lookup"><span data-stu-id="eb108-172">Add hello following code toohello `links` section:</span></span>

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      <span data-ttu-id="eb108-173">Этот код указывает, что сообщения передаются из hello `hello_world` модуль слишком`my_module`.</span><span class="sxs-lookup"><span data-stu-id="eb108-173">This code specifies that messages are transferred from hello `hello_world` module too`my_module`.</span></span>

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. <span data-ttu-id="eb108-175">Запустите hello `hello_world` пример приложения, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="eb108-175">Run hello `hello_world` sample app by running hello following command:</span></span>

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   <span data-ttu-id="eb108-176">Hello `--config` параметр предписывает hello `run-hello-world.js` сценария с помощью hello toorun `hello_world.json` файл.</span><span class="sxs-lookup"><span data-stu-id="eb108-176">hello `--config` parameter forces hello `run-hello-world.js` script toorun by using hello `hello_world.json` file.</span></span>

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

<span data-ttu-id="eb108-178">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="eb108-178">Congratulations.</span></span> <span data-ttu-id="eb108-179">Теперь можно увидеть поведение hello этого модуля, он просто выводит сообщения «hello world» с меткой времени, другой результат от исходного модуля «hello_world» hello.</span><span class="sxs-lookup"><span data-stu-id="eb108-179">You can now see hello behavior of this new module, it simply prints out "hello world" messages with a timestamp, a different result from hello original "hello_world" module.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb108-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eb108-180">Next Steps</span></span>

<span data-ttu-id="eb108-181">Создан новый модуль, добавленные его образец hello_world toohello и toorun get hello пример приложения hello новый модуль на шлюзе.</span><span class="sxs-lookup"><span data-stu-id="eb108-181">You’ve created a new module, added it toohello hello_world sample, and get hello sample app toorun with hello new module on your gateway.</span></span> <span data-ttu-id="eb108-182">Дополнительные сведения о модулях шлюза Azure IoT toolearn следует Дополнительные примеры модуля здесь можно найти: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span><span class="sxs-lookup"><span data-stu-id="eb108-182">If you want toolearn more about Azure IoT gateway modules, you can find more module samples here: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span></span>

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
