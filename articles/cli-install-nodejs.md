---
title: "Установка Azure CLI 1.0 | Документация Майкрософт"
description: "Установка Azure CLI 1.0 на компьютерах Mac OS, Linux и Windows и начало работы со службами Azure."
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
ms.openlocfilehash: 63b35ed25b809a16b61b685fd35aa67474b0a369
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="install-the-azure-cli-10"></a><span data-ttu-id="c48e5-103">Установка Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c48e5-103">Install the Azure CLI 1.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c48e5-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c48e5-104">PowerShell</span></span>](/powershell/azure/overview)
> * [<span data-ttu-id="c48e5-105">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c48e5-105">Azure CLI 1.0</span></span>](cli-install-nodejs.md)
> * [<span data-ttu-id="c48e5-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c48e5-106">Azure CLI 2.0</span></span>](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> <span data-ttu-id="c48e5-107">В этом разделе описывается, как установить Azure CLI 1.0, который основан на NodeJS и поддерживает все вызовы API классического развертывания, а также множество действий развертывания Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c48e5-107">This topic describes how to install the Azure CLI 1.0, which is built on nodeJs and supports all classic deployment API calls as well as a large number of Resource Manager deployment activities.</span></span> <span data-ttu-id="c48e5-108">Следует использовать [Azure CLI 2.0](/cli/azure/overview) для развертывания новых и перспективных служб и управления ими.</span><span class="sxs-lookup"><span data-stu-id="c48e5-108">You should use the [Azure CLI 2.0](/cli/azure/overview) for new or forward-looking CLI deployments and management.</span></span>

<span data-ttu-id="c48e5-109">Вы можете выполнить быструю установку интерфейса командной строки Azure (Azure CLI 1.0), чтобы использовать набор консольных команд с открытым кодом для управления ресурсами в среде Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c48e5-109">Quickly install the Azure Command-Line Interface (Azure CLI 1.0) to use a set of open-source shell-based commands for creating and managing resources in Microsoft Azure.</span></span> <span data-ttu-id="c48e5-110">Существует несколько вариантов установки этих кроссплатформенных инструментов на компьютер.</span><span class="sxs-lookup"><span data-stu-id="c48e5-110">You have several options to install these cross-platform tools on your computer:</span></span>

* <span data-ttu-id="c48e5-111">**Пакет npm**. Запустите npm (диспетчер пакетов для JavaScript), чтобы установить последнюю версию пакета для Azure CLI 1.0 в дистрибутиве или ОС Linux.</span><span class="sxs-lookup"><span data-stu-id="c48e5-111">**npm package** - Run npm (the package manager for JavaScript) to install the latest Azure CLI 1.0 package on your Linux distribution or OS.</span></span> <span data-ttu-id="c48e5-112">На компьютере должны быть установлены node.js и npm.</span><span class="sxs-lookup"><span data-stu-id="c48e5-112">Requires node.js and npm on your computer.</span></span>
* <span data-ttu-id="c48e5-113">**Установщик**. Скачайте установщик, чтобы легко установить эти инструменты на компьютеры Mac или Windows.</span><span class="sxs-lookup"><span data-stu-id="c48e5-113">**Installer** - Download an installer for easy installation on Mac or Windows.</span></span>
* <span data-ttu-id="c48e5-114">**Контейнер Docker**. Приступите к использованию последней версии интерфейса командной строки из готового контейнера Docker.</span><span class="sxs-lookup"><span data-stu-id="c48e5-114">**Docker container** - Start using the latest CLI in a ready-to-run Docker container.</span></span> <span data-ttu-id="c48e5-115">На компьютере требуется наличие узла Docker.</span><span class="sxs-lookup"><span data-stu-id="c48e5-115">Requires Docker host on your computer.</span></span>

<span data-ttu-id="c48e5-116">Дополнительные сведения и варианты установки см. в репозитории проектов на сайте [GitHub](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="c48e5-116">For more options and background, see the project repository on [GitHub](https://github.com/azure/azure-xplat-cli).</span></span>

<span data-ttu-id="c48e5-117">После установки Azure CLI 1.0 вы сможете [подключить его к своей подписке Azure](xplat-cli-connect.md) и работать с ресурсами Azure c помощью команд **azure** из интерфейса командной строки (Bash, терминала, командной строки и т. д.).</span><span class="sxs-lookup"><span data-stu-id="c48e5-117">Once the Azure CLI 1.0 is installed, [connect it with your Azure subscription](xplat-cli-connect.md) and run the **azure** commands from your command-line interface (Bash, Terminal, Command prompt, and so on) to work with your Azure resources.</span></span>

## <a name="option-1-install-an-npm-package"></a><span data-ttu-id="c48e5-118">Вариант 1. Установка пакета npm</span><span class="sxs-lookup"><span data-stu-id="c48e5-118">Option 1: Install an npm package</span></span>
<span data-ttu-id="c48e5-119">Для установки интерфейса командной строки из пакета NPM в системе должна быть установлена [последняя версия Node.js и npm](https://nodejs.org/en/download/package-manager/).</span><span class="sxs-lookup"><span data-stu-id="c48e5-119">To install the CLI from an npm package, make sure you have downloaded and installed the [latest Node.js and npm](https://nodejs.org/en/download/package-manager/).</span></span> <span data-ttu-id="c48e5-120">Затем запустите **npm install** для установки пакета azure-cli:</span><span class="sxs-lookup"><span data-stu-id="c48e5-120">Then, run **npm install** to install the azure-cli package:</span></span>

```bash
npm install -g azure-cli
```

<span data-ttu-id="c48e5-121">В системах Linux для выполнения команды **npm** может потребоваться команда **sudo**:</span><span class="sxs-lookup"><span data-stu-id="c48e5-121">On Linux distributions, you might need to use **sudo** to successfully run the **npm** command, as follows:</span></span>

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> <span data-ttu-id="c48e5-122">Если необходимо установить или обновить Node.js и npm в дистрибутиве или ОС Linux, рекомендуется установить последнюю версию Node.js LTS (4.x).</span><span class="sxs-lookup"><span data-stu-id="c48e5-122">If you need to install or update Node.js and npm on your Linux distribution or OS, we recommend that you install the most recent Node.js LTS version (4.x).</span></span> <span data-ttu-id="c48e5-123">Если вы используете более раннюю версию, возможны ошибки при установке.</span><span class="sxs-lookup"><span data-stu-id="c48e5-123">If you use an older version, you might get installation errors.</span></span>

<span data-ttu-id="c48e5-124">Если хотите, скачайте последнюю версию [TAR-файла][linux-installer] пакета npm для Linux на локальный компьютер.</span><span class="sxs-lookup"><span data-stu-id="c48e5-124">If you prefer, download the latest Linux [tar file][linux-installer] for the npm package locally.</span></span> <span data-ttu-id="c48e5-125">Затем установите скачанный пакет npm, как описано ниже (для дистрибутивов Linux может потребоваться использовать **sudo**).</span><span class="sxs-lookup"><span data-stu-id="c48e5-125">Then, install the downloaded npm package as follows (on Linux distributions you might need to use **sudo**):</span></span>

```bash
npm install -g <path to downloaded tar file>
```

## <a name="option-2-use-an-installer"></a><span data-ttu-id="c48e5-126">Вариант 2. Использование установщика</span><span class="sxs-lookup"><span data-stu-id="c48e5-126">Option 2: Use an installer</span></span>
<span data-ttu-id="c48e5-127">При использовании компьютера Windows или Mac можно скачать следующие установщики интерфейса командной строки:</span><span class="sxs-lookup"><span data-stu-id="c48e5-127">If you use a Mac or Windows computer, the following CLI installers are available for download:</span></span>

* <span data-ttu-id="c48e5-128">[Установщик Mac OS X][mac-installer]</span><span class="sxs-lookup"><span data-stu-id="c48e5-128">[Mac OS X installer][mac-installer]</span></span>
* <span data-ttu-id="c48e5-129">[MSI-файл Windows][windows-installer]</span><span class="sxs-lookup"><span data-stu-id="c48e5-129">[Windows MSI][windows-installer]</span></span>

> [!TIP]
> <span data-ttu-id="c48e5-130">В Windows для установки интерфейса командной строки можно также скачать [установщик веб-платформы](https://go.microsoft.com/?linkid=9828653) .</span><span class="sxs-lookup"><span data-stu-id="c48e5-130">On Windows, you can also download the [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) to install the CLI.</span></span> <span data-ttu-id="c48e5-131">Этот установщик дает возможность установить дополнительный пакет SDK для Azure и программы командной строки после установки интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="c48e5-131">This installer gives you the option to install additional Azure SDK and command-line tools after installing the CLI.</span></span>

## <a name="option-3-use-a-docker-container"></a><span data-ttu-id="c48e5-132">Вариант 3. Использование контейнера Docker</span><span class="sxs-lookup"><span data-stu-id="c48e5-132">Option 3: Use a Docker container</span></span>
<span data-ttu-id="c48e5-133">Если вы настроили компьютер в качестве узла [Docker](https://docs.docker.com/engine/understanding-docker/), то можете запустить последнюю версию Azure CLI 1.0 в контейнере Docker.</span><span class="sxs-lookup"><span data-stu-id="c48e5-133">If you have set up your computer as a [Docker](https://docs.docker.com/engine/understanding-docker/) host, you can run the latest Azure CLI 1.0 in a Docker container.</span></span> <span data-ttu-id="c48e5-134">Выполните следующую команду (в системах Linux для выполнения команды npm может потребоваться команда **sudo**):</span><span class="sxs-lookup"><span data-stu-id="c48e5-134">Run the following command (on Linux distributions you might need to use **sudo**):</span></span>

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a><span data-ttu-id="c48e5-135">Выполнение команд Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c48e5-135">Run Azure CLI 1.0 commands</span></span>
<span data-ttu-id="c48e5-136">После установки Azure CLI 1.0 команду **azure** можно выполнить в любом пользовательском интерфейсе командной строки (Bash, терминале, командной строке и т. д.).</span><span class="sxs-lookup"><span data-stu-id="c48e5-136">After the Azure CLI 1.0 is installed, run the **azure** command from your command-line user interface (Bash, Terminal, Command prompt, and so on).</span></span> <span data-ttu-id="c48e5-137">Например, чтобы выполнить команду справки, введите следующее:</span><span class="sxs-lookup"><span data-stu-id="c48e5-137">For example, to run the help command, type the following:</span></span>

```azurecli
azure help
```

> [!NOTE]
> <span data-ttu-id="c48e5-138">Для некоторых дистрибутивов Linux может появиться сообщение об ошибке `/usr/bin/env: ‘node’: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="c48e5-138">On some Linux distributions, you may receive an error similar to `/usr/bin/env: ‘node’: No such file or directory`.</span></span> <span data-ttu-id="c48e5-139">Это связано с тем, что новые установки Node.js размещаются в папке /usr/bin/nodejs.</span><span class="sxs-lookup"><span data-stu-id="c48e5-139">This error comes from recent installations of Node.js being installed at /usr/bin/nodejs.</span></span> <span data-ttu-id="c48e5-140">Для устранения этой ошибки создайте символьную ссылку /usr/bin/node, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c48e5-140">To fix it, create a symbolic link to /usr/bin/node by running this command:</span></span>

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

<span data-ttu-id="c48e5-141">Чтобы просмотреть версию установленного интерфейса Azure CLI 1.0, введите следующую команду.</span><span class="sxs-lookup"><span data-stu-id="c48e5-141">To see the version of the Azure CLI 1.0 you installed, type the following:</span></span>

```azurecli
azure --version
```

<span data-ttu-id="c48e5-142">Теперь все готово к работе.</span><span class="sxs-lookup"><span data-stu-id="c48e5-142">Now you are ready!</span></span> <span data-ttu-id="c48e5-143">Чтобы получить доступ ко всем командам интерфейса командной строки для работы с ресурсами, [подключитесь к подписке Azure из интерфейса командной строки Azure](xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="c48e5-143">To access all the CLI commands to work with your own resources, [connect to your Azure subscription from the Azure CLI](xplat-cli-connect.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c48e5-144">При первом использовании Azure CLI появится сообщение с вопросом, следует ли разрешить корпорации Майкрософт собирать сведения об использовании.</span><span class="sxs-lookup"><span data-stu-id="c48e5-144">When you first use Azure CLI, you see a message asking if you want to allow Microsoft to collect usage information.</span></span> <span data-ttu-id="c48e5-145">Участие является добровольным.</span><span class="sxs-lookup"><span data-stu-id="c48e5-145">Participation is voluntary.</span></span> <span data-ttu-id="c48e5-146">Если вы согласились участвовать в этой программе, сбор сведений можно остановить в любой момент, выполнив команду `azure telemetry --disable`.</span><span class="sxs-lookup"><span data-stu-id="c48e5-146">If you choose to participate, you can stop at any time by running `azure telemetry --disable`.</span></span> <span data-ttu-id="c48e5-147">Чтобы включить участие в любой момент, выполните команду `azure telemetry --enable`.</span><span class="sxs-lookup"><span data-stu-id="c48e5-147">To enable participation at any time, run `azure telemetry --enable`.</span></span>

## <a name="update-the-cli"></a><span data-ttu-id="c48e5-148">Обновление интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="c48e5-148">Update the CLI</span></span>
<span data-ttu-id="c48e5-149">Корпорация Майкрософт часто выпускает обновленные версии Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c48e5-149">Microsoft frequently releases updated versions of the Azure CLI.</span></span> <span data-ttu-id="c48e5-150">Переустановите интерфейс командной строки с помощью установщика для соответствующей операционной системы или запустите актуальную версию контейнера Docker.</span><span class="sxs-lookup"><span data-stu-id="c48e5-150">Reinstall the CLI using the installer for your operating system, or run the latest Docker container.</span></span> <span data-ttu-id="c48e5-151">Если вы установили последние версии Node.js и NPM, введите следующую команду (в системах Linux может потребоваться использовать режим **sudo**).</span><span class="sxs-lookup"><span data-stu-id="c48e5-151">Or, if you have the latest Node.js and npm installed, update by typing the following (on Linux distributions you might need to use **sudo**).</span></span>

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a><span data-ttu-id="c48e5-152">Включение выполнения нажатием клавиши TAB</span><span class="sxs-lookup"><span data-stu-id="c48e5-152">Enable tab completion</span></span>
<span data-ttu-id="c48e5-153">Выполнение команд интерфейса командной строки нажатием клавиши TAB поддерживается на компьютерах MAC и Linux.</span><span class="sxs-lookup"><span data-stu-id="c48e5-153">Tab completion of CLI commands is supported for Mac and Linux.</span></span>

<span data-ttu-id="c48e5-154">Чтобы включить эту функцию в zsh, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c48e5-154">To enable it in zsh, run:</span></span>

```bash
echo '. <(azure --completion)' >> .zshrc
```

<span data-ttu-id="c48e5-155">Чтобы включить эту функцию в bash, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c48e5-155">To enable it in bash, run:</span></span>

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a><span data-ttu-id="c48e5-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c48e5-156">Next steps</span></span>
* <span data-ttu-id="c48e5-157">[Подключитесь к подписке Azure из интерфейса командной строки](xplat-cli-connect.md) для создания ресурсов Azure и управления ими.</span><span class="sxs-lookup"><span data-stu-id="c48e5-157">[Connect from the CLI to your Azure subscription](xplat-cli-connect.md) to create and manage Azure resources.</span></span>
* <span data-ttu-id="c48e5-158">Для того чтобы получить дополнительные сведения об интерфейсе командной строки Azure, скачать исходный код, сообщить о проблемах или принять участие в проекте, зайдите в [репозиторий GitHub для интерфейса командной строки Azure](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="c48e5-158">To learn more about the Azure CLI, download source code, report problems, or contribute to the project, visit the [GitHub repository for the Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="c48e5-159">Если у вас возникли вопросы об использовании интерфейса командной строки Azure или платформы Azure, посетите [форумы Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span><span class="sxs-lookup"><span data-stu-id="c48e5-159">If you have questions about using the Azure CLI, or Azure, visit the [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
