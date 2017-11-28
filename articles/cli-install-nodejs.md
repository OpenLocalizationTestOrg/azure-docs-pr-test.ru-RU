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
# <a name="install-hello-azure-cli-10"></a><span data-ttu-id="e4bb4-103">Установка hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e4bb4-103">Install hello Azure CLI 1.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e4bb4-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e4bb4-104">PowerShell</span></span>](/powershell/azure/overview)
> * [<span data-ttu-id="e4bb4-105">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e4bb4-105">Azure CLI 1.0</span></span>](cli-install-nodejs.md)
> * [<span data-ttu-id="e4bb4-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e4bb4-106">Azure CLI 2.0</span></span>](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> <span data-ttu-id="e4bb4-107">Описывается, как вызовы tooinstall hello Azure CLI 1.0, которая основана на nodeJs и поддерживает все API классического развертывания и большое количество действий развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e4bb4-107">This topic describes how tooinstall hello Azure CLI 1.0, which is built on nodeJs and supports all classic deployment API calls as well as a large number of Resource Manager deployment activities.</span></span> <span data-ttu-id="e4bb4-108">Следует использовать hello [Azure CLI 2.0](/cli/azure/overview) нового и перспективных CLI развертывания и управления.</span><span class="sxs-lookup"><span data-stu-id="e4bb4-108">You should use hello [Azure CLI 2.0](/cli/azure/overview) for new or forward-looking CLI deployments and management.</span></span>

<span data-ttu-id="e4bb4-109">Быстро установите интерфейс командной строки Azure (Azure CLI 1.0) hello toouse набор команд командной строки открытым исходным кодом, для создания и управления ресурсами в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e4bb4-109">Quickly install hello Azure Command-Line Interface (Azure CLI 1.0) toouse a set of open-source shell-based commands for creating and managing resources in Microsoft Azure.</span></span> <span data-ttu-id="e4bb4-110">У вас есть несколько вариантов tooinstall эти средства кросс платформенных на вашем компьютере:</span><span class="sxs-lookup"><span data-stu-id="e4bb4-110">You have several options tooinstall these cross-platform tools on your computer:</span></span>

* <span data-ttu-id="e4bb4-111">**пакет npm** — выполнения npm (hello диспетчер пакетов для JavaScript) tooinstall hello последнюю версию Azure CLI 1.0 пакета в дистрибутив Linux или ОС.</span><span class="sxs-lookup"><span data-stu-id="e4bb4-111">**npm package** - Run npm (hello package manager for JavaScript) tooinstall hello latest Azure CLI 1.0 package on your Linux distribution or OS.</span></span> <span data-ttu-id="e4bb4-112">На компьютере должны быть установлены node.js и npm.</span><span class="sxs-lookup"><span data-stu-id="e4bb4-112">Requires node.js and npm on your computer.</span></span>
* <span data-ttu-id="e4bb4-113">**Установщик**. Скачайте установщик, чтобы легко установить эти инструменты на компьютеры Mac или Windows.</span><span class="sxs-lookup"><span data-stu-id="e4bb4-113">**Installer** - Download an installer for easy installation on Mac or Windows.</span></span>
* <span data-ttu-id="e4bb4-114">**Контейнер docker** — начать использование hello последнюю CLI в контейнер Docker готов к запуску.</span><span class="sxs-lookup"><span data-stu-id="e4bb4-114">**Docker container** - Start using hello latest CLI in a ready-to-run Docker container.</span></span> <span data-ttu-id="e4bb4-115">На компьютере требуется наличие узла Docker.</span><span class="sxs-lookup"><span data-stu-id="e4bb4-115">Requires Docker host on your computer.</span></span>

<span data-ttu-id="e4bb4-116">Дополнительные параметры и фона, см. репозиторий проекта hello [GitHub](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="e4bb4-116">For more options and background, see hello project repository on [GitHub](https://github.com/azure/azure-xplat-cli).</span></span>

<span data-ttu-id="e4bb4-117">После установки hello Azure CLI 1.0 [подключить к подписке Azure](xplat-cli-connect.md) и выполнения hello **azure** команды из интерфейса командной строки (Bash, терминалов, командной строки и т. д.) toowork с ресурсы Azure.</span><span class="sxs-lookup"><span data-stu-id="e4bb4-117">Once hello Azure CLI 1.0 is installed, [connect it with your Azure subscription](xplat-cli-connect.md) and run hello **azure** commands from your command-line interface (Bash, Terminal, Command prompt, and so on) toowork with your Azure resources.</span></span>

## <a name="option-1-install-an-npm-package"></a><span data-ttu-id="e4bb4-118">Вариант 1. Установка пакета npm</span><span class="sxs-lookup"><span data-stu-id="e4bb4-118">Option 1: Install an npm package</span></span>
<span data-ttu-id="e4bb4-119">hello tooinstall CLI из пакета npm убедитесь, вы загрузили и установили hello [последние Node.js и npm](https://nodejs.org/en/download/package-manager/).</span><span class="sxs-lookup"><span data-stu-id="e4bb4-119">tooinstall hello CLI from an npm package, make sure you have downloaded and installed hello [latest Node.js and npm](https://nodejs.org/en/download/package-manager/).</span></span> <span data-ttu-id="e4bb4-120">Затем запустите **установки npm** tooinstall hello azure cli пакета:</span><span class="sxs-lookup"><span data-stu-id="e4bb4-120">Then, run **npm install** tooinstall hello azure-cli package:</span></span>

```bash
npm install -g azure-cli
```

<span data-ttu-id="e4bb4-121">На дистрибутивов Linux, может потребоваться toouse **sudo** toosuccessfully запуска hello **npm** команды, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="e4bb4-121">On Linux distributions, you might need toouse **sudo** toosuccessfully run hello **npm** command, as follows:</span></span>

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> <span data-ttu-id="e4bb4-122">При необходимости tooinstall или обновлении Node.js и npm в дистрибутив Linux или операционной системы, рекомендуется установить последнюю версию Node.js LTS hello (4.x).</span><span class="sxs-lookup"><span data-stu-id="e4bb4-122">If you need tooinstall or update Node.js and npm on your Linux distribution or OS, we recommend that you install hello most recent Node.js LTS version (4.x).</span></span> <span data-ttu-id="e4bb4-123">Если вы используете более раннюю версию, возможны ошибки при установке.</span><span class="sxs-lookup"><span data-stu-id="e4bb4-123">If you use an older version, you might get installation errors.</span></span>

<span data-ttu-id="e4bb4-124">Если вы предпочитаете загрузить hello последнюю Linux [tar-файл] [ linux-installer] hello npm пакета локально.</span><span class="sxs-lookup"><span data-stu-id="e4bb4-124">If you prefer, download hello latest Linux [tar file][linux-installer] for hello npm package locally.</span></span> <span data-ttu-id="e4bb4-125">Установите hello загруженный npm следующим образом (в ОС Linux могут потребоваться toouse **sudo**):</span><span class="sxs-lookup"><span data-stu-id="e4bb4-125">Then, install hello downloaded npm package as follows (on Linux distributions you might need toouse **sudo**):</span></span>

```bash
npm install -g <path toodownloaded tar file>
```

## <a name="option-2-use-an-installer"></a><span data-ttu-id="e4bb4-126">Вариант 2. Использование установщика</span><span class="sxs-lookup"><span data-stu-id="e4bb4-126">Option 2: Use an installer</span></span>
<span data-ttu-id="e4bb4-127">Если вы используете компьютер Mac и Windows, следующие установщики CLI hello доступны для загрузки:</span><span class="sxs-lookup"><span data-stu-id="e4bb4-127">If you use a Mac or Windows computer, hello following CLI installers are available for download:</span></span>

* <span data-ttu-id="e4bb4-128">[Установщик Mac OS X][mac-installer]</span><span class="sxs-lookup"><span data-stu-id="e4bb4-128">[Mac OS X installer][mac-installer]</span></span>
* <span data-ttu-id="e4bb4-129">[MSI-файл Windows][windows-installer]</span><span class="sxs-lookup"><span data-stu-id="e4bb4-129">[Windows MSI][windows-installer]</span></span>

> [!TIP]
> <span data-ttu-id="e4bb4-130">В Windows можно также загрузить hello [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) tooinstall hello CLI.</span><span class="sxs-lookup"><span data-stu-id="e4bb4-130">On Windows, you can also download hello [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) tooinstall hello CLI.</span></span> <span data-ttu-id="e4bb4-131">Это дает установщика hello параметр tooinstall дополнительных Azure SDK и средства командной строки после установки hello CLI.</span><span class="sxs-lookup"><span data-stu-id="e4bb4-131">This installer gives you hello option tooinstall additional Azure SDK and command-line tools after installing hello CLI.</span></span>

## <a name="option-3-use-a-docker-container"></a><span data-ttu-id="e4bb4-132">Вариант 3. Использование контейнера Docker</span><span class="sxs-lookup"><span data-stu-id="e4bb4-132">Option 3: Use a Docker container</span></span>
<span data-ttu-id="e4bb4-133">Если вы настроили компьютер как [Docker](https://docs.docker.com/engine/understanding-docker/) узла, можно запустить hello последнюю Azure CLI 1.0 в контейнер Docker.</span><span class="sxs-lookup"><span data-stu-id="e4bb4-133">If you have set up your computer as a [Docker](https://docs.docker.com/engine/understanding-docker/) host, you can run hello latest Azure CLI 1.0 in a Docker container.</span></span> <span data-ttu-id="e4bb4-134">Выполнения hello следующую команду (в ОС Linux могут потребоваться toouse **sudo**):</span><span class="sxs-lookup"><span data-stu-id="e4bb4-134">Run hello following command (on Linux distributions you might need toouse **sudo**):</span></span>

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a><span data-ttu-id="e4bb4-135">Выполнение команд Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e4bb4-135">Run Azure CLI 1.0 commands</span></span>
<span data-ttu-id="e4bb4-136">После установки hello Azure CLI 1.0 запустите hello **azure** команду из командной строки пользовательского интерфейса (Bash, терминалов, командной строки и т. д.).</span><span class="sxs-lookup"><span data-stu-id="e4bb4-136">After hello Azure CLI 1.0 is installed, run hello **azure** command from your command-line user interface (Bash, Terminal, Command prompt, and so on).</span></span> <span data-ttu-id="e4bb4-137">Например, команду help toorun hello, введите ниже hello:</span><span class="sxs-lookup"><span data-stu-id="e4bb4-137">For example, toorun hello help command, type hello following:</span></span>

```azurecli
azure help
```

> [!NOTE]
> <span data-ttu-id="e4bb4-138">На некоторых дистрибутивов Linux, может появиться сообщение об ошибке слишком`/usr/bin/env: ‘node’: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="e4bb4-138">On some Linux distributions, you may receive an error similar too`/usr/bin/env: ‘node’: No such file or directory`.</span></span> <span data-ttu-id="e4bb4-139">Это связано с тем, что новые установки Node.js размещаются в папке /usr/bin/nodejs.</span><span class="sxs-lookup"><span data-stu-id="e4bb4-139">This error comes from recent installations of Node.js being installed at /usr/bin/nodejs.</span></span> <span data-ttu-id="e4bb4-140">toofix, создайте символьную ссылку слишком/usr/bin/узла, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e4bb4-140">toofix it, create a symbolic link too/usr/bin/node by running this command:</span></span>

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

<span data-ttu-id="e4bb4-141">версия hello toosee hello Azure CLI 1.0 установлена, тип hello следующие:</span><span class="sxs-lookup"><span data-stu-id="e4bb4-141">toosee hello version of hello Azure CLI 1.0 you installed, type hello following:</span></span>

```azurecli
azure --version
```

<span data-ttu-id="e4bb4-142">Теперь все готово к работе.</span><span class="sxs-lookup"><span data-stu-id="e4bb4-142">Now you are ready!</span></span> <span data-ttu-id="e4bb4-143">все tooaccess hello toowork команд CLI с вашими ресурсами, [подключение tooyour подписки Azure из hello Azure CLI](xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="e4bb4-143">tooaccess all hello CLI commands toowork with your own resources, [connect tooyour Azure subscription from hello Azure CLI](xplat-cli-connect.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e4bb4-144">Во время первого использования Azure CLI, появится сообщение с вопросом, следует ли tooallow сведения об использовании Microsoft toocollect.</span><span class="sxs-lookup"><span data-stu-id="e4bb4-144">When you first use Azure CLI, you see a message asking if you want tooallow Microsoft toocollect usage information.</span></span> <span data-ttu-id="e4bb4-145">Участие является добровольным.</span><span class="sxs-lookup"><span data-stu-id="e4bb4-145">Participation is voluntary.</span></span> <span data-ttu-id="e4bb4-146">При выборе tooparticipate можно остановить в любой момент, выполнив `azure telemetry --disable`.</span><span class="sxs-lookup"><span data-stu-id="e4bb4-146">If you choose tooparticipate, you can stop at any time by running `azure telemetry --disable`.</span></span> <span data-ttu-id="e4bb4-147">tooenable участие в любое время выполнить `azure telemetry --enable`.</span><span class="sxs-lookup"><span data-stu-id="e4bb4-147">tooenable participation at any time, run `azure telemetry --enable`.</span></span>

## <a name="update-hello-cli"></a><span data-ttu-id="e4bb4-148">Обновление hello CLI</span><span class="sxs-lookup"><span data-stu-id="e4bb4-148">Update hello CLI</span></span>
<span data-ttu-id="e4bb4-149">Корпорация Майкрософт выпускает часто обновленные версии hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e4bb4-149">Microsoft frequently releases updated versions of hello Azure CLI.</span></span> <span data-ttu-id="e4bb4-150">Переустановите hello CLI с помощью установщика hello для вашей операционной системы, или выполните последнюю контейнера Docker hello.</span><span class="sxs-lookup"><span data-stu-id="e4bb4-150">Reinstall hello CLI using hello installer for your operating system, or run hello latest Docker container.</span></span> <span data-ttu-id="e4bb4-151">Или если имеют hello последние Node.js и npm установлен, обновления, введя следующее hello (в ОС Linux могут потребоваться toouse **sudo**).</span><span class="sxs-lookup"><span data-stu-id="e4bb4-151">Or, if you have hello latest Node.js and npm installed, update by typing hello following (on Linux distributions you might need toouse **sudo**).</span></span>

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a><span data-ttu-id="e4bb4-152">Включение выполнения нажатием клавиши TAB</span><span class="sxs-lookup"><span data-stu-id="e4bb4-152">Enable tab completion</span></span>
<span data-ttu-id="e4bb4-153">Выполнение команд интерфейса командной строки нажатием клавиши TAB поддерживается на компьютерах MAC и Linux.</span><span class="sxs-lookup"><span data-stu-id="e4bb4-153">Tab completion of CLI commands is supported for Mac and Linux.</span></span>

<span data-ttu-id="e4bb4-154">tooenable в zsh, выполните:</span><span class="sxs-lookup"><span data-stu-id="e4bb4-154">tooenable it in zsh, run:</span></span>

```bash
echo '. <(azure --completion)' >> .zshrc
```

<span data-ttu-id="e4bb4-155">tooenable его в bash, выполните:</span><span class="sxs-lookup"><span data-stu-id="e4bb4-155">tooenable it in bash, run:</span></span>

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a><span data-ttu-id="e4bb4-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e4bb4-156">Next steps</span></span>
* <span data-ttu-id="e4bb4-157">[Подключение из tooyour CLI hello подписки Azure](xplat-cli-connect.md) toocreate и управления ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="e4bb4-157">[Connect from hello CLI tooyour Azure subscription](xplat-cli-connect.md) toocreate and manage Azure resources.</span></span>
* <span data-ttu-id="e4bb4-158">toolearn Дополнительные сведения о hello Azure CLI Загрузка исходного кода, сообщения о проблемах, или передавать toohello проекта см. hello [репозиторий GitHub для hello Azure CLI](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="e4bb4-158">toolearn more about hello Azure CLI, download source code, report problems, or contribute toohello project, visit hello [GitHub repository for hello Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="e4bb4-159">Если у вас есть вопросы по использованию hello Azure CLI или Azure, посетите hello [форумы Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span><span class="sxs-lookup"><span data-stu-id="e4bb4-159">If you have questions about using hello Azure CLI, or Azure, visit hello [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
