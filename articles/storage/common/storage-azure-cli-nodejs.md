---
title: "aaaUsing hello Azure 1.0 CLI со службой хранилища Azure | Документы Microsoft"
description: "Узнайте, как toouse hello Azure командной строки (CLI Azure) 1.0 с toocreate хранилища Azure и управление учетными записями хранения и работы с файлами и больших двоичных объектов Azure. Hello Azure CLI — это средство кросс платформенных"
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: b502232a-e8f6-4d6c-befd-3476592e0e35
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: seguler
ms.openlocfilehash: 25e459403dde631741403c8722ed07beafac35c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-10-with-azure-storage"></a><span data-ttu-id="f6e5d-104">С помощью Azure CLI 1.0 hello со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="f6e5d-104">Using hello Azure CLI 1.0 with Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="f6e5d-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="f6e5d-105">Overview</span></span>

<span data-ttu-id="f6e5d-106">Hello Azure CLI предоставляет набор с открытым исходным кодом кросс платформенных команды для работы с hello платформы Azure.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-106">hello Azure CLI provides a set of open source, cross-platform commands for working with hello Azure Platform.</span></span> <span data-ttu-id="f6e5d-107">Она предоставляет большую часть hello же функциональные возможности, найденные в hello [портал Azure](https://portal.azure.com) также как сложных данных, доступ к функциям.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-107">It provides much of hello same functionality found in hello [Azure portal](https://portal.azure.com) as well as rich data access functionality.</span></span>

<span data-ttu-id="f6e5d-108">В этом руководстве мы изучим как toouse [интерфейса командной строки Azure (Azure CLI)](../../cli-install-nodejs.md) tooperform различных задач разработки и администрирования хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-108">In this guide, we'll explore how toouse [Azure Command-Line Interface (Azure CLI)](../../cli-install-nodejs.md) tooperform a variety of development and administration tasks with Azure Storage.</span></span> <span data-ttu-id="f6e5d-109">Рекомендуется загрузить и установить или обновить toohello последнюю Azure CLI перед использованием в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-109">We recommend that you download and install or upgrade toohello latest Azure CLI before using this guide.</span></span>

<span data-ttu-id="f6e5d-110">В этом руководстве предполагается, что вы понимаете основные понятия hello хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-110">This guide assumes that you understand hello basic concepts of Azure Storage.</span></span> <span data-ttu-id="f6e5d-111">Hello руководство содержит ряд сценариев использования hello toodemonstrate hello Azure CLI со службой хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-111">hello guide provides a number of scripts toodemonstrate hello usage of hello Azure CLI with Azure Storage.</span></span> <span data-ttu-id="f6e5d-112">Быть убедиться, что tooupdate hello переменные сценария, на основе конфигурации перед выполнением каждого скрипта.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-112">Be sure tooupdate hello script variables based on your configuration before running each script.</span></span>

> [!NOTE]
> <span data-ttu-id="f6e5d-113">руководство по Hello примеры hello Azure CLI команд и скриптов для классические учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-113">hello guide provides hello Azure CLI command and script examples for classic storage accounts.</span></span> <span data-ttu-id="f6e5d-114">В разделе [использование hello Azure CLI для Mac, Linux и Windows с помощью управления ресурсами Azure](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) для команды Azure CLI для учетных записей хранения Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-114">See [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) for Azure CLI commands for Resource Manager storage accounts.</span></span>
>
>

[!INCLUDE [storage-cli-versions](../../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-hello-azure-cli-in-5-minutes"></a><span data-ttu-id="f6e5d-115">Приступая к работе с хранилищем Azure и hello Azure CLI в 5 минут</span><span class="sxs-lookup"><span data-stu-id="f6e5d-115">Get started with Azure Storage and hello Azure CLI in 5 minutes</span></span>
<span data-ttu-id="f6e5d-116">В этом руководстве для демонстрации примеров используется ОС Ubuntu, но другие платформы должны работать аналогично.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-116">This guide uses Ubuntu for examples, but other OS platforms should perform similarly.</span></span>

<span data-ttu-id="f6e5d-117">**Новый tooAzure:** получить подписку Microsoft Azure и учетной записи Майкрософт, связанные с этой подпиской.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-117">**New tooAzure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="f6e5d-118">Сведения о способах приобретения Azure см. на страницах [Создайте бесплатную учетную запись Azure уже сегодня](https://azure.microsoft.com/pricing/free-trial/), [Как приобрести Azure](https://azure.microsoft.com/pricing/purchase-options/) и [Предложения для участников](https://azure.microsoft.com/pricing/member-offers/) (для подписчиков MSDN, участников Microsoft Partner Network, BizSpark и других наших программ).</span><span class="sxs-lookup"><span data-stu-id="f6e5d-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="f6e5d-119">Дополнительные сведения о подписках Azure см. на странице [Назначение ролей администратора в Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx).</span><span class="sxs-lookup"><span data-stu-id="f6e5d-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="f6e5d-120">**После создания подписки Microsoft Azure и учетной записи:**</span><span class="sxs-lookup"><span data-stu-id="f6e5d-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="f6e5d-121">Загрузите и установите Azure CLI, следуя инструкциям hello появлялся hello [Install hello Azure CLI](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f6e5d-121">Download and install hello Azure CLI following hello instructions outlined in [Install hello Azure CLI](../../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="f6e5d-122">После hello Azure CLI установлено, вы сможете может toouse hello azure команда из команды Azure CLI hello tooaccess интерфейс командной строки (Bash, терминалов, Командная строка).</span><span class="sxs-lookup"><span data-stu-id="f6e5d-122">Once hello Azure CLI has been installed, you will be able toouse hello azure command from your command-line interface (Bash, Terminal, Command prompt) tooaccess hello Azure CLI commands.</span></span> <span data-ttu-id="f6e5d-123">Тип hello _azure_ команда и вы увидите hello следующие выходные данные.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-123">Type hello _azure_ command and you should see hello following output.</span></span>

    ![Вывод команды Azure](./media/storage-azure-cli/azure_command.png)   
3. <span data-ttu-id="f6e5d-125">Hello интерфейса командной строки, введите `azure storage` toolist все hello команд хранилища azure и получить первое впечатление hello функции hello предоставляет Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-125">In hello command-line interface, type `azure storage` toolist out all hello azure storage commands and get a first impression of hello functionalities hello Azure CLI provides.</span></span> <span data-ttu-id="f6e5d-126">Можно ввести имя команды с **-h** параметра (например, `azure storage share create -h`) toosee подробные сведения о синтаксисе команды.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-126">You can type command name with **-h** parameter (for example, `azure storage share create -h`) toosee details of command syntax.</span></span>
4. <span data-ttu-id="f6e5d-127">Теперь мы указываем, простой сценарий, который показывает основные tooaccess команды Azure CLI хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-127">Now, we'll give you a simple script that shows basic Azure CLI commands tooaccess Azure Storage.</span></span> <span data-ttu-id="f6e5d-128">сценарий Hello сначала запросит tooset две переменные для учетной записи хранилища и ключа.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-128">hello script will first ask you tooset two variables for your storage account and key.</span></span> <span data-ttu-id="f6e5d-129">Затем сценарий hello создать контейнер в этой новой учетной записи хранения и отправить существующий контейнер toothat образ файла (blob).</span><span class="sxs-lookup"><span data-stu-id="f6e5d-129">Then, hello script will create a new container in this new storage account and upload an existing image file (blob) toothat container.</span></span> <span data-ttu-id="f6e5d-130">После hello скрипт перечисляет все большие двоичные объекты в этом контейнере, он будет загружен hello образ файла toohello целевой каталог, существующего на локальном компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-130">After hello script lists all blobs in that container, it will download hello image file toohello destination directory which exists on hello local computer.</span></span>

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating hello container..."
    azure storage container create $container_name

    echo "Uploading hello image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing hello blobs..."
    azure storage blob list $container_name

    echo "Downloading hello image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. <span data-ttu-id="f6e5d-131">Откройте любой текстовый редактор на локальном компьютере (например, Vim)</span><span class="sxs-lookup"><span data-stu-id="f6e5d-131">In your local computer, open your preferred text editor (vim for example).</span></span> <span data-ttu-id="f6e5d-132">Тип hello выше скрипт в текстовый редактор.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-132">Type hello above script into your text editor.</span></span>
6. <span data-ttu-id="f6e5d-133">Теперь требуется переменных сценария hello tooupdate на основании параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-133">Now, you need tooupdate hello script variables based on your configuration settings.</span></span>

   * <span data-ttu-id="f6e5d-134">**< Storage_account_name >** использовать hello с заданным именем в скрипте hello, или введите новое имя для вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-134">**<storage_account_name>** Use hello given name in hello script or enter a new name for your storage account.</span></span> <span data-ttu-id="f6e5d-135">**Важно:** hello имя учетной записи хранения hello должно быть уникальным в Azure.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-135">**Important:** hello name of hello storage account must be unique in Azure.</span></span> <span data-ttu-id="f6e5d-136">и состоять из символов нижнего регистра.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-136">It must be lowercase, too!</span></span>
   * <span data-ttu-id="f6e5d-137">**< storage_account_key >** hello ключ доступа учетной записи.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-137">**<storage_account_key>** hello access key of your storage account.</span></span>
   * <span data-ttu-id="f6e5d-138">**< Container_name >** использовать hello с заданным именем в скрипте hello, или введите новое имя для контейнера.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-138">**<container_name>** Use hello given name in hello script or enter a new name for your container.</span></span>
   * <span data-ttu-id="f6e5d-139">**< Image_to_upload >** введите рисунок tooa путь на локальном компьютере, например: «~ / images/HelloWorld.png».</span><span class="sxs-lookup"><span data-stu-id="f6e5d-139">**<image_to_upload>** Enter a path tooa picture on your local computer, such as: "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="f6e5d-140">**< Destination_folder >** файлы toostore путь локального каталога tooa загружаются из хранилища Azure, такие как ввод: «~/downloadImages».</span><span class="sxs-lookup"><span data-stu-id="f6e5d-140">**<destination_folder>** Enter a path tooa local directory toostore files downloaded from Azure Storage, such as: "~/downloadImages".</span></span>
7. <span data-ttu-id="f6e5d-141">После обновления hello необходимые переменные в vim, нажмите клавишу сочетания клавиш `ESC`, `:`, `wq!` toosave hello скрипта.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-141">After you've updated hello necessary variables in vim, press key combinations `ESC`, `:`, `wq!` toosave hello script.</span></span>
8. <span data-ttu-id="f6e5d-142">toorun этот скрипт просто типа hello имя файла скрипта в консоли bash hello.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-142">toorun this script, simply type hello script file name in hello bash console.</span></span> <span data-ttu-id="f6e5d-143">После запуска этого сценария должно быть локальную целевую папку, которая содержит файл изображения загружаются hello.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-143">After this script runs, you should have a local destination folder that includes hello downloaded image file.</span></span> <span data-ttu-id="f6e5d-144">Следующий снимок экрана приветствия показан пример выходных данных:</span><span class="sxs-lookup"><span data-stu-id="f6e5d-144">hello following screenshot shows an example output:</span></span>

<span data-ttu-id="f6e5d-145">После запуска сценария hello должно быть локальную целевую папку, которая содержит файл изображения загружаются hello.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-145">After hello script runs, you should have a local destination folder that includes hello downloaded image file.</span></span>

## <a name="manage-storage-accounts-with-hello-azure-cli"></a><span data-ttu-id="f6e5d-146">Управление учетными записями хранения с hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f6e5d-146">Manage storage accounts with hello Azure CLI</span></span>
### <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="f6e5d-147">Подключение tooyour подписки Azure</span><span class="sxs-lookup"><span data-stu-id="f6e5d-147">Connect tooyour Azure subscription</span></span>
<span data-ttu-id="f6e5d-148">Большинство команд hello хранилища будет работать без подписки Azure, но рекомендуется tooconnect tooyour подписки из hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-148">While most of hello storage commands will work without an Azure subscription, we recommend you tooconnect tooyour subscription from hello Azure CLI.</span></span> <span data-ttu-id="f6e5d-149">tooconfigure hello Azure CLI toowork с подпиской, следуйте указаниям hello [подключение tooan подписки Azure из hello Azure CLI](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="f6e5d-149">tooconfigure hello Azure CLI toowork with your subscription, follow hello steps in [Connect tooan Azure subscription from hello Azure CLI](../../xplat-cli-connect.md).</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="f6e5d-150">Создание новой учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="f6e5d-150">Create a new storage account</span></span>
<span data-ttu-id="f6e5d-151">toouse хранилища Azure, потребуется учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-151">toouse Azure storage, you will need a storage account.</span></span> <span data-ttu-id="f6e5d-152">После настройки подписки tooyour tooconnect компьютера, можно создать новую учетную запись хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-152">You can create a new Azure storage account after you have configured your computer tooconnect tooyour subscription.</span></span>

```azurecli
azure storage account create <account_name>
```

<span data-ttu-id="f6e5d-153">Hello имя учетной записи должно быть от 3 до 24 символов и содержать только строчные буквы и цифры.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-153">hello name of your storage account must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a><span data-ttu-id="f6e5d-154">Установите учетную запись хранения Azure по умолчанию в переменных среды</span><span class="sxs-lookup"><span data-stu-id="f6e5d-154">Set a default Azure storage account in environment variables</span></span>
<span data-ttu-id="f6e5d-155">В подписке может иметься несколько учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-155">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="f6e5d-156">Можно выбрать один из них и задать его в hello переменные среды для всех хранилищ hello команд hello же сеанса.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-156">You can choose one of them and set it in hello environment variables for all hello storage commands in hello same session.</span></span> <span data-ttu-id="f6e5d-157">Это позволяет toorun хранилища Azure CLI hello команды без указания hello хранилища учетной записи и ключа явным образом.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-157">This enables you toorun hello Azure CLI storage commands without specifying hello storage account and key explicitly.</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="f6e5d-158">Другой способ tooset учетной записи хранения по умолчанию использует строку подключения.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-158">Another way tooset a default storage account is using connection string.</span></span> <span data-ttu-id="f6e5d-159">Во-первых, получите строку подключения hello командой:</span><span class="sxs-lookup"><span data-stu-id="f6e5d-159">Firstly get hello connection string by command:</span></span>

```azurecli
azure storage account connectionstring show <account_name>
```

<span data-ttu-id="f6e5d-160">Затем скопируйте строку подключения для вывода hello и задать для него tooenvironment переменной:</span><span class="sxs-lookup"><span data-stu-id="f6e5d-160">Then copy hello output connection string and set it tooenvironment variable:</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a><span data-ttu-id="f6e5d-161">Создание больших двоичных объектов (BLOB-объектов) и управление ими</span><span class="sxs-lookup"><span data-stu-id="f6e5d-161">Create and manage blobs</span></span>
<span data-ttu-id="f6e5d-162">Хранилище Azure BLOB-объекта — это служба для хранения больших объемов неструктурированных данных, например текстовых или двоичных данных, который может осуществляться из любого места в Здравствуй, мир! через HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-162">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="f6e5d-163">В этом разделе предполагается, что вы уже знакомы с основными понятиями хранилища больших двоичных объектов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-163">This section assumes that you are already familiar with hello Azure Blob storage concepts.</span></span> <span data-ttu-id="f6e5d-164">Дополнительные сведения см. в статьях [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](../blobs/storage-dotnet-how-to-use-blobs.md) и [Основные понятия службы BLOB-объектов](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="f6e5d-164">For detailed information, see [Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="f6e5d-165">Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="f6e5d-165">Create a container</span></span>
<span data-ttu-id="f6e5d-166">Каждый BLOB-объект в хранилище Azure должен находиться в контейнере.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-166">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="f6e5d-167">Можно создать закрытый контейнер с помощью hello `azure storage container create` команды:</span><span class="sxs-lookup"><span data-stu-id="f6e5d-167">You can create a private container using hello `azure storage container create` command:</span></span>

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> <span data-ttu-id="f6e5d-168">Существует три уровня анонимного доступа для чтения: **Отключено**, **Большой двоичный объект** и **Контейнер**.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-168">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="f6e5d-169">tooprevent анонимный доступ к tooblobs параметр разрешения hello набора слишком**Off**.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-169">tooprevent anonymous access tooblobs, set hello Permission parameter too**Off**.</span></span> <span data-ttu-id="f6e5d-170">По умолчанию hello новый контейнер является закрытым и может осуществляться только владельцем учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-170">By default, hello new container is private and can be accessed only by hello account owner.</span></span> <span data-ttu-id="f6e5d-171">анонимные открытый tooallow чтения tooblob доступ к ресурсам, но не toocontainer метаданные или toohello список больших двоичных объектов в контейнере hello, параметру hello разрешение слишком**большого двоичного объекта**.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-171">tooallow anonymous public read access tooblob resources, but not toocontainer metadata or toohello list of blobs in hello container, set hello Permission parameter too**Blob**.</span></span> <span data-ttu-id="f6e5d-172">полный открытый tooallow чтения tooblob доступ к ресурсам, метаданные контейнера и hello список больших двоичных объектов в контейнере hello, задайте параметр разрешение hello слишком**контейнер**.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-172">tooallow full public read access tooblob resources, container metadata, and hello list of blobs in hello container, set hello Permission parameter too**Container**.</span></span> <span data-ttu-id="f6e5d-173">Дополнительные сведения см. в разделе [управления toocontainers анонимный доступ для чтения и большие двоичные объекты](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="f6e5d-173">For more information, see [Manage anonymous read access toocontainers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>
>
>

### <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="f6e5d-174">Отправка BLOB-объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="f6e5d-174">Upload a blob into a container</span></span>
<span data-ttu-id="f6e5d-175">Хранилище BLOB-объектов Azure поддерживает блочные и страничные BLOB-объекты.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-175">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="f6e5d-176">Дополнительные сведения см. в статье [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx) (Основные сведения о блочных, добавочных и страничных BLOB-объектах).</span><span class="sxs-lookup"><span data-stu-id="f6e5d-176">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="f6e5d-177">tooupload большие двоичные объекты в контейнере tooa, можно использовать hello `azure storage blob upload`.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-177">tooupload blobs in tooa container, you can use hello `azure storage blob upload`.</span></span> <span data-ttu-id="f6e5d-178">По умолчанию эта команда передает hello локальные файлы tooa блочного большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-178">By default, this command uploads hello local files tooa block blob.</span></span> <span data-ttu-id="f6e5d-179">Тип hello toospecify для hello большого двоичного объекта, вы можете использовать hello `--blobtype` параметра.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-179">toospecify hello type for hello blob, you can use hello `--blobtype` parameter.</span></span>

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a><span data-ttu-id="f6e5d-180">Загрузка BLOB-объектов из контейнера</span><span class="sxs-lookup"><span data-stu-id="f6e5d-180">Download blobs from a container</span></span>
<span data-ttu-id="f6e5d-181">Привет, в следующем примере показано, как toodownload большие двоичные объекты из контейнера.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-181">hello following example demonstrates how toodownload blobs from a container.</span></span>

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a><span data-ttu-id="f6e5d-182">Копирование BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="f6e5d-182">Copy blobs</span></span>
<span data-ttu-id="f6e5d-183">Можно асинхронно копировать BLOB-объекты между учетными записями хранения и областями или внутри них.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-183">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="f6e5d-184">Hello ниже приведен пример tooanother учетной записи toocopy больших двоичных объектов из одного места хранения.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-184">hello following example demonstrates how toocopy blobs from one storage account tooanother.</span></span> <span data-ttu-id="f6e5d-185">В этом примере мы создаем контейнер с общим анонимным доступом к BLOB-объектам.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-185">In this sample we create a container where blobs are publicly, anonymously accessible.</span></span>

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

<span data-ttu-id="f6e5d-186">В этом примере выполняется асинхронное копирование.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-186">This sample performs an asynchronous copy.</span></span> <span data-ttu-id="f6e5d-187">Можно отслеживать состояние hello каждой операции копирования, запустив hello `azure storage blob copy show` операции.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-187">You can monitor hello status of each copy operation by running hello `azure storage blob copy show` operation.</span></span>

<span data-ttu-id="f6e5d-188">Обратите внимание, что hello исходный URL-адрес, указанный для операции копирования hello должен быть общедоступным или включать токен SAS (подпись общего доступа).</span><span class="sxs-lookup"><span data-stu-id="f6e5d-188">Note that hello source URL provided for hello copy operation must either be publicly accessible, or include a SAS (shared access signature) token.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="f6e5d-189">Удаление большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="f6e5d-189">Delete a blob</span></span>
<span data-ttu-id="f6e5d-190">toodelete большого двоичного объекта используйте hello ниже команду:</span><span class="sxs-lookup"><span data-stu-id="f6e5d-190">toodelete a blob, use hello below command:</span></span>

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="f6e5d-191">Создание общих папок и управление ими</span><span class="sxs-lookup"><span data-stu-id="f6e5d-191">Create and manage file shares</span></span>
<span data-ttu-id="f6e5d-192">Хранилище файлов Azure предоставляет общее хранилище для приложений с помощью стандартного протокола SMB hello.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-192">Azure File storage offers shared storage for applications using hello standard SMB protocol.</span></span> <span data-ttu-id="f6e5d-193">Виртуальные машины Microsoft Azure и облачные службы, а также локальные приложения, могут совместно использовать данные через монтированные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-193">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="f6e5d-194">Вы можете управлять файловыми ресурсами и файл данных с помощью hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-194">You can manage file shares and file data via hello Azure CLI.</span></span> <span data-ttu-id="f6e5d-195">Дополнительные сведения о хранилище файлов Azure см. в разделе [приступить к работе с хранилищем Windows Azure файл](../storage-dotnet-how-to-use-files.md) или [как toouse хранилища Azure File с Linux](../storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f6e5d-195">For more information on Azure File storage, see [Get started with Azure File storage on Windows](../storage-dotnet-how-to-use-files.md) or [How toouse Azure File storage with Linux](../storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="f6e5d-196">Создайте общую папку</span><span class="sxs-lookup"><span data-stu-id="f6e5d-196">Create a file share</span></span>
<span data-ttu-id="f6e5d-197">Общая папка Azure представляет собой общую папку с файлами SMB в Azure.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-197">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="f6e5d-198">Все каталоги и файлы должны быть созданы в общей папке.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-198">All directories and files must be created in a file share.</span></span> <span data-ttu-id="f6e5d-199">Учетная запись может содержать неограниченное количество общих ресурсов и общую папку можно сохранить неограниченное количество файлов копирование ограничения емкости toohello hello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-199">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up toohello capacity limits of hello storage account.</span></span> <span data-ttu-id="f6e5d-200">Hello следующий пример создает общую папку с именем **myshare**.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-200">hello following example creates a file share named **myshare**.</span></span>

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="f6e5d-201">Создайте каталог</span><span class="sxs-lookup"><span data-stu-id="f6e5d-201">Create a directory</span></span>
<span data-ttu-id="f6e5d-202">Каталог обеспечивает дополнительную иерархическую структуру для общей папки Azure.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-202">A directory provides an optional hierarchical structure for an Azure file share.</span></span> <span data-ttu-id="f6e5d-203">Hello следующий пример создает каталог с именем **myDir** в общей папке hello.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-203">hello following example creates a directory named **myDir** in hello file share.</span></span>

```azurecli
azure storage directory create myshare myDir
```

<span data-ttu-id="f6e5d-204">Обратите внимание, что путь к каталогу может включать несколько уровней, *например***a/b**.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-204">Note that directory path can include multiple levels, *e.g.*, **a/b**.</span></span> <span data-ttu-id="f6e5d-205">Однако необходимо убедиться в наличии всех родительских каталогов.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-205">However, you must ensure that all parent directories exist.</span></span> <span data-ttu-id="f6e5d-206">Например, для пути **a/b** вам потребуется сначала создать каталог **a**, а затем — каталог **b**.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-206">For example, for path **a/b**, you must create directory **a** first, then create directory **b**.</span></span>

### <a name="upload-a-local-file-toodirectory"></a><span data-ttu-id="f6e5d-207">Отправка toodirectory локального файла</span><span class="sxs-lookup"><span data-stu-id="f6e5d-207">Upload a local file toodirectory</span></span>
<span data-ttu-id="f6e5d-208">Hello следующий пример отправляет файл из **~/temp/samplefile.txt** toohello **myDir** каталога.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-208">hello following example uploads a file from **~/temp/samplefile.txt** toohello **myDir** directory.</span></span> <span data-ttu-id="f6e5d-209">Измените путь к файлу hello, которое указывает допустимый файл tooa на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-209">Edit hello file path so that it points tooa valid file on your local machine:</span></span>

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

<span data-ttu-id="f6e5d-210">Обратите внимание, что может быть файл в общей папке hello вверх too1 ТБ.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-210">Note that a file in hello share can be up too1 TB in size.</span></span>

### <a name="list-hello-files-in-hello-share-root-or-directory"></a><span data-ttu-id="f6e5d-211">Список файлов hello в корневой папке hello или каталога</span><span class="sxs-lookup"><span data-stu-id="f6e5d-211">List hello files in hello share root or directory</span></span>
<span data-ttu-id="f6e5d-212">Можно перечислить hello файлов и подкаталогов в корневой общей папки или каталога, используя hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f6e5d-212">You can list hello files and subdirectories in a share root or a directory using hello following command:</span></span>

```azurecli
azure storage file list myshare myDir
```

<span data-ttu-id="f6e5d-213">Обратите внимание, что имя каталога, hello является необязательным для операции перечисления hello.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-213">Note that hello directory name is optional for hello listing operation.</span></span> <span data-ttu-id="f6e5d-214">Если не указано, команда hello перечисляет содержимое hello hello корневой каталог общего ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-214">If omitted, hello command lists hello contents of hello root directory of hello share.</span></span>

### <a name="copy-files"></a><span data-ttu-id="f6e5d-215">Копирование файлов</span><span class="sxs-lookup"><span data-stu-id="f6e5d-215">Copy files</span></span>
<span data-ttu-id="f6e5d-216">Начиная с версии 0.9.8 Azure CLI, можно скопировать файл tooanother, большой двоичный объект файла tooa или tooa файла большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-216">Beginning with version 0.9.8 of Azure CLI, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="f6e5d-217">Ниже показано как tooperform их копирования операции с помощью команды CLI.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-217">Below we demonstrate how tooperform these copy operations using CLI commands.</span></span> <span data-ttu-id="f6e5d-218">toocopy новый каталог toohello файла:</span><span class="sxs-lookup"><span data-stu-id="f6e5d-218">toocopy a file toohello new directory:</span></span>

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

<span data-ttu-id="f6e5d-219">toocopy tooa файла большого двоичного объекта каталога:</span><span class="sxs-lookup"><span data-stu-id="f6e5d-219">toocopy a blob tooa file directory:</span></span>

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a><span data-ttu-id="f6e5d-220">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f6e5d-220">Next Steps</span></span>

<span data-ttu-id="f6e5d-221">Справочник по командам Azure CLI 1.0 для работы с ресурсами службы хранилища можно найти здесь:</span><span class="sxs-lookup"><span data-stu-id="f6e5d-221">You can find Azure CLI 1.0 command reference for working with Storage resources here:</span></span>

* [<span data-ttu-id="f6e5d-222">Команды Azure CLI в режиме Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f6e5d-222">Azure CLI commands in Resource Manager mode</span></span>](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [<span data-ttu-id="f6e5d-223">Установка Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f6e5d-223">Azure CLI commands in Azure Service Management mode</span></span>](../../cli-install-nodejs.md)

<span data-ttu-id="f6e5d-224">Хотелось tootry hello [Azure CLI 2.0](../storage-azure-cli.md), нашей CLI следующего поколения, написанные на Python, для использования в модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="f6e5d-224">You may also like tootry hello [Azure CLI 2.0](../storage-azure-cli.md), our next-generation CLI written in Python, for use with hello Resource Manager deployment model.</span></span>
