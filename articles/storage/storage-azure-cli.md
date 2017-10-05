---
title: "Использование Azure CLI 2.0 со службой хранилища Azure | Документация Майкрософт"
description: "Узнайте, как использовать интерфейс командной строки Azure (Azure CLI) версии 2.0 для создания учетных записей хранения и управления ими, а также для работы с большими двоичными объектами и файлами Azure в службе хранилища Azure. Azure CLI 2.0 — это кроссплатформенное средство, написанное на языке Python."
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
ms.openlocfilehash: 6098216f7dd901ea48fb3ab969c7934cc288b247
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-cli-20-with-azure-storage"></a><span data-ttu-id="b80ea-104">Использование Azure CLI 2.0 со службой хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="b80ea-104">Using the Azure CLI 2.0 with Azure Storage</span></span>

<span data-ttu-id="b80ea-105">Кроссплатформенный Azure CLI 2.0 с открытым кодом представляет собой набор команд для работы с платформой Azure.</span><span class="sxs-lookup"><span data-stu-id="b80ea-105">The open-source, cross-platform Azure CLI 2.0 provides a set of commands for working with the Azure platform.</span></span> <span data-ttu-id="b80ea-106">Он предоставляет практически те же функции, что и [портал Azure](https://portal.azure.com), а также различные возможности доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="b80ea-106">It provides much of the same functionality found in the [Azure portal](https://portal.azure.com), including rich data access.</span></span>

<span data-ttu-id="b80ea-107">В этом руководстве рассказывается о том, как использовать [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) для выполнения нескольких задач при работе с ресурсами в учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="b80ea-107">In this guide, we show you how to use the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) to perform several tasks working with resources in your Azure Storage account.</span></span> <span data-ttu-id="b80ea-108">Рекомендуем скачать и установить (или обновить до последней версии) CLI 2.0, прежде чем продолжать работу с этим руководством.</span><span class="sxs-lookup"><span data-stu-id="b80ea-108">We recommend that you download and install or upgrade to the latest version of the CLI 2.0 before using this guide.</span></span>

<span data-ttu-id="b80ea-109">В примерах, приведенных в этом руководстве, используется оболочка Bash на Ubuntu. Другие платформы должны работать аналогично.</span><span class="sxs-lookup"><span data-stu-id="b80ea-109">The examples in the guide assume the use of the Bash shell on Ubuntu, but other platforms should perform similarly.</span></span> 

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a><span data-ttu-id="b80ea-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b80ea-110">Prerequisites</span></span>
<span data-ttu-id="b80ea-111">В этом руководстве предполагается, что вам знакомы основные понятия службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="b80ea-111">This guide assumes that you understand the basic concepts of Azure Storage.</span></span> <span data-ttu-id="b80ea-112">Также предполагается, что вы можете выполнить требования для создания учетной записи и службы хранилища Azure. Эти требования перечислены ниже.</span><span class="sxs-lookup"><span data-stu-id="b80ea-112">It also assumes that you're able to satisfy the account creation requirements that are specified below for Azure and the Storage service.</span></span>

### <a name="accounts"></a><span data-ttu-id="b80ea-113">Учетные записи</span><span class="sxs-lookup"><span data-stu-id="b80ea-113">Accounts</span></span>
* <span data-ttu-id="b80ea-114">**Учетная запись Azure.** Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="b80ea-114">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="b80ea-115">**Учетная запись хранения**. См. раздел [Создание учетной записи хранения](../storage/storage-create-storage-account.md#create-a-storage-account) в статье [Об учетных записях хранения Azure](../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="b80ea-115">**Storage account**: See [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/storage-create-storage-account.md).</span></span>

### <a name="install-the-azure-cli-20"></a><span data-ttu-id="b80ea-116">Установка Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b80ea-116">Install the Azure CLI 2.0</span></span>

<span data-ttu-id="b80ea-117">Скачайте и установите Azure CLI 2.0 согласно инструкциям в статье [Install Azure CLI 2.0](/cli/azure/install-az-cli2) (Установка Azure CLI 2.0).</span><span class="sxs-lookup"><span data-stu-id="b80ea-117">Download and install the Azure CLI 2.0 by following the instructions outlined in [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

> [!TIP]
> <span data-ttu-id="b80ea-118">Если у вас возникают проблемы с установкой, см. сведения об устранении неполадок в [этом разделе](/cli/azure/install-az-cli2#installation-troubleshooting) и в руководстве по [устранению неполадок при установке](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) на GitHub.</span><span class="sxs-lookup"><span data-stu-id="b80ea-118">If you have trouble with the installation, check out the [Installation Troubleshooting](/cli/azure/install-az-cli2#installation-troubleshooting) section of the article, and the [Install Troubleshooting](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guide on GitHub.</span></span>
>

## <a name="working-with-the-cli"></a><span data-ttu-id="b80ea-119">Работа с интерфейсом командной строки</span><span class="sxs-lookup"><span data-stu-id="b80ea-119">Working with the CLI</span></span>

<span data-ttu-id="b80ea-120">После установки Azure CLI для доступа к соответствующим функциям вы можете использовать команду `az` в интерфейсе командной строки (Bash, терминал, командная строка).</span><span class="sxs-lookup"><span data-stu-id="b80ea-120">Once you've installed the CLI, you can use the `az` command in your command-line interface (Bash, Terminal, Command Prompt) to access the Azure CLI commands.</span></span> <span data-ttu-id="b80ea-121">Введите команду `az`, чтобы отобразить полный список основных команд (пример выходных данных ниже приведен в сокращении):</span><span class="sxs-lookup"><span data-stu-id="b80ea-121">Type the `az` command to see a full list of the base commands (the following example output has been truncated):</span></span>

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome to the cool new Azure CLI!

Here are the base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

<span data-ttu-id="b80ea-122">В интерфейсе командной строки выполните команду `az storage --help`, чтобы вывести список подгрупп команды `storage`.</span><span class="sxs-lookup"><span data-stu-id="b80ea-122">In your command-line interface, execute the command `az storage --help` to list the `storage` command subgroups.</span></span> <span data-ttu-id="b80ea-123">Описания подгрупп дают общие сведения о функциональных возможностях, предоставляемых Azure CLI для работы с ресурсами хранилища.</span><span class="sxs-lookup"><span data-stu-id="b80ea-123">The descriptions of the subgroups provide an overview of the functionality the Azure CLI provides for working with your storage resources.</span></span>

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
    file     : File shares that use the standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues to effectively scale applications according to traffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-the-cli-to-your-azure-subscription"></a><span data-ttu-id="b80ea-124">Подключение интерфейса командной строки к своей подписке Azure</span><span class="sxs-lookup"><span data-stu-id="b80ea-124">Connect the CLI to your Azure subscription</span></span>

<span data-ttu-id="b80ea-125">Для работы с ресурсами в подписке Azure необходимо сначала войти в учетную запись Azure с помощью `az login`.</span><span class="sxs-lookup"><span data-stu-id="b80ea-125">To work with the resources in your Azure subscription, you must first log in to your Azure account with `az login`.</span></span> <span data-ttu-id="b80ea-126">Для этого существует несколько способов.</span><span class="sxs-lookup"><span data-stu-id="b80ea-126">There are several ways you can log in:</span></span>

* <span data-ttu-id="b80ea-127">**Интерактивный вход**: `az login`.</span><span class="sxs-lookup"><span data-stu-id="b80ea-127">**Interactive login**: `az login`</span></span>
* <span data-ttu-id="b80ea-128">**Вход с использованием имени пользователя SSH и пароля**: `az login -u johndoe@contoso.com -p VerySecret`.</span><span class="sxs-lookup"><span data-stu-id="b80ea-128">**Log in with user name and password**: `az login -u johndoe@contoso.com -p VerySecret`</span></span>
  * <span data-ttu-id="b80ea-129">Этот способ не работает с учетными записями Майкрософт или с учетными записями, которые используют многофакторную идентификацию.</span><span class="sxs-lookup"><span data-stu-id="b80ea-129">This doesn't work with Microsoft accounts or accounts that use multi-factor authentication.</span></span>
* <span data-ttu-id="b80ea-130">**Вход с использованием субъекта-службы**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="b80ea-130">**Log in with a service principal**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span></span>

## <a name="azure-cli-20-sample-script"></a><span data-ttu-id="b80ea-131">Пример скрипта Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b80ea-131">Azure CLI 2.0 sample script</span></span>

<span data-ttu-id="b80ea-132">Далее мы создадим небольшой сценарий оболочки, который запускает несколько базовых команд Azure CLI 2.0 для взаимодействия с ресурсами службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="b80ea-132">Next, we'll work with a small shell script that issues a few basic Azure CLI 2.0 commands to interact with Azure Storage resources.</span></span> <span data-ttu-id="b80ea-133">Сначала скрипт создает новый контейнер в учетной записи хранения, а затем отправляет существующий файл (в виде большого двоичного объекта) в этот контейнер.</span><span class="sxs-lookup"><span data-stu-id="b80ea-133">The script first creates a new container in your storage account, then uploads an existing file (as a blob) to that container.</span></span> <span data-ttu-id="b80ea-134">После этого он выводит список всех больших двоичных объектов в контейнере и скачивает файл в заданное вами место на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="b80ea-134">It then lists all blobs in the container, and finally, downloads the file to a destination on your local computer that you specify.</span></span>

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating the container..."
az storage container create --name $container_name

echo "Uploading the file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing the blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading the file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

<span data-ttu-id="b80ea-135">**Настройка и запуск скрипта**</span><span class="sxs-lookup"><span data-stu-id="b80ea-135">**Configure and run the script**</span></span>

1. <span data-ttu-id="b80ea-136">Откройте текстовый редактор по выбору, а затем скопируйте и вставьте в него предыдущий скрипт.</span><span class="sxs-lookup"><span data-stu-id="b80ea-136">Open your favorite text editor, then copy and paste the preceding script into the editor.</span></span>

2. <span data-ttu-id="b80ea-137">После этого обновите переменные скрипта в соответствии с параметрами конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b80ea-137">Next, update the script's variables to reflect your configuration settings.</span></span> <span data-ttu-id="b80ea-138">Замените следующие значения соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="b80ea-138">Replace the following values as specified:</span></span>

   * <span data-ttu-id="b80ea-139">**\<storage_account_name\>**: имя вашей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="b80ea-139">**\<storage_account_name\>** The name of your storage account.</span></span>
   * <span data-ttu-id="b80ea-140">**\<storage_account_key\>**: первичный или вторичный ключ доступа к вашей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="b80ea-140">**\<storage_account_key\>** The primary or secondary access key for your storage account.</span></span>
   * <span data-ttu-id="b80ea-141">**\<container_name\>**: имя нового контейнера, который необходимо создать, например azure-cli-sample-container.</span><span class="sxs-lookup"><span data-stu-id="b80ea-141">**\<container_name\>** A name the new container to create, such as "azure-cli-sample-container".</span></span>
   * <span data-ttu-id="b80ea-142">**\<blob_name\>**: имя целевого большого двоичного объекта в контейнере.</span><span class="sxs-lookup"><span data-stu-id="b80ea-142">**\<blob_name\>** A name for the destination blob in the container.</span></span>
   * <span data-ttu-id="b80ea-143">**\<file_to_upload\>**: путь к небольшому файлу на локальном компьютере, например ~/images/HelloWorld.png.</span><span class="sxs-lookup"><span data-stu-id="b80ea-143">**\<file_to_upload\>** The path to small file on your local computer, such as "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="b80ea-144">**\<destination_file\>**: путь к конечному файлу, например ~/downloadedImage.png.</span><span class="sxs-lookup"><span data-stu-id="b80ea-144">**\<destination_file\>** The destination file path, such as "~/downloadedImage.png".</span></span>

3. <span data-ttu-id="b80ea-145">После обновления необходимых переменных сохраните скрипт и выйдите из редактора.</span><span class="sxs-lookup"><span data-stu-id="b80ea-145">After you've updated the necessary variables, save the script and exit your editor.</span></span> <span data-ttu-id="b80ea-146">В описанных ниже действиях предполагается, что скрипту присвоено имя **my_storage_sample.sh**.</span><span class="sxs-lookup"><span data-stu-id="b80ea-146">The next steps assume you've named your script **my_storage_sample.sh**.</span></span>

4. <span data-ttu-id="b80ea-147">При необходимости пометьте скрипт как исполняемый файл: `chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="b80ea-147">Mark the script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>

5. <span data-ttu-id="b80ea-148">Выполните скрипт,</span><span class="sxs-lookup"><span data-stu-id="b80ea-148">Execute the script.</span></span> <span data-ttu-id="b80ea-149">например в Bash: `./my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="b80ea-149">For example, in Bash: `./my_storage_sample.sh`</span></span>

<span data-ttu-id="b80ea-150">Вы увидите результат, аналогичный приведенному ниже. Указанный в скрипте **\<destination_file\>** появится на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="b80ea-150">You should see output similar to the following, and the **\<destination_file\>** you specified in the script should appear on your local computer.</span></span>

```
Creating the container...
{
  "created": true
}
Uploading the file...
Percent complete: %100.0
Listing the blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading the file...
Name
---------
README.md
Done
```

> [!TIP]
> <span data-ttu-id="b80ea-151">Предыдущие выходные данные отображаются в **табличном** формате.</span><span class="sxs-lookup"><span data-stu-id="b80ea-151">The preceding output is in **table** format.</span></span> <span data-ttu-id="b80ea-152">Можно указать, какой формат выходных данных следует использовать. Для этого задайте аргумент `--output` в командах интерфейса командной строки или задайте его глобально с помощью `az configure`.</span><span class="sxs-lookup"><span data-stu-id="b80ea-152">You can specify which output format to use by specifying the `--output` argument in your CLI commands, or set it globally using `az configure`.</span></span>
>

## <a name="manage-storage-accounts"></a><span data-ttu-id="b80ea-153">Управление учетными записями хранения</span><span class="sxs-lookup"><span data-stu-id="b80ea-153">Manage storage accounts</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="b80ea-154">Создание новой учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="b80ea-154">Create a new storage account</span></span>
<span data-ttu-id="b80ea-155">Для использования службы хранилища Azure вам потребуется учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="b80ea-155">To use Azure Storage, you need a storage account.</span></span> <span data-ttu-id="b80ea-156">После настройки компьютера для [подключения к подписке](#connect-to-your-azure-subscription) можно создать новую учетную запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="b80ea-156">You can create a new Azure Storage account after you've configured your computer to [connect to your subscription](#connect-to-your-azure-subscription).</span></span>

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* <span data-ttu-id="b80ea-157">`--location` — расположение (обязательный параметр).</span><span class="sxs-lookup"><span data-stu-id="b80ea-157">`--location` [Required]: Location.</span></span> <span data-ttu-id="b80ea-158">Например, "западная часть США".</span><span class="sxs-lookup"><span data-stu-id="b80ea-158">For example, "West US".</span></span>
* <span data-ttu-id="b80ea-159">`--name` — имя учетной записи хранения (обязательный параметр).</span><span class="sxs-lookup"><span data-stu-id="b80ea-159">`--name` [Required]: The storage account name.</span></span> <span data-ttu-id="b80ea-160">Имя должно быть не меньше 3 и не больше 24 символов и содержать только буквенно-цифровые символы.</span><span class="sxs-lookup"><span data-stu-id="b80ea-160">The name must be 3 to 24 characters in length, and use only lowercase alphanumeric characters.</span></span>
* <span data-ttu-id="b80ea-161">`--resource-group` — имя группы ресурсов (обязательный параметр).</span><span class="sxs-lookup"><span data-stu-id="b80ea-161">`--resource-group` [Required]: Name of resource group.</span></span>
* <span data-ttu-id="b80ea-162">`--sku` — номер SKU учетной записи хранения (обязательный параметр).</span><span class="sxs-lookup"><span data-stu-id="b80ea-162">`--sku` [Required]: The storage account SKU.</span></span> <span data-ttu-id="b80ea-163">Допустимые значения:</span><span class="sxs-lookup"><span data-stu-id="b80ea-163">Allowed values:</span></span>
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a><span data-ttu-id="b80ea-164">Установка учетной записи хранения Azure по умолчанию в переменные среды</span><span class="sxs-lookup"><span data-stu-id="b80ea-164">Set default Azure storage account environment variables</span></span>
<span data-ttu-id="b80ea-165">В подписке может быть несколько учетных записей хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="b80ea-165">You can have multiple storage accounts in your Azure subscription.</span></span> <span data-ttu-id="b80ea-166">Чтобы выбрать одну из них для использования для всех последующих команд службы хранилища, задайте эти переменные среды:</span><span class="sxs-lookup"><span data-stu-id="b80ea-166">To select one of them to use for all subsequent storage commands, you can set these environment variables:</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="b80ea-167">Установить учетную запись хранения по умолчанию можно также с помощью строки подключения.</span><span class="sxs-lookup"><span data-stu-id="b80ea-167">Another way to set a default storage account is by using a connection string.</span></span> <span data-ttu-id="b80ea-168">Сначала получите строку подключения с помощью команды `show-connection-string`:</span><span class="sxs-lookup"><span data-stu-id="b80ea-168">First, get the connection string with the `show-connection-string` command:</span></span>

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

<span data-ttu-id="b80ea-169">Затем скопируйте полученную строку подключения и задайте переменную среды `AZURE_STORAGE_CONNECTION_STRING` (строки подключения может понадобиться заключить в кавычки):</span><span class="sxs-lookup"><span data-stu-id="b80ea-169">Then copy the output connection string and set the `AZURE_STORAGE_CONNECTION_STRING` environment variable (you might need to enclose the connection string in quotes):</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> <span data-ttu-id="b80ea-170">Во всех примерах в следующих разделах этой статьи предполагается, что вы задали переменные среды `AZURE_STORAGE_ACCOUNT` и `AZURE_STORAGE_ACCESS_KEY`.</span><span class="sxs-lookup"><span data-stu-id="b80ea-170">All examples in the following sections of this article assume that you've set the `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY` environment variables.</span></span>
>

## <a name="create-and-manage-blobs"></a><span data-ttu-id="b80ea-171">Создание больших двоичных объектов (BLOB-объектов) и управление ими</span><span class="sxs-lookup"><span data-stu-id="b80ea-171">Create and manage blobs</span></span>
<span data-ttu-id="b80ea-172">Хранилище BLOB-объектов Azure — это служба хранения большого количества неструктурированных данных, таких как текстовые или бинарные файлы, к которым можно получить доступ практически из любой точки мира по протоколу HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b80ea-172">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="b80ea-173">В этом разделе предполагается, что вы уже знакомы с понятиями службы хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="b80ea-173">This section assumes that you are already familiar with Azure Blob storage concepts.</span></span> <span data-ttu-id="b80ea-174">Дополнительные сведения см. в статьях [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](storage-dotnet-how-to-use-blobs.md) и [Основные понятия службы BLOB-объектов](/rest/api/storageservices/blob-service-concepts).</span><span class="sxs-lookup"><span data-stu-id="b80ea-174">For detailed information, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](/rest/api/storageservices/blob-service-concepts).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="b80ea-175">Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="b80ea-175">Create a container</span></span>
<span data-ttu-id="b80ea-176">Каждый BLOB-объект в хранилище Azure должен находиться в контейнере.</span><span class="sxs-lookup"><span data-stu-id="b80ea-176">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="b80ea-177">Вы можете создать контейнер с помощью команды `az storage container create`:</span><span class="sxs-lookup"><span data-stu-id="b80ea-177">You can create a container by using the `az storage container create` command:</span></span>

```azurecli
az storage container create --name <container_name>
```

<span data-ttu-id="b80ea-178">Для нового контейнера можно задать один из трех уровней доступа на чтение с помощью необязательного аргумента `--public-access`.</span><span class="sxs-lookup"><span data-stu-id="b80ea-178">You can set one of three levels of read access for a new container by specifying the optional  `--public-access` argument:</span></span>

* <span data-ttu-id="b80ea-179">`off`: данные контейнера являются личными данными владельца учетной записи (значение по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="b80ea-179">`off` (default): Container data is private to the account owner.</span></span>
* <span data-ttu-id="b80ea-180">`blob`: общий доступ на чтение для больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="b80ea-180">`blob`: Public read access for blobs.</span></span>
* <span data-ttu-id="b80ea-181">`container`: общий доступ на чтение и создание списков для всего контейнера.</span><span class="sxs-lookup"><span data-stu-id="b80ea-181">`container`: Public read and list access to the entire container.</span></span>

<span data-ttu-id="b80ea-182">Дополнительные сведения см. в статье [Управление анонимным доступом на чтение к контейнерам и большим двоичным объектам](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="b80ea-182">For more information, see [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>

### <a name="upload-a-blob-to-a-container"></a><span data-ttu-id="b80ea-183">Отправка большого двоичного объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="b80ea-183">Upload a blob to a container</span></span>
<span data-ttu-id="b80ea-184">Хранилище BLOB-объектов Azure поддерживает блочные, добавочные и страничные BLOB-объекты.</span><span class="sxs-lookup"><span data-stu-id="b80ea-184">Azure Blob storage supports block, append, and page blobs.</span></span> <span data-ttu-id="b80ea-185">Отправьте большие двоичные объекты в контейнер с помощью команды `blob upload`:</span><span class="sxs-lookup"><span data-stu-id="b80ea-185">Upload blobs to a container by using the `blob upload` command:</span></span>

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 <span data-ttu-id="b80ea-186">По умолчанию команда `blob upload` отправляет файлы с расширением *.vhd в страничные или блочные BLOB-объекты.</span><span class="sxs-lookup"><span data-stu-id="b80ea-186">By default, the `blob upload` command uploads *.vhd files to page blobs, or block blobs otherwise.</span></span> <span data-ttu-id="b80ea-187">Чтобы указать другой тип при отправке большого двоичного объекта, можно использовать аргумент `--type`. Допустимые значения: `append`, `block`, и `page`.</span><span class="sxs-lookup"><span data-stu-id="b80ea-187">To specify another type when you upload a blob, you can use the `--type` argument--allowed values are `append`, `block`, and `page`.</span></span>

 <span data-ttu-id="b80ea-188">Дополнительные сведения о различных больших двоичных объектах см. в статье [Understanding Block Blobs, Append Blobs, and Page Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) (Основные сведения о блочных, добавочных и страничных BLOB-объектах).</span><span class="sxs-lookup"><span data-stu-id="b80ea-188">For more information on the different blob types, see [Understanding Block Blobs, Append Blobs, and Page Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span></span>


### <a name="download-a-blob-from-a-container"></a><span data-ttu-id="b80ea-189">Скачивание большого двоичного объекта из контейнера</span><span class="sxs-lookup"><span data-stu-id="b80ea-189">Download a blob from a container</span></span>
<span data-ttu-id="b80ea-190">Следующий пример демонстрирует скачивание больших двоичных объектов из контейнера:</span><span class="sxs-lookup"><span data-stu-id="b80ea-190">This example demonstrates how to download a blob from a container:</span></span>

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="b80ea-191">Перечисление BLOB-объектов в контейнере</span><span class="sxs-lookup"><span data-stu-id="b80ea-191">List the blobs in a container</span></span>

<span data-ttu-id="b80ea-192">Выведите список больших двоичных объектов в контейнере, выполнив команду [az storage blob list](/cli/azure/storage/blob#list).</span><span class="sxs-lookup"><span data-stu-id="b80ea-192">List the blobs in a container with the [az storage blob list](/cli/azure/storage/blob#list) command.</span></span>

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a><span data-ttu-id="b80ea-193">Копирование BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="b80ea-193">Copy blobs</span></span>
<span data-ttu-id="b80ea-194">Можно асинхронно копировать BLOB-объекты между учетными записями хранения и областями или внутри них.</span><span class="sxs-lookup"><span data-stu-id="b80ea-194">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="b80ea-195">Следующий пример демонстрирует копирование BLOB-объектов из одной учетной записи хранения в другую.</span><span class="sxs-lookup"><span data-stu-id="b80ea-195">The following example demonstrates how to copy blobs from one storage account to another.</span></span> <span data-ttu-id="b80ea-196">Сначала мы создадим контейнер в исходной учетной записи хранения, задав общий доступ для чтения к его большим двоичным объектам.</span><span class="sxs-lookup"><span data-stu-id="b80ea-196">We first create a container in the source storage account, specifying public read-access for its blobs.</span></span> <span data-ttu-id="b80ea-197">Далее мы передадим файл в контейнер и, наконец, скопируем большой двоичный объект из этого контейнера в контейнер в целевой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="b80ea-197">Next, we upload a file to the container, and finally, copy the blob from that container into a container in the destination storage account.</span></span>

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob to container in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account to destination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

<span data-ttu-id="b80ea-198">В приведенном выше примере для успешного выполнения операции копирования целевой контейнер уже должен существовать в целевой учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="b80ea-198">In the above example, the destination container must already exist in the destination storage account for the copy operation to succeed.</span></span> <span data-ttu-id="b80ea-199">Кроме того, исходный большой двоичный объект, указанный в аргументе `--source-uri`, либо должен включать в себя токен подписанного URL-адреса (SAS), либо быть общедоступным, как в данном примере.</span><span class="sxs-lookup"><span data-stu-id="b80ea-199">Additionally, the source blob specified in the `--source-uri` argument must either include a shared access signature (SAS) token, or be publicly accessible, as in this example.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="b80ea-200">Удаление большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="b80ea-200">Delete a blob</span></span>
<span data-ttu-id="b80ea-201">Чтобы удалить большой двоичный объект, используйте команду `blob delete`:</span><span class="sxs-lookup"><span data-stu-id="b80ea-201">To delete a blob, use the `blob delete` command:</span></span>

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="b80ea-202">Создание общих папок и управление ими</span><span class="sxs-lookup"><span data-stu-id="b80ea-202">Create and manage file shares</span></span>
<span data-ttu-id="b80ea-203">Хранилище файлов Azure предоставляет общее хранилище для приложений с помощью протокола SMB.</span><span class="sxs-lookup"><span data-stu-id="b80ea-203">Azure File storage offers shared storage for applications using the Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="b80ea-204">Виртуальные машины Microsoft Azure и облачные службы, а также локальные приложения, могут совместно использовать данные через монтированные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="b80ea-204">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="b80ea-205">Вы можете управлять общими папками и файловыми данными через интерфейс командной строки Azure.</span><span class="sxs-lookup"><span data-stu-id="b80ea-205">You can manage file shares and file data via the Azure CLI.</span></span> <span data-ttu-id="b80ea-206">Дополнительные сведения о хранилище файлов Azure см. в статье [Приступая к работе с хранилищем файлов Azure в Windows](storage-dotnet-how-to-use-files.md) или [Использование хранилища файлов Azure с Linux](storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b80ea-206">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) or [How to use Azure File storage with Linux](storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="b80ea-207">Создайте общую папку</span><span class="sxs-lookup"><span data-stu-id="b80ea-207">Create a file share</span></span>
<span data-ttu-id="b80ea-208">Общая папка Azure представляет собой общую папку с файлами SMB в Azure.</span><span class="sxs-lookup"><span data-stu-id="b80ea-208">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="b80ea-209">Все каталоги и файлы должны быть созданы в общей папке.</span><span class="sxs-lookup"><span data-stu-id="b80ea-209">All directories and files must be created in a file share.</span></span> <span data-ttu-id="b80ea-210">Учетная запись может содержать любое количество совместно используемых ресурсов, а ресурс может содержать любое количество файлов, насколько это позволяет емкость учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="b80ea-210">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up to the capacity limits of the storage account.</span></span> <span data-ttu-id="b80ea-211">В следующем примере создается общая папка с именем **myshare**.</span><span class="sxs-lookup"><span data-stu-id="b80ea-211">The following example creates a file share named **myshare**.</span></span>

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="b80ea-212">Создайте каталог</span><span class="sxs-lookup"><span data-stu-id="b80ea-212">Create a directory</span></span>
<span data-ttu-id="b80ea-213">Каталог обеспечивает иерархическую структуру в общей папке Azure.</span><span class="sxs-lookup"><span data-stu-id="b80ea-213">A directory provides a hierarchical structure in an Azure file share.</span></span> <span data-ttu-id="b80ea-214">В следующем примере в общей папке создается каталог с именем **myDir** .</span><span class="sxs-lookup"><span data-stu-id="b80ea-214">The following example creates a directory named **myDir** in the file share.</span></span>

```azurecli
az storage directory create --name myDir --share-name myshare
```

<span data-ttu-id="b80ea-215">Путь к каталогу может включать несколько уровней, например **dir1/dir2**.</span><span class="sxs-lookup"><span data-stu-id="b80ea-215">A directory path can include multiple levels, for example **dir1/dir2**.</span></span> <span data-ttu-id="b80ea-216">Однако прежде чем создавать подкаталог, необходимо убедиться в наличии всех родительских каталогов.</span><span class="sxs-lookup"><span data-stu-id="b80ea-216">However, you must ensure that all parent directories exist before creating a subdirectory.</span></span> <span data-ttu-id="b80ea-217">Например, для пути **dir1/dir2** вам потребуется сначала создать каталог **dir1**, а затем — каталог **dir2**.</span><span class="sxs-lookup"><span data-stu-id="b80ea-217">For example, for path **dir1/dir2**, you must first create directory **dir1**, then create directory **dir2**.</span></span>

### <a name="upload-a-local-file-to-a-share"></a><span data-ttu-id="b80ea-218">Отправка локального файла в общую папку</span><span class="sxs-lookup"><span data-stu-id="b80ea-218">Upload a local file to a share</span></span>
<span data-ttu-id="b80ea-219">В следующем примере выполняется отправка файла из **~/temp/samplefile.txt** в корень общей папки **myshare**.</span><span class="sxs-lookup"><span data-stu-id="b80ea-219">The following example uploads a file from **~/temp/samplefile.txt** to root of the **myshare** file share.</span></span> <span data-ttu-id="b80ea-220">Аргумент `--source` указывает существующий локальный файл для отправки.</span><span class="sxs-lookup"><span data-stu-id="b80ea-220">The `--source` argument specifies the existing local file to upload.</span></span>

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

<span data-ttu-id="b80ea-221">Как и при создании каталога, вы можете указать путь к каталогу в общей папке, чтобы отправить файл в существующий каталог внутри общей папки:</span><span class="sxs-lookup"><span data-stu-id="b80ea-221">As with directory creation, you can specify a directory path within the share to upload the file to an existing directory within the share:</span></span>

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

<span data-ttu-id="b80ea-222">Размер файла в общей папке может составлять до 1 ТБ.</span><span class="sxs-lookup"><span data-stu-id="b80ea-222">A file in the share can be up to 1 TB in size.</span></span>

### <a name="list-the-files-in-a-share"></a><span data-ttu-id="b80ea-223">Вывод списка файлов в общей папке</span><span class="sxs-lookup"><span data-stu-id="b80ea-223">List the files in a share</span></span>
<span data-ttu-id="b80ea-224">Вывести список файлов и каталогов в общей папке можно с помощью команды `az storage file list`:</span><span class="sxs-lookup"><span data-stu-id="b80ea-224">You can list files and directories in a share by using the `az storage file list` command:</span></span>

```azurecli
# List the files in the root of a share
az storage file list --share-name myshare --output table

# List the files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List the files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a><span data-ttu-id="b80ea-225">Копирование файлов</span><span class="sxs-lookup"><span data-stu-id="b80ea-225">Copy files</span></span>      
<span data-ttu-id="b80ea-226">Вы можете скопировать файл в другой файл, файл в большой двоичный объект или большой двоичный объект в файл.</span><span class="sxs-lookup"><span data-stu-id="b80ea-226">You can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="b80ea-227">Например, чтобы скопировать файл в каталог в другой общей папке, выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="b80ea-227">For example, to copy a file to a directory in a different share:</span></span>        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a><span data-ttu-id="b80ea-228">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b80ea-228">Next steps</span></span>
<span data-ttu-id="b80ea-229">Дополнительные сведения о работе с Azure CLI 2.0 см. в следующих ресурсах:</span><span class="sxs-lookup"><span data-stu-id="b80ea-229">Here are some additional resources for learning more about working with the Azure CLI 2.0.</span></span>

* <span data-ttu-id="b80ea-230">[Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) (Приступая к работе с Azure CLI 2.0)</span><span class="sxs-lookup"><span data-stu-id="b80ea-230">[Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)</span></span>
* <span data-ttu-id="b80ea-231">[Azure CLI 2.0 command reference](/cli/azure) (Справочник по командам Azure CLI 2.0)</span><span class="sxs-lookup"><span data-stu-id="b80ea-231">[Azure CLI 2.0 command reference](/cli/azure)</span></span>
* [<span data-ttu-id="b80ea-232">Статья об Azure CLI 2.0 на сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="b80ea-232">Azure CLI 2.0 on GitHub</span></span>](https://github.com/Azure/azure-cli)
