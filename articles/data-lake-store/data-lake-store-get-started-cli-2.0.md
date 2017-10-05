---
title: "Использование Azure Data Lake Store с помощью интерфейса командной строки Azure CLI 2.0 | Документация Майкрософт"
description: "Использование кроссплатформенного интерфейса командной строки Azure 2.0 для создания учетной записи Data Lake Store и выполнения базовых операций"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 4ffa0f4a-1cca-46ac-803d-1fc8538c685b
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: ed78d25f2bac0a9996f1796ee503f31a36940977
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a><span data-ttu-id="166ab-103">Начало работы с Azure Data Lake Store с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="166ab-103">Get started with Azure Data Lake Store using Azure CLI 2.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="166ab-104">Портал</span><span class="sxs-lookup"><span data-stu-id="166ab-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="166ab-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="166ab-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="166ab-106">Пакет SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="166ab-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="166ab-107">Пакет SDK для Java</span><span class="sxs-lookup"><span data-stu-id="166ab-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="166ab-108">REST API</span><span class="sxs-lookup"><span data-stu-id="166ab-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="166ab-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="166ab-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="166ab-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="166ab-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="166ab-111">Python</span><span class="sxs-lookup"><span data-stu-id="166ab-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="166ab-112">Узнайте, как с помощью Azure CLI 2.0 создать учетную запись Azure Data Lake Store и выполнять такие базовые операции, как создание папок, передача и загрузка файлов данных, удаление учетной записи и т. д. Дополнительные сведения о Data Lake Store см. в [обзоре Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="166ab-112">Learn how to use Azure CLI 2.0 to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="166ab-113">Azure CLI 2.0 — это новый интерфейс командной строки Azure для управления ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="166ab-113">The Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="166ab-114">Его можно использовать в Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="166ab-114">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="166ab-115">Дополнительные сведения см. в [обзоре Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="166ab-115">For more information, see [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview).</span></span> <span data-ttu-id="166ab-116">Полный список команд и синтаксис см. в [справочнике интерфейса командной строки 2.0 Azure Data Lake Store](https://docs.microsoft.com/cli/azure/dls).</span><span class="sxs-lookup"><span data-stu-id="166ab-116">You can also look at the [Azure Data Lake Store CLI 2.0 reference](https://docs.microsoft.com/cli/azure/dls) for a complete list of commands and syntax.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="166ab-117">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="166ab-117">Prerequisites</span></span>
<span data-ttu-id="166ab-118">Перед началом работы с этой статьей необходимо иметь следующее:</span><span class="sxs-lookup"><span data-stu-id="166ab-118">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="166ab-119">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="166ab-119">**An Azure subscription**.</span></span> <span data-ttu-id="166ab-120">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="166ab-120">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="166ab-121">**Azure CLI 2.0** — см. инструкции в статье об [установке Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="166ab-121">**Azure CLI 2.0** - See [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) for instructions.</span></span>

## <a name="authentication"></a><span data-ttu-id="166ab-122">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="166ab-122">Authentication</span></span>

<span data-ttu-id="166ab-123">В этой статье используется более простой подход к проверке подлинности в службе Data Lake Store, в которую выполняется вход от имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="166ab-123">This article uses a simpler authentication approach with Data Lake Store where you log in as an end-user user.</span></span> <span data-ttu-id="166ab-124">Уровень доступа к учетной записи Data Lake Store и файловой системе зависит от уровня доступа пользователя, который вошел в систему.</span><span class="sxs-lookup"><span data-stu-id="166ab-124">The access level to Data Lake Store account and file system is then governed by the access level of the logged in user.</span></span> <span data-ttu-id="166ab-125">Существуют разные способы проверки подлинности в Data Lake Store, включая **проверку подлинности пользователя** и **проверку подлинности с взаимодействием между службами**.</span><span class="sxs-lookup"><span data-stu-id="166ab-125">However, there are other approaches as well to authenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="166ab-126">Инструкции и дополнительные сведения об аутентификации см. в разделах [Аутентификация пользователей](data-lake-store-end-user-authenticate-using-active-directory.md) и [Аутентификация между службами](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="166ab-126">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>


## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="166ab-127">Вход в подписку Azure</span><span class="sxs-lookup"><span data-stu-id="166ab-127">Log in to your Azure subscription</span></span>

1. <span data-ttu-id="166ab-128">Войдите в подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="166ab-128">Log into your Azure subscription.</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="166ab-129">Получите код для использования на следующем шаге.</span><span class="sxs-lookup"><span data-stu-id="166ab-129">You get a code to use in the next step.</span></span> <span data-ttu-id="166ab-130">Откройте в веб-браузере страницу https://aka.ms/devicelogin и введите код для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="166ab-130">Use a web browser to open the page https://aka.ms/devicelogin and enter the code to authenticate.</span></span> <span data-ttu-id="166ab-131">Вам будет предложено выполнить вход с использованием учетных данных.</span><span class="sxs-lookup"><span data-stu-id="166ab-131">You are prompted to log in using your credentials.</span></span>

2. <span data-ttu-id="166ab-132">После входа вы увидите список всех подписок Azure, связанных с вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="166ab-132">Once you log in, the window lists all the Azure subscriptions that are associated with your account.</span></span> <span data-ttu-id="166ab-133">Чтобы выбрать определенную подписку, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="166ab-133">Use the following command to use a specific subscription.</span></span>
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="166ab-134">Создание учетной записи хранения озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="166ab-134">Create an Azure Data Lake Store account</span></span>

1. <span data-ttu-id="166ab-135">Создайте новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="166ab-135">Create a new resource group.</span></span> <span data-ttu-id="166ab-136">В следующей команде укажите значения параметров, которые требуется использовать.</span><span class="sxs-lookup"><span data-stu-id="166ab-136">In the following command, provide the parameter values you want to use.</span></span> <span data-ttu-id="166ab-137">Если имя расположения содержит пробелы, заключите его в кавычки.</span><span class="sxs-lookup"><span data-stu-id="166ab-137">If the location name contains spaces, put it in quotes.</span></span> <span data-ttu-id="166ab-138">Например, "East US 2".</span><span class="sxs-lookup"><span data-stu-id="166ab-138">For example "East US 2".</span></span> 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. <span data-ttu-id="166ab-139">Создайте учетную запись хранилища озера данных.</span><span class="sxs-lookup"><span data-stu-id="166ab-139">Create the Data Lake Store account.</span></span>
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="166ab-140">Создание папок в учетной записи хранения озера данных</span><span class="sxs-lookup"><span data-stu-id="166ab-140">Create folders in a Data Lake Store account</span></span>

<span data-ttu-id="166ab-141">Чтобы хранить данные и управлять ими, вы можете создать папки в своей учетной записи хранилища озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="166ab-141">You can create folders under your Azure Data Lake Store account to manage and store data.</span></span> <span data-ttu-id="166ab-142">Используйте следующую команду, чтобы создать папку с именем **mynewfolder** в корневом каталоге Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="166ab-142">Use the following command to create a folder called **mynewfolder** at the root of the Data Lake Store.</span></span>

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> <span data-ttu-id="166ab-143">Команда создаст папку, используя параметр `--folder`.</span><span class="sxs-lookup"><span data-stu-id="166ab-143">The `--folder` parameter ensures that the command creates a folder.</span></span> <span data-ttu-id="166ab-144">Если этот параметр отсутствует, команда создаст пустой файл с именем mynewfolder в корневом каталоге учетной записи Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="166ab-144">If this parameter is not present, the command creates an empty file called mynewfolder at the root of the Data Lake Store account.</span></span>
> 
>

## <a name="upload-data-to-a-data-lake-store-account"></a><span data-ttu-id="166ab-145">Отправка данных в учетную запись Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="166ab-145">Upload data to a Data Lake Store account</span></span>

<span data-ttu-id="166ab-146">Данные можно передавать в Data Lake Store непосредственно на корневой уровень или в папку, созданную в учетной записи.</span><span class="sxs-lookup"><span data-stu-id="166ab-146">You can upload data to Data Lake Store directly at the root level or to a folder that you created within the account.</span></span> <span data-ttu-id="166ab-147">Фрагменты кода ниже показывают, как передать некоторые примеры данных в папку (**mynewfolder**), которая была создана в предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="166ab-147">The snippets below demonstrate how to upload some sample data to the folder (**mynewfolder**) you created in the previous section.</span></span>

<span data-ttu-id="166ab-148">Если у вас нет под рукой подходящих для этих целей данных, передайте папку **Ambulance Data** из [репозитория Git для озера данных Azure](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="166ab-148">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="166ab-149">Загрузите файл и сохраните его в локальном каталоге на компьютере, например в расположении C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="166ab-149">Download the file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> <span data-ttu-id="166ab-150">Укажите полный путь в качестве назначения, включая имя файла.</span><span class="sxs-lookup"><span data-stu-id="166ab-150">For the destination, you must specify the complete path including the file name.</span></span>
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a><span data-ttu-id="166ab-151">Вывод списка файлов в учетной записи Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="166ab-151">List files in a Data Lake Store account</span></span>

<span data-ttu-id="166ab-152">Чтобы вывести список файлов в учетной записи хранилища озера данных, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="166ab-152">Use the following command to list the files in a Data Lake Store account.</span></span>

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

<span data-ttu-id="166ab-153">Результат этой команды должен выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="166ab-153">The output of this should be similar to the following:</span></span>

    [
        {
            "accessTime": 1491323529542,
            "aclBit": false,
            "blockSize": 268435456,
            "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "length": 1589881,
            "modificationTime": 1491323531638,
            "msExpirationTime": 0,
            "name": "mynewfolder/vehicle1_09142014.csv",
            "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "pathSuffix": "vehicle1_09142014.csv",
            "permission": "770",
            "replication": 1,
            "type": "FILE"
        }
    ]

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a><span data-ttu-id="166ab-154">Переименование, скачивание и удаление данных из Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="166ab-154">Rename, download, and delete data from a Data Lake Store account</span></span> 

* <span data-ttu-id="166ab-155">**Чтобы переименовать файл**, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="166ab-155">**To rename a file**, use the following command:</span></span>
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* <span data-ttu-id="166ab-156">**Чтобы загрузить файл**, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="166ab-156">**To download a file**, use the following command.</span></span> <span data-ttu-id="166ab-157">Убедитесь, что указанный конечный путь уже существует.</span><span class="sxs-lookup"><span data-stu-id="166ab-157">Make sure the destination path you specify already exists.</span></span>
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > <span data-ttu-id="166ab-158">Команда создаст целевую папку, если она не существует.</span><span class="sxs-lookup"><span data-stu-id="166ab-158">The command creates the destination folder if it does not exist.</span></span>
    > 
    >

* <span data-ttu-id="166ab-159">**Чтобы удалить файл**, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="166ab-159">**To delete a file**, use the following command:</span></span>
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    <span data-ttu-id="166ab-160">Если вы хотите удалить папку **mynewfolder** и файл **vehicle1_09142014_copy.csv** с помощью одной команды, используйте параметр --recurse.</span><span class="sxs-lookup"><span data-stu-id="166ab-160">If you want to delete the folder **mynewfolder** and the file **vehicle1_09142014_copy.csv** together in one command, use the --recurse parameter</span></span>

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a><span data-ttu-id="166ab-161">Работа с разрешениями и списками управления доступом для учетной записи Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="166ab-161">Work with permissions and ACLs for a Data Lake Store account</span></span>

<span data-ttu-id="166ab-162">Из этого раздела вы узнаете, как управлять списками управления доступом и разрешениями, с помощью Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="166ab-162">In this section you learn about how to manage ACLs and permissions using Azure CLI 2.0.</span></span> <span data-ttu-id="166ab-163">Подробные сведения о реализации списков ACL в Azure Data Lake Store см. в статье [Контроль доступа в Azure Data Lake Store](data-lake-store-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="166ab-163">For a detailed discussion on how ACLs are implemented in Azure Data Lake Store, see [Access control in Azure Data Lake Store](data-lake-store-access-control.md).</span></span>

* <span data-ttu-id="166ab-164">**Чтобы обновить владельца файла или папки**, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="166ab-164">**To update the owner of a file/folder**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="166ab-165">**Чтобы обновить разрешения для файла или папки**, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="166ab-165">**To update the permissions for a file/folder**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* <span data-ttu-id="166ab-166">**Чтобы получить списки ACL для определенного пути**, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="166ab-166">**To get the ACLs for a given path**, use the following command:</span></span>

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    <span data-ttu-id="166ab-167">Должен быть получен результат, аналогичный приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="166ab-167">The output should be similar to the following:</span></span>

        {
            "entries": [
            "user::rwx",
            "group::rwx",
            "other::---"
          ],
          "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "permission": "770",
          "stickyBit": false
        }

* <span data-ttu-id="166ab-168">**Чтобы создать запись для ACL**, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="166ab-168">**To set an entry for an ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* <span data-ttu-id="166ab-169">**Чтобы удалить запись для ACL**, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="166ab-169">**To remove an entry for an ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="166ab-170">**Чтобы удалить весь стандартный список ACL**, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="166ab-170">**To remove an entire default ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* <span data-ttu-id="166ab-171">**Чтобы удалить весь настраиваемый список ACL**, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="166ab-171">**To remove an entire non-default ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="166ab-172">Удаление учетной записи хранения озера данных</span><span class="sxs-lookup"><span data-stu-id="166ab-172">Delete a Data Lake Store account</span></span>
<span data-ttu-id="166ab-173">Чтобы удалить учетную запись хранилища озера данных, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="166ab-173">Use the following command to delete a Data Lake Store account.</span></span>

```azurecli
az dls account delete --account mydatalakestore
```

<span data-ttu-id="166ab-174">При появлении запроса введите **Y** , чтобы удалить учетную запись.</span><span class="sxs-lookup"><span data-stu-id="166ab-174">When prompted, enter **Y** to delete the account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="166ab-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="166ab-175">Next steps</span></span>

* [<span data-ttu-id="166ab-176">Справочник по CLI 2.0 Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="166ab-176">Azure Data Lake Store CLI 2.0 reference</span></span>](https://docs.microsoft.com/cli/azure/dls)
* [<span data-ttu-id="166ab-177">Защита данных в Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="166ab-177">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="166ab-178">Использование аналитики озера данных Azure с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="166ab-178">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="166ab-179">Использование Azure HDInsight с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="166ab-179">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
