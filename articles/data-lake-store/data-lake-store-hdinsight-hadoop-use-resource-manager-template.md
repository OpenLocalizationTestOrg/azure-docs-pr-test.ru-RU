---
title: "Создание HDInsight и Data Lake Store с помощью шаблонов Azure | Документация Майкрософт"
description: "Создание кластеров HDInsight для работы с Azure Data Lake Store с помощью шаблонов Azure Resource Manager"
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
ms.openlocfilehash: 6f43423096f0e74f41afea275e4ec9801dc2cea5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a><span data-ttu-id="5c9d3-103">Создание кластера HDInsight с Data Lake Store с помощью шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5c9d3-103">Create an HDInsight cluster with Data Lake Store using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5c9d3-104">Использование портала</span><span class="sxs-lookup"><span data-stu-id="5c9d3-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="5c9d3-105">Использование PowerShell (для хранилища по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="5c9d3-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="5c9d3-106">Использование PowerShell (для дополнительного хранилища)</span><span class="sxs-lookup"><span data-stu-id="5c9d3-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="5c9d3-107">Использование Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5c9d3-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="5c9d3-108">Узнайте, как с помощью Azure PowerShell настроить кластер HDInsight с Azure Data Lake Store в качестве **дополнительного хранилища**.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-108">Learn how to use Azure PowerShell to configure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span>

<span data-ttu-id="5c9d3-109">В поддерживаемых типах кластеров Data Lake Store можно использовать в качестве хранилища по умолчанию или дополнительной учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-109">For supported cluster types, Data Lake Store be used as an default storage or additional storage account.</span></span> <span data-ttu-id="5c9d3-110">Если Data Lake Store используется как дополнительное хранилище, в этом случае в качестве учетной записи хранения по умолчанию для кластеров по-прежнему используется Azure Storage Blob (WASB). Кроме того, относящиеся к кластеру файлы (журналы и т. д.) записываются в хранилище по умолчанию, а данные, которые необходимо обработать, могут храниться в учетной записи Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-110">When Data Lake Store is used as additional storage, the default storage account for the clusters will still be Azure Storage Blobs (WASB) and the cluster-related files (such as logs, etc.) are still written to the default storage, while the data that you want to process can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="5c9d3-111">Использование хранилища озера данных в качестве дополнительной учетной записи хранения не влияет на производительность или возможность выполнять чтение и запись в хранилище из кластера.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-111">Using Data Lake Store as an additional storage account does not impact performance or the ability to read/write to the storage from the cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="5c9d3-112">Использование Data Lake Store в качестве хранилища кластера HDInsight</span><span class="sxs-lookup"><span data-stu-id="5c9d3-112">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="5c9d3-113">Ниже приведены некоторые важные сведения об использовании HDInsight с Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-113">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="5c9d3-114">Возможность создавать кластеры HDInsight с доступом к Data Lake Store в качестве хранилища по умолчанию поддерживается в HDInsight версий 3.5 и 3.6.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-114">Option to create HDInsight clusters with access to Data Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="5c9d3-115">Возможность создавать кластеры HDInsight с доступом к Data Lake Store в качестве дополнительного хранилища поддерживается в HDInsight версий 3.2, 3.4, 3.5 и 3.6.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-115">Option to create HDInsight clusters with access to Data Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="5c9d3-116">В этой статье мы подготовим кластер Hadoop, в котором хранилище озера данных будет дополнительным хранилищем.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-116">In this article, we provision a Hadoop cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="5c9d3-117">Инструкции по созданию кластера Hadoop с Data Lake Store в качестве хранилища по умолчанию см. в статье [Создание кластера HDInsight с Data Lake Store с помощью портала Azure](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5c9d3-117">For instructions on how to create a Hadoop cluster with Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c9d3-118">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5c9d3-118">Prerequisites</span></span>
<span data-ttu-id="5c9d3-119">Перед началом работы с этим учебником необходимо иметь следующее:</span><span class="sxs-lookup"><span data-stu-id="5c9d3-119">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="5c9d3-120">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-120">**An Azure subscription**.</span></span> <span data-ttu-id="5c9d3-121">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5c9d3-121">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5c9d3-122">**Azure PowerShell 1.0 или более поздней версии**.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-122">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="5c9d3-123">Ознакомьтесь со статьей [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5c9d3-123">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="5c9d3-124">**Субъект-служба Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-124">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="5c9d3-125">В этом учебнике приведены инструкции по созданию субъекта-службы в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-125">Steps in this tutorial provide instructions on how to create a service principal in Azure AD.</span></span> <span data-ttu-id="5c9d3-126">Однако, чтобы создать субъект-службу, необходимо быть администратором Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-126">However, you must be an Azure AD administrator to be able to create a service principal.</span></span> <span data-ttu-id="5c9d3-127">Если вы являетесь администратором Azure AD, то можете пропустить это предварительное требование и продолжить работу с учебником.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-127">If you are an Azure AD administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    <span data-ttu-id="5c9d3-128">**Если вы не являетесь администратором Azure AD**, то вы не сможете выполнить шаги, необходимые для создания субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-128">**If you are not an Azure AD administrator**, you will not be able to perform the steps required to create a service principal.</span></span> <span data-ttu-id="5c9d3-129">В этом случае администратор Azure AD должен сначала создать субъект-службу, после чего вы сможете создать кластер HDInsight с Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-129">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="5c9d3-130">При создании субъекта-службы также необходимо использовать сертификат, как описано в разделе [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority) (Создание субъекта-службы с сертификатом).</span><span class="sxs-lookup"><span data-stu-id="5c9d3-130">Also, the service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a><span data-ttu-id="5c9d3-131">Создание кластера HDInsight с помощью Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5c9d3-131">Create an HDInsight cluster with Azure Data Lake Store</span></span>
<span data-ttu-id="5c9d3-132">Шаблон Resource Manager и предварительные требования для использования шаблона см. в статье [Deploy a HDInsight Linux cluster with new Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage) (Развертывание кластера HDInsight Linux с помощью нового хранилища Data Lake Store) на GitHub.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-132">The Resource Manager template, and the prerequisites for using the template, are available on GitHub at [Deploy a HDInsight Linux cluster with new Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span></span> <span data-ttu-id="5c9d3-133">Следуйте инструкциям по этой ссылке, чтобы создать кластер HDInsight с Azure Data Lake Store в качестве дополнительного хранилища.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-133">Follow the instructions provided at this link to create an HDInsight cluster with Azure Data Lake Store as the additional storage.</span></span>

<span data-ttu-id="5c9d3-134">Инструкции по ссылке выше требуют PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-134">The instructions at the link mentioned above require PowerShell.</span></span> <span data-ttu-id="5c9d3-135">Прежде чем начать работу с ними, обязательно войдите в учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-135">Before you start with those instructions, make sure you log in to your Azure account.</span></span> <span data-ttu-id="5c9d3-136">На своем компьютере откройте новое окно Azure PowerShell и введите следующий фрагмент кода.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-136">From your desktop, open a new Azure PowerShell window, and enter the following snippets.</span></span> <span data-ttu-id="5c9d3-137">Когда вам будет предложено войти, введите учетные данные администратора или владельца подписки.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-137">When prompted to log in, make sure you log in as one of the subscription admininistrators/owner:</span></span>

```
# Log in to your Azure account
Login-AzureRmAccount

# List all the subscriptions associated to your account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-to-the-azure-data-lake-store"></a><span data-ttu-id="5c9d3-138">Отправка примера данных в Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5c9d3-138">Upload sample data to the Azure Data Lake Store</span></span>
<span data-ttu-id="5c9d3-139">Шаблон Resource Manager создает новую учетную запись Data Lake Store и связывает ее с кластером HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-139">The Resource Manager template creates a new Data Lake Store account and associates it with the HDInsight cluster.</span></span> <span data-ttu-id="5c9d3-140">Отправьте пример данных в Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-140">You must now upload some sample data to the Data Lake Store.</span></span> <span data-ttu-id="5c9d3-141">Эти данные потребуются позже при выполнении заданий из кластера HDInsight для получения доступа к данным в хранилище озера данных.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-141">You'll need this data later in the tutorial to run jobs from an HDInsight cluster that access data in the Data Lake Store.</span></span> <span data-ttu-id="5c9d3-142">Указания по отправке данных см. в разделе [Отправка файла в Data Lake Store](data-lake-store-get-started-portal.md#uploaddata).</span><span class="sxs-lookup"><span data-stu-id="5c9d3-142">For instructions on how to upload data, see [Upload a file to your Data Lake Store](data-lake-store-get-started-portal.md#uploaddata).</span></span> <span data-ttu-id="5c9d3-143">Если у вас нет под рукой подходящих для этих целей данных, передайте папку **Ambulance Data** из [репозитория Git для озера данных Azure](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="5c9d3-143">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

## <a name="set-relevant-acls-on-the-sample-data"></a><span data-ttu-id="5c9d3-144">Установка соответствующих списков управления доступом для примера данных</span><span class="sxs-lookup"><span data-stu-id="5c9d3-144">Set relevant ACLs on the sample data</span></span>
<span data-ttu-id="5c9d3-145">Чтобы обеспечить доступ к отправляемым примерам данных для кластера HDInsight, необходимо убедиться, что у приложения Azure AD, используемого для определения удостоверения между кластером HDInsight и Data Lake Store, есть доступ к файлу или папке, к которой вы пытаетесь получить доступ.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-145">To make sure the sample data you upload is accessible from the HDInsight cluster, you must ensure that the Azure AD application that is used to establish identity between the HDInsight cluster and Data Lake Store has access to the file/folder you are trying to access.</span></span> <span data-ttu-id="5c9d3-146">Для этого сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-146">To do this, perform the following steps.</span></span>

1. <span data-ttu-id="5c9d3-147">Найдите имя приложения Azure AD, связанного с кластером HDInsight и Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-147">Find the name of the Azure AD application that is associated with HDInsight cluster and the Data Lake Store.</span></span> <span data-ttu-id="5c9d3-148">Чтобы найти его, можно открыть колонку кластера HDInsight, созданного с помощью шаблона Resource Manager, выбрать вкладку **Удостоверение кластера AAD** и просмотреть значение параметра **Service Principal Display Name** (Отображаемое имя субъекта-службы).</span><span class="sxs-lookup"><span data-stu-id="5c9d3-148">One way to look for the name is to open the HDInsight cluster blade that you created using the Resource Manager template, click the **Cluster AAD Identity** tab, and look for the value of **Service Principal Display Name**.</span></span>
2. <span data-ttu-id="5c9d3-149">Теперь предоставьте этому приложению Azure AD доступ к файлу или папке, к которым необходимо получить доступ из кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-149">Now, provide access to this Azure AD application on the file/folder that you want to access from the HDInsight cluster.</span></span> <span data-ttu-id="5c9d3-150">Чтобы установить подходящие списки управления доступом для файла или папки в Data Lake Store, см. статью [Защита данных, хранимых в хранилище озера данных](data-lake-store-secure-data.md#filepermissions).</span><span class="sxs-lookup"><span data-stu-id="5c9d3-150">To set the right ACLs on the file/folder in Data Lake Store, see [Securing data in Data Lake Store](data-lake-store-secure-data.md#filepermissions).</span></span>

## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-the-data-lake-store"></a><span data-ttu-id="5c9d3-151">Выполнение тестовых заданий в кластере HDInsight</span><span class="sxs-lookup"><span data-stu-id="5c9d3-151">Run test jobs on the HDInsight cluster to use the Data Lake Store</span></span>
<span data-ttu-id="5c9d3-152">После настройки кластера HDInsight выполните в нем тестовые задания, чтобы проверить, доступно ли ему хранилище озера данных.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-152">After you have configured an HDInsight cluster, you can run test jobs on the cluster to test that the HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="5c9d3-153">Для этого запустите образец задания Hive, создающего таблицу с данными, которые вы ранее отправили в хранилище озера данных.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-153">To do so, we will run a sample Hive job that creates a table using the sample data that you uploaded earlier to your Data Lake Store.</span></span>

<span data-ttu-id="5c9d3-154">В этом разделе вы подключитесь к кластеру HDInsight на платформе Linux по протоколу SSH и выполните пример запроса Hive.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-154">In this section you will SSH into an HDInsight Linux cluster and run the a sample Hive query.</span></span> <span data-ttu-id="5c9d3-155">Если вы работаете с клиентом Windows, рекомендуется использовать **PuTTY**, который можно скачать по адресу: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="5c9d3-155">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="5c9d3-156">Дополнительные сведения об использовании PuTTY см. в разделе [Использование SSH с Hadoop на основе Linux в HDInsight из Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="5c9d3-156">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

1. <span data-ttu-id="5c9d3-157">После подключения запустите интерфейс командной строки Hive с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="5c9d3-157">Once connected, start the Hive CLI by using the following command:</span></span>

   ```
   hive
   ```
2. <span data-ttu-id="5c9d3-158">Используя интерфейс командной строки, введите следующие инструкции, чтобы создать таблицу с именем **vehicles** с помощью примера данных в хранилище озера данных.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-158">Using the CLI, enter the following statements to create a new table named **vehicles** by using the sample data in the Data Lake Store:</span></span>

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   <span data-ttu-id="5c9d3-159">Должен отобразиться результат, аналогичный приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="5c9d3-159">You should see an output similar to the following:</span></span>

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


## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="5c9d3-160">Доступ к хранилищу озера данных с помощью команд HDFS</span><span class="sxs-lookup"><span data-stu-id="5c9d3-160">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="5c9d3-161">Настроив в кластере HDInsight параметры для работы с хранилищем озера данных, используйте для доступа к хранилищу команды оболочки HDFS.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-161">Once you have configured the HDInsight cluster to use Data Lake Store, you can use the HDFS shell commands to access the store.</span></span>

<span data-ttu-id="5c9d3-162">В этом разделе вы подключитесь к кластеру HDInsight на платформе Linux по протоколу SSH и выполните команды HDFS.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-162">In this section you will SSH into an HDInsight Linux cluster and run the HDFS commands.</span></span> <span data-ttu-id="5c9d3-163">Если вы работаете с клиентом Windows, рекомендуется использовать **PuTTY**, который можно скачать по адресу: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="5c9d3-163">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="5c9d3-164">Дополнительные сведения об использовании PuTTY см. в разделе [Использование SSH с Hadoop на основе Linux в HDInsight из Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="5c9d3-164">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

<span data-ttu-id="5c9d3-165">После подключения используйте следующую команду файловой системы HDFS для получения списка файлов в хранилище озера данных.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-165">Once connected, use the following HDFS filesystem command to list the files in the Data Lake Store.</span></span>

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

<span data-ttu-id="5c9d3-166">Эта команда должна показать файл, который вы ранее отправили в хранилище озера данных.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-166">This should list the file that you uploaded earlier to the Data Lake Store.</span></span>

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

<span data-ttu-id="5c9d3-167">С помощью команды `hdfs dfs -put` вы можете отправить в хранилище озера данных некоторые файлы, а затем с помощью команды `hdfs dfs -ls` проверить, успешно ли они передались.</span><span class="sxs-lookup"><span data-stu-id="5c9d3-167">You can also use the `hdfs dfs -put` command to upload some files to the Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5c9d3-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5c9d3-168">Next steps</span></span>
* [<span data-ttu-id="5c9d3-169">Копирование данных из больших двоичных объектов службы хранилища Azure в Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="5c9d3-169">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-wasb-distcp.md)
