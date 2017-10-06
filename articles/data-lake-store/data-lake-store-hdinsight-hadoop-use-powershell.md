---
<span data-ttu-id="f9bee-101">Заголовок: aaa "PowerShell: кластера Azure HDInsight с помощью хранилища Озера данных в виде дополнительное хранилище | Документы Microsoft» служб:-хранилищу Озера данных — hdinsight documentationcenter: '' Автор: диспетчер nitinme: jhubbard редактор: cgronlun</span><span class="sxs-lookup"><span data-stu-id="f9bee-101">title: aaa"PowerShell: Azure HDInsight cluster with Data Lake Store as add-on storage | Microsoft Docs" services: data-lake-store,hdinsight documentationcenter: '' author: nitinme manager: jhubbard editor: cgronlun</span></span>

<span data-ttu-id="f9bee-102">MS.AssetId: 164ada5a-222e-4be2-bd32-e51dbe993bc0 ms.service: ms.devlang хранилища Озера данных: н/д ms.topic: статья ms.tgt_pltfrm: ms.workload н/д: ms.date большие наборы данных: ms.author 06/08/2017 г.: nitinme</span><span class="sxs-lookup"><span data-stu-id="f9bee-102">ms.assetid: 164ada5a-222e-4be2-bd32-e51dbe993bc0 ms.service: data-lake-store ms.devlang: na ms.topic: article ms.tgt_pltfrm: na ms.workload: big-data ms.date: 06/08/2017 ms.author: nitinme</span></span>

---
# <a name="use-azure-powershell-toocreate-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="f9bee-103">Использовать Azure PowerShell toocreate кластер HDInsight с хранилища Озера данных (в качестве дополнительного хранилища)</span><span class="sxs-lookup"><span data-stu-id="f9bee-103">Use Azure PowerShell toocreate an HDInsight cluster with Data Lake Store (as additional storage)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f9bee-104">Использование портала</span><span class="sxs-lookup"><span data-stu-id="f9bee-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="f9bee-105">Использование PowerShell (для хранилища по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="f9bee-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="f9bee-106">Использование PowerShell (для дополнительного хранилища)</span><span class="sxs-lookup"><span data-stu-id="f9bee-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="f9bee-107">Использование Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f9bee-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="f9bee-108">Узнайте, как tooconfigure toouse Azure PowerShell HDInsight кластер с хранилища Озера данных Azure, **как дополнительное хранилище**.</span><span class="sxs-lookup"><span data-stu-id="f9bee-108">Learn how toouse Azure PowerShell tooconfigure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span> <span data-ttu-id="f9bee-109">Инструкции как toocreate HDInsight кластер с хранилища Озера данных Azure, как хранилище по умолчанию см. в разделе [создать кластер HDInsight с помощью хранилища Озера данных в качестве хранилища по умолчанию](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span><span class="sxs-lookup"><span data-stu-id="f9bee-109">For instructions on how toocreate an HDInsight cluster with Azure Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store as default storage](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f9bee-110">Если вы собираетесь хранилища Озера данных Azure toouse как дополнительное хранилище для кластера HDInsight, настоятельно рекомендуется это сделать, при создании кластера hello, как описано в этой статье.</span><span class="sxs-lookup"><span data-stu-id="f9bee-110">If you are going toouse Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create hello cluster as described in this article.</span></span> <span data-ttu-id="f9bee-111">Добавление хранилища Озера данных Azure в качестве дополнительного хранилища tooan существующий кластер HDInsight является сложным процессом и ошибкам tooerrors.</span><span class="sxs-lookup"><span data-stu-id="f9bee-111">Adding Azure Data Lake Store as additional storage tooan existing HDInsight cluster is a complicated process and prone tooerrors.</span></span>
>

<span data-ttu-id="f9bee-112">В поддерживаемых типах кластеров Data Lake Store можно использовать в качестве хранилища по умолчанию или дополнительной учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="f9bee-112">For supported cluster types, Data Lake Store can be used as a default storage or additional storage account.</span></span> <span data-ttu-id="f9bee-113">При использовании хранилища Озера данных как дополнительное хранилище hello учетной записи хранения по умолчанию для кластеров hello по-прежнему будут хранилища больших двоичных объектов Azure (WASB) и hello кластера файлов (например, журналы, т. д.) по-прежнему записываются toohello хранилища по умолчанию, при hello данных, которые необходимо tooprocess могут храниться в учетной записи хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="f9bee-113">When Data Lake Store is used as additional storage, hello default storage account for hello clusters will still be Azure Storage Blobs (WASB) and hello cluster-related files (such as logs, etc.) are still written toohello default storage, while hello data that you want tooprocess can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="f9bee-114">С помощью хранилища Озера данных от имени учетной записи дополнительное хранилище не влияет на производительность и работу хранилища toohello hello возможность tooread и записи из кластера hello.</span><span class="sxs-lookup"><span data-stu-id="f9bee-114">Using Data Lake Store as an additional storage account does not impact performance or hello ability tooread/write toohello storage from hello cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="f9bee-115">Использование Data Lake Store в качестве хранилища кластера HDInsight</span><span class="sxs-lookup"><span data-stu-id="f9bee-115">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="f9bee-116">Ниже приведены некоторые важные сведения об использовании HDInsight с Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f9bee-116">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="f9bee-117">Кластеры HDInsight toocreate параметр с доступом хранилища Озера tooData как дополнительное хранилище доступно для HDInsight версии 3.2, 3.4, 3.5 и 3.6.</span><span class="sxs-lookup"><span data-stu-id="f9bee-117">Option toocreate HDInsight clusters with access tooData Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="f9bee-118">Настройка HDInsight toowork с хранилища Озера данных с помощью PowerShell включает следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="f9bee-118">Configuring HDInsight toowork with Data Lake Store using PowerShell involves hello following steps:</span></span>

* <span data-ttu-id="f9bee-119">Создание хранилища озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="f9bee-119">Create an Azure Data Lake Store</span></span>
* <span data-ttu-id="f9bee-120">Настройка проверки подлинности на основе ролей доступ к хранилищу Озера tooData</span><span class="sxs-lookup"><span data-stu-id="f9bee-120">Set up authentication for role-based access tooData Lake Store</span></span>
* <span data-ttu-id="f9bee-121">Создание кластера HDInsight с хранилища Озера tooData проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="f9bee-121">Create HDInsight cluster with authentication tooData Lake Store</span></span>
* <span data-ttu-id="f9bee-122">Запустите задание тестов на кластере hello</span><span class="sxs-lookup"><span data-stu-id="f9bee-122">Run a test job on hello cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9bee-123">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f9bee-123">Prerequisites</span></span>
<span data-ttu-id="f9bee-124">Прежде чем начать работу с учебником, необходимо иметь следующие hello.</span><span class="sxs-lookup"><span data-stu-id="f9bee-124">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="f9bee-125">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="f9bee-125">**An Azure subscription**.</span></span> <span data-ttu-id="f9bee-126">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f9bee-126">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f9bee-127">**Azure PowerShell 1.0 или более поздней версии**.</span><span class="sxs-lookup"><span data-stu-id="f9bee-127">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="f9bee-128">В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f9bee-128">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="f9bee-129">**Пакет SDK Windows**.</span><span class="sxs-lookup"><span data-stu-id="f9bee-129">**Windows SDK**.</span></span> <span data-ttu-id="f9bee-130">Его можно установить [отсюда](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="f9bee-130">You can install it from [here](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="f9bee-131">Использовать этот toocreate сертификат безопасности.</span><span class="sxs-lookup"><span data-stu-id="f9bee-131">You use this toocreate a security certificate.</span></span>
* <span data-ttu-id="f9bee-132">**Субъект-служба Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f9bee-132">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="f9bee-133">В этом учебнике приведены инструкции о том, как toocreate участника службы в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9bee-133">Steps in this tutorial provide instructions on how toocreate a service principal in Azure AD.</span></span> <span data-ttu-id="f9bee-134">Тем не менее необходимо быть toocreate toobe может субъекта-службы администрирования Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9bee-134">However, you must be an Azure AD administrator toobe able toocreate a service principal.</span></span> <span data-ttu-id="f9bee-135">Если вы являетесь администратором Azure AD, можно пропустить это предварительное условие и продолжить работу с учебником hello.</span><span class="sxs-lookup"><span data-stu-id="f9bee-135">If you are an Azure AD administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    <span data-ttu-id="f9bee-136">**Если вы не являетесь администратором Azure AD**, не будет возможности tooperform hello действия требуется toocreate участника службы.</span><span class="sxs-lookup"><span data-stu-id="f9bee-136">**If you are not an Azure AD administrator**, you will not be able tooperform hello steps required toocreate a service principal.</span></span> <span data-ttu-id="f9bee-137">В этом случае администратор Azure AD должен сначала создать субъект-службу, после чего вы сможете создать кластер HDInsight с Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f9bee-137">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="f9bee-138">Кроме того, hello участника-службы должны создаваться с помощью сертификата, как описано в разделе [создании участника службы с сертификатом](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="f9bee-138">Also, hello service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="f9bee-139">Создание хранилища озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="f9bee-139">Create an Azure Data Lake Store</span></span>
<span data-ttu-id="f9bee-140">Выполните эти шаги toocreate хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="f9bee-140">Follow these steps toocreate a Data Lake Store.</span></span>

1. <span data-ttu-id="f9bee-141">С рабочего стола откройте новое окно Azure PowerShell и введите следующий фрагмент кода hello.</span><span class="sxs-lookup"><span data-stu-id="f9bee-141">From your desktop, open a new Azure PowerShell window, and enter hello following snippet.</span></span> <span data-ttu-id="f9bee-142">Когда запрос toolog, убедитесь, что войти в систему один администратор или владелец подписки hello:</span><span class="sxs-lookup"><span data-stu-id="f9bee-142">When prompted toolog in, make sure you log in as one of hello subscription administrator/owner:</span></span>

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > <span data-ttu-id="f9bee-143">Если появится сообщение об ошибке слишком`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` при регистрации поставщика ресурсов хранилища Озера данных hello, это возможно, что ваша подписка не входят для хранилища Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="f9bee-143">If you receive an error similar too`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` when registering hello Data Lake Store resource provider, it is possible that your subscription is not whitelisted for Azure Data Lake Store.</span></span> <span data-ttu-id="f9bee-144">Убедитесь, что подписка Azure для общедоступной предварительной версии Data Lake Store включена, выполнив указанные [инструкции](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f9bee-144">Make sure you enable your Azure subscription for Data Lake Store public preview by following these [instructions](data-lake-store-get-started-portal.md).</span></span>
   >
   >
2. <span data-ttu-id="f9bee-145">Учетная запись хранения озера данных Azure связывается с группой ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="f9bee-145">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="f9bee-146">Для начала создайте группу ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="f9bee-146">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="f9bee-147">Вы должны увидеть подобные выходные данные:</span><span class="sxs-lookup"><span data-stu-id="f9bee-147">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="f9bee-148">Создайте учетную запись хранения озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="f9bee-148">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="f9bee-149">Hello учетная запись, что имя должно содержать только строчные буквы и цифры.</span><span class="sxs-lookup"><span data-stu-id="f9bee-149">hello account name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="f9bee-150">Вы должны увидеть результаты hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f9bee-150">You should see an output like hello following:</span></span>

        ...
        ProvisioningState           : Succeeded
        State                       : Active
        CreationTime                : 5/5/2017 10:53:56 PM
        EncryptionState             : Enabled
        ...
        LastModifiedTime            : 5/5/2017 10:53:56 PM
        Endpoint                    : hdiadlstore.azuredatalakestore.net
        DefaultGroup                :
        Id                          : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp/providers/Microsoft.DataLakeStore/accounts/hdiadlstore
        Name                        : hdiadlstore
        Type                        : Microsoft.DataLakeStore/accounts
        Location                    : East US 2
        Tags                        : {}

5. <span data-ttu-id="f9bee-151">Отправьте некоторые образец данных tooAzure Озера данных.</span><span class="sxs-lookup"><span data-stu-id="f9bee-151">Upload some sample data tooAzure Data Lake.</span></span> <span data-ttu-id="f9bee-152">Мы будем использовать далее в этой статье tooverify, что hello данных доступен с кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f9bee-152">We'll use this later in this article tooverify that hello data is accessible from an HDInsight cluster.</span></span> <span data-ttu-id="f9bee-153">Если вы ищете некоторые tooupload образец данных, вы можете получить hello **скорая помощь данных** папку из hello [репозитории Озера данных Azure](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="f9bee-153">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path toodata>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a><span data-ttu-id="f9bee-154">Настройка проверки подлинности на основе ролей доступ к хранилищу Озера tooData</span><span class="sxs-lookup"><span data-stu-id="f9bee-154">Set up authentication for role-based access tooData Lake Store</span></span>
<span data-ttu-id="f9bee-155">Каждая подписка Azure связана со службой Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f9bee-155">Every Azure subscription is associated with an Azure Active Directory.</span></span> <span data-ttu-id="f9bee-156">Пользователей и служб, которые обращаются к ресурсам hello подписки с помощью hello классический портал Azure или API диспетчера ресурсов Azure должны сначала пройти проверку подлинности с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f9bee-156">Users and services that access resources of hello subscription using hello Azure Classic Portal or Azure Resource Manager API must first authenticate with that Azure Active Directory.</span></span> <span data-ttu-id="f9bee-157">Доступ предоставляется tooAzure подписками и службами путем назначения им hello соответствующей роли на ресурс Azure.</span><span class="sxs-lookup"><span data-stu-id="f9bee-157">Access is granted tooAzure subscriptions and services by assigning them hello appropriate role on an Azure resource.</span></span>  <span data-ttu-id="f9bee-158">Для служб субъекта-службы идентифицирует службу hello в hello Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="f9bee-158">For services, a service principal identifies hello service in hello Azure Active Directory (AAD).</span></span> <span data-ttu-id="f9bee-159">В этом разделе показано, как службы toogrant приложения, как HDInsight tooan доступа ресурсов Azure (hello созданную ранее учетную запись хранилища Озера данных Azure) путем создания участника службы для приложения hello и назначение ролей toothat через Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f9bee-159">This section illustrates how toogrant an application service, like HDInsight, access tooan Azure resource (hello Azure Data Lake Store account you created earlier) by creating a service principal for hello application and assigning roles toothat via Azure PowerShell.</span></span>

<span data-ttu-id="f9bee-160">tooset проверку подлинности Active Directory для Озера данных Azure, необходимо выполнить следующие задачи hello.</span><span class="sxs-lookup"><span data-stu-id="f9bee-160">tooset up Active Directory authentication for Azure Data Lake, you must perform hello following tasks.</span></span>

* <span data-ttu-id="f9bee-161">Создание самозаверяющего сертификата</span><span class="sxs-lookup"><span data-stu-id="f9bee-161">Create a self-signed certificate</span></span>
* <span data-ttu-id="f9bee-162">создать приложение в Azure Active Directory и субъект-службу.</span><span class="sxs-lookup"><span data-stu-id="f9bee-162">Create an application in Azure Active Directory and a Service Principal</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="f9bee-163">Создание самозаверяющего сертификата</span><span class="sxs-lookup"><span data-stu-id="f9bee-163">Create a self-signed certificate</span></span>
<span data-ttu-id="f9bee-164">Убедитесь, что у вас есть [пакета Windows SDK](https://dev.windows.com/en-us/downloads) установлен перед продолжением hello шаги в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="f9bee-164">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with hello steps in this section.</span></span> <span data-ttu-id="f9bee-165">Необходимо также создать каталог, например **C:\mycertdir**, где будет создан сертификат hello.</span><span class="sxs-lookup"><span data-stu-id="f9bee-165">You must have also created a directory, such as **C:\mycertdir**, where hello certificate will be created.</span></span>

1. <span data-ttu-id="f9bee-166">В окне PowerShell hello перейдите toohello расположение, где установлен пакет SDK для Windows (как правило, `C:\Program Files (x86)\Windows Kits\10\bin\x86` и использовать hello [MakeCert] [ makecert] toocreate программа самозаверяющий сертификат и закрытый ключ.</span><span class="sxs-lookup"><span data-stu-id="f9bee-166">From hello PowerShell window, navigate toohello location where you installed Windows SDK (typically, `C:\Program Files (x86)\Windows Kits\10\bin\x86` and use hello [MakeCert][makecert] utility toocreate a self-signed certificate and a private key.</span></span> <span data-ttu-id="f9bee-167">Используйте следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="f9bee-167">Use hello following commands.</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="f9bee-168">Появится запрос tooenter hello пароль для закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="f9bee-168">You will be prompted tooenter hello private key password.</span></span> <span data-ttu-id="f9bee-169">После hello команда выполнена успешно, вы увидите **CertFile.cer** и **mykey.pvk** в указанный каталог сертификат hello.</span><span class="sxs-lookup"><span data-stu-id="f9bee-169">After hello command successfully executes, you should see a **CertFile.cer** and **mykey.pvk** in hello certificate directory you specified.</span></span>
2. <span data-ttu-id="f9bee-170">Используйте hello [Pvk2Pfx] [ pvk2pfx] .pvk hello tooconvert программы или CER-файлы, MakeCert созданный tooa PFX-файл.</span><span class="sxs-lookup"><span data-stu-id="f9bee-170">Use hello [Pvk2Pfx][pvk2pfx] utility tooconvert hello .pvk and .cer files that MakeCert created tooa .pfx file.</span></span> <span data-ttu-id="f9bee-171">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="f9bee-171">Run hello following command.</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="f9bee-172">При появлении запроса введите hello пароль закрытого ключа, указанной вами ранее.</span><span class="sxs-lookup"><span data-stu-id="f9bee-172">When prompted enter hello private key password you specified earlier.</span></span> <span data-ttu-id="f9bee-173">значение, указываемое для hello Hello **-po** параметр является hello пароль, связанный с hello PFX-файл.</span><span class="sxs-lookup"><span data-stu-id="f9bee-173">hello value you specify for hello **-po** parameter is hello password that is associated with hello .pfx file.</span></span> <span data-ttu-id="f9bee-174">После успешного завершения команды hello вы также увидите CertFile.pfx в каталог hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="f9bee-174">After hello command successfully completes, you should also see a CertFile.pfx in hello certificate directory you specified.</span></span>

### <a name="create-an-azure-active-directory-and-a-service-principal"></a><span data-ttu-id="f9bee-175">Создание приложения в Azure Active Directory и субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="f9bee-175">Create an Azure Active Directory and a service principal</span></span>
<span data-ttu-id="f9bee-176">В этом разделе выполните шаги hello toocreate участника службы для приложения Azure Active Directory, назначение роли участника службы toohello и проверять подлинность как у участника-службы hello, предоставляя сертификат.</span><span class="sxs-lookup"><span data-stu-id="f9bee-176">In this section, you perform hello steps toocreate a service principal for an Azure Active Directory application, assign a role toohello service principal, and authenticate as hello service principal by providing a certificate.</span></span> <span data-ttu-id="f9bee-177">Запустите следующие команды toocreate hello приложения в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f9bee-177">Run hello following commands toocreate an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="f9bee-178">Вставьте следующие командлеты в окне консоли PowerShell hello hello.</span><span class="sxs-lookup"><span data-stu-id="f9bee-178">Paste hello following cmdlets in hello PowerShell console window.</span></span> <span data-ttu-id="f9bee-179">Убедитесь, что значение hello укажите для hello **- DisplayName** свойство является уникальным.</span><span class="sxs-lookup"><span data-stu-id="f9bee-179">Make sure hello value you specify for hello **-DisplayName** property is unique.</span></span> <span data-ttu-id="f9bee-180">Кроме того, hello значения для **- Домашняя страница** и **- IdentiferUris** значения заполнителя, а не проверяются.</span><span class="sxs-lookup"><span data-stu-id="f9bee-180">Also, hello values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter hello password" # This is hello password you specified for hello .pfx file

        $certificatePFX = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($certificateFilePath, $password)

        $rawCertificateData = $certificatePFX.GetRawCertData()

        $credential = [System.Convert]::ToBase64String($rawCertificateData)

        $application = New-AzureRmADApplication `
            -DisplayName "HDIADL" `
            -HomePage "https://contoso.com" `
            -IdentifierUris "https://mycontoso.com" `
            -CertValue $credential  `
            -StartDate $certificatePFX.NotBefore  `
            -EndDate $certificatePFX.NotAfter

        $applicationId = $application.ApplicationId
2. <span data-ttu-id="f9bee-181">Создание участника службы с помощью идентификатора приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f9bee-181">Create a service principal using hello application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="f9bee-182">Предоставьте hello службы доступа toohello хранилища Озера данных папки и файла hello, вы получите доступ к кластеру HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="f9bee-182">Grant hello service principal access toohello Data Lake Store folder and hello file that you will access from hello HDInsight cluster.</span></span> <span data-ttu-id="f9bee-183">в приведенном ниже фрагменте Hello предоставляет доступ toohello корень hello хранилища Озера данных учетной записи (который вы скопировали hello образец файла данных) и сам файл hello.</span><span class="sxs-lookup"><span data-stu-id="f9bee-183">hello snippet below provides access toohello root of hello Data Lake Store account (where you copied hello sample data file), and hello file itself.</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="f9bee-184">Создание кластера HDInsight на платформе Linux с Data Lake Store в качестве дополнительного хранилища</span><span class="sxs-lookup"><span data-stu-id="f9bee-184">Create an HDInsight Linux cluster with Data Lake Store as additional storage</span></span>

<span data-ttu-id="f9bee-185">В этом разделе показано, как создать кластер HDInsight Hadoop на платформе Linux с Data Lake Store в качестве дополнительного хранилища.</span><span class="sxs-lookup"><span data-stu-id="f9bee-185">In this section, we create an HDInsight Hadoop Linux cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="f9bee-186">В этом выпуске кластера HDInsight hello и hello хранилища Озера данных должны находиться в hello местоположения.</span><span class="sxs-lookup"><span data-stu-id="f9bee-186">For this release, hello HDInsight cluster and hello Data Lake Store must be in hello same location.</span></span>

1. <span data-ttu-id="f9bee-187">Начать с получения идентификатора hello подписки клиента.</span><span class="sxs-lookup"><span data-stu-id="f9bee-187">Start with retrieving hello subscription tenant ID.</span></span> <span data-ttu-id="f9bee-188">Позже он вам понадобится.</span><span class="sxs-lookup"><span data-stu-id="f9bee-188">You will need that later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. <span data-ttu-id="f9bee-189">Для этого выпуска кластер Hadoop, хранилище Озера данных может использоваться только как дополнительное хранилище для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="f9bee-189">For this release, for a Hadoop cluster, Data Lake Store can only be used as an additional storage for hello cluster.</span></span> <span data-ttu-id="f9bee-190">хранилище по умолчанию Hello по-прежнему будут hello Azure хранилища больших двоичных объектов (WASB).</span><span class="sxs-lookup"><span data-stu-id="f9bee-190">hello default storage will still be hello Azure storage blobs (WASB).</span></span> <span data-ttu-id="f9bee-191">Таким образом сначала создадим hello учетной записи и хранилища контейнеров хранилища для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="f9bee-191">So, we'll first create hello storage account and storage containers required for hello cluster.</span></span>

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. <span data-ttu-id="f9bee-192">Создание кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="f9bee-192">Create hello HDInsight cluster.</span></span> <span data-ttu-id="f9bee-193">Используйте следующие командлеты hello.</span><span class="sxs-lookup"><span data-stu-id="f9bee-193">Use hello following cmdlets.</span></span>

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have hello same name for hello cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    <span data-ttu-id="f9bee-194">После успешного завершения командлет hello должны появиться сведения кластера hello списка выходных данных.</span><span class="sxs-lookup"><span data-stu-id="f9bee-194">After hello cmdlet successfully completes, you should see an output listing hello cluster details.</span></span>


## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a><span data-ttu-id="f9bee-195">Запуск тестовых заданий в hello HDInsight кластера toouse hello хранилища Озера данных</span><span class="sxs-lookup"><span data-stu-id="f9bee-195">Run test jobs on hello HDInsight cluster toouse hello Data Lake Store</span></span>
<span data-ttu-id="f9bee-196">После настройки кластера HDInsight можно запускать тестовые задания на tootest кластера hello, hello HDInsight кластера можно получить доступ к хранилищу Озера данных.</span><span class="sxs-lookup"><span data-stu-id="f9bee-196">After you have configured an HDInsight cluster, you can run test jobs on hello cluster tootest that hello HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="f9bee-197">toodo таким образом, будет выполняться задание куста образец, создающий таблицу, используя данные образца hello, отправленный хранилища Озера данных более ранних tooyour.</span><span class="sxs-lookup"><span data-stu-id="f9bee-197">toodo so, we will run a sample Hive job that creates a table using hello sample data that you uploaded earlier tooyour Data Lake Store.</span></span>

<span data-ttu-id="f9bee-198">В этом разделе будет SSH в HDInsight Linux кластер был создан и выполнения запроса Hive образец hello hello.</span><span class="sxs-lookup"><span data-stu-id="f9bee-198">In this section you will SSH into hello HDInsight Linux cluster you created and run hello a sample Hive query.</span></span>

* <span data-ttu-id="f9bee-199">При использовании клиента Windows tooSSH в кластер hello. в разделе [использование SSH с Linux-based Hadoop в HDInsight из Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="f9bee-199">If you are using a Windows client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="f9bee-200">При использовании tooSSH клиента Linux в кластер hello. в разделе [использование SSH с Linux-based Hadoop в HDInsight в Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="f9bee-200">If you are using a Linux client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

1. <span data-ttu-id="f9bee-201">После установления соединения, запустите hello Hive CLI с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f9bee-201">Once connected, start hello Hive CLI by using hello following command:</span></span>

        hive
2. <span data-ttu-id="f9bee-202">С помощью hello (CLI), введите следующие инструкции toocreate новую таблицу с именем hello **автомобилей** , используя данные образца hello hello хранилища Озера данных:</span><span class="sxs-lookup"><span data-stu-id="f9bee-202">Using hello CLI, enter hello following statements toocreate a new table named **vehicles** by using hello sample data in hello Data Lake Store:</span></span>

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    <span data-ttu-id="f9bee-203">Вы должны увидеть следующие выходные данные как toohello.</span><span class="sxs-lookup"><span data-stu-id="f9bee-203">You should see an output similar toohello following:</span></span>

        1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
        1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
        1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
        1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
        1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
        1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
        1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
        1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
        1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
        1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1

## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="f9bee-204">Доступ к хранилищу озера данных с помощью команд HDFS</span><span class="sxs-lookup"><span data-stu-id="f9bee-204">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="f9bee-205">После настройки хранилища Озера данных toouse кластера HDInsight hello hello HDFS оболочки команды tooaccess hello хранилища можно использовать.</span><span class="sxs-lookup"><span data-stu-id="f9bee-205">Once you have configured hello HDInsight cluster toouse Data Lake Store, you can use hello HDFS shell commands tooaccess hello store.</span></span>

<span data-ttu-id="f9bee-206">В этом разделе будет SSH в HDInsight Linux кластер был создан и выполнения команд HDFS hello hello.</span><span class="sxs-lookup"><span data-stu-id="f9bee-206">In this section you will SSH into hello HDInsight Linux cluster you created and run hello HDFS commands.</span></span>

* <span data-ttu-id="f9bee-207">При использовании клиента Windows tooSSH в кластер hello. в разделе [использование SSH с Linux-based Hadoop в HDInsight из Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="f9bee-207">If you are using a Windows client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="f9bee-208">При использовании tooSSH клиента Linux в кластер hello. в разделе [использование SSH с Linux-based Hadoop в HDInsight в Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="f9bee-208">If you are using a Linux client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

<span data-ttu-id="f9bee-209">После подключения, используйте следующие файлы hello toolist команды файловой системы HDFS в хранилище Озера данных hello hello.</span><span class="sxs-lookup"><span data-stu-id="f9bee-209">Once connected, use hello following HDFS filesystem command toolist hello files in hello Data Lake Store.</span></span>

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

<span data-ttu-id="f9bee-210">Должен быть выведен список hello файл, отправленный хранилища Озера данных более ранних toohello.</span><span class="sxs-lookup"><span data-stu-id="f9bee-210">This should list hello file that you uploaded earlier toohello Data Lake Store.</span></span>

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

<span data-ttu-id="f9bee-211">Можно также использовать hello `hdfs dfs -put` команды tooupload toohello некоторые файлы хранилища Озера данных, а затем используйте `hdfs dfs -ls` tooverify ли hello файлы были успешно отправлены.</span><span class="sxs-lookup"><span data-stu-id="f9bee-211">You can also use hello `hdfs dfs -put` command tooupload some files toohello Data Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="f9bee-212">См. также</span><span class="sxs-lookup"><span data-stu-id="f9bee-212">See Also</span></span>
* [<span data-ttu-id="f9bee-213">Портал: Создание toouse кластера HDInsight хранилища Озера данных</span><span class="sxs-lookup"><span data-stu-id="f9bee-213">Portal: Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
