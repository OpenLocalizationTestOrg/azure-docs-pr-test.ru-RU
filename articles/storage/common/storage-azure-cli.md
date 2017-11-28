---
title: "aaaUsing hello Azure CLI 2.0 со службой хранилища Azure | Документы Microsoft"
description: "Узнайте, как toouse hello Azure командной строки (CLI Azure) 2.0 с toocreate хранилища Azure и управление учетными записями хранения и работы с файлами и больших двоичных объектов Azure. Hello Azure CLI 2.0 — это средство кросс платформенных, написанных на Python."
services: storage
documentationcenter: na
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 06/02/2017
ms.author: marsma
ms.openlocfilehash: 14e6eb0c913676380c90a72563276245e7f08aa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-20-with-azure-storage"></a><span data-ttu-id="94a29-104">С помощью hello Azure CLI 2.0 со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="94a29-104">Using hello Azure CLI 2.0 with Azure Storage</span></span>

<span data-ttu-id="94a29-105">Hello открытый исходный код, кросс платформенных Azure CLI 2.0 предоставляет набор команд для работы с hello платформы Azure.</span><span class="sxs-lookup"><span data-stu-id="94a29-105">hello open-source, cross-platform Azure CLI 2.0 provides a set of commands for working with hello Azure platform.</span></span> <span data-ttu-id="94a29-106">Она предоставляет большую часть hello же функциональные возможности, найденные в hello [портал Azure](https://portal.azure.com), включая доступ сложных данных.</span><span class="sxs-lookup"><span data-stu-id="94a29-106">It provides much of hello same functionality found in hello [Azure portal](https://portal.azure.com), including rich data access.</span></span>

<span data-ttu-id="94a29-107">В этом руководстве вы узнаете toouse hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform несколько задач, работы с ресурсами в вашей учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="94a29-107">In this guide, we show you how toouse hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform several tasks working with resources in your Azure Storage account.</span></span> <span data-ttu-id="94a29-108">Рекомендуется загрузить и установить или обновление toohello последнюю версию CLI 2.0 hello ранее с помощью этого руководства.</span><span class="sxs-lookup"><span data-stu-id="94a29-108">We recommend that you download and install or upgrade toohello latest version of hello CLI 2.0 before using this guide.</span></span>

<span data-ttu-id="94a29-109">Примеры Hello в руководстве hello предполагается использование hello hello оболочке Bash на Ubuntu, но другие платформы должен выполнять аналогичным образом.</span><span class="sxs-lookup"><span data-stu-id="94a29-109">hello examples in hello guide assume hello use of hello Bash shell on Ubuntu, but other platforms should perform similarly.</span></span> 

[!INCLUDE [storage-cli-versions](../../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a><span data-ttu-id="94a29-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="94a29-110">Prerequisites</span></span>
<span data-ttu-id="94a29-111">В этом руководстве предполагается, что вы понимаете основные понятия hello хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="94a29-111">This guide assumes that you understand hello basic concepts of Azure Storage.</span></span> <span data-ttu-id="94a29-112">Также предполагается, что вы будете требования к создания может toosatisfy hello учетной записи, указанные ниже для Azure и hello службы хранилища.</span><span class="sxs-lookup"><span data-stu-id="94a29-112">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Storage service.</span></span>

### <a name="accounts"></a><span data-ttu-id="94a29-113">Учетные записи</span><span class="sxs-lookup"><span data-stu-id="94a29-113">Accounts</span></span>
* <span data-ttu-id="94a29-114">**Учетная запись Azure.** Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="94a29-114">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="94a29-115">**Учетная запись хранения**. См. раздел [Создание учетной записи хранения](storage-create-storage-account.md#create-a-storage-account) в статье [Об учетных записях хранения Azure](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="94a29-115">**Storage account**: See [Create a storage account](storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](storage-create-storage-account.md).</span></span>

### <a name="install-hello-azure-cli-20"></a><span data-ttu-id="94a29-116">Установка hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="94a29-116">Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="94a29-117">Загрузите и установите hello Azure CLI 2.0, следуя указаниям hello в [установить CLI Azure 2.0](/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="94a29-117">Download and install hello Azure CLI 2.0 by following hello instructions outlined in [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

> [!TIP]
> <span data-ttu-id="94a29-118">Если возникли проблемы с установкой hello, извлечь hello [Устранение неполадок установки](/cli/azure/install-az-cli2#installation-troubleshooting) раздел статьи hello и hello [Устранение неполадок установки](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) руководство по на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="94a29-118">If you have trouble with hello installation, check out hello [Installation Troubleshooting](/cli/azure/install-az-cli2#installation-troubleshooting) section of hello article, and hello [Install Troubleshooting](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guide on GitHub.</span></span>
>

## <a name="working-with-hello-cli"></a><span data-ttu-id="94a29-119">Работа с hello CLI</span><span class="sxs-lookup"><span data-stu-id="94a29-119">Working with hello CLI</span></span>

<span data-ttu-id="94a29-120">После установки hello CLI можно использовать hello `az` в командах Azure CLI hello tooaccess интерфейс командной строки (Bash, терминалов, командной строки).</span><span class="sxs-lookup"><span data-stu-id="94a29-120">Once you've installed hello CLI, you can use hello `az` command in your command-line interface (Bash, Terminal, Command Prompt) tooaccess hello Azure CLI commands.</span></span> <span data-ttu-id="94a29-121">Тип hello `az` toosee команда полный список базовых команд hello (был усечен hello следующий пример выходных данных):</span><span class="sxs-lookup"><span data-stu-id="94a29-121">Type hello `az` command toosee a full list of hello base commands (hello following example output has been truncated):</span></span>

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome toohello cool new Azure CLI!

Here are hello base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

<span data-ttu-id="94a29-122">В интерфейсе командной строки, выполните команду hello `az storage --help` toolist hello `storage` команды подгруппы.</span><span class="sxs-lookup"><span data-stu-id="94a29-122">In your command-line interface, execute hello command `az storage --help` toolist hello `storage` command subgroups.</span></span> <span data-ttu-id="94a29-123">описания Hello подгрупп hello содержит краткую приветствия функции hello Azure CLI предоставляет для работы с ресурсами хранилища.</span><span class="sxs-lookup"><span data-stu-id="94a29-123">hello descriptions of hello subgroups provide an overview of hello functionality hello Azure CLI provides for working with your storage resources.</span></span>

```
Group
    az storage: Durable, highly available, and massively scalable cloud storage.

Subgroups:
    account  : Manage storage accounts.
    blob     : Object storage for unstructured data.
    container: Manage blob storage containers.
    cors     : Manage Storage service Cross-Origin Resource Sharing (CORS).
    directory: Manage file storage directories.
    entity   : Manage table storage entities.
    file     : File shares that use hello standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues tooeffectively scale applications according tootraffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-hello-cli-tooyour-azure-subscription"></a><span data-ttu-id="94a29-124">Подключение tooyour CLI hello подписки Azure</span><span class="sxs-lookup"><span data-stu-id="94a29-124">Connect hello CLI tooyour Azure subscription</span></span>

<span data-ttu-id="94a29-125">toowork с ресурсами hello в вашей подписке Azure необходимо сначала войти в tooyour учетная запись Azure с `az login`.</span><span class="sxs-lookup"><span data-stu-id="94a29-125">toowork with hello resources in your Azure subscription, you must first log in tooyour Azure account with `az login`.</span></span> <span data-ttu-id="94a29-126">Для этого существует несколько способов.</span><span class="sxs-lookup"><span data-stu-id="94a29-126">There are several ways you can log in:</span></span>

* <span data-ttu-id="94a29-127">**Интерактивный вход**: `az login`.</span><span class="sxs-lookup"><span data-stu-id="94a29-127">**Interactive login**: `az login`</span></span>
* <span data-ttu-id="94a29-128">**Вход с использованием имени пользователя SSH и пароля**: `az login -u johndoe@contoso.com -p VerySecret`.</span><span class="sxs-lookup"><span data-stu-id="94a29-128">**Log in with user name and password**: `az login -u johndoe@contoso.com -p VerySecret`</span></span>
  * <span data-ttu-id="94a29-129">Этот способ не работает с учетными записями Майкрософт или с учетными записями, которые используют многофакторную идентификацию.</span><span class="sxs-lookup"><span data-stu-id="94a29-129">This doesn't work with Microsoft accounts or accounts that use multi-factor authentication.</span></span>
* <span data-ttu-id="94a29-130">**Вход с использованием субъекта-службы**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="94a29-130">**Log in with a service principal**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span></span>

## <a name="azure-cli-20-sample-script"></a><span data-ttu-id="94a29-131">Пример скрипта Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="94a29-131">Azure CLI 2.0 sample script</span></span>

<span data-ttu-id="94a29-132">Далее мы будем работать с небольшой сценарий, который выдает несколько основных toointeract команды Azure CLI 2.0 с ресурсов хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="94a29-132">Next, we'll work with a small shell script that issues a few basic Azure CLI 2.0 commands toointeract with Azure Storage resources.</span></span> <span data-ttu-id="94a29-133">Hello скрипт сначала создает новый контейнер в учетной записи, а затем передает существующий контейнер toothat файла (в виде больших двоичных объектов).</span><span class="sxs-lookup"><span data-stu-id="94a29-133">hello script first creates a new container in your storage account, then uploads an existing file (as a blob) toothat container.</span></span> <span data-ttu-id="94a29-134">Затем перечисляет все большие двоичные объекты в контейнере hello и наконец, загружает hello назначения tooa файл на локальном компьютере, который можно указать.</span><span class="sxs-lookup"><span data-stu-id="94a29-134">It then lists all blobs in hello container, and finally, downloads hello file tooa destination on your local computer that you specify.</span></span>

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating hello container..."
az storage container create --name $container_name

echo "Uploading hello file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing hello blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading hello file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

<span data-ttu-id="94a29-135">**Настройка и выполнение скрипта hello**</span><span class="sxs-lookup"><span data-stu-id="94a29-135">**Configure and run hello script**</span></span>

1. <span data-ttu-id="94a29-136">Откройте текстовый редактор, затем скопируйте и вставьте hello предшествующий скрипт в редактор hello.</span><span class="sxs-lookup"><span data-stu-id="94a29-136">Open your favorite text editor, then copy and paste hello preceding script into hello editor.</span></span>

2. <span data-ttu-id="94a29-137">Затем обновите tooreflect переменные сценария hello параметры конфигурации.</span><span class="sxs-lookup"><span data-stu-id="94a29-137">Next, update hello script's variables tooreflect your configuration settings.</span></span> <span data-ttu-id="94a29-138">Замените следующие значения, заданные hello:</span><span class="sxs-lookup"><span data-stu-id="94a29-138">Replace hello following values as specified:</span></span>

   * <span data-ttu-id="94a29-139">**\<storage_account_name\>**  hello имя вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="94a29-139">**\<storage_account_name\>** hello name of your storage account.</span></span>
   * <span data-ttu-id="94a29-140">**\<storage_account_key\>**  hello первичный или вторичный ключ доступа для учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="94a29-140">**\<storage_account_key\>** hello primary or secondary access key for your storage account.</span></span>
   * <span data-ttu-id="94a29-141">**\<container_name\>**  имя hello новый контейнер toocreate, такие как «azure-cli пример container».</span><span class="sxs-lookup"><span data-stu-id="94a29-141">**\<container_name\>** A name hello new container toocreate, such as "azure-cli-sample-container".</span></span>
   * <span data-ttu-id="94a29-142">**\<blob_name\>**  имя BLOB-объект назначения hello в контейнере hello.</span><span class="sxs-lookup"><span data-stu-id="94a29-142">**\<blob_name\>** A name for hello destination blob in hello container.</span></span>
   * <span data-ttu-id="94a29-143">**\<file_to_upload\>**  hello путь к файлу toosmall на локальном компьютере, такие как «~ / images/HelloWorld.png».</span><span class="sxs-lookup"><span data-stu-id="94a29-143">**\<file_to_upload\>** hello path toosmall file on your local computer, such as "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="94a29-144">**\<destination_file\>**  hello путь к файлу назначения, такие как «~ / downloadedImage.png».</span><span class="sxs-lookup"><span data-stu-id="94a29-144">**\<destination_file\>** hello destination file path, such as "~/downloadedImage.png".</span></span>

3. <span data-ttu-id="94a29-145">После обновления hello необходимые переменные, сохранить сценарий hello и выйти из редактора.</span><span class="sxs-lookup"><span data-stu-id="94a29-145">After you've updated hello necessary variables, save hello script and exit your editor.</span></span> <span data-ttu-id="94a29-146">Hello Далее предполагается, что с названием сценарий **my_storage_sample.sh**.</span><span class="sxs-lookup"><span data-stu-id="94a29-146">hello next steps assume you've named your script **my_storage_sample.sh**.</span></span>

4. <span data-ttu-id="94a29-147">Пометка hello скрипта как исполняемый файл и при необходимости:`chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="94a29-147">Mark hello script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>

5. <span data-ttu-id="94a29-148">Выполнение скрипта hello.</span><span class="sxs-lookup"><span data-stu-id="94a29-148">Execute hello script.</span></span> <span data-ttu-id="94a29-149">например в Bash: `./my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="94a29-149">For example, in Bash: `./my_storage_sample.sh`</span></span>

<span data-ttu-id="94a29-150">Вы должны видеть аналогичные toohello следующие выходные данные и hello  **\<destination_file\>**  указан в hello скрипт должен отобразиться на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="94a29-150">You should see output similar toohello following, and hello **\<destination_file\>** you specified in hello script should appear on your local computer.</span></span>

```
Creating hello container...
{
  "created": true
}
Uploading hello file...
Percent complete: %100.0
Listing hello blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading hello file...
Name
---------
README.md
Done
```

> [!TIP]
> <span data-ttu-id="94a29-151">Hello выше выходные данные выглядят в **таблицы** формат.</span><span class="sxs-lookup"><span data-stu-id="94a29-151">hello preceding output is in **table** format.</span></span> <span data-ttu-id="94a29-152">Можно указать, какой выход toouse формат, указав hello `--output` аргумент командах CLI или задать глобально с помощью `az configure`.</span><span class="sxs-lookup"><span data-stu-id="94a29-152">You can specify which output format toouse by specifying hello `--output` argument in your CLI commands, or set it globally using `az configure`.</span></span>
>

## <a name="manage-storage-accounts"></a><span data-ttu-id="94a29-153">Управление учетными записями хранения</span><span class="sxs-lookup"><span data-stu-id="94a29-153">Manage storage accounts</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="94a29-154">Создать новую учетную запись хранения</span><span class="sxs-lookup"><span data-stu-id="94a29-154">Create a new storage account</span></span>
<span data-ttu-id="94a29-155">toouse хранилища Azure, необходима учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="94a29-155">toouse Azure Storage, you need a storage account.</span></span> <span data-ttu-id="94a29-156">Можно создать новую учетную запись хранилища Azure, после настройки компьютера слишком[подключения подписки tooyour](#connect-to-your-azure-subscription).</span><span class="sxs-lookup"><span data-stu-id="94a29-156">You can create a new Azure Storage account after you've configured your computer too[connect tooyour subscription](#connect-to-your-azure-subscription).</span></span>

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* <span data-ttu-id="94a29-157">`--location` — расположение (обязательный параметр).</span><span class="sxs-lookup"><span data-stu-id="94a29-157">`--location` [Required]: Location.</span></span> <span data-ttu-id="94a29-158">Например, "западная часть США".</span><span class="sxs-lookup"><span data-stu-id="94a29-158">For example, "West US".</span></span>
* <span data-ttu-id="94a29-159">`--name`[Обязательно]: имя учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="94a29-159">`--name` [Required]: hello storage account name.</span></span> <span data-ttu-id="94a29-160">Hello имя должно состоять из 3 символов too24 и использовать только строчные буквы или цифры.</span><span class="sxs-lookup"><span data-stu-id="94a29-160">hello name must be 3 too24 characters in length, and use only lowercase alphanumeric characters.</span></span>
* <span data-ttu-id="94a29-161">`--resource-group` — имя группы ресурсов (обязательный параметр).</span><span class="sxs-lookup"><span data-stu-id="94a29-161">`--resource-group` [Required]: Name of resource group.</span></span>
* <span data-ttu-id="94a29-162">`--sku`[Обязательно]: hello учетной записи хранилища Конфигураций.</span><span class="sxs-lookup"><span data-stu-id="94a29-162">`--sku` [Required]: hello storage account SKU.</span></span> <span data-ttu-id="94a29-163">Допустимые значения:</span><span class="sxs-lookup"><span data-stu-id="94a29-163">Allowed values:</span></span>
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a><span data-ttu-id="94a29-164">Установка учетной записи хранения Azure по умолчанию в переменные среды</span><span class="sxs-lookup"><span data-stu-id="94a29-164">Set default Azure storage account environment variables</span></span>
<span data-ttu-id="94a29-165">В подписке может быть несколько учетных записей хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="94a29-165">You can have multiple storage accounts in your Azure subscription.</span></span> <span data-ttu-id="94a29-166">один из них tooselect toouse для хранения всех последующих команд, можно задать эти переменные среды:</span><span class="sxs-lookup"><span data-stu-id="94a29-166">tooselect one of them toouse for all subsequent storage commands, you can set these environment variables:</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="94a29-167">Другой способ tooset учетной записи хранения по умолчанию — с помощью строки подключения.</span><span class="sxs-lookup"><span data-stu-id="94a29-167">Another way tooset a default storage account is by using a connection string.</span></span> <span data-ttu-id="94a29-168">Сначала необходимо получить строку подключения hello с hello `show-connection-string` команды:</span><span class="sxs-lookup"><span data-stu-id="94a29-168">First, get hello connection string with hello `show-connection-string` command:</span></span>

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

<span data-ttu-id="94a29-169">Затем hello копирования выходных данных строки подключения и установите hello `AZURE_STORAGE_CONNECTION_STRING` переменной среды (возможно, придется строка подключения tooenclose hello в кавычки):</span><span class="sxs-lookup"><span data-stu-id="94a29-169">Then copy hello output connection string and set hello `AZURE_STORAGE_CONNECTION_STRING` environment variable (you might need tooenclose hello connection string in quotes):</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> <span data-ttu-id="94a29-170">Все примеры в следующих разделах этой статьи hello предполагается, что вы задали hello `AZURE_STORAGE_ACCOUNT` и `AZURE_STORAGE_ACCESS_KEY` переменные среды.</span><span class="sxs-lookup"><span data-stu-id="94a29-170">All examples in hello following sections of this article assume that you've set hello `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY` environment variables.</span></span>
>

## <a name="create-and-manage-blobs"></a><span data-ttu-id="94a29-171">Создание больших двоичных объектов (BLOB-объектов) и управление ими</span><span class="sxs-lookup"><span data-stu-id="94a29-171">Create and manage blobs</span></span>
<span data-ttu-id="94a29-172">Хранилище Azure BLOB-объекта — это служба для хранения больших объемов неструктурированных данных, например текстовых или двоичных данных, который может осуществляться из любого места в Здравствуй, мир! через HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="94a29-172">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="94a29-173">В этом разделе предполагается, что вы уже знакомы с понятиями службы хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="94a29-173">This section assumes that you are already familiar with Azure Blob storage concepts.</span></span> <span data-ttu-id="94a29-174">Дополнительные сведения см. в статьях [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](../blobs/storage-dotnet-how-to-use-blobs.md) и [Основные понятия службы BLOB-объектов](/rest/api/storageservices/blob-service-concepts).</span><span class="sxs-lookup"><span data-stu-id="94a29-174">For detailed information, see [Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](/rest/api/storageservices/blob-service-concepts).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="94a29-175">Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="94a29-175">Create a container</span></span>
<span data-ttu-id="94a29-176">Каждый BLOB-объект в хранилище Azure должен находиться в контейнере.</span><span class="sxs-lookup"><span data-stu-id="94a29-176">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="94a29-177">Контейнер можно создать с помощью hello `az storage container create` команды:</span><span class="sxs-lookup"><span data-stu-id="94a29-177">You can create a container by using hello `az storage container create` command:</span></span>

```azurecli
az storage container create --name <container_name>
```

<span data-ttu-id="94a29-178">Можно задать один из трех уровней доступа на чтение для нового контейнера с помощью hello необязательно `--public-access` аргумент:</span><span class="sxs-lookup"><span data-stu-id="94a29-178">You can set one of three levels of read access for a new container by specifying hello optional  `--public-access` argument:</span></span>

* <span data-ttu-id="94a29-179">`off`(по умолчанию): контейнер данных является закрытым toohello владелец учетной записи.</span><span class="sxs-lookup"><span data-stu-id="94a29-179">`off` (default): Container data is private toohello account owner.</span></span>
* <span data-ttu-id="94a29-180">`blob`: общий доступ на чтение для больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="94a29-180">`blob`: Public read access for blobs.</span></span>
* <span data-ttu-id="94a29-181">`container`: Открытого списка доступа toohello весь контейнер.</span><span class="sxs-lookup"><span data-stu-id="94a29-181">`container`: Public read and list access toohello entire container.</span></span>

<span data-ttu-id="94a29-182">Дополнительные сведения см. в разделе [управления toocontainers анонимный доступ для чтения и большие двоичные объекты](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="94a29-182">For more information, see [Manage anonymous read access toocontainers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>

### <a name="upload-a-blob-tooa-container"></a><span data-ttu-id="94a29-183">Отправка tooa контейнер больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="94a29-183">Upload a blob tooa container</span></span>
<span data-ttu-id="94a29-184">Хранилище BLOB-объектов Azure поддерживает блочные, добавочные и страничные BLOB-объекты.</span><span class="sxs-lookup"><span data-stu-id="94a29-184">Azure Blob storage supports block, append, and page blobs.</span></span> <span data-ttu-id="94a29-185">Отправка больших двоичных объектов tooa контейнера с помощью hello `blob upload` команды:</span><span class="sxs-lookup"><span data-stu-id="94a29-185">Upload blobs tooa container by using hello `blob upload` command:</span></span>

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 <span data-ttu-id="94a29-186">По умолчанию hello `blob upload` команда отправляет большие двоичные объекты toopage *.vhd файлы, или блочных BLOB-объектов в противном случае.</span><span class="sxs-lookup"><span data-stu-id="94a29-186">By default, hello `blob upload` command uploads *.vhd files toopage blobs, or block blobs otherwise.</span></span> <span data-ttu-id="94a29-187">toospecify другой тип при отправить большой двоичный объект, можно использовать hello `--type` аргумент--допустимыми значениями являются `append`, `block`, и `page`.</span><span class="sxs-lookup"><span data-stu-id="94a29-187">toospecify another type when you upload a blob, you can use hello `--type` argument--allowed values are `append`, `block`, and `page`.</span></span>

 <span data-ttu-id="94a29-188">Дополнительные сведения о типах другой большой двоичный объект hello. в разделе [основные сведения о блочных, добавлять большие двоичные объекты и страничные большие двоичные объекты](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span><span class="sxs-lookup"><span data-stu-id="94a29-188">For more information on hello different blob types, see [Understanding Block Blobs, Append Blobs, and Page Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span></span>


### <a name="download-a-blob-from-a-container"></a><span data-ttu-id="94a29-189">Скачивание большого двоичного объекта из контейнера</span><span class="sxs-lookup"><span data-stu-id="94a29-189">Download a blob from a container</span></span>
<span data-ttu-id="94a29-190">В этом примере показано, как toodownload большого двоичного объекта из контейнера:</span><span class="sxs-lookup"><span data-stu-id="94a29-190">This example demonstrates how toodownload a blob from a container:</span></span>

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="94a29-191">Перечисление hello больших двоичных объектов в контейнере</span><span class="sxs-lookup"><span data-stu-id="94a29-191">List hello blobs in a container</span></span>

<span data-ttu-id="94a29-192">Перечисление hello больших двоичных объектов в контейнере с hello [списка больших двоичных объектов хранилища az](/cli/azure/storage/blob#list) команды.</span><span class="sxs-lookup"><span data-stu-id="94a29-192">List hello blobs in a container with hello [az storage blob list](/cli/azure/storage/blob#list) command.</span></span>

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a><span data-ttu-id="94a29-193">Копирование BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="94a29-193">Copy blobs</span></span>
<span data-ttu-id="94a29-194">Можно асинхронно копировать BLOB-объекты между учетными записями хранения и областями или внутри них.</span><span class="sxs-lookup"><span data-stu-id="94a29-194">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="94a29-195">Hello ниже приведен пример tooanother учетной записи toocopy больших двоичных объектов из одного места хранения.</span><span class="sxs-lookup"><span data-stu-id="94a29-195">hello following example demonstrates how toocopy blobs from one storage account tooanother.</span></span> <span data-ttu-id="94a29-196">Сначала создается контейнер в учетной записи хранения источника hello, указав доступ для чтения к его большим двоичным объектам.</span><span class="sxs-lookup"><span data-stu-id="94a29-196">We first create a container in hello source storage account, specifying public read-access for its blobs.</span></span> <span data-ttu-id="94a29-197">Далее мы отправьте файл toohello контейнера и, наконец, копирования hello BLOB-объекта контейнера, в котором в контейнер в учетной записи хранения назначения hello.</span><span class="sxs-lookup"><span data-stu-id="94a29-197">Next, we upload a file toohello container, and finally, copy hello blob from that container into a container in hello destination storage account.</span></span>

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob toocontainer in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account toodestination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

<span data-ttu-id="94a29-198">В приведенном выше примере hello hello конечный контейнер должен уже существовать в hello целевой учетной записью хранения для toosucceed операцию копирования hello.</span><span class="sxs-lookup"><span data-stu-id="94a29-198">In hello above example, hello destination container must already exist in hello destination storage account for hello copy operation toosucceed.</span></span> <span data-ttu-id="94a29-199">Кроме того, hello исходного большого двоичного объекта указан в hello `--source-uri` аргумент должен включать токен общего доступа адреса (SAS) или быть общедоступным, как показано в примере.</span><span class="sxs-lookup"><span data-stu-id="94a29-199">Additionally, hello source blob specified in hello `--source-uri` argument must either include a shared access signature (SAS) token, or be publicly accessible, as in this example.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="94a29-200">Удаление большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="94a29-200">Delete a blob</span></span>
<span data-ttu-id="94a29-201">toodelete большого двоичного объекта используйте hello `blob delete` команды:</span><span class="sxs-lookup"><span data-stu-id="94a29-201">toodelete a blob, use hello `blob delete` command:</span></span>

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="94a29-202">Создание общих папок и управление ими</span><span class="sxs-lookup"><span data-stu-id="94a29-202">Create and manage file shares</span></span>
<span data-ttu-id="94a29-203">Хранилище файлов Azure предоставляет общее хранилище для приложений с помощью протокола Server Message Block (SMB) hello.</span><span class="sxs-lookup"><span data-stu-id="94a29-203">Azure File storage offers shared storage for applications using hello Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="94a29-204">Виртуальные машины Microsoft Azure и облачные службы, а также локальные приложения, могут совместно использовать данные через монтированные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="94a29-204">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="94a29-205">Вы можете управлять файловыми ресурсами и файл данных с помощью hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="94a29-205">You can manage file shares and file data via hello Azure CLI.</span></span> <span data-ttu-id="94a29-206">Дополнительные сведения о хранилище файлов Azure см. в разделе [приступить к работе с хранилищем Windows Azure файл](../storage-dotnet-how-to-use-files.md) или [как toouse хранилища Azure File с Linux](../storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="94a29-206">For more information on Azure File storage, see [Get started with Azure File storage on Windows](../storage-dotnet-how-to-use-files.md) or [How toouse Azure File storage with Linux](../storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="94a29-207">Создайте общую папку</span><span class="sxs-lookup"><span data-stu-id="94a29-207">Create a file share</span></span>
<span data-ttu-id="94a29-208">Общая папка Azure представляет собой общую папку с файлами SMB в Azure.</span><span class="sxs-lookup"><span data-stu-id="94a29-208">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="94a29-209">Все каталоги и файлы должны быть созданы в общей папке.</span><span class="sxs-lookup"><span data-stu-id="94a29-209">All directories and files must be created in a file share.</span></span> <span data-ttu-id="94a29-210">Учетная запись может содержать неограниченное количество общих ресурсов и общую папку можно сохранить неограниченное количество файлов копирование ограничения емкости toohello hello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="94a29-210">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up toohello capacity limits of hello storage account.</span></span> <span data-ttu-id="94a29-211">Hello следующий пример создает общую папку с именем **myshare**.</span><span class="sxs-lookup"><span data-stu-id="94a29-211">hello following example creates a file share named **myshare**.</span></span>

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="94a29-212">Создайте каталог</span><span class="sxs-lookup"><span data-stu-id="94a29-212">Create a directory</span></span>
<span data-ttu-id="94a29-213">Каталог обеспечивает иерархическую структуру в общей папке Azure.</span><span class="sxs-lookup"><span data-stu-id="94a29-213">A directory provides a hierarchical structure in an Azure file share.</span></span> <span data-ttu-id="94a29-214">Hello следующий пример создает каталог с именем **myDir** в общей папке hello.</span><span class="sxs-lookup"><span data-stu-id="94a29-214">hello following example creates a directory named **myDir** in hello file share.</span></span>

```azurecli
az storage directory create --name myDir --share-name myshare
```

<span data-ttu-id="94a29-215">Путь к каталогу может включать несколько уровней, например **dir1/dir2**.</span><span class="sxs-lookup"><span data-stu-id="94a29-215">A directory path can include multiple levels, for example **dir1/dir2**.</span></span> <span data-ttu-id="94a29-216">Однако прежде чем создавать подкаталог, необходимо убедиться в наличии всех родительских каталогов.</span><span class="sxs-lookup"><span data-stu-id="94a29-216">However, you must ensure that all parent directories exist before creating a subdirectory.</span></span> <span data-ttu-id="94a29-217">Например, для пути **dir1/dir2** вам потребуется сначала создать каталог **dir1**, а затем — каталог **dir2**.</span><span class="sxs-lookup"><span data-stu-id="94a29-217">For example, for path **dir1/dir2**, you must first create directory **dir1**, then create directory **dir2**.</span></span>

### <a name="upload-a-local-file-tooa-share"></a><span data-ttu-id="94a29-218">Отправка в локальной папке tooa</span><span class="sxs-lookup"><span data-stu-id="94a29-218">Upload a local file tooa share</span></span>
<span data-ttu-id="94a29-219">Hello следующий пример отправляет файл из **~/temp/samplefile.txt** tooroot из hello **myshare** общей папки.</span><span class="sxs-lookup"><span data-stu-id="94a29-219">hello following example uploads a file from **~/temp/samplefile.txt** tooroot of hello **myshare** file share.</span></span> <span data-ttu-id="94a29-220">Hello `--source` аргумент задает существующего локального файла tooupload hello.</span><span class="sxs-lookup"><span data-stu-id="94a29-220">hello `--source` argument specifies hello existing local file tooupload.</span></span>

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

<span data-ttu-id="94a29-221">Как и в случае создания каталога можно указать путь к каталогу в hello общего ресурса tooupload hello tooan существующий каталог файлов в общей папке hello:</span><span class="sxs-lookup"><span data-stu-id="94a29-221">As with directory creation, you can specify a directory path within hello share tooupload hello file tooan existing directory within hello share:</span></span>

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

<span data-ttu-id="94a29-222">Копирование ТБ too1 может быть файл в общей папке hello.</span><span class="sxs-lookup"><span data-stu-id="94a29-222">A file in hello share can be up too1 TB in size.</span></span>

### <a name="list-hello-files-in-a-share"></a><span data-ttu-id="94a29-223">Список файлов hello в общей папке</span><span class="sxs-lookup"><span data-stu-id="94a29-223">List hello files in a share</span></span>
<span data-ttu-id="94a29-224">Список файлов и каталогов в общей папке, можно с помощью hello `az storage file list` команды:</span><span class="sxs-lookup"><span data-stu-id="94a29-224">You can list files and directories in a share by using hello `az storage file list` command:</span></span>

```azurecli
# List hello files in hello root of a share
az storage file list --share-name myshare --output table

# List hello files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List hello files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a><span data-ttu-id="94a29-225">Копирование файлов</span><span class="sxs-lookup"><span data-stu-id="94a29-225">Copy files</span></span>      
<span data-ttu-id="94a29-226">Можно скопировать файл tooanother, большой двоичный объект файла tooa или tooa файла большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="94a29-226">You can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="94a29-227">Например, toocopy tooa каталога файла в другую общую папку:</span><span class="sxs-lookup"><span data-stu-id="94a29-227">For example, toocopy a file tooa directory in a different share:</span></span>        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a><span data-ttu-id="94a29-228">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="94a29-228">Next steps</span></span>
<span data-ttu-id="94a29-229">Ниже приведены некоторые дополнительные ресурсы для изучения работы с hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="94a29-229">Here are some additional resources for learning more about working with hello Azure CLI 2.0.</span></span>

* <span data-ttu-id="94a29-230">[Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) (Приступая к работе с Azure CLI 2.0)</span><span class="sxs-lookup"><span data-stu-id="94a29-230">[Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)</span></span>
* <span data-ttu-id="94a29-231">[Azure CLI 2.0 command reference](/cli/azure) (Справочник по командам Azure CLI 2.0)</span><span class="sxs-lookup"><span data-stu-id="94a29-231">[Azure CLI 2.0 command reference](/cli/azure)</span></span>
* [<span data-ttu-id="94a29-232">Статья об Azure CLI 2.0 на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="94a29-232">Azure CLI 2.0 on GitHub</span></span>](https://github.com/Azure/azure-cli)
