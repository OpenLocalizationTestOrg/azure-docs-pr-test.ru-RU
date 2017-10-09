---
title: "aaaCreate HDInsight кластер хранилища Озера данных хранения по умолчанию с помощью PowerShell | Документы Microsoft"
description: "Использовать toocreate Azure PowerShell и использовать кластеров HDInsight в хранилище Озера данных Azure"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8917af15-8e37-46cf-87ad-4e6d5d67ecdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/08/2017
ms.author: nitinme
ms.openlocfilehash: a5c0ad416da6ad9bd07204af2ebb6b7470916085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a><span data-ttu-id="64903-103">Создание кластеров HDInsight, использующих Data Lake Store, с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="64903-103">Create HDInsight clusters with Data Lake Store as default storage by using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="64903-104">Использовать hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="64903-104">Use hello Azure portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="64903-105">Использование PowerShell (для хранилища по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="64903-105">Use PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="64903-106">Использование PowerShell (для дополнительного хранилища)</span><span class="sxs-lookup"><span data-stu-id="64903-106">Use PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="64903-107">Использование Resource Manager</span><span class="sxs-lookup"><span data-stu-id="64903-107">Use Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

<span data-ttu-id="64903-108">Узнайте, как кластеры tooconfigure toouse Azure PowerShell Azure HDInsight с хранилища Озера данных Azure, как хранилище по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="64903-108">Learn how toouse Azure PowerShell tooconfigure Azure HDInsight clusters with Azure Data Lake Store, as default storage.</span></span> <span data-ttu-id="64903-109">Инструкции по созданию кластера HDInsight, использующего Data Lake Store в качестве дополнительного хранилища, см. в статье [Создание кластера HDInsight с Data Lake Store (как дополнительное хранилище) с помощью Azure PowerShell](data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="64903-109">For instructions on creating an HDInsight cluster with Data Lake Store as additional storage, see [Create an HDInsight cluster with Data Lake Store as additional storage](data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

<span data-ttu-id="64903-110">Ниже приведены некоторые важные сведения об использовании HDInsight с Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="64903-110">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="64903-111">кластеры HDInsight toocreate параметр Hello с доступом хранилища Озера tooData хранения по умолчанию доступна для HDInsight версии 3.5 и 3.6.</span><span class="sxs-lookup"><span data-stu-id="64903-111">hello option toocreate HDInsight clusters with access tooData Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="64903-112">кластеры HDInsight с toocreate параметр Hello получить доступ к хранилищу Озера tooData как хранилищем по умолчанию *недоступно* для кластеров HDInsight Premium.</span><span class="sxs-lookup"><span data-stu-id="64903-112">hello option toocreate HDInsight clusters with access tooData Lake Store as default storage is *not available* for HDInsight Premium clusters.</span></span>

<span data-ttu-id="64903-113">tooconfigure toowork HDInsight в хранилище Озера данных с помощью PowerShell, следуйте инструкциям hello в разделах следующие пять hello.</span><span class="sxs-lookup"><span data-stu-id="64903-113">tooconfigure HDInsight toowork with Data Lake Store by using PowerShell, follow hello instructions in hello next five sections.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64903-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="64903-114">Prerequisites</span></span>
<span data-ttu-id="64903-115">Прежде чем начать работу с учебником, убедитесь, что выполнены следующие требования к hello:</span><span class="sxs-lookup"><span data-stu-id="64903-115">Before you begin this tutorial, make sure that you meet hello following requirements:</span></span>

* <span data-ttu-id="64903-116">**Подписка Azure**: перейти слишком[получить бесплатная пробная версия](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="64903-116">**An Azure subscription**: Go too[Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="64903-117">**Azure PowerShell 1.0 или более поздней**: в разделе [как tooinstall и настройте PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="64903-117">**Azure PowerShell 1.0 or greater**: See [How tooinstall and configure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="64903-118">**Пакет средств разработки программного обеспечения (SDK)**: tooinstall Windows SDK, перейдите в слишком[загружает и средств для Windows 10](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="64903-118">**Windows Software Development Kit (SDK)**: tooinstall Windows SDK, go too[Downloads and tools for Windows 10](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="64903-119">Hello SDK — toocreate используется сертификат безопасности.</span><span class="sxs-lookup"><span data-stu-id="64903-119">hello SDK is used toocreate a security certificate.</span></span>
* <span data-ttu-id="64903-120">**Субъекту-службе Azure Active Directory**: в данном учебнике как toocreate участника службы в Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="64903-120">**Azure Active Directory service principal**: This tutorial describes how toocreate a service principal in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="64903-121">Однако toocreate участника службы, необходимо быть администратором Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64903-121">However, toocreate a service principal, you must be an Azure AD administrator.</span></span> <span data-ttu-id="64903-122">Если вы являетесь администратором, можно пропустить это предварительное условие и продолжить работу с учебником hello.</span><span class="sxs-lookup"><span data-stu-id="64903-122">If you are an administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    >[!NOTE]
    ><span data-ttu-id="64903-123">Создать субъект-службу может только администратор Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64903-123">You can create a service principal only if you are an Azure AD administrator.</span></span> <span data-ttu-id="64903-124">Администратор Azure AD должен сначала создать субъект-службу, после чего вы сможете создать кластер HDInsight, использующий Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="64903-124">Your Azure AD administrator must create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="64903-125">Hello участника-службы должны создаваться с помощью сертификата, как описано в [создании участника службы с сертификатом](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="64903-125">hello service principal must be created with a certificate, as described in [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>
    >

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="64903-126">Создание учетной записи хранения озера данных</span><span class="sxs-lookup"><span data-stu-id="64903-126">Create a Data Lake Store account</span></span>
<span data-ttu-id="64903-127">toocreate учетную запись хранилища Озера данных hello следующие:</span><span class="sxs-lookup"><span data-stu-id="64903-127">toocreate a Data Lake Store account, do hello following:</span></span>

1. <span data-ttu-id="64903-128">С рабочего стола откройте окно PowerShell, а затем введите ниже фрагменты hello.</span><span class="sxs-lookup"><span data-stu-id="64903-128">From your desktop, open a PowerShell window, and then enter hello snippets below.</span></span> <span data-ttu-id="64903-129">Когда вы будете запрашиваемые toosign в знак в качестве одного из администраторов подписки hello или владельцы.</span><span class="sxs-lookup"><span data-stu-id="64903-129">When you are prompted toosign in, sign in as one of hello subscription administrators or owners.</span></span> 

        # Sign in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > <span data-ttu-id="64903-130">Если регистрация поставщика ресурсов хранилища Озера данных hello и получать сообщение об ошибке слишком`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, подписки не может быть входят для хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="64903-130">If you register hello Data Lake Store resource provider and receive an error similar too`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, your subscription might not be whitelisted for Data Lake Store.</span></span> <span data-ttu-id="64903-131">tooenable подписки Azure hello хранилища Озера данных общедоступной предварительной версии, следуйте инструкциям hello [Приступая к работе с хранилища Озера данных Azure с помощью портала Azure hello](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="64903-131">tooenable your Azure subscription for hello Data Lake Store public preview, follow hello instructions in [Get started with Azure Data Lake Store by using hello Azure portal](data-lake-store-get-started-portal.md).</span></span>
    >

2. <span data-ttu-id="64903-132">Учетная запись Data Lake Store связывается с группой ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="64903-132">A Data Lake Store account is associated with an Azure resource group.</span></span> <span data-ttu-id="64903-133">Для начала создайте группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="64903-133">Start by creating a resource group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="64903-134">Вы должны увидеть подобные выходные данные:</span><span class="sxs-lookup"><span data-stu-id="64903-134">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="64903-135">Создайте учетную запись Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="64903-135">Create a Data Lake Store account.</span></span> <span data-ttu-id="64903-136">Hello учетной записи, имя должно содержать только строчные буквы и цифры.</span><span class="sxs-lookup"><span data-stu-id="64903-136">hello account name you specify must contain only lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="64903-137">Вы должны увидеть результаты hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="64903-137">You should see an output like hello following:</span></span>

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

4. <span data-ttu-id="64903-138">Использование хранилища Озера данных хранения по умолчанию требует вы toospecify корневой путь toowhich hello кластера файлы скопированы во время создания кластера.</span><span class="sxs-lookup"><span data-stu-id="64903-138">Using Data Lake Store as default storage requires you toospecify a root path toowhich hello cluster-specific files are copied during cluster creation.</span></span> <span data-ttu-id="64903-139">корневой путь, который является toocreate **/кластеры/hdiadlcluster** в фрагменте hello, используйте следующие командлеты hello:</span><span class="sxs-lookup"><span data-stu-id="64903-139">toocreate a root path, which is **/clusters/hdiadlcluster** in hello  snippet, use hello following cmdlets:</span></span>

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a><span data-ttu-id="64903-140">Настройка проверки подлинности на основе ролей доступ к хранилищу Озера tooData</span><span class="sxs-lookup"><span data-stu-id="64903-140">Set up authentication for role-based access tooData Lake Store</span></span>
<span data-ttu-id="64903-141">Каждая подписка Azure связана с сущностью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64903-141">Every Azure subscription is associated with an Azure AD entity.</span></span> <span data-ttu-id="64903-142">Пользователей и служб, доступ к ресурсам подписки с помощью hello портал Azure или hello API диспетчера ресурсов Azure должны сначала пройти проверку подлинности в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64903-142">Users and services that access subscription resources by using hello Azure portal or hello Azure Resource Manager API must first authenticate with Azure AD.</span></span> <span data-ttu-id="64903-143">Доступ предоставляется tooAzure подписками и службами путем назначения им hello соответствующей роли на ресурс Azure.</span><span class="sxs-lookup"><span data-stu-id="64903-143">Access is granted tooAzure subscriptions and services by assigning them hello appropriate role on an Azure resource.</span></span> <span data-ttu-id="64903-144">Для служб субъекта-службы идентифицирует службу hello в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64903-144">For services, a service principal identifies hello service in Azure AD.</span></span>

<span data-ttu-id="64903-145">В этом разделе показано, как службы toogrant приложения, такие как HDInsight, tooan доступ ресурсов Azure (hello ранее созданной учетной записи хранилища Озера данных).</span><span class="sxs-lookup"><span data-stu-id="64903-145">This section illustrates how toogrant an application service, such as HDInsight, access tooan Azure resource (hello Data Lake Store account that you created earlier).</span></span> <span data-ttu-id="64903-146">Осуществляется путем создания службы основного приложения hello и назначение ролей tooit через PowerShell.</span><span class="sxs-lookup"><span data-stu-id="64903-146">You do so by creating a service principal for hello application and assigning roles tooit via PowerShell.</span></span>

<span data-ttu-id="64903-147">tooset проверку подлинности Active Directory для Озера данных Azure, выполнять задачи hello в следующих двух разделах hello.</span><span class="sxs-lookup"><span data-stu-id="64903-147">tooset up Active Directory authentication for Azure Data Lake, perform hello tasks in hello following two sections.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="64903-148">Создание самозаверяющего сертификата</span><span class="sxs-lookup"><span data-stu-id="64903-148">Create a self-signed certificate</span></span>
<span data-ttu-id="64903-149">Убедитесь, что у вас есть [пакета Windows SDK](https://dev.windows.com/en-us/downloads) установлен перед продолжением hello шаги в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="64903-149">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with hello steps in this section.</span></span> <span data-ttu-id="64903-150">Необходимо также создать каталог, например *C:\mycertdir*, в котором можно создать сертификат hello.</span><span class="sxs-lookup"><span data-stu-id="64903-150">You must have also created a directory, such as *C:\mycertdir*, where you create hello certificate.</span></span>

1. <span data-ttu-id="64903-151">Из окна PowerShell hello, go toohello расположение, где установлен пакет SDK для Windows (как правило, *\Windows Kits\10\bin\x86 C:\Program Files (x86)*) и использовать hello [MakeCert] [ makecert] toocreate программа самозаверяющий сертификат и закрытый ключ.</span><span class="sxs-lookup"><span data-stu-id="64903-151">From hello PowerShell window, go toohello location where you installed Windows SDK (typically, *C:\Program Files (x86)\Windows Kits\10\bin\x86*) and use hello [MakeCert][makecert] utility toocreate a self-signed certificate and a private key.</span></span> <span data-ttu-id="64903-152">Используйте hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="64903-152">Use hello following commands:</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="64903-153">Появится запрос tooenter hello пароль для закрытого ключа.</span><span class="sxs-lookup"><span data-stu-id="64903-153">You will be prompted tooenter hello private key password.</span></span> <span data-ttu-id="64903-154">После успешного выполнения команды hello, вы увидите **CertFile.cer** и **mykey.pvk** в указанный каталог hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="64903-154">After hello command is successfully executed, you should see **CertFile.cer** and **mykey.pvk** in hello certificate directory that you specified.</span></span>
2. <span data-ttu-id="64903-155">Используйте hello [Pvk2Pfx] [ pvk2pfx] .pvk hello tooconvert программы или CER-файлы, MakeCert созданный tooa PFX-файл.</span><span class="sxs-lookup"><span data-stu-id="64903-155">Use hello [Pvk2Pfx][pvk2pfx] utility tooconvert hello .pvk and .cer files that MakeCert created tooa .pfx file.</span></span> <span data-ttu-id="64903-156">Выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="64903-156">Run hello following command:</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="64903-157">Когда вам будет предложено ввести hello пароль закрытого ключа, указанный ранее.</span><span class="sxs-lookup"><span data-stu-id="64903-157">When you are prompted, enter hello private key password that you specified earlier.</span></span> <span data-ttu-id="64903-158">значение, указываемое для hello Hello **-po** параметр является hello пароль, связанный с hello PFX-файл.</span><span class="sxs-lookup"><span data-stu-id="64903-158">hello value you specify for hello **-po** parameter is hello password that's associated with hello .pfx file.</span></span> <span data-ttu-id="64903-159">После успешного завершения команды hello, вы также увидите **CertFile.pfx** в указанный каталог hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="64903-159">After hello command has been completed successfully, you should also see a **CertFile.pfx** in hello certificate directory that you specified.</span></span>

### <a name="create-an-azure-ad-and-a-service-principal"></a><span data-ttu-id="64903-160">Создание приложения Azure AD и субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="64903-160">Create an Azure AD and a service principal</span></span>
<span data-ttu-id="64903-161">В этом разделе Создание субъекта-службы для приложения Azure AD, назначение роли участника службы toohello и проверять подлинность как у участника-службы hello, предоставляя сертификат.</span><span class="sxs-lookup"><span data-stu-id="64903-161">In this section, you create a service principal for an Azure AD application, assign a role toohello service principal, and authenticate as hello service principal by providing a certificate.</span></span> <span data-ttu-id="64903-162">toocreate hello, следующие команды запуска приложения в Azure AD:</span><span class="sxs-lookup"><span data-stu-id="64903-162">toocreate an application in Azure AD, run hello following commands:</span></span>

1. <span data-ttu-id="64903-163">Вставьте следующие командлеты в окне консоли PowerShell hello hello.</span><span class="sxs-lookup"><span data-stu-id="64903-163">Paste hello following cmdlets in hello PowerShell console window.</span></span> <span data-ttu-id="64903-164">Убедитесь, что это значение hello, укажите для hello **- DisplayName** свойство является уникальным.</span><span class="sxs-lookup"><span data-stu-id="64903-164">Make sure that hello value you specify for hello **-DisplayName** property is unique.</span></span> <span data-ttu-id="64903-165">Здравствуйте, значения для **- Домашняя страница** и **- IdentiferUris** значения заполнителя, а не проверяются.</span><span class="sxs-lookup"><span data-stu-id="64903-165">hello values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

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
2. <span data-ttu-id="64903-166">Создание участника службы с помощью идентификатора приложения hello.</span><span class="sxs-lookup"><span data-stu-id="64903-166">Create a service principal by using hello application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="64903-167">Предоставьте корневой папки хранилища Озера данных toohello hello службы доступа и папкам hello в hello корневой путь, указанный ранее.</span><span class="sxs-lookup"><span data-stu-id="64903-167">Grant hello service principal access toohello Data Lake Store root and all hello folders in hello root path that you specified earlier.</span></span> <span data-ttu-id="64903-168">Используйте следующие командлеты hello.</span><span class="sxs-lookup"><span data-stu-id="64903-168">Use hello following cmdlets:</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-hello-default-storage"></a><span data-ttu-id="64903-169">Создание кластера HDInsight Linux с хранилища Озера данных хранения по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="64903-169">Create an HDInsight Linux cluster with Data Lake Store as hello default storage</span></span>

<span data-ttu-id="64903-170">В этом разделе создается кластер HDInsight Hadoop Linux с хранилища Озера данных хранения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="64903-170">In this section, you create an HDInsight Hadoop Linux cluster with Data Lake Store as hello default storage.</span></span> <span data-ttu-id="64903-171">В этом выпуске hello кластер HDInsight и хранилище Озера данных должна находиться в hello местоположения.</span><span class="sxs-lookup"><span data-stu-id="64903-171">For this release, hello HDInsight cluster and Data Lake Store must be in hello same location.</span></span>

1. <span data-ttu-id="64903-172">Получить идентификатор клиента подписки hello и сохраните ее toouse позже.</span><span class="sxs-lookup"><span data-stu-id="64903-172">Retrieve hello subscription tenant ID, and store it toouse later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. <span data-ttu-id="64903-173">Создание кластера HDInsight hello с помощью hello следующие командлеты:</span><span class="sxs-lookup"><span data-stu-id="64903-173">Create hello HDInsight cluster by using hello following cmdlets:</span></span>

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = "<unique cluster name>"
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster `
               -ClusterType Hadoop `
               -OSType Linux `
               -ClusterSizeInNodes $clusterNodes `
               -ResourceGroupName $resourceGroupName `
               -ClusterName $clusterName `
               -HttpCredential $httpCredentials `
               -Location $location `
               -DefaultStorageAccountType AzureDataLakeStore `
               -DefaultStorageAccountName "$storageAccountName.azuredatalakestore.net" `
               -DefaultStorageRootPath $storageRootPath `
               -Version "3.6" `
               -SshCredential $sshCredentials `
               -AadTenantId $tenantId `
               -ObjectId $objectId `
               -CertificateFilePath $certificateFilePath `
               -CertificatePassword $password

    <span data-ttu-id="64903-174">После успешного завершения hello командлета вы увидите выход, содержащий сведения о кластере hello.</span><span class="sxs-lookup"><span data-stu-id="64903-174">After hello cmdlet has been successfully completed, you should see an output that lists hello cluster details.</span></span>

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-data-lake-store"></a><span data-ttu-id="64903-175">Запуск тестовых заданий в toouse кластера HDInsight hello хранилища Озера данных</span><span class="sxs-lookup"><span data-stu-id="64903-175">Run test jobs on hello HDInsight cluster toouse Data Lake Store</span></span>
<span data-ttu-id="64903-176">После настройки кластера HDInsight можно запускать задания теста для его tooensure его доступность хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="64903-176">After you have configured an HDInsight cluster, you can run test jobs on it tooensure that it can access Data Lake Store.</span></span> <span data-ttu-id="64903-177">Таким образом, toodo запуска toocreate задания Hive образец таблицы, использующей hello образец данных, уже доступный в хранилище Озера данных  *<cluster root>/example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="64903-177">toodo so, run a sample Hive job toocreate a table that uses hello sample data that's already available in Data Lake Store at *<cluster root>/example/data/sample.log*.</span></span>

<span data-ttu-id="64903-178">В этом разделе в hello кластера hdinsight под Linux, созданного подключения Secure Shell (SSH) и запустите образец запроса Hive.</span><span class="sxs-lookup"><span data-stu-id="64903-178">In this section, you make a Secure Shell (SSH) connection into hello HDInsight Linux cluster that you created, and then you run a sample Hive query.</span></span>

* <span data-ttu-id="64903-179">Если вы используете Windows клиент toomake SSH-подключения в кластер hello, см. раздел [использование SSH с Linux-based Hadoop в HDInsight из Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="64903-179">If you are using a Windows client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="64903-180">При использовании toomake клиента Linux SSH-подключения в кластер hello. в разделе [использование SSH с Linux-based Hadoop в HDInsight в Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="64903-180">If you are using a Linux client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="64903-181">После внесения hello соединения, запустите hello Hive командной строки (CLI) с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="64903-181">After you have made hello connection, start hello Hive command-line interface (CLI) by using hello following command:</span></span>

        hive
2. <span data-ttu-id="64903-182">Следующие инструкции toocreate новую таблицу с именем tooenter hello используйте hello CLI **автомобилей** с помощью hello образец данных в хранилище Озера данных:</span><span class="sxs-lookup"><span data-stu-id="64903-182">Use hello CLI tooenter hello following statements toocreate a new table named **vehicles** by using hello sample data in Data Lake Store:</span></span>

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="64903-183">Вы увидите выходные данные запроса hello hello SSH консоли.</span><span class="sxs-lookup"><span data-stu-id="64903-183">You should see hello query output on hello SSH console.</span></span>

    >[!NOTE]
    ><span data-ttu-id="64903-184">Hello путь toohello образцов данных в hello предшествующий команда CREATE TABLE является `adl:///example/data/`, где `adl:///` корневой кластер hello.</span><span class="sxs-lookup"><span data-stu-id="64903-184">hello path toohello sample data in hello preceding CREATE TABLE command is `adl:///example/data/`, where `adl:///` is hello cluster root.</span></span> <span data-ttu-id="64903-185">Следующий пример hello корневого кластера hello, указанный в этом учебнике, является команда hello `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span><span class="sxs-lookup"><span data-stu-id="64903-185">Following hello example of hello cluster root that's specified in this tutorial, hello command is `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span></span> <span data-ttu-id="64903-186">Можно использовать краткого варианта hello или предоставить корневого кластера toohello полный путь hello.</span><span class="sxs-lookup"><span data-stu-id="64903-186">You can either use hello shorter alternative or provide hello complete path toohello cluster root.</span></span>
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a><span data-ttu-id="64903-187">Доступ к Data Lake Store с помощью команд HDFS</span><span class="sxs-lookup"><span data-stu-id="64903-187">Access Data Lake Store by using HDFS commands</span></span>
<span data-ttu-id="64903-188">После настройки хранилища Озера данных toouse кластера HDInsight hello, можно использовать системы распределенных файла Hadoop (HDFS) оболочки команды tooaccess hello хранилища.</span><span class="sxs-lookup"><span data-stu-id="64903-188">After you have configured hello HDInsight cluster toouse Data Lake Store, you can use Hadoop Distributed File System (HDFS) shell commands tooaccess hello store.</span></span>

<span data-ttu-id="64903-189">В этом разделе сделать SSH-подключения в hello кластера hdinsight под Linux, созданного и выполните команды HDFS hello.</span><span class="sxs-lookup"><span data-stu-id="64903-189">In this section, you make an SSH connection into hello HDInsight Linux cluster that you created, and then you run hello HDFS commands.</span></span>

* <span data-ttu-id="64903-190">Если вы используете Windows клиент toomake SSH-подключения в кластер hello, см. раздел [использование SSH с Linux-based Hadoop в HDInsight из Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="64903-190">If you are using a Windows client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="64903-191">При использовании toomake клиента Linux SSH-подключения в кластер hello. в разделе [использование SSH с Linux-based Hadoop в HDInsight в Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="64903-191">If you are using a Linux client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="64903-192">После внесения hello подключения список файлов hello в хранилище Озера данных с помощью hello, следующая команда системы файла HDFS.</span><span class="sxs-lookup"><span data-stu-id="64903-192">After you've made hello connection, list hello files in Data Lake Store by using hello following HDFS file system command.</span></span>

    hdfs dfs -ls adl:///

<span data-ttu-id="64903-193">Можно также использовать hello `hdfs dfs -put` команды tooupload хранилища Озера tooData некоторые файлы, а затем используйте `hdfs dfs -ls` tooverify ли hello файлы были успешно отправлены.</span><span class="sxs-lookup"><span data-stu-id="64903-193">You can also use hello `hdfs dfs -put` command tooupload some files tooData Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="64903-194">См. также</span><span class="sxs-lookup"><span data-stu-id="64903-194">See also</span></span>
* [<span data-ttu-id="64903-195">Портал Azure: создайте toouse кластера HDInsight хранилища Озера данных</span><span class="sxs-lookup"><span data-stu-id="64903-195">Azure portal: Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
