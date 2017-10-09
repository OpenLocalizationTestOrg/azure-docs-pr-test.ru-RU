---
title: "Подключение Edison Intel (узел) tooAzure IoT — занятия 4: Устранение неполадок | Документы Microsoft"
description: "Страница со сведениями об устранении неполадок в работе Intel Edison Node.js"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "устранение неполадок Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: f11c5521-8a36-44c0-baad-f5ec26ab4618
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 9502300f7f372255572b49bea45dd3e1fdaeeb37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>Устранение неполадок
## <a name="hardware-issues"></a>Проблемы с оборудованием
Сведения об устранении типичных проблем на Intel Edison см. в разделе hello [официальный по устранению неполадок страницы](https://software.intel.com/en-us/node/637974).

## <a name="nodejs-package-issues"></a>Проблемы с пакетами Node.js
### <a name="no-response-during-gulp-tasks"></a>Нет ответа при выполнении задач Gulp
Если возникли проблемы при выполнении задачи gulp, можно добавить hello `--verbose` параметра для отладки. Повторите tooterminate текущие задачи gulp с помощью `Ctrl + C`, а затем выполнения hello следующую команду в сообщения отладки toosee окна консоли. В выходных данных консоли должны отобразиться подробные сообщения об ошибках. 

```bash
gulp --verbose
```

### <a name="npm-issues"></a>проблемы с NPM
Попробуйте tooupdate пакета NPM с hello следующую команду:

```bash
npm install -g npm
```

Если hello проблема остается, оставьте комментарий в конце hello в этой статье, или создать вопрос GitHub в нашем [репозитории примеров][sample-repository].

## <a name="remote-debugging"></a>Удаленная отладка

### <a name="run-hello-sample-application-in-debug-mode"></a>Запустить образец приложения hello в режиме отладки

```bash
gulp run --debug
```

После подготовки hello отладчик должен быть доступ toosee ```Debugger listening on port 5858``` из выходных данных консоли hello.

### <a name="configure-vs-code-tooconnect-toohello-remote-device"></a>Настройте удаленное устройство VS Code tooconnect toohello

Откройте hello **отладки** панели hello слева.

Щелкните зеленый hello **начать отладку** кнопки (F5). Будет открыт VS Code **launch.json** файл, который требуется tooupdate.

Обновление hello **launch.json** с hello следующие содержимое файла, замените `[device hostname or IP address]` с hello само устройство IP-адрес или имя узла.  

```json
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
            "remoteRoot": null
        }
    ]
}
```

![Конфигурация удаленной отладки](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_configuration.png)

### <a name="attach-toohello-remote-application"></a>Присоединение удаленного приложения toohello

Щелкните зеленый hello **начать отладку** (F5) кнопку и наслаждаться отладки.

Можно прочитать [JavaScript в VS Code](https://code.visualstudio.com/docs/languages/javascript#_debugging) toolearn Дополнительные сведения об отладчике hello.

![Интерактивная удаленная отладка](media/iot-hub-intel-edison-lessons/troubleshooting/remote_debugging_interactive.png)

## <a name="azure-cli-issues"></a>Проблемы с Azure CLI
Hello Azure командной строки (CLI Azure) — это построение предварительного просмотра. Искать решение в hello [руководство по установке Preview](https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md) tooseek решения. Повторите версии toolatest tooupgrade Azure cli, когда команды не работают должным образом.

При возникновении любых ошибок с помощью средства hello файл [проблема](https://github.com/Azure/azure-cli/issues) в hello **проблемы** раздел hello в репозитории GitHub.

Для получения справки по устранению общих проблем, проверьте hello [readme](https://github.com/Azure/azure-cli/blob/master/README.rst).

Если соблюдаются «Не удалось найти версию, которая соответствует требованиям hello», проверьте выполнения hello следующая команда tooupgrade pip toolastest версии.

```bash
python -m pip install --upgrade pip
```

## <a name="python-installation-issues"></a>Проблемы с установкой Python
### <a name="legacy-installation-issues-macos"></a>Проблемы с устаревшими установками (macOS)
При установке **pip** возникает ошибка разрешения, если есть устаревшие пакеты, которые устанавливаются с использованием разрешений **su**. Такая ситуация возникает из-за того, что предыдущая установка Python с использованием brew (macOS) удалена не полностью. Некоторые **pip** пакеты из предыдущей установки были созданы корневым элементом, который приводит к возникновению ошибки разрешение hello. Здравствуйте, решение является tooremove эти пакеты, установленные корневым элементом. Используйте следующие шаги toocomplete hello этой задачи:

1. Перейдите к папке /usr/local/lib/python2.7/site-packages.
2. Выведите список пакетов, созданных с использованием разрешений корневой папки: `ls -l | grep root`.
3. Удалите пакеты из шага 2: `sudo rm -rf {package name}`.
4. Переустановите Python.

## <a name="azure-iot-hub-issues"></a>Проблемы с Центром Интернета вещей Azure
Если успешной подготовки ваш центр Azure IoT с `azure-cli`, и необходимо, чтобы устройства hello toomanage средство, подключающимися центра IoT tooyour, попробуйте hello следующие средства:

### <a name="device-explorer"></a>Обозреватель устройств
[Обозреватель устройств](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) выполняется на локальном компьютере Windows и подключается tooyour центр IoT в Azure. Он взаимодействует с hello следующие [конечные точки центра IoT](iot-hub-devguide.md):

- _Управление устройствами удостоверения_ tooprovision и управления ими устройствах, зарегистрированных в центр IoT.
- _Получение устройства в облако_ можно наблюдать за сообщений, отправленных из центра IoT tooyour вашего устройства.
- _Отправить облака на устройство_ для отправки сообщений tooyour устройств из вашего центра IoT.

Настройка вашего `IoT hub connection string` в этот инструмент toouse его возможности.

### <a name="iot-hub-explorer"></a>Обозреватель Центра Интернета вещей
[Центр IoT Explorer](https://github.com/Azure/iothub-explorer) -это средство многоплатформенного CLI образец toomanage клиентов устройств. Можно использовать hello средство toomanage hello устройства в реестре удостоверений hello, отслеживать сообщения из устройства в облако и отправлять команды облака на устройство.

tooinstall hello последняя (Предварительная) версия hello центром IOT-анализатор, запустите следующую команду в среде командной строки hello:

```bash
npm install -g iothub-explorer@latest
```

Можно использовать следующую команду, tooget дополнительную справку обо всех hello центром IOT обозреватель команды и их параметрах hello.

```bash
iothub-explorer help
```

### <a name="azure-portal"></a>Портал Azure
Все возможности интерфейса командной строки помогают создавать все ресурсы Azure и управлять ими. Можно также toouse hello [портал Azure](../azure-portal-overview.md) toohelp подготовки, управления и отладки ресурсам Azure.

## <a name="azure-storage-issues"></a>Проблемы со службой хранилища Azure
[Обозреватель хранилищ Microsoft Azure (Предварительная версия)](http://storageexplorer.com) имеет отдельное приложение от Майкрософт, можно использовать toowork с [хранилища Azure](https://azure.microsoft.com/en-us/services/storage/) данных в Windows, macOS и Linux. С ее помощью можно подключиться tooyour таблицы и просмотра данных hello. Можно использовать этот инструмент tootroubleshoot вашей проблемы хранилища Azure.

## <a name="next-steps"></a>Дальнейшие действия
Эта страница содержит только наиболее распространенные проблемы hello комплекта Intel Edison. Также можно оставить комментарии нижней tooreport вопросы по устранению неполадок.

Возврат слишком[Приступая к работе с Edison Intel (Node.js)](iot-hub-intel-edison-kit-node-get-started.md)

<!-- Images and links -->

[sample-repository]: https://github.com/Azure-Samples/iot-hub-node-edison-getting-started