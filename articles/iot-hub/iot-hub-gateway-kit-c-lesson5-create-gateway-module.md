---
title: "Создание первого модуля шлюза Azure IoT | Документация Майкрософт"
description: "Создайте модуль и добавьте его в пример приложения для настройки поведения модуля."
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
ms.openlocfilehash: 5e28422158684c3aaf0ac3fdf5b19c80fbccfb02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-5-create-your-first-azure-iot-gateway-module"></a><span data-ttu-id="a8254-103">Урок 5. Создание первого модуля шлюза Azure IoT</span><span class="sxs-lookup"><span data-stu-id="a8254-103">Lesson 5: Create your first Azure IoT Gateway module</span></span>
<span data-ttu-id="a8254-104">Edge Интернета вещей Azure позволяет создавать модули, написанные на Java, .NET или Node.js, но в этом руководстве описаны шаги по созданию модуля на C.</span><span class="sxs-lookup"><span data-stu-id="a8254-104">While Azure IoT Edge allows you to build modules written in Java, .NET, or Node.js, this tutorial walks you through the steps for building a module in C.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="a8254-105">Выполняемая задача</span><span class="sxs-lookup"><span data-stu-id="a8254-105">What you will do</span></span>

- <span data-ttu-id="a8254-106">Компиляция и запуск примера приложения hello_world на устройстве Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="a8254-106">Compile and run the hello_world sample app on Intel NUC.</span></span>
- <span data-ttu-id="a8254-107">Создание модуля и его компиляция на Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="a8254-107">Create a module and compile it on Intel NUC.</span></span>
- <span data-ttu-id="a8254-108">Добавление нового модуля в пример приложения hello_world и запуск примера на Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="a8254-108">Add the new module to the hello_world sample app and then run the sample on Intel NUC.</span></span> <span data-ttu-id="a8254-109">Новый модуль выводит на экран сообщение "hello_world" с меткой времени.</span><span class="sxs-lookup"><span data-stu-id="a8254-109">The new module prints out "hello_world" messages with a timestamp.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a8254-110">Новые знания</span><span class="sxs-lookup"><span data-stu-id="a8254-110">What you will learn</span></span>

- <span data-ttu-id="a8254-111">Как скомпилировать и запустить пример приложения на Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="a8254-111">How to compile and run a sample app on Intel NUC.</span></span>
- <span data-ttu-id="a8254-112">Как создать модуль.</span><span class="sxs-lookup"><span data-stu-id="a8254-112">How to create a module.</span></span>
- <span data-ttu-id="a8254-113">Как добавить модуль в пример приложения.</span><span class="sxs-lookup"><span data-stu-id="a8254-113">How to add module to a sample app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a8254-114">Необходимые элементы</span><span class="sxs-lookup"><span data-stu-id="a8254-114">What you need</span></span>

<span data-ttu-id="a8254-115">Edge Интернета вещей Azure, установленный на главном компьютере.</span><span class="sxs-lookup"><span data-stu-id="a8254-115">Azure IoT Edge that has been installed on your host computer.</span></span>

## <a name="folder-structure"></a><span data-ttu-id="a8254-116">Структура папок</span><span class="sxs-lookup"><span data-stu-id="a8254-116">Folder structure</span></span>

<span data-ttu-id="a8254-117">В уроке 5 вложенная папка с примером кода, который вы клонировали в уроке 1, содержит папку `module` и папку `sample`.</span><span class="sxs-lookup"><span data-stu-id="a8254-117">In the Lesson 5 subfolder of the sample code which you cloned in lesson 1, there is a `module` folder and a `sample` folder.</span></span>

![my_module](media/iot-hub-gateway-kit-lessons/lesson5/my_module.png)

- <span data-ttu-id="a8254-119">Папка `module/my_module` содержит исходный код и скрипт для создания модуля.</span><span class="sxs-lookup"><span data-stu-id="a8254-119">The `module/my_module` folder contains the source code and script to build the module.</span></span>
- <span data-ttu-id="a8254-120">Папка `sample` содержит исходный код и скрипт для создания примера приложения.</span><span class="sxs-lookup"><span data-stu-id="a8254-120">The `sample` folder contains the source code and script to build the sample app.</span></span>

## <a name="compile-and-run-the-helloworld-sample-app-on-intel-nuc"></a><span data-ttu-id="a8254-121">Компиляция и запуск примера приложения hello_world на Intel NUC</span><span class="sxs-lookup"><span data-stu-id="a8254-121">Compile and run the hello_world sample app on Intel NUC</span></span>

<span data-ttu-id="a8254-122">Пример `hello_world` создает шлюз на основе файла `hello_world.json`, который задает два предопределенных модуля, связанных с приложением.</span><span class="sxs-lookup"><span data-stu-id="a8254-122">The `hello_world` sample creates a gateway based on the `hello_world.json` file which specifies the two predefined modules associated with the app.</span></span> <span data-ttu-id="a8254-123">Шлюз записывает сообщение "hello world" в файл каждые 5 секунд.</span><span class="sxs-lookup"><span data-stu-id="a8254-123">The gateway logs a "hello world" message to a file every 5 seconds.</span></span> <span data-ttu-id="a8254-124">В этом разделе вы скомпилируете и запустите приложение `hello_world` с его модулем по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a8254-124">In this section, you compile and run the `hello_world` app with its default module.</span></span>

<span data-ttu-id="a8254-125">Чтобы скомпилировать и запустить приложение `hello_world`, на главном компьютере выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a8254-125">To compile and run the `hello_world` app, follow these steps on your host computer:</span></span>

1. <span data-ttu-id="a8254-126">Инициализируйте файлы конфигурации, выполнив приведенные ниже команды.</span><span class="sxs-lookup"><span data-stu-id="a8254-126">Initialize the configuration files by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-intel-nuc-gateway-getting-started
   cd Lesson5
   npm install
   gulp init
   ```

1. <span data-ttu-id="a8254-127">Добавьте в файл конфигурации шлюза MAC-адрес устройства Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="a8254-127">Update the gateway configuration file with the MAC address of Intel NUC.</span></span> <span data-ttu-id="a8254-128">Пропустите этот шаг, если вы прошли урок по [настройке и запуску примера приложения BLE][config_ble].</span><span class="sxs-lookup"><span data-stu-id="a8254-128">Skip this step if you have gone through the lesson to [configure and run a BLE sample application][config_ble].</span></span>

   1. <span data-ttu-id="a8254-129">Откройте файл конфигурации шлюза, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a8254-129">Open the gateway configuration file by running the following command:</span></span>

      ```bash
      # For Windows command prompt
      code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json

      # For MacOS or Ubuntu
      code ~/.iot-hub-getting-started/config-gateway.json
      ```

   1. <span data-ttu-id="a8254-130">Обновите MAC-адрес шлюза во время [настройки Intel NUC в качестве шлюза IoT][setup_nuc], а затем сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="a8254-130">Update the gateway's MAC address when you [set up Intel NUC as a IoT gateway][setup_nuc], and then save the file.</span></span>

1. <span data-ttu-id="a8254-131">Скомпилируйте пример исходного кода, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a8254-131">Compile the sample source code by running the following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="a8254-132">Команда передает пример исходного кода на Intel NUC и запускает `build.sh` для его компиляции.</span><span class="sxs-lookup"><span data-stu-id="a8254-132">The command transfers the sample source code to Intel NUC and runs `build.sh` to compile it.</span></span>

1. <span data-ttu-id="a8254-133">Запустите приложение `hello_world` на Intel NUC, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a8254-133">Run the `hello_world` app on Intel NUC by running the following command:</span></span>

   ```bash
   gulp run
   ```

   <span data-ttu-id="a8254-134">Команда запускает `../Tools/run-hello-world.js`, указанный в `config.json`, для запуска примера приложения на Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="a8254-134">The command runs `../Tools/run-hello-world.js` that is specified in `config.json` to start the sample app on Intel NUC.</span></span>

   ![run_sample](media/iot-hub-gateway-kit-lessons/lesson5/run_sample.png)

## <a name="create-a-new-module-and-compile-it-on-intel-nuc"></a><span data-ttu-id="a8254-136">Создание нового модуля и его компиляция на Intel NUC</span><span class="sxs-lookup"><span data-stu-id="a8254-136">Create a new module and compile it on Intel NUC</span></span>

<span data-ttu-id="a8254-137">С помощью приведенных ниже действий вы сможете создать новый модуль и скомпилировать его на устройстве Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="a8254-137">The steps below walk you through creating a new module and compile it on Intel NUC.</span></span> <span data-ttu-id="a8254-138">При получении сообщений модуль выводит их на экран с меткой времени.</span><span class="sxs-lookup"><span data-stu-id="a8254-138">The module prints out messages with a timestamp upon receiving them.</span></span> <span data-ttu-id="a8254-139">В этом разделе вы создадите первый настроенный модуль шлюза.</span><span class="sxs-lookup"><span data-stu-id="a8254-139">You will create your first customized gateway module in this section.</span></span>

<span data-ttu-id="a8254-140">Любой модуль Edge Интернета вещей Azure должен реализовать следующие интерфейсы:</span><span class="sxs-lookup"><span data-stu-id="a8254-140">Any Azure IoT Edge module must implement the following interfaces:</span></span>

   ```C
   pfModule_ParseConfigurationFromJson Module_ParseConfigurationFromJson
   pfModule_FreeConfiguration Module_FreeConfiguration
   pfModule_Create Module_Create
   pfModule_Destroy Module_Destroy
   pfModule_Receive Module_Receive
   ```

<span data-ttu-id="a8254-141">При необходимости можно реализовать следующий интерфейс:</span><span class="sxs-lookup"><span data-stu-id="a8254-141">You can optionally implement the following interface:</span></span>

   ```C
   pfModule_Start Module_Start
   ```

<span data-ttu-id="a8254-142">На схеме ниже показаны переходы между основными состояниями модуля.</span><span class="sxs-lookup"><span data-stu-id="a8254-142">The following diagram shows the important state paths of a module.</span></span> <span data-ttu-id="a8254-143">Прямоугольниками обозначены методы, с помощью которых выполняются операции, когда модуль перемещается между состояниями.</span><span class="sxs-lookup"><span data-stu-id="a8254-143">The square rectangles represent methods you implement to perform operations when the module moves between states.</span></span> <span data-ttu-id="a8254-144">Овалами показаны основные состояния, в которых может находиться модуль.</span><span class="sxs-lookup"><span data-stu-id="a8254-144">The ovals are major states the module can be in.</span></span>

![state_path](media/iot-hub-gateway-kit-lessons/lesson5/state_path.png)

<span data-ttu-id="a8254-146">Теперь создадим модуль на основе шаблона:</span><span class="sxs-lookup"><span data-stu-id="a8254-146">Now let’s create a module based on the template:</span></span>

1. <span data-ttu-id="a8254-147">Откройте папку шаблонов, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a8254-147">Open the template folder by running the following command:</span></span>

   ```bash
   code module/my_module
   ```

   ![code_module](media/iot-hub-gateway-kit-lessons/lesson5/code_module.png)

   - <span data-ttu-id="a8254-149">`src/my_module.c` служит в качестве шаблона, который упрощает создание модуля.</span><span class="sxs-lookup"><span data-stu-id="a8254-149">`src/my_module.c` serves as a template that facilitates the creation of a module.</span></span> <span data-ttu-id="a8254-150">Шаблон объявляет интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="a8254-150">The template declares the interfaces.</span></span> <span data-ttu-id="a8254-151">Вам остается только добавить логику в функцию `MyModule_Receive`.</span><span class="sxs-lookup"><span data-stu-id="a8254-151">All you need to do is to add logic to the `MyModule_Receive` function.</span></span>
   - <span data-ttu-id="a8254-152">`build.sh` — это скрипт сборки для компиляции модуля на устройстве Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="a8254-152">`build.sh` is the build script to compile the module on Intel NUC.</span></span>
1. <span data-ttu-id="a8254-153">Откройте файл `src/my_module.c` и включите два файла заголовков:</span><span class="sxs-lookup"><span data-stu-id="a8254-153">Open the `src/my_module.c` file and include two header files:</span></span>

   ```C
   #include <stdio.h>
   #include "azure_c_shared_utility/xlogging.h"
   ```

1. <span data-ttu-id="a8254-154">Добавьте в функцию `MyModule_Receive` следующий код:</span><span class="sxs-lookup"><span data-stu-id="a8254-154">Add the following code to the `MyModule_Receive` function:</span></span>

   ```C
   if (message == NULL)
   {
      LogError("invalid arg message");
   }
   else
   {
      // get the message content
      const CONSTBUFFER * content = Message_GetContent(message);
      // get the local time and format it
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
                  LogError("unable to strftime");
              }
              else
              {
                  printf("[%s] %.*s\r\n", timetemp, (int)content->size, content->buffer);
              }
          }
      }
   }
   ```

1. <span data-ttu-id="a8254-155">Укажите в файле `config.json` папку `workspace` на главном компьютере и путь развертывания на устройстве Intel NUC.</span><span class="sxs-lookup"><span data-stu-id="a8254-155">Update the `config.json` file to specify the `workspace` folder on your host computer and the deployment path on Intel NUC.</span></span> <span data-ttu-id="a8254-156">Во время компиляции файлы в папке `workspace` будут переданы в путь развертывания.</span><span class="sxs-lookup"><span data-stu-id="a8254-156">During compiling, the files in the `workspace` folder will be transferred to the deployment path.</span></span>

   1. <span data-ttu-id="a8254-157">Откройте файл `config.json`, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a8254-157">Open the `config.json` file by running the following command:</span></span>

      ```bash
      code config.json
      ```

   1. <span data-ttu-id="a8254-158">Дополните `config.json` следующей конфигурацией:</span><span class="sxs-lookup"><span data-stu-id="a8254-158">Update `config.json` with the following configuration:</span></span>

      ```json
      "workspace": "./module/my_module",
      "deploy_path": "module/my_module"
      ```

      ![config_json](media/iot-hub-gateway-kit-lessons/lesson5/config_json.png)

1. <span data-ttu-id="a8254-160">Скомпилируйте модуль, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a8254-160">Compile the module by running the following command:</span></span>

   ```bash
   gulp compile
   ```

   <span data-ttu-id="a8254-161">Команда передает исходный код на устройство Intel NUC и выполняет `build.sh` для компиляции модуля.</span><span class="sxs-lookup"><span data-stu-id="a8254-161">The command transfers the source code to Intel NUC and runs `build.sh` to compile the module.</span></span>

## <a name="add-the-module-to-the-helloworld-sample-app-and-run-the-app-on-intel-nuc"></a><span data-ttu-id="a8254-162">Добавление модуля в пример приложения hello_world и запуск приложения на Intel NUC</span><span class="sxs-lookup"><span data-stu-id="a8254-162">Add the module to the hello_world sample app and run the app on Intel NUC</span></span>

<span data-ttu-id="a8254-163">Для этого выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a8254-163">To perform this task, follow these steps:</span></span>

1. <span data-ttu-id="a8254-164">Выведите список всех доступных двоичных файлов модуля (SO-файлов) на устройстве Intel NUC, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a8254-164">List all the available module binaries (.so files) on Intel NUC by running the following command:</span></span>

   ```bash
   gulp modules --list
   ```

   <span data-ttu-id="a8254-165">Укажите путь к двоичным файлам скомпилированного кода `my_module`, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="a8254-165">The binary path of `my_module` that you compiled should be listed as below:</span></span>

   ```path
   /root/gateway_sample/module/my_module/build/libmy_module.so
   ```

   <span data-ttu-id="a8254-166">Если изменить стандартное имя пользователя для входа в `config-gateway.json`, путь к двоичным файлам будет начинаться с `home/<your username>`, а не `root`.</span><span class="sxs-lookup"><span data-stu-id="a8254-166">If you change the default login username in `config-gateway.json`, the binary path will start with `home/<your username>` instead of `root`.</span></span>

1. <span data-ttu-id="a8254-167">Добавьте `my_module` в пример приложения `hello_world`:</span><span class="sxs-lookup"><span data-stu-id="a8254-167">Add `my_module` to the `hello_world` sample app:</span></span>

   1. <span data-ttu-id="a8254-168">Откройте файл `hello_world.json`, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a8254-168">Open the `hello_world.json` file by running the following command:</span></span>

      ```bash
      code sample/hello_world/src/hello_world.json
      ```

   1. <span data-ttu-id="a8254-169">Добавьте в раздел `modules` следующий код:</span><span class="sxs-lookup"><span data-stu-id="a8254-169">Add the following code to the `modules` section:</span></span>

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

      <span data-ttu-id="a8254-170">Значение `module.path` должно быть следующим: `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span><span class="sxs-lookup"><span data-stu-id="a8254-170">The value of `module.path` should be `/root/gateway_sample/module/my_module/build/libmy_module.so`.</span></span> <span data-ttu-id="a8254-171">Код объявляет `my_module` для связывания со шлюзом, а также расположение двоичного файла модуля, указанного в `module.path`.</span><span class="sxs-lookup"><span data-stu-id="a8254-171">The code declares `my_module` to be associated with the gateway as well as the location of the module binary specified in `module.path`.</span></span>
   1. <span data-ttu-id="a8254-172">Добавьте в раздел `links` следующий код:</span><span class="sxs-lookup"><span data-stu-id="a8254-172">Add the following code to the `links` section:</span></span>

      ```json
      {
        "source": "hello_world",
        "sink": "my_module"
      }
      ```

      <span data-ttu-id="a8254-173">Этот код указывает, что сообщения передаются из модуля `hello_world` в `my_module`.</span><span class="sxs-lookup"><span data-stu-id="a8254-173">This code specifies that messages are transferred from the `hello_world` module to `my_module`.</span></span>

      ![hello_world_json](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_json.png)

1. <span data-ttu-id="a8254-175">Запустите пример приложения `hello_world`, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a8254-175">Run the `hello_world` sample app by running the following command:</span></span>

   ```bash
   gulp run --config sample/hello_world/src/hello_world.json
   ```

   <span data-ttu-id="a8254-176">Параметр `--config` принудительно запускает скрипт `run-hello-world.js` с помощью файла `hello_world.json`.</span><span class="sxs-lookup"><span data-stu-id="a8254-176">The `--config` parameter forces the `run-hello-world.js` script to run by using the `hello_world.json` file.</span></span>

   ![hello_world_new](media/iot-hub-gateway-kit-lessons/lesson5/hello_world_new.png)

<span data-ttu-id="a8254-178">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="a8254-178">Congratulations.</span></span> <span data-ttu-id="a8254-179">Теперь вы можете увидеть поведение этого нового модуля: он просто выводит на экран сообщения "hello world" с меткой времени, чем отличается от исходного модуля "hello_world".</span><span class="sxs-lookup"><span data-stu-id="a8254-179">You can now see the behavior of this new module, it simply prints out "hello world" messages with a timestamp, a different result from the original "hello_world" module.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8254-180">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a8254-180">Next Steps</span></span>

<span data-ttu-id="a8254-181">Вы создали новый модуль, добавили его в пример приложения hello_world и запустили пример приложения с новым модулем в шлюзе.</span><span class="sxs-lookup"><span data-stu-id="a8254-181">You’ve created a new module, added it to the hello_world sample, and get the sample app to run with the new module on your gateway.</span></span> <span data-ttu-id="a8254-182">Дополнительные сведения о модулях шлюза Azure IoT и другие примеры модулей см. здесь: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span><span class="sxs-lookup"><span data-stu-id="a8254-182">If you want to learn more about Azure IoT gateway modules, you can find more module samples here: [https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules](https://github.com/Azure/azure-iot-gateway-sdk/tree/master/modules).</span></span>

<!-- Images and links -->

[config_ble]: iot-hub-gateway-kit-c-lesson3-configure-ble-app.md
[setup_nuc]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
