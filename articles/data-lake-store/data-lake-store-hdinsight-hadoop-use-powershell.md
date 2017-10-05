---
title: "PowerShell: кластер Azure HDInsight с Data Lake Store в качестве дополнительного хранилища | Документация Майкрософт"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 164ada5a-222e-4be2-bd32-e51dbe993bc0
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/08/2017
ms.author: nitinme
ms.openlocfilehash: 7a7069adab5742a9dae2833c13a1db57337a41a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-powershell-to-create-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="df206-102">Создание кластера HDInsight с Data Lake Store (как дополнительное хранилище) с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="df206-102">Use Azure PowerShell to create an HDInsight cluster with Data Lake Store (as additional storage)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="df206-103">Использование портала</span><span class="sxs-lookup"><span data-stu-id="df206-103">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="df206-104">Использование PowerShell (для хранилища по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="df206-104">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="df206-105">Использование PowerShell (для дополнительного хранилища)</span><span class="sxs-lookup"><span data-stu-id="df206-105">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="df206-106">Использование Resource Manager</span><span class="sxs-lookup"><span data-stu-id="df206-106">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="df206-107">Узнайте, как с помощью Azure PowerShell настроить кластер HDInsight с Azure Data Lake Store в качестве **дополнительного хранилища**.</span><span class="sxs-lookup"><span data-stu-id="df206-107">Learn how to use Azure PowerShell to configure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span> <span data-ttu-id="df206-108">Инструкции по созданию кластера HDInsight с Data Lake Store в качестве хранилища по умолчанию см. в статье [Создание кластера HDInsight с Data Lake Store (как хранилище по умолчанию) с помощью Azure PowerShell](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span><span class="sxs-lookup"><span data-stu-id="df206-108">For instructions on how to create an HDInsight cluster with Azure Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store as default storage](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span></span>

> [!NOTE]
> <span data-ttu-id="df206-109">Если вы собираетесь добавить Azure Data Lake Store в качестве дополнительного хранилища для кластера HDInsight, настоятельно рекомендуется сделать это во время создания кластера, как описано в этой статье.</span><span class="sxs-lookup"><span data-stu-id="df206-109">If you are going to use Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create the cluster as described in this article.</span></span> <span data-ttu-id="df206-110">Добавление Azure Data Lake Store в качестве дополнительного хранилища для существующего кластера HDInsight — очень сложный процесс, который может привести к ошибкам.</span><span class="sxs-lookup"><span data-stu-id="df206-110">Adding Azure Data Lake Store as additional storage to an existing HDInsight cluster is a complicated process and prone to errors.</span></span>
>

<span data-ttu-id="df206-111">В поддерживаемых типах кластеров Data Lake Store можно использовать в качестве хранилища по умолчанию или дополнительной учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="df206-111">For supported cluster types, Data Lake Store can be used as a default storage or additional storage account.</span></span> <span data-ttu-id="df206-112">Если Data Lake Store используется как дополнительное хранилище, в этом случае в качестве учетной записи хранения по умолчанию для кластеров по-прежнему используется Azure Storage Blob (WASB). Кроме того, относящиеся к кластеру файлы (журналы и т. д.) записываются в хранилище по умолчанию, а данные, которые необходимо обработать, могут храниться в учетной записи Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="df206-112">When Data Lake Store is used as additional storage, the default storage account for the clusters will still be Azure Storage Blobs (WASB) and the cluster-related files (such as logs, etc.) are still written to the default storage, while the data that you want to process can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="df206-113">Использование хранилища озера данных в качестве дополнительной учетной записи хранения не влияет на производительность или возможность выполнять чтение и запись в хранилище из кластера.</span><span class="sxs-lookup"><span data-stu-id="df206-113">Using Data Lake Store as an additional storage account does not impact performance or the ability to read/write to the storage from the cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="df206-114">Использование Data Lake Store в качестве хранилища кластера HDInsight</span><span class="sxs-lookup"><span data-stu-id="df206-114">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="df206-115">Ниже приведены некоторые важные сведения об использовании HDInsight с Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="df206-115">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="df206-116">Возможность создавать кластеры HDInsight с доступом к Data Lake Store в качестве дополнительного хранилища поддерживается для версий HDInsight 3.2, 3.4, 3.5 и 3.6.</span><span class="sxs-lookup"><span data-stu-id="df206-116">Option to create HDInsight clusters with access to Data Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="df206-117">Настройка в HDInsight хранилища озера данных с помощью PowerShell состоит из нескольких этапов:</span><span class="sxs-lookup"><span data-stu-id="df206-117">Configuring HDInsight to work with Data Lake Store using PowerShell involves the following steps:</span></span>

* <span data-ttu-id="df206-118">создание хранилища озера данных Azure;</span><span class="sxs-lookup"><span data-stu-id="df206-118">Create an Azure Data Lake Store</span></span>
* <span data-ttu-id="df206-119">настройка проверки подлинности для доступа к хранилищу озера данных на основе ролей;</span><span class="sxs-lookup"><span data-stu-id="df206-119">Set up authentication for role-based access to Data Lake Store</span></span>
* <span data-ttu-id="df206-120">создание кластера HDInsight с проверкой подлинности в хранилище озера данных;</span><span class="sxs-lookup"><span data-stu-id="df206-120">Create HDInsight cluster with authentication to Data Lake Store</span></span>
* <span data-ttu-id="df206-121">выполнение тестового задания в кластере.</span><span class="sxs-lookup"><span data-stu-id="df206-121">Run a test job on the cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df206-122">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="df206-122">Prerequisites</span></span>
<span data-ttu-id="df206-123">Перед началом работы с этим учебником необходимо иметь следующее:</span><span class="sxs-lookup"><span data-stu-id="df206-123">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="df206-124">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="df206-124">**An Azure subscription**.</span></span> <span data-ttu-id="df206-125">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="df206-125">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="df206-126">**Azure PowerShell 1.0 или более поздней версии**.</span><span class="sxs-lookup"><span data-stu-id="df206-126">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="df206-127">Ознакомьтесь со статьей [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="df206-127">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="df206-128">**Пакет SDK Windows**.</span><span class="sxs-lookup"><span data-stu-id="df206-128">**Windows SDK**.</span></span> <span data-ttu-id="df206-129">Его можно установить [отсюда](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="df206-129">You can install it from [here](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="df206-130">Пакет используется для создания сертификата безопасности.</span><span class="sxs-lookup"><span data-stu-id="df206-130">You use this to create a security certificate.</span></span>
* <span data-ttu-id="df206-131">**Субъект-служба Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="df206-131">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="df206-132">В этом учебнике приведены инструкции по созданию субъекта-службы в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df206-132">Steps in this tutorial provide instructions on how to create a service principal in Azure AD.</span></span> <span data-ttu-id="df206-133">Однако, чтобы создать субъект-службу, необходимо быть администратором Azure AD.</span><span class="sxs-lookup"><span data-stu-id="df206-133">However, you must be an Azure AD administrator to be able to create a service principal.</span></span> <span data-ttu-id="df206-134">Если вы являетесь администратором Azure AD, то можете пропустить это предварительное требование и продолжить работу с учебником.</span><span class="sxs-lookup"><span data-stu-id="df206-134">If you are an Azure AD administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    <span data-ttu-id="df206-135">**Если вы не являетесь администратором Azure AD**, то вы не сможете выполнить шаги, необходимые для создания субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="df206-135">**If you are not an Azure AD administrator**, you will not be able to perform the steps required to create a service principal.</span></span> <span data-ttu-id="df206-136">В этом случае администратор Azure AD должен сначала создать субъект-службу, после чего вы сможете создать кластер HDInsight с Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="df206-136">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="df206-137">При создании субъекта-службы также необходимо использовать сертификат, как описано в разделе [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority) (Создание субъекта-службы с сертификатом).</span><span class="sxs-lookup"><span data-stu-id="df206-137">Also, the service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="df206-138">Создание хранилища озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="df206-138">Create an Azure Data Lake Store</span></span>
<span data-ttu-id="df206-139">Чтобы создать хранилище озера данных, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="df206-139">Follow these steps to create a Data Lake Store.</span></span>

1. <span data-ttu-id="df206-140">На своем компьютере откройте новое окно Azure PowerShell и введите следующий фрагмент кода.</span><span class="sxs-lookup"><span data-stu-id="df206-140">From your desktop, open a new Azure PowerShell window, and enter the following snippet.</span></span> <span data-ttu-id="df206-141">Когда вам будет предложено войти, введите учетные данные администратора или владельца подписки:</span><span class="sxs-lookup"><span data-stu-id="df206-141">When prompted to log in, make sure you log in as one of the subscription administrator/owner:</span></span>

        # Log in to your Azure account
        Login-AzureRmAccount

        # List all the subscriptions associated to your account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > <span data-ttu-id="df206-142">Если при регистрации поставщика ресурсов Data Lake Store появляется сообщение об ошибке, похожее на `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid`, это может означать, что ваша подписка отсутствует в списке разрешений для Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="df206-142">If you receive an error similar to `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid` when registering the Data Lake Store resource provider, it is possible that your subscription is not whitelisted for Azure Data Lake Store.</span></span> <span data-ttu-id="df206-143">Убедитесь, что подписка Azure для общедоступной предварительной версии Data Lake Store включена, выполнив указанные [инструкции](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="df206-143">Make sure you enable your Azure subscription for Data Lake Store public preview by following these [instructions](data-lake-store-get-started-portal.md).</span></span>
   >
   >
2. <span data-ttu-id="df206-144">Учетная запись хранения озера данных Azure связывается с группой ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="df206-144">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="df206-145">Для начала создайте группу ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="df206-145">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="df206-146">Вы должны увидеть подобные выходные данные:</span><span class="sxs-lookup"><span data-stu-id="df206-146">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="df206-147">Создайте учетную запись хранения озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="df206-147">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="df206-148">Имя новой учетной записи должно содержать только строчные буквы и цифры.</span><span class="sxs-lookup"><span data-stu-id="df206-148">The account name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="df206-149">Вы должны увидеть подобные выходные данные:</span><span class="sxs-lookup"><span data-stu-id="df206-149">You should see an output like the following:</span></span>

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

5. <span data-ttu-id="df206-150">Отправьте пример данных в озеро данных Azure.</span><span class="sxs-lookup"><span data-stu-id="df206-150">Upload some sample data to Azure Data Lake.</span></span> <span data-ttu-id="df206-151">Позже мы проверим, доступны ли эти данные из кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="df206-151">We'll use this later in this article to verify that the data is accessible from an HDInsight cluster.</span></span> <span data-ttu-id="df206-152">Если у вас нет под рукой подходящих для этих целей данных, передайте папку **Ambulance Data** из [репозитория Git для озера данных Azure](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="df206-152">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path to data>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-to-data-lake-store"></a><span data-ttu-id="df206-153">настройка проверки подлинности для доступа к хранилищу озера данных на основе ролей;</span><span class="sxs-lookup"><span data-stu-id="df206-153">Set up authentication for role-based access to Data Lake Store</span></span>
<span data-ttu-id="df206-154">Каждая подписка Azure связана со службой Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="df206-154">Every Azure subscription is associated with an Azure Active Directory.</span></span> <span data-ttu-id="df206-155">Пользователи и службы, получающие доступ к ресурсам подписки через классический портал Azure или API Azure Resource Manager, сначала должны пройти аутентификацию в соответствующей службе Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="df206-155">Users and services that access resources of the subscription using the Azure Classic Portal or Azure Resource Manager API must first authenticate with that Azure Active Directory.</span></span> <span data-ttu-id="df206-156">Доступ к подпискам и службам Azure предоставляется путем назначения соответствующей роли для ресурса Azure.</span><span class="sxs-lookup"><span data-stu-id="df206-156">Access is granted to Azure subscriptions and services by assigning them the appropriate role on an Azure resource.</span></span>  <span data-ttu-id="df206-157">В случае со службами субъект-служба идентифицирует службу в Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="df206-157">For services, a service principal identifies the service in the Azure Active Directory (AAD).</span></span> <span data-ttu-id="df206-158">В этом разделе мы расскажем, как предоставить службе приложения, в частности HDInsight, доступ к ресурсу Azure (созданной ранее учетной записи хранилища озера данных Azure). Для этого с помощью Azure PowerShell мы создадим для приложения субъект-службу и назначим ему роли.</span><span class="sxs-lookup"><span data-stu-id="df206-158">This section illustrates how to grant an application service, like HDInsight, access to an Azure resource (the Azure Data Lake Store account you created earlier) by creating a service principal for the application and assigning roles to that via Azure PowerShell.</span></span>

<span data-ttu-id="df206-159">Чтобы настроить для озера данных Azure проверку подлинности в Active Directory, вам необходимо сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="df206-159">To set up Active Directory authentication for Azure Data Lake, you must perform the following tasks.</span></span>

* <span data-ttu-id="df206-160">Создание самозаверяющего сертификата</span><span class="sxs-lookup"><span data-stu-id="df206-160">Create a self-signed certificate</span></span>
* <span data-ttu-id="df206-161">создать приложение в Azure Active Directory и субъект-службу.</span><span class="sxs-lookup"><span data-stu-id="df206-161">Create an application in Azure Active Directory and a Service Principal</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="df206-162">Создание самозаверяющего сертификата</span><span class="sxs-lookup"><span data-stu-id="df206-162">Create a self-signed certificate</span></span>
<span data-ttu-id="df206-163">Прежде чем выполнять дальнейшие действия, описанные в этом разделе, убедитесь, что на вашем компьютере установлен [пакет SDK Windows](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="df206-163">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with the steps in this section.</span></span> <span data-ttu-id="df206-164">Вам также необходимо создать каталог, например **C:\mycertdir**, в котором будет создан сертификат.</span><span class="sxs-lookup"><span data-stu-id="df206-164">You must have also created a directory, such as **C:\mycertdir**, where the certificate will be created.</span></span>

1. <span data-ttu-id="df206-165">В окне PowerShell перейдите в расположение, где установлен пакет SDK Windows (обычно это `C:\Program Files (x86)\Windows Kits\10\bin\x86`), и с помощью служебной программы [MakeCert][makecert] создайте самозаверяющий сертификат и закрытый ключ.</span><span class="sxs-lookup"><span data-stu-id="df206-165">From the PowerShell window, navigate to the location where you installed Windows SDK (typically, `C:\Program Files (x86)\Windows Kits\10\bin\x86` and use the [MakeCert][makecert] utility to create a self-signed certificate and a private key.</span></span> <span data-ttu-id="df206-166">Используйте такие команды:</span><span class="sxs-lookup"><span data-stu-id="df206-166">Use the following commands.</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="df206-167">Вам будет предложено ввести пароль для закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="df206-167">You will be prompted to enter the private key password.</span></span> <span data-ttu-id="df206-168">После успешного выполнения команды в указанном каталоге сертификатов должны появиться файлы **CertFile.cer** и **mykey.pvk**.</span><span class="sxs-lookup"><span data-stu-id="df206-168">After the command successfully executes, you should see a **CertFile.cer** and **mykey.pvk** in the certificate directory you specified.</span></span>
2. <span data-ttu-id="df206-169">С помощью служебной программы [Pvk2Pfx][pvk2pfx] преобразуйте созданные программой MakeCert PVK- и CER-файлы в PFX-файл.</span><span class="sxs-lookup"><span data-stu-id="df206-169">Use the [Pvk2Pfx][pvk2pfx] utility to convert the .pvk and .cer files that MakeCert created to a .pfx file.</span></span> <span data-ttu-id="df206-170">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="df206-170">Run the following command.</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="df206-171">При появлении соответствующего запроса введите указанный ранее пароль для закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="df206-171">When prompted enter the private key password you specified earlier.</span></span> <span data-ttu-id="df206-172">Значение, указываемое для параметра **-po** — это пароль, связанный с PFX-файлом.</span><span class="sxs-lookup"><span data-stu-id="df206-172">The value you specify for the **-po** parameter is the password that is associated with the .pfx file.</span></span> <span data-ttu-id="df206-173">После успешного выполнения команды вы должны увидеть в указанном каталоге сертификата файл CertFile.pfx.</span><span class="sxs-lookup"><span data-stu-id="df206-173">After the command successfully completes, you should also see a CertFile.pfx in the certificate directory you specified.</span></span>

### <a name="create-an-azure-active-directory-and-a-service-principal"></a><span data-ttu-id="df206-174">Создание приложения в Azure Active Directory и субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="df206-174">Create an Azure Active Directory and a service principal</span></span>
<span data-ttu-id="df206-175">Следуя описаниям, приведенным в этом разделе, вы создадите субъект-службу для приложения Azure Active Directory, назначите роль субъекту-службе и пройдете проверку подлинности в качестве субъекта-службы, используя сертификат.</span><span class="sxs-lookup"><span data-stu-id="df206-175">In this section, you perform the steps to create a service principal for an Azure Active Directory application, assign a role to the service principal, and authenticate as the service principal by providing a certificate.</span></span> <span data-ttu-id="df206-176">Чтобы создать приложение в Azure Active Directory, выполните следующие команды.</span><span class="sxs-lookup"><span data-stu-id="df206-176">Run the following commands to create an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="df206-177">В окне консоли PowerShell вставьте из буфера обмена следующие командлеты.</span><span class="sxs-lookup"><span data-stu-id="df206-177">Paste the following cmdlets in the PowerShell console window.</span></span> <span data-ttu-id="df206-178">Укажите для свойства **-DisplayName** уникальное значение.</span><span class="sxs-lookup"><span data-stu-id="df206-178">Make sure the value you specify for the **-DisplayName** property is unique.</span></span> <span data-ttu-id="df206-179">Значения свойств **-HomePage** b **-IdentiferUris** — это заполнители, которые не проверяются.</span><span class="sxs-lookup"><span data-stu-id="df206-179">Also, the values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter the password" # This is the password you specified for the .pfx file

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
2. <span data-ttu-id="df206-180">С помощью идентификатора приложения создайте субъект-службу.</span><span class="sxs-lookup"><span data-stu-id="df206-180">Create a service principal using the application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="df206-181">Предоставьте субъекту-службе доступ к файлу и папке Data Lake Store, к которым будете обращаться из кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="df206-181">Grant the service principal access to the Data Lake Store folder and the file that you will access from the HDInsight cluster.</span></span> <span data-ttu-id="df206-182">Приведенный ниже фрагмент предоставляет доступ к корню учетной записи Data Lake Store (в который вы скопировали пример файла данных) и к самому файлу.</span><span class="sxs-lookup"><span data-stu-id="df206-182">The snippet below provides access to the root of the Data Lake Store account (where you copied the sample data file), and the file itself.</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="df206-183">Создание кластера HDInsight на платформе Linux с Data Lake Store в качестве дополнительного хранилища</span><span class="sxs-lookup"><span data-stu-id="df206-183">Create an HDInsight Linux cluster with Data Lake Store as additional storage</span></span>

<span data-ttu-id="df206-184">В этом разделе показано, как создать кластер HDInsight Hadoop на платформе Linux с Data Lake Store в качестве дополнительного хранилища.</span><span class="sxs-lookup"><span data-stu-id="df206-184">In this section, we create an HDInsight Hadoop Linux cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="df206-185">В этом выпуске кластер HDInsight и Data Lake Store должны быть в одном расположении.</span><span class="sxs-lookup"><span data-stu-id="df206-185">For this release, the HDInsight cluster and the Data Lake Store must be in the same location.</span></span>

1. <span data-ttu-id="df206-186">Сначала получите идентификатор клиента подписки.</span><span class="sxs-lookup"><span data-stu-id="df206-186">Start with retrieving the subscription tenant ID.</span></span> <span data-ttu-id="df206-187">Позже он вам понадобится.</span><span class="sxs-lookup"><span data-stu-id="df206-187">You will need that later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. <span data-ttu-id="df206-188">В этом выпуске в кластере Hadoop хранилище озера данных может использоваться только как дополнительное хранилище кластера.</span><span class="sxs-lookup"><span data-stu-id="df206-188">For this release, for a Hadoop cluster, Data Lake Store can only be used as an additional storage for the cluster.</span></span> <span data-ttu-id="df206-189">Хранилищем по умолчанию по-прежнему будут BLOB-объекты хранилища Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="df206-189">The default storage will still be the Azure storage blobs (WASB).</span></span> <span data-ttu-id="df206-190">Поэтому мы сначала создадим учетную запись хранения и контейнеры хранилища, необходимые для кластера.</span><span class="sxs-lookup"><span data-stu-id="df206-190">So, we'll first create the storage account and storage containers required for the cluster.</span></span>

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. <span data-ttu-id="df206-191">Создайте кластер HDInsight,</span><span class="sxs-lookup"><span data-stu-id="df206-191">Create the HDInsight cluster.</span></span> <span data-ttu-id="df206-192">выполнив следующие командлеты.</span><span class="sxs-lookup"><span data-stu-id="df206-192">Use the following cmdlets.</span></span>

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have the same name for the cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # The number of nodes in the HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    <span data-ttu-id="df206-193">В случае успешного выполнения командлета должен отобразиться список сведений о кластере.</span><span class="sxs-lookup"><span data-stu-id="df206-193">After the cmdlet successfully completes, you should see an output listing the cluster details.</span></span>


## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-the-data-lake-store"></a><span data-ttu-id="df206-194">Выполнение тестовых заданий в кластере HDInsight</span><span class="sxs-lookup"><span data-stu-id="df206-194">Run test jobs on the HDInsight cluster to use the Data Lake Store</span></span>
<span data-ttu-id="df206-195">После настройки кластера HDInsight выполните в нем тестовые задания, чтобы проверить, доступно ли ему хранилище озера данных.</span><span class="sxs-lookup"><span data-stu-id="df206-195">After you have configured an HDInsight cluster, you can run test jobs on the cluster to test that the HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="df206-196">Для этого запустите образец задания Hive, создающего таблицу с данными, которые вы ранее отправили в хранилище озера данных.</span><span class="sxs-lookup"><span data-stu-id="df206-196">To do so, we will run a sample Hive job that creates a table using the sample data that you uploaded earlier to your Data Lake Store.</span></span>

<span data-ttu-id="df206-197">В этом разделе вы подключитесь к созданному кластеру HDInsight под управлением Linux по протоколу SSH и выполните пример запроса Hive.</span><span class="sxs-lookup"><span data-stu-id="df206-197">In this section you will SSH into the HDInsight Linux cluster you created and run the a sample Hive query.</span></span>

* <span data-ttu-id="df206-198">Если вы используете клиент Windows для подключения к кластеру по протоколу SSH, ознакомьтесь со статьей [Использование SSH с HDInsight (Hadoop) в PuTTY на базе Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="df206-198">If you are using a Windows client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="df206-199">Если вы используете клиент Linux для подключения к кластеру по SSH, ознакомьтесь со статьей [Использование SSH с HDInsight (Hadoop) на платформе Windows, Linux, Unix или OS X](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="df206-199">If you are using a Linux client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

1. <span data-ttu-id="df206-200">После подключения запустите интерфейс командной строки Hive с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="df206-200">Once connected, start the Hive CLI by using the following command:</span></span>

        hive
2. <span data-ttu-id="df206-201">Используя интерфейс командной строки, введите следующие инструкции, чтобы создать таблицу с именем **vehicles** с помощью примера данных в хранилище озера данных.</span><span class="sxs-lookup"><span data-stu-id="df206-201">Using the CLI, enter the following statements to create a new table named **vehicles** by using the sample data in the Data Lake Store:</span></span>

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    <span data-ttu-id="df206-202">Должен отобразиться результат, аналогичный приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="df206-202">You should see an output similar to the following:</span></span>

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

## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="df206-203">Доступ к хранилищу озера данных с помощью команд HDFS</span><span class="sxs-lookup"><span data-stu-id="df206-203">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="df206-204">Настроив в кластере HDInsight параметры для работы с хранилищем озера данных, используйте для доступа к хранилищу команды оболочки HDFS.</span><span class="sxs-lookup"><span data-stu-id="df206-204">Once you have configured the HDInsight cluster to use Data Lake Store, you can use the HDFS shell commands to access the store.</span></span>

<span data-ttu-id="df206-205">В этом разделе вы подключитесь к созданному кластеру HDInsight под управлением Linux по протоколу SSH и выполните команды HDFS.</span><span class="sxs-lookup"><span data-stu-id="df206-205">In this section you will SSH into the HDInsight Linux cluster you created and run the HDFS commands.</span></span>

* <span data-ttu-id="df206-206">Если вы используете клиент Windows для подключения к кластеру по протоколу SSH, ознакомьтесь со статьей [Использование SSH с HDInsight (Hadoop) в PuTTY на базе Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="df206-206">If you are using a Windows client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="df206-207">Если вы используете клиент Linux для подключения к кластеру по SSH, ознакомьтесь со статьей [Использование SSH с HDInsight (Hadoop) на платформе Windows, Linux, Unix или OS X](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="df206-207">If you are using a Linux client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

<span data-ttu-id="df206-208">После подключения используйте следующую команду файловой системы HDFS для получения списка файлов в хранилище озера данных.</span><span class="sxs-lookup"><span data-stu-id="df206-208">Once connected, use the following HDFS filesystem command to list the files in the Data Lake Store.</span></span>

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

<span data-ttu-id="df206-209">Эта команда должна показать файл, который вы ранее отправили в хранилище озера данных.</span><span class="sxs-lookup"><span data-stu-id="df206-209">This should list the file that you uploaded earlier to the Data Lake Store.</span></span>

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

<span data-ttu-id="df206-210">С помощью команды `hdfs dfs -put` вы можете отправить в хранилище озера данных некоторые файлы, а затем с помощью команды `hdfs dfs -ls` проверить, успешно ли они передались.</span><span class="sxs-lookup"><span data-stu-id="df206-210">You can also use the `hdfs dfs -put` command to upload some files to the Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="df206-211">См. также</span><span class="sxs-lookup"><span data-stu-id="df206-211">See Also</span></span>
* [<span data-ttu-id="df206-212">Портал: создание кластера HDInsight для работы с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="df206-212">Portal: Create an HDInsight cluster to use Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
