---
title: "Connect Arduino (C) tooAzure IoT — Устранение неполадок | Документы Microsoft"
description: "Страница со сведениями об устранении неполадок в работе Adafruit Feather M0 WiFi Arduino"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "Устранение неполадок Arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: fdcc56ff-4420-463c-8a0e-5a1d215a874f
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: ed793041ffa1887dbe73067f7c48d2417e982866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting"></a>Устранение неполадок
## <a name="hardware-issues"></a>Проблемы с оборудованием
Сведения об устранении типичных проблем на доске Adafruit Растушевка M0 Wi-Fi Arduino см. в разделе hello [официальный по устранению неполадок страницы](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500?view=all#faq).

## <a name="nodejs-package-issues"></a>Проблемы с пакетами Node.js
### <a name="no-response-during-gulp-tasks"></a>Нет ответа при выполнении задач Gulp
Если возникли проблемы при выполнении задачи gulp, можно добавить hello `--verbose` параметра для отладки. Повторите tooterminate текущие задачи gulp с помощью `Ctrl + C`, а затем выполнения hello следующую команду в сообщения отладки toosee окна консоли. В выходных данных консоли должны отобразиться подробные сообщения об ошибках.

```bash
gulp --verbose
```

Или можно добавить `--listen` сведения о журнале устройства toooutput tooopen последовательного порта.

```bash
gulp --listen
``` 

### <a name="npm-issues"></a>проблемы с NPM
Попробуйте tooupdate пакета NPM с hello следующую команду:

```bash
npm install -g npm
```

Если hello проблема остается, оставьте комментарий в конце hello в этой статье, или создать вопрос GitHub в нашем [репозитории примеров][sample-repository].

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

* *Управление устройствами удостоверения* tooprovision и управления ими устройствах, зарегистрированных в центр IoT.
* *Получение устройства в облако* можно наблюдать за сообщений, отправленных из центра IoT tooyour вашего устройства.
* *Отправить облака на устройство* для отправки сообщений tooyour устройств из вашего центра IoT.

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
[Обозреватель хранилищ Microsoft Azure (Предварительная версия)](http://storageexplorer.com) имеет отдельное приложение от Майкрософт, можно использовать toowork с данных из хранилища Azure в Windows, macOS и Linux. С ее помощью можно подключиться tooyour таблицы и просмотра данных hello. Можно использовать этот инструмент tootroubleshoot вашей проблемы хранилища Azure.

<!-- Images and links -->

[sample-repository]: https://github.com/Azure/azure-cli/blob/master/doc/preview_install_guide.md