---
title: "aaaUse PowerShell tooget к выполнению хранилища Озера данных Azure | Документы Microsoft"
description: "Использование Azure PowerShell toocreate учетной записи хранилища Озера данных и выполнения основных операций"
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
ms.openlocfilehash: 9c958bfd63e412ec0b0a4113a149f61aee026bc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a><span data-ttu-id="9e839-103">Начало работы с хранилищем озера данных Azure с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e839-103">Get started with Azure Data Lake Store using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9e839-104">Портал</span><span class="sxs-lookup"><span data-stu-id="9e839-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="9e839-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e839-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="9e839-106">Пакет SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="9e839-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="9e839-107">Пакет SDK для Java</span><span class="sxs-lookup"><span data-stu-id="9e839-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="9e839-108">REST API</span><span class="sxs-lookup"><span data-stu-id="9e839-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="9e839-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9e839-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="9e839-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="9e839-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="9e839-111">Python</span><span class="sxs-lookup"><span data-stu-id="9e839-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="9e839-112">Узнайте, как toocreate toouse Azure PowerShell Azure Озера данных хранения учетной записи и выполнения основных операций, таких как создание папками, отправка и загрузка файлов данных, удалите учетную запись, и т. д. Дополнительные сведения о хранилище озера данных см. в [обзоре Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9e839-112">Learn how toouse Azure PowerShell toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e839-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9e839-113">Prerequisites</span></span>
<span data-ttu-id="9e839-114">Прежде чем начать работу с учебником, необходимо иметь следующие hello.</span><span class="sxs-lookup"><span data-stu-id="9e839-114">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="9e839-115">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="9e839-115">**An Azure subscription**.</span></span> <span data-ttu-id="9e839-116">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9e839-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="9e839-117">**Azure PowerShell 1.0 или более поздней версии**.</span><span class="sxs-lookup"><span data-stu-id="9e839-117">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="9e839-118">В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9e839-118">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="authentication"></a><span data-ttu-id="9e839-119">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="9e839-119">Authentication</span></span>
<span data-ttu-id="9e839-120">В этой статье используется более простой подход проверки подлинности с помощью которых вы являетесь запрашиваемые tooenter хранилища Озера данных учетные данные учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="9e839-120">This article uses a simpler authentication approach with Data Lake Store where you are prompted tooenter your Azure account credentials.</span></span> <span data-ttu-id="9e839-121">Hello доступ уровня хранилища Озера tooData учетной записи и файловая система распространяется уровень доступа hello приветствия вошедшего пользователя.</span><span class="sxs-lookup"><span data-stu-id="9e839-121">hello access level tooData Lake Store account and file system is then governed by hello access level of hello logged in user.</span></span> <span data-ttu-id="9e839-122">Однако существуют другие методы как хорошо tooauthenticate с хранилища Озера данных, которые являются **проверки подлинности для конечных пользователей** или **проверки подлинности службы для службы**.</span><span class="sxs-lookup"><span data-stu-id="9e839-122">However, there are other approaches as well tooauthenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="9e839-123">Инструкции и Дополнительные сведения о том, как tooauthenticate, в разделе [проверки подлинности для конечных пользователей](data-lake-store-end-user-authenticate-using-active-directory.md) или [проверки подлинности службы для службы](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="9e839-123">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="9e839-124">Создание учетной записи хранения озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="9e839-124">Create an Azure Data Lake Store account</span></span>
1. <span data-ttu-id="9e839-125">С рабочего стола откройте новое окно Windows PowerShell и введите hello, следующий фрагмент toolog в tooyour учетная запись Azure, задайте hello подписки и регистрации поставщика хранилища Озера данных hello.</span><span class="sxs-lookup"><span data-stu-id="9e839-125">From your desktop, open a new Windows PowerShell window, and enter hello following snippet toolog in tooyour Azure account, set hello subscription, and register hello Data Lake Store provider.</span></span> <span data-ttu-id="9e839-126">При toolog запрос, убедитесь, что войти в систему один hello admininistrators/владелец подписки:</span><span class="sxs-lookup"><span data-stu-id="9e839-126">When prompted toolog in, make sure you log in as one of hello subscription admininistrators/owner:</span></span>

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. <span data-ttu-id="9e839-127">Учетная запись хранения озера данных Azure связывается с группой ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="9e839-127">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="9e839-128">Для начала создайте группу ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="9e839-128">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="9e839-129">![Создание группы ресурсов Azure](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Создание группы ресурсов Azure")</span><span class="sxs-lookup"><span data-stu-id="9e839-129">![Create an Azure Resource Group](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")</span></span>
3. <span data-ttu-id="9e839-130">Создайте учетную запись хранения озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="9e839-130">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="9e839-131">Hello имя должно содержать только строчные буквы и цифры.</span><span class="sxs-lookup"><span data-stu-id="9e839-131">hello name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="9e839-132">![Создание учетной записи Azure Data Lake Store](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Создание учетной записи Azure Data Lake Store")</span><span class="sxs-lookup"><span data-stu-id="9e839-132">![Create an Azure Data Lake Store account](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake Store account")</span></span>
4. <span data-ttu-id="9e839-133">Убедитесь, что учетная запись hello успешно создан.</span><span class="sxs-lookup"><span data-stu-id="9e839-133">Verify that hello account is successfully created.</span></span>

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    <span data-ttu-id="9e839-134">выходные данные для этого необходимо использовать Hello **True**.</span><span class="sxs-lookup"><span data-stu-id="9e839-134">hello output for this should be **True**.</span></span>

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a><span data-ttu-id="9e839-135">Создание структуры каталогов в хранилище озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="9e839-135">Create directory structures in your Azure Data Lake Store</span></span>
<span data-ttu-id="9e839-136">Можно создать каталоги под вашей toomanage учетной записи хранилища Озера данных Azure и хранения данных.</span><span class="sxs-lookup"><span data-stu-id="9e839-136">You can create directories under your Azure Data Lake Store account toomanage and store data.</span></span>

1. <span data-ttu-id="9e839-137">Укажите корневой каталог.</span><span class="sxs-lookup"><span data-stu-id="9e839-137">Specify a root directory.</span></span>

        $myrootdir = "/"
2. <span data-ttu-id="9e839-138">Создайте новую папку с именем **mynewdirectory** в корне указанного hello.</span><span class="sxs-lookup"><span data-stu-id="9e839-138">Create a new directory called **mynewdirectory** under hello specified root.</span></span>

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. <span data-ttu-id="9e839-139">Убедитесь, что в этом новом каталоге hello успешно создан.</span><span class="sxs-lookup"><span data-stu-id="9e839-139">Verify that hello new directory is successfully created.</span></span>

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    <span data-ttu-id="9e839-140">Должна отобразиться выход hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9e839-140">It should show an output like hello following:</span></span>

    <span data-ttu-id="9e839-141">![Проверка каталога](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Проверка каталога")</span><span class="sxs-lookup"><span data-stu-id="9e839-141">![Verify Directory](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verify Directory")</span></span>

## <a name="upload-data-tooyour-azure-data-lake-store"></a><span data-ttu-id="9e839-142">Отправка хранилища Озера данных Azure tooyour данных</span><span class="sxs-lookup"><span data-stu-id="9e839-142">Upload data tooyour Azure Data Lake Store</span></span>
<span data-ttu-id="9e839-143">Можно передать в хранилище Озера данных tooData непосредственно на hello корневого уровня или tooa каталог, созданный в пределах учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="9e839-143">You can upload your data tooData Lake Store directly at hello root level or tooa directory that you created within hello account.</span></span> <span data-ttu-id="9e839-144">фрагменты кода Hello ниже показано, как tooupload некоторые каталог образцов данных toohello (**mynewdirectory**) был создан в предыдущем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="9e839-144">hello snippets below demonstrate how tooupload some sample data toohello directory (**mynewdirectory**) you created in hello previous section.</span></span>

<span data-ttu-id="9e839-145">Если вы ищете некоторые tooupload образец данных, вы можете получить hello **скорая помощь данных** папку из hello [репозитории Озера данных Azure](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="9e839-145">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="9e839-146">Загрузите файл hello и сохранить его в локальный каталог на компьютере, например C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="9e839-146">Download hello file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a><span data-ttu-id="9e839-147">Переименование, загрузка и удаление данных из хранилища озера данных</span><span class="sxs-lookup"><span data-stu-id="9e839-147">Rename, download, and delete data from your Data Lake Store</span></span>
<span data-ttu-id="9e839-148">toorename файл hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="9e839-148">toorename a file, use hello following command:</span></span>

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="9e839-149">toodownload файл hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="9e839-149">toodownload a file, use hello following command:</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

<span data-ttu-id="9e839-150">toodelete файл hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="9e839-150">toodelete a file, use hello following command:</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="9e839-151">При появлении запроса введите **Y** toodelete hello элемента.</span><span class="sxs-lookup"><span data-stu-id="9e839-151">When prompted, enter **Y** toodelete hello item.</span></span> <span data-ttu-id="9e839-152">При наличии более одного файла toodelete, чтобы обеспечить всех hello путей, разделенных точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="9e839-152">If you have more than one file toodelete, you can provide all hello paths separated by comma.</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a><span data-ttu-id="9e839-153">Удаление учетной записи хранения озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="9e839-153">Delete your Azure Data Lake Store account</span></span>
<span data-ttu-id="9e839-154">Используйте следующие команды toodelete hello вашей учетной записи хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="9e839-154">Use hello following command toodelete your Data Lake Store account.</span></span>

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

<span data-ttu-id="9e839-155">При появлении запроса введите **Y** учетной записи toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="9e839-155">When prompted, enter **Y** toodelete hello account.</span></span>

## <a name="performance-guidance-while-using-powershell"></a><span data-ttu-id="9e839-156">Рекомендации по производительности при использовании PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e839-156">Performance guidance while using PowerShell</span></span>

<span data-ttu-id="9e839-157">Ниже приведены наиболее важные параметры, которые могут быть настроенном tooget hello наилучшей производительности при работе с PowerShell toowork с хранилищем данных Озера hello.</span><span class="sxs-lookup"><span data-stu-id="9e839-157">Below are hello most important settings that can be tuned tooget hello best performance while using PowerShell toowork with Data Lake Store:</span></span>

| <span data-ttu-id="9e839-158">Свойство</span><span class="sxs-lookup"><span data-stu-id="9e839-158">Property</span></span>            | <span data-ttu-id="9e839-159">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="9e839-159">Default</span></span> | <span data-ttu-id="9e839-160">Описание</span><span class="sxs-lookup"><span data-stu-id="9e839-160">Description</span></span> |
|---------------------|---------|-------------|
| <span data-ttu-id="9e839-161">PerFileThreadCount</span><span class="sxs-lookup"><span data-stu-id="9e839-161">PerFileThreadCount</span></span>  | <span data-ttu-id="9e839-162">10</span><span class="sxs-lookup"><span data-stu-id="9e839-162">10</span></span>      | <span data-ttu-id="9e839-163">Этот параметр включает toochoose hello число параллельных потоков для отправки или загрузки каждого файла.</span><span class="sxs-lookup"><span data-stu-id="9e839-163">This parameter enables you toochoose hello number of parallel threads for uploading or downloading each file.</span></span> <span data-ttu-id="9e839-164">Это число представляет hello максимального количества потоков, которые могут быть распределены на файл, но можно получить меньше потоков в зависимости от вашего сценария (например при отправке файла 1 КБ, вы получите один поток, даже если вы запрашиваете 20 потоков).</span><span class="sxs-lookup"><span data-stu-id="9e839-164">This number represents hello max threads that can be allocated per file, but you may get less threads depending on your scenario (e.g. if you are uploading a 1KB file, you will get one thread even if you ask for 20 threads).</span></span>  |
| <span data-ttu-id="9e839-165">ConcurrentFileCount</span><span class="sxs-lookup"><span data-stu-id="9e839-165">ConcurrentFileCount</span></span> | <span data-ttu-id="9e839-166">10</span><span class="sxs-lookup"><span data-stu-id="9e839-166">10</span></span>      | <span data-ttu-id="9e839-167">Этот параметр предназначен для отправки или скачивания папок.</span><span class="sxs-lookup"><span data-stu-id="9e839-167">This parameter is specifically for uploading or downloading folders.</span></span> <span data-ttu-id="9e839-168">Этот параметр определяет количество одновременных файлы, которые передаются или загружаются в hello.</span><span class="sxs-lookup"><span data-stu-id="9e839-168">This parameter determines hello number of concurrent files that can be uploaded or downloaded.</span></span> <span data-ttu-id="9e839-169">Это число представляет hello максимальное число одновременных файлы, которые можно передать или загрузить за один раз, но можно получить меньше параллелизма в зависимости от вашего сценария (например при отправке два файла, вы получите два передачи файлов, даже при обращении за 15).</span><span class="sxs-lookup"><span data-stu-id="9e839-169">This number represents hello maximum number of concurrent files that can be uploaded or downloaded at one time, but you may get less concurrency depending on your scenario (e.g. if you are uploading two files, you will get two concurrent file uploads even if you ask for 15).</span></span> |

<span data-ttu-id="9e839-170">**Пример**</span><span class="sxs-lookup"><span data-stu-id="9e839-170">**Example**</span></span>

<span data-ttu-id="9e839-171">Эта команда загружает файлы с локального диска toohello пользователь хранилища Озера данных Azure с помощью 20 потоков на файл и 100 одновременных файлов.</span><span class="sxs-lookup"><span data-stu-id="9e839-171">This command downloads files from Azure Data Lake Store toohello user's local drive using 20 threads per file and 100 concurrent files.</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

### <a name="how-do-i-determine-hello-value-tooset-for-these-parameters"></a><span data-ttu-id="9e839-172">Как определить hello tooset значения для этих параметров?</span><span class="sxs-lookup"><span data-stu-id="9e839-172">How do I determine hello value tooset for these parameters?</span></span>

<span data-ttu-id="9e839-173">Ниже представлены некоторые полезные рекомендации.</span><span class="sxs-lookup"><span data-stu-id="9e839-173">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="9e839-174">**Шаг 1: Определение количества общий поток hello** -следует начать с toouse число поток общее расчет hello.</span><span class="sxs-lookup"><span data-stu-id="9e839-174">**Step 1: Determine hello total thread count** - You should start by calculating hello total thread count toouse.</span></span> <span data-ttu-id="9e839-175">Как правило, следует использовать 6 потоков для каждого физического ядра.</span><span class="sxs-lookup"><span data-stu-id="9e839-175">As a general guideline, you should use 6 threads for each physical core.</span></span>

        Total thread count = total physical cores * 6

    <span data-ttu-id="9e839-176">**Пример**</span><span class="sxs-lookup"><span data-stu-id="9e839-176">**Example**</span></span>

    <span data-ttu-id="9e839-177">При условии, что вы используете hello PowerShell команды из виртуальной Машины D14 имеет 16 ядер</span><span class="sxs-lookup"><span data-stu-id="9e839-177">Assuming you are running hello PowerShell commands from a D14 VM that has 16 cores</span></span>

        Total thread count = 16 cores * 6 = 96 threads


* <span data-ttu-id="9e839-178">**Шаг 2: Вычисление PerFileThreadCount** -вычислять наших PerFileThreadCount, в зависимости от размера файлов hello hello.</span><span class="sxs-lookup"><span data-stu-id="9e839-178">**Step 2: Calculate PerFileThreadCount**  - We calculate our PerFileThreadCount based on hello size of hello files.</span></span> <span data-ttu-id="9e839-179">Для файлов размером менее 2,5 ГБ нет toochange нет необходимости этот параметр, так как по умолчанию hello 10 достаточно.</span><span class="sxs-lookup"><span data-stu-id="9e839-179">For files smaller than 2.5GB, there is no need toochange this parameter because hello default of 10 is sufficient.</span></span> <span data-ttu-id="9e839-180">Для файлов больше 2,5 ГБ 10 потоков следует использовать как hello базы для hello первые 2,5 ГБ и добавьте одному потоку для каждой дополнительной увеличение 256 МБ размера файла.</span><span class="sxs-lookup"><span data-stu-id="9e839-180">For files larger than 2.5GB, you should use 10 threads as hello base for hello first 2.5GB and add 1 thread for each additional 256MB increase in file size.</span></span> <span data-ttu-id="9e839-181">При копировании папки с файлами разного размера рекомендуется разделить их на группы по схожим размерам.</span><span class="sxs-lookup"><span data-stu-id="9e839-181">If you are copying a folder with a large range of file sizes, consider grouping them into similar file sizes.</span></span> <span data-ttu-id="9e839-182">Использование файлов разных размеров может привести к снижению производительности.</span><span class="sxs-lookup"><span data-stu-id="9e839-182">Having dissimilar file sizes may cause non-optimal performance.</span></span> <span data-ttu-id="9e839-183">Если это возможно toogroup сходные размеры файлов, необходимо задать PerFileThreadCount основании hello максимальный размер файла.</span><span class="sxs-lookup"><span data-stu-id="9e839-183">If that's not possible toogroup similar file sizes, you should set PerFileThreadCount based on hello largest file size.</span></span>

        PerFileThreadCount = 10 threads for hello first 2.5GB + 1 thread for each additional 256MB increase in file size

    <span data-ttu-id="9e839-184">**Пример**</span><span class="sxs-lookup"><span data-stu-id="9e839-184">**Example**</span></span>

    <span data-ttu-id="9e839-185">Предположим, что у вас есть 100 файлов в диапазоне от 1 ГБ too10GB, мы используем hello 10 ГБ, как hello наибольший размер формула, которая будет читаться hello следующим образом файла.</span><span class="sxs-lookup"><span data-stu-id="9e839-185">Assuming you have 100 files ranging from 1GB too10GB, we use hello 10GB as hello largest file size for equation, which would read like hello following.</span></span>

        PerFileThreadCount = 10 + ((10GB - 2.5GB) / 256MB) = 40 threads

* <span data-ttu-id="9e839-186">**Шаг 3: Вычисление ConcurrentFilecount** -поток общее число использований hello и PerFileThreadCount toocalculate ConcurrentFileCount с учетом hello, следующая формула.</span><span class="sxs-lookup"><span data-stu-id="9e839-186">**Step 3: Calculate ConcurrentFilecount** - Use hello total thread count and PerFileThreadCount toocalculate ConcurrentFileCount based on hello following equation.</span></span>

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    <span data-ttu-id="9e839-187">**Пример**</span><span class="sxs-lookup"><span data-stu-id="9e839-187">**Example**</span></span>

    <span data-ttu-id="9e839-188">На основе значений пример hello, мы использовали</span><span class="sxs-lookup"><span data-stu-id="9e839-188">Based on hello example values we have been using</span></span>

        96 = 40 * ConcurrentFileCount

    <span data-ttu-id="9e839-189">Таким образом **ConcurrentFileCount** — **2.4**, который мы можно округлить слишком**2**.</span><span class="sxs-lookup"><span data-stu-id="9e839-189">So, **ConcurrentFileCount** is **2.4**, which we can round off too**2**.</span></span>

### <a name="further-tuning"></a><span data-ttu-id="9e839-190">Дополнительные настройки</span><span class="sxs-lookup"><span data-stu-id="9e839-190">Further tuning</span></span>

<span data-ttu-id="9e839-191">Могут потребоваться дополнительные настройки из-за диапазон toowork размеры файлов с.</span><span class="sxs-lookup"><span data-stu-id="9e839-191">You might require further tuning because there is a range of file sizes toowork with.</span></span> <span data-ttu-id="9e839-192">Hello выше вычисления работает также в том случае, если все или большинство файлов hello являются более крупными и подробный toohello диапазон 10 ГБ.</span><span class="sxs-lookup"><span data-stu-id="9e839-192">hello above calculation works well if all or most of hello files are larger and closer toohello 10GB range.</span></span> <span data-ttu-id="9e839-193">Однако если у вас есть множество файлов разных размеров (меньше 10 ГБ), можно уменьшить значение параметра PerFileThreadCount.</span><span class="sxs-lookup"><span data-stu-id="9e839-193">If instead, there are many different files sizes with many files being smaller, then you could reduce PerFileThreadCount.</span></span> <span data-ttu-id="9e839-194">Уменьшая hello PerFileThreadCount, мы увеличим ConcurrentFileCount.</span><span class="sxs-lookup"><span data-stu-id="9e839-194">By reducing hello PerFileThreadCount, we can increase ConcurrentFileCount.</span></span> <span data-ttu-id="9e839-195">Таким образом Если предполагается, что большая часть наших файлов меньшего размера, в диапазоне hello 5 ГБ, мы можем повторно выполните наших вычислений:</span><span class="sxs-lookup"><span data-stu-id="9e839-195">So, if we assume that most of our files are smaller in hello 5GB range, we can re-do our calculation:</span></span>

    PerFileThreadCount = 10 + ((5GB - 2.5GB) / 256MB) = 20

<span data-ttu-id="9e839-196">Таким образом **ConcurrentFileCount** будет теперь 96/20, являющийся 4.8 округлено слишком**4**.</span><span class="sxs-lookup"><span data-stu-id="9e839-196">So, **ConcurrentFileCount** will now be 96/20, which is 4.8, rounded off too**4**.</span></span>

<span data-ttu-id="9e839-197">Вы можете продолжить tootune эти параметры, изменение hello **PerFileThreadCount** вверх и вниз в зависимости от распределения hello размер файлов.</span><span class="sxs-lookup"><span data-stu-id="9e839-197">You can continue tootune these settings by changing hello **PerFileThreadCount** up and down depending on hello distribution of your file sizes.</span></span>

### <a name="limitation"></a><span data-ttu-id="9e839-198">Ограничение</span><span class="sxs-lookup"><span data-stu-id="9e839-198">Limitation</span></span>

* <span data-ttu-id="9e839-199">**Количество файлов меньше, чем ConcurrentFileCount**: Если hello число файлов, которые вы отправляете меньше hello **ConcurrentFileCount** , вычисленную, то следует уменьшить  **ConcurrentFileCount** toobe равно toohello число файлов.</span><span class="sxs-lookup"><span data-stu-id="9e839-199">**Number of files is less than ConcurrentFileCount**: If hello number of files you are uploading is smaller than hello **ConcurrentFileCount** that you calculated, then you should reduce **ConcurrentFileCount** toobe equal toohello number of files.</span></span> <span data-ttu-id="9e839-200">Можно использовать все остальные потоки tooincrease **PerFileThreadCount**.</span><span class="sxs-lookup"><span data-stu-id="9e839-200">You can use any remaining threads tooincrease **PerFileThreadCount**.</span></span>

* <span data-ttu-id="9e839-201">**Слишком много потоков**: Если увеличить поток слишком большого объема без увеличения размер кластера, запустите hello риск снижение производительности.</span><span class="sxs-lookup"><span data-stu-id="9e839-201">**Too many threads**: If you increase thread count too much without increasing your cluster size, you run hello risk of degraded performance.</span></span> <span data-ttu-id="9e839-202">При переключении контекста на hello ЦП может быть конфликтным.</span><span class="sxs-lookup"><span data-stu-id="9e839-202">There can be contention issues when context-switching on hello CPU.</span></span>

* <span data-ttu-id="9e839-203">**Недостаточно параллелизма**: Если параллелизма hello недостаточно, то кластера может быть слишком мал.</span><span class="sxs-lookup"><span data-stu-id="9e839-203">**Insufficient concurrency**: If hello concurrency is not sufficient, then your cluster may be too small.</span></span> <span data-ttu-id="9e839-204">Можно увеличить hello количество узлов в кластере, в которых можно получить дополнительные параллелизма.</span><span class="sxs-lookup"><span data-stu-id="9e839-204">You can increase hello number of nodes in your cluster which will give you more concurrency.</span></span>

* <span data-ttu-id="9e839-205">**Ошибки регулирования.** При слишком высоком уровне параллелизма могут возникнуть ошибки регулирования.</span><span class="sxs-lookup"><span data-stu-id="9e839-205">**Throttling errors**: You may see throttling errors if your concurrency is too high.</span></span> <span data-ttu-id="9e839-206">Если вы видите ошибки регулирования, следует уменьшению параллелизма hello или свяжитесь с нами.</span><span class="sxs-lookup"><span data-stu-id="9e839-206">If you are seeing throttling errors, you should either reduce hello concurrency or contact us.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e839-207">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9e839-207">Next steps</span></span>
* [<span data-ttu-id="9e839-208">Защита данных в хранилище озера данных</span><span class="sxs-lookup"><span data-stu-id="9e839-208">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="9e839-209">Использование аналитики озера данных Azure с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="9e839-209">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="9e839-210">Использование Azure HDInsight с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="9e839-210">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

