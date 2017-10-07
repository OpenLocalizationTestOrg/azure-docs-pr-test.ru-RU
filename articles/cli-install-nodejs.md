---
title: "aaaInstall hello Azure CLI 1.0 | Документы Microsoft"
description: "Установка hello Azure CLI 1.0 для toostart Mac, Linux и Windows с помощью служб Azure"
editor: 
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: bdb776c8-7a76-4f3a-887c-236b4fffee10
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: command-line-interface
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: rasquill
ms.openlocfilehash: a8cd4e38fde6e4b17a768a7caecd280cd91a70f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-cli-10"></a>Установка hello Azure CLI 1.0
> [!div class="op_single_selector"]
> * [PowerShell](/powershell/azure/overview)
> * [Azure CLI 1.0](cli-install-nodejs.md)
> * [Azure CLI 2.0](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> Описывается, как вызовы tooinstall hello Azure CLI 1.0, которая основана на nodeJs и поддерживает все API классического развертывания и большое количество действий развертывания диспетчера ресурсов. Следует использовать hello [Azure CLI 2.0](/cli/azure/overview) нового и перспективных CLI развертывания и управления.

Быстро установите интерфейс командной строки Azure (Azure CLI 1.0) hello toouse набор команд командной строки открытым исходным кодом, для создания и управления ресурсами в Microsoft Azure. У вас есть несколько вариантов tooinstall эти средства кросс платформенных на вашем компьютере:

* **пакет npm** — выполнения npm (hello диспетчер пакетов для JavaScript) tooinstall hello последнюю версию Azure CLI 1.0 пакета в дистрибутив Linux или ОС. На компьютере должны быть установлены node.js и npm.
* **Установщик**. Скачайте установщик, чтобы легко установить эти инструменты на компьютеры Mac или Windows.
* **Контейнер docker** — начать использование hello последнюю CLI в контейнер Docker готов к запуску. На компьютере требуется наличие узла Docker.

Дополнительные параметры и фона, см. репозиторий проекта hello [GitHub](https://github.com/azure/azure-xplat-cli).

После установки hello Azure CLI 1.0 [подключить к подписке Azure](xplat-cli-connect.md) и выполнения hello **azure** команды из интерфейса командной строки (Bash, терминалов, командной строки и т. д.) toowork с ресурсы Azure.

## <a name="option-1-install-an-npm-package"></a>Вариант 1. Установка пакета npm
hello tooinstall CLI из пакета npm убедитесь, вы загрузили и установили hello [последние Node.js и npm](https://nodejs.org/en/download/package-manager/). Затем запустите **установки npm** tooinstall hello azure cli пакета:

```bash
npm install -g azure-cli
```

На дистрибутивов Linux, может потребоваться toouse **sudo** toosuccessfully запуска hello **npm** команды, как показано ниже:

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> При необходимости tooinstall или обновлении Node.js и npm в дистрибутив Linux или операционной системы, рекомендуется установить последнюю версию Node.js LTS hello (4.x). Если вы используете более раннюю версию, возможны ошибки при установке.

Если вы предпочитаете загрузить hello последнюю Linux [tar-файл] [ linux-installer] hello npm пакета локально. Установите hello загруженный npm следующим образом (в ОС Linux могут потребоваться toouse **sudo**):

```bash
npm install -g <path toodownloaded tar file>
```

## <a name="option-2-use-an-installer"></a>Вариант 2. Использование установщика
Если вы используете компьютер Mac и Windows, следующие установщики CLI hello доступны для загрузки:

* [Установщик Mac OS X][mac-installer]
* [MSI-файл Windows][windows-installer]

> [!TIP]
> В Windows можно также загрузить hello [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) tooinstall hello CLI. Это дает установщика hello параметр tooinstall дополнительных Azure SDK и средства командной строки после установки hello CLI.

## <a name="option-3-use-a-docker-container"></a>Вариант 3. Использование контейнера Docker
Если вы настроили компьютер как [Docker](https://docs.docker.com/engine/understanding-docker/) узла, можно запустить hello последнюю Azure CLI 1.0 в контейнер Docker. Выполнения hello следующую команду (в ОС Linux могут потребоваться toouse **sudo**):

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a>Выполнение команд Azure CLI 1.0
После установки hello Azure CLI 1.0 запустите hello **azure** команду из командной строки пользовательского интерфейса (Bash, терминалов, командной строки и т. д.). Например, команду help toorun hello, введите ниже hello:

```azurecli
azure help
```

> [!NOTE]
> На некоторых дистрибутивов Linux, может появиться сообщение об ошибке слишком`/usr/bin/env: ‘node’: No such file or directory`. Это связано с тем, что новые установки Node.js размещаются в папке /usr/bin/nodejs. toofix, создайте символьную ссылку слишком/usr/bin/узла, выполните следующую команду:

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

версия hello toosee hello Azure CLI 1.0 установлена, тип hello следующие:

```azurecli
azure --version
```

Теперь все готово к работе. все tooaccess hello toowork команд CLI с вашими ресурсами, [подключение tooyour подписки Azure из hello Azure CLI](xplat-cli-connect.md).

> [!NOTE]
> Во время первого использования Azure CLI, появится сообщение с вопросом, следует ли tooallow сведения об использовании Microsoft toocollect. Участие является добровольным. При выборе tooparticipate можно остановить в любой момент, выполнив `azure telemetry --disable`. tooenable участие в любое время выполнить `azure telemetry --enable`.

## <a name="update-hello-cli"></a>Обновление hello CLI
Корпорация Майкрософт выпускает часто обновленные версии hello Azure CLI. Переустановите hello CLI с помощью установщика hello для вашей операционной системы, или выполните последнюю контейнера Docker hello. Или если имеют hello последние Node.js и npm установлен, обновления, введя следующее hello (в ОС Linux могут потребоваться toouse **sudo**).

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a>Включение выполнения нажатием клавиши TAB
Выполнение команд интерфейса командной строки нажатием клавиши TAB поддерживается на компьютерах MAC и Linux.

tooenable в zsh, выполните:

```bash
echo '. <(azure --completion)' >> .zshrc
```

tooenable его в bash, выполните:

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a>Дальнейшие действия
* [Подключение из tooyour CLI hello подписки Azure](xplat-cli-connect.md) toocreate и управления ресурсами Azure.
* toolearn Дополнительные сведения о hello Azure CLI Загрузка исходного кода, сообщения о проблемах, или передавать toohello проекта см. hello [репозиторий GitHub для hello Azure CLI](https://github.com/azure/azure-xplat-cli).
* Если у вас есть вопросы по использованию hello Azure CLI или Azure, посетите hello [форумы Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
