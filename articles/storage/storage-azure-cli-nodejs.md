---
title: "Использование Azure CLI 1.0 со службой хранилища Azure | Документация Майкрософт"
description: "Узнайте, как использовать интерфейс командной строки Azure (Azure CLI) версии 1.0 для создания учетных записей хранения и управления ими, а также для работы с большими двоичными объектами и файлами Azure в службе хранилища Azure. Azure CLI — это кроссплатформенное средство"
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
ms.openlocfilehash: b246d8813a41d353a9c0fa31fe838e025fc93046
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-cli-10-with-azure-storage"></a><span data-ttu-id="73d66-104">Использование Azure CLI 1.0 со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="73d66-104">Using the Azure CLI 1.0 with Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="73d66-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="73d66-105">Overview</span></span>

<span data-ttu-id="73d66-106">Интерфейс командной строки Azure представляет собой набор межплатформенных команд с открытым кодом для работы с платформой Azure.</span><span class="sxs-lookup"><span data-stu-id="73d66-106">The Azure CLI provides a set of open source, cross-platform commands for working with the Azure Platform.</span></span> <span data-ttu-id="73d66-107">Он предоставляет практически те же функции, что и [портал Azure](https://portal.azure.com) , а также различные возможности доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="73d66-107">It provides much of the same functionality found in the [Azure portal](https://portal.azure.com) as well as rich data access functionality.</span></span>

<span data-ttu-id="73d66-108">В этом руководстве вы узнаете, как использовать [интерфейс командной строки Azure (Azure CLI)](../cli-install-nodejs.md) для выполнения различных задач, связанных с разработкой и администрированием, в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="73d66-108">In this guide, we'll explore how to use [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md) to perform a variety of development and administration tasks with Azure Storage.</span></span> <span data-ttu-id="73d66-109">Рекомендуем загрузить и установить (или обновить до последней версии) интерфейс командной строки Azure перед использованием в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="73d66-109">We recommend that you download and install or upgrade to the latest Azure CLI before using this guide.</span></span>

<span data-ttu-id="73d66-110">В этом руководстве предполагается, что вам знакомы основные понятия службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="73d66-110">This guide assumes that you understand the basic concepts of Azure Storage.</span></span> <span data-ttu-id="73d66-111">Руководство предоставляет несколько сценариев для демонстрации использования интерфейса командной строки Azure со службой хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="73d66-111">The guide provides a number of scripts to demonstrate the usage of the Azure CLI with Azure Storage.</span></span> <span data-ttu-id="73d66-112">Перед выполнением каждого сценария необходимо обновить переменные сценария в зависимости от конфигурации.</span><span class="sxs-lookup"><span data-stu-id="73d66-112">Be sure to update the script variables based on your configuration before running each script.</span></span>

> [!NOTE]
> <span data-ttu-id="73d66-113">Руководство содержит команды Azure CLI и примеры сценариев для классических учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="73d66-113">The guide provides the Azure CLI command and script examples for classic storage accounts.</span></span> <span data-ttu-id="73d66-114">Перечень команд Azure CLI учетных записей хранения Resource Manager см. в разделе [Использование Azure CLI для Mac, Linux и Windows с диспетчером ресурсов Azure](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects).</span><span class="sxs-lookup"><span data-stu-id="73d66-114">See [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) for Azure CLI commands for Resource Manager storage accounts.</span></span>
>
>

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-the-azure-cli-in-5-minutes"></a><span data-ttu-id="73d66-115">Начало работы со службой хранилища Azure и интерфейсом командной строки Azure в течение 5 минут</span><span class="sxs-lookup"><span data-stu-id="73d66-115">Get started with Azure Storage and the Azure CLI in 5 minutes</span></span>
<span data-ttu-id="73d66-116">В этом руководстве для демонстрации примеров используется ОС Ubuntu, но другие платформы должны работать аналогично.</span><span class="sxs-lookup"><span data-stu-id="73d66-116">This guide uses Ubuntu for examples, but other OS platforms should perform similarly.</span></span>

<span data-ttu-id="73d66-117">**Впервые используете Azure?** Получите подписку на Microsoft Azure и связанную с ней учетную запись Microsoft.</span><span class="sxs-lookup"><span data-stu-id="73d66-117">**New to Azure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="73d66-118">Сведения о способах приобретения Azure см. на страницах [Создайте бесплатную учетную запись Azure уже сегодня](https://azure.microsoft.com/pricing/free-trial/), [Как приобрести Azure](https://azure.microsoft.com/pricing/purchase-options/) и [Предложения для участников](https://azure.microsoft.com/pricing/member-offers/) (для подписчиков MSDN, участников Microsoft Partner Network, BizSpark и других наших программ).</span><span class="sxs-lookup"><span data-stu-id="73d66-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="73d66-119">Дополнительные сведения о подписках Azure см. на странице [Назначение ролей администратора в Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx).</span><span class="sxs-lookup"><span data-stu-id="73d66-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="73d66-120">**После создания подписки Microsoft Azure и учетной записи:**</span><span class="sxs-lookup"><span data-stu-id="73d66-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="73d66-121">Загрузите и установите интерфейс командной строки Azure согласно инструкциям в статье [Установка интерфейса командной строки Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="73d66-121">Download and install the Azure CLI following the instructions outlined in [Install the Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="73d66-122">После установки интерфейса командной строки Azure для доступа к соответствующим функциям можно использовать команду azure в интерфейсе командной строки (Bash, терминал, командная строка).</span><span class="sxs-lookup"><span data-stu-id="73d66-122">Once the Azure CLI has been installed, you will be able to use the azure command from your command-line interface (Bash, Terminal, Command prompt) to access the Azure CLI commands.</span></span> <span data-ttu-id="73d66-123">Введите команду _azure_, после чего вы должны увидеть следующие выходные данные.</span><span class="sxs-lookup"><span data-stu-id="73d66-123">Type the _azure_ command and you should see the following output.</span></span>

    ![Вывод команды Azure][Image1]
3. <span data-ttu-id="73d66-125">В интерфейсе командной строки введите `azure storage`, чтобы вывести список всех команд службы хранилища Azure и ознакомиться с функциями, предоставляемыми интерфейсом командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="73d66-125">In the command-line interface, type `azure storage` to list out all the azure storage commands and get a first impression of the functionalities the Azure CLI provides.</span></span> <span data-ttu-id="73d66-126">Вы можете ввести название команды с параметром **-h** (например, `azure storage share create -h`), чтобы увидеть подробные сведения о синтаксисе команды.</span><span class="sxs-lookup"><span data-stu-id="73d66-126">You can type command name with **-h** parameter (for example, `azure storage share create -h`) to see details of command syntax.</span></span>
4. <span data-ttu-id="73d66-127">Теперь мы предоставим вам простой сценарий, который показывает основные команды интерфейса командной строки Azure для доступа к службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="73d66-127">Now, we'll give you a simple script that shows basic Azure CLI commands to access Azure Storage.</span></span> <span data-ttu-id="73d66-128">Сценарий сначала потребует установить две переменные для учетной записи хранения и ключа.</span><span class="sxs-lookup"><span data-stu-id="73d66-128">The script will first ask you to set two variables for your storage account and key.</span></span> <span data-ttu-id="73d66-129">Затем сценарий создает новый контейнер в этой новой учетной записи хранения и передает существующий файл образа (BLOB) в этот контейнер.</span><span class="sxs-lookup"><span data-stu-id="73d66-129">Then, the script will create a new container in this new storage account and upload an existing image file (blob) to that container.</span></span> <span data-ttu-id="73d66-130">После этого сценарий выводит список всех BLOB-объектов в этом контейнере и загружает файл образа в каталог назначения, существующий на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="73d66-130">After the script lists all blobs in that container, it will download the image file to the destination directory which exists on the local computer.</span></span>

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating the container..."
    azure storage container create $container_name

    echo "Uploading the image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing the blobs..."
    azure storage blob list $container_name

    echo "Downloading the image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. <span data-ttu-id="73d66-131">Откройте любой текстовый редактор на локальном компьютере (например, Vim)</span><span class="sxs-lookup"><span data-stu-id="73d66-131">In your local computer, open your preferred text editor (vim for example).</span></span> <span data-ttu-id="73d66-132">Введите указанный сценарий в текстовый редактор.</span><span class="sxs-lookup"><span data-stu-id="73d66-132">Type the above script into your text editor.</span></span>
6. <span data-ttu-id="73d66-133">Теперь необходимо обновить переменные сценария на основе заданных параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="73d66-133">Now, you need to update the script variables based on your configuration settings.</span></span>

   * <span data-ttu-id="73d66-134">**<имя_учетной_записи_хранения>**: используйте заданное в сценарии имя или введите новое имя для учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="73d66-134">**<storage_account_name>** Use the given name in the script or enter a new name for your storage account.</span></span> <span data-ttu-id="73d66-135">**Внимание!** Имя учетной записи хранения в Azure должно быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="73d66-135">**Important:** The name of the storage account must be unique in Azure.</span></span> <span data-ttu-id="73d66-136">и состоять из символов нижнего регистра.</span><span class="sxs-lookup"><span data-stu-id="73d66-136">It must be lowercase, too!</span></span>
   * <span data-ttu-id="73d66-137">**<ключ_учетной_записи_хранения>**: ключ доступа к вашей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="73d66-137">**<storage_account_key>** The access key of your storage account.</span></span>
   * <span data-ttu-id="73d66-138">**<имя_контейнера>**: используйте заданное в сценарии имя или введите новое имя для контейнера.</span><span class="sxs-lookup"><span data-stu-id="73d66-138">**<container_name>** Use the given name in the script or enter a new name for your container.</span></span>
   * <span data-ttu-id="73d66-139">**<передаваемое_изображение>**: введите путь к изображению на локальном компьютере (например, ~/images/HelloWorld.png).</span><span class="sxs-lookup"><span data-stu-id="73d66-139">**<image_to_upload>** Enter a path to a picture on your local computer, such as: "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="73d66-140">**<папка_назначения>**: введите путь к локальному каталогу для хранения файлов, скачанных из службы хранилища Azure (например, ~/downloadImages).</span><span class="sxs-lookup"><span data-stu-id="73d66-140">**<destination_folder>** Enter a path to a local directory to store files downloaded from Azure Storage, such as: "~/downloadImages".</span></span>
7. <span data-ttu-id="73d66-141">После обновления необходимых переменных в Vim нажмите комбинации клавиш `ESC`, `:`, `wq!`, чтобы сохранить сценарий.</span><span class="sxs-lookup"><span data-stu-id="73d66-141">After you've updated the necessary variables in vim, press key combinations `ESC`, `:`, `wq!` to save the script.</span></span>
8. <span data-ttu-id="73d66-142">Чтобы выполнить этот сценарий, введите имя файла сценария в консоль Bash.</span><span class="sxs-lookup"><span data-stu-id="73d66-142">To run this script, simply type the script file name in the bash console.</span></span> <span data-ttu-id="73d66-143">После выполнения сценария появится локальная целевая папка, которая содержит загруженный файл образа.</span><span class="sxs-lookup"><span data-stu-id="73d66-143">After this script runs, you should have a local destination folder that includes the downloaded image file.</span></span> <span data-ttu-id="73d66-144">На следующем снимке экрана показан пример вывода:</span><span class="sxs-lookup"><span data-stu-id="73d66-144">The following screenshot shows an example output:</span></span>

<span data-ttu-id="73d66-145">После выполнения сценария появится локальная целевая папка, которая содержит загруженный файл образа.</span><span class="sxs-lookup"><span data-stu-id="73d66-145">After the script runs, you should have a local destination folder that includes the downloaded image file.</span></span>

## <a name="manage-storage-accounts-with-the-azure-cli"></a><span data-ttu-id="73d66-146">Управление учетными записями хранения с помощью интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="73d66-146">Manage storage accounts with the Azure CLI</span></span>
### <a name="connect-to-your-azure-subscription"></a><span data-ttu-id="73d66-147">Подключение к подписке Azure</span><span class="sxs-lookup"><span data-stu-id="73d66-147">Connect to your Azure subscription</span></span>
<span data-ttu-id="73d66-148">Хотя большинство команд хранилища могут работать без подписки Azure, рекомендуем вам подключить свою подписку через интерфейс командной строки Azure (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="73d66-148">While most of the storage commands will work without an Azure subscription, we recommend you to connect to your subscription from the Azure CLI.</span></span> <span data-ttu-id="73d66-149">Чтобы настроить Azure CLI для работы с подпиской, следуйте инструкциям в статье [Подключение к среде Azure с использованием интерфейса командной строки Azure (Azure CLI)](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="73d66-149">To configure the Azure CLI to work with your subscription, follow the steps in [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="73d66-150">Создание новой учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="73d66-150">Create a new storage account</span></span>
<span data-ttu-id="73d66-151">Для использования службы хранилища Azure потребуется учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="73d66-151">To use Azure storage, you will need a storage account.</span></span> <span data-ttu-id="73d66-152">После настройки компьютера для подключения к подписке можно создать новую учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="73d66-152">You can create a new Azure storage account after you have configured your computer to connect to your subscription.</span></span>

```azurecli
azure storage account create <account_name>
```

<span data-ttu-id="73d66-153">Имя учетной записи хранения должно содержать от 3 до 24 символов и состоять только из цифр и букв нижнего регистра.</span><span class="sxs-lookup"><span data-stu-id="73d66-153">The name of your storage account must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a><span data-ttu-id="73d66-154">Установите учетную запись хранения Azure по умолчанию в переменных среды</span><span class="sxs-lookup"><span data-stu-id="73d66-154">Set a default Azure storage account in environment variables</span></span>
<span data-ttu-id="73d66-155">В подписке может иметься несколько учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="73d66-155">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="73d66-156">Вы можете выбрать одну из них и установить ее в переменных среды для всех команд хранилища в одном сеансе.</span><span class="sxs-lookup"><span data-stu-id="73d66-156">You can choose one of them and set it in the environment variables for all the storage commands in the same session.</span></span> <span data-ttu-id="73d66-157">Это позволяет выполнять команды хранилища интерфейса командной строки Azure без явного указания учетной записи и ключа хранения.</span><span class="sxs-lookup"><span data-stu-id="73d66-157">This enables you to run the Azure CLI storage commands without specifying the storage account and key explicitly.</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="73d66-158">Установить учетную запись хранения по умолчанию можно также с помощью строки подключения.</span><span class="sxs-lookup"><span data-stu-id="73d66-158">Another way to set a default storage account is using connection string.</span></span> <span data-ttu-id="73d66-159">Во-первых, получите строку подключения при помощи следующей команды:</span><span class="sxs-lookup"><span data-stu-id="73d66-159">Firstly get the connection string by command:</span></span>

```azurecli
azure storage account connectionstring show <account_name>
```

<span data-ttu-id="73d66-160">Затем скопируйте полученную строку подключения и установите ее на переменную среды:</span><span class="sxs-lookup"><span data-stu-id="73d66-160">Then copy the output connection string and set it to environment variable:</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a><span data-ttu-id="73d66-161">Создание больших двоичных объектов (BLOB-объектов) и управление ими</span><span class="sxs-lookup"><span data-stu-id="73d66-161">Create and manage blobs</span></span>
<span data-ttu-id="73d66-162">Хранилище BLOB-объектов Azure — это служба хранения большого количества неструктурированных данных, таких как текстовые или бинарные файлы, к которым можно получить доступ практически из любой точки мира по протоколу HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="73d66-162">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="73d66-163">В этом разделе предполагается, что вы уже знакомы с понятиями службы хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="73d66-163">This section assumes that you are already familiar with the Azure Blob storage concepts.</span></span> <span data-ttu-id="73d66-164">Дополнительные сведения см. в статьях [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](storage-dotnet-how-to-use-blobs.md) и [Основные понятия службы BLOB-объектов](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="73d66-164">For detailed information, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="73d66-165">Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="73d66-165">Create a container</span></span>
<span data-ttu-id="73d66-166">Каждый BLOB-объект в хранилище Azure должен находиться в контейнере.</span><span class="sxs-lookup"><span data-stu-id="73d66-166">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="73d66-167">Вы можете создать закрытый контейнер с помощью команды `azure storage container create` :</span><span class="sxs-lookup"><span data-stu-id="73d66-167">You can create a private container using the `azure storage container create` command:</span></span>

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> <span data-ttu-id="73d66-168">Существует три уровня анонимного доступа для чтения: **Отключено**, **Большой двоичный объект** и **Контейнер**.</span><span class="sxs-lookup"><span data-stu-id="73d66-168">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="73d66-169">Чтобы запретить анонимный доступ к большому двоичному объекту, присвойте параметру разрешение **Отключено**.</span><span class="sxs-lookup"><span data-stu-id="73d66-169">To prevent anonymous access to blobs, set the Permission parameter to **Off**.</span></span> <span data-ttu-id="73d66-170">По умолчанию новый контейнер является закрытым, доступ к нему может осуществляться только владельцем учетной записи.</span><span class="sxs-lookup"><span data-stu-id="73d66-170">By default, the new container is private and can be accessed only by the account owner.</span></span> <span data-ttu-id="73d66-171">Чтобы разрешить анонимный общий доступ на чтение к ресурсам больших двоичных объектов, но не к метаданным контейнера или списку больших двоичных объектов в контейнере, присвойте параметру разрешение **Большой двоичный объект**.</span><span class="sxs-lookup"><span data-stu-id="73d66-171">To allow anonymous public read access to blob resources, but not to container metadata or to the list of blobs in the container, set the Permission parameter to **Blob**.</span></span> <span data-ttu-id="73d66-172">Чтобы разрешить полный общий доступ на чтение к ресурсам больших двоичных объектов, метаданным контейнера и списку больших двоичных объектов в контейнере, присвойте параметру разрешение **Контейнер**.</span><span class="sxs-lookup"><span data-stu-id="73d66-172">To allow full public read access to blob resources, container metadata, and the list of blobs in the container, set the Permission parameter to **Container**.</span></span> <span data-ttu-id="73d66-173">Дополнительные сведения см. в статье [Управление анонимным доступом на чтение к контейнерам и большим двоичным объектам](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="73d66-173">For more information, see [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>
>
>

### <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="73d66-174">Отправка BLOB-объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="73d66-174">Upload a blob into a container</span></span>
<span data-ttu-id="73d66-175">Хранилище BLOB-объектов Azure поддерживает блочные и страничные BLOB-объекты.</span><span class="sxs-lookup"><span data-stu-id="73d66-175">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="73d66-176">Дополнительные сведения см. в статье [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx) (Основные сведения о блочных, добавочных и страничных BLOB-объектах).</span><span class="sxs-lookup"><span data-stu-id="73d66-176">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="73d66-177">Чтобы загрузить BLOB-объекты в контейнер, вы можете использовать `azure storage blob upload`.</span><span class="sxs-lookup"><span data-stu-id="73d66-177">To upload blobs in to a container, you can use the `azure storage blob upload`.</span></span> <span data-ttu-id="73d66-178">По умолчанию эта команда отправляет локальные файлы в BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="73d66-178">By default, this command uploads the local files to a block blob.</span></span> <span data-ttu-id="73d66-179">Чтобы указать тип BLOB-объекта можно использовать параметр `--blobtype` .</span><span class="sxs-lookup"><span data-stu-id="73d66-179">To specify the type for the blob, you can use the `--blobtype` parameter.</span></span>

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a><span data-ttu-id="73d66-180">Загрузка BLOB-объектов из контейнера</span><span class="sxs-lookup"><span data-stu-id="73d66-180">Download blobs from a container</span></span>
<span data-ttu-id="73d66-181">Следующий пример демонстрирует загрузку BLOB-объектов из контейнера.</span><span class="sxs-lookup"><span data-stu-id="73d66-181">The following example demonstrates how to download blobs from a container.</span></span>

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a><span data-ttu-id="73d66-182">Копирование BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="73d66-182">Copy blobs</span></span>
<span data-ttu-id="73d66-183">Можно асинхронно копировать BLOB-объекты между учетными записями хранения и областями или внутри них.</span><span class="sxs-lookup"><span data-stu-id="73d66-183">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="73d66-184">Следующий пример демонстрирует копирование BLOB-объектов из одной учетной записи хранения в другую.</span><span class="sxs-lookup"><span data-stu-id="73d66-184">The following example demonstrates how to copy blobs from one storage account to another.</span></span> <span data-ttu-id="73d66-185">В этом примере мы создаем контейнер с общим анонимным доступом к BLOB-объектам.</span><span class="sxs-lookup"><span data-stu-id="73d66-185">In this sample we create a container where blobs are publicly, anonymously accessible.</span></span>

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

<span data-ttu-id="73d66-186">В этом примере выполняется асинхронное копирование.</span><span class="sxs-lookup"><span data-stu-id="73d66-186">This sample performs an asynchronous copy.</span></span> <span data-ttu-id="73d66-187">Вы можете следить за состоянием операции копирования, выполнив операцию `azure storage blob copy show`.</span><span class="sxs-lookup"><span data-stu-id="73d66-187">You can monitor the status of each copy operation by running the `azure storage blob copy show` operation.</span></span>

<span data-ttu-id="73d66-188">Обратите внимание, что URL-адрес источника, предоставленный для операции копирования, должен либо быть общедоступным, либо содержать маркер SAS (подписанный URL-адрес). </span><span class="sxs-lookup"><span data-stu-id="73d66-188">Note that the source URL provided for the copy operation must either be publicly accessible, or include a SAS (shared access signature) token.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="73d66-189">Удаление большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="73d66-189">Delete a blob</span></span>
<span data-ttu-id="73d66-190">Чтобы удалить BLOB-объект, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="73d66-190">To delete a blob, use the below command:</span></span>

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="73d66-191">Создание общих папок и управление ими</span><span class="sxs-lookup"><span data-stu-id="73d66-191">Create and manage file shares</span></span>
<span data-ttu-id="73d66-192">Хранилище файлов Azure предоставляет общее хранилище для приложений с помощью стандартного протокола SMB.</span><span class="sxs-lookup"><span data-stu-id="73d66-192">Azure File storage offers shared storage for applications using the standard SMB protocol.</span></span> <span data-ttu-id="73d66-193">Виртуальные машины Microsoft Azure и облачные службы, а также локальные приложения, могут совместно использовать данные через монтированные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="73d66-193">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="73d66-194">Вы можете управлять общими папками и файловыми данными через интерфейс командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="73d66-194">You can manage file shares and file data via the Azure CLI.</span></span> <span data-ttu-id="73d66-195">Дополнительные сведения о хранилище файлов Azure см. в статье [Приступая к работе с хранилищем файлов Azure в Windows](storage-dotnet-how-to-use-files.md) или [Использование хранилища файлов Azure с Linux](storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="73d66-195">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) or [How to use Azure File storage with Linux](storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="73d66-196">Создайте общую папку</span><span class="sxs-lookup"><span data-stu-id="73d66-196">Create a file share</span></span>
<span data-ttu-id="73d66-197">Общая папка Azure представляет собой общую папку с файлами SMB в Azure.</span><span class="sxs-lookup"><span data-stu-id="73d66-197">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="73d66-198">Все каталоги и файлы должны быть созданы в общей папке.</span><span class="sxs-lookup"><span data-stu-id="73d66-198">All directories and files must be created in a file share.</span></span> <span data-ttu-id="73d66-199">Учетная запись может содержать любое количество совместно используемых ресурсов, а ресурс может содержать любое количество файлов, насколько это позволяет емкость учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="73d66-199">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up to the capacity limits of the storage account.</span></span> <span data-ttu-id="73d66-200">В следующем примере создается общая папка с именем **myshare**.</span><span class="sxs-lookup"><span data-stu-id="73d66-200">The following example creates a file share named **myshare**.</span></span>

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="73d66-201">Создайте каталог</span><span class="sxs-lookup"><span data-stu-id="73d66-201">Create a directory</span></span>
<span data-ttu-id="73d66-202">Каталог обеспечивает дополнительную иерархическую структуру для общей папки Azure.</span><span class="sxs-lookup"><span data-stu-id="73d66-202">A directory provides an optional hierarchical structure for an Azure file share.</span></span> <span data-ttu-id="73d66-203">В следующем примере в общей папке создается каталог с именем **myDir** .</span><span class="sxs-lookup"><span data-stu-id="73d66-203">The following example creates a directory named **myDir** in the file share.</span></span>

```azurecli
azure storage directory create myshare myDir
```

<span data-ttu-id="73d66-204">Обратите внимание, что путь к каталогу может включать несколько уровней, *например***a/b**.</span><span class="sxs-lookup"><span data-stu-id="73d66-204">Note that directory path can include multiple levels, *e.g.*, **a/b**.</span></span> <span data-ttu-id="73d66-205">Однако необходимо убедиться в наличии всех родительских каталогов.</span><span class="sxs-lookup"><span data-stu-id="73d66-205">However, you must ensure that all parent directories exist.</span></span> <span data-ttu-id="73d66-206">Например, для пути **a/b** вам потребуется сначала создать каталог **a**, а затем — каталог **b**.</span><span class="sxs-lookup"><span data-stu-id="73d66-206">For example, for path **a/b**, you must create directory **a** first, then create directory **b**.</span></span>

### <a name="upload-a-local-file-to-directory"></a><span data-ttu-id="73d66-207">Отправка локального файла в каталог</span><span class="sxs-lookup"><span data-stu-id="73d66-207">Upload a local file to directory</span></span>
<span data-ttu-id="73d66-208">В следующем примере выполняется передача файла из **~/temp/samplefile.txt** в каталог **myDir**.</span><span class="sxs-lookup"><span data-stu-id="73d66-208">The following example uploads a file from **~/temp/samplefile.txt** to the **myDir** directory.</span></span> <span data-ttu-id="73d66-209">Отредактируйте путь к файлу, чтобы он соответствовал пути к существующему файлу на локальном компьютере:</span><span class="sxs-lookup"><span data-stu-id="73d66-209">Edit the file path so that it points to a valid file on your local machine:</span></span>

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

<span data-ttu-id="73d66-210">Обратите внимание, что размер файла в общей папке может составлять до 1 ТБ.</span><span class="sxs-lookup"><span data-stu-id="73d66-210">Note that a file in the share can be up to 1 TB in size.</span></span>

### <a name="list-the-files-in-the-share-root-or-directory"></a><span data-ttu-id="73d66-211">Укажите список файлов в корне или каталоге общей папки</span><span class="sxs-lookup"><span data-stu-id="73d66-211">List the files in the share root or directory</span></span>
<span data-ttu-id="73d66-212">Вы можете указать список файлов и подкаталогов в корне или каталоге общей папки с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="73d66-212">You can list the files and subdirectories in a share root or a directory using the following command:</span></span>

```azurecli
azure storage file list myshare myDir
```

<span data-ttu-id="73d66-213">Обратите внимание, что имя каталога необязательно для операции перечисления.</span><span class="sxs-lookup"><span data-stu-id="73d66-213">Note that the directory name is optional for the listing operation.</span></span> <span data-ttu-id="73d66-214">Если имя каталога не указано, команда перечислит содержимое корневого каталога общей папки.</span><span class="sxs-lookup"><span data-stu-id="73d66-214">If omitted, the command lists the contents of the root directory of the share.</span></span>

### <a name="copy-files"></a><span data-ttu-id="73d66-215">Копирование файлов</span><span class="sxs-lookup"><span data-stu-id="73d66-215">Copy files</span></span>
<span data-ttu-id="73d66-216">Начиная с версии 0.9.8 интерфейса Azure CLI, можно скопировать файл в другой файл, файл в большой двоичный объект или BLOB-объект в файл.</span><span class="sxs-lookup"><span data-stu-id="73d66-216">Beginning with version 0.9.8 of Azure CLI, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="73d66-217">Ниже демонстрируется выполнение этих операций копирования с помощью команд CLI.</span><span class="sxs-lookup"><span data-stu-id="73d66-217">Below we demonstrate how to perform these copy operations using CLI commands.</span></span> <span data-ttu-id="73d66-218">Копирование файла в новый каталог:</span><span class="sxs-lookup"><span data-stu-id="73d66-218">To copy a file to the new directory:</span></span>

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

<span data-ttu-id="73d66-219">Копирование большого двоичного объекта в каталог файлов:</span><span class="sxs-lookup"><span data-stu-id="73d66-219">To copy a blob to a file directory:</span></span>

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a><span data-ttu-id="73d66-220">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="73d66-220">Next Steps</span></span>

<span data-ttu-id="73d66-221">Справочник по командам Azure CLI 1.0 для работы с ресурсами службы хранилища можно найти здесь:</span><span class="sxs-lookup"><span data-stu-id="73d66-221">You can find Azure CLI 1.0 command reference for working with Storage resources here:</span></span>

* [<span data-ttu-id="73d66-222">Команды Azure CLI в режиме Resource Manager</span><span class="sxs-lookup"><span data-stu-id="73d66-222">Azure CLI commands in Resource Manager mode</span></span>](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [<span data-ttu-id="73d66-223">Установка Azure CLI</span><span class="sxs-lookup"><span data-stu-id="73d66-223">Azure CLI commands in Azure Service Management mode</span></span>](../cli-install-nodejs.md)

<span data-ttu-id="73d66-224">Кроме того, вы можете применить [Azure CLI 2.0](storage-azure-cli.md). Это интерфейс командной строки нового поколения, написанный на языке Python, для модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="73d66-224">You may also like to try the [Azure CLI 2.0](storage-azure-cli.md), our next-generation CLI written in Python, for use with the Resource Manager deployment model.</span></span>

[Image1]: ./media/storage-azure-cli/azure_command.png
