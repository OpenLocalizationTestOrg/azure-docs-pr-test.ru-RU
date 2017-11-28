---
title: "кластеры aaaCreate Hadoop с помощью шаблонов - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toocreate кластеры для HDInsight с помощью шаблонов диспетчера ресурсов"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00a80dea-011f-44f0-92a4-25d09db9d996
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: jgao
ms.openlocfilehash: 92a6c1d888e401a11537dba34f188245ac17f448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a><span data-ttu-id="3c500-103">Создание кластеров Hadoop в HDInsight с помощью шаблонов Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3c500-103">Create Hadoop clusters in HDInsight by using Resource Manager templates</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="3c500-104">В этой статье вы узнаете несколько способов кластеры toocreate Azure HDInsight с помощью шаблонов диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="3c500-104">In this article, you learn several ways toocreate Azure HDInsight clusters with Azure Resource Manager templates.</span></span> <span data-ttu-id="3c500-105">Узнайте подробнее [о развертывании приложения с помощью шаблона диспетчера ресурсов Azure](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="3c500-105">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="3c500-106">toolearn о другие инструменты для создания кластера и функциях, щелкните селектор вкладку hello на hello верхней части этой страницы или см. в разделе [кластера методы создания](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span><span class="sxs-lookup"><span data-stu-id="3c500-106">toolearn about other cluster creation tools and features, click hello tab selector on hello top of this page or see [Cluster creation methods](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c500-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3c500-107">Prerequisites</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="3c500-108">инструкции toofollow hello в этой статье, необходимо иметь:</span><span class="sxs-lookup"><span data-stu-id="3c500-108">toofollow hello instructions in this article, you'll need:</span></span>

* <span data-ttu-id="3c500-109">[Подписка Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="3c500-109">An [Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="3c500-110">Azure PowerShell и (или) Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="3c500-110">Azure PowerShell and/or Azure CLI.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a><span data-ttu-id="3c500-111">Шаблоны диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="3c500-111">Resource Manager templates</span></span>
<span data-ttu-id="3c500-112">Следующие приложения в одной операцией скоординированного hello легко toocreate становится шаблона диспетчера ресурсов:</span><span class="sxs-lookup"><span data-stu-id="3c500-112">A Resource Manager template makes it easy toocreate hello following for your application in a single, coordinated operation:</span></span>
* <span data-ttu-id="3c500-113">Кластеры HDInsight и их зависимых ресурсов (например, учетной записи хранения по умолчанию hello)</span><span class="sxs-lookup"><span data-stu-id="3c500-113">HDInsight clusters and their dependent resources (such as hello default storage account)</span></span>
* <span data-ttu-id="3c500-114">Другие ресурсы (например, база данных SQL Azure toouse Apache Sqoop)</span><span class="sxs-lookup"><span data-stu-id="3c500-114">Other resources (such as Azure SQL Database toouse Apache Sqoop)</span></span>

<span data-ttu-id="3c500-115">В шаблоне hello определить hello ресурсы, необходимые для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="3c500-115">In hello template, you define hello resources that are needed for hello application.</span></span> <span data-ttu-id="3c500-116">Можно также указать значения tooinput параметров развертывания для разных сред.</span><span class="sxs-lookup"><span data-stu-id="3c500-116">You also specify deployment parameters tooinput values for different environments.</span></span> <span data-ttu-id="3c500-117">шаблон Hello состоит из выражения, использование значения tooconstruct развертывания и JSON.</span><span class="sxs-lookup"><span data-stu-id="3c500-117">hello template consists of JSON and expressions that you use tooconstruct values for your deployment.</span></span>

<span data-ttu-id="3c500-118">Примеры шаблонов HDInsight можно найти в [коллекции шаблонов быстрого запуска Azure](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span><span class="sxs-lookup"><span data-stu-id="3c500-118">You can find HDInsight template samples at [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span></span> <span data-ttu-id="3c500-119">Использовать кросс платформенных [кода Visual Studio](https://code.visualstudio.com/#alt-downloads) с hello [расширения диспетчера ресурсов](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) или текстовый редактор toosave hello шаблон в файл на рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="3c500-119">Use cross-platform [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) with hello [Resource Manager extension](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) or a text editor toosave hello template into a file on your workstation.</span></span> <span data-ttu-id="3c500-120">Вы узнаете, как toocall hello шаблона с использованием различных методов.</span><span class="sxs-lookup"><span data-stu-id="3c500-120">You learn how toocall hello template by using different methods.</span></span>

<span data-ttu-id="3c500-121">Дополнительные сведения о шаблонах диспетчера ресурсов см. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="3c500-121">For more information about Resource Manager templates, see hello following articles:</span></span>

* [<span data-ttu-id="3c500-122">Шаблоны диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="3c500-122">Author Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="3c500-123">Развертывание ресурсов с использованием шаблонов Resource Manager и Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3c500-123">Deploy an application with Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a><span data-ttu-id="3c500-124">Создание шаблонов</span><span class="sxs-lookup"><span data-stu-id="3c500-124">Generate templates</span></span>

<span data-ttu-id="3c500-125">С помощью hello портал Azure, можно настроить все свойства hello кластера и затем сохраните шаблон hello перед его развертыванием.</span><span class="sxs-lookup"><span data-stu-id="3c500-125">By using hello Azure portal, you can configure all hello properties of a cluster and then save hello template before deploying it.</span></span> <span data-ttu-id="3c500-126">Затем можно повторно использовать шаблон hello.</span><span class="sxs-lookup"><span data-stu-id="3c500-126">You can then reuse hello template.</span></span>

<span data-ttu-id="3c500-127">**toogenerate шаблона с использованием hello портал Azure**</span><span class="sxs-lookup"><span data-stu-id="3c500-127">**toogenerate a template by using hello Azure portal**</span></span>

1. <span data-ttu-id="3c500-128">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3c500-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3c500-129">Нажмите кнопку **New** hello слева в меню **аналитики + аналитика**, а затем нажмите кнопку **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="3c500-129">Click **New** on hello left menu, click **Intelligence + analytics**, and then click **HDInsight**.</span></span>
3. <span data-ttu-id="3c500-130">Соблюдают hello инструкции tooenter.</span><span class="sxs-lookup"><span data-stu-id="3c500-130">Follow hello instructions tooenter properties.</span></span> <span data-ttu-id="3c500-131">Можно использовать либо hello **быстрое создание** или hello **настраиваемый** параметр.</span><span class="sxs-lookup"><span data-stu-id="3c500-131">You can use either hello **Quick create** or hello **Custom** option.</span></span>
4. <span data-ttu-id="3c500-132">На hello **Сводка** щелкните **загрузки шаблона и параметров**:</span><span class="sxs-lookup"><span data-stu-id="3c500-132">On hello **Summary** tab, click **Download template and parameters**:</span></span>

    ![Скачивание шаблона Resource Manager для создания кластера HDInsight Hadoop](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    <span data-ttu-id="3c500-134">Появится список hello файл шаблона, файл параметров и кода выборок toodeploy hello шаблона:</span><span class="sxs-lookup"><span data-stu-id="3c500-134">You see a list of hello template file, parameters file, and code samples used toodeploy hello template:</span></span>

    ![Параметры скачивания шаблона Resource Manager для создания кластера HDInsight Hadoop](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    <span data-ttu-id="3c500-136">Здесь можно загрузить шаблон hello, сохраните его tooyour библиотеки шаблонов или развертывания шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="3c500-136">From here, you can download hello template, save it tooyour template library, or deploy hello template.</span></span>

    <span data-ttu-id="3c500-137">tooaccess шаблон в библиотеке, нажмите кнопку **дополнительные службы** hello левом меню, и нажмите кнопку **шаблоны** (в разделе hello **других** категории).</span><span class="sxs-lookup"><span data-stu-id="3c500-137">tooaccess a template in your library, click **More services** from hello left menu, and then click **Templates** (under hello **Other** category).</span></span>

    > [!Note]
    > <span data-ttu-id="3c500-138">файл шаблона и параметров Hello должны использоваться совместно.</span><span class="sxs-lookup"><span data-stu-id="3c500-138">hello template and parameters file must be used together.</span></span> <span data-ttu-id="3c500-139">В противном случае можно получить непредвиденные результаты.</span><span class="sxs-lookup"><span data-stu-id="3c500-139">Otherwise, you might get unexpected results.</span></span> <span data-ttu-id="3c500-140">Здравствуйте, например, по умолчанию **clusterKind** всегда является значение свойства **hadoop**, несмотря на то, что вы укажите до загрузки шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="3c500-140">For example, hello default **clusterKind** property value is always **hadoop**, despite what you specify before you download hello template.</span></span>



## <a name="deploy-with-powershell"></a><span data-ttu-id="3c500-141">Развертывание с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c500-141">Deploy with PowerShell</span></span>

<span data-ttu-id="3c500-142">В этой процедуре создается кластер Hadoop в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3c500-142">This procedure creates a Hadoop cluster in HDInsight.</span></span>

1. <span data-ttu-id="3c500-143">Сохраните файл JSON hello в hello [приложение](#appx-a-arm-template) tooyour рабочей станции.</span><span class="sxs-lookup"><span data-stu-id="3c500-143">Save hello JSON file in hello [Appendix](#appx-a-arm-template) tooyour workstation.</span></span> <span data-ttu-id="3c500-144">В hello сценарий PowerShell, имя файла hello — `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span><span class="sxs-lookup"><span data-stu-id="3c500-144">In hello PowerShell script, hello file name is `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span></span>
2. <span data-ttu-id="3c500-145">При необходимости создать hello параметров и переменных.</span><span class="sxs-lookup"><span data-stu-id="3c500-145">Set hello parameters and variables if needed.</span></span>
3. <span data-ttu-id="3c500-146">Выполните hello шаблона с помощью hello следующий сценарий PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3c500-146">Run hello template by using hello following PowerShell script:</span></span>

        ####################################
        # Set these variables
        ####################################
        #region - used for creating Azure service names
        $nameToken = "<Enter an Alias>"
        $templateFile = "C:\HDITutorials-ARM\hdinsight-arm-template.json"
        #endregion

        ####################################
        # Service names and variables
        ####################################
        #region - service names
        $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

        $resourceGroupName = $namePrefix + "rg"
        $hdinsightClusterName = $namePrefix + "hdi"
        $defaultStorageAccountName = $namePrefix + "store"
        $defaultBlobContainerName = $hdinsightClusterName

        $location = "East US 2"

        $armDeploymentName = $namePrefix
        #endregion

        ####################################
        # Connect tooAzure
        ####################################
        #region - Connect tooAzure subscription
        Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and hello dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    <span data-ttu-id="3c500-147">Сценарий PowerShell Hello настраивает только имени кластера hello.</span><span class="sxs-lookup"><span data-stu-id="3c500-147">hello PowerShell script configures only hello cluster name.</span></span> <span data-ttu-id="3c500-148">Имя учетной записи хранения Hello жестко закодирована в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="3c500-148">hello storage account name is hard-coded in hello template.</span></span> <span data-ttu-id="3c500-149">Все запрашиваемые tooenter hello кластера пользователя пароль.</span><span class="sxs-lookup"><span data-stu-id="3c500-149">You are prompted tooenter hello cluster user password.</span></span> <span data-ttu-id="3c500-150">(имя пользователя по умолчанию hello **администратора**.) Вы также являются пароль пользователя SSH запрашиваемые tooenter hello.</span><span class="sxs-lookup"><span data-stu-id="3c500-150">(hello default username is **admin**.) You are also prompted tooenter hello SSH user password.</span></span> <span data-ttu-id="3c500-151">(имя пользователя SSH по умолчанию hello **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="3c500-151">(hello default SSH username is **sshuser**.)</span></span>  

<span data-ttu-id="3c500-152">Дополнительные сведения см. в статье [Развертывание ресурсов с использованием шаблонов Resource Manager и Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="3c500-152">For more information, see  [Deploy with PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span>

## <a name="deploy-with-cli"></a><span data-ttu-id="3c500-153">Развертывание с помощью интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="3c500-153">Deploy with CLI</span></span>
<span data-ttu-id="3c500-154">Следующий образец Hello использует Azure командной строки (CLI).</span><span class="sxs-lookup"><span data-stu-id="3c500-154">hello following sample uses Azure command-line interface (CLI).</span></span> <span data-ttu-id="3c500-155">Он создает кластер и его учетную запись хранения и контейнер, вызывая шаблон Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3c500-155">It creates a cluster and its dependent storage account and container by calling a Resource Manager template:</span></span>

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

<span data-ttu-id="3c500-156">Запрос tooenter будут:</span><span class="sxs-lookup"><span data-stu-id="3c500-156">You are prompted tooenter:</span></span>
* <span data-ttu-id="3c500-157">Имя кластера Hello.</span><span class="sxs-lookup"><span data-stu-id="3c500-157">hello cluster name.</span></span>
* <span data-ttu-id="3c500-158">пароль пользователя кластера Hello.</span><span class="sxs-lookup"><span data-stu-id="3c500-158">hello cluster user password.</span></span> <span data-ttu-id="3c500-159">(имя пользователя по умолчанию hello **администратора**.)</span><span class="sxs-lookup"><span data-stu-id="3c500-159">(hello default username is **admin**.)</span></span>
* <span data-ttu-id="3c500-160">пароль пользователя для SSH Hello.</span><span class="sxs-lookup"><span data-stu-id="3c500-160">hello SSH user password.</span></span> <span data-ttu-id="3c500-161">(имя пользователя SSH по умолчанию hello **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="3c500-161">(hello default SSH username is **sshuser**.)</span></span>

<span data-ttu-id="3c500-162">После кода Hello предоставляет встроенные параметры:</span><span class="sxs-lookup"><span data-stu-id="3c500-162">hello following code provides inline parameters:</span></span>

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-hello-rest-api"></a><span data-ttu-id="3c500-163">Развертывание с помощью API-интерфейса REST hello</span><span class="sxs-lookup"><span data-stu-id="3c500-163">Deploy with hello REST API</span></span>
<span data-ttu-id="3c500-164">В разделе [развертывание с помощью API-интерфейса REST hello](../azure-resource-manager/resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="3c500-164">See [Deploy with hello REST API](../azure-resource-manager/resource-group-template-deploy-rest.md).</span></span>

## <a name="deploy-with-visual-studio"></a><span data-ttu-id="3c500-165">Развертывание с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3c500-165">Deploy with Visual Studio</span></span>
 <span data-ttu-id="3c500-166">Использовать Visual Studio toocreate проекта группы ресурсов и разверните его tooAzure через пользовательский интерфейс hello.</span><span class="sxs-lookup"><span data-stu-id="3c500-166">Use Visual Studio toocreate a resource group project and deploy it tooAzure through hello user interface.</span></span> <span data-ttu-id="3c500-167">Выберите тип hello tooinclude ресурсы в своем проекте.</span><span class="sxs-lookup"><span data-stu-id="3c500-167">You select hello type of resources tooinclude in your project.</span></span> <span data-ttu-id="3c500-168">Эти ресурсы будут автоматически добавлены toohello шаблона диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3c500-168">Those resources are automatically added toohello Resource Manager template.</span></span> <span data-ttu-id="3c500-169">проект Hello также предоставляет шаблон hello toodeploy скрипта PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3c500-169">hello project also provides a PowerShell script toodeploy hello template.</span></span>

<span data-ttu-id="3c500-170">Введение toousing Visual Studio с группами ресурсов. в разделе [Создание и развертывание группы ресурсов Azure с помощью Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="3c500-170">For an introduction toousing Visual Studio with resource groups, see [Creating and deploying Azure resource groups through Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="3c500-171">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="3c500-171">Troubleshoot</span></span>

<span data-ttu-id="3c500-172">Если при создании кластеров HDInsight возникли проблемы, см. раздел [Создание кластеров](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="3c500-172">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c500-173">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3c500-173">Next steps</span></span>
<span data-ttu-id="3c500-174">В этой статье было изучено несколько способов toocreate кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3c500-174">In this article, you have learned several ways toocreate an HDInsight cluster.</span></span> <span data-ttu-id="3c500-175">toolearn более, см. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="3c500-175">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="3c500-176">Пример развертывания ресурсов через клиентскую библиотеку .NET hello. в разделе [развертывания ресурсов с помощью библиотеки .NET и шаблона](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3c500-176">For an example of deploying resources through hello .NET client library, see [Deploy resources by using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="3c500-177">Подробный пример развертывания приложения см. в статье [Предсказуемые подготовка и развертывание микрослужб в Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span><span class="sxs-lookup"><span data-stu-id="3c500-177">For an in-depth example of deploying an application, see [Provision and deploy microservices predictably in Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span></span>
* <span data-ttu-id="3c500-178">Руководство по развертыванию решения toodifferent сред в разделе [сред разработки и тестирования в Microsoft Azure](../solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="3c500-178">For guidance on deploying your solution toodifferent environments, see [Development and test environments in Microsoft Azure](../solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="3c500-179">toolearn о разделах hello hello шаблона диспетчера ресурсов Azure, в разделе [разработки шаблонов](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3c500-179">toolearn about hello sections of hello Azure Resource Manager template, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="3c500-180">Список функций hello в шаблоне диспетчера ресурсов Azure можно использовать, см. [функции шаблона](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="3c500-180">For a list of hello functions you can use in an Azure Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md).</span></span>

## <a name="appendix-resource-manager-template-toocreate-a-hadoop-cluster"></a><span data-ttu-id="3c500-181">Приложение: Диспетчер ресурсов шаблона toocreate кластера Hadoop</span><span class="sxs-lookup"><span data-stu-id="3c500-181">Appendix: Resource Manager template toocreate a Hadoop cluster</span></span>
<span data-ttu-id="3c500-182">Hello следующий шаблон диспетчера ресурсов Azure создает кластер Hadoop под управлением Linux с учетной записью hello зависимых хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="3c500-182">hello following Azure Resource Manager template creates a Linux-based Hadoop cluster with hello dependent Azure storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="3c500-183">В этом примере содержатся сведения о конфигурации для хранилищ метаданных Hive и Oozie.</span><span class="sxs-lookup"><span data-stu-id="3c500-183">This sample includes configuration information for Hive metastore and Oozie metastore.</span></span> <span data-ttu-id="3c500-184">Удалить раздел hello или настраивать раздел hello перед использованием hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="3c500-184">Remove hello section or configure hello section before using hello template.</span></span>
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "hello name of hello HDInsight cluster toocreate."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used tooremotely access hello cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "location": {
        "type": "string",
        "defaultValue": "East US",
        "allowedValues": [
            "East US",
            "East US 2",
            "North Central US",
            "South Central US",
            "West US",
            "North Europe",
            "West Europe",
            "East Asia",
            "Southeast Asia",
            "Japan East",
            "Japan West",
            "Australia East",
            "Australia Southeast"
        ],
        "metadata": {
            "description": "hello location where all azure resources will be deployed."
        }
        },
        "clusterType": {
        "type": "string",
        "defaultValue": "hadoop",
        "allowedValues": [
            "hadoop",
            "hbase",
            "storm",
            "spark"
        ],
        "metadata": {
            "description": "hello type of hello HDInsight cluster toocreate."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "hello number of nodes in hello HDInsight cluster."
        }
        }
    },
    "variables": {
        "defaultApiVersion": "2015-05-01-preview",
        "clusterApiVersion": "2015-03-01-preview",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
        {
        "name": "[parameters('clusterName')]",
        "type": "Microsoft.HDInsight/clusters",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('clusterApiVersion')]",
        "dependsOn": [ "[concat('Microsoft.Storage/storageAccounts/',variables('clusterStorageAccountName'))]" ],
        "tags": {

        },
        "properties": {
            "clusterVersion": "3.4",
            "osType": "Linux",
            "tier": "standard",
            "clusterDefinition": {
            "kind": "[parameters('clusterType')]",
            "configurations": {
                "gateway": {
                "restAuthCredential.isEnabled": true,
                "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                },
                "hive-site": {
                    "javax.jdo.option.ConnectionDriverName": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "javax.jdo.option.ConnectionURL": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "javax.jdo.option.ConnectionUserName": "johndole",
                    "javax.jdo.option.ConnectionPassword": "myPassword$"
                },
                "hive-env": {
                    "hive_database": "Existing MSSQL Server database with SQL authentication",
                    "hive_database_name": "myhive20160901",
                    "hive_database_type": "mssql",
                    "hive_existing_mssql_server_database": "myhive20160901",
                    "hive_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "hive_hostname": "myadla0901dbserver.database.windows.net"
                },
                "oozie-site": {
                    "oozie.service.JPAService.jdbc.driver": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "oozie.service.JPAService.jdbc.url": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "oozie.service.JPAService.jdbc.username": "johndole",
                    "oozie.service.JPAService.jdbc.password": "myPassword$",
                    "oozie.db.schema.name": "oozie"
                },
                "oozie-env": {
                    "oozie_database": "Existing MSSQL Server database with SQL authentication",
                    "oozie_database_name": "myhive20160901",
                    "oozie_database_type": "mssql",
                    "oozie_existing_mssql_server_database": "myhive20160901",
                    "oozie_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "oozie_hostname": "myadla0901dbserver.database.windows.net"
                }            
            }
            },
            "storageProfile": {
            "storageaccounts": [
                {
                "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                "isDefault": true,
                "container": "[parameters('clusterName')]",
                "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                }
            ]
            },
            "computeProfile": {
            "roles": [
                {
                "name": "headnode",
                "targetInstanceCount": "2",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                },
                {
                "name": "workernode",
                "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                }
            ]
            }
        }
        }
    ],
    "outputs": {
        "cluster": {
        "type": "object",
        "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
        }
    }
    }

## <a name="appendix-resource-manager-template-toocreate-a-spark-cluster"></a><span data-ttu-id="3c500-185">Приложение: Диспетчер ресурсов шаблона toocreate кластера Spark</span><span class="sxs-lookup"><span data-stu-id="3c500-185">Appendix: Resource Manager template toocreate a Spark cluster</span></span>

<span data-ttu-id="3c500-186">Этот раздел содержит шаблона диспетчера ресурсов, которые можно использовать toocreate кластер HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="3c500-186">This section provides a Resource Manager template that you can use toocreate an HDInsight Spark cluster.</span></span> <span data-ttu-id="3c500-187">Этот шаблон содержит настройки для `spark-defaults` и `spark-thrift-sparkconf` (для кластеров Spark 1.6), а также для `spark2-defaults` и `spark2-thrift-sparkconf` (для кластеров Spark 2).</span><span class="sxs-lookup"><span data-stu-id="3c500-187">This template includes configurations for `spark-defaults` and `spark-thrift-sparkconf` (for Spark 1.6 clusters) and `spark2-defaults` and `spark2-thrift-sparkconf` (for Spark 2 clusters).</span></span> <span data-ttu-id="3c500-188">В дополнение к этому toothis, HDInsight вычисляет и задает конфигурации, такие как `spark.executor.instances`, `spark.executor.memory`, и `spark.executor.cores` на основе размера кластера hello.</span><span class="sxs-lookup"><span data-stu-id="3c500-188">In addition toothis, HDInsight calculates and sets configurations such as `spark.executor.instances`, `spark.executor.memory`, and `spark.executor.cores` based on hello cluster size.</span></span> 

<span data-ttu-id="3c500-189">При выборе любой из параметров в разделе как часть самого шаблона hello HDInsight не вычисления и задать другие параметры hello hello один раздел.</span><span class="sxs-lookup"><span data-stu-id="3c500-189">If you set any one parameter in a section as part of hello template itself, HDInsight does not calculate and set hello other parameters of hello same section.</span></span> <span data-ttu-id="3c500-190">Например, параметр `spark.executor.instances` в hello `spark-defaults` конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3c500-190">For example, parameter `spark.executor.instances` is in hello  `spark-defaults` configuration.</span></span> <span data-ttu-id="3c500-191">Если в качестве параметра другой (например, `spark.yarn.exector.memoryOverhead`) в hello `spark-defaults` конфигурации, HDInsight не вычисления и установите hello `spark.executor.instances` также.</span><span class="sxs-lookup"><span data-stu-id="3c500-191">If you set another parameter (for example, `spark.yarn.exector.memoryOverhead`) in hello `spark-defaults` configuration, HDInsight does not calculate and set hello `spark.executor.instances` parameter as well.</span></span>

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "hello name of hello HDInsight cluster toocreate."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "hello location where all azure resources will be deployed."
            }
        },
        "clusterVersion": {
            "type": "string",
            "defaultValue": "3.5",
            "metadata": {
                "description": "HDInsight cluster version."
            }
        },
        "clusterWorkerNodeCount": {
            "type": "int",
            "defaultValue": 4,
            "metadata": {
                "description": "hello number of nodes in hello HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "hello type of hello HDInsight cluster toocreate."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used tooremotely access hello cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        }
    },
    "variables": {
        "defaultApiVersion": "2017-06-01",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
    {
            "apiVersion": "2015-03-01-preview",
            "name": "[parameters('clusterName')]",
            "type": "Microsoft.HDInsight/clusters",
            "location": "[parameters('location')]",
            "dependsOn": [],
            "properties": {
                "clusterVersion": "[parameters('clusterVersion')]",
                "osType": "Linux",
                "tier": "standard",
                "clusterDefinition": {
                    "kind": "[parameters('clusterKind')]",
                    "configurations": {
                        "gateway": {
                            "restAuthCredential.isEnabled": true,
                            "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                            "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                        },
                        "spark-defaults": {
                            "spark.executor.cores": "2"
                        },
                        "spark-thrift-sparkconf": {
                            "spark.yarn.executor.memoryOverhead": "896"
                        }
                    }
                },
                "storageProfile": {
                    "storageaccounts": [
                        {
                            "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                            "isDefault": true,
                            "container": "[parameters('clusterName')]",
                            "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                        }
                    ]
                },
                "computeProfile": {
                    "roles": [
                        {
                            "name": "headnode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 2,
                            "hardwareProfile": {
                                "vmSize": "Standard_D12"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                }
                            },
                            "virtualNetworkProfile": null,
                            "scriptActions": []
                        },
                        {
                            "name": "workernode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 4,
                            "hardwareProfile": {
                                "vmSize": "Standard_D4"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                    }
                                },
                                "virtualNetworkProfile": null,
                                "scriptActions": []
                            }
                        ]
                    }
                }
            }
        ]
    }
