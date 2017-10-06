---
title: "Приступая к работе с имитацией устройства и шлюзом Azure IoT. Устранение неполадок | Документация Майкрософт"
description: "Страница со сведениями об устранении неполадок для шлюза Intel NUC"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "неполадки Интернета вещей, проблемы Интернета вещей"
ROBOTS: NOINDEX
ms.assetid: 3ee8f4b0-5799-40a3-8cf0-8d5aa44dbc2b
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: cc7add6273e66aadeca9a4915a44f5edf61a0a59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>Устранение неполадок

## <a name="hardware-issues"></a>Проблемы с оборудованием

### <a name="ti-sensortag-cannot-be-connected"></a>Не удается подключить TI SensorTag

проблемы с подключением SensorTag tootroubleshoot, использовать hello [SensorTag приложения](http://processors.wiki.ti.com/index.php/SensorTag_User_Guide#SensorTag_App_user_guide).

### <a name="have-an-issue-with-intel-nuc"></a>Проблема с Intel NUC

ошибки при загрузке tootroubleshoot, см. слишком[устранения неполадок без загрузки на Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000005845.html).

tootroubleshoot проблемы операционной системы, см. слишком[Устранение неполадок операционной системы на Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/000006018.html).

tootroubleshoot слишком ссылаются другие проблемы[Blink коды и звуковой сигнал для Intel NUC](http://www.intel.com/content/www/us/en/support/boards-and-kits/intel-nuc-boards/000005854.html).

## <a name="nodejs-package-issues"></a>Проблемы с пакетами Node.js

### <a name="no-response-during-gulp-tasks"></a>Нет ответа при выполнении задач Gulp

Если возникли проблемы при выполнении задачи gulp, вы можете добавить hello `--verbose` параметра для отладки. Повторите tooterminate текущие задачи gulp с помощью `Ctrl + C`, а затем выполнения hello следующую команду в сообщения отладки toosee окна консоли. В выходных данных консоли должны отобразиться подробные сообщения об ошибках.

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a>Проблемы с обнаружением устройств

Для помощи при устранении типичных проблем с hello `discover-sensortag` команды, проверьте hello [вики-странице](https://wiki.archlinux.org/index.php/bluetooth#Bluetoothctl).

### <a name="npm-issues"></a>проблемы с NPM

Попробуйте tooupdate пакета npm, выполнив следующую команду hello.

```bash
npm install -g npm
```

Если hello проблема остается, оставьте комментарий в конце hello в этой статье, или создать вопрос GitHub в нашем [репозитории примеров](https://github.com/azure-samples/iot-hub-c-intel-nuc-gateway-getting-started).

## <a name="remote-debugging"></a>Удаленная отладка
> Приведенные ниже инструкции предназначены для отладки сценариев Node.js, используемых в этом руководстве.
### <a name="run-hello-sample-application-in-debug-mode"></a>Запустить образец приложения hello в режиме отладки

Выполните пример приложения hello в режиме отладки, запустив hello следующую команду:

```bash
gulp run --debug
```

При готовности модуль отладки hello вы увидите `Debugger listening on port 5858` в выходных данных консоли hello.

### <a name="configure-visual-studio-code-tooconnect-toohello-remote-device"></a>Настройка Visual Studio Code tooconnect toohello удаленного устройства

1. Откройте hello **отладки** панели на hello слева.
2. Щелкните зеленый hello **начать отладку** кнопки (F5). В Visual Studio Code откроется файл `launch.json`.
3. Обновление hello `launch.json` файл с hello после содержимого. Замените `[device hostname or IP address]` с hello само устройство IP адрес или имя узла.

   ``` json
   {
     "version": "0.2.0",
     "configurations": [
        {
            "name": "Attach",
            "type": "node",
            "request": "attach",
            "port": 5858,
            "address": "[device hostname or IP address]",
            "restart": false,
            "sourceMaps": false,
            "outDir": null,
            "localRoot": "${workspaceRoot}",
            "remoteRoot": "~/ble_sample"
        }
     ]
   }
   ```

![Конфигурация удаленной отладки](./media/iot-hub-gateway-kit-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a>Присоединение удаленного приложения toohello

Щелкните зеленый hello **начать отладку** отладки toostart кнопки (F5).

Чтение [JavaScript в VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn Дополнительные сведения об отладчике hello.

![Отладка примера BLE](./media/iot-hub-gateway-kit-lessons/troubleshooting/debugging_ble_sample.png)

## <a name="azure-cli-issues"></a>Проблемы с интерфейсом командной строки Azure

Hello Azure командной строки (CLI Azure) — это построение предварительного просмотра. tooseek решений, можно использовать hello [руководство по установке предварительной версии](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md).

При возникновении любых ошибок с помощью средства hello файл [проблема](https://github.com/Azure/azure-cli/issues) в hello **проблемы** раздел hello в репозитории GitHub.

Для помощи при устранении неполадок проверьте hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).

Если соблюдаются «Не удалось найти версию, которая соответствует требованиям hello», проверьте выполнения hello следующая команда tooupgrade pip toolastest версии.

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a>Проблемы с установкой Python

### <a name="legacy-installation-issues-macos"></a>Проблемы с устаревшими установками (macOS)

При установке pip возникает ошибка разрешения, если есть устаревшие пакеты, которые устанавливаются с использованием разрешений **su**. Такая ситуация возникает из-за того, что предыдущая установка Python с использованием brew (macOS) удалена не полностью. Корневым элементом, который приводит к возникновению ошибки разрешение hello были созданы некоторые pip пакеты из предыдущей установки. Здравствуйте, решение является tooremove эти пакеты, установленные корневым элементом. Используйте следующие шаги toocomplete hello этой задачи:

1. Go слишком`/usr/local/lib/python2.7/site-packages`
2. Выведите список пакетов, созданных с использованием разрешений корневой папки: `ls -l | grep root`.
3. Удалите пакеты из шага 2: `sudo rm -rf {package name}`.
4. Переустановите Python.

## <a name="azure-iot-hub-issues"></a>Проблемы с Центром Интернета вещей Azure

Если успешной подготовки ваш центр Azure IoT с hello Azure CLI, и требуется средство устройств hello toomanage, подключающимися центра IoT tooyour, попробуйте следующие средства hello.

### <a name="device-explorer"></a>Обозреватель устройств

[Обозреватель устройств](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) выполняется на локальном компьютере Windows и подключается tooyour центр IoT в Azure. Он взаимодействует с hello следующие [конечные точки центра IoT](https://azure.microsoft.com/en-us/documentation/articles/iot-hub-devguide/):

- Tooprovision управления удостоверения устройства и управлять ими устройствах, зарегистрированных в центр IoT.
- Получают устройства в облако, поэтому можно отслеживать сообщения, отправляемые из центра IoT tooyour вашего устройства.
- Отправьте облака на устройство, чтобы сообщения можно отправлять tooyour устройств из вашего центра IoT.

Настройка строки подключения концентратора IoT в этот инструмент toouse его возможности.

### <a name="iothub-explorer"></a>iothub-explorer

[обозреватель центром IOT](https://github.com/Azure/iothub-explorer) -это средство многоплатформенного CLI образец toomanage клиентов устройств. Можно использовать hello средство toomanage hello устройства в реестре удостоверений hello, отслеживать сообщения из устройства в облако и отправлять команды облака на устройство.

tooinstall hello последняя (Предварительная) версия средства обозревателя центром IOT hello, запустите следующую команду hello:

```bash
npm install -g iothub-explorer@latest
```

дополнительную справку tooget обо всех hello центром IOT обозреватель команды и их параметрах, запустите hello следующую команду:

```bash
iothub-explorer help
```

### <a name="hello-azure-portal"></a>Hello портал Azure

Все возможности интерфейса командной строки помогают создавать все ресурсы Azure и управлять ими. Можно также toouse hello [портал Azure](https://azure.microsoft.com/en-us/documentation/articles/azure-portal-overview/) toohelp подготовки, управления и отладки ресурсам Azure.

## <a name="azure-storage-issues"></a>Проблемы с хранилищем Azure

[Обозреватель хранилищ Microsoft Azure (Предварительная версия)](http://storageexplorer.com/) имеет отдельное приложение от Майкрософт, можно использовать toowork с данных из хранилища Azure в Windows, macOS и Linux. С ее помощью можно подключиться tooyour таблицы и просмотра данных hello. Можно использовать этот инструмент tootroubleshoot вашей проблемы хранилища Azure.
