---
title: "Connect Raspberry PI (C) tooAzure IoT — Устранение неполадок | Документы Microsoft"
description: "Страница со сведениями об устранении неполадок в работе Raspberry Pi Node.js"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "неполадки Интернета вещей, проблемы Интернета вещей"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 3653c79b-8a0c-41d4-b0bf-f6b4edb4d233
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4f1ea81dd25d10a39c2939f5ee5f19f6d2ba2b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>Устранение неполадок
## <a name="hardware-issues"></a>Проблемы с оборудованием
### <a name="hello-application-runs-well-but-hello-led-is-not-blinking"></a>приложение Hello также выполняется, но hello Индикатор мигает. это не
Эта проблема не будет всегда связанные toohello оборудования канала связи. Используйте следующие шаги tooidentify проблемы hello.

1. Проверьте, что выбран правильный hello **объект групповой ПОЛИТИКИ** на доске. Hello двух портов должно быть **Земля объект групповой ПОЛИТИКИ (6 ПИН-код)** и **04 объект групповой ПОЛИТИКИ (7 ПИН-код)**.
2. Проверьте правильность полярности hello вашей индикатора. участок больше Hello должно быть указано hello **положительное**, анод ПИН-код.
3. Используйте hello **закрепить 3,3 в** и **Земля ПИН-код** на Pi Raspberry 3. Считать Pi hello питания постоянного ТОКА. Убедитесь, что этот Индикатор hello работает нормально.

![Спецификация светодиодного индикатора](media/iot-hub-raspberry-pi-lessons/troubleshooting/led_spec.png)

### <a name="other-hardware-issues"></a>Другие проблемы с оборудованием
Сведения об устранении типичных проблем на Raspberry Pi 3 см. в разделе hello [официальный по устранению неполадок страницы](http://elinux.org/R-Pi_Troubleshooting).

## <a name="nodejs-package-issues"></a>Проблемы с пакетами Node.js
### <a name="no-response-during-gulp-tasks"></a>Нет ответа при выполнении задач Gulp
Если возникли проблемы при выполнении задачи gulp, можно добавить hello `--verbose` параметра для отладки. Повторите tooterminate текущие задачи gulp с помощью `Ctrl + C`, а затем выполнения hello следующую команду в сообщения отладки toosee окна консоли. В выходных данных консоли должны отобразиться подробные сообщения об ошибках. 

```bash
gulp --verbose
```

### <a name="device-discovery-issues"></a>Проблемы с обнаружением устройств
Для помощи при устранении типичных проблем с hello `devdisco` команды, проверьте hello [readme](https://github.com/Azure/device-discovery-cli/blob/develop/readme.md).

### <a name="npm-issues"></a>проблемы с NPM
Попробуйте tooupdate пакета NPM с hello следующую команду:

```bash
npm install -g npm
```

Если hello проблема остается, оставьте комментарий в конце hello в этой статье, или создать вопрос GitHub в нашем [репозитории примеров](https://github.com/Azure-Samples/iot-hub-c-raspberrypi-getting-started)

## <a name="remote-debugging"></a>Удаленная отладка

Поддержка удаленной отладки скоро станет доступной в расширении C/C++ для Visual Studio Code.

Кроме того, вы можете использовать инструмент GDB через привычный терминал SSH:

```bash
cd c-pi-lesson-x
sudo gdb app
```

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
[Обозреватель устройств](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) выполняется на локальном компьютере Windows и подключается tooyour центр IoT в Azure. Он взаимодействует с hello следующие [конечные точки центра IoT](iot-hub-devguide.md):

* *Управление устройствами удостоверения* tooprovision и управления ими устройствах, зарегистрированных в центр IoT.
* *Получение устройства в облако* можно наблюдать за сообщений, отправленных из центра IoT tooyour вашего устройства.
* *Отправить облака на устройство* для отправки сообщений tooyour устройств из вашего центра IoT.

Настройка вашего `IoT hub connection string` в этот инструмент toouse его возможности.

### <a name="iot-hub-explorer"></a>Обозреватель Центра Интернета вещей
[Центр IoT Explorer](https://github.com/Azure/iothub-explorer) -это средство многоплатформенного CLI образец toomanage клиентов устройств. Можно использовать hello средство toomanage hello устройства в реестре удостоверений hello, отслеживать сообщения из устройства в облако и отправлять команды облака на устройство.

tooinstall hello последняя (Предварительная) версия hello центром IOT-анализатор, запустите следующую команду в среде командной строки hello:

```
npm install -g iothub-explorer@latest
```

Можно использовать следующую команду, tooget дополнительную справку обо всех hello центром IOT обозреватель команды и их параметрах hello.

```bash
iothub-explorer help
```

### <a name="azure-portal"></a>Портал Azure
Все возможности интерфейса командной строки помогают создавать все ресурсы Azure и управлять ими. Можно также toouse hello [портал Azure](../azure-portal-overview.md) toohelp подготовки, управления и отладки ресурсам Azure.

## <a name="azure-storage-issues"></a>Проблемы со службой хранилища Azure
[Обозреватель хранилищ Microsoft Azure (Предварительная версия)](http://storageexplorer.com) имеет отдельное приложение от Майкрософт, можно использовать toowork с данных из хранилища Azure в Windows, macOS и Linux. С ее помощью можно подключиться tooyour таблицы и просмотра данных hello. Можно использовать этот инструмент tootroubleshoot вашей проблемы хранилища Azure.
