---
title: "Начало работы с Azure Data Lake Store с помощью PowerShell | Документация Майкрософт"
description: "Использование Azure PowerShell для создания учетной записи хранения озера данных и выполнения базовых операций"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf85f369-f9aa-4ca1-9ae7-e03a78eb7290
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 23c9aaa089251bff5132652475f4daadc2c128fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a><span data-ttu-id="55a16-103">Начало работы с хранилищем озера данных Azure с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="55a16-103">Get started with Azure Data Lake Store using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="55a16-104">Портал</span><span class="sxs-lookup"><span data-stu-id="55a16-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="55a16-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="55a16-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="55a16-106">Пакет SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="55a16-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="55a16-107">Пакет SDK для Java</span><span class="sxs-lookup"><span data-stu-id="55a16-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="55a16-108">REST API</span><span class="sxs-lookup"><span data-stu-id="55a16-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="55a16-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="55a16-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="55a16-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="55a16-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="55a16-111">Python</span><span class="sxs-lookup"><span data-stu-id="55a16-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="55a16-112">Узнайте, как с помощью Azure PowerShell создать учетную запись хранения озера данных Azure и выполнять базовые операции, такие как создание папок, передача и загрузка файлов данных, удаление учетной записи и т. д. Дополнительные сведения о хранилище озера данных см. в [обзоре Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="55a16-112">Learn how to use Azure PowerShell to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55a16-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="55a16-113">Prerequisites</span></span>
<span data-ttu-id="55a16-114">Перед началом работы с этим учебником необходимо иметь следующее:</span><span class="sxs-lookup"><span data-stu-id="55a16-114">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="55a16-115">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="55a16-115">**An Azure subscription**.</span></span> <span data-ttu-id="55a16-116">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="55a16-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="55a16-117">**Azure PowerShell 1.0 или более поздней версии**.</span><span class="sxs-lookup"><span data-stu-id="55a16-117">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="55a16-118">См. статью [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="55a16-118">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="authentication"></a><span data-ttu-id="55a16-119">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="55a16-119">Authentication</span></span>
<span data-ttu-id="55a16-120">В этой статье используется более простой подход к проверке подлинности в Data Lake Store, при котором нужно ввести учетные данные учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="55a16-120">This article uses a simpler authentication approach with Data Lake Store where you are prompted to enter your Azure account credentials.</span></span> <span data-ttu-id="55a16-121">Уровень доступа к учетной записи Data Lake Store и файловой системе зависит от уровня доступа пользователя, который вошел в систему.</span><span class="sxs-lookup"><span data-stu-id="55a16-121">The access level to Data Lake Store account and file system is then governed by the access level of the logged in user.</span></span> <span data-ttu-id="55a16-122">Существуют разные способы проверки подлинности в Data Lake Store, включая **проверку подлинности пользователя** и **проверку подлинности с взаимодействием между службами**.</span><span class="sxs-lookup"><span data-stu-id="55a16-122">However, there are other approaches as well to authenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="55a16-123">Инструкции и дополнительные сведения об аутентификации см. в разделах [Аутентификация пользователей](data-lake-store-end-user-authenticate-using-active-directory.md) и [Аутентификация между службами](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="55a16-123">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="55a16-124">Создание учетной записи хранения озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="55a16-124">Create an Azure Data Lake Store account</span></span>
1. <span data-ttu-id="55a16-125">На рабочем столе откройте новое окно Windows PowerShell и выполните следующий фрагмент кода, чтобы войти в свою учетную запись Azure, выбрать подписку и зарегистрировать поставщик Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="55a16-125">From your desktop, open a new Windows PowerShell window, and enter the following snippet to log in to your Azure account, set the subscription, and register the Data Lake Store provider.</span></span> <span data-ttu-id="55a16-126">Когда вам будет предложено войти, введите учетные данные администратора или владельца подписки.</span><span class="sxs-lookup"><span data-stu-id="55a16-126">When prompted to log in, make sure you log in as one of the subscription admininistrators/owner:</span></span>

        # Log in to your Azure account
        Login-AzureRmAccount

        # List all the subscriptions associated to your account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. <span data-ttu-id="55a16-127">Учетная запись хранения озера данных Azure связывается с группой ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="55a16-127">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="55a16-128">Для начала создайте группу ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="55a16-128">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="55a16-129">![Создание группы ресурсов Azure](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Создание группы ресурсов Azure")</span><span class="sxs-lookup"><span data-stu-id="55a16-129">![Create an Azure Resource Group](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")</span></span>
3. <span data-ttu-id="55a16-130">Создайте учетную запись хранения озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="55a16-130">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="55a16-131">Указанное имя должно содержать только строчные буквы и цифры.</span><span class="sxs-lookup"><span data-stu-id="55a16-131">The name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="55a16-132">![Создание учетной записи Azure Data Lake Store](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Создание учетной записи Azure Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="55a16-132">![Create an Azure Data Lake Store account](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake Store account")</span></span>
4. <span data-ttu-id="55a16-133">Убедитесь, что учетная запись создана.</span><span class="sxs-lookup"><span data-stu-id="55a16-133">Verify that the account is successfully created.</span></span>

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    <span data-ttu-id="55a16-134">Результат должен иметь значение **True**.</span><span class="sxs-lookup"><span data-stu-id="55a16-134">The output for this should be **True**.</span></span>

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a><span data-ttu-id="55a16-135">Создание структуры каталогов в хранилище озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="55a16-135">Create directory structures in your Azure Data Lake Store</span></span>
<span data-ttu-id="55a16-136">Чтобы хранить данные и управлять ими, вы можете создать папки в своей учетной записи хранения озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="55a16-136">You can create directories under your Azure Data Lake Store account to manage and store data.</span></span>

1. <span data-ttu-id="55a16-137">Укажите корневой каталог.</span><span class="sxs-lookup"><span data-stu-id="55a16-137">Specify a root directory.</span></span>

        $myrootdir = "/"
2. <span data-ttu-id="55a16-138">Создайте новый каталог с именем **mynewdirectory** в указанном корневом каталоге.</span><span class="sxs-lookup"><span data-stu-id="55a16-138">Create a new directory called **mynewdirectory** under the specified root.</span></span>

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. <span data-ttu-id="55a16-139">Убедитесь, что новый каталог создан.</span><span class="sxs-lookup"><span data-stu-id="55a16-139">Verify that the new directory is successfully created.</span></span>

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    <span data-ttu-id="55a16-140">Вы должны увидеть примерно следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="55a16-140">It should show an output like the following:</span></span>

    <span data-ttu-id="55a16-141">![Проверка каталога](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Проверка каталога")</span><span class="sxs-lookup"><span data-stu-id="55a16-141">![Verify Directory](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verify Directory")</span></span>

## <a name="upload-data-to-your-azure-data-lake-store"></a><span data-ttu-id="55a16-142">Передача данных в хранилище озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="55a16-142">Upload data to your Azure Data Lake Store</span></span>
<span data-ttu-id="55a16-143">Данные можно передавать в хранилище озера данных Azure непосредственно на корневой уровень или в каталог, созданный в учетной записи.</span><span class="sxs-lookup"><span data-stu-id="55a16-143">You can upload your data to Data Lake Store directly at the root level or to a directory that you created within the account.</span></span> <span data-ttu-id="55a16-144">Фрагменты кода ниже показывают, как отправить некоторые образцы данных в каталог (**mynewdirectory**), который был создан в предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="55a16-144">The snippets below demonstrate how to upload some sample data to the directory (**mynewdirectory**) you created in the previous section.</span></span>

<span data-ttu-id="55a16-145">Если у вас нет под рукой подходящих для этих целей данных, передайте папку **Ambulance Data** из [репозитория Git для озера данных Azure](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="55a16-145">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="55a16-146">Загрузите файл и сохраните его в локальном каталоге на компьютере, например в расположении C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="55a16-146">Download the file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a><span data-ttu-id="55a16-147">Переименование, загрузка и удаление данных из хранилища озера данных</span><span class="sxs-lookup"><span data-stu-id="55a16-147">Rename, download, and delete data from your Data Lake Store</span></span>
<span data-ttu-id="55a16-148">Чтобы переименовать файл, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="55a16-148">To rename a file, use the following command:</span></span>

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="55a16-149">Чтобы загрузить файл, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="55a16-149">To download a file, use the following command:</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

<span data-ttu-id="55a16-150">Чтобы удалить файл, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="55a16-150">To delete a file, use the following command:</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="55a16-151">При появлении запроса введите **Y** , чтобы удалить элемент.</span><span class="sxs-lookup"><span data-stu-id="55a16-151">When prompted, enter **Y** to delete the item.</span></span> <span data-ttu-id="55a16-152">Если нужно удалить несколько файлов, можно указать все пути через запятую.</span><span class="sxs-lookup"><span data-stu-id="55a16-152">If you have more than one file to delete, you can provide all the paths separated by comma.</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a><span data-ttu-id="55a16-153">Удаление учетной записи хранения озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="55a16-153">Delete your Azure Data Lake Store account</span></span>
<span data-ttu-id="55a16-154">Чтобы удалить свою учетную запись хранения озера данных, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="55a16-154">Use the following command to delete your Data Lake Store account.</span></span>

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

<span data-ttu-id="55a16-155">При появлении запроса введите **Y** , чтобы удалить учетную запись.</span><span class="sxs-lookup"><span data-stu-id="55a16-155">When prompted, enter **Y** to delete the account.</span></span>

## <a name="performance-guidance-while-using-powershell"></a><span data-ttu-id="55a16-156">Рекомендации по производительности при использовании PowerShell</span><span class="sxs-lookup"><span data-stu-id="55a16-156">Performance guidance while using PowerShell</span></span>

<span data-ttu-id="55a16-157">Ниже приведены самые важные параметры, настроив которые можно обеспечить высокую производительность при использовании PowerShell для работы с Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="55a16-157">Below are the most important settings that can be tuned to get the best performance while using PowerShell to work with Data Lake Store:</span></span>

| <span data-ttu-id="55a16-158">Свойство</span><span class="sxs-lookup"><span data-stu-id="55a16-158">Property</span></span>            | <span data-ttu-id="55a16-159">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="55a16-159">Default</span></span> | <span data-ttu-id="55a16-160">Описание</span><span class="sxs-lookup"><span data-stu-id="55a16-160">Description</span></span> |
|---------------------|---------|-------------|
| <span data-ttu-id="55a16-161">PerFileThreadCount</span><span class="sxs-lookup"><span data-stu-id="55a16-161">PerFileThreadCount</span></span>  | <span data-ttu-id="55a16-162">10</span><span class="sxs-lookup"><span data-stu-id="55a16-162">10</span></span>      | <span data-ttu-id="55a16-163">Этот параметр позволяет выбрать количество параллельных потоков для отправки или скачивания каждого файла.</span><span class="sxs-lookup"><span data-stu-id="55a16-163">This parameter enables you to choose the number of parallel threads for uploading or downloading each file.</span></span> <span data-ttu-id="55a16-164">Это количество представляет собой максимальное количество потоков, которые можно выделить для каждого файла. В зависимости от сценария количество потоков может быть меньше (например, при отправке файла размером 1 КБ вы получите один поток, даже если запросите 20).</span><span class="sxs-lookup"><span data-stu-id="55a16-164">This number represents the max threads that can be allocated per file, but you may get less threads depending on your scenario (e.g. if you are uploading a 1KB file, you will get one thread even if you ask for 20 threads).</span></span>  |
| <span data-ttu-id="55a16-165">ConcurrentFileCount</span><span class="sxs-lookup"><span data-stu-id="55a16-165">ConcurrentFileCount</span></span> | <span data-ttu-id="55a16-166">10</span><span class="sxs-lookup"><span data-stu-id="55a16-166">10</span></span>      | <span data-ttu-id="55a16-167">Этот параметр предназначен для отправки или скачивания папок.</span><span class="sxs-lookup"><span data-stu-id="55a16-167">This parameter is specifically for uploading or downloading folders.</span></span> <span data-ttu-id="55a16-168">Он определяет количество одновременно отправляемых или скачиваемых файлов.</span><span class="sxs-lookup"><span data-stu-id="55a16-168">This parameter determines the number of concurrent files that can be uploaded or downloaded.</span></span> <span data-ttu-id="55a16-169">Это количество представляет собой максимальное количество файлов, которые можно отправить или скачать одновременно. В зависимости от сценария количество параллельно отправляемых или скачиваемых файлов может быть меньше (например, при отправке двух файлов одновременно будут отправляться два файла, даже если запрошено 15).</span><span class="sxs-lookup"><span data-stu-id="55a16-169">This number represents the maximum number of concurrent files that can be uploaded or downloaded at one time, but you may get less concurrency depending on your scenario (e.g. if you are uploading two files, you will get two concurrent file uploads even if you ask for 15).</span></span> |

<span data-ttu-id="55a16-170">**Пример**</span><span class="sxs-lookup"><span data-stu-id="55a16-170">**Example**</span></span>

<span data-ttu-id="55a16-171">Эта команда скачивает файлы из Azure Data Lake Store на локальный диск пользователя, используя 20 потоков на один файл и 100 одновременно скачиваемых файлов.</span><span class="sxs-lookup"><span data-stu-id="55a16-171">This command downloads files from Azure Data Lake Store to the user's local drive using 20 threads per file and 100 concurrent files.</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

### <a name="how-do-i-determine-the-value-to-set-for-these-parameters"></a><span data-ttu-id="55a16-172">Как определить значение для этих параметров?</span><span class="sxs-lookup"><span data-stu-id="55a16-172">How do I determine the value to set for these parameters?</span></span>

<span data-ttu-id="55a16-173">Ниже представлены некоторые полезные рекомендации.</span><span class="sxs-lookup"><span data-stu-id="55a16-173">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="55a16-174">**Шаг 1. Определение общего числа потоков.** Сначала нужно определить общее число потоков, которые следует использовать.</span><span class="sxs-lookup"><span data-stu-id="55a16-174">**Step 1: Determine the total thread count** - You should start by calculating the total thread count to use.</span></span> <span data-ttu-id="55a16-175">Как правило, следует использовать 6 потоков для каждого физического ядра.</span><span class="sxs-lookup"><span data-stu-id="55a16-175">As a general guideline, you should use 6 threads for each physical core.</span></span>

        Total thread count = total physical cores * 6

    <span data-ttu-id="55a16-176">**Пример**</span><span class="sxs-lookup"><span data-stu-id="55a16-176">**Example**</span></span>

    <span data-ttu-id="55a16-177">Предположим, что вы выполняете команды PowerShell на виртуальной машине D14 с 16 ядрами.</span><span class="sxs-lookup"><span data-stu-id="55a16-177">Assuming you are running the PowerShell commands from a D14 VM that has 16 cores</span></span>

        Total thread count = 16 cores * 6 = 96 threads


* <span data-ttu-id="55a16-178">**Шаг 2. Расчет значения параметра PerFileThreadCount.** Мы вычисляем значение параметра PerFileThreadCount на основе размера файлов.</span><span class="sxs-lookup"><span data-stu-id="55a16-178">**Step 2: Calculate PerFileThreadCount**  - We calculate our PerFileThreadCount based on the size of the files.</span></span> <span data-ttu-id="55a16-179">Для файлов размером менее 2,5 ГБ не нужно изменять этот параметр, так как значения по умолчанию 10 будет достаточно.</span><span class="sxs-lookup"><span data-stu-id="55a16-179">For files smaller than 2.5GB, there is no need to change this parameter because the default of 10 is sufficient.</span></span> <span data-ttu-id="55a16-180">Для файлов размером более 2,5 ГБ следует использовать 10 потоков для первых 2,5 ГБ и добавлять по 1 потоку на каждые дополнительные 256 МБ файла.</span><span class="sxs-lookup"><span data-stu-id="55a16-180">For files larger than 2.5GB, you should use 10 threads as the base for the first 2.5GB and add 1 thread for each additional 256MB increase in file size.</span></span> <span data-ttu-id="55a16-181">При копировании папки с файлами разного размера рекомендуется разделить их на группы по схожим размерам.</span><span class="sxs-lookup"><span data-stu-id="55a16-181">If you are copying a folder with a large range of file sizes, consider grouping them into similar file sizes.</span></span> <span data-ttu-id="55a16-182">Использование файлов разных размеров может привести к снижению производительности.</span><span class="sxs-lookup"><span data-stu-id="55a16-182">Having dissimilar file sizes may cause non-optimal performance.</span></span> <span data-ttu-id="55a16-183">Если невозможно сгруппировать файлы по схожим размерам, следует задать значение параметра PerFileThreadCount в соответствии с максимальным размером файла.</span><span class="sxs-lookup"><span data-stu-id="55a16-183">If that's not possible to group similar file sizes, you should set PerFileThreadCount based on the largest file size.</span></span>

        PerFileThreadCount = 10 threads for the first 2.5GB + 1 thread for each additional 256MB increase in file size

    <span data-ttu-id="55a16-184">**Пример**</span><span class="sxs-lookup"><span data-stu-id="55a16-184">**Example**</span></span>

    <span data-ttu-id="55a16-185">Предположим, что у вас есть 100 файлов от 1 до 10 ГБ. Мы используем файл на 10 ГБ в качестве максимального размера файла в формуле, подобной следующей.</span><span class="sxs-lookup"><span data-stu-id="55a16-185">Assuming you have 100 files ranging from 1GB to 10GB, we use the 10GB as the largest file size for equation, which would read like the following.</span></span>

        PerFileThreadCount = 10 + ((10GB - 2.5GB) / 256MB) = 40 threads

* <span data-ttu-id="55a16-186">**Шаг 3. Вычисление значения параметра ConcurrentFilecount.** Используйте общее число потоков и значение параметра PerFileThreadCount, чтобы вычислить значение параметра ConcurrentFileCount по следующей формуле.</span><span class="sxs-lookup"><span data-stu-id="55a16-186">**Step 3: Calculate ConcurrentFilecount** - Use the total thread count and PerFileThreadCount to calculate ConcurrentFileCount based on the following equation.</span></span>

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    <span data-ttu-id="55a16-187">**Пример**</span><span class="sxs-lookup"><span data-stu-id="55a16-187">**Example**</span></span>

    <span data-ttu-id="55a16-188">На основе использованных примеров значений.</span><span class="sxs-lookup"><span data-stu-id="55a16-188">Based on the example values we have been using</span></span>

        96 = 40 * ConcurrentFileCount

    <span data-ttu-id="55a16-189">Таким образом значение **ConcurrentFileCount** — **2,4**, которое можно округлить до **2**.</span><span class="sxs-lookup"><span data-stu-id="55a16-189">So, **ConcurrentFileCount** is **2.4**, which we can round off to **2**.</span></span>

### <a name="further-tuning"></a><span data-ttu-id="55a16-190">Дополнительные настройки</span><span class="sxs-lookup"><span data-stu-id="55a16-190">Further tuning</span></span>

<span data-ttu-id="55a16-191">Вам могут потребоваться дополнительные настройки, так как вы работаете с файлами разного размера.</span><span class="sxs-lookup"><span data-stu-id="55a16-191">You might require further tuning because there is a range of file sizes to work with.</span></span> <span data-ttu-id="55a16-192">Вычисления выше подходят, если размер всех или большинства файлов больше 10 ГБ или ближе к этому показателю.</span><span class="sxs-lookup"><span data-stu-id="55a16-192">The above calculation works well if all or most of the files are larger and closer to the 10GB range.</span></span> <span data-ttu-id="55a16-193">Однако если у вас есть множество файлов разных размеров (меньше 10 ГБ), можно уменьшить значение параметра PerFileThreadCount.</span><span class="sxs-lookup"><span data-stu-id="55a16-193">If instead, there are many different files sizes with many files being smaller, then you could reduce PerFileThreadCount.</span></span> <span data-ttu-id="55a16-194">Сделав так, мы увеличим значение ConcurrentFileCount.</span><span class="sxs-lookup"><span data-stu-id="55a16-194">By reducing the PerFileThreadCount, we can increase ConcurrentFileCount.</span></span> <span data-ttu-id="55a16-195">Таким образом, если предположить, что большая часть файлов меньше 5 ГБ, можно повторно выполнить вычисления:</span><span class="sxs-lookup"><span data-stu-id="55a16-195">So, if we assume that most of our files are smaller in the 5GB range, we can re-do our calculation:</span></span>

    PerFileThreadCount = 10 + ((5GB - 2.5GB) / 256MB) = 20

<span data-ttu-id="55a16-196">Теперь **ConcurrentFileCount** имеет значение 96/20 — 4,8, которое можно округлить до **4**.</span><span class="sxs-lookup"><span data-stu-id="55a16-196">So, **ConcurrentFileCount** will now be 96/20, which is 4.8, rounded off to **4**.</span></span>

<span data-ttu-id="55a16-197">Вы можете продолжить изменять значения этих параметров, уменьшая и увеличивая значение **PerFileThreadCount** в зависимости от размера файлов.</span><span class="sxs-lookup"><span data-stu-id="55a16-197">You can continue to tune these settings by changing the **PerFileThreadCount** up and down depending on the distribution of your file sizes.</span></span>

### <a name="limitation"></a><span data-ttu-id="55a16-198">Ограничение</span><span class="sxs-lookup"><span data-stu-id="55a16-198">Limitation</span></span>

* <span data-ttu-id="55a16-199">**Число файлов меньше, чем значение ConcurrentFileCount.** Если количество отправляемых файлов меньше вычисленного значения **ConcurrentFileCount**, следует уменьшить значение **ConcurrentFileCount** в соответствии с числом файлов.</span><span class="sxs-lookup"><span data-stu-id="55a16-199">**Number of files is less than ConcurrentFileCount**: If the number of files you are uploading is smaller than the **ConcurrentFileCount** that you calculated, then you should reduce **ConcurrentFileCount** to be equal to the number of files.</span></span> <span data-ttu-id="55a16-200">Все остальные потоки можно использовать для увеличения значения **PerFileThreadCount**.</span><span class="sxs-lookup"><span data-stu-id="55a16-200">You can use any remaining threads to increase **PerFileThreadCount**.</span></span>

* <span data-ttu-id="55a16-201">**Слишком много потоков.** Указав слишком большое число потоков, не увеличивая размер кластера, вы рискуете снизить производительность.</span><span class="sxs-lookup"><span data-stu-id="55a16-201">**Too many threads**: If you increase thread count too much without increasing your cluster size, you run the risk of degraded performance.</span></span> <span data-ttu-id="55a16-202">При переключении контекста в ЦП могут возникнуть конфликты.</span><span class="sxs-lookup"><span data-stu-id="55a16-202">There can be contention issues when context-switching on the CPU.</span></span>

* <span data-ttu-id="55a16-203">**Недостаточный уровень параллелизма.** Если уровень параллелизма недостаточный, кластер может быть слишком мал.</span><span class="sxs-lookup"><span data-stu-id="55a16-203">**Insufficient concurrency**: If the concurrency is not sufficient, then your cluster may be too small.</span></span> <span data-ttu-id="55a16-204">Вы можете увеличить количество узлов в кластере, что повысит уровень параллелизма.</span><span class="sxs-lookup"><span data-stu-id="55a16-204">You can increase the number of nodes in your cluster which will give you more concurrency.</span></span>

* <span data-ttu-id="55a16-205">**Ошибки регулирования.** При слишком высоком уровне параллелизма могут возникнуть ошибки регулирования.</span><span class="sxs-lookup"><span data-stu-id="55a16-205">**Throttling errors**: You may see throttling errors if your concurrency is too high.</span></span> <span data-ttu-id="55a16-206">При этом необходимо уменьшить уровень параллелизма или обратиться к нам.</span><span class="sxs-lookup"><span data-stu-id="55a16-206">If you are seeing throttling errors, you should either reduce the concurrency or contact us.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55a16-207">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="55a16-207">Next steps</span></span>
* [<span data-ttu-id="55a16-208">Защита данных в хранилище озера данных</span><span class="sxs-lookup"><span data-stu-id="55a16-208">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="55a16-209">Использование аналитики озера данных Azure с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="55a16-209">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="55a16-210">Использование Azure HDInsight с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="55a16-210">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

