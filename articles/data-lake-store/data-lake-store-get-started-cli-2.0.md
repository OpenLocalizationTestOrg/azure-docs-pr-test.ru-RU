---
title: "интерфейс tooget aaaUse Azure 2.0 командной строки к выполнению хранилища Озера данных Azure | Документы Microsoft"
description: "Использование командной строки Azure кросс платформенных 2.0 toocreate учетной записи хранилища Озера данных и выполнения основных операций"
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
ms.openlocfilehash: 374dcd6cdbc13ad19f6c65502329986ecae60ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a><span data-ttu-id="8e15e-103">Начало работы с Azure Data Lake Store с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8e15e-103">Get started with Azure Data Lake Store using Azure CLI 2.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8e15e-104">Портал</span><span class="sxs-lookup"><span data-stu-id="8e15e-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="8e15e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8e15e-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="8e15e-106">Пакет SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="8e15e-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="8e15e-107">Пакет SDK для Java</span><span class="sxs-lookup"><span data-stu-id="8e15e-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="8e15e-108">REST API</span><span class="sxs-lookup"><span data-stu-id="8e15e-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="8e15e-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8e15e-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="8e15e-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="8e15e-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="8e15e-111">Python</span><span class="sxs-lookup"><span data-stu-id="8e15e-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="8e15e-112">Узнайте, как toocreate toouse Azure CLI 2.0 Azure Озера данных хранения учетной записи и выполнения основных операций, таких как создание папками, отправка и загрузка файлов данных, удалите учетную запись, и т. д. Дополнительные сведения о хранилище озера данных см. в [обзоре Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8e15e-112">Learn how toouse Azure CLI 2.0 toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="8e15e-113">Hello Azure CLI 2.0 — это новый интерфейс командной строки Azure для управления ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="8e15e-113">hello Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="8e15e-114">Его можно использовать в Windows, Linux и macOS.</span><span class="sxs-lookup"><span data-stu-id="8e15e-114">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="8e15e-115">Дополнительные сведения см. в [обзоре Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8e15e-115">For more information, see [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview).</span></span> <span data-ttu-id="8e15e-116">Вы также можете изучить hello [хранилища Озера данных Azure, CLI 2.0 ссылка](https://docs.microsoft.com/cli/azure/dls) полный список команд и синтаксис.</span><span class="sxs-lookup"><span data-stu-id="8e15e-116">You can also look at hello [Azure Data Lake Store CLI 2.0 reference](https://docs.microsoft.com/cli/azure/dls) for a complete list of commands and syntax.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="8e15e-117">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8e15e-117">Prerequisites</span></span>
<span data-ttu-id="8e15e-118">Прежде чем приступать к этой статье, необходимо иметь следующие hello:</span><span class="sxs-lookup"><span data-stu-id="8e15e-118">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="8e15e-119">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="8e15e-119">**An Azure subscription**.</span></span> <span data-ttu-id="8e15e-120">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8e15e-120">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="8e15e-121">**Azure CLI 2.0** — см. инструкции в статье об [установке Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8e15e-121">**Azure CLI 2.0** - See [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) for instructions.</span></span>

## <a name="authentication"></a><span data-ttu-id="8e15e-122">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="8e15e-122">Authentication</span></span>

<span data-ttu-id="8e15e-123">В этой статье используется более простой подход к проверке подлинности в службе Data Lake Store, в которую выполняется вход от имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="8e15e-123">This article uses a simpler authentication approach with Data Lake Store where you log in as an end-user user.</span></span> <span data-ttu-id="8e15e-124">Hello доступ уровня хранилища Озера tooData учетной записи и файловая система распространяется уровень доступа hello приветствия вошедшего пользователя.</span><span class="sxs-lookup"><span data-stu-id="8e15e-124">hello access level tooData Lake Store account and file system is then governed by hello access level of hello logged in user.</span></span> <span data-ttu-id="8e15e-125">Однако существуют другие методы как хорошо tooauthenticate с хранилища Озера данных, которые являются **проверки подлинности для конечных пользователей** или **проверки подлинности службы для службы**.</span><span class="sxs-lookup"><span data-stu-id="8e15e-125">However, there are other approaches as well tooauthenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="8e15e-126">Инструкции и Дополнительные сведения о том, как tooauthenticate, в разделе [проверки подлинности для конечных пользователей](data-lake-store-end-user-authenticate-using-active-directory.md) или [проверки подлинности службы для службы](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="8e15e-126">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>


## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="8e15e-127">Войдите в tooyour подписки Azure</span><span class="sxs-lookup"><span data-stu-id="8e15e-127">Log in tooyour Azure subscription</span></span>

1. <span data-ttu-id="8e15e-128">Войдите в подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="8e15e-128">Log into your Azure subscription.</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="8e15e-129">В следующем шаге hello получить toouse кода.</span><span class="sxs-lookup"><span data-stu-id="8e15e-129">You get a code toouse in hello next step.</span></span> <span data-ttu-id="8e15e-130">Используйте страницу https://aka.ms/devicelogin hello tooopen веб браузера и введите tooauthenticate кода hello.</span><span class="sxs-lookup"><span data-stu-id="8e15e-130">Use a web browser tooopen hello page https://aka.ms/devicelogin and enter hello code tooauthenticate.</span></span> <span data-ttu-id="8e15e-131">Все запрашиваемые toolog, используя свои учетные данные.</span><span class="sxs-lookup"><span data-stu-id="8e15e-131">You are prompted toolog in using your credentials.</span></span>

2. <span data-ttu-id="8e15e-132">После входа список окна hello всех hello подписки Azure, которые связаны с вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="8e15e-132">Once you log in, hello window lists all hello Azure subscriptions that are associated with your account.</span></span> <span data-ttu-id="8e15e-133">Используйте hello, следующая команда toouse конкретной подписки.</span><span class="sxs-lookup"><span data-stu-id="8e15e-133">Use hello following command toouse a specific subscription.</span></span>
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="8e15e-134">Создание учетной записи хранения озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="8e15e-134">Create an Azure Data Lake Store account</span></span>

1. <span data-ttu-id="8e15e-135">Создайте новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8e15e-135">Create a new resource group.</span></span> <span data-ttu-id="8e15e-136">В hello следующую команду предоставляют значения параметров, которые вы хотите toouse hello.</span><span class="sxs-lookup"><span data-stu-id="8e15e-136">In hello following command, provide hello parameter values you want toouse.</span></span> <span data-ttu-id="8e15e-137">Если имя расположения hello содержит пробелы, необходимо поместите его в кавычки.</span><span class="sxs-lookup"><span data-stu-id="8e15e-137">If hello location name contains spaces, put it in quotes.</span></span> <span data-ttu-id="8e15e-138">Например, "East US 2".</span><span class="sxs-lookup"><span data-stu-id="8e15e-138">For example "East US 2".</span></span> 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. <span data-ttu-id="8e15e-139">Создайте учетную запись хранилища Озера данных hello.</span><span class="sxs-lookup"><span data-stu-id="8e15e-139">Create hello Data Lake Store account.</span></span>
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="8e15e-140">Создание папок в учетной записи хранения озера данных</span><span class="sxs-lookup"><span data-stu-id="8e15e-140">Create folders in a Data Lake Store account</span></span>

<span data-ttu-id="8e15e-141">Можно создать папки под вашей toomanage учетной записи хранилища Озера данных Azure и хранения данных.</span><span class="sxs-lookup"><span data-stu-id="8e15e-141">You can create folders under your Azure Data Lake Store account toomanage and store data.</span></span> <span data-ttu-id="8e15e-142">Следующая команда toocreate папка hello используйте **mynewfolder** hello корню hello хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="8e15e-142">Use hello following command toocreate a folder called **mynewfolder** at hello root of hello Data Lake Store.</span></span>

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> <span data-ttu-id="8e15e-143">Hello `--folder` параметр гарантирует, что команда hello создает папку.</span><span class="sxs-lookup"><span data-stu-id="8e15e-143">hello `--folder` parameter ensures that hello command creates a folder.</span></span> <span data-ttu-id="8e15e-144">Если этот параметр не указан, команда hello создает пустой файл с именем mynewfolder в корне hello hello хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="8e15e-144">If this parameter is not present, hello command creates an empty file called mynewfolder at hello root of hello Data Lake Store account.</span></span>
> 
>

## <a name="upload-data-tooa-data-lake-store-account"></a><span data-ttu-id="8e15e-145">Отправка учетной записи хранилища Озера данных tooa данных</span><span class="sxs-lookup"><span data-stu-id="8e15e-145">Upload data tooa Data Lake Store account</span></span>

<span data-ttu-id="8e15e-146">Можно передать хранилища Озера данных tooData непосредственно на hello корневого уровня или tooa папку, созданную в пределах учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="8e15e-146">You can upload data tooData Lake Store directly at hello root level or tooa folder that you created within hello account.</span></span> <span data-ttu-id="8e15e-147">фрагменты кода Hello ниже показано, как tooupload некоторые папку с образцами данных toohello (**mynewfolder**) был создан в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="8e15e-147">hello snippets below demonstrate how tooupload some sample data toohello folder (**mynewfolder**) you created in hello previous section.</span></span>

<span data-ttu-id="8e15e-148">Если вы ищете некоторые tooupload образец данных, вы можете получить hello **скорая помощь данных** папку из hello [репозитории Озера данных Azure](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="8e15e-148">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="8e15e-149">Загрузите файл hello и сохранить его в локальный каталог на компьютере, например C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="8e15e-149">Download hello file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> <span data-ttu-id="8e15e-150">Для назначения hello необходимо указать hello полный путь, включая имя файла hello.</span><span class="sxs-lookup"><span data-stu-id="8e15e-150">For hello destination, you must specify hello complete path including hello file name.</span></span>
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a><span data-ttu-id="8e15e-151">Вывод списка файлов в учетной записи Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="8e15e-151">List files in a Data Lake Store account</span></span>

<span data-ttu-id="8e15e-152">Используйте следующие команды toolist hello файлы в учетную запись хранилища Озера данных hello.</span><span class="sxs-lookup"><span data-stu-id="8e15e-152">Use hello following command toolist hello files in a Data Lake Store account.</span></span>

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

<span data-ttu-id="8e15e-153">выходные данные Hello объекта должны быть примерно следующее toohello:</span><span class="sxs-lookup"><span data-stu-id="8e15e-153">hello output of this should be similar toohello following:</span></span>

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

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a><span data-ttu-id="8e15e-154">Переименование, скачивание и удаление данных из Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="8e15e-154">Rename, download, and delete data from a Data Lake Store account</span></span> 

* <span data-ttu-id="8e15e-155">**файл toorename**, использовать hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8e15e-155">**toorename a file**, use hello following command:</span></span>
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* <span data-ttu-id="8e15e-156">**файл toodownload**, используйте следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="8e15e-156">**toodownload a file**, use hello following command.</span></span> <span data-ttu-id="8e15e-157">Убедитесь, что путь hello назначения уже существует.</span><span class="sxs-lookup"><span data-stu-id="8e15e-157">Make sure hello destination path you specify already exists.</span></span>
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > <span data-ttu-id="8e15e-158">Hello команда создает папку назначения hello, если он не существует.</span><span class="sxs-lookup"><span data-stu-id="8e15e-158">hello command creates hello destination folder if it does not exist.</span></span>
    > 
    >

* <span data-ttu-id="8e15e-159">**файл toodelete**, использовать hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8e15e-159">**toodelete a file**, use hello following command:</span></span>
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    <span data-ttu-id="8e15e-160">Папка hello toodelete **mynewfolder** и файл hello **vehicle1_09142014_copy.csv** вместе в одной команде, используйте hello--recurse параметра</span><span class="sxs-lookup"><span data-stu-id="8e15e-160">If you want toodelete hello folder **mynewfolder** and hello file **vehicle1_09142014_copy.csv** together in one command, use hello --recurse parameter</span></span>

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a><span data-ttu-id="8e15e-161">Работа с разрешениями и списками управления доступом для учетной записи Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="8e15e-161">Work with permissions and ACLs for a Data Lake Store account</span></span>

<span data-ttu-id="8e15e-162">В этом разделе вы узнаете о том, как toomanage списки управления доступом и разрешения с помощью Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="8e15e-162">In this section you learn about how toomanage ACLs and permissions using Azure CLI 2.0.</span></span> <span data-ttu-id="8e15e-163">Подробные сведения о реализации списков ACL в Azure Data Lake Store см. в статье [Контроль доступа в Azure Data Lake Store](data-lake-store-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="8e15e-163">For a detailed discussion on how ACLs are implemented in Azure Data Lake Store, see [Access control in Azure Data Lake Store](data-lake-store-access-control.md).</span></span>

* <span data-ttu-id="8e15e-164">**tooupdate hello владельца файла или папки**, использовать hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8e15e-164">**tooupdate hello owner of a file/folder**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="8e15e-165">**tooupdate hello разрешения для файла или папки**, использовать hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8e15e-165">**tooupdate hello permissions for a file/folder**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* <span data-ttu-id="8e15e-166">**hello tooget ACL для определенного пути**, использовать hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8e15e-166">**tooget hello ACLs for a given path**, use hello following command:</span></span>

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    <span data-ttu-id="8e15e-167">Hello выходные данные должны быть примерно toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="8e15e-167">hello output should be similar toohello following:</span></span>

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

* <span data-ttu-id="8e15e-168">**tooset запись ACL**, использовать hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8e15e-168">**tooset an entry for an ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* <span data-ttu-id="8e15e-169">**tooremove запись ACL**, использовать hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8e15e-169">**tooremove an entry for an ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="8e15e-170">**весь список управления Доступом по умолчанию tooremove**, использовать hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8e15e-170">**tooremove an entire default ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* <span data-ttu-id="8e15e-171">**tooremove всей нестандартных ACL**, использовать hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8e15e-171">**tooremove an entire non-default ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="8e15e-172">Удаление учетной записи хранения озера данных</span><span class="sxs-lookup"><span data-stu-id="8e15e-172">Delete a Data Lake Store account</span></span>
<span data-ttu-id="8e15e-173">Используйте следующие команды toodelete учетной записи хранилища Озера данных hello.</span><span class="sxs-lookup"><span data-stu-id="8e15e-173">Use hello following command toodelete a Data Lake Store account.</span></span>

```azurecli
az dls account delete --account mydatalakestore
```

<span data-ttu-id="8e15e-174">При появлении запроса введите **Y** учетной записи toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="8e15e-174">When prompted, enter **Y** toodelete hello account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e15e-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8e15e-175">Next steps</span></span>

* [<span data-ttu-id="8e15e-176">Справочник по CLI 2.0 Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="8e15e-176">Azure Data Lake Store CLI 2.0 reference</span></span>](https://docs.microsoft.com/cli/azure/dls)
* [<span data-ttu-id="8e15e-177">Защита данных в Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="8e15e-177">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="8e15e-178">Использование аналитики озера данных Azure с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="8e15e-178">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="8e15e-179">Использование Azure HDInsight с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="8e15e-179">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
