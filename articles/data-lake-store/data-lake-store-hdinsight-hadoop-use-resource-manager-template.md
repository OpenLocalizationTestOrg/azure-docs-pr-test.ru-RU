---
title: "toocreate aaaUse шаблоны Azure HDInsight и хранилище Озера данных | Документы Microsoft"
description: "Использовать toocreate шаблонов диспетчера ресурсов Azure и использовать кластеров HDInsight в хранилище Озера данных Azure"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8ef8152f-2121-461e-956c-51c55144919d
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: nitinme
ms.openlocfilehash: eb88a626f2837dcc29295f3f73a91757059c3bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a><span data-ttu-id="1a062-103">Создание кластера HDInsight с Data Lake Store с помощью шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1a062-103">Create an HDInsight cluster with Data Lake Store using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1a062-104">Использование портала</span><span class="sxs-lookup"><span data-stu-id="1a062-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="1a062-105">Использование PowerShell (для хранилища по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="1a062-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="1a062-106">Использование PowerShell (для дополнительного хранилища)</span><span class="sxs-lookup"><span data-stu-id="1a062-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="1a062-107">Использование Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1a062-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="1a062-108">Узнайте, как tooconfigure toouse Azure PowerShell HDInsight кластер с хранилища Озера данных Azure, **как дополнительное хранилище**.</span><span class="sxs-lookup"><span data-stu-id="1a062-108">Learn how toouse Azure PowerShell tooconfigure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span>

<span data-ttu-id="1a062-109">В поддерживаемых типах кластеров Data Lake Store можно использовать в качестве хранилища по умолчанию или дополнительной учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="1a062-109">For supported cluster types, Data Lake Store be used as an default storage or additional storage account.</span></span> <span data-ttu-id="1a062-110">При использовании хранилища Озера данных как дополнительное хранилище hello учетной записи хранения по умолчанию для кластеров hello по-прежнему будут хранилища больших двоичных объектов Azure (WASB) и hello кластера файлов (например, журналы, т. д.) по-прежнему записываются toohello хранилища по умолчанию, при hello данных, которые необходимо tooprocess могут храниться в учетной записи хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="1a062-110">When Data Lake Store is used as additional storage, hello default storage account for hello clusters will still be Azure Storage Blobs (WASB) and hello cluster-related files (such as logs, etc.) are still written toohello default storage, while hello data that you want tooprocess can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="1a062-111">С помощью хранилища Озера данных от имени учетной записи дополнительное хранилище не влияет на производительность и работу хранилища toohello hello возможность tooread и записи из кластера hello.</span><span class="sxs-lookup"><span data-stu-id="1a062-111">Using Data Lake Store as an additional storage account does not impact performance or hello ability tooread/write toohello storage from hello cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="1a062-112">Использование Data Lake Store в качестве хранилища кластера HDInsight</span><span class="sxs-lookup"><span data-stu-id="1a062-112">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="1a062-113">Ниже приведены некоторые важные сведения об использовании HDInsight с Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1a062-113">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="1a062-114">Кластеры HDInsight toocreate параметр с доступом хранилища Озера tooData хранения по умолчанию доступна для HDInsight версии 3.5 и 3.6.</span><span class="sxs-lookup"><span data-stu-id="1a062-114">Option toocreate HDInsight clusters with access tooData Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="1a062-115">Кластеры HDInsight toocreate параметр с доступом хранилища Озера tooData как дополнительное хранилище доступно для HDInsight версии 3.2, 3.4, 3.5 и 3.6.</span><span class="sxs-lookup"><span data-stu-id="1a062-115">Option toocreate HDInsight clusters with access tooData Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="1a062-116">В этой статье мы подготовим кластер Hadoop, в котором хранилище озера данных будет дополнительным хранилищем.</span><span class="sxs-lookup"><span data-stu-id="1a062-116">In this article, we provision a Hadoop cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="1a062-117">Инструкции как toocreate Hadoop кластер с хранилища Озера данных в качестве хранилища по умолчанию см. в разделе [создать кластер HDInsight в хранилище Озера данных с помощью портала Azure](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1a062-117">For instructions on how toocreate a Hadoop cluster with Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a062-118">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1a062-118">Prerequisites</span></span>
<span data-ttu-id="1a062-119">Прежде чем начать работу с учебником, необходимо иметь следующие hello.</span><span class="sxs-lookup"><span data-stu-id="1a062-119">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="1a062-120">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="1a062-120">**An Azure subscription**.</span></span> <span data-ttu-id="1a062-121">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1a062-121">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="1a062-122">**Azure PowerShell 1.0 или более поздней версии**.</span><span class="sxs-lookup"><span data-stu-id="1a062-122">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="1a062-123">В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1a062-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="1a062-124">**Субъект-служба Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1a062-124">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="1a062-125">В этом учебнике приведены инструкции о том, как toocreate участника службы в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a062-125">Steps in this tutorial provide instructions on how toocreate a service principal in Azure AD.</span></span> <span data-ttu-id="1a062-126">Тем не менее необходимо быть toocreate toobe может субъекта-службы администрирования Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a062-126">However, you must be an Azure AD administrator toobe able toocreate a service principal.</span></span> <span data-ttu-id="1a062-127">Если вы являетесь администратором Azure AD, можно пропустить это предварительное условие и продолжить работу с учебником hello.</span><span class="sxs-lookup"><span data-stu-id="1a062-127">If you are an Azure AD administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    <span data-ttu-id="1a062-128">**Если вы не являетесь администратором Azure AD**, не будет возможности tooperform hello действия требуется toocreate участника службы.</span><span class="sxs-lookup"><span data-stu-id="1a062-128">**If you are not an Azure AD administrator**, you will not be able tooperform hello steps required toocreate a service principal.</span></span> <span data-ttu-id="1a062-129">В этом случае администратор Azure AD должен сначала создать субъект-службу, после чего вы сможете создать кластер HDInsight с Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1a062-129">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="1a062-130">Кроме того, hello участника-службы должны создаваться с помощью сертификата, как описано в разделе [создании участника службы с сертификатом](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="1a062-130">Also, hello service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a><span data-ttu-id="1a062-131">Создание кластера HDInsight с помощью Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1a062-131">Create an HDInsight cluster with Azure Data Lake Store</span></span>
<span data-ttu-id="1a062-132">Hello шаблона диспетчера ресурсов и hello предварительные требования для использования шаблона hello, можно найти на github на сайте [развертывания кластера HDInsight Linux с помощью нового хранилища Озера данных](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="1a062-132">hello Resource Manager template, and hello prerequisites for using hello template, are available on GitHub at [Deploy a HDInsight Linux cluster with new Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span></span> <span data-ttu-id="1a062-133">Выполните hello инструкций, приведенных в этой связи toocreate кластер HDInsight с хранилища Озера данных Azure как дополнительное хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="1a062-133">Follow hello instructions provided at this link toocreate an HDInsight cluster with Azure Data Lake Store as hello additional storage.</span></span>

<span data-ttu-id="1a062-134">Hello инструкциям по ссылке hello вышеупомянутых требуются PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1a062-134">hello instructions at hello link mentioned above require PowerShell.</span></span> <span data-ttu-id="1a062-135">Прежде чем начать с этих инструкций, убедитесь, что вход tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="1a062-135">Before you start with those instructions, make sure you log in tooyour Azure account.</span></span> <span data-ttu-id="1a062-136">С рабочего стола откройте новое окно Azure PowerShell и введите следующие фрагменты кода hello.</span><span class="sxs-lookup"><span data-stu-id="1a062-136">From your desktop, open a new Azure PowerShell window, and enter hello following snippets.</span></span> <span data-ttu-id="1a062-137">При toolog запрос, убедитесь, что войти в систему один hello admininistrators/владелец подписки:</span><span class="sxs-lookup"><span data-stu-id="1a062-137">When prompted toolog in, make sure you log in as one of hello subscription admininistrators/owner:</span></span>

```
# Log in tooyour Azure account
Login-AzureRmAccount

# List all hello subscriptions associated tooyour account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-toohello-azure-data-lake-store"></a><span data-ttu-id="1a062-138">Отправка хранилища Озера данных Azure toohello образца данных</span><span class="sxs-lookup"><span data-stu-id="1a062-138">Upload sample data toohello Azure Data Lake Store</span></span>
<span data-ttu-id="1a062-139">шаблон диспетчера ресурсов Hello создает новую учетную запись хранилища Озера данных и связывает его с кластером HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="1a062-139">hello Resource Manager template creates a new Data Lake Store account and associates it with hello HDInsight cluster.</span></span> <span data-ttu-id="1a062-140">Теперь необходимо отправить некоторые toohello данных образец хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="1a062-140">You must now upload some sample data toohello Data Lake Store.</span></span> <span data-ttu-id="1a062-141">Вам потребуется позже в заданий учебника toorun hello из кластера HDInsight, доступа к данным в хранилище Озера данных hello эти данные.</span><span class="sxs-lookup"><span data-stu-id="1a062-141">You'll need this data later in hello tutorial toorun jobs from an HDInsight cluster that access data in hello Data Lake Store.</span></span> <span data-ttu-id="1a062-142">Дополнительные сведения о данных tooupload см. [отправить файл tooyour хранилища Озера данных](data-lake-store-get-started-portal.md#uploaddata).</span><span class="sxs-lookup"><span data-stu-id="1a062-142">For instructions on how tooupload data, see [Upload a file tooyour Data Lake Store](data-lake-store-get-started-portal.md#uploaddata).</span></span> <span data-ttu-id="1a062-143">Если вы ищете некоторые tooupload образец данных, вы можете получить hello **скорая помощь данных** папку из hello [репозитории Озера данных Azure](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="1a062-143">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

## <a name="set-relevant-acls-on-hello-sample-data"></a><span data-ttu-id="1a062-144">Установите соответствующие разрешения на hello образец данных</span><span class="sxs-lookup"><span data-stu-id="1a062-144">Set relevant ACLs on hello sample data</span></span>
<span data-ttu-id="1a062-145">toomake убедиться, что данные образца hello, загруженными доступен с кластера HDInsight hello, необходимо убедиться, приложение hello Azure AD, удостоверения используемый tooestablish между кластером HDInsight hello и хранилище Озера данных имеет доступ toohello файла или папки, которые Этот tooaccess.</span><span class="sxs-lookup"><span data-stu-id="1a062-145">toomake sure hello sample data you upload is accessible from hello HDInsight cluster, you must ensure that hello Azure AD application that is used tooestablish identity between hello HDInsight cluster and Data Lake Store has access toohello file/folder you are trying tooaccess.</span></span> <span data-ttu-id="1a062-146">toodo это, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="1a062-146">toodo this, perform hello following steps.</span></span>

1. <span data-ttu-id="1a062-147">Найти имя hello hello приложения Azure AD, которая связана с кластером HDInsight и hello хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="1a062-147">Find hello name of hello Azure AD application that is associated with HDInsight cluster and hello Data Lake Store.</span></span> <span data-ttu-id="1a062-148">Одним из способов toolook имени hello tooopen hello HDInsight кластера колонки, созданные с помощью шаблона диспетчера ресурсов hello, нажмите кнопку hello **удостоверение кластера AAD** и найдите значение hello **участника-службы Отображаемое имя**.</span><span class="sxs-lookup"><span data-stu-id="1a062-148">One way toolook for hello name is tooopen hello HDInsight cluster blade that you created using hello Resource Manager template, click hello **Cluster AAD Identity** tab, and look for hello value of **Service Principal Display Name**.</span></span>
2. <span data-ttu-id="1a062-149">Теперь предоставляют доступ toothis приложения Azure AD в hello файл или папку, которые должны tooaccess из кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="1a062-149">Now, provide access toothis Azure AD application on hello file/folder that you want tooaccess from hello HDInsight cluster.</span></span> <span data-ttu-id="1a062-150">право hello tooset списки управления доступом на hello файл или папку в хранилище Озера данных, см. [защиты данных в хранилище Озера данных](data-lake-store-secure-data.md#filepermissions).</span><span class="sxs-lookup"><span data-stu-id="1a062-150">tooset hello right ACLs on hello file/folder in Data Lake Store, see [Securing data in Data Lake Store](data-lake-store-secure-data.md#filepermissions).</span></span>

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a><span data-ttu-id="1a062-151">Запуск тестовых заданий в hello HDInsight кластера toouse hello хранилища Озера данных</span><span class="sxs-lookup"><span data-stu-id="1a062-151">Run test jobs on hello HDInsight cluster toouse hello Data Lake Store</span></span>
<span data-ttu-id="1a062-152">После настройки кластера HDInsight можно запускать тестовые задания на tootest кластера hello, hello HDInsight кластера можно получить доступ к хранилищу Озера данных.</span><span class="sxs-lookup"><span data-stu-id="1a062-152">After you have configured an HDInsight cluster, you can run test jobs on hello cluster tootest that hello HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="1a062-153">toodo таким образом, будет выполняться задание куста образец, создающий таблицу, используя данные образца hello, отправленный хранилища Озера данных более ранних tooyour.</span><span class="sxs-lookup"><span data-stu-id="1a062-153">toodo so, we will run a sample Hive job that creates a table using hello sample data that you uploaded earlier tooyour Data Lake Store.</span></span>

<span data-ttu-id="1a062-154">В этом разделе вы будете SSH в кластере HDInsight Linux и выполнения hello образец запроса Hive.</span><span class="sxs-lookup"><span data-stu-id="1a062-154">In this section you will SSH into an HDInsight Linux cluster and run hello a sample Hive query.</span></span> <span data-ttu-id="1a062-155">Если вы работаете с клиентом Windows, рекомендуется использовать **PuTTY**, который можно скачать по адресу: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="1a062-155">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="1a062-156">Дополнительные сведения об использовании PuTTY см. в разделе [Использование SSH с Hadoop на основе Linux в HDInsight из Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="1a062-156">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

1. <span data-ttu-id="1a062-157">После установления соединения, запустите hello Hive CLI с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="1a062-157">Once connected, start hello Hive CLI by using hello following command:</span></span>

   ```
   hive
   ```
2. <span data-ttu-id="1a062-158">С помощью hello (CLI), введите следующие инструкции toocreate новую таблицу с именем hello **автомобилей** , используя данные образца hello hello хранилища Озера данных:</span><span class="sxs-lookup"><span data-stu-id="1a062-158">Using hello CLI, enter hello following statements toocreate a new table named **vehicles** by using hello sample data in hello Data Lake Store:</span></span>

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   <span data-ttu-id="1a062-159">Вы должны увидеть следующие выходные данные как toohello.</span><span class="sxs-lookup"><span data-stu-id="1a062-159">You should see an output similar toohello following:</span></span>

   ```
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
   ```


## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="1a062-160">Доступ к хранилищу озера данных с помощью команд HDFS</span><span class="sxs-lookup"><span data-stu-id="1a062-160">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="1a062-161">После настройки хранилища Озера данных toouse кластера HDInsight hello hello HDFS оболочки команды tooaccess hello хранилища можно использовать.</span><span class="sxs-lookup"><span data-stu-id="1a062-161">Once you have configured hello HDInsight cluster toouse Data Lake Store, you can use hello HDFS shell commands tooaccess hello store.</span></span>

<span data-ttu-id="1a062-162">В этом разделе вы будете SSH в кластере HDInsight Linux и выполнения hello команды HDFS.</span><span class="sxs-lookup"><span data-stu-id="1a062-162">In this section you will SSH into an HDInsight Linux cluster and run hello HDFS commands.</span></span> <span data-ttu-id="1a062-163">Если вы работаете с клиентом Windows, рекомендуется использовать **PuTTY**, который можно скачать по адресу: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="1a062-163">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="1a062-164">Дополнительные сведения об использовании PuTTY см. в разделе [Использование SSH с Hadoop на основе Linux в HDInsight из Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="1a062-164">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

<span data-ttu-id="1a062-165">После подключения, используйте следующие файлы hello toolist команды файловой системы HDFS в хранилище Озера данных hello hello.</span><span class="sxs-lookup"><span data-stu-id="1a062-165">Once connected, use hello following HDFS filesystem command toolist hello files in hello Data Lake Store.</span></span>

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

<span data-ttu-id="1a062-166">Должен быть выведен список hello файл, отправленный хранилища Озера данных более ранних toohello.</span><span class="sxs-lookup"><span data-stu-id="1a062-166">This should list hello file that you uploaded earlier toohello Data Lake Store.</span></span>

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

<span data-ttu-id="1a062-167">Можно также использовать hello `hdfs dfs -put` команды tooupload toohello некоторые файлы хранилища Озера данных, а затем используйте `hdfs dfs -ls` tooverify ли hello файлы были успешно отправлены.</span><span class="sxs-lookup"><span data-stu-id="1a062-167">You can also use hello `hdfs dfs -put` command tooupload some files toohello Data Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1a062-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1a062-168">Next steps</span></span>
* [<span data-ttu-id="1a062-169">Копирование данных из хранилища Озера tooData больших двоичных объектов хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="1a062-169">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-wasb-distcp.md)
